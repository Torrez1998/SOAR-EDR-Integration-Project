<div align="center">
  <h2>SOAR EDR Integration & Automation</h2>
</div>
<div align="center">
  <img src="https://github.com/user-attachments/assets/866274d9-7249-4ea0-9acd-1b93921c6d60" alt="Description" width="500">
</div>

# Project Objective
This project showcases the integration of Security Orchestration, Automation, and Response (SOAR) with Endpoint Detection and Response (EDR) to automate security workflows and enhance cybersecurity posture. Using LimaCharlie for EDR and Tines for SOAR, the project provides real-time security insights and automated responses, focusing on detecting and mitigating credential access attacks with the LaZagne tool.

LimaCharlie detects the use of LaZagne on endpoint devices, triggering automated alerts and remediation actions, with the option for users to decide whether to isolate affected machines. Communication is streamlined through Slack and email, ensuring timely alerts and responses, making security operations more dynamic and adaptable.

# Tools Used
- <b>Windows Machine</b>: Target machine LimaCharlie will detect for isolation decision, where users can choose to isolate it based on the threat severity.
- <b> LimaCharlie (EDR)</b>: Used to detect and respond to security threats.
- <b>Tines (SOAR)</b>: Automates the security workflows and orchestrates the response actions.
- <b>Slack</b>: Serves as the communication platform to receive alert detections.
- <b>SquareX (Email)</b>: Used to receive detection alert emails.
- <b>Vultr</b>: Cloud provider for hosting the virtual machine used in the project. (You can use other cloud providers or use Vmware/VirtualBox, just make sure they are connected to the internet)

# Skills Gained 
- Integration of SOAR and EDR Tools: Developed the ability to integrate SOAR tools with EDR platforms, enhancing automated incident response capabilities.
- Automation of Security Workflows: Learned to design and implement automated security workflows, enabling real-time detection, response, and notification processes that streamline incident handling.
- Threat Detection and Response: Gained experience in configuring and using LimaCharlie to detect threats on compromised endpoints, including decision-making on whether to isolate affected machines based on detected threats.
- Communication and Alerting Systems: Enhanced skills in setting up and managing communication and alerting systems using Slack and email, ensuring timely and effective dissemination of critical security information.
- User Prompt Configuration: Acquired the ability to create and configure user prompts within the SOAR workflow, allowing for interactive decision-making during the incident response process.
- Incident Response Management: Improved overall incident response management skills, including the ability to coordinate responses across multiple tools and platforms, ensuring a cohesive and efficient approach to handling security incidents.


