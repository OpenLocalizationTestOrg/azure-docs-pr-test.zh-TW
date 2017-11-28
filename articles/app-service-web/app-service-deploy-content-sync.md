---
title: "從雲端資料夾 tooAzure App Service aaaSync 內容"
description: "了解如何 toodeploy 內容透過您的應用程式 tooAzure 應用程式服務從同步處理雲端資料夾。"
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
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="e5de1-103">從雲端資料夾 tooAzure 應用程式服務的同步處理內容</span><span class="sxs-lookup"><span data-stu-id="e5de1-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="e5de1-104">本教學課程示範如何 toodeploy 太[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)所同步處理您的內容從 Dropbox 和 OneDrive 等熱門的雲端儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="e5de1-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="e5de1-105"><a name="overview"></a>內容同步處理部署概觀</span><span class="sxs-lookup"><span data-stu-id="e5de1-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="e5de1-106">hello 視內容的同步處理部署由 hello [Kudu 部署引擎](https://github.com/projectkudu/kudu/wiki)整合與應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="e5de1-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="e5de1-107">在 hello [Azure 入口網站](https://portal.azure.com)，您可以指定您的雲端儲存體中的資料夾，使用您的應用程式程式碼和內容，在該資料夾中，然後以 hello 同步 tooApp 服務按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="e5de1-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="e5de1-108">內容的同步處理會使用組建和部署的 hello Kudu 程序。</span><span class="sxs-lookup"><span data-stu-id="e5de1-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="e5de1-109"><a name="contentsync"></a>Tooenable 內容同步處理的部署方式</span><span class="sxs-lookup"><span data-stu-id="e5de1-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="e5de1-110">從 hello tooenable 內容同步[Azure 入口網站](https://portal.azure.com)，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e5de1-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="e5de1-111">在您的應用程式] 刀鋒視窗 hello Azure 入口網站中，按一下 [**設定** > **部署來源**。</span><span class="sxs-lookup"><span data-stu-id="e5de1-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="e5de1-112">按一下**選擇來源**，然後選取**OneDrive**或**Dropbox**做為部署的 hello 來源。</span><span class="sxs-lookup"><span data-stu-id="e5de1-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![內容同步處理](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="e5de1-114">Hello 應用程式開發介面，因此基礎**商務用 OneDrive**不支援這一次。</span><span class="sxs-lookup"><span data-stu-id="e5de1-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="e5de1-115">完成 hello 授權工作流程 tooenable App Service tooaccess 特定預先定義的指定之的路徑的 OneDrive 或 Dropbox 會儲存所有您應用程式服務的內容。</span><span class="sxs-lookup"><span data-stu-id="e5de1-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="e5de1-116">應用程式服務平台可讓您的授權 hello 之後 hello 選項 toocreate 內容 資料夾之下的 hello 會指定內容的路徑或 toochoose 這個指定之內容的路徑下的現有內容資料夾。</span><span class="sxs-lookup"><span data-stu-id="e5de1-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="e5de1-117">在您用於應用程式服務同步處理的雲端儲存體帳戶下的 hello 指定內容路徑是 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e5de1-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="e5de1-118">**OneDrive**：`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="e5de1-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="e5de1-119">**Dropbox**：`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="e5de1-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="e5de1-120">Hello 之後，您可以視需要從 hello Azure 入口網站啟動初始內容的同步處理 hello 內容同步處理。</span><span class="sxs-lookup"><span data-stu-id="e5de1-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="e5de1-121">部署歷程記錄是可用以 hello**部署**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e5de1-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![部署歷程記錄](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="e5de1-123">[從 Dropbox 部署](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx)下有 Dropbox 部署的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e5de1-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

