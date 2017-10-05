---
title: "了解如何在邏輯應用程式中使用 FTP 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 連線到 FTP 伺服器來管理您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 FTP 伺服器中的檔案。"
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
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="5b7a1-105">開始使用 FTP 連接器</span><span class="sxs-lookup"><span data-stu-id="5b7a1-105">Get started with the FTP connector</span></span>
<span data-ttu-id="5b7a1-106">使用 FTP 連接器在 FTP 伺服器上監視、管理和建立檔案。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="5b7a1-107">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="5b7a1-108">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="5b7a1-109">連接至 FTP</span><span class="sxs-lookup"><span data-stu-id="5b7a1-109">Connect to FTP</span></span>
<span data-ttu-id="5b7a1-110">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="5b7a1-111">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="5b7a1-112">建立至 FTP 的連線</span><span class="sxs-lookup"><span data-stu-id="5b7a1-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="5b7a1-113">使用 FTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b7a1-113">Use a FTP trigger</span></span>
<span data-ttu-id="5b7a1-114">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="5b7a1-115">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="5b7a1-116">FTP 連接器需要可從網際網路存取且設定為以「被動」模式運作的 FTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="5b7a1-117">此外，FTP 連接器**與隱含 FTPS (FTP over SSL) 不相容**。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="5b7a1-118">FTP 連接器只支援明確 FTPS (FTP over SSL)。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="5b7a1-119">在此範例中，我將告訴您如何使用 **FTP - 新增或修改檔案時**觸發程序，在檔案新增或修改於 FTP 伺服器時起始邏輯應用程式工作流程。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="5b7a1-120">在企業範例中，您可以使用此觸發程序來監視代表客戶訂單的新檔案 FTP 資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="5b7a1-121">然後，您可以使用 FTP 連接器動作 (例如**取得檔案內容**) 取得訂單的內容以進一步處理並儲存在訂單資料庫中。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="5b7a1-122">在邏輯應用程式設計工具的搜尋方塊中輸入 *ftp*，然後選取 [SFTP - 當新增或修改檔案時] 觸發程序</span><span class="sxs-lookup"><span data-stu-id="5b7a1-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="5b7a1-123">![FTP 觸發程序影像 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="5b7a1-124">[當新增或修改檔案時] 控制項隨即開啟</span><span class="sxs-lookup"><span data-stu-id="5b7a1-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="5b7a1-125">![FTP 觸發程序影像 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="5b7a1-126">選取位於控制項右側的 [...]  。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="5b7a1-127">這會開啟資料夾選擇器控制項 </span><span class="sxs-lookup"><span data-stu-id="5b7a1-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="5b7a1-128">![FTP 觸發程序影像 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="5b7a1-129">選取 **>** (向右箭號)，並瀏覽尋找您要對新的或修改過檔案監視的資料夾。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="5b7a1-130">選取資料夾，請注意資料夾現已顯示在 [資料夾] 控制項中。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="5b7a1-131">![FTP 觸發程序影像 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="5b7a1-132">此時，邏輯應用程式已設有觸發程序，該觸發程序會在檔案於特定 FTP 資料夾中修改或建立時，開始執行工作流程中的其他觸發程序和動作。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="5b7a1-133">若要讓邏輯應用程式能夠運作，它必須至少包含一個觸發程序和一個動作。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="5b7a1-134">請依照下一節中的步驟來新增動作。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="5b7a1-135">使用 FTP 動作</span><span class="sxs-lookup"><span data-stu-id="5b7a1-135">Use a FTP action</span></span>
<span data-ttu-id="5b7a1-136">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="5b7a1-137">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="5b7a1-138">您現已新增觸發程序，請遵循下列步驟來新增動作，該動作將會取得觸發程序所找到之新的或修改過檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="5b7a1-139">選取 [+ 新增步驟] 來新增動作，以取得 FTP 伺服器上檔案的內容</span><span class="sxs-lookup"><span data-stu-id="5b7a1-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="5b7a1-140">選取 [新增動作]  連結。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="5b7a1-141">![FTP 動作影像 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="5b7a1-142">輸入 *FTP* 以搜尋與 FTP 相關的所有動作。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="5b7a1-143">選取 [FTP - 取得檔案內容]，做為在 FTP 資料夾中找到新的或修改過檔案時所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="5b7a1-144">![FTP 動作影像 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="5b7a1-145">[取得檔案內容] 控制項隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-145">The **Get file content** control opens.</span></span> <span data-ttu-id="5b7a1-146">**附註：**如果您未曾授權邏輯應用程式存取您的 FTP 伺服器帳戶，系統會提示您這麼做。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="5b7a1-147">![FTP 動作影像 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="5b7a1-148">選取 [檔案] 控制項 (位於 [檔案]* 下方的空白處)。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="5b7a1-149">在這裡，您可以使用 FTP 伺服器上找到之新的或修改過檔案中的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="5b7a1-150">選取 [檔案內容] 選項。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="5b7a1-151">![FTP 動作影像 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="5b7a1-152">控制項已更新，這表示 [FTP - 取得檔案內容] 動作會取得 FTP 伺服器上新的或修改過檔案的*檔案內容*。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="5b7a1-153">![FTP 動作影像 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="5b7a1-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="5b7a1-154">儲存您的工作，然後將檔案加入至 FTP 資料夾，以測試您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="5b7a1-155">此時，邏輯應用程式已設有觸發程序來監視 FTP 伺服器上的資料夾，而當它在 FTP 伺服器上找到新的檔案或修改過的檔案時會起始工作流程。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="5b7a1-156">邏輯應用程式也已設有一個動作，以取得新的或修改過檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="5b7a1-157">您現在可以新增另一個動作，例如 [SQL Server - 插入資料列](connectors-create-api-sqlazure.md)動作，已在 SQL Database 資料表中插入新的或修改過檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="5b7a1-158">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="5b7a1-158">Connector-specific details</span></span>

<span data-ttu-id="5b7a1-159">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/ftpconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="5b7a1-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5b7a1-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b7a1-160">Next Steps</span></span>
[<span data-ttu-id="5b7a1-161">建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="5b7a1-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

