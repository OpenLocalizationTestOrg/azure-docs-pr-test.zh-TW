---
title: "Azure App Service 中的.NET WebJob aaaCreate |Microsoft 文件"
description: "使用 ASP.NET MVC 和 Azure 建立多層式應用程式。 hello 前端執行 web 應用程式在 Azure 應用程式服務，並且 hello 在後端執行的 webjob。 hello 應用程式會使用 Entity Framework、 SQL Database 和 Azure 儲存體佇列和 blob。"
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="22593-105">在 Azure App Service 中建立 .NET WebJob</span><span class="sxs-lookup"><span data-stu-id="22593-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="22593-106">本教學課程示範 toowrite 簡單的多層式 ASP.NET MVC 5 應用程式使用 hello 的程式碼[WebJobs SDK](websites-dotnet-webjobs-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="22593-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="22593-107">hello 目的 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 程式碼，您可以執行的 WebJob，例如映像處理、 佇列的處理、 RSS 彙總、 檔案維護的一般工作為撰寫，且傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="22593-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="22593-108">hello WebJobs SDK 有內建的功能，使用 Azure 儲存體和 Service Bus、 工作排程和處理錯誤，以及許多其他常見的案例。</span><span class="sxs-lookup"><span data-stu-id="22593-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="22593-109">此外，它擁有設計 toobe 可擴充，而且沒有[擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。</span><span class="sxs-lookup"><span data-stu-id="22593-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="22593-110">hello 範例應用程式是廣告電子佈告欄。</span><span class="sxs-lookup"><span data-stu-id="22593-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="22593-111">使用者可以上傳映像，以廣告，並後端程序轉換 hello 映像 toothumbnails 資料。</span><span class="sxs-lookup"><span data-stu-id="22593-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="22593-112">hello ad 清單頁面會顯示 hello 縮圖、 和 hello ad 詳細資料頁面會顯示 hello 完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="22593-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="22593-113">以下為螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="22593-113">Here's a screenshot:</span></span>

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="22593-115">此範例應用程式能夠與 [Azure 佇列](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 和 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="22593-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="22593-116">hello 教學課程會示範如何 toodeploy hello 應用程式太[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)和[Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)。</span><span class="sxs-lookup"><span data-stu-id="22593-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="22593-117"><a id="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="22593-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="22593-118">hello 教學課程假設您已經知道如何與 toowork [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio 中的專案。</span><span class="sxs-lookup"><span data-stu-id="22593-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="22593-119">hello 教學課程原始寫入 Visual Studio 2013，但可以搭配 Visual Studio 的更新版本。</span><span class="sxs-lookup"><span data-stu-id="22593-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="22593-120">如果您使用 Visual Studio 2015 或 2017年，記下您在本機執行 hello 應用程式之前，您必須變更 hello `Data Source` hello Web.config 和 App.config 檔案中的 hello SQL Server LocalDB 連接字串的一部分`Data Source=(localdb)\v11.0`太`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="22593-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="22593-121"><a name="note"></a>您必須擁有 Azure 帳戶 toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="22593-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="22593-122">您可以[開啟免費的 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)： 取得信用額度，您可以使用 tootry 出支付 Azure 服務，以及它們甚至用完之後，您可以讓 hello 的帳戶，並使用免費的 Azure 服務，例如網站。</span><span class="sxs-lookup"><span data-stu-id="22593-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="22593-123">永遠不會將向您的信用卡，除非您明確地變更您的設定，並詢問 toobe 收費。</span><span class="sxs-lookup"><span data-stu-id="22593-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="22593-124">您可以[啟用 Visual Studio 訂閱者的每月 Azure 額度](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)：您的訂用帳戶每個月都會提供額度，供您用在付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="22593-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="22593-125">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="22593-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="22593-126">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="22593-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="22593-127"><a id="learn"></a>您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="22593-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="22593-128">hello 教學課程會示範如何 toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="22593-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="22593-129">（僅適用於 Visual Studio 2013 和 2015年使用者） 安裝 hello Azure SDK 來啟用 Azure 的開發電腦。</span><span class="sxs-lookup"><span data-stu-id="22593-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="22593-130">建立部署 hello 相關聯的 web 專案時，會自動部署 Azure webjob 的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="22593-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="22593-131">測試 hello 開發電腦上本機 WebJobs SDK 後的端。</span><span class="sxs-lookup"><span data-stu-id="22593-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="22593-132">應用程式服務中發佈 WebJobs 後端 tooa web 應用程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="22593-133">上傳檔案，並將它們儲存在 hello Azure Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="22593-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="22593-134">使用 Azure 儲存體佇列和 blob 的 hello Azure WebJobs SDK toowork。</span><span class="sxs-lookup"><span data-stu-id="22593-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="22593-135"><a id="contosoads"></a>應用程式架構</span><span class="sxs-lookup"><span data-stu-id="22593-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="22593-136">hello 範例應用程式使用 hello[佇列為主的工作模式](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)toooff 負載 hello CPU 運算密集工作建立縮圖 tooa 後端處理程序。</span><span class="sxs-lookup"><span data-stu-id="22593-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="22593-137">hello 應用程式會儲存在 SQL 資料庫中，使用 Entity Framework Code First toocreate hello 資料表和存取 hello 資料廣告。</span><span class="sxs-lookup"><span data-stu-id="22593-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="22593-138">對於每個廣告，hello 資料庫會儲存兩個 Url： 一個用於 hello 完整大小的影像，一個用於 hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="22593-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="22593-140">使用者當上傳的影像、 hello web 應用程式儲存中的 hello 映像[Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，而且會儲存點 toohello blob 的 url hello 資料庫中的 hello ad 資訊。</span><span class="sxs-lookup"><span data-stu-id="22593-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="22593-141">在 hello 相同時間，它會將訊息 tooan Azure 佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="22593-142">執行 Azure webjob 的後端程序，在 hello WebJobs SDK 輪詢 hello 新訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="22593-143">新的訊息出現時，hello WebJob 建立該映像的縮圖，並更新 hello 該廣告的縮圖 URL 資料庫欄位。</span><span class="sxs-lookup"><span data-stu-id="22593-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="22593-144">以下是顯示 hello 部分 hello 應用程式之間的互動圖表：</span><span class="sxs-lookup"><span data-stu-id="22593-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="22593-146">hello 教學課程指示適用於 tooAzure SDK for.NET 2.7.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="22593-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="22593-147"><a id="storage"></a>建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="22593-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="22593-148">Azure 儲存體帳戶提供佇列和 blob 資料儲存在 hello 雲端中的資源。</span><span class="sxs-lookup"><span data-stu-id="22593-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="22593-149">它也可供 hello WebJobs SDK toostore 記錄資料 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="22593-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="22593-150">在實際應用程式中，您通常會為應用程式資料與記錄資料建立不同的帳戶，並為測試資料與生產資料建立不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="22593-151">在本教學課程中，您只會使用一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="22593-152">開啟 hello**伺服器總管**Visual Studio 中的視窗。</span><span class="sxs-lookup"><span data-stu-id="22593-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="22593-153">以滑鼠右鍵按一下 hello **Azure**節點，然後再按一下**連接 tooMicrosoft Azure 訂用帳戶...**.</span><span class="sxs-lookup"><span data-stu-id="22593-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![連接 tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="22593-155">使用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="22593-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="22593-156">以滑鼠右鍵按一下**儲存體**底下 hello Azure 的節點，然後按一下**建立儲存體帳戶**。</span><span class="sxs-lookup"><span data-stu-id="22593-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![建立儲存體帳戶](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="22593-158">在 [hello**建立儲存體帳戶**] 對話方塊中，輸入 hello 儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="22593-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="22593-159">hello 名稱必須是必須是唯一的 (沒有其他的 Azure 儲存體帳戶可以有 hello 相同的名稱)。</span><span class="sxs-lookup"><span data-stu-id="22593-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="22593-160">如果您輸入的 hello 名稱已在使用中，您會得到機會 toochange 它。</span><span class="sxs-lookup"><span data-stu-id="22593-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="22593-161">hello 儲存體帳戶將會是 URL tooaccess *{name}*。.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="22593-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="22593-162">設定 hello**地區或同質群組**下拉式選單 toohello 區域最接近 tooyou。</span><span class="sxs-lookup"><span data-stu-id="22593-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="22593-163">此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="22593-164">對於本教學課程，您的選擇將不會造成顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="22593-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="22593-165">不過，生產環境 web 應用程式中，您希望您的 web 伺服器和您在 hello 的儲存體帳戶 toobe 相同區域 toominimize 延遲和資料輸出費用。</span><span class="sxs-lookup"><span data-stu-id="22593-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="22593-166">hello web 應用程式 （您將在稍後建立） 的資料中心應該接近盡可能 toohello 瀏覽器存取的順序 toominimize 延遲 hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="22593-167">設定 hello**複寫**下拉式清單也列出**本機備援**。</span><span class="sxs-lookup"><span data-stu-id="22593-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="22593-168">儲存體帳戶啟用地理複寫時，儲存的 hello 內容是複寫的 tooa 次要資料中心 tooenable 容錯移轉 toothat 位置發生重大災害 hello 主要位置中。</span><span class="sxs-lookup"><span data-stu-id="22593-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="22593-169">地理區域複寫會引發額外成本。</span><span class="sxs-lookup"><span data-stu-id="22593-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="22593-170">針對測試和開發的帳戶，您通常不想要 toopay 地理複寫。</span><span class="sxs-lookup"><span data-stu-id="22593-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="22593-171">如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="22593-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="22593-172">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="22593-172">Click **Create**.</span></span>

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="22593-174"><a id="download"></a>下載 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="22593-175">下載並解壓縮 hello[完成方案](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)。</span><span class="sxs-lookup"><span data-stu-id="22593-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="22593-176">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="22593-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="22593-177">從 hello**檔案**功能表中選擇 **開啟 > 專案/方案**，瀏覽 toowhere 下載 hello 方案，並開啟 hello 方案檔。</span><span class="sxs-lookup"><span data-stu-id="22593-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="22593-178">按 CTRL + SHIFT + B toobuild hello 方案。</span><span class="sxs-lookup"><span data-stu-id="22593-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="22593-179">根據預設，Visual Studio 會自動還原 hello NuGet 套件的內容，其中未包含在 hello *.zip*檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="22593-180">如果未還原 hello 套件，安裝這些手動移 toohello**管理方案的 NuGet 套件**對話方塊，然後按一下 hello**還原**在 hello 右上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="22593-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="22593-181">在**方案總管 中**，請確定**ContosoAdsWeb**選取為 hello 啟始專案。</span><span class="sxs-lookup"><span data-stu-id="22593-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="22593-182"><a id="configurestorage"></a>設定 hello 應用程式 toouse 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="22593-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="22593-183">開啟 hello 應用程式*Web.config* hello ContosoAdsWeb 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="22593-184">hello 檔案包含 SQL 連接字串和處理的 blob 和佇列的 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="22593-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="22593-185">hello SQL 連接字串指向 tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx)資料庫。</span><span class="sxs-lookup"><span data-stu-id="22593-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="22593-186">hello 儲存體連接字串是具有預留位置 hello 儲存體帳戶名稱和存取金鑰的範例。</span><span class="sxs-lookup"><span data-stu-id="22593-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="22593-187">您會使用連接字串具有 hello 名稱和儲存體帳戶金鑰取代。</span><span class="sxs-lookup"><span data-stu-id="22593-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="22593-188">hello 儲存體連接字串是預設名稱為 AzureWebJobsStorage 因為這是使用 WebJobs SDK 的 hello 名稱 hello。</span><span class="sxs-lookup"><span data-stu-id="22593-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="22593-189">hello hello Azure 環境中有 tooset 只能有一個連接字串值，因此這裡使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="22593-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="22593-190">在**伺服器總管**，以滑鼠右鍵按一下 儲存體帳戶下 hello**儲存體**節點，然後再按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="22593-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![按一下 [儲存體帳戶] 屬性](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="22593-192">在 hello**屬性**視窗中，按一下 **儲存體帳戶金鑰**，然後按一下hello 省略符號。</span><span class="sxs-lookup"><span data-stu-id="22593-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![儲存體帳戶金鑰](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="22593-194">複製 hello**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="22593-194">Copy hello **Connection String**.</span></span>

    ![[儲存體帳戶金鑰] 對話方塊](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="22593-196">取代 hello 儲存體連接字串中 hello *Web.config* hello 您剛才複製的連接字串的檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="22593-197">請確定您選取的所有項目在 hello 引號內，但不是包括 hello 引號之前貼。</span><span class="sxs-lookup"><span data-stu-id="22593-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="22593-198">開啟 hello *App.config* hello ContosoAdsWebJob 專案中的檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="22593-199">此檔案有兩個儲存體連接字串，一個供應用程式使用，另一個供記錄使用。</span><span class="sxs-lookup"><span data-stu-id="22593-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="22593-200">您可以對應用程式資料和記錄使用不同的儲存體帳戶，以及您可以 [對資料使用多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="22593-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="22593-201">在本教學課程中，您將使用單一儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="22593-202">hello 連接字串具有 hello 儲存體帳戶金鑰的預留位置。</span><span class="sxs-lookup"><span data-stu-id="22593-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="22593-203">根據預設，hello WebJobs SDK 會尋找名為 AzureWebJobsStorage 和 AzureWebJobsDashboard 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="22593-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="22593-204">或者，您可以[hello 連接字串儲存，但是您想要傳入明確 toohello`JobHost`物件](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config)。</span><span class="sxs-lookup"><span data-stu-id="22593-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="22593-205">這兩個儲存體連接字串取代為您之前複製的 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="22593-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="22593-206">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="22593-206">Save your changes.</span></span>

## <span data-ttu-id="22593-207"><a id="run"></a>在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="22593-208">toostart hello web 前端的 hello 應用程式，請按 CTRL + F5。</span><span class="sxs-lookup"><span data-stu-id="22593-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="22593-209">hello 預設瀏覽器會開啟 toohello 首頁。</span><span class="sxs-lookup"><span data-stu-id="22593-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="22593-210">(hello web 專案會執行，因為您取消了 hello 啟始專案。)</span><span class="sxs-lookup"><span data-stu-id="22593-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="22593-212">toostart hello WebJob 後端的 hello 應用程式，以滑鼠右鍵按一下中的 hello ContosoAdsWebJob 專案**方案總管 中**，然後按一下**偵錯** > **開始新執行個體**.</span><span class="sxs-lookup"><span data-stu-id="22593-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="22593-213">主控台應用程式視窗開啟，並顯示表示 hello WebJobs SDK JobHost 物件已開始 toorun 記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="22593-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![執行主控台應用程式視窗中顯示該 hello 後端](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="22593-215">在您的瀏覽器中按一下 [建立廣告]。</span><span class="sxs-lookup"><span data-stu-id="22593-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="22593-216">輸入一些測試資料、 選取映像 tooupload，，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="22593-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="22593-218">hello 應用程式 toohello 索引頁面上，但它不會顯示 hello 新 ad 縮圖，因為該處理尚未尚未發生。</span><span class="sxs-lookup"><span data-stu-id="22593-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="22593-219">同時之後簡短等候, hello 主控台應用程式視窗中的記錄訊息會顯示佇列訊息被接收，而且已經處理。</span><span class="sxs-lookup"><span data-stu-id="22593-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="22593-221">您會看到 hello hello 主控台應用程式視窗中的記錄訊息之後，重新整理 hello 索引頁面 toosee hello 縮圖。</span><span class="sxs-lookup"><span data-stu-id="22593-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![索引頁面](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="22593-223">按一下**詳細資料**ad toosee hello 全尺寸映像。</span><span class="sxs-lookup"><span data-stu-id="22593-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="22593-225">您已在您的本機電腦上執行 hello 應用程式和使用 SQL Server 資料庫位於您的電腦，但它會使用佇列和 blob 中 hello 雲端。</span><span class="sxs-lookup"><span data-stu-id="22593-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="22593-226">在下列章節的 hello 您將執行 hello 應用程式 hello 雲端中使用的雲端資料庫，以及雲端 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="22593-227"><a id="runincloud"></a>在 hello 雲端中執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="22593-228">您將會執行 hello 遵循 hello 雲端中的步驟 toorun hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="22593-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="22593-229">部署 tooWeb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="22593-230">Visual Studio 會在 App Service 和 SQL 資料庫執行個體中自動建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="22593-231">設定 hello web 應用程式 toouse Azure SQL database 與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="22593-232">您已建立一些廣告時 hello 雲端中執行之後，您會檢視 hello WebJobs SDK 儀表板 toosee hello 豐富的監視功能，它有 toooffer。</span><span class="sxs-lookup"><span data-stu-id="22593-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="22593-233">部署 tooWeb 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="22593-234">關閉 hello 瀏覽器和 hello 主控台應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="22593-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="22593-235">Hello 中的 hello 步驟[發行 SQL Database 的 tooAzure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) > 一節。</span><span class="sxs-lookup"><span data-stu-id="22593-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="22593-236">完成部署的 hello 步驟之後，繼續這篇文章中的 hello 其餘工作。</span><span class="sxs-lookup"><span data-stu-id="22593-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="22593-237">設定 hello web 應用程式 toouse Azure SQL database 與儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="22593-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="22593-238">安全性最佳作法是太[避免讓儲存在儲存機制中的程式碼來源檔案中的連接字串等機密資訊](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)。</span><span class="sxs-lookup"><span data-stu-id="22593-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="22593-239">Azure 提供的方式 toodo 的： 您可以在 hello Azure 環境中，設定連接字串和其他設定值，以及 ASP.NET 組態應用程式開發介面會自動挑選這些值在 Azure 中的 hello 應用程式執行時。</span><span class="sxs-lookup"><span data-stu-id="22593-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="22593-240">您也可以使用在 Azure 中設定這些值**伺服器總管**、 hello Azure 網站、 Windows PowerShell 或 hello 跨平台命令列介面。</span><span class="sxs-lookup"><span data-stu-id="22593-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="22593-241">如需詳細資訊，請參閱 [應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="22593-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="22593-242">在本節中，您會使用**伺服器總管**tooset 連接字串值，在 Azure 中的。</span><span class="sxs-lookup"><span data-stu-id="22593-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="22593-243">在 伺服器總管 中，於 Azure > App Service > {您的資源群組} 下的 Web 應用程式上按一下滑鼠右鍵，然後按一下檢視設定。</span><span class="sxs-lookup"><span data-stu-id="22593-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="22593-244">hello **Azure Web 應用程式**hello 上開啟的視窗**組態** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="22593-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="22593-245">Hello DefaultConnection 連接字串 toohello 名稱變更 hello 名稱您選擇在 hello 設定 hello SQL database 時[發行 SQL Database 的 tooAzure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database)發行項。</span><span class="sxs-lookup"><span data-stu-id="22593-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="22593-246">Azure 會自動建立此連接字串，當您建立 hello web 應用程式與相關聯的資料庫，所以它已有 hello 正確的連接字串值。</span><span class="sxs-lookup"><span data-stu-id="22593-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="22593-247">您要變更只 hello 名稱 toowhat 尋找您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="22593-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="22593-248">新增兩個新的連接字串，將他們命名為 AzureWebJobsStorage 和 AzureWebJobsDashboard。</span><span class="sxs-lookup"><span data-stu-id="22593-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="22593-249">設定得 hello 資料庫類型**自訂**，和集合 hello 連接字串值 toohello 相同的值，您使用稍早 hello *Web.config*和*App.config*檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="22593-250">（請確定您包含 hello 整個連接字串中，不只是 hello 存取金鑰，並不會包含 hello 引號）。</span><span class="sxs-lookup"><span data-stu-id="22593-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="22593-251">Hello WebJobs SDK，一個應用程式資料，一個用於記錄會使用這些連接字串。</span><span class="sxs-lookup"><span data-stu-id="22593-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="22593-252">如稍早所見，hello web 前端的程式碼也會使用應用程式資料的其中一個 hello。</span><span class="sxs-lookup"><span data-stu-id="22593-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="22593-253">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="22593-253">Click **Save**.</span></span>

    ![Azure 入口網站中的連接字串](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="22593-255">在**伺服器總管**hello web 應用程式，以滑鼠右鍵按一下，然後按**停止**。</span><span class="sxs-lookup"><span data-stu-id="22593-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="22593-256">Hello web 應用程式停止之後，再次以滑鼠右鍵按一下 hello web 應用程式，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="22593-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="22593-257">當您發行，但它會停止進行組態變更時，會自動啟動 hello WebJob。</span><span class="sxs-lookup"><span data-stu-id="22593-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="22593-258">toorestart，您可以重新啟動 hello web 應用程式，或在 hello 中重新啟動 hello WebJob [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)。</span><span class="sxs-lookup"><span data-stu-id="22593-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="22593-259">它通常建議的 toorestart hello web 應用程式之後設定變更時。</span><span class="sxs-lookup"><span data-stu-id="22593-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="22593-260">重新整理已 hello web 應用程式 URL，其網址列中的 hello 瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="22593-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="22593-261">hello 首頁會出現。</span><span class="sxs-lookup"><span data-stu-id="22593-261">hello home page appears.</span></span>
8. <span data-ttu-id="22593-262">建立 ad，您可以如同時您[執行 hello 應用程式在本機](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)。</span><span class="sxs-lookup"><span data-stu-id="22593-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="22593-263">下一開始的縮圖，顯示 hello 索引頁面。</span><span class="sxs-lookup"><span data-stu-id="22593-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="22593-264">幾秒之後重新整理 hello 頁面並 hello 縮圖出現。</span><span class="sxs-lookup"><span data-stu-id="22593-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="22593-265">如果未出現 hello 縮圖，您可能會有 toowait 約一分鐘 hello WebJob toorestart。</span><span class="sxs-lookup"><span data-stu-id="22593-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="22593-266">如果一段時間之後，您仍然看 hello 縮圖，當您重新整理 hello] 頁面上，[hello WebJob 可能不會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="22593-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="22593-267">在此情況下，移 toohello**應用程式服務**刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com/)，找出您的 web 應用程式，然後按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="22593-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="22593-268">檢視 hello WebJobs SDK 儀表板</span><span class="sxs-lookup"><span data-stu-id="22593-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="22593-269">在 hello [Azure 入口網站](https://portal.azure.com/)，選取 hello**應用程式服務刀鋒視窗**，找出您的 web 應用程式，並選取**WebJobs**。</span><span class="sxs-lookup"><span data-stu-id="22593-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="22593-270">選取 hello**記錄** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="22593-270">Select hello **Logs** tab.</span></span>

    ![記錄索引標籤](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="22593-272">新的瀏覽器索引標籤會開啟 toohello WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="22593-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="22593-273">hello 儀表板會顯示該 hello web 工作正在執行，並顯示您的程式碼 WebJobs SDK 所觸發的 hello 函式的清單。</span><span class="sxs-lookup"><span data-stu-id="22593-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="22593-274">按一下其中一個執行有關的 hello 函式 toosee 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="22593-274">Click one of hello functions toosee details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="22593-277">hello **Replay 函式**此頁面上的按鈕會導致 hello WebJobs SDK framework toocall hello 函式一次，並可提供您機會 toochange hello 傳遞資料 toohello 函式第一次。</span><span class="sxs-lookup"><span data-stu-id="22593-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="22593-278">當您完成測試，請考慮刪除 hello web 應用程式、 儲存體帳戶和您的 SQL Database 執行個體。</span><span class="sxs-lookup"><span data-stu-id="22593-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="22593-279">hello web 應用程式是免費的但 hello SQL 儲存體帳戶和資料庫執行個體都會產生費用 (雖然 toohello 較小，因為最小)。</span><span class="sxs-lookup"><span data-stu-id="22593-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="22593-280">此外，如果您離開 hello web 應用程式執行時，您的 URL 會尋找任何人可以建立及檢視廣告。</span><span class="sxs-lookup"><span data-stu-id="22593-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="22593-281">刪除 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-281">Delete your web app</span></span>
<span data-ttu-id="22593-282">在 hello 入口網站中，移 toohello**應用程式服務**刀鋒視窗中，找出並選取您的 web 應用程式，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="22593-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="22593-283">如果您只想 tootemporarily 防止其他人從存取 hello web 應用程式，請按一下**停止**改為。</span><span class="sxs-lookup"><span data-stu-id="22593-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="22593-284">在此情況下，費用將繼續 tooaccrue hello SQL 資料庫和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="22593-285">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="22593-285">Delete your storage account</span></span>
<span data-ttu-id="22593-286">toodelete 儲存體帳戶，請參閱[刪除儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="22593-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="22593-287">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="22593-287">Delete your database</span></span>
<span data-ttu-id="22593-288">toodelete SQL 資料庫，請參閱 hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/)文件。</span><span class="sxs-lookup"><span data-stu-id="22593-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="22593-289"><a id="create"></a>從頭開始建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="22593-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="22593-290">本節中，您將會執行下列工作 hello:</span><span class="sxs-lookup"><span data-stu-id="22593-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="22593-291">使用 Web 專案建立 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="22593-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="22593-292">加入類別庫專案 hello 資料 hello 前端及後端之間共用的存取層。</span><span class="sxs-lookup"><span data-stu-id="22593-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="22593-293">使用 WebJobs 部署啟用加入 hello 後端中，主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="22593-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="22593-294">新增 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="22593-294">Add NuGet packages.</span></span>
* <span data-ttu-id="22593-295">設定專案參考。</span><span class="sxs-lookup"><span data-stu-id="22593-295">Set project references.</span></span>
* <span data-ttu-id="22593-296">複製應用程式程式碼和組態檔案從您使用過 hello hello 教學課程的上一節中的 hello 下載應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="22593-297">檢閱 hello hello 程式碼部分與 Azure blob 和佇列並 hello WebJobs SDK。</span><span class="sxs-lookup"><span data-stu-id="22593-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="22593-298">使用 Web 專案和類別庫專案建立 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="22593-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="22593-299">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="22593-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="22593-300">在 [hello**新專案**] 對話方塊中，選擇**Visual C#** > **Web** > **ASP.NET Web 應用程式 (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="22593-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="22593-301">Hello 專案 ContosoAdsWeb、 hello 方案 ContosoAdsWebJobsSDK 命名 (變更 hello 方案名稱，如果您要將它放置在 hello hello 與相同的資料夾會下載解決方案)，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22593-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![New Project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="22593-303">在 hello**新的 ASP.NET Web 應用程式** 對話方塊中，選擇 hello MVC 範本，並選取 **變更驗證**。</span><span class="sxs-lookup"><span data-stu-id="22593-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![變更驗證](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="22593-305">在 hello**變更驗證** 對話方塊中，選擇**非驗證**，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22593-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![不需要驗證](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="22593-307">在 [hello**新的 ASP.NET Web 應用程式**] 對話方塊中，按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22593-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="22593-308">Visual Studio 建立 hello 方案和 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="22593-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="22593-309">在**方案總管] 中**，以滑鼠右鍵按一下 hello 方案 （不 hello 專案），然後選擇 [**新增** > **新專案**。</span><span class="sxs-lookup"><span data-stu-id="22593-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="22593-310">在 [hello**加入新的專案**] 對話方塊中，選擇**Visual C#** > **的傳統 Windows 桌面** > **類別程式庫 (.NET架構）**範本。</span><span class="sxs-lookup"><span data-stu-id="22593-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="22593-311">名稱 hello 專案*ContosoAdsCommon*，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="22593-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="22593-312">這個專案會包含 hello Entity Framework 內容和 hello 資料模型的這兩個 hello 前端和後端將會使用。</span><span class="sxs-lookup"><span data-stu-id="22593-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="22593-313">或者，可以在 hello web 專案中定義 hello EF 相關類別，從 hello WebJob 專案參考該專案。</span><span class="sxs-lookup"><span data-stu-id="22593-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="22593-314">但是，然後在 WebJob 專案必須參考 tooweb 組件，它不需要。</span><span class="sxs-lookup"><span data-stu-id="22593-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="22593-315">新增已啟用 WebJobs 部署的主控台應用程式專案</span><span class="sxs-lookup"><span data-stu-id="22593-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="22593-316">Hello web 專案 （非 hello 方案或 hello 類別庫專案），以滑鼠右鍵按一下，然後按一下**新增** > **新增 Azure WebJob 專案**。</span><span class="sxs-lookup"><span data-stu-id="22593-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="22593-318">在 hello**新增 Azure WebJob**  對話方塊中，輸入這兩個 hello ContosoAdsWebJob**專案名稱**和 hello **WebJob 名稱**。</span><span class="sxs-lookup"><span data-stu-id="22593-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="22593-319">保留**模式執行的 WebJob**設定得**持續執行**。</span><span class="sxs-lookup"><span data-stu-id="22593-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="22593-320">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="22593-320">Click **OK**.</span></span>

   <span data-ttu-id="22593-321">Visual Studio 建立主控台應用程式所設定的 toodeploy webjob 每當您將部署的 hello web 專案。</span><span class="sxs-lookup"><span data-stu-id="22593-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="22593-322">它會執行下列工作建立 hello 專案後的 hello toodo:</span><span class="sxs-lookup"><span data-stu-id="22593-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="22593-323">加入*webjob 發行 settings.json* hello WebJob 專案屬性 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="22593-324">加入*webjobs list.json* hello web 專案屬性 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="22593-325">Hello Microsoft.Web.WebJobs.Publish NuGet 封裝安裝在 hello WebJob 專案中。</span><span class="sxs-lookup"><span data-stu-id="22593-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="22593-326">如需有關這些變更的詳細資訊，請參閱[如何使用 Visual Studio toodeploy WebJobs](websites-dotnet-deploy-webjobs.md)。</span><span class="sxs-lookup"><span data-stu-id="22593-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="22593-327">新增 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="22593-327">Add NuGet packages</span></span>
<span data-ttu-id="22593-328">WebJob 專案的 hello 新專案範本會自動安裝 hello WebJobs SDK 的 NuGet 套件[Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs)及其相依項目。</span><span class="sxs-lookup"><span data-stu-id="22593-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="22593-329">其中一個 hello hello WebJob 專案中自動安裝 WebJobs SDK 相依性是 hello Azure 儲存體用戶端程式庫 (SCL)。</span><span class="sxs-lookup"><span data-stu-id="22593-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="22593-330">不過，您需要 tooadd 它 toohello web 專案 toowork 使用 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="22593-331">開啟 hello**管理 NuGet 封裝**hello 解決方案的對話方塊。</span><span class="sxs-lookup"><span data-stu-id="22593-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="22593-332">Hello 左窗格中，選取**安裝封裝**。</span><span class="sxs-lookup"><span data-stu-id="22593-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="22593-333">尋找 hello *Azure 儲存體*封裝，然後按一下**管理**。</span><span class="sxs-lookup"><span data-stu-id="22593-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="22593-334">在 hello**選取專案** 方塊中，選取 hello **ContosoAdsWeb**核取方塊，然後**確定**。</span><span class="sxs-lookup"><span data-stu-id="22593-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="22593-335">所有的三個專案使用 hello Entity Framework toowork SQL 資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="22593-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="22593-336">Hello 左窗格中，選取**線上**。</span><span class="sxs-lookup"><span data-stu-id="22593-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="22593-337">尋找 hello *EntityFramework* NuGet 封裝，並將它安裝在所有的三個專案。</span><span class="sxs-lookup"><span data-stu-id="22593-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="22593-338">設定專案參考</span><span class="sxs-lookup"><span data-stu-id="22593-338">Set project references</span></span>
<span data-ttu-id="22593-339">Web 和 WebJob 專案，使用 hello SQL 資料庫，因此兩者都必須參考 toohello ContosoAdsCommon 專案。</span><span class="sxs-lookup"><span data-stu-id="22593-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="22593-340">在 hello ContosoAdsWeb 專案設定參考 toohello ContosoAdsCommon 專案。</span><span class="sxs-lookup"><span data-stu-id="22593-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="22593-341">(Hello ContosoAdsWeb 專案中，以滑鼠右鍵按一下，然後按一下**新增** > **參考**。</span><span class="sxs-lookup"><span data-stu-id="22593-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="22593-342">在 hello**參考管理員**對話方塊中，選取**專案** > **方案** > **ContosoAdsCommon**，然後按一下**確定**。)</span><span class="sxs-lookup"><span data-stu-id="22593-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="22593-343">hello WebJob 專案必須參考使用映像以及存取連接字串。</span><span class="sxs-lookup"><span data-stu-id="22593-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="22593-344">在 hello ContosoAdsWebJob 專案中，設定參照太`System.Drawing`和`System.Configuration`。</span><span class="sxs-lookup"><span data-stu-id="22593-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="22593-345">新增程式碼和組態檔</span><span class="sxs-lookup"><span data-stu-id="22593-345">Add code and configuration files</span></span>
<span data-ttu-id="22593-346">本教學課程不會顯示如何太[建立 MVC 控制器和檢視使用 scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)、 如何太[撰寫適用於 SQL Server 資料庫的 Entity Framework 程式碼](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)，或[hello 的基本概念非同步程式設計中 ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)。</span><span class="sxs-lookup"><span data-stu-id="22593-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="22593-347">因此，所有會維持為 toodo 是從下載的 hello 方案到 hello 新解決方案的複製程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="22593-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="22593-348">這麼做之後，hello 下列各節顯示並說明 hello 程式碼的關鍵部分。</span><span class="sxs-lookup"><span data-stu-id="22593-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="22593-349">tooadd 檔案 tooa 專案或資料夾、 以滑鼠右鍵按一下 hello 專案或資料夾並按一下**新增** > **現有項目**。</span><span class="sxs-lookup"><span data-stu-id="22593-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="22593-350">選取 hello 檔案和按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="22593-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="22593-351">如果系統詢問您是否想 tooreplace 現有檔案，按一下**是**。</span><span class="sxs-lookup"><span data-stu-id="22593-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="22593-352">在 hello ContosoAdsCommon 專案中，刪除 hello *Class1.cs*檔案，然後加入下列檔案從下載的 hello 專案及其位置 hello 中。</span><span class="sxs-lookup"><span data-stu-id="22593-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="22593-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-353">*Ad.cs*</span></span>
   * <span data-ttu-id="22593-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="22593-355">BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="22593-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="22593-356">在 hello ContosoAdsWeb 專案中，新增 hello hello 下載專案中的下列檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="22593-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="22593-357">*Web.config*</span></span>
   * <span data-ttu-id="22593-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="22593-359">在 hello*控制器*資料夾： *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="22593-360">在 hello *_layout.cshtml*資料夾： *_Layout.cshtml*檔案</span><span class="sxs-lookup"><span data-stu-id="22593-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="22593-361">在 hello *Views\Home*資料夾： *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="22593-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="22593-362">在 hello *Views\Ad*資料夾 （第一次建立 hello 資料夾）： 五個*.cshtml*檔案</span><span class="sxs-lookup"><span data-stu-id="22593-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="22593-363">在 hello ContosoAdsWebJob 專案中，新增 hello hello 下載專案中的下列檔案。</span><span class="sxs-lookup"><span data-stu-id="22593-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="22593-364">*App.config* (也變更 hello 檔案類型篩選**所有檔案**)</span><span class="sxs-lookup"><span data-stu-id="22593-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="22593-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-365">*Program.cs*</span></span>
   * <span data-ttu-id="22593-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="22593-366">*Functions.cs*</span></span>

<span data-ttu-id="22593-367">您現在可以建置、 執行及部署如稍早在 hello 教學課程中所指示的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="22593-368">您這麼做之前，不過，停止 hello 仍在執行部署到 hello 第一個 web 應用程式中的 WebJob。</span><span class="sxs-lookup"><span data-stu-id="22593-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="22593-369">否則，該 WebJob 會處理在本機建立的佇列訊息或由執行新的 web 應用程式中的 hello 應用程式，因為所有使用 hello 相同儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="22593-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="22593-370"><a id="code"></a>檢閱 hello 應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="22593-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="22593-371">hello 下列各節說明 hello 程式碼相關的 tooworking 以 hello WebJobs SDK 和 Azure 儲存體 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="22593-372">如 hello 程式碼特定 toohello WebJobs SDK，請移至 toohello [Program.cs 和 Functions.cs](#programcs)區段。</span><span class="sxs-lookup"><span data-stu-id="22593-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="22593-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="22593-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="22593-374">hello Ad.cs 檔案定義 ad 類別列舉和廣告資訊的 POCO 實體類別。</span><span class="sxs-lookup"><span data-stu-id="22593-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="22593-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="22593-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="22593-376">hello ContosoAdsContext 類別指定 hello Ad 類別用於 DbSet 集合，其中 Entity Framework 將儲存在 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="22593-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="22593-377">hello 類別有兩個建構函式。</span><span class="sxs-lookup"><span data-stu-id="22593-377">hello class has two constructors.</span></span> <span data-ttu-id="22593-378">hello 首先 hello web 專案中，使用，並指定連接字串儲存在 hello Web.config 檔案或 hello Azure 執行階段環境的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="22593-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="22593-379">hello 第二個建構函式可讓您 toopass hello 實際的連接字串中。</span><span class="sxs-lookup"><span data-stu-id="22593-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="22593-380">是因為它沒有 Web.config 檔需要 hello WebJob 專案。</span><span class="sxs-lookup"><span data-stu-id="22593-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="22593-381">之前看到這個連接字串的儲存位置，而您會看到如何 hello 程式碼會擷取 hello 連接字串時，它會具現化 hello DbContext 類別。</span><span class="sxs-lookup"><span data-stu-id="22593-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="22593-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="22593-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="22593-383">hello`BlobInformation`類別是使用的 toostore 佇列訊息中的映像 blob 資訊。</span><span class="sxs-lookup"><span data-stu-id="22593-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="22593-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="22593-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="22593-385">程式碼從 hello 呼叫`Application_Start`方法會建立*映像*blob 容器和*映像*排入佇列，如果它們不存在。</span><span class="sxs-lookup"><span data-stu-id="22593-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="22593-386">這可確保每當您開始使用新的儲存體帳戶，hello 必要的 blob 容器和佇列會自動建立。</span><span class="sxs-lookup"><span data-stu-id="22593-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="22593-387">使用從 hello hello 儲存體連接字串 hello 程式碼取得存取 toohello 儲存體帳戶*Web.config*檔案或 Azure 執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="22593-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="22593-388">然後，它會取得參考 toohello*映像*blob 容器時，如果它不存在，並設定存取權限 hello 新的容器建立 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="22593-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="22593-389">根據預設，新的容器允許透過儲存體帳戶認證 tooaccess blob 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="22593-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="22593-390">hello web 應用程式需要 hello blob toobe 公開，讓它可以顯示使用該點 toohello 映像 blob Url 的映像。</span><span class="sxs-lookup"><span data-stu-id="22593-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="22593-391">類似的程式碼取得參考 toohello *thumbnailrequest*佇列，並建立新的佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="22593-392">在此情況下，即不需要變更權限。</span><span class="sxs-lookup"><span data-stu-id="22593-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="22593-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="22593-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="22593-394">hello *_Layout.cshtml*檔案設定中 hello 頁首和頁尾，hello 應用程式名稱，並建立"廣告 」 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="22593-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="22593-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="22593-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="22593-396">hello *Views\Home\Index.cshtml*檔案 hello 首頁上顯示類別目錄連結。</span><span class="sxs-lookup"><span data-stu-id="22593-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="22593-397">hello 連結傳遞 hello 整數值的 hello `Category` querystring 變數 toohello 廣告索引頁面中的列舉。</span><span class="sxs-lookup"><span data-stu-id="22593-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="22593-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="22593-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="22593-399">在 hello *AdController.cs*檔案、 hello 建構函式呼叫 hello`InitializeStorage`方法 toocreate Azure 儲存體用戶端程式庫物件，提供應用程式開發介面使用的 blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="22593-400">然後，hello 程式碼會取得參考 toohello*映像*blob 容器，如稍早在您所見*Global.asax.cs*。</span><span class="sxs-lookup"><span data-stu-id="22593-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="22593-401">在執行該動作時，它會設定適用 Web 應用程式的預設 [重試原則](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) 。</span><span class="sxs-lookup"><span data-stu-id="22593-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="22593-402">hello 預設指數型輪詢重試原則無法停止回應 hello web 應用程式的時間超過一分鐘上重複的重試的暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="22593-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="22593-403">此處指定的 hello 重試原則會等待三秒鐘之後每個嘗試向上 toothree 嘗試。</span><span class="sxs-lookup"><span data-stu-id="22593-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="22593-404">類似的程式碼取得參考 toohello*映像*佇列。</span><span class="sxs-lookup"><span data-stu-id="22593-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="22593-405">大部分的 hello 控制器程式碼是使用 Entity Framework 資料模型使用 DbContext 類別的一般。</span><span class="sxs-lookup"><span data-stu-id="22593-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="22593-406">例外狀況為 hello HttpPost`Create`方法，這個方法會將檔案上傳，並將它儲存在 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="22593-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="22593-407">hello 模型繫結器提供[HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 方法的物件。</span><span class="sxs-lookup"><span data-stu-id="22593-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="22593-408">如果 hello 使用者選取檔案 tooupload，hello 程式碼會 hello 檔案上傳、 將它儲存在 blob，並更新 hello Ad 資料庫記錄點 toohello blob 的 URL。</span><span class="sxs-lookup"><span data-stu-id="22593-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="22593-409">hello 沒有 hello 上傳的程式碼處於 hello`UploadAndSaveBlobAsync`方法。</span><span class="sxs-lookup"><span data-stu-id="22593-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="22593-410">它會建立 GUID hello blob、 上傳和儲存 hello 檔案，並傳回參考 toohello 儲存 blob。</span><span class="sxs-lookup"><span data-stu-id="22593-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="22593-411">之後 hello HttpPost`Create`方法上傳 blob 並更新 hello 資料庫，它會建立佇列訊息 tooinform hello 後端程序映像可供轉換 tooa 縮圖。</span><span class="sxs-lookup"><span data-stu-id="22593-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="22593-412">hello 碼 hello HttpPost`Edit`方法很類似，不同之處在於如果 hello 使用者選取新的映像檔，必須刪除此 ad 已存在的任何 blob。</span><span class="sxs-lookup"><span data-stu-id="22593-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="22593-413">以下是當您刪除廣告時，會刪除 blob 的 hello 程式碼：</span><span class="sxs-lookup"><span data-stu-id="22593-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="22593-414">ContosoAdsWeb - Views\Ad\Index.cshtml 和 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="22593-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="22593-415">hello *Index.cshtml*檔案就會顯示以 hello 的縮圖，其他的 ad 資料：</span><span class="sxs-lookup"><span data-stu-id="22593-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="22593-416">hello *Details.cshtml*檔案會顯示 hello 完整大小的影像：</span><span class="sxs-lookup"><span data-stu-id="22593-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="22593-417">ContosoAdsWeb - Views\Ad\Create.cshtml 和 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="22593-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="22593-418">hello *Create.cshtml*和*Edit.cshtml*檔案會指定表單編碼可讓 hello 控制器 tooget hello`HttpPostedFileBase`物件。</span><span class="sxs-lookup"><span data-stu-id="22593-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="22593-419">`<input>`項目會告知 hello 瀏覽器 tooprovide 檔案選取對話方塊。</span><span class="sxs-lookup"><span data-stu-id="22593-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="22593-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="22593-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="22593-421">當 hello WebJob 啟動 hello`Main`方法呼叫 hello WebJobs SDK`JobHost.RunAndBlock`方法 toobegin 觸發的函式 hello 目前執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="22593-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="22593-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 方法</span><span class="sxs-lookup"><span data-stu-id="22593-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="22593-423">接收佇列訊息時，hello WebJobs SDK 會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="22593-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="22593-424">hello 方法會建立縮圖，並將 hello 縮圖 hello 資料庫中的 URL。</span><span class="sxs-lookup"><span data-stu-id="22593-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="22593-425">hello`QueueTrigger`屬性會指示 hello WebJobs SDK toocall 這個方法 hello thumbnailrequest 佇列上收到一封新郵件時。</span><span class="sxs-lookup"><span data-stu-id="22593-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="22593-426">hello `BlobInformation` hello 佇列訊息中的物件是自動還原序列化成 hello`blobInfo`參數。</span><span class="sxs-lookup"><span data-stu-id="22593-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="22593-427">Hello 方法完成時，就會刪除 hello 佇列訊息。</span><span class="sxs-lookup"><span data-stu-id="22593-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="22593-428">如果在完成之前，hello 方法失敗，則不會刪除 hello 佇列訊息;在 10 分鐘租用到期之後，hello 訊息會是發行的 toobe 再度收取和處理。</span><span class="sxs-lookup"><span data-stu-id="22593-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="22593-429">如果某個訊息總是導致例外狀況，則不會無限制地重複此順序。</span><span class="sxs-lookup"><span data-stu-id="22593-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="22593-430">Hello 訊息 5 失敗嘗試 tooprocess 訊息之後，是移動的 tooa 佇列名為 {queuename}-有害。</span><span class="sxs-lookup"><span data-stu-id="22593-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="22593-431">hello 的嘗試次數上限是可設定的。</span><span class="sxs-lookup"><span data-stu-id="22593-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="22593-432">兩個 hello`Blob`屬性提供的繫結的 tooblobs 物件： 一個 toohello 現有映像的 blob 和一個 tooa 新縮圖 blob hello 方法建立。</span><span class="sxs-lookup"><span data-stu-id="22593-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="22593-433">Blob 名稱來自於屬性的 hello `BlobInformation` hello 佇列郵件中收到的物件 (`BlobName`和`BlobNameWithoutExtension`)。</span><span class="sxs-lookup"><span data-stu-id="22593-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="22593-434">tooget hello 完整功能 hello 儲存體用戶端程式庫，您可以使用 hello`CloudBlockBlob`類別 toowork 與 blob。</span><span class="sxs-lookup"><span data-stu-id="22593-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="22593-435">如果您想 tooreuse 撰寫程式碼都已使用 toowork`Stream`物件，您可以使用 hello`Stream`類別。</span><span class="sxs-lookup"><span data-stu-id="22593-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="22593-436">如需有關如何 toowrite 函式都使用 WebJobs SDK 屬性，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="22593-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="22593-437">如何 toouse Azure 佇列儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="22593-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="22593-438">如何 toouse Azure blob 儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="22593-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="22593-439">如何 toouse Azure 資料表儲存體與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="22593-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="22593-440">如何 toouse Azure 服務匯流排與 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="22593-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="22593-441">如果您的 web 應用程式在多個 Vm 上執行，將會同時執行多個 WebJobs，在某些情況下這會導致 hello 相同資料進行處理多次。</span><span class="sxs-lookup"><span data-stu-id="22593-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="22593-442">如果您使用 hello 內建佇列、 blob 和 Service Bus 觸發程序，這是不發生問題。</span><span class="sxs-lookup"><span data-stu-id="22593-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="22593-443">hello SDK 可確保您的函式將會一次處理的每個訊息或 blob。</span><span class="sxs-lookup"><span data-stu-id="22593-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="22593-444">如需有關資訊 tooimplement 正常關機，請參閱[正常關機](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)。</span><span class="sxs-lookup"><span data-stu-id="22593-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="22593-445">hello hello 中的程式碼`ConvertImageToThumbnailJPG`（未顯示） 的方法會使用類別中 hello`System.Drawing`為了簡單起見命名空間。</span><span class="sxs-lookup"><span data-stu-id="22593-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="22593-446">不過，此命名空間中的 hello 類別針對搭配 Windows Form 使用所設計。</span><span class="sxs-lookup"><span data-stu-id="22593-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="22593-447">不支援將它們用於 Windows 或 ASP.NET 服務。</span><span class="sxs-lookup"><span data-stu-id="22593-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="22593-448">如需映像處理選項的詳細資訊，請參閱[動態映像產生](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx)和[深入調整映像大小](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)。</span><span class="sxs-lookup"><span data-stu-id="22593-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="22593-449">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22593-449">Next steps</span></span>
<span data-ttu-id="22593-450">在本教學課程中，您已經看到 hello WebJobs SDK 用於後端處理簡單多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="22593-451">如要進一步了解 ASP.NET 多層式應用程式和 WebJobs，請參考本節所提供的一些建議。</span><span class="sxs-lookup"><span data-stu-id="22593-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="22593-452">遺漏的功能</span><span class="sxs-lookup"><span data-stu-id="22593-452">Missing features</span></span>
<span data-ttu-id="22593-453">hello 應用程式已經過簡化，快速入門教學課程。</span><span class="sxs-lookup"><span data-stu-id="22593-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="22593-454">在真實世界的應用程式就會實作[相依性插入](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)和 hello[儲存機制和單位運作模式](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)，使用[記錄介面](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)，使用[EF Code First 移轉](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 資料模型變更，並使用[EF 連接恢復功能](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)toomanage 暫時性的網路錯誤。</span><span class="sxs-lookup"><span data-stu-id="22593-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="22593-455">調整 WebJob 的規模</span><span class="sxs-lookup"><span data-stu-id="22593-455">Scaling WebJobs</span></span>
<span data-ttu-id="22593-456">WebJobs hello 內容 web 應用程式中執行而且無法擴充分開。</span><span class="sxs-lookup"><span data-stu-id="22593-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="22593-457">比方說，如果您有一個標準的 web 應用程式執行個體，您只有一個執行個體背景程序執行，且使用部分 hello 伺服器的資源 （CPU、 記憶體等），否則將會使用 tooserve web 內容。</span><span class="sxs-lookup"><span data-stu-id="22593-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="22593-458">如果流量會因日或每週的時間，而且 hello 後端處理中，您需要可等候 toodo，您無法在低流量的時間排程 WebJobs toorun。</span><span class="sxs-lookup"><span data-stu-id="22593-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="22593-459">如果 hello 負載仍為該方案太高，您可以在不同的 web 應用程式專用的 webjob 執行 hello 後端，針對該目的項目。</span><span class="sxs-lookup"><span data-stu-id="22593-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="22593-460">接著您可以擴充後端 Web 應用程式，而不會影響到前端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22593-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="22593-461">如需詳細資訊，請參閱 [調整 WebJob](websites-webjobs-resources.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="22593-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="22593-462">避免關機時 Web 應用程式逾時</span><span class="sxs-lookup"><span data-stu-id="22593-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="22593-463">toomake 確定您的 WebJobs 會一直執行，而且在您 web 應用程式的所有執行個體上執行，您有 tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx)功能。</span><span class="sxs-lookup"><span data-stu-id="22593-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="22593-464">使用 hello 之外 WebJobs WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="22593-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="22593-465">Azure 在 WebJob 中使用 WebJobs SDK hello 的程式沒有 toorun。</span><span class="sxs-lookup"><span data-stu-id="22593-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="22593-466">它可以在本機執行，也可以在如雲端服務背景工作角色或 Windows 服務等其他環境中執行。</span><span class="sxs-lookup"><span data-stu-id="22593-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="22593-467">不過，您可以透過 Azure web 應用程式只能存取 hello WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="22593-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="22593-468">toouse hello 儀表板有 tooconnect hello web 應用程式 toohello 儲存您所使用的帳戶設定 hello AzureWebJobsDashboard 連接字串 hello**設定**hello 傳統入口網站 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="22593-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="22593-469">然後，您可以使用下列 URL 的 hello 取得 toohello 儀表板：</span><span class="sxs-lookup"><span data-stu-id="22593-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="22593-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="22593-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="22593-471">如需詳細資訊，請參閱[儀表板取得以 hello WebJobs SDK 的本機開發](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)，但請注意，它會顯示舊的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="22593-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="22593-472">其他 WebJobs 文件</span><span class="sxs-lookup"><span data-stu-id="22593-472">More WebJobs documentation</span></span>
<span data-ttu-id="22593-473">如需詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?LinkId=390226)。</span><span class="sxs-lookup"><span data-stu-id="22593-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