#### <b> *Please note: You can use any cloud provider or hosted hypervisor for this project.* </b>
- [Vmware](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
----
# Windows Server Virtual Machine Setup in Vultr 

  Navigate to [Vultr](https://www.vultr.com/) and create an account. You can use any Cloud software.

<b> - Select Deploy + or Deploy New Server.</b>

![image](https://github.com/user-attachments/assets/8876a24c-eddc-4b52-a6e9-83a365454b27)




Select “Cloud compute - shared CPU or dedicated CPU for larger databases” as your New Instance and select your desired location.

![image](https://github.com/user-attachments/assets/7402ad1a-c91a-4b85-b7ce-3c87b7f7ec42)


For OS, select Windows Standard 2022.

![image](https://github.com/user-attachments/assets/c0bc2b14-24d3-436b-aa9d-5f060c2beda3)


Please select a plan, we went with vc2-1c-2gb.  In this case, it will be $28/month.

![image](https://github.com/user-attachments/assets/fceb8b7f-5965-4d9c-a291-aeb74a0a5bde)


Server settings can leave blank for this project. Name your Hostname & Label then hit "deploy"

![image](https://github.com/user-attachments/assets/b34a63e2-4bdf-4cc2-95ae-16ec0fbd9a42)


After you deploy the server, you will get the “Running” status

![image](https://github.com/user-attachments/assets/8adeecf5-dbf8-4f45-97e6-c2e97aee4fad)



Once the installation is completed and you get “Running” status, select “View Server Details” to obtain the machine’s password and “View Console” to access the VM.

![image](https://github.com/user-attachments/assets/8fd7a6fd-74bd-4d65-9bb6-d2ff8de1594a)


![image](https://github.com/user-attachments/assets/d415d649-6040-4b88-9892-b39bf7816f8e)


-----
<b> - Next, we’ll set up the firewall.</b>.

Under products, select <b>Network</b> > <b>Firewall</b> > <b>Firewall Group</b>.

![image](https://github.com/user-attachments/assets/af71f3f3-ebd1-4897-a34c-0efd16f58869)

![image](https://github.com/user-attachments/assets/6ae9a0aa-67e4-44dc-aa55-12fb3839c88d)



Give a Description Name and select <b>Add Firewall Group</b>

![image](https://github.com/user-attachments/assets/8cdc976b-62b8-476c-bab1-baf9e4a6bb0c)


For Protocol, select <b>MS RDP</b>. <b>Source</b>, select <b>my IP or custom add it in</b> and hit the + button. 

![image](https://github.com/user-attachments/assets/014bf562-3344-4536-a59d-bb187964fefd)


To add the firewall, go back to your machine and select <b>Settings</b> > <b>Firewall</b> > Click the dropdown and select the firewall you created > <b>Update Firewall Group</b>. We are good to go.

![image](https://github.com/user-attachments/assets/948a18aa-c06b-4ab6-914c-2234cf03a833)

![image](https://github.com/user-attachments/assets/27c8bf11-240e-4cfd-9fc8-f23d38c24c34)

![image](https://github.com/user-attachments/assets/00561065-90fd-4e4e-b449-7bb805843a3e)

![image](https://github.com/user-attachments/assets/dec88e9f-08aa-48b3-a45b-1fb33114179f)


-----
# ![LimaCharlie](https://images.ctfassets.net/8ypp714zy4gs/56gQDOjtMywHI4R70K8WdJ/162b909916246fd2cb77fd95c0f74100/LimaCharlie_LogoMarkOnly_WHITE.png?w=64&q=100) EDR Installation on Virtual Machine

Navigate to [LimaCharlie](https://limacharlie.io/) and create an account.

Create a New Organization, select your name and desired residency region.

![image](https://github.com/user-attachments/assets/51cd1acd-a624-446e-9258-23a9c87f6169)


For the installation key, go to Sensors and click "Installation keys" remove the default keys and create a new key with your description.

![image](https://github.com/user-attachments/assets/a71d067e-ea90-4155-8508-70784441fca8)

![image](https://github.com/user-attachments/assets/2657c50c-a377-439e-ba46-b01d621bca39)

![image](https://github.com/user-attachments/assets/b1257d40-ac3c-450d-8188-8e55ffe8e044)



Next, under <b>Sensor Downloads</b> in the same "Installation keys" section, copy the link address for the <b>Windows 64 bit</b> EDR agent and paste into server MS Edge page.

![image](https://github.com/user-attachments/assets/299c29d3-cf6d-4121-b850-db0b0ab0cea8)

![image](https://github.com/user-attachments/assets/c8215eae-7dfd-4f00-a971-26c063f4fd9b)


Next copy sensor key which is the installation key

![image](https://github.com/user-attachments/assets/eb891ee5-4be2-4a4f-8c50-cf7b8441e9c6)


Open Powershell on the Server as <b>Administrator</b>.
![image](https://github.com/user-attachments/assets/bf152697-a1dd-4164-9d1f-0e73101c7474)

Navigate to the downloads directory.
hcp  
![image](https://github.com/user-attachments/assets/95d4f635-cafd-46c9-b636-141edb24039b)

Type in the hcp.exe downloaded, insert <b> -i </b>, the sensor key (installation key) and hit enter.

![image](https://github.com/user-attachments/assets/615e120c-22d7-4b31-9d3c-06b9db61d66d)


<b>Sweet! The Agent was installed successfully!</b>

![image](https://github.com/user-attachments/assets/5b6e105e-f451-4693-b05f-5e3dc476e99a)


We can confirm that the sensor is active in Services! 

![image](https://github.com/user-attachments/assets/328fa7a5-ef11-43ec-9968-ce1efa839028)


Go back to limacharlie and check that your server is on your sensory list and click to get an overview and other commands.

![image](https://github.com/user-attachments/assets/1ef3341a-c61b-4908-83c0-cc94e54126e4)


---
<b> - Next, we will download LaZagne (Password Recovery Tool) on the Windows Server to generate telemetry in LimaCharlie </b>

Click on the [LaZagne](https://github.com/AlessandroZ/LaZagne) Repo by Alessandro and select <b>Release v2.4.6 > LaZagne.exe</b>

#### <b> *Please note: You will have to disable Real-time protection under Windows Security for LaZagne.exe to download successfully.* </b>

From the downloads folder, hold shift and right-click on <b>LaZagne</b> and <b>Open Powershell window here</b>.

<img src="https://github.com/user-attachments/assets/cef7b445-21ea-4c0c-85fa-088ef4815458" width="500" />

Can confirm LaZagne is working. 

<img src="https://github.com/user-attachments/assets/4e293a18-2073-46ff-a320-1e338d96c34a" width="500" />

After running the command, LimaCharlie will generate a <b>NEW_PROCESS event</b>.

<img src="https://github.com/user-attachments/assets/ff96c3bf-6c75-415b-934e-7413d4b9e94a" width="500" />

Event Information:

![image](https://github.com/user-attachments/assets/9d82cd95-22a1-42c4-9d54-8b7848e3fbf6)



<b> - Detection & Response Rule Creation </b>

Navigate to <b>Automation</b> > <b>D&R Rules</b> > <b>New Rule</b>. 

![image](https://github.com/user-attachments/assets/6a9fe386-dfd4-4173-b406-9119f7afa62a)


#### - *We will use a template as a guide to help create what we need for our detection rule.*
Navigate to <b>Automation</b> > <b>D&R Rules</b> > <b>windows_process_creation/proc_creation_win_lolbin_device_credential_deployment</b>

<img src="https://github.com/user-attachments/assets/3440779a-44b8-4425-a371-cd1bb6fdc1de" width="500" />

Under the D&R rule, click on the GitHub repository.

<img src="https://github.com/user-attachments/assets/aa02e367-9c30-4e95-b204-3243e9f08ebe" width="500" />

Select <b>Raw</b> and copy the rule content. 

<img src="https://github.com/user-attachments/assets/9b6aeddf-861d-4511-b02d-90e859820254" width="500" />

*<b>Modify the rule content.*</b>

Detect Rule:

![image](https://github.com/user-attachments/assets/224d9803-9971-425c-9a8f-24fdcfa2d932)


Respond Rule:

![image](https://github.com/user-attachments/assets/83bdda82-87ad-4e29-ac56-4f5684539a90)


Name the New Rule and hit save:

![image](https://github.com/user-attachments/assets/adc60153-7aed-4daf-ae82-b5d4e0ff49d4)


To test the new rule, go down the page, copy the event from the timeline, paste it into the event section, and hit <b>Test Event</b>.
  
![image](https://github.com/user-attachments/assets/6effdd49-e346-462e-a549-317b8ae346c7)



*<b>Can confirm that the new rule is working.</b>*

![image](https://github.com/user-attachments/assets/c4d8cffa-f2bc-4c69-a625-bf904bb4260b)


*After running a command in the Windows Server, a detection will pop up under the <b>Detections</b> tab.*
You will now get detections!
-----
# ![Slack](https://a.slack-edge.com/3d92b39/marketing/img/nav/slack-salesforce-logo-nav-white.png)

Create [Slack](https://slack.com/get-started#/createnew) account. 

Create A New Workspace. 

![image](https://github.com/user-attachments/assets/69a3e7d2-44ff-4246-96f2-eef2a4e1b395)


Choose the free plan.

Create a new channel and name it <b>alerts</b>.

![image](https://github.com/user-attachments/assets/131fbca3-4b2e-4b85-853b-23c6b0fedcc2)

![image](https://github.com/user-attachments/assets/485d5066-f474-4624-b961-acd7733c08bb)


---- 

<img src="https://firebasestorage.googleapis.com/v0/b/standards-site-beta.appspot.com/o/documents%2Fjycsjx9ypwh%2F02csbs2azqv%2FTinesLogoWhite.svg?alt=media&token=f31af318-7b96-463b-8048-9835598142ae" alt="Tines Logo" width="150" />

Create a free [tines](https://www.tines.com/) account.

Go to Tines dashboard ny clicking icon on the top left side.

![image](https://github.com/user-attachments/assets/ef9d3587-d294-4c9f-b4ad-8a6de7a748de)

![image](https://github.com/user-attachments/assets/cf854dbe-f44d-4a10-962a-60f5d13f7be5)


*<b>The goal is to link LimaCharlie and tines.*</b>

Grab the <b>Webhook</b> icon from the tools section and drag it to the story. 

Name the Webhook <b>Retrieves Detections</b> and Description <b>Retrieves Detections from LimaCharlie</b>. 

Copy the <b>Webhook URL</b> and go to LimaCharlie. 

![image](https://github.com/user-attachments/assets/3619e8a2-0878-40ac-a9da-b1f44884dec1)


In LimaCharlie, navigate to <b>Outputs > Add Output > Detections > Tines.

![](https://github.com/user-attachments/assets/83d0f0a4-d3c1-4e81-a6d5-33c7c525611e)
![](https://github.com/user-attachments/assets/6997900f-f5e5-4289-96c9-711b1e8ff1b2)
![](https://github.com/user-attachments/assets/830badc7-fb4b-4dd8-ae81-e2e65d6e5cb9)

Name the Output and paste the Webhook URL.

![image](https://github.com/user-attachments/assets/65955a5d-ee93-43a8-b164-a1ce5a7c76f8)


*<b>After saving the output, you will not see a detection. Run a command in the virtual machine, Refresh Samples, and a sample detection will appear.</b>*

![image](https://github.com/user-attachments/assets/05876e87-4175-4f67-9a77-f7dcc8e9acdf)


GO BACK TO TINES. Under <b>Retrieve Detections</b>, select <b>Events</b> and take a look at the most recent event. 

![image](https://github.com/user-attachments/assets/4ef9b384-eeb7-4374-91f4-760ad3dbb786)

![image](https://github.com/user-attachments/assets/dde4029d-434b-43a1-8e03-ad1dfe56e7af)


*<b>Next, we will link tines to slack.</b>

On slack, select <b> More > Automations > search for tines > Add > Add to Slack.</b>

<img src="https://github.com/user-attachments/assets/c84cd47e-d729-49d9-9c0e-c941b8004168" width="300" />

Follow the steps for installing the app. 

<img src="https://github.com/user-attachments/assets/9696c5d1-1012-4bc7-b4d7-e657e9aa3205" width="500" />

In the tines dashboard, navigate to <b>Your teams > Credentials > New Credentials > Slack > Use Tine's app for Slack </b>

![](https://github.com/user-attachments/assets/f924649b-3ac7-4602-a3b1-039fbc497160)

![](https://github.com/user-attachments/assets/c7e7b120-b322-459f-b482-98c61c1b5df2)

![](https://github.com/user-attachments/assets/5c44bb84-a085-4085-a9f9-2575f51e388f)

New Slack Credential.

![](https://github.com/user-attachments/assets/2625a7fe-3c34-496a-b9d2-d683881882e6)

*Slack & LimaCahrlie Credentials will be needed moving forward.*

![](https://github.com/user-attachments/assets/c72df98c-1e6c-4dd4-ac29-ca1555e1422f)

Under templates in tines, select <b> Slack > Send a message template.</b>

On slack, right-click on alerts, select view channel details, and copy channel ID.

![](https://github.com/user-attachments/assets/212763bb-cf8e-4c29-98ca-71e423139a4f)

![image](https://github.com/user-attachments/assets/042ddb30-9861-4878-aedc-a41b63140716)


Paste the channel ID on tines.

![image](https://github.com/user-attachments/assets/8b49dc2b-5ac8-4651-824d-03f8fc4eb2a4)


Connect Webhook and Slack on Tines by dragging a line attaching them and run to check if they are connected.

![image](https://github.com/user-attachments/assets/e60b8d4e-932e-4355-89cf-7b861a735688)

go back to Slack and check to see if we received the message.

![image](https://github.com/user-attachments/assets/96a6e106-6433-4566-bf8f-6bfd784fcc36)

Now that this is done we can move on to sending an email.


----
<b> - Next we'll create a Send Email Action.</b>

Drag the Send Email Action onto the story and connect it to Webhook. 

Name the <b>Description, Sender name, and Subject</b>. 

use a burner email for this

![image](https://github.com/user-attachments/assets/f77f4787-6408-46f8-aa51-38ec4db748d3)


Select Run > Retrieve Detections > Test. 

![image](https://github.com/user-attachments/assets/66847713-cbcc-48c5-afd0-11e1ae503921)


Confirmed email!

![image](https://github.com/user-attachments/assets/2fefb9c9-23b3-4934-b9d8-e5ee6de28729)


---
<b> - For User Prompt, we will also edit what we copy and pasted into our notepad here into the contents. </b>

![image](https://github.com/user-attachments/assets/2c5501de-d84a-47db-b108-8e35d0dce609)


Next we will make an if/else trigger. for the Rule we are using User_prompt -> body -> body -> isolate. If this does not pop up, then you need to generate an event from the user prompt by visiting page and going through the response.

![image](https://github.com/user-attachments/assets/b10afd43-8e2b-4748-b899-59274a61d37c)

Duplicate the first slack message connection to make a new one with recieving detections from the computer only including a response.

![image](https://github.com/user-attachments/assets/0e128927-e657-4ace-a192-9cbb446e56ec)

![image](https://github.com/user-attachments/assets/6e165a60-9277-4079-bc5b-26be55c153b9)

connect to trigger.

![image](https://github.com/user-attachments/assets/540d5ade-b4ec-4c24-801f-e429879eaa0e)


go back to Webhook and click on Events and under "retrieve detections" extend "body".

![image](https://github.com/user-attachments/assets/b69d0df0-7535-423d-9d31-dccd5ebabc8c)

Use Notepad to organize yourself as we will copy and paste the fields we are interested in. Make sure to put them in an order so when we receive this message with the information, it is organized. Example image below. 


![image](https://github.com/user-attachments/assets/df7fade8-82d8-484c-a902-739b5ec5ae2b)

Cool!!

Go to your Slack in Tines and in messages copy and paste what we copied from webhook. You can also name your information and re-paste.

![image](https://github.com/user-attachments/assets/8f23efdf-b26e-4880-96f5-3abfa2fe43f4)

![image](https://github.com/user-attachments/assets/77be59f9-b1e7-479c-a871-f37055aaa859)


Go to Slack and test and alert, all the information should pop up.

![image](https://github.com/user-attachments/assets/f702e7ca-7666-44a0-a4fb-da0d9dbc051a)

We will make sure we can send an email as well. go to "send email" on Tines and in the body section, add the "Retrieve detections" info we copied and pasted and change it into HTML Format so the email comes out correctly. Simply add the next line commmand to each section. Run and test.

![image](https://github.com/user-attachments/assets/6a0c5994-0004-436c-ba05-a09f424ff9ff)

![image](https://github.com/user-attachments/assets/f6945d39-8fa5-4116-b2b7-e8fba7bfab08)

![image](https://github.com/user-attachments/assets/717881d7-9d2e-4bad-88d1-5ff413a071cd)

Beautiful.


---

<b> Select the Trigger tool and drag to story. Name it No and input the rules. </b>

![](https://github.com/user-attachments/assets/e1338c23-989a-4638-94e7-ab78dcdb57f3)

![](https://github.com/user-attachments/assets/f382830b-4fbb-483b-aa9f-30d9715804f0)

Add the Slack template to <b>Send a message</b> and connect it to the Trigger action. 

![](https://github.com/user-attachments/assets/cf2671ff-7092-422f-8bbc-6ba7f48d7967)

Under Message, add the value, <b>retrieve_detections.body.detect.routing.hostname</b>. 

![image](https://github.com/user-attachments/assets/8200247a-7780-492f-8b90-9f8f3894f58f)


Visit the User Prompt page and select No.

![image](https://github.com/user-attachments/assets/810a809b-daa4-413d-9694-2edc2aa388b3)


*<b>A message will appear on slack to investigate.</b>*

![image](https://github.com/user-attachments/assets/9d884cf1-7f53-4a57-978a-520074be7e73)

Next we will setup the automated response when we select "yes" for the user prompt.
we will need to create another trigger, change the name to "Yes" and the rule from "false" to "true" and connect to user prompt.

![image](https://github.com/user-attachments/assets/e538c16e-23c4-4538-a9c0-6f3e8f5b9270)

next we will need to connect limacharlie to Isolate the virtual machine. build a template and search for an isolator.

![image](https://github.com/user-attachments/assets/e09afa45-1aa0-4f7a-90c4-040f629350d1)

copy and paste the sid onto the URL.

![image](https://github.com/user-attachments/assets/fe440cf6-81f6-4aac-aab7-2ef99ba32087)

We need to create a credential for lima charlie.
go to limacharlie and EXTEND "Access management"  and you will see "REST API" We need to copy the organization API Keys as it is recommended to use in their Documentation.
go to main menu of Tines and click on credentials, we will make this a text credential.


![image](https://github.com/user-attachments/assets/be4b0af0-0792-42e8-ae60-f1a2e213af9d)

![image](https://github.com/user-attachments/assets/eba69df0-9e8e-434e-a465-bec3da4d4885)

![image](https://github.com/user-attachments/assets/24696f1d-370d-4917-96a0-d4896151d208)

![image](https://github.com/user-attachments/assets/513d9625-21e0-4068-a3ea-77c8231d8f77)

create the text credentials for LimaCharlie, and under "Value" paste the Org API

![image](https://github.com/user-attachments/assets/916748b1-4211-4a41-a9af-24924a1a7688)

add the limacharlie domain as shown. this will ensure the credentials can only be used for this website and any subdomains.
after that hit save and it should create the credential for you.

back into our story on Tines. Connect limaCharlie with the credentials we just made.

![image](https://github.com/user-attachments/assets/d6a92731-6aad-4e45-bc23-0c29b9e4839f)

now for the moment of truth, lets run the playbook specifically the "yes" prompt and see if its isolates the machine.
Go to LimaCharlie under "sensors" then "sensors lists" and check to see if your machine is isolated. might need to refresh the page to show. 

![image](https://github.com/user-attachments/assets/e3f8e0b0-1a8a-4585-b1d2-f0e1358e5fac)

Great!

next we need to show this as a message on Slack. lets copy the Slack from the "no" trigger side.

![image](https://github.com/user-attachments/assets/f118ba57-7b6f-403f-8efe-4d43e1825dd1)

Next create a limaCharlie template so we can add an Isolation status into our Slack Message.

![image](https://github.com/user-attachments/assets/ed4a954e-c0e2-4ebc-9b70-5457ea5edfd3)

Build out the template. and make sure that the credential is correct by connecting to the LimaCharlie one we created earlier as it will show that it needs to be connected.

![image](https://github.com/user-attachments/assets/94dd7b09-ccb9-412a-936d-170895d29c8e)

![image](https://github.com/user-attachments/assets/f03de3fa-17bf-4fa3-818f-67b01b501c44)

connect Story sections.

![image](https://github.com/user-attachments/assets/0d591697-7949-428a-b8b3-32cde9e57d9e)

Let us Edit our Most recent Slack template to get our Isolation status. make sure to re-run the story so that Slack can receive data to pull. you can quickly do this by Re-emiting the User Prompt.

![image](https://github.com/user-attachments/assets/072d0d65-d33b-4b52-9337-a08e92a79adc)


![image](https://github.com/user-attachments/assets/9a560bb8-bd27-4bdc-987c-5859987c4f49)

Everything should be Setup and done! Lets test everrything out by playing our our story on the "Yes" Prompt and "no", and making sure we receive our messages and emails.

We got our first Slack message.

![image](https://github.com/user-attachments/assets/198d54dc-07e5-4f4e-874f-ab809237441e)

We got our E-mail.

![image](https://github.com/user-attachments/assets/051e9d23-90d8-48bf-8470-b78daed12c8e)

Our User Prompt page is displaying the correct info.

![image](https://github.com/user-attachments/assets/cbe9d773-6a60-4f1c-b794-9e23cd6867d0)

The "no" Prompt is working.

![image](https://github.com/user-attachments/assets/05871c56-e2ff-4fd3-9231-4777057594df)

Our "Yes" Prompt is also working. We can check LimaCharlie and see that our VM is isolated and that we received our Slack message.

![image](https://github.com/user-attachments/assets/30f43049-32eb-4d8c-981c-17b147c62794)

![image](https://github.com/user-attachments/assets/e4c4f400-686e-405f-8d3e-92e0e1a32a19)

To double check that our VM is isolated I Pinged Google.com to see if we have a connection and we don't.

![image](https://github.com/user-attachments/assets/2a7218c2-0b53-4b81-b9d0-3052076857f2)

Final Tines playbook.

![image](https://github.com/user-attachments/assets/fdb5df89-5c15-49f4-97c6-f211eee12151)
