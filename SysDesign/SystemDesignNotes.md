
class note of [hiredintech](http://www.hiredintech.com/system-design/the-system-design-process/)

Design a URL shorten services

##Step 1: Constraints and use cases  
  
User Case
-----------------------

1.Shortening: take a url=>return a much shorter url  
2. Redirection: take a shrot url=> redirect to the original url  
3.Custom url  
4.High availability of the system.  

out of scope:  
5.Analytics  
6.Automatic link expiration  
7.Manual link removal  
8.UI vs API  


Constraints
-----------------------
1. Amount of traffic?   
2. Amount of Data ? Per month? Per-second?   


well-known facts:  
1. Facebook active users=1.71 billion(10^9) monthly user  
2.  wechat 700 million (10^6)   

*Exp.*   
1.  Twitter 350 million, 15 billion tweets/month ==> 1.5 Billion shorten URL.  
Sites below the Top3: shorten 300M per month.    
==> 100M/month we handle.

2. 1BN requests Per Month.
3. 10% from shortening and 90% from redirection. 
4. Requests per second: 400+ (40 shortens+ 360 redirects)  
5. 6BN URLs in 5 years.
6. 500 bytes per URL  
7. 6 bytes per hash
8. **3TB for all urls, 36GB for all hashes (over 5 years)**  
9. **New data written per second: 40*(500+6)=20k**  
10. **Data read per second=360*506 bytes=180k**  
 
##Step 2: Abstract design
Once you've scoped the system you're about to design, you should continue by outlining a high-level abstract design.     
You can tell the interviewer that you would like to do that and draw a simple diagram of your ideas. Sketch your main components and the connections between them. If you do this, very quickly you will be able to get feedback if you are moving in the right direction. Of course, you must be able to justify the high-level design that you just drew.  

1. Application Service layer (server the request)    
    - shortening service  
    - Redirection service

2.Data Storage Layer  
    - Acts like a hash table KV table.   

Hashed_url = convert_to_base62(md5(original_url+random_salt))[:6]  


