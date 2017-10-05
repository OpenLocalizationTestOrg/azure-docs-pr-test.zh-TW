---
title: "Logic Apps B2B EDIFACT 解碼解析 UNH2.5 - Azure Logic Apps | Microsoft Docs"
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
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="f41b3-103">如何處理具有 UNH2.5 區段的 EDIFACT 文件</span><span class="sxs-lookup"><span data-stu-id="f41b3-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="f41b3-104">EDIFACT 文件中有 UNH2.5 時，它會用於結構描述查詢。</span><span class="sxs-lookup"><span data-stu-id="f41b3-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="f41b3-105">範例︰UNH 欄位在 EDIFACT 訊息中是 **EAN008**</span><span class="sxs-lookup"><span data-stu-id="f41b3-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="f41b3-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="f41b3-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="f41b3-107">要處理訊息所需遵循的步驟</span><span class="sxs-lookup"><span data-stu-id="f41b3-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="f41b3-108">更新結構描述</span><span class="sxs-lookup"><span data-stu-id="f41b3-108">Update the schema</span></span>
2. <span data-ttu-id="f41b3-109">檢查合約設定</span><span class="sxs-lookup"><span data-stu-id="f41b3-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="f41b3-110">更新結構描述</span><span class="sxs-lookup"><span data-stu-id="f41b3-110">Update the schema</span></span>
<span data-ttu-id="f41b3-111">若要處理訊息，您需要部署具有 UNH2.5 根節點名稱的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f41b3-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="f41b3-112">假設範例，結構描述根名稱就是 **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="f41b3-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="f41b3-113">針對每個具有不同 UNH2.5 區段的 D03B_ORDERS，您就必須部署個別的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f41b3-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="f41b3-114">將結構描述新增至 EDIFACT 合約</span><span class="sxs-lookup"><span data-stu-id="f41b3-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="f41b3-115">EDIFACT 解碼</span><span class="sxs-lookup"><span data-stu-id="f41b3-115">EDIFACT Decode</span></span>
<span data-ttu-id="f41b3-116">若要將內送郵件解碼，請設定 EDIFACT 合約接收設定中的結構描述</span><span class="sxs-lookup"><span data-stu-id="f41b3-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="f41b3-117">將結構描述新增至整合帳戶</span><span class="sxs-lookup"><span data-stu-id="f41b3-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="f41b3-118">設定 EDIFACT 合約接收設定中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f41b3-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="f41b3-119">選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。</span><span class="sxs-lookup"><span data-stu-id="f41b3-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="f41b3-120">在接收合約中新增 UNH2.5 值 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f41b3-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="f41b3-121">EDIFACT 編碼</span><span class="sxs-lookup"><span data-stu-id="f41b3-121">EDIFACT Encode</span></span>
<span data-ttu-id="f41b3-122">若要將內送郵件編碼，請設定 EDIFACT 合約傳送設定中的結構描述</span><span class="sxs-lookup"><span data-stu-id="f41b3-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="f41b3-123">將結構描述新增至整合帳戶</span><span class="sxs-lookup"><span data-stu-id="f41b3-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="f41b3-124">設定 EDIFACT 合約傳送設定中的結構描述。</span><span class="sxs-lookup"><span data-stu-id="f41b3-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="f41b3-125">選取 EDIFACT 合約，然後按一下 [編輯為 JSON]。</span><span class="sxs-lookup"><span data-stu-id="f41b3-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="f41b3-126">在傳送合約中新增 UNH2.5 值 **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="f41b3-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f41b3-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f41b3-127">Next Steps</span></span>
* [<span data-ttu-id="f41b3-128">深入了解整合帳戶合約</span><span class="sxs-lookup"><span data-stu-id="f41b3-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "深入了解企業整合合約")  