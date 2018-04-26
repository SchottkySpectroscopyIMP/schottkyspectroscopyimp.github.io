---
layout: page

sidebar:
    title: Platform
    navigation: platform

title: Data monitor
date: 2018-04-25 18:11:00 +0800
author: SchoSpec
post_meta: false
permalink: /project/platform/data-monitor/
---
[code for data-monitor](https://github.com/schottkyspectroscopyimp/data-monitor){: .btn .btn-outline--primary .btn--small .grow}

After collecting the data from the Schottky resonator, we can not get any visual result from the raw data itself. The display of the acquired data in real time is of importance to monitor the experimental status, and help to adjust the machine parameters according to the condition whenever necessary. It allows for an splendid feedback to optimize the beam-time utillizing efficiency to the maximum.

In our situation, a good data monitor may require as follows.
* displaying the results in a graphical user interface (GUI)
* able to promptly respond to the ambient changes (e.g. new files collected, user clicking a button, etc.)
* able to watch the changes of all collected data files

## Code design

* Establishing a GUI
    - `multithread.py`: a useful library to conduct multithread program for Qt.<br/>
    It uses *QRunnable* and *QThreadPool* to run the called module in another threads.
    It resets the signal for the called module in anther thread.
    - `monitor.ui`: a UI drawn by *QtCreator*.<br/>
    It contains all the static elements of our interface.
    - `monitor.py`: the main program to lanuch.<br/>
    It lists all the signal-slot functions for the interaction with users.
    The program imports `multithread.py` to deploy the interface displaying in the main thread and data processing in another thread.
    Also you need its accompanied `monitor.ui` to load the GUI elements.
* [Processing the result from the data (more details in another project)]()
    - `preprocessing.py`: to read the head file of the data and load the original data
    - `dpss.py`: a nice method to calculate *discrete prolate spheroidal sequeneces (DPSS)* for the signal processing
    - `processing.py`: several methods (e.g. various windows, [multitaper](https://en.wikipedia.org/wiki/Multitaper)) for signal processing (both 1D and 2D)

## Interface of the monitor 

![image](https://github.com/SchottkySpectroscopyIMP/data-monitor/blob/master/Monitor-GUI.png?raw=true)

Usage for the spectrum display

* Using the mouse wheel to zoom in or out for the waterfall spectrum and power spectrum.
* Drag the frame bar in the waterfall spectrum to change the frame display in power spectrum.
* The coordinate of the mouse will be shown at the lower left corner of the power spectrum.
* Click hided `A` button at the lower left corner of the waterfall spectrum if you wants to restore to the original display.


