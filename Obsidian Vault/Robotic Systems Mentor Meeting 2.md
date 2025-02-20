31-10-2024

# Context 
Compare maximum frequency and data quality.
Keep increasing speed of the frequency to data freshness, find the threshold of frequency it works on. This is an initial plot, the first stage of IR communication.

Now, does the distance affect it? Minimum frequency on Y, distance on X and data freshness on Z. 

3 dimensional graph is the goal. The 2D graph of frequency vs data quality would be a simple step graph and pintless, it could be explained with a singe sentence. 

Single emitter pin for IR and bump sensors. Task scheduling is needed. 
The delay brought about by the task scheduling will be mitigated by PID. 

The error in the PID controller is the target distance. If the robot is too fast, error is too large frequency threshold is bypassed and the communication will break down. 

**relation between distance, frequency and speed.** 

# Next Week Goals 
Come up with an experimental plan, implementation plan - for starting with a straight line. 
Decide what useful amount of information is to be transferred.  