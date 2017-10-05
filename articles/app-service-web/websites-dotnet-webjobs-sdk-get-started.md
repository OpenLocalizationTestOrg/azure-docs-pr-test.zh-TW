---
title: "在 Azure App Service 中建立 .NET WebJob | Microsoft Docs"
description: "使用 ASP.NET MVC 和 Azure 建立多層式應用程式。 前端是在 Azure App Service 的 Web 應用程式中執行，後端則是以 WebJob 形式執行。 該應用程式使用 Entity Framework、SQL Database 及 Azure 儲存體佇列和 Blob。"
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="0b995-105">在 Azure App Service 中建立 .NET WebJob</span><span class="sxs-lookup"><span data-stu-id="0b995-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="0b995-106">本教學指導示範如何為使用 [WebJobs SDK](websites-dotnet-webjobs-sdk.md)的簡單多層次 ASP.NET MVC 5 應用程式撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="0b995-107">[WebJobs SDK](websites-webjobs-resources.md) 的目的是為了簡化您對 WebJob 可執行的一般工作 (例如，映像處理、佇列處理、RSS 彙總、檔案維護和傳送電子郵件) 所撰寫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="0b995-108">WebJobs SDK 具有內建功能，用於處理 Azure 儲存體和服務匯流排、工作排程和處理錯誤，以及許多其他常見案例。</span><span class="sxs-lookup"><span data-stu-id="0b995-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="0b995-109">此外，它的設計具有擴充性，而且有 [擴充功能的開放原始碼儲存機制](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)。</span><span class="sxs-lookup"><span data-stu-id="0b995-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="0b995-110">此範例應用程式是廣告看板。</span><span class="sxs-lookup"><span data-stu-id="0b995-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="0b995-111">使用者可以上傳廣告的影像，然後後端程序會將影像轉換成縮圖。</span><span class="sxs-lookup"><span data-stu-id="0b995-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="0b995-112">廣告清單頁面會顯示縮圖，而廣告詳細資料頁面則會顯示完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="0b995-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="0b995-113">以下為螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="0b995-113">Here's a screenshot:</span></span>

