---
title: "開始使用 Azure 雲端服務和 ASP.NET 的 aaaGet |Microsoft 文件"
description: "深入了解如何 toocreate 使用 ASP.NET MVC 和 Azure 的多層式應用程式。 hello 應用程式會在雲端服務中，使用 web 角色和背景工作角色執行。 它使用 Entity Framework、SQL Database 及 Azure 儲存體佇列和 Blob。"
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="321c7-105">開始使用 Azure 雲端服務和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="321c7-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="321c7-106">概觀</span><span class="sxs-lookup"><span data-stu-id="321c7-106">Overview</span></span>
<span data-ttu-id="321c7-107">本教學課程示範如何 toocreate 多層.NET 應用程式與 ASP.NET MVC 前端伺服器上，並將其部署 tooan [Azure 雲端服務](cloud-services-choose-me.md)。</span><span class="sxs-lookup"><span data-stu-id="321c7-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="321c7-108">hello 應用程式會使用[Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)，hello [Azure Blob 服務](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，和 hello [Azure 佇列服務](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)。</span><span class="sxs-lookup"><span data-stu-id="321c7-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="321c7-109">您可以[下載 hello Visual Studio 專案](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)從 MSDN Code Gallery hello。</span><span class="sxs-lookup"><span data-stu-id="321c7-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="321c7-110">hello 教學課程會示範如何 toobuild 和執行 hello 本機應用程式，如何 toodeploy 它 tooAzure 和執行中的 hello 雲端，以及如何 toobuild 從頭它。</span><span class="sxs-lookup"><span data-stu-id="321c7-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="321c7-111">您可以啟動從頭建置和執行 hello 測試並部署步驟之後，如果您偏好。</span><span class="sxs-lookup"><span data-stu-id="321c7-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="321c7-112">Contoso Ads 應用程式</span><span class="sxs-lookup"><span data-stu-id="321c7-112">Contoso Ads application</span></span>
<span data-ttu-id="321c7-113">hello 應用程式是廣告電子佈告欄。</span><span class="sxs-lookup"><span data-stu-id="321c7-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="321c7-114">使用者透過輸入文字和上傳影像來建立廣告。</span><span class="sxs-lookup"><span data-stu-id="321c7-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="321c7-115">使用者可以查看清單的廣告以縮圖影像，以及使用者可以看見 hello 完整大小的影像時，它們會選取 ad toosee hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="321c7-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Ad list](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="321c7-117">hello 應用程式會使用 hello[佇列為主的工作模式](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)toooff 負載 hello CPU 運算密集工作建立縮圖 tooa 後端程序。</span><span class="sxs-lookup"><span data-stu-id="321c7-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="321c7-118">替代架構：網站和 WebJobs</span><span class="sxs-lookup"><span data-stu-id="321c7-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="321c7-119">本教學課程示範如何 toorun 前端和後端 Azure 中雲端服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="321c7-120">替代方式是在前端 toorun hello [Azure 網站](/services/web-sites/)並用 hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello 後端 （目前處於預覽階段） 功能。</span><span class="sxs-lookup"><span data-stu-id="321c7-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="321c7-121">使用 WebJobs 教學課程中，請參閱[hello Azure WebJobs SDK 快速入門](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="321c7-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="321c7-122">如資訊如何 toochoose hello 服務最符合您的案例，請參閱 < [Azure 網站、 雲端服務和虛擬機器的比較](../app-service-web/choose-web-site-cloud-service-vm.md)。</span><span class="sxs-lookup"><span data-stu-id="321c7-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="321c7-123">您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="321c7-123">What you'll learn</span></span>
* <span data-ttu-id="321c7-124">如何 tooenable 電腦所安裝的 Azure 開發 hello Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="321c7-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="321c7-125">如何 toocreate Visual Studio 將雲端服務專案，使用 ASP.NET MVC web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="321c7-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="321c7-126">如何 tootest hello 雲端服務專案在本機，使用 hello Azure 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="321c7-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="321c7-127">如何 toopublish hello 雲端專案 tooan Azure 雲端服務，並測試使用的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="321c7-128">如何 tooupload 檔案，並將其儲存在 hello Azure Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="321c7-129">如何 toouse hello Azure 佇列服務各層之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="321c7-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="321c7-130">必要條件</span><span class="sxs-lookup"><span data-stu-id="321c7-130">Prerequisites</span></span>
<span data-ttu-id="321c7-131">hello 教學課程假設您已了解[Azure 的基本概念的雲端服務](cloud-services-choose-me.md)例如*web 角色*和*背景工作角色*術語。</span><span class="sxs-lookup"><span data-stu-id="321c7-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="321c7-132">它也假設您知道如何與 toowork [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)或[Web Form](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio 中的專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="321c7-133">hello 範例應用程式使用 MVC 中，但大部分的 hello 教學課程也適用於 tooWeb 表單。</span><span class="sxs-lookup"><span data-stu-id="321c7-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="321c7-134">您可以執行 Azure 訂用帳戶中，未使用在本機的 hello 應用程式，但是您將需要一個 toodeploy hello 應用程式 toohello 雲端。</span><span class="sxs-lookup"><span data-stu-id="321c7-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="321c7-135">如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668)或是[申請免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)。</span><span class="sxs-lookup"><span data-stu-id="321c7-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="321c7-136">hello 教學課程的指示運作 hello 下列產品的其中一種：</span><span class="sxs-lookup"><span data-stu-id="321c7-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="321c7-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="321c7-137">Visual Studio 2013</span></span>
* <span data-ttu-id="321c7-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="321c7-138">Visual Studio 2015</span></span>
* <span data-ttu-id="321c7-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="321c7-139">Visual Studio 2017</span></span>

<span data-ttu-id="321c7-140">如果您沒有下列其中一種，Visual Studio 可能會自動安裝時安裝 hello Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="321c7-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="321c7-141">應用程式架構</span><span class="sxs-lookup"><span data-stu-id="321c7-141">Application architecture</span></span>
<span data-ttu-id="321c7-142">hello 應用程式會儲存在 SQL 資料庫中，使用 Entity Framework Code First toocreate hello 資料表和存取 hello 資料廣告。</span><span class="sxs-lookup"><span data-stu-id="321c7-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="321c7-143">每個廣告，hello 資料庫存放區兩個 Url，一個用於 hello 完整大小的影像，另一個用於 hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="321c7-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="321c7-145">當使用者上傳映像時，hello 前端執行的 web 角色中會儲存中的 hello 映像[Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，而且會儲存點 toohello blob 的 url hello 資料庫中的 hello ad 資訊。</span><span class="sxs-lookup"><span data-stu-id="321c7-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="321c7-146">在 hello 相同時間，它會將訊息 tooan Azure 佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="321c7-147">定期執行背景工作角色中的後端程序就會輪詢 hello 新訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="321c7-148">新的訊息出現時，hello 背景工作角色建立該映像的縮圖，並更新 hello 該廣告的縮圖 URL 資料庫欄位。</span><span class="sxs-lookup"><span data-stu-id="321c7-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="321c7-149">hello 下列圖表顯示 hello 部分 hello 應用程式互動的方式。</span><span class="sxs-lookup"><span data-stu-id="321c7-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="321c7-151">下載並執行已完成的 hello 方案</span><span class="sxs-lookup"><span data-stu-id="321c7-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="321c7-152">下載並解壓縮 hello[完成方案](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)。</span><span class="sxs-lookup"><span data-stu-id="321c7-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="321c7-153">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="321c7-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="321c7-154">從 hello**檔案**功能表中選擇 **開啟專案**，瀏覽 toowhere 下載 hello 方案，並開啟 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="321c7-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="321c7-155">按 CTRL + SHIFT + B toobuild hello 方案。</span><span class="sxs-lookup"><span data-stu-id="321c7-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="321c7-156">根據預設，Visual Studio 會自動還原 hello NuGet 套件的內容，其中未包含在 hello *.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="321c7-157">如果未還原 hello 套件，安裝這些手動移 toohello**管理方案的 NuGet 套件** 對話方塊，然後按一下 hello**還原**在 hello 右上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="321c7-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="321c7-158">在**方案總管 中**，請確定**ContosoAdsCloudService**選取為 hello 啟始專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="321c7-159">如果您使用 Visual Studio 2015 或更新版本中，變更 hello 應用程式中的 hello SQL Server 連接字串*Web.config*檔案 hello ContosoAdsWeb 專案並在 hello *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService 專案檔。</span><span class="sxs-lookup"><span data-stu-id="321c7-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="321c7-160">在每個案例中，變更 」 (localdb) \v11.0 」 太 」 (localdb) \MSSQLLocalDB"。</span><span class="sxs-lookup"><span data-stu-id="321c7-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="321c7-161">按 CTRL + F5 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="321c7-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="321c7-162">當您在本機執行雲端服務專案時，Visual Studio 自動叫用 hello Azure*計算模擬器*和 Azure*儲存體模擬器*。</span><span class="sxs-lookup"><span data-stu-id="321c7-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="321c7-163">hello 計算模擬器會使用您的電腦資源 toosimulate hello web 角色和背景工作角色環境。</span><span class="sxs-lookup"><span data-stu-id="321c7-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="321c7-164">hello 儲存體模擬器會使用[SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx)資料庫 toosimulate Azure 雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="321c7-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="321c7-165">hello 第一次執行雲端服務專案所需約一分鐘 hello 模擬器 toostart 組成。</span><span class="sxs-lookup"><span data-stu-id="321c7-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="321c7-166">模擬器啟動完成時，hello 預設瀏覽器會開啟 toohello 應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="321c7-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Contoso Ads architecture](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="321c7-168">按一下 [建立廣告]。</span><span class="sxs-lookup"><span data-stu-id="321c7-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="321c7-169">輸入一些測試資料，並選取*.jpg* tooupload 的映像，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="321c7-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="321c7-171">hello 應用程式 toohello 索引頁面上，但它不會顯示 hello 新 ad 縮圖，因為該處理尚未尚未發生。</span><span class="sxs-lookup"><span data-stu-id="321c7-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="321c7-172">稍候片刻，然後重新整理 hello 索引頁面 toosee hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="321c7-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![索引頁面](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="321c7-174">按一下**詳細資料**ad toosee hello 全尺寸映像。</span><span class="sxs-lookup"><span data-stu-id="321c7-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Details page](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="321c7-176">您已完全在本機電腦沒有連線 toohello 雲端上執行 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="321c7-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="321c7-177">hello 儲存體模擬器儲存 hello 佇列和 SQL Server Express LocalDB 資料庫和 hello 應用程式中的 blob 資料儲存在另一個 LocalDB 資料庫 hello ad 資料。</span><span class="sxs-lookup"><span data-stu-id="321c7-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="321c7-178">Entity Framework Code First 自動建立的 hello ad 資料庫 hello hello web 應用程式嘗試 tooaccess 的第一次它。</span><span class="sxs-lookup"><span data-stu-id="321c7-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="321c7-179">Hello 下列區段中，您需要設定 hello 方案 toouse Azure 雲端資源的佇列、 blob 和 hello 應用程式資料庫 hello 雲端中執行時進行。</span><span class="sxs-lookup"><span data-stu-id="321c7-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="321c7-180">如果您想要在本機 toocontinue toorun，但使用雲端儲存體和資料庫資源，您可以執行。</span><span class="sxs-lookup"><span data-stu-id="321c7-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="321c7-181">它是只需設定連接字串，您會看到如何 toodo。</span><span class="sxs-lookup"><span data-stu-id="321c7-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="321c7-182">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="321c7-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="321c7-183">您將會執行 hello 遵循 hello 雲端中的步驟 toorun hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="321c7-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="321c7-184">建立 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="321c7-185">建立 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="321c7-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="321c7-186">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="321c7-187">在 Azure 中執行時設定 hello 方案 toouse Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="321c7-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="321c7-188">在 Azure 中執行時設定 hello 方案 toouse Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="321c7-189">將 hello 專案 tooyour Azure 雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="321c7-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="321c7-190">建立 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="321c7-190">Create an Azure cloud service</span></span>
<span data-ttu-id="321c7-191">Azure 雲端服務是 hello 環境 hello 應用程式將執行。</span><span class="sxs-lookup"><span data-stu-id="321c7-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="321c7-192">在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="321c7-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="321c7-193">按一下 [新增] > [計算] > [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="321c7-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="321c7-194">在 hello DNS 名稱輸入方塊中，輸入 hello 雲端服務的 URL 前置詞。</span><span class="sxs-lookup"><span data-stu-id="321c7-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="321c7-195">這個 URL 有 toobe 唯一。</span><span class="sxs-lookup"><span data-stu-id="321c7-195">This URL has toobe unique.</span></span>  <span data-ttu-id="321c7-196">如果您選擇的 hello 前置詞已在使用，您會收到錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="321c7-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="321c7-197">指定 hello 服務的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="321c7-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="321c7-198">按一下**建立新**然後 hello 資源群組輸入方塊中，例如 CS_contososadsRG 輸入的名稱。</span><span class="sxs-lookup"><span data-stu-id="321c7-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="321c7-199">選擇您想 toodeploy hello 應用程式的 hello 地區。</span><span class="sxs-lookup"><span data-stu-id="321c7-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="321c7-200">此欄位會指定將託管您的雲端服務的資料中心。</span><span class="sxs-lookup"><span data-stu-id="321c7-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="321c7-201">對於生產應用程式中，您應選擇 hello 區域最接近 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="321c7-202">此教學課程中，選擇 hello 區域最接近 tooyou。</span><span class="sxs-lookup"><span data-stu-id="321c7-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="321c7-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="321c7-203">Click **Create**.</span></span>

    <span data-ttu-id="321c7-204">在下列映像的 hello，雲端服務會建立以 hello URL CSvccontosoads.cloudapp.net。</span><span class="sxs-lookup"><span data-stu-id="321c7-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![New Cloud Service](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="321c7-206">建立 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="321c7-206">Create an Azure SQL database</span></span>
<span data-ttu-id="321c7-207">Hello 應用程式執行時 hello 雲端中，它會使用以雲端為基礎的資料庫。</span><span class="sxs-lookup"><span data-stu-id="321c7-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="321c7-208">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增 > 資料庫 > SQL Database**。</span><span class="sxs-lookup"><span data-stu-id="321c7-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="321c7-209">在 hello**資料庫名稱**方塊中，輸入*contosoads*。</span><span class="sxs-lookup"><span data-stu-id="321c7-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="321c7-210">在 hello**資源群組**，按一下 **使用現有**與選取的 hello hello 雲端服務所使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="321c7-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="321c7-211">在 hello 下列映像，按一下 **伺服器-設定必要的設定**和**建立新的伺服器**。</span><span class="sxs-lookup"><span data-stu-id="321c7-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![通道 toodatabase 伺服器](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="321c7-213">或者，如果您訂用帳戶已經有伺服器，您可以從 hello 下拉式清單中選取該伺服器。</span><span class="sxs-lookup"><span data-stu-id="321c7-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="321c7-214">在 hello**伺服器名稱**方塊中，輸入*csvccontosodbserver*。</span><span class="sxs-lookup"><span data-stu-id="321c7-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="321c7-215">輸入系統管理員的 [登入名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="321c7-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="321c7-216">如果您選取了 [建立新伺服器]，則不要在此輸入現有的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="321c7-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="321c7-217">您正在輸入的新名稱和密碼，您正在定義現在 toouse 稍後當您存取 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="321c7-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="321c7-218">如果您選取您先前建立的伺服器時，會提示您已經建立 hello 密碼 toohello 系統管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="321c7-219">選擇 hello 相同**位置**您選擇 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="321c7-220">當 hello 雲端服務和資料庫位於不同的資料中心 （不同的區域），延遲會增加，您將支付 hello 資料中心外部的頻寬。</span><span class="sxs-lookup"><span data-stu-id="321c7-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="321c7-221">資料中心內的頻寬則是免費的。</span><span class="sxs-lookup"><span data-stu-id="321c7-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="321c7-222">請檢查**允許 azure 服務 tooaccess 伺服器**。</span><span class="sxs-lookup"><span data-stu-id="321c7-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="321c7-223">按一下**選取**hello 新伺服器。</span><span class="sxs-lookup"><span data-stu-id="321c7-223">Click **Select** for hello new server.</span></span>

    ![新的 SQL Database 伺服器](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="321c7-225">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="321c7-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="321c7-226">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="321c7-226">Create an Azure storage account</span></span>
<span data-ttu-id="321c7-227">Azure 儲存體帳戶提供佇列和 blob 資料儲存在 hello 雲端中的資源。</span><span class="sxs-lookup"><span data-stu-id="321c7-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="321c7-228">在真實世界應用程式中，您一般會為應用程式資料與記錄資料建立不同的帳戶，以及為測試資料與生產資料建立不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="321c7-229">在本教學課程中，您只會使用一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="321c7-230">在 hello [Azure 入口網站](https://portal.azure.com)，按一下 **新增 > 儲存體 > 儲存體帳戶-blob、 檔案、 資料表、 佇列**。</span><span class="sxs-lookup"><span data-stu-id="321c7-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="321c7-231">在 hello**名稱**方塊中，輸入的 URL 前置詞。</span><span class="sxs-lookup"><span data-stu-id="321c7-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="321c7-232">您在 [hello] 方塊下，請參閱此前置詞加上 hello 文字將 hello 唯一 URL tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="321c7-233">如果已經被其他人使用您輸入的 hello 前置詞，您就必須 toochoose 在不同的前置詞。</span><span class="sxs-lookup"><span data-stu-id="321c7-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="321c7-234">設定 hello**部署模型**太*傳統*。</span><span class="sxs-lookup"><span data-stu-id="321c7-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="321c7-235">設定 hello**複寫**下拉式清單也列出**本機備援儲存體**。</span><span class="sxs-lookup"><span data-stu-id="321c7-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="321c7-236">儲存體帳戶啟用地理複寫時，儲存的 hello 內容 hello 主要位置中發生重大災害時，就會為複寫的 tooa 次要資料中心 tooenable 容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="321c7-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="321c7-237">地理區域複寫會引發額外成本。</span><span class="sxs-lookup"><span data-stu-id="321c7-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="321c7-238">針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。</span><span class="sxs-lookup"><span data-stu-id="321c7-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="321c7-239">如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="321c7-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="321c7-240">在 hello**資源群組**，按一下 **使用現有**與選取的 hello hello 雲端服務所使用的資源群組。</span><span class="sxs-lookup"><span data-stu-id="321c7-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="321c7-241">設定 hello**位置**下拉式選單 toohello 您選擇 hello 雲端服務的相同地區。</span><span class="sxs-lookup"><span data-stu-id="321c7-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="321c7-242">Hello 雲端服務和儲存體帳戶位於不同的資料中心 （不同的區域），延遲會增加，您將支付 hello 資料中心外部的頻寬。</span><span class="sxs-lookup"><span data-stu-id="321c7-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="321c7-243">資料中心內的頻寬則是免費的。</span><span class="sxs-lookup"><span data-stu-id="321c7-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="321c7-244">Azure 同質群組提供機制 toominimize hello 之間的距離資料中心，以降低延遲的資源。</span><span class="sxs-lookup"><span data-stu-id="321c7-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="321c7-245">本教學課程不會使用同質群組。</span><span class="sxs-lookup"><span data-stu-id="321c7-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="321c7-246">如需詳細資訊，請參閱[如何 tooCreate 親和性群組在 Azure 中](http://msdn.microsoft.com/library/jj156209.aspx)。</span><span class="sxs-lookup"><span data-stu-id="321c7-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="321c7-247">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="321c7-247">Click **Create**.</span></span>

    ![New storage account](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="321c7-249">Hello 映像，在儲存體帳戶會建立具有 hello URL `csvccontosoads.core.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="321c7-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="321c7-250">在 Azure 中執行時設定 hello 方案 toouse Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="321c7-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="321c7-251">hello web 專案 hello 背景工作角色專案各有自己的資料庫連接字串和每個需求 toopoint toohello Azure SQL database 在 Azure 中的 hello 應用程式執行時。</span><span class="sxs-lookup"><span data-stu-id="321c7-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="321c7-252">您將使用[Web.config 轉換](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations)hello web 角色和 hello 背景工作角色的雲端服務環境設定。</span><span class="sxs-lookup"><span data-stu-id="321c7-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="321c7-253">在這一節和 hello 下一節中，您可以將專案檔中的認證來儲存。</span><span class="sxs-lookup"><span data-stu-id="321c7-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="321c7-254">[請勿將敏感性資料儲存在公用原始程式碼存放庫](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)。</span><span class="sxs-lookup"><span data-stu-id="321c7-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="321c7-255">在 hello ContosoAdsWeb 專案中，開啟 hello *Web.Release.config* hello 應用程式轉換檔*Web.config*檔案中，刪除 hello 註解區塊包含`<connectionStrings>`項目，並貼上下列程式碼，其所在位置的 hello。</span><span class="sxs-lookup"><span data-stu-id="321c7-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="321c7-256">保留 hello 檔案開啟以供編輯。</span><span class="sxs-lookup"><span data-stu-id="321c7-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="321c7-257">在 hello [Azure 入口網站](https://portal.azure.com)，按一下  **SQL 資料庫**hello 左窗格中，按一下 在此教學課程中，您所建立的 hello 資料庫，然後按一下**顯示連接字串**。</span><span class="sxs-lookup"><span data-stu-id="321c7-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Show connection strings](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="321c7-259">hello 入口網站會顯示以 hello 密碼預留位置的連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![連接字串](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="321c7-261">在 hello *Web.Release.config*轉換檔案，請刪除`{connectionstring}`在其位置 hello ADO.NET 連接字串 hello Azure 入口網站中貼上。</span><span class="sxs-lookup"><span data-stu-id="321c7-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="321c7-262">您貼入 hello hello 連接字串中*Web.Release.config*轉換檔案，請取代`{your_password_here}`與您建立新 SQL database hello 的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="321c7-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="321c7-263">儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-263">Save hello file.</span></span>  
6. <span data-ttu-id="321c7-264">選取並複製 hello 連接字串 （不含 hello 周圍的引號)，用於 hello 設定 hello 背景工作角色專案的步驟。</span><span class="sxs-lookup"><span data-stu-id="321c7-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="321c7-265">在**方案總管 中**下**角色**hello 雲端服務專案中，以滑鼠右鍵按一下**ContosoAdsWorker** ，然後按一下**屬性**.</span><span class="sxs-lookup"><span data-stu-id="321c7-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="321c7-267">按一下 hello**設定** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="321c7-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="321c7-268">變更**服務組態**太**雲端**。</span><span class="sxs-lookup"><span data-stu-id="321c7-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="321c7-269">選取 hello**值**欄位 hello`ContosoAdsDbConnectionString`設定，然後再貼上您所複製的 hello hello 教學課程的上一節的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Database connection string for worker role](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="321c7-271">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="321c7-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="321c7-272">在 Azure 中執行時設定 hello 方案 toouse Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="321c7-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="321c7-273">Hello web 角色專案和 hello 背景工作角色專案的 azure 儲存體帳戶連接字串會儲存在 hello 雲端服務專案中的環境設定。</span><span class="sxs-lookup"><span data-stu-id="321c7-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="321c7-274">對於每個專案，一組個別的 hello 應用程式會在本機執行時使用的設定 toobe 和 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="321c7-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="321c7-275">您要更新的 web 和背景工作角色專案 hello 雲端環境的設定。</span><span class="sxs-lookup"><span data-stu-id="321c7-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="321c7-276">在**方案總管 中**，以滑鼠右鍵按一下**ContosoAdsWeb**下**角色**在 hello **ContosoAdsCloudService**專案，然後再按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="321c7-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="321c7-278">按一下 hello**設定**] 索引標籤。在 [hello**服務組態**下拉式清單方塊中，選擇**雲端**。</span><span class="sxs-lookup"><span data-stu-id="321c7-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloud configuration](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="321c7-280">選取 hello **StorageConnectionString**項目，而且您會看到省略符號 (**...**) hello 右尾 hello 按鈕。</span><span class="sxs-lookup"><span data-stu-id="321c7-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="321c7-281">按一下 hello 省略符號按鈕 tooopen hello**建立儲存體帳戶連接字串** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="321c7-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Open Connection String Create box](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="321c7-283">在 hello**建立儲存體連接字串**對話方塊中，按一下 **訂用帳戶**，選擇您先前建立的 hello 儲存體帳戶，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="321c7-284">如果您尚未登入，將提示您輸入 Azure 帳戶憑證。</span><span class="sxs-lookup"><span data-stu-id="321c7-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Create Storage Connection String](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="321c7-286">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="321c7-286">Save your changes.</span></span>
6. <span data-ttu-id="321c7-287">後續 hello 相同程序與您用於 hello`StorageConnectionString`連接字串 tooset hello`Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString`連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="321c7-288">此連接字串用於記錄。</span><span class="sxs-lookup"><span data-stu-id="321c7-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="321c7-289">後續 hello 相同程序與您用於 hello **ContosoAdsWeb**角色 tooset hello 這兩個連接字串**ContosoAdsWorker**角色。</span><span class="sxs-lookup"><span data-stu-id="321c7-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="321c7-290">別忘了 tooset**服務組態**太**雲端**。</span><span class="sxs-lookup"><span data-stu-id="321c7-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="321c7-291">您已設定使用 Visual Studio UI hello hello 角色環境設定會儲存在下列檔案 hello ContosoAdsCloudService 專案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="321c7-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="321c7-292">*ServiceDefinition.csdef* -定義 hello 設定名稱。</span><span class="sxs-lookup"><span data-stu-id="321c7-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="321c7-293">*ServiceConfiguration.Cloud.cscfg* -hello 雲端中的 hello 應用程式執行時提供值。</span><span class="sxs-lookup"><span data-stu-id="321c7-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="321c7-294">*ServiceConfiguration.Local.cscfg* -hello 應用程式在本機上執行提供的值。</span><span class="sxs-lookup"><span data-stu-id="321c7-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="321c7-295">比方說，hello ServiceDefinition.csdef 包含 hello 下列定義：</span><span class="sxs-lookup"><span data-stu-id="321c7-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="321c7-296">和 hello *ServiceConfiguration.Cloud.cscfg*檔案包含您輸入的這些設定，在 Visual Studio 中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="321c7-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="321c7-297">hello`<Instances>`設定指定 hello Azure 將 hello 背景工作角色執行程式碼的虛擬機器數目。</span><span class="sxs-lookup"><span data-stu-id="321c7-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="321c7-298">hello[後續步驟](#next-steps)章節包含有關向外延展的雲端服務，連結 toomore 資訊</span><span class="sxs-lookup"><span data-stu-id="321c7-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="321c7-299">部署 hello 專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="321c7-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="321c7-300">在**方案總管] 中**，以滑鼠右鍵按一下 hello **ContosoAdsCloudService**雲端專案，然後選取 [**發行**。</span><span class="sxs-lookup"><span data-stu-id="321c7-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Publish menu](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="321c7-302">在 [hello**登入**hello 的步驟**發行 Azure 應用程式**精靈] 中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="321c7-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Sign in step](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="321c7-304">在 [hello**設定**步驟 hello 精靈] 中，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="321c7-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Settings step](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="321c7-306">hello hello 中的預設設定**進階**索引標籤會顯示在此教學課程正常。</span><span class="sxs-lookup"><span data-stu-id="321c7-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="321c7-307">Hello 進階 索引標籤的相關資訊，請參閱[發行 Azure 應用程式精靈](http://msdn.microsoft.com/library/hh535756.aspx)。</span><span class="sxs-lookup"><span data-stu-id="321c7-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="321c7-308">在 hello**摘要**步驟中，按一下 **發行**。</span><span class="sxs-lookup"><span data-stu-id="321c7-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Summary step](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="321c7-310">hello **Azure 活動記錄檔**視窗在 Visual Studio 中開啟。</span><span class="sxs-lookup"><span data-stu-id="321c7-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="321c7-311">按一下 hello 向右箭號圖示 tooexpand hello 部署詳細資料。</span><span class="sxs-lookup"><span data-stu-id="321c7-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="321c7-312">hello 部署可能會佔用 too5 分鐘或更多 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="321c7-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Azure Activity Log window](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="321c7-314">Hello 部署狀態完成時，按一下 hello **Web 應用程式 URL** toostart hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="321c7-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="321c7-315">您現在可以測試 hello 應用程式所建立、 檢視和編輯某些廣告，如同您在本機執行 hello 應用程式時。</span><span class="sxs-lookup"><span data-stu-id="321c7-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="321c7-316">當您完成測試、 刪除或停止 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="321c7-317">即使您不使用 hello 雲端服務，它持費用，因為它會保留虛擬機器資源。</span><span class="sxs-lookup"><span data-stu-id="321c7-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="321c7-318">如果您讓它保持執行，找到您 URL 的任何人都可以建立和檢視廣告。</span><span class="sxs-lookup"><span data-stu-id="321c7-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="321c7-319">在 hello [Azure 入口網站](https://portal.azure.com)，移 toohello**概觀**標籤為您的雲端服務，然後按一下hello**刪除**hello hello 頁頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="321c7-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="321c7-320">如果您只想 tootemporarily 防止其他人無法存取 hello 站台，按一下 **停止**改為。</span><span class="sxs-lookup"><span data-stu-id="321c7-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="321c7-321">在此情況下，費用將繼續 tooaccrue。</span><span class="sxs-lookup"><span data-stu-id="321c7-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="321c7-322">當您不再需要它們時，您可以依照類似的程序 toodelete hello SQL 資料庫和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="321c7-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="321c7-323">從頭開始建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="321c7-323">Create hello application from scratch</span></span>
<span data-ttu-id="321c7-324">如果尚未下載[hello 完成應用程式](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)，請立刻進行升級。</span><span class="sxs-lookup"><span data-stu-id="321c7-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="321c7-325">您將下載的 hello 專案將檔案複製到 hello 新專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="321c7-326">建立 hello Contoso 廣告應用程式包括 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="321c7-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="321c7-327">建立雲端服務 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="321c7-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="321c7-328">更新和加入 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="321c7-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="321c7-329">設定專案參考。</span><span class="sxs-lookup"><span data-stu-id="321c7-329">Set project references.</span></span>
* <span data-ttu-id="321c7-330">設定連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-330">Configure connection strings.</span></span>
* <span data-ttu-id="321c7-331">加入程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-331">Add code files.</span></span>

<span data-ttu-id="321c7-332">建立 hello 方案之後，您將檢閱 hello 的程式碼的唯一 toocloud 服務專案和 Azure blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="321c7-333">建立雲端服務 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="321c7-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="321c7-334">在 Visual Studio 中，選擇 **新專案**從 hello**檔案**功能表。</span><span class="sxs-lookup"><span data-stu-id="321c7-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="321c7-335">Hello hello 左窗格中**新專案**對話方塊方塊中，展開  **Visual C#**選擇**雲端**範本，然後選擇 hello **Azure 雲端服務**範本。</span><span class="sxs-lookup"><span data-stu-id="321c7-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="321c7-336">命名 hello 專案和方案 ContosoAdsCloudService，，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![New Project](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="321c7-338">在 hello**新的 Azure 雲端服務**對話方塊方塊中，加入 web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="321c7-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="321c7-339">命名 hello web 角色 ContosoAdsWeb，並命名為 hello ContosoAdsWorker 的背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="321c7-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="321c7-340">（hello 右窗格 toochange hello 預設 hello 角色名稱中使用 hello 鉛筆圖示）。</span><span class="sxs-lookup"><span data-stu-id="321c7-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![New Cloud Service Project](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="321c7-342">當您看到 hello**新增 ASP.NET 專案**hello web 角色 對話方塊選擇 hello MVC 範本，然後按一下**變更驗證**。</span><span class="sxs-lookup"><span data-stu-id="321c7-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![變更驗證](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="321c7-344">在 hello**變更驗證**對話方塊方塊中，選擇**非驗證**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![不需要驗證](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="321c7-346">在 [hello**新增 ASP.NET 專案**] 對話方塊中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="321c7-347">在**方案總管] 中**，以滑鼠右鍵按一下 hello 方案 （不是其中一個 hello 專案），然後選擇 [**新增為新的專案**。</span><span class="sxs-lookup"><span data-stu-id="321c7-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="321c7-348">在 hello**加入新的專案**對話方塊方塊中，選擇**Windows**下**Visual C#**在 hello 左的窗格，然後按一下hello**類別庫**範本。</span><span class="sxs-lookup"><span data-stu-id="321c7-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="321c7-349">名稱 hello 專案*ContosoAdsCommon*，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="321c7-350">您需要 tooreference hello Entity Framework 內容和 hello 資料模型從 web 和背景工作角色專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="321c7-351">或者，可以在 hello web 角色專案中定義 hello EF 相關類別，從 hello 背景工作角色專案參考該專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="321c7-352">但在 hello 的替代方法，您的背景工作角色專案必須參考 tooweb 組件，它不需要。</span><span class="sxs-lookup"><span data-stu-id="321c7-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="321c7-353">更新和加入 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="321c7-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="321c7-354">開啟 hello**管理 NuGet 封裝**hello 解決方案的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="321c7-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="321c7-355">在 hello hello 視窗頂端，選取**更新**。</span><span class="sxs-lookup"><span data-stu-id="321c7-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="321c7-356">尋找 hello *WindowsAzure.Storage*封裝，以及是否 hello 清單中，選取它，然後選取 hello 專案 tooupdate web 和背景工作，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="321c7-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="321c7-357">hello 儲存體用戶端程式庫會比 Visual Studio 專案範本，更頻繁地更新，所以您通常會發現該 hello 版本中更新新建立的專案需求 toobe。</span><span class="sxs-lookup"><span data-stu-id="321c7-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="321c7-358">在 hello hello 視窗頂端，選取**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="321c7-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="321c7-359">尋找 hello *EntityFramework* NuGet 封裝，並將它安裝在所有的三個專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="321c7-360">尋找 hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet 封裝，並將它安裝在 hello 背景工作角色專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="321c7-361">設定專案參考</span><span class="sxs-lookup"><span data-stu-id="321c7-361">Set project references</span></span>
1. <span data-ttu-id="321c7-362">在 hello ContosoAdsWeb 專案設定參考 toohello ContosoAdsCommon 專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="321c7-363">Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**參考** - **加入參考**。</span><span class="sxs-lookup"><span data-stu-id="321c7-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="321c7-364">在 hello**參考管理員**對話方塊中，選取**方案 – 專案**hello 左窗格中，選取**ContosoAdsCommon**，然後按一下**確定**.</span><span class="sxs-lookup"><span data-stu-id="321c7-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="321c7-365">在 hello ContosoAdsWorker 專案設定參考 toohello ContosAdsCommon 專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="321c7-366">ContosoAdsCommon 將包含 hello Entity Framework 資料模型和內容類別，這將會使用這兩個 hello 前端和後端。</span><span class="sxs-lookup"><span data-stu-id="321c7-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="321c7-367">在 hello ContosoAdsWorker 專案中，設定參照太`System.Drawing`。</span><span class="sxs-lookup"><span data-stu-id="321c7-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="321c7-368">Hello 後端 tooconvert 映像 toothumbnails 會使用這個組件。</span><span class="sxs-lookup"><span data-stu-id="321c7-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="321c7-369">設定連接字串</span><span class="sxs-lookup"><span data-stu-id="321c7-369">Configure connection strings</span></span>
<span data-ttu-id="321c7-370">在本節中，您將針對本機測試用途來設定 Azure 儲存體和 SQL 連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="321c7-371">hello hello 教學課程中先前的部署指示會說明如何 tooset hello 連線字串 hello 應用程式執行時發生 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="321c7-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="321c7-372">在 hello ContosoAdsWeb 專案、 開啟 hello 應用程式 Web.config 檔案，並插入 hello 下列`connectionStrings`hello 之後的項目`configSections`項目。</span><span class="sxs-lookup"><span data-stu-id="321c7-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="321c7-373">如果您使用 Visual Studio 2015 或更新版本，將 "v11.0" 取代為 "MSSQLLocalDB"。</span><span class="sxs-lookup"><span data-stu-id="321c7-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="321c7-374">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="321c7-374">Save your changes.</span></span>
3. <span data-ttu-id="321c7-375">在 hello ContosoAdsCloudService 專案中，以滑鼠右鍵按一下底下的 ContosoAdsWeb**角色**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="321c7-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Role properties](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="321c7-377">在 [hello **ContosAdsWeb [角色]**屬性] 視窗中，按一下 hello**設定**索引標籤，然後再按一下**加入設定**。</span><span class="sxs-lookup"><span data-stu-id="321c7-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="321c7-378">保留**服務組態**設定得**所有組態**。</span><span class="sxs-lookup"><span data-stu-id="321c7-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="321c7-379">新增名為 *StorageConnectionString*的設定。</span><span class="sxs-lookup"><span data-stu-id="321c7-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="321c7-380">設定**類型**太*ConnectionString*，並設定**值**太*UseDevelopmentStorage = true*。</span><span class="sxs-lookup"><span data-stu-id="321c7-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![New connection string](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="321c7-382">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="321c7-382">Save your changes.</span></span>
7. <span data-ttu-id="321c7-383">後續 hello 相同的程序 tooadd hello ContosoAdsWorker 角色內容中的儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="321c7-384">仍在 hello **ContosoAdsWorker [角色]**屬性 視窗中，加入另一個連接字串：</span><span class="sxs-lookup"><span data-stu-id="321c7-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="321c7-385">名稱：ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="321c7-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="321c7-386">類型：字串</span><span class="sxs-lookup"><span data-stu-id="321c7-386">Type: String</span></span>
   * <span data-ttu-id="321c7-387">的值： 貼上 hello 相同 hello web 角色專案使用的連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="321c7-388">（適用於 Visual Studio 2013 的 hello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="321c7-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="321c7-389">別忘了 toochange hello 資料來源如果複製此範例中，而您使用 Visual Studio 2015 或更新版本。）</span><span class="sxs-lookup"><span data-stu-id="321c7-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="321c7-390">加入程式碼檔案</span><span class="sxs-lookup"><span data-stu-id="321c7-390">Add code files</span></span>
<span data-ttu-id="321c7-391">本節中，您將複製程式碼檔案從下載的 hello 方案到 hello 新方案。</span><span class="sxs-lookup"><span data-stu-id="321c7-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="321c7-392">hello 下列各節將顯示，並說明此程式碼的關鍵部分。</span><span class="sxs-lookup"><span data-stu-id="321c7-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="321c7-393">tooadd 檔案 tooa 專案或資料夾、 以滑鼠右鍵按一下 hello 專案或資料夾並按一下**新增** - **現有項目**。</span><span class="sxs-lookup"><span data-stu-id="321c7-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="321c7-394">選取您想要然後按一下 hello 檔案**新增**。</span><span class="sxs-lookup"><span data-stu-id="321c7-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="321c7-395">如果系統詢問您是否想 tooreplace 現有檔案，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="321c7-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="321c7-396">在 hello ContosoAdsCommon 專案中，刪除 hello *Class1.cs*檔案，然後在其位置 hello 加入*Ad.cs*和*ContosoAdscontext.cs* hello 中的檔案已經下載專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="321c7-397">在 hello ContosoAdsWeb 專案中，新增 hello hello 下載專案中的下列檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="321c7-398">*Global.asax.cs*。</span><span class="sxs-lookup"><span data-stu-id="321c7-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="321c7-399">在 hello *_layout.cshtml*資料夾：  *\_Layout.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="321c7-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="321c7-400">在 hello *Views\Home*資料夾： *Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="321c7-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="321c7-401">在 hello*控制器*資料夾： *AdController.cs*。</span><span class="sxs-lookup"><span data-stu-id="321c7-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="321c7-402">在 hello *Views\Ad*資料夾 （第一次建立 hello 資料夾）： 五個*.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="321c7-403">在 hello ContosoAdsWorker 專案中，加入*WorkerRole.cs* hello 從已經下載專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="321c7-404">您現在可以建置及執行 hello 應用程式，如稍早在 hello 教學課程中所指示和 hello 應用程式會使用本機資料庫和儲存體模擬器的資源。</span><span class="sxs-lookup"><span data-stu-id="321c7-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="321c7-405">hello 下列各節說明 hello 程式碼與相關的 tooworking hello Azure 環境、 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="321c7-406">本教學課程並未說明如何 toocreate MVC 控制器和檢視表使用 scaffolding toowrite Entity Framework 程式碼的運作方式與 SQL Server 資料庫或 ASP.NET 4.5 中非同步程式設計的 hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="321c7-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="321c7-407">如需這些主題的資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="321c7-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="321c7-408">開始使用 MVC 5</span><span class="sxs-lookup"><span data-stu-id="321c7-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="321c7-409">開始使用 EF 6 和 MVC 5</span><span class="sxs-lookup"><span data-stu-id="321c7-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="321c7-410">[在.NET 4.5 簡介 tooasynchronous 程式設計](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)。</span><span class="sxs-lookup"><span data-stu-id="321c7-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="321c7-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="321c7-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="321c7-412">hello Ad.cs 檔案定義 ad 類別列舉和廣告資訊的 POCO 實體類別。</span><span class="sxs-lookup"><span data-stu-id="321c7-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="321c7-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="321c7-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="321c7-414">hello ContosoAdsContext 類別指定 hello Ad 類別用於 DbSet 集合，其中 Entity Framework 會將儲存在 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="321c7-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="321c7-415">hello 類別有兩個建構函式。</span><span class="sxs-lookup"><span data-stu-id="321c7-415">hello class has two constructors.</span></span> <span data-ttu-id="321c7-416">第一次 hello 它們正由 hello web 專案，並指定 hello hello Web.config 檔案中儲存的連接字串的名稱。</span><span class="sxs-lookup"><span data-stu-id="321c7-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="321c7-417">hello 第二個建構函式可讓您 toopass hello 實際的連接字串使用 hello 背景工作角色專案，因為它沒有 Web.config 檔中。</span><span class="sxs-lookup"><span data-stu-id="321c7-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="321c7-418">之前看到這個連接字串的儲存位置，而您會看到如何 hello 程式碼會擷取 hello 連接字串時，它會具現化 hello DbContext 類別。</span><span class="sxs-lookup"><span data-stu-id="321c7-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="321c7-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="321c7-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="321c7-420">程式碼從 hello 呼叫`Application_Start`方法會建立*映像*blob 容器和*映像*排入佇列，如果它們不存在。</span><span class="sxs-lookup"><span data-stu-id="321c7-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="321c7-421">這可確保，每當您開始使用新的儲存體帳戶，或開始使用新的電腦上的 hello 儲存體模擬器，hello 所需的 blob 容器和佇列將會自動建立。</span><span class="sxs-lookup"><span data-stu-id="321c7-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="321c7-422">使用從 hello hello 儲存體連接字串 hello 程式碼取得存取 toohello 儲存體帳戶*.cscfg*檔案。</span><span class="sxs-lookup"><span data-stu-id="321c7-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="321c7-423">然後它會取得參考 toohello*映像*blob 容器時，如果它不存在，並設定存取權限 hello 新的容器建立 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="321c7-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="321c7-424">根據預設，新的容器只允許用戶端與儲存體帳戶認證 tooaccess blob。</span><span class="sxs-lookup"><span data-stu-id="321c7-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="321c7-425">hello 網站需要 hello blob toobe 公開，讓它可以顯示使用該點 toohello 映像 blob Url 的映像。</span><span class="sxs-lookup"><span data-stu-id="321c7-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="321c7-426">類似的程式碼取得參考 toohello*映像*佇列，並建立新的佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="321c7-427">在此情況下，即不需要變更權限。</span><span class="sxs-lookup"><span data-stu-id="321c7-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="321c7-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="321c7-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="321c7-429">hello *_Layout.cshtml*檔案設定中 hello 頁首和頁尾，hello 應用程式名稱，並建立"廣告 」 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="321c7-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="321c7-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="321c7-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="321c7-431">hello *Views\Home\Index.cshtml*檔案 hello 首頁上顯示類別目錄連結。</span><span class="sxs-lookup"><span data-stu-id="321c7-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="321c7-432">hello 連結傳遞 hello 整數值的 hello `Category` querystring 變數 toohello 廣告索引頁面中的列舉。</span><span class="sxs-lookup"><span data-stu-id="321c7-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="321c7-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="321c7-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="321c7-434">在 hello *AdController.cs*檔案、 hello 建構函式呼叫 hello`InitializeStorage`方法 toocreate Azure 儲存體用戶端程式庫物件，提供應用程式開發介面使用的 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="321c7-435">然後 hello 程式碼會取得參考 toohello*映像*blob 容器，如稍早在您所見*Global.asax.cs*。</span><span class="sxs-lookup"><span data-stu-id="321c7-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="321c7-436">在執行該動作時，它會設定適用 Web 應用程式的預設 [重試原則](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) 。</span><span class="sxs-lookup"><span data-stu-id="321c7-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="321c7-437">hello 預設指數型輪詢重試原則無法停止回應 hello web 應用程式的時間超過一分鐘上重複的重試的暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="321c7-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="321c7-438">此處指定的 hello 重試原則會等待三秒鐘之後每個嘗試向上 toothree 嘗試。</span><span class="sxs-lookup"><span data-stu-id="321c7-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="321c7-439">類似的程式碼取得參考 toohello*映像*佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="321c7-440">大部分的 hello 控制器程式碼是使用 Entity Framework 資料模型使用 DbContext 類別的一般。</span><span class="sxs-lookup"><span data-stu-id="321c7-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="321c7-441">例外狀況為 hello HttpPost`Create`方法，這個方法會將檔案上傳，並將它儲存在 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="321c7-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="321c7-442">hello 模型繫結器提供[HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 方法的物件。</span><span class="sxs-lookup"><span data-stu-id="321c7-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="321c7-443">如果 hello 使用者選取檔案 tooupload，hello 程式碼會 hello 檔案上傳、 將它儲存在 blob，並更新 hello Ad 資料庫記錄點 toohello blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="321c7-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="321c7-444">hello 沒有 hello 上傳的程式碼處於 hello`UploadAndSaveBlobAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="321c7-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="321c7-445">它會建立 GUID hello blob、 上傳和儲存 hello 檔案，並傳回參考 toohello 儲存 blob。</span><span class="sxs-lookup"><span data-stu-id="321c7-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="321c7-446">之後 hello HttpPost`Create`方法上傳 blob 並更新 hello 資料庫，它會建立佇列訊息 tooinform 該映像可供轉換 tooa 縮圖的後端程序。</span><span class="sxs-lookup"><span data-stu-id="321c7-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="321c7-447">hello 碼 hello HttpPost`Edit`方法很類似，不同之處在於如果 hello 使用者選取新的映像檔必須先刪除任何存在的 blob。</span><span class="sxs-lookup"><span data-stu-id="321c7-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="321c7-448">hello 下一個範例顯示當您刪除廣告時，會刪除 blob 的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="321c7-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="321c7-449">ContosoAdsWeb - Views\Ad\Index.cshtml 和 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="321c7-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="321c7-450">hello *Index.cshtml*檔案就會顯示以 hello 的縮圖，其他的 ad 資料。</span><span class="sxs-lookup"><span data-stu-id="321c7-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="321c7-451">hello *Details.cshtml*檔案會顯示 hello 完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="321c7-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="321c7-452">ContosoAdsWeb - Views\Ad\Create.cshtml 和 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="321c7-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="321c7-453">hello *Create.cshtml*和*Edit.cshtml*檔案會指定表單編碼可讓 hello 控制器 tooget hello`HttpPostedFileBase`物件。</span><span class="sxs-lookup"><span data-stu-id="321c7-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="321c7-454">`<input>`項目會告知 hello 瀏覽器 tooprovide 檔案選取對話方塊。</span><span class="sxs-lookup"><span data-stu-id="321c7-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="321c7-455">ContosoAdsWorker - WorkerRole.cs - OnStart 方法</span><span class="sxs-lookup"><span data-stu-id="321c7-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="321c7-456">hello Azure 背景工作角色環境呼叫 hello`OnStart`方法在 hello`WorkerRole`類別時快速入門 hello 背景工作角色，而且它會呼叫 hello`Run`方法時 hello`OnStart`方法完成。</span><span class="sxs-lookup"><span data-stu-id="321c7-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="321c7-457">hello`OnStart`方法取得 hello 資料庫連接字串從 hello *.cscfg*檔案，並將其傳遞 toohello Entity Framework DbContext 類別。</span><span class="sxs-lookup"><span data-stu-id="321c7-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="321c7-458">hello SQLClient 提供者會根據預設，使用的因此 hello 提供者並沒有指定 toobe。</span><span class="sxs-lookup"><span data-stu-id="321c7-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="321c7-459">在這之後，hello 方法會取得參考 toohello 儲存體帳戶，並建立 hello blob 容器和佇列，如果不存在。</span><span class="sxs-lookup"><span data-stu-id="321c7-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="321c7-460">hello 的程式碼是您已經在 hello web 角色中所看到的類似 toowhat`Application_Start`方法。</span><span class="sxs-lookup"><span data-stu-id="321c7-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="321c7-461">ContosoAdsWorker - WorkerRole.cs - Run 方法</span><span class="sxs-lookup"><span data-stu-id="321c7-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="321c7-462">hello`Run`呼叫方法時，hello`OnStart`方法完成初始設定工作。</span><span class="sxs-lookup"><span data-stu-id="321c7-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="321c7-463">hello 方法執行時造成無限迴圈，監看新的佇列訊息，並到達時加以處理。</span><span class="sxs-lookup"><span data-stu-id="321c7-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="321c7-464">在 hello 迴圈的每個反覆項目，如果找不到任何佇列訊息，hello 程式睡眠第二個。</span><span class="sxs-lookup"><span data-stu-id="321c7-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="321c7-465">這樣可避免產生過多 CPU 時間和儲存體交易成本 hello 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="321c7-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="321c7-466">hello Microsoft 客戶諮詢小組的開發人員忘記 tooinclude，告知劇本部署 tooproduction，而且留下休假時。</span><span class="sxs-lookup"><span data-stu-id="321c7-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="321c7-467">在他回之後，他監督成本超過 hello 休假時。</span><span class="sxs-lookup"><span data-stu-id="321c7-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="321c7-468">有時 hello 訊息內容的佇列將導致處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="321c7-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="321c7-469">這稱為*有害訊息*，以及如果您只記錄錯誤並重新啟動 hello 迴圈，您可以不斷地嘗試 tooprocess 該訊息。</span><span class="sxs-lookup"><span data-stu-id="321c7-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="321c7-470">因此 hello catch 區塊包含 if 陳述式會檢查 toosee 多少次 hello 應用程式已嘗試 tooprocess hello 目前的訊息，而且如果它已超過 5 次，hello 訊息從 hello 佇列中刪除。</span><span class="sxs-lookup"><span data-stu-id="321c7-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="321c7-471">`ProcessQueueMessage` 。</span><span class="sxs-lookup"><span data-stu-id="321c7-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="321c7-472">這段程式碼讀取 hello 資料庫 tooget hello 影像 URL，將轉換 hello 影像 tooa 縮圖、 hello 縮圖會將儲存在 blob、 hello 縮圖的 blob URL，以更新 hello 資料庫並刪除 hello 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="321c7-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="321c7-473">hello hello 中的程式碼`ConvertImageToThumbnailJPG`方法為了簡單起見 hello System.Drawing 命名空間中使用類別。</span><span class="sxs-lookup"><span data-stu-id="321c7-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="321c7-474">不過，此命名空間中的 hello 類別針對搭配 Windows Form 使用所設計。</span><span class="sxs-lookup"><span data-stu-id="321c7-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="321c7-475">不支援將它們用於 Windows 或 ASP.NET 服務。</span><span class="sxs-lookup"><span data-stu-id="321c7-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="321c7-476">如需映像處理選項的詳細資訊，請參閱[動態映像產生](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx)和[深入調整映像大小](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)。</span><span class="sxs-lookup"><span data-stu-id="321c7-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="321c7-477">疑難排解</span><span class="sxs-lookup"><span data-stu-id="321c7-477">Troubleshooting</span></span>
<span data-ttu-id="321c7-478">如果項目無法運作時遵循 hello 指示在本教學課程中，以下是一些常見錯誤及如何 tooresolve 它們。</span><span class="sxs-lookup"><span data-stu-id="321c7-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="321c7-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="321c7-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="321c7-480">hello`RoleEnvironment`當您在 Azure 中執行應用程式，或當您執行使用 hello Azure 計算模擬器在本機，物件由 Azure 提供。</span><span class="sxs-lookup"><span data-stu-id="321c7-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="321c7-481">如果您在本機執行時，您會收到這個錯誤，，請確定您已設定 hello ContosoAdsCloudService 專案為 hello 啟始專案。</span><span class="sxs-lookup"><span data-stu-id="321c7-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="321c7-482">這會設定 hello 專案 toorun 使用 hello Azure 計算模擬器。</span><span class="sxs-lookup"><span data-stu-id="321c7-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="321c7-483">Hello 應用程式會使用 hello Azure RoleEnvironment 的 hello 事項之一是 tooget hello 連接字串值儲存在 hello *.cscfg*檔案，所以此例外狀況的另一個原因是遺漏的連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="321c7-484">請確定在 hello ContosoAdsWeb 專案中，建立同時雲端的 hello StorageConnectionString 設定與本機設定，而且您 hello ContosoAdsWorker 專案中建立這兩種設定這兩個連接字串。</span><span class="sxs-lookup"><span data-stu-id="321c7-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="321c7-485">如果您這樣做**全部尋找**搜尋為 StorageConnectionString hello 整個方案中，您應該會看到它 9 次 6 檔案中。</span><span class="sxs-lookup"><span data-stu-id="321c7-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="321c7-486">無法覆寫 tooport xxx。</span><span class="sxs-lookup"><span data-stu-id="321c7-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="321c7-487">低於最小值的新連接埠，對通訊協定 http 允許的值為 8080</span><span class="sxs-lookup"><span data-stu-id="321c7-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="321c7-488">請嘗試變更 hello hello web 專案所使用的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="321c7-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="321c7-489">Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="321c7-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="321c7-490">按一下 hello **Web**索引標籤，然後再變更 hello hello 連接埠號碼**專案 Url**設定。</span><span class="sxs-lookup"><span data-stu-id="321c7-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="321c7-491">可能會解決 hello 問題的另一個替代方式，請參閱下列章節的 hello。</span><span class="sxs-lookup"><span data-stu-id="321c7-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="321c7-492">在本機執行時的其他錯誤</span><span class="sxs-lookup"><span data-stu-id="321c7-492">Other errors when running locally</span></span>
<span data-ttu-id="321c7-493">預設的新雲端服務專案會使用 hello Azure 計算模擬器的 express toosimulate hello Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="321c7-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="321c7-494">這是輕量版的 hello 完整計算模擬器，並在某些條件 hello 完整模擬器時 hello express 版本並不會。</span><span class="sxs-lookup"><span data-stu-id="321c7-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="321c7-495">toochange hello 專案 toouse hello 完整模擬器，hello ContosoAdsCloudService 專案中，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="321c7-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="321c7-496">在 hello**屬性**視窗中按一下 hello **Web**索引標籤，然後再按一下 hello**使用完整模擬器**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="321c7-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="321c7-497">順序與 hello 完整模擬器的 toorun hello 應用程式，您必須 tooopen Visual Studio 系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="321c7-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="321c7-498">後續步驟</span><span class="sxs-lookup"><span data-stu-id="321c7-498">Next steps</span></span>
<span data-ttu-id="321c7-499">hello Contoso 廣告應用程式具有刻意保留簡單快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="321c7-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="321c7-500">比方說，它不會實作[相依性插入](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)或 hello[儲存機制和單位運作模式](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)，不是[介面用於記錄](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)，它不會使用[EF Code First 移轉](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 資料模型變更或[EF 連接恢復功能](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 暫時性網路錯誤，等等。</span><span class="sxs-lookup"><span data-stu-id="321c7-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="321c7-501">以下是一些雲端服務的範例應用程式示範多個實際的編碼方式，從較不複雜 toomore 複雜：</span><span class="sxs-lookup"><span data-stu-id="321c7-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="321c7-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31)。</span><span class="sxs-lookup"><span data-stu-id="321c7-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="321c7-503">在概念上類似 tooContoso 廣告但實作更多功能和多個真實世界的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="321c7-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="321c7-504">[具有表格、佇列和 Blob 的 Azure 雲端服務多層式應用程式](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)。</span><span class="sxs-lookup"><span data-stu-id="321c7-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="321c7-505">介紹 Azure 儲存體資料表以及 Blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="321c7-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="321c7-506">根據較舊版本的 hello Azure SDK for.NET，將需要與 hello 目前的版本部分修改 toowork。</span><span class="sxs-lookup"><span data-stu-id="321c7-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="321c7-507">[Microsoft Azure 中的雲端服務基礎](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649)。</span><span class="sxs-lookup"><span data-stu-id="321c7-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="321c7-508">完整範例，示範各種不同的最佳作法，hello Microsoft Patterns and Practices 團隊所產生。</span><span class="sxs-lookup"><span data-stu-id="321c7-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="321c7-509">如需 hello 雲端開發的一般資訊，請參閱[建置真實世界雲端應用程式與 Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)。</span><span class="sxs-lookup"><span data-stu-id="321c7-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="321c7-510">介紹影片 tooAzure 存放裝置的最佳作法和模式，請參閱[Microsoft Azure 儲存體-最佳作法與模式新](http://channel9.msdn.com/Events/Build/2014/3-628)。</span><span class="sxs-lookup"><span data-stu-id="321c7-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="321c7-511">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="321c7-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="321c7-512">Azure 雲端服務第 1 部分：簡介</span><span class="sxs-lookup"><span data-stu-id="321c7-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="321c7-513">如何 toomanage 雲端服務</span><span class="sxs-lookup"><span data-stu-id="321c7-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="321c7-514">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="321c7-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="321c7-515">如何 toochoose 雲端服務提供者</span><span class="sxs-lookup"><span data-stu-id="321c7-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
