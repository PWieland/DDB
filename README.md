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
They are cheaper and smaller but assembling these PCBs by hand takes some experience. 

## The Buffers

I started with two basic designs. Both were designed to be used with 25x25mm heatsinks glued to the back.

### The Walt-Jung inspired classic, with LED-based current sources and triple output pairs

The first one (top PCBs in picture) is very basic and inspired by Walt Jung's articles in Electronic Design Magazine:
https://pearl-hifi.com/06_Lit_Archive/14_Books_Tech_Papers/Jung_W/Realizing_Good_Buffers.pdf

<img width="1217" alt="image" src="https://github.com/PWieland/DDB/assets/65927363/93e6639d-ad2f-421e-8aae-9243687e30ba">

I chose to use identical transistors (e.g. PXT2907A/PXT2222A) for driver and output stage and employ three parallel output pairs.
Originally I chose to run all at the same current to establish similar operating points for better thermal stability and lower offset.
The high bias current in the driver stages however is somewhat wasteful and results in a buffer that is toastier than I prefer.
As far as the hardware implementation goes, I used a 4-Layer PCB with partly exposed VCC and VEE copper pours on the bottom layer.

### Bootstrap version

The second version (bottom PCBs in picture) is sligthly more complex because the buffer is bootstrapped to the output.
It also has the collectors of the driver transistors connected to the emitters of the opposite output transistors.
Both these modifications aim to decrease distortion by introducing local feedback, which also introduces a tendency to oscillate.
Fixing stability issues will often cost bandwidth, which is especially critical if the buffer is to be used in a feedback loop.
In my limited experience the more sophisticated variants tend to fall short of their promises, both in simulation and reality.

![IMG_0166](https://github.com/PWieland/DDB/assets/65927363/5900f13f-ad8e-4c53-a13a-c2e7290ddf6c)

A more compact version of the bootstrapped buffer, using a 20x20x10mm heatsink.
It also features CRDs (Current Regulator Diodes) instead of discrete JFET current sources.
The diode can easily be substituted by a resistor, avoiding the somewhat exotic CRD.

![IMG_1712](https://github.com/PWieland/DDB/assets/65927363/e94fc26d-e403-4591-9036-c352ff144fc7)

## Performance

I designed these buffers to be used within the feedback loop of OpAmps to drive headphones with vanishingly low distortion levels.
For basic testing of this configuration, I designed a dual channel test board with the OpAmps configured as differential amplifiers.
To achieve the best possible performance, as little as possible of the OpAmp's loop gain may be "wasted" throughout the audio band.
Therefore, it is recommended to apply two-pole-compensation schemes instead of single-/dominant-pole compensation schemes.

![IMG_1713](https://github.com/PWieland/DDB/assets/65927363/e38ad0f8-9381-40a7-a4e8-a1718934670b)

The "classic" diamond buffer inspired by Walt Jung combined with LME49720, driving 1kHz@2Vrms into 50Ω.
The buffer was running fairly hot at about 10mA per transistor on +/- 12V rails. 
The actual load resistance is slightly lower than 50Ω, due to the fairly low impedance of the Cosmos ADC used for measurement.
Under these conditions, the output stage is operating at the upper end of its Class A region.

![newhpa](https://github.com/PWieland/DDB/assets/65927363/272459f1-a2bf-4d2a-9d27-d979934ba07c)



