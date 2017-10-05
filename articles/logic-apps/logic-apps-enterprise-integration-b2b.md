---
title: "建立 B2B 解決方案 - Azure Logic Apps | Microsoft Docs"
description: "使用企業整合套件中的 B2B 功能在邏輯應用程式中接收資料"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="04589-103">使用企業整合套件中的 B2B 功能在邏輯應用程式中接收資料</span><span class="sxs-lookup"><span data-stu-id="04589-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="04589-104">建立具有合作夥伴與合約的整合帳戶之後，您就可以使用[企業整合套件](logic-apps-enterprise-integration-overview.md)為您的邏輯應用程式建立企業對企業 (B2B) 工作流程。</span><span class="sxs-lookup"><span data-stu-id="04589-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04589-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="04589-105">Prerequisites</span></span>

<span data-ttu-id="04589-106">若要使用 AS2 和 X12 動作，您必須有企業整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="04589-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="04589-107">了解[如何建立企業整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="04589-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="04589-108">使用 B2B 連接器建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="04589-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="04589-109">依照這些步驟建立使用 AS2 與 X12 動作從交易合作夥伴接收資料的 B2B 邏輯應用程式：</span><span class="sxs-lookup"><span data-stu-id="04589-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="04589-110">建立邏輯應用程式，然後[將應用程式連結到您的整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="04589-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="04589-111">將 [要求 - 收到 HTTP 要求時]  觸發程序新增到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="04589-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="04589-112">若要新增 [將 AS2 解碼] 動作，請選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="04589-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="04589-113">若要篩選所有動作以尋找您要的動作，請在搜尋方塊中輸入 **as2**。</span><span class="sxs-lookup"><span data-stu-id="04589-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="04589-114">選取 [AS2 - 將 AS2 訊息解碼] 動作。</span><span class="sxs-lookup"><span data-stu-id="04589-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="04589-115">新增要做為輸入使用的 [主體]。</span><span class="sxs-lookup"><span data-stu-id="04589-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="04589-116">在此範例中，選取觸發邏輯應用程式的 HTTP 要求主體。</span><span class="sxs-lookup"><span data-stu-id="04589-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="04589-117">或者，輸入會在 [標頭] 欄位輸入標頭的運算式：</span><span class="sxs-lookup"><span data-stu-id="04589-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="04589-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="04589-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="04589-119">針對 AS2 新增要求的 [標頭]，您可以在 HTTP 要求標頭中找到標頭。</span><span class="sxs-lookup"><span data-stu-id="04589-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="04589-120">在此範例中，選取觸發邏輯應用程式的 HTTP 要求標頭。</span><span class="sxs-lookup"><span data-stu-id="04589-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="04589-121">現在，新增「將 X12 訊息解碼」動作。</span><span class="sxs-lookup"><span data-stu-id="04589-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="04589-122">選取 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="04589-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="04589-123">若要篩選所有動作以尋找您要的動作，請在搜尋方塊中輸入 **x12**。</span><span class="sxs-lookup"><span data-stu-id="04589-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="04589-124">選取 [X12 - 將 X12 訊息解碼] 動作。</span><span class="sxs-lookup"><span data-stu-id="04589-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="04589-125">現在您必須指定此動作的輸入。</span><span class="sxs-lookup"><span data-stu-id="04589-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="04589-126">此輸入是上一個 AS2 動作的輸出。</span><span class="sxs-lookup"><span data-stu-id="04589-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="04589-127">實際訊息內容是 JSON 物件格式且使用 base64 編碼，因此您必須將運算式指定為輸入。</span><span class="sxs-lookup"><span data-stu-id="04589-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="04589-128">在 [要解碼的 X12 一般檔案訊息] 輸入欄位中輸入下列運算式：</span><span class="sxs-lookup"><span data-stu-id="04589-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="04589-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="04589-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="04589-130">現在，請新增步驟以將接收自交易夥伴的 X12 資料解碼，並輸出 JSON 物件中的一些項目。</span><span class="sxs-lookup"><span data-stu-id="04589-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="04589-131">若要通知合作夥伴已收到資料，您可以在 HTTP 回應動作中送回包含 AS2 郵件處置通知 (MDN) 的回應。</span><span class="sxs-lookup"><span data-stu-id="04589-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="04589-132">若要新增 [回應] 動作，請選擇 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="04589-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="04589-133">若要篩選所有動作以尋找您要的動作，請在搜尋方塊中輸入**回應**。</span><span class="sxs-lookup"><span data-stu-id="04589-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="04589-134">選取 [回應] 動作。</span><span class="sxs-lookup"><span data-stu-id="04589-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="04589-135">若要從 [將 X12 訊息解碼] 動作的輸出存取 MDN，請使用此運算式設定回應**主體**：</span><span class="sxs-lookup"><span data-stu-id="04589-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="04589-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="04589-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="04589-137">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="04589-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="04589-138">您現在已完成 B2B 邏輯應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="04589-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="04589-139">在真實世界應用程式中，您可能想要在企業營運 (LOB) 應用程式或資料存放區中儲存已解碼的 X12 資料。</span><span class="sxs-lookup"><span data-stu-id="04589-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="04589-140">若要連線到您自己的 LOB 應用程式並在您的邏輯應用程式中使用這些 API，您可以新增進一步的動作或撰寫自訂 API。</span><span class="sxs-lookup"><span data-stu-id="04589-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="04589-141">功能和使用案例</span><span class="sxs-lookup"><span data-stu-id="04589-141">Features and use cases</span></span>

* <span data-ttu-id="04589-142">AS2 與 X12 解碼與編碼動作可讓您在邏輯應用程式中使用業界標準通訊協定在交易合作夥伴之間交換資料。</span><span class="sxs-lookup"><span data-stu-id="04589-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="04589-143">若要與交易合作夥伴交換資料，您可以使用 AS2 或 X12 其中一種或將兩種搭配使用。</span><span class="sxs-lookup"><span data-stu-id="04589-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="04589-144">B2B 動作可協助您在整合帳戶中輕鬆地建立合作夥伴與合約，並在邏輯應用程式中取用。</span><span class="sxs-lookup"><span data-stu-id="04589-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="04589-145">當您使用其他動作延伸您邏輯應用程式的功能時，您可以在其他應用程式與服務 (例如 SalesForce) 之間傳送及接收資料。</span><span class="sxs-lookup"><span data-stu-id="04589-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="04589-146">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="04589-146">Learn more</span></span>
[<span data-ttu-id="04589-147">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="04589-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
