
Requirements
- Where to store the req and response of external APIs like JUSTPAY?
- What should be the retention policy?
- The data will be used for searching for debugging purposes.
Questions
- Will we need each and every event?
	- Each and Every requests is required.
- What is the approx size of the data?
	  - 
- Does it have PCI data?
	- This data will be there. Payment Id or trans id would be enough to get the data.
- How frequent will the data be accessed?
	  - Data will be used to debug and deep dive SR realted changes. 
	    once in a week.
Discussions
- Response is already maintained in the databases
- Use and event store, so the idea is that events would be logged using the existing logging libs and fluentd would scan and store it in some dbs.
- Check how it can be used at the org level?

Research
- [[Logging VS Distributed Tracing]]


