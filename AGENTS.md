
Dhambaal P2P: A Peer-to-Peer Encrypted Chat Web Application for Somalia
___________________________________________________________________

Candidates
Mubaarak Abdikadir Jamac
Safiyo Maxamed Maxamuud
Zamzam Shucayb Maxamed
Ismail Yusuf Ibrahin
__________________________________________________
THIS PROPOSAL IS SUBMITTED IN PARTIAL FULFILLMENT OF THE
REQUIREMENTS FOR THE AWARD OF THE BACHELOR’S DEGREE IN
COMPUTER SCIENCE & INFORMATION TECHNOLOGY, FACULTY OF
COMPUTER SCIENCE & INFORMATION TECHNOLOGY,
DEPARTMENT OF INFORMATION TECHNOLOGY
__________________________________________
HORMUUD UNIVERSITY
MOGADISHU-SOMALIA
________________________________
SUBMITTED ON FEBRUARY, 2026




DECLARATION
We, the undersigned hereby declare that this thesis entitled Dhambaal P2P: A Peer-to-Peer Encrypted Chat Web Application for Somalia; Design and Implementation of a Peer-to-Peer Offline-First Messaging System for Data Sovereignty; is our original work and has been submitted to Hormuud University in partial fulfillment of our Bachelor's degree. All sources of information used in this study have been properly acknowledged through references. Any assistance received during the preparation of this research has been duly recognized. The work presented in this thesis was carried out under the supervision of the assigned instructor and in accordance with the academic regulations of Hormuud University.

We take full responsibility for any errors or omissions contained in this work.

Signed by : 
Supervisor:
Dr. Bashir Sheikh
Signature _____________________                       Date: ______/______/2026

Candidates:

Mubaarak Abdikadir Jamac
Signature _____________________                       Date: ______/______/2026

Safiyo Maxamed Maxamuud
Signature _____________________                       Date: ______/______/2026

Zamzam Shucayb Maxamed
Signature _____________________                       Date: ______/______/2026

Ismail Yusuf Ibrahin
Signature _____________________                       Date: ______/______/2026



ACKNOWLEDGEMENT
First and foremost, we express our deepest gratitude to Allah for granting us the strength, patience, and knowledge to complete this thesis. We would also like to extend our heartfelt thanks to our supervisor, Dr. Bashir Sheikh for his invaluable guidance, support, and encouragement throughout this project. His expertise and insights have been instrumental in shaping the direction and quality of our work. Special thanks go to the leader of our group, Mubaarak Abdikadir Jamac, whose dedication and leadership have been crucial in coordinating our efforts and ensuring the successful completion of this thesis. Your commitment to the project has been a source of inspiration and motivation for all of us. We also wish to acknowledge the contribution of all our team members: Safiyo Maxamed Maxamuud, Zamzam Shucayb Maxamed and Ismail Yusuf Ibrahim. Your hard work, collaborative spirit, and unwavering commitment have made this journey enjoyable and fruitful. Each one of you has brought unique strengths and perspectives that have enriched our project. Additionally, we would like to extend our thanks to the authority of HORMUUD UNIVERSITY for their continuous support and encouragement throughout this project. The university’s commitment to academic excellence has been a cornerstone of our educational journey, and we are proud to be a part of this esteemed institution. 

Finally, we acknowledge all those who have directly or indirectly supported us in this. Your contributions, no matter how small, have played a significant role in the successful completion of this thesis. Thank you all for your unwavering support and encouragement.


ABSTRACT
The rapid growth of online communication has led to widespread dependence on centralized messaging platforms such as WhatsApp and Telegram. While these systems provide convenience, they introduce serious challenges related to data sovereignty, privacy, latency, and system availability, particularly for developing countries like Somalia. Most centralized communication platforms route local messages through foreign servers, exposing user data to external control and creating a single point of failure.
This study presents the design and implementation of Dhambaal P2P, a secure, offline-first, peer-to-peer messaging system tailored specifically for the Somali context. The proposed system eliminates reliance on centralized server data storage by enabling direct browser-to-browser communication using WebRTC DataChannels, while Gun.js is utilized for decentralized identity management and encrypted local storage. All user data remains encrypted and stored locally on user devices, ensuring full data sovereignty and privacy.
The system adopts a Dual-Layer Hybrid Architecture, where lightweight MQTT brokers are used strictly as blind signaling channels for peer discovery, while actual message transmission occurs directly between peers through WebRTC DataChannels. The application is implemented as a cross-platform mobile and web application using React Native and Expo (with Expo Router), allowing it to function natively on Android/iOS and web browsers, maintaining communication continuity during outages through offline-first local synchronization.
Experimental evaluation demonstrates that the proposed P2P architecture significantly reduces message latency for local users and maintains communication continuity during network disruptions. Furthermore, the system features a fully localized Somali-language user interface to enhance usability and adoption among non-technical users.
The findings of this study confirm that decentralized, local-first communication systems are technically feasible, cost-effective, and highly suitable for improving digital sovereignty and communication resilience in Somalia.



CONTENT PAGE


