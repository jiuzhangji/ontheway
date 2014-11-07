Design Feed System
==================

#Major Functions on Feed System
1. get post list for userId
2. get time-line for userId
extra: support like, comment, repost, time rage search, pagination

#There 5 problems have to solve.
1. Data model, how to store the data model, and how to query them.
2. How design the algorithm to achieve the major function-- time line, and give quantitative analyse of different algorithms on your data model
3. how scale up your systems? 
4. the system architecture --- 4 tier system, everybody knows...
5. some details for the storage 
   Do not tell what DB you want to use, because your system can be done by using any storage technology!!!
   if the interviewer want to know whether you are familiar with DB technology.


#Data models
1. event stream
I don't know how to do with this model. 

2. relation data
create tables to store user and post relations, and make simple SQL query on them.
not easy to make extensions, and not easy to scale up the system.
BUT, we can learn the data relations between those Entities. we can easy to know the relation ships between them (E-R graph) 

3. graph
take every Entities(Users, Posts, Likes, Comments, Reposts ... etc.) as a general Object Node in a Graph.
and the actions (one way friend(follow)/bidirectional friend , create a post, like a post, comment a post, make a repost) be the edges in the Graph.

how graph works----- 2nd degree query.
user->friends->friend's posts
     1 degree    2 degree
user->post list->like count for each post
     1 degree    2 degree
user->friends->friend's chat history

.....


#Algorithms for query 2nd degree relations from graph
there 2 ways: pull and push.
pull(out-box): all posts are stored in the graph, we can retrieve the relations by 2 steps:
             1. fetch friend list
             2. batch get posts for each friend user	
    out-box: means, I put my posts in my out-box(in the graph), and wait my friends to get them.

push(in-box): besides store the objects in the graph, we also store my friends in my "in-box"
             1. user create a post, store it to the graph
             2. fetch friend list
			 3. batch write to my friend's in-boxes.
			 
	in-box: like a mail box, if any updates from friends, it will store in it, if you want to read, just read from your in-box.
	
Compare those two methods
suppose we have:
	U number users
	F1 as average follower number for each user
	F2 as average followee number for each user
	P as the average post number per day in your system.
	UP as the average post number for each user.   UP = P/U
	V as the average PageView number per day in your system (get time-line)

	
what to compare? -- the whole systems READ and WRITE numbers (or number, it's the same) 
					Pull		Push
create a post(W)	P			P*F1
get time line(R)	V*(1+F2)	V

For implementation, Push model have to maintenance the in-box, so "more work" for the special component.
in-box provided some tolerance,
we can partition in-box, some in-box down, it won't affect other in-boxes(assume that we partition the in-boxes by user-id), and of course won't affect post write.
out-box can not do this.
if one partition down, the whole feed system down, you can not read, and can not write.(of source if you want, you may also do some duplication for it to avoid this problem)

If F2 is large push is not so good way (big VIP)
for topical system constrain, we will limit the max followee number. so F2 won't be so large, so pull will works well if V is no large.
If V is very large, we have to use push model. and should use special resource to process Write problem for VIP.

For bidirectional friends system (Facebook, WeChat, IM system)
F1=F2, and won't be so large, both pull and push works well.

Here I want to make some clarification about the response time:
both pull and push can be fast to send notification to users.
it depends on the strategies that how often to make notification to let user know that you have new feeds.
once user got the notification, he can refresh it's time-line by pull, or read from push, that's OK.

#How scale up your systems? 
That's easy, you must divide your system to many components
each components provide it's interface independently, 
we can call it meta-data interfaces, and we can not divide it be smaller.
so they do not have any relation to each others.(Orthogonal)
that means your system become liner scalable.

##For our feed system read:
meta-data interfaces: getFriendListByUserId, batchGetPostListByUserId(pull model), getTimeLineFromInBoxByUserId(push model)
external interfaces: getTimeLineByUserId 
1 getTimeLineByUserId call = 1 getFriendListByUserId call + 1 batchGetPostListByUserId call  (pull model)
1 getTimeLineByUserId call = 1 getTimeLineFromInBoxByUserId call  (push model)

getFriendList is scalable, your address-book system will take the responsibility for it's scalability. 
getPostListByUserId is scalable, your post system will take the responsibility for it's scalability.
getTimeLineFromInBox is scalable too...


##For our feed system write:
meta-data interfaces: writePostByUserId(all model), batchAppendPostToInBoxByUserId(push model)
external interfaces: createPostByUserId

1 createPostByUserId = 1 writePostByUserId 										(pull model)
1 createPostByUserId = 1 writePostByUserId + 1 batchAppendPostToInBoxByUserId	(push model)

batchAppendPostToInBoxByUserId is scalable, because we can partition it by userId.
writePostByUserId is scalable, because we can partition it by time, and in each time range we can do partition by userId if we want.




	 

