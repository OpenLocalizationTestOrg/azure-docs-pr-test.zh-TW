---
title: "在 Azure 中的 Visual Studio Team Services 與 Git aaaContinuous 傳遞 |Microsoft 文件"
description: "了解如何 tooconfigure Visual Studio Team Services 的 team 的專案 toouse Git tooautomatically 建置和部署 Azure 應用程式服務或雲端服務中的 toohello Web 應用程式功能。"
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="747dc-103">使用 Visual Studio Team Services 和 Git 的持續傳遞 tooAzure</span><span class="sxs-lookup"><span data-stu-id="747dc-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="747dc-104">您可以使用 Visual Studio Team Services 團隊專案 toohost Git 儲存機制的原始程式碼，自動建置和 tooAzure web 應用程式部署或雲端服務，每當您推送認可 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="747dc-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="747dc-105">您將需要 Visual Studio 2013 和 Azure SDK 安裝 hello。</span><span class="sxs-lookup"><span data-stu-id="747dc-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="747dc-106">如果您還沒有 Visual Studio 2013，下載選擇 hello**免費開始**連結[www.visualstudio.com](http://www.visualstudio.com)。安裝 hello 從 Azure SDK[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)。</span><span class="sxs-lookup"><span data-stu-id="747dc-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="747dc-107">本教學課程需要 Visual Studio Team Services 帳戶 toocomplete： 您可以[免費開啟 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。</span><span class="sxs-lookup"><span data-stu-id="747dc-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="747dc-108">設定雲端服務 tooautomatically tooset 建置和部署使用 Visual Studio Team Services tooAzure，依照下列步驟。</span><span class="sxs-lookup"><span data-stu-id="747dc-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="747dc-109">1：建立 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="747dc-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="747dc-110">如果您還沒有 Visual Studio Team Services 帳戶，請在[這裡](http://go.microsoft.com/fwlink/?LinkId=397665)取得。</span><span class="sxs-lookup"><span data-stu-id="747dc-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="747dc-111">建立小組專案時，請選擇 Git 作為原始檔控制系統。</span><span class="sxs-lookup"><span data-stu-id="747dc-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="747dc-112">請遵循 hello 指示 tooconnect Visual Studio tooyour team 專案。</span><span class="sxs-lookup"><span data-stu-id="747dc-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="747dc-113">在**Team Explorer**，選擇 hello**複製這個儲存機制**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="747dc-114">指定 hello hello 本機複本的位置，然後選擇 [hello**複製**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="747dc-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="747dc-115">2： 建立專案，並加以認可 toohello 儲存機制</span><span class="sxs-lookup"><span data-stu-id="747dc-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="747dc-116">在**Team Explorer**，在 hello**解決方案**區段中，選擇 hello**新增**連結 toocreate hello 本機儲存機制中新的專案。</span><span class="sxs-lookup"><span data-stu-id="747dc-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="747dc-117">您可以將 web 應用程式部署或雲端服務 （Azure 應用程式），由下列 hello 步驟在本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="747dc-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="747dc-118">建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="747dc-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="747dc-119">請確定 hello 專案的目標 hello.NET Framework 4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="747dc-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="747dc-120">如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色與背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="747dc-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="747dc-121">如果您想 toocreate web 應用程式，請選擇 hello **ASP.NET Web 應用程式**專案範本，然後選擇**MVC**。</span><span class="sxs-lookup"><span data-stu-id="747dc-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="747dc-122">如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md) 。</span><span class="sxs-lookup"><span data-stu-id="747dc-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="747dc-123">開啟 hello hello 方案的捷徑功能表並選擇 **認可**。</span><span class="sxs-lookup"><span data-stu-id="747dc-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="747dc-124">如果這是 hello 第一次您在 Visual Studio Team Services 使用 Git，您必須 tooprovide 某些資訊 tooidentify 自行在 Git 中。</span><span class="sxs-lookup"><span data-stu-id="747dc-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="747dc-125">在 hello**暫止的變更**區域**Team Explorer**、 輸入您的使用者名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="747dc-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="747dc-126">輸入 hello 認可的註解，然後選擇 [hello**認可**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="747dc-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="747dc-127">請注意 hello 選項 tooinclude 或排除特定的變更，當您簽入。</span><span class="sxs-lookup"><span data-stu-id="747dc-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="747dc-128">如果 hello 變更您想要排除，請選擇**全部包含**。</span><span class="sxs-lookup"><span data-stu-id="747dc-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="747dc-129">您現在已認可的 hello 變更 hello 儲存機制的本機複本中。</span><span class="sxs-lookup"><span data-stu-id="747dc-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="747dc-130">接下來，選擇 hello 同步這些變更與 hello 伺服器**同步**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="747dc-131">3： 連接 hello 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="747dc-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="747dc-132">現在您有 Visual Studio Team Services 中具有某些來源中的程式碼它的 Git 儲存機制，您就準備 tooconnect 您的 git 儲存機制 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="747dc-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="747dc-133">在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，選取 雲端服務或 web 應用程式，或建立一個新選擇 hello + 圖示 hello 左下方，然後選擇**雲端服務**或**Web 應用程式**然後**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="747dc-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="747dc-134">雲端服務，選擇 hello**設定發行與 Visual Studio Team Services**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="747dc-135">針對 web 應用程式中，選擇 hello**設定從原始檔控制進行部署**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="747dc-136">在 hello 精靈中，在 hello 文字方塊中輸入 hello 您的 Visual Studio Team Services 帳戶名稱，然後選擇 hello**現在授權**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="747dc-137">您可能會要求 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="747dc-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="747dc-138">在 hello**連線要求**快顯對話方塊中，選擇**接受**tooauthorize Azure tooconfigure 您 team 專案在 Visual Studio Team Services。</span><span class="sxs-lookup"><span data-stu-id="747dc-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="747dc-139">授權成功後，將出現含有 Visual Studio Team Services 之 Team 專案的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="747dc-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="747dc-140">選取 hello hello 先前步驟中，在您建立 team 專案名稱，然後選擇 hello 精靈的核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="747dc-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="747dc-141">hello 推送認可 tooyour 儲存機制，Visual Studio Team Services 的下一次將建置和部署專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="747dc-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="747dc-142">4：觸發重建和重新部署專案</span><span class="sxs-lookup"><span data-stu-id="747dc-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="747dc-143">在 Visual Studio 中，開啟檔案進行變更。</span><span class="sxs-lookup"><span data-stu-id="747dc-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="747dc-144">例如，變更 hello 檔案`_Layout.cshtml`hello 檢視下\\MVC web 角色中的共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="747dc-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="747dc-145">編輯 hello 站台的 hello 頁尾文字，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="747dc-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="747dc-146">在**方案總管 中**，hello 方案節點、 專案節點或 hello 檔案變更，您開啟 hello 捷徑功能表，然後選擇**認可**。</span><span class="sxs-lookup"><span data-stu-id="747dc-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="747dc-147">輸入註解並選擇 [認可] 。</span><span class="sxs-lookup"><span data-stu-id="747dc-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="747dc-148">選擇 hello**同步**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="747dc-149">選擇 hello**推送**連結 toopush Visual Studio Team Services 在您認可 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="747dc-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="747dc-150">(您也可以使用 hello**同步**按鈕 toocopy 您認可 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="747dc-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="747dc-151">hello 的差別在於**同步**提取也 hello hello 儲存機制中的最新變更。)</span><span class="sxs-lookup"><span data-stu-id="747dc-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="747dc-152">選擇 hello**家用**按鈕 tooreturn toohello **Team Explorer**首頁。</span><span class="sxs-lookup"><span data-stu-id="747dc-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="747dc-153">選擇**建置**tooview hello 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="747dc-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="747dc-154">**Team Explorer** 會顯示簽入已觸發的組建。</span><span class="sxs-lookup"><span data-stu-id="747dc-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="747dc-155">tooview 詳細的記錄檔為 hello 建置進行時，連按兩下 hello 名稱 hello 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="747dc-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="747dc-156">進行中 hello 組建時，看看 hello 用 hello 精靈 toolink tooAzure 時所建立的組建定義。</span><span class="sxs-lookup"><span data-stu-id="747dc-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="747dc-157">開啟 hello hello 組建定義的捷徑功能表並選擇 **編輯組建定義**。</span><span class="sxs-lookup"><span data-stu-id="747dc-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="747dc-158">在 hello**觸發程序**索引標籤上，您會看到的 hello 組建定義 toobuild 上每個簽入，預設設定。</span><span class="sxs-lookup"><span data-stu-id="747dc-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="747dc-159">（雲端服務中，Visual Studio Team Services 建置和部署 hello 的主要分支 toohello 自動預備環境。</span><span class="sxs-lookup"><span data-stu-id="747dc-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="747dc-160">您仍然必須 toodo 手動步驟 toodeploy toohello 即時網站。</span><span class="sxs-lookup"><span data-stu-id="747dc-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="747dc-161">Web 應用程式中不是預備環境，它會將部署 hello 主要分支直接 toohello 即時網站。</span><span class="sxs-lookup"><span data-stu-id="747dc-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="747dc-162">在 hello**程序**索引標籤上，您可以看到 hello 部署環境設定的雲端服務或 web 應用程式的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="747dc-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="747dc-163">如果您想要比 hello 預設值不同的值，指定 hello 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="747dc-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="747dc-164">hello 屬性 Azure 發行會在 hello**部署** 區段中，而且您可能也需要 tooset MSBuild 參數。</span><span class="sxs-lookup"><span data-stu-id="747dc-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="747dc-165">例如，在雲端服務專案中，toospecify 「 雲端 」，以外的服務組態中設定太 hello MSbuild 參數`/p:TargetProfile=[YourProfile]`其中*[YourProfile]*符合服務組態檔的名稱，例如使用ServiceConfiguration。*YourProfile*.cscfg。</span><span class="sxs-lookup"><span data-stu-id="747dc-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="747dc-166">hello 下列資料表顯示 hello 可用的屬性中 hello**部署**> 一節：</span><span class="sxs-lookup"><span data-stu-id="747dc-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="747dc-167">屬性</span><span class="sxs-lookup"><span data-stu-id="747dc-167">Property</span></span> | <span data-ttu-id="747dc-168">預設值</span><span class="sxs-lookup"><span data-stu-id="747dc-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="747dc-169">允許未受信任的憑證</span><span class="sxs-lookup"><span data-stu-id="747dc-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="747dc-170">如果為 false，SSL 憑證必須經過根授權單位簽署。</span><span class="sxs-lookup"><span data-stu-id="747dc-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="747dc-171">允許升級</span><span class="sxs-lookup"><span data-stu-id="747dc-171">Allow Upgrade</span></span> |<span data-ttu-id="747dc-172">可讓 hello 部署 tooupdate 而不是建立一個新現有的部署。</span><span class="sxs-lookup"><span data-stu-id="747dc-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="747dc-173">會保留 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="747dc-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="747dc-174">不要刪除</span><span class="sxs-lookup"><span data-stu-id="747dc-174">Do Not Delete</span></span> |<span data-ttu-id="747dc-175">如果為 true，則不要覆寫現有不相關的部署 (允許升級)。</span><span class="sxs-lookup"><span data-stu-id="747dc-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="747dc-176">路徑 tooDeployment 設定</span><span class="sxs-lookup"><span data-stu-id="747dc-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="747dc-177">hello 路徑 tooyour.pubxml 檔案是 web 應用程式，相對 toohello hello 儲存機制根資料夾。</span><span class="sxs-lookup"><span data-stu-id="747dc-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="747dc-178">雲端服務則會忽略。</span><span class="sxs-lookup"><span data-stu-id="747dc-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="747dc-179">SharePoint 部署環境</span><span class="sxs-lookup"><span data-stu-id="747dc-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="747dc-180">hello 與 hello 服務名稱的相同。</span><span class="sxs-lookup"><span data-stu-id="747dc-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="747dc-181">Azure 部署環境</span><span class="sxs-lookup"><span data-stu-id="747dc-181">Azure Deployment Environment</span></span> |<span data-ttu-id="747dc-182">hello web 應用程式或雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="747dc-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="747dc-183">現在應該已順利完成您的組建。</span><span class="sxs-lookup"><span data-stu-id="747dc-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="747dc-184">如果您按兩下 hello 組建名稱時，Visual Studio 會顯示**組建摘要**，包括中的任何測試結果相關聯的單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="747dc-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="747dc-185">在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，您可以檢視相關聯的 hello 部署上 hello**部署**索引標籤上，選取 預備環境的 hello 時。</span><span class="sxs-lookup"><span data-stu-id="747dc-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="747dc-186">瀏覽 tooyour 網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="747dc-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="747dc-187">Web 應用程式中，只需選擇 hello**瀏覽**hello 入口網站中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="747dc-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="747dc-188">雲端服務中，選擇 hello URL 在 hello**快速概覽**區段 hello**儀表板**顯示 hello 預備環境的頁面。</span><span class="sxs-lookup"><span data-stu-id="747dc-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="747dc-189">從雲端服務的持續整合的部署都是預設的已發行的 toohello 預備環境。</span><span class="sxs-lookup"><span data-stu-id="747dc-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="747dc-190">您可以變更此設定 hello**替代雲端服務環境**屬性太**生產**。</span><span class="sxs-lookup"><span data-stu-id="747dc-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="747dc-191">以下是程式 hello 站台 URL 是在 hello 雲端服務的儀表板頁面上。</span><span class="sxs-lookup"><span data-stu-id="747dc-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="747dc-192">新的瀏覽器索引標籤會開啟 tooreveal 您執行的網站。</span><span class="sxs-lookup"><span data-stu-id="747dc-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="747dc-193">如果您進行的其他變更 tooyour 專案、 更建置您的觸發程序，和您將會累積多個部署。</span><span class="sxs-lookup"><span data-stu-id="747dc-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="747dc-194">hello 最近一個標示為 使用。</span><span class="sxs-lookup"><span data-stu-id="747dc-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="747dc-195">5：重新部署舊版組建</span><span class="sxs-lookup"><span data-stu-id="747dc-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="747dc-196">此為選用步驟。</span><span class="sxs-lookup"><span data-stu-id="747dc-196">This step is optional.</span></span> <span data-ttu-id="747dc-197">在 hello Azure 傳統入口網站，選擇先前的部署，然後選擇 **重新部署**toorewind 簽入之前您站台 tooan。</span><span class="sxs-lookup"><span data-stu-id="747dc-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="747dc-198">請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。</span><span class="sxs-lookup"><span data-stu-id="747dc-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="747dc-199">6： 變更 hello 生產環境部署</span><span class="sxs-lookup"><span data-stu-id="747dc-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="747dc-200">當您準備好時，您可以選擇升級 hello 臨時 toohello 生產環境**交換**hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="747dc-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="747dc-201">新部署的 hello 臨時環境是已升級的 tooProduction 而 hello 先前生產環境中，如果有的話，會變成預備環境。</span><span class="sxs-lookup"><span data-stu-id="747dc-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="747dc-202">hello 作用中的部署可能會不同 hello 生產與預備環境，但最近組建 hello 部署歷程記錄是 hello 相同的環境而定。</span><span class="sxs-lookup"><span data-stu-id="747dc-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="747dc-203">7：從工作分支部署。</span><span class="sxs-lookup"><span data-stu-id="747dc-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="747dc-204">當您使用 Git 時，您通常在工作分支中進行變更，並整合 hello 主要分支，當您開發達到完成的狀態。</span><span class="sxs-lookup"><span data-stu-id="747dc-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="747dc-205">Hello 專案的開發階段，您會想 toobuild 和部署 hello 工作分支 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="747dc-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="747dc-206">在**Team Explorer**，選擇 hello**首頁**按鈕，然後選擇 [hello**分支**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="747dc-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="747dc-207">選擇 hello**新分支**連結。</span><span class="sxs-lookup"><span data-stu-id="747dc-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="747dc-208">輸入 hello 名稱 hello 分支，例如 「 處理中 」，然後選擇 **建立分支**。</span><span class="sxs-lookup"><span data-stu-id="747dc-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="747dc-209">這樣會建立新的本機分支。</span><span class="sxs-lookup"><span data-stu-id="747dc-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="747dc-210">發行 hello 分支。</span><span class="sxs-lookup"><span data-stu-id="747dc-210">Publish hello branch.</span></span> <span data-ttu-id="747dc-211">選擇在 hello 分支名稱**取消發行分支**，然後選擇 **發行**。</span><span class="sxs-lookup"><span data-stu-id="747dc-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="747dc-212">根據預設，只會變更 toohello 主要分支的觸發程序連續的組建。</span><span class="sxs-lookup"><span data-stu-id="747dc-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="747dc-213">連續建置工作分支，tooset 選擇 hello**建置**頁面**Team Explorer**，然後選擇 **編輯組建定義**。</span><span class="sxs-lookup"><span data-stu-id="747dc-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="747dc-214">開啟 hello**來源設定** 索引標籤。在下**監視用於持續整合及建置分支**，選擇**按一下這裡 tooadd 新的資料列**。</span><span class="sxs-lookup"><span data-stu-id="747dc-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="747dc-215">指定在建立，例如 refs/heads/有效的 hello 分支。</span><span class="sxs-lookup"><span data-stu-id="747dc-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="747dc-216">進行變更以 hello 程式碼中，開啟 hello hello 變更檔案的捷徑功能表，然後選擇 **認可**。</span><span class="sxs-lookup"><span data-stu-id="747dc-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="747dc-217">選擇 hello**未同步處理認可**連結，然後選擇 hello**同步**按鈕或 hello**推送**連結 toocopy hello 變更 Visual Studio 中的 hello 工作分支的 toohello 副本Team Services。</span><span class="sxs-lookup"><span data-stu-id="747dc-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="747dc-218">瀏覽 toohello**建置**檢視，並尋找 hello 工作分支只收到觸發的 hello 組建。</span><span class="sxs-lookup"><span data-stu-id="747dc-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="747dc-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="747dc-219">Next steps</span></span>
<span data-ttu-id="747dc-220">toolearn 秘訣在 Git 中使用 Visual Studio Team Services，請參閱[開發和共用您的程式碼中使用 Visual Studio 的 Git](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)及使用未受 Visual Studio Team Services toopublish 的 Git 儲存機制的相關資訊tooAzure，請參閱[連續部署 tooAzure App Service](../app-service-web/app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="747dc-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="747dc-221">如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。</span><span class="sxs-lookup"><span data-stu-id="747dc-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
