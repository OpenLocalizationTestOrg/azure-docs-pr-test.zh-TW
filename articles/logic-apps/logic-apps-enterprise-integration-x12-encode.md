---
title: "aaaEncode X12 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 和轉換 XML 編碼 Azure 邏輯應用程式訊息編碼器 hello 企業版整合套件中的 x12 訊息"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="70c8e-103">將 X12 編碼訊息 Azure 邏輯應用程式以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="70c8e-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="70c8e-104">與 hello X12 編碼訊息連接器，您可以驗證 EDI 和夥伴特定的屬性，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集和要求技術通知，功能通知，或兩者。</span><span class="sxs-lookup"><span data-stu-id="70c8e-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="70c8e-105">toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。</span><span class="sxs-lookup"><span data-stu-id="70c8e-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="70c8e-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="70c8e-106">Before you start</span></span>

<span data-ttu-id="70c8e-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="70c8e-107">Here's hello items you need:</span></span>

* <span data-ttu-id="70c8e-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="70c8e-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="70c8e-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="70c8e-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="70c8e-110">您必須為整合帳戶 toouse hello X12 編碼訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="70c8e-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="70c8e-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="70c8e-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="70c8e-112">已經在整合帳戶中定義的 [X12 合約](logic-apps-enterprise-integration-x12.md)</span><span class="sxs-lookup"><span data-stu-id="70c8e-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="70c8e-113">編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="70c8e-113">Encode X12 messages</span></span>

1. <span data-ttu-id="70c8e-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="70c8e-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="70c8e-115">沒有觸發程序，hello X12 編碼訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="70c8e-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="70c8e-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="70c8e-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="70c8e-117">Hello 搜尋方塊中，輸入您的篩選器"x12"。</span><span class="sxs-lookup"><span data-stu-id="70c8e-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="70c8e-118">選取  **X12-將 tooX12 訊息編碼協議名稱**或**X12-將編碼識別 tooX12 訊息**。</span><span class="sxs-lookup"><span data-stu-id="70c8e-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![搜尋 "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="70c8e-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="70c8e-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="70c8e-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="70c8e-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![整合帳戶連線](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="70c8e-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="70c8e-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="70c8e-124">屬性</span><span class="sxs-lookup"><span data-stu-id="70c8e-124">Property</span></span> | <span data-ttu-id="70c8e-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="70c8e-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="70c8e-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="70c8e-126">Connection Name *</span></span> |<span data-ttu-id="70c8e-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="70c8e-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="70c8e-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="70c8e-128">Integration Account *</span></span> |<span data-ttu-id="70c8e-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="70c8e-129">Enter a name for your integration account.</span></span> <span data-ttu-id="70c8e-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="70c8e-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="70c8e-131">當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="70c8e-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="70c8e-132">選擇 建立您的連線，toofinish**建立**。</span><span class="sxs-lookup"><span data-stu-id="70c8e-132">toofinish creating your connection, choose **Create**.</span></span>

    ![整合帳戶連線已建立](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="70c8e-134">現在已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="70c8e-134">Your connection is now created.</span></span>

    ![整合帳戶連線詳細資料](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="70c8e-136">由協議名稱編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="70c8e-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="70c8e-137">如果您選擇 tooencode X12 訊息的協議名稱，開啟 hello**名稱的 X12 協議**清單中，輸入或選取您現有的 X12 協議。</span><span class="sxs-lookup"><span data-stu-id="70c8e-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="70c8e-138">輸入 hello XML 訊息 tooencode。</span><span class="sxs-lookup"><span data-stu-id="70c8e-138">Enter hello XML message tooencode.</span></span>

![輸入 X12 協議名稱和 XML 訊息 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="70c8e-140">由身分識別編碼 X12 訊息</span><span class="sxs-lookup"><span data-stu-id="70c8e-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="70c8e-141">如果您選擇 tooencode X12 訊息的身分識別，輸入 hello 寄件者識別碼、 傳送者辨識符號、 接收者識別碼和接收者辨識符號設定在您的 X12 協議。</span><span class="sxs-lookup"><span data-stu-id="70c8e-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="70c8e-142">選取 hello XML 訊息 tooencode。</span><span class="sxs-lookup"><span data-stu-id="70c8e-142">Select hello XML message tooencode.</span></span>
   
![提供身分識別傳送者和接收者，選取 XML 訊息 tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="70c8e-144">X12 編碼詳細資料</span><span class="sxs-lookup"><span data-stu-id="70c8e-144">X12 Encode details</span></span>

<span data-ttu-id="70c8e-145">hello X12 編碼連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="70c8e-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="70c8e-146">藉由比對傳送者和接收者內容屬性進行合約解析。</span><span class="sxs-lookup"><span data-stu-id="70c8e-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="70c8e-147">序列化 hello EDI 交換，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集。</span><span class="sxs-lookup"><span data-stu-id="70c8e-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="70c8e-148">套用交易集標頭和結尾區段</span><span class="sxs-lookup"><span data-stu-id="70c8e-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="70c8e-149">產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號</span><span class="sxs-lookup"><span data-stu-id="70c8e-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="70c8e-150">取代 hello 裝載資料中的分隔符號</span><span class="sxs-lookup"><span data-stu-id="70c8e-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="70c8e-151">驗證 EDI 和夥伴特定屬性</span><span class="sxs-lookup"><span data-stu-id="70c8e-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="70c8e-152">Hello 交易集資料元素與 hello 訊息結構描述的結構描述驗證</span><span class="sxs-lookup"><span data-stu-id="70c8e-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="70c8e-153">對交易集資料元素執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="70c8e-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="70c8e-154">對交易集資料元素執行擴充驗證</span><span class="sxs-lookup"><span data-stu-id="70c8e-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="70c8e-155">要求技術和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="70c8e-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="70c8e-156">標頭驗證後會產生技術確認。</span><span class="sxs-lookup"><span data-stu-id="70c8e-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="70c8e-157">hello 技術通知會報告對交換標頭和結尾 hello 位址接收者 hello 處理 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="70c8e-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="70c8e-158">內文驗證後會產生功能確認。</span><span class="sxs-lookup"><span data-stu-id="70c8e-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="70c8e-159">hello 功能通知會報告每個處理 hello 收到文件時所遇到的錯誤</span><span class="sxs-lookup"><span data-stu-id="70c8e-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="70c8e-160">檢視 hello swagger</span><span class="sxs-lookup"><span data-stu-id="70c8e-160">View hello swagger</span></span>
<span data-ttu-id="70c8e-161">請參閱 hello [swagger 詳細資料](/connectors/x12/)。</span><span class="sxs-lookup"><span data-stu-id="70c8e-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="70c8e-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="70c8e-162">Next steps</span></span>
[<span data-ttu-id="70c8e-163">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="70c8e-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

