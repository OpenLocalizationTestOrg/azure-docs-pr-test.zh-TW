---
title: "在 Azure 中的 Visual Studio Team Services 與 aaaContinuous 傳遞 |Microsoft 文件"
description: "了解如何 tooconfigure Visual Studio Team Services 的 team 的專案 tooautomatically 建置和部署 Azure 應用程式服務或雲端服務中的 toohello Web 應用程式功能。"
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
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="1d9e2-103">使用 Visual Studio Team Services 的持續傳遞 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d9e2-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="1d9e2-104">您可以設定 Visual Studio Team Services 團隊專案 tooautomatically 組建和部署 tooAzure web 應用程式或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="1d9e2-105">(如需有關如何 tooset 連續的組建及部署使用系統資訊*內部*Team Foundation Server，請參閱[Azure 雲端服務的持續傳遞](cloud-services-dotnet-continuous-delivery.md)。)</span><span class="sxs-lookup"><span data-stu-id="1d9e2-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="1d9e2-106">本教學課程假設您有 Visual Studio 2013 和 Azure SDK 安裝 hello。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="1d9e2-107">如果您還沒有 Visual Studio 2013，下載選擇 hello**免費開始**連結[www.visualstudio.com](http://www.visualstudio.com)。安裝 hello 從 Azure SDK[這裡](http://go.microsoft.com/fwlink/?LinkId=239540)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="1d9e2-108">本教學課程需要 Visual Studio Team Services 帳戶 toocomplete： 您可以[免費開啟 Visual Studio Team Services 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=512979)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="1d9e2-109">設定雲端服務 tooautomatically tooset 建置和部署使用 Visual Studio Team Services tooAzure，依照下列步驟。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="1d9e2-110">1：建立 Team 專案</span><span class="sxs-lookup"><span data-stu-id="1d9e2-110">1: Create a team project</span></span>
<span data-ttu-id="1d9e2-111">遵循 hello[這裡](http://go.microsoft.com/fwlink/?LinkId=512980)toocreate 您 team 專案，並將它連結 tooVisual Studio。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="1d9e2-112">本逐步解說假設您使用 Team Foundation 版本控制 (TFVC) 做為原始檔控制解決方案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="1d9e2-113">如果您想 toouse Git 進行版本控制，請參閱[本逐步解說的 hello Git 版本](http://go.microsoft.com/fwlink/p/?LinkId=397358)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="1d9e2-114">2： 檢查專案 toosource 控制項中</span><span class="sxs-lookup"><span data-stu-id="1d9e2-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="1d9e2-115">在 Visual Studio 中，開啟您想要 toodeploy，或建立一個新的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="1d9e2-116">您可以將 web 應用程式部署或雲端服務 （Azure 應用程式），由下列 hello 步驟在本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="1d9e2-117">如果您想 toocreate 新方案，建立新的 Azure 雲端服務專案或新的 ASP.NET MVC 專案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="1d9e2-118">請確定 hello 專案目標.NET Framework 4 或 4.5，而且如果您要建立雲端服務專案，加入 ASP.NET MVC web 角色和背景工作角色，然後選擇 hello web 角色的網際網路應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="1d9e2-119">出現提示時，選擇 [ **網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="1d9e2-120">如果您想 toocreate web 應用程式中，選擇 hello ASP.NET Web 應用程式專案範本，然後選擇 MVC。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="1d9e2-121">請參閱「 [在 Azure App Service 中建立 ASP.NET Web 應用程式](../app-service-web/app-service-web-get-started-dotnet.md)」。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1d9e2-122">Visual Studio Team Services 目前僅支援 Visual Studio Web 應用程式的 CI 部署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="1d9e2-123">Web Site 專案超出範圍。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="1d9e2-124">開啟 hello hello 方案的內容功能表並選擇 **將方案加入 tooSource 控制項**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="1d9e2-125">接受或變更 hello 預設值，以及選擇 hello**確定** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="1d9e2-126">Hello 程序完成之後，原始檔控制圖示會出現在**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="1d9e2-127">開啟 hello hello 方案的捷徑功能表並選擇 **簽入**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="1d9e2-128">在 hello**暫止的變更**區域**Team Explorer**、 輸入 hello 簽入註解，然後選擇 hello**簽入**按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="1d9e2-129">請注意 hello 選項 tooinclude 或排除特定的變更，當您簽入。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="1d9e2-130">如果想要排除的變更，請選擇 hello**全部包含**連結。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="1d9e2-131">3： 連接 hello 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d9e2-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="1d9e2-132">現在您有一些原始程式碼的 VS Team Services team 專案中，您就準備好 tooconnect 您的小組專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="1d9e2-133">在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，選取 雲端服務或 web 應用程式，或建立一個新選擇 hello  **+**  hello 左下方，然後選擇圖示**的雲端服務**或**Web 應用程式**然後**快速建立**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="1d9e2-134">選擇 hello**設定發行與 Visual Studio Team Services**連結。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="1d9e2-135">在 hello 精靈中，輸入 hello 您的 Visual Studio Team Services 帳戶名稱在 hello 文字方塊中，按一下 hello**現在授權**連結。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="1d9e2-136">您可能會要求 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="1d9e2-137">在 hello**連線要求**快顯對話方塊中，選擇 hello**接受**按鈕 tooauthorize Azure tooconfigure 您的小組專案 VS Team Services 中。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="1d9e2-138">授權成功時，將出現含有 Visual Studio Team Services 小組專案清單的下拉清單。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="1d9e2-139">選擇 hello hello 先前步驟中，在您建立 team 專案名稱，然後選擇 hello 精靈的核取記號按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="1d9e2-140">您的專案連結之後，您會看到一些簽入變更 tooyour Visual Studio Team Services 的 team 專案的指示。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="1d9e2-141">在您下一步簽入時，Visual Studio Team Services 將會建置並部署專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="1d9e2-142">再試一次按一下 hello 現在這個**簽入從 Visual Studio**連結，然後再 hello**啟動 Visual Studio**連結 (或對等的 hello **Visual Studio**在 hello 底部的按鈕hello 入口網站畫面）。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="1d9e2-143">4：觸發重建和重新部署專案</span><span class="sxs-lookup"><span data-stu-id="1d9e2-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="1d9e2-144">在 Visual Studio 的**Team Explorer**，選擇 hello**原始檔控制總管**連結。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="1d9e2-145">瀏覽 tooyour 方案檔，並將它開啟。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="1d9e2-146">在 [方案總管] 中，開啟檔案進行變更。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="1d9e2-147">例如，變更 hello 檔案`_Layout.cshtml`hello 檢視下\\MVC web 角色中的共用資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="1d9e2-148">編輯 hello 站台的 hello 標誌，然後選擇  **Ctrl + S** toosave hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="1d9e2-149">在**Team Explorer**，選擇 hello**暫止的變更**連結。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="1d9e2-150">輸入註解，然後選擇 [hello**簽入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="1d9e2-151">選擇 hello**家用**按鈕 tooreturn toohello **Team Explorer**首頁。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="1d9e2-152">選擇 hello**建置**連結 tooview hello 建置進行中。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="1d9e2-153">**Team Explorer** 會顯示簽入已觸發的組建。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="1d9e2-154">按兩下 hello 進度 tooview 詳細的記錄檔中的 hello 組建名稱 hello 組建進行。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="1d9e2-155">進行中 hello 組建時，看看您連結 TFS tooAzure 使用 hello 精靈時所建立的 hello 組建定義。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="1d9e2-156">開啟 hello hello 組建定義的捷徑功能表並選擇 **編輯組建定義**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="1d9e2-157">在 hello**觸發程序**索引標籤上，您會看到 hello 組建定義設定在每個簽入 toobuild 預設。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="1d9e2-158">在 hello**程序**索引標籤上，您可以看到 hello 部署環境設定的雲端服務或 web 應用程式的 toohello 名稱。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="1d9e2-159">如果您正在使用 web 應用程式，您會看到 hello 屬性將會與不同如下所示。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="1d9e2-160">如果您想要比 hello 預設值不同的值，指定 hello 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="1d9e2-161">hello 屬性 Azure 發行會在 hello**部署**> 一節。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="1d9e2-162">hello 下列資料表顯示 hello 可用的屬性中 hello**部署**> 一節：</span><span class="sxs-lookup"><span data-stu-id="1d9e2-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="1d9e2-163">屬性</span><span class="sxs-lookup"><span data-stu-id="1d9e2-163">Property</span></span> | <span data-ttu-id="1d9e2-164">預設值</span><span class="sxs-lookup"><span data-stu-id="1d9e2-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1d9e2-165">允許未受信任的憑證</span><span class="sxs-lookup"><span data-stu-id="1d9e2-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="1d9e2-166">如果為 false，SSL 憑證必須經過根授權單位簽署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="1d9e2-167">允許升級</span><span class="sxs-lookup"><span data-stu-id="1d9e2-167">Allow Upgrade</span></span> |<span data-ttu-id="1d9e2-168">可讓 hello 部署 tooupdate 而不是建立一個新現有的部署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="1d9e2-169">會保留 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="1d9e2-170">不要刪除</span><span class="sxs-lookup"><span data-stu-id="1d9e2-170">Do Not Delete</span></span> |<span data-ttu-id="1d9e2-171">如果為 true，則不要覆寫現有不相關的部署 (允許升級)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="1d9e2-172">路徑 tooDeployment 設定</span><span class="sxs-lookup"><span data-stu-id="1d9e2-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="1d9e2-173">hello 路徑 tooyour.pubxml 檔案是 web 應用程式，相對 toohello hello 儲存機制根資料夾。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="1d9e2-174">雲端服務則會忽略。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="1d9e2-175">SharePoint 部署環境</span><span class="sxs-lookup"><span data-stu-id="1d9e2-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="1d9e2-176">hello 與 hello 服務名稱的相同。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="1d9e2-177">Azure 部署環境</span><span class="sxs-lookup"><span data-stu-id="1d9e2-177">Azure Deployment Environment</span></span> |<span data-ttu-id="1d9e2-178">hello web 應用程式或雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="1d9e2-179">如果您使用多個服務組態 （.cscfg 檔），您可以指定 hello 所需的服務組態中 hello**建置，進階，MSBuild 引數**設定。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="1d9e2-180">例如，toouse ServiceConfiguration.Test.cscfg，會設定 MSBuild 引數行選項`/p:TargetProfile=Test`。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="1d9e2-181">現在應該已順利完成您的組建。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="1d9e2-182">如果您按兩下 hello 組建名稱時，Visual Studio 會顯示**組建摘要**，包括中的任何測試結果相關聯的單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="1d9e2-183">在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)，您可以檢視相關聯的 hello 部署上 hello**部署**索引標籤上，選取 預備環境的 hello 時。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="1d9e2-184">瀏覽 tooyour 網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="1d9e2-185">Web 應用程式中，只要按一下 hello**瀏覽**hello 命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="1d9e2-186">雲端服務中，選擇 hello URL 在 hello**快速概覽**區段 hello**儀表板**顯示 hello 預備環境的雲端服務的頁面。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="1d9e2-187">從雲端服務的持續整合的部署都是預設的已發行的 toohello 預備環境。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="1d9e2-188">您可以變更此設定 hello**替代雲端服務環境**屬性太**生產**。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="1d9e2-189">這個螢幕擷取畫面會顯示在 hello 網站 URL 是 hello 雲端服務的儀表板頁面上。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="1d9e2-190">新的瀏覽器索引標籤會開啟 tooreveal 您執行的網站。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="1d9e2-191">雲端服務，如果您進行其他變更 tooyour 專案時，更建置您的觸發程序，和您將會累積多個部署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="1d9e2-192">hello 最新標示為 使用。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="1d9e2-193">5：重新部署舊版組建</span><span class="sxs-lookup"><span data-stu-id="1d9e2-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="1d9e2-194">這個步驟適用於 toocloud 服務，並為選擇性。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="1d9e2-195">在 hello Azure 傳統入口網站中，選擇先前的部署，然後選擇 hello**重新部署**按鈕 toorewind 簽入之前您站台 tooan。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="1d9e2-196">請注意，這會在 TFS 中觸發新的組建，並在部署歷程記錄中建立新的項目。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="1d9e2-197">6： 變更 hello 生產環境部署</span><span class="sxs-lookup"><span data-stu-id="1d9e2-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="1d9e2-198">這個步驟適用於只有 toocloud 服務，不適用於 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="1d9e2-199">當您準備好時，您可以藉由選擇 hello 升級 hello 臨時 toohello 生產環境**交換**hello Azure 傳統入口網站中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="1d9e2-200">新部署的 hello 臨時環境是已升級的 tooProduction 而 hello 先前生產環境中，如果有的話，會變成預備環境。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="1d9e2-201">hello 作用中的部署可能會不同 hello 生產與預備環境，但最近組建 hello 部署歷程記錄是 hello 相同的環境而定。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="1d9e2-202">7：執行單元測試</span><span class="sxs-lookup"><span data-stu-id="1d9e2-202">7: Run unit tests</span></span>
<span data-ttu-id="1d9e2-203">這個步驟適用於只有 tooweb 應用程式，不是雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="1d9e2-204">tooput 品質把關上您的部署，您可以執行單元測試，以及如果他們，您可以停止 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="1d9e2-205">在 Visual Studio 中，加入單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="1d9e2-206">新增您想要 tootest 專案參考 toohello 專案。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="1d9e2-207">加入一些單元測試。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-207">Add some unit tests.</span></span> <span data-ttu-id="1d9e2-208">tooget 啟動，請一律會在傳遞的 dummy 測試。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-208">tooget started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="1d9e2-209">編輯 hello 組建定義中，選擇 hello**程序**索引標籤，然後展開 hello**測試**節點。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="1d9e2-210">設定 hello**在測試失敗時使組建**tooTrue。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="1d9e2-211">這表示除非 hello 測試成功，就不會執行 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="1d9e2-212">將新組建排入佇列。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="1d9e2-213">而繼續 hello 組建，檢查其進度。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="1d9e2-214">Hello 組建完成時，請檢查 hello 測試結果。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="1d9e2-215">嘗試建立將失敗的測試。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-215">Try creating a test that will fail.</span></span> <span data-ttu-id="1d9e2-216">藉由複製 hello 第一個加入新的測試、 重新命名，並註解化 hello 說明 NotImplementedException 沒有預期的例外狀況的程式碼行。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="1d9e2-217">Hello 的簽入變更 tooqueue 新組建。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="1d9e2-218">檢視 hello 測試結果 toosee 詳細 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="1d9e2-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d9e2-219">Next steps</span></span>
<span data-ttu-id="1d9e2-220">如需在 Visual Studio Team Services 中進行單元測試的詳細資訊，請參閱 [在建置中執行單元測試](http://go.microsoft.com/fwlink/p/?LinkId=510474)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="1d9e2-221">如果您使用 Git，請參閱[共用程式碼在 Git 中的](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx)和[連續部署 tooAzure App Service](../app-service-web/app-service-continuous-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="1d9e2-222">如需 Visual Studio Team Services 的詳細資訊，請參閱 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。</span><span class="sxs-lookup"><span data-stu-id="1d9e2-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