Dhambaal P2P: A Peer-to-Peer Encrypted Chat Web Application for Somalia
DECLARATION
ACKNOWLEDGEMENT
ABSTRACT
CONTENT PAGE
CHAPTER ONE
INTRODUCTION
1.0 Introduction
1.0.1 Data Sovereignty
1.0.2 Single Point of Failure (Availability Risks)
1.1 Background Study
1.1.1 Problem Overview
1.2 Statement of the Problem
1.2.1 Violation of Data Sovereignty
1.2.2 The Risk of a "Single Point of Failure."
1.2.3 Lack of Localized Solutions
1.3 Research Questions
1.4 Purpose of the project
1.5 Objective
1.5.1 General Objective
1.5.2 Specific Objectives
1.6 Scope
1.6.1 Content Scope
1.6.2 Geographical Scope:
1.6.3 Period:
1.7 Significance of this study
1.7.1 To Future Researchers and Academicians
1.7.2 To National Data Security (Data Sovereignty):
1.7.3 To The General Public and Non-Technical Users:
1.8 Chapter Organization:
Chapter One: Introduction
Chapter Two: Literature Review
Chapter Three: Methodology
CHAPTER TWO
LITERATURE REVIEW
2.1 Introduction
2.2 Theoretical Framework
2.2.1 Application of TAM Constructs to "Dhambaal P2P."
2.2.1.1 External Variables-System Characteristics:
2.2.1.2 Analysis of Perceived Usefulness - PU
2.2.1.3 Analysis of Perceived Ease of Use - PEOU
2.2.2 Comparative Analysis
2.2.3 Theoretical Diagram
2.2.3.1 Signaling Path
2.2.3.1 Data Path
2.3 Review Of Related Literature
2.3.1 P2P Architecture and WebRTC Technology
2.3.2 Digital Colonialism and Data Sovereignty
2.3.3 "Local-First" Framework and the Power of the Internet
2.4 SUMMARY OF KEY STUDIES
2.5 Identified System Gaps
CHAPTER THREE
METHODOLOGY
3.1 Introduction
3.2 Research Design
3.2.1 Software Development Methodology
3.2.2 Research Approach
3.3 Tools Used
3.3.1 Front-end Technologies
3.3.2 Core P2P Stack
3.3.3 Design & Environment
3.4 Feasibility Analysis
3.4.1 Technical Feasibility
3.4.2 Economic Feasibility:
3.5 Data Collection
3.6 Summary
Reference




List of Figures
Figure 1.1 Centralized communication work flow
Figure 1.2 P2P communication work flow
Figure 2.1 Dhambaal system workflow


List of tables
Table 2.1: Comparison between Centralized Systems and P2P
Table 2.2: Comparison of Related Messaging Applications
Table 3.1 Description of Economic Comparison




CHAPTER ONE
INTRODUCTION
1.0 Introduction
The whole world is moving on the use of these modern online communication applications; these applications have made it easier for people to share information very quickly and communicate with each other. The journey of online communities reflects humanity’s desire to connect and share. From the beginnings of Internet Communication, humans have witnessed the evolution of online communication and the interconnected platforms of today. Each evolution has shaped how people interact and build relationships online.In the digital age, online communication has become an essential part of human daily lives, businesses, and social services.However, most of these online communication tools, such as WhatsApp, Telegram, and Facebook Messenger, are built on a system design known as “Centralized Architecture”; this centralized architecture system relies on a central server.Tanenbaum and van Steen (2017) explain in their book that centralized systems have a Single Point of Failure, which means that if the server crashes, the entire system may go down [1].This system, although widespread, is an architecture that raises privacy concerns, as a third party stands between the sender and receiver to capture and store metadata.

Figure 1.1 Centralized communication work flow

Therefore, this research focuses on the design and implementation of a “Peer-to-Peer”  Architecture for online communication.
This P2P system eliminates the need for a central server to manage data and store metadata; instead, it enables users to connect directly and pass information to each other.P2P Messaging means peer-to-peer or person-to-person communication, and it involves the direct exchange of data or messages between two individuals without the involvement of any third-party entity.


Figure 1.2 P2P communication work flow
This project introduces a solution we call "Dhambaal P2P," which is a secure chat network specifically designed to operate in Somalia.Therefore, this system leverages the robust architecture of Peer-to-Peer networks, the strong cryptography of End-to-End Encryption (E2EE), and the enhanced usability of the Progressive Web Application (PWA) is what we aim to implement where all data of anyone own belongs to them, and anyone have the right to it, and will not leave the user and will be stored on user device, whether it is a phone or a computer, and will never go to the server. The purpose of this is that in Somalia, the use of the internet and smartphones is rising day by day. Local telecommunications companies have made efforts to provide internet services that reach both rural and urban areas.However, the major problem facing Somali users is that conversations on online communication applications are routed through servers that are located in Europe and America. And these two major problems  : 
1.0.1 Data Sovereignty
This raises strong concerns related to the "Data Sovereignty" of individuals and nations.As noted in a study titled ‘Digital Colonialism’ by Kwet (2019), there is a phenomenon called digital imperialism, when looking at the global use of cloud services coming from the Global North, it indicates the control and ownership of digital infrastructure by companies in the Global North, and Kwet believes that this creates absolute powerlessness in developing countries, making them highly vulnerable to massive data spying. In Somalia, local data is exposed to foreign interference because private communication in the country is largely dependent on these cloud services. Therefore, a new technical solution is needed to place Somali data on the right side of the equation [2].
1.0.2 Single Point of Failure (Availability Risks)
Centralized communication has vulnerabilities where the entire network's operation depends on a small number of core servers. A notable example of this systemic fragility occurred during the 2021 Meta outage, where a single configuration error at a central point took down WhatsApp, Facebook, and Instagram globally for several hours.This event shows us how a centralized “Single Point of Failure” can suddenly become unavailable and become a useless tool for the billions of people, highlighting the critical need for decentralized P2P architectures that remain operational even if a central hub fails [3]. Finally, reliance on centralized digital infrastructures creates a dual crisis for developing countries.
1.1 Background Study
Humans have always been on the hunt for faster ways to get a message across. It’s been a long journey, starting with something as simple as smoke signals and leading all the way to the instant texting we take for granted today. Honestly, the internet has completely reshaped how the world handles everything from politics to business. But if we want to understand why the Dhambaal P2P project is such a big deal, we have to look at how communication has evolved on three specific levels: globally, throughout Africa, and especially within Somalia.

