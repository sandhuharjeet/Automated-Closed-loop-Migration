# Automated-Closed-loop-Migration-Project

Using Pythion, Ansible, CLI Regex parsing, streaming telemetry & APIs etc., we will be building a fully automated web app for MPLS to segment routing migration. We will also use open source tools like Jupyter Notebooks, InfluxDB etc. Additionally, we will be utilizing VIRL for simulating the customer network

## Business/Technical Challenge

Cisco customer especially SPs & large enterprises are looking forward to simplify and scale their core network specially to address new NFV application environments. Segment routing (SR) is one of the technologies that helps with this, Firstly by simplifying core with removal of extra control plane protocols and secondly making core more scalable from prospective of traffic engineering, as with SR we don't require any tunnel state or signaling in the core.
 
Though SR offer seamless deployment by co-existing with current LDP core, but SP customers have OPEX and time-to-market challenges with this big change in their core network. Also, other issue that we have seen very prevalent in SP/Large Enterprise customers with this big change in the core technology is how they can validate the impact of introduction SR on their existing services.


## Proposed Solution


Our proposed solution will try to address OPEX challenge specially during the migration of the LDP core to segment routing core. We will be fully automating the migration process for LDP core to Segment routing core. This will cover the seamless and fully automated conversion of L3vpn, Direct internet and other services to new SR core.
 
This being full automation of all phases of LDP to SR migration, so will it help not only with time to market but also considerably reduce OPEX cost during this migration, as to do this change manually will take lot of man hours and migration windows.

Also, as we will be using VIRL in our solution so customer will be able to test this migration using their own production configurations as well as validate each phase of this migration. Apart from this end customer will be able to run this migration from web-based app for easy execution, logging results for each step and will have capability to share/store result in web page format for each execution.  

 
We will be utilizing Streaming telemetry for closed loop feedback to validate service performance during this migration. This way if at any time during migration there is service drop or performance degradation, changes can be rolled back using rollback automation.

 
As part of this project we will also add some additional features based on evaluation of usability and Gap analysis.


### Cisco Products Technologies/ Services


Our solution will leverage the following Cisco technologies

* [iosxr-ansible](https://developer.cisco.com/codeexchange/github/repo/ios-xr/iosxr-ansible/)
* [Segment Routing](http://www.segment-routing.net/)
* [IOS-XR Programmable Interface](https://developer.cisco.com/site/ios-xr/)
* [Cisco IOS XR Telemetry](https://xrdocs.io/telemetry/)
* [Virtual Internet Routing Lab(VIR)](virl.cisco.com)

Our Solution will Leverage the following Open source technologies

* [Jupyter Notebook](http://jupyter.org/)
* [InfluxDB](https://github.com/influxdata/influxdb)
* [grafana](https://grafana.com/)
* [pandas](https://pandas.pydata.org/)



## Team Members


* Harjeet Sandhu <harjeets@cisco.com> - SP AMERICAS
* Raj Singh <rajsin2@cisco.com> - SP AMERICAS



## Solution Components


<!-- This does not need to be completed during the initial submission phase  

Provide a brief overview of the components involved with this project. e.g Python /  -->


## Usage

<!-- This does not need to be completed during the initial submission phase  

Provide a brief overview of how to use the solution  -->



## Installation

How to install or setup the project for use.


## Documentation

Pointer to reference documentation for this project.


## License

Provided under Cisco Sample Code License, for details see [LICENSE](./LICENSE.md)

## Code of Conduct

Our code of conduct is available [here](./CODE_OF_CONDUCT.md)

## Contributing

See our contributing guidelines [here](./CONTRIBUTING.md)
