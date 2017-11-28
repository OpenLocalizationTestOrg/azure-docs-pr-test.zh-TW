---
title: "aaaCreate B2B 解決方案-Azure 邏輯應用程式 |Microsoft 文件"
description: "邏輯應用程式中接收資料，使用 hello 企業版整合套件 hello B2B 功能"
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
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="be7da-103">在邏輯與 hello 企業版整合套件中的 hello B2B 功能的應用程式中接收資料</span><span class="sxs-lookup"><span data-stu-id="be7da-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="be7da-104">建立具有夥伴和協議的整合帳戶之後，您就準備好 toocreate 商務 toobusiness (B2B) 工作流程應用程式邏輯，以 hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="be7da-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be7da-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="be7da-105">Prerequisites</span></span>

<span data-ttu-id="be7da-106">toouse hello AS2 與 X12 動作，您必須擁有 Enterprise 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="be7da-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="be7da-107">深入了解[如何 toocreate 企業整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="be7da-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="be7da-108">使用 B2B 連接器建立邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="be7da-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="be7da-109">請遵循這些步驟 toocreate B2B 邏輯的應用程式使用 hello AS2 與 X12 動作 tooreceive 資料從交易夥伴：</span><span class="sxs-lookup"><span data-stu-id="be7da-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="be7da-110">建立邏輯應用程式，然後[連結您的應用程式 tooyour 整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="be7da-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="be7da-111">新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="be7da-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="be7da-112">tooadd hello**解碼的 AS2**動作選取**將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="be7da-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="be7da-113">toofilter，其中的所有動作 toohello 都輸入 hello 字**as2** hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="be7da-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="be7da-114">選取 hello **AS2 的解碼 AS2 訊息**動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="be7da-115">新增 hello**主體**想 toouse 做為輸入。</span><span class="sxs-lookup"><span data-stu-id="be7da-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="be7da-116">在此範例中，選取 hello hello 觸發程序 hello 邏輯應用程式的 HTTP 要求主體。</span><span class="sxs-lookup"><span data-stu-id="be7da-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="be7da-117">或輸入運算式，以輸入 hello 標頭中 hello**標頭**欄位：</span><span class="sxs-lookup"><span data-stu-id="be7da-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="be7da-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="be7da-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="be7da-119">新增所需的 hello**標頭**as2，您可以在 hello HTTP 要求標頭中找到。</span><span class="sxs-lookup"><span data-stu-id="be7da-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="be7da-120">在此範例中，選取 hello hello HTTP 要求標頭該觸發程序 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="be7da-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="be7da-121">現在加入 hello 解碼 X12 訊息的動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="be7da-122">選取 [新增動作] 。</span><span class="sxs-lookup"><span data-stu-id="be7da-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="be7da-123">toofilter，其中的所有動作 toohello 都輸入 hello 字**x12** hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="be7da-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="be7da-124">選取 hello **X12-解碼 X12 訊息**動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="be7da-125">現在，您必須指定 hello 輸入的 toothis 動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="be7da-126">這項輸入是來自上一個 AS2 動作 hello 的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="be7da-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="be7da-127">hello 實際訊息內容的 JSON 物件中，而且是 base64 編碼，因此您必須指定的運算式做為輸入 hello。</span><span class="sxs-lookup"><span data-stu-id="be7da-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="be7da-128">輸入下列運算式在 hello hello **X12 一般檔案訊息 tooDECODE**輸入的欄位：</span><span class="sxs-lookup"><span data-stu-id="be7da-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="be7da-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="be7da-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="be7da-130">現在加入的步驟 toodecode hello X12 資料收到來自交易夥伴的 hello 和輸出的 JSON 物件中的項目。</span><span class="sxs-lookup"><span data-stu-id="be7da-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="be7da-131">收到 hello 資料 toonotify hello 協力電腦，您可以將回應傳回包含 hello AS2 訊息處理通知 (MDN) 中 HTTP 回應動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="be7da-132">tooadd hello**回應**動作中，選擇**將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="be7da-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="be7da-133">toofilter，其中的所有動作 toohello 都輸入 hello 字**回應**hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="be7da-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="be7da-134">選取 hello**回應**動作。</span><span class="sxs-lookup"><span data-stu-id="be7da-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="be7da-135">tooaccess hello hello hello 輸出 MDN**解碼 X12 訊息**動作，集 hello 回應**主體**欄位的這個運算式：</span><span class="sxs-lookup"><span data-stu-id="be7da-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="be7da-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="be7da-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="be7da-137">儲存您的工作。</span><span class="sxs-lookup"><span data-stu-id="be7da-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="be7da-138">您現在已完成 B2B 邏輯應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="be7da-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="be7da-139">在真實世界應用程式中，您可能想 toostore hello 解碼 X12 特定業務 (LOB) 應用程式或資料存放區中的資料。</span><span class="sxs-lookup"><span data-stu-id="be7da-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="be7da-140">tooconnect 您自己的 LOB 應用程式和應用程式邏輯中使用這些 Api，您可以新增進一步的動作或撰寫自訂應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="be7da-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="be7da-141">功能和使用案例</span><span class="sxs-lookup"><span data-stu-id="be7da-141">Features and use cases</span></span>

* <span data-ttu-id="be7da-142">hello AS2 與 X12 解碼和編碼動作可讓您在邏輯應用程式中使用業界標準通訊協定交易夥伴間交換資料。</span><span class="sxs-lookup"><span data-stu-id="be7da-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="be7da-143">與交易夥伴 tooexchange 資料，您可以使用 AS2 與 X12，不論彼此。</span><span class="sxs-lookup"><span data-stu-id="be7da-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="be7da-144">hello B2B 動作可協助您整合帳戶中輕鬆地建立夥伴和協議，及在邏輯應用程式中使用它們。</span><span class="sxs-lookup"><span data-stu-id="be7da-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="be7da-145">當您使用其他動作延伸您邏輯應用程式的功能時，您可以在其他應用程式與服務 (例如 SalesForce) 之間傳送及接收資料。</span><span class="sxs-lookup"><span data-stu-id="be7da-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="be7da-146">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="be7da-146">Learn more</span></span>
[<span data-ttu-id="be7da-147">深入了解 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="be7da-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