Globally, the world today has completely shifted to the use of Instant Messaging Applications. These tools have become the backbone of modern social and business communication.
However, recent research shows great concern about the structure of popular apps such as WhatsApp, Telegram, and Facebook Messenger. These tools are based on a system called Centralized Architecture. This system means that all messages, images, and audio messages sent must go through the Central Server before they reach the person who receives them.As noted in a recent study published in Bilad Alrafidain Journal for Engineering Science and Technology, these central servers create a major risk known as a "Single Point of Failure." This means that if the central server fails or is attacked, the entire communication service will stop for millions of people [4]. 
For example, if Meta's server in California experiences a failure, the online communication in Mogadishu will be shut down, showing the vulnerability of the central system.The second global problem is the issue of Data Ownership and Accessibility. In centralized applications, the service provider controls the information, not the user. However, a study published in TechRxiv highlights the benefits of shifting to distributed architectures. The study argues that in these systems, 'data access is quicker, and users have local control over their data' [5]. This shift is essential for ensuring that users—not corporations—retain autonomy over their personal 
Continentially, when we get down to the African continent, the situation is even more complicated. Africa is undergoing a digital transformation. According to the African Union’s Second Ten-Year Implementation Plan of Agenda 2063 (2024), African nations are prioritizing the 'Digital Transformation Strategy' to build a secure Digital Single Market and invest in infrastructure to keep pace with the global economy [6].However, the biggest challenge facing the continent is not the lack of internet, but rather Digital Sovereignty. Africa has become a major market for competing technology companies from the West.Legal analysis in the International Cybersecurity Law Review (2025) highlights a critical challenge to Africa's digital sovereignty. According to Bu [7], the continent’s digital transformation is currently hindered by 'digital colonialism,' where African data is increasingly controlled by foreign tech giants from China and the West. This dependency exists because Africa lacks sufficient local cloud infrastructure, forcing much of the continent's data to be processed and stored in foreign-controlled jurisdictions [7].This causes a technical problem called "Hairpinning". When two people in Africa send each other a message, the data travels to another continent (Europe/USA) to return to Africa. This long journey causes:
Latency: Slow internet due to the remote server.
Security Threat: The data of African citizens is being handed over to unaccountable foreign companies.This study underscores that the only solution for Africa to protect its data is to build local systems that do not export data.
Locally, finally, when we look at Somalia, the telecommunications sector is one of the most dynamic in East Africa. After the collapse of the central government in 1991, private companies filled the void, building modern telecommunications networks (GSM/4G).As noted in the International Journal of Economics, Commerce and Management, local companies in Somalia have succeeded in bringing high-speed internet to major cities and even remote regions. The rollout of fiber optic cables in 2013 was a major step forward in the country’s technological advancement [8]. Similarly, another study published in an SSRN paper showed that internet usage in Somalia is expanding rapidly, with 1.95 million users by January 2021, representing 12.1% of the population, indicating that the society is ready for modern digital solutions [9].
1.1.1 Problem Overview
Even though the local internet infrastructure is getting a lot better, we noticed a pretty big problem during our study. It turns out that everyone—from students to business people—is still relying way too much on foreign apps like WhatsApp. Here’s the weird part: even when the local internet is working fine, if two people in Mogadishu want to chat, their message has to travel all the way to a server in the US or Europe and then back again. It’s a massive detour for a conversation happening just a few blocks away.This system causes two major problems that affect Somali users.
Latency, because the data has to travel such a long way, it's not a direct connection and really depends on how fast that foreign server is running. Here's the catch: if the international connection drops, your local service is going to stop, even if your own local network is working just fine.Data Sovereignty, right now, personal data for Somali citizens is all being stored outside the country. That really goes against the whole idea of national data sovereignty. It basically leaves us dependent on foreign companies that don't even have a reason to care about protecting our data.Therefore, there is an urgent need for a Peer-to-Peer (P2P) system. This system allows Somalis to communicate directly without the need for a middleman. This project takes advantage of the country's existing internet infrastructure (Fiber Optic & 4G), but eliminates the dependence on foreign data storage servers, keeping the data within the country.
1.2 Statement of the Problem
Despite significant global advancements in communication technology, Somali society continues to rely on communication systems that are designed, hosted, and controlled in foreign jurisdictions. During our research and review of current systems, we identified the following critical problems that require immediate resolution.
1.2.1 Violation of Data Sovereignty
The primary issue is that the international online communication applications currently in use route and store all Somali citizens' data—including messages, photos, and voice notes—on foreign servers located in the United States and Europe. This creates a paradox where, although Somalia possesses robust, high-quality internet infrastructure, the country's "Digital Assets" remain under the control of foreign corporations. This external dependency poses a significant threat to national security and personal privacy.
1.2.2 The Risk of a "Single Point of Failure."
Centralized architectures inherently contain a major vulnerability: if the central server experiences a failure or technical outage, the entire service ceases to function. This means that local communication can be disrupted by external failures, rendering the application useless even when the local network is functioning perfectly.
1.2.3 Lack of Localized Solutions
There is a distinct lack of decentralized tools tailored to the local context. Most existing Peer-to-Peer (P2P) programs globally do not support the Somali language and are often too complex for the average person. Currently, there is no modern application adapted to the culture and language of the Somali people that enables non-technical users to adopt a secure, decentralized system easily.
1.3 Research Questions
Based on the problems identified, this study aims to answer the following key questions:
1.How can we eliminate the dependency on central servers?
2.How can we ensure that Somali users' data remains on their devices to protect data sovereignty?
3.How can we develop a user-friendly interface that supports the Somali language for local users?
4.How can the application maintain communication continuity during network interruptions or outages?
5,How can Peer-to-Peer architecture reduce message latency (delay) for local users in Somalia?
1.4 Purpose of the project 
The primary purpose of this study is to design and implement a secure Peer-to-Peer encrypted chat application tailored specifically for the Somali country. The project seeks to move away from the traditional centralized communication model, where data passes through foreign servers, and instead establish a direct connection between the users. This approach aims to ensure that communication is not only private but also resilient against the systemic failures often associated with centralized servers.Furthermore, this study aims to address the critical challenge of network instability by developing an “Offline-First” communication system.
1.5 Objective
1.5.1 General Objective
The general objective of this study is to design and implement a secure, peer-to-peer, web-based chat application that enables direct communication, is offline-first, and eliminates reliance on centralized foreign data storage servers, thereby enhancing data sovereignty.
1.5.2 Specific Objectives
To achieve the general aim, the study focuses on the following specific objectives:To design a decentralized network architecture that connects users directly to one another, removing the  “Single Point of Failure” associated with central servers.To implement a “Local-First” storage mechanism where all users' data is encrypted and stored physically on the client’s device, ensuring that no private information is exposed to third-party cloud providers.To develop a responsive User Interface (UI) that is fully localized in the Somali language, ensuring the system is accessible and intuitive for non-technical local users.To implement an offline synchronization protocol that allows the application to queue messages during an internet outage and automatically transmit them once connectivity is restored.To evaluate the system’s performance in low-bandwidth environments to demonstrate reduced latency compared to traditional

