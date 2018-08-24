---
layout: page

sidebar:
    title: Tools
    navigation: tools

title: Schottky data analysis
data: 2018-08-06 14:20:00 +0800
author: SchoSpec
post_meta: false
permalink: /project/tools/data-analysis/
---

[code for data-analysis](https://github.com/SchottkySpectroscopyIMP/data-analysis){: .btn .btn-outline--primary .btn--small .grow}

The Schottky spectroscopy experiments highly rely on the algorithms useful fr Schottky data analysis. 
The repo presented in this page arts as a library of the functions for data analysis, which includes common spectral estimator and analysis methods, such as numerical calculation of <b>discrete prolate spheroidal sequence (DPSS)</b>, spectral density estimation of Schottky signal, <b>periodogram</b> with different windows, <b>multitaper</b>, and so on.

All the work may require the possession of basic *digital signal processing* knowledge at the graduate level to grasp the scientific rationale under the code.
However, for the users only want to obtain a nice plot of the Schottky power spectrogram, applying the code according to some basic parameters is enough. 

## Code design

The code includes three scripts written in `Python 3`. It is just a library of data analysis, you need to import it in our own script or notebook like `Jupyter`.

The functional scripts:

* `preprocessing.py`: reading the header and loading the data ([*details*](https://github.com/SchottkySpectroscopyIMP/data-analysis/wiki/Loading-Files){: .gray .hover-blue})
    - the module extract and parse the called data file as default.
        - `extract_wv()` is applied for the data files (one acquisition includes a `.wvh` file as header and a `.wvd` file as raw data) from the R&S device. 
        - `extract_tiq()` is applied for the data files (only a `.tiq` file for each acquisition) from the Tektronix device.
    - optional functions for the called data file are as following. 
        - `display()` is for printing all the data acquisition parameters onto the screen.
        - `load()` is for loading the data into memory. 
        - `draw()` is for plotting the signal in the in-phase and quadrature parts as a function of time.
        - `diagnosis()` is for checking the data by plotting them.
* `processing.py`: data analysis using several methods ([*details*](https://github.com/SchottkySpectroscopyIMP/data-analysis/wiki/The-Working-Horse){: .gray .hover-blue}) 
    - analysis methods: all methods provide two functions for results of 1d spectrum with windowed time series and 2d spectrogram with the whole acquisition time series.
        - `fft_1d()`, `fft_2d()`: FFT method <br/>
        computing the Fourier transform
        - `spectrom()`, `spectrogram`: FFT method <br/>
        computing the amplitude of the Fourier transform 
        - `periodogram_1d()`, `periodogram_2d()`: FFT method <br/>
        estimating the power spectral density with FFT method
        - `multitaper_1d()`, `multitaper_2d()`: multitaper method <br/>
        estimating the power spectral density with multitaper method
        - `adaptive_multitaper_1d()`, `adaptive_multitaper_2d()`: adaptive multitaper method <br/>
        estimating the power spectral density with adaptive multitaper method
        - `time_average_1d()`, `time_average_2d()`: can apply all the methods <br/>
        estimating the power spectral density with time average

    - plot methods
        - `plot_1d()`: 1d spectrum
        - `plot_2d()`: 2d spectrogram
    - error analysis
        - `confidence_band()`: return the <b>confience band</b> of the spectral density esimation at a given confidence level. 
* `DPSS.py`: generating <b>the Discrete Prolate Speroidal Sequenece</b> (<b>DPSS</b>), which is required for multitaper and adaptive multitaper methods.
    - `gen_sequences()`, `plot_sequences()`: generating the DPSSs, and plotting them in the time domain, respectively.
    - `gen_spectra()`, `plot_spectra()`: Fourier transforming the DPSSs into the frequency domain, and plotting the result, respectively.

## Usage

First of all is to ensure the followings are installed.

* `Python 3`
* `Scipy`, `Numpy`
* [`BLAS`](http://www.netlib.org/blas/) and [`LAPACK`](http://www.netlib.org/lapack/) libraries (*essential for matrix computation*)
* [`PyFFTW`](https://hgomersall.github.io/pyFFTW/) (*essential for FFT*)
* `Matplotlib` (*optional, only if visualization is needed*)
* `IPython` and `Jupyter` (*optional, only if presentation in a notebook is needed*)

Next is to create a *main* Python script or a `Jupyter` notebook and import all the codes as modules.

```Python
from preprocessing import Preprocessing
from dpss import DPSS
from processing import Processing
```
Reference [Wiki](https://github.com/SchottkySpectroscopyIMP/data-analysis/wiki){: .red .hover-blue} for more explanations about the class methods and arguments.

