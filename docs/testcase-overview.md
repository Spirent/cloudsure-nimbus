# CloudSure-n Test Case Overview
A testcase is set of actions that will be performed on one or more targets while measuring the resulting impact in a specific enviroment. 

 Each testcase consists of following sections, and each section contains one or more mandatory attributes as well as possibly some optional. 

1. [Information](#information)
2. [Environment](#environment)
3. [Scenarios](#scenarios)
4. [Observability](#observability)
5. [Analytics](#analytics)

> Note: Every testcase requires all of the these sections, except analytics which is optional. 

## Information
This section provides basic information about each testcase, and includes the following attributes:

- **Testcase Name:** A short meaningful name to make a testcase easy to find.
- **Testcase Description (optional):** This is a more verbose statement about the testcase that makes it clearer what it does.
- **Project Name:** This user-defined grouping of test cases.
- **Project Description (optional):** This is a more verbose statement about the Project that makes it clearer what it is for.
- **Unique ID:** This is to simplify to the identification of a testcase using the common format of "XXX-123". Not two testcases can have the same number.
- **Date Created/Updated** This is the date when the testcase created or updated a testcase.
- **Creator/Updator:** This is the name of the person who created or updated a testcase.
- **Tags (optional):** These are single word descriptors, or keywords that allow a user to more easily search.

> Note: Only Testcase Name/Description and Project Name/Description are supported currently. 

## Environment
This section defines where a testcase will be executed.  This is typically a Kubernetes namespace, cluster, etc, and is defined a user's account and access rights.

A testcase can include all the Environment's attributes within within the testcase itself, or (and more perferrably) point to a seperate Enviroment spec by name.

Here are the Environment attributes:

- **Environment Name:**
- **Auth Type:**
- **API Endpoint:**
- **Certification Authority Data:**
- **Client Certification Data:**
- **Client Key Data:**

> Note: Description to be added. 

## Scenarios
This is the section of the testcase that defines the actions to be performed on one or more targets. Each testcase consists of at least one scenario, but also could have multiple scenarios. 

Each scenario will include a delay option, and all but the first with have a timing aspects relative to the sequence. 

Lastly, each scenario includes one or more actions.

Each scenario has the following attributes:
- **Scenario Name:** A short meaningful name to make a scenario easy to find.
- **Scenario Timing:**
    - **Scenario Start:** This defines if this Scenario will start "After Previous Scenario" or "With Previous Scenario"
    - **Scenario Delay:** This defines the amount of time in seconds.  This Scenario will wait before starting.  

- **Action(s):** 

    Each scenario consists of at least one action, but also (more typically) could have multiple actions. 

    If more than one action are required, they are in a sequentional list, and each action (other than the first) will include a timing aspects relative to the sequence. 
    
    Each  action has the following attributes:
  - **Action Name:** A short meaningful name for an action.
  - **Action Type:** This is the category that an action is from.  Initially, the following types are supported: Impairment and Load (5G).
  - **Action Target(s):** This attibute is used in combination with actions that can target specific Kubernetes objects.

  - **Action Settings:** Some actions will have one or more settings, and they will vary depending on the specific action.


    See [Impairment Actions](#impairment-actions) or [Session Actions](#session-actions) for relevant details about how to select targets, the use settings or controls for each type of action.
  
  - **Action Timing:**
    - **Action Start:** This defines if this Action will start "After Previous Action" or "With Previous Action"
    - **Action Delay:** This defines the amount of time in seconds  this Action will wait before starting.  

   ### Impairment Action

   Here are the currently supported impairment actions in three groups:

   Network Contention
    - [Network Latency](#network-latency)  
    - [Packet Loss](#packet-loss)
    - [DNS Disruption](#dns-disruption)
   
   Object Failure
    - [Container Failure](#container-failure)
    - [Pod Failure](#pod-failure)
    - [Node Failure](#node-failure)
   
   Resource Constraint 
    - [Node Drain](#node-drain)
    - [Node Taint](#node-taint)
    - [Pod CPU Hog](#pod-cpu-hog)
    - [Pod Disk Full](#pod-disk-full)
    - [Pod Memory Hog](#pod-memory-hog)
    - [Node Contention](#node-contention)

    #### Network Latency

    - **Target Selection**
            
        Network Latency can be applied to traffic destined for one or more containers or pods in a specific namespace.

        - **Selecting by Pod:** A pod can be selected by the namespace, name, label, DeploymentSet, StatefulSet.  The pod name and label can be selected by full name or partial match (i.e. "Regex").

        - **Selecting by Container:** A container can be selected by the name or label, and can be selected by full name or partial match (i.e. "Regex").

    - **Settings**
        - **SSH:**
        - **Network Device:**
        - **Destination Address:**
        - **Selection Method:** Selection Count, Selection Percent
        - **Duration:**
        - **Delay:**
        - **Progression:** None, List, Steps
        - **Latency Amount:**

    #### Packet Loss
    - **Target Selection**
            
        Packet Loss can be  applied to traffic destined for one or more containers or pods in a specific namespace.

        - **Selecting by Pod:** A pod can be selected by the namespace, name, label, DeploymentSet, StatefulSet, name and label can also be seleted by "Regex" or partial match.

        - **Selecting by Container:** A container can be selected by the name or label by "Regex" or partial match.

    - **Settings**
        - **SSH:**
        - **Network Device:**
        - **Destination Address:**
        - **Selection Method:** Selection Count, Selection Percent
        - **Duration:**
        - **Delay:**
        - **Progression:** None, List, Steps
        - **Packet Loss Amount:**

    #### DNS Disruption
    - **Selecting Targets**

        DNS Disurption can be  applied to traffic destined for one or more containers or pods in a specific namespace.

        - **Selecting by Pod:** A pod can be selected by the namespace, name, label, DeploymentSet, StatefulSet, name and label can also be seleted by "Regex" or partial match.

        - **Selecting by Container:** A container can be selected by the name or label by "Regex" or partial match.

    - **Settings**
        - **SSH:**
        - **Network Device:**
        - **Destination Address:**
        - **Selection Method:** Selection Count, Selection Percent
        - **Duration:**
        - **Delay:**
        - **Progression:** None, List, Steps
        - **DNS Disruption Amount:**

    #### Container Failure
    - **Target Selection**
    - **Settings**

    #### Pod Failure
    - **Target Selection**
    - **Settings**
    #### Node Failure
    - **Target Selection**
    - **Settings**

    #### Node Drain
    - **Target Selection**
    - **Settings**

    #### Node Taint
    - **Target Selection**
    - **Settings**

    #### Pod CPU Hog
    - **Target Selection**
    - **Settings**

    #### Pod Disk Full
    - **Target Selection**
    - **Settings**

    #### Pod Memory Hog
    - **Target Selection**
    - **Settings**

    #### Node Contention
    - **Target Selection**
    - **Settings**

    ### Session Actions
    
    A Session Action is defined by (synonymous with) a LandSlide Test Session, and a each scenario can have a single LandSlide Test Session.  A testcase can have different LandSlide Test Sessions in different scernarios.
    
    Each Load (5G) Action can be one of the following controls:

    - **Start:** This will start a new LandSlide Test Session by name within a desired library.  This control also allows the user to override key values of the given session.
    - **Stop:** This will stop a LandSlide Test Session by name that has already been started.
    - **Resume:** This will resume a LandSlide Test Session by name that has been put into a wait state with the test session.

## Observability
> Still needs to be defined

This will start at the beginning of the Test Case, and will provde an option to extend metrics collection beyond the end of the Test Case.

The targets will be selected from: container, node or kubestate metrics. 

Metrics Controller URL

Select
Metrics Controller API Key

Verify Metrics Controller Certificate
ON
InfluxDB Configuration
Write Metrics to TC IQ
OFF
Write Metrics to CSV
OFF
Metrics Fetch Parameters
Error Interval (sec)



Fetch Interval (sec)



Maximum Window (sec)



Readiness (sec)




## Analytics
> Still needs to be defined