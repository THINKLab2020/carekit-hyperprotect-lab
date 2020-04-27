- - - -
# Configuring the Apple CareKit application with a Hyper Protect Virtual Server and a Hyper Protect DBaaS MongoDB Backend.
Follow the listed steps below in order to successfully build the Apple CareKit application on an HPVS instance, while leveraging the Hyper Protect DBaaS for mongodb service as a viable backend database. 
- - - -

<br/>

# Prerequisites
	
* Hyper Protect Virtual Server instance
	* Follow steps here for assistance provisioning a Virtual Server {insert URL at here}

* Hyper Protect DBaaS for MongoDB instance
	* Follow steps located {here - url} for assistance provisioning a Hyper Protect MongoDB

* Ubuntu package 'git' must be installed on the Virtual Server for this lab. Please access the Virtual Server via ssh protocol, and run the following command: _sudo apt-get install -y git_
	* After the package has finished installing, verify the installation by executing command _git --version_

* Install 'npm' on Virtual Server using  _sudo apt-get -y install npm_
	* The _npm_ package manager is required for the NodeJS platform
	* To verify the installation of _npm_ type in command _npm -v_

* Install 'docker' on the Virtual Server using command _sudo apt-get -y install docker.io
	
	* verify that docker was installed correctly using _docker --version_
		* If required, type in _systemctl |grep docker_ and the output should tell you if the Docker service was installed. If the service is present yet disabled, start the service using  _sudo systemctl start docker_


<br/>

# Configuration Steps

1. Access the Hyper Protect Virtual Server via ssh
	* Instructions on how to access the VS can be found in the Prerequisite section above.


2. Clone the 'carekit-apple' Github repository on the provisioned HP Virtual Server using the following command: _git clone https://github.com/carekit-apple/CareKit.git_
	* See the afforementioned prerequisite section for assistance installing _git_
	* Note: This repository contains the CareKit's frontend (UI)


3. One additional repo is required for this configuration, run this command: _git clone https://github.com/carekit-apple/HyperProtectBackendSDK.git_
	* This particular repository contains the application backend written in typescript, utilizing TypeORM.


4. Within the Virtual Server, change the current directory to the recently cloned backend repository.
	* Changing directories can be achieved by using _cd HyperProtectBackendSDK-master_


5. An environmental variable file (.env) has been created in the root directory, it is imperative that we add the necessary MongoDB options to our environment, which includes; username, password, and db uri
	* Open up the '.env' file, and set the following values based on the information that the DBaaS MongoDB instance was created with
		* MONGO_USER={MongoDB username} - ID was created during the provisioning of the DBaaS instance
		* MONGO_PASS={MongoDB password} - Password was also created during the provisioning of MongoDB
		* MONGO_DB={mongodb://dbaasXX.hyperp-dbaas.cloud.ibm.com:XXXX...}
			* Fill in full cluster URI, which should consist of 3 total DBaaS replica endpoints


6. Run the 'npm' installation by using command _npm install_ from the root directory of the Github repo {enter name here once finalized}
	* The _npm install_ process will install all of the required packages and dependencies needed to run the CareKit application
	* Ensure that the ts-node version is **greater** than 3.3.0, as several compiler errors will occur during the next step if an older version is used.


7. Finally, start the application backend by executing the _npm start_ command. This particular command will initialize the application, and bring the application online leveraging port 3000. 
	* If the _npm start_ execution was successful, the message stating that 'Server started on port 3000' should propagate.


