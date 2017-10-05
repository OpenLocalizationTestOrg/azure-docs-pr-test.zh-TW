---
title: "使用工作流程中的 XML 訊息 - Azure Logic Apps | Microsoft Docs"
description: "使用企業整合套件處理、驗證、轉換和擴充邏輯應用程式和商務中的 XML 訊息案例"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 3fec4935f5317be4bf8c9e05f1c24a7c05381b1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="c37d7-103">驗證和轉換的 XML、編碼和解碼一般檔案，並擴充邏輯應用程式中的訊息功能</span><span class="sxs-lookup"><span data-stu-id="c37d7-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="c37d7-104">使用邏輯應用程式，您可以處理您傳送和接收的 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="c37d7-104">Using logic apps, you have the ability to process XML messages that you send and receive.</span></span> <span data-ttu-id="c37d7-105">這項功能包含於企業整合套件。</span><span class="sxs-lookup"><span data-stu-id="c37d7-105">This feature is included with the Enterprise Integration Pack.</span></span> <span data-ttu-id="c37d7-106">針對具有 BizTalk Server 背景的這些使用者，企業整合套件可為您提供與轉換和驗證訊息、使用一般檔案，甚至使用 XPath 加強或從訊息擷取特定屬性的類似功能。</span><span class="sxs-lookup"><span data-stu-id="c37d7-106">For those users with a BizTalk Server background, the Enterprise Integration Pack gives you similar abilities to transform and validate messages, work with flat files, and even use XPath to enrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="c37d7-107">此空間不熟悉的使用者，這些功能可展開您工作流程內的處理訊息方式。</span><span class="sxs-lookup"><span data-stu-id="c37d7-107">For those users who are new to this space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="c37d7-108">例如，如果您是在企業對企業案例中，並且使用特定的 XML 結構描述，則您可以使用企業整合套件以增強貴公司處理這些訊息的方式。</span><span class="sxs-lookup"><span data-stu-id="c37d7-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use the Enterprise Integration Pack to enhance how your company processes these messages.</span></span> 

<span data-ttu-id="c37d7-109">企業整合套件包含：</span><span class="sxs-lookup"><span data-stu-id="c37d7-109">The Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="c37d7-110">[XML 驗證](logic-apps-enterprise-integration-xml-validation.md "了解 XML 訊息驗證") - 根據特定的結構描述，驗證傳入或傳出 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="c37d7-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="c37d7-111">[XML 轉換](../logic-apps/logic-apps-enterprise-integration-transform.md "了解 XML 訊息轉換和對應") - 根據您的需求或夥伴的需求轉換或自訂 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="c37d7-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or the requirements of a partner.</span></span>
* <span data-ttu-id="c37d7-112">[一般檔案編碼與一般檔案解碼](logic-apps-enterprise-integration-flatfile.md "了解一般檔案編碼/解碼") - 編碼或解碼一般檔案。</span><span class="sxs-lookup"><span data-stu-id="c37d7-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="c37d7-113">例如，SAP 接受並以一般檔案格式傳送 IDOC 檔案。</span><span class="sxs-lookup"><span data-stu-id="c37d7-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="c37d7-114">許多整合平台會建立 XML 訊息，包括邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c37d7-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="c37d7-115">因此，您可以建立使用一般檔案編碼器將 XML 檔案「轉換」為一般檔案的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="c37d7-115">So, you can create a logic app that uses the flat file encoder to "convert" XML files to flat files.</span></span> 
* <span data-ttu-id="c37d7-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - 可擴充訊息，並從訊息擷取特定的屬性。</span><span class="sxs-lookup"><span data-stu-id="c37d7-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from the message.</span></span> <span data-ttu-id="c37d7-117">然後您可以使用擷取的屬性將訊息傳送至目的地或中繼端點。</span><span class="sxs-lookup"><span data-stu-id="c37d7-117">You can then use the extracted properties to route the message to a destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="c37d7-118">試做</span><span class="sxs-lookup"><span data-stu-id="c37d7-118">Try it out</span></span>
<span data-ttu-id="c37d7-119">使用 Azure Logic Apps 中的 XML 功能，[部署全功能的邏輯應用程式 (GitHub sample)](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline)。</span><span class="sxs-lookup"><span data-stu-id="c37d7-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using the XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c37d7-120">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="c37d7-120">Learn more</span></span>
[<span data-ttu-id="c37d7-121">深入了解企業整合套件</span><span class="sxs-lookup"><span data-stu-id="c37d7-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "了解企業整合套件")
