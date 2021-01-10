# Next Generation Network Module Review(Slides)
## 1. QoS (Quality of Service)
   In QoS, there are three major questions need to be considered:  
    1. Latency
    2. Jitter
    3. Capacity
    4. Packet Loss  

### 1. Latency
   A. Meaning
    The time spent in transmitting packets to their destination in networks. 
    B. Position in OSI 7-Layer Model
    Can not be solved above layer 4, but needs to be solved at layer 3 and below.(WHY??)
    Reasons: Transport Layer is going to solve packet recovery, reuse of data stream from different applications but in the same end-point and sort the packets received. => Latency is related to layer 1,2,3 because "latency" includes: process delay, queue delay, transmission delay and propagation delay. 
    C. Real-word meaning
    For video or voice conferences, latency is a serious problem.

### 2. Jitter
   A. Meaning
    Jitter means there will be sudden variation in the latency of receiving packets.
    B. Position in OSI 7-Layer Model
    CAN be solved in application level through larger buffer, but will increase latency (WHY??)
    Reasons: Larger buffer => larger queue => more latency
    C. Real-word meaning
    Some real-time required applications needs low jitter, which means they expect receiving a packet after another packet in a certain time.

### 3. Packet Loss
   A. Meaning 
    In the process of transmission packets in a session, there is always possible that losing some packets in the middles. 
    B. Position in OSI 7-Layer Model
    Ideally, it can be solved in layer 3 (Network Layer), but packet loss can influence all the  layers, but at least, it can be moderated in layer 4(Transport layer), depends on TCP protocol to recover some lost packets.
    C. Real-word meaning
    Not too bad for video or voice and voice and video do not use TCP since it would be better to loose a frame than having it  back at a later time. (Latency is important in voice, video)

### 4. Capacity
   A. Meaning
    Capacity is related to other three questions, e.g. low capacity=> large queue=>large latency, increase the probability of packet loss, jitter will become more unstable.
    B. Position in OSI 7-Layer Model
    Layer 1 ,layer2 and layer3
    C. Real-word meaning
    real-time applications.

### 5. Solutions
   1. Ultimately depends on capacity
    Solving all three problems with increasing capacity , but it will increase latency. (WHY???)
    Reasons: Since large capacity=>large queue=>large latency.
    2. Statistical multiplexing
    A great method to share resources to deal with bursty data.

### 6. Developments
   Is there a method to maintain the benefits of Statistical multiplexing(avoid excessive overprovisioning) and have a good behaviour in terms of packet loss, latency and jitter.
    => Not all applications have same requirements, so deciding which problem has the highest priority is a key question.

### 7. QoS Differentiation
   Based on the discussion above, it can be found that the key question is not searching a method which can feed every kind of applications' requirements but finding a method to set priority to the three questions above, and solve them by the priority.

### 8. QoS Tools
   1. Policer
    discards(abandon) packets when they go above a pre-established threshold(limit). 
    1. Shaper
    delay packets so that the bandwidth threshold is not exceed at any given time.
    2. Classifier
    Inspects an incoming packet and assigns to it a class of service(COS)
    3. Metering and colouring 
    Check the rate which packets are coming in against pre-established threshold and subsequently marks packets with different colours. 
    4. Queueing differentiation 
    Queues all work in FIFO model, but packets with different COS can be assigned different queues.
    5. Scheduler
    it decides in which order to get packets from the different queues.
    6. Rewrite
    It can modify a packet COS marking.

### 9. Effects
   1. QoS tools
    packet loss caused by: traffic policer, drop by the queue
    Latency caused by: shaper, scheduler
    Jitter caused by: Shaper, scheduler
    2. Queue Size
    Longer queue is able to absorb heavier traffic bursts, lower chance of queue filling up and traffic being dropped
    But packets spend longer time in queue, so the delay and jitter increase.

### 10. Scheduler implementation
   1. FIFO
    2. FQ
    3. SP
    4. WFQ
    5. WRR
    6. DWRR
    7. PB-DWRR

### 11. SLA and TrTCM
   1. SLA
       1. Service level agreement 
       2. CIR: Committed Information Rate(must be satisfied)
       3. PIR: Peak Information Rate(is satisfied if capacity is available)
    2. TrTCM
       1. Colour blind(all input are the same)
          1. Data below CIR marked green
          2. Above CIR,but below PIR as yellow
          3. Above PIR as red(dropped)
       2. Colour aware(input already marked green or yellow)
          1. Green goes into CIR queue, but if above CIR goes into PIR queue
          2. Yellow goes into PIR queue
          3. Any traffic above PIR is red(dropped)
          4. Notice that yellow never become green even if CIR is still available

## 2. Fixed Network


## 3. Wireless Network
### 1. Wireless channel impairments and mitigation
 1. Impairments
       1. Shadowing: Models attenuates since obstacles, typically modeled in log-normal distribution(frequency up, the negative effect of shadowing and obstacles is more serious)
       2. Fading: Quick variation in received power due to time-varying channel characteristics.
       3. Interference: 
       4. Path loss: Signal attenuates with distance; roughly proportional to 1/d^2
       5. Multipath: Due to the differences of scattering and reflection, which will lead multiple versions of the transmitted signal arrive at the receiver. Delay spread: original signal is spread due to the different delays of parts of the signal
       6. Noise: Unwanted signal added to the message signal; may due to that the signal is generated in natural phenomena e.g. lightning; SNR often used to assess the quality of channel.
    2. Mitigation
       1. Diversity
          1. Spatial diversity: multiple distant antennas
          2. Frequency diversity: transmit the same signal in multiple frequencies
          3. Temporal diversity: repeated transmission of the same signal
          4. Polarization diversity: different polarizations
       2. Directional antennas: can be used to reduce interference, the probability of interception or jamming
       3. Coding and modulation: BER(Basic Encode Rules); QPSK and QAM are different implementation of a certain BER.
       4. spread spectrum: signals are distributed over a wide range of frequencies and the collected back at the receiver
       5. Frequency hopping
       6. Direct sequence spread spectrum(DSSS), Frequency Hopping Spread Spectrum(FHSS), DSSS is more effective in resisting to fading and multipath and much harder to detect, but FHSS is easier to be implemented than DSSS.
       7. system-level mitigation: frequency and code planning, multiple access method,etc.

