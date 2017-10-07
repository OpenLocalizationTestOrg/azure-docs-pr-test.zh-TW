---
title: "aaaConfigure 使用 Git-Azure API 管理服務 |Microsoft 文件"
description: "深入了解如何 toosave 並設定您使用 Git 的 API 管理服務組態。"
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
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="da051-103">如何 toosave 並設定您使用 Git 的 API 管理服務設定</span><span class="sxs-lookup"><span data-stu-id="da051-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="da051-104">每個 API 管理服務執行個體維護組態資料庫，其中包含 hello 組態與 hello 服務執行個體的中繼資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="da051-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="da051-105">可以變更 toohello 服務執行個體變更 hello 發行者入口網站中的設定、 使用 PowerShell cmdlet 或 REST API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="da051-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="da051-106">此外 toothese 方法，您也可以管理您的服務執行個體設定使用 Git，請啟用服務管理案例，例如：</span><span class="sxs-lookup"><span data-stu-id="da051-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="da051-107">組態版本 - 下載並儲存不同版本的服務組態</span><span class="sxs-lookup"><span data-stu-id="da051-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="da051-108">大量的組態變更-在本機儲存機制中進行變更 toomultiple 組件的服務組態和整合 hello 變更後 toohello 與單一作業</span><span class="sxs-lookup"><span data-stu-id="da051-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="da051-109">熟悉 Git 工具鏈和工作流程-使用 hello Git 工具，以及您已熟悉的工作流程</span><span class="sxs-lookup"><span data-stu-id="da051-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="da051-110">hello 下列圖表顯示 hello 不同的方式 tooconfigure 概觀您 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="da051-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Git 設定][api-management-git-configure]

<span data-ttu-id="da051-112">當您使用 hello 發行者入口網站、 PowerShell cmdlet 或 REST API hello tooyour 服務進行變更時，您要管理服務設定資料庫使用 hello`https://{name}.management.azure-api.net`端點，右邊 hello hello 圖表所示。</span><span class="sxs-lookup"><span data-stu-id="da051-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="da051-113">hello 左下的方 hello 圖表將說明如何管理您使用 Git 的服務組態和您服務的 Git 儲存機制位於`https://{name}.scm.azure-api.net`。</span><span class="sxs-lookup"><span data-stu-id="da051-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="da051-114">hello 下列步驟提供管理 API 管理服務執行個體使用 Git 的概觀。</span><span class="sxs-lookup"><span data-stu-id="da051-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="da051-115">存取服務中的 Git 組態</span><span class="sxs-lookup"><span data-stu-id="da051-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="da051-116">儲存您服務組態資料庫 tooyour Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="da051-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="da051-117">複製 hello Git 儲存機制 tooyour 本機電腦</span><span class="sxs-lookup"><span data-stu-id="da051-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="da051-118">提取下 tooyour 本機 hello 最新的儲存機制和認可並推送變更後 tooyour 儲存機制</span><span class="sxs-lookup"><span data-stu-id="da051-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="da051-119">從您的儲存機制的 hello 變更部署至您的服務組態資料庫</span><span class="sxs-lookup"><span data-stu-id="da051-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="da051-120">本文說明如何 tooenable 和您的服務組態使用 Git toomanage hello Git 儲存機制中的 hello 檔案和資料夾提供的參考。</span><span class="sxs-lookup"><span data-stu-id="da051-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="da051-121">存取服務中的 Git 組態</span><span class="sxs-lookup"><span data-stu-id="da051-121">Access Git configuration in your service</span></span>
<span data-ttu-id="da051-122">您可以在 hello 右上角的 hello 發行者入口網站中檢視 hello Git 圖示，快速檢視 hello Git 組態狀態。</span><span class="sxs-lookup"><span data-stu-id="da051-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="da051-123">在此範例中，hello 狀態訊息會指出有未儲存的變更 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="da051-124">這是因為 hello API 管理服務組態資料庫有尚未儲存 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Git 狀態][api-management-git-icon-enable]

