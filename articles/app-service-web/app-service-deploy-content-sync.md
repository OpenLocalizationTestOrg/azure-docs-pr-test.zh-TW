---
title: "將雲端資料夾的內容同步處理到 Azure App Service"
description: "了解如何從雲端資料夾透過內容同步處理，將您的應用程式部署至 Azure App Service。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 010e7dc492abefaa3afe814c0322af9f6fe5acd2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sync-content-from-a-cloud-folder-to-azure-app-service"></a><span data-ttu-id="53cb3-103">將雲端資料夾的內容同步處理到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="53cb3-103">Sync content from a cloud folder to Azure App Service</span></span>
<span data-ttu-id="53cb3-104">本教學課程將示範如何從受歡迎的雲端儲存體服務 (例如 Dropbox 與 OneDrive) 同步處理內容，以部署至 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 。</span><span class="sxs-lookup"><span data-stu-id="53cb3-104">This tutorial shows you how to deploy to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="53cb3-105"><a name="overview"></a>內容同步處理部署概觀</span><span class="sxs-lookup"><span data-stu-id="53cb3-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="53cb3-106">隨選內容同步處理部署是由與 App Service 整合之 [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki) 所提供。</span><span class="sxs-lookup"><span data-stu-id="53cb3-106">The on-demand content sync deployment is powered by the [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="53cb3-107">在 [Azure 入口網站](https://portal.azure.com)中，您可以在雲端儲存空間中指定特殊資料夾、在該資料夾中處理您的應用程式程式碼和內容，並按一下按鈕以同步至 App Service。</span><span class="sxs-lookup"><span data-stu-id="53cb3-107">In the [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync to App Service with the click of a button.</span></span> <span data-ttu-id="53cb3-108">內容同步處理會在組建和部署使用 Kudu 程序。</span><span class="sxs-lookup"><span data-stu-id="53cb3-108">Content sync utilizes the Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="53cb3-109"><a name="contentsync"></a>如何啟用內容同步處理部署</span><span class="sxs-lookup"><span data-stu-id="53cb3-109"><a name="contentsync"></a>How to enable content sync deployment</span></span>
<span data-ttu-id="53cb3-110">若要從 [Azure 入口網站](https://portal.azure.com)啟用內容同步處理，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="53cb3-110">To enable content sync from the [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="53cb3-111">在 Azure 入口網站上您的應用程式刀鋒視窗中，按一下 [設定] > [部署來源]。</span><span class="sxs-lookup"><span data-stu-id="53cb3-111">In your app's blade in the Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="53cb3-112">按一下 [選擇來源]，然後選取 [OneDrive] 或 [Dropbox] 作為部署來源。</span><span class="sxs-lookup"><span data-stu-id="53cb3-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as the source for deployment.</span></span> 
   
    ![內容同步處理](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="53cb3-114">由於 API 中的基礎差異，目前不支援**商務用 OneDrive**。</span><span class="sxs-lookup"><span data-stu-id="53cb3-114">Because of underlying differences in the APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="53cb3-115">完成授權工作流程，以便讓 App Service 存取將會儲存所有 App Service 內容之 OneDrive 或 Dropbox 的特定預先定義指定路徑。</span><span class="sxs-lookup"><span data-stu-id="53cb3-115">Complete the authorization workflow to enable App Service to access a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="53cb3-116">授權之後，App Service 平台會提供您在指定內容路徑下建立內容資料夾的選項，或是選擇此指定的內容路徑下的現有內容資料夾。</span><span class="sxs-lookup"><span data-stu-id="53cb3-116">After authorization the App Service platform will give you the option to create a content folder under the designated content path, or to choose an existing content folder under this designated content path.</span></span> <span data-ttu-id="53cb3-117">以下為針對 App Service 同步處理所使用之雲端儲存體帳戶下的指定內容路徑：</span><span class="sxs-lookup"><span data-stu-id="53cb3-117">The designated content paths under your cloud storage accounts used for App Service sync are the following:</span></span>  
   
   * <span data-ttu-id="53cb3-118">**OneDrive**：`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="53cb3-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="53cb3-119">**Dropbox**：`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="53cb3-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="53cb3-120">初始內容同步處理之後，內容同步處理可以視需要從 Azure 入口網站啟動。</span><span class="sxs-lookup"><span data-stu-id="53cb3-120">After the initial content sync the content sync can be initiated on demand from the Azure portal.</span></span> <span data-ttu-id="53cb3-121">[部署]  刀鋒視窗提供了部署歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="53cb3-121">Deployment history is available with the **Deployments** blade.</span></span>
   
    ![部署歷程記錄](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="53cb3-123">[從 Dropbox 部署](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx)下有 Dropbox 部署的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="53cb3-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

