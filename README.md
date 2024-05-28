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

1. Under **/sitecore/system/Modules/AI Profiler/Settings/Trees/Home**, create at least one item with the template **Tree Settings** (Insert Options are configured, use the Insert menu) pointing to the root item of the content tree you want to analyze:
   ![Tree Settings item](/images/Tree-Settings.png)
    1. **Root**: Point to the root item of the content tree to be profiled; 									
	1. **Process Profiles**: Select the Profile Cards to be used in the profile. Profile Cards are stored under **/sitecore/system/Marketing Control Panel/Profiles** and can be defined by your marketing team to represent your most common audiences. For further information about creating Profiles [check this documentation page](https://doc.sitecore.com/xp/en/users/104/sitecore-experience-platform/content-profiling.html);


## Usage

After the module is installed and configured, you will see these two buttons in the Content Editor Ribbon, under **Analyze**:

![AI Profiler Chunk in Content Editor](/images/AI-Profiler-Content-Editor.png)

> [!NOTE]
> The **Profile Page** button will be disabled if the selected item doesn't have some Layout configured (is not a *Page Item*). The **Profile Tree** button will be disabled if the selected item doesn't have some Layout, or no children items underneat it.


### CASE 1 - Profiling an individual Page

You can profile an individual page by selecting an item at the tree in Content Editor and clicking the **Profile Page** button under the **Analyze** ribbon (see screenshot above). 

The module will analyze the page content and assign Profile Cards accordingly. When the process finishes, you can then see the assigned Profile Cards in Content Editor at the top right corner:

![Assigned Profile Card to the profiled item](/images/Profile-Cards-Assigned.png)

> [!TIP]
> If you don't see the Profile Cards assigned, verify the following:
> - The **Tree Settings** item is correctly configured:
>	- The **Root** field has a path that encompasses the profiled item;
>	- The **Process Profiles** field points to at least one valid Profile, that is correctly deployed and has meaningful information the AI can use to profile your content;
> - The profiled item has some valid content  

### CASE 2 - Profiling an entire Content Tree

> [!NOTE]
> When profiling a full Tree, items if they have some Layout (also known as *Page Items*). Items without Layout configured will be ignored.

### CASE 3 - Automatic profiling triggered via Workflow 


### How the Tree Settings item is selected

If more than one **Tree Settings** item has the **Root** field pointing to items under the same path, the one with path closer to the item being profiled will be used.

For instance, consider the following **Tree Settings** items:

- **TreeSettings1**: 
  - **Root**: */sitecore/content/Home*
- **TreeSettings2**: 
  - **Root**: */sitecore/content/Home/Products*

The chosen **Tree Settings** item is determided by the path of the item being profiled:
1. If the path is */sitecore/content/Home/Products/CDP*, **TreeSettings2** is used (because this path is closer to */sitecore/content/Home/Products* than */sitecore/content/Home*)
1. If the path is */sitecore/content/Home/ContactUs*, **TreeSettings1** is used (because */sitecore/content/Home* is the only one matching this path)



