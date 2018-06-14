# HadoopSummitCloudbreak
Crash Course for Cloudbreak for Data Works Summit 2018 San Jose.
- [Prerequisites](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_prerequisites.md)
  - a. Before launching Cloudbreak on AWS, you must meet the [AWS prerequisites.](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_prerequisites.md)
  - b. Before launching Cloudbreak on Azure, you must meet the [Azure prerequisites.](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/azure_prerequisites.md)

- [1. Log into the Cloudbreak application](#1-log-into-the-cloudbreak-application)
  - [a. Confirm the security exception](#a-confirm-the-security-exception)
  - [b. Login page](#b-login-page)
  - [c. Create Cloudbreak Credentials](#c-create-cloudbreak-credentials)
- [2. Creating an HDP cluster on AWS](#2-create-an-hdp-cluster-on-aws)
  - [a. General Configuration](#a-hdp-general-configuration)
  - [b. Hardware and Storage](#b-hdp-hardware-and-storage)
  - [c. Gateway Configuration](#c-hdp-gateway-configuration)
  - [d. Network](#d-hdp-Network)
  - [e. Security](#e-hdp-Security)
  - [f. Cluster Summary](#f-hdp-cluster-summary)
  - [g. Ambari](#g-hdp-ambari)      
- [3. Accessing a cluster](#3-accessing-a-cluster)
  - a. Finding cluster information in the web UI
  - c. Cluster summary
  - d. Cluster information
  - e. Event history
  - f. Accessing cluster via SSH
  - g. Access Ambari
- [4. Managing and monitoring clusters](#4-managing-and-monitoring-clusters)
  - [a. Resize a cluster](#a-Resize-a-cluster)
  - [b. Synchronize a cluster](#4-managing-and-monitoring-clusters)
  - [c. Stop a cluster](#4-managing-and-monitoring-clusters)
  - [d. Restart a cluster](#4-managing-and-monitoring-clusters)
  - [e. Terminate a cluster](#4-managing-and-monitoring-clusters)
  - [f. Force terminate a cluster](#4-managing-and-monitoring-clusters)
  - [g. View cluster history](#4-managing-and-monitoring-clusters)
  - [h. History report content](#4-managing-and-monitoring-clusters)
- [5. Autoscaling](#5-autoscaling)
  - [a. Enable Auto Scaling](#a-enable-auto-scaling)
  - [b. Defining an Alert](#b-defining-an-alert)
  - [c. Create a Scaling Policy](#c-create-a-scaling-policy)
  - [d. Configure Autoscaling Settings](#d-configure-autoscaling-settings)
- [6. Creating an HDF cluster on AWS](#6-creating-an-hdf-cluster-on-aws)
  - [a. General Configuration](#a-general-configuration)
  - [b. Hardware and Storage](#b-hardware-and-storage)
  - [c. Gateway Configuration](#c-gateway-configuration)
  - [d. Network](#d-network)
  - [e. Security](#e-security)
  - [f. Cluster Summary](#f-cluster-summary)
  - [g. Ambari](#g-ambari)
---------------

# Cloudbreak launches clusters on the cloud in 3 easy steps:
  - 1. Pick a Blueprint: Cloudbreak uses [Ambari Blueprints](https://cwiki.apache.org/confluence/display/AMBARI/Blueprints)  to have declarative Hadoop cluster definition. Blueprints can be designed for specialized applications and workloads (such as Data Science or IoT Apps). Cloudbreak includes a few default Blueprints for common cluster configurations but you can always upload your own Blueprint to build the cluster just the way you like it.
  - 2. Choose a Cloud: Cloudbreak is configured to work with cloud infrastructure resources (such as servers, network setup and security options). Choose the cloud infrastructure you want to use for the cluster.
  - 3. Launch Cluster: In this step, Cloudbreak obtains the chosen cloud infrastructure platform, installs Apache Ambari and applies the desired Blueprint. The result: your cluster is launched and ready to go!

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/3EasySteps.png)

## 1. Log into the Cloudbreak application

#### a. Confirm the security exception
Access https://cloud.eng.hortonworks.com/ 
Click on Advance and then proceed to cloudbreak server.
  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AdvancedConnectionWarning.png)
  
#### b. login page
Cloudbreak login page. Credentials will be provided for these services by the instructor. 

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/CB_login.png)

#### c. Create Cloudbreak Credentials
Before launching Cloudbreak on AWS, you must meet the [prerequisites.](aws_prerequisites.md)  
The first thing you need are credentials to a cloud provider of your choice. 
1. Click on Credentials in the right menu   
2. Then click on Create Credentials  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Credentials_1.png)

Pick the cloud provider of your choice

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Credentials_2.png)

Get the Access Key and Secret Key from the [Prerequisites section](aws_prerequisites.md#1-Key-based) 

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Credentials_3.png)


## 2. Create an HDP cluster on aws 
  
###  a. HDP General Configuration
Click the Create Cluster button and the Create Cluster wizard is displayed.

By default, Basic view is displayed.
**Select Credentials** Choose a previously created credential  
**Cluster Name**: Enter a name for your cluster. The name must be between 5 and 40 characters, must start with a letter, and must only include lowercase letters, numbers, and hyphens  
**Region**: Select the region in which you would like to launch your cluster  
**Cluster Type**: Choose one of default cluster configurations  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/GeneralConfig27.png)

### b. HDP Hardware And Storage
Go with default storage options

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/HWStorage27.png)

### c. HDP Gateway Configuration   
When creating a cluster, Cloudbreak installs and configures a gateway, powered by Apache Knox, to protect access to the cluster resources: This gateway is installed on the same host as the Ambari server.  
By default, the gateway is deployed and Ambari is proxied through the gateway.  
The choice of cluster services to expose and proxy through the gateway depends on your blueprint.   

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Gateway.png)
  
### d. HDP Network
Go with default Network setup

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Network27.png)


### e. HDP Security
Provide the following:  
**Cluster User**: This will be the user that you should use to log in to Ambari and other cluster UIs. By default, this is admin.  
**Cluster Password**: Password for the cluster user.  
**SSH public key**: Select the existing public SSH key or paste your key. The key will be placed on the cluster VMs so that you can use the matching private key to access the VMs via SSH. [You can get this from the prerequisites section](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/aws_prerequisites.md#ssh-key-pair)

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Security27.png)

### b. Advance Cluster Options
Once your cluster is up and running, click on the tile representing your cluster in the Cloudbreak UI to access information related the cluster and access cluster actions.

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AccessCluster_1.png)

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AccessCluster_2.png)
  
 The information presented includes:  

  - Cluster summary
  - Cluster information
  - Event history

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AccessCluster.png)
  
  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ClusterAdvanceOptions.png)

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AdvPreWarmed.png)

## 3. Accessing a Cluster

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ClusterInfo.png)

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ConnectionWarning.png)


## 4. Managing and Monitoring Clusters
Click on Clusters in the right menu, then click on a cluster name to see details.  
- a.Resize a cluster
- b.Synchronize a cluster
- c.Stop a cluster
- d.Restart a cluster
- e.Terminate a cluster
- f.Force terminate a cluster
- g.View cluster history
- h.History report content

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ManageCluster2.png)

### a. Resize a cluster

To Resize a cluster you can either add or remove nodes from a hostgroup. In this example, the Host Groups are worker and compute. Click Resize.    

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Resize.png)

Cluster Resize window pops up.  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Resize2.png)

By default this cluster has 0 nodes in compute Host Group. Choose compute Host Group and increase nodes from 0 to 1.  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Resize3.png)

A new Host Group line item for compute shows up in the HARDWARE tab. Note that the ID, FQDN (Fully Qualified Domain Name), Private & Public IPs are all N/A at this point.  
Log information about adding 1 new instance to the infrastructure also shows up in the Event History. You can continue watching this space as events happen, they are logged here. 

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Resize5.png)

Finally when the instance is created the compute Host Group line item has all the key information like ID, FQDN and IPs.  
  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ResizeResult.png)

All the log information is also captured.  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ResizeEventLog.png)

Alternatively you can also flip over to AWS view and see the instance being created.  You will now see a new instance with the name pkdatalake-276-compute.  

  ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ResizeAWS.png)

For additional details visit [Cloudbreak documentation](https://hortonworks.github.io/cloudbreak-documentation/latest/index.html)


## 5. Autoscaling
  
##### a. Enable Auto Scaling  
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/EnableAutoscaling.png)

##### b. Defining an Alert: 
After you have enabled autoscaling, define a metric-based or time-based alert.
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/Alert.png)

##### c. Creating a Scaling Policy
1. In the Policy Configuration section, provide needed information:
2. Click + to save the alert
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/PolicyConfiguration.png)
   
##### d. Configure Autoscaling Settings:
After enabling autoscaling, perform these steps to configure the auto scaling settings for your cluster.
  - 1. In the Cluster Scaling Configuration, provide the following information:
      - Cooldown time: After an auto scaling event occurs, the amount of time to wait before enforcing another scaling policy.	
      - Minimum Cluster Size:	The minimum size allowed for the cluster. Auto scaling policies cannot scale the cluster below or above this size.
      - Maximum Cluster Size:	The maximum size allowed for the cluster. Auto scaling policies cannot scale the cluster below or above this size.
  - 2. Click Save to save the changes.

   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/ScalingConfiguration.png)

##### 2 new Worker nodes are being requested at 21:33 as per the Time based Alert
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AutoScaledHistory_1.png)

##### 2 new Worker nodes are created.
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AutoScalesHistory_2.png)

Look in Azure Dashboard for the newly created nodes.
   ![Image](https://github.com/purn1mak/HadoopSummitCloudbreak/blob/master/AutoscaledNodesAzure.png)

## 6. Creating an HDF cluster on AWS
As of Cloudbreak 2.7, you can deploy Hortonworks Data Flow (HDF) clusters.  Currently there are two HDF cluster types supported: Flow Management (NiFi) and Messaging Management (Kafka).  We will walk you through deploying an HDF 3.1 Flow Management cluster using Cloudbreak 2.7.

In the left manu, click on `Clusters`.  Cloudbreak will display configured clusters.  Click the `CREATE CLUSTER` button.  Cloudbreak will display the Create Cluster wizard

#### a. General Configuration

By default, the General Configuration screen is displayed using the `BASIC` view.  The `ADVANCED` view gives you more control of AWS and cluster settings, to include tags.  You can change your view to `ADVANCED` manually or you can change your Cloudbreak preferences to show `ADVANCED` view by default.  We wil use the `BASIC` view.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/hdf-general-configuration.png)

**Credential**: Select the AWS credential you created.  Most users will only have 1 credential per platform which will be selected automatically.

**Cluster Name**: Enter a name for your cluster. The name must be between 5 and 40 characters, must start with a letter, and must only include lowercase letters, numbers, and hyphens.

**Region**: Select the region in w`hich you would like to launch your cluster.

**Platform Version**: Cloudbreak currently defaults to HDP 2.6.  Select the dropdown arrow and select `HDF 3.1`.

**Cluster Type**: As mentioned previously, there are two supported cluster types.  We'll select the `Flow Management` clsuter type.  This will allow us to deploy a an HDF/NiFi cluster.

Click the green `NEXT` button.

#### b. Hardware and Storage

Cloudbreak will display the `Hardware and Storage`screen.  On this screen, you have the ability to change the instance types, attached storage and where the Ambari server will be installed.  As you you can see, we will deploy 1 NiFi and 1 Zookeeper node.  In a prodution environment you would typically have at least 3 Zookeper nodes.  We will use the defaults.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/hdf-hardware.png)

Click the green `NEXT` button.

#### c. Gateway Configuration

Cloudbreak will display the `Gateway Configuration` screen.  On this screen, you have the ability to enable a protected gateway.  This gateway uses Knox to provide a secure access point for the cluster.  Cloudbreak does not currently support configuring Knox for HDF.  We will leave this option disabled.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/hdf-gateway.png)

Click the green `NEXT` button.

#### d. Network

Cloudbreak will display the `Network` screen.  On this screen, you have the ability to specify the `Network`, `Subnet`, and `Security Groups`.  Cloudbreak defaults to creating new items.  For production use cases, we highly recommend creating and refining your own definitions within the cloud platform.  You can tell Cloudbreak to use those via the drop down menus.  We will use the default options to create new.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/hdf-network-1.png)

Click the green `NEXT` button.

#### e. Security

Cloudbreak will display the `Security` screen.  On this screen, you have the ability to specify the Ambari admin username and password.  You can create a new SSH key or selecting an existing on.  And finally, you have the ability to enable Kerberos on the cluster.  We will use `admin` for the username and `BadPass#1` for the password.  Select an existing SSH key from the drop down list.  We will NOT be enabling Kerberos.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/hdf-security.png)

You have the ability to display a `JSON` version of the blueprint.  You also have the ability display a `JSON` version of the cluster definition.  Both of these can be used with Cloudbreak CLI to programatically automate these operations.

Click the green `CREATE CLUSTER` button.

#### f. Cluster Summary

Cloudbreak will display the `Cluster Summary` page.  It will generally take between 10-15 minutes for the cluster to be fully deployed.  As you can see, this screen looks similar to and HDP cluster.  The big difference is the `Blueprint` and `HDF Version`.


   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/cb-cluster-summary.png)

Click on the `Ambari URL` to open the Ambari UI.

#### g. Ambari

You will likely see a browser warning when you first open the Ambari UI.  That is because we are using self-signed certificates.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/ambari-browser-warning-1.png)

Click on the `ADANCED` button.  Then click the link to `Proceed`.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/ambari-browser-warning-2.png)

You will be presented with the Ambari login page.  You will login using the username and password you specified when you created the cluster.  That should have been `admin` and `BadPass#1`.  Click the green `Sign In` button.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/ambari-login.png)

You should see the cluster summary screen.  As you can see, we have a cluster with Zookeeper, NiFi, and the NiFi Registry.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/ambari-summary.png)

Click on the `NiFi` service in the left hand menu.  Now you can access the `Quick Links` menu for a shortcut to the NiFi UI.

   ![Image](https://github.com/jaraxal/HadoopSummitCloudbreak/blob/master/ambari-nifi.png)
