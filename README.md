# LinkedIn Architecture

Do you wonder how LinkedIn scaled to 930 million users?

This post outlines how LinkedIn evolved its software architecture over time. I will walk you through their architectural evolution in 11 stages. Each stage shows how they changed the architecture to meet increasing scalability needs.

If you want to learn more, scroll to the bottom and find the references. Also, consider sharing this post with someone who wants to study system design.

## Scalable Software Architecture

LinkedIn started with 2,700 users in 2003 and now has around 930 million users. Here is the chronological order of their evolutionary stages:

### 1. The Monolith

They installed a single monolith application and a few databases to do all the work.

### 2. Graph Service

As the number of users grew, they wanted to manage connections between users in an efficient way.

So they created a separate in-memory graph service and communicated with it via RPC.

### 3. Scaling Database

The database became a performance bottleneck. As a workaround, they scaled it vertically by adding CPU and memory. But soon it hit limitations and became expensive.

So they installed (replica) follower databases to scale further. It served reads.

But this solution worked only for the medium term because it didn’t scale the writes. So they partitioned the database to scale writes.

### 4. Service-Oriented Architecture

They needed high availability but it was hard for the app server to keep up with high traffic.

So they broke the monolith into many small stateless services:
- **Frontend service** - presentation logic
- **Mid-tier service** - API access to data models
- **Backend data service** - access to the database

They kept the services stateless because it is easy to scale out by replication. Besides, they did load testing and performance monitoring.

LinkedIn had 750 services in 2015.

### 5. Caching

Caching was the right choice for them to meet scalability needs with hypergrowth.

Also, they relied on CDN and browser cache.

Besides, they stored precomputed results in the database.

### 6. Birth of Kafka

They needed data to flow into the data warehouse and Hadoop for analytics. So they created Kafka to stream and queue data.

Kafka is a distributed pub-sub messaging platform.

### 7. Scaling Engineering Teams

They put the entire focus on improving tooling, deployment, infrastructure, and developer productivity. And paused feature development.

It improved their engineering agility to build scalable products.

### 8. Birth of Rest.li Framework

They wanted to decouple services, so they switched to RESTful API and sent JSON over HTTP.

And built the Rest.li web framework to abstract many parts of data exchange.

### 9. Super Blocks

Service-oriented architecture caused many downstream calls and it became a problem. So they grouped the backend services to create a single access API.

### 10. Multi Data Center

They needed high availability and wanted to avoid single points of failure.

So they replicated data across many data centers. And redirected user requests to nearby data centers.

### 11. Ditch JSON

JSON data serialization became a performance bottleneck. So they moved from JSON to Protobuf to reduce latency.

## References



![image](https://github.com/Dhanshree0802/linkedin_architecture/assets/98329064/d9171e9c-00cf-4b14-9d1d-ce77a9df0aa9)

![image](https://github.com/Dhanshree0802/linkedin_architecture/assets/98329064/190765a4-c0be-41c1-b081-6674c234bf51)



![image](https://github.com/Dhanshree0802/linkedin_architecture/assets/98329064/899c80ab-3e7c-47e8-bced-f29b324fcf6a)

![image](https://github.com/Dhanshree0802/linkedin_architecture/assets/98329064/4dbdf8c3-d806-4137-8834-3e0de11353d6)

