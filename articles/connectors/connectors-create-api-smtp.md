---
title: "Azure 邏輯應用程式中的 aaaSMTP 連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooSMTP toosend 電子郵件。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="ff53e-104">開始使用 hello SMTP 連接器</span><span class="sxs-lookup"><span data-stu-id="ff53e-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="ff53e-105">連接 tooSMTP toosend 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="ff53e-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="ff53e-106">toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff53e-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="ff53e-107">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="ff53e-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="ff53e-108">連接 tooSMTP</span><span class="sxs-lookup"><span data-stu-id="ff53e-108">Connect tooSMTP</span></span>
<span data-ttu-id="ff53e-109">邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="ff53e-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="ff53e-110">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="ff53e-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="ff53e-111">例如，tooconnect tooSMTP，您必須先 SMTP*連接*。</span><span class="sxs-lookup"><span data-stu-id="ff53e-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="ff53e-112">toocreate 連線，請輸入您平常用 tooaccess hello 服務連接到 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="ff53e-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="ff53e-113">因此，在 hello SMTP 範例中，輸入 hello 認證 tooyour 連線名稱、 SMTP 伺服器位址，以及使用者登入資訊 toocreate hello 連接 tooSMTP。</span><span class="sxs-lookup"><span data-stu-id="ff53e-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="ff53e-114">建立連接 tooSMTP</span><span class="sxs-lookup"><span data-stu-id="ff53e-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="ff53e-115">使用 SMTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="ff53e-115">Use an SMTP trigger</span></span>
<span data-ttu-id="ff53e-116">觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。</span><span class="sxs-lookup"><span data-stu-id="ff53e-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="ff53e-117">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="ff53e-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="ff53e-118">在此範例中，因為 SMTP 沒有觸發程序，我們將使用 hello **Salesforce-建立物件時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ff53e-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="ff53e-119">當 Salesforce 中有新的物件建立時，觸發程序就會啟動。</span><span class="sxs-lookup"><span data-stu-id="ff53e-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="ff53e-120">範例中，我們會設定它使得每次在 Salesforce 中建立新的前置*傳送電子郵件*透過 hello SMTP 連接器，以建立 hello 新潛在客戶通知所發生的動作。</span><span class="sxs-lookup"><span data-stu-id="ff53e-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="ff53e-121">輸入*salesforce* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **Salesforce-建立物件時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ff53e-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="ff53e-122">hello**當建立物件**顯示控制項。</span><span class="sxs-lookup"><span data-stu-id="ff53e-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="ff53e-123">選取 hello**物件型別**然後選取*導致*hello 清單中的物件。</span><span class="sxs-lookup"><span data-stu-id="ff53e-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="ff53e-124">在此步驟中，您會指出您要建立一個觸發程序，此觸發程序將在每次 Salesforce 中有建立新潛在客戶的情況時，通知您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff53e-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="ff53e-125">已建立 hello 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="ff53e-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="ff53e-126">使用 SMTP 動作</span><span class="sxs-lookup"><span data-stu-id="ff53e-126">Use an SMTP action</span></span>
<span data-ttu-id="ff53e-127">動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。</span><span class="sxs-lookup"><span data-stu-id="ff53e-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="ff53e-128">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="ff53e-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="ff53e-129">既然 hello 已加入觸發程序，請遵循在 Salesforce 中建立新的負責人時，會發生這些步驟 tooadd SMTP 動作。</span><span class="sxs-lookup"><span data-stu-id="ff53e-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="ff53e-130">選取**+ 新增步驟**tooadd hello 動作您想要 tootake，建立新的負責人時。</span><span class="sxs-lookup"><span data-stu-id="ff53e-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="ff53e-131">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="ff53e-131">Select **Add an action**.</span></span> <span data-ttu-id="ff53e-132">此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。</span><span class="sxs-lookup"><span data-stu-id="ff53e-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="ff53e-133">輸入*smtp*動作相關 tooSMTP 的 toosearch。</span><span class="sxs-lookup"><span data-stu-id="ff53e-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="ff53e-134">選取**SMTP-傳送電子郵件**為 hello 動作 tootake hello 新前置建立時。</span><span class="sxs-lookup"><span data-stu-id="ff53e-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="ff53e-135">hello 動作控制區塊會開啟。</span><span class="sxs-lookup"><span data-stu-id="ff53e-135">hello action control block opens.</span></span> <span data-ttu-id="ff53e-136">您將 tooestablish smtp 連接 hello 設計工具在區塊中有如果您有之前未曾這麼做。</span><span class="sxs-lookup"><span data-stu-id="ff53e-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="ff53e-137">輸入您想要的電子郵件中的資訊 hello **SMTP-傳送電子郵件**區塊。</span><span class="sxs-lookup"><span data-stu-id="ff53e-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="ff53e-138">儲存您的工作順序 tooactivate 在您的工作流程。</span><span class="sxs-lookup"><span data-stu-id="ff53e-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="ff53e-139">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="ff53e-139">Connector-specific details</span></span>

<span data-ttu-id="ff53e-140">檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/smtpconnector/)。</span><span class="sxs-lookup"><span data-stu-id="ff53e-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="ff53e-141">其他連接器</span><span class="sxs-lookup"><span data-stu-id="ff53e-141">More connectors</span></span>
<span data-ttu-id="ff53e-142">返回 toohello [Api 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="ff53e-142">Go back toohello [APIs list](apis-list.md).</span></span>