<span data-ttu-id="da051-126">tooview 和設定您的 Git 組態設定，您可以按一下 hello Git 圖示，或按一下 hello**安全性**功能表和瀏覽 toohello**設定存放庫** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da051-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![啟用 GIT][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="da051-128">屬性會儲存在 hello 儲存機制，並將保留在其歷程記錄，直到您未定義任何機密停用然後重新啟用 Git 權限。</span><span class="sxs-lookup"><span data-stu-id="da051-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="da051-129">屬性會提供安全的地方 toomanage 常數字串值，所以您不需 toostore，包括密碼，跨所有應用程式開發介面設定和原則，它們直接在您的原則陳述式中。</span><span class="sxs-lookup"><span data-stu-id="da051-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="da051-130">如需詳細資訊，請參閱[如何在 Azure API 管理原則中的 toouse 屬性](api-management-howto-properties.md)。</span><span class="sxs-lookup"><span data-stu-id="da051-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="da051-131">啟用或停用使用 hello REST API 的 Git 存取資訊，請參閱[啟用或停用使用 hello REST API 的 Git 存取](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit)。</span><span class="sxs-lookup"><span data-stu-id="da051-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="da051-132">toosave hello 服務組態 toohello Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="da051-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="da051-133">hello 複製 hello 儲存機制之前的第一個步驟是 toosave hello 目前狀態的 hello 服務組態 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="da051-134">按一下**儲存組態 toorepository**。</span><span class="sxs-lookup"><span data-stu-id="da051-134">Click **Save configuration toorepository**.</span></span>

![儲存組態][api-management-save-configuration]

<span data-ttu-id="da051-136">Hello 確認畫面上進行任何所需的變更，然後按一下 **確定**toosave。</span><span class="sxs-lookup"><span data-stu-id="da051-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![儲存組態][api-management-save-configuration-confirm]

<span data-ttu-id="da051-138">在幾分鐘之後會儲存 hello 組態，並且會顯示 hello 儲存機制 hello 組態狀態，包括 hello 日期和時間 hello 最後一項組態變更，而且 hello 之間 hello 服務組態和 hello 上次同步處理儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![組態狀態][api-management-configuration-status]

<span data-ttu-id="da051-140">一旦 toohello 儲存機制時，會儲存 hello 組態，可以被複製。</span><span class="sxs-lookup"><span data-stu-id="da051-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="da051-141">如需執行這項作業使用 hello REST API 的資訊，請參閱[認可組態快照集使用 REST API hello](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot)。</span><span class="sxs-lookup"><span data-stu-id="da051-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="da051-142">tooclone hello 儲存機制 tooyour 本機電腦</span><span class="sxs-lookup"><span data-stu-id="da051-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="da051-143">tooclone 儲存機制，您需要 hello URL tooyour 儲存機制、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="da051-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="da051-144">hello 使用者名稱和 URL 會顯示 hello hello 頂端附近**設定存放庫** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da051-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![git 複製][api-management-configuration-git-clone]

<span data-ttu-id="da051-146">在 hello hello 底端會產生 hello 密碼**設定存放庫** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da051-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![產生密碼][api-management-generate-password]

<span data-ttu-id="da051-148">toogenerate 密碼，必須先確定該 hello**到期**是設定 toohello 預期到期日和時間，然後按一下**產生語彙基元**。</span><span class="sxs-lookup"><span data-stu-id="da051-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![密碼][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="da051-150">記下此密碼。</span><span class="sxs-lookup"><span data-stu-id="da051-150">Make a note of this password.</span></span> <span data-ttu-id="da051-151">一旦您離開此頁面 hello 密碼不會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="da051-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="da051-152">下列範例使用 hello Git Bash hello 工具[Git for Windows](http://www.git-scm.com/downloads)但您可以使用任何您已熟悉的 Git 工具。</span><span class="sxs-lookup"><span data-stu-id="da051-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="da051-153">在 hello 所要的資料夾中開啟您的 Git 工具，並執行下列命令 tooclone hello git 儲存機制 tooyour 本機電腦，請使用 hello 命令 hello 發行者入口網站所提供的 hello。</span><span class="sxs-lookup"><span data-stu-id="da051-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da051-154">Hello 使用者名稱和密碼提示時提供。</span><span class="sxs-lookup"><span data-stu-id="da051-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="da051-155">如果您收到任何錯誤，請嘗試修改您`git clone`命令 tooinclude hello 使用者名稱和密碼，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="da051-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da051-156">如果這會提供錯誤，請再試一次 URL 編碼 hello 命令 hello 密碼部分。</span><span class="sxs-lookup"><span data-stu-id="da051-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="da051-157">一個快速方式 toodo 這是 tooopen Visual Studio 中，而且問題 hello 下列命令在 hello**即時運算視窗**。</span><span class="sxs-lookup"><span data-stu-id="da051-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="da051-158">tooopen hello**即時運算視窗**、 Visual Studio 中開啟任何方案或專案 （或建立新的空白的主控台應用程式），然後選擇  **Windows**，**即時運算**從hello**偵錯**功能表。</span><span class="sxs-lookup"><span data-stu-id="da051-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="da051-159">使用 hello 編碼密碼，以及使用者名稱和儲存機制位置 tooconstruct hello git 命令。</span><span class="sxs-lookup"><span data-stu-id="da051-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="da051-160">一旦複製 hello 儲存機制是您可以檢視，並在您的本機檔案系統中使用它。</span><span class="sxs-lookup"><span data-stu-id="da051-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="da051-161">如需詳細資訊，請參閱 [本機 Git 儲存機制的檔案和資料夾結構參考](#file-and-folder-structure-reference-of-local-git-repository)。</span><span class="sxs-lookup"><span data-stu-id="da051-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="da051-162">tooupdate 本機儲存機制與 hello 最新的服務執行個體組態</span><span class="sxs-lookup"><span data-stu-id="da051-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="da051-163">如果您在 hello 發行者入口網站或使用 hello REST API 中進行變更 tooyour API 管理服務執行個體，您必須先儲存這些變更 toohello 儲存機制之前您可以使用 hello 最新的變更來更新本機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="da051-164">toodo 此，依序按一下**儲存組態 toorepository**上 hello**設定存放庫**hello 發行者入口網站，在索引標籤，然後發出下列命令在本機儲存機制中的 hello。</span><span class="sxs-lookup"><span data-stu-id="da051-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="da051-165">執行前`git pull`確認您的本機儲存機制是 hello 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="da051-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="da051-166">如果您剛完成 hello`git clone`命令時，則您必須變更 hello 目錄 tooyour 儲存機制，藉由執行 hello 下列類似的命令。</span><span class="sxs-lookup"><span data-stu-id="da051-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="da051-167">從本機儲存機制 toohello 伺服器儲存機制的 toopush 變更</span><span class="sxs-lookup"><span data-stu-id="da051-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="da051-168">toopush 變更從本機儲存機制 toohello 伺服器儲存機制，您必須認可您的變更，然後將其推送 toohello 伺服器儲存機制。</span><span class="sxs-lookup"><span data-stu-id="da051-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="da051-169">toocommit 您的變更，開啟您的 Git 命令工具，本機儲存機制，與下列命令的問題 hello 的交換器 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="da051-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="da051-170">toopush hello 的所有認可 toohello 伺服器上執行下列命令 hello。</span><span class="sxs-lookup"><span data-stu-id="da051-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="da051-171">toodeploy 任何服務組態變更 toohello API 管理服務執行個體</span><span class="sxs-lookup"><span data-stu-id="da051-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="da051-172">一旦您的本機變更認可並推送 toohello 伺服器儲存機制，您可以將它們部署 tooyour API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="da051-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![部署][api-management-configuration-deploy]

<span data-ttu-id="da051-174">如需執行這項作業使用 hello REST API 的資訊，請參閱[部署 Git 變更 tooconfiguration 資料庫使用 REST API hello](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration)。</span><span class="sxs-lookup"><span data-stu-id="da051-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="da051-175">本機 Git 儲存機制的檔案和資料夾結構參考</span><span class="sxs-lookup"><span data-stu-id="da051-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="da051-176">hello hello 本機 git 儲存機制中檔案和資料夾包含 hello 關於 hello 服務執行個體的組態資訊。</span><span class="sxs-lookup"><span data-stu-id="da051-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="da051-177">Item</span><span class="sxs-lookup"><span data-stu-id="da051-177">Item</span></span> | <span data-ttu-id="da051-178">說明</span><span class="sxs-lookup"><span data-stu-id="da051-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da051-179">根 api 管理資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-179">root api-management folder</span></span> |<span data-ttu-id="da051-180">包含最上層 hello 服務執行個體組態</span><span class="sxs-lookup"><span data-stu-id="da051-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="da051-181">apis 資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-181">apis folder</span></span> |<span data-ttu-id="da051-182">包含 hello 服務執行個體中的 hello 應用程式開發介面的 hello 組態</span><span class="sxs-lookup"><span data-stu-id="da051-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="da051-183">群組資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-183">groups folder</span></span> |<span data-ttu-id="da051-184">Hello 服務執行個體中包含 hello hello 群組組態</span><span class="sxs-lookup"><span data-stu-id="da051-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="da051-185">原則資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-185">policies folder</span></span> |<span data-ttu-id="da051-186">Hello 服務執行個體中包含 hello 原則</span><span class="sxs-lookup"><span data-stu-id="da051-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="da051-187">portalStyles 資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-187">portalStyles folder</span></span> |<span data-ttu-id="da051-188">Hello 服務執行個體中包含 hello hello 開發人員入口網站的自訂項目組態</span><span class="sxs-lookup"><span data-stu-id="da051-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="da051-189">產品資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-189">products folder</span></span> |<span data-ttu-id="da051-190">Hello 服務執行個體中包含 hello hello 產品的組態</span><span class="sxs-lookup"><span data-stu-id="da051-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="da051-191">範本資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-191">templates folder</span></span> |<span data-ttu-id="da051-192">Hello 服務執行個體中包含 hello hello 電子郵件範本的組態</span><span class="sxs-lookup"><span data-stu-id="da051-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="da051-193">每個資料夾可以包含一或多個檔案，在某些情況下可以包含一或多個資料夾，例如每個 API、產品或群組的資料夾。</span><span class="sxs-lookup"><span data-stu-id="da051-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="da051-194">每個資料夾中的 hello 檔案特有的 hello hello 資料夾名稱所描述的實體類型。</span><span class="sxs-lookup"><span data-stu-id="da051-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="da051-195">檔案類型</span><span class="sxs-lookup"><span data-stu-id="da051-195">File type</span></span> | <span data-ttu-id="da051-196">目的</span><span class="sxs-lookup"><span data-stu-id="da051-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="da051-197">json</span><span class="sxs-lookup"><span data-stu-id="da051-197">json</span></span> |<span data-ttu-id="da051-198">Hello 個別實體的組態資訊</span><span class="sxs-lookup"><span data-stu-id="da051-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="da051-199">html</span><span class="sxs-lookup"><span data-stu-id="da051-199">html</span></span> |<span data-ttu-id="da051-200">通常顯示 hello 開發人員入口網站中的 hello 實體有關的說明。</span><span class="sxs-lookup"><span data-stu-id="da051-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="da051-201">xml</span><span class="sxs-lookup"><span data-stu-id="da051-201">xml</span></span> |<span data-ttu-id="da051-202">Policy statements</span><span class="sxs-lookup"><span data-stu-id="da051-202">Policy statements</span></span> |
| <span data-ttu-id="da051-203">css</span><span class="sxs-lookup"><span data-stu-id="da051-203">css</span></span> |<span data-ttu-id="da051-204">開發人員入口網站自訂的樣式表</span><span class="sxs-lookup"><span data-stu-id="da051-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="da051-205">這些檔案可以建立、 刪除、 編輯和管理您的本機檔案系統和 hello 變更部署後 toohello 您 API 管理服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="da051-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="da051-206">hello 下列實體不會包含在 hello Git 儲存機制中，無法使用 Git 進行設定。</span><span class="sxs-lookup"><span data-stu-id="da051-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="da051-207">使用者</span><span class="sxs-lookup"><span data-stu-id="da051-207">Users</span></span>
> * <span data-ttu-id="da051-208">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da051-208">Subscriptions</span></span>
> * <span data-ttu-id="da051-209">屬性</span><span class="sxs-lookup"><span data-stu-id="da051-209">Properties</span></span>
> * <span data-ttu-id="da051-210">樣式以外的開發人員入口網站實體</span><span class="sxs-lookup"><span data-stu-id="da051-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="da051-211">根 api 管理資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-211">Root api-management folder</span></span>
<span data-ttu-id="da051-212">hello 根`api-management`資料夾包含`configuration.json`檔案，其中包含最上層 hello hello 遵循格式中的服務執行個體的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="da051-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

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

<span data-ttu-id="da051-213">hello 前四個設定 (`RegistrationEnabled`， `UserRegistrationTerms`， `UserRegistrationTermsEnabled`，和`UserRegistrationTermsConsentRequired`) 對應 toohello 遵循 hello 設定**識別** 索引標籤中 hello**安全性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="da051-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="da051-214">身分識別設定</span><span class="sxs-lookup"><span data-stu-id="da051-214">Identity setting</span></span> | <span data-ttu-id="da051-215">太對應</span><span class="sxs-lookup"><span data-stu-id="da051-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="da051-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="da051-216">RegistrationEnabled</span></span> |<span data-ttu-id="da051-217">**匿名使用者 toosign 頁面上將重新導向**核取方塊</span><span class="sxs-lookup"><span data-stu-id="da051-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="da051-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="da051-218">UserRegistrationTerms</span></span> |<span data-ttu-id="da051-219"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="da051-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="da051-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="da051-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="da051-221"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="da051-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="da051-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="da051-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="da051-223"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="da051-223">**Require consent** checkbox</span></span> |

![身分識別設定][api-management-identity-settings]

<span data-ttu-id="da051-225">hello 接下來四個設定 (`DelegationEnabled`， `DelegationUrl`， `DelegatedSubscriptionEnabled`，和`DelegationValidationKey`) 對應 toohello 遵循 hello 設定**委派** 索引標籤中 hello**安全性**> 一節。</span><span class="sxs-lookup"><span data-stu-id="da051-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="da051-226">委派設定</span><span class="sxs-lookup"><span data-stu-id="da051-226">Delegation setting</span></span> | <span data-ttu-id="da051-227">太對應</span><span class="sxs-lookup"><span data-stu-id="da051-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="da051-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="da051-228">DelegationEnabled</span></span> |<span data-ttu-id="da051-229">[委派登入和註冊] 核取方塊</span><span class="sxs-lookup"><span data-stu-id="da051-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="da051-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="da051-230">DelegationUrl</span></span> |<span data-ttu-id="da051-231"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="da051-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="da051-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="da051-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="da051-233"> 核取方塊</span><span class="sxs-lookup"><span data-stu-id="da051-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="da051-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="da051-234">DelegationValidationKey</span></span> |<span data-ttu-id="da051-235"> 文字方塊</span><span class="sxs-lookup"><span data-stu-id="da051-235">**Delegate Validation Key** textbox</span></span> |

![委派設定][api-management-delegation-settings]

<span data-ttu-id="da051-237">hello 最終設定， `$ref-policy`，對應 toohello hello 服務執行個體的全域原則陳述式檔案。</span><span class="sxs-lookup"><span data-stu-id="da051-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="da051-238">apis 資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-238">apis folder</span></span>
<span data-ttu-id="da051-239">hello`apis`資料夾的每個應用程式開發介面包含一個資料夾，其中包含下列項目 hello hello 服務執行個體中。</span><span class="sxs-lookup"><span data-stu-id="da051-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="da051-240">`apis\<api name>\configuration.json`-這是 hello API 的 hello 組態，而且包含 hello 後端服務 URL 和 hello 作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="da051-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="da051-241">這是 hello 相同的資訊將會傳回，如果您 toocall[取得特定 API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI)與`export=true`中`application/json`格式。</span><span class="sxs-lookup"><span data-stu-id="da051-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="da051-242">`apis\<api name>\api.description.html`-這是 hello hello API 描述和對應 toohello`description`屬性 hello [API 實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties)。</span><span class="sxs-lookup"><span data-stu-id="da051-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="da051-243">`apis\<api name>\operations\`-此資料夾包含`<operation name>.description.html`toohello 作業 hello API 中的對應的檔案。</span><span class="sxs-lookup"><span data-stu-id="da051-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="da051-244">每個檔案包含單一作業中 hello API，其對應 toohello hello 描述`description`屬性 hello[作業實體](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties)hello REST API 中。</span><span class="sxs-lookup"><span data-stu-id="da051-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="da051-245">群組資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-245">groups folder</span></span>
<span data-ttu-id="da051-246">hello`groups`資料夾包含 hello 服務執行個體中定義的每個群組的資料夾。</span><span class="sxs-lookup"><span data-stu-id="da051-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="da051-247">`groups\<group name>\configuration.json`-這是 hello hello 群組組態。</span><span class="sxs-lookup"><span data-stu-id="da051-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="da051-248">這是 hello 相同的資訊將會傳回，如果您 toocall hello[取得特定群組](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup)作業。</span><span class="sxs-lookup"><span data-stu-id="da051-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="da051-249">`groups\<group name>\description.html`-這是 hello hello 群組描述和對應 toohello`description`屬性 hello[群組實體](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties)。</span><span class="sxs-lookup"><span data-stu-id="da051-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="da051-250">原則資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-250">policies folder</span></span>
<span data-ttu-id="da051-251">hello`policies`資料夾包含您的服務執行個體的 hello 原則陳述式。</span><span class="sxs-lookup"><span data-stu-id="da051-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="da051-252">`policies\global.xml` - 包含在您服務執行個體的全域範圍中定義的原則。</span><span class="sxs-lookup"><span data-stu-id="da051-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="da051-253">`policies\apis\<api name>\` - 如果您在 API 範圍中定義了任何原則，它們就會包含在此資料夾中。</span><span class="sxs-lookup"><span data-stu-id="da051-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="da051-254">`policies\apis\<api name>\<operation name>\`資料夾-如果您有在作業範圍內定義的任何原則，它們包含在這個資料夾中`<operation name>.xml`對應 toohello 原則陳述式，每個作業的檔案。</span><span class="sxs-lookup"><span data-stu-id="da051-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="da051-255">`policies\products\`-如果您有任何定義於產品範圍的原則，它們包含在這個資料夾中，其中包含`<product name>.xml`對應 toohello 每項產品的原則陳述式的檔案。</span><span class="sxs-lookup"><span data-stu-id="da051-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="da051-256">portalStyles 資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-256">portalStyles folder</span></span>
<span data-ttu-id="da051-257">hello`portalStyles`資料夾包含用於開發人員入口網站的自訂 hello 服務執行個體的組態與樣式表。</span><span class="sxs-lookup"><span data-stu-id="da051-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="da051-258">`portalStyles\configuration.json`-包含 hello hello hello 開發人員入口網站所使用的樣式表名稱</span><span class="sxs-lookup"><span data-stu-id="da051-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="da051-259">`portalStyles\<style name>.css`-每個`<style name>.css`檔案包含樣式 hello 開發人員入口網站 (`Preview.css`和`Production.css`依預設)。</span><span class="sxs-lookup"><span data-stu-id="da051-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="da051-260">產品資料夾</span><span class="sxs-lookup"><span data-stu-id="da051-260">products folder</span></span>
<span data-ttu-id="da051-261">hello`products`資料夾都包含資料夾，以定義 hello 服務執行個體中每個產品。</span><span class="sxs-lookup"><span data-stu-id="da051-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="da051-262">`products\<product name>\configuration.json`-這是 hello hello 之產品的組態。</span><span class="sxs-lookup"><span data-stu-id="da051-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="da051-263">這是 hello 相同的資訊將會傳回，如果您 toocall hello[取得特定產品](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct)作業。</span><span class="sxs-lookup"><span data-stu-id="da051-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="da051-264">`products\<product name>\product.description.html`-這是 hello hello 產品描述及對應 toohello`description`屬性 hello [product 實體](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product)hello REST API 中。</span><span class="sxs-lookup"><span data-stu-id="da051-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="da051-265">範本</span><span class="sxs-lookup"><span data-stu-id="da051-265">templates</span></span>
<span data-ttu-id="da051-266">hello`templates`資料夾包含組態的 hello[電子郵件範本](api-management-howto-configure-notifications.md)hello 服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="da051-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="da051-267">`<template name>\configuration.json`-這是 hello hello 電子郵件範本的設定。</span><span class="sxs-lookup"><span data-stu-id="da051-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="da051-268">`<template name>\body.html`-這是 hello 主體 hello 電子郵件範本。</span><span class="sxs-lookup"><span data-stu-id="da051-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da051-269">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da051-269">Next steps</span></span>
<span data-ttu-id="da051-270">如需其他方式 toomanage 您服務執行個體，請參閱：</span><span class="sxs-lookup"><span data-stu-id="da051-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="da051-271">管理服務執行個體使用下列 PowerShell 指令程式的 hello</span><span class="sxs-lookup"><span data-stu-id="da051-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="da051-272">服務部署 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="da051-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="da051-273">服務管理 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="da051-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="da051-274">管理您的服務執行個體在 hello 發行者入口網站</span><span class="sxs-lookup"><span data-stu-id="da051-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="da051-275">管理第一個 API</span><span class="sxs-lookup"><span data-stu-id="da051-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="da051-276">管理服務執行個體使用 hello REST API</span><span class="sxs-lookup"><span data-stu-id="da051-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="da051-277">API 管理 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="da051-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="da051-278">觀看影片概觀</span><span class="sxs-lookup"><span data-stu-id="da051-278">Watch a video overview</span></span>
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




