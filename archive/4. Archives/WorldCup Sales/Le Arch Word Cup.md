

Seat layout
- getShowinfo
	- left side
	- de call
- getlayoutdrawing
	- 2calls full and area category wise
	- 30mins cache
	- 15mins cached on redis
- getSeatLayout
	- IS call
	- to be called with getShowinfo

ticket options 
- book api
- getBookmingInfoex

concurrency 
- bts redis


HaProxy queueing for book button
nm-api
le-api



numbers???
single point of failures??


le nmcms queueuing

split 
	only for one api


mongo
	pss

redis

master slave 3nodes


ceiling limit


More Questions
- Circuit breaking for getUserTicketLock?
- What are the implications of showing static data for LE Apis?
- timeout values of 10sec seems higher
- which mongo db to make pss?
- caching for getShowinfo on saet layout page?
- Do you pass x-client-workflow header for all IS call?

Action Items
ToDo
- [x] Load Test to get the per pod capacity @completed(2024-01-01T15:44:38)
- [x] CF caching for getevent @completed(2024-01-01T15:44:58)

Verify
-  Verify caching is happening for the LE Synopsis page
-  Verify circuit breaking is working properly for LE apis
- Circuit breaking for non critical apis on LE apis
-  max connection 10000 should be reduced after the load test
- le api and nmcms queueing
-  consider retries while doing chaos tests

Infra 
NMCMS MDB pss
	2core 8gb
	conection limit 4000
NMCMS Redis
	max connection 10000 should be reduced after the load test
	1 core 8gb 

BTS mongo
	4core 32gb
	pss
	conn limit 10000
BTS redis
	1core 8gb
	connecion 10000

