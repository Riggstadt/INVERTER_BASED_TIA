# CMOS Inverter as simple Transimpedance Amplifier
## Purpose
With this project, I aim to use a CD4007UBE CMOS inverter IC as the basis for a simple photodiode amplifier. CMOS inverters are usually used for digital applications and are as a result most often either driven into the linear or cutoff region, as staying too long in the saturation region will draw too much power.

However, the inverter can also be used as a low-gain amplifier in its saturation region. This often undocumented property of the CMOS inverter is utilized to our benefit in this project.

## Theory and design process

The easiest way of finding the open loop gain of the inverter (when in saturation) is to plot what is called the "Voltage Transfer Characteristic", or the VTC curve. The slope of the curve in the region of saturation (recoghizable because of the curve's steepness) is the open loop gain of the inverter, when no or minimal loading is present and no forms of negative feedback are introduced.

After some small-signal approximations, we may, as depicted in <a href="">this</a> "The Signal Path" video, obtain a closed loop gain $A_{CL}$ equal to $-\(gm_{n}+gm_{p}\)\cdot\(r_{o,n}||r_{o,p}||R_{F}\)$. $R_{F}$ is the value of the feedback resistor, introduced to stabilize the bias point of the inverter to about $\frac{1}{2}\\;V_{DD}$. The feedback resistor should have a high value, as loading the inverter too much might lower the gain significantly.

The video linked above does not go into detail about the capacitive loading of the circuit, as the various parasitic capacitances present in a CMOS inverter are very low, on the order of picoFarads. However, for photodiode amplifiers the diode capacitance of the photodetector has a clear impact on performance. The simplest TIA is a bare resistor connected in series with a reverse biased photodiode. The resistive TIA has severe bandwidth issues, as its Bandwidth (BW) is restricted to $f_{-3dB}=\frac{1}{2\\;\pi\cdot R_{L}\\;C_{D}}$. 

Active TIAs(either the slower op-amp based ones, or the faster GHz-level transistor ones), have the advantage of higher linearity and greater Bandwidth.

In this short project, the Transimpedance amplifier is centered around a CMOS inverter, as depicted in the figure below.

[IMAGINE CIRCUIT SI CIRCUIT ECHIVALENT]

We may develop a simple transfer function for our inverter-based TIA, in order to gauge the extent of the amplifier's bandwidth. After some mathematical manipulations we obtain an approximate transfer function of the form: 

$$\frac{V_{o}}{I_{in}}=\frac{R_{F}\cdot \frac{G}{1-G}}{1+s\cdot\frac{C_{in}\\;R_{F}}{1-G}}$$

We've represented the negative gain of the CMOS inverter as $G=-A$, where A is the gain of the **loaded** CMOS amplifier.

## Design process
I had at my disposal the following appropriate components:
- 
