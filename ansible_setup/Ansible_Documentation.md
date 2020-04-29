# HyperProtectSDK_Ansible
Please follow the listed steps below to clone this repository, and successfully run the ansible playbook that configures the newly provisioned HPVS instance.
- - - -


# Setup Steps
1. Clone the repository on the local machine
    * git clone <github url>
    * This github repository containing the ansible playbooks has been made public
<br/>
   
2. Change the directory to the recently cloned repository
    * cd ~/Directory/Containing/Playbooks/HyperProtectSDK_Ansible
<br/>

3. Two crucial additions to the yaml files must be made in order to successfully run the hpvs_setup.yml playbook. Add the following values accordingly:
    * ansible.cfg
       * Within the ansible.cfg file, the value for environmental variable _ansible_ssh_private_key_file_ is currently an empty string. Add the location and name of your public SSH key used to provision the Hyper Protect Virtual Server
       * Example: ansible_ssh_private_key_file = "~/.ssh/id_rsa.pub"
       ![Example-Of-CFG-File](screenshots/cfgFile.png)
       <br/>
       
    * inventory.yml
       * Underneath the commented line, add the public IP address of the Hyper Protect Virtual Server
       * Example:
       ![Example-Of-Inventory-File](screenshots/hostFile.png)
<br/>

4. One final preparation step is required prior to running the ansible playbook. The DBaaS MongoDB admin ID and password needs to be added to the mongo URI, as this value will be passed into the command line when invoking the playbook.
     * Ensure that the entire string including all 3 replica hosts are in the uri string, and also the Cluster name at the end.
     * Example:
     ```
     mongodb://admin:password@dbaas30.hyperp-dbaas.cloud.ibm.com:28162,dbaas29.hyperp-dbaas.cloud.ibm.com:28130,dbaas31.hyperp-dbaas.cloud.ibm.com:28222/admin?replicaSet=Wu-Tang_Clan
     ```
      * Replace 'admin' and 'password' with the proper admin ID and correlated password into the MongoDB URI string provided after provisioning the DBaaS instance.
<br/>

5. Now that the Public IP address has been added as a listed host, and the location of the public SSH key was specified, it is now time to run the ansible playbook for setup. Use the following command in order to run the playbook properly.
    * Notice that the initial portion of the extra variable being passed to the playbook starts with _db=_. This is required to specify which variable is being passed to the ansible playbook.
    * Command Example:
    ```
    ansible-playbook hpvs_setup.yml -e "db=mongodb://{admin_ID}:{Mongo_Password}@DBaaS_Mongo_URI:port.../admin?replicaSet=Cluster_Example"
     ```
     <br/>
     
 ![Example-Of-Ansible-Command](screenshots/Command.png)
 
 <br/>
 
 6. Allow the playbook to run through it's designated tasks and configure the HPVS container.
 ![Example-Of-Playbook-Running-Tasks](screenshots/Playbook.png)
 
 <br/>
  
**The HPVS configuration should now be complete, follow the validation test listed below to confirm the setup worked as intended.**

<br/>

# Validation Test
To validate that the app is running properly, and listening on port 3000, a simple curl command can be issued to for verification. Please make certain that the IP address is changed in the http address after the POST declaration, as the goal is to hit the running application using the pulic IP addresss of the Virtual Server.
	
* Copy the entire curl command below, after replacing the HPVS Public IP address
* Run command from local machine, this will verify that the application is running on the Virtual Server, and is accessible. 
* If the test is successful, a returned output of 'RevisionRecord stored' will populate after the curl command. 
	* Also, on the Virtual Server running the application, the POST call will come through, and a _201_ code will be returned. 

**Curl Command**
```
curl --location --request POST 'http://{HPVS_Public_IP_Address}:3000/revisionRecord' \
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
	
 ![Docker-Logs-Example](screenshots/Results.png)
