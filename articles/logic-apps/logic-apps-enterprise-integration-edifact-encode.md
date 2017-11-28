---
title: "將 EDIFACT 訊息編碼 - Azure Logic Apps | Microsoft Docs"
description: "在 Azure Logic Apps 的企業整合套件中使用 EDIFACT 訊息編碼器來驗證 EDI 及產生 XML"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="708ab-103">使用企業整合套件將 Azure Logic Apps 的 EDIFACT 訊息編碼</span><span class="sxs-lookup"><span data-stu-id="708ab-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="708ab-104">使用編碼 EDIFACT 訊息連接器，可以驗證 EDI 和夥伴特定屬性，產生每個交易集的 XML 文件，以及要求技術通知、功能通知或兩者。</span><span class="sxs-lookup"><span data-stu-id="708ab-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="708ab-105">若要使用此連接器，您必須將連接器新增至邏輯應用程式中的現有觸發程序。</span><span class="sxs-lookup"><span data-stu-id="708ab-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="708ab-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="708ab-106">Before you start</span></span>

<span data-ttu-id="708ab-107">以下是您所需的項目︰</span><span class="sxs-lookup"><span data-stu-id="708ab-107">Here's the items you need:</span></span>

* <span data-ttu-id="708ab-108">Azure 帳戶；您可以建立一個 [免費帳戶](https://azure.microsoft.com/free)</span><span class="sxs-lookup"><span data-stu-id="708ab-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="708ab-109">已經定義並與 Azure 訂用帳戶相關聯的[整合帳戶](logic-apps-enterprise-integration-create-integration-account.md)。</span><span class="sxs-lookup"><span data-stu-id="708ab-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="708ab-110">您必須有整合帳戶才能使用編碼 EDIFACT 訊息連接器。</span><span class="sxs-lookup"><span data-stu-id="708ab-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="708ab-111">至少已經在整合帳戶中定義兩個[夥伴](logic-apps-enterprise-integration-partners.md)</span><span class="sxs-lookup"><span data-stu-id="708ab-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="708ab-112">已經在整合帳戶中定義的 [EDIFACT 合約](logic-apps-enterprise-integration-edifact.md)</span><span class="sxs-lookup"><span data-stu-id="708ab-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="708ab-113">編碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="708ab-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="708ab-114">[建立邏輯應用程式](logic-apps-create-a-logic-app.md)。</span><span class="sxs-lookup"><span data-stu-id="708ab-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="708ab-115">編碼 EDIFACT 訊息連接器沒有觸發程序，因此您必須新增觸發程序 (例如要求觸發程序) 來啟動邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="708ab-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="708ab-116">在 Logic Apps 設計工具中，新增觸發程序，然後將動作新增至您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="708ab-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="708ab-117">在搜尋方塊中，輸入 "EDIFACT" 做為篩選條件。</span><span class="sxs-lookup"><span data-stu-id="708ab-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="708ab-118">選取 [依照合約名稱編碼為 EDIFACT 訊息] 或是 [依照身分識別編碼為 EDIFACT 訊息]。</span><span class="sxs-lookup"><span data-stu-id="708ab-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![搜尋 EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="708ab-120">如果您先前未建立與整合帳戶的任何連線，系統將會提示您立即建立該連線。</span><span class="sxs-lookup"><span data-stu-id="708ab-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="708ab-121">替連線命名，然後選取您要連線的整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="708ab-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![建立整合帳戶連線](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="708ab-123">具有星號的屬性為必要項目。</span><span class="sxs-lookup"><span data-stu-id="708ab-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="708ab-124">屬性</span><span class="sxs-lookup"><span data-stu-id="708ab-124">Property</span></span> | <span data-ttu-id="708ab-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="708ab-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="708ab-126">連線名稱 *</span><span class="sxs-lookup"><span data-stu-id="708ab-126">Connection Name *</span></span> |<span data-ttu-id="708ab-127">為連接器輸入任何名稱。</span><span class="sxs-lookup"><span data-stu-id="708ab-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="708ab-128">整合帳戶 *</span><span class="sxs-lookup"><span data-stu-id="708ab-128">Integration Account *</span></span> |<span data-ttu-id="708ab-129">輸入整合帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="708ab-129">Enter a name for your integration account.</span></span> <span data-ttu-id="708ab-130">確定您的整合帳戶和邏輯應用程式位於相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="708ab-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="708ab-131">當您完成時，連線詳細資料看起來類似此範例。</span><span class="sxs-lookup"><span data-stu-id="708ab-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="708ab-132">若要完成連線建立，請選擇 [建立]。</span><span class="sxs-lookup"><span data-stu-id="708ab-132">To finish creating your connection, choose **Create**.</span></span>

    ![整合帳戶連線詳細資料](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="708ab-134">現在已建立您的連線。</span><span class="sxs-lookup"><span data-stu-id="708ab-134">Your connection is now created.</span></span>

    ![整合帳戶連線已建立](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="708ab-136">依協議名稱將 EDIFACT 訊息編碼</span><span class="sxs-lookup"><span data-stu-id="708ab-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="708ab-137">如果您選擇依協議名稱將 EDIFACT 訊息編碼，請開啟 [EDIFACT 協議名稱] 清單，輸入或選取您的 EDIFACT 協議名稱。</span><span class="sxs-lookup"><span data-stu-id="708ab-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="708ab-138">輸入 XML 訊息進行編碼。</span><span class="sxs-lookup"><span data-stu-id="708ab-138">Enter the XML message to encode.</span></span>

![輸入 EDIFACT 協議名稱和 XML 訊息進行編碼](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="708ab-140">由身分識別編碼 EDIFACT 訊息</span><span class="sxs-lookup"><span data-stu-id="708ab-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="708ab-141">如果您選擇依照身分識別將 EDIFACT 訊息編碼，請輸入傳送者識別碼、傳送者限定詞、接收者識別碼和接收者限定詞，如 EDIFACT 合約中所設定。</span><span class="sxs-lookup"><span data-stu-id="708ab-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="708ab-142">選取要編碼的 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="708ab-142">Select the XML message to encode.</span></span>

![提供傳送者與收件者的身分識別，選取要編碼的 XML 訊息](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="708ab-144">EDIFACT 編碼詳細資料</span><span class="sxs-lookup"><span data-stu-id="708ab-144">EDIFACT Encode details</span></span>

<span data-ttu-id="708ab-145">編碼 EDIFACT 連接器會執行下列工作︰</span><span class="sxs-lookup"><span data-stu-id="708ab-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="708ab-146">比對傳送者辨識符號和識別項，以及接收者辨識符號和識別項，以解析合約</span><span class="sxs-lookup"><span data-stu-id="708ab-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="708ab-147">序列化 EDI 交換，將 XML 編碼訊息轉換為交換中的 EDI 交易集。</span><span class="sxs-lookup"><span data-stu-id="708ab-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="708ab-148">套用交易集標頭和結尾區段</span><span class="sxs-lookup"><span data-stu-id="708ab-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="708ab-149">產生交換控制編號、群組控制編號和每個傳出交換的交易集控制編號</span><span class="sxs-lookup"><span data-stu-id="708ab-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="708ab-150">取代承載資料中的分隔符號</span><span class="sxs-lookup"><span data-stu-id="708ab-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="708ab-151">驗證 EDI 和夥伴特定屬性</span><span class="sxs-lookup"><span data-stu-id="708ab-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="708ab-152">針對訊息結構描述進行交易集資料元素的結構描述驗證。</span><span class="sxs-lookup"><span data-stu-id="708ab-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="708ab-153">對交易集資料元素執行 EDI 驗證。</span><span class="sxs-lookup"><span data-stu-id="708ab-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="708ab-154">對交易集資料元素執行擴充驗證</span><span class="sxs-lookup"><span data-stu-id="708ab-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="708ab-155">產生每個交易集的 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="708ab-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="708ab-156">要求技術和/或功能確認 (若已設定)。</span><span class="sxs-lookup"><span data-stu-id="708ab-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="708ab-157">做為技術確認，CONTRL 訊息會指示交換的接收。</span><span class="sxs-lookup"><span data-stu-id="708ab-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="708ab-158">做為功能確認，CONTRL 訊息會指示接受或拒絕接收的交換、群組或訊息，並列出錯誤或不支援的功能清單</span><span class="sxs-lookup"><span data-stu-id="708ab-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="708ab-159">檢視 Swagger 檔案</span><span class="sxs-lookup"><span data-stu-id="708ab-159">View Swagger file</span></span>
<span data-ttu-id="708ab-160">若要檢視 EDIFACT 連接器的 Swagger 詳細資料，請參閱 [EDIFACT](/connectors/edifact/)。</span><span class="sxs-lookup"><span data-stu-id="708ab-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="708ab-161">後續步驟</span><span class="sxs-lookup"><span data-stu-id="708ab-161">Next steps</span></span>
[<span data-ttu-id="708ab-162">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="708ab-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "了解企業整合套件") 

