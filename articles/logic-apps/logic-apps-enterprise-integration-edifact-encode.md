---
title: "aaaEncode EDIFACT 訊息-Azure 邏輯應用程式 |Microsoft 文件"
description: "驗證 EDI 並產生 Azure 邏輯應用程式與 EDIFACT 訊息編碼器 hello 企業版整合套件中的 XML"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2cc71-103">Azure 邏輯應用程式的 EDIFACT 訊息編碼以 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="2cc71-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2cc71-104">與 hello 編碼 EDIFACT 訊息連接器，您可以驗證 EDI 和夥伴特定的屬性，產生 XML 文件的每個交易集，並要求技術通知，功能通知，或兩者。</span><span class="sxs-lookup"><span data-stu-id="2cc71-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="2cc71-105">toouse 此連接器，您必須加入現有的觸發程序邏輯應用程式中的 hello 連接器 tooan。</span><span class="sxs-lookup"><span data-stu-id="2cc71-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2cc71-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="2cc71-106">Before you start</span></span>

<span data-ttu-id="2cc71-107">以下是您所需要的 hello 項目：</span><span class="sxs-lookup"><span data-stu-id="2cc71-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2cc71-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="2cc71-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2cc71-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="2cc71-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2cc71-110">您必須為整合帳戶 toouse hello 編碼 EDIFACT 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="2cc71-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="2cc71-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="2cc71-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2cc71-112">已經在整合帳戶中定義的 [EDIFACT 合約](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="2cc71-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="2cc71-113">編碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="2cc71-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="2cc71-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="2cc71-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2cc71-115">沒有觸發程序，hello 編碼 EDIFACT 訊息連接器，所以您必須新增啟動邏輯應用程式，像是要求觸發程序的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="2cc71-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2cc71-116">在 hello 邏輯應用程式的設計工具，加入觸發程序，然後再加入動作 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="2cc71-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2cc71-117">在 hello 搜尋方塊中輸入"EDIFACT"做為您的篩選器。</span><span class="sxs-lookup"><span data-stu-id="2cc71-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="2cc71-118">選取  **EDIFACT 訊息編碼協議名稱**或**識別編碼 tooEDIFACT 訊息**。</span><span class="sxs-lookup"><span data-stu-id="2cc71-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![搜尋 EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="2cc71-120">如果您先前未建立任何連線 tooyour 整合帳戶，則會提示您 toocreate 現在該連接。</span><span class="sxs-lookup"><span data-stu-id="2cc71-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2cc71-121">命名您的連線，並選取您想 tooconnect hello 整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="2cc71-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![建立整合帳戶連線](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="2cc71-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="2cc71-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2cc71-124">屬性</span><span class="sxs-lookup"><span data-stu-id="2cc71-124">Property</span></span> | <span data-ttu-id="2cc71-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="2cc71-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2cc71-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="2cc71-126">Connection Name *</span></span> |<span data-ttu-id="2cc71-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc71-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2cc71-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="2cc71-128">Integration Account *</span></span> |<span data-ttu-id="2cc71-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc71-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2cc71-130">請確定應用程式整合帳戶和邏輯位於 hello 相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="2cc71-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2cc71-131">當您完成時，您的連線詳細資料看起來應該類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="2cc71-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2cc71-132">選擇 建立您的連線，toofinish**建立**。</span><span class="sxs-lookup"><span data-stu-id="2cc71-132">toofinish creating your connection, choose **Create**.</span></span>

    ![整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="2cc71-134">現在已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="2cc71-134">Your connection is now created.</span></span>

    ![整合帳戶連線已建立](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="2cc71-136">依協議名稱將 EDIFACT 訊息編碼</span><span class="sxs-lookup"><span data-stu-id="2cc71-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="2cc71-137">如果您選擇 tooencode EDIFACT 訊息的協議名稱，開啟 hello**名稱的 EDIFACT 協議**清單中，輸入或選取您 EDIFACT 協議的名稱。</span><span class="sxs-lookup"><span data-stu-id="2cc71-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="2cc71-138">輸入 hello XML 訊息 tooencode。</span><span class="sxs-lookup"><span data-stu-id="2cc71-138">Enter hello XML message tooencode.</span></span>

![輸入 EDIFACT 協議名稱和 XML 訊息 tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="2cc71-140">由身分識別編碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="2cc71-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="2cc71-141">如果您選擇 tooencode EDIFACT 訊息的身分識別，請輸入 hello 寄件者識別碼、 傳送者辨識符號、 接收者識別碼和接收者辨識符號為您的 EDIFACT 協議中設定。</span><span class="sxs-lookup"><span data-stu-id="2cc71-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="2cc71-142">選取 hello XML 訊息 tooencode。</span><span class="sxs-lookup"><span data-stu-id="2cc71-142">Select hello XML message tooencode.</span></span>

![提供身分識別傳送者和接收者，選取 XML 訊息 tooencode](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="2cc71-144">EDIFACT 編碼詳細資料</span><span class="sxs-lookup"><span data-stu-id="2cc71-144">EDIFACT Encode details</span></span>

<span data-ttu-id="2cc71-145">hello 編碼 EDIFACT 連接器會執行這些工作：</span><span class="sxs-lookup"><span data-stu-id="2cc71-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="2cc71-146">比對 hello 傳送者辨識符號和識別項和接收者辨識符號和識別項，以解析 hello 協議</span><span class="sxs-lookup"><span data-stu-id="2cc71-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="2cc71-147">序列化 hello EDI 交換，將 XML 編碼訊息轉換成 hello 交換中的 EDI 交易集。</span><span class="sxs-lookup"><span data-stu-id="2cc71-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="2cc71-148">套用交易集標頭和結尾區段</span><span class="sxs-lookup"><span data-stu-id="2cc71-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="2cc71-149">產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號</span><span class="sxs-lookup"><span data-stu-id="2cc71-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="2cc71-150">取代 hello 裝載資料中的分隔符號</span><span class="sxs-lookup"><span data-stu-id="2cc71-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="2cc71-151">驗證 EDI 和夥伴特定屬性</span><span class="sxs-lookup"><span data-stu-id="2cc71-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="2cc71-152">針對 hello 訊息結構描述的 hello 交易集資料元素的結構描述驗證。</span><span class="sxs-lookup"><span data-stu-id="2cc71-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="2cc71-153">對交易集資料元素執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="2cc71-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="2cc71-154">對交易集資料元素執行擴充驗證</span><span class="sxs-lookup"><span data-stu-id="2cc71-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="2cc71-155">產生每個交易集的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="2cc71-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="2cc71-156">要求技術和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="2cc71-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="2cc71-157">做為技術通知，hello CONTRL 訊息會指示接收交換。</span><span class="sxs-lookup"><span data-stu-id="2cc71-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="2cc71-158">做為功能通知，hello CONTRL 訊息會指示接受或拒絕的錯誤或不支援的功能清單 hello 收到交換、 群組或訊息，</span><span class="sxs-lookup"><span data-stu-id="2cc71-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="2cc71-159">檢視 Swagger 檔案</span><span class="sxs-lookup"><span data-stu-id="2cc71-159">View Swagger file</span></span>
<span data-ttu-id="2cc71-160">tooview hello Swagger 詳細資料，hello EDIFACT 連接器，請參閱[EDIFACT](/connectors/edifact/)。</span><span class="sxs-lookup"><span data-stu-id="2cc71-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2cc71-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2cc71-161">Next steps</span></span>
[<span data-ttu-id="2cc71-162">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="2cc71-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack") 

