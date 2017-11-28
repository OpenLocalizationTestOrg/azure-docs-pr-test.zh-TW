---
title: "aaaDecode AS2 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "Toouse hello hello 企業版整合套件中的 AS2 解碼器 Azure 邏輯應用程式的方式"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 2406e5ec68e0906700fad97d60cb83ef0d106cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="decode-as2-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="6a36e-103">Azure 邏輯應用程式的解碼 AS2 訊息，以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="6a36e-103">Decode AS2 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span> 

<span data-ttu-id="6a36e-104">tooestablish 安全性和可靠性時傳輸訊息，使用 hello 解碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="6a36e-104">tooestablish security and reliability while transmitting messages, use hello Decode AS2 message connector.</span></span> <span data-ttu-id="6a36e-105">此連接器可透過訊息處置通知 (MDN) 提供數位簽章、解密和通知。</span><span class="sxs-lookup"><span data-stu-id="6a36e-105">This connector provides digital signing, decryption, and acknowledgements through Message Disposition Notifications (MDN).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="6a36e-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="6a36e-106">Before you start</span></span>

<span data-ttu-id="6a36e-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="6a36e-107">Here's hello items you need:</span></span>

* <span data-ttu-id="6a36e-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="6a36e-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="6a36e-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="6a36e-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="6a36e-110">您必須為整合帳戶 toouse hello 解碼 AS2 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="6a36e-110">You must have an integration account toouse hello Decode AS2 message connector.</span></span>
* <span data-ttu-id="6a36e-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="6a36e-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="6a36e-112">已經在整合帳戶中定義的 [AS2 合約](logic-apps-enterprise-integration-as2.md)</span><span class="sxs-lookup"><span data-stu-id="6a36e-112">An [AS2 agreement](logic-apps-enterprise-integration-as2.md) that's already defined in your integration account</span></span>

## <a name="decode-as2-messages"></a><span data-ttu-id="6a36e-113">解碼 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="6a36e-113">Decode AS2 messages</span></span>