1.6 Scope
1.6.1 Content Scope
This study is strictly limited to the design and implementation of a text-based and audio Peer-to-Peer (P2P) chat application. The research and development specifically cover the following functional and theoretical areas:


• Real-time Text Messaging and Audio:
Implementation of text and audio communication between peers using WebRTC. This phase of the research explicitly excludes real-time video conferencing features.
• Secure File Sharing:
Enabling users to share documents and images directly between peers without relying on a central server.
• End-to-End Encryption (E2EE):
Application of cryptographic protocols, specifically Gun.js SEA (Security, Encryption, Authorization), to ensure message confidentiality and user privacy.
• Offline Data Persistence (Local-First):
Storing chat history locally on the user’s device to allow access to messages even in the absence of an internet connection.
• System Localization:
Designing a user-friendly interface fully localized in the Somali language to ensure accessibility for non-technical local users.
1.6.2 Geographical Scope:
The geographical scope of this study is focused on Mogadishu, Somalia. This location was selected because, as the capital city, it hosts the largest concentration of internet users, universities, and businesses that rely on digital communication.
1.6.3 Period:
The project will be carried out over a period of six months, starting from December 2025 to May 2026. This duration allows adequate time for all phases of the Software development life cycle (SDLC), including requirements gathering, system design, coding, and testing.

1.7 Significance of this study
The findings and the practical implementation of this study hold significant value for various stakeholders within the Somali community. By introducing a decentralized, offline-first communication model, this project addresses critical gaps in the current technological infrastructure, and the significance of this study is categorized as follows:
1.7.1 To Future Researchers and Academicians
This project will serve as a foundational reference for future students at Hormuud University and other institutions who wish to study Distributed Systems and Graph Databases (Gun.js). It filled a gap in local academic literature regarding Peer-to-Peer networks in the East African context, providing a baseline for further research into decentralized technology.
1.7.2 To National Data Security (Data Sovereignty):
This study contributes to the national interest by introducing a practical framework for Data Sovereignty. By keeping data stored locally on user devices rather than exporting it to a foreign cloud server, the system reduces the risk of massive surveillance and protects the digital assets of Somali citizens. It serves as a proof of concept that Somalis can build a self-reliant digital infrastructure.
1.7.3 To The General Public and Non-Technical Users:
This system offers a secure communication channel for individuals who prioritize privacy, ensuring that their conversations remain confidential through client-side encryption. Furthermore, the application features a fully localized User Interface (UI) in the Somali language. This removes language barriers, allowing non-technical users to easily adopt and use decentralized technology without requiring advanced English proficiency.
1.8 Chapter Organization:
This thesis is organized into five chapters, structured as follows:
Chapter One: Introduction
This chapter provides the foundation overview of the study, and it includes the background of the study, the statement of the problem, research questions, objective, scope, and the significance of the project.
Chapter Two: Literature Review
This chapter reviews existing literature, academic journals, and theoretical frameworks related to Peer-to-Peer architecture, End-to-End Encryption (E2EE), and Data Sovereignty, and it also analyzes the gaps in current centralized systems that this project aims to fill.
Chapter Three: Methodology
This chapter describes the research design and the specific software development methodology used, detailing the tools and technologies employed, such as React Native (Expo) and Gun.js, and explains the procedures for system requirement analysis and data collection.




