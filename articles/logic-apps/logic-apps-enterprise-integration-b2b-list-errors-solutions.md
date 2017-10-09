---
title: "Logic Apps B2B 錯誤與解決方案清單：Azure App Service | Microsoft Docs"
description: "Logic Apps B2B 錯誤與解決方案清單"
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
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="7f358-103">Logic Apps B2B 錯誤與解決方案清單</span><span class="sxs-lookup"><span data-stu-id="7f358-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="7f358-104">本文協助您針對可能發生在 Logic Apps B2B 案例中的錯誤進行疑難排解，並提出修正這些錯誤的適當動作。</span><span class="sxs-lookup"><span data-stu-id="7f358-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="7f358-105">合約解析</span><span class="sxs-lookup"><span data-stu-id="7f358-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="7f358-106">*找不到合約</span><span class="sxs-lookup"><span data-stu-id="7f358-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="7f358-107">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-107">Error description</span></span> | <span data-ttu-id="7f358-108">找不到具有合約解析參數的合約</span><span class="sxs-lookup"><span data-stu-id="7f358-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="7f358-109">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-109">User action</span></span> | <span data-ttu-id="7f358-110">hello 協議應加入 toohello 整合帳戶同意的企業身分識別。</span><span class="sxs-lookup"><span data-stu-id="7f358-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="7f358-111">hello 的商務識別應該符合 toohello 輸入的訊息識別碼</span><span class="sxs-lookup"><span data-stu-id="7f358-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="7f358-112">* 找不到具有識別身分的合約</span><span class="sxs-lookup"><span data-stu-id="7f358-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7f358-113">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-113">Error description</span></span> | <span data-ttu-id="7f358-114">找不到具有識別身分的合約：'AS2Identity'::'Partner1' 和 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="7f358-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="7f358-115">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-115">User action</span></span> | <span data-ttu-id="7f358-116">無效的 AS2-從或針對協議的 AS2 tooconfigured。</span><span class="sxs-lookup"><span data-stu-id="7f358-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="7f358-117">正確的 AS2 訊息 AS2-從或 AS2 tooheaders 或合約 toomatch AS2 id，在 AS2 訊息標頭與協議設定</span><span class="sxs-lookup"><span data-stu-id="7f358-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="7f358-118">AS2</span><span class="sxs-lookup"><span data-stu-id="7f358-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="7f358-119">* 遺漏 AS2 訊息標題</span><span class="sxs-lookup"><span data-stu-id="7f358-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="7f358-120">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-120">Error description</span></span>| <span data-ttu-id="7f358-121">不正確的 AS2 標題。</span><span class="sxs-lookup"><span data-stu-id="7f358-121">Invalid AS2 headers.</span></span> <span data-ttu-id="7f358-122">'AS2-To' 或 'AS2-From' 其中一個標題為空白</span><span class="sxs-lookup"><span data-stu-id="7f358-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="7f358-123">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-123">User action</span></span> | <span data-ttu-id="7f358-124">收到的 AS2 訊息不包含 hello AS2-從或 AS2 tooor 這兩個標頭。</span><span class="sxs-lookup"><span data-stu-id="7f358-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="7f358-125">檢查 AS2 訊息 AS2-從和 AS2 tooheaders 並更正根據協議設定</span><span class="sxs-lookup"><span data-stu-id="7f358-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="7f358-126">* 遺漏 AS2 訊息本文和標題</span><span class="sxs-lookup"><span data-stu-id="7f358-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="7f358-127">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-127">Error description</span></span>| <span data-ttu-id="7f358-128">hello 要求內容為 null 或空白</span><span class="sxs-lookup"><span data-stu-id="7f358-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="7f358-129">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-129">User action</span></span> | <span data-ttu-id="7f358-130">收到的 AS2 訊息不包含 hello 訊息內文</span><span class="sxs-lookup"><span data-stu-id="7f358-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="7f358-131">* AS2 訊息解密失敗</span><span class="sxs-lookup"><span data-stu-id="7f358-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7f358-132">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-132">Error description</span></span> |  <span data-ttu-id="7f358-133">[已處理/錯誤：解密失敗]</span><span class="sxs-lookup"><span data-stu-id="7f358-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="7f358-134">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-134">User action</span></span> | <span data-ttu-id="7f358-135">新增@base64ToBinarytooAS2Message 傳送 toopartner 之前</span><span class="sxs-lookup"><span data-stu-id="7f358-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="7f358-136">* MDN 解密失敗</span><span class="sxs-lookup"><span data-stu-id="7f358-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7f358-137">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-137">Error description</span></span> |  <span data-ttu-id="7f358-138">[已處理/錯誤：解密失敗]</span><span class="sxs-lookup"><span data-stu-id="7f358-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="7f358-139">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-139">User action</span></span> | <span data-ttu-id="7f358-140">新增@base64ToBinarytooMDN 傳送 toopartner 之前</span><span class="sxs-lookup"><span data-stu-id="7f358-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="7f358-141">* 遺漏簽署憑證</span><span class="sxs-lookup"><span data-stu-id="7f358-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="7f358-142">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-142">Error description</span></span>| <span data-ttu-id="7f358-143">hello 簽署憑證尚未設定 AS2 合作對象。</span><span class="sxs-lookup"><span data-stu-id="7f358-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="7f358-144">AS2-From：partner1 AS2-To：partner2</span><span class="sxs-lookup"><span data-stu-id="7f358-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="7f358-145">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-145">User action</span></span> | <span data-ttu-id="7f358-146">以正確的簽章憑證設定 AS2 合約設定</span><span class="sxs-lookup"><span data-stu-id="7f358-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="7f358-147">X12 和 EDIFACT</span><span class="sxs-lookup"><span data-stu-id="7f358-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="7f358-148">* 發現前置或尾端空格</span><span class="sxs-lookup"><span data-stu-id="7f358-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="7f358-149">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-149">Error description</span></span> | <span data-ttu-id="7f358-150">剖析期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7f358-150">Error encountered during parsing.</span></span> <span data-ttu-id="7f358-151">hello Edifact 交易集與 '（不含群組） 的交換中識別碼為 '987654 包含' id' 123456，為傳送者識別碼 'Partner1'、 接收者識別碼 '夥伴 2' 處於暫停狀態，錯誤如下： 找到前置尾端分隔符號</span><span class="sxs-lookup"><span data-stu-id="7f358-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="7f358-152">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-152">User action</span></span> | <span data-ttu-id="7f358-153">hello 協議設定 toobe 設定 tooallow 開頭與尾端空白字元。</span><span class="sxs-lookup"><span data-stu-id="7f358-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="7f358-154">編輯協議設定 tooallow 開頭與尾端空白字元</span><span class="sxs-lookup"><span data-stu-id="7f358-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![允許空格](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="7f358-156">* 重複檢查已啟用在 hello 協議</span><span class="sxs-lookup"><span data-stu-id="7f358-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7f358-157">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-157">Error description</span></span> | <span data-ttu-id="7f358-158">重複控制編號</span><span class="sxs-lookup"><span data-stu-id="7f358-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="7f358-159">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-159">User action</span></span> | <span data-ttu-id="7f358-160">此錯誤表示收到 hello 訊息有重複的控制編號。</span><span class="sxs-lookup"><span data-stu-id="7f358-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="7f358-161">更正 hello 控制編號，然後再重新傳送 hello 訊息</span><span class="sxs-lookup"><span data-stu-id="7f358-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="7f358-162">* 遺漏 hello 協議中的結構描述</span><span class="sxs-lookup"><span data-stu-id="7f358-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7f358-163">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-163">Error description</span></span> | <span data-ttu-id="7f358-164">剖析期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="7f358-164">Error encountered during parsing.</span></span> <span data-ttu-id="7f358-165">識別碼為 '564220001' 包含在功能群組識別碼為 '56422'，在交換傳送者識別碼為' 12345678 id '000056422'，' 接收者識別碼 ' 87654321' hello X12 交易集處於暫停狀態，錯誤如下 「 hello 訊息有不明的文件 type 和未解析 tooany hello hello 協議中設定的現有結構描述的 「</span><span class="sxs-lookup"><span data-stu-id="7f358-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="7f358-166">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-166">User action</span></span> | <span data-ttu-id="7f358-167">在 hello 協議設定中設定結構描述</span><span class="sxs-lookup"><span data-stu-id="7f358-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="7f358-168">* 不正確的結構描述在 hello 協議</span><span class="sxs-lookup"><span data-stu-id="7f358-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="7f358-169">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-169">Error description</span></span> | <span data-ttu-id="7f358-170">hello 訊息具有不明的文件型別，而且未解析 tooany hello hello 協議中設定的現有結構描述。</span><span class="sxs-lookup"><span data-stu-id="7f358-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="7f358-171">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-171">User action</span></span> | <span data-ttu-id="7f358-172">在 hello 協議設定中設定正確的結構描述</span><span class="sxs-lookup"><span data-stu-id="7f358-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="7f358-173">一般檔案</span><span class="sxs-lookup"><span data-stu-id="7f358-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="7f358-174">* 輸入訊息沒有本文</span><span class="sxs-lookup"><span data-stu-id="7f358-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="7f358-175">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="7f358-175">Error description</span></span> | <span data-ttu-id="7f358-176">InvalidTemplate。</span><span class="sxs-lookup"><span data-stu-id="7f358-176">InvalidTemplate.</span></span> <span data-ttu-id="7f358-177">在行 '1' 與欄 '1902' 動作 'Flat_File_Decoding' 輸入中的無法 tooprocess 範本語言運算式: ' 需要 'content' 屬性必須要有值，但卻收到 null。</span><span class="sxs-lookup"><span data-stu-id="7f358-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="7f358-178">路徑 ''.'。</span><span class="sxs-lookup"><span data-stu-id="7f358-178">Path ''.'.</span></span> |
| <span data-ttu-id="7f358-179">使用者動作</span><span class="sxs-lookup"><span data-stu-id="7f358-179">User action</span></span> | <span data-ttu-id="7f358-180">此錯誤表示 hello 輸入的訊息不包含主體</span><span class="sxs-lookup"><span data-stu-id="7f358-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="7f358-181">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7f358-181">Learn more</span></span>
[<span data-ttu-id="7f358-182">深入了解 hello 企業版整合套件</span><span class="sxs-lookup"><span data-stu-id="7f358-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
