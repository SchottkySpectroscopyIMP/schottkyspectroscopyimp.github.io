---
layout: page

sidebar:
    title: Platform
    navigation: platform

title: Data acquisition system
date: 2018-04-25 18:10:00 +0800
author: SchoSpec
post_meta: false
permalink: /project/platform/data-acquisition/
---
[code for data-acquisition](https://github.com/schottkyspectroscopyimp/data-acquisition){: .btn .btn-outline--primary .btn--small .grow}

For a Schottky resonator in the storage ring, the important measurement parameters of the beam are such as the revolution frequency, momentum spread of the ions, etc. Since these information is relative with the frequency domain. The data acquisition (DAQ) system of the resonator pays close attention to the frequency domain. A `spectrum analyzer` and an accompanied `storage hardware` is enough to form a simple DAQ system.

However, the DAQ system of the resonator focuses more on the measurement itself. To help with the experiments, the necessary parameters for the setting of it are as follows.
* `center frequency`: cohered to the specific parameters of the resonator (have a notable effect on the magnification of the spectrum)
* `span`: the range of spectrum, which you will get
* `reference level`: decide the precision of the spectrum's amplitude
* `duration`: the time of the collected data

Moreover, to accomplish the phyisics experiment of the long-time measurement, a DAQ system of the resonator may also meet the following requirements.
* stable and reliable long-time operation
* able to remote control
* uninterruptedly acquiring both large size and amount of data according to the setting
* real-time feedback of the progress of the DAQ processing

## Hardware

![Hardware](https://github.com/SchottkySpectroscopyIMP/data-acquisition/blob/master/wiki-pic/DAQ-Hardware.png?raw=true)

The whole system is based on a `spectrum analyzer` (R&S FSVR-7), an `IQR recorder` (R&S IQR-100), an independent `trigger system` and the `server`.

* [`spectrum analyzer`](https://www.rohde-schwarz.com/us/product/fsvr-productstartpage_63493-11047.html): digitizes the analog signal from the resonator, and filters it to the frequency range of interest
* [`IQ recorder`](https://www.rohde-schwarz.com/us/product/iqr-productstartpage_63493-11213.html): packs the data flow into files and exports them to the server
* <a href="#trigger">`trigger system`</a>: catch the trigger signal and sends a *triggered message* to the server
* `server`: control the whole system and stores the data files

<h3 id="trigger"> independent trigger system</h3>

[code for trigger-system](https://github.com/SchottkySpectroscopyIMP/ArduinoTriggerSystem){: .btn .btn-outline--primary .btn--small .grow}

![triggerSignal](https://github.com/SchottkySpectroscopyIMP/ArduinoTriggerSystem/blob/master/Pic/triggerSignal.png?raw=true)

![Circuit](https://github.com/SchottkySpectroscopyIMP/ArduinoTriggerSystem/blob/master/Pic/Circuit.png?raw=true)

![triggerSystem](https://github.com/SchottkySpectroscopyIMP/ArduinoTriggerSystem/blob/master/Pic/UnderTest_ArduinoYun.png?raw=true)

## Software

The software has two version, command-line interface (CLI) and graphical user interface (GUI).

<h3 id="CLI"> version 1. CLI</h3>

The first version was used in the beamtime of Dec. 2016 and Dec. 2017.

[code for data-acquisition-CLI](https://github.com/SchottkySpectroscopyIMP/data-acquisition/tree/cli-continuous){: .btn .btn-outline--primary .btn--small .grow}

![CLI](https://github.com/SchottkySpectroscopyIMP/data-acquisition/blob/master/wiki-pic/DAQ-Software_CLI.png?raw=true)

![CLIFlow](https://github.com/SchottkySpectroscopyIMP/data-acquisition/blob/master/wiki-pic/DAQ-Software_CLI_flow.png?raw=true)


<h3 id="GUI">version 2. GUI</h3>

The second version has been used from the beamtime of Jan. 2018 until now.

[code for data-acquisition-GUI](https://github.com/schottkyspectroscopyimp/data-acquisition){: .btn .btn-outline--primary .btn--small .grow}

![GUI](https://github.com/SchottkySpectroscopyIMP/data-acquisition/blob/master/wiki-pic/DAQ-Software_GUI.png?raw=true)

![GUIFlow](https://github.com/SchottkySpectroscopyIMP/data-acquisition/blob/master/wiki-pic/DAQ-Software_GUI_flow.png?raw=true)
