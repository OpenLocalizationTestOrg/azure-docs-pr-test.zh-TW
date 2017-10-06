---
title: "aaaLearn toouse hello 邏輯應用程式中的 FTP 連接器的方式 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooFTP 伺服器 toomanage 您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 FTP 伺服器中的檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="c3b9c-105">開始使用 hello FTP 連接器</span><span class="sxs-lookup"><span data-stu-id="c3b9c-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="c3b9c-106">使用 hello FTP 連接器 toomonitor、 管理以及建立 FTP 伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="c3b9c-107">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="c3b9c-108">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="c3b9c-109">連接 tooFTP</span><span class="sxs-lookup"><span data-stu-id="c3b9c-109">Connect tooFTP</span></span>
<span data-ttu-id="c3b9c-110">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="c3b9c-111">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="c3b9c-112">建立連接 tooFTP</span><span class="sxs-lookup"><span data-stu-id="c3b9c-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="c3b9c-113">使用 FTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="c3b9c-113">Use a FTP trigger</span></span>
<span data-ttu-id="c3b9c-114">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="c3b9c-115">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c3b9c-116">hello FTP 連接器，必須從 hello 網際網路存取的 FTP 伺服器是設定 toooperate 被動模式。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="c3b9c-117">此外，hello FTP 連接器是**隱含 FTPS (FTP over SSL) 與不相容**。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="c3b9c-118">hello FTP 連接器僅支援明確 FTPS (FTP over SSL)。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="c3b9c-119">在此範例中，我將示範如何 toouse hello **FTP-時加入或修改檔案**觸發 tooinitiate 邏輯應用程式工作流程時，新增或修改 FTP 伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="c3b9c-120">在企業範例中，您可以使用此觸發程序 toomonitor FTP 資料夾，表示客戶訂單的新檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="c3b9c-121">您無法再使用 FTP 連接器動作例如**取得檔案內容**tooget hello 內容的進一步處理和儲存體 orders 資料庫中的 hello 順序。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="c3b9c-122">輸入*ftp* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **FTP-時加入或修改檔案**觸發程序</span><span class="sxs-lookup"><span data-stu-id="c3b9c-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="c3b9c-123">![FTP 觸發程序影像 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="c3b9c-124">hello**時加入或修改檔案**控制開啟</span><span class="sxs-lookup"><span data-stu-id="c3b9c-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="c3b9c-125">![FTP 觸發程序影像 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="c3b9c-126">選取 hello **...**位於 hello 控制項 hello 右邊。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="c3b9c-127">這會開啟 hello 資料夾選擇器控制項</span><span class="sxs-lookup"><span data-stu-id="c3b9c-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="c3b9c-128">![FTP 觸發程序影像 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="c3b9c-129">選取 hello  **>**  （向右箭號），並瀏覽 toofind hello 資料夾 toomonitor 需新增或修改檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="c3b9c-130">選取 hello 資料夾，並注意 hello 資料夾現在會顯示在 hello**資料夾**控制項。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="c3b9c-131">![FTP 觸發程序影像 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="c3b9c-132">此時，應用程式邏輯已使用的觸發程序會在開始執行的 hello 其他觸發程序和 hello 工作流程中的動作檔案修改或建立 hello 特定 FTP 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="c3b9c-133">功能的邏輯應用程式 toobe，它必須包含至少一個觸發程序與一個動作。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="c3b9c-134">請遵循下一個區段 tooadd hello 動作中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="c3b9c-135">使用 FTP 動作</span><span class="sxs-lookup"><span data-stu-id="c3b9c-135">Use a FTP action</span></span>
<span data-ttu-id="c3b9c-136">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="c3b9c-137">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="c3b9c-138">既然您已加入觸發程序，請遵循這些步驟 tooadd 會收到 hello hello 觸發程序所找到的 hello 新增或修改檔案內容的動作。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="c3b9c-139">選取**+ 新增步驟**tooadd hello hello 動作 tooget hello hello 上檔案的內容 hello FTP 伺服器</span><span class="sxs-lookup"><span data-stu-id="c3b9c-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="c3b9c-140">選取 hello**將動作加入**連結。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="c3b9c-141">![FTP 動作影像 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="c3b9c-142">輸入*FTP* toosearch 所有動作相關 tooFTP。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="c3b9c-143">選取**FTP-取得檔案內容**為 hello 動作 tootake hello FTP 資料夾中發現新的或修改檔案時。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="c3b9c-144">![FTP 動作影像 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="c3b9c-145">hello**取得檔案內容**控制隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="c3b9c-146">**請注意**： 您將會提示的 tooauthorize 您邏輯應用程式 tooaccess FTP 伺服器帳戶如果您有之前未曾這麼做。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="c3b9c-147">![FTP 動作影像 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="c3b9c-148">選取 hello**檔案**控制項 (hello 空白字元位於下方**檔案***)。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="c3b9c-149">在這裡，您可以使用任何 hello 的各種屬性從 hello FTP 伺服器上找到的 hello 新增或修改檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="c3b9c-150">選取 hello**檔案內容**選項。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="c3b9c-151">![FTP 動作影像 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="c3b9c-152">更新 hello 控制項時，表示該 hello **FTP-取得檔案內容**動作會收到 hello*檔案內容*hello hello FTP 伺服器上新增或修改檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="c3b9c-153">![FTP 動作影像 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="c3b9c-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="c3b9c-154">儲存您的工作，然後將檔案 toohello FTP 資料夾 tootest 加入您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="c3b9c-155">此時，已經過 hello 邏輯應用程式與觸發程序 toomonitor 資料夾上設定 FTP 伺服器，並起始 hello 工作流程時它發現新的檔案或 hello FTP 伺服器上的已修改的檔案。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="c3b9c-156">hello 邏輯應用程式也已設定與動作 tooget hello 的 hello 新增或修改檔案內容。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="c3b9c-157">您現在可以加入另一個動作，例如 hello [SQL Server-插入資料列](connectors-create-api-sqlazure.md)hello 到 SQL 資料庫資料表的新增或修改檔案動作 tooinsert hello 內容。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="c3b9c-158">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="c3b9c-158">Connector-specific details</span></span>

<span data-ttu-id="c3b9c-159">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/ftpconnector/)。</span><span class="sxs-lookup"><span data-stu-id="c3b9c-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3b9c-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c3b9c-160">Next Steps</span></span>
[<span data-ttu-id="c3b9c-161">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="c3b9c-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

