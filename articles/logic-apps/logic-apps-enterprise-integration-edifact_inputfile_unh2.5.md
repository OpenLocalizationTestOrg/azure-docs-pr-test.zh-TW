---
title: "應用程式 B2B edifact 解碼 aaaLogic 解析的 UNH2.5-Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure Logic Apps B2B EDIFACT 解碼解析 UNH2.5"
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
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="c4a1f-103">如何 toohandle EDIFACT 文件有 UNH2.5 區段</span><span class="sxs-lookup"><span data-stu-id="c4a1f-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="c4a1f-104">Hello EDIFACT 文件中有 UNH2.5 時，它用於結構描述查閱。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="c4a1f-105">範例： hello UNH 欄位是**EAN008** hello EDIFACT 訊息中</span><span class="sxs-lookup"><span data-stu-id="c4a1f-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="c4a1f-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="c4a1f-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="c4a1f-107">步驟 toofollow toohandle hello 訊息</span><span class="sxs-lookup"><span data-stu-id="c4a1f-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="c4a1f-108">更新 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="c4a1f-108">Update hello schema</span></span>
2. <span data-ttu-id="c4a1f-109">請檢查 hello 協議設定</span><span class="sxs-lookup"><span data-stu-id="c4a1f-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="c4a1f-110">更新 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="c4a1f-110">Update hello schema</span></span>
<span data-ttu-id="c4a1f-111">tooprocess hello 訊息，您需要 toodeploy 具有 hello UNH2.5 根節點名稱的結構描述。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="c4a1f-112">Hello 結構描述根名稱指定的範例，就是**EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="c4a1f-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="c4a1f-113">針對每個 D03B_ORDERS 以不同的 UNH2.5 區段中，您就必須 toodeploy 個別結構描述。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="c4a1f-114">新增結構描述 toohello EDIFACT 協議</span><span class="sxs-lookup"><span data-stu-id="c4a1f-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="c4a1f-115">EDIFACT 解碼</span><span class="sxs-lookup"><span data-stu-id="c4a1f-115">EDIFACT Decode</span></span>
<span data-ttu-id="c4a1f-116">tooDecode hello 內送訊息，設定 hello 結構描述中 hello EDIFACT 協議接收設定</span><span class="sxs-lookup"><span data-stu-id="c4a1f-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="c4a1f-117">新增 hello 結構描述 toohello 整合帳戶</span><span class="sxs-lookup"><span data-stu-id="c4a1f-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="c4a1f-118">設定 hello 結構描述中 hello EDIFACT 協議接收設定。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="c4a1f-119">選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="c4a1f-120">在 hello 接收協議中加入 UNH2.5 值**schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="c4a1f-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="c4a1f-121">EDIFACT 編碼</span><span class="sxs-lookup"><span data-stu-id="c4a1f-121">EDIFACT Encode</span></span>
<span data-ttu-id="c4a1f-122">tooEncode hello 內送訊息、 在 hello EDIFACT 協議的傳送設定中設定 hello 結構描述</span><span class="sxs-lookup"><span data-stu-id="c4a1f-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="c4a1f-123">新增 hello 結構描述 toohello 整合帳戶</span><span class="sxs-lookup"><span data-stu-id="c4a1f-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="c4a1f-124">在 hello EDIFACT 協議的傳送設定中設定 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="c4a1f-125">選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。</span><span class="sxs-lookup"><span data-stu-id="c4a1f-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="c4a1f-126">在 hello 傳送協議中加入 UNH2.5 值**schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c4a1f-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4a1f-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4a1f-127">Next Steps</span></span>
* [<span data-ttu-id="c4a1f-128">深入了解整合帳戶合約</span><span class="sxs-lookup"><span data-stu-id="c4a1f-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "深入了解企業整合合約")  