CHAPTER TWO
LITERATURE REVIEW
2.1 Introduction
The main purpose of this chapter is to conduct a comprehensive review of the literature, theories, and levels of technology that are the foundation of the architecture of decentralized communications. This chapter delivers an in-depth analysis of the major changes in today’s technology. And that is a transition from systems that are based on centralized systems, and moving to systems that are based on P2P (Peer-to-Peer), highlighting the benefits and challenges of both systems(centralized and decentralized), especially in developing countries.Finally, this chapter is designed to cover the following four points:
Theoretical Framework: This section will use a theory known as the Technology Acceptance Model TAM. To get an idea of the impact on users who will use the system to accept this new system.
Review of Related Literature: In this section, we will review previous studies on this topic, such as "Offline-First", End-to-End Encryption, and the issue of Data Sovereignty in Africa.
Summary of key studies: In this section, we will review key points of previous studies. Especially those who have proven the benefits of decentralized systems.
Gaps Identified: Lastly, this chapter highlights gaps that exist in currently used global applications (such as WhatsApp), while proving the need for a local solution like “Dhambaal P2P” that can fill the gap.
The ultimate goal of this review is to build a solid study foundation that supports the technical decisions we made for the construction of this project.
2.2 Theoretical Framework
To evaluate the effectiveness of the design and the possibility that Somali society will accept the “Dhambaal P2P” system. This study applies the theory known as the Technology Acceptance Model (TAM), which was developed by Fred Davis in 1989. It’s the most commonly used framework in “Information Systems” to predict whether people will use new technologies or not.The main point of this theory, the Technology Acceptance Model (TAM), is that user acceptance is not only dependent on the complexity of the code, but rather on the two main psychological factors that determine it:
Perceived Usefulness (PU) : This is defined as “The level that the person believes  that using a particular system will enhance their productivity.” In this study, usefulness is not measured by office productivity, but rather in terms of Communication Resilience. The user considers "P2P Privacy" useful if it allows them to send messages during internet outages, a problem that other apps (such as WhatsApp) cannot solve.
Perceived Ease of Use (PEOU) : Additionally, this is defined as “the degree to which a person believes that using the system does not require spending more time learning how to use,” and this point is particularly important in the situation in Somalia. If a decentralized system requires complex configuration or does not provide support in a local language, the "effort" increases and usage decreases. Therefore, we argue that making the interface available in the Somali language is the biggest key to ease of use.By focusing on Efficiency and Simplicity, TAM allows us to justify the technical decisions we have made in building “Dhambaal P2P”.
2.2.1 Application of TAM Constructs to "Dhambaal P2P."
According to the Technology Acceptance Model (TAM) theory, the acceptance of a new system is influenced by external variables that impact how people view its effectiveness and ease of use. This section deeply analyzes how the unique architecture of “Dhambaal P2P” meets these requirements by breaking it down into three main points:
2.2.1.1 External Variables-System Characteristics:
External variables are specific features within the system that change user behavior. The “Dhambaal P2P” system has two very different technical characteristics:
2.2.1.1.1 Dual-Layer Hybrid Architecture:
Unlike regular P2P applications, this project implements a modern architecture that separates signaling and data transmission. This system will use lightweight MQTT brokers to help users discover each other and negotiate connections (acting as a blind signaling channel), while the actual messages and files are transmitted directly between peers over WebRTC Data Channels. These technical features are more important to the “External Variables” because they guarantee that the signaling broker has never seen or stored any data (acting as a "blind" signaling pipe), which increases user confidence.
2.2.1.1.2 System Localization:
Another important feature is that the entire UI system is built in the Somali Language to avoid language barriers, which can reduce the acceptance, and this characteristic of having the local UI language affects how lay users perceive the system.
2.2.1.2 Analysis of Perceived Usefulness - PU
According to Davis (1989), users will accept a system if they believe that using a system will solve a problem they have. “Dhambaal P2P” increases efficiency while solving two major problems:
2.2.1.2.1 Data Privacy:
In this modern era, Somali users use centralized online communication, and this raises concerns about “Spying” and having their data fall into foreign hands.Since the "Dhambaal P2P" architecture ensures that messages are sent directly between the two users without going through a central server, the user considers this system to be “useful” in terms of security. The signaling brokers act as "blind relays" and cannot read message content (which is encrypted end-to-end and transmitted peer-to-peer), giving the user an advantage that centralized apps like WhatsApp do not have.
2.2.1.2.2 Reduced Latency & Efficiency
The second advantage is speed; a centralized system delivers messages through servers that are located in faraway places that the sender is not even closer to, which causes latency.“Dhambaal P2P” is useful to the local community because it creates a direct path between the two users, and that increases the communication speed, especially when users are on the same internet network, such as the same  ISP.
2.2.1.3 Analysis of Perceived Ease of Use - PEOU
Even if the system is effective, the Technology Acceptance Model (TAM)  indicates that if the system is hard to use, users will reject it. And “Dhambaal P2P” will use a technique known as “Abstraction,” by hiding complexity.
2.2.1.3.1 Abstraction of Cryptography
Normally, P2P systems require the user to manage their keys (private key and public keys). To increase ease of use, “Dhambaa P2Pl” made this method work automatically in the background, so users will only see their username and public key, while the system automatically manages key exchanges and WebRTC connections in the background. And this makes the system easy to use, similar to WhatsApp
2.2.2 Comparative Analysis
It is necessary to compare the current system with the proposed new system. This analysis is based on the difference between centralized and decentralized systems.
As noted, Ahmed and Bashar (2025) in their study about “Security and Privacy in Mobile Instant Messaging Through Decentralized Authentication Techniques”, the centralized system that is used now has major flaws: "the service stops if the central server is attacked or malfunctions," which is called Single Point of Failure [4].
On the other hand, data sovereignty, Kwet (2018) argues that reliance on foreign infrastructure servers means that these companies “own and manage critical infrastructure,” which eliminates the ability of the developing countries to control their own data[2].The “Dhambaal P2P” solves both problems by eliminating the need for a central server.
Table 2.1: Comparison between Centralized Systems and P2P

