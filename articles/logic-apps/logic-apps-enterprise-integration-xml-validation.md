---
title: "驗證 XML - Azure Logic Apps | Microsoft Docs"
description: "使用企業整合套件，以 Azure Logic Apps 與 B2B 案例的結構描述來驗證 XML"
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
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="deee0-103">針對企業整合驗證 XML</span><span class="sxs-lookup"><span data-stu-id="deee0-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="deee0-104">通常在 B2B 案例中，協議中的合作夥伴必須先確認他們交換的訊息是有效的，才能開始處理資料。</span><span class="sxs-lookup"><span data-stu-id="deee0-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="deee0-105">您可以使用企業整合套件中的 XML 驗證連接器，根據預先定義的結構描述來驗證文件。</span><span class="sxs-lookup"><span data-stu-id="deee0-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="deee0-106">利用 XML 驗證連接器驗證文件</span><span class="sxs-lookup"><span data-stu-id="deee0-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="deee0-107">建立邏輯應用程式，並[將應用程式連結到整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md "了解如何將整合帳戶連結到邏輯應用程式")，該應用程式包含用來驗證 XML 資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="deee0-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="deee0-108">將 [要求 - 收到 HTTP 要求時]  觸發程序新增到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="deee0-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="deee0-109">若要新增 [XML 驗證] 動作，選擇 [新增動作]。</span><span class="sxs-lookup"><span data-stu-id="deee0-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="deee0-110">若要篩選所有動作直到找到您想要的，請在搜尋方塊中輸入 *xml*。</span><span class="sxs-lookup"><span data-stu-id="deee0-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="deee0-111">選擇 [XML 驗證]。</span><span class="sxs-lookup"><span data-stu-id="deee0-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="deee0-112">若要指定您想要驗證的 XML 內容，請選取 [內容]。</span><span class="sxs-lookup"><span data-stu-id="deee0-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="deee0-113">選取內文標記做為要驗證的內容。</span><span class="sxs-lookup"><span data-stu-id="deee0-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="deee0-114">若要指定用來驗證前面 *content* 輸入的結構描述，請選擇 [結構描述名稱]。</span><span class="sxs-lookup"><span data-stu-id="deee0-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="deee0-115">儲存您的工作 </span><span class="sxs-lookup"><span data-stu-id="deee0-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="deee0-116">現在您已完成設定驗證連接器。</span><span class="sxs-lookup"><span data-stu-id="deee0-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="deee0-117">在實際的應用程式中，您可能要將驗證的資料儲存在 SalesForce 之類的商業 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="deee0-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="deee0-118">若要將驗證的輸出傳送到 Salesforce，請新增一個動作。</span><span class="sxs-lookup"><span data-stu-id="deee0-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="deee0-119">若要測試您的驗證動作，請對 HTTP 端點提出要求。</span><span class="sxs-lookup"><span data-stu-id="deee0-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="deee0-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="deee0-120">Next steps</span></span>
[<span data-ttu-id="deee0-121">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="deee0-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "了解企業整合套件")   

