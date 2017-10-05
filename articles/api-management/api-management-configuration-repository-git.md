---
title: "使用 Git 設定 API 管理服務 - Azure | Microsoft Docs"
description: "了解如何使用 Git 儲存和設定 API 管理服務組態。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f5d6bb7ccbf15424e9940ccda2fac668a2af5a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-save-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="c7e40-103">如何使用 Git 儲存和設定 API 管理服務組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-103">How to save and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="c7e40-104">每個 API 管理服務執行個體會維護組態資料庫，包含服務執行個體的組態和中繼資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c7e40-104">Each API Management service instance maintains a configuration database that contains information about the configuration and metadata for the service instance.</span></span> <span data-ttu-id="c7e40-105">可以對服務執行個體進行變更，方法是使用PowerShell Cmdlet 或進行 REST API 呼叫，變更發佈者入口網站中的設定。</span><span class="sxs-lookup"><span data-stu-id="c7e40-105">Changes can be made to the service instance by changing a setting in the publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="c7e40-106">除了這些方法，您也可以使用 Git 管理服務執行個體組態，啟用下列服務管理案例︰</span><span class="sxs-lookup"><span data-stu-id="c7e40-106">In addition to these methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="c7e40-107">組態版本 - 下載並儲存不同版本的服務組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="c7e40-108">大量的組態變更 - 對本機儲存機制中服務組態的多個部分進行變更，並且使用單一作業將變更整合回伺服器</span><span class="sxs-lookup"><span data-stu-id="c7e40-108">Bulk configuration changes - make changes to multiple parts of your service configuration in your local repository and integrate the changes back to the server with a single operation</span></span>
* <span data-ttu-id="c7e40-109">熟悉的 Git 工具鏈和工作流程 - 使用您已熟悉的 Git 工具和工作流程</span><span class="sxs-lookup"><span data-stu-id="c7e40-109">Familiar Git toolchain and workflow - use the Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="c7e40-110">下圖顯示設定您的 API 管理服務執行個體的不同方式的概觀。</span><span class="sxs-lookup"><span data-stu-id="c7e40-110">The following diagram shows an overview of the different ways to configure your API Management service instance.</span></span>

![Git 設定][api-management-git-configure]

<span data-ttu-id="c7e40-112">當您使用發佈者入口網站、PowerShell Cmdlet 或 REST API 對服務進行變更時，您會使用 `https://{name}.management.azure-api.net` 端點管理服務組態資料庫，如圖表右側所示。</span><span class="sxs-lookup"><span data-stu-id="c7e40-112">When you make changes to your service using the publisher portal, PowerShell cmdlets, or the REST API, you are managing your service configuration database using the `https://{name}.management.azure-api.net` endpoint, as shown on the right side of the diagram.</span></span> <span data-ttu-id="c7e40-113">圖表左側說明如何針對位於 `https://{name}.scm.azure-api.net`的服務，使用 Git 和 Git 儲存機制管理服務組態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-113">The left side of the diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="c7e40-114">下列步驟提供使用 Git 管理 API 管理服務執行個體的概觀。</span><span class="sxs-lookup"><span data-stu-id="c7e40-114">The following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="c7e40-115">存取服務中的 Git 組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="c7e40-116">將您的服務組態資料庫儲存至您的 Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="c7e40-116">Save your service configuration database to your Git repository</span></span>
3. <span data-ttu-id="c7e40-117">將 Git 儲存機制複製到本機電腦</span><span class="sxs-lookup"><span data-stu-id="c7e40-117">Clone the Git repo to your local machine</span></span>
4. <span data-ttu-id="c7e40-118">將最新的儲存機制提取至您的本機電腦，認可並且將變更推送回您的儲存機制</span><span class="sxs-lookup"><span data-stu-id="c7e40-118">Pull the latest repo down to your local machine, and commit and push changes back to your repo</span></span>
5. <span data-ttu-id="c7e40-119">從您的儲存機制將變更部署至您的服務組態資料庫</span><span class="sxs-lookup"><span data-stu-id="c7e40-119">Deploy the changes from your repo into your service configuration database</span></span>