Feature / Criteria
Centralized Systems (e.g.,WhatsApp,Telegram)
Proposed System (Dhambaal P2P)
System Architecture
Centralized (Client-Server): 
Relies on a single central authority for data processing and routing.
Dual-Layer Hybrid: 
Uses MQTT brokers for signaling only, while messages travel directly via WebRTC DataChannels (Peer-to-Peer).
Data Sovereignty
Foreign Residency: 
User data is stored in cloud servers located in the Global North (USA/Europe).
Local Residency: 
Data remains physically stored on the user's device (Local-First), ensuring full data sovereignty.
Privacy Model
Trust-Based: 
Users must trust the service provider not to access or sell metadata.
Zero-Trust (Blind Server): 
The MQTT signaling brokers are technically incapable of reading message content; no intermediate storage exists.
Point of Failure
Single Point of Failure: 
If the central server experiences downtime, the service stops globally.
Decentralized Resilience: 
No central database holds the messages; if signaling brokers fail, only new user discovery/calling is paused, not local access or existing chats.
User Interface (UI)
Global-Standard: Interfaces are primarily designed for English or Arabic speakers.
Localized: 
Native Somali interface designed specifically to enhance ease of use for local non-technical users.
Latency & Routing
High Latency: 
Local traffic is routed internationally before returning to the recipient.
Low Latency: 
Data travels the shortest path between peers (Browser-to-Browser), utilizing local ISP bandwidth efficiently.

Table 2.2: Comparison of Related Messaging Applications
Application
Architecture
Offline Capability
Somali Language
Data Sovereignty
WhatsApp
Centralized
No
Partial
Low
Signal
Centralized
No
No
Medium
Briar
P2P / Mesh
Yes
No
High
Dhambaal P2P (Proposed)
P2P / Mesh
Yes (Local-First)
Full (Localized)
Maximum


2.2.3 Theoretical Diagram
The diagram (Figure 2.1) visually explains the structure of the “Dual-Layer Hybrid Architecture”  of the “Dhambaal P2P”. The diagram shows the separation between the “Signaling Path” and “Data Path”.
2.2.3.1 Signaling Path
This line connects the peers to the MQTT signaling brokers, and its only function is discovery and WebRTC connection negotiation (ICE candidates, session descriptions, public key exchange). The brokers do not see any chat message or media data.
2.2.3.1 Data Path
This line connects User A and User B directly using WebRTC DataChannels. This is the path through which text messages, voice notes, and shared files are transmitted. Since this line doesn’t go through any central server, it guarantees "Zero-Trust Privacy" and high speed.
This diagram clearly explains how the “Dhambaal P2P” system solves the “Single Point of Failure” problem, because even if the signaling MQTT brokers are disconnected, direct P2P connections that are already established remain fully active.

Figure 2.1 Dhambaal system workflow
 2.3 Review Of Related Literature
This section presents the latest research related to the core technologies of the “Dhambaal P2P” system, specifically WebRTC, Data Independence, and “Local First”.
2.3.1 P2P Architecture and WebRTC Technology
The Web Real-Time Communication (WebRTC) technology has become the gold standard for building a real-time communication system. Normally, a client-server requires a central server to transmit data, which creates a security risk. However, a study published in IEEE (2024) explains that WebRTC is a technology that allows browsers to establish direct communication.The study demonstrated that WebRTC makes easy “direct peer-to-peer audio, video, and data communication between web browsers without needing a central server [10].  The “Dhambaal P2P” system directly implements this theory using RTCDataChannels to transmit text messages, ensuring that data does not stop at a central location. 
2.3.2 Digital Colonialism and Data Sovereignty
The second topic has focused heavily on the threat of Digital Colonialism. In the case of developing countries in Africa, reliance on foreign cloud infrastructure is not just a technical, but it is a political and security issue.A study by Kwet (2018) argues that the current structure of the internet is designed to allow Westerners to control the world’s data. The author argues that “US corporations have colonized the digital ecosystem,” and that means US companies have colonized the digital ecosystem, controlling the flow of data from other countries [2].
This situation creates what is known as “Data Extrusion”, where data of Somali citizens is taken out of the country, and stored on foreign servers that are not controlled by the Somali government. The “Dhambaal P2P” system directly addresses these arguments by implementing “Data Sovereignty”, as the data never leaves the user device.
2.3.3 "Local-First" Framework and the Power of the Internet
The third technology which is the main point of this study is a framework called “Local-First”. Normally, cloud based applications (such as Google Docs or WhatsApp Web) stop working if the main server crashes or fails. A study by Kleppmann et al. (2019) suggested that the best solution is to store data on the user's device first. The authors stated that the main advantage of a system is to be “allow users to read and write data without an internet connection, meaning that the user can save data and search histories without an internet connection[0].
The “Dhambaal P2P” system implements this concept using browser storage. When the internet comes back, the system automatically performs “Synchronization” by sending messages to the other person that the user communicates with.

