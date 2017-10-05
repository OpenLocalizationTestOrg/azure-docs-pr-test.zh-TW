---
title: "將記錄從 Azure 資源整合到 SIEM 系統 | Microsoft Docs"
description: "了解 Azure 記錄整合、其主要功能及運作方式。"
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 6c3a2ac18fdb7a7a722447af720b9dee28adef08
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-microsoft-azure-log-integration"></a><span data-ttu-id="1c173-103">Microsoft Azure 記錄整合簡介</span><span class="sxs-lookup"><span data-stu-id="1c173-103">Introduction to Microsoft Azure log integration</span></span>
<span data-ttu-id="1c173-104">了解 Azure 記錄整合、其主要功能及運作方式。</span><span class="sxs-lookup"><span data-stu-id="1c173-104">Learn about Azure log integration, its key capabilities, and how it works.</span></span>

## <a name="overview"></a><span data-ttu-id="1c173-105">概觀</span><span class="sxs-lookup"><span data-stu-id="1c173-105">Overview</span></span>

<span data-ttu-id="1c173-106">Azure 記錄整合是免費的解決方案，可讓您將來自 Azure 資源的未經處理記錄，整合到內部部署安全性資訊及事件管理 (SIEM) 系統內。</span><span class="sxs-lookup"><span data-stu-id="1c173-106">Azure log integration is a free solution that enables you to integrate raw logs from your Azure resources in to your on-premises Security Information and Event Management (SIEM) systems.</span></span>

