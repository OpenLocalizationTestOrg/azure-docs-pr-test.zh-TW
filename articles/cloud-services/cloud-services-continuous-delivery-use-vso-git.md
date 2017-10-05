---
title: "在 Azure 中使用 Git 和 Visual Studio Team Services 來持續傳遞 | Microsoft Docs"
description: "了解如何設定 Visual Studio Team Services 的 Team 專案，以使用 Git 自動建置和部署至 Azure App Service 或雲端服務中的 Web 應用程式功能。"
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="821ab-103">使用 Visual Studio Team Services 和 Git 連續傳遞至 Azure</span><span class="sxs-lookup"><span data-stu-id="821ab-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="821ab-104">您可以使用 Visual Studio Team Services 的 Team 專案託管原始程式碼的 Git 儲存機制，並在每次將認可推送至儲存機制時，自動建置該機制並部署至 Azure Web 應用程式或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="821ab-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="821ab-105">您需要安裝 Visual Studio 2013 和 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="821ab-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="821ab-106">如果您還沒有 Visual Studio 2013，請至 [www.visualstudio.com](http://www.visualstudio.com) 選擇 [免費開始用] 連結來下載。</span><span class="sxs-lookup"><span data-stu-id="821ab-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="821ab-107">從[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="821ab-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="821ab-108">您需要 Visual Studio Team Services 帳戶，才能完成本教學課程：您可以 [開啟免費的 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。</span><span class="sxs-lookup"><span data-stu-id="821ab-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="821ab-109">若要使用 Visual Studio Team Services 將雲端服務設定為自動建立和部署至 Azure，請依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="821ab-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="821ab-110">1：建立 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="821ab-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="821ab-111">如果您還沒有 Visual Studio Team Services 帳戶，請在[這裡](http://go.microsoft.com/fwlink/?LinkId=397665)取得。</span><span class="sxs-lookup"><span data-stu-id="821ab-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="821ab-112">建立小組專案時，請選擇 Git 作為原始檔控制系統。</span><span class="sxs-lookup"><span data-stu-id="821ab-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="821ab-113">依照指示將 Visual Studio 連接至小組專案。</span><span class="sxs-lookup"><span data-stu-id="821ab-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="821ab-114">在 **Team Explorer** 中，選擇 [複製這個儲存機制] 連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="821ab-115">指定本機複本的位置，然後選擇 [複製]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="821ab-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="821ab-116">2：建立專案並認可至儲存機制</span><span class="sxs-lookup"><span data-stu-id="821ab-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="821ab-117">在 **Team Explorer** 中，在 [方案] 區段中選擇 [新增] 連結，在本機儲存機制中建立新專案。</span><span class="sxs-lookup"><span data-stu-id="821ab-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="821ab-118">您可以依照此逐步解說的步驟部署 Web 應用程式或雲端服務 (Azure 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="821ab-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="821ab-119">建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="821ab-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="821ab-120">請確認專案以 .NET Framework 4 或更新版本為目標。</span><span class="sxs-lookup"><span data-stu-id="821ab-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="821ab-121">如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色與背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="821ab-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="821ab-122">如果要建立 Web 應用程式，請選擇 [ASP.NET Web 應用程式] 專案範本，然後選擇 [MVC]。</span><span class="sxs-lookup"><span data-stu-id="821ab-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="821ab-123">如需詳細資訊，請參閱 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md) 。</span><span class="sxs-lookup"><span data-stu-id="821ab-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="821ab-124">開啟方案的捷徑功能表，選擇 [認可] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="821ab-125">如果是第一次在 Visual Studio Team Services 中使用 Git，您需要提供一些資訊在 Git 中識別您的身分。</span><span class="sxs-lookup"><span data-stu-id="821ab-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="821ab-126">在 **Team Explorer** 的 [暫止的變更] 區域中，輸入您的使用者名稱和電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="821ab-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="821ab-127">輸入認可的註解，然後選擇 [認可]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="821ab-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="821ab-128">請注意簽入時用來包含或排除特定變更的選項。</span><span class="sxs-lookup"><span data-stu-id="821ab-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="821ab-129">如果已排除您要的變更，請選擇 [全部包含] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="821ab-130">您現在已在儲存機制的本機複本中認可變更。</span><span class="sxs-lookup"><span data-stu-id="821ab-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="821ab-131">接下來，選擇 [同步處理]  連結，將這些變更同步至伺服器。</span><span class="sxs-lookup"><span data-stu-id="821ab-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="821ab-132">3：將專案連線至 Azure</span><span class="sxs-lookup"><span data-stu-id="821ab-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="821ab-133">現在，您在 Visual Studio Team Services 中有一個 Git 儲存機制，裡面還有一些原始程式碼，您可以準備將 Git 儲存機制連接至 Azure。</span><span class="sxs-lookup"><span data-stu-id="821ab-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="821ab-134">在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取您的雲端服務或 Web 應用程式，或選取左下方的 + 圖示並選擇 [雲端服務] 或 [Web 應用程式]，然後選取 [快速建立]，建立新的雲端服務或 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="821ab-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="821ab-135">若是雲端服務，請擇 [使用 Visual Studio Team Services 設定發行]  連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="821ab-136">若是 Web 應用程式，請選擇 [設定從原始檔控制進行部署]  連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="821ab-137">在精靈中，於文字方塊中輸入 Visual Studio Team Services 帳戶的名稱，然後選擇 [立即授權]  連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="821ab-138">可能會要求您登入。</span><span class="sxs-lookup"><span data-stu-id="821ab-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="821ab-139">在 [連接要求] 快顯對話方塊中，選擇 [接受]，授權 Azure 在 Visual Studio Team Services 中設定 Team 專案。</span><span class="sxs-lookup"><span data-stu-id="821ab-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="821ab-140">授權成功後，將出現含有 Visual Studio Team Services 之 Team 專案的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="821ab-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="821ab-141">選取您在先前步驟中建立的小組專案，然後選擇精靈的勾選記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="821ab-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="821ab-142">您下次將認可推送至儲存機制時，Visual Studio Team Services 將會建置專案並部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="821ab-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="821ab-143">4：觸發重建和重新部署專案</span><span class="sxs-lookup"><span data-stu-id="821ab-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="821ab-144">在 Visual Studio 中，開啟檔案進行變更。</span><span class="sxs-lookup"><span data-stu-id="821ab-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="821ab-145">例如，在 MVC Web 角色中，變更 Views\\Shared 資料夾下的 `_Layout.cshtml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="821ab-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="821ab-146">編輯網站的頁尾文字，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="821ab-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="821ab-147">在 [方案總管] 中，開啟方案節點、專案節點或您變更之檔案的快顯功能表，然後選擇 [認可]。</span><span class="sxs-lookup"><span data-stu-id="821ab-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="821ab-148">輸入註解並選擇 [認可] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="821ab-149">選擇 [ **同步處理** ] 連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="821ab-150">選擇 [推送]  連結，將認可推送至 Visual Studio Team Services 中的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="821ab-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="821ab-151">(您也可以使用 [同步處理]  按鈕，將認可複製到儲存機制。</span><span class="sxs-lookup"><span data-stu-id="821ab-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="821ab-152">差別在於 [同步處理]  還會從儲存機制中提取最新的變更)。</span><span class="sxs-lookup"><span data-stu-id="821ab-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="821ab-153">選擇 [首頁] 按鈕回到 **Team Explorer** 首頁。</span><span class="sxs-lookup"><span data-stu-id="821ab-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="821ab-154">選擇 [組建]  來檢視進行中的組建。</span><span class="sxs-lookup"><span data-stu-id="821ab-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="821ab-155">**Team Explorer** 會顯示簽入已觸發的組建。</span><span class="sxs-lookup"><span data-stu-id="821ab-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="821ab-156">若要在組建進行時檢視詳細記錄，請按兩下進行中組建的名稱。</span><span class="sxs-lookup"><span data-stu-id="821ab-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="821ab-157">當組建進行時，查看您使用精靈連結至 Azure 時所建立的組建定義。</span><span class="sxs-lookup"><span data-stu-id="821ab-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="821ab-158">開啟組建定義的捷徑功能表，然後選擇 [編輯組建定義] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="821ab-159">在 [觸發程序]  索引標籤中，您會看到組建定義已設為依預設每次簽入時建置。</span><span class="sxs-lookup"><span data-stu-id="821ab-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="821ab-160">(若是雲端服務，Visual Studio Team Services 會自動建置主要分支並部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="821ab-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="821ab-161">您仍然必須執行手動步驟來部署至即時網站。</span><span class="sxs-lookup"><span data-stu-id="821ab-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="821ab-162">對於沒有預備環境的 Web 應用程式，它會將主要分支直接部署到即時網站。</span><span class="sxs-lookup"><span data-stu-id="821ab-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="821ab-163">在 [處理序]  索引標籤中，您可以看到部署環境已設為您的雲端服務或 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="821ab-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="821ab-164">如果不想要使用預設值，請指定屬性的值。</span><span class="sxs-lookup"><span data-stu-id="821ab-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="821ab-165">Azure 發佈屬性在 [部署]  區段中，您也可能需要設定 MSBuild 參數。</span><span class="sxs-lookup"><span data-stu-id="821ab-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="821ab-166">例如，在雲端服務專案中，若要指定 "Cloud" 以外的服務組態，請將 MSbuild 參數設為 `/p:TargetProfile=[YourProfile]`，其中，[YourProfile] 符合一個以 ServiceConfiguration.YourProfile.cscfg 命名的服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="821ab-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="821ab-167">下表顯示 [部署]  區段中可用的屬性：</span><span class="sxs-lookup"><span data-stu-id="821ab-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="821ab-168">屬性</span><span class="sxs-lookup"><span data-stu-id="821ab-168">Property</span></span> | <span data-ttu-id="821ab-169">預設值</span><span class="sxs-lookup"><span data-stu-id="821ab-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="821ab-170">允許未受信任的憑證</span><span class="sxs-lookup"><span data-stu-id="821ab-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="821ab-171">如果為 false，SSL 憑證必須經過根授權單位簽署。</span><span class="sxs-lookup"><span data-stu-id="821ab-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="821ab-172">允許升級</span><span class="sxs-lookup"><span data-stu-id="821ab-172">Allow Upgrade</span></span> |<span data-ttu-id="821ab-173">允許部署更新現有的部署而非建立新的部署。</span><span class="sxs-lookup"><span data-stu-id="821ab-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="821ab-174">保留 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="821ab-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="821ab-175">不要刪除</span><span class="sxs-lookup"><span data-stu-id="821ab-175">Do Not Delete</span></span> |<span data-ttu-id="821ab-176">如果為 true，則不要覆寫現有不相關的部署 (允許升級)。</span><span class="sxs-lookup"><span data-stu-id="821ab-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="821ab-177">部署設定的路徑</span><span class="sxs-lookup"><span data-stu-id="821ab-177">Path to Deployment Settings</span></span> |<span data-ttu-id="821ab-178">Web 應用程式的 .pubxml 檔的路徑，這是儲存機制之根資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="821ab-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="821ab-179">雲端服務則會忽略。</span><span class="sxs-lookup"><span data-stu-id="821ab-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="821ab-180">SharePoint 部署環境</span><span class="sxs-lookup"><span data-stu-id="821ab-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="821ab-181">與服務名稱相同。</span><span class="sxs-lookup"><span data-stu-id="821ab-181">The same as the service name.</span></span> |
    | <span data-ttu-id="821ab-182">Azure 部署環境</span><span class="sxs-lookup"><span data-stu-id="821ab-182">Azure Deployment Environment</span></span> |<span data-ttu-id="821ab-183">Web 應用程式或雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="821ab-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="821ab-184">現在應該已順利完成您的組建。</span><span class="sxs-lookup"><span data-stu-id="821ab-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="821ab-185">如果按兩下組建名稱，Visual Studio 會顯示 [組建摘要] ，包括與單元測試專案相關聯的任何測試結果。</span><span class="sxs-lookup"><span data-stu-id="821ab-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="821ab-186">在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取預備環境之後，您可以在 [部署] 索引標籤上檢視相關聯的部署。</span><span class="sxs-lookup"><span data-stu-id="821ab-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="821ab-187">瀏覽至網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="821ab-187">Browse to your site's URL.</span></span> <span data-ttu-id="821ab-188">若是 Web 應用程式，請選擇入口網站中的 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="821ab-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="821ab-189">若是雲端服務，請在 [儀表板] 頁面的 [快速概覽] 區段中選擇 URL，以顯示預備環境。</span><span class="sxs-lookup"><span data-stu-id="821ab-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="821ab-190">依預設，來自雲端服務連續整合的部署會發佈至預備環境。</span><span class="sxs-lookup"><span data-stu-id="821ab-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="821ab-191">您可以將 [替代雲端服務環境] 屬性設為 [生產] 來變更此設定。</span><span class="sxs-lookup"><span data-stu-id="821ab-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="821ab-192">以下是網站 URL 在雲端服務儀表板頁面上的位置。</span><span class="sxs-lookup"><span data-stu-id="821ab-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="821ab-193">新的瀏覽器索引標籤會開啟來顯示您執行中的網站。</span><span class="sxs-lookup"><span data-stu-id="821ab-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="821ab-194">如果對專案進行其他變更，則會觸發更多組建，將累積多個部署。</span><span class="sxs-lookup"><span data-stu-id="821ab-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="821ab-195">最後一個會標示為「作用中」。</span><span class="sxs-lookup"><span data-stu-id="821ab-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="821ab-196">5：重新部署舊版組建</span><span class="sxs-lookup"><span data-stu-id="821ab-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="821ab-197">此為選用步驟。</span><span class="sxs-lookup"><span data-stu-id="821ab-197">This step is optional.</span></span> <span data-ttu-id="821ab-198">在 Azure 傳統入口網站中，選擇先前的部署，然後選擇 [重新部署]  ，將網站倒回到更早的簽入。</span><span class="sxs-lookup"><span data-stu-id="821ab-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="821ab-199">請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。</span><span class="sxs-lookup"><span data-stu-id="821ab-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="821ab-200">6：變更生產部署</span><span class="sxs-lookup"><span data-stu-id="821ab-200">6: Change the Production deployment</span></span>
<span data-ttu-id="821ab-201">準備就緒後，您可以在 Azure 傳統入口網站中選擇 [交換]  按鈕，將預備環境升級至生產環境。</span><span class="sxs-lookup"><span data-stu-id="821ab-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="821ab-202">新部署的預備環境會升級至「生產」，而先前的生產環境 (若有的話) 會變成預備環境。</span><span class="sxs-lookup"><span data-stu-id="821ab-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="821ab-203">「作用中」部署可能與生產和預備環境不同，但最近組建的部署歷程記錄都一樣，與環境無關。</span><span class="sxs-lookup"><span data-stu-id="821ab-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="821ab-204">7：從工作分支部署。</span><span class="sxs-lookup"><span data-stu-id="821ab-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="821ab-205">使用 Git 時，您通常會在工作分支中進行變更，等到開發達到完成狀態時，再整合至主要分支。</span><span class="sxs-lookup"><span data-stu-id="821ab-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="821ab-206">在專案的開發階段期間，您可以建置工作分支並部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="821ab-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="821ab-207">在 **Team Explorer** 中，選擇 [首頁] 按鈕，然後選擇 [分支] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="821ab-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="821ab-208">選擇 [新增分支]  連結。</span><span class="sxs-lookup"><span data-stu-id="821ab-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="821ab-209">輸入分支的名稱，例如 "working"，然後選擇 [建立分支] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="821ab-210">這樣會建立新的本機分支。</span><span class="sxs-lookup"><span data-stu-id="821ab-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="821ab-211">發佈分支。</span><span class="sxs-lookup"><span data-stu-id="821ab-211">Publish the branch.</span></span> <span data-ttu-id="821ab-212">在 [取消發佈的分支] 中選擇分支名稱，然後選擇 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="821ab-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="821ab-213">依預設，只有主要分支的變更才會觸發連續組建。</span><span class="sxs-lookup"><span data-stu-id="821ab-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="821ab-214">若要設定工作分支的連續組建，請在 **Team Explorer** 中選擇 [組建] 頁面，然後選擇 [編輯組建定義]。</span><span class="sxs-lookup"><span data-stu-id="821ab-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="821ab-215">開啟 [來源設定]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="821ab-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="821ab-216">在 [監視連續整合和組建的分支] 下，選擇 [按一下這裡加入新的列]。</span><span class="sxs-lookup"><span data-stu-id="821ab-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="821ab-217">指定您建立的分支，例如 refs/heads/working。</span><span class="sxs-lookup"><span data-stu-id="821ab-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="821ab-218">變更程式碼，開啟已變更之檔案的快顯功能表，然後選擇 [認可] 。</span><span class="sxs-lookup"><span data-stu-id="821ab-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="821ab-219">選擇 [未同步處理的認可] 連結，再選擇 [同步處理] 按鈕或 [推送] 連結，將變更複製到 Visual Studio Team Services 中工作分支的複本。</span><span class="sxs-lookup"><span data-stu-id="821ab-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="821ab-220">瀏覽至 [組建]  檢視，找出工作分支剛觸發的組建。</span><span class="sxs-lookup"><span data-stu-id="821ab-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="821ab-221">後續步驟</span><span class="sxs-lookup"><span data-stu-id="821ab-221">Next steps</span></span>
<span data-ttu-id="821ab-222">如需深入了解有關使用 Git 搭配 Visual Studio Team Services 的祕訣，請參閱[使用 Visual Studio 在 Git 中開發和共用程式碼](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017)；關於使用未受 Visual Studio Team Services 管理的 Git 儲存機制來發佈至 Azure 的詳細資訊，請參閱[持續部署至 Azure App Service](../app-service-web/app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="821ab-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="821ab-223">如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。</span><span class="sxs-lookup"><span data-stu-id="821ab-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
