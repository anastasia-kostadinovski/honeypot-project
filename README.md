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
- In my project, I'll deploy a Cowrie honeypot that's classified as a medium-interaction honeypot. Before that, remaining aware of the risk is important - keeping honeypot in VLAN and making sure it’s isolated from the main network is essential. I should also control its internet access to prevent attackers from using it as a launch point, and always monitor the activity from a safe, separate system. This way, I can collect valuable data without putting the real environment at risk. For my project I'll build a honeypot inside WSL Powershell without publicly exploiting it, so all the attacks will be improvised by me for educational purpose. No malicious code will be shared as well as promoted - this project is meant only for security education.

## Step 2 - Update & Upgrade
- Before we begin with Cowrie installation, we need to make sure in our Powershell that all needed updates and upgrades are on our device. Cowrie has Python dependencies ( shown later ), and a system that has up-to-date updates ensures running our necessities smoothly. Besides securing dependency compatibility, this secures higher security and stability for our honeypot. Providing this can be done through coding in Powershell and using Linux commands :
   sudo apt update && sudo apt upgrade - y
( -y is optional and a personal preference, it means automatic yes and allows system to run without manual confirmation).
After installing necessities, we'll be running a code that ensures our system has all Python necessities that our honeypot needs, such as ensuring core functions ( SSH/Telnet ), smooth set up and security. Full code is shown in the link at the bottom of the post.

## Step 3 - Adding Cowrie User
- Providing a new user on our Powershell just for honeypot is essential and non-negotiable. Except keeping things tidy on our device, another user account is a form of security isolation since our core account that interacts with the device is separated and not visible to attackers. By limiting system access and improving our security, we can safely monitor malicious activity on our honeypot. You can choose if you'd like your account to be password secured or not. Since I'll use a password ( link at the bottom of a post ), if your preference would be no password on your separate account, command would be :
  sudo adduser --disabled-password user123 ( or a username of choice ).

## Step 4 - Cowrie Cloning
- This is actually an installation of Cowrie and its code. Since Git doesn't actually download the project but just keeps it's copies, we'll be getting that. For the record, this clone has everything - just a name is tricky. With Cowrie cloning, we'll be getting a fully functional software that haves the latest updates. As you run the command for it's cloning, you'll run a change directory code to switch it to Cowrie, from where your WSL Powershell ( or a virtual machine of choice ) should look like :
  user123@DESKTOP-A123B4:~/cowrie$ ( example )
Congrats, you're inside of a Cowrie directory! Here is where we'll write commands from now on for our honeypot. 

## Step 5 - Python Virtual Environment
- As previously mentioned, Cowrie has Python dependencies that are non-negotiable for its running. Securing a Python VE ensures that other projects on our device won't be disturbed since it'll be separated. After its installation you should have created a Python VE and then activating it so that Cowrie will use it. If this step is skipped, there is a chance for Cowrie disturbing other systems or not doing well. To be sure you're now in a separate environment, your WSL Powershell ( or a virtual machine of choice ) should look like :
  (cowrie-env) user123@DESKTOP-A12B345:~/cowrie$
Now we are in safe environment for starting Cowrie.

## Step 6 - Installing Requirements
- Installing Python VE isn't enough. At Step 2 we installed basic Python dependencies such as cyptography, loggin and network handling, now we are upgrading to make sure that what we will install will run smoothly and efficiently. We will use 2 pip commands - one for installing upgrade and the other for installing requirements. This sequence matters because without any newer update, the tools we'll be installing might not work - so by running :
  pip install --upgrade pip
we are upgrade the pip installer to being up-to-date so that we won't come accross some errors such as ' wheel not supported ' and that we can be able to install needed modern Python packages. This is a general code that by itself provides enough stability for Python, but in case we'd like to be secure that we will bypass potential errors, using a command :
  pip install --upgrade pip setuptools
wouldn't hurt, matter fact it can secure us fully so that our work can go by undisturbed.
When it comes to requirements, further will be explain in the link bellow the post, but they

## Step 7 - Cowrie Configuration
- Just few steps away from officially launching our honeypot! Now we will make sure that our Cowrie gets a few final adjustments before starting it. So far, we've just installed a default configuration file that is like a template for our honeypot. It contains information such as what port it listens to, where it saves logs, basic settings etc. Now what we will do is copy this Cowrie template so that we can our own editable configuration that Cowrie will be working on. This step is important because Cowrie can't work on a sample template, besides that by copying it we are keeping the original safe from being in case an error occurs. Later we will be looking at " listen-endpoints" section ( after entering a command for cowrie configuration, link at the bottom ) that will show us what service Cowrie is simulating for attackers - SSH or Telnet. We can choose to set one or another. This will safely imitate original protocols without any possibility of disturbing their systems. The interface value ( interface=0.0.0.0) means that our honeypot is accessible for any network address as well as accessible for monitoring possible attacks. 

## Step 8 - Set Up Port Forwarding ( optional but recommended )
- This is a optional step but a helpful & recommended one. What this does is make our honeypot more realistic by switching it from a Cowrie's custom port ( 2222/2223 ) to a real SSH/Telnet ports ( 22/23 - choose one! ). This can be done for a better insight in attacker's behavior because attackers try getting access into well-known ports, making this port forwarding more realistic. In translation, this is a way of system doing ' exchange ' - sending an attacker from a vulnerable port to a secure one where any action that's put in results harmlessly. Command example for redirecting from SSH port 22 to Cowrie port 2222 :
  sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
worth noting is that if you use nftables instead of iptables, the command will be different:
  sudo nft add rule ip nat prerouting tcp dport 22 redirect to 2222
due to the generation difference between these two firewalls, their commands slightly vary.

## Step 9 -Start Cowrie
- We are finally at the final step of our honeypot building! Before starting our Cowrie honeypot, we'll need to make sure that our virtual environment is still active - simply seeing ( cowrie-env ) means that it is activate ; in case you don't see it, check the link bellow the post for seeing how to fix it. Now, finally after all needed checkups, we can activate Cowrie! Running the following command helps us do that :
  bin/cowrie start
  after its starting, you should see a message confirming that Cowrie has started. But if you'd like additional confirmation about Cowrie's status ( is it running or if it has stopped ), following command helps us do that :
  bin/cowrie status
