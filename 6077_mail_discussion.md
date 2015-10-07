## MaRNEW Mail Discussion: Open Research Issues in Internet Congestion Control
Over the course of the [MaRNEW](https://iab.org/workshops/marnew) Workshop there was a discussion on the [MaRNEW Mailing List](mailto:marnew@iab.org) about internet congestion control, sharing of data and new possible solutions. 

### RFC 6077: Open Research Issues in Internet Congestion Control [RFC6077]
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

### Needed Research
#### Research Need Identified in 6077
The [6077] document lists some information (data) that could help improve congestion control across networks and infrasturture. Those relevant to MaRNEW and focused on (or covering) mobile networks include:
  1. Capacity of (outgoing) links
  2. Traffic carried over (outgoing) links
  3. Internal buffer statistics

Readers should refer to the main document for descriptions of each.

The [6077] document askes a number of open research questions, some relevant to MaRNEW are:
* "How much can network elements theoretically improve performance in the complete range of communication scenarios that exist in the Internet without damaging or impacting end-to-end mechanisms already in place?"
* "Is it possible to design robust congestion control mechanisms that offer significant benefits with minimum additional risks, even if Internet traffic patterns will change in the future?"
* What is the minimum support that is needed from the network in order to achieve significantly better performance than with end-to-end mechanisms and the current IP header limitations that provide at most unary ECN signals?

#### Research Need Identified on the MaRNEW Mailing List
The [MaRNEW Mailing List](mailto:marnew@iab.org) discussion also focused on the need for data, it briefly looked into what data is needed and at what scale. 

### Gathering Data
#### Desired Data to Collect
Within the MaRNEW Discussion these data were requsted or noted to be useful in the investigation of the effectiveness or need for network management elements or to make dynamic decisions at the application level.

* Channel bandwidth (at base station)
* Allocated channels vs available channels (at base station)
* Data across use cases (e.g. use case of someone using their phone at home, then in the car, and then in the office)
* Bandwidth is necessary, but not sufficient, for fully understanding underlying network characteristics.
* Knowing the RRC state. If an endpoint knows it's in IDLE, DCH, FACH, etc it can make better decisions. 

#### Issues with Gathering Data
Some vendors and operators sited issues with gathering data, these are listed below:

* Someone mentioned congestion control hints from the mobile network would be "too ephemeral and dynamic to be useful" (e.g. someone turns on a microwave oven and congestion becomes high)
  * But there may be cases where the Android API can provide a coarse hint that is useful, and this would be worth testing.
  * Ephemeral elements include: aggregate channel BW, per user BW, latency, ...  on time scales of 10-100's of ms and variations on the order of 50:1 or more (or less).  
  * RAN vendors have been loath to expose this since its hard to predict accuracy and easy to make bad decisions based on ever changing data.   
  * Over a larger time scale (say many seconds / minutes), you can conclude some level of overall aggregate channel conditions. In aggregate, you can conclude that there are problems and some mitigation of traffic for certain classes of users could result in an aggregate improvement in QoE.  
  * It would be good to divorce traffic management methods, from the dependence on traffic type detection mechanisms.
  * Each specific user still may see a wide variation of performance since they may be in very good signal-to-noise areas (getting a higher share of BW) or very bad signal-to-noise areas (getting a very low BW).  
* Data received may be out of date as soon at the endpoint receives it.
* Someone mentioned "No Operator would share that kind of information from their base station", although some content providers said they have managed to work with operators and exchange data successfully. Operators may need to consider the following before sharing data
  * Is this info free or paid for (NN issue)?
  * If I sell it to one content providers, do I need to sell it to another too to save on anti-trust issues?
  * Can my competitor or customers get this information and use it against me (e.g. here is map of where your network is poor during rush hour)?
  * Can my suppliers get this information and use it against me?
  * Facebook have asked a couple of vendors for congestion hints in a variety of ways, with no real response.


### Warnings and Requirements
The discussion on the [MaRNEW Mailing List](mailto:marnew@iab.org) identified the following warnings or requirements for evolved congestion control work.

* Need to make sure that such efforts do not merely shift the bottleneck to cause problems elsewhere
* Info pertaining to the cell (or cell cluster) as a whole may be best managed at the RRC, the dedicated radio resource controller within 3GPP networks. 
* There is usually a lag between changing conditions in a cell and the UE detecting reduced/increased bandwidth
* New solutions will need to work across network types
* Many basic approaches in CC related to RTT or loss are skewed by radio network characteristics and start to break down.

### Existing Solutions
The MaRNEW mailing list discussion highlighted some solutions which exist currently.

* Android's [requestBandwidthUpdate](http://developer.android.com/reference/android/net/ConnectivityManager.html#requestBandwidthUpdate) is coming up in Android M as an API of exposing available capacity on the radio downlink 
* (Pacing) Will even the beest possible signal coming from the RAN be effectively used by a TCP sender? 
  * In LTE it's probably latency variability that impacts the most TCP.  Even with zero packet loss rate thanks to link adaptation, poor ACK clocking caused by the latency would augment TCP burstiness.  This can bring buffer losses that could be avoided by simply pacing TCP on the sender side.
    * It may be counter-intuitive but link adaptation could help avoid channel losses,  augment latency variability causes buffer losses. 
    * Pacing is hard to implement but can be simpler than closed loop protocols based on complex feedback. 
    * Also TCP pacing over LTE would not suffer from the known fairness issues as buffers for different UEs aren't shared in the tower. 
    * No-one believed pacing is being used at a TCP layer, but RSSI and other signal parameters such as RSSI/RSRP are being used for interface/network selection or in connection manager type applications. 
* (Heuristics) From an application point of view, parameters such as Jitter, Latency and Delay parameters (based on some explicit measurements) on an access link are used to some extent; if it is then this may be a proprietary art and there may be good amount of heuristics involved in such calculations.
* (Signal Strength Parameters) Some popular end-points do make use of signal strength parameters, not at the application level but for network selection; such as performing an handover between two access points, when the RSSI differential between those adjacent AP’s is below a certain threshold, or a mobile router's selection of an egress link (LTE or Wi-Fi) based on these parameters. 
* (Channel Quality Indicator) A recent paper from Andreas (Google) and UCSD folks proposed a [channel quality indicator (CQI)](http://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43311.pdf) based cross-layer congestion control for cellular networks. 
  * TCP pacing with rate inferred from the feedback. Pacing is implemented usingtoken bucket rate limitation. 
  * Performance could be good by just pacing at the Ack clock rate. This is not explored in this paper but if so the implementation would not require any feedback from the RAN. 
* CDN metadata exchange idea where a CDN and content provider exchanges metadata for radio network information.


### References
#### Informative References
[6077](https://tools.ietf.org/html/rfc6077)