![Ad list](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="0b995-115">此範例應用程式能夠與 [Azure 佇列](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 和 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage) 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="0b995-116">本教學課程顯示如何將應用程式部署至 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 和 [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)。</span><span class="sxs-lookup"><span data-stu-id="0b995-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="0b995-117"><a id="prerequisites"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="0b995-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="0b995-118">本教學課程假設您知道如何在 Visual Studio 中使用 [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) 專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="0b995-119">本教學課程一開始是針對 Visual Studio 2013 所撰寫，但可以與更新版本的 Visual Studio 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="0b995-120">如果您要使用 Visual Studio 2015 或 2017，請注意，在本機執行應用程式之前，您必須將 Web.config 和 App.config 檔案中 SQL Server LocalDB 連接字串的 `Data Source` 部分，從 `Data Source=(localdb)\v11.0` 變更為 `Data Source=(LocalDb)\MSSQLLocalDB`。</span><span class="sxs-lookup"><span data-stu-id="0b995-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="0b995-121"><a name="note"></a>您必須具備 Azure 帳戶，才能完成此教學課程：</span><span class="sxs-lookup"><span data-stu-id="0b995-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="0b995-122">您可以[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)：您將取得可試用付費 Azure 服務的額度，即使在額度用完後，您仍可保留帳戶，並使用免費的 Azure 服務，例如「網站」。</span><span class="sxs-lookup"><span data-stu-id="0b995-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="0b995-123">除非您明確變更您的設定且同意付費，否則我們將不會從您的信用卡收取任何費用。</span><span class="sxs-lookup"><span data-stu-id="0b995-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="0b995-124">您可以[啟用 Visual Studio 訂閱者的每月 Azure 額度](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)：您的訂用帳戶每個月都會提供額度，供您用在付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="0b995-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="0b995-125">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0b995-126">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="0b995-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="0b995-127"><a id="learn"></a>您將學到什麼</span><span class="sxs-lookup"><span data-stu-id="0b995-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="0b995-128">本教學課程說明如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="0b995-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="0b995-129">安裝 Azure SDK 好讓電腦適合用於進行 Azure 開發 (僅適用於 Visual Studio 2013 和 2015 使用者)。</span><span class="sxs-lookup"><span data-stu-id="0b995-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="0b995-130">建立會在您部署相關的 Web 專案時，自動部署成為 Azure WebJob 的主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="0b995-131">在開發電腦上本機測試 WebJobs SDK 後端。</span><span class="sxs-lookup"><span data-stu-id="0b995-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="0b995-132">將具有 WebJob 後端的應用程式發佈至 App Service 中的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="0b995-133">上傳檔案，並將檔案儲存在 Azure Blob 服務。</span><span class="sxs-lookup"><span data-stu-id="0b995-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="0b995-134">運用 Azure WebJobs SDK 來使用 Azure 儲存體佇列和 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="0b995-135"><a id="contosoads"></a>應用程式架構</span><span class="sxs-lookup"><span data-stu-id="0b995-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="0b995-136">此範例應用程式會使用 [以佇列為中心的工作模式](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) ，將建立縮圖這個需要大量 CPU 的工作轉變為後端程序。</span><span class="sxs-lookup"><span data-stu-id="0b995-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="0b995-137">本應用程式會將廣告儲存在 SQL 資料庫中，使用 Entity Framework Code First 來建立表格和存取資料。</span><span class="sxs-lookup"><span data-stu-id="0b995-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="0b995-138">針對每個廣告，資料庫會儲存兩個 URL：一個用於完整大小的影像，而另一個用於縮圖。</span><span class="sxs-lookup"><span data-stu-id="0b995-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Ad table](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="0b995-140">當使用者上傳影像時，Web 應用程式會將影像儲存在 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)，並將廣告資訊 (內含指向該 Blob 的 URL) 儲存在資料庫。</span><span class="sxs-lookup"><span data-stu-id="0b995-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="0b995-141">同時會將訊息寫入 Azure 佇列。</span><span class="sxs-lookup"><span data-stu-id="0b995-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="0b995-142">在以 Azure WebJob 形式執行的後端處理中，WebJobs SDK 會輪詢佇列以尋找新訊息。</span><span class="sxs-lookup"><span data-stu-id="0b995-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="0b995-143">出現新訊息時，WebJob 便會建立該影像的縮圖，並更新該廣告的縮圖 URL 資料庫欄位。</span><span class="sxs-lookup"><span data-stu-id="0b995-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="0b995-144">以下圖表顯示應用程式的這些部分的互動情況：</span><span class="sxs-lookup"><span data-stu-id="0b995-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Contoso Ads architecture](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="0b995-146">本教學課程的指示適用於 Azure SDK for.NET 2.7.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0b995-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="0b995-147"><a id="storage"></a>建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0b995-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="0b995-148">Azure 儲存體帳戶可提供在雲端中儲存佇列和 Blob 資料的資源。</span><span class="sxs-lookup"><span data-stu-id="0b995-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="0b995-149">WebJobs SDK 也會使用該帳戶來儲存儀表板的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="0b995-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="0b995-150">在實際應用程式中，您通常會為應用程式資料與記錄資料建立不同的帳戶，並為測試資料與生產資料建立不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="0b995-151">在本教學課程中，您只會使用一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="0b995-152">在 Visual Studio 中開啟 [伺服器總管]  視窗。</span><span class="sxs-lookup"><span data-stu-id="0b995-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="0b995-153">以滑鼠右鍵按一下 **Azure** 節點，然後按一下 [連線至 Microsoft Azure 訂用帳戶...]。</span><span class="sxs-lookup"><span data-stu-id="0b995-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![連接到 Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="0b995-155">使用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="0b995-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="0b995-156">以滑鼠右鍵按一下 Azure 節點下的 [儲存體]，然後按一下 [建立儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="0b995-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![建立儲存體帳戶](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="0b995-158">在 [建立儲存體帳戶]  對話方塊中，輸入儲存體帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="0b995-159">這個名稱必須是唯一的 (其他 Azure 儲存體帳戶不可以有相同的名稱)。</span><span class="sxs-lookup"><span data-stu-id="0b995-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="0b995-160">如果您輸入的名稱已在使用中，則可以變更此名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="0b995-161">存取儲存體帳戶的 URL 會是 *{name}*.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="0b995-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="0b995-162">將 [區域或同質群組]  下拉式清單設為離您最近的區域。</span><span class="sxs-lookup"><span data-stu-id="0b995-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="0b995-163">此設定會指定哪個 Azure 資料中心將會主控您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="0b995-164">對於本教學課程，您的選擇將不會造成顯著的差異。</span><span class="sxs-lookup"><span data-stu-id="0b995-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="0b995-165">不過，對於生產 Web 應用程式，您會希望 Web 伺服器和儲存體帳戶都位於相同區域，以減少延遲和資料輸出費用。</span><span class="sxs-lookup"><span data-stu-id="0b995-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="0b995-166">您稍後將建立的 Web 應用程式資料中心應該盡可能接近可存取您 Web 應用程式的瀏覽器，以便將延遲降至最低。</span><span class="sxs-lookup"><span data-stu-id="0b995-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="0b995-167">將 [複寫] 下拉式清單設為 [本機備援]。</span><span class="sxs-lookup"><span data-stu-id="0b995-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="0b995-168">對儲存體帳戶啟用地理區域複寫時，儲存內容會複寫至次要資料中心，以便能在主要位置發生嚴重災難時容錯移轉至該位置。</span><span class="sxs-lookup"><span data-stu-id="0b995-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="0b995-169">地理區域複寫會引發額外成本。</span><span class="sxs-lookup"><span data-stu-id="0b995-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="0b995-170">對於測試和開發帳戶，您通常不會想要付費使用地理區域複寫功能。</span><span class="sxs-lookup"><span data-stu-id="0b995-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="0b995-171">如需詳細資訊，請參閱 [建立、管理或刪除儲存體帳戶](../storage/common/storage-create-storage-account.md)。</span><span class="sxs-lookup"><span data-stu-id="0b995-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="0b995-172">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-172">Click **Create**.</span></span>

    ![New storage account](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="0b995-174"><a id="download"></a>下載應用程式</span><span class="sxs-lookup"><span data-stu-id="0b995-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="0b995-175">下載並解壓縮 [已完成的方案](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)(英文)。</span><span class="sxs-lookup"><span data-stu-id="0b995-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="0b995-176">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="0b995-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="0b995-177">從 [檔案] 功能表中，依序選擇 [開啟] > [專案/方案]，並導覽至您下載方案的位置，然後開啟方案檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="0b995-178">按 CTRL+SHIFT+B 建置解決方案。</span><span class="sxs-lookup"><span data-stu-id="0b995-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="0b995-179">根據預設，Visual Studio 會自動還原未包含在 *.zip* 檔案中的 NuGet 封裝內容。</span><span class="sxs-lookup"><span data-stu-id="0b995-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="0b995-180">如果封裝未還原，請移至 [管理方案的 NuGet 套件] 對話方塊，然後按一下右上方的 [還原] 按鈕來手動安裝。</span><span class="sxs-lookup"><span data-stu-id="0b995-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="0b995-181">在 [方案總管] 中，確定已選取 **ContosoAdsWeb** 作為啟始專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="0b995-182"><a id="configurestorage"></a>設定應用程式以使用儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0b995-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="0b995-183">開啟 ContosoAdsWeb 專案中的應用程式 *Web.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="0b995-184">此檔案包含 SQL 連接字串和用來使用 Blob 和佇列的 Azure 儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="0b995-185">SQL 連接字串會指向 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0b995-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="0b995-186">儲存體連接字串是具有儲存體帳戶名稱和存取金鑰預留位置的範例。</span><span class="sxs-lookup"><span data-stu-id="0b995-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="0b995-187">您將會使用具有您儲存體帳戶名稱和金鑰的連接字串來進行取代。</span><span class="sxs-lookup"><span data-stu-id="0b995-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="0b995-188">儲存體連接字串的名稱是 AzureWebJobsStorage，因為這是 WebJobs SDK 預設使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="0b995-189">這裡會使用相同的名稱，因此在 Azure 環境中您只需要設定一個連接字串值。</span><span class="sxs-lookup"><span data-stu-id="0b995-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="0b995-190">在 [伺服器總管] 中，在 [儲存體] 節點下方的儲存體帳戶上按一下滑鼠右鍵，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="0b995-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![按一下 [儲存體帳戶] 屬性](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="0b995-192">在 [屬性] 視窗中，按一下 [儲存體帳戶金鑰]，然後按一下省略符號。</span><span class="sxs-lookup"><span data-stu-id="0b995-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![儲存體帳戶金鑰](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="0b995-194">複製 [連接字串] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-194">Copy the **Connection String**.</span></span>

    ![[儲存體帳戶金鑰] 對話方塊](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="0b995-196">使用您剛才複製的連接字串來取代 *Web.config* 檔案中的儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="0b995-197">在貼上之前請確定您選取引號內的所有項目，但不包括引號。</span><span class="sxs-lookup"><span data-stu-id="0b995-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="0b995-198">開啟 ContosoAdsWebJob 專案中的 *App.config* 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="0b995-199">此檔案有兩個儲存體連接字串，一個供應用程式使用，另一個供記錄使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="0b995-200">您可以對應用程式資料和記錄使用不同的儲存體帳戶，以及您可以 [對資料使用多個儲存體帳戶](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)。</span><span class="sxs-lookup"><span data-stu-id="0b995-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="0b995-201">在本教學課程中，您將使用單一儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="0b995-202">連接字串具有儲存體帳戶金鑰的預留位置。</span><span class="sxs-lookup"><span data-stu-id="0b995-202">The connection strings have placeholders for the storage account keys.</span></span>

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

    <span data-ttu-id="0b995-203">依預設，WebJobs SDK 會尋找名為 AzureWebJobsStorage 和 AzureWebJobsDashboard 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="0b995-204">另一種方式是，您可以[任意儲存您要的連接字串，並將它明確傳遞至 `JobHost` 物件](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config)。</span><span class="sxs-lookup"><span data-stu-id="0b995-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="0b995-205">使用您先前複製的連接字串來取代這兩個儲存體連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="0b995-206">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0b995-206">Save your changes.</span></span>

## <span data-ttu-id="0b995-207"><a id="run"></a>在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="0b995-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="0b995-208">若要啟動應用程式的 Web 前端，請按 CTRL+F5。</span><span class="sxs-lookup"><span data-stu-id="0b995-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="0b995-209">預設瀏覽器便會開啟到首頁。</span><span class="sxs-lookup"><span data-stu-id="0b995-209">The default browser opens to the home page.</span></span> <span data-ttu-id="0b995-210">(系統即會執行 Web 專案，這是因為您已將它設定為啟始專案。)</span><span class="sxs-lookup"><span data-stu-id="0b995-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads home page](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="0b995-212">若要啟動應用程式的 WebJob 後端，以滑鼠右鍵按一下 [方案總管] 中的 ContosoAdsWebJob 專案，然後依序按一下 [偵錯]  >  [開始新執行個體]。</span><span class="sxs-lookup"><span data-stu-id="0b995-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="0b995-213">主控台應用程式視窗隨即開啟，並顯示指出 WebJobs SDK JobHost 物件已開始執行的記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="0b995-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Console application window showing that the backend is running](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="0b995-215">在您的瀏覽器中按一下 [建立廣告]。</span><span class="sxs-lookup"><span data-stu-id="0b995-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="0b995-216">輸入部分測試資料，並選取要上傳的影像，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="0b995-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Create page](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="0b995-218">應用程式會進入索引頁面，但不會顯示新廣告的縮圖，因為處理尚未發生。</span><span class="sxs-lookup"><span data-stu-id="0b995-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="0b995-219">同時，不久之後，主控台應用程式視窗中的記錄訊息會顯示已收到佇列訊息並已開始處理。</span><span class="sxs-lookup"><span data-stu-id="0b995-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Console application window showing that a queue message has been processed](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="0b995-221">在看到主控台應用程式視窗中的記錄訊息後，您可以重新整理索引頁面以查看縮圖。</span><span class="sxs-lookup"><span data-stu-id="0b995-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![索引頁面](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="0b995-223">按一下廣告的 [詳細資料]  以查看完整大小的影像。</span><span class="sxs-lookup"><span data-stu-id="0b995-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Details page](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="0b995-225">您一直在本機電腦上執行應用程式，並使用位於電腦上的 SQL Server 資料庫，但它會使用雲端中的佇列和 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="0b995-226">在下一節中，您將會使用雲端資料庫以及雲端 Blob 和佇列，在雲端中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="0b995-227"><a id="runincloud"></a>在雲端中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="0b995-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="0b995-228">您將執行下列步驟，在雲端中執行應用程式：</span><span class="sxs-lookup"><span data-stu-id="0b995-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="0b995-229">部署至 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="0b995-229">Deploy to Web Apps.</span></span> <span data-ttu-id="0b995-230">Visual Studio 會在 App Service 和 SQL 資料庫執行個體中自動建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="0b995-231">設定 Web 應用程式來使用您的 Azure SQL Database 和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="0b995-232">在建立一些廣告並在雲端中執行後，您將檢視 WebJobs SDK 儀表板，以查看儀表板所提供的豐富監視功能。</span><span class="sxs-lookup"><span data-stu-id="0b995-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="0b995-233">部署至 Web Apps</span><span class="sxs-lookup"><span data-stu-id="0b995-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="0b995-234">關閉瀏覽器和主控台應用程式視窗。</span><span class="sxs-lookup"><span data-stu-id="0b995-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="0b995-235">完成[發佈至含有 SQL Database 的 Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="0b995-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="0b995-236">在您完成部署步驟之後，請繼續進行本文中的其餘工作。</span><span class="sxs-lookup"><span data-stu-id="0b995-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="0b995-237">設定 Web 應用程式來使用您的 Azure SQL Database 和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0b995-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="0b995-238">[避免將敏感資訊 (例如連接字串) 放在儲存於原始程式碼儲存機制的檔案](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(英文) 會是安全性最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0b995-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="0b995-239">Azure 提供實作上述最佳做法的方式：您可以在 Azure 環境中設定連接字串和其他設定值，當應用程式在 Azure 中執行時，ASP.NET 組態 API 便會自動挑選這些值。</span><span class="sxs-lookup"><span data-stu-id="0b995-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="0b995-240">您可以使用 [伺服器總管] 、Azure 入口網站、Windows PowerShell，或跨平台的命令列介面，在 Azure 中設定這些值。</span><span class="sxs-lookup"><span data-stu-id="0b995-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="0b995-241">如需詳細資訊，請參閱 [應用程式字串與連接字串的運作方式](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。</span><span class="sxs-lookup"><span data-stu-id="0b995-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="0b995-242">在本節中，您會使用 [伺服器總管] 在 Azure 中設定連接字串值。</span><span class="sxs-lookup"><span data-stu-id="0b995-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="0b995-243">在 [伺服器總管] 中，於 [Azure] > [App Service] > {您的資源群組} 下的 Web 應用程式上按一下滑鼠右鍵，然後按一下 [檢視設定]。</span><span class="sxs-lookup"><span data-stu-id="0b995-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="0b995-244">隨即會在 [設定] 索引標籤中開啟 [Azure Web 應用程式] 視窗。</span><span class="sxs-lookup"><span data-stu-id="0b995-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="0b995-245">將 DefaultConnection 連接字串的名稱變更為您在[發佈至含有 SQL Database 的 Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 文章中設定 SQL Database 時所選擇的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="0b995-246">Azure 便會在您建立 Web 應用程式和相關資料庫時自動建立此連接字串，因此它已包含正確的連接字串值。</span><span class="sxs-lookup"><span data-stu-id="0b995-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="0b995-247">您只是單純將名稱變更為程式碼要尋找的名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="0b995-248">新增兩個新的連接字串，將他們命名為 AzureWebJobsStorage 和 AzureWebJobsDashboard。</span><span class="sxs-lookup"><span data-stu-id="0b995-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="0b995-249">將資料庫類型設定為 [自訂]，並將連接字串值設定為您稍早在 *Web.config* 和 *App.config* 檔案中所用的相同值</span><span class="sxs-lookup"><span data-stu-id="0b995-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="0b995-250">(請確定您包含整個連接字串，而不只是存取金鑰而已，並且不要包含引號)。</span><span class="sxs-lookup"><span data-stu-id="0b995-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="0b995-251">WebJobs SDK 會使用這些連接字串，一個供應用程式資料使用，一個供記錄使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="0b995-252">如稍早所看到的，供應用程式資料使用的連接字串也會提供給 Web 前端程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="0b995-253">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-253">Click **Save**.</span></span>

    ![Azure 入口網站中的連接字串](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="0b995-255">在 [伺服器總管] 中，於 Web 應用程式上按一下滑鼠右鍵，然後按一下 [停止]。</span><span class="sxs-lookup"><span data-stu-id="0b995-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="0b995-256">當 Web 應用程式停止之後，再次以滑鼠右鍵按一下該 Web 應用程式，然後按一下 [啟動] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="0b995-257">發行時，WebJob 便會自動啟動，但在您進行組態變更時便會停止。</span><span class="sxs-lookup"><span data-stu-id="0b995-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="0b995-258">若要重新啟動它，您可以重新啟動 Web 應用程式，或在 [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)中重新啟動 WebJob。</span><span class="sxs-lookup"><span data-stu-id="0b995-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="0b995-259">通常建議您在進行設定變更之後重新啟動 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="0b995-260">重新整理網址列中具有 Web 應用程式 URL 的瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="0b995-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="0b995-261">首頁便會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0b995-261">The home page appears.</span></span>
8. <span data-ttu-id="0b995-262">建立廣告，就像您在[本機執行應用程式](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)時所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="0b995-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="0b995-263">一開始，顯示的索引頁面沒有縮圖。</span><span class="sxs-lookup"><span data-stu-id="0b995-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="0b995-264">在幾秒後重新整理頁面，縮圖便會隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0b995-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="0b995-265">如果未出現縮圖，您可能必須等候一分鐘左右，讓 WebJob 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0b995-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="0b995-266">在一段時間後，如果您重新整理頁面時仍未看到縮圖，則 WebJob 可能未自動啟動。</span><span class="sxs-lookup"><span data-stu-id="0b995-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="0b995-267">在該情況下，請移至 [Azure 入口網站](https://portal.azure.com/)中的 [應用程式服務] 刀鋒視窗，並找到您的 Web 應用程式，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="0b995-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="0b995-268">檢視 WebJobs SDK 儀表板</span><span class="sxs-lookup"><span data-stu-id="0b995-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="0b995-269">在 [Azure 入口網站](https://portal.azure.com/)中，選取 [應用程式服務] 刀鋒視窗，並找到您的 Web 應用程式，然後選取 [WebJob]。</span><span class="sxs-lookup"><span data-stu-id="0b995-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="0b995-270">選取 [記錄] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0b995-270">Select the **Logs** tab.</span></span>

    ![記錄索引標籤](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="0b995-272">新的瀏覽器索引標籤即會開啟到 WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="0b995-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="0b995-273">儀表板會顯示 WebJob 正在執行中，並顯示在 WebJobs SDK 所觸發之程式碼中的函數清單。</span><span class="sxs-lookup"><span data-stu-id="0b995-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="0b995-274">按一下其中一個函式，以查看其執行的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0b995-274">Click one of the functions to see details about its execution.</span></span>

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="0b995-277">此頁面上的 [轉送函數]  按鈕會造成 WebJobs SDK 架構再次呼叫此函數，這可提供您一個機會來變更首先傳送至函數的資料。</span><span class="sxs-lookup"><span data-stu-id="0b995-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="0b995-278">當您完成測試時，請考慮刪除 Web 應用程式、儲存體帳戶和您的 SQL Database 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0b995-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="0b995-279">Web 應用程式是免費提供的，但 SQL 儲存體帳戶和資料庫執行個體則會累算費用 (儘管是小規模，還是會收取基本費用)。</span><span class="sxs-lookup"><span data-stu-id="0b995-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="0b995-280">另外，如果您持續執行 Web 應用程式，那麼，找到您 URL 的任何人都可以建立和檢視廣告。</span><span class="sxs-lookup"><span data-stu-id="0b995-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="0b995-281">刪除 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0b995-281">Delete your web app</span></span>
<span data-ttu-id="0b995-282">在入口網站中，移至 [應用程式服務] 刀鋒視窗，並找到和選取您的 Web 應用程式，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="0b995-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="0b995-283">如果您只想暫時避免他人存取 Web 應用程式，請改為按一下 [停止]  。</span><span class="sxs-lookup"><span data-stu-id="0b995-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="0b995-284">在此情況下，將會繼續累算 SQL Database 和儲存體帳戶的費用。</span><span class="sxs-lookup"><span data-stu-id="0b995-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="0b995-285">刪除儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="0b995-285">Delete your storage account</span></span>
<span data-ttu-id="0b995-286">若要刪除儲存體帳戶，請參閱[刪除儲存體帳戶](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="0b995-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="0b995-287">刪除資料庫</span><span class="sxs-lookup"><span data-stu-id="0b995-287">Delete your database</span></span>
<span data-ttu-id="0b995-288">若要刪除您的 SQL Database，請參閱 [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) 文件。</span><span class="sxs-lookup"><span data-stu-id="0b995-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="0b995-289"><a id="create"></a>從頭開始建立應用程式</span><span class="sxs-lookup"><span data-stu-id="0b995-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="0b995-290">您將在本節執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="0b995-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="0b995-291">使用 Web 專案建立 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="0b995-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="0b995-292">在前端與後端之間共用的資料存取層中，新增類別庫專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="0b995-293">在啟用 WebJobs 部署的後端中新增主控台應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="0b995-294">新增 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="0b995-294">Add NuGet packages.</span></span>
* <span data-ttu-id="0b995-295">設定專案參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-295">Set project references.</span></span>
* <span data-ttu-id="0b995-296">從您在前一節的教學課程中使用的所下載應用程式，複製其應用程式程式碼和組態檔。</span><span class="sxs-lookup"><span data-stu-id="0b995-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="0b995-297">針對使用 Azure Blob 和佇列及 WebJobs SDK 該部分的程式碼進行審查。</span><span class="sxs-lookup"><span data-stu-id="0b995-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="0b995-298">使用 Web 專案和類別庫專案建立 Visual Studio 方案</span><span class="sxs-lookup"><span data-stu-id="0b995-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="0b995-299">在 Visual Studio 中，選擇 [檔案] > [新增] > [專案]。</span><span class="sxs-lookup"><span data-stu-id="0b995-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="0b995-300">在 [新增專案] 對話方塊中，依序選擇 [Visual C#] > [Web] > [ASP.NET Web 應用程式 (.NET Framework)]。</span><span class="sxs-lookup"><span data-stu-id="0b995-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="0b995-301">將專案命名為 ContosoAdsWeb，將方案命名為 ContosoAdsWebJobsSDK (如果您要將方案放入與所下載方案相同的資料夾中，則請變更方案名稱)，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![New Project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="0b995-303">在 [新增 ASP.NET Web 應用程式] 對話方塊中，選擇 MVC 範本，然後選取 [變更驗證]。</span><span class="sxs-lookup"><span data-stu-id="0b995-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![變更驗證](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="0b995-305">在 [變更驗證] 對話方塊中，選擇 [不需要驗證]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0b995-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![不需要驗證](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="0b995-307">在 [新增 ASP.NET Web 應用程式] 對話方塊中，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0b995-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="0b995-308">Visual Studio 便會建立方案和 Web 專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="0b995-309">在 [方案總管] 中，以滑鼠右鍵按一下方案 (不是專案)，並依序選擇 [新增]  >  [新專案]。</span><span class="sxs-lookup"><span data-stu-id="0b995-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="0b995-310">在 [新增專案] 對話方塊中，選擇 [Visual C#] > [Windows 傳統桌面] > [類別庫 (.NET Framework)] 範本。</span><span class="sxs-lookup"><span data-stu-id="0b995-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="0b995-311">將專案命名為 *ContosoAdsCommon*，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0b995-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="0b995-312">此專案將包含由前端與後端使用的 Entity Framework 內容和資料模型。</span><span class="sxs-lookup"><span data-stu-id="0b995-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="0b995-313">作為替代方式，您可以在 Web 專案中定義 EF 相關的類別，並從 WebJob 專案參考該專案。</span><span class="sxs-lookup"><span data-stu-id="0b995-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="0b995-314">但之後您的 WebJob 專案會有不需要的 Web 組件參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="0b995-315">新增已啟用 WebJobs 部署的主控台應用程式專案</span><span class="sxs-lookup"><span data-stu-id="0b995-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="0b995-316">以滑鼠右鍵按一下 Web 專案 (不是方案或類別庫專案)，然後依序按一下 [新增]  > 的簡單多層次 ASP.NET MVC 5 應用程式撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project menu selection](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="0b995-318">在 [新增 Azure WebJob] 對話方塊中，在 [專案名稱] 和 [WebJob 名稱] 中輸入 ContosoAdsWebJob。</span><span class="sxs-lookup"><span data-stu-id="0b995-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="0b995-319">保留 [WebJob 執行模式] 的 [連續執行] 設定。</span><span class="sxs-lookup"><span data-stu-id="0b995-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="0b995-320">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-320">Click **OK**.</span></span>

   <span data-ttu-id="0b995-321">Visual Studio 便會建立設定為每次部署 Web 專案時，便會部署成為 WebJob 的主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="0b995-322">若要執行此動作，應用程式在建立專案後執行了下列工作：</span><span class="sxs-lookup"><span data-stu-id="0b995-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="0b995-323">在 WebJob 專案的 Properties 資料夾中新增了 *webjob-publish-settings.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="0b995-324">在 Web 專案的 Properties 資料夾中新增了 *webjobs-list.json* 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="0b995-325">在 WebJob 專案中安裝了 Microsoft.Web.WebJobs.Publish NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="0b995-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="0b995-326">如需這些變更的詳細資訊，請參閱 [如何使用 Visual Studio 部署 WebJobs](websites-dotnet-deploy-webjobs.md)。</span><span class="sxs-lookup"><span data-stu-id="0b995-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="0b995-327">新增 NuGet 封裝</span><span class="sxs-lookup"><span data-stu-id="0b995-327">Add NuGet packages</span></span>
<span data-ttu-id="0b995-328">WebJob 專案的新專案範本會自動安裝 WebJobs SDK NuGet 封裝 [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) 及其相依項目。</span><span class="sxs-lookup"><span data-stu-id="0b995-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="0b995-329">在 WebJob 專案自動安裝的 WebJobs SDK 相依性中，其中一個相依性是 Azure 儲存體用戶端程式庫 (SCL)。</span><span class="sxs-lookup"><span data-stu-id="0b995-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="0b995-330">不過，您需要將它新增至 Web 專案才能使用 Blob 和佇列。</span><span class="sxs-lookup"><span data-stu-id="0b995-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="0b995-331">開啟方案的 [管理 NuGet 封裝]  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0b995-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="0b995-332">在左側窗格中，選取 [Installed packages] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="0b995-333">尋找 Azure 儲存體套件，然後按一下 [管理]。</span><span class="sxs-lookup"><span data-stu-id="0b995-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="0b995-334">在 [選取專案] 方塊中，勾選 **ContosoAdsWeb** 核取方塊，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0b995-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="0b995-335">這三個專案都會透過 Entity Framework 來使用 SQL Database 中的資料。</span><span class="sxs-lookup"><span data-stu-id="0b995-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="0b995-336">在左側窗格中，選取 [線上] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="0b995-337">尋找 *EntityFramework* NuGet 封裝，並將它安裝在這三個專案中。</span><span class="sxs-lookup"><span data-stu-id="0b995-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="0b995-338">設定專案參考</span><span class="sxs-lookup"><span data-stu-id="0b995-338">Set project references</span></span>
<span data-ttu-id="0b995-339">Web 和 WebJob 專案都將使用 SQL Database，因此兩者都會需要 ContosoAdsCommon 專案的參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="0b995-340">在 ContosoAdsWeb 專案中，設定 ContosoAdsCommon 專案的參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="0b995-341">(以滑鼠右鍵按一下 ContosoAdsWeb 專案，然後依序按一下 [新增]  > **K**的簡單多層次 ASP.NET MVC 5 應用程式撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="0b995-342">在 [參考管理員] 對話方塊中，選取 [專案] > [方案] > [ContosoAdsCommon]，然後按一下 [確定]。)</span><span class="sxs-lookup"><span data-stu-id="0b995-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="0b995-343">WebJob 專案需要參考，才能使用映像及存取連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="0b995-344">在 ContosoAdsWebJob 專案中，設定 `System.Drawing` 和 `System.Configuration` 的參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="0b995-345">新增程式碼和組態檔</span><span class="sxs-lookup"><span data-stu-id="0b995-345">Add code and configuration files</span></span>
<span data-ttu-id="0b995-346">本教學檔案未說明如何[使用 Scaffolding 建立 MVC 控制器和檢視](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)、如何[編寫能與 SQL Server 資料庫搭配使用的 Entity Framework 程式碼](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)或 [ASP.NET 4.5 中非同步程式設計的基本概念](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)。</span><span class="sxs-lookup"><span data-stu-id="0b995-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="0b995-347">因此剩下要進行的作業就是，從所下載的方案將程式碼和設定檔複製到新方案。</span><span class="sxs-lookup"><span data-stu-id="0b995-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="0b995-348">在執行該作業後，下一節將示範和說明程式碼的重要部分。</span><span class="sxs-lookup"><span data-stu-id="0b995-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="0b995-349">若要加入檔案到專案或資料夾，請以滑鼠右鍵按一下專案或資料夾，然後按一下 [加入]  > 的簡單多層次 ASP.NET MVC 5 應用程式撰寫程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="0b995-350">選取您需要的檔案，然後按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="0b995-351">如果詢問您是否要取代現有的檔案，請按一下 [是] 。</span><span class="sxs-lookup"><span data-stu-id="0b995-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="0b995-352">在 ContosoAdsCommon 專案中，刪除 *Class1.cs* 檔案，並在其位置加入所下載專案的下列檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="0b995-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="0b995-353">*Ad.cs*</span></span>
   * <span data-ttu-id="0b995-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="0b995-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="0b995-355">BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="0b995-356">在 ContosoAdsWeb 專案中，從所下載的專案加入下列檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="0b995-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="0b995-357">*Web.config*</span></span>
   * <span data-ttu-id="0b995-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="0b995-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="0b995-359">在 Controllers 資料夾中，新增檔案︰AdController.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="0b995-360">在 Views\Shared 資料夾中：_Layout.cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="0b995-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="0b995-361">在 Views\Home 資料夾中：Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b995-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="0b995-362">在 Views\Ad 資料夾中 (請先建立此資料夾)：五個 .cshtml 檔案</span><span class="sxs-lookup"><span data-stu-id="0b995-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="0b995-363">在 ContosoAdsWebJob 專案中，從所下載的專案加入下列檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="0b995-364">App.config (將檔案類型篩選變更為 [全部檔案])</span><span class="sxs-lookup"><span data-stu-id="0b995-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="0b995-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="0b995-365">*Program.cs*</span></span>
   * <span data-ttu-id="0b995-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="0b995-366">*Functions.cs*</span></span>

<span data-ttu-id="0b995-367">您現在可以如本教學課程中稍早所指示般建置、執行及部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="0b995-368">不過，在您開始執行此動作之前，請先將仍在您部署的第一個 Web 應用程式中執行的 WebJob 停止。</span><span class="sxs-lookup"><span data-stu-id="0b995-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="0b995-369">否則，WebJob 將會處理在本機建立或由在新 Web 應用程式中執行之應用程式所建立的佇列訊息，因為它們全都使用相同的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0b995-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="0b995-370"><a id="code"></a>檢閱應用程式程式碼</span><span class="sxs-lookup"><span data-stu-id="0b995-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="0b995-371">以下小節將說明 WebJobs SDK、Azure 儲存體 Blob 和佇列相關的程式碼。</span><span class="sxs-lookup"><span data-stu-id="0b995-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="0b995-372">如需 WebJobs SDK 特定的程式碼，請移至 [Program.cs 和 Functions.cs](#programcs) 區段。</span><span class="sxs-lookup"><span data-stu-id="0b995-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="0b995-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="0b995-374">Ad.cs 檔案可定義廣告類別列舉，以及廣告資訊的 POCO 實體類別。</span><span class="sxs-lookup"><span data-stu-id="0b995-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="0b995-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="0b995-376">ContosoAdsContext 類別可指定廣告類別用於 DbSet 集合，Entity Framework 會儲存在 SQL 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="0b995-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="0b995-377">類別含兩個建構函式。</span><span class="sxs-lookup"><span data-stu-id="0b995-377">The class has two constructors.</span></span> <span data-ttu-id="0b995-378">第一個是由 Web 專案所使用，指定儲存在 Web.config 檔案或 Azure 執行階段環境中的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="0b995-379">第二個建構函式可讓您傳入實際的連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="0b995-380">WebJob 專案會需要該資訊，因為它沒有 Web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b995-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="0b995-381">您稍早已看見儲存此連接字串的位置，之後您會看到程式碼如何在具現化 DbContext 類別時擷取連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="0b995-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="0b995-383">`BlobInformation` 類別可用來在佇列訊息中儲存影像 Blob 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0b995-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="0b995-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="0b995-385">自 `Application_Start` 方法呼叫的程式碼會建立 images Blob 容器和 images 佇列 (如果尚不存在)。</span><span class="sxs-lookup"><span data-stu-id="0b995-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="0b995-386">這可確保每當使用新的儲存體帳戶啟動時，系統便會自動建立必要的 Blob 容器和佇列。</span><span class="sxs-lookup"><span data-stu-id="0b995-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="0b995-387">此程式碼會使用 *Web.config* 檔案或 Azure 執行階段環境中的儲存體連接字串，來取得儲存體帳戶的存取權限。</span><span class="sxs-lookup"><span data-stu-id="0b995-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="0b995-388">之後會取得 images Blob 容器的參考、建立容器 (如果尚不存在)，並設定新容器的存取權限。</span><span class="sxs-lookup"><span data-stu-id="0b995-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="0b995-389">依預設，新的容器只允許具有儲存體帳戶認證的用戶端存取 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="0b995-390">Web 應用程式需要 Blob 處於公用狀態，才能使用指向影像 Blob 的 URL 來顯示影像。</span><span class="sxs-lookup"><span data-stu-id="0b995-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="0b995-391">類似的程式碼可取得 *thumbnailrequest* 佇列的參考，並建立新佇列。</span><span class="sxs-lookup"><span data-stu-id="0b995-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="0b995-392">在此情況下，即不需要變更權限。</span><span class="sxs-lookup"><span data-stu-id="0b995-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="0b995-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b995-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="0b995-394">*_Layout.cshtml* 檔案可設定頁首與頁尾中的應用程式名稱，並建立 "Ads" 功能表項目。</span><span class="sxs-lookup"><span data-stu-id="0b995-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="0b995-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b995-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="0b995-396">Views\Home\Index.cshtml 檔案在首頁上顯示類別連結。</span><span class="sxs-lookup"><span data-stu-id="0b995-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="0b995-397">連結會將查詢字串變數中 `Category` 列舉的整數值傳遞至 [廣告索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="0b995-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="0b995-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="0b995-399">在 AdController.cs 檔案中，建構子會呼叫 `InitializeStorage` 方法來建立 Azure 儲存體用戶端程式庫物件，該物件可提供用於處理 Blob 和佇列的 API。</span><span class="sxs-lookup"><span data-stu-id="0b995-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="0b995-400">之後，程式碼可取得 images Blob 容器的參考，如您稍早在 Global.asax.cs 中所見。</span><span class="sxs-lookup"><span data-stu-id="0b995-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="0b995-401">在執行該動作時，它會設定適用 Web 應用程式的預設 [重試原則](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) 。</span><span class="sxs-lookup"><span data-stu-id="0b995-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="0b995-402">預設指數輪詢重試原則，可能會因為對暫時性的錯誤進行反覆重試，使得 Web 應用程式停止回應超過一分鐘。</span><span class="sxs-lookup"><span data-stu-id="0b995-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="0b995-403">此處指定的重試原則會在每次嘗試後等候 3 秒，最多嘗試 3 次。</span><span class="sxs-lookup"><span data-stu-id="0b995-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="0b995-404">類似的程式碼可取得 *images* 佇列的參考。</span><span class="sxs-lookup"><span data-stu-id="0b995-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="0b995-405">多數的控制器程式碼通常用於使用 DbContext 類別來處理 Entity Framework 資料模型。</span><span class="sxs-lookup"><span data-stu-id="0b995-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="0b995-406">例外狀況為 HttpPost `Create` 方法，它會上傳檔案，並將檔案儲存在 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0b995-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="0b995-407">模型繫結器可為方法提供 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) 物件。</span><span class="sxs-lookup"><span data-stu-id="0b995-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="0b995-408">如果使用者選取要上傳的檔案，程式碼會上傳檔案、將檔案儲存在 Blob，並以指向 Blob 的 URL 更新廣告資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="0b995-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="0b995-409">執行上傳的程式碼位於 `UploadAndSaveBlobAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="0b995-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="0b995-410">它會為 Blob 建立 GUID 名稱、上傳並儲存檔案，然後傳回參考至儲存的 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="0b995-411">在 HttpPost `Create` 方法建立 Blob 並更新資料庫之後，它會建立佇列訊息，以通知後端程序，有一個影像已備妥可供轉換成縮圖。</span><span class="sxs-lookup"><span data-stu-id="0b995-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="0b995-412">HttpPost `Edit` 方法的程式碼也是類似的，不同的是如果使用者選取一個新影像檔案，則必須刪除此廣告的任何現有 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="0b995-413">以下是當您刪除廣告時會刪除 Blob 的程式碼：</span><span class="sxs-lookup"><span data-stu-id="0b995-413">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="0b995-414">ContosoAdsWeb - Views\Ad\Index.cshtml 和 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b995-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="0b995-415">*Index.cshtml* 檔案會顯示縮圖與其他廣告資料：</span><span class="sxs-lookup"><span data-stu-id="0b995-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="0b995-416">*Details.cshtml* 檔案會顯示完整大小的影像：</span><span class="sxs-lookup"><span data-stu-id="0b995-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="0b995-417">ContosoAdsWeb - Views\Ad\Create.cshtml 和 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="0b995-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="0b995-418">Create.cshtml 和 Edit.cshtml 檔案可指定表單編碼，供控制器取得 `HttpPostedFileBase` 物件。</span><span class="sxs-lookup"><span data-stu-id="0b995-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="0b995-419">`<input>` 元素告知瀏覽器提供檔案選取對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0b995-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="0b995-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="0b995-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="0b995-421">當 WebJob 啟動時，`Main` 方法會呼叫 WebJobs SDK `JobHost.RunAndBlock` 方法，開始執行目前執行緒上所觸發的函數。</span><span class="sxs-lookup"><span data-stu-id="0b995-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="0b995-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 方法</span><span class="sxs-lookup"><span data-stu-id="0b995-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="0b995-423">WebJobs SDK 會在收到佇列訊息時呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="0b995-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="0b995-424">此方法會建立縮圖，並將縮圖 URL 放入資料庫。</span><span class="sxs-lookup"><span data-stu-id="0b995-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

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
            // be instantiated and disposed within the function.
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

* <span data-ttu-id="0b995-425">當 thumbnailrequest 佇列收到新訊息時，`QueueTrigger` 屬性便會指示 WebJobs SDK 呼叫此方法。</span><span class="sxs-lookup"><span data-stu-id="0b995-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="0b995-426">佇列訊息中的 `BlobInformation` 物件會自動還原序列化成 `blobInfo` 參數。</span><span class="sxs-lookup"><span data-stu-id="0b995-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="0b995-427">方法完成時，佇列訊息便會被刪除。</span><span class="sxs-lookup"><span data-stu-id="0b995-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="0b995-428">如果方法在完成前失敗，則佇列訊息不會被刪除；在 10 分鐘的租用到期後，訊息便會被釋放並等待被再次挑選與處理。</span><span class="sxs-lookup"><span data-stu-id="0b995-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="0b995-429">如果某個訊息總是導致例外狀況，則不會無限制地重複此順序。</span><span class="sxs-lookup"><span data-stu-id="0b995-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="0b995-430">在嘗試處理訊息失敗 5 次之後，訊息便會被移至名為 {queuename}-poison 的佇列。</span><span class="sxs-lookup"><span data-stu-id="0b995-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="0b995-431">您可以設定嘗試的數目上限。</span><span class="sxs-lookup"><span data-stu-id="0b995-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="0b995-432">這兩個 `Blob` 屬性提供繫結到 Blob 的物件：一個繫結到現有影像的 Blob，一個繫結到方法建立的新縮圖 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="0b995-433">Blob 名稱取自佇列訊息 (`BlobName` 和 `BlobNameWithoutExtension`) 中所收到 `BlobInformation` 物件的屬性。</span><span class="sxs-lookup"><span data-stu-id="0b995-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="0b995-434">若要取得儲存體用戶端程式庫的完整功能，您可以利用 `CloudBlockBlob` 類別來使用 Blob。</span><span class="sxs-lookup"><span data-stu-id="0b995-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="0b995-435">如果您想要重複使用為使用 `Stream` 物件所撰寫的程式碼，您可以使用 `Stream` 類別。</span><span class="sxs-lookup"><span data-stu-id="0b995-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="0b995-436">如需如何撰寫使用 WebJobs SDK 屬性的函式詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="0b995-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="0b995-437">如何透過 WebJobs SDK 使用 Azure 佇列儲存體 (英文)</span><span class="sxs-lookup"><span data-stu-id="0b995-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="0b995-438">如何透過 WebJobs SDK 使用 Azure Blob 儲存體 (英文)</span><span class="sxs-lookup"><span data-stu-id="0b995-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="0b995-439">如何透過 WebJobs SDK 使用 Azure 資料表儲存體 (英文)</span><span class="sxs-lookup"><span data-stu-id="0b995-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="0b995-440">如何搭配使用 Azure 服務匯流排與 WebJobs SDK (英文)</span><span class="sxs-lookup"><span data-stu-id="0b995-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="0b995-441">如果您的 Web 應用程式在多個 VM 上執行，則系統將同時執行多個 WebJobs，且在某些情況下，這會導致相同的資料多次進行處理。</span><span class="sxs-lookup"><span data-stu-id="0b995-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="0b995-442">如果您使用內建佇列、blob 和服務匯流排觸發程序，這不會造成問題。</span><span class="sxs-lookup"><span data-stu-id="0b995-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="0b995-443">SDK 可確保您的函式針對每個訊息或 blob 僅會處理一次。</span><span class="sxs-lookup"><span data-stu-id="0b995-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="0b995-444">如需如何實作順利關機的詳細資訊，請參閱 [順利關機](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)。</span><span class="sxs-lookup"><span data-stu-id="0b995-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="0b995-445">為求簡化，`ConvertImageToThumbnailJPG` 方法 (未顯示) 中的程式碼會使用 `System.Drawing` 命名空間中的類別。</span><span class="sxs-lookup"><span data-stu-id="0b995-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="0b995-446">不過，此命名空間中類別的設計原意是要與 Windows Form 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0b995-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="0b995-447">不支援將它們用於 Windows 或 ASP.NET 服務。</span><span class="sxs-lookup"><span data-stu-id="0b995-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="0b995-448">如需映像處理選項的詳細資訊，請參閱[動態映像產生](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx)和[深入調整映像大小](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)。</span><span class="sxs-lookup"><span data-stu-id="0b995-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0b995-449">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b995-449">Next steps</span></span>
<span data-ttu-id="0b995-450">在本教學課程中，您看到使用 WebJobs SDK 進行後端處理的簡單多層次應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="0b995-451">如要進一步了解 ASP.NET 多層式應用程式和 WebJobs，請參考本節所提供的一些建議。</span><span class="sxs-lookup"><span data-stu-id="0b995-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="0b995-452">遺漏的功能</span><span class="sxs-lookup"><span data-stu-id="0b995-452">Missing features</span></span>
<span data-ttu-id="0b995-453">此應用程式設計得很簡單，以做為入門的教學課程。</span><span class="sxs-lookup"><span data-stu-id="0b995-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="0b995-454">在真實世界中，您將實作[相依性插入](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)和[存放庫和工作單位模式](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)的應用程式會使用[介面來記錄](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)、使用 [EF Code First 移轉](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)來管理資料模型變更，以及使用 [EF 連線復原](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)來管理暫時性網路錯誤。</span><span class="sxs-lookup"><span data-stu-id="0b995-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="0b995-455">調整 WebJob 的規模</span><span class="sxs-lookup"><span data-stu-id="0b995-455">Scaling WebJobs</span></span>
<span data-ttu-id="0b995-456">WebJob 會在 Web 應用程式的內容中執行，且無法單獨調整。</span><span class="sxs-lookup"><span data-stu-id="0b995-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="0b995-457">例如，如果您擁有一個標準的 Web 應用程式執行個體，則您的背景程序只有一個執行中的執行個體，而且它會使用亦可用來提供 Web 內容的部分伺服器資源 (CPU、記憶體等)。</span><span class="sxs-lookup"><span data-stu-id="0b995-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="0b995-458">如果流量會因為一天中的某個時段或一週中的某天而有所不同，而且如果必須執行的後端處理可以暫緩的話，您可以排程 WebJobs 在低流量時段中執行。</span><span class="sxs-lookup"><span data-stu-id="0b995-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="0b995-459">如果該解決方案的負載仍然太高，您可以在針對該用途專用的 Web 應用程式中以 WebJob 形式執行後端。</span><span class="sxs-lookup"><span data-stu-id="0b995-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="0b995-460">接著您可以擴充後端 Web 應用程式，而不會影響到前端 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b995-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="0b995-461">如需詳細資訊，請參閱 [調整 WebJob](websites-webjobs-resources.md#scale)。</span><span class="sxs-lookup"><span data-stu-id="0b995-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="0b995-462">避免關機時 Web 應用程式逾時</span><span class="sxs-lookup"><span data-stu-id="0b995-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="0b995-463">若要確保您的 WebJobs 持續不斷地在 Web 應用程式的所有執行個體上執行，您必須啟用 [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) 功能。</span><span class="sxs-lookup"><span data-stu-id="0b995-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="0b995-464">在 WebJobs 外部使用 WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="0b995-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="0b995-465">使用 WebJobs SDK 的程式無需在 Azure 的 WebJob 中執行。</span><span class="sxs-lookup"><span data-stu-id="0b995-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="0b995-466">它可以在本機執行，也可以在如雲端服務背景工作角色或 Windows 服務等其他環境中執行。</span><span class="sxs-lookup"><span data-stu-id="0b995-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="0b995-467">不過，您僅能透過 Azure Web 應用程式來存取 WebJobs SDK 儀表板。</span><span class="sxs-lookup"><span data-stu-id="0b995-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="0b995-468">若要使用儀表板，您必須將 Web 應用程式連線到您所使用的儲存體帳戶，方法是在傳統入口網站的 [設定]  索引標籤上設定 AzureWebJobsDashboard 連接字串。</span><span class="sxs-lookup"><span data-stu-id="0b995-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="0b995-469">然後，您可以使用下列 URL 來進入儀表板：</span><span class="sxs-lookup"><span data-stu-id="0b995-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="0b995-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="0b995-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="0b995-471">如需詳細資訊，請參閱 [使用 WebJobs SDK 來取得本機開發的儀表板](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)(英文)，但請注意，它會顯示舊的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="0b995-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="0b995-472">其他 WebJobs 文件</span><span class="sxs-lookup"><span data-stu-id="0b995-472">More WebJobs documentation</span></span>
<span data-ttu-id="0b995-473">如需詳細資訊，請參閱 [Azure WebJobs 文件資源](http://go.microsoft.com/fwlink/?LinkId=390226)。</span><span class="sxs-lookup"><span data-stu-id="0b995-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
