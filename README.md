# honeypot-project
Documenting my first hands-on project in detail. 

1. ## Interaction
 
## About Honeypots
- A honeypot is a security mechanism in the form of software, system, or network resource that is intentionally designed to appear vulnerable or valuable, with the purpose of attracting, engaging, and monitoring malicious activity. It monitors hackers behavior, what programs they use and what files are their biggest interested in getting access to. Besides honeypot, there's also honeynet ( multiple honeypots put in a net ), honeyfiles 
( files that resemble importance in order to attract hackers ) and honeytoken ( a bit of tracable data that allows us to monitor what is hacker doing with our files ) 
## Core Objectives
1. Detection ; 2. Deception ; 3. Research & Training

## Types of Honeypots
- Types of honeypots are determined by how much insight they can receive from their system as well as the complexity of making one. There are 3 types of honeypots:
1. Low-Interaction - simulates only specific parts of the system, easier to deploy but gains less insight in hackers activity
2. Medium-Interaction - provides more service than low-interaction honeypot, haves richer insight but still not a complete picture of hackers behavior
3. High-Interaction - deploying real systems and allowing hackers to interact with entire system, allowing us to monitor their usual behavior during data exploitation, high risk but high price.

## Advantages & Disadvantages 
  Advantages : helps security analyst learn about new attack methods, helps keep real systems safe by distracting attackers and drawing them away.
  Disadvantages : limited monitoring ( monitoring only activity inside of a honeypot ), containtment risk.


  2. ## Honeypot Deployement Process

 ## Step 1 - Safety 
- In my project, I'll deploy a Cowrie honeypot that's classified as a high-interaction honeypot. Before that, remaining aware of the risk is important - keeping honeypot in VLAN and making sure it’s isolated from the main network is essential. I should also control its internet access to prevent attackers from using it as a launch point, and always monitor the activity from a safe, separate system. This way, I can collect valuable data without putting the real environment at risk.

## Step 2
