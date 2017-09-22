# Translation Units for the FRINX ODL CLI service module

This repository contains documentation for all available translation units for our FRINX ODL CLI service module. A translation unit is a piece of code that includes handlers to read or write to a specific device (e.g. Cisco IOS classic router) and translate that information in OpenConfig models. 
The purpose of this documentation is to see which commands can be read and set and how they map to the respective YANG models.
Every section has a README file that provides an overview of all show and configuration commands that are supported.
Multiple translation units are finally packaged together and made available as a karaf feature that can be installed at runtime. 
