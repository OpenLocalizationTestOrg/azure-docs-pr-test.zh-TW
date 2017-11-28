---
title: "Azure 邏輯應用程式中的 aaaDropbox 連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooDropbox toomanage 您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。"
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="82c11-105">開始使用 hello Dropbox 連接器</span><span class="sxs-lookup"><span data-stu-id="82c11-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="82c11-106">連接 tooDropbox toomanage 您的檔案。</span><span class="sxs-lookup"><span data-stu-id="82c11-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="82c11-107">您可以執行各種動作，例如上傳、更新、取得及刪除 Dropbox 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="82c11-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="82c11-108">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="82c11-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="82c11-109">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="82c11-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="82c11-110">連接 tooDropbox</span><span class="sxs-lookup"><span data-stu-id="82c11-110">Connect tooDropbox</span></span>
<span data-ttu-id="82c11-111">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="82c11-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="82c11-112">連線可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="82c11-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="82c11-113">例如，在訂單 tooconnect tooDropbox，您必須先 Dropbox*連接*。</span><span class="sxs-lookup"><span data-stu-id="82c11-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="82c11-114">toocreate 連線，您將需要您通常會使用您想要的 tooconnect tooaccess hello 服務 tooprovide hello 認證。</span><span class="sxs-lookup"><span data-stu-id="82c11-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="82c11-115">因此，在 hello Dropbox 範例中，您將需要 hello 認證 tooyour 順序 toocreate hello 連接 tooDropbox 的 Dropbox 帳戶。</span><span class="sxs-lookup"><span data-stu-id="82c11-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="82c11-116">深入了解連線</span><span class="sxs-lookup"><span data-stu-id="82c11-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="82c11-117">建立連接 tooDropbox</span><span class="sxs-lookup"><span data-stu-id="82c11-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="82c11-118">使用 Dropbox 觸發程序</span><span class="sxs-lookup"><span data-stu-id="82c11-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="82c11-119">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="82c11-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="82c11-120">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="82c11-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="82c11-121">在此範例中，我們將使用 hello**會建立一個檔案**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="82c11-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="82c11-122">這個觸發程序時，我們會呼叫 hello**取得檔案的內容使用路徑**Dropbox 動作。</span><span class="sxs-lookup"><span data-stu-id="82c11-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="82c11-123">輸入*dropbox* hello hello Logic Apps 設計工具上的搜尋方塊，然後選取 hello **Dropbox-建立檔案時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="82c11-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="82c11-124">選取您想在其中 tootrack 檔案建立 hello 資料夾。</span><span class="sxs-lookup"><span data-stu-id="82c11-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="82c11-125">選取此項目...（在 hello 紅色方塊識別） 和瀏覽 toohello 資料夾想 tooselect hello 觸發程序的輸入。</span><span class="sxs-lookup"><span data-stu-id="82c11-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="82c11-126">使用 Dropbox 動作</span><span class="sxs-lookup"><span data-stu-id="82c11-126">Use a Dropbox action</span></span>
<span data-ttu-id="82c11-127">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="82c11-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="82c11-128">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="82c11-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="82c11-129">既然 hello 已加入觸發程序，請遵循這些步驟 tooadd 執行的動作，會收到 hello 新檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="82c11-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="82c11-130">選取**+ 新增步驟**tooadd hello 動作您想要 tootake，建立新檔案時。</span><span class="sxs-lookup"><span data-stu-id="82c11-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="82c11-131">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="82c11-131">Select **Add an action**.</span></span> <span data-ttu-id="82c11-132">此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。</span><span class="sxs-lookup"><span data-stu-id="82c11-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="82c11-133">輸入*dropbox*動作相關 tooDropbox 的 toosearch。</span><span class="sxs-lookup"><span data-stu-id="82c11-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="82c11-134">選取**Dropbox-取得檔案的內容使用路徑**hello 動作 tootake hello 中建立新的檔案時選取的 Dropbox 資料夾。</span><span class="sxs-lookup"><span data-stu-id="82c11-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="82c11-135">hello 動作控制區塊會開啟。</span><span class="sxs-lookup"><span data-stu-id="82c11-135">hello action control block opens.</span></span> <span data-ttu-id="82c11-136">您將會提示的 tooauthorize 您邏輯應用程式 tooaccess，如果您還沒有這麼做之前，您的 Dropbox 帳戶。</span><span class="sxs-lookup"><span data-stu-id="82c11-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="82c11-137">選取此項目...(位於 hello hello 右邊**檔案路徑**控制項)，並瀏覽您想要 toouse toohello 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="82c11-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="82c11-138">或者，使用 hello**檔案路徑**語彙基元 toospeed 註冊您的邏輯應用程式建立。</span><span class="sxs-lookup"><span data-stu-id="82c11-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="82c11-139">儲存您的工作，並在 Dropbox tooactivate 中您的工作流程建立新的檔案。</span><span class="sxs-lookup"><span data-stu-id="82c11-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="82c11-140">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="82c11-140">Connector-specific details</span></span>

<span data-ttu-id="82c11-141">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/dropbox/)。</span><span class="sxs-lookup"><span data-stu-id="82c11-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="82c11-142">其他連接器</span><span class="sxs-lookup"><span data-stu-id="82c11-142">More connectors</span></span>
<span data-ttu-id="82c11-143">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="82c11-143">Go back toohello [APIs list](apis-list.md).</span></span>
