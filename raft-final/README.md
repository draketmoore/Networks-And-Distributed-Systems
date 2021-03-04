For our milestone, we implemented the first 5 steps from the project page. This was basically implementing get() and put() requests that get/put data into the kv store without replicating it across the datastores. Additionally, there was a log to keep track of past transactions 

Then we had to implement the parts of the raft election protocol, which included election and reelection and sending heartbeats in intervals. We had new message types that included one for starting an election, responding ok to a vote, and heartbeats. To ensure elections, we needed to implement the election timeout in which each replica has to check if the leader has failed and keeps track of the candidacy. Getting a vote response will not allow a replica to vote once again. 

Essentially we had to implement the rest of the steps described in the project specs, steps 6-11. 

A difficult part of this assignment was getting the partition to work since the conditions were quite specific. Additionally, the main challenge was implementing raft basically from scratch made it hard to get a baseline going since there was so much to keep track of. 
