---
date: 2024-01-24
name: Fault Tolerance across BMS
---

Date:  2024-01-24
Attendees: [[Ralstan Vaz]] [[Lalit Mevani]] [[Mahesh Kadam]]
---

# Agenda
1. 
# Discussion notes
- We want to create a single fault tolerance mechanism for the entire BookMyShow website
- Want to achieve using cloudflare key value features
- So what we can do is cache all the pages in KV store of CF
- There would be a fetcher worker that would serve the page from the KV store
- A scheduler would run that would cache the pages to the KV Store
- There should be a way to enable the caching only for one of the page types
- page type would be different type of pages like homepage would be apage type that would include all the endpoints for homepages
- We also need to support different key generation. 1:1 and many:1
- many:1 is like all the endpoints would be mapped to a single key in the KV store
- The idea is to make the logic as generic as possible so in the future adding any new page would be as simple as adding a config.
- 
# Questions??
- 
# Action items
- [ ] #ToDo Read more about hashing functions ➕ 2024-01-24
- [ ] 


