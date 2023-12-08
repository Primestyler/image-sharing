# 

**About arc42**

arc42, the template for documentation of software and system
architecture.

Template Version 8.2 EN. (based upon AsciiDoc version), January 2023

Created, maintained and © by Dr. Peter Hruschka, Dr. Gernot Starke and
contributors. See <https://arc42.org>.

<div class="note">

This version of the template contains some help and explanations. It is
used for familiarization with arc42 and the understanding of the
concepts. For documentation of your own system you use better the
*plain* version.

</div>

<div style="page-break-after: always;"></div>

# Introduction and Goals

Fancygram is a unique social media platform tailored for those who love sharing and discovering exceptional images not commonly found on other platforms. Our main goal is to provide a creative space for users to showcase their editing skills, connect with like-minded individuals, and have fun with challenges and competitions. Fancygram is more than just a platform; it's a commitment to creativity, community, and quality. By meeting the expectations of our diverse stakeholders, Fancygram aims to be a space where visual expression has limitless possibilities.

## Requirements Overview

<div class="formalpara-title">
Fancygram is a specialized platform crafted with the primary goal of empowering users to share and explore visually stunning, high-quality images that are distinctive from what is commonly found on other social media platforms. Its core mission is to facilitate the seamless sharing of such exceptional visuals within a tight-knit community. The app offers a range of essential features, including advanced tools for editing pictures, intuitive mechanisms for sharing and sorting images, seamless connectivity among users, opportunities to share editing tips and techniques, and an avenue for creating and participating in engaging challenges and competitions within the user community.



| Feature                           | Use Case                                                                             |
|---------------------------------------|------------------------------------------------------------------------------------------|
| Photo Editing with Advanced Tools | Users creatively modify images using an array of advanced editing tools.                 |
| Image Sharing and Sorting          | Users upload, organize, and share their images, creating personalized galleries.         |
| User Connections*                  | Users engage in conversations, collaborate on projects, and connect with like-minded individuals. |
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

A table with quality goals and concrete scenarios, ordered by priorities

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
| OB1 | Team        | The team consists of Lin Hao, Hickelsberger and Kalarickal Dominic. |

<div style="page-break-after: always;"></div>

# System Scope and Context

<div class="formalpara-title">
    
