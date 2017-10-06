---
title: "aaaLocal Git 部署 tooAzure 應用程式服務"
description: "深入了解如何本機 Git 部署 tooAzure tooenable 應用程式服務。"
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
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="b408b-103">本機 Git 部署 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b408b-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="b408b-104">本教學課程示範如何 toodeploy 您的應用程式太[Azure App Service]從本機電腦上的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b408b-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="b408b-105">應用程式服務支援使用這個方法以 hello**本機 Git** hello 中的部署選項[Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="b408b-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="b408b-106">許多本文中所述的 hello Git 命令時，會執行自動建立 App Service 應用程式使用 hello [Azure 命令列介面]述[這裡](app-service-web-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b408b-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b408b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="b408b-107">Prerequisites</span></span>
<span data-ttu-id="b408b-108">toocomplete 本教學課程中，您需要：</span><span class="sxs-lookup"><span data-stu-id="b408b-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="b408b-109">Git。</span><span class="sxs-lookup"><span data-stu-id="b408b-109">Git.</span></span> <span data-ttu-id="b408b-110">您可以下載 hello 安裝二進位檔案[這裡](http://www.git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="b408b-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="b408b-111">Git 基本知識。</span><span class="sxs-lookup"><span data-stu-id="b408b-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="b408b-112">Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b408b-112">A Microsoft Azure account.</span></span> <span data-ttu-id="b408b-113">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)。</span><span class="sxs-lookup"><span data-stu-id="b408b-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="b408b-114">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的起始應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="b408b-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="b408b-115">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="b408b-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="b408b-116"><a name="Step1"></a>步驟 1：建立本機儲存機制</span><span class="sxs-lookup"><span data-stu-id="b408b-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="b408b-117">執行下列工作 toocreate 新的 Git 儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="b408b-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="b408b-118">啟動命令列工具，例如 **GitBash** (Windows) 或 **Bash** (Unix Shell)。</span><span class="sxs-lookup"><span data-stu-id="b408b-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="b408b-119">您可以在 OS X 系統上存取 hello 命令列透過 hello**終端機**應用程式。</span><span class="sxs-lookup"><span data-stu-id="b408b-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="b408b-120">瀏覽應該放置 hello 內容 toodeploy toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="b408b-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="b408b-121">使用下列命令 tooinitialize 新的 Git 儲存機制的 hello:</span><span class="sxs-lookup"><span data-stu-id="b408b-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="b408b-122"><a name="Step2"></a>步驟 2︰認可內容</span><span class="sxs-lookup"><span data-stu-id="b408b-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="b408b-123">App Service 支援以各種程式設計語言建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b408b-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="b408b-124">如果您的儲存機制已包含內容的略過此點，而且移動 toopoint 底下 2。</span><span class="sxs-lookup"><span data-stu-id="b408b-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="b408b-125">如果您的儲存機制尚未包含內容，請只要填入靜態的 .html 檔案，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="b408b-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="b408b-126">使用文字編輯器中，建立名為的新檔案**index.html**根目錄 hello hello Git 儲存機制</span><span class="sxs-lookup"><span data-stu-id="b408b-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="b408b-127">新增 hello hello index.html hello 內容檔案，並將它儲存為下列文字： *Hello Git ！*</span><span class="sxs-lookup"><span data-stu-id="b408b-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="b408b-128">從命令列的 hello，確認您在 hello 的 Git 儲存機制的根目錄下。</span><span class="sxs-lookup"><span data-stu-id="b408b-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="b408b-129">接著，使用下列命令 tooadd 檔案 tooyour 儲存機制的 hello:</span><span class="sxs-lookup"><span data-stu-id="b408b-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="b408b-130">接下來，使用下列命令的 hello 認可 hello 變更 toohello 儲存機制：</span><span class="sxs-lookup"><span data-stu-id="b408b-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="b408b-131"><a name="Step3"></a>步驟 3： 啟用 hello App Service 應用程式儲存機制</span><span class="sxs-lookup"><span data-stu-id="b408b-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="b408b-132">執行下列步驟 tooenable 您 App Service 應用程式的 Git 儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="b408b-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="b408b-133">登入 toohello [Azure 入口網站]。</span><span class="sxs-lookup"><span data-stu-id="b408b-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="b408b-134">在 App Service 應用程式的刀鋒視窗中，按一下 [設定] > [部署來源]。</span><span class="sxs-lookup"><span data-stu-id="b408b-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="b408b-135">依序按一下 [選擇來源]、[本機 Git 儲存機制] 以及 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b408b-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![本機 Git 儲存機制](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="b408b-137">如果這是您第一次設定 Azure 中的儲存機制，您會需要它 toocreate 登入認證。</span><span class="sxs-lookup"><span data-stu-id="b408b-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="b408b-138">您將使用這些 toolog 到 hello Azure 儲存機制並將變更推播從本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b408b-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="b408b-139">從應用程式的刀鋒視窗中，按一下 [設定] > [部署認證]，然後設定您的部署使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="b408b-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="b408b-140">完成後，按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b408b-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="b408b-141"><a name="Step4"></a>步驟 4：部署專案</span><span class="sxs-lookup"><span data-stu-id="b408b-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="b408b-142">使用下列步驟 toopublish hello 您應用程式 tooApp 使用本機 Git 服務。</span><span class="sxs-lookup"><span data-stu-id="b408b-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="b408b-143">在您的應用程式] 刀鋒視窗 hello Azure 入口網站中，按一下 [**設定 > 屬性**hello **Git URL**。</span><span class="sxs-lookup"><span data-stu-id="b408b-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="b408b-144">**Git URL**是 hello 遠端參照 toodeploy toofrom 本機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b408b-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="b408b-145">Hello 步驟中，您將使用此 URL。</span><span class="sxs-lookup"><span data-stu-id="b408b-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="b408b-146">使用命令列的 hello，確認您是在 hello 的本機 Git 儲存機制的根目錄。</span><span class="sxs-lookup"><span data-stu-id="b408b-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="b408b-147">使用`git remote`tooadd hello 遠端參考中所列**Git URL**步驟 1 中。</span><span class="sxs-lookup"><span data-stu-id="b408b-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="b408b-148">您的命令看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b408b-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="b408b-149">hello**遠端**命令會將具名的參考 tooa 遠端儲存機制。</span><span class="sxs-lookup"><span data-stu-id="b408b-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="b408b-150">在此範例中，它會為您 Web 應用程式的儲存機制建立名為 'azure' 的參考。</span><span class="sxs-lookup"><span data-stu-id="b408b-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="b408b-151">推送您的內容 tooApp 服務使用新的 hello **azure**遠端您剛建立。</span><span class="sxs-lookup"><span data-stu-id="b408b-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="b408b-152">返回 tooyour hello Azure 入口網站中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b408b-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="b408b-153">您最近發送的記錄項目應該會顯示在 hello**部署**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b408b-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="b408b-154">按一下 hello**瀏覽**已部署的 hello 應用程式 刀鋒視窗 tooverify hello 內容 hello 頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="b408b-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="b408b-155"><a name="Step5"></a>疑難排解</span><span class="sxs-lookup"><span data-stu-id="b408b-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="b408b-156">hello 如下的錯誤或在 Azure 中使用 Git toopublish tooan App Service 應用程式時經常會遇到的問題：</span><span class="sxs-lookup"><span data-stu-id="b408b-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="b408b-157">**徵兆**： 無法 tooaccess [siteURL]: 無法 tooconnect 太 [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="b408b-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="b408b-158">**可能的原因**： 如果 hello 應用程式不會啟動並執行，可能會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="b408b-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="b408b-159">**解析**: hello Azure 入口網站中的開始 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b408b-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="b408b-160">Git 部署將無法運作，除非 hello 應用程式正在執行。</span><span class="sxs-lookup"><span data-stu-id="b408b-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="b408b-161">**徵兆**：無法解析主機 'hostname'</span><span class="sxs-lookup"><span data-stu-id="b408b-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="b408b-162">**可能的原因**： 會發生此錯誤如果 hello 位址資訊輸入時建立 hello 'azure' 遠端不正確。</span><span class="sxs-lookup"><span data-stu-id="b408b-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="b408b-163">**解析**： 使用 hello`git remote -v`命令 toolist 所有的遙控器，以及相關聯的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="b408b-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="b408b-164">請確認 hello hello 'azure' 遠端 URL 正確。</span><span class="sxs-lookup"><span data-stu-id="b408b-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="b408b-165">如果需要請移除並重新建立此遠端使用 hello 正確的 URL。</span><span class="sxs-lookup"><span data-stu-id="b408b-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="b408b-166">**徵兆**：通常沒有參考且沒有指定；不執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="b408b-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="b408b-167">或許您應該指定分支，例如 'master'。</span><span class="sxs-lookup"><span data-stu-id="b408b-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="b408b-168">**可能的原因**： 如果您不指定分支時執行 git push 作業，且 not set hello push.default 值使用 Git，可能會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="b408b-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="b408b-169">**解析**: hello 推入然後再執行作業，指定 hello 主要分支。</span><span class="sxs-lookup"><span data-stu-id="b408b-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="b408b-170">例如：</span><span class="sxs-lookup"><span data-stu-id="b408b-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="b408b-171">**徵兆**：src refspec [branchname] 沒有任何符合項目。</span><span class="sxs-lookup"><span data-stu-id="b408b-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="b408b-172">**可能的原因**： 如果您嘗試在 hello 'azure' 遠端 master 以外 toopush tooa 分支，則會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="b408b-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="b408b-173">**解析**: hello 推入然後再執行作業，指定 hello 主要分支。</span><span class="sxs-lookup"><span data-stu-id="b408b-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="b408b-174">例如：</span><span class="sxs-lookup"><span data-stu-id="b408b-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="b408b-175">**徵兆**RPC 失敗；結果 = 22，HTTP 代碼 = 502。</span><span class="sxs-lookup"><span data-stu-id="b408b-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="b408b-176">**可能的原因**： 如果您嘗試透過 HTTPS 的 toopush 大型的 git 儲存機制，會發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="b408b-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="b408b-177">**解析**： 變更 hello git 設定上更大的 hello 本機 toomake hello 後置</span><span class="sxs-lookup"><span data-stu-id="b408b-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="b408b-178">**徵兆**： 錯誤-變更認可的 tooremote 儲存機制，但不是會更新您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b408b-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="b408b-179">**原因**：如果您打算部署包含 package.json 檔案的 Node.js 應用程式，但該檔案指出需要額外的模組，便有可能發生此錯誤。</span><span class="sxs-lookup"><span data-stu-id="b408b-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="b408b-180">**解決方式**︰其他包含 'npm ERR!' 的訊息</span><span class="sxs-lookup"><span data-stu-id="b408b-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="b408b-181">應已記錄的先前 toothis 錯誤，而且可以在 hello 失敗時提供額外的內容。</span><span class="sxs-lookup"><span data-stu-id="b408b-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="b408b-182">hello 下列已知導致此錯誤的原因，並且 hello 對應 'npm ERR ！'</span><span class="sxs-lookup"><span data-stu-id="b408b-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="b408b-183">message:</span><span class="sxs-lookup"><span data-stu-id="b408b-183">message:</span></span>

