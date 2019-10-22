# ODA-Alexa Integration - Alexa Set Up

Updated: October 17th, 2019

This part of the lab builds the Alexa side of the integration.

## Objectives

- Creating a Skill
- Configuring the Skill

## Steps

### **STEP 1**: Your Amazon Developer Account

- If you do not have a developer account, sign up for one here: [Sign Up](https://developer.amazon.com/en-US/alexa/alexa-skills-kit/start)

### **STEP 2**: Log in to your account

- Sign in to the developer console using your Amazon Developer account. This may require a one-time PIN which will be sent to your email. 

### **STEP 3**: Creating a Skill

- Ensure Skills Tab is selected 

- Click **Create Skill**.

<img src="images/100ODA/alexa-create-skill-1.png" alt="">

- Enter your skill name. Under **Choose a model to add**, select 'Custom'. Under **Choose a method to host your skill's backend resources**, select 'Provision your own'. Finally, select **Create Skill**.

<img src="images/100ODA/alexa-create-skill-2.png" alt="">

<img src="images/100ODA/alexa-create-skill-3.png" alt="" width="80%">

- From **Choose a template**, select 'Start from scratch'.

<img src="images/100ODA/alexa-create-skill-4.png" alt="" width="90%">

### **STEP 4**: Define the Skill

- From the created skill, select the **Invocation** option on the left panel.

<img src="images/100ODA/alexa-setup-skill-1.png" alt="" width="200">

- Under **Skill Invocation Name**, enter the phrase you would like to invoke the bot (must be 2 words).

<img src="images/100ODA/alexa-setup-skill-2.png" alt="" width="60%">

- Select the **Slot Types** option on the left panel. 

<img src="images/100ODA/alexa-setup-skill-3.png" alt="" width="200">

- Select **Add Slot Type**. Select **Create custom slot type** and enter a name for your slot. 

<img src="images/100ODA/alexa-setup-skill-4.png" alt="" width="70%">

<img src="images/100ODA/alexa-setup-skill-5.png" alt="" width="70%">

- Enter a name for your slot into the **Slot Values** textbox and press enter. 

<img src="images/100ODA/alexa-setup-skill-6.png" alt="" width="80%">

- Find the **Intent** option on the left panel.

<img src="images/100ODA/alexa-setup-skill-7.png" alt="" width="200">

- Create a new Intent with the **Add Intent** button

<img src="images/100ODA/alexa-setup-skill-8.png" alt="" width="200">

- Select **Create custom intent** and enter exactly "CommandBot" for your intent name. <!--This name cannot be the same as your slot name that you created previously.--> 

<img src="images/100ODA/alexa-setup-skill-9.png" alt="" width="50%">

- In **Sample Utterances**, enter {command} and press enter. 

<img src="images/100ODA/alexa-setup-skill-10.png" alt="" width="80%">

- Scroll down and find **Intent Slots**. For 'command' select your custom slot type as the slot type. 

<img src="images/100ODA/alexa-setup-skill-11.png" alt="" width="80%">

### **STEP 5**: Note the Skill ID

- Scroll to the top of the page and press the 'Your Skills' option. 

<img src="images/100ODA/alexa-setup-skill-12.png" alt="" width="360">

- Find your skill in the list, and click 'View Skill ID'. Copy this ID into notepad, as we will be using it later. 

<img src="images/100ODA/alexa-setup-skill-13.png" alt="" width="360">

**This completes the Set Up!**

**You are ready to proceed to [Lab 200](ODA-Alexa-200.md)**

