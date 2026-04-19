---
kindle-highlights: 
name: Untitled 6
tags: 
date: 2024-06-08
---
# Main Takeaways

Chapter 1: Scale from zero to millions
- https://www.usenix.org/system/files/conference/nsdi13/nsdi13-final170_update.pdf
- Read how to cache dynamic content
- While sharding db the sharding key is the most important factor
	- Resharding data
	- Celebrity Problem
	- Join and de-normalize
	- 
Chapter 4: Build a rate limimter
- There are different algo that can be used to make a rate limiter
- Bucket
	- Each user has a bucket and for every action the counter in the bucket is reduced
	- the bucket will have to be refilled
- Leaky Bucket
	- Its similar to previous
	- Its imp0lemented with a FIFO queue
	- If the queue is full the messages are dropped
	- 
- Fixed Window
	- Here time is divided into slices and a count is maitnained for each time slice
	- If the count reaches the threshold we drop the requests
	
- Counter Sliding Window
	- Here we use a formula to check 
	- If we are checking the count at 30% of the current time window the formula would be
		- 0.70 * previos time window + current timewindow count
		- This assumes that the requests have come in evenly
- Log Sliding Window
	- Here the also keeps track of the timestamp 
	- For a new requests all the logs prior to the window are deleted
	- new entry is added
	- count is taken to check if it is within the threshold

# Didn't agree with

# What can be applied from this book?