# **Caching**

Every time we start an application, We load data and resource files from storage. It happens every single time that it slows down our application. So to make it faster and smoother, we use a technique called CACHING.

# How does it work

Caches are temporary files that contain various kinds of data and resources related to an application. Cache files may be more frequently or more recently used data. They are stored in fast access memories such as RAM (random access memory), Optane memory, or sometimes in hard drives.

# Cache Creation

<p>Various approaches that we can use to create caches.</p>

## Cache aside

<p>  In this type, cache and database are independent of each other and comes in contact.

When a user has requested for some data, Server or Application first search that dataset in the cache memory if found then it returns the data otherwise it searches in the database and retrieves the dataset to the user as well as alongside it writes that dataset into the cache memory. </p>

![Cache](/img/Cacheaside.png?raw=true)

### Pro's

* If cache goes down, application and database remain unaffected.
* It protects the system from going down.
* cache model and database model can be different.

### Con's

* If cache goes down, it slows the system
* It is difficult to update cache memory.

## Read through cache

Server or application never contacts the database directly. Cache memory lies between system and database. So when the first request comes in, it performs a [cache miss](https://hazelcast.com/glossary/cache-miss/) that fetches data from the database and populates the cache memory for later requests 

![Cache](/img/Readthrough.png?raw=true)

## Write through cache

<p> It is quite similar to the "read through cache". When application adds new data to the database, it first writes that data to the cache memory and then the cache will write the data into the database.</p>

![Cache](/img/writethrough.png?raw=true)

**_NOTE_**

"Read through cache" and "write Through cache" are mainly used together. The data model of the database and caches must be similar. Cache memory is responsible for writing data to the database and fetching data from the database. So if cache goes down the whole system goes down.

## Write around cache

<p> This technique writes data directly to the database but read data from the cache memory.</p>

![Cache](/img/writearound.png?raw=true)

### Pro's

* It reduces the latency.
* Best use for bulk data write requests.

### Con's

* If cache goes down, system goes down.
* Requires same data modeling.

## Write back cache
<p> In this case cache waits and collects multiple write request from the application and then write them all together to the database</p> 

![Cache](/img/writeback.png?raw=true)

### Pro's

* Best for handling bulk write requests
* If the database goes down, the cache can protect the write requests and process them later on when the database is up and running.

### Con's

* If cache goes down, whole system goes down.

# Cache Invalidation/Lifespan
<p> Cache invalidation is one of the most difficult  PRoblem. But it plays a major role. Choose lifespan/lifecycle of cache is complex.</p>

## Cache with TTL (time to live)
<p> We set a time limit on the cache to refresh and maintain itself. From time to time server clears the cache and updates the cache with new data. It happens regularly and moslty used for the servers that frequently update their data. </p>

## Cache without TTL
<p> This is mainly used in applications that use more static data and do not require frequent changes. Updation of cache memory happens occasionally </p>

# Maintainance

We use different algorithms to maintain the cache memory.

* Least Frequently Used (LFU):- It keeps track of the data usage and least used dataset gets deleted.

* Least Recently Used (LRU):- It prioritize the recently used data and when cache memory is full it deletes the least reacently used data.

* Most Recently Used (MRU):- It removes the recently used data and prioritize the old data.

# Conclusion

<p> Cache are very important to scale an application as well as make it faster. But we need to be very carefull on how we implement our caches. Caches may take some memory which is expensive but they are worth it. </p>