<span data-ttu-id="1c173-107">Azure 記錄整合會從 Windows 事件檢視器記錄收集 Windows 事件，從 Azure 資源收集 [Azure 活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)、[Azure 資訊安全中心警示](../security-center/security-center-intro.md)和 [Azure 診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="1c173-107">Azure log integration collects Windows events from Windows Event Viewer logs, [Azure Activity Logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center alerts](../security-center/security-center-intro.md), and [Azure Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) from Azure resources.</span></span> <span data-ttu-id="1c173-108">這項整合協助您的 SIEM 方案提供內部部署或在雲端中所有資產統一的儀表板，以便您彙總、相互關聯、分析和警示安全性事件。</span><span class="sxs-lookup"><span data-stu-id="1c173-108">This integration helps your SIEM solution provide a unified dashboard for all your assets, on-premises or in the cloud, so that you can aggregate, correlate, analyze, and alert for security events.</span></span>

>[!NOTE]
<span data-ttu-id="1c173-109">目前唯一支援的雲端是 Azure 商業和 Azure Government。</span><span class="sxs-lookup"><span data-stu-id="1c173-109">At this time, the only supported clouds are Azure commercial and Azure Government.</span></span> <span data-ttu-id="1c173-110">不支援其他雲端。</span><span class="sxs-lookup"><span data-stu-id="1c173-110">Other clouds are not supported.</span></span>

![Azure 記錄整合][1]

## <a name="what-logs-can-i-integrate"></a><span data-ttu-id="1c173-112">可以整合哪些記錄檔？</span><span class="sxs-lookup"><span data-stu-id="1c173-112">What logs can I integrate?</span></span>
<span data-ttu-id="1c173-113">Azure 會為每項 Azure 服務產生大量記錄。</span><span class="sxs-lookup"><span data-stu-id="1c173-113">Azure produces extensive logging for every Azure service.</span></span> <span data-ttu-id="1c173-114">這些記錄檔表示三種類型的記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="1c173-114">These logs represent three types of logs:</span></span>

* <span data-ttu-id="1c173-115">**控制/管理記錄檔**：可讓您看到 [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) 的 CREATE、UPDATE 和 DELETE 作業。</span><span class="sxs-lookup"><span data-stu-id="1c173-115">**Control/management logs** provide visibility into the [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) CREATE, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="1c173-116">Azure 活動記錄是本類型的一個範例。</span><span class="sxs-lookup"><span data-stu-id="1c173-116">Azure Activity Logs is an example of this type of log.</span></span>
* <span data-ttu-id="1c173-117">**資料平面記錄檔**：可讓您看到使用 Azure 資源時所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="1c173-117">**Data plane logs** provide visibility into the events raised as part of the usage of an Azure resource.</span></span> <span data-ttu-id="1c173-118">本類型的記錄檔範例是 Windows 事件檢視器**系統**、**安全性**和 Windows 虛擬機器中的**應用程式**頻道。</span><span class="sxs-lookup"><span data-stu-id="1c173-118">An example of this type of log is the Windows Event Viewer's **System**, **Security**, and **Application** channels in a Windows virtual machine.</span></span> <span data-ttu-id="1c173-119">另一個範例是透過 Azure 監視設定的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="1c173-119">Another example is  Diagnostics Logging configured through Azure Monitor</span></span>
* <span data-ttu-id="1c173-120">**處理事件**提供分析的事件與以您的名義處理的警示資訊。</span><span class="sxs-lookup"><span data-stu-id="1c173-120">**Processed events** provide analyzed event and alert information processed on your behalf.</span></span> <span data-ttu-id="1c173-121">本事件類型的範例是 Azure 安全性中心警示，其中 Azure 資訊安全中心已處理並分析您的訂用帳戶，以提供與您目前安全性狀態相關的警示。</span><span class="sxs-lookup"><span data-stu-id="1c173-121">An example of this type of event is Azure Security Center Alerts, where Azure Security Center has processed and analyzed your subscription to provide alerts relevant to your current security posture.</span></span>

<span data-ttu-id="1c173-122">Azure 記錄整合支援 ArcSight、QRadar 及 Splunk。</span><span class="sxs-lookup"><span data-stu-id="1c173-122">Azure Log Integration supports ArcSight, QRadar, and Splunk.</span></span> <span data-ttu-id="1c173-123">不論在何種情況下，請向您的 SIEM 廠商確認，以了解對方是否有原生的連接器。</span><span class="sxs-lookup"><span data-stu-id="1c173-123">In all circumstances, please check with your SIEM vendor to assess whether they have a native connector.</span></span> <span data-ttu-id="1c173-124">有些情況下，如果有原生連接器可供使用，您就不需要使用 Azure 記錄整合。</span><span class="sxs-lookup"><span data-stu-id="1c173-124">In some cases, you will not need to use Azure Log Integration when native connectors are available.</span></span> <span data-ttu-id="1c173-125">如需支援之記錄類型的其他資訊，請瀏覽常見問題集。</span><span class="sxs-lookup"><span data-stu-id="1c173-125">For additional information on supported log types please visit the FAQ.</span></span>

>[!NOTE]
<span data-ttu-id="1c173-126">雖然 Azure 記錄整合是免費的解決方案，記錄檔資訊的儲存體仍會產生 Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="1c173-126">While Azure Log Integration is a free solution, there are Azure storage costs resulting from the log file information storage.</span></span>

<span data-ttu-id="1c173-127">可透過 [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)取得社群協助。</span><span class="sxs-lookup"><span data-stu-id="1c173-127">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="1c173-128">論壇讓 AzLog 社群能針對如何充分利用 Azure 記錄整合，透過分享問題、解答、祕訣和技巧支援彼此。</span><span class="sxs-lookup"><span data-stu-id="1c173-128">The forum provides the AzLog community the ability to support each other with questions, answers, tips, and tricks on how to get the most out of Azure Log Integration.</span></span> <span data-ttu-id="1c173-129">此外，Azure 記錄整合小組會監視這個論壇，並且會盡全力提供協助。</span><span class="sxs-lookup"><span data-stu-id="1c173-129">In addition, the Azure Log Integration team monitors this forum and will help whenever we can.</span></span>

<span data-ttu-id="1c173-130">您也可以建立[支援要求](../azure-supportability/how-to-create-azure-support-request.md)。</span><span class="sxs-lookup"><span data-stu-id="1c173-130">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="1c173-131">若要這樣做，請選取 [記錄整合] 作為您要求支援的服務。</span><span class="sxs-lookup"><span data-stu-id="1c173-131">To do this, select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c173-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1c173-132">Next steps</span></span>
<span data-ttu-id="1c173-133">在本文中為您介紹了 Azure 記錄整合。</span><span class="sxs-lookup"><span data-stu-id="1c173-133">In this document, you were introduced to Azure log integration.</span></span> <span data-ttu-id="1c173-134">若要深入了解 Azure 記錄整合和支援的記錄檔的類型，請參閱下列各項︰</span><span class="sxs-lookup"><span data-stu-id="1c173-134">To learn more about Azure log integration and the types of logs supported, see the following:</span></span>

* <span data-ttu-id="1c173-135">[Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 記錄整合詳細資料、系統需求和安裝指示的下載中心。</span><span class="sxs-lookup"><span data-stu-id="1c173-135">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span></span>
* <span data-ttu-id="1c173-136">[開始使用 Azure 記錄整合](security-azure-log-integration-get-started.md) - 本教學課程將逐步引導您安裝 Azure 記錄整合，和來自 Azure WAD 儲存體、Azure 活動記錄、Azure 資訊安全中心警示以及 Azure Active Directory 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1c173-136">[Get started with Azure log integration](security-azure-log-integration-get-started.md) - This tutorial walks you through installation of Azure log integration and integrating logs from Azure WAD storage, Azure Activity Logs, Azure Security Center alerts and Azure Active Directory audit logs.</span></span>
* <span data-ttu-id="1c173-137">[合作夥伴設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – 此部落格文章說明如何設定 Azure 記錄整合，以搭配使用合作夥伴解決方案 Splunk、HP ArcSight 和 IBM QRadar。</span><span class="sxs-lookup"><span data-stu-id="1c173-137">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how to configure Azure log integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span> <span data-ttu-id="1c173-138">這篇部落格代表我們目前針對設定合作夥伴解決方案的定位。</span><span class="sxs-lookup"><span data-stu-id="1c173-138">This blog represents our current position on configuring the partner solutions.</span></span> <span data-ttu-id="1c173-139">在所有情況下，都請先參閱合作夥伴解決方案文件。</span><span class="sxs-lookup"><span data-stu-id="1c173-139">In all cases, please refer to partner solution documentation first.</span></span>
* <span data-ttu-id="1c173-140">[透過 syslog 傳送到 QRadar 的活動和 ASC 警示 (英文)](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – 此部落格文章提供透過 syslog 將活動和 Azure 資訊安全中心警示傳送至 QRadar 的步驟</span><span class="sxs-lookup"><span data-stu-id="1c173-140">[Activity and ASC alerts over syslog to QRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – This blog post provides the steps to send Activity and Azure Security Center alerts over syslog to QRadar</span></span>
* <span data-ttu-id="1c173-141">[Azure 記錄整合常見問題集 (FAQ)](security-azure-log-integration-faq.md) - 此常見問題集會回答有關 Azure 記錄整合的問題。</span><span class="sxs-lookup"><span data-stu-id="1c173-141">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span></span>
* <span data-ttu-id="1c173-142">[Azure 記錄整合的整合資訊安全中心警示](../security-center/security-center-integrating-alerts-with-log-integration.md) – 本文件說明使用 Azure 記錄整合同步 Azure 資訊安全中心警示。</span><span class="sxs-lookup"><span data-stu-id="1c173-142">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how to sync Azure Security Center alerts with Azure Log Integration.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
