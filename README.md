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

<hr/>

### Option 1 - Using the Sitecore Package (.zip)

For a quick installation via Sitecore Package, follow the steps below:

1. Download the latest .zip package from the [Releases](https://github.com/peplau/AI-Content-Profiler/releases) page;
1. Install the package with the Sitecore Installation Wizard (In case of conflicts use the *Merge/Merge* option).

<hr/>

### Option 2 - With Sitecore CLI Content Serialization (.itempackage)

To use SCS packages (.itempackage) as build artifacts in your continuous integration pipeline, install it in your delivery pipeline:

1. Download the latest .itempackage package from the [Releases](https://github.com/peplau/AI-Content-Profiler/releases) page;
1. Install the package in your delivery pipeline [following this instructions](https://doc.sitecore.com/xp/en/developers/104/developer-tools/create-and-install-a-sitecore-content-serialization-package.html#install-an-scs-package-in-your-delivery-pipeline).

<hr/>

### Post-installation Steps

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


## Usage Instructions

After the module is installed and configured, you will see the following buttons in the Content Editor Ribbon, under **Analyze**:

![AI Profiler Chunk in Content Editor](/images/AI-Profiler-Content-Editor.png)

> [!NOTE]
> - **Profile Page** is disabled if the selected item has no Layout (is not a *Page Item*);
> - **Profile Tree** is disabled if the selected item has no Layout and no children items underneat it.

<hr/>

### CASE 1 - Profiling an individual Page

You can profile an individual page by selecting an item at the tree in Content Editor and clicking the **Profile Page** button under the **Analyze** ribbon (see screenshot above). The page content will be analyzed and Profile Cards assigned accordingly. 

When the process finishes, you can then see the assigned Profile Cards in Content Editor at the top right corner:

![Assigned Profile Card to the profiled item](/images/Profile-Cards-Assigned.png)

> [!TIP]
> If after profiling a page you still don't see the Profile Cards assigned to it, follow the steps below:
> 1. Check if the **Tree Settings** item is correctly configured, including:
>     1. The **Root** field has a path that encompasses the profiled item;
>     1. The **Process Profiles** field points to at least one valid Profile, the Profiles are correctly deployed and have meaningful information that can be used to profile your content.
> 1. Verify if the profiled item has any valid content, and the content matches the Profile Cards you are expecting to see assigned.
> 1. Check the Sitecore CM logs for any errors or warnings that might have occurred during the profiling process.

<hr/>

### CASE 2 - Profiling an entire Content Tree

To profile an entire content tree, select the root item to be analyzed in Content Editor and click the **Profile Tree** button under the **Analyze** ribbon. The content tree will be entirely analyzed, and Profile Cards  assigned accordingly. 

When the process finishes, you can then see the assigned Profile Cards in Content Editor, as seen in [CASE 1](#case-1---profiling-an-individual-page).

> [!NOTE]
> When profiling a full Tree, items will only be processed if they have some Layout (also known as *Page Items*). Items without Layout configured will be skipped.

> [!TIP]
> If after profiling a page you still don't see the Profile Cards assigned to your pages, please go throught the same debugging steps as described in [CASE 1](#case-1---profiling-an-individual-page).

<hr/>

### CASE 3 - Automatic profiling triggered in a Workflow 

To keep the page profiling always updated as your content changes, you can automate the profiling process with Workflows. 

The module comes with a sample workflow called **Sample AI Profiler Workflow**. When using this workflow, the content profiling is triggered at the **Run AI Profiler** action, after the command **"Approve and Publish"** is executed (normally by the content reviewer).

![Sample AI Profiler Workflow](/images/Demo-Workflow.png)

> [!TIP]
> You can easily integrate the **Run AI Profiler** action in your custom workflows. To do so, copy the OOTB action to your workflow, or follow the steps below:
> 1. Create a new action item under your workflow command using the template **/sitecore/templates/Modules/PowerShell Console/PowerShell Script Workflow Action**
> 1. Point the **Script** field to **/sitecore/system/Modules/PowerShell/Script Library/AI Profiler/Module/AI Profiler - Workflow Action**
> 1. Edit the Enable Rule field as shown in the screenshot above, by selecting the condition "where the item has a layout"

## Frequently Asked Questions (FAQ)

### Q1 - When profiling a page, how is the Tree Settings item selected?

The **Tree Settings** item is selected based on the path of the item being profiled. If more than one have the **Root** field pointing to items under the same path, the one with closer path to the profiled item will be used.

For instance, if we have the following **Tree Settings** items:

- **TreeSettings1**: 
  - **Root**: */sitecore/content/Home*
- **TreeSettings2**: 
  - **Root**: */sitecore/content/Home/Products*

The chosen one is determided by the path that is closer to the profiled item:
1. If the profiled path is */sitecore/content/Home/Products/CDP*, **TreeSettings2** is used because this path is closer to */sitecore/content/Home/Products* than */sitecore/content/Home*;
1. If the profiled path is */sitecore/content/Home/ContactUs*, **TreeSettings1** is used because */sitecore/content/Home* is the only one matching this path.

### Q2 - After profiling a page (or an entire tree) I still don't see any Profile Cards assigned, what should I do?

If after profiling a page you still don't see the Profile Cards assigned to them, verify the following:
1. That the **Tree Settings** item is correctly configured, including:
    1. The **Root** field has a path that encompasses the profiled item;
    1. The **Process Profiles** field points to at least one valid Profile, the Profiles are correctly deployed and have meaningful information that can be used to profile your content.
1. The profiled item has some valid content, and the content matches the Profile Cards you are expecting to see assigned.
1. Check the Sitecore CM logs for any errors or warnings that might have occurred during the profiling process.

### Q3 - What elements are important for a Profile to be relevant and effectively utilized in profiling?

A Profile is a collection of attributes that represent a specific audience segment. To be effective, a Profile should contain attributes that are relevant to the audience segment it represents. 

The module comes with a sample Profile called **Sitecore Public**, representing some possible profiles of visitors interested about Sitecore content. 

![Demo Profile called 'Sitecore Public'](/images/Demo-Profile--Sitecore-Public.png)

When the content profiling starts, your Profiles are serialized and sent to the GenAI as part of the content to be analyzed. The following Profile fields are serialized (in the same order as in the above screenshot):

1. **Profile** (Template: */sitecore/templates/System/Analytics/Profile*)   
   1. Name
   1. Description
1. **Profile Keys** (Template: */sitecore/templates/System/Analytics/Profile Key*)
   1. Name
   1. MinValue
   1. MaxValue
1. **Profile Cards** (Template: */sitecore/templates/System/Analytics/Profile Card*)
   1. Name
   1. Details
   1. Description
   1. Profile Card Value

> [!TIP]
> To ensure the best results when building your Profiles, make sure to include meaningful content on each of these field.
   

### Q4 - What elements are important for my content to be effectively profiled?

The content of your pages is analyzed by the GenAI to determine the Profile Cards to be assigned. When the content profiling starts, all fields matching the following conditions are serialized:

- Text-typed fields (Single-Line, Multi-Line, Rich Text) that are not Sitecore internal (names not starting with "__")

> [!TIP]
> To ensure the best profiling results, make sure to include meaningful content at least on the main fields of your pages (Eg: Title, Summary, Body, etc).
>
> Also make sure the content of your pages relates with the Profiles used for content profiling. For instance, content about **Sports** have a lower chance to be identified with the demo Profile **"Sitecore Public"** then content about **Technology** or **Marketing**.
