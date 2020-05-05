### THINK 2020 Virtual Lab :

# CareKit SDK + IBM Hyper Protect SDK for iOS

## May 06th 2020, 3:00 - 5:00 PM EST

### Moderators:

- Elton de Souza (Cloud Native Client Success - IBM)
- Mal Pattiaratchi (IBM Technical Leader - IBM)
- Ryley Wharton (Client Success and Developer Advocate - IBM

### Agenda:

- [CareKit SDK + IBM Hyper Protect SDK for iOS](#carekit-sdk--ibm-hyper-protect-sdk-for-ios)
  - [May 06th 2020, 3:00 - 5:00 PM EST](#may-06th-2020-300---500-pm-est)
    - [Moderators:](#moderators)
    - [Agenda:](#agenda)
    - [Useful links:](#useful-links)
- [Account setup](#account-setup)
  - [<br/>](#br)
- [Modify/add OCKTask to the SampleApp](#modifyadd-ocktask-to-the-sampleapp)
- [IBM Hyper Protect SDK for iOS](#ibm-hyper-protect-sdk-for-ios)
    - [Roadmap](#roadmap)
    - [Getting Started](#getting-started)
    - [Contributing](#contributing)
    - [Known Issues:](#known-issues)
    - [Troubleshooting:](#troubleshooting)
- [Deploying a Hyper Protect Virtual Server and Hyper Protect DBaaS for MongoDB instance tutorial](#deploying-a-hyper-protect-virtual-server-and-hyper-protect-dbaas-for-mongodb-instance-tutorial)
  - [Steps](#steps)
    - [Connecting to your Virtual Server](#connecting-to-your-virtual-server)
    - [**Useful IBM Cloud Links:**](#useful-ibm-cloud-links)
- [Integrating CareKit HyperProtect SDK for iOS with SampleApp](#integrating-carekit-hyperprotect-sdk-for-ios-with-sampleapp)
    - [_DRAFT_](#draft)
- [Configuring the CareKit application with a Hyper Protect Virtual Server and a Hyper Protect DBaaS MongoDB Backend.](#configuring-the-carekit-application-with-a-hyper-protect-virtual-server-and-a-hyper-protect-dbaas-mongodb-backend)
  - [Prerequisites](#prerequisites)
  - [Initial setup to prepare for running ansible](#initial-setup-to-prepare-for-running-ansible)
  - [Instructions for the 'hpvs_setup.yml' playbook](#instructions-for-the-hpvssetupyml-playbook)
  - [Instructions for the 'local_setup.yml' playbook](#instructions-for-the-localsetupyml-playbook)
  - [Validation Test](#validation-test)

### Useful links:

- Developer Blogpost:
- Executive Blogpost:
- CareKit
- IBM Cloud Hyper Protect Services



<br/>

---
# Account setup

Goal : At the end of this section, you should have pre-requisite accounts needed to successfully complete this lab

---

1. Apple ID //TODO


2. IBM Cloud Account:

An IBM Cloud account is required for authentication

* Log into the IBM Cloud dashboard using the following URL: (https://cloud.ibm.com)
	* If creating an IBM Cloud account is required, navigate to the registration page and fill out all required fields.
	* https://cloud.ibm.com/registration

Additional documentation illustrating the process to create an IBM Cloud account.
  > https://cloud.ibm.com/docs/account?topic=account-signup


<br/>
---
# Modify/add OCKTask to the SampleApp

Goal: At the end of this section, you should have a new talk showing up your SampleApp
- - -
//TODO

# IBM Hyper Protect SDK for iOS

This SDK implements CareKit's Remote Synchronization API and must be coupled with the backend SDK [IBM-HyperProtectMBaaS](https://github.com/carekit-apple/IBM-HyperProtectMBaaS) on the server side.

_Note, this is a pre-1.0 release and is still in beta_

### Roadmap

- [ ] Logging with OSLog
- [ ] OAuth2 support with JWT
- [ ] Bi-directional Synchronization of other high level entities (Contact, CarePlan, Patient)
- [ ] Comprehensive integration tests
- [ ] Comprehensive system tests
- [ ] OpenAPI Specification template
- [ ] IBM Cloud Starter Kit support
- [ ] Travis Build Support

### Getting Started

This package can be imported into XCode using Swift Package Manager:

![spm-add-packages](./docs/spm-add-package.png)

![spm-add-git-url](./docs/spm-add-git-url.png)

![spm-git-master](./docs/spm-git-master.png)

![spm-add-target](./docs/spm-add-target.png)

Now import the package with

```swift
import IBMHyperProtectSDK
```

and pass it in to your OCKStore:

```swift

let remote = IBMMongoRemote()
let store = OCKStore(name: "SampleAppStore", type:
  inMemory, remote: remote)
```

By default if no backend API information is passed in, it will default to `https://localhost:3000` . Pass in the `apiLocation` parameter to point to your IBM Hyper Protect MBaaS deployed locally for development or in IBM Cloud.

### Contributing

We're always looking for contributors to help improve the CareKit and IBM Hyper Protect community. Please follow the [guide](./CONTRIBUTING.md)

### Known Issues:

When using the IBM Hyper Protect SDK, you must also include CareKit in your app via SPM. Including CareKit using the traditional sub-project approach can cause runtime errors in the CoreData stack.

### Troubleshooting:

Work in progress


<br/>

# Deploying a Hyper Protect Virtual Server and Hyper Protect DBaaS for MongoDB instance tutorial
- - - 
Goal : At the end of this section, you should have a production ready MongoDB instance from IBM Hyper Protect DBaaS and a secure container environment from IBM Hyper Protect Virtual Servers to deploy the TypeScript server on.
- - -

<br/>

## Steps

1. Log into the IBM Cloud dashboard (https://cloud.ibm.com)
	* Please refer to the documentation on the _README_ page for further instructions on logging into IBM Cloud, or obtaining an IBM Cloud account


2. After the IBM Cloud homepage loads, click the blue 'Create Resource' button on the top right of the page, directly underneath the Cloud toolbar. Alternatively, the create resource function is accessible by selecting the 'Add Resource +' option underneath the Resouce Summary table.
	* The desired destination is the Cloud catalog, where all current availble Cloud offerings are listed
	* In order to view the full list of Cloud offerings, ensure that the 'Services' tab is selected on the left-hand side of the catalog


3. Within the catalog listings, locate and click on 'Hyper Protect Virtual Servers'. 	
    * The page defaults to the 'Create' tab, where the various Virtual Server options are able to be selected. 
    * Choose the appropriate region to deploy the virtual server in, as well as a suitable pricing plan based on the technical requirements for the Virtual Server
      * The 'free' payment option will be adequate for this lab
 
    * Add any necessary tags for labeling the virtual server
	  * Lastly, copy and paste in a public ssh key into the last field. This is a required step as the Virtual server is only accessible via ssh key.
	  * After all required fields have been properly filled out, click the create button on the bottom right hand side of this page to begin provisioning of the Hyper Protect Virtual Server instance


4. Navigate back to the IBM Cloud catalog, and search for the 'Hyper Protect DBaaS for MongoDB' offering.
	* Choose the appropriate region to deploy the virtual server in, as well as a suitable pricing plan based on the technical requirements needed for the MongoDB service.
  
    * There are several fields listed below the pricing plans, some of which are required, while other fields are optional. Follow the next steps for the required fields.
      * The non-essential fields will be left to the default values
  
    * Create and add a 'Cluster Name' for the database
      * Example: My_Mongo_Cluster
  
    * Choose an admin ID name for the MongoDB service, this ID will have full administrative access to the database. 
      * Example: admin
  
    * Generate a password for the associated database admin user
      * Requirements: 15 characters minimum, must include 1 capital letter, and 1 number. Characters are allowed.
	
  * After all required fields have been properly filled out, click the create button on the bottom right hand side of this page to begin provisioning of the Hyper Protect DBaaS for MongoDB

Note: Please allow up to 5 minutes for both services to deploy after the process initiates. 


### Connecting to your Virtual Server

Now that both required Cloud services have been deployed, it is time to access the newly provisioned virtual server using ssh protocol
	
* To obtain the public IP address of the virtual server, navigate to the Cloud dashboard homepage, and click on 'Services' in the Resource Summary box. Once the deployed services are listed, locate the Hyper Protect virtual server instance and click on the name. The public IP address will be displayed on the following screen.
  
  * After finding the public IP address, access a terminal and leverage the ssh protocol to navigate to the virtual server.
	   * Example ssh command: ssh root@{public_IP}
		
	* The ID required for a successful ssh connection must be 'root'

**You should now be successfully connected to your Virtual Server!**

### **Useful IBM Cloud Links:**
HPVS Documentation: https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-getting-started
<br/>

DBaaS Documentation: https://cloud.ibm.com/docs/services/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-gettingstarted
- - - 
<br/>

# Integrating CareKit HyperProtect SDK for iOS with SampleApp

### _DRAFT_

_Goal_ : At the end of this section, you should have a fully running CareKit based app end-to-end that consumed IBM Hyper Protect Services
The SDK consists of 2 layers:

---

- The frontend Swift component that gets included in XCode
- The backend TypeScript server that acts as a mediator between the frontend and the database

// todo : Include Arch Diagram

// todo : inline NPM steps for backend

// todo : inline Swift code changes (+ XCode screenshots) for frontend



<br/>
<br/>
<br/>

- - - -
# Configuring the CareKit application with a Hyper Protect Virtual Server and a Hyper Protect DBaaS MongoDB Backend.
_Goal_: At the end of this next section, the recently provisioned Hyper Protect Virtual server and Hyper Protect DBaaS Instance should be fully configured with the Backend SDK CareKit application. Follow the illustrated steps below to run the _ansible_ playbook for automated setup. 
- - - -

<br/>


## Prerequisites
1. Install ansible via pip3 (or pip)
    * In order to run this playbook on the local machine _ansible_ is a required package.
    * Command for installation: _pip3 install ansible_
      * Please note that this command uses pip3, if you still have python2 as the default python interpreter, use 'pip' in lieu of pip3
  
2. Install docker-compose via pip3
   * pip3 install docker-compose

3. Install docker
   * pip3 install docker

## Initial setup to prepare for running ansible
1. Clone the repository on the local machine
    * git clone https://github.com/e-desouza/carekit-hyperprotect-lab.git
    * This github repository containing the ansible playbooks has been made public in order to clone this repository 
<br/>
   
2. After the Github repo has been cloned to the local machine, change the terminal directory to _carekit-hyperprotect-lab/ansible_setup_
    * cd Directory/whereRepository/wasCloned/carekit-hyperprotect-lab/ansible_setup
<br/>

3. There are two ansible playbooks that can be run for bringing up the CareKit Backend SDK application. The first uses a HyperProtect Virtual Server, and DBaaS MongoDB instance. While the second option will configure the Backend SDK app on the local machine, uses localhost. Choose the next set of instructions accordingly.

<br/>


## Instructions for the 'hpvs_setup.yml' playbook 
Requires HPVS and MongoDB IBM Cloud instances

1. Two critical additions to the yml files must be made in order to successfully run the hpvs_setup.yml playbook. Add the following values accordingly:
    * ansible.cfg
       * Within the ansible.cfg file, the value for environmental variable _ansible_ssh_private_key_file_ is currently an empty string. Add the location and name of your public SSH key used to provision the Hyper Protect Virtual Server
       * Example: ansible_ssh_private_key_file = "~/.ssh/id_rsa.pub"
       ![Example-Of-CFG-File](./ansible_setup/screenshots/cfgFile.png)
       <br/>
       
    * inventory.yml
       * Underneath the commented line, add the public IP address of the Hyper Protect Virtual Server
       * Example:
       ![Example-Of-Inventory-File](./ansible_setup/screenshots/hostFile.png)
<br/>

2. One final preparation step is required prior to running the ansible playbook. The DBaaS MongoDB admin ID and password needs to be added to the mongo URI, as this value will be passed into the command line when invoking the playbook.
     * Ensure that the entire string including all 3 replica hosts are in the uri string, and also the Cluster name at the end.
     * Example:
     ```
     mongodb://admin:password@dbaas30.hyperp-dbaas.cloud.ibm.com:28162,dbaas29.hyperp-dbaas.cloud.ibm.com:28130,dbaas31.hyperp-dbaas.cloud.ibm.com:28222/admin?replicaSet=Wu-Tang_Clan
     ```
      * Replace 'admin' and 'password' with the proper admin ID and correlated password into the MongoDB URI string provided after provisioning the DBaaS instance.
<br/>

3. Now that the Public IP address has been added as a listed host, and the location of the public SSH key was specified, it is now time to run the ansible playbook for setup. Use the following command in order to run the playbook properly.
    * Notice that the initial portion of the extra variable being passed to the playbook starts with _db=_. This is required to specify which variable is being passed to the ansible playbook.
    * Command Example:
    ```
    ansible-playbook hpvs_setup.yml -e "db=mongodb://{admin_ID}:{Mongo_Password}@DBaaS_Mongo_URI:port.../admin?replicaSet=Cluster_Example"
     ```
     <br/>
     
 ![Example-Of-Ansible-Command](./ansible_setup/screenshots/Command.png)
 
 <br/>
 
4. Allow the playbook to run through it's designated tasks and configure the HPVS container.
![Example-Of-Playbook-Running-Tasks](./ansible_setup/screenshots/Playbook.png)
 
 <br/>
  
**The HPVS configuration should now be complete, follow the validation test section listed below to confirm the setup worked as intended.**

<br/>



## Instructions for the 'local_setup.yml' playbook 
Please note that while the local setup does _not_ require an IBM Cloud HPVS nor DBaaS instance, a few local 

1. Unlike the 'hpvs_setup.yml' playbook, the local setup already has the correct _locahost_ configurations written within the playbook itself, and does not require any other changes to the inventory file, nor ansible.cfg. Please use the listed command below to run the ansible script.
  * Command: _ansible-playbook local_setup.yml -K_
    * The _-K_ argument is required due to the playbook utilizing the "Become" parameter. Enter the local machine password (user profile credentials) when prompted.

![Run-Local-Setup](./ansible_setup/screenshots/local_setup.png)

<br/>

2. Allow the playbook to run and complete the predefined tasks. 

![Playbook-After-Completion](./ansible_setup/screenshots/finished_playbook.png)

<br/>

3. In order to ensure that the Backend SDK app was created properly, use the following docker commands to check.
 * _docker ps -a_
     * You should see two containers as a result, one labeled as 'hyperprotectbackendsdk', and the other container as 'mongo'.
   
 * Copy the Container ID serial number from the above output, and use the _docker logs <containerID>_ command to check the logs. 
     * If the app is running properly from the local machine, you will see output stating that the example app is running on port 3000.

![Example-Of-Docker-Commands](./ansible_setup/screenshots/docker_example.png)

<br/>





## Validation Test
To validate that the app is running properly, and listening on port 3000, a simple curl command can be issued to for verification. Please make certain that the IP address is changed in the http address after the POST declaration, as the goal is to hit the running application using the pulic IP addresss of the Virtual Server.
  
* Copy the entire curl command below, after replacing the _{HPVS_IP_or_locahost}_ parameter depending on which setup playbook was run.
  * If 'local_setup.yml' was used for configuration, change the parameter to _localhost_
  * If 'hpvs_setup.yml' was used instead, simply change the parameter to the public IP address of the HPVS instance
* Run the curl command from local machine, this will validate the Backend SDK application is reachable, and taking requests.
* If the test is successful, a returned output of 'RevisionRecord stored' will populate after the curl command. 
  * Also, within the docker container logs, the POST call will come through, and a _201_ code will be returned. 
  * Command to view docker logs: _docker logs <containerID>_
    * ContainerID can be found by running _docker ps -a_ and locating the HyperProtectBackendSDK container

**Curl Command**
```
curl --cacert rootCA.crt --location --request POST 'https://{HPVS_IP_or_locahost}:3000/revisionRecord' \
--header 'Content-Type: application/json' \
--data-raw '{
    "entities": [
        {
            "type": "task",
            "object": {
                "schemaVersion": {
                    "majorVersion": 2,
                    "minorVersion": 0,
                    "patchNumber": 4
                },
                "id": "nausea",
                "uuid": "75EE244A-7303-43CF-9AA5-6CC3BB81210A",
                "createdDate": 609212115.685683,
                "updatedDate": 609212115.685702,
                "title": "Track your nausea",
                "notes": [],
                "timezone": {
                    "identifier": "America/Sao_Paulo"
                },
                "instructions": "Tap the button below anytime you experience nausea.",
                "impactsAdherence": false,
                "effectiveDate": 608785200,
                "schedule": {
                    "elements": [
                        {
                            "text": "Anytime throughout the day",
                            "duration": {
                                "isAllDay": true
                            },
                            "interval": {
                                "minute": 0,
                                "hour": 0,
                                "second": 0,
                                "day": 1,
                                "month": 0,
                                "year": 0,
                                "weekOfYear": 0
                            },
                            "targetValues": [],
                            "start": 608785200
                        }
                    ]
                }
            }
        },
        {
            "type": "task",
            "object": {
                "schemaVersion": {
                    "majorVersion": 2,
                    "minorVersion": 0,
                    "patchNumber": 4
                },
                "id": "doxylamine",
                "uuid": "C0861A29-C726-4B58-B3AB-89CF3E3294F6",
                "createdDate": 609212115.696223,
                "updatedDate": 609212115.696224,
                "title": "Take Doxylamine",
                "notes": [],
                "timezone": {
                    "identifier": "America/Sao_Paulo"
                },
                "instructions": "Take 25mg of doxylamine when you experience nausea.",
                "impactsAdherence": true,
                "effectiveDate": 608814000,
                "schedule": {
                    "elements": [
                        {
                            "duration": {
                                "seconds": 0,
                                "isAllDay": false
                            },
                            "interval": {
                                "minute": 0,
                                "hour": 0,
                                "second": 0,
                                "day": 1,
                                "month": 0,
                                "year": 0,
                                "weekOfYear": 0
                            },
                            "targetValues": [],
                            "start": 608814000
                        },
                        {
                            "duration": {
                                "seconds": 0,
                                "isAllDay": false
                            },
                            "interval": {
                                "minute": 0,
                                "hour": 0,
                                "second": 0,
                                "day": 2,
                                "month": 0,
                                "year": 0,
                                "weekOfYear": 0
                            },
                            "targetValues": [],
                            "start": 608835600
                        }
                    ]
                }
            }
        },
        {
            "type": "task",
            "object": {
                "schemaVersion": {
                    "majorVersion": 2,
                    "minorVersion": 0,
                    "patchNumber": 4
                },
                "id": "kegels",
                "uuid": "1B6AA55A-E5A1-4124-8B9E-59DE3EEF9DE5",
                "createdDate": 609212115.697711,
                "updatedDate": 609212115.697713,
                "title": "Kegel Exercises",
                "notes": [],
                "timezone": {
                    "identifier": "America/Sao_Paulo"
                },
                "instructions": "Perform kegel exercies",
                "impactsAdherence": true,
                "effectiveDate": 608814000,
                "schedule": {
                    "elements": [
                        {
                            "duration": {
                                "seconds": 0,
                                "isAllDay": false
                            },
                            "interval": {
                                "minute": 0,
                                "hour": 0,
                                "second": 0,
                                "day": 2,
                                "month": 0,
                                "year": 0,
                                "weekOfYear": 0
                            },
                            "targetValues": [],
                            "start": 608814000
                        }
                    ]
                }
            }
        }
    ],
    "knowledgeVector": {
        "processes": [
            { "id" : "1C43F648-D41A-4A5A-8708-15737425FA7C", "clock" : 10},
            { "id" : "2B43F648-D41A-4A5A-8708-15737425FA7C", "clock" : 4}
        ]
    }
}'
```

After the curl command has been issued, if successful the response will look similar to this screenshot:
```
>     "knowledgeVector": {
>         "processes": [
>             { "id" : "1C43F648-D41A-4A5A-8708-15737425FA7C", "clock" : 10},
>             { "id" : "2B43F648-D41A-4A5A-8708-15737425FA7C", "clock" : 4}
>         ]
>     }
> }'
RevisionRecord stored
```

<br/>

Another verification check is to check the Docker container logs on the Virtual Server. The docker logs can be checked as such:

1. Check docker for running containers
> docker ps -a
  
* Locate the Docker container ID
  * Example: 
  ```
  root@b4e8f18c497b:~# docker ps -a
  CONTAINER ID        IMAGE                            COMMAND                  CREATED             STATUS
  c876afbe4704        hyperprotectbackendsdktest_app   "docker-entrypoint.s…"   2 hours ago         Up 2 hours          
  ```
<br/>

2. Use container ID from previous step to check current log entries
> docker logs {Container_ID}
  
* View the Docker logs, traces of the curl command should be present as depicted in the screenshot below. 
  
 ![Docker-Logs-Example](./ansible_setup/screenshots/Results.png)
