## 6077 Mail Discussion
A summary of the points in the 6077 mail discussion, will rename later.

## RFC 6077: Open Research Issues in Internet Congestion Control [RFC6077]
The document describes some of the open problems in Internet congestion control that are known today.  This includes several new challenges that are becoming important as the network grows, as well as some issues that have been known for many years.  These challenges are generally considered to be open research topics that may require more study or application of innovative techniques before Internet-scale solutions can be confidently engineered and deployed.

primal congestion
dual congestion

3.1.  Challenge 1: Network Support

Explicit signaling mechanisms, whether in-band
   or out-of-band, require a communication between network components
   and end-systems. 
   
   the problem with various AQM schemes is the difficulty in
   identifying correct values of the parameters that affect the
   performance of the queuing scheme (due to variation in the number of
   sources, the capacity, and the feedback delay)
   
     The second class of approaches uses explicit signaling.  By using
   explicit feedback from the network, connection endpoints can obtain
   more accurate information about the current network characteristics
   on the path.  This allows endpoints to make more precise decisions
   that can better control congestion.
   
   It suggests that functions
   that can be realized both in the end-systems and in the network should be implemented in the end-systems.

However, as discussed in [Moors02] for instance, congestion control
   cannot be realized as a pure end-to-end function only.  Congestion is
   an inherent network phenomenon and can only be resolved efficiently
   by some cooperation of end-systems and the network.  
   
   Even if a new protocol structure were found, it seems unlikely that
   network flow state could be avoided given the network's per-packet
   flow rate instructions would need to be compared against variations
   in the actual flow rate, which is inherently not a per-packet metric.
   
    Open questions are:

   -  How much can network elements theoretically improve performance in
      the complete range of communication scenarios that exist in the
      Internet without damaging or impacting end-to-end mechanisms
      already in place?

   -  Is it possible to design robust congestion control mechanisms that
      offer significant benefits with minimum additional risks, even if
      Internet traffic patterns will change in the future?

   -  What is the minimum support that is needed from the network in
      order to achieve significantly better performance than with end-
      to-end mechanisms and the current IP header limitations that
      provide at most unary ECN signals?

Needed Info
  1. Capacity of (outgoing) links
  2. 2. Traffic carried over (outgoing) links
  3.    3. Internal buffer statistics
  4.    
  
Challenge 7: Misbehaving Senders and Receivers

   In the current Internet architecture, congestion control depends on
   parties acting against their own interests.  It is not in a
   receiver's interest to honestly return feedback about congestion on
   the path, effectively requesting a slower transfer.  It is not in the
   sender's interest to reduce its rate in response to congestion if it
   can rely on others to do so. 
   
   large volumes of unresponsive voice traffic could
   represent such a threat, particularly for countries with less
   generous provisioning [RFC3714].  Also, Internet video on demand
   services that transfer much greater data rates without congestion
   control are becoming popular.  In general, it is recommended that
   such UDP applications use some form of congestion control [RFC5405].
   
   Note also that self-restraint could disappear from the Internet.  So,
   it may no longer be sufficient to rely on developers/users
   voluntarily submitting themselves to congestion control.
   
   A large variety of ALGs and middleboxes use such
   mechanisms to improve the performance of applications (Performance
   Enhancing Proxies, Application Accelerators, etc.).  However, the
   implications of such mechanisms, which are often proprietary and not
   documented, have not been studied systematically so far.
   
   
  







### References
#### Informative References
[6077](https://tools.ietf.org/html/rfc6077)