<span data-ttu-id="c7e40-120">本文說明如何啟用及使用 Git 來管理您的服務組態，並提供 Git 儲存機制中檔案和資料夾的參考。</span><span class="sxs-lookup"><span data-stu-id="c7e40-120">This article describes how to enable and use Git to manage your service configuration and provides a reference for the files and folders in the Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="c7e40-121">存取服務中的 Git 組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-121">Access Git configuration in your service</span></span>
<span data-ttu-id="c7e40-122">您可以檢視發行者入口網站右上角的 Git 圖示，藉以快速檢視 Git 組態的狀態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-122">You can quickly view the status of your Git configuration by viewing the Git icon in the upper-right corner of the publisher portal.</span></span> <span data-ttu-id="c7e40-123">在此範例中，狀態訊息指出存放庫有未儲存的變更。</span><span class="sxs-lookup"><span data-stu-id="c7e40-123">In this example, the status message indicates that there are unsaved changes to the repository.</span></span> <span data-ttu-id="c7e40-124">這是因為 API 管理服務組態資料庫尚未儲存到儲存機制所致。</span><span class="sxs-lookup"><span data-stu-id="c7e40-124">This is because the API Management service configuration database has not yet been saved to the repository.</span></span>

![Git 狀態][api-management-git-icon-enable]

<span data-ttu-id="c7e40-126">若要檢視並設定您的 Git 組態設定，您可以按一下 [Git] 圖示，或按一下 [安全性] 功能表，然後瀏覽至 [組態儲存機制] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c7e40-126">To view and configure your Git configuration settings, you can either click the Git icon, or click the **Security** menu and navigate to the **Configuration repository** tab.</span></span>

