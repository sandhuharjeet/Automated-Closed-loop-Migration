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


![alt text]( https://github.com/sandhuharjeet/Automated-Closed-loop-Migration/blob/master/Component-Diagram.png)

**Automation Components**:

**Ansible** : Most of the automation is done using Ansible IOS-XR modules like iosxr_config, iosxr_command etc. Most of the automation and structure is build in a manner that same automation can be applied to production environment by just updating variables file. 

**Jupyter Notebook** : The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. This is being used for generating an Automation MOP, which in turn calls Ansible scripts to execute MOP steps. This act as front end for end user. Apart from ansible playbooks, other python-based automation is done within jupyter notebook cells. Other useful features of Jupyter notebook are:

Logging: Which helps with saving MOP execution for later validation and troubleshooting. MOP can be shared, as PDF, HTML, email, dropbox, github etc. 

Webhosted Application: Which helps to run all the MOPs on single server, and end MOP execution engineer just need to have web-based link to access MOP.

Interactive Output: As we execute each MOP step, output is displayed on the same web page, and also code can produce rich, interactive output like HTML, tables, images etc.  

**TextFSM** : TextFSM is a Python module that implements a template based state machine for parsing semi-formatted text. This module is used for programmatic access to information given by the output of CLI for the routers. Using TextFSM we have converted multiple CLI output to Json format. We have developed new TextFSM templates to convert specific IOS-XR CLIs into Json, which is used for programmatic validation of given step. 

**Pandas** : For user experience other feature we have used in our MOP is python based Pandas library, which is used to cover CLI output into beautiful tables. Once TextFSM converts CLI output into Json, we have used Pandas dataFrames to covert that output into HTML tables. With table format of CLI output, end user can easily validate specific output. 



**Streaming Telemetry Components**:  

As we execute MOP to covert MPLS LDP based network to Segment routing based network, we need to make sure that end user traffic is not impacted. For this we need a mechanism for continuous feedback for end user traffic forwarding. For this we have used Cisco IOS-XR based Streaming telemetry. Using streaming telemetry, we get live feedback for end user traffic forwarding. If at any given time we see any drop in end user traffic, various actions can be take, like validating why traffic dropped or we can immediately execute Backout MOP, which is also part of the overall automation. Various components used for digesting telemetry data are :-

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

This solution can be used in two different ways. First to demo the automated solution to end audience. Second for production environment to migrate MPLS LDP based network to Segment-routing based network. 

**For Demo Purposes** :

Once you have installed a complete solution using steps described below in Installation section, you can use this automated solution to demo MPLS LDP based SP network to Segment routing based network. You can open Grafana dashboard to validate end to end L3vpn and Global Internet traffic is running fine, without any drop. If everything is running fine, you can open Jupyter notebook **“Automated_MPLS_to_SR_migration_MOP.ipynb”** and execute entire MOP by clicking on “Run All” under “cell” sub-menu of notebook or run each step of MOP one by one by clicking “run cell” but for each step. 

If during execution there is any traffic drop and error seen, then you can open “Automated_MPLS_to_SR_migration_Rollback_MOP.ipynb” jupyter notbook and execute all the cells to rollback the migration. 

Once any of the notebook is run successfully you can save the entire output of the MOP by using “Save as HTML” under “File” Menu. This can be used for sharing the MOP code and also execution output with other users for reference. 


**For Production Purposes** :

For production you can use either Ansible playbooks individually for any Migration steps or use it with Jupyter Notebooks (Automated_MPLS_to_SR_migration_MOP.ipynb & Automated_MPLS_to_SR_migration_Rollback_MOP.ipynb)to execute entire MOP as used in this development. 

To use Ansible automation for production, only file that need to be udated is “main.yml” under /roles/<specific role>”/defaults directory. These main.yml files contain variables for each ansible playbook(role). 
For production we need to change variables required for production like Segment routing SIDs, Loopback IP addressed, Prefix for Mapping server etc. 
Also this automation was build considering SP network is using ISIS as IGP in the core. If SP network is using OSPF in the core, then we need to update couple of ansible playbooks to match that. If you require to make those changes, please reach out to the development team mentioned above in Team member section. 



## Installation

As mentioned above this solution can be used as a Demo or used in production, so we will explain installation steps for both these below :

**Installation for Demo** :

These steps are for Ubuntu Linux but can be used for other installation as well. Also Python version 2.5 or later is required. 

**Step1**: [Install and setup VIRL](http://get.virl.info/)
**Step2**: [Install/Setup Pipeline, InfluxDB and Grafana]( https://github.com/cisco/bigmuddy-network-telemetry-pipeline)
**Step3**: [Install/setup Jupyter Notebook]( https://jupyter.org/install.html)
**Step4**: [Install Ansible 2.6 or later] (https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
**Step6**: [Install TextFSM using “pip install textfsm”] (https://pypi.org/project/textfsm/)
**Step7**: [Git Clone the automation to local linux server] (https://github.com/sandhuharjeet/Automated-Closed-loop-Migration)
**Step8**: Run Virl and load topology file “LDP_to_SR_Demo_VIRL_Base_config.virl” under “Virl_files” folder of cloned project. Start the simulation. 
**Step9**: Start Ostinato client on ubuntu and load traffic generation profile “LDP_to_SR_Demo_ostinato_traffic_generator_VIRL.ossn” under “Virl_files” folder of cloned project.
**Step10**: Load Garfana Dashboard using profile file “SR-Demo-all-interface-stats-1548624550086.json” under “Garfana Profile” Folder.
**Step11**: Start Jupyter Notebook Server and Open “Automated_MPLS_to_SR_migration_MOP.ipynb” & “Automated_MPLS_to_SR_migration_Rollback_MOP.ipynb” notebooks.
**Step12**: This completes the installation, please use above Usage section to run the complete demo.


**Installation for Production** :

For Production only requirement are that you should have Ansible 2.5 or higher and Jupyter notebook server. Once you have installed and setup Ansible, jupyter notebook, you can execute either ansible playbooks individually or use Juypter notebooks “Automated_MPLS_to_SR_migration_MOP.ipynb” & “Automated_MPLS_to_SR_migration_Rollback_MOP.ipynb” to run these MOPs. Please update main.yml file as described above in usage section. 









## Documentation

Pointer to reference documentation for this project.

[Learn Ansible for Cisco routers] (https://learninglabs.cisco.com/labs/tags/Ansible)

[Learn VIRL] (https://learningnetwork.cisco.com/community/learning_center/virl-training-videos)



## License

Provided under Cisco Sample Code License, for details see [LICENSE](./LICENSE.md)

## Code of Conduct

Our code of conduct is available [here](./CODE_OF_CONDUCT.md)

## Contributing

See our contributing guidelines [here](./CONTRIBUTING.md)

