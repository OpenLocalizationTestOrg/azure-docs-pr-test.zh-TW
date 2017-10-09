---
title: "使用 Visual Studio 中的 已連接服務的 Azure 儲存體 aaaAdd |Microsoft 文件"
description: "新增 Azure 儲存體 tooyour 應用程式使用 hello Visual Studio 加入已連接服務對話方塊"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="a4f04-103">使用 Visual Studio 的已連接服務加入 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a4f04-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="a4f04-104">Visual Studio 中，您可以使用連接任何 hello 遵循 tooAzure 儲存體使用 hello**加入已連接服務**對話方塊：</span><span class="sxs-lookup"><span data-stu-id="a4f04-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="a4f04-105">C# 雲端服務</span><span class="sxs-lookup"><span data-stu-id="a4f04-105">C# cloud service</span></span>
- <span data-ttu-id="a4f04-106">.NET 後端行動服務</span><span class="sxs-lookup"><span data-stu-id="a4f04-106">.NET backend mobile service</span></span>
- <span data-ttu-id="a4f04-107">ASP.NET 網站或服務</span><span class="sxs-lookup"><span data-stu-id="a4f04-107">ASP.NET website or service</span></span>
- <span data-ttu-id="a4f04-108">ASP.NET Core 服務</span><span class="sxs-lookup"><span data-stu-id="a4f04-108">ASP.NET Core service</span></span>
- <span data-ttu-id="a4f04-109">Azure WebJob 服務</span><span class="sxs-lookup"><span data-stu-id="a4f04-109">Azure WebJob service</span></span> 

<span data-ttu-id="a4f04-110">hello 已連接的服務功能加入所有需要的 hello 參考和連線程式碼 tooyour 專案，並會適當地修改您的設定檔。</span><span class="sxs-lookup"><span data-stu-id="a4f04-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="a4f04-111">完成之後，hello**加入已連接服務**對話方塊會自動顯示文件詳述 hello 步驟需要的 toostart 使用 blob 儲存體、 佇列和資料表。</span><span class="sxs-lookup"><span data-stu-id="a4f04-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="a4f04-112">連接 tooAzure 儲存體使用 hello 已連接服務對話方塊</span><span class="sxs-lookup"><span data-stu-id="a4f04-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="a4f04-113">在 Visual Studio 中開啟您的專案</span><span class="sxs-lookup"><span data-stu-id="a4f04-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="a4f04-114">在**方案總管 中**，以滑鼠右鍵按一下 hello**已連接服務** 節點，然後從 hello 內容功能表，然後選取**加入已連接服務**。</span><span class="sxs-lookup"><span data-stu-id="a4f04-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![新增 Azure 已連接服務](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="a4f04-116">在 hello**已連接服務**頁面上，選取**雲端儲存體與 Azure 儲存體**。</span><span class="sxs-lookup"><span data-stu-id="a4f04-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![新增 Azure 儲存體](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="a4f04-118">在 hello **Azure 儲存體**對話方塊中，選取現有的儲存體帳戶，並選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a4f04-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="a4f04-119">如果您需要 toocreate 儲存體帳戶，請移 toohello 下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="a4f04-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="a4f04-120">否則，請略過 toostep 6。</span><span class="sxs-lookup"><span data-stu-id="a4f04-120">Otherwise, skip toostep 6.</span></span>
    
    ![加入現有的儲存體帳戶 tooproject](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="a4f04-122">toocreate 儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="a4f04-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="a4f04-123">選取**建立新的儲存體帳戶**在 hello hello 對話方塊底部。</span><span class="sxs-lookup"><span data-stu-id="a4f04-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="a4f04-124">填寫 hello**建立儲存體帳戶** 對話方塊中，然後選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="a4f04-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![新的 Azure 儲存體帳戶](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="a4f04-126">當 hello **Azure 儲存體** 對話方塊隨即出現，hello 新儲存體帳戶會顯示 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="a4f04-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="a4f04-127">在 [hello] 清單中，選取 hello 新儲存體帳戶，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="a4f04-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="a4f04-128">hello 儲存體已連接的服務之下 hello**服務參考**您的專案節點。</span><span class="sxs-lookup"><span data-stu-id="a4f04-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="a4f04-129">您的專案修改方式</span><span class="sxs-lookup"><span data-stu-id="a4f04-129">How your project is modified</span></span>
<span data-ttu-id="a4f04-130">當您完成 hello 對話方塊時，Visual Studio 會將參考加入和修改某些組態檔。</span><span class="sxs-lookup"><span data-stu-id="a4f04-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="a4f04-131">hello 特定變更 hello 專案類型而定：</span><span class="sxs-lookup"><span data-stu-id="a4f04-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="a4f04-132">ASP.NET 專案 - [發生什麼事 - ASP.NET 專案](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="a4f04-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="a4f04-133">ASP.NET Core 專案 - [發生什麼事 - ASP.NET 5 專案](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="a4f04-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="a4f04-134">雲端服務專案 (Web 角色和背景工作角色) - [發生什麼事 - 雲端服務專案](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="a4f04-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="a4f04-135">WebJob 專案 - [發生什麼事 - WebJob 專案](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="a4f04-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4f04-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4f04-136">Next steps</span></span>
- [<span data-ttu-id="a4f04-137">MSDN 論壇︰Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a4f04-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="a4f04-138">Microsoft Azure 儲存體小組部落格 (英文)</span><span class="sxs-lookup"><span data-stu-id="a4f04-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="a4f04-139">Azure 儲存體文件</span><span class="sxs-lookup"><span data-stu-id="a4f04-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
