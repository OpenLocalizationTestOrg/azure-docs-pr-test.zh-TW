---
title: "Azure Functions 的持續部署 | Microsoft Docs"
description: "使用 Azure App Service 的持續部署工具來發佈 Azure Functions。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="57e97-103">Azure Functions 的持續部署</span><span class="sxs-lookup"><span data-stu-id="57e97-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="57e97-104">Azure Functions 可讓您使用 App Service 持續整合來輕鬆部署您的函數應用程式。</span><span class="sxs-lookup"><span data-stu-id="57e97-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="57e97-105">Functions 可與 BitBucket、Dropbox、GitHub 及 Visual Studio Team Services (VSTS) 整合。</span><span class="sxs-lookup"><span data-stu-id="57e97-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="57e97-106">這可讓使用這其中一項整合式服務進行函數程式碼更新的工作流程觸發以 Azure 為目的地的部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="57e97-107">如果您不熟悉 Azure Functions，請從 [Azure Functions 概觀](functions-overview.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="57e97-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="57e97-108">持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。</span><span class="sxs-lookup"><span data-stu-id="57e97-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="57e97-109">它也可讓您維護函式程式碼的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="57e97-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="57e97-110">目前支援的部署來源如下：</span><span class="sxs-lookup"><span data-stu-id="57e97-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="57e97-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="57e97-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="57e97-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="57e97-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="57e97-113">外部存放庫 (Git 或 Mercurial)</span><span class="sxs-lookup"><span data-stu-id="57e97-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="57e97-114">Git 本機存放庫</span><span class="sxs-lookup"><span data-stu-id="57e97-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="57e97-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="57e97-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="57e97-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="57e97-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="57e97-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="57e97-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="57e97-118">設定部署時，是依每一函數應用程式進行設定。</span><span class="sxs-lookup"><span data-stu-id="57e97-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="57e97-119">當持續部署啟用後，在入口網站中對函式程式碼的存取權會設定為「唯讀」 。</span><span class="sxs-lookup"><span data-stu-id="57e97-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="57e97-120">持續部署需求</span><span class="sxs-lookup"><span data-stu-id="57e97-120">Continuous deployment requirements</span></span>

<span data-ttu-id="57e97-121">您必須先設定部署來源，並將函數程式碼放入部署來源中，才能設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="57e97-122">在指定的函數應用程式部署中，每個函式會存在於具名子目錄中，而其目錄名稱則為函式的名稱。</span><span class="sxs-lookup"><span data-stu-id="57e97-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="57e97-123">設定連續部署</span><span class="sxs-lookup"><span data-stu-id="57e97-123">Set up continuous deployment</span></span>
<span data-ttu-id="57e97-124">您可以使用此程序來為現有的函數應用程式設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="57e97-125">這些步驟會示範與 GitHub 存放庫的整合，但類似的步驟也適用於 Visual Studio Team Services 或其他部署服務。</span><span class="sxs-lookup"><span data-stu-id="57e97-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="57e97-126">在 [Azure 入口網站](https://portal.azure.com)中您的函數應用程式中，按一下 [平台功能] 和 [部署選項]。</span><span class="sxs-lookup"><span data-stu-id="57e97-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="57e97-128">然後，在 [部署] 刀鋒視窗中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="57e97-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="57e97-130">在 [部署來源] 刀鋒視窗中，按一下 [選擇來源]、填入所選部署來源的資訊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="57e97-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![選擇部署來源](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="57e97-132">設定完持續部署之後，部署來源中的所有檔案變更都會複製到函數應用程式，並觸發完整的網站部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="57e97-133">當來源中的檔案更新時，便會重新部署網站。</span><span class="sxs-lookup"><span data-stu-id="57e97-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="57e97-134">部署選項</span><span class="sxs-lookup"><span data-stu-id="57e97-134">Deployment options</span></span>

<span data-ttu-id="57e97-135">以下是一些典型的部署案例︰</span><span class="sxs-lookup"><span data-stu-id="57e97-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="57e97-136">建立預備部署</span><span class="sxs-lookup"><span data-stu-id="57e97-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="57e97-137">將現有函式移至持續部署</span><span class="sxs-lookup"><span data-stu-id="57e97-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="57e97-138">建立預備部署</span><span class="sxs-lookup"><span data-stu-id="57e97-138">Create a staging deployment</span></span>

<span data-ttu-id="57e97-139">函式應用程式尚未支援部署位置。</span><span class="sxs-lookup"><span data-stu-id="57e97-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="57e97-140">不過，您仍可使用持續整合來管理個別的預備部署和生產部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="57e97-141">設定及使用預備部署的程序通常應該會像下面這樣︰</span><span class="sxs-lookup"><span data-stu-id="57e97-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="57e97-142">在訂用帳戶中建立兩個函式應用程式，一個用於生產程式碼，一個用於預備。</span><span class="sxs-lookup"><span data-stu-id="57e97-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="57e97-143">建立部署來源 (如果還未擁有)。</span><span class="sxs-lookup"><span data-stu-id="57e97-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="57e97-144">此範例使用 [GitHub]。</span><span class="sxs-lookup"><span data-stu-id="57e97-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="57e97-145">針對生產函數應用程式，完成上述在**設定持續部署**中的步驟，並將部署分支設定為 GitHub 存放庫的主要分支。</span><span class="sxs-lookup"><span data-stu-id="57e97-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![選擇部署分支](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="57e97-147">針對預備函數應用程式重複此步驟，但改為在 GitHub 存放庫中選擇預備分支。</span><span class="sxs-lookup"><span data-stu-id="57e97-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="57e97-148">如果部署來源不支援分支功能，請使用不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="57e97-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="57e97-149">對預備分支或資料夾中的程式碼進行更新，然後確認預備部署中已反映這些變更。</span><span class="sxs-lookup"><span data-stu-id="57e97-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="57e97-150">經過測試之後，將預備分支的變更合併到主要分支。</span><span class="sxs-lookup"><span data-stu-id="57e97-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="57e97-151">這項合併會觸發以函數應用程式為目的地的部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="57e97-152">如果部署來源不支援分支，請以預備資料夾中的檔案覆寫生產資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="57e97-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="57e97-153">將現有函式移至持續部署</span><span class="sxs-lookup"><span data-stu-id="57e97-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="57e97-154">當您擁有在入口網站中建立並維護的現有函式時，您必須先使用 FTP 或本機 Git 存放庫下載現有的函式程式碼檔案，才能如上所述設定持續部署。</span><span class="sxs-lookup"><span data-stu-id="57e97-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="57e97-155">您可以在函式應用程式的 App Service 設定中進行此操作。</span><span class="sxs-lookup"><span data-stu-id="57e97-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="57e97-156">下載了檔案之後，可以將其上傳至所選的持續部署來源。</span><span class="sxs-lookup"><span data-stu-id="57e97-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="57e97-157">在設定持續整合之後，您就再也無法於 Functions 入口網站編輯原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="57e97-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="57e97-158">作法：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="57e97-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="57e97-159">作法︰使用 FTP 下載檔案</span><span class="sxs-lookup"><span data-stu-id="57e97-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="57e97-160">操作說明︰使用本機 Git 存放庫來下載檔案</span><span class="sxs-lookup"><span data-stu-id="57e97-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="57e97-161">作法：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="57e97-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="57e97-162">在使用 FTP 或 本機 Git 存放庫從函數應用程式下載檔案之前，您必須先設定認證以存取網站。</span><span class="sxs-lookup"><span data-stu-id="57e97-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="57e97-163">認證是在函式應用程式層級進行設定。</span><span class="sxs-lookup"><span data-stu-id="57e97-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="57e97-164">請使用下列步驟，在 Azure 入口網站中設定部署認證：</span><span class="sxs-lookup"><span data-stu-id="57e97-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="57e97-165">在 [Azure 入口網站](https://portal.azure.com)中您的函數應用程式中，按一下 [平台功能] 和 [部署認證]。</span><span class="sxs-lookup"><span data-stu-id="57e97-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![設定本機部署認證](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="57e97-167">輸入使用者名稱和密碼，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57e97-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="57e97-168">您現在可以使用這些認證從 FTP 或內建的 Git 儲存機制存取函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="57e97-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="57e97-169">作法︰使用 FTP 下載檔案</span><span class="sxs-lookup"><span data-stu-id="57e97-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="57e97-170">在 [Azure 入口網站](https://portal.azure.com)中您的函數應用程式中，按一下 [平台功能] 和 [屬性]，然後複製 [FTP/部署使用者]、[FTP 主機名稱] 及 [FTPS 主機名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="57e97-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="57e97-171">[FTP/部署使用者] 中必須輸入入口網站中所顯示的值 (包括應用程式名稱)，以針對 FTP 伺服器提供適當的內容。</span><span class="sxs-lookup"><span data-stu-id="57e97-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![取得部署資訊](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="57e97-173">從您的 FTP 用戶端，使用您所蒐集的連接資訊連接到您的應用程式，並下載函式的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="57e97-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="57e97-174">操作說明：使用本機 Git 存放庫來下載檔案</span><span class="sxs-lookup"><span data-stu-id="57e97-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="57e97-175">在 [Azure 入口網站](https://portal.azure.com)中您的函數應用程式中，按一下 [平台功能] 和 [部署選項]。</span><span class="sxs-lookup"><span data-stu-id="57e97-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="57e97-177">然後，在 [部署] 刀鋒視窗中，按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="57e97-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="57e97-179">在 [部署來源] 刀鋒視窗中，按一下 [本機 Git 存放庫]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="57e97-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="57e97-180">在 [平台功能] 中，按一下 [屬性]，然後記下 Git URL 的值。</span><span class="sxs-lookup"><span data-stu-id="57e97-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="57e97-182">使用 Git 感知命令列提示字元或您慣用的 Git 工具，來複製本機電腦上的存放庫。</span><span class="sxs-lookup"><span data-stu-id="57e97-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="57e97-183">Git 複製命令看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="57e97-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="57e97-184">將函式應用程式的檔案擷取到本機電腦上的複製，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="57e97-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="57e97-185">如果系統要求，請提供[已設定的部署認證](#credentials)。</span><span class="sxs-lookup"><span data-stu-id="57e97-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="57e97-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="57e97-186">[GitHub]: https://github.com/</span></span>
