## 1. Why do we not see any PCB design with 90° traces?
For multiple reasons, PCB designers have been suggested to avoid using 90° traces. Here are a few of them:
- 90° traces are simply harder to manufacture. Such an angle causes the outside corner of the trace to be more narrowly etched than the standard width. This introduces impedance discontinuities sometimes.
- During the etching process, these 90° angles accumulate acid and hold onto it for a duration greater than what the design requires, this is called an "acid trap". This leads to all sorts of issues, but can be avoided with a simple vertical bubble etch.
- 90° traces affect signal integrity if the frequency of the signal is greater than GHz. This is due to the parasitic capacitance effect, high amount of signal reflections.
- You can route more traces in the same space using 45° angles, due to corners taking up more room.

References: 
https://resources.pcb.cadence.com/blog/2022-the-challenges-of-right-angle-pcb-traces
https://electronics.stackexchange.com/questions/226582/pcb-90-degree-angles
https://www.reddit.com/r/AskElectronics/comments/y1op3k/why_are_rightangle_tracks_in_pcbs_considered_to/

## 2. Why do we need an active low as well as an active high?
Active low refers to a pin that is activated when the voltage level is low, usually logic 0, which is near 0V. To activate an active low pin, you connect it to ground. 

Active high refers to a pin that is activated when the voltage level is high, usually logic 1, which is typically around 3.3V or 5V. To activate an active high pin, you connect it to your high voltage.

Active low signals were preferred when their use would reduce the number of gates in a PCB design, thus reducing their cost. Active low signals are also more tolerant of noise in some older devices. Active low is useful when a number of signals need to be "OR"ed together, used if the output is open drain/open collector.

References:
https://embeddeddesignblog.blogspot.com/2014/09/basics-why-active-low-signals-used.html
https://electronics.stackexchange.com/questions/60401/why-does-active-low-even-exist
https://www.reddit.com/r/AskElectronics/comments/2benae/is_there_any_advantage_to_using_active_low/