### 2. Overview of wireless networks
   1. Nomadic
    2. Mobile
    3. OSI reference model
       1. Physical Layer(layer1):Frequency selection, modulation,signal detection,encryption
       2. Data Link Layer(layer2):Medium access,error control
       3. Network layer(layer3):Routing, handover between different networks,network-wide addressing, device location
       4. Transport Layer(layer4): Reliable delivery, error recovery, congestion control
       5. Session layer(layer5)
       6. Presentation layer (layer6)
       7. Application layer(layer7): application-specific exchange of messages, Wireless Application Protocol(WAP)
    4. Broadcast, radio and TV: 
    5. Cellular and PCS: 2G Cellular Phone 800-900 MHZ; 3G Broadband Wireless 746-794 MHZ,1.7-1.85 GHZ,2.5-2.7 GHZ; Personal Communication Service(PCS)1.85-1.99 GHZ
    6. WLANs,WPANs,fixed wireless: IEEE 802.11b,g 2.4GHZ; IEEE 802.11a 5GHZ; Bluetooth 2.45GHZ; LMDS 27.5-31.3GHZ 
    7. Regulators: ITU-R handles standardization and frequency planning
    8.  Harmonization: some degree of harmonization(more rational/efficient re-organization ) of spectrum wold-wide is desirable.
    9.  Dynamic spectrum access
    10. Transmission at lower frequencies attenuate less with distance, so lower frequencies are ideal for long range transmissions. 

### 3. WLAN(IEEE 802.11)
   1. Motivation
       1. Simplicity
       2. Support for nomadic users
       3. Robustness to disasters
       4. Spontaneous deployment
    2. Limitations
        1. QoS: throughput is lower than wireline counterparts; limited support for service differentiation or guarantees
        2. Regulatory issues: limitation on maximum transmit power;often operate in ISM bands(Industrial, Scientific and Medical)
        3. Coexistence:multiple standards, overlapping frequency bands
        4. Security: easy to eavesdrop
    3. Goals
       1. Coordination of international spectrum regulation; license-free operation
       2. low power
       3. Robustness
       4. Interoperability:WLAN/WWAN(e.g. 802.11/3G-4G),WLAN/WPAN(e.g. 802.11/Bluetooth)
       5. Security
       6. Application support
    4. Comparison of using infrared and radio
    5. Comparison of infrastructure model and ad-hoc model
       1. infrastructure-based=>access point is responsible for forwarding message,limited control and management functions. Applications: office-wide WLANs, hotspots
       2. Ad-hoc model: stations communicate directly with one another, may perform routing functions. Applications: military,sensor networks, vehicular networks
    6.  WIFI
       3.  interoperability of 802.11-based products
    7. IEEE 802.11b
       1. higher-speed physical layer in the 2.4 GHZ
       2.  same MAC functions
       3.  data rates: 11,5.5,2 and 1 Mbps, in practice, about 6-7 Mbps
       4.  DSSS
       5.  1 Mbps: DBPSK, 2 Mbps: DQPSK
    8. IEEE 802.11a
       1.  Operates in 5Ghz band (shorter range than 802.11b or 802.11g; not directly compatible with 802.11b or 802.11g)
       2.  12 non-overlapping channels
       3.  Uses OFDM to achieve up to 54Mbps
    9.  OFDM
        1.  Distributes the data over several carriers spaced apart at precise frequencies
        2.  Also used in ADSL and digital TV(in Europe)
        3.  802.11a uses 52 subcarriers equally spaced around a center frequency. Four of these subcarriers are used for pilot signals(signal detection)
    10. IEEE 802.11g
        1.  tries to combine the best features of 802.11a and 802.11b
        2.  data rates of 20+ Mbps(up to 54 Mbps)
        3.  Operates in 2.4 Ghz
        4.  OFDM, forward error correction
        5.  Interoperable with 802.11b
    11. IEEE 802.11 series products summary
        1. Highest cost: 802.11 a
        2. Fastest maximum speed: 802.11a
        3. Shortest range signal: 802.11a
        4. Lowest cost: 802.11b
        5. Slowest data rate:802.11b
        6. Largest range: 802.11b, 802.11g (same frequency)
    12. Other comparisons between 802.11a,b,g
        1.  in 802.11b,g, 802.11 g has a higher data rate, but 802.11g costs more than 802.11b
        2.   Other appliances may interfere same frequency band(802.11b,g)
        3.   both 802.11g,a  supports more simultaneous users.
        4.   802.11a can not be compatible with 802.11b,g(different frequencies)
    13. IEEE 802.11n
        1.  Higher data rate through using MIMO
        2.  Operate in 2.4 Ghz and/or 5GHZ
        3.  physical rate: up to 600 Mbps
    14. IEEE 802.11ag (WiGig)
        1.  Date throughput speeds up to 7 Gbps
        2.  60 GHZ ISM band(large bandwidth, reduced interference)
        3.  range: few meters=> very small range, suits for very short range(across a room) but high data volume(e.g. HD video)
    15. IEEE 802.11ax(WIFI 6)
        1. designed specifically for high-density public environments, like trains, stadiums and airports
        2.  will also be beneficial to IoT deployments
        3.  designed for cellular data offloading
        4.  deliver a total theoretical bandwidth of 14 Gbps
        5.  Backward compatibility with 802.11n
        6.  Operate in both 2.4 Ghz and  Ghz
        7.  Using MU-MIMO (Multiuser-MIMO) and Orthogonal Frequency Division Multiple Access(OFDMA)

