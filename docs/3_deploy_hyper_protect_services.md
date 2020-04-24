- - - -
# Deploying a Hyper Protect Virtual Server and Hyper Protect DBaaS for MongoDB instance tutorial

- - - -

Goal : At the end of this section, you should have a production ready MongoDB instance from IBM Hyper Protect DBaaS and a secure container environment from IBM Hyper Protect Virtual Servers to deploy the TypeScript server on.

* * *

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


## Connecting to your Virtual Server

Now that both required Cloud services have been deployed, it is time to access the newly provisioned virtual server using ssh protocol
	
* To obtain the public IP address of the virtual server, navigate to the Cloud dashboard homepage, and click on 'Services' in the Resource Summary box. Once the deployed services are listed, locate the Hyper Protect virtual server instance and click on the name. The public IP address will be displayed on the following screen.
  
  * After finding the public IP address, access a terminal and leverage the ssh protocol to navigate to the virtual server.
	   * Example ssh command: ssh root@{public_IP}
		
	* The ID required for a successful ssh connection must be 'root'

**You should now be successfully connected to your Virtual Server!**


- - - -
### Useful Links:
HPVS Documentation: https://cloud.ibm.com/docs/services/hp-virtual-servers?topic=hp-virtual-servers-getting-started
<br/>

DBaaS Documentation: https://cloud.ibm.com/docs/services/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-gettingstarted
