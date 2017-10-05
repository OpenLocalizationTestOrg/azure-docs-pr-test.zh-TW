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
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="a349d-103">Logic Apps B2B 錯誤與解決方案清單</span><span class="sxs-lookup"><span data-stu-id="a349d-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="a349d-104">本文協助您針對可能發生在 Logic Apps B2B 案例中的錯誤進行疑難排解，並提出修正這些錯誤的適當動作。</span><span class="sxs-lookup"><span data-stu-id="a349d-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="a349d-105">合約解析</span><span class="sxs-lookup"><span data-stu-id="a349d-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="a349d-106">*找不到合約</span><span class="sxs-lookup"><span data-stu-id="a349d-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="a349d-107">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-107">Error description</span></span> | <span data-ttu-id="a349d-108">找不到具有合約解析參數的合約</span><span class="sxs-lookup"><span data-stu-id="a349d-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="a349d-109">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-109">User action</span></span> | <span data-ttu-id="a349d-110">合約應新增至具議定的商務識別之整合帳戶。</span><span class="sxs-lookup"><span data-stu-id="a349d-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="a349d-111">商務識別應與輸入訊息識別碼相符</span><span class="sxs-lookup"><span data-stu-id="a349d-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="a349d-112">* 找不到具有識別身分的合約</span><span class="sxs-lookup"><span data-stu-id="a349d-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a349d-113">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-113">Error description</span></span> | <span data-ttu-id="a349d-114">找不到具有識別身分的合約：'AS2Identity'::'Partner1' 和 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="a349d-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="a349d-115">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-115">User action</span></span> | <span data-ttu-id="a349d-116">為合約設定的無效 AS2-From 或 AS2-To。</span><span class="sxs-lookup"><span data-stu-id="a349d-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="a349d-117">以合約設定更正 AS2 訊息 AS2-From 或 AS2-To 標題或合約，以符合 AS2 訊息標題中的 AS2 識別碼</span><span class="sxs-lookup"><span data-stu-id="a349d-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="a349d-118">AS2</span><span class="sxs-lookup"><span data-stu-id="a349d-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="a349d-119">* 遺漏 AS2 訊息標題</span><span class="sxs-lookup"><span data-stu-id="a349d-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="a349d-120">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-120">Error description</span></span>| <span data-ttu-id="a349d-121">不正確的 AS2 標題。</span><span class="sxs-lookup"><span data-stu-id="a349d-121">Invalid AS2 headers.</span></span> <span data-ttu-id="a349d-122">'AS2-To' 或 'AS2-From' 其中一個標題為空白</span><span class="sxs-lookup"><span data-stu-id="a349d-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="a349d-123">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-123">User action</span></span> | <span data-ttu-id="a349d-124">收到的 AS2 訊息未包含 AS2-From 或 AS2-To 或兩個標題皆未包含。</span><span class="sxs-lookup"><span data-stu-id="a349d-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="a349d-125">檢查 AS2 訊息 AS2-From 和 AS2-To 標題，並根據合約設定進行更正</span><span class="sxs-lookup"><span data-stu-id="a349d-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="a349d-126">* 遺漏 AS2 訊息本文和標題</span><span class="sxs-lookup"><span data-stu-id="a349d-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="a349d-127">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-127">Error description</span></span>| <span data-ttu-id="a349d-128">要求內容為 Null 或空白</span><span class="sxs-lookup"><span data-stu-id="a349d-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="a349d-129">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-129">User action</span></span> | <span data-ttu-id="a349d-130">收到未包含訊息本文的 AS2 訊息</span><span class="sxs-lookup"><span data-stu-id="a349d-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="a349d-131">* AS2 訊息解密失敗</span><span class="sxs-lookup"><span data-stu-id="a349d-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a349d-132">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-132">Error description</span></span> |  <span data-ttu-id="a349d-133">[已處理/錯誤：解密失敗]</span><span class="sxs-lookup"><span data-stu-id="a349d-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="a349d-134">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-134">User action</span></span> | <span data-ttu-id="a349d-135">傳送給夥伴前將 @base64ToBinary 新增至 AS2Message</span><span class="sxs-lookup"><span data-stu-id="a349d-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="a349d-136">* MDN 解密失敗</span><span class="sxs-lookup"><span data-stu-id="a349d-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a349d-137">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-137">Error description</span></span> |  <span data-ttu-id="a349d-138">[已處理/錯誤：解密失敗]</span><span class="sxs-lookup"><span data-stu-id="a349d-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="a349d-139">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-139">User action</span></span> | <span data-ttu-id="a349d-140">傳送給夥伴前將 @base64ToBinary 新增至 MDN</span><span class="sxs-lookup"><span data-stu-id="a349d-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="a349d-141">* 遺漏簽署憑證</span><span class="sxs-lookup"><span data-stu-id="a349d-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="a349d-142">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-142">Error description</span></span>| <span data-ttu-id="a349d-143">尚未設定 AS2 合作對象的簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="a349d-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="a349d-144">AS2-From：partner1 AS2-To：partner2</span><span class="sxs-lookup"><span data-stu-id="a349d-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="a349d-145">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-145">User action</span></span> | <span data-ttu-id="a349d-146">以正確的簽章憑證設定 AS2 合約設定</span><span class="sxs-lookup"><span data-stu-id="a349d-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="a349d-147">X12 和 EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a349d-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="a349d-148">* 發現前置或尾端空格</span><span class="sxs-lookup"><span data-stu-id="a349d-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="a349d-149">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-149">Error description</span></span> | <span data-ttu-id="a349d-150">剖析期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a349d-150">Error encountered during parsing.</span></span> <span data-ttu-id="a349d-151">包含在識別碼 '987654' 的交換 (沒有群組) 中識別碼為 '123456' 的 Edifact 交易集 (其傳送者識別碼為 'Partner1'，接收者識別碼為 'Partner2') 因為下列錯誤而暫止：發現前置尾端分隔符號</span><span class="sxs-lookup"><span data-stu-id="a349d-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="a349d-152">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-152">User action</span></span> | <span data-ttu-id="a349d-153">要設定的合約設定，以允許前置和尾端空格。</span><span class="sxs-lookup"><span data-stu-id="a349d-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="a349d-154">編輯合約設定，以允許前置和尾端空格</span><span class="sxs-lookup"><span data-stu-id="a349d-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![允許空格](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="a349d-156">* 合約中已啟用重複檢查</span><span class="sxs-lookup"><span data-stu-id="a349d-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a349d-157">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-157">Error description</span></span> | <span data-ttu-id="a349d-158">重複控制編號</span><span class="sxs-lookup"><span data-stu-id="a349d-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="a349d-159">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-159">User action</span></span> | <span data-ttu-id="a349d-160">此錯誤表示收到的訊息具有重複控制編號。</span><span class="sxs-lookup"><span data-stu-id="a349d-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="a349d-161">更正控制編號並重新傳送訊息</span><span class="sxs-lookup"><span data-stu-id="a349d-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="a349d-162">* 合約中遺漏結構描述</span><span class="sxs-lookup"><span data-stu-id="a349d-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a349d-163">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-163">Error description</span></span> | <span data-ttu-id="a349d-164">剖析期間發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="a349d-164">Error encountered during parsing.</span></span> <span data-ttu-id="a349d-165">包含在識別碼 '000056422' 的交換中識別碼 '56422' 的功能群組內識別碼為 '564220001' 的 X12 交易集 (其傳送者識別碼為 '12345678       '，接收者識別碼為 '87654321       ') 因為下列錯誤而暫止「訊息具有不明的文件型別，且未解析合約中設定的任何現有結構描述」</span><span class="sxs-lookup"><span data-stu-id="a349d-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="a349d-166">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-166">User action</span></span> | <span data-ttu-id="a349d-167">在合約設定中設定結構描述</span><span class="sxs-lookup"><span data-stu-id="a349d-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="a349d-168">* 合約中不正確的結構描述</span><span class="sxs-lookup"><span data-stu-id="a349d-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="a349d-169">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-169">Error description</span></span> | <span data-ttu-id="a349d-170">訊息具有不明的文件型別，且未解析合約中設定的任何現有結構描述。</span><span class="sxs-lookup"><span data-stu-id="a349d-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="a349d-171">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-171">User action</span></span> | <span data-ttu-id="a349d-172">在合約設定中設定正確的結構描述</span><span class="sxs-lookup"><span data-stu-id="a349d-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="a349d-173">一般檔案</span><span class="sxs-lookup"><span data-stu-id="a349d-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="a349d-174">* 輸入訊息沒有本文</span><span class="sxs-lookup"><span data-stu-id="a349d-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="a349d-175">錯誤說明</span><span class="sxs-lookup"><span data-stu-id="a349d-175">Error description</span></span> | <span data-ttu-id="a349d-176">InvalidTemplate。</span><span class="sxs-lookup"><span data-stu-id="a349d-176">InvalidTemplate.</span></span> <span data-ttu-id="a349d-177">無法在行 '1' 與欄 '1902' 的動作 'Flat_File_Decoding' 輸入中處理範本語言運算式：'必要屬性「內容」需有值但收到 null。</span><span class="sxs-lookup"><span data-stu-id="a349d-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="a349d-178">路徑 ''.'。</span><span class="sxs-lookup"><span data-stu-id="a349d-178">Path ''.'.</span></span> |
| <span data-ttu-id="a349d-179">使用者動作</span><span class="sxs-lookup"><span data-stu-id="a349d-179">User action</span></span> | <span data-ttu-id="a349d-180">此錯誤表示輸入訊息未包含本文</span><span class="sxs-lookup"><span data-stu-id="a349d-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="a349d-181">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a349d-181">Learn more</span></span>
[<span data-ttu-id="a349d-182">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="a349d-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)