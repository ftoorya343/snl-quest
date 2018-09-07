<img src="es_gui/resources/logo/Quest_Logo_RGB.png" alt="QuESt logo" width=300px margin="auto" />

# QuESt: Optimizing Energy Storage
Current version: 1.0

## Table of contents
- [Introduction](#intro)
- [Getting started](#getting-started)
- [QuESt Data Manager](#quest-data-manager)
- [QuESt Valuation](#quest-valuation)

### What is it?
<a id="intro"></a>
QuESt is an open source, Python-based application suite for energy storage simulation and analysis developed by the Energy Storage Systems program at Sandia National Laboratories, Albuquerque, NM. It is designed to give users access to models and analysis for energy storage used and developed by Sandia National Laboratories. It's designed to be transparent and easy to use without having to have knowledge of the mathematics behind the models or knowing how to develop code in Python. At the same time, because it is open source, users may modify it to suit their needs should they desire to. We will continue developing QuESt and its applications to enable more functionality.

#### QuESt Data Manager
An application for acquiring data from regional transmission operator (RTO), independent system operator (ISO), or other electricity market operating entities. Data selected for download is acquired in a format and structure compatible with other QuESt applications.

*Note: An internet connection is required to download data.*

*Note: Certain data sources require registering an account to obtain access.*

#### QuESt Valuation

An application for energy storage valuation, an analysis where the maximum revenue of a hypothetical energy storage device is estimated using historical market data. This is done by determining the sequence of state of charge management actions that optimize revenue generation, assuming perfect foresight of the historical data.

### Who should use it?
The software is designed to be used by anyone with an interest in performing analysis of energy storage or its applications without having to create their own models or write their own code. It’s designed to be easy to use out of the box but also modifiable by the savvy user if they so choose. The software is intended to be used as a platform for running simulations, obtaining results, and using the information to inform planning decisions. 

## Getting started
<a id="getting-started"></a>

### Requirements
* Python 3.6+
* Kivy 1.10.1+ and its dependencies
* Solver compatible with Pyomo

### Installation
You will want to obtain the codebase for QuESt. You can do that by either cloning this repository or downloading a compressed archive of it by clicking the "Clone or download" button on this page. We recommend keeping the QuESt files in a location where you have read/write permission. Once you have the codebase, follow the appropriate set of instructions for your operating system.

#### Windows
1. Install Python 3.x, preferably via scientific distribution such as [Anaconda](https://www.anaconda.com/download/). Use the 64 or 32-Bit Graphical installer as appropriate.
2. Install Kivy. Check [here](https://kivy.org/docs/installation/installation-windows.html) for the latest instructions. From the Anaconda Prompt or other Command Prompt where Python is recognized:
  1. Ensure you have the latest pip and wheel:
  ``python -m pip install --upgrade pip wheel setuptools
  ``
  2. Install the dependencies:
  ``python -m pip install docutils pygments pypiwin32 kivy.deps.sdl2 kivy.deps.glew
  ``
  3. Install kivy:
  ``python -m pip install kivy
    ``
3. Navigate to the root directory of the codebase. Then run the setup
 ``python setup.py develop`` This will check dependencies for QuESt and install them as needed.
4. Install a solver for Pyomo to use. See other sections for instructions on this.

##### Installing GLPK
1. Download and extract the executables for Windows linked [here](http://winglpk.sourceforge.net/).
2. The .dll and glpsol.exe files are in the `w32` and `w64` subdirectories for 32-Bit and 64-Bit Windows, respectively. These files need to be in the search path for Windows. The easiest way to do this is to move those files to the `C:\windows\system32` directory.

##### Installing IPOPT
1. Download and extract the pre-compiled binaries linked [here](https://www.coin-or.org/download/binary/Ipopt/). Select the latest version appropriate for your system and OS.
2. Add the directory with the `ipopt.exe` executable file to your path system environment variable. For example, if you extracted the archive to `C:\ipopt`, then `C:\ipopt\bin` must be added to your path.

### Running QuESt
From the Anaconda Prompt or Command Prompt, run:
```
python main.py
```

Alternatively, run ```main.py``` in a Python IDE of your choice.

**NOTE: The current working directory must be where ``main.py`` is located (the root of the repository).**

## QuESt Data Manager
<a id="quest-data-manager"></a>

### Frequently Asked Questions

> I am connecting to the internet through a proxy, such as on a corporate network. How should I configure my connection settings?

Typically, devices have their connection settings configured for the network they will primarily residing on. For example, proxy settings may already be configured in system environment variables and whatnot. We recommend that your proxy settings be configured at the operating system level and that you do not additionally specify using a proxy in QuESt settings. In our experience, additionally specifying the same proxy settings in QuESt "does no harm," but your mileage may vary.

> I am trying to download data and am receiving many messages about connection errors, timeouts, etc. What should I do?

We found these issues to be very network dependent and hard to diagnose or mitigate against. The best practice would be to limit the amount of data that you request at a time. Additionally, QuESt Data Manager is configured to skip data that is already downloaded so you can just issue the same request to patch up any data that may have failed to download.

> How do I obtain PJM Data Miner 2 API access?

Refer to the instructions in QuESt Data Manager or see the API guide [here](http://www.pjm.com/markets-and-operations/etools/data-miner-2.aspx).

<!-- > How do I obtain an ISO-NE ISO Express account?

Refer to the instructions in QuESt Data Manager or simply register an account at ISO-NE's [website](https://www.iso-ne.com/). Make sure to sign up for Data Feeds access. -->

> Why can't I download [data for which no option in QuESt Data Manager exists]?

RTO/ISO/etc. provide a lot more varieties of data than what is shown in QuESt Data Manager. We are focused on acquiring data necessary for other QuESt applications to function. Additionally, acquiring data is not the fastest process. In order to improve the user experience, we decided to limit the amount of data that one can request at a time. For that reason, we have limited the number of pricing nodes for which data can be requested directly. (For reference, PJM has over 11,000 pricing nodes.) We can consider lifting some of these limitations if requested.

## QuESt Valuation
<a id="quest-valuation"></a>

### Frequently Asked Questions

> I am getting import errors when trying to run QuESt.

The current working directory must be where ``main.py`` is located.

> Why are only [x] options available for market areas/historical data/revenue streams/etc.?

These options are based on the data that you have downloaded through QuESt Data Manager. Download more varieties if you wish to use them!

<!-- > I downloaded data for MISO but it's not appearing as an option under QuESt Valuation sections. What gives?

Depending on the amount of data downloaded, it may take a long time for the software to complete scanning and cataloging the data that you have. At the moment, that process is performed concurrently in the background when QuESt is launched so it may not be complete by the time you open a section that requires that information. We are looking into options for making this experience less jarring. -->

> I'm getting solver errors/QuESt is crashing when building optimization models. How can I fix that?

Our experience indicates that most crashes are due to data issues. For example, data for a month is missing unexpectedly, disallowing the model building process from completing. We make every effort to limit these incidents from happening, but it is difficult to perfectly predict the data that we need to design around. We will try to handle these exceptions as best we can as we learn more about the common situations.

> The appearance of GUI elements in QuESt do not appear correct/The window does not display properly.

There appears to be a display issue with certain displays causing GUI elements such as buttons and text to not be displayed as they were designed to be. This appears to be a scaling issue and has most commonly been observed on Apple Macbook Pros. One solution for this issue is to connect to an external display and run QuESt on it.

QuESt is designed to be displayed at minimum resolution of 1600x900. The window size may be increased but many GUI elements, such as fonts, may not scale accordingly.

> An electricity market area I want to do analysis on isn't available. When will it be available?

The development team is working on modeling and doing analysis for the remaining market areas. When we have vetted the results and viability of data acquisition and processing, we will work on implementing them into QuESt. Please look forward to it!

#### Wizard

> I selected [x] year for my historical dataset and only [y] months had results after the optimization. Why is that?

Due to (rolling) data availability, data for certain periods may be absent. For example, ERCOT's 2010 data only starts at December or data sets for the current year will obviously be incomplete. There's also the possibility that the data failed to download.

> Why can I only adjust [x] parameters for my energy storage device?

To streamline the user experience in the Wizard, we decided to reduce the range of options available. Please try the "Single Run" and "Batch Runs" interfaces for fuller flexibility.

> The pro forma report's appearance doesn't seem quite right/there is a bunch of cryptic commands underneath the "Optimization formulation" section.

For best results when viewing the report, you must be connected to the internet and enable JavaScript. We use content delivery services for resources such as fonts (Google Fonts) and use JavaScript to render the equations under the "Optimization formulation" section (MathJax).

#### Batch Runs

> What is a parameter sweep?

A parameter sweep will adjust the specified parameter from the min value to the max value in the given number of steps. It will do this for each month of data selected on the "data" interface. A simulation will be performed for the all of the combinations. This is a useful way for performing sensitivity analysis.