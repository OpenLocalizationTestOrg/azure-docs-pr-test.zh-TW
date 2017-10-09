---
title: "Azure 函式的 aaaContinuous 部署 |Microsoft 文件"
description: "使用 Azure App Service toopublish 持續部署功能 Azure 函式。"
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
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="704b7-103">Azure Functions 的持續部署</span><span class="sxs-lookup"><span data-stu-id="704b7-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="704b7-104">Azure 函式可讓您輕鬆 toodeploy 函式應用程式使用應用程式服務的持續整合。</span><span class="sxs-lookup"><span data-stu-id="704b7-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="704b7-105">Functions 可與 BitBucket、Dropbox、GitHub 及 Visual Studio Team Services (VSTS) 整合。</span><span class="sxs-lookup"><span data-stu-id="704b7-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="704b7-106">這可讓使用這些整合式的服務，觸發程序部署 tooAzure 的其中一個所做的工作流程更新函式程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="704b7-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="704b7-107">如果您是新 tooAzure 函式，以啟動[Azure 函式概觀](functions-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="704b7-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="704b7-108">持續部署對於整合了多個經常參與的專案而言是一個絕佳選項。</span><span class="sxs-lookup"><span data-stu-id="704b7-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="704b7-109">它也可讓您維護函式程式碼的原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="704b7-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="704b7-110">目前支援下列部署來源 hello:</span><span class="sxs-lookup"><span data-stu-id="704b7-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="704b7-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="704b7-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="704b7-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="704b7-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="704b7-113">外部存放庫 (Git 或 Mercurial)</span><span class="sxs-lookup"><span data-stu-id="704b7-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="704b7-114">Git 本機存放庫</span><span class="sxs-lookup"><span data-stu-id="704b7-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="704b7-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="704b7-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="704b7-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="704b7-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="704b7-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="704b7-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="704b7-118">設定部署時，是依每一函數應用程式進行設定。</span><span class="sxs-lookup"><span data-stu-id="704b7-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="704b7-119">啟用連續部署之後，存取 toofunction 碼 hello 入口網站中的設定得*唯讀*。</span><span class="sxs-lookup"><span data-stu-id="704b7-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="704b7-120">持續部署需求</span><span class="sxs-lookup"><span data-stu-id="704b7-120">Continuous deployment requirements</span></span>

<span data-ttu-id="704b7-121">您必須在您設定的部署來源與函式程式碼 hello 部署來源，才能設定連續部署。</span><span class="sxs-lookup"><span data-stu-id="704b7-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="704b7-122">在指定的函式應用程式部署中，每個函式位於命名的子目錄，其中 hello 目錄名稱是 hello hello 函式名稱。</span><span class="sxs-lookup"><span data-stu-id="704b7-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="704b7-123">設定連續部署</span><span class="sxs-lookup"><span data-stu-id="704b7-123">Set up continuous deployment</span></span>
<span data-ttu-id="704b7-124">使用此程序 tooconfigure 連續部署現有的函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="704b7-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="704b7-125">這些步驟會示範與 GitHub 存放庫的整合，但類似的步驟也適用於 Visual Studio Team Services 或其他部署服務。</span><span class="sxs-lookup"><span data-stu-id="704b7-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="704b7-126">您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署選項**。</span><span class="sxs-lookup"><span data-stu-id="704b7-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="704b7-128">接著在 hello**部署**刀鋒視窗中按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="704b7-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="704b7-130">在 hello**部署來源**刀鋒視窗中，按一下**選擇來源**，然後填入您所選擇的部署來源 hello 資訊，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="704b7-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![選擇部署來源](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="704b7-132">設定連續部署之後，您的部署來源中的所有檔案變更都會複製的 toohello 函式應用程式，而且會觸發完整站台部署。</span><span class="sxs-lookup"><span data-stu-id="704b7-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="704b7-133">hello 來源中的檔案更新時，會重新部署 hello 站台。</span><span class="sxs-lookup"><span data-stu-id="704b7-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="704b7-134">部署選項</span><span class="sxs-lookup"><span data-stu-id="704b7-134">Deployment options</span></span>

<span data-ttu-id="704b7-135">hello 以下是一些典型部署案例：</span><span class="sxs-lookup"><span data-stu-id="704b7-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="704b7-136">建立預備部署</span><span class="sxs-lookup"><span data-stu-id="704b7-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="704b7-137">移動現有的函式 toocontinuous 部署</span><span class="sxs-lookup"><span data-stu-id="704b7-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="704b7-138">建立預備部署</span><span class="sxs-lookup"><span data-stu-id="704b7-138">Create a staging deployment</span></span>

<span data-ttu-id="704b7-139">函式應用程式尚未支援部署位置。</span><span class="sxs-lookup"><span data-stu-id="704b7-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="704b7-140">不過，您仍可使用持續整合來管理個別的預備部署和生產部署。</span><span class="sxs-lookup"><span data-stu-id="704b7-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="704b7-141">hello tooconfigure 程序，並使用預備環境部署通常看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="704b7-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="704b7-142">建立兩個函式應用程式在您的訂閱 hello 實際執行程式碼，一個供暫存。</span><span class="sxs-lookup"><span data-stu-id="704b7-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="704b7-143">建立部署來源 (如果還未擁有)。</span><span class="sxs-lookup"><span data-stu-id="704b7-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="704b7-144">此範例使用 [GitHub]。</span><span class="sxs-lookup"><span data-stu-id="704b7-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="704b7-145">您實際執行的函式應用程式中的步驟完成前述的 hello**設定連續部署**組 hello 部署分支 toohello 主要分支您的 GitHub 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="704b7-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![選擇部署分支](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="704b7-147">針對 hello 暫存函式應用程式時，重複此步驟，但是選擇暫存分支改為在您的 GitHub 儲存機制中的 hello。</span><span class="sxs-lookup"><span data-stu-id="704b7-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="704b7-148">如果部署來源不支援分支功能，請使用不同的資料夾。</span><span class="sxs-lookup"><span data-stu-id="704b7-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="704b7-149">請更新 tooyour 程式碼中 hello 暫存分支或資料夾，然後確認這些變更會反映在預備環境部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="704b7-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="704b7-150">測試之後，合併變更 hello 臨時分支到 hello 主要分支。</span><span class="sxs-lookup"><span data-stu-id="704b7-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="704b7-151">此合併觸發程序部署 toohello 生產函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="704b7-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="704b7-152">如果您部署的來源不支援分支，檔案覆寫 hello 生產資料夾中的 hello 檔案 hello 從 hello 暫存資料夾。</span><span class="sxs-lookup"><span data-stu-id="704b7-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="704b7-153">移動現有的函式 toocontinuous 部署</span><span class="sxs-lookup"><span data-stu-id="704b7-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="704b7-154">當您有現有的函式，您已建立並維護在 hello 入口網站，您需要 toodownload 現有函式 （如上所述），才能設定連續部署使用 FTP 或 hello 本機 Git 儲存機制的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="704b7-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="704b7-155">您可以在 hello 應用程式服務設定為函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="704b7-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="704b7-156">下載檔案之後，您可以上傳它們 tooyour 選擇連續部署來源。</span><span class="sxs-lookup"><span data-stu-id="704b7-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="704b7-157">設定持續整合之後，您將不再能夠 tooedit hello 函式的入口網站中的程式來源檔案。</span><span class="sxs-lookup"><span data-stu-id="704b7-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="704b7-158">作法：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="704b7-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="704b7-159">作法︰使用 FTP 下載檔案</span><span class="sxs-lookup"><span data-stu-id="704b7-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="704b7-160">如何： 使用 hello 本機 Git 儲存機制下載檔案</span><span class="sxs-lookup"><span data-stu-id="704b7-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="704b7-161">作法：設定部署認證</span><span class="sxs-lookup"><span data-stu-id="704b7-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="704b7-162">您可以從您使用 FTP 或本機 Git 儲存機制的函式應用程式下載檔案之前，您必須設定認證 tooaccess hello 站台。</span><span class="sxs-lookup"><span data-stu-id="704b7-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="704b7-163">認證會在 hello 函式應用程式層級設定。</span><span class="sxs-lookup"><span data-stu-id="704b7-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="704b7-164">使用下列步驟 tooset 部署認證 hello Azure 入口網站中的 hello:</span><span class="sxs-lookup"><span data-stu-id="704b7-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="704b7-165">您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署認證**。</span><span class="sxs-lookup"><span data-stu-id="704b7-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![設定本機部署認證](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="704b7-167">輸入使用者名稱和密碼，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="704b7-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="704b7-168">您現在可以使用這些認證 tooaccess 函式應用程式從 FTP 或 hello 內建的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="704b7-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="704b7-169">作法︰使用 FTP 下載檔案</span><span class="sxs-lookup"><span data-stu-id="704b7-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="704b7-170">您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下**平台功能**和**屬性**，然後將複製的 hello 值**FTP/部署使用者**， **FTP 主機名稱**，和**FTPS 主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="704b7-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="704b7-171">**FTP/部署使用者**必須輸入 hello 入口網站，包括 hello 應用程式名稱、 tooprovide hello FTP 伺服器的適當的內容中所示。</span><span class="sxs-lookup"><span data-stu-id="704b7-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![取得部署資訊](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="704b7-173">從您的 FTP 用戶端，使用您所蒐集 tooconnect tooyour 應用程式的 hello 連接資訊和下載 hello 函式的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="704b7-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="704b7-174">操作說明：使用本機 Git 存放庫來下載檔案</span><span class="sxs-lookup"><span data-stu-id="704b7-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="704b7-175">您函式中應用程式中 hello [Azure 入口網站](https://portal.azure.com)，按一下 **平台功能**和**部署選項**。</span><span class="sxs-lookup"><span data-stu-id="704b7-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="704b7-177">接著在 hello**部署**刀鋒視窗中按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="704b7-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![設定持續部署](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="704b7-179">在 hello**部署來源**刀鋒視窗中，按一下**本機 Git 儲存機制**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="704b7-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="704b7-180">在**平台功能**，按一下 **屬性**並記下 hello Git URL 值。</span><span class="sxs-lookup"><span data-stu-id="704b7-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![設定持續部署](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="704b7-182">使用 Git 感知的命令提示字元或您慣用的 Git 工具在本機電腦上複製 hello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="704b7-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="704b7-183">hello Git clone 命令看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="704b7-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="704b7-184">擷取函式應用程式 toohello 再製的檔案儲存在本機電腦，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="704b7-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="704b7-185">如果系統要求，請提供[已設定的部署認證](#credentials)。</span><span class="sxs-lookup"><span data-stu-id="704b7-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
