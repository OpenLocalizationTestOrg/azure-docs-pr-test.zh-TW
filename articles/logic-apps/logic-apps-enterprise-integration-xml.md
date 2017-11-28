---
title: "aaaWorking 搭配 XML 訊息中工作流程-Azure 邏輯應用程式 |Microsoft 文件"
description: "處理、 驗證、 轉換和擴充 XML 訊息中的 logic apps 和商務 tooscenarios 使用 hello 企業版整合套件"
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
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="d8417-103">驗證和轉換的 XML、編碼和解碼一般檔案，並擴充邏輯應用程式中的訊息功能</span><span class="sxs-lookup"><span data-stu-id="d8417-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="d8417-104">使用邏輯應用程式，您尚未 hello 能力 tooprocess XML 訊息傳送和接收。</span><span class="sxs-lookup"><span data-stu-id="d8417-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="d8417-105">此功能隨附於 hello 企業版整合套件。</span><span class="sxs-lookup"><span data-stu-id="d8417-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="d8417-106">BizTalk Server 背景的使用者，hello 企業版整合套件提供您類似能力 tootransform 和驗證訊息、 使用一般檔案，即使使用 XPath tooenrich 或從訊息擷取特定的屬性。</span><span class="sxs-lookup"><span data-stu-id="d8417-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="d8417-107">這些使用者是新 toothis 空間，這些功能會展開如何在您的工作流程內處理訊息。</span><span class="sxs-lookup"><span data-stu-id="d8417-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="d8417-108">例如，如果您是在企業對企業案例中，而且使用特定的 XML 結構描述，則您可以使用 hello Enterprise Integration Pack tooenhance 如何公司就會處理這些訊息。</span><span class="sxs-lookup"><span data-stu-id="d8417-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="d8417-109">hello 企業版整合套件包括：</span><span class="sxs-lookup"><span data-stu-id="d8417-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="d8417-110">[XML 驗證](logic-apps-enterprise-integration-xml-validation.md "了解 XML 訊息驗證") - 根據特定的結構描述，驗證傳入或傳出 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="d8417-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="d8417-111">[XML 轉換](../logic-apps/logic-apps-enterprise-integration-transform.md "深入了解 XML 訊息轉換和對應")-轉換或自訂您的需求或協力廠商的 hello 需求為基礎的 XML 訊息。</span><span class="sxs-lookup"><span data-stu-id="d8417-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="d8417-112">[一般檔案編碼與一般檔案解碼](logic-apps-enterprise-integration-flatfile.md "了解一般檔案編碼/解碼") - 編碼或解碼一般檔案。</span><span class="sxs-lookup"><span data-stu-id="d8417-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="d8417-113">例如，SAP 接受並以一般檔案格式傳送 IDOC 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8417-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="d8417-114">許多整合平台會建立 XML 訊息，包括邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="d8417-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="d8417-115">因此，您可以建立邏輯應用程式，使用 hello 一般檔案編碼器太 「 轉換 」 的 XML 檔案 tooflat 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8417-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="d8417-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) -來擴充訊息，並從 hello 訊息中擷取特定的屬性。</span><span class="sxs-lookup"><span data-stu-id="d8417-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="d8417-117">接著，您可以使用 hello 擷取屬性 tooroute hello 訊息 tooa 目的地或中繼端點。</span><span class="sxs-lookup"><span data-stu-id="d8417-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="d8417-118">試做</span><span class="sxs-lookup"><span data-stu-id="d8417-118">Try it out</span></span>
<span data-ttu-id="d8417-119">[將完全正常運作的邏輯應用程式部署](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline)（GitHub 範例） 利用 Azure 邏輯應用程式中的 hello XML 功能。</span><span class="sxs-lookup"><span data-stu-id="d8417-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="d8417-120">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="d8417-120">Learn more</span></span>
[<span data-ttu-id="d8417-121">深入了解 hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="d8417-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "深入了解 Enterprise Integration Pack")
