# pyTHM1176
Python interface to Metrolab 3 axis Hall probe THM1176

This interface is incomplete and only implements acquisitions in "continuous mode". It is however easy to add the different functionalities of the probe to the API module. Contributions are welcome. We hope this can help others.

It has been verified to work with Python 3.6 under Windows 10 and under Ubuntu 16.04 LTS

# Dependencies
This has been tested with Python 3.x
You will need to install the following packages:
- [python-usbtmc](https://github.com/python-ivi/python-usbtmc) (required if not using pyVISA)
  - pyUSB (installable using pip, [documentation](http://pyusb.github.io/pyusb/))
- [pyVISA](https://github.com/pyvisa/pyvisa) (required if not using python-usbtmc, installable using pip)
  - NI-VISA (Download from NI website)
- numpy
- matplotlib for the logging example

# Installation
This isn't packaged for pip or conda yet. Not even a setup.py. Install is manual. Either clone the repo and run the examples/tests, or include the package in your project and start coding your application.

The interface relies on either pyVISA or python-USBTMC for the backend.
python-usbtmc is by far the easiest to use.
pyVISA backend has been implemented as a legacy item and we thought some people might like to keep using VISA
However, there is very limited support of the VISA library in Linux and using python-usbtmc is the best approach under Linux.
python-usbtmc can be used under Windows but requires to make sure of using libusb to drive the THM1176 communications. This can be done conveniently with the tool [Zadig](https://zadig.akeo.ie/)

We believe python-usbtmc is the most lightweight approach as it requires minimal software download and install (compared to the NI-VISA behemoth), and no reboot at all. You don't even need to install the Metrolab drivers.

## Windows
* pyVISA
  1. Install NI-VISA.
  2. You may have to set the usb driver of the tHM1176 to the IVI VISA USB driver see [here](https://knowledge.ni.com/KnowledgeArticleDetails?id=kA00Z0000019La2SAE) for instructions.
  3. Install pyVISA (using pip).
  4. Install numpy and matplotlib using conda or pip.
  5. Clone the repo and run the example `log_thm.py`.

* python-usbtmc. 
  1. Install pyUSB using pip.
  2. Install python-usbtmc using pip.
  2. Install [Zadig](https://zadig.akeo.ie/). 
  3. After plugging the THM1176 in, run Zadig and change the driver of the Metrolab probe to libusb.
  4. Install numpy and matplotlib using conda or pip
  4. Clone the repository and run the example `log_thm.py`.

## Linux
pyVISA doesn't work well on standard distributions like Ubuntu. There is a pure python version that doesn't rely on the binaries released by NI but it has performance issues. We have found it is much better to run on the usbtmc backend directly.

Install dependencies listed above, based on python-usbtmc. Refer to the python-usbtmc [documentation](http://alexforencich.com/wiki/en/python-usbtmc/readme). There are detailed explanations about what needs to be done in udev to make the device accessible in case you have permission issues.

# Things to do
* Make the API feature-complete for both VISA and usbtmc backends.
* Make the switch between VISA and usbtmc more seamless, for example with a switch in a parameter file. 
* Improve maintainability by using a single API module that can interact with both backends.
* Create a conda and/or pip package
* Add unit tests
