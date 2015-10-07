## 6077 Mail Discussion
A summary of the points in the 6077 mail discussion, will rename later.

## RFC 6077: Open Research Issues in Internet Congestion Control [RFC6077]
The document describes some of the open problems in Internet congestion control that are known today.  This includes several new challenges that are becoming important as the network grows, as well as some issues that have been known for many years.  These challenges are generally considered to be open research topics that may require more study or application of innovative techniques before Internet-scale solutions can be confidently engineered and deployed.

Readers are encouraged to read the whole document. For the purposes of MaRNEW the document details a number of key points for managing networks and congestion control. Some of these points are given below:

* The document divides congestion into primal congestion control and dual congestion control representing congestion control being managed by the traffic-sender and routers in the network respectively.
* [ECN](#) and [AQM](#) deployments are analysed, AQM is noted as having difficulty in identifying correct values of the parameters that affect the performance of the queuing scheme
* Congestion control in networks is explored in section [3.1](), congestion control here happens through queue management / scheduling and explicit signaling (using explicit feedback from the network to allow endpoints to make decisions)
* The document discusses the end-to-end argument with reference to router support, the principle suggests that functions that can be realized both in the end-systems and in the network should be implemented in the end-systems.
* However, the document also states that according to [Moors02] "congestion control cannot be realized as a pure end-to-end function only.  Congestion is an inherent network phenomenon and can only be resolved efficiently by some cooperation of end-systems and the network".  
* Network flow-rates are not a per-packet metric, so comparing these to per-packet flow rate would be hard. The document talks about this in refrence to devsing a new protocol structure.
* The document discusses "Misbehaving Senders and Receivers" in section 7, which details why congestion control depends on parties acting against their own interest and some may lie about their traffic to avoid slow transfer.
* Evolutions in networks have allowed for more complex content and for UDP to become more widely used; video-on-demand is listed as a good use case here, and one where UDP may benefit from some congestion control.
* The document warns that "self-restraint" could be removed from the internet, so developers/users may not be a reliable party in controlling congestion control. 
* Middleboxes are also mentioned as having the aim of improving the performance of applications, but "the implications of such mechanisms, which are often proprietary and not documented, have not been studied systematically so far".

The document lists some information (data) that could help improve congestion control across networks and infrasturture. Those relevant to MaRNEW and focused on (or covering) mobile networks include:
  1. Capacity of (outgoing) links
  2. Traffic carried over (outgoing) links
  3. Internal buffer statistics

Readers should refer to the main document for descriptions of each.

The document askes a number of open research questions, some relevant to MaRNEW are:
* "How much can network elements theoretically improve performance in the complete range of communication scenarios that exist in the Internet without damaging or impacting end-to-end mechanisms already in place?"
* "Is it possible to design robust congestion control mechanisms that offer significant benefits with minimum additional risks, even if Internet traffic patterns will change in the future?"
* What is the minimum support that is needed from the network in order to achieve significantly better performance than with end-to-end mechanisms and the current IP header limitations that provide at most unary ECN signals?






### References
#### Informative References
[6077](https://tools.ietf.org/html/rfc6077)





[MaRNEW Mailing List](mailto:marnew@iab.org) 
