---
tags:
  - basics
---

## Basics
- Global Storage Platform - regional based/resilient. During creating an S3 instance, you do not have to select a region, only when you create  things inside an S3 you have to select a region.
- Public service, it runs from the AWS Public zone, unlimited data & multi-user usage. Millions of users can access.
- Perfect for hosting data like audio, video, lard data sets.
- Economical & accessed VIA ui/cli/api/http
- It contains data in form of Objects & Buckets.

Is S3 a regional service?
?
False.
S3 itself is not a regional service but the things inside S3 are region specific.
<!--SR:!2024-08-29,13,230-->

What is the data structure format of an S3?::Objects and Buckets
<!--SR:!2024-09-01,16,210-->
### Objects
- We can think of them like files and conceptually most of the time they are interchangeable.
- An object has a key and value.
- If you know the object key and bucket then you can access the object value.
- **Remember, by default, even for public services, there is no access in AWS initially, you have to set it up.**
- An object could be from 0 bytes to 5TB.
- Objects also have Version ID, Metadata, Access Control, Sub resources.
What is the size range of an object in s2?::0 to 5 TB.
<!--SR:!2024-08-22,6,230-->
### Buckets
- Created inside a **specific AWS region**.
- Data never leaves that region unless configured to, this ensures **data sovereignty**.
- Blast Radius is a region.
- Bucket name is **Globally Unique**, no one can use duplicate bucket names through out the world.
- Buckets can **hold unlimited number of objects** and an object could be of 0 bytes to 5TB, this makes S3 and **infinitely scalable system**.
- S3 is a **flat structure, it is not a complex structure**. All objects in a buckets are stored in the same level. It is **not like a file system**. Everything is stored in the buckets at **the same level**.
- Even the UI displays folder like structure inside S3 but it should be notes that S3 is a flat structure.
- Objects are sometimes represented in a way that it looks folder like structure , e.g /old/pic.jpeg , but in reality is just a key that maps to a value and this is useful to accommodate data for different clients in a single S3 bucket.

![[s3_imp_things.png]]

## S3 Patterns and Anti-Patterns

![[s3_patterns.png]]

S3 is ==an object== store.
<!--SR:!2024-08-29,13,230-->

What is the soft and hard limit for the number of S3 buckets per AWS account::100 and 1000.
<!--SR:!2024-08-18,2,210-->

Can you have unlimited number of objects inside a bucket?::True, where each object size ranges from 0 bytes to 5TB.
<!--SR:!2024-08-22,6,230-->


Is S2 public or private by default?::S3 by default, is a private service, only the account root has access to S3 when it is created.