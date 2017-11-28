---
title: "aaaValidate XML-Azure 邏輯應用程式 |Microsoft 文件"
description: "Azure 邏輯應用程式和 B2B 案例的結構描述驗證 XML，利用 hello 企業版整合套件"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="34059-103">針對企業整合驗證 XML</span><span class="sxs-lookup"><span data-stu-id="34059-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="34059-104">通常在 B2B 實例中，必須先確定 hello 訊息交換所有效之後，才能開始資料處理 hello 夥伴協議中。</span><span class="sxs-lookup"><span data-stu-id="34059-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="34059-105">您可以利用 hello 企業版整合套件中的 hello 使用 hello XML 驗證連接器驗證針對預先定義的結構描述的文件。</span><span class="sxs-lookup"><span data-stu-id="34059-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="34059-106">驗證文件以 hello XML 驗證連接器</span><span class="sxs-lookup"><span data-stu-id="34059-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="34059-107">建立邏輯應用程式和[hello 應用程式 toohello 整合帳戶連結](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink 整合帳戶 tooa 邏輯應用程式了解")具有要用於驗證 XML 資料 toouse hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="34059-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="34059-108">新增**要求-當 HTTP 要求**觸發程序 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="34059-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="34059-109">tooadd hello **XML 驗證**動作中，選擇**將動作加入**。</span><span class="sxs-lookup"><span data-stu-id="34059-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="34059-110">輸入所有 hello，其中一個動作 toohello toofilter *xml* hello [搜尋] 方塊中。</span><span class="sxs-lookup"><span data-stu-id="34059-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="34059-111">選擇 [XML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="34059-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="34059-112">選取您想要 toovalidate 的 XML 內容的 toospecify hello**內容**。</span><span class="sxs-lookup"><span data-stu-id="34059-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="34059-113">選取要作為內容的 toovalidate hello hello body 標記。</span><span class="sxs-lookup"><span data-stu-id="34059-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="34059-114">toospecify hello 結構描述要用於驗證先前 hello toouse*內容*輸入中，選擇 **結構描述名稱**。</span><span class="sxs-lookup"><span data-stu-id="34059-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="34059-115">儲存您的工作 </span><span class="sxs-lookup"><span data-stu-id="34059-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="34059-116">現在您已完成設定驗證連接器。</span><span class="sxs-lookup"><span data-stu-id="34059-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="34059-117">在真實世界應用程式中，您可能想 toostore hello 驗證資料中的特定業務 (LOB) 應用程式，例如 SalesForce。</span><span class="sxs-lookup"><span data-stu-id="34059-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="34059-118">toosend hello 驗證的輸出 tooSalesforce，加入的動作。</span><span class="sxs-lookup"><span data-stu-id="34059-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="34059-119">tootest 您驗證的動作，讓要求 toohello HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="34059-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34059-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="34059-120">Next steps</span></span>
[<span data-ttu-id="34059-121">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="34059-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")   

