# RF_Power_Measurements_Using_Scope

<p align="center">
<img src="./img/measurement_hints.jpg" width="1000" height="600"/>
</p> 

## Setup overview

When using osciloscope to measure output power we rather measure voltage level on known resistive dummy load (low reactance) and then use simple formulas to convert obtained results to power in Watts or dBm's.

Measuring power levels exceeding a few dBm's requires (!) attenuator/RF Tap to limit signal level reaching used osciloscope.

It shall be aslo stressed that to obtain results, which can be compared with formal specifications, we shall always use sinusoidal waveform stimulus.
In case of HF transceivers, this requires switching to CW mode since for both SSB/USB modes carrier has been surpressed. 
Most formal RF device specifications would refer to RMS Power when specifying device output power.

Moreover when using osiloscope to measure output power it is very important to ensure that both output of the device under test (on the picture above we use functional generator) and the output of the rf tap/attenuator are matched to 50ohm. Most budget scopes will have output impedance in the range of 1Mohm, that is why we cannot connect such scope directly to rf tap output and instead must use tee adapter with one of the outputs termninated with 50ohm low power dummy load (see hint #2) and another one connected to our osciloscope. Most functional generators do have option to select device output impedance, in our case we need to set it to 50ohm. Connecting osciloscope to the output of the functional generator does not impact measurement results since again input impedance of the scope is in the range of 1Mohm i.e. is much greater then output impedane of the generator or device under test (see hint #1). Of course we assume that dummy load, attenduator/rf tap, and cabeling are all 50ohm as well.

Characteristics of the load used during power measurments can heavily impact results! That is why even the best antenna cannot replace the proper dummy load!

When measuring high power levels (above 50W/47dBm), limit the time dummy load is subjected to such power. Prolonged exposure to high power levels do impact dummy load characteristics and ultimately cause permanent damage.

## Useful Formulas

<p align="center">
<img src="./img/Sinwave.jpg" width="600" height="400"/>
</p>

where:

$Upp$ - Peak to Peak Voltage

$Up$ - Peak Voltage

$Urms$ - Root Mean Square Voltage 

$Up = Upp / 2$

and for sinusoidal voltage:

$Urms = \frac{Up}{\sqrt{2}}$

$P=U * I$

Power dicipating on the load R:

$Pp = \frac{Up^2}{R}$

$Prms =  \frac{Up^2}{2*R}$

Voltage occuring on the load R for given power level:

$Up = \sqrt{Pp*R}$

or

$Up = \sqrt{2 * Prms * R}$

To convert power given in Watts to dBm we use:

$P[W] = 10^{\left(\frac{P[dBm]}{10} - 3\right)}$

To convert power given in dBm to Watts we use:

$P[dBm] = \log{\frac{P[W]}{0,001}}$


### Measurement example

We measure sinusoidal waveform supplied by functional generator set to ouput power of 1dBm. Coresponding osciloscope readings have been shown below:
Blue wave represents functional generator output [Uin/Pin], while yellow cureve is an generator output attenuated by 40dB [Uout/Pout].
<p align="center">
<img src="./meas/Combined_DSO_2024-05-11 11-47-25.png" width="600" height="400"/>
</p>
<p align="center">
<img src="./meas/Uin_DSO_2024-05-11 11-46-20.png" width="400" height="200"/>
<img src="./meas/Uout_DSO_2024-05-11 11-46-20.png" width="400" height="200"/>
</p>

$Uinpp = 6.4V$

$Uoutpp = 64.8mV$

$Uinp = Uinpp / 2 = 3.2V$

$Uoutp = Uoutpp / 2 = 32.4mV$

$Pinrms =  \frac{Up^2}{2*R} = 0.1024W$


$Poutrms =  \frac{Uoutp^2}{2*R} = \frac{(32.4^10-3)^2}{2*50} = 1.05*10-5W$

## References

[1] [The definitive guide to RF Power measurement](<https://qrp-labs.com/qcx/rfpower.html>)


