---
title: "本機 Git 部署至 Azure App Service"
description: "了解如何啟用本機 Git 部署至 Azure App Service。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="ac5e5-103">本機 Git 部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ac5e5-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="ac5e5-104">本教學課程會示範如何將應用程式從本機電腦上的 Git 儲存機制部署到 [Azure App Service] 。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="ac5e5-105">App Service 支援使用這個方法和 [Azure 入口網站]的 [本機 Git] 部署選項。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="ac5e5-106">使用[這裡](app-service-web-get-started.md)描述的 [Azure 命令列介面]來建立 App Service 應用程式時，會自動執行本文中描述的許多 Git 命令。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac5e5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ac5e5-107">Prerequisites</span></span>
<span data-ttu-id="ac5e5-108">若要完成本教學課程，您需要：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ac5e5-109">Git。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-109">Git.</span></span> <span data-ttu-id="ac5e5-110">您可以在 [這裡](http://www.git-scm.com/downloads)下載安裝二進位檔。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="ac5e5-111">Git 基本知識。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="ac5e5-112">Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-112">A Microsoft Azure account.</span></span> <span data-ttu-id="ac5e5-113">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="ac5e5-114">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期的入門應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="ac5e5-115">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="ac5e5-116"><a name="Step1"></a>步驟 1：建立本機儲存機制</span><span class="sxs-lookup"><span data-stu-id="ac5e5-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="ac5e5-117">請執行下列工作以建立新的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="ac5e5-118">啟動命令列工具，例如 **GitBash** (Windows) 或 **Bash** (Unix Shell)。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="ac5e5-119">在 OS X 系統上，您可以透過 **[終端機]** 應用程式來存取命令列。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="ac5e5-120">瀏覽至部署內容所在的目錄。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="ac5e5-121">使用下列命令來初始化新的 Git 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="ac5e5-122"><a name="Step2"></a>步驟 2︰認可內容</span><span class="sxs-lookup"><span data-stu-id="ac5e5-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="ac5e5-123">App Service 支援以各種程式設計語言建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="ac5e5-124">如果您的儲存機制已經包含內容，請略過這點，並移至下面的第 2 點。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="ac5e5-125">如果您的儲存機制尚未包含內容，請只要填入靜態的 .html 檔案，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="ac5e5-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="ac5e5-126">使用文字編輯器，在 Git 儲存機制的根目錄建立新檔案 **index.html** 。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="ac5e5-127">在 index.html 檔案中加入並儲存下列文字內容： *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="ac5e5-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="ac5e5-128">從命令列，驗證您位在 Git 儲存機制的根目錄下。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="ac5e5-129">然後使用下列命令將檔案加入儲存機制中：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="ac5e5-130">接著，使用下列命令來認可對儲存機制的變更：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="ac5e5-131"><a name="Step3"></a>步驟 3︰啟用 App Service 應用程式儲存機制</span><span class="sxs-lookup"><span data-stu-id="ac5e5-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="ac5e5-132">執行下列步驟以啟用 App Service 應用程式的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="ac5e5-133">登入 [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="ac5e5-134">在 App Service 應用程式的刀鋒視窗中，按一下 [設定] > [部署來源]。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="ac5e5-135">依序按一下 [選擇來源]、[本機 Git 儲存機制] 以及 [確定]。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![本機 Git 儲存機制](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="ac5e5-137">如果這是您第一次在 Azure 中設定儲存機制，就需要為它建立登入認證。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="ac5e5-138">您將使用這些認證來登入 Azure 儲存機制，並推播來自您本機 Git 儲存機制的變更。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="ac5e5-139">從應用程式的刀鋒視窗中，按一下 [設定] > [部署認證]，然後設定您的部署使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="ac5e5-140">完成後，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="ac5e5-141"><a name="Step4"></a>步驟 4：部署專案</span><span class="sxs-lookup"><span data-stu-id="ac5e5-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="ac5e5-142">使用下列步驟，使用本機 Git 將應用程式發佈至 App Service。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="ac5e5-143">在 Azure 入口網站上的應用程式刀鋒視窗中，按一下 [Git URL] 的 [設定] > [屬性]。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="ac5e5-144">**Git URL** 是從本機儲存機制部署的遠端參考。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="ac5e5-145">在下列步驟中，您將使用此 URL。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="ac5e5-146">使用命令列驗證您位在 Git 儲存機制的根目錄。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="ac5e5-147">使用 `git remote` 加入從步驟 1 的 **Git URL** 中所列的遠端參考。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="ac5e5-148">您的命令將類似以下範例：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="ac5e5-149">**remote** 命令會將指定的參考新增至遠端儲存機制。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="ac5e5-150">在此範例中，它會為您 Web 應用程式的儲存機制建立名為 'azure' 的參考。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="ac5e5-151">使用剛建立的新 **zure** 遠端將您的內容推送至 App Service。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="ac5e5-152">回到 Azure 入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="ac5e5-153">最近推送的記錄項目應該會顯示在 [部署]  刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="ac5e5-154">按一下應用程式刀鋒視窗頂端的 [瀏覽]  按鈕確認是否已部署內容。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="ac5e5-155"><a name="Step5"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="ac5e5-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="ac5e5-156">使用 Git 發佈至 Azure 的 App Service 應用程式時，下列是經常會遇到的錯誤或問題：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="ac5e5-157">**徵兆**：無法存取 '[siteURL]'：無法連接至 [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="ac5e5-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="ac5e5-158">**原因**：如果應用程式尚未啟動並執行，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="ac5e5-159">**解決方式**：在 Azure 入口網站中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="ac5e5-160">除非應用程式正在執行，否則 Git 部署將無法運作。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="ac5e5-161">**徵兆**：無法解析主機 'hostname'</span><span class="sxs-lookup"><span data-stu-id="ac5e5-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="ac5e5-162">**原因**：如果建立 'azure' 遠端時所輸入的位址資訊不正確，便有可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="ac5e5-163">**解決方式**：使用 `git remote -v` 命令，列出所有遠端以及相關聯的 URL。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="ac5e5-164">驗證 'azure' 遠端的 URL 是否正確。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="ac5e5-165">如有需要，移除此遠端並使用正確的 URL 重新建立。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="ac5e5-166">**徵兆**：通常沒有參考且沒有指定；不執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="ac5e5-167">或許您應該指定分支，例如 'master'。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="ac5e5-168">**原因**：執行 git 推送操作時，如果您沒有指定分支，且沒有設定 Git 所使用的 push.default 值，便有可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="ac5e5-169">**解決方式**：指定主要分支，重新執行推送操作。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="ac5e5-170">例如：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ac5e5-171">**徵兆**：src refspec [branchname] 沒有任何符合項目。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="ac5e5-172">**原因**：如果您嘗試在 'azure' 遠端上推送至除了主要以外的分支，便有可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="ac5e5-173">**解決方式**：指定主要分支，重新執行推送操作。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="ac5e5-174">例如：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ac5e5-175">**徵兆**RPC 失敗；結果 = 22，HTTP 代碼 = 502。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="ac5e5-176">**原因**︰如果您嘗試透過 HTTPS 推送大型 Git 儲存機制，可能會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="ac5e5-177">**解決方式**︰變更本機電腦上的 Git 組態以加大 postBuffer</span><span class="sxs-lookup"><span data-stu-id="ac5e5-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="ac5e5-178">**徵兆**：錯誤 - 對遠端儲存機制認可變更，但您的 Web 應用程式未更新。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="ac5e5-179">**原因**：如果您打算部署包含 package.json 檔案的 Node.js 應用程式，但該檔案指出需要額外的模組，便有可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="ac5e5-180">**解決方式**︰其他包含 'npm ERR!' 的訊息</span><span class="sxs-lookup"><span data-stu-id="ac5e5-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="ac5e5-181">在發生此錯誤之前應該就有記錄，可提供關於此失敗的更多資訊。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="ac5e5-182">下列是此錯誤的已知原因及其對應的 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="ac5e5-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="ac5e5-183">message:</span><span class="sxs-lookup"><span data-stu-id="ac5e5-183">message:</span></span>

* <span data-ttu-id="ac5e5-184">**格式錯誤的 package.json 檔案**：npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ac5e5-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="ac5e5-185">無法讀取相依性。</span><span class="sxs-lookup"><span data-stu-id="ac5e5-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="ac5e5-186">**原生模組沒有適用於 Windows 的二進位檔發佈**：</span><span class="sxs-lookup"><span data-stu-id="ac5e5-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="ac5e5-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ac5e5-187">npm ERR!</span></span> <span data-ttu-id="ac5e5-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="ac5e5-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="ac5e5-189">或</span><span class="sxs-lookup"><span data-stu-id="ac5e5-189">OR</span></span>
  * <span data-ttu-id="ac5e5-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ac5e5-190">npm ERR!</span></span> <span data-ttu-id="ac5e5-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="ac5e5-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac5e5-192">其他資源</span><span class="sxs-lookup"><span data-stu-id="ac5e5-192">Additional Resources</span></span>
* [<span data-ttu-id="ac5e5-193">Git 文件</span><span class="sxs-lookup"><span data-stu-id="ac5e5-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="ac5e5-194">專案 Kudu 文件</span><span class="sxs-lookup"><span data-stu-id="ac5e5-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="ac5e5-195">持續部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ac5e5-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="ac5e5-196">如何使用適用於 Azure 的 PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac5e5-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ac5e5-197">如何使用 Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="ac5e5-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="ac5e5-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="ac5e5-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="ac5e5-199">[Azure 入口網站]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ac5e5-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="ac5e5-200">[Azure 命令列介面]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="ac5e5-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
