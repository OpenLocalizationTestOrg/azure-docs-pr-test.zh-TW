---
title: "Azure Logic Apps 中的 Dropbox 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 連線到 Dropbox 來管理您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="2d234-105">開始使用 Dropbox 連接器</span><span class="sxs-lookup"><span data-stu-id="2d234-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="2d234-106">連線到 Dropbox 來管理您的檔案。</span><span class="sxs-lookup"><span data-stu-id="2d234-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="2d234-107">您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="2d234-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="2d234-108">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d234-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="2d234-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="2d234-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="2d234-110">連接至 Dropbox。</span><span class="sxs-lookup"><span data-stu-id="2d234-110">Connect to Dropbox</span></span>
<span data-ttu-id="2d234-111">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="2d234-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="2d234-112">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="2d234-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="2d234-113">例如，若要連線至 Dropbox，您必須先建立 Dropbox *連線*。</span><span class="sxs-lookup"><span data-stu-id="2d234-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="2d234-114">若要建立連線，您需要提供平常用來存取所要連線之服務的認證。</span><span class="sxs-lookup"><span data-stu-id="2d234-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="2d234-115">因此，在 Dropbox 範例中，您需要 Dropbox 帳戶的認證，才能建立與 Dropbox 的連線。</span><span class="sxs-lookup"><span data-stu-id="2d234-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="2d234-116">深入了解連線</span><span class="sxs-lookup"><span data-stu-id="2d234-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="2d234-117">建立 Dropbox 連線</span><span class="sxs-lookup"><span data-stu-id="2d234-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="2d234-118">使用 Dropbox 觸發程序</span><span class="sxs-lookup"><span data-stu-id="2d234-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="2d234-119">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="2d234-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="2d234-120">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="2d234-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="2d234-121">在此範例中，我們將使用**建立檔案時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2d234-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="2d234-122">當此觸發程序發生時，我們會呼叫**使用路徑來取得檔案內容** Dropbox 動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="2d234-123">在 Logic Apps 設計工具的搜尋方塊中輸入 *dropbox*，然後選取 [Dropbox - 建立檔案時] 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2d234-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="2d234-124">選取您想要追蹤檔案建立所在的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d234-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="2d234-125">選取 [...]\(以紅色方塊識別)，並瀏覽至您想要針對觸發程序的輸入而選取的資料夾。</span><span class="sxs-lookup"><span data-stu-id="2d234-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="2d234-126">使用 Dropbox 動作</span><span class="sxs-lookup"><span data-stu-id="2d234-126">Use a Dropbox action</span></span>
<span data-ttu-id="2d234-127">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="2d234-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="2d234-128">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="2d234-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="2d234-129">現在已新增觸發程序，請遵循下列步驟來新增將會取得新檔案內容的動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="2d234-130">選取 [+ 新的步驟] 來新增您想要在新檔案建立時採取的動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="2d234-131">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="2d234-131">Select **Add an action**.</span></span> <span data-ttu-id="2d234-132">這會開啟搜尋方塊，您可以在其中搜尋任何想要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="2d234-133">輸入 *dropbox* 以搜尋與 Dropbox 相關的動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="2d234-134">選取 [Dropbox - 使用路徑來取得檔案內容]，做為在選取的 Dropbox 資料夾中建立新檔案時所要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="2d234-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="2d234-135">動作控制區塊便會開啟。</span><span class="sxs-lookup"><span data-stu-id="2d234-135">The action control block opens.</span></span> <span data-ttu-id="2d234-136">如果您未曾授權邏輯應用程式存取您的 Dropbox 帳戶，系統會提示您這麼做。</span><span class="sxs-lookup"><span data-stu-id="2d234-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="2d234-137">選取 [...]\(位於 [檔案路徑] 控制項的右側)，並瀏覽至您想要使用的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="2d234-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="2d234-138">或者，使用**檔案路徑**權杖來加速建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d234-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="2d234-139">儲存您的工作並在 Dropbox 中建立新檔案，以啟動您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="2d234-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="2d234-140">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="2d234-140">Connector-specific details</span></span>

<span data-ttu-id="2d234-141">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/dropbox/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="2d234-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="2d234-142">其他連接器</span><span class="sxs-lookup"><span data-stu-id="2d234-142">More connectors</span></span>
<span data-ttu-id="2d234-143">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="2d234-143">Go back to the [APIs list](apis-list.md).</span></span>