---
title: "aaaEnterprise b2b-Azure 邏輯應用程式的整合 |Microsoft 文件"
description: "建立 B2B 工作流程和以 hello 企業版整合套件的 logic apps 支援企業整合案例"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="1b866-103">概觀： B2B 案例和 hello 企業版整合套件與通訊</span><span class="sxs-lookup"><span data-stu-id="1b866-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="1b866-104">企業對企業 (B2B) 工作流程和無縫通訊與 Azure 邏輯應用程式，您可以啟用與 Microsoft 雲端為基礎的解決方案，hello 企業版整合套件的企業整合案例。</span><span class="sxs-lookup"><span data-stu-id="1b866-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="1b866-105">組織能以電子方式來交換訊息，即使他們使用不同的通訊協定與格式。</span><span class="sxs-lookup"><span data-stu-id="1b866-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="1b866-106">hello 組件會將不同的格式轉換成組織的系統可解譯並處理的格式。</span><span class="sxs-lookup"><span data-stu-id="1b866-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="1b866-107">組織可以透過業界標準通訊協定 (包括 [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md)、[X12](logic-apps-enterprise-integration-x12.md) 與 [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md)) 來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="1b866-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="1b866-108">您也可以使用加密與數位簽章來保護訊息的安全。</span><span class="sxs-lookup"><span data-stu-id="1b866-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="1b866-109">如果您熟悉 BizTalk Server 或 Microsoft Azure BizTalk 服務，hello 企業整合功能會是簡單 toouse，因為大部分的概念很相似。</span><span class="sxs-lookup"><span data-stu-id="1b866-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="1b866-110">一項主要差異是企業整合會使用整合帳戶 toosimplify hello 儲存和管理成品 B2B 通訊中所用。</span><span class="sxs-lookup"><span data-stu-id="1b866-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="1b866-111">在架構上，hello 企業版整合套件根據 「 整合帳戶 」。</span><span class="sxs-lookup"><span data-stu-id="1b866-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="1b866-112">這些帳戶是雲端型容器，其中儲存您的所有構件，例如結構描述、合作夥伴、憑證、對應與合約。</span><span class="sxs-lookup"><span data-stu-id="1b866-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="1b866-113">您可以使用這些成品 toodesign、 部署和維護 B2B 應用程式和也 logic apps toobuild B2B 工作流程。</span><span class="sxs-lookup"><span data-stu-id="1b866-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="1b866-114">但是，您可以使用這些成品之前，您必須先連結整合帳戶 tooyour 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b866-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="1b866-115">之後，您的邏輯應用程式就可以存取您整合帳戶的構件。</span><span class="sxs-lookup"><span data-stu-id="1b866-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="1b866-116">為什麼應該使用企業整合？</span><span class="sxs-lookup"><span data-stu-id="1b866-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="1b866-117">透過企業整合，您可以在一個位置 (亦即您的整合帳戶) 儲存您的所有構件。</span><span class="sxs-lookup"><span data-stu-id="1b866-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="1b866-118">您可以建置 B2B 工作流程，並整合協力廠商軟體做為服務 (SaaS) 應用程式、 內部部署應用程式，與自訂應用程式使用 hello Azure 邏輯應用程式的引擎和其所有的連接器。</span><span class="sxs-lookup"><span data-stu-id="1b866-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="1b866-119">您可以使用 Azure 函式為您的邏輯應用程式建立自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="1b866-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="1b866-120">如何 tooget 入門企業整合？</span><span class="sxs-lookup"><span data-stu-id="1b866-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="1b866-121">您可以建立和管理 B2B 應用程式，以透過 hello 邏輯應用程式的設計工具中 hello hello Enterprise Integration Pack **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="1b866-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="1b866-122">您也可以使用 [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell 主題") 來管理您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b866-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="1b866-123">您可以在 hello Azure 入口網站中建立應用程式之前，您必須採取的 hello 高階步驟如下：</span><span class="sxs-lookup"><span data-stu-id="1b866-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![概觀影像](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="1b866-125">有哪些常見的案例？</span><span class="sxs-lookup"><span data-stu-id="1b866-125">What are some common scenarios?</span></span>

<span data-ttu-id="1b866-126">企業整合支援下列產業標準：</span><span class="sxs-lookup"><span data-stu-id="1b866-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="1b866-127">EDI - 電子資料交換</span><span class="sxs-lookup"><span data-stu-id="1b866-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="1b866-128">EAI - 企業應用程式整合</span><span class="sxs-lookup"><span data-stu-id="1b866-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="1b866-129">以下是您需要啟動 tooget</span><span class="sxs-lookup"><span data-stu-id="1b866-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="1b866-130">具有整合帳戶的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b866-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="1b866-131">Visual Studio 2015 toocreate 對應與結構描述</span><span class="sxs-lookup"><span data-stu-id="1b866-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="1b866-132">Visual Studio 2015 2.0 適用的 Microsoft Azure Logic Apps 企業整合工具</span><span class="sxs-lookup"><span data-stu-id="1b866-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="1b866-133">立刻嘗試</span><span class="sxs-lookup"><span data-stu-id="1b866-133">Try it now</span></span>

<span data-ttu-id="1b866-134">[部署完全正常運作的範例 AS2 傳送與接收邏輯應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive)hello B2B 功能使用 Azure 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b866-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="1b866-135">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="1b866-135">Learn more</span></span>
* [<span data-ttu-id="1b866-136">合約</span><span class="sxs-lookup"><span data-stu-id="1b866-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")
* [<span data-ttu-id="1b866-137">商務 tooBusiness (B2B) 案例</span><span class="sxs-lookup"><span data-stu-id="1b866-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "深入了解如何與 B2B 功能 toocreate Logic apps")  
* [<span data-ttu-id="1b866-138">憑證</span><span class="sxs-lookup"><span data-stu-id="1b866-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "了解企業整合憑證")
* [<span data-ttu-id="1b866-139">一般檔案編碼/解碼</span><span class="sxs-lookup"><span data-stu-id="1b866-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "深入了解如何 tooencode 及解碼一般檔案內容")  
* [<span data-ttu-id="1b866-140">整合帳戶</span><span class="sxs-lookup"><span data-stu-id="1b866-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "了解整合帳戶")
* [<span data-ttu-id="1b866-141">對應</span><span class="sxs-lookup"><span data-stu-id="1b866-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")
* [<span data-ttu-id="1b866-142">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="1b866-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "了解企業整合夥伴")
* [<span data-ttu-id="1b866-143">結構描述</span><span class="sxs-lookup"><span data-stu-id="1b866-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "了解企業整合結構描述")
* [<span data-ttu-id="1b866-144">XML 訊息驗證</span><span class="sxs-lookup"><span data-stu-id="1b866-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "深入了解如何 toovalidate XML 訊息與邏輯應用程式")
* [<span data-ttu-id="1b866-145">XML 轉換</span><span class="sxs-lookup"><span data-stu-id="1b866-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "了解企業整合對應")
* [<span data-ttu-id="1b866-146">企業整合連接器</span><span class="sxs-lookup"><span data-stu-id="1b866-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "了解企業整合套件連接器")
* [<span data-ttu-id="1b866-147">整合帳戶中繼資料</span><span class="sxs-lookup"><span data-stu-id="1b866-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "深入了解整合帳戶中繼資料")
* [<span data-ttu-id="1b866-148">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="1b866-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "深入了解監視 B2B 訊息")
* [<span data-ttu-id="1b866-149">在 OMS 入口網站中追蹤 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="1b866-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "深入了解在 OMS 入口網站中追蹤 B2B 訊息")