### Buisness Context
![image](https://github.com/Primestyler/image-sharing/assets/127980400/12221d3e-08cf-4863-8c23-88d58a6a1659)

| **User/System**  | **Description**                              | **Input**                                    | **Output**                                      |
|------------------|----------------------------------------------|----------------------------------------------|-------------------------------------------------|
| User             | The user interacting with Fancygram          | Uploads images                               | View edited images                              |
| Fancygram        | The image sharing app                        | Receives image uploads                       | Processes and stores images                     |
| AWS              | Cloud storage service                        | Receives images from Fancygram               | Stores and retrieves images in the cloud        |
| Pixlr            | Image editing service providing filters      | Receives images from Fancygram for filtering | Returns edited images with applied filers       |
| Social Media     | User are connected on social media           | Shares edited images from fancygram          | Displays shared images on respective platforms  |
| Filters Database | Database storing custom and pre-made filters | Retrieves filters for image editing          | Stores and updates filters for future use       |

## Technical Context

<div class="formalpara-title">

**Contents**

</div>

Technical interfaces (channels and transmission media) linking your
system to its environment. In addition a mapping of domain specific
input/output to the channels, i.e. an explanation which I/O uses which
channel.

<div class="formalpara-title">

**Motivation**

</div>

Many stakeholders make architectural decision based on the technical
interfaces between the system and its context. Especially infrastructure
or hardware designers decide these technical interfaces.

<div class="formalpara-title">

**Form**

</div>

E.g. UML deployment diagram describing channels to neighboring systems,
together with a mapping table showing the relationships between channels
and input/output.

**\<Diagram or Table>**

**\<optionally: Explanation of technical interfaces>**

**\<Mapping Input/Output to Channels>**

<div style="page-break-after: always;"></div>

# Solution Strategy

### Reliability

To ensure that Fancygram works reliably, we've organized our system using something called microservices. It's like having different teams that can fix specific issues without affecting the whole system. This way, even if there are small problems, Fancygram remains reliable and doesn't crash.

### Scalability

As Fancygram becomes more popular, we want it to handle a lot of users smoothly. So, we've set up the system to grow easily as more people join. This way, Fancygram can handle more users, more pictures, and new features without slowing down. We're planning for Fancygram to grow and adapt as more people use it.

### User Experience

To make Fancygram visually appealing and user-friendly, we've chosen to use Bootstrap. It's a tool that helps us create a website that looks great and is easy for everyone to use. This decision is all about making Fancygram a pleasant and user-friendly platform.

### Technology Choices and Team Collaboration

We've also made important decisions about the technology we use. We chose AWS for our database because it's reliable and can grow with us. Our team collaborates using an agile process, which means we can be flexible and work well together. These choices are like the building blocks for Fancygram, ensuring it's strong, reliable, and set up for success.


<div style="page-break-after: always;"></div>

# Building Block View

<div class="formalpara-title">

**Content**

</div>

The building block view shows the static decomposition of the system
into building blocks (modules, components, subsystems, classes,
interfaces, packages, libraries, frameworks, layers, partitions, tiers,
functions, macros, operations, data structures, …) as well as their
dependencies (relationships, associations, …)

This view is mandatory for every architecture documentation. In analogy
to a house this is the *floor plan*.

<div class="formalpara-title">

**Motivation**

</div>

Maintain an overview of your source code by making its structure
understandable through abstraction.

This allows you to communicate with your stakeholder on an abstract
level without disclosing implementation details.

<div class="formalpara-title">

**Building Block View**



</div>

**Whitebox view**
    
**Level 1**

Our system consists of eight main groupings. The Editor is our main program which is our company developed. The other Block interact with outer systems to provide information to our editing tool. As portrayed in the diagram bellow these consist of an upload to various social media platforms, a cloud storage system , a payment option as well as location services    

![level one Building Block View](images/Builidng_Block_View_levele_1.png)
 
 1 uploads: are responsible for distributing our edited images to outer systems. It can stand alone and be used to upload different files to other platforms if utilized for a different sales point. 

 2 payment: controls the flow of money in our company. Moreover it also regulates which content is permitted to specific users, by passing on order confirmations to the user management. 
 
 3 User management: transfers user data to the editor to permit certain features. Moreover this Block handles the users and allows them to log in and sign up and manage their accounts. This can also be done by system administrators

 4 Location: is used to accurately portray the current location of the users in images (if they want to and allow the function) so that they can share it to their community and show it as a sign of status. Moreover it helps customize certian features and filters for countries as well as language settings. This can however be disabled within the users device.

5 File storage system AWS: is used to store filters, pictures and data.  this cooperates with user management and the editor aswell as the filters supplied and stored by pixlr. 

6 Filters: are responsible for allowing users to saave and expand filters created by the editing tool and linking them to the Filters from Pixlr.
 
7 Editor: This component is the heart of our System. It can be used to modify images and filters aswell as layer these. 

**Level 2** 

 **editor**
 
 The editor consists of 7 blocks of which 3 communicate with outer systems. these allow the editor to accept pictures, export them through uploads as well as customizing filters. 

 <div style="text-align: center;"> 

 ![level two editor Building Block View](images/Builidng_Block_View_level_2_editor.png)

 </div>

1 Picture editing: consists of the user operating the tools inside the app and utilizing them to improve the images.

2 Remodelling tools: provides the necessary tools to customise images as well as filters to improve them to the specific needs of the user

3 Layer management: allows the user to apply more than one filter onto images or even layer filters over each other to create a new one. This can also be restricted due to free and premium user imbalance.

4 Effects and filters: contain the already created filters with certain effects which have already been created. This includes already layered effects.

5 Text tools: consist of all different elements used to output
text onto images and filters. these can also be incorporated with location services to accurately portray locations and situations.

6 Remodelling tools: are used to customize images and filters and complete the image or filter to the specific users liking . Moreover they are combined with  User management to ensure users get the Filters they paid for.

**Picture**

![level two editor Building Block View](images/layer2-picture.png)

1 Virus checker: check if the file is not corupted and all data still works.

2 Format checker: check format to ensure it can be handeld from our system.

3 Image converter: if the format doesnt match the needed format, it gets converted to png so it can be edited on our application.

4 Filter Applicator: filters can be applied to the image when uploaded.

**User Management**

![level two editor Building Block View](images/layer2-user-management.png)

1 Data saver: Controlls the data of the user and the inputs while registering. they then can be processed and stored to a database.

2 Data revison: entered data can be revised and changed. The changed values of course get validated again and then stored in the database

3 account permission: The value if a payment has occured from this account is revieced from the financial division and then the permsissions can be passed on to the editor. Furthermore this also entails the oportunity to advertise and add the posiblity of further payments to this account.

**locations** 

stores locations with timestamps in near realtime and provides access to locations for the last 30 minutes

![level two editor Building Block View](images/layer2-location.png)


1 LocationController: manages the current locations needed for the app to post them on your images.

2 LocationMessaging: this allows users transfer thier real time locations so that the app can present other users who are in their proximity.

3 LocationsListener: Gets the timezones aswell as the current time at the specified location.

4 LocationService: retrieve current coordinates of the user to accurately display them on the app allowing them to interact with users nearby as well as displaying it on their profile.

5 LocationRepository: stores past locations so that we can sell them to whatsapp to make more money.


**Level 3** 

![level three editor Building Block View](images/Builidng_Block_View_level_3_remodelingtools.png)

1 Artistic effects: are different images, emojis, gifs and tools which can be used to style and improve images and filters.

2 Filter effects: are applied to images or layered over other filters to create a new style of an image or a new filter.

3 colour corrections effects: are used to correct or improve contrasts of light or colours to make it more appealing for the user.

<div style="page-break-after: always;"></div>

# Runtime View

<div class="formalpara-title">

**Contents**

</div>

The runtime view describes concrete behavior and interactions of the
system’s building blocks in form of scenarios from the following areas:

-   important use cases or features: how do building blocks execute
    them?

-   interactions at critical external interfaces: how do building blocks
    cooperate with users and neighboring systems?

-   operation and administration: launch, start-up, stop

-   error and exception scenarios

Remark: The main criterion for the choice of possible scenarios
(sequences, workflows) is their **architectural relevance**. It is
**not** important to describe a large number of scenarios. You should
rather document a representative selection.

<div class="formalpara-title">

**Motivation**

</div>

You should understand how (instances of) building blocks of your system
perform their job and communicate at runtime. You will mainly capture
scenarios in your documentation to communicate your architecture to
stakeholders that are less willing or able to read and understand the
static models (building block view, deployment view).

<div class="formalpara-title">

**Form**

</div>

There are many notations for describing scenarios, e.g.

-   numbered list of steps (in natural language)

-   activity diagrams or flow charts

-   sequence diagrams

-   BPMN or EPCs (event process chains)

-   state machines

-   …

See [Runtime View](https://docs.arc42.org/section-6/) in the arc42
documentation.

## Runtime Scenario 1

![image](https://github.com/Primestyler/image-sharing/assets/127980400/5dc2908c-219a-41db-9ba6-b5ee2537c0d7)

### User Image Upload:

- The interaction begins with the User uploading an image to the Server/Editor.
- This represents a straightforward user action, initiating the image editing process.

### Permission Request to User Management:

- After receiving the image, the Server/Editor requests permission from the User Management building block.
- This step ensures that the user has the necessary permissions to access the editing tools.

### Editing Tools Request to Editing Tools Database:

- Upon obtaining permission, the Server/Editor requests the available editing tools from the Editing Tools Database.
- This interaction signifies the dynamic nature of the application, where the available tools may vary based on user permissions.

### Conditional Retrieval of Editing Tools:

- The Editing Tools Database responds differently based on the user's subscription status.
  - If the user has a paid version, all available editing tools are returned.
  - If the user has a free version, a limited set of editing tools is returned.

### Editing Tools Confirmation to User:

- The Server/Editor sends a confirmation message to the User, informing them about the editing tools they have access to.
- This confirmation is a crucial aspect of user communication, providing clarity on available features.



## Runtime Scenario: Image Sharing

![Runtime View](https://github.com/Primestyler/image-sharing/blob/main/arc42/images/Runtime_View2.png?raw=true)


### User Initiates Image Share:

- The interaction begins with the User selecting the "Share" option in the app.
- This represents a user action, indicating the intent to share an image.

### Server/Editor Provides Social Media Options:

- The Server/Editor responds by providing a list of social media platforms available for image sharing.

### User Selects Social Media Platform:

- The User selects a specific social media platform from the provided options.
- This choice determines where the image will be shared.

### Server Checks User's Login Status:

- The Server/Editor checks if the User is currently logged in to the selected social media platform.
- This verification is crucial for seamless integration with the chosen platform.

### Social Media API Validates Login Status:

- The Server/Editor sends a request to the Social Media API to validate the User's login status.
- The Social Media API responds with the confirmation of the User's login status.

### User Login Loop:

- If the User is not logged in, a loop is initiated to handle the login process.
  - The Server/Editor sends login information to the User.
  - The User provides login credentials.
  - The User's login data is sent to the Social Media API for validation.
  - The validation result is relayed back to the Server/Editor.
  - The loop continues until the User is successfully logged in.

### User Requests Image Share:

- After the login process, the User informs the Server/Editor about the intent to share an image.
- This triggers a request from the Server/Editor to the Image Storage/AWS for the selected image.

### Image Retrieval from Image Storage/AWS:

- The Image Storage/AWS responds by providing the requested image to the Server/Editor.
- This ensures that the Server/Editor has access to the image for further processing.

### Image Format Conversion:

- The Server/Editor sends the image to the Image Converter for format conversion.
- The Image Converter processes the image and returns the formatted version to the Server/Editor.

### Image Share to Social Media:

- The Server/Editor sends the formatted image to the Social Media API for sharing on the selected platform.
- The Social Media API acknowledges the successful image share.

### Confirmation to User:

- The Server/Editor sends a confirmation message to the User, indicating that the image has been successfully shared.




## \<Runtime Scenario n>

<div style="page-break-after: always;"></div>

# Deployment View

<div class="formalpara-title">

**Content**

</div>

The deployment view describes:

1.  technical infrastructure used to execute your system, with
    infrastructure elements like geographical locations, environments,
    computers, processors, channels and net topologies as well as other
    infrastructure elements and

2.  mapping of (software) building blocks to that infrastructure
    elements.

Often systems are executed in different environments, e.g. development
environment, test environment, production environment. In such cases you
should document all relevant environments.

Especially document a deployment view if your software is executed as
distributed system with more than one computer, processor, server or
container or when you design and construct your own hardware processors
and chips.

From a software perspective it is sufficient to capture only those
elements of an infrastructure that are needed to show a deployment of
your building blocks. Hardware architects can go beyond that and
describe an infrastructure to any level of detail they need to capture.

<div class="formalpara-title">

**Motivation**

</div>

Software does not run without hardware. This underlying infrastructure
can and will influence a system and/or some cross-cutting concepts.
Therefore, there is a need to know the infrastructure.

Maybe a highest level deployment diagram is already contained in section
3.2. as technical context with your own infrastructure as ONE black box.
In this section one can zoom into this black box using additional
deployment diagrams:

-   UML offers deployment diagrams to express that view. Use it,
    probably with nested diagrams, when your infrastructure is more
    complex.

-   When your (hardware) stakeholders prefer other kinds of diagrams
    rather than a deployment diagram, let them use any kind that is able
    to show nodes and channels of the infrastructure.

See [Deployment View](https://docs.arc42.org/section-7/) in the arc42
documentation.

## Infrastructure Level 1

Describe (usually in a combination of diagrams, tables, and text):

-   distribution of a system to multiple locations, environments,
    computers, processors, .., as well as physical connections between
    them

-   important justifications or motivations for this deployment
    structure

-   quality and/or performance features of this infrastructure

-   mapping of software artifacts to elements of this infrastructure

For multiple environments or alternative deployments please copy and
adapt this section of arc42 for all relevant environments.

***\<Overview Diagram>***

Motivation  
*\<explanation in text form>*

Quality and/or Performance Features  
*\<explanation in text form>*

Mapping of Building Blocks to Infrastructure  
*\<description of the mapping>*

## Infrastructure Level 2

Here you can include the internal structure of (some) infrastructure
elements from level 1.

Please copy the structure from level 1 for each selected element.

### *\<Infrastructure Element 1>*

*\<diagram + explanation>*

### *\<Infrastructure Element 2>*

*\<diagram + explanation>*

…

### *\<Infrastructure Element n>*

*\<diagram + explanation>*

<div style="page-break-after: always;"></div>

# Cross-cutting Concepts

<div class="formalpara-title">

**Content**

</div>

This section describes overall, principal regulations and solution ideas
that are relevant in multiple parts (= cross-cutting) of your system.
Such concepts are often related to multiple building blocks. They can
include many different topics, such as

-   models, especially domain models

-   architecture or design patterns

-   rules for using specific technology

-   principal, often technical decisions of an overarching (=
    cross-cutting) nature

-   implementation rules

<div class="formalpara-title">

**Motivation**

</div>

Concepts form the basis for *conceptual integrity* (consistency,
homogeneity) of the architecture. Thus, they are an important
contribution to achieve inner qualities of your system.

Some of these concepts cannot be assigned to individual building blocks,
e.g. security or safety.

<div class="formalpara-title">

**Form**

</div>

The form can be varied:

-   concept papers with any kind of structure

-   cross-cutting model excerpts or scenarios using notations of the
    architecture views

-   sample implementations, especially for technical concepts

-   reference to typical usage of standard frameworks (e.g. using
    Hibernate for object/relational mapping)

<div class="formalpara-title">

**Structure**

</div>

A potential (but not mandatory) structure for this section could be:

-   Domain concepts

-   User Experience concepts (UX)

-   Safety and security concepts

-   Architecture and design patterns

-   "Under-the-hood"

-   development concepts

-   operational concepts

Note: it might be difficult to assign individual concepts to one
specific topic on this list.

![Topics for crosscutting
concepts](images/Crosscutting.png)

## *\<Concept 1>*

*\<explanation>*

## *\<Concept 2>*

*\<explanation>*

…

## *\<Concept n>*

*\<explanation>*

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

# Quality Requirements

<div class="formalpara-title">

**Content**

</div>

This section contains all quality requirements as quality tree with
scenarios. The most important ones have already been described in
section 1.2. (quality goals)

Here you can also capture quality requirements with lesser priority,
which will not create high risks when they are not fully achieved.

<div class="formalpara-title">

**Motivation**

</div>

Since quality requirements will have a lot of influence on architectural
decisions you should know for every stakeholder what is really important
to them, concrete and measurable.

See [Quality Requirements](https://docs.arc42.org/section-10/) in the
arc42 documentation.

## Quality Tree

![Quality_Tree](images/Quality_Tree.png)

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

<div class="formalpara-title">

**Contents**

</div>

The most important domain and technical terms that your stakeholders use
when discussing the system.

You can also see the glossary as source for translations if you work in
multi-language teams.

<div class="formalpara-title">

**Motivation**

</div>

You should clearly define your terms, so that all stakeholders

-   have an identical understanding of these terms

-   do not use synonyms and homonyms

A table with columns \<Term> and \<Definition>.

Potentially more columns in case you need translations.

See [Glossary](https://docs.arc42.org/section-12/) in the arc42
documentation.

| Term        | Definition        |
|-------------|-------------------|
| *\<Term-1>* | *\<definition-1>* |
| *\<Term-2>* | *\<definition-2>* |
