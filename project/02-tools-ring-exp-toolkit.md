---
layout: page

sidebar:
    title: Tools
    navigation: tools

title: Ring experiment toolkit
date: 2018-04-25 18:15:00 +0800
author: SchoSpec
post_meta: false
permalink: /project/tools/ring-exp-toolkit/
---

[code for ring-exp-toolkit](https://github.com/SchottkySpectroscopyIMP/ring-exp-toolkit){: .btn .btn-outline--primary .btn--small .grow}

During a heavy-ion experiment at storage ring, a specific calculator to estimate certain beam kinetic parameters for beam tuning or strategy planning in a timely manner is also in high demand. This toolkit uses the <b>CSRe@IMP</b> as the example ring to realize the functions of the special calculator. It can easily be adapted to other storage rings by changing the machine parameters to their particular values as well.

## Code design

The code are two scripts written in `Python 3`. Using a `IPython` or its optional `Jupter` notebook for interactive processing may be a perfect choice.

The functional scripts:

* `utility.py`: beam calculator
    - using the certain center frequency and span for the Schottky resonator, to get the ion's velocity (β and γ), revolution frequency, magnetic rigidity, kinetic energy as well as the peak location in the Schottky spectrum
* `ion_id.py`: ions identification
    - estimate the location and strength of an ion signal given the [LISE++](http://lise.nscl.msu.edu/lise.html) simulation result
    - filter out the unqualified ion candidates owing to the low yields and/or the short half-lives
    - identify ions given a Schottky spectrum with multiple peaks

## Usage

The first of all is to ensure the followings are installed.

* `Python3`
* `Numpy`, `Pandas`, `IPython`/`Jupter` (*optional*)

The next is for the required `.txt` files.

* `mass16.txt` - [atomic mass database](http://amdc.in2p3.fr/masstables/Ame2016/mass16.txt)
* `nubase2016.txt` - [atomic half-life database](http://amdc.in2p3.fr/nubase/nubase2016.txt) 
* LISE++ simulation files (*only for the ion identification*)

Now, it is the time for the interaction in the environment of `IPython`. The following is a example.

input:
```Python
# the beam calculator
import utility as _util
util = _util.Utility(242.9, 500) # center frequency in [MHz], span in [kHz] 
util.set_ion("58Ni19")           # the target ion
util.set_L_CSRe(200)             # circumference in [m]
util.set_energy(186.3)           # kinetic energy in [MeV/u]
```
output:
```Python
target ion              58Ni19+
γ                       1.2
β                       0.552771
Bρ                      6.28344 Tm
kinetic energy          186.299 MeV/u
ring circumference      200 m
revolution frequency    0.828583 MHz
center frequency        242.9 MHz
span                    500 kHz
peak location(s)        -125 kHz
harmonic number(s)      293
```
input:
```Python
# ion identification
import ion_id as _iid
iid = _iid.IID("58Ni28.lpp", 242.9, 800) # center frequency in [MHz], span in [kHz]
```

output:
```Python
center frequency        242.9 MHz
span                    800 kHz
orbital length          128.8 m
Bρ                      5.47156 Tm

Weight    Ion      Half-life   Yield     Rev.Freq. PeakLoc. Harmonic
2.50e+09  58Ni28   stbl        1.40e+06  1.508789   15      161
1.42e+07  56Co27   77.236 d    8.56e+03  1.507636  -171     161
4.64e+06  54Fe26   stbl        3.02e+03  1.506473  -358     161
8.18e+05  57Co27   271.70 d    5.04e+02  1.492147   320     163
7.17e+05  47V23    32.6 m      5.86e+02  1.520519   383     160
5.26e+05  45Ti22   184.8 m     4.71e+02  1.519651   244     160
4.62e+05  46Ti22   stbl        4.24e+02  1.500514   183     162
3.83e+05  43Sc21   3.891 h     3.76e+02  1.518705   93      160
2.75e+05  41Ca20   99.4 ky     2.99e+02  1.517706  -67      160
2.71e+05  55Fe26   2.744 y     1.80e+02  1.490373   31      163
```
## Notice

Interesting?<br/>
Go and enjoy a scientific journey with our [freshman Alice (*beam calculator*)](https://github.com/SchottkySpectroscopyIMP/ring-exp-toolkit/wiki/Beam-Physics-Calculator){: .red .hover-blue} and [summer school student Bob (*ion identification*)](https://github.com/SchottkySpectroscopyIMP/ring-exp-toolkit/wiki/Ion-Identification){: .red .hover-blue} to learn more~ :)

