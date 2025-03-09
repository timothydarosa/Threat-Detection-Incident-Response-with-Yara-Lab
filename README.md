# Threat-Detection-Incident-Response-with-Yara-Lab

**Cyber Attack/Defense home lab using Sliver, LimaCharlie [SIEM], & VM's to simulate C&C, Threat Detection, and classifying malware with YARA etc.   
I did a demonstration on this home lab be sure to check it out on Youtube below.   
Thanks for Eric Capuano for putting this blog together it has tons of value...**
###
**[Click to watch My Youtube Demonstration for this Lab](https://youtu.be/O-iN99pJXZM)**

## Project:
The goal of this lab is to simulate an actual cyberattack and to detect and respond to endpoints. I'll be simulating the threat and victim machines using virtual machines, following Eric Capuano's online tutorial. 'Sliver' will be used as a C2 framework by the attack machine to target a Windows endpoint that is running 'LimaCharlie' as an EDR solution.

Eric Capuano's Guide: https://blog.ecapuano.com/p/so-you-want-to-be-a-soc-analyst-intro?utm_campaign=post&utm_medium=web

## Setup

Setting up both machines is the initial stage in the lab. The endpoint will be running Windows 11, while the attack computer will be running Ubuntu Server. Microsoft Defender should be disabled (along with other settings) for this lab to function properly. In addition, I plan to install LimaCharlie as an EDR solution on the Windows computer and Sliver as my adversary tool on the Ubuntu computer. LimaCharlie will import Sysmon records and have a sensor connected to the Windows computer.

> Windows 11 Machine - Turn off Microsoft Defender & Go into registry and disable it too. Installed Sysmon as with swifts configuration well.
![image](https://github.com/user-attachments/assets/2f8c55af-0be3-4448-bcac-31e6f07240e9)
![image](https://github.com/user-attachments/assets/89b16d4e-2307-4d92-a9f9-bd4706b012dc)
![image](https://github.com/user-attachments/assets/f2de3618-bf2c-4bd0-bc01-fa8e14d98688)
![image](https://github.com/user-attachments/assets/f3d46b82-7236-4850-9b66-21fec13b81f9)
![image](https://github.com/user-attachments/assets/479fdba7-84d7-4d7d-9c0a-8400185b913d)   
> Ubuntu Machine - Install Sliver Server and other dependancies
![image](https://github.com/user-attachments/assets/94793c0b-e4c4-4836-ba94-e5142c9cb0e3)

## Let's start Attacking & Defending !
Creating our payload on Sliver and infecting the Windows host computer with malware is the first stage. Once the malware has been run on the endpoint, we can establish a command and control session.   

> Let's make a payload and run our malware   
![image](https://github.com/user-attachments/assets/ff9167d7-f4b7-417d-87d7-87ed11a32d55)
![image](https://github.com/user-attachments/assets/271557df-c03a-4fba-8158-9bf53da9b795)

> Now that our malware was executed on the endpoint, we can establish our C2 session. The attack machine can allow us to now start looking around, verifying privileges, obtaining host information, and determining the host's security level since we have a live session between the two machines.   
![image](https://github.com/user-attachments/assets/5d1b6efd-a33c-45dc-9e21-add526cc422c)
![image](https://github.com/user-attachments/assets/4347f446-768d-4f96-8b97-3467de5974c8)
![image](https://github.com/user-attachments/assets/3fe4e2b9-81ba-41ed-afe2-f82d5b6fc955)

> We can examine our LimaCharlie SIEM on the host computer and see the attacker's telemetry. We are able to determine which payload is operating and which IP address it is linked to.
![image](https://github.com/user-attachments/assets/6f251470-548f-48cd-b0ca-ad0d674baef4)
![image](https://github.com/user-attachments/assets/72f30feb-d46c-44de-ba39-f1a2d142309f)
![image](https://github.com/user-attachments/assets/17219a4d-3365-45e5-96b6-306065b157b8)

> It says file is not found because we just created our malware and the hash has never been seen before, but that does not mean it innocent.
![image](https://github.com/user-attachments/assets/73ed040c-6ec8-4844-b58d-f01021d69824)   

> If I dragged the EXE inside VT, it is then analyized and detected by multiple Security Vendors like BitDefender, Microsoft, Kaspersky, and etc.
![image](https://github.com/user-attachments/assets/a42ab505-d3ff-42b0-b758-0737509b95f5)
#

> By dumping the LSASS memory on the attack machine, we can now mimic an attack to steal credentials. To identify the sensitive process, we can write rules, monitor the telemetry, and inspect the sensors in LimaCharlie.   
![image](https://github.com/user-attachments/assets/ba850b10-03e9-4cf1-b54d-91d76c17c097)
![image](https://github.com/user-attachments/assets/77c2a9cd-1bdc-40f5-a795-9207f3f2207a)
> Now that we created a D&R Rule it should time out and give us a detection response.
![image](https://github.com/user-attachments/assets/ac6c08b3-1e4c-4208-ab2e-491bfe6e7105)
![image](https://github.com/user-attachments/assets/5bcd0014-da2b-4b6c-80ed-21aa852b9544)   

#
We can now practice writing a rule that will identify and stop the attacks coming from the Sliver server using LimaCharlie, rather than just using detection. By trying to remove the volume shadow copies on the Ubuntu computer, we can mimic some aspects of a ransomware attack. We can view the telemetry in LimaCharlie and then create a rule that completely prevents the attack. The Ubuntu machine won't be able to attempt the same attack again once we've created the rule in our SIEM.   


![image](https://github.com/user-attachments/assets/ff2960dc-b5a1-47d1-8ec6-c448c9c4a7a4)
![image](https://github.com/user-attachments/assets/d5930420-8310-44fd-9ecf-7e8d0a50e908)
![image](https://github.com/user-attachments/assets/62d1b9a3-2f84-4781-ab5b-94391e71841a)
![image](https://github.com/user-attachments/assets/c053494a-ff10-49d9-bef0-693d71ce1d16)
![image](https://github.com/user-attachments/assets/67a73ca2-763a-4ab2-ba2c-038c94d32cc3)

#
You can continue the rest of the lab on YouTube.

