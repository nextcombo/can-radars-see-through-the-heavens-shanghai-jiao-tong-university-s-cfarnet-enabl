# Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]

Is radar capable of "seeing through the heavens"? Shanghai Jiao Tong University's CFARNet: Let mmWave radar see multiple targets closely by face
Hello everyone, this is EW Frontier.
Today, let's talk about a recent paper from the team led by Tao Meixia at Shanghai Jiao Tong University, published in arXiv - CFARNet. This innovative work uses CNN to directly replace the traditional radar's "bottleneck" CFAR, enabling mmWave Rainbow Beam Radar to accurately measure distance, speed, and angle even in low power and multi-target close-to-face scenarios, with a speed increase of over 100 times.
This article will be presented in plain language with humorous anecdotes, making it easy to understand the cutting-edge innovation of 6G integrated senses without needing to delve into complex formulas.
Firstly, let's address the pain points: why do traditional radars "blind themselves when they get too close?" Picture yourself using mmWave radar to scan a crossroads:
Cars, people, and electric vehicles are crowded together, with only a 1° or 1.5° difference in angle
The transmitting power is not high, and the signal-to-noise ratio is very low
Traditional solutions: CFAR detector + MUSIC superresolution
The problem lies in the CFAR step:
It relies on calculating thresholds based on surrounding clutter, which gets "blurry" as targets crowd in
Strong targets mask weak ones, leading to direct missed detections
In non-uniform clutter, false alarms and wrong detections fly everywhere
The result is that: **two closely spaced targets → mistaken for one; weak targets → disappear completely; low signal-to-noise ratio → parameters estimated wildly off.**
This is the real pain point of 6G integrated senses (ISAC): broadband fast scanning + multi-target denseness = traditional CFAR can't handle it.
Secondly, Rainbow Beam Radar: Fast and fierce, but more "selective for detectors"
This uses phase time-varying array PTA + Rainbow Beam mmWave OFDM radar.
Simply put:
Different subcarriers → pointing at different angles
A single OFDM symbol → scanning large angles in one go
No need for repeated beam scanning, with extremely low delay and suitability for 6G
However, it's great, but it's more demanding on peak detection: angle information is directly tied to subcarrier index, if the peak is not found correctly → angle measurement is incorrect → the whole process crashes down.
Traditional CFAR here, directly turned into performance ceiling.
III. What exactly did CFARNet do? In a nutshell, it discarded CFAR and replaced it with a pre-trained CNN, specifically designed to "find peaks" on the angle-Doppler plot.
The entire process is incredibly intuitive:
1  
Backscatter signal → FFT → Angle - Doppler spectrum
2  
Take the logarithmic magnitude → feed into CFARNet
3  
Directly output the probability of each subcarrier being the target peak.
4  
Extract Top-K peak → Use rainbow beam's frequency - angle mapping to calculate the angle.
5  
Use MUSIC to calculate distance and velocity in the small frequency band.
In a nutshell: CFARNet = the "super CFAR" learned, specifically designed to tackle dense multi-target scenarios and low signal-to-noise ratios.
IV. CFARNet Network: What is its appearance and how to train? There are no need to remember layers, focus on three key points:
1. Network structure input: Angle - Doppler log spectrum
Subject: 4 sets of 2D convolutional blocks, extract features and compress multi-Doppler vectors.
Output: The logit vector of length M, where each dimension corresponds to the confidence of a subcarrier being "peak"
2. Training trick is very essential, no need to use hard one-hot encoding, instead use Gaussian label smoothing:
Draw a small Gaussian envelope near the real peak.
Network learning: "The surrounding area is like a peak," more robust, not sticking to the point.
Loss function: BCEWithLogitsLoss, end-to-end training, simple and stable.
3. The deduction is extremely simple: just input a piece of music.
A series of scores come out.
Select the top K positions with the highest scores → These are the target subcarriers.
Ten times more convenient than traditional CFAR with sliding windows, estimation of clutter, and calculation of thresholds.
V. Results: BOOM! Low power + 5 targets with face-on, error difference by two orders of magnitude. The paper conducted full-configuration comparisons against the YOLO baseline using CFAR+MUSIC.
1. Minimum angle of approach (1°) + Lowest power 45dBm: 90th percentile angle error 0.056°
Baseline: 0.283° → Precision 5 times
2. Hell Difficulty: 5 targets clustered together baseline directly collapses with corner error of 15.83° and distance error of 17.28m
CFARNet: Steady as a veteran dog: Angle 0.08°, distance 0.85m → Accurate by nearly 200 times, distance accurate by 20 times +
3. Hyper-speed GPU: Single sample 7.6ms
CPU: 75.8ms  
Traditional baseline CPU: 1.26s → fastest, 166 times faster, also 16 times faster for the CPU.
One sentence: With a large number of people, close faces, and dim lighting (low power), CFARNet can still clearly identify who is who.
VI. Why is this important? The key step in 6G's integration of communication and radar:
Shared hardware, shared spectrum
Vehicles, drones, industrial perception rely on it.
In millimeter-wave multi-target dense scenarios, CFAR has always been a bottleneck.
CFARNet provides a feasible path:
Replace manual signal processing modules with data-driven ones.
Preserve mature algorithms like MUSIC, without starting over.
Accuracy, robustness, and speed all achieved
This is the "notebook" within the integrated sense of sensation and perception: neural networks for pattern recognition, traditional algorithms for precise calculations, 1+1>2.
VII. Minimal Summary (Can be used to chat about after watching) Question: Traditional CFAR underperforms in dense multi-target + low signal-to-noise ratio scenarios.
Solution: CFARNet, replace CFAR with CNN for angle - Doppler peak detection.
Highlights: High-precision Gaussian label smoothing, end-to-end training, and ultra-fast inference.
Effect: Nearly two orders of magnitude improvement in corner resolution, speed up by a factor of 100.
Meaning: A new paradigm of multi-target real-time perception with 6G millimeter wave communication and sensing integrated.
Paper Information: CFARNet: Learning-Based High-Resolution Multi-Target Detection for Rainbow Beam Radar
Authors: Qiushi Liang, Yeyue Cai, Jianhua Mo, Meixia Tao
Institution: School of Electronic Engineering, Shanghai Jiao Tong University

Interactive: Do you think replacing traditional signal processing modules with CNNs will become the mainstream trend in radar / communication? Share your thoughts in the comments section!
Follow EW Frontier to continuously bring you the most straightforward interpretations of cutting-edge topics such as 6G, integrated sensory and communication, and semantic communication.

## Images

![Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]](01.jpg)
![Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]](02.jpg)
![Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]](03.jpg)
![Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]](04.jpg)
![Can radars "see through the heavens"? Shanghai Jiao Tong University's CFARNet: enabling millimeter-wave radar to see multiple targets close up. [Includes Python code]](05.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