2.4 SUMMARY OF KEY STUDIES
The literature and research we reviewed in this chapter clearly outline the need for structural change. Combining the studies of Abbas & Nema (2025), Kwet (2019), and Kleppmann et al. (2019), three main findings emerge as the basis for building a “P2P Notification” system:Central System Vulnerability: All studies agree that "Client-Server" systems have a major flaw of "Single Point of Failure". When the central server fails, the community connection is severed.
The Importance of Data Privacy: The fear of "Digital Colonialism" is real. The only solution to protect against espionage and data theft is to keep data on the user's device (Local Device) instead of being deployed to a foreign Cloud.
WebRTC Opportunity: WebRTC technology has provided a golden opportunity that enables the browser itself to become a server, eliminating the need for a middleman.
2.5 Identified System Gaps
Centralize Architecture Limitation: 
Most of the existing messaging systems rely on centralized servers, which creates a single point of failure. If the server is unavailable, communications are disrupted completely. Such architecture also raises dependency on third-party service providers.The leading issues in question are privacy and data control.Current systems store the users' data on external servers managed by the service providers. This increases serious concerns about data privacy, unauthorized access, surveillance, and full user control over personal information. 
Limited Localization and Language Support
Most systems are not very supportive of locally adapted languages or culturally adapted interfaces. This reduces usability and accessibility for users without broad technical knowledge or those who are non-English-speaking.
High Latency and Inefficient Data Routing
Messages often travel through distant servers even when users are geographically close. This increases latency, consumes unnecessary bandwidth, and reduces communication efficiency. Trust-Based Security Models 
However, users must implicitly trust these service providers in protecting their data. Even with encryption, metadata collection and server-side control remain a major concern, because users cannot independently verify data handling practices.
Scalability and Resilience Challenges
Centralized systems face scalability issues during peak usage and are vulnerable to outages, cyberattacks, or censorship, limiting reliability and long-term sustainability.






CHAPTER THREE
METHODOLOGY
3.1 Introduction
This chapter provides a detailed explanation of the methods, techniques, and procedures used to build and implement the “Dhambaal P2P” project. The main purpose of this chapter is to delineate the scientific and systematic methodology employed to address the following scientific and systematic approach. 
This study combines two aspects: the research aspect to understand the community's needs, and the software development aspect to build the technical solution. Therefore, this chapter focuses on the “Applied Research” approach to the development of the “Agile Methodology,” which enables this project to build, test, and refine at various stages.
Finally, this chapter is divided into important parts, which are:
Research Design
Tools Used
 Feasibility Analysis
Data Collection
3.2 Research Design
This study will use an Experimental Design, and this was chosen to analyze the relationship between two variables: System Architecture and Data Privacy Level.
The study conducts a technical experiment by comparing two scenarios: 
Control Group: Existing Central Systems (such as WhatsApp), which store data on a server. 
Experimental Group: New "P2P Message" system, which stores data on the user's device (Local-First). The purpose of the experiment is to prove that the use of the P2P system (Independent Variable) directly increases Data Independence and Communication Speed ​​(Dependent Variables) within Somalia.
3.2.1 Software Development Methodology
To implement the technical system, this study used the Agile Methodology, which involves repeating stages and allows the development to break the project into small, testable parts.The reasons for choosing Agile include:Security: It allowed us to test security levels (Encryption) step by step, to ensure that data could not be intercepted.
Flexibility: It will help us to apply the app’s UI design to suit the Somali language.
3.2.2 Research Approach
This study used a “Mixed Methods” approach, which combines:
Qualitative: Observing how the centralized system is risking the privacy of individuals and how people need a system that does not risk their privacy.
Quantitative: Performance metrics to prove that the P2P system is faster than a centralized system that exports data into places that are not necessary to go.
3.3 Tools Used
To ensure that the “Dhambaal P2P” system is secure, fast, and independent of a central server, the study needs to select modern tools and technologies suitable for building a Distributed System. The tools used were divided into three categories:
Front-end
Core Logic
Design
3.3.1 Front-end Technologies
React Native & Expo
We chose React Native and Expo as our application framework. This allows the application to compile both to high-performance native iOS/Android packages and to a web application using React Native Web. It supports offline-first capabilities, runs as a real native app with access to device resources, and works seamlessly even without internet connectivity.
React Native Stylesheet
To build a responsive design compatible with all screen sizes across mobile and web platforms, we used React Native's StyleSheet styling engine. This enables clean, optimized component styling and a custom Somali user interface tailored for ease of use.
3.3.2 Core P2P Stack
This is the heart of the system, and this is where the power of the "Dual-Layer Architecture" comes from:
Gun.js (Decentralized Graph Database)
Gun.js is used as our offline-first local database and reactive state manager on the client. It handles the SEA (Security, Encryption, Authorization) cryptographic protocols to automatically generate public/private keypairs, encrypt chat data lists, and verify user credentials completely client-side without relying on a central database.
WebRTC (Web Real-Time Communication)
As we mentioned in Chapter 2, WebRTC is used to create “Data Channels”. This pipeline, through which messages pass, connects the two users directly (Peer-to-Peer)
MQTT Multi-Broker Signaling (Blind Relays)
Rather than a single signaling server (which introduces a single point of failure), the signaling layer utilizes multiple public MQTT brokers (e.g., EMQX, HiveMQ) accessed via WebSockets. These brokers serve strictly as blind relays for connection negotiation (ICE candidates, session descriptions, public key exchange) and do not store any message content or metadata.
3.3.3 Design & Environment
Figma:Before the coding, the design (UI/UX) was done in Figma to test the user experience and ensure that the Somali terminology was understandable.
GitHub:For GitHub, we will use it to manage code changes (Version Control) and team collaboration.
3.4 Feasibility Analysis
The study conducted an in-depth analysis to confirm that the “Dhambaal P2P” project is feasible in terms of technical and economic aspects.
3.4.1 Technical Feasibility
The technical evaluation showed that the selected technologies (React Native/Expo and Gun.js) are easy to implement and maintain.
Client-Side Device Power: 
Since the system is based on WebRTC and client-side processing, it doesn’t require a centralized backend server. Heavy computation, including end-to-end encryption (SEA) and local persistence, is handled directly on the user's mobile device or web browser. This local-first processing model makes the system technically feasible and highly performant.
Compatibility: Gun.js integrates natively with the React Native and AsyncStorage layers, facilitating a unified pipeline for cross-platform app state, security, and reactive user interfaces.
3.4.2 Economic Feasibility:
In terms of economics, this project is much less expensive than typical centralized systems.
Storage Coast:
Systems like Supabase or Firebase charge a monthly fee of approximately $25/month or even more when database usage grows. However, “Dhambaal P2P” is $0/month in terms of storage, because the data is stored on the user device and there is no “Central Cloud Bill”. Signaling and Discovery Cost:  By leveraging public, shared MQTT brokers for signaling, the project minimizes recurring infrastructure costs to $0.00. Even if custom dedicated signaling brokers are deployed, their maintenance costs are extremely low (estimated at $5 to $10 per month) due to the zero-storage nature of signaling data. 