* <span data-ttu-id="b408b-184">**格式錯誤的 package.json 檔案**：npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b408b-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="b408b-185">無法讀取相依性。</span><span class="sxs-lookup"><span data-stu-id="b408b-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="b408b-186">**原生模組沒有適用於 Windows 的二進位檔發佈**：</span><span class="sxs-lookup"><span data-stu-id="b408b-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="b408b-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b408b-187">npm ERR!</span></span> <span data-ttu-id="b408b-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span><span class="sxs-lookup"><span data-stu-id="b408b-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="b408b-189">或</span><span class="sxs-lookup"><span data-stu-id="b408b-189">OR</span></span>
  * <span data-ttu-id="b408b-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="b408b-190">npm ERR!</span></span> <span data-ttu-id="b408b-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="b408b-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b408b-192">其他資源</span><span class="sxs-lookup"><span data-stu-id="b408b-192">Additional Resources</span></span>
* [<span data-ttu-id="b408b-193">Git 文件</span><span class="sxs-lookup"><span data-stu-id="b408b-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="b408b-194">專案 Kudu 文件</span><span class="sxs-lookup"><span data-stu-id="b408b-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="b408b-195">連續部署 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b408b-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="b408b-196">如何 toouse PowerShell for Azure</span><span class="sxs-lookup"><span data-stu-id="b408b-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="b408b-197">如何 toouse hello Azure 命令列介面</span><span class="sxs-lookup"><span data-stu-id="b408b-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure 入口網站]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure 命令列介面]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
