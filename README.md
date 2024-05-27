# AI Content Profiler for Sitecore XP

A **Powershell Module** for **Sitecore XP** that leverages **Generative AI** to **analyze page content** and automatically assign the proper **Profile Cards**, enabling marketers to effortlessly implement **behavioral targeting** and streamlining the process of creating **personalized user experiences**.

![AI Content Profiler for Sitecore XP](/images/AI-Content-Profiler-Banner.png)

## Problem Statement

Marketers constantly strive to deliver targeted, personalized content to their audiences. Profile Cards in Sitecore XP play a crucial role in achieving this by enabling the segmentation of users and the delivery of content tailored to their interests and behaviors. 

![Profile Cards showing for a contact in Experience Profile](/images/best-pattern-matches.png)

Adopting and mantaining Profile Cards can be a daunting and time-consuming task for Content Editors. Analyzing content and picking the right Profile Cards can be challenging, and the frequent updates and changes require continual adjustments, leading to a significant burden on the content management team.

![Select Profile Cards dialogue in Sitecore XP](/images/2-tagging-content-multiple-profile-cards---tannis---two.webp)

## Behavioural Targeted Personalization made easy

This module leverages Generative AI to automatically assign Profile Cards to Sitecore Pages based on their content, ensuring that Profile Cards are always up-to-date, and dramatically reducing the workload on Content Editors. 

![AI Profiler Chunk in Content Editor](/images/AI-Profiler-Content-Editor.png)

By streamlining this process, the module allows marketers to adopt Behavioural Targeted Personalization with Profile Cards more quickly, and with less pressure on their team. 

### Key Benefits:

* **Automated Profile Assignment**: The AI-driven automation assigns Profile Cards to pages, ensuring they are always current without manual intervention.
* **Increased Efficiency**: Reduces the workload on Content Editors, allowing them to focus on creating quality content rather than managing Profile Cards.
* **Enhanced Personalization**: Facilitates the delivery of highly targeted and personalized content, improving user engagement and campaign effectiveness.
* **Quick Adoption**: Speeds up the implementation and benefits realization of Behavioural Targeted Personalization within your Sitecore websites.

## Prerequisites
* [Sitecore XP](https://developers.sitecore.com/downloads/Sitecore_Experience_Platform)
* [Sitecore Powershell Extensions](https://doc.sitecorepowershell.com/installation)
* [OpenAI API Key](CreatingAPIKeys.md) - Before using the module, you need to configure the OpenAI API Key. If you need help to get your API Key, follow the steps in the [Creating an OpenAI API Key guide](CreatingAPIKeys.md)

## Installation

**AI Content Profiler** is a content-only Powershell Module that doesn't include any binaries or executables. To start using it, all you have to do is to install the module into your Sitecore instance with a few simple steps.

The module is distributed in two flavors: 

- **Option 1 - Using a Sitecore Package (.zip)**, better for quick manual installations;
- **Option 2 - Sitecore CLI Content Serialization (.itempackage)**, more appropriated for automated deployments and continuous integration pipelines.

### - Option 1 - Using the Sitecore Package (.zip)

For a quick installation via Sitecore Package, follow the steps below:

1. Download the latest .zip package from the [Releases](https://github.com/peplau/AI-Content-Profiler/releases) page;
1. Install the package with the Sitecore Installation Wizard (In case of conflicts use the *Merge/Merge* option).

### - Option 2 - With Sitecore CLI Content Serialization (.itempackage)

To use SCS packages (.itempackage) as build artifacts in your continuous integration pipeline, install it in your delivery pipeline:

1. Download the latest .itempackage package from the [Releases](https://github.com/peplau/AI-Content-Profiler/releases) page;
1. Install the package in your delivery pipeline [following this instructions](https://doc.sitecore.com/xp/en/developers/104/developer-tools/create-and-install-a-sitecore-content-serialization-package.html#install-an-scs-package-in-your-delivery-pipeline).

### - Post-installation Steps

No matter the option selected, after installing the package, you need to sync the library with the Content Editor to make the module available for use:

1. Open Sitecore PowerShell ISE;

1. Go to Settings Ribbon, Rebuild All button, Sync Library with Content Editor Ribbon;
   ![AI Profiler Chunk in Content Editor](/images/Sync-Library-Ribbon.png)

1. (Optional) If you want to use the sample "Sitecore Public" Profile, [Deploy all marketing definitions](https://doc.sitecore.com/xp/en/users/104/sitecore-experience-platform/deploy-marketing-definitions-and-taxonomies.html#deploy-all-marketing-definitions-and-taxonomies) from the Marketing Control Panel.

## Configuring the Module

1. Open **/sitecore/system/Modules/AI Profiler/Settings/OpenAI Settings** item in Content Editor;

1. Populate the fields **API Key** with your [OpenAI API Key](#prerequisites) and select the **Model** you want to use;
  ![OpenAI Settings item](/images/OpenAI-Settings-Item.png)



## Usage
