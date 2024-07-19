---
tags:
  - basics
---
What is the difference bewteen these 2 ARNs, \`arn:aws:s3:::catgifs`, `arn:aws:s3:::catgifs/*`
?
The first one specifies the bucket catgifs, no access will be given to objects inside.
The second ARN refers to the objects inside the buck but not the bucket itself.