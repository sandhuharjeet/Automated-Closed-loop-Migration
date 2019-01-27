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


* Harjeet Sandhu <harjeets@cisco.com> -  TELCO & MOBILE HQ
* Raj Singh <rajsin2@cisco.com> -  TELCO & MOBILE HQ
* Marty Fierbaugh <mfierbau@cisco.com> - SELECT HQ



## Solution Components




**Automation Components**:

**Ansible** : Most of the automation is done using Ansible IOS-XR modules like iosxr_config, iosxr_command etc. Most of the automation and structure is build in a manner that same automation can be applied to production environment by just updating variables file. 

**Jupyter Notebook** : The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. This is being used for generating an Automation MOP, which in turn calls Ansible scripts to execute MOP steps. This act as front end for end user. Apart from ansible playbooks, other python based automation is done within jupyter notebook cells. Other useful features of Jupyter notebook are:

Logging: Which helps with saving MOP execution for later validation and troubleshooting. MOP can be shared, as PDF, HTML, email, dropbox, github etc. 
Webhosted Application: Which helps to run all the MOPs on single server, and end MOP execution engineer just need to have web based link to access MOP.
Interactive Output: As we execute each MOP step, output is displayed on the same web page, and also code can produce rich, interactive output like HTML, tables, images etc.  

**TextFSM** : TextFSM is a Python module that implements a template based state machine for parsing semi-formatted text. This module is used for programmatic access to information given by the output of CLI for the routers. Using TextFSM we have converted multiple CLI output to Json format. We have developed new TextFSM templates to convert specific IOS-XR CLIs into Json, which is used for programmatic validation of given step. 

**Pandas** : For user experience other feature we have used in our MOP is python based Pandas library, which is used to cover CLI output into beautiful tables. Once TextFSM converts CLI output into Json, we have used Pandas dataframes to covert that output into HTML tables. With table format of CLI output, end user can easily validate specific output. 



**Streaming Telemetry Components**:  

As we execute MOP to covert MPLS LDP based network to Segement routing based network, we need to make sure that end user traffic is not impacted. For this we need a mechanism for continuous feedback for end user traffic forwarding. For this we have used Cisco IOS-XR based Streaming telemetry. Using streaming telemetry, we get live feedback for end user traffic forwarding. If at any given time we see any drop in end user traffic, various actions can be take, like validating why traffic dropped or we can immediately execute Backout MOP, which is also part of the overall automation. Various components used for digesting telemetry data are :-

**Pipeline** : Pipeline is an all-batteries-included utility which consumes IOS XR telemetry streams directly from the router or indirectly from a publish/subscribe bus. Once collected, pipeline can perform some
limited transformations of the data and forwards the resulting content
on to a downstream, typically off-the-shelf, consumer. Supported
downstream consumers include Apache Kafka, Influxdata TICK
stack, prometheus, dedicated gRPC clients, as well as dump-to-file for diagnostics. 

**InfluxDb** : Pipeline write telemetry data into InfluxDB, an open source platform for time-series data. This database is used to store telemetry data being streamed from the routers. 

**Grafana** : Grafana is a very popular visualization tool, that can be used for monitoring and alerting. We have used Garfana as front end to visualize live status of the end user traffic across SP core, when the execution of the MOP is happening. 



**Virtualization components for Demo** :  

For implementing this solution and performing Demo’s for the customer, we have used all virtual environment running in two different VMs on UCS-C240. One VM is used to simulate Customer network using Cisco Virl, which is powerful, easy-to-use, and extensible network modeling and simulation environment. Other VM is used for other automation tools described above.

Using VIRL we have simulated typical SP network with two types of services, L3VPN service and Global Internet Service. Base configuration consists of end to end MPLS LDP based L3vpn service and end to end ipv4 based global Internet service.  

**Virtual Router**: For simulating SP core and Edge we have used IOS-XRv 6.2.1 image.  For end customer CE routers we have used virtual IOS image. 

**Virtual Traffic Generator**: Also, to simulate end user traffic we have used Virtual traffic generator Ostinato. This is also running as VM inside VIRL environment. 







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