![啟用 GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="c7e40-128">未定義為屬性的任何密碼會儲存在儲存機制，並且仍然保留其歷程記錄，直到您停用然後重新啟用 Git 存取。</span><span class="sxs-lookup"><span data-stu-id="c7e40-128">Any secrets that are not defined as properties will be stored in the repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="c7e40-129">屬性會提供一個安全的地方以管理跨所有的 API 組態和原則的常數字串值，包括密碼，因此您不必將它們直接儲存在您的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="c7e40-129">Properties provide a secure place to manage constant string values, including secrets, across all API configuration and policies, so you don't have to store them directly in your policy statements.</span></span> <span data-ttu-id="c7e40-130">如需詳細資訊，請參閱 [如何使用 Azure API 管理原則中的屬性](api-management-howto-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-130">For more information, see [How to use properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="c7e40-131">如需使用 REST API 啟用或停用 Git 存取的詳細資訊，請參閱 [使用 REST API 啟用或停用 Git 存取](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-131">For information on enabling or disabling Git access using the REST API, see [Enable or disable Git access using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="to-save-the-service-configuration-to-the-git-repository"></a><span data-ttu-id="c7e40-132">將服務組態儲存至 Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="c7e40-132">To save the service configuration to the Git repository</span></span>
<span data-ttu-id="c7e40-133">複製儲存機制之前的第一個步驟是將服務組態的目前狀態儲存至儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7e40-133">The first step before cloning the repository is to save the current state of the service configuration to the repository.</span></span> <span data-ttu-id="c7e40-134">按一下 [將組態儲存至儲存機制] 。</span><span class="sxs-lookup"><span data-stu-id="c7e40-134">Click **Save configuration to repository**.</span></span>

![儲存組態][api-management-save-configuration]

<span data-ttu-id="c7e40-136">在 [確認] 畫面上進行任何所需的變更，然後按一下 [確定]  以儲存。</span><span class="sxs-lookup"><span data-stu-id="c7e40-136">Make any desired changes on the confirmation screen and click **Ok** to save.</span></span>

![儲存組態][api-management-save-configuration-confirm]

<span data-ttu-id="c7e40-138">儲存組態一段時間後，儲存機制的組態狀態隨即顯示，包括最後組態變更和上次同步處理服務組態和儲存機制的日期與時間。</span><span class="sxs-lookup"><span data-stu-id="c7e40-138">After a few moments the configuration is saved, and the configuration status of the repository is displayed, including the date and time of the last configuration change and the last synchronization between the service configuration and the repository.</span></span>

![組態狀態][api-management-configuration-status]

<span data-ttu-id="c7e40-140">一旦組態儲存至儲存機制，就可以複製。</span><span class="sxs-lookup"><span data-stu-id="c7e40-140">Once the configuration is saved to the repository, it can be cloned.</span></span>

<span data-ttu-id="c7e40-141">如需使用 REST API 執行此作業的詳細資訊，請參閱 [使用 REST API 認可組態快照集](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-141">For information on performing this operation using the REST API, see [Commit configuration snapshot using the REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="to-clone-the-repository-to-your-local-machine"></a><span data-ttu-id="c7e40-142">將儲存機制複製到本機電腦</span><span class="sxs-lookup"><span data-stu-id="c7e40-142">To clone the repository to your local machine</span></span>
<span data-ttu-id="c7e40-143">若要複製儲存機制，您需要儲存機制的 URL、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c7e40-143">To clone a repository, you need the URL to your repository, a user name, and a password.</span></span> <span data-ttu-id="c7e40-144">使用者名稱和 URL 會顯示於接近 [組態儲存機制]  索引標籤頂端的地方。</span><span class="sxs-lookup"><span data-stu-id="c7e40-144">The user name and URL are displayed near the top of the **Configuration repository** tab.</span></span>

![git 複製][api-management-configuration-git-clone]

<span data-ttu-id="c7e40-146">密碼會在 [組態儲存機制]  索引標籤的底端產生。</span><span class="sxs-lookup"><span data-stu-id="c7e40-146">The password is generated at the bottom of the **Configuration repository** tab.</span></span>

![產生密碼][api-management-generate-password]

<span data-ttu-id="c7e40-148">若要產生密碼，請先確定已將 [到期] 設為所需的到期日期和時間，然後按一下 [產生權杖]。</span><span class="sxs-lookup"><span data-stu-id="c7e40-148">To generate a password, first ensure that the **Expiry** is set to the desired expiration date and time, and then click **Generate Token**.</span></span>

![密碼][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="c7e40-150">記下此密碼。</span><span class="sxs-lookup"><span data-stu-id="c7e40-150">Make a note of this password.</span></span> <span data-ttu-id="c7e40-151">一旦您離開此頁面，就不會再次顯示密碼。</span><span class="sxs-lookup"><span data-stu-id="c7e40-151">Once you leave this page the password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="c7e40-152">下列範例會使用來自 [Git for Windows](http://www.git-scm.com/downloads) 的 Git Bash 工具，但是您可以使用任何您已熟悉的 Git 工具。</span><span class="sxs-lookup"><span data-stu-id="c7e40-152">The following examples use the Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="c7e40-153">在想要的資料夾中開啟 Git 工具，然後執行下列命令，使用發佈者入口網站提供的命令，將 git 儲存機制複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="c7e40-153">Open your Git tool in the desired folder and run the following command to clone the git repository to your local machine, using the command provided by the publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="c7e40-154">出現提示時，請提供使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="c7e40-154">Provide the user name and password when prompted.</span></span>

<span data-ttu-id="c7e40-155">如果您收到任何錯誤，請嘗試修改您的 `git clone` 命令以包含使用者名稱和密碼，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="c7e40-155">If you receive any errors, try modifying your `git clone` command to include the user name and password, as shown in the following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="c7e40-156">如果發生錯誤，請嘗試 URL 編碼命令的密碼部分。</span><span class="sxs-lookup"><span data-stu-id="c7e40-156">If this provides an error, try URL encoding the password portion of the command.</span></span> <span data-ttu-id="c7e40-157">完成這項操作的其中一個快速方法是開啟 Visual Studio，並且在 [即時運算視窗] 發出下列命令。</span><span class="sxs-lookup"><span data-stu-id="c7e40-157">One quick way to do this is to open Visual Studio, and issue the following command in the **Immediate Window**.</span></span> <span data-ttu-id="c7e40-158">若要開啟 [即時運算視窗]，請在 Visual Studio 中開啟任何解決方案或專案 (或建立新的空白主控台應用程式)，然後從 [偵錯] 功能表選擇 [視窗]、[即時運算]。</span><span class="sxs-lookup"><span data-stu-id="c7e40-158">To open the **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from the **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="c7e40-159">使用編碼的密碼以及使用者名稱和儲存機制位置以建構 git 命令。</span><span class="sxs-lookup"><span data-stu-id="c7e40-159">Use the encoded password along with your user name and repository location to construct the git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="c7e40-160">複製儲存機制之後，您可以在您的本機檔案系統中檢視及使用它。</span><span class="sxs-lookup"><span data-stu-id="c7e40-160">Once the repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="c7e40-161">如需詳細資訊，請參閱 [本機 Git 儲存機制的檔案和資料夾結構參考](#file-and-folder-structure-reference-of-local-git-repository)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="to-update-your-local-repository-with-the-most-current-service-instance-configuration"></a><span data-ttu-id="c7e40-162">使用最新的服務執行個體組態更新本機儲存機制</span><span class="sxs-lookup"><span data-stu-id="c7e40-162">To update your local repository with the most current service instance configuration</span></span>
<span data-ttu-id="c7e40-163">如果您在發佈者入口網站中或使用 REST API 變更您的 API 管理服務執行個體，您必須先將這些變更儲存至儲存機制，才能使用最新的變更來更新本機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7e40-163">If you make changes to your API Management service instance in the publisher portal or using the REST API, you must save these changes to the repository before you can update your local repository with the latest changes.</span></span> <span data-ttu-id="c7e40-164">若要這樣做，請按一下發佈者入口網站中 [組態儲存機制] 索引標籤上的 [將組態儲存至儲存機制]，然後在本機儲存機制中發出下列命令。</span><span class="sxs-lookup"><span data-stu-id="c7e40-164">To do this, click **Save configuration to repository** on the **Configuration repository** tab in the publisher portal, and then issue the following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="c7e40-165">在執行 `git pull` 之前，請確認您是位於本機儲存機制的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c7e40-165">Before running `git pull` ensure that you are in the folder for your local repository.</span></span> <span data-ttu-id="c7e40-166">如果您已完成 `git clone` 命令，則必須執行類似下列的命令，將目錄變更為您的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7e40-166">If you have just completed the `git clone` command, then you must change the directory to your repo by running a command like the following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="to-push-changes-from-your-local-repo-to-the-server-repo"></a><span data-ttu-id="c7e40-167">將變更從您的本機儲存機制推送至伺服器儲存機制</span><span class="sxs-lookup"><span data-stu-id="c7e40-167">To push changes from your local repo to the server repo</span></span>
<span data-ttu-id="c7e40-168">若要將變更從本機儲存機制推送至伺服器儲存機制，必須認可您的變更，然後再將其推送至伺服器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="c7e40-168">To push changes from your local repository to the server repository, you must commit your changes and then push them to the server repository.</span></span> <span data-ttu-id="c7e40-169">若要認可變更，請開啟您的 Git 命令工具，切換至您的本機儲存機制的目錄，然後發出下列命令。</span><span class="sxs-lookup"><span data-stu-id="c7e40-169">To commit your changes, open your Git command tool, switch to the directory of your local repository, and issue the following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="c7e40-170">若要將所有認可推送至伺服器，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="c7e40-170">To push all of the commits to the server, run the following command.</span></span>

```
git push
```

## <a name="to-deploy-any-service-configuration-changes-to-the-api-management-service-instance"></a><span data-ttu-id="c7e40-171">將服務組態變更部署至 API 管理服務執行個體</span><span class="sxs-lookup"><span data-stu-id="c7e40-171">To deploy any service configuration changes to the API Management service instance</span></span>
<span data-ttu-id="c7e40-172">一旦您的本機變更被認可並且推送至伺服器儲存機制，您可以將它們部署到您的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7e40-172">Once your local changes are committed and pushed to the server repository, you can deploy them to your API Management service instance.</span></span>

![部署][api-management-configuration-deploy]

<span data-ttu-id="c7e40-174">如需使用 REST API 執行此作業的詳細資訊，請參閱 [使用 REST API 將 Git 變更部署至組態資料庫](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-174">For information on performing this operation using the REST API, see [Deploy Git changes to configuration database using the REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="c7e40-175">本機 Git 儲存機制的檔案和資料夾結構參考</span><span class="sxs-lookup"><span data-stu-id="c7e40-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="c7e40-176">本機 git 儲存機制中的檔案和資料夾包含服務執行個體的相關組態資訊。</span><span class="sxs-lookup"><span data-stu-id="c7e40-176">The files and folders in the local git repository contain the configuration information about the service instance.</span></span>

| <span data-ttu-id="c7e40-177">項目</span><span class="sxs-lookup"><span data-stu-id="c7e40-177">Item</span></span> | <span data-ttu-id="c7e40-178">說明</span><span class="sxs-lookup"><span data-stu-id="c7e40-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c7e40-179">根 api 管理資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-179">root api-management folder</span></span> |<span data-ttu-id="c7e40-180">包含服務執行個體的最上層組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-180">Contains top-level configuration for the service instance</span></span> |
| <span data-ttu-id="c7e40-181">apis 資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-181">apis folder</span></span> |<span data-ttu-id="c7e40-182">包含服務執行個體中 apis 的組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-182">Contains the configuration for the apis in the service instance</span></span> |
| <span data-ttu-id="c7e40-183">群組資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-183">groups folder</span></span> |<span data-ttu-id="c7e40-184">包含服務執行個體中群組的組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-184">Contains the configuration for the groups in the service instance</span></span> |
| <span data-ttu-id="c7e40-185">原則資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-185">policies folder</span></span> |<span data-ttu-id="c7e40-186">包含服務執行個體中的原則</span><span class="sxs-lookup"><span data-stu-id="c7e40-186">Contains the policies in the service instance</span></span> |
| <span data-ttu-id="c7e40-187">portalStyles 資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-187">portalStyles folder</span></span> |<span data-ttu-id="c7e40-188">包含服務執行個體中開發人員入口網站自訂的組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-188">Contains the configuration for the developer portal customizations in the service instance</span></span> |
| <span data-ttu-id="c7e40-189">產品資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-189">products folder</span></span> |<span data-ttu-id="c7e40-190">包含服務執行個體中產品的組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-190">Contains the configuration for the products in the service instance</span></span> |
| <span data-ttu-id="c7e40-191">範本資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-191">templates folder</span></span> |<span data-ttu-id="c7e40-192">包含服務執行個體中電子郵件範本的組態</span><span class="sxs-lookup"><span data-stu-id="c7e40-192">Contains the configuration for the email templates in the service instance</span></span> |

<span data-ttu-id="c7e40-193">每個資料夾可以包含一或多個檔案，在某些情況下可以包含一或多個資料夾，例如每個 API、產品或群組的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7e40-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="c7e40-194">每個資料夾中的檔案是特定於資料夾名稱所描述的實體類型。</span><span class="sxs-lookup"><span data-stu-id="c7e40-194">The files within each folder are specific for the entity type described by the folder name.</span></span>

| <span data-ttu-id="c7e40-195">檔案類型</span><span class="sxs-lookup"><span data-stu-id="c7e40-195">File type</span></span> | <span data-ttu-id="c7e40-196">目的</span><span class="sxs-lookup"><span data-stu-id="c7e40-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="c7e40-197">json</span><span class="sxs-lookup"><span data-stu-id="c7e40-197">json</span></span> |<span data-ttu-id="c7e40-198">個別實體的組態資訊</span><span class="sxs-lookup"><span data-stu-id="c7e40-198">Configuration information about the respective entity</span></span> |
| <span data-ttu-id="c7e40-199">html</span><span class="sxs-lookup"><span data-stu-id="c7e40-199">html</span></span> |<span data-ttu-id="c7e40-200">實體的相關描述，通常顯示於開發人員入口網站</span><span class="sxs-lookup"><span data-stu-id="c7e40-200">Descriptions about the entity, often displayed in the developer portal</span></span> |
| <span data-ttu-id="c7e40-201">xml</span><span class="sxs-lookup"><span data-stu-id="c7e40-201">xml</span></span> |<span data-ttu-id="c7e40-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="c7e40-202">Policy statements</span></span> |
| <span data-ttu-id="c7e40-203">css</span><span class="sxs-lookup"><span data-stu-id="c7e40-203">css</span></span> |<span data-ttu-id="c7e40-204">開發人員入口網站自訂的樣式表</span><span class="sxs-lookup"><span data-stu-id="c7e40-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="c7e40-205">可以在您的本機檔案系統上建立、刪除、編輯和管理這些檔案，並將變更部署回您的 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="c7e40-205">These files can be created, deleted, edited, and managed on your local file system, and the changes deployed back to the your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e40-206">下列實體不包含在 Git 儲存機制，因此無法使用 Git 來設定。</span><span class="sxs-lookup"><span data-stu-id="c7e40-206">The following entities are not contained in the Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="c7e40-207">使用者</span><span class="sxs-lookup"><span data-stu-id="c7e40-207">Users</span></span>
> * <span data-ttu-id="c7e40-208">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c7e40-208">Subscriptions</span></span>
> * <span data-ttu-id="c7e40-209">屬性</span><span class="sxs-lookup"><span data-stu-id="c7e40-209">Properties</span></span>
> * <span data-ttu-id="c7e40-210">樣式以外的開發人員入口網站實體</span><span class="sxs-lookup"><span data-stu-id="c7e40-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="c7e40-211">根 api 管理資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-211">Root api-management folder</span></span>
<span data-ttu-id="c7e40-212">根 `api-management` 資料夾包含 `configuration.json` 檔案，其中包含服務執行個體的最上層資訊，格式如下。</span><span class="sxs-lookup"><span data-stu-id="c7e40-212">The root `api-management` folder contains a `configuration.json` file that contains top-level information about the service instance in the following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="c7e40-213">前四個設定 (`RegistrationEnabled`、`UserRegistrationTerms`、`UserRegistrationTermsEnabled` 和 `UserRegistrationTermsConsentRequired`) 對應至 [安全性] 區段的 [身分識別] 索引標籤中的下列設定。</span><span class="sxs-lookup"><span data-stu-id="c7e40-213">The first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map to the following settings on the **Identities** tab in the **Security** section.</span></span>

| <span data-ttu-id="c7e40-214">身分識別設定</span><span class="sxs-lookup"><span data-stu-id="c7e40-214">Identity setting</span></span> | <span data-ttu-id="c7e40-215">對應至</span><span class="sxs-lookup"><span data-stu-id="c7e40-215">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="c7e40-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="c7e40-216">RegistrationEnabled</span></span> |<span data-ttu-id="c7e40-217"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-217">**Redirect anonymous users to sign-in page** checkbox</span></span> |
| <span data-ttu-id="c7e40-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="c7e40-218">UserRegistrationTerms</span></span> |<span data-ttu-id="c7e40-219"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="c7e40-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="c7e40-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="c7e40-221"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="c7e40-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="c7e40-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="c7e40-223"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-223">**Require consent** checkbox</span></span> |

![身分識別設定][api-management-identity-settings]

<span data-ttu-id="c7e40-225">接下來四個設定 (`DelegationEnabled`、`DelegationUrl`、`DelegatedSubscriptionEnabled` 和 `DelegationValidationKey`) 對應至 [安全性] 區段的 [委派] 索引標籤中的下列設定。</span><span class="sxs-lookup"><span data-stu-id="c7e40-225">The next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map to the following settings on the **Delegation** tab in the **Security** section.</span></span>

| <span data-ttu-id="c7e40-226">委派設定</span><span class="sxs-lookup"><span data-stu-id="c7e40-226">Delegation setting</span></span> | <span data-ttu-id="c7e40-227">對應至</span><span class="sxs-lookup"><span data-stu-id="c7e40-227">Maps to</span></span> |
| --- | --- |
| <span data-ttu-id="c7e40-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="c7e40-228">DelegationEnabled</span></span> |<span data-ttu-id="c7e40-229">[委派登入和註冊] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="c7e40-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="c7e40-230">DelegationUrl</span></span> |<span data-ttu-id="c7e40-231"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="c7e40-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="c7e40-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="c7e40-233"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="c7e40-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="c7e40-234">DelegationValidationKey</span></span> |<span data-ttu-id="c7e40-235"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="c7e40-235">**Delegate Validation Key** textbox</span></span> |

![委派設定][api-management-delegation-settings]

<span data-ttu-id="c7e40-237">最後的設定 ( `$ref-policy`) 會對應至服務執行個體的全域原則陳述式檔案。</span><span class="sxs-lookup"><span data-stu-id="c7e40-237">The final setting, `$ref-policy`, maps to the global policy statements file for the service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="c7e40-238">apis 資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-238">apis folder</span></span>
<span data-ttu-id="c7e40-239">`apis` 資料夾包含服務執行個體中每個 API 的資料夾，其中包含下列項目。</span><span class="sxs-lookup"><span data-stu-id="c7e40-239">The `apis` folder contains a folder for each API in the service instance which contains the following items.</span></span>

* <span data-ttu-id="c7e40-240">`apis\<api name>\configuration.json` - 這是 API 的組態，而且包含後端服務 URL 和作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c7e40-240">`apis\<api name>\configuration.json` - this is the configuration for the API and contains information about the backend service URL and the operations.</span></span> <span data-ttu-id="c7e40-241">此資訊與當您以 `application/json` 格式的 `export=true` 呼叫[取得特定 API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) 時傳回的資訊相同。</span><span class="sxs-lookup"><span data-stu-id="c7e40-241">This is the same information that would be returned if you were to call [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="c7e40-242">`apis\<api name>\api.description.html` - 這是 API 的說明，並會對應至 [API 實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)的 `description` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c7e40-242">`apis\<api name>\api.description.html` - this is the description of the API and corresponds to the `description` property of the [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="c7e40-243">`apis\<api name>\operations\` - 此資料夾包含 `<operation name>.description.html` 檔案，該檔案對應至 API 中的作業。</span><span class="sxs-lookup"><span data-stu-id="c7e40-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map to the operations in the API.</span></span> <span data-ttu-id="c7e40-244">每個檔案包含 API 中單一作業的說明，其會對應至 REST API 中[作業實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties)的 `description` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c7e40-244">Each file contains the description of a single operation in the API which maps to the `description` property of the [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in the REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="c7e40-245">群組資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-245">groups folder</span></span>
<span data-ttu-id="c7e40-246">`groups` 資料夾包含服務執行個體中定義的每個群組的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7e40-246">The `groups` folder contains a folder for each group defined in the service instance.</span></span>

* <span data-ttu-id="c7e40-247">`groups\<group name>\configuration.json` - 這是群組的組態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-247">`groups\<group name>\configuration.json` - this is the configuration for the group.</span></span> <span data-ttu-id="c7e40-248">此資訊與當您呼叫 [取得特定群組](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) 作業時傳回的資訊相同。</span><span class="sxs-lookup"><span data-stu-id="c7e40-248">This is the same information that would be returned if you were to call the [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="c7e40-249">`groups\<group name>\description.html` - 這是群組的說明，並會對應至[群組實體](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)的 `description` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c7e40-249">`groups\<group name>\description.html` - this is the description of the group and corresponds to the `description` property of the [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="c7e40-250">原則資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-250">policies folder</span></span>
<span data-ttu-id="c7e40-251">`policies` 資料夾包含您的服務執行個體的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="c7e40-251">The `policies` folder contains the policy statements for your service instance.</span></span>

* <span data-ttu-id="c7e40-252">`policies\global.xml` - 包含在您服務執行個體的全域範圍中定義的原則。</span><span class="sxs-lookup"><span data-stu-id="c7e40-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="c7e40-253">`policies\apis\<api name>\` - 如果您在 API 範圍中定義了任何原則，它們就會包含在此資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c7e40-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="c7e40-254">`policies\apis\<api name>\<operation name>\` 資料夾 - 如果您有任何定義於作業範圍中的原則，它們就會包含在此資料夾的 `<operation name>.xml` 檔案中，其會對應至每個作業的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="c7e40-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map to the policy statements for each operation.</span></span>
* <span data-ttu-id="c7e40-255">`policies\products\` - 如果您有任何定義於產品範圍中的原則，它們就會包含在此資料夾中，其中包含 `<product name>.xml` 檔案，其會對應至每個產品的原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="c7e40-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map to the policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="c7e40-256">portalStyles 資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-256">portalStyles folder</span></span>
<span data-ttu-id="c7e40-257">`portalStyles` 資料夾包含適用於服務執行個體的開發人員入口網站自訂的組態和樣式表。</span><span class="sxs-lookup"><span data-stu-id="c7e40-257">The `portalStyles` folder contains configuration and style sheets for developer portal customizations for the service instance.</span></span>

* <span data-ttu-id="c7e40-258">`portalStyles\configuration.json` - 包含開發人員入口網站所使用的樣式表名稱</span><span class="sxs-lookup"><span data-stu-id="c7e40-258">`portalStyles\configuration.json` - contains the names of the style sheets used by the developer portal</span></span>
* <span data-ttu-id="c7e40-259">`portalStyles\<style name>.css` - 每個 `<style name>.css` 檔案包含開發人員入口網站的樣式 (預設為 `Preview.css` 和 `Production.css`)。</span><span class="sxs-lookup"><span data-stu-id="c7e40-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for the developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="c7e40-260">產品資料夾</span><span class="sxs-lookup"><span data-stu-id="c7e40-260">products folder</span></span>
<span data-ttu-id="c7e40-261">`products` 資料夾包含服務執行個體中定義的每個產品的資料夾。</span><span class="sxs-lookup"><span data-stu-id="c7e40-261">The `products` folder contains a folder for each product defined in the service instance.</span></span>

* <span data-ttu-id="c7e40-262">`products\<product name>\configuration.json` - 這是產品的組態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-262">`products\<product name>\configuration.json` - this is the configuration for the product.</span></span> <span data-ttu-id="c7e40-263">此資訊與當您呼叫 [取得特定產品](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) 作業時傳回的資訊相同。</span><span class="sxs-lookup"><span data-stu-id="c7e40-263">This is the same information that would be returned if you were to call the [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="c7e40-264">`products\<product name>\product.description.html` - 這是產品的說明，並會對應至 REST API 中[產品實體](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product)的 `description` 屬性。</span><span class="sxs-lookup"><span data-stu-id="c7e40-264">`products\<product name>\product.description.html` - this is the description of the product and corresponds to the `description` property of the [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in the REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="c7e40-265">範本</span><span class="sxs-lookup"><span data-stu-id="c7e40-265">templates</span></span>
<span data-ttu-id="c7e40-266">`templates` 資料夾包含服務執行個體的 [電子郵件範本](api-management-howto-configure-notifications.md) 的組態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-266">The `templates` folder contains configuration for the [email templates](api-management-howto-configure-notifications.md) of the service instance.</span></span>

* <span data-ttu-id="c7e40-267">`<template name>\configuration.json` - 這是電子郵件範本的組態。</span><span class="sxs-lookup"><span data-stu-id="c7e40-267">`<template name>\configuration.json` - this is the configuration for the email template.</span></span>
* <span data-ttu-id="c7e40-268">`<template name>\body.html` - 這是電子郵件範本的主體。</span><span class="sxs-lookup"><span data-stu-id="c7e40-268">`<template name>\body.html` - this is the body of the email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7e40-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7e40-269">Next steps</span></span>
<span data-ttu-id="c7e40-270">如需管理您的服務執行個體的其他方法的詳細資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="c7e40-270">For information on other ways to manage your service instance, see:</span></span>

* <span data-ttu-id="c7e40-271">使用下列 PowerShell Cmdlet 管理您的服務執行個體</span><span class="sxs-lookup"><span data-stu-id="c7e40-271">Manage your service instance using the following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="c7e40-272">服務部署 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="c7e40-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="c7e40-273">服務管理 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="c7e40-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="c7e40-274">在發佈者入口網站中管理您的服務執行個體</span><span class="sxs-lookup"><span data-stu-id="c7e40-274">Manage your service instance in the publisher portal</span></span>
  * [<span data-ttu-id="c7e40-275">管理第一個 API</span><span class="sxs-lookup"><span data-stu-id="c7e40-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="c7e40-276">使用 REST API 管理您的服務執行個體</span><span class="sxs-lookup"><span data-stu-id="c7e40-276">Manage your service instance using the REST API</span></span>
  * [<span data-ttu-id="c7e40-277">API 管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c7e40-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="c7e40-278">觀看影片概觀</span><span class="sxs-lookup"><span data-stu-id="c7e40-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




