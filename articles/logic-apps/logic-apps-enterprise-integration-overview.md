---
title: "適用於 B2B 的企業整合 - Azure Logic Apps | Microsoft Docs"
description: "使用企業整合套件針對邏輯應用程式建置 B2B 工作流程並支援企業整合案例"
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="787c0-103">概觀：使用企業整合套件的 B2B 案例與通訊</span><span class="sxs-lookup"><span data-stu-id="787c0-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="787c0-104">對於企業對企業 (B2B) 工作流程以及使用 Azure Logic Apps 進行無接縫通訊，您可以搭配 Microsoft 的雲端解決方案「企業整合套件」啟用企業整合案例。</span><span class="sxs-lookup"><span data-stu-id="787c0-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="787c0-105">組織能以電子方式來交換訊息，即使他們使用不同的通訊協定與格式。</span><span class="sxs-lookup"><span data-stu-id="787c0-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="787c0-106">該套件會將不同的格式轉換為組織系統的可以解譯並處理的格式。</span><span class="sxs-lookup"><span data-stu-id="787c0-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="787c0-107">組織可以透過業界標準通訊協定 (包括 [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md)、[X12](logic-apps-enterprise-integration-x12.md) 與 [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md)) 來交換訊息。</span><span class="sxs-lookup"><span data-stu-id="787c0-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="787c0-108">您也可以使用加密與數位簽章來保護訊息的安全。</span><span class="sxs-lookup"><span data-stu-id="787c0-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="787c0-109">若您熟悉 BizTalk Server 或 Microsoft Azure BizTalk 服務，您會發現企業整合功能很容易使用，因為大部分的概念是類似的。</span><span class="sxs-lookup"><span data-stu-id="787c0-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="787c0-110">有一個主要差異是企業整合會使用整合帳戶，來簡化對於 B2B 通訊中所使用構件的儲存與管理。</span><span class="sxs-lookup"><span data-stu-id="787c0-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="787c0-111">就架構而言，企業整合套件是以「整合帳戶」為基礎。</span><span class="sxs-lookup"><span data-stu-id="787c0-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="787c0-112">這些帳戶是雲端型容器，其中儲存您的所有構件，例如結構描述、合作夥伴、憑證、對應與合約。</span><span class="sxs-lookup"><span data-stu-id="787c0-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="787c0-113">您可以使用這些構件來設計、部署及維護您的 B2B 應用程式，以及針對邏輯應用程式建置 B2B 工作流程。</span><span class="sxs-lookup"><span data-stu-id="787c0-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="787c0-114">但是，在您可以使用這些構件之前，您必須先將您的整合帳戶連結到您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="787c0-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="787c0-115">之後，您的邏輯應用程式就可以存取您整合帳戶的構件。</span><span class="sxs-lookup"><span data-stu-id="787c0-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="787c0-116">為什麼應該使用企業整合？</span><span class="sxs-lookup"><span data-stu-id="787c0-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="787c0-117">透過企業整合，您可以在一個位置 (亦即您的整合帳戶) 儲存您的所有構件。</span><span class="sxs-lookup"><span data-stu-id="787c0-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="787c0-118">您可以使用 Azure Logic Apps 與其所有連接器來建置 B2B 工作流程，並整合協力廠商軟體即服務 (SaaS) 應用程式、內部部署應用程式與自訂應用程式。</span><span class="sxs-lookup"><span data-stu-id="787c0-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="787c0-119">您可以使用 Azure 函式為您的邏輯應用程式建立自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="787c0-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="787c0-120">如何開始使用企業整合？</span><span class="sxs-lookup"><span data-stu-id="787c0-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="787c0-121">您可以透過 **Azure 入口網站**中的邏輯應用程式設計工具，使用企業整合套件來建置及管理 B2B 應用程式。</span><span class="sxs-lookup"><span data-stu-id="787c0-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="787c0-122">您也可以使用 [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell 主題") 來管理您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="787c0-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="787c0-123">以下是在 Azure 入口網站中建立應用程式之前必須執行的高階步驟︰</span><span class="sxs-lookup"><span data-stu-id="787c0-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![概觀影像](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="787c0-125">有哪些常見的案例？</span><span class="sxs-lookup"><span data-stu-id="787c0-125">What are some common scenarios?</span></span>

<span data-ttu-id="787c0-126">企業整合支援下列產業標準：</span><span class="sxs-lookup"><span data-stu-id="787c0-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="787c0-127">EDI - 電子資料交換</span><span class="sxs-lookup"><span data-stu-id="787c0-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="787c0-128">EAI - 企業應用程式整合</span><span class="sxs-lookup"><span data-stu-id="787c0-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="787c0-129">若要開始，您需要：</span><span class="sxs-lookup"><span data-stu-id="787c0-129">Here's what you need to get started</span></span>

* <span data-ttu-id="787c0-130">具有整合帳戶的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="787c0-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="787c0-131">可建立對應和結構描述的 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="787c0-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="787c0-132">Visual Studio 2015 2.0 適用的 Microsoft Azure Logic Apps 企業整合工具</span><span class="sxs-lookup"><span data-stu-id="787c0-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="787c0-133">立刻嘗試</span><span class="sxs-lookup"><span data-stu-id="787c0-133">Try it now</span></span>

<span data-ttu-id="787c0-134">[部署可運作的 AS2 傳送與接收邏輯應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive)，這些應用程式使用 Azure Logic Apps 的 B2B 功能。</span><span class="sxs-lookup"><span data-stu-id="787c0-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="787c0-135">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="787c0-135">Learn more</span></span>
* [<span data-ttu-id="787c0-136">合約</span><span class="sxs-lookup"><span data-stu-id="787c0-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")
* [<span data-ttu-id="787c0-137">企業對企業 (B2B) 案例</span><span class="sxs-lookup"><span data-stu-id="787c0-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "了解如何建立具有 B2B 功能的 Logic Apps")  
* [<span data-ttu-id="787c0-138">憑證</span><span class="sxs-lookup"><span data-stu-id="787c0-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "了解企業整合憑證")
* [<span data-ttu-id="787c0-139">一般檔案編碼/解碼</span><span class="sxs-lookup"><span data-stu-id="787c0-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "了解如何將一般檔案內容編碼和解碼")  
* [<span data-ttu-id="787c0-140">整合帳戶</span><span class="sxs-lookup"><span data-stu-id="787c0-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "了解整合帳戶")
* [<span data-ttu-id="787c0-141">對應</span><span class="sxs-lookup"><span data-stu-id="787c0-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")
* [<span data-ttu-id="787c0-142">合作夥伴</span><span class="sxs-lookup"><span data-stu-id="787c0-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "了解企業整合夥伴")
* [<span data-ttu-id="787c0-143">結構描述</span><span class="sxs-lookup"><span data-stu-id="787c0-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "了解企業整合結構描述")
* [<span data-ttu-id="787c0-144">XML 訊息驗證</span><span class="sxs-lookup"><span data-stu-id="787c0-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "了解如何使用 Logic Apps 驗證 XML 訊息")
* [<span data-ttu-id="787c0-145">XML 轉換</span><span class="sxs-lookup"><span data-stu-id="787c0-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "了解企業整合對應")
* [<span data-ttu-id="787c0-146">企業整合連接器</span><span class="sxs-lookup"><span data-stu-id="787c0-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "了解企業整合套件連接器")
* [<span data-ttu-id="787c0-147">整合帳戶中繼資料</span><span class="sxs-lookup"><span data-stu-id="787c0-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "深入了解整合帳戶中繼資料")
* [<span data-ttu-id="787c0-148">監視 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="787c0-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "深入了解監視 B2B 訊息")
* [<span data-ttu-id="787c0-149">在 OMS 入口網站中追蹤 B2B 訊息</span><span class="sxs-lookup"><span data-stu-id="787c0-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "深入了解在 OMS 入口網站中追蹤 B2B 訊息")

