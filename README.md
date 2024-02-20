# DDB

This is a collection of diamond buffers implemented with discrete components. DDB thus stands for "Discrete Diamond Buffer".

## Discrete Diamond Buffers

Diamond buffers are an output stage topology consisting of four transistors at its core. 
Two transistors form a traditional complementary push-pull emitter-follower/common-collector output stage. 
The other two transistors are configured as a complementary, folded, emitter-follower/common-collector driver stage.
The original patent for this topology (as far as I am aware) dates back to 1968 and was filed by Yee Seening of Sperry Rand Corp.

Diamond buffers in fact are everywhere, mostly as part of Current Feedback Amplifiers (CFAs), a subset of operational amplifiers.
The CFA was invented at Comlinear Corporation in the early 1980s and commercialized by both Comlinear Corp and Elantech.
Today CFAs are used for example as line drivers for DSL or video lines, but also in medical and other test equipment.

Both diamond buffers and CFAs have been popular among audio people for a while and a quick search will yield thousands of examples.
The audio field is also pretty much the only field where anyone bothers constructing this topology from discrete devices.
There are good reasons for this: Poor device parameter matching, little to no thermal tracking, high parasitic capacitances, ...

IC diamond buffers thus offer much higher bandwidths, usually better protection circuitry, lower offset ... just to name a few.

Case in point: Try competing with a cheap but beefy CFA like TPA6120A2 on performance or cost with a discrete design.
Doing one at a time is challenging at the very least, doing both at the same time is impossible.