### 4. HetNet, small cell deployments, mmWave
   1. Q: How do we cope with the demand for higher capacity?
       1. more bps over the same link
       2. getting more spectrum
       3. more nodes in the wireless infrastructure
    2. Homogeneous Network(HomNet) and Heterogeneous Network(HetWork)
       1. HomNet: Mobile devices connect to the nearest Macro-cell base station
       2. HetNet: Similar to HomNet, but there are some small-cell base station in the edge of cellular, and so that the mobile devices in the cellular edge can connect to the small-cell base station but not Macro-cell base station.=>increase the performance for the distant users
    3. Interference in HetNet
          1. Massive deployments of Low Power Nodes(LPNs)
          2. All theses nodes share the same frequency band and same Radio Access Technology(OFDMA based systems)
          3. So, there will be two kinds of interference: Macro to LPN interference, LPN to Macron interference. => These two kinds of interference can be called "Inter-cell interference"
    4. Fixed spectrum allocation for HetNet
       1. REUSE 1-1: let multiple Macro-cells use the same frequency
       2. REUSE 3-1: distribute frequency into different parts and assign them to Macro-cells
       3. ORTHOGONAL ASSIGNMENT: 
    5. mmWave(e.g. 5G cellular)
       1. Cellular system live with a little microwave spectrum
       2. Huge amount of spectrum available in mmWave bands

## 4. Next generation Software-defined controlled systems
### 1. Architecture paradigm provides:
 A centralized control of a network.
    Enhance programmability of network component(i.e. switch, router)
    Enable a modular design and implementation of network's architecture.
    Promise reduction of Capital Expenses, Operation Expenses, and Energy Awareness.
   
### 2. Terminology, concepts and definitions
 1. Data plane
   2. Forwarding device
    3. Flow
    4. Flow rules
    5. Flow table
    6. Southbound interface
    7. Control plane
    8. Northbound interface 
    9. Management plane
   
### 3. OpenFlow Protocol
   1. Use: to communicate between programmable network devices and centralized controller.
    2. Aggregated and flow-based
   
## 6. Traffic Modelling
### 1. Queue System
   1. Elements of a queueing system: input=>queue=>server=>output
    2. \lambda is the customer arrival rate
    3. C means the amount of servers
    4. a/b/m/k Notation
       1. a = type of arrival process
          1. M: Markov=>denotes Poisson arrivals, so interarrival times are i.i.d, exponential random variables.
       2. b = service time distribution 
          1. M: Markov=>denotes exponentially distributed
          2. D: Deterministic=>denotes constant service times
          3. G: General=> denotes i.i.d service times following some general distribution.
       3. m=number of servers
       4. k=maximum customers allowed in the system(not necessary when defining)

### 2. M/M/1 Queue(LOTS OF CALCULATION!!)
   1. E[n] = \lambda * E[\tao]: \lambda: customer arrival rate, E[n]: expected number in queue, E[\tao]: average time spend in the queue
    2. Single-server system
    3. \rho = \lambda / \mu (<1) => utilization
    4. Pn denote the probability that n customers are currently in the system
    5. P0  = (1-\rho), Pn = \rho^n * (1-\rho)
    6. So, average customers in the system:E[n] = \rho / (1-\rho)
    7. average delay in the system: E[\tao] = 1/(\mu-\lambda)
    8. average waiting time: E[\tao q] = \rho/\mu*(1-\rho)
    9. average number of customers in the queue: E[nq] = \rho^2/(1-\rho)
   
### 3. Other M/M/... Queue(LOTS OF CALCULATION!!)
   1. All of the other M/M/... queue system are similar: Poisson arrival process; exponential service times
       1. M/M/1/N: finite buffer(system capacity =N)
       2. M/M/m: m servers(rather than 1)
       3. M/M/infinite: infinite number of servers(no queueing)
       4. M/M/m/m: m servers without queueing
   
