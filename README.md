# DDB

This is a collection of diamond buffers implemented with discrete components. DDB thus stands for "Discrete Diamond Buffer".
The designs shared here are mostly dimensioned for driving headphones of average efficiency from bipolar 10V to 15V rails.

## Discrete Diamond Buffers

The diamond buffer is an output stage topology consisting of four transistors at its core. 
Two transistors form a traditional complementary push-pull emitter-follower/common-collector output stage. 
The other two transistors are configured as a complementary, folded, emitter-follower/common-collector driver stage.
The original patent for this topology (afaik) dates back to 1968 and was filed by Yee Seening of Sperry Rand Corp.

Diamond buffers in fact are everywhere, mostly as part of Current Feedback Amplifiers (CFAs), a subset of operational amplifiers.
The CFA was invented at Comlinear Corporation in the early 1980s and commercialized by both Comlinear Corp and Elantech.
Today CFAs are used for example as line drivers for DSL or video lines, but also in medical and other test equipment.

Both diamond buffers and CFAs have been popular among audio people for a while and a quick search will yield thousands of examples.
The audio field is also pretty much the only field where anyone bothers constructing this topology from discrete devices.
The reasons are quite obvious: Poor device parameter matching, little to no thermal tracking, high parasitic capacitances, ...

IC diamond buffers thus offer much higher bandwidths, usually better protection circuitry, lower offset ... just to name a few.

Case in point: Try competing with a cheap but beefy CFA like TPA6120A2 on performance or cost with a discrete design.
Doing one at a time is challenging at the very least, doing both at the same time is impossible.

## Design Philosophy / My Approach

In contrast to the vast majority of discrete diamond buffers out there, I exclusively use modern SMD components.
They are cheaper, smaller and simply the way forward but assembling these PCBs by hand takes some experience.

## The Buffers

I started with two basic designs. The first one is very basic and inspired by Walt Jung's articles in Electronic Design Magazine:

https://pearl-hifi.com/06_Lit_Archive/14_Books_Tech_Papers/Jung_W/Realizing_Good_Buffers.pdf

I chose to use identical transistors (e.g. PXT2907A/PXT2222A) for driver and output stage and employ three parallel output pairs.
Originally I chose to run all at the same current to establish similar operating points for better thermal stability and offset.
The high bias current in the driver stages however is somewhat wasteful and results in a buffer that is toastier than I prefer.
As far as the hardware implementation goes, I used a 4-Layer PCB with partly exposed VCC and VEE copper pours on the bottom layer.

The second version (bottom PCBs in picture) is sligthly more complex because the buffer is bootstrapped to the output.
It also has the collectors of the driver transistors connected to the emitters of the opposite output transistors.
Both these modifications aim to decrease distortion by introducing some form of local feedback.

![IMG_0166](https://github.com/PWieland/DDB/assets/65927363/5900f13f-ad8e-4c53-a13a-c2e7290ddf6c)
