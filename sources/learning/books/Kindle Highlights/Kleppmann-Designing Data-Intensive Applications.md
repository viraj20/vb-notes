---
kindle-sync:
  bookId: '21757'
  title: >-
    Designing Data-Intensive Applications: The Big Ideas Behind Reliable,
    Scalable, and Maintainable Systems
  author: Martin Kleppmann
  asin: B06XPJML5D
  lastAnnotatedDate: '2023-04-06'
  bookImageUrl: 'https://m.media-amazon.com/images/I/91YfNb49PLL._SY160.jpg'
  highlightsCount: 44
captured: 2023-06-09
captured_via: kindle
wiki_compiled: true
---
# Designing Data-Intensive Applications
## Metadata
* Author: [Martin Kleppmann](https://www.amazon.comundefined)
* ASIN: B06XPJML5D
* Reference: https://www.amazon.com/dp/B06XPJML5D
* [Kindle link](kindle://book?action=open&asin=B06XPJML5D)

## Highlights
book, you can look up references using a search engine. For academic papers, you can search for the title in Google Scholar to find open-access PDF files. Alternatively, you can find all of the references at https://github.com/ept/ddia-references, where we maintain up-to-date links. — location: [103](kindle://book?action=open&asin=B06XPJML5D&location=103) ^ref-38809

---
amount of data, the complexity of data, and the speed at which it is changing. — location: [207](kindle://book?action=open&asin=B06XPJML5D&location=207) ^ref-29895

---
The boundaries between the categories are becoming blurred. — location: [238](kindle://book?action=open&asin=B06XPJML5D&location=238) ^ref-52558

---
How do you ensure that the data remains correct and complete, even when things go wrong internally? How do you provide consistently good performance to clients, even when parts of your system are degraded? How do you scale to handle an increase in load? What does a good API for the service look like? — location: [255](kindle://book?action=open&asin=B06XPJML5D&location=255) ^ref-63337

---
continuing to work correctly, even when things go wrong.” — location: [284](kindle://book?action=open&asin=B06XPJML5D&location=284) ^ref-41243

---
A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. It is impossible to reduce the probability of a fault to zero; therefore it is usually best to design fault-tolerance mechanisms that prevent faults from causing failures. — location: [294](kindle://book?action=open&asin=B06XPJML5D&location=294) ^ref-28047

---
it is revealed that the software is making some kind of assumption about its environment—and while that assumption is usually true, it eventually stops being true for some reason [11]. — location: [367](kindle://book?action=open&asin=B06XPJML5D&location=367) ^ref-19013

---
Scalability is the term we use to describe a system’s ability to cope with increased load. — location: [420](kindle://book?action=open&asin=B06XPJML5D&location=420) ^ref-31449

---
The best choice of parameters depends on the architecture of your system: it may be requests per second to a web server, the ratio of reads to writes in a database, the number of simultaneously active users in a chat room, the hit rate on a cache, or something else. Perhaps the average case is what matters for you, or perhaps your bottleneck is dominated by a small number of extreme cases. — location: [428](kindle://book?action=open&asin=B06XPJML5D&location=428) ^ref-58283

---
company switched to approach 2. This works better because the average rate of published tweets is almost two orders of magnitude lower than the rate of home timeline reads, and so in this case it’s preferable to do more work at write time and less at read time. — location: [464](kindle://book?action=open&asin=B06XPJML5D&location=464) ^ref-28375

---
even though it only affects 1 in 1,000 requests. This is because the customers with the slowest requests are often those who have the most data on their accounts because they have made many purchases—that is, they’re the most valuable customers [19]. — location: [537](kindle://book?action=open&asin=B06XPJML5D&location=537) ^ref-14433

---
head-of-line blocking. — location: [559](kindle://book?action=open&asin=B06XPJML5D&location=559) ^ref-19208

---
tail latency amplification [24]). — location: [573](kindle://book?action=open&asin=B06XPJML5D&location=573) ^ref-14042

---
Distributing load across multiple machines is also known as a shared-nothing architecture. — location: [605](kindle://book?action=open&asin=B06XPJML5D&location=605) ^ref-45106

---
For this reason, common wisdom until recently was to keep your database on a single node (scale up) until scaling cost or high-availability requirements forced you to make it distributed. — location: [615](kindle://book?action=open&asin=B06XPJML5D&location=615) ^ref-22867

---
An architecture that scales well for a particular application is built around assumptions of which operations will be common and which will be rare—the load parameters. — location: [626](kindle://book?action=open&asin=B06XPJML5D&location=626) ^ref-44204

---
Operability Make it easy for operations teams to keep the system running smoothly. Simplicity Make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. (Note this is not the same as simplicity of the user interface.) Evolvability Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity. — location: [644](kindle://book?action=open&asin=B06XPJML5D&location=644) ^ref-35524

---
“good operations can often work around the limitations of bad (or incomplete) software, but good software cannot run reliably with bad operations” [12]. — location: [654](kindle://book?action=open&asin=B06XPJML5D&location=654) ^ref-6749

---
symptoms of complexity: explosion of the state space, tight coupling of modules, tangled dependencies, inconsistent naming and terminology, hacks aimed at solving performance problems, special-casing to work around issues elsewhere, and many more. — location: [685](kindle://book?action=open&asin=B06XPJML5D&location=685) ^ref-15807

---
Moseley and Marks [32] define complexity as accidental if it is not inherent in the problem that the software solves (as seen by the users) but arises only from the implementation. — location: [696](kindle://book?action=open&asin=B06XPJML5D&location=696) ^ref-9461

---

each layer hides the complexity of the layers below it by providing a clean data model. These abstractions allow different groups of people—for example, the engineers at the database vendor and the application developers using their database—to work together effectively. — location: [882](kindle://book?action=open&asin=B06XPJML5D&location=882) ^ref-41143

---
impedance mismatch.i — location: [944](kindle://book?action=open&asin=B06XPJML5D&location=944) ^ref-57786

---
Object-relational mapping (ORM) — location: [948](kindle://book?action=open&asin=B06XPJML5D&location=948) ^ref-18853

---
one-to-many relationships from the user profile to the user’s positions, educational history, and contact information imply a tree structure in the data, — location: [1028](kindle://book?action=open&asin=B06XPJML5D&location=1028) ^ref-23861

---
Anything that is meaningful to humans may need to change sometime in the future—and if that information is duplicated, all the redundant copies need to be updated. — location: [1051](kindle://book?action=open&asin=B06XPJML5D&location=1051) ^ref-31958

---
Removing such duplication is the key idea behind normalization in databases.ii — location: [1053](kindle://book?action=open&asin=B06XPJML5D&location=1053) ^ref-40572

---
If the database itself does not support joins, you have to emulate a join in application code by making multiple queries to the database. — location: [1068](kindle://book?action=open&asin=B06XPJML5D&location=1068) ^ref-37745

---
The main arguments in favor of the document data model are schema flexibility, better performance due to locality, and that for some applications it is closer to the data structures used by the application. The relational model counters by providing better support for joins, and many-to-one and many-to-many relationships. Which data model leads to simpler application code? — location: [1169](kindle://book?action=open&asin=B06XPJML5D&location=1169) ^ref-14930

---
However, if your application does use many-to-many relationships, the document model becomes less appealing. — location: [1187](kindle://book?action=open&asin=B06XPJML5D&location=1187) ^ref-56987

---
Schema flexibility in the document model — location: [1195](kindle://book?action=open&asin=B06XPJML5D&location=1195) ^ref-34125

---
schema-on-read — location: [1205](kindle://book?action=open&asin=B06XPJML5D&location=1205) ^ref-24137

---
schema-on-write — location: [1206](kindle://book?action=open&asin=B06XPJML5D&location=1206) ^ref-37592

---
MySQL is a notable exception—it copies the entire table on ALTER TABLE, which can mean minutes or even hours of downtime when altering a large table—although — location: [1244](kindle://book?action=open&asin=B06XPJML5D&location=1244) ^ref-47496

---
There are many different types of objects, and it is not practicable to put each type of object in its own table. The structure of the data is determined by external systems over which you have no control and which may change at any time. — location: [1254](kindle://book?action=open&asin=B06XPJML5D&location=1254) ^ref-62917

---
Data locality for queries — location: [1260](kindle://book?action=open&asin=B06XPJML5D&location=1260) ^ref-31145

---
you want—what conditions the results must meet, and how you want the data to be transformed (e.g., sorted, grouped, and aggregated)—but not how to achieve that goal. It is up to the database system’s query optimizer to decide which indexes and which join methods to use, and in which order to execute various parts of the query. — location: [1357](kindle://book?action=open&asin=B06XPJML5D&location=1357) ^ref-35953

---
The fact that SQL is more limited in functionality gives the database much more room for automatic optimizations. — location: [1366](kindle://book?action=open&asin=B06XPJML5D&location=1366) ^ref-29832

---
MapReduce is neither a declarative query language nor a fully imperative query API, but somewhere in between: the logic of the query is expressed with snippets of code, which are called repeatedly by the processing framework. It is based on the map (also known as collect) and reduce (also known as fold or inject) functions that exist in many functional programming languages. — location: [1478](kindle://book?action=open&asin=B06XPJML5D&location=1478) ^ref-24001

---
property graph model — location: [1648](kindle://book?action=open&asin=B06XPJML5D&location=1648) ^ref-26095

---
Example 2-5. The same query as Example 2-4, written in SQL using recursive common table expressions — location: [1790](kindle://book?action=open&asin=B06XPJML5D&location=1790) ^ref-58135

---
there is a big difference between storage engines that are optimized for transactional workloads and those that are optimized for analytics. — location: [2351](kindle://book?action=open&asin=B06XPJML5D&location=2351) ^ref-56493

---
Maintaining additional structures incurs overhead, especially on writes. For writes, it’s hard to beat the performance of simply appending to a file, because that’s the simplest possible write operation. — location: [2403](kindle://book?action=open&asin=B06XPJML5D&location=2403) ^ref-45943

---
Any kind of index usually slows down writes, because the index also needs to be updated every time data is written. — location: [2404](kindle://book?action=open&asin=B06XPJML5D&location=2404) ^ref-3673

---
well-chosen indexes speed up read queries, but every index slows down writes. — location: [2405](kindle://book?action=open&asin=B06XPJML5D&location=2405) ^ref-1747

---
