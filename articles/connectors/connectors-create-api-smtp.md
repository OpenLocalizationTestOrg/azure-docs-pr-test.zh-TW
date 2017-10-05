---
title: "Azure Logic Apps 中的 SMTP 連接器 | Microsoft Docs"
description: "使用 Azure App Service 建立邏輯應用程式。 連接到 SMTP 以傳送電子郵件。"
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
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="0bed7-104">開始使用 SMTP 連接器</span><span class="sxs-lookup"><span data-stu-id="0bed7-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="0bed7-105">連接到 SMTP 以傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="0bed7-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="0bed7-106">若要使用[任何連接器](apis-list.md)，您必須先建立邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bed7-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="0bed7-107">您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。</span><span class="sxs-lookup"><span data-stu-id="0bed7-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="0bed7-108">連接到 SMTP</span><span class="sxs-lookup"><span data-stu-id="0bed7-108">Connect to SMTP</span></span>
<span data-ttu-id="0bed7-109">您必須先建立與服務的連線，才能透過邏輯應用程式存取任何服務。</span><span class="sxs-lookup"><span data-stu-id="0bed7-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="0bed7-110">[連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。</span><span class="sxs-lookup"><span data-stu-id="0bed7-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="0bed7-111">例如，若要連接到 SMTP，您必須先有 SMTP「連線」。</span><span class="sxs-lookup"><span data-stu-id="0bed7-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="0bed7-112">若要建立連線，請輸入平常用來存取連線服務的認證。</span><span class="sxs-lookup"><span data-stu-id="0bed7-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="0bed7-113">因此，在 SMTP 範例中，請輸入連接名稱、SMTP 伺服器位址，以及使用者登入資訊等認證來建立 SMTP 連線。</span><span class="sxs-lookup"><span data-stu-id="0bed7-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="0bed7-114">建立至 SMTP 的連線</span><span class="sxs-lookup"><span data-stu-id="0bed7-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="0bed7-115">使用 SMTP 觸發程序</span><span class="sxs-lookup"><span data-stu-id="0bed7-115">Use an SMTP trigger</span></span>
<span data-ttu-id="0bed7-116">觸發程序是可用來啟動邏輯應用程式中所定義之工作流程的事件。</span><span class="sxs-lookup"><span data-stu-id="0bed7-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="0bed7-117">[深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="0bed7-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="0bed7-118">在此範例中，由於 SMTP 沒有自己的觸發程序，因此我們將使用 **Salesforce - 當物件建立時**觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0bed7-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="0bed7-119">當 Salesforce 中有新的物件建立時，觸發程序就會啟動。</span><span class="sxs-lookup"><span data-stu-id="0bed7-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="0bed7-120">在範例中，我們會設定使其每次在 Salesforce 中建立新的潛在客戶時，系統會透過 SMTP 連接器執行*傳送電子郵件*的動作，並附帶已建立新潛在客戶的通知。</span><span class="sxs-lookup"><span data-stu-id="0bed7-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="0bed7-121">在邏輯應用程式設計工具的搜尋方塊中輸入 *salesforce*，然後選取 [Salesforce - 當建立物件時] 觸發程序。</span><span class="sxs-lookup"><span data-stu-id="0bed7-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="0bed7-122">[當建立物件時]  控制項隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="0bed7-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="0bed7-123">選取 [物件類型] 然後從清單的物件中選取 [潛在客戶]。</span><span class="sxs-lookup"><span data-stu-id="0bed7-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="0bed7-124">在此步驟中，您會指出您要建立一個觸發程序，此觸發程序將在每次 Salesforce 中有建立新潛在客戶的情況時，通知您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="0bed7-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="0bed7-125">觸發程序已建立。</span><span class="sxs-lookup"><span data-stu-id="0bed7-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="0bed7-126">使用 SMTP 動作</span><span class="sxs-lookup"><span data-stu-id="0bed7-126">Use an SMTP action</span></span>
<span data-ttu-id="0bed7-127">動作是由邏輯應用程式中定義的工作流程所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="0bed7-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="0bed7-128">[深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。</span><span class="sxs-lookup"><span data-stu-id="0bed7-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="0bed7-129">現在已新增觸發程序之後，請遵循下列步驟新增 Salesforce 中有新的潛在客戶建立時會發生的 SMTP 動作。</span><span class="sxs-lookup"><span data-stu-id="0bed7-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="0bed7-130">選取 [+ 新的步驟]，來新增您想要在建立新的潛在客戶時採取的動作。</span><span class="sxs-lookup"><span data-stu-id="0bed7-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="0bed7-131">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="0bed7-131">Select **Add an action**.</span></span> <span data-ttu-id="0bed7-132">這會開啟搜尋方塊，您可以在其中搜尋任何想要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="0bed7-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="0bed7-133">輸入 *smtp* 以搜尋與 SMTP 相關的動作。</span><span class="sxs-lookup"><span data-stu-id="0bed7-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="0bed7-134">選取 [SMTP - 傳送電子郵件]，做為建立新的潛在客戶時要採取的動作。</span><span class="sxs-lookup"><span data-stu-id="0bed7-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="0bed7-135">動作控制區塊便會開啟。</span><span class="sxs-lookup"><span data-stu-id="0bed7-135">The action control block opens.</span></span> <span data-ttu-id="0bed7-136">如果您先前未曾在設計工具區塊中建立 SMTP 連線，您必須這麼做。</span><span class="sxs-lookup"><span data-stu-id="0bed7-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="0bed7-137">在 [SMTP - 傳送電子郵件] 區塊中輸入所需的電子郵件資訊。</span><span class="sxs-lookup"><span data-stu-id="0bed7-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="0bed7-138">儲存您的工作以啟動工作流程。</span><span class="sxs-lookup"><span data-stu-id="0bed7-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="0bed7-139">連接器特定的詳細資料</span><span class="sxs-lookup"><span data-stu-id="0bed7-139">Connector-specific details</span></span>

<span data-ttu-id="0bed7-140">檢視 Swagger 中定義的任何觸發程序和動作，另請參閱[連接器詳細資料](/connectors/smtpconnector/)的所有限制。</span><span class="sxs-lookup"><span data-stu-id="0bed7-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0bed7-141">其他連接器</span><span class="sxs-lookup"><span data-stu-id="0bed7-141">More connectors</span></span>
<span data-ttu-id="0bed7-142">返回 [API 清單](apis-list.md)。</span><span class="sxs-lookup"><span data-stu-id="0bed7-142">Go back to the [APIs list](apis-list.md).</span></span>