Table 3.1 Description of Economic Comparison
Cost Category
Centralized Systems (Firebase/Supabase)
Dhambaal-P2P(Proposed)
Data Storage
Variable: $0.025 - $0.10 per GB/month
Fixed: $0.00
Database Server
Scaling: Increases with CPU/RAM needs as concurrent users grow.
Decentralized: No central DB server required.
Signaling/Relay
Included in premium tier pricing.
Fixed: $5.00 – $10.00 / month
Bandwidth (Egress)
High: Charged for every byte sent from cloud to user.
Low/Zero: Data moves directly between peers.
Total Monthly
High & Unpredictable ($25.00 → $$$)
Low & Predictable ($5.00 – $10.00)



3.5 Data Collection
To confirm the need for the system and its effectiveness, the study collected data from two main primary sources. Observation and Interviews:
Initial data was collected from Hormuud University students and a section of the community living in Kahda District.
Method: We conducted direct observation to understand the problem experienced by existing applications, such as WhatsApp, during periods of slow or interrupted internet connections.
Technical Experimentation
Since the study is experimental, a significant portion of the data was generated from testing the “Dhambaal P2P” system.
Methods: We measured the latency metrics when using WebRTC and when using a regular server. This technical data was collected to prove that the P2P system is faster than a system that exports data to an external server.
3.6 Summary
This chapter provided a comprehensive explanation of the process that involved building the “Dhambaal P2P” project. The study adopted an Experimental Design to test the relationship between P2P systems and data security. The development method chosen was Agile Methodology, which facilitates the development of the project in stages. The tools used include React Native and Expo for the Front-End, Gun.js for the Database, MQTT for signaling, and WebRTC for Real-Time Communication. The feasibility analysis has shown that the project is economically viable and technically feasible.
Finally, this chapter sets the stage for Chapter Four, which will focus on the actual implementation of the code, design, and test results.


 


Reference

[1] A. S. Tanenbaum and M. van Steen, Distributed Systems: Principles and Paradigms, 3rd ed. Upper Saddle River, NJ, USA: Pearson, 2017.
[2] Kwet, M. (2018). Digital Colonialism: US Empire and the New Imperialism in the Global South. SSRN Electronic Journal.
[3] Dominik, Rehse, and Sebastian Valet, “Competition among digital services: Evidence from the 2021 Meta outage,” 2025, Accessed: Dec. 22, 2025. [Online]. Available: https://www.econstor.eu/handle/10419/314420
[4] Ahmed R. AlMhanawi and Bashar M. Nema, “Enhancing Security and Privacy in Mobile Instant Messaging Through Decentralized Authentication Techniques,” Bilad Alrafidain Journal for Engineering Science and Technology, vol. 4, no. 1, pp. 73–84, Mar. 2025, doi: 10.56990/BAJEST/2025.040107.

[5] N. Akhil Chaparala, S. Maddikunta, S. Maneendra Pingili, S. Reddy Kumar Pullamgari, and S. Kumar Reddy Pullamgari, “Distributed Database Usage in Real-Time,” Authorea Preprints, Oct. 2025, doi: 10.36227/TECHRXIV.176184721.11529177/V1.
[6] African Union, “THE DIGITAL TRANSFORMATION STRATEGY FOR AFRICA (2020-2030)”, Accessed: Dec. 24, 2025. [Online]. Available: www.au.int
[7] Q. Bu, “Data sovereignty in Africa: steering digital transformation between China and the West,” International Cybersecurity Law Review 2025, pp. 1–15, Dec. 2025, doi: 10.1365/S43439-025-00165-1.
[8] M. M. Mohamed, N. N. Isak, and D. H. Roble, “International Journal of Economics, Commerce and Management United Kingdom PRIVATE SECTOR DEVELOPMENTS IN SOMALIA: ANALYSIS ON SOME MAJOR SECTORS,” vol. VII, 2019, Accessed: Jan. 06, 2026. [Online]. Available: http://ijecm.co.uk/

[9] A. I. Farah, “Digital Literacy in Somalia: A Pathway to Holistic Education and Sustainable Development,” July 2025, doi: 10.2139/SSRN.5466927.
 
[10]  G. Suciu, S. Stefanescu, C. Beceanu, and M. Ceaparu, “WebRTC role in real-time communication and video conferencing,” GIoTS 2020 - Global Internet of Things Summit, Proceedings, June 2020, doi: 10.1109/GIOTS49054.2020.9119656.
  