### 4. M/G/1 Queue(LOTS OF CALCULATION!!!)
   1. M/G/1: like M/M/1, but allows that the service times with general distribution
    2. Average service time: 1/ \mu, second moment of service time: E{X^2}
    3. P-K Formula: expected waiting time in queue for M/G/1: W = \lambda *E{X^2}/(2*(1- \rho )), \rho = \lambda *(1/\mu) => (utilization)
    4. G/G/N/K Queue(Kendall's Notation): G:means any distribution;First letter denotes the arrival process,M means exponential or memoryless type of arrival process;Second letter: service time distribution,M: exponential,D: Deterministic;Third letter: number of servers; Fourth letter, number of customers in system(means the sum of being in queue and served)
   
### 5. traffic models
   1. Traffic models
       1. 
    2. Burstiness 
       1. A bursty source generates traffic in random clusters
       2. Deterministic traffic is not bursty
       3. Poisson process (in continuous time) and Bernoulli process (in discrete time) are bursty as single processes
    3. Self-similar phenomena
       1. A phenomenon that is self-similar looks or behaves the same when viewed at different degrees of “magnification” or different scales on a dimension (time or space)
    4. Hurst parameter
       1. H is the Hurst Parameter, a key measure of self-similarity
       2. H=0.5 indicates the absence of self similarity
       3. H closer to 1 indicates a higher degree of persistence of long-range dependence (self similarity)
       4. It turns out data traffic is well-modeled as a self-similar process in many practical networking situations
    5. Ethernet traffic
       1. Authors estimated Hurst parameter of H = 0.9
       2. Aggregating several streams does not remove self-similarity
       3. We know that Poisson is not a good model in this case. But what is? => Superposition of many Pareto-like ON/OFF sources
    6. Fractal dimension:
          1.  Log(C)/Log(b)...

## 7. Fixed mobile convergence
### 1. LTE, LTE-A, LTE-A-PRO
   1. Motivation
       1. Evolution from 2G and 3G cellular systems
       2. Drivers
          1. Exponential increase in demand
          2. Higher data rates
          3. Lower latency
          4. ...
       3. Smooth transition to 4G(IMT-Advanced)
    2. LTE performance
       1. 100 Mbps peak DL, 50 Mbps peak UL
       2. Backward compatibility with GSM/EDGE/UMTS
       3. Wide applications
    3. LTE Features
       1. OFDM/OFDMA => increase spectral efficiency=> increase data rates
       2. All-IP architecture => simplified network management, reduced CAPEX(Capital Expenditure) and OPEX(Operating Expense)
       3. Spectrum Flexibility
          1. Operating in a wide range of spectrum
          2. Operating in different-size bands
       4. Protocol layers
          1. Packet data convergence protocol(PDCP)
             1. IP header compression
             2. Cyphering and integrity protection
          2. Radio link Control(RLC)
             1. Segmentation and concatenation
             2. Retransmission handling
             3. In-order delivery to higher layers
          3. Medium access control (MAC)
             1. Uplink and downlink scheduling at eNB(evolved Node B)
             2. Hybrid Automatic Repeat ReQuest(HARQ)
          4. Physical Layer(PHY)
             1. Coding/decoding
             2. Modulation/demodulation (OFDM)
             3. Multi-antenna use
             4. OFDMA with cyclic prefix in DL, SC-OFDMA with cyclic prefix in UL
             5. Duplexing(双工): FDD(Frequency Division Duplex) and TDD(Time Division Duplex)
             6. 10 ms radio frames, containing 20 slots of 0.5 ms duration
             7. Supported modulation: QPSK,16-QAM,64-QAM
             8. Broadcast channel uses QPSK
             9. Maximum information block size(information block: are the smallest elements of resource allocation): 6144 bits
             10. CRC-24 for error detection
          5. Scheduling
             1. Scheduler in eNB allocates resources blocks to users for predetermined amount of time
             2. Slots consists of either 6(for long cycling prefix) or 7(for short cycling prefix) OFDM symbols
             3. Longer cyclic prefixes are used to address longer multipath fading channel length
             4. Number of available subcarriers changes depending on transmission bandwidth
          6. OFDMA
             1. OFDM uses a large number of narrow subcarriers for multi-carrier transmission
             2. The basic LTE DL physical resources can be seen as a time-frequency grid.
                1. In the frequency domain, the spacing between the subcarriers is \delta f = 15Khz
                2. symbol duration time: 1/ \delta + cyclic prefix
                3. Cyclic prefix is used to avoid inter-symbol interference and allows the use of simpler receiver architectures
                4. One resource element carriers QPSK,16QAM or 64QAM
                5. OFDM symbols are grouped into resources blocks
                6. Resource blocks have a total size of 180kHz in the frequency domain and 0.5ms in the time domain 
          7. Multi-antenna techniques
             1. Transmit diversity
             2. beam-forming
             3. spatial multiplexing
             4. Multi user MIMO
          8. Services
    4. LTE Advanced(LTE+) goals
       1. Peak data rates: DL=>1Gbps, UL=>500Mbps
       2. Spectrum efficiency: 3 times than LTE
       3. ...
    5. LTE Advanced Pro
       1. Propel mobile broadband even further
          1. Carrier aggregation evolution-wider bandwidth
          2. LTE in unlicensed spectrum
          3. TDD/FDD evolution-faster, more flexible
          4. Many more antennas- path to massive MIMO
       2. Proliferate LTE to new use cases
          1. Contact the IoT
          2. New ways to connect and interact(e.g. LTE V2X Communication)
          3. New classes of services(e.g. digital TV broadcasting)

### 2. Fixed mobile convergence(optical wireless networks convergence)
   1. Optical Transmission
      1. Optical fibre: typical path loss is 0.2 db/km, which means signal can go 150 KM without amplification
      2. Twisted pair and coaxial(同轴电缆)
          1. Twisting the copper helps reducing interference from external sources
          2. Coaxial uses external sheet to confine the radiation within the cable
       3. Total internal reflection
       4. n = C0/C(C0: the speed of light in vacuum, C: speed of light in the medium considered)
       5. if n1>n2(reflective index)=>\xita2>\xita1=>C1>C2
       6. Try to transmit the signals with the minimum distortion
       7. Path loss in fibre
          1. The amount of power lost during propagation depends on the frequency (or wavelength) used for transmission.
          2. The smallest loss is at a wavelength of 1.55 μm, and is 0.2 dB/Km
       8. Dispersion in fibre
          1. Dispersion in fibre is due to the fact that the refractive index n is not constant, but its value depends on the frequency of the signal.
          2. There are three types of dispersion:
             1. Modal dispersion: because different modes propagate at different speed (only occurs in multi-mode fibre)
             2. Chromatic dispersion: because different frequencies within a single mode propagate at different speed
             3. Polarization mode dispersion: because different spatial polarization can propagate at different speed
          3. Model dispersion: Since some modes will reflect a narrower angle than other modes, so even if they propagate in a same speed, they will still arrive the end in different time
          4. impairments caused by model dispersion
             1. The pulse spreads will be different between different modes, so the peak power will decrease
             2. In a communication channel, when i transmit several pulses, they do overlapping=>intersymbol interference(ISI)
          5. Single-mode and multi-mode
             1. Multi-core has a larger core, which allows multiple modes to coexist at the same frequencies for optical transmission
             2. Single-mode has a smaller core, which only allow one propagation mode.
             3. model dispersion will be simply eliminated by using single-mode fibre
          6. Chromatic dispersion
             1. Optical communication is achieved by transmitting pulses
             2. Each pulse has a finite spectral width(it's made of adjacent frequencies)
             3. If lower frequencies travel slower than the higher ones, the pulse spreads, causing transmission errors
          7. Chromatic and modal dispersion
             1. Modal dispersion has the biggest effects
             2. Chromatic dispersion is the second most important
          8. Dispersion shifted fibre
             1. Dispersion in fibre is due to: the material (cannot be changed) the shape of the waveguide, i.e. the shape of the fibre cross section
             2. modify the dispersion by changing the distribution of the refractive index
          9. Polarization-mode dispersion(PMD)
             1.  The electric field in a single mode fibre propagates with two orthogonal polarization
             2.  Because of imperfect production techniques, the fibre is not completely symmetric
             3.  The two orthogonal components of the electric field have different propagation characteristics
             4.  The two polarizations travel at different speed
             5.  At the receiver the pulse is wider than at the source
             6.  But PMD is less severe than chromatic dispersion: about 0.5 ps/km
        10. LASER:A device that emits coherent light;A device used for cutting steel in heavy industry;A telecommunication device used to transmit information
        11. Signal modulation
            1.  Modulation is used to add information to a carrier signal
            2.  Two methods to use to modulate
                1.  Direct laser modulation: switching the power current on and off
                2.  External modulation: obscuring intermittently the light generated by a laser.
        12. Concepts of optical link design
            1.  usually have a BER requirement that needs to be satisfied, in order to satisfy the BER, I need to consider the following constraints
                1.  power budget 
                2.  OSNR
                3.  other impairments
            2. Noise in optical systems
               1. Amplified Spontaneous Emission (ASE): due to optical amplifiers, which besides amplifying the signal carrying information also introduces additional noise.
               2. Thermal noise: due to the random thermal-driven motion of electrons at the receiver, which sums up to the signal carrying information
               3. Shot noise: due to the quantistic nature of an optical signal, the photons carrying the information arrive at the detector with random arrival times 
            3. BER(Bit Error Ratio) and OSNR(Optical signal-to-noise ratio)
               1. The OSNR is the relation between the power of the signal and the power of the noise at the receiver
               2. The optical noise is due to the presence of optical amplifiers
               3. if there are no amplifiers then the optical noise will be low and the limiting factor will be the electrical thermal noise at the receiver
               4. The higher the OSNR value, the easier will be to determine whether  a received bit has a 0 or 1 value
               5. reducing the amplifiers spacing increases the OSNR
        13. Wavelength division multiplexing(WDM):Like in (electric) wired and wireless communication difference frequency bands can be used to create different communication channels. Different wavelengths are individually modulated and sent over the fibre.
    2.  Optical & wireless convergence
      1.  Question: how to increase mobile capacity by 1000 times (by 2020??)
      2.  Cell density issue
            1. Backhauling a macro BS with fibre, is feasible from a cost perspective, because the BS aggregates many users, thus it generates considerable revenue
            2. With higher cell density, each (small) cell only serves a few users at a time (this is the way it can provide higher rates)
      3. Coax in distributed RAN(Radio Access Network)
         1. Up to 4G, base stations used to be distributed, meaning that each cell has a mast, antenna as well as all the radio and digital processing units up to layer 3.
         2. Recently this is changing, and the digital processing part starts becoming centralized
      4. Fibre optics in distributed RAN: In order to reduce this issue, vendors have come up with a solution to replace the coax with fibre
      5. CPRI: Common Public Radio Interface
         1. The connection between the BBU(Baseband Unit, interpret baseband frequencies) and RRU(远程无线电头,Remote radio head) over fibre is through a protocol called Common Public Radio Interface (CPRI).
      6. BBU Hoteling(placing the BBU in a completely different location)
      7. BBU pooling( trying some statistical multiplexing of the data and use a smaller number of BBUs)
      8. Cloud-RAN
      9. How does CPRI work?
         1.  CPRI puts the division line close to the Antenna
      10. RAT vs Fronthaul rates: Fronthaul requires a transmission capacity 16 times higher than the equivalent backhaul rate! This is independent of usage… it’s a sustained rate! 
## 8. Future development(Network Automation, complex system science)

## 9. Module review
   1. Shannon Formula
   2. Dominant factor for WAN? For LAN in Shannon Formula? LAN: Interfering signal power, WAN: Noise power
   3. Dominant factor for WAN? For LAN "Wireless channel impairments"? LAN: interference , WAN: path loss, noise
   4. Transmit power up, coverage up, interference up; increasing bandwidth, more data potentially achievable, more noise
   5. 8-QAM: 3 bit/symbol, 16-QAM: 4 bit/symbol, 64-QAM: 6 bit/symbol ...
   6. MIMO? SISO?: MIMO: 2 spatial stream, SISO: 1 spatial stream
   7. QPSK?
   8. In MIMO channel corresponding matrix, higher rank => better to go for MIMO spatial multiplexing => higher data rate; lower rank => better to go for spatial diversity (high reliability)
   9. Round Robin(RR)? Max Carrier/Interference(MAX C/I)? Proportional Fair(PF)?
   10. Spatial Multiplexing increase the spectral efficiency.
   11. Comparing "reuse one"(Sharing all the bandwidth between all the transmitters), increasing the frequency reuse enables a better protection against interference.
   12. In CDMA, every signal that transmitter send should be orthogonal to each other(dot production equals 0)
   
## 10. two quiz

## 11. Calculation related modules
   1. M/M/1
    2. CDMA
    3. 64-QAM,8-QAM...
    4. MIMO, multiple-in-multiple-out,
    5. SISO: single-in-single-out, 1 spatial stream
    6. QPSK
    7. Dispersion Time in Optical Fibre
       1. Formula: DT=Dispersion coefficient (in ps/km/nm)  * fibre length (in km) * signal bandwidth (in nm).
       2. DCF: a kind of method to compensate the dispersion in the fibre
       3. Be careful, there are some conditions can be used in different parts of question...
       4. 比特率的倒数就是时间片(the reciprocal of the bit rate is the optical transmission's time slot duration)
   
## 12. Cognitive Radio and Self Organizing Networks
   1. Cognitive radio
      1. Evolution: Traditional Radios(firmware radios)=>software defined radios=> cognitive radios=>cognitive Networks
      2. CR: a radio that is aware of and can sense its environment, and can make decisions about its operating behaviour based on that information and pre-defined objectives
      3. Definition: A transceiver that is aware, adaptive, and capable of learning from experience
         1. "aware": of its own capability, of policies need to follow, of network conditions, of other users' priorities and authorizations, of the Radio Frequency environment 
         2. "adaptive": transmit power control, dynamic waveform selection, dynamic spectrum access, block edge masks, routing, negotiation of waveform and protocols
         3. "learning": experience-weighted table lookup, machine learning algorithm
      4. Cognitive applications
         1. Dynamic Spectrum Access(DSA)
         2. Cooperative medium access and cooperative communications
         3. Opportunistic switching among available wireless networks (cellular, WLAN, mesh, etc.)
         4. ...
      5. DSA
         1. major players: IEEE and other standard organizations
         2. Federal Communications Commission (US), Ofcom (UK), ComReg (Ireland) and regulators around the world
   2. Self organizing networks
      1. Characteristics of complex adaptive systems
         1.  Non-linearity: any small actions may cause unpredictable and unexpected events which have huge impacts to the whole system
         2. Emergence: The whole of the interactions becomes greater than the sum of the separate parts 
         3.  Dynamical systems change: Interactions within, between and among subsystems and parts are volatile, turbulent, and cascade rapidly and unpredictably.
         4.  Adaption: huge and complex task for system elements to respond and adapt to each other
         5.  Methods for modelling
             1.  Cellular Automata(CA)
                 1. Spatial lattice of cells
                 2. States
             2.  Agent Based Modelling (ABM)
                 1. Simplified entities within system interacting w/ each other
                 2. Signals and Rules
                 3. An ABM agent is anything that makes choices in a network
                 4. An ABM agent has its own goals and behaviours
                 5. An ABM agent operate in parallel with other ABM agents
   
## 13. Spectrum Sharing
### 1. Benefits of unlicensed
   1. Facilitating market entry
   2. Enabling niche applications or services to be addressed quickly and cheaply using existing technology and spectrum
   3. Providing certainty about spectrum access
   4. Security of tenure
   5. Reduced congestion in licensed bands
   6. The ability to extend the reach of fixed communication networks, by providing wireless local area connectivity in homes, businesses and at public traffic hotspots. 
### 2.WIFI(wireless Fidelity )
   1. Wi-Fi (Wireless Fidelity) is the wireless broadband data technology based on the IEEE 802.11 series of standards, whose main use is providing wireless broadband connectivity to fixed or mobile user devices. 
   2. WIFI: 1Gbps, MIMO
      1. 802.11n variant which may be either single (2.4 GHz) or dual band and incorporates additional enhancements such as MIMO antennas and the use of wider (40 MHz) channels
      2. 802.11ac=>notably the ability to use even wider channels (80 or 160 MHz), higher level modulation (256QAM) and up to eight MIMO streams to extend the theoretical over-the-air bit rate
   3. WIFI: M2M,<1GHZ
      1. 802.11ah=>802.11ah is primarily aimed at M2M and other relatively low bit rate applications
   4. WIFI:60HZ,>7GBPS
      1. 802.11ad, also referred to as Wi-Gig, operates in the 60 GHz millimetre wave band and is intended for very high speed, short range applications.
      2. The standard is expected to deliver speeds of up to 7 Gbps over ranges of up to 10 metres (MAX!!!!!)
   5. WiFi: 60GHz, >30Gbps
      1. 802.11ay is being developed by the IEEE and is aiming at data rates in excess of 30 Gbps. 
   6. 5GHz – the promised land of unlicensed capacity
   7. WIFI by range
      1. The largest range: 802.11 af
      2. The smallest range: 802.11ad(82.11ay)
   8. 5GHz-the promised land of unlicensed capacity.Reasons?
      1. The trade-off between capacity and coverage
      2. 60 GHz doesn’t offer useful coverage yet
      3. At these frequencies a small cell can serve a full room or a few rooms 

## 14. Metro-core networks
### 1. First generation of optical networks
   1. The optical transmission network was terminated by Electronic Cross Connects
   2. The IP topology was built on top of the E-XC links

### 2. IP-over-WDM proposition
   1. The idea is to remove the OXC and use the routers to terminate all traffic
   2. No need for L2 network(data link layer) as the IP transmits directly on top of WDM network
   3. The problem is that all traffic is terminated, every wavelength in the fibre needs a port in the router, and routers are very expensive..

### Second generation optical networks
   1. The Optical Cross Connect is the optical element that provides switching. The entire optical switching element is often referred to as Reconfigurable Optical Add Drop Multiplexer (ROADM)
   2. Ability to route entire optical channels at once
   3. Notice this only applies to channels that don’t need to operate add/drop
   4. Optical Cross Connects: a devices that switches light without converting it into digital electronic signal

### MPLS: deciding routes explicitly((i.e., tell exactly a packet what route it should follow))
   1. It creates deterministic paths for data to follow
   2. It’s a 2.5 layer, is a type of packet switching (e.g., like Ethernet) but it can operate at a global scale
   3. It’s a transport protocol, meaning that it can be used to transport different types of network protocols
   4. How MPLS work?
      1. use label distribution protocol (LDP) that gives each MPLS switch a label for the flow
      2. When an MPLS switch receives a packet
         1. it reads the MPLS label (only)
         2. It checks its switching table to identify the output port
         3. Before sending the packet it pops the MPLS label (the one agreed with the previous switch) and pushes a new MPLS label (the one agreed with the subsequent switch) – this operation is called label swapping 
   5. Forwarding Equivalence Class(FEC)
      1. The Forwarding Equivalence Class is the set of all IP addresses that get mapped into the same MPLS tunnel
      2. FECs are manually initiated by the operator
      3. MPLS was originally invented to speed up switching, as the smaller address space could make forwarding decisions faster
      4. However with the development of new ASIC and T-CAM memories IP routing could also be done fast (at line rate speed) so the speed advantage of MPLS became obsolete
      5. Thus the main application is for traffic engineering
   6. Ethernet frame
      1. Preamble (PRE): 7-byte sequence for frame synchronization
      2. Start-of-frame delimiter (SFD): 1-byte, defines the end of the PRE
      3. Destination Address (DA): 6-byte Ethernet destination address of the frame
      4. Source Address (SA): 6-byte Ethernet source address of the frame
      5. Length/Type: 2-byte, indicates either the length of the data field (up to 1500 bytes value) or the frame type (if value higher than 1536)
      6. Payload: 46 to 1500 bytes, carries the data
      7. Frame Check Sequence (FCS): 4-byte cyclic redundancy check
   7. Virtual LAN(VLAN)
      1. Virtual LANs allows to build multiple independent subnetworks on top of the same physical topology
   8. VLAN 802.1Q
      1. The 802.1Q adds a VLAN header to the Ethernet frame
   9. 802.1 ad(Q-IN-Q)
      1.  802.1ad (also called Q-in-Q) adds an extra tag to the Ethernet header
      2.  When the customer packet arrives at the provider it adds the S-VID (12- bit) which identifies that VLAN within the provider
      3.  The S-VID is removed before sending the packet to the destination end customer
   10. MAC-IN-MAC(802.1ah)
       1.  The idea of nesting was then extended to the Ethernet packet itself
       2.  It’s an interesting idea, but not used in practice because while Q-in- Q works with legacy switches, MAC-in-MAC requires new hardware

## 15. 5G and IoT
   1. Massive MTC
      1. Requirements
         1. architecturally simple devices that use a low-complexity transmission mode
         2. devices that can run on battery power for many years
         3. long transmission ranges for devices in remote locations
         4. scalable networks that can connect either a large or a small number of M2M devices
      2. Massive MTC refers to services that typically span a very large numbers of devices, usually sensors and actuators
         1. Sensors are extremely low cost and consume very low amounts of energy in order to sustain long battery life. Clearly, the amount of data generated by each sensor is normally very small, and very low latency is not a critical requirement
         2. Actuators are similarly limited in cost, they will likely have varying energy footprints ranging from very low to moderate energy consumption
      3. Critical MTC refers to applications such as traffic safety/control, control of critical infrastructure and wireless connectivity for industrial processes
         1. Such applications require very high reliability and availability in terms of wireless connectivity, as well as very low latency
      4. Low Power Wide Area Networks (LPWAN)
         1. A technology that supports small messages with specific duty cycles
         2. A technology that supports low power end nodes and hence long battery life (10 years)
         3. A technology that is suited to accessing sensors in awkward spots (in-building 500m-3km and rural up to 30km)
         4. A technology that has a cost point that suits the end applications
         5.  Supports the creation of public networks that serve multiple use and users
      5. LORA(unlicensed spectrum<1Ghz)
         1. 868 MHz technology (Europe)
         2. Spread spectrum based (very robust to noise)
         3. Bidirectional(双向的)
         4. 250 bps to 50 kbps
         5. Up to 154 dB link budget
         6. Battery based end-devices
      6. Sigfox(unlicensed spectrum<1Ghz)
      7. RPMA(ISM band,2.4GHZ)
      8. LTE NB-IOT(licensed spectrum)
      9. 5G capabilities
         1.  5G goal is to deliver 50Mbps everywhere;
         2.  5G will allow you to create your own network;
         3.  5G will deliver a single scalable solution for sensor networks and the IoT
         4.  G will enable an ultra-reliable network for mission critical applications;
         5.  5G will make the realization of the tactile internet possible
         6.  5G will deliver a meaningful and efficient broadcast service.
         7.  ...
      10. 5G three directions: enhanced mobile broadband,massive machine type communication, ultra reliable& low latency communications
      11. Massive machine type communications requirements importance: most connection density
      12. Ultra reliable & low latency communications requirements importance: most latency and mobility
      13. Network slices
          1.  A network slice is a connectivity service defined by a number of customizable software-defined functions that govern geographical coverage area, duration, capacity, speed, latency, robustness, security and availability.  
      14. SDN – Software Defined Networks
          1.  The benefit of SDN lies in its ability to provide an abstraction of the physical network infrastructure
          2.  The level of network programmability provided by SDN allows several network slices, customized and optimized for different service deployments, to be configured using the same physical and logical network infrastructure
          3.  NFV– Network Function Virtualisation
              1.  By separating hardware from software, NFV allows a network function to be implemented programmatically instead of by a physical piece of hardware
              2.  The most significant benefit brought about by NFV is the flexibility to execute network functions independently of location

## 16.Fixed access networks
   1. Statistical multiplexing
   2. Issues with access networks
      1. The issue is the cost per connection upgrade, which is on a per-user basis.
      2. This explain why many connections, especially in the rural areas are based on copper
   3. Twisted pair and coaxial
      1. Twisting the copper helps reducing interference from external sources
      2. However the coaxial uses external sheet to confine the radiation within the cable
   4. Capacity vs. distance of DSL
      1. The solution is obviously to reduce the distance of the copper link
   5. DSL details
      1. ADSL occupies up to 1.1 MHz bandwidth, using Discrete Multi-Tone Modulation (DMT - similar to OFDM) with 256 channels
      2. ADSL-2 also occupies up to 1.1 MHz bandwidth, using DMT but improving modulation efficiency
      3. ADSL-2+ occupies up to 2.2 MHz bandwidth, using DMT
   6. FTTC(fibre-to-the-cabinet)
      1. Replace the first part of the copper (that shared by most users) with fibre
   7. Now with FTTC, DSL works on the fast side, but the SNR is still high, which allows to develop also better technology
   8. FTTC's main feature is that a twisted copper pair is used in some part of the connection.
   9. VDSL/VDSL2
      1.  VDSL:A typical VDSL maximum rate is of 52 and 16 Mbps respectively in DS/US (ITU-G.993.1 year 2001), using frequencies up to 12 MHz
      2.  VDSL2: VDSL2 (ITU-G.993.2 year 2006), uses frequencies up to 30 MHz to achieve symmetric 100MB/s capacity
   10. G.FAST
       1.  G.fast increases the rate by using much larger bandwidth, up to 106 MHz;Notice that it overlaps with FM radio!
       2.  Initially targeting distances up to 250m, was then extended to up to 500m
       3.  This technology can work both for FTTC and FTTDp
   11. FTTDp(Fibre-to-the-distribution-point ) or FTTB(Fibre-to-the-building)
       1.  Replace the copper all the way to the DP (that shared by most users) with fibre
       2.  FTTDp technology
           1.  G.FAST
           2.  XG.FAST
           3.  Notice that in a building you could use Gigabit Ethernet or 10GE, but this means installing new Cat-5 or Cat-6 cables
   12. XG.fast::Towards 10Gb/s symmetric over very short copper distance
   13. FTTDp backhaul
       1. The closer you put fibre to the home the higher its cost
       2. FTTDp can provide very high rate, but how do we connect the DP to the central office? =? point-to-point fibre and Passive Optical Networks
   1.  Fibre-to-the-home (FTTH)
       1.  Replace the copper all the way to the house
       2.  No copper remains, and the user can avail of the full speed of optical technology
       3.  FTTH technology
           1.  Point-to-point fibre
           2.  Passive Optical Networks (PON) 
               1.  TDM-PON
               2.  WDM-PON
               3.  TWDM-PON
   2.  Point-to-point fibre
       1.  In a point to point fibre development each user is served by an individual fibre connection
       2.  The idea is simple: replace the copper with fibre and leave everything else as it is.
   3.  Passive optical network (PON)
       1.  It is expensive to deploy fibre solutions to the access as the cost of each connection is not shared among users
       2.  PONs were invented to reduce the cost for Capital (CAPEX) and Operational (OPEX) expenditures
       3.  It allows one network termination or Optical Line Terminal (OLT) to serve many Optical Network Units (ONUs) at the user side
   4.  Time Division Multiplexing PON (TDM-PON)
       1.  The protocol is based on TDM/TDMA
       2. Downstream and upstream channels
          1. Downstream transmission (OLT => ONU) is achieved through broadcast, the ONUs filter out the packets destined for them
          2. The downstream signal is continuous, and such receivers are not expensive.
          3. In the upstream direction a MAC is implemented to avoid collision of signals from different ONUs
          4. The access to the upstream channel is TDMA
   5. Dynamic Bandwidth Assignment(DBA)
      1. DBA is the process by which the OLT decides how to assign upstream transmission opportunities (e.g., bandwidth) to the ONUs
   6. Difference between GPON(Gigabit PON) and EPON(Ethernet PON) upstream
      1. GPON:Stricter specifications, rigid frame structure and strong QoS focus
      2. EPON: Looser standard definition, use of “packetized” Ethernet packets frame structure
      3. Duplex Scheme
         1. The most (economically) convenient duplex scheme is wavelength division duplex over single fibre, although two-fibre systems are allowed by the standard
      4. Split ratio
         1. Split ratio indicates the total number of ONUs that can be served by one OLT, i.e., the number of leaves of the PON tree
         2. Higher split ratio: Allow better cost sharing; Lower capacity per user; Increases the optical loss
      5. Security Issues
         1. The basic security problem with GPON, and other PONs based on power splitters is that messages are physically broadcast by the ONUs and filtered by the ONUs
   7. Wavelength division multiplexing PON(WDM-PON)
      1. In WDM-PON each user is served by a separate wavelength channel and a WDM splitter is placed in the cabinet to separate the wavelengths into different fibres
   8. Time/Wavelength Division Multiplexing PON (TWDM-PON)
      1. The concept is the same as the TDM-PON, but now multiple wavelengths are used over the fibre
   9. DOCSIS(Data Over Cable Service Interference Specification)
      1.  The cable network is different from the telephone network, as cable in not point-to-point, but is shared among a number of houses.
      2.  The standard for cable broadband is called DOCSIS (Data Over Cable Service Interface Specification).
      3.  This is a copper technology. But it utilizes a coaxial cable nested of a twisted copper pair!
   10. Access network sharing
       1.  Copper access
           1.   Local Loop Unbundling (LLU)
                1.   The local loop is the transmission medium from the central Office to the end user, hence the name
                2.   Local Loop Unbundling gives new operators (Other Licensed Operators –OLO) access to the network of the ex national operator (incumbent operator)
           2.  Sub Loop Unbundling (SLU)
               1.  LLU is useful for DSL, but technology like VDSL2 that use FTTCabinet need to share copper from the cabinet to the end user (i e., the sub-loop)
               2.  SLU then deals with sharing of the copper from the cabinet to the user
           3.  Bitstream
               1.  Bitstream access involves the creation of virtual circuits so that an OLO can offer broadband to an end user through a virtual circuit
               2.  The advantage is that the OLO does not need to provide physical infrastructure to terminate the copper lines
           4.  Virtual Unbundling Line Access (VULA)
           5.  Bitstream Next Generation Access (NGA)
       2.  Fibre access
       3.  So with bitstream access an OLO can provide services to an end user without owning access infrastructure. But The problem with bitstream is that it offers a standard rate connection to the OLOs without service differentiation
       4.  Virtual Unbundling Line Access (VULA)
           1.  VULA was born to allow OLOs to differentiate their product
           2.  In VULA, the OLO can put the interconnection in the central office, similarly to LLU
       5. Next Generation Access (NGA) Bitstream
          1. It provides a way for OLOs to avoid the need to interconnect at every Local Exchange, while offering better service than legacy bitstream
          2. Interconnection points can be Metro, Regional or National PoPs(入网点，point-of-presence)
          3. PON unbundling
          4. Wavelength-routed vs. power-split PON



