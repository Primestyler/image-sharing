
<p align="center">
  <img src="https://github.com/Primestyler/image-sharing/blob/main/arc42/images/arc42-logo.png" alt="Fancygram Logo" width="300"/>
</p>

<div class="note">

This version of the template contains some help and explanations. It is
used for familiarization with arc42 and the understanding of the
concepts. For documentation of your own system you use better the
*plain* version.

</div>


<div style="page-break-after: always;"></div>



# Fancygram Documentation - arc42

---
<p align="center">
  <img src="https://github.com/Primestyler/image-sharing/blob/main/arc42/images/fancy-logo.png" alt="Fancygram Logo" width="400"/>
</p>

*Version 9.2*

*Date: 12.12.2023*

---

## Team

- Lin Hao
- Hickelsberger Alexander
- Kalarickal Dominic

---
<div style="page-break-after: always;"></div>


# Table of Contents

1. [Introduction and Goals](#introduction-and-goals)
2. [Architecture Constraints](#architecture-constraints)
3. [System Scope and Context](#system-scope-and-context)
4. [Solution Strategy](#solution-strategy)
5. [Building Block View](#building-block-view)
6. [Runtime View](#runtime-view)
7. [Deployment View](#deployment-view)
8. [Cross-cutting Concepts](#cross-cutting-concepts)
9. [Architecture Decisions](#architecture-decisions)
10. [Quality Requirements](#quality-requirements)
11. [Risks and Technical Debts](#risks-and-technical-debts)
12. [Glossary](#glossary)




<div style="page-break-after: always;"></div>

# Introduction and Goals

Fancygram will be a unique Social Media Platform where users can share their stunning images. These exceptional images can be modified by the in-app editing program. Our mission is to connect like minded individuals through their visual expressions. User cannot only share their images, but also their editing tips and tricks. The community will be challenged with engaging competitions and task where user interaction will be the key to winning. 

To ensure that every stakeholder is satisfied Fancygram will meet the requirements of diverse Data protection guidelines so that its users can trust the team and. The system should also be designed for accessibility and consistency for the best user experience. The system should be designed for minimal downtime and best user experience. 



## Requirements Overview

<div class="formalpara-title">

</br>

| Feature                           | Use Case                                                                             |
|---------------------------------------|------------------------------------------------------------------------------------------|
| Photo Editing with Advanced Tools | Users creatively modify images using an array of advanced editing tools.                 |
| Image Sharing and Sorting          | Users upload, organize, and share their images, creating personalized galleries.         |
| Export to other social media                  |Users can export images to various external social media platforms to share their masterpieces. |
| Share Editing Tips and Techniques | Users exchange insights, techniques, and tutorials, fostering a culture of learning.        |
| Challenges and Competitions       | Users create and participate in challenges, adding a gamified layer to the platform.      |

## Quality Goals

<div class="formalpara-title">
</div>

| Quality Goals |               |                                                                                                           |
|---------------|---------------|-----------------------------------------------------------------------------------------------------------|
| Priority      | Quality       | Motivation                                                                                                |
| 1             | Usability     | Users are more likely to continue using the app, recommend it to others                                   |
| 2             | Reliability   | A trustworthy app builds trust with users and they are more likely to rely on it for sharing their images |
| 3             | Compatibility | Users should be able to use the app on their preferred devices.                                           |

</div>

<div class="formalpara-title">
</div>


## Stakeholders

<div class="formalpara-title">

|     Role/Name                        |  Contact details                  |     Expectations                                                                                                     |
|--------------------------------------|-----------------------------------|----------------------------------------------------------------------------------------------------------------------|
|     Photography enthusiast/expert    |  Lucas.Rodriguez@gmail.com        |     Multifunctional editing tool. Sharing   their images/filters with others                                         |
|     Pixlr                            |  pix.lr@gmail.com                 |     An app which uses and incorporates good   features                                                               |
|     Financial department             |  Laura.Kraner@gmail.com           |     A good pricing to the app which   provides the necessary funds for the company                                   |
|     Marketing Manager                |  Sahra.chen@gmail.com             |     Unique selling points and features to   highlight in promotional materials     Insight to the target audience    |
|     Indian bilionaire               |  dominig.Kalikal.senior@gmail.com |     A user friendly app with good community guidelines and no explicit content                                       |

</div>

<div style="page-break-after: always;"></div>

# Architecture Constraints

<div class="formalpara-title">

### Technical Constraints 
| ID  | Constraints                                       | Background and/or Motivation                                                                                                                                                                                                                                |
|-----|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| TB1 | Memory friendly                                   | Memory can be limited (due to availability on a shared host or deployment to cloud based host).  If deployed to a cloud based solution, every megabyte of memory costs this especially effects us  due to us being a startup and not well funded as of now. |
| TB2 | Deployable to a Linux server                      | Linux is suitable for industries that require customization, flexibility,  and low cost which we would prefer in the early stages of our project.                                                                                                           |
| TB3 | Third party software must be available (PIXLR)    | Third party services libraries have their own requirements and limitations.  Furthermore licensing is key with these services, however it has to be confirmed  that the used filters fulfill our requirements and guidelines.                               |
| TB4 | Data and Privacy regulations  (EU, USA and China) | Due to the large amount of data stored from the various user some guidelines  need to be upheld for the safety of our users as well as protection from legal repercussions.                                                                                 |
| TB5 | Budget requirements                               | As a startup we only have a small budget (100 000 EUR).                                                                           

### Organizational Constraints
| ID  | Constraints | Background and/or Motivation                                        
|-----|-------------|---------------------------------------------------------------------|
| OB1 | Team        | The team consists of Lin Hao, Hickelsberger Alexander and Kalarickal Dominic. |

<div style="page-break-after: always;"></div>

# System Scope and Context

<div class="formalpara-title">
    
### Buisness Context
 <div style="text-align: center;"> 

![image](https://github.com/Primestyler/image-sharing/assets/127980400/12221d3e-08cf-4863-8c23-88d58a6a1659)
</div>


| User/System      | Description                                  | Input                               | Output                                                 |
|------------------|----------------------------------------------|-------------------------------------|--------------------------------------------------------|
| User             | The user interacting with Fancygram          |                                     |                                                        |
| Fancygram        | The image sharing app                        | Receives image uploads              | Edited images and storage of edited images             |
| AWS              | Cloud storage service                        | Server request                      | Stores and retrieves images and user data in the cloud |
| Pixlr            | Image editing service providing filters      | Receives filter request             | Provides Filter                                        |
| Social Media     | User are connected on social media           | Edited images from fancygram        | Displays shared images on respective platforms         |
| Filters Database | Database storing custom and pre-made filters | Retrieves filters for image editing | Stores and updates filters for future use              |

## Technical Context

<div class="formalpara-title">
 <div style="text-align: center;"> 

![Technical Context](images/technicalContext.png)
</div>

**Contents**

</div>

| Component                   | Description                                                                                                                                                                                                  | Input                          | output                                  |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------|-----------------------------------------|
| Web Server                  | The web server is responsible for handling HTTP requests and responses, serving as an API gateway.                                                                                                           | http requests                  | http response with requested data       |
| App Server 1,2              | Execute server-side application logic, handling the editing of our pictures, and creating a connection to our AWS databases.                                                                                 | Request from Web Server        | Response of processed request           |
| Database                    | Central database where user data, images and filters are stored and retrieved.                                                                                                                               | SQL commands and/or Data       | Data                                    |
| Cache                       | We implemented a caching layer to increase our performance speed. A more detailed explanation is accessible in the point Deployment view.                                                                    | Data                           | cached Data or messages related to data |
| Backend                     | With microservices being our architecture and our platform being available for web, IOS and Android we used backend as a placeholder for the various programming languages.                                   | service request                               |  server answer                                       |
| Frontend                    | With microservices being our architecture and our platform being available for web, IOS and Android we used frontend as a placeholder for various Libraries, styling languages as well as formatting elements. | user interactions              | update page                             |
| PostgreSQL                  | Is used as a relation database model. It not only is open source but also is compatible with AWS and is even offered as integrated service by Amazon (Amazon RDS (Relational Database Service))              | commands                        | data                                    |
| External Service (Database) | Represents an external service, such as AWS , facilitating seamless integration with Pixlr.                                                                                                                  | requests from front or backend | Filters                                 |


<div style="page-break-after: always;"></div>

# Solution Strategy

We want to archive consistency, easy deployment, and updates by using microservices architecture. This will make sure that Fancygram will be more resilient to failure and or overload. This should run smoothly because as time approaches, more of the commodity will be demanded. Therefore, we want to design a flexible system which is expected to increase in size as more people are using the app. Through this, Fancygram would capture more users, photographs, many other things. This way, we can predict on how Fancygram could grow with its increasing user base. The reason we selected Bootstrap is to give Fancygram a simple but beautiful view. This is all about designing a simple atmosphere of Fancygram platform. 
Moreover, we have addressed some big concerns and questions raised on the technological options. First, we have chosen AWS simply for its dependability since it will be easy to scale as the business expands. We have an agile approach, which keeps our flexibility high and improves interactions among team members. Using Java for our web applications and a fast API(MQTT) design so that microservices can communicate with each other efficiently.


<div style="page-break-after: always;"></div>

# Building Block View

**Level 1**

Our system consists of eight main groupings. The Editor is our main program which is our company developed. The other Block interact with outer systems to provide information to our editing tool. As portrayed in the diagram bellow these consist of an upload to various social media platforms, a cloud storage system , a payment option as well as location services    
 <div style="text-align: center;"> 

![level one Building Block View](images/Builidng_Block_View_levele_1.png)
 </div>
 
 1. **uploads**: are responsible for distributing our edited images to outer systems. It can stand alone and be used to upload different files to other platforms if utilized for a different sales point. 

 2. **payment**: controls the flow of money in our company. Moreover it also regulates which content is permitted to specific users, by passing on order confirmations to the user management. 
 
 3. **User management**: transfers user data to the editor to permit certain features. Moreover this Block handles the users and allows them to log in and sign up and manage their accounts. This can also be done by system administrators

 4. **Location**: is used to accurately portray the current location of the users in images (if they want to and allow the function) so that they can share it to their community and show it as a sign of status. Moreover it helps customize certian features and filters for countries as well as language settings. This can however be disabled within the users device.

5. **File storage system AWS**: is used to store filters, pictures and data.  this cooperates with user management and the editor aswell as the filters supplied and stored by pixlr. 

6. **Filters**: are responsible for allowing users to saave and expand filters created by the editing tool and linking them to the Filters from Pixlr.
 
7. **Editor**: This component is the heart of our System. It can be used to modify images and filters aswell as layer these. 

8. **Pictures**: is used to check image formats and convert them in case of not accesped formats. Moever this block allows user to apply filters while taking pictures.

**Level 2** 

 **Editor**
 
 The editor consists of 7 blocks of which 3 communicate with outer systems. these allow the editor to accept pictures, export them through uploads as well as customizing filters. 

 <div style="text-align: center;"> 

 ![level two editor Building Block View](images/Builidng_Block_View_level_2_editor.png)

 </div>

1. **Picture editing**: consists of the user operating the tools inside the app and utilizing them to improve the images.

2. **Remodelling tools**: provides the necessary tools to customise images as well as filters to improve them to the specific needs of the user

3. **Layer management**: allows the user to apply more than one filter onto images or even layer filters over each other to create a new one. This can also be restricted due to free and premium user imbalance.

4. **Effects and filters**: contain the already created filters with certain effects which have already been created. This includes already layered effects.

5. **Text tools**: consist of all different elements used to output
text onto images and filters. these can also be incorporated with location services to accurately portray locations and situations.

6. **Customized filters**: allows the user to use various editing tools to create new filters as well as layer different existing filters.

7. **Export**: This block prepares edited images to be shared to various social media sites.

**Picture**

This component deals with the upload of images to our app/ page. This also includes applying filters to certain images in the upload as well as a format conversion.

 <div style="text-align: center;"> 

![level two editor Building Block View](images/layer2-picture.png)
</div>

1. **Virus checker**: check if the file is not corupted and all data still works.

2. **Format checker**: check format to ensure it can be handeld from our system.

3. **Image converter**: if the format doesnt match the needed format, it gets converted to png so it can be edited on our application.

4. **Filter Applicator**: filters can be applied to the image when uploaded.

**User Management**

User management includes the transfers of user data to the editor to permit certain features. Moreover this Block handles the users and allows them to log in and sign up as well as manage their accounts. This can also be done by system administrators.

 <div style="text-align: center;"> 

![level two editor Building Block View](images/layer2-user-management.png)
</div>

1. **Data saver**: Controlls the data of the user and the inputs while registering. they then can be processed and stored to a database.

2. **Data revison**: entered data can be revised and changed. The changed values of course get validated again and then stored in the database

3. **account permission**: The value if a payment has occured from this account is revieced from the financial division and then the permsissions can be passed on to the editor. Furthermore this also entails the oportunity to advertise and add the posiblity of further payments to this account.

**Locations** 

stores locations with timestamps in near realtime and provides access to locations for the last 30 minutes

 <div style="text-align: center;"> 

![level two editor Building Block View](images/layer2-location.png)

</div>

1. **LocationController**: manages the current locations needed for the app to post them on your images.

2. **LocationMessaging**: this allows users transfer thier real time locations so that the app can present other users who are in their proximity.

3. **LocationsListener**: Gets the timezones aswell as the current time at the specified location.

4. **LocationService**: retrieve current coordinates of the user to accurately display them on the app allowing them to interact with users nearby as well as displaying it on their profile.

5. **LocationRepository**: stores locations of the past 30 min so that they can be used by the user for socialising with other users.


**Level 3** 

**Editor-Remodeling Tools**

 <div style="text-align: center;"> 

![level three editor Building Block View](images/Builidng_Block_View_level_3_remodelingtools.png)
</div>

1. **Artistic effects**: are different images, emojis, gifs and tools which can be used to style and improve images and filters.

2. **Filter effects**: are applied to images or layered over other filters to create a new style of an image or a new filter.

3. **colour corrections effects**: are used to correct or improve contrasts of light or colours to make it more appealing for the user.

<div style="page-break-after: always;"></div>

# Runtime View

<div class="formalpara-title">

## Runtime Scenario: Image Editing

 <div style="text-align: center;"> 

![image](https://github.com/Primestyler/image-sharing/assets/127980400/5dc2908c-219a-41db-9ba6-b5ee2537c0d7)

</div>

1. The process starts with the user uploading an image to our server so that they  can start editing it.
2. the server then requests information of the user regarding their clearance level to enable certain tools for the user.
3. With that information the editing tools are retrieved.
4. Depending on the access the user has they then get certain features which enable them to edit their image.
5. These tools are then returned to the user.

## Runtime Scenario: Image Sharing

 <div style="text-align: center;"> 

![Runtime View](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/Runtime_View2.png?raw=true)

</div>

1. The process begins with the users' intention to share an image.
2. The Server/Editor provides the user a list of possible social media platforms to share the image.
3. The user selects one of these platforms. Then the Server/Editor asks the Social Media Api if the user is currently logged in into the specific platform.
4. If the user is not logged in then a loop is startded, where the user inputs his login credentials to the Server. This specific data is then sent to the Social Media API, which returns the validation. The loop is only stopped if the user is logged in.
5. After the login process, the user requests the image from the database and the image format from the Image Converter.
6. Subsequently, the Server transmits the image to the Social Media API, where the successful sharing is acknowledged.
7. Finally, the server notificies the user about the successful share.

<div style="page-break-after: always;"></div>

# Deployment View

<div class="formalpara-title">


</div>



## Infrastructure Level 1

 <div style="text-align: center;"> 

![Deployment Diagram](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/deployment_diagram.png?raw=true)
</div>



The deployment of the image-sharing app involves multiple components distributed across various locations and environments, each contributing to the system's quality and performance features.

### Components and Connections

1. **Mobile Device and Website:**
   - Represents the user interface accessible through mobile devices and web browsers.
   - Connected to a Load Balancer for distributing incoming traffic.

2. **Load Balancer (AWS Elastic Load Balancing):**
   - Manages and distributes incoming requests to the Server Nodes.
   - Ensures high availability and scalability.
   

3. **Server Nodes:**
   - Handle the core functionality of the image-sharing app.
   - Connected to external services and databases for enhanced features.

4. **Pixlr:**
   - Third-party integration providing advanced image editing tools.
   - Enhances the app's editing capabilities.

5. **Caching Layer (Redis):**
   - Improves performance by caching frequently accessed data.
   - Reduces the load on the server nodes.

6. **Monitoring Tools (Nagios):**
   - Monitors the health and performance of the entire system.
   - Alerts administrators to any issues for proactive management.

7. **Multiple AWS Cloud Databases:**
   - Used for horizontal scaling to handle growing data demands.
   - Ensures data availability and reliability.

### Key Features and Motivations

- **Scalability:** The deployment structure allows horizontal scaling of the database layer in the AWS Cloud, ensuring efficient handling of increasing data volumes. This contributes to high availability and optimal performance.

- **Performance Optimization:** The inclusion of a Caching Layer enhances overall system performance by reducing the load on server nodes and minimizing response times. Monitoring Tools (Nagios) ensure proactive management and prompt issue resolution.



## Infrastructure Level 2

## Internal Structure of Server Nodes
 <div style="text-align: center;"> 

![Server Nodes Diagram](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/server_nodes.png?raw=true)
</div>


### 1. Image Processing Module

The Image Processing Module is a critical component within the Server Nodes responsible for handling image processing tasks. This module executes various operations on the uploaded images, such as resizing, cropping, or applying filters.

### 2. Database Interaction Module

The Database Interaction Module is responsible for the communication between the Server Nodes and the database. It is responsible for storing and retrieving data related to user accounts, uploaded images, and other relevant information. This module ensures seamless data transactions between the server and the persistent storage.

#### Connections:

- **Image Processing Module to Database Interaction Module:** Communication occurs to store or retrieve possibly processed images. For example, processed images may need to be stored for future reference or retrieved for further editing.

### 3. Pixlr Integration Module

The Pixlr Integration Module is an external component called by the Server Nodes. It enables the integration of Pixlr, a third-party editing tool. This module acts as a bridge between the Server Nodes and Pixlr, allowing users to access advanced editing tools for their images.

### 4. Caching Management Module 

The Caching Management Module is responsible for optimizing data access by managing a cache. It stores frequently accessed data locally, reducing the need to fetch the same data repeatedly from the database. This module enhances performance by minimizing latency in data retrieval.

#### Connections:

- **Caching Management Module to Database Interaction Module:** The cache is updated or retrieved based on data changes in the underlying database.

### 5. Monitoring Integration Module

The Monitoring Integration Module plays a crucial role in maintaining the health and performance of the internal modules within the Server Nodes. It integrates with monitoring tools, such as Nagios, to track various metrics, detect anomalies, and generate alerts if issues arise.

## Internal Structure of AWS databases

 <div style="text-align: center;"> 

![Database Diagram](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/aws_databases.png?raw=true)

</div>

1. **Data Storage Module:**
   - Responsible for storing and retrieving data.
   - Connected to the Query Optimization Module to enhance data retrieval efficiency.

2. **Query Optimization Module:**
   - Enhances the efficiency of database queries.
   - Receives input from the Data Storage, Backup and Recovery, and Security and Access Control Modules.

3. **Backup and Recovery Module:**
   - Manages backup and recovery processes for data resilience.
   - Collaborates with the Query Optimization Module to ensure optimal recovery strategies.

4. **Security and Access Control Module:**
   - Implements security measures and access control for database protection.
   - Integrates with the Query Optimization Module to enhance secure data access.
     
## Internal Structure of Load Balancer

 <div style="text-align: center;"> 

![Database Diagram](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/load_balancer.png?raw=true)

</div>


1. **Load Balancing Algorithm:**
   - Utilizes the Round Robin algorithm to distribute incoming requests.
   - Influences the Request Distribution Module's decision-making.

2. **Request Distribution Module:**
   - Executes the load balancing algorithm.
   - Distributes requests to the appropriate Server Nodes based on algorithmic decisions.


<div style="page-break-after: always;"></div>


# Cross-cutting Concepts
 <div style="text-align: center;"> 

![Topics for crosscutting
concepts](images/Crosscutting.png)
</div>

## Security and Safety

We decided that Fancygram should follow the EU GDPR to ensure that user can put trust in our application. The data saved should always be retrievable and transparent. As for threat modelling, each design idea is being looked at to try to find weaknesses that may impact our system. Everything should be designed to anticipate threats and prevent security risks.

At last, the access control for users should be kept at the bare minimum. Each user should only get minimum access to perform the task needed. This is to prevent data breaches and improve data security.

## Architecture

For architecture, it has been decided to use microservices for improved resilience and scalability. The microservices communicate with each other with MQTT API for real-time data exchange and lightweight protocol.

To prevent system overloading, it has been decided to use AWS Elastic Load Balancing tool. It will not only improve event distribution but also prevent bottlenecks and system unresponsiveness.

## Operation Concepts

To keep the downtime as low as possible, everything should be monitored. The decision has fallen on the Nagios Monitoring system to monitor system health. It will be able to detect system failure, overload, or unresponsiveness. Furthermore, auto-scaling policies will be defined, so that each system does not need any manual work to scale if necessary.

For minimal downtime, Continuous Integration and Deployment will be used so that code changes are built and tested automatically.


<div style="page-break-after: always;"></div>

# Architecture Decisions

<div class="formalpara-title">

### Architecture Decision Table

| Problem                    | Considered Alternatives                                         | Decision                                  |
|----------------------------|----------------------------------------------------------------|-------------------------------------------|
| Database Size Unknown      | • In-House Database<br> • Online NoSQL Database                | Online NoSQL Database on AWS              |
| Microservices Cost         | • Monolith<br> • Microservices<br> • SOA                       | Microservices                             |
| Platform Scalability       | • Vertical Scaling<br> • Horizontal Scaling                    | Horizontal Scaling (to accommodate growth)|
| Different Types of Data    | • Forcing Users to Use One Type<br> • Converting Images to a Standard Format | Converting Images to a Standard Format     |
| User Authentication        | • OAuth<br> • JWT Tokens                                       | OAuth (for a secure and user-friendly experience)  |
| Database Hosting           | • AWS<br> • Azure<br> • Google Cloud                           | AWS                                       |

<div style="page-break-after: always;"></div>


## Quality Tree
 <div style="text-align: center;"> 

![Quality_Tree](images/Quality_Tree.png)
</div>

## Quality Scenarios

| Quality Attribute  | Description |
|--------------------|-------------|
| Intuitive Design   | The design is user-friendly and easy to navigate, reducing the learning curve for new users. |
| Accessibility      | The system is equipped with features to aid users with disabilities, including screen readers, keyboard shortcuts, and colorblind-friendly palettes. |
| Backup Mechanism    | There is a robust backup system in place to ensure users' data is stored securely and can be recovered in case of any failure. |
| Consistent Output   | The system performs reliably, delivering consistent output regardless of varying loads or conditions. |
| Smooth Integration  | The system integrates seamlessly with third-party services, maintaining high performance and compatibility. |
| Cross-Platform      | The system's interface and functionality are consistent across different operating systems, ensuring a uniform user experience. |


<div style="page-break-after: always;"></div>

# Risks and Technical Debts

<div class="formalpara-title">

**Contents**

</div>

| Risk/Technical Debt              | Description | Preventive Measures |
|----------------------------------|-------------|---------------------|
| Inadequate Scalability           | Systems could be slow, unresponsive, or crash during high traffic periods. | Utilize microservices architecture to enhance scalability and manage high traffic more efficiently. |
| Documentation Debt               | Due to the fast growth of the system, certain additions might be falsely or not documented at all. | Implement continuous integration practices that include automatic documentation generation and regular reviews to ensure accuracy and completeness. |
| Third-Party Service Dependencies | If a third-party service has problems or difficulties, it can negatively impact our app. | Design the system with fallback options and ensure microservices can operate independently to reduce reliance on any single third-party service. |
| Technical Obsolescence           | The technology stack may become outdated, leading to increased security risks and maintenance challenges. | Regularly review and update the technology stack to current standards and invest in training for the development team on emerging technologies. |


<div style="page-break-after: always;"></div>

# Glossary

| Term                   | Definition                                                                               |
|------------------------|------------------------------------------------------------------------------------------|
| Fancygram              | Social Media Platform for sharing and editing images.                                    |
| Microservices          | Architectural style where an app is built as independent, small services.                |
| AWS                    | Amazon Web Services, a cloud platform providing various services.                        |
| Pixlr                  | Third-party image editing service integrated into Fancygram.                             |
| EU GDPR                | Data protection rules and regulations in the European Union.                             |
| Nagios                 | Monitoring system for overseeing system health and performance.                          |
| Continuous Integration | Development practice automating code building, testing, and integration.                 |
| OAuth                  | Authentication protocol securing user data and permissions.                              |
| JWT Tokens             | Compact, secure tokens for transferring claims between parties.                          |
| Horizontal Scaling     | Increasing capacity by connecting multiple entities to work as a single unit.            |
| Query Optimization     | Improving efficiency and performance of database queries.                                |
| Load Balancer          | Distributes incoming network traffic across multiple servers.                            |
| Caching Layer          | Mechanism storing frequently accessed data, reducing database fetches.                   |
| Monolith               | Single-tiered software application with tightly integrated components.                   |
| SOA                    | Service-Oriented Architecture, where components communicate as services.                 |
| Vertical Scaling       | Increasing capacity by adding resources to a single entity.                              |
| Third-Party Service    | External service or API integrated into Fancygram for added functionality.               |
| Technical Obsolescence | State of being outdated or no longer in use due to technology advancements.              |
| Continuous Deployment  | Extension of continuous integration, automatically deploying code changes to production. |
| Fallback Options       | Alternative strategies or paths used when the primary option encounters.                 |
