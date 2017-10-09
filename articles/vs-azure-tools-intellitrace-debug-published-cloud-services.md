---
title: "aaaDebugging 已發行的 Azure 雲端服務與 Visual Studio 和 IntelliTrace |Microsoft 文件"
description: "了解如何 toodebug 雲端服務與 Visual Studio 和 IntelliTrace"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="63494-103">使用 Visual Studio 和 IntelliTrace 進行已發佈 Azure 雲端服務的偵錯</span><span class="sxs-lookup"><span data-stu-id="63494-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="63494-104">有了 IntelliTrace，您可以於角色執行個體在 Azure 中執行時，記錄其廣泛的偵錯資訊。</span><span class="sxs-lookup"><span data-stu-id="63494-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="63494-105">如果您需要 toofind hello 問題的原因，您可以使用 hello IntelliTrace 記錄檔 toostep，透過您的程式碼，從 Visual Studio 在 Azure 中執行一樣即可。</span><span class="sxs-lookup"><span data-stu-id="63494-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="63494-106">實際上，IntelliTrace 記錄索引鍵的程式碼執行和環境資料時以雲端服務在 Azure 中，執行 Azure 應用程式，並讓您重新執行從 Visual Studio 的 hello 記錄資料。</span><span class="sxs-lookup"><span data-stu-id="63494-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="63494-107">如果您有安裝 Visual Studio Enterprise，而您的 Azure 應用程式以 .NET Framework 4 或更新版本為目標，則可以使用 IntelliTrace。</span><span class="sxs-lookup"><span data-stu-id="63494-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="63494-108">IntelliTrace 會收集 Azure 角色的資訊。</span><span class="sxs-lookup"><span data-stu-id="63494-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="63494-109">hello 這些角色的虛擬機器永遠會執行 64 位元作業系統。</span><span class="sxs-lookup"><span data-stu-id="63494-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="63494-110">或者，您可以使用[遠端偵錯](http://go.microsoft.com/fwlink/p/?LinkId=623041)tooattach 直接 tooa 雲端服務是在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="63494-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63494-111">IntelliTrace 僅適用於偵錯，並且不應該用於生產環境部署。</span><span class="sxs-lookup"><span data-stu-id="63494-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="63494-112">為 IntelliTrace 設定 Azure 應用程式</span><span class="sxs-lookup"><span data-stu-id="63494-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="63494-113">tooenable IntelliTrace Azure 應用程式，您必須建立並發行 hello 應用程式，從 Visual Studio Azure 專案。</span><span class="sxs-lookup"><span data-stu-id="63494-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="63494-114">TooAzure 發行之前，您必須將 IntelliTrace 設定 Azure 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="63494-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="63494-115">如果您發行應用程式但未設定 IntelliTrace，您會需要 toorepublish hello 專案。</span><span class="sxs-lookup"><span data-stu-id="63494-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="63494-116">如需詳細資訊，請參閱[使用 Visual Studio 專案發佈 Azure 雲端服務](http://go.microsoft.com/fwlink/p/?LinkId=623012)。</span><span class="sxs-lookup"><span data-stu-id="63494-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="63494-117">當您準備就緒 toodeploy Azure 應用程式，請確認專案建置目標已設定太**偵錯**。</span><span class="sxs-lookup"><span data-stu-id="63494-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="63494-118">在**方案總管 中**，以滑鼠右鍵按一下專案，然後 hello 內容功能表中選取**發行**。</span><span class="sxs-lookup"><span data-stu-id="63494-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="63494-119">在 hello**發行 Azure 應用程式**對話方塊中，選取 hello Azure 訂用帳戶，並選取**下一步**。</span><span class="sxs-lookup"><span data-stu-id="63494-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="63494-120">在 [hello**設定**頁面上，選取 hello**進階設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="63494-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="63494-121">開啟 hello**啟用 IntelliTrace**選項 toocollect IntelliTrace 記錄檔以取得您的應用程式發佈 hello 定域機組中時。</span><span class="sxs-lookup"><span data-stu-id="63494-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="63494-122">toocustomize hello 基本 IntelliTrace 組態中，選取**設定**下一步太**啟用 IntelliTrace**。</span><span class="sxs-lookup"><span data-stu-id="63494-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![IntelliTrace 設定連結](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="63494-124">在 [hello **IntelliTrace 設定**] 對話方塊中，您可以指定哪些事件 toolog、 是否 toocollect 呼叫資訊、 哪些模組和處理序 toocollect 的記錄，以及多少空間 tooallocate toohello 錄製。</span><span class="sxs-lookup"><span data-stu-id="63494-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="63494-125">如需有關 IntelliTrace 的詳細資訊，請參閱 [使用 IntelliTrace 進行偵錯](http://go.microsoft.com/fwlink/?LinkId=214468)。</span><span class="sxs-lookup"><span data-stu-id="63494-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace 設定](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="63494-127">hello IntelliTrace 記錄檔是 hello 大小上限 （hello 預設大小為 250 MB） 的 hello IntelliTrace 設定中指定的循環記錄檔。</span><span class="sxs-lookup"><span data-stu-id="63494-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="63494-128">IntelliTrace 記錄檔會收集的 tooa hello hello 虛擬機器的檔案系統中的檔案。</span><span class="sxs-lookup"><span data-stu-id="63494-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="63494-129">當您要求 hello 記錄檔時，快照集時間中該時間點取得，而下載 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="63494-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="63494-130">已發行的 tooAzure hello Azure 雲端服務。 之後，您可以判斷是否已啟用 IntelliTrace 從 hello Azure 中的節點**伺服器總管**hello 下列影像所示：</span><span class="sxs-lookup"><span data-stu-id="63494-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![伺服器總管 - 已啟用 IntelliTrace](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="63494-132">下載角色執行個體的 IntelliTrace 記錄檔</span><span class="sxs-lookup"><span data-stu-id="63494-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="63494-133">使用 Visual Studio，您可以依照下列步驟來下載角色執行個體的 IntelliTrace 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="63494-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="63494-134">在**伺服器總管**，依序展開 [hello**雲端服務**] 節點，並找出角色執行個體想 toodownload 為記錄檔。</span><span class="sxs-lookup"><span data-stu-id="63494-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="63494-135">Hello 角色執行個體，以滑鼠右鍵按一下，然後從 hello s 內容功能表中，選取**檢視 IntelliTrace 記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="63494-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![[檢視 IntelliTrace 記錄檔] 功能表選項](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="63494-137">hello IntelliTrace 記錄檔會在本機電腦上的下載的 tooa 檔案的目錄中。</span><span class="sxs-lookup"><span data-stu-id="63494-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="63494-138">您要求 hello IntelliTrace 記錄檔，每次建立新的快照。</span><span class="sxs-lookup"><span data-stu-id="63494-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="63494-139">Visual Studio 下載的 hello 記錄檔，同時顯示 hello 作業進度的 hello hello **Azure 活動記錄檔**視窗。</span><span class="sxs-lookup"><span data-stu-id="63494-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="63494-140">Hello 遵循圖所示，您可以展開 hello 作業 toosee hello 線條項目更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="63494-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="63494-142">Hello IntelliTrace 記錄檔會下載時，您可以在 Visual Studio 中繼續 toowork。</span><span class="sxs-lookup"><span data-stu-id="63494-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="63494-143">當下載完成 hello 記錄之後時，會開啟 Visual Studio 中。</span><span class="sxs-lookup"><span data-stu-id="63494-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="63494-144">hello IntelliTrace 記錄檔可能包含例外狀況會產生該 hello 架構，並處理之後。</span><span class="sxs-lookup"><span data-stu-id="63494-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="63494-145">內部架構程式碼會在正常啟動角色時產生這些例外狀況，因此您可以放心忽略。</span><span class="sxs-lookup"><span data-stu-id="63494-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="63494-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63494-146">Next steps</span></span>
- [<span data-ttu-id="63494-147">進行 Azure 雲端服務偵錯的選項</span><span class="sxs-lookup"><span data-stu-id="63494-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="63494-148">使用 Visual Studio 發佈 Azure 雲端服務</span><span class="sxs-lookup"><span data-stu-id="63494-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)