1. <span data-ttu-id="6a36e-114">[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="6a36e-114">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="6a36e-115">沒有觸發程序，hello 解碼 AS2 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="6a36e-115">hello Decode AS2 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="6a36e-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a36e-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="6a36e-117">Hello 搜尋方塊中，輸入您的篩選器"AS2"。</span><span class="sxs-lookup"><span data-stu-id="6a36e-117">In hello search box, enter "AS2" for your filter.</span></span> <span data-ttu-id="6a36e-118">選取 [AS2 - 解碼 AS2 訊息]。</span><span class="sxs-lookup"><span data-stu-id="6a36e-118">Select **AS2 - Decode AS2 message**.</span></span>
   
    ![搜尋 "AS2"](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage1.png)

4. <span data-ttu-id="6a36e-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="6a36e-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="6a36e-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a36e-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage2.png)

    <span data-ttu-id="6a36e-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="6a36e-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="6a36e-124">屬性</span><span class="sxs-lookup"><span data-stu-id="6a36e-124">Property</span></span> | <span data-ttu-id="6a36e-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="6a36e-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="6a36e-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="6a36e-126">Connection Name *</span></span> |<span data-ttu-id="6a36e-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="6a36e-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="6a36e-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="6a36e-128">Integration Account *</span></span> |<span data-ttu-id="6a36e-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="6a36e-129">Enter a name for your integration account.</span></span> <span data-ttu-id="6a36e-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="6a36e-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="6a36e-131">當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="6a36e-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="6a36e-132">選擇 建立您的連線，toofinish**建立**。</span><span class="sxs-lookup"><span data-stu-id="6a36e-132">toofinish creating your connection, choose **Create**.</span></span>

    ![整合連線詳細資料](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage3.png)

6. <span data-ttu-id="6a36e-134">建立您的連線時，此範例中所示之後，請選取**主體**和**標頭**hello 從要求的輸出。</span><span class="sxs-lookup"><span data-stu-id="6a36e-134">After your connection is created, as shown in this example, select **Body** and **Headers** from hello Request outputs.</span></span>
   
    ![已建立整合連線](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage4.png) 

    <span data-ttu-id="6a36e-136">例如：</span><span class="sxs-lookup"><span data-stu-id="6a36e-136">For example:</span></span>

    ![從要求輸出選取內文和標頭](media/logic-apps-enterprise-integration-as2-decode/as2decodeimage5.png) 

## <a name="as2-decoder-details"></a><span data-ttu-id="6a36e-138">AS2 解碼器詳細資料</span><span class="sxs-lookup"><span data-stu-id="6a36e-138">AS2 decoder details</span></span>

<span data-ttu-id="6a36e-139">hello 解碼的 AS2 連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="6a36e-139">hello Decode AS2 connector performs these tasks:</span></span> 

* <span data-ttu-id="6a36e-140">處理 AS2/HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="6a36e-140">Processes AS2/HTTP headers</span></span>
* <span data-ttu-id="6a36e-141">確認 hello 簽章 （如果有設定）</span><span class="sxs-lookup"><span data-stu-id="6a36e-141">Verifies hello signature (if configured)</span></span>
* <span data-ttu-id="6a36e-142">解密 hello 訊息 （若已設定）</span><span class="sxs-lookup"><span data-stu-id="6a36e-142">Decrypts hello messages (if configured)</span></span>
* <span data-ttu-id="6a36e-143">將解壓縮 hello 訊息 （若已設定）</span><span class="sxs-lookup"><span data-stu-id="6a36e-143">Decompresses hello message (if configured)</span></span>
* <span data-ttu-id="6a36e-144">協調收到的 MDN 與 hello 原始輸出訊息</span><span class="sxs-lookup"><span data-stu-id="6a36e-144">Reconciles a received MDN with hello original outbound message</span></span>
* <span data-ttu-id="6a36e-145">更新，並將 hello 不可否認性資料庫中的記錄相互關聯</span><span class="sxs-lookup"><span data-stu-id="6a36e-145">Updates and correlates records in hello non-repudiation database</span></span>
* <span data-ttu-id="6a36e-146">寫入記錄以便進行 AS2 狀態報告</span><span class="sxs-lookup"><span data-stu-id="6a36e-146">Writes records for AS2 status reporting</span></span>
* <span data-ttu-id="6a36e-147">hello 裝載內容的輸出是以 base64 編碼</span><span class="sxs-lookup"><span data-stu-id="6a36e-147">hello output payload contents are base64 encoded</span></span>
* <span data-ttu-id="6a36e-148">判斷是否 MDN 是必要項目，是否 hello MDN 應該是同步或非同步根據設定 AS2 協議中</span><span class="sxs-lookup"><span data-stu-id="6a36e-148">Determines whether an MDN is required, and whether hello MDN should be synchronous or asynchronous based on configuration in AS2 agreement</span></span>
* <span data-ttu-id="6a36e-149">產生同步或非同步 MDN (根據合約組態)</span><span class="sxs-lookup"><span data-stu-id="6a36e-149">Generates a synchronous or asynchronous MDN (based on agreement configurations)</span></span>
* <span data-ttu-id="6a36e-150">設定 hello MDN hello 相互關聯 token 和屬性</span><span class="sxs-lookup"><span data-stu-id="6a36e-150">Sets hello correlation tokens and properties on hello MDN</span></span>

## <a name="try-this-sample"></a><span data-ttu-id="6a36e-151">嘗試此範例</span><span class="sxs-lookup"><span data-stu-id="6a36e-151">Try this sample</span></span>

<span data-ttu-id="6a36e-152">tootry 部署完全正常運作的邏輯應用程式和範例 AS2 案例，請參閱 hello [AS2 邏輯應用程式範本和案例](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/)。</span><span class="sxs-lookup"><span data-stu-id="6a36e-152">tootry deploying a fully operational logic app and sample AS2 scenario, see hello [AS2 logic app template and scenario](https://azure.microsoft.com/documentation/templates/201-logic-app-as2-send-receive/).</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="6a36e-153">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="6a36e-153">View hello swagger</span></span>
<span data-ttu-id="6a36e-154">請參閱 hello [swagger 詳細資料](/connectors/as2/)。</span><span class="sxs-lookup"><span data-stu-id="6a36e-154">See hello [swagger details](/connectors/as2/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6a36e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a36e-155">Next steps</span></span>
[<span data-ttu-id="6a36e-156">深入了解 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="6a36e-156">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md) 

