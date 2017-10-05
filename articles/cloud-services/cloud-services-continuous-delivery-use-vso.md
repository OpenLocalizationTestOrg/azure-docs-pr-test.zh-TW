---
title: "在 Azure 中使用 Visual Studio Team Services 來持續傳遞 | Microsoft Docs"
description: "了解如何設定 Visual Studio Team Services 的 Team 專案，自動建置和部署至 Azure App Service 或雲端服務中的 Web 應用程式功能。"
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="0053c-103">使用 Visual Studio Team Services 連續傳遞至 Azure</span><span class="sxs-lookup"><span data-stu-id="0053c-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="0053c-104">您可以將 Visual Studio Team Services 小組專案設定為自動建置和部署至 Azure Web 應用程式或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0053c-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="0053c-105">(如需如何使用「內部部署」  的 Team Foundation Server 來設定連續組建及部署系統的相關資訊，請參閱 [Azure 中雲端服務的連續傳遞](cloud-services-dotnet-continuous-delivery.md))。</span><span class="sxs-lookup"><span data-stu-id="0053c-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="0053c-106">本教學課程假設您已安裝 Visual Studio 2013 和 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="0053c-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="0053c-107">如果您還沒有 Visual Studio 2013，請至 [www.visualstudio.com](http://www.visualstudio.com) 選擇 [免費開始用] 連結來下載。</span><span class="sxs-lookup"><span data-stu-id="0053c-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="0053c-108">從[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)安裝 Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="0053c-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="0053c-109">您需要 Visual Studio Team Services 帳戶，才能完成本教學課程：您可以 [開啟免費的 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。</span><span class="sxs-lookup"><span data-stu-id="0053c-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="0053c-110">若要使用 Visual Studio Team Services 將雲端服務設定為自動建立和部署至 Azure，請依照下列步驟進行。</span><span class="sxs-lookup"><span data-stu-id="0053c-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="0053c-111">1：建立 Team 專案</span><span class="sxs-lookup"><span data-stu-id="0053c-111">1: Create a team project</span></span>
<span data-ttu-id="0053c-112">請遵循 [這裡](http://go.microsoft.com/fwlink/?LinkId=512980) 的指示來建立您的 Team 專案，並將專案連結至 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0053c-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="0053c-113">本逐步解說假設您使用 Team Foundation 版本控制 (TFVC) 做為原始檔控制解決方案。</span><span class="sxs-lookup"><span data-stu-id="0053c-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="0053c-114">如果您想使用 Git 進行版本控制，請參閱 [本逐步解說的 Git 版本](http://go.microsoft.com/fwlink/p/?LinkId=397358)(英文)。</span><span class="sxs-lookup"><span data-stu-id="0053c-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="0053c-115">2︰將專案簽入原始檔控制</span><span class="sxs-lookup"><span data-stu-id="0053c-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="0053c-116">在 Visual Studio 中，開啟您要部署的方案，或建立新方案。</span><span class="sxs-lookup"><span data-stu-id="0053c-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="0053c-117">您可以依照此逐步解說的步驟部署 Web 應用程式或雲端服務 (Azure 應用程式)。</span><span class="sxs-lookup"><span data-stu-id="0053c-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="0053c-118">如果要建立新方案，請建立新的 Azure 雲端服務專案，或建立新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="0053c-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="0053c-119">請確定專案以 .NET Framework 4 或 4.5 為目標，如果是建立雲端服務專案，請加入 ASP.NET MVC Web 角色和背景工作角色，然後對 Web 角色選擇網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="0053c-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="0053c-120">出現提示時，選擇 [ **網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="0053c-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="0053c-121">如果要建立 Web 應用程式，請選擇 ASP.NET Web 應用程式的專案範本，然後選擇 [MVC]。</span><span class="sxs-lookup"><span data-stu-id="0053c-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="0053c-122">請參閱「 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md)」。</span><span class="sxs-lookup"><span data-stu-id="0053c-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0053c-123">Visual Studio Team Services 目前僅支援 Visual Studio Web 應用程式的 CI 部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="0053c-124">Web Site 專案超出範圍。</span><span class="sxs-lookup"><span data-stu-id="0053c-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="0053c-125">開啟方案的內容功能表，選擇 [將方案加入至原始檔控制] 。</span><span class="sxs-lookup"><span data-stu-id="0053c-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="0053c-126">接受或變更預設值，然後選擇 [確定]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0053c-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="0053c-127">處理完成之後，[方案總管] 中會出現原始檔控制圖示。</span><span class="sxs-lookup"><span data-stu-id="0053c-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="0053c-128">開啟解決方案的捷徑功能表，選擇 [簽入] 。</span><span class="sxs-lookup"><span data-stu-id="0053c-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="0053c-129">在 **Team Explorer** 的 [暫止的變更] 區域中，輸入簽入註解，然後選擇 [簽入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0053c-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="0053c-130">請注意簽入時用來包含或排除特定變更的選項。</span><span class="sxs-lookup"><span data-stu-id="0053c-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="0053c-131">如果已排除您要的變更，請選擇 [全部包含]  。</span><span class="sxs-lookup"><span data-stu-id="0053c-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="0053c-132">3：將專案連線至 Azure</span><span class="sxs-lookup"><span data-stu-id="0053c-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="0053c-133">您現有一個 VS Team Services 小組專案，且裡面有一些原始程式碼，可以準備將小組專案連接至 Azure。</span><span class="sxs-lookup"><span data-stu-id="0053c-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="0053c-134">在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取您的雲端服務或 Web 應用程式，或選取左下方的 **+** 圖示並選擇 [雲端服務] 或 [Web 應用程式]，然後選取 [快速建立]，建立新的雲端服務或 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0053c-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="0053c-135">請選擇 [使用 Visual Studio Team Services 設定發行]  連結。</span><span class="sxs-lookup"><span data-stu-id="0053c-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="0053c-136">在精靈中，於文字方塊中輸入 Visual Studio Team Services 帳戶的名稱，然後按一下 [立即授權]  連結。</span><span class="sxs-lookup"><span data-stu-id="0053c-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="0053c-137">可能會要求您登入。</span><span class="sxs-lookup"><span data-stu-id="0053c-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="0053c-138">在 [連接要求] 快顯對話方塊中，選擇 [接受] 按鈕，以授權 Azure 在 VS Team Services 中設定 Team 專案。</span><span class="sxs-lookup"><span data-stu-id="0053c-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="0053c-139">授權成功時，將出現含有 Visual Studio Team Services 小組專案清單的下拉清單。</span><span class="sxs-lookup"><span data-stu-id="0053c-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="0053c-140">選擇您在先前步驟中建立的小組專案，然後選擇精靈的勾選記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="0053c-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="0053c-141">連結專案之後，將出現一些指示，指出如何將變更簽入至 Visual Studio Team Services 小組專案。</span><span class="sxs-lookup"><span data-stu-id="0053c-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="0053c-142">下次簽入時，Visual Studio Team Services 就會建立專案並部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="0053c-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="0053c-143">現在就試著按一下 [從 Visual Studio 簽入] 連結，再按一下 [啟動 Visual Studio] 連結 (或入口網站畫面底部同等的 [Visual Studio] 按鈕)。</span><span class="sxs-lookup"><span data-stu-id="0053c-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="0053c-144">4：觸發重建和重新部署專案</span><span class="sxs-lookup"><span data-stu-id="0053c-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="0053c-145">在 Visual Studio 的 **Team Explorer** 中，選擇 [原始檔控制總管] 連結。</span><span class="sxs-lookup"><span data-stu-id="0053c-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="0053c-146">瀏覽至方案檔並開啟。</span><span class="sxs-lookup"><span data-stu-id="0053c-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="0053c-147">在 [方案總管] 中，開啟檔案進行變更。</span><span class="sxs-lookup"><span data-stu-id="0053c-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="0053c-148">例如，在 MVC Web 角色中，變更 Views\\Shared 資料夾下的 `_Layout.cshtml` 檔案。</span><span class="sxs-lookup"><span data-stu-id="0053c-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="0053c-149">編輯網站的標誌，然後選擇 **Ctrl+S** 儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="0053c-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="0053c-150">在 **Team Explorer** 中，選擇 [暫止的變更] 連結。</span><span class="sxs-lookup"><span data-stu-id="0053c-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="0053c-151">輸入註解，然後選擇 [簽入]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0053c-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="0053c-152">選擇 [首頁] 按鈕回到 **Team Explorer** 首頁。</span><span class="sxs-lookup"><span data-stu-id="0053c-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="0053c-153">選擇 [組建]  連結來檢視進行中的組件。</span><span class="sxs-lookup"><span data-stu-id="0053c-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="0053c-154">**Team Explorer** 會顯示簽入已觸發的組建。</span><span class="sxs-lookup"><span data-stu-id="0053c-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="0053c-155">按兩下進行中的組建名稱，檢視進行中組建的詳細記錄。</span><span class="sxs-lookup"><span data-stu-id="0053c-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="0053c-156">當組建進行時，查看您使用精靈將 TFS 連結至 Azure 時所建立的組建定義。</span><span class="sxs-lookup"><span data-stu-id="0053c-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="0053c-157">開啟組建定義的捷徑功能表，然後選擇 [編輯組建定義] 。</span><span class="sxs-lookup"><span data-stu-id="0053c-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="0053c-158">在 [觸發程序]  索引標籤中，您會看到已設為依預設每次簽入時建置的組建定義。</span><span class="sxs-lookup"><span data-stu-id="0053c-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="0053c-159">在 [處理序]  索引標籤中，您可以看到部署環境已設為您的雲端服務或 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="0053c-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="0053c-160">如果您使用的是 Web 應用程式，則顯示的屬性跟下面的屬性不同。</span><span class="sxs-lookup"><span data-stu-id="0053c-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="0053c-161">如果不想要使用預設值，請指定屬性的值。</span><span class="sxs-lookup"><span data-stu-id="0053c-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="0053c-162">Azure 發行屬性在 [部署]  區段中。</span><span class="sxs-lookup"><span data-stu-id="0053c-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="0053c-163">下表顯示 [部署]  區段中可用的屬性：</span><span class="sxs-lookup"><span data-stu-id="0053c-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="0053c-164">屬性</span><span class="sxs-lookup"><span data-stu-id="0053c-164">Property</span></span> | <span data-ttu-id="0053c-165">預設值</span><span class="sxs-lookup"><span data-stu-id="0053c-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0053c-166">允許未受信任的憑證</span><span class="sxs-lookup"><span data-stu-id="0053c-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="0053c-167">如果為 false，SSL 憑證必須經過根授權單位簽署。</span><span class="sxs-lookup"><span data-stu-id="0053c-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="0053c-168">允許升級</span><span class="sxs-lookup"><span data-stu-id="0053c-168">Allow Upgrade</span></span> |<span data-ttu-id="0053c-169">允許部署更新現有的部署而非建立新的部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="0053c-170">保留 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0053c-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="0053c-171">不要刪除</span><span class="sxs-lookup"><span data-stu-id="0053c-171">Do Not Delete</span></span> |<span data-ttu-id="0053c-172">如果為 true，則不要覆寫現有不相關的部署 (允許升級)。</span><span class="sxs-lookup"><span data-stu-id="0053c-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="0053c-173">部署設定的路徑</span><span class="sxs-lookup"><span data-stu-id="0053c-173">Path to Deployment Settings</span></span> |<span data-ttu-id="0053c-174">Web 應用程式的 .pubxml 檔的路徑，這是儲存機制之根資料夾的相對路徑。</span><span class="sxs-lookup"><span data-stu-id="0053c-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="0053c-175">雲端服務則會忽略。</span><span class="sxs-lookup"><span data-stu-id="0053c-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="0053c-176">SharePoint 部署環境</span><span class="sxs-lookup"><span data-stu-id="0053c-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="0053c-177">與服務名稱相同。</span><span class="sxs-lookup"><span data-stu-id="0053c-177">The same as the service name.</span></span> |
    | <span data-ttu-id="0053c-178">Azure 部署環境</span><span class="sxs-lookup"><span data-stu-id="0053c-178">Azure Deployment Environment</span></span> |<span data-ttu-id="0053c-179">Web 應用程式或雲端服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="0053c-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="0053c-180">如果使用多個服務組態 (.cscfg 檔)，則可以在 [組建、進階、MSBuild 引數]  設定中指定所需的服務組態。</span><span class="sxs-lookup"><span data-stu-id="0053c-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="0053c-181">例如，若要使用 ServiceConfiguration.Test.cscfg，請設定 MSBuild 引數的命令列選項 `/p:TargetProfile=Test`。</span><span class="sxs-lookup"><span data-stu-id="0053c-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="0053c-182">現在應該已順利完成您的組建。</span><span class="sxs-lookup"><span data-stu-id="0053c-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="0053c-183">如果按兩下組建名稱，Visual Studio 會顯示 [組建摘要] ，包括與單元測試專案相關聯的任何測試結果。</span><span class="sxs-lookup"><span data-stu-id="0053c-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="0053c-184">在 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)中，選取預備環境之後，您可以在 [部署] 索引標籤上檢視相關聯的部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="0053c-185">瀏覽至網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="0053c-185">Browse to your site's URL.</span></span> <span data-ttu-id="0053c-186">若是 Web 應用程式，請按一下命令列的 [瀏覽] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0053c-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="0053c-187">若是雲端服務，請在 [儀表板] 頁面的 [快速概覽] 區段中選擇 URL，以顯示雲端服務的預備環境。</span><span class="sxs-lookup"><span data-stu-id="0053c-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="0053c-188">依預設，來自雲端服務連續整合的部署會發佈至預備環境。</span><span class="sxs-lookup"><span data-stu-id="0053c-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="0053c-189">您可以將 [替代雲端服務環境] 屬性設為 [生產] 來變更此設定。</span><span class="sxs-lookup"><span data-stu-id="0053c-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="0053c-190">此擷取畫面顯示網站 URL 在雲端服務儀表板頁面上的位置。</span><span class="sxs-lookup"><span data-stu-id="0053c-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="0053c-191">新的瀏覽器索引標籤會開啟來顯示您執行中的網站。</span><span class="sxs-lookup"><span data-stu-id="0053c-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="0053c-192">若為雲端服務，如果對專案進行其他變更，則會觸發更多組建，將累積多個部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="0053c-193">最後一個會標示為「作用中」。</span><span class="sxs-lookup"><span data-stu-id="0053c-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="0053c-194">5：重新部署舊版組建</span><span class="sxs-lookup"><span data-stu-id="0053c-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="0053c-195">此步驟適用於雲端服務，且為選用的。</span><span class="sxs-lookup"><span data-stu-id="0053c-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="0053c-196">在 Azure 傳統入口網站中，選擇先前的部署，然後選擇 [重新部署]  按鈕，將網站倒回到更早的簽入。</span><span class="sxs-lookup"><span data-stu-id="0053c-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="0053c-197">請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。</span><span class="sxs-lookup"><span data-stu-id="0053c-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="0053c-198">6：變更生產部署</span><span class="sxs-lookup"><span data-stu-id="0053c-198">6: Change the Production deployment</span></span>
<span data-ttu-id="0053c-199">此步驟僅適用於雲端服務，不適用於 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0053c-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="0053c-200">準備就緒後，您可以在 Azure 傳統入口網站中選擇 [交換]  按鈕，將預備環境升級至生產環境。</span><span class="sxs-lookup"><span data-stu-id="0053c-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="0053c-201">新部署的預備環境會升級至「生產」，而先前的生產環境 (若有的話) 會變成預備環境。</span><span class="sxs-lookup"><span data-stu-id="0053c-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="0053c-202">「作用中」部署可能與生產和預備環境不同，但最近組建的部署歷程記錄都一樣，與環境無關。</span><span class="sxs-lookup"><span data-stu-id="0053c-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="0053c-203">7：執行單元測試</span><span class="sxs-lookup"><span data-stu-id="0053c-203">7: Run unit tests</span></span>
<span data-ttu-id="0053c-204">此步驟僅適用於 Web 應用程式，不適用於雲端服務。</span><span class="sxs-lookup"><span data-stu-id="0053c-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="0053c-205">若要為部署的品質把關，您可以執行單元測試；如果測試失敗，則可以停止部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="0053c-206">在 Visual Studio 中，加入單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="0053c-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="0053c-207">將專案參考加入您要測試的專案。</span><span class="sxs-lookup"><span data-stu-id="0053c-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="0053c-208">加入一些單元測試。</span><span class="sxs-lookup"><span data-stu-id="0053c-208">Add some unit tests.</span></span> <span data-ttu-id="0053c-209">若要開始使用，請嘗試一律會通過的虛擬測試。</span><span class="sxs-lookup"><span data-stu-id="0053c-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="0053c-210">編輯組建定義，選擇 [處理序] 索引標籤，然後展開 [測試] 節點。</span><span class="sxs-lookup"><span data-stu-id="0053c-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="0053c-211">將 [在測試失敗時使組建失敗]  設為 True。</span><span class="sxs-lookup"><span data-stu-id="0053c-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="0053c-212">換句話說，除非通過測試，否則不會進行部署。</span><span class="sxs-lookup"><span data-stu-id="0053c-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="0053c-213">將新組建排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0053c-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="0053c-214">在建置進行時，檢查其進度。</span><span class="sxs-lookup"><span data-stu-id="0053c-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="0053c-215">在建置完成時，檢查測試結果。</span><span class="sxs-lookup"><span data-stu-id="0053c-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="0053c-216">嘗試建立將失敗的測試。</span><span class="sxs-lookup"><span data-stu-id="0053c-216">Try creating a test that will fail.</span></span> <span data-ttu-id="0053c-217">透過複製第一個測試、將其重新命名，並將 NotImplementedException 標記為預期的例外狀況的程式碼行加上註解，來加入新的測試。</span><span class="sxs-lookup"><span data-stu-id="0053c-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="0053c-218">簽入變更，以將新組建排入佇列。</span><span class="sxs-lookup"><span data-stu-id="0053c-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="0053c-219">檢視測試結果，以查看失敗的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0053c-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="0053c-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0053c-220">Next steps</span></span>
<span data-ttu-id="0053c-221">如需在 Visual Studio Team Services 中進行單元測試的詳細資訊，請參閱 [在建置中執行單元測試](http://go.microsoft.com/fwlink/p/?LinkId=510474)。</span><span class="sxs-lookup"><span data-stu-id="0053c-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="0053c-222">如果您使用的是 Git，請參閱[在 Git 中共用程式碼](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx)和[持續部署至 Azure App Service](../app-service-web/app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0053c-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="0053c-223">如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。</span><span class="sxs-lookup"><span data-stu-id="0053c-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
