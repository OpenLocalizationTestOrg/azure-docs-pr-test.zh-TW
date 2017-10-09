---
title: "從 Azure 資源至 SIEM 系統 aaaIntegrate 記錄檔 |Microsoft 文件"
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
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a><span data-ttu-id="26632-103">簡介 tooMicrosoft Azure 記錄檔整合</span><span class="sxs-lookup"><span data-stu-id="26632-103">Introduction tooMicrosoft Azure log integration</span></span>
<span data-ttu-id="26632-104">了解 Azure 記錄整合、其主要功能及運作方式。</span><span class="sxs-lookup"><span data-stu-id="26632-104">Learn about Azure log integration, its key capabilities, and how it works.</span></span>

## <a name="overview"></a><span data-ttu-id="26632-105">概觀</span><span class="sxs-lookup"><span data-stu-id="26632-105">Overview</span></span>

<span data-ttu-id="26632-106">Azure 記錄檔整合是可用的解決方案，可讓您在 tooyour 在內部部署安全性資訊和事件管理 (SIEM) 系統的 toointegrate 原始記錄檔從您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="26632-106">Azure log integration is a free solution that enables you toointegrate raw logs from your Azure resources in tooyour on-premises Security Information and Event Management (SIEM) systems.</span></span>

<span data-ttu-id="26632-107">Azure 記錄整合會從 Windows 事件檢視器記錄收集 Windows 事件，從 Azure 資源收集 [Azure 活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)、[Azure 資訊安全中心警示](../security-center/security-center-intro.md)和 [Azure 診斷記錄](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="26632-107">Azure log integration collects Windows events from Windows Event Viewer logs, [Azure Activity Logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center alerts](../security-center/security-center-intro.md), and [Azure Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) from Azure resources.</span></span> <span data-ttu-id="26632-108">這項整合可協助您的 SIEM 解決方案提供統一的儀表板為您所有的資產、 在內部部署或在 hello 雲端中，以便您可以彙總，相互關聯、 分析和安全性事件的警示。</span><span class="sxs-lookup"><span data-stu-id="26632-108">This integration helps your SIEM solution provide a unified dashboard for all your assets, on-premises or in hello cloud, so that you can aggregate, correlate, analyze, and alert for security events.</span></span>

>[!NOTE]
<span data-ttu-id="26632-109">在這個階段中，只支援 hello 雲端可商業 Azure 和 Azure 政府。</span><span class="sxs-lookup"><span data-stu-id="26632-109">At this time, hello only supported clouds are Azure commercial and Azure Government.</span></span> <span data-ttu-id="26632-110">不支援其他雲端。</span><span class="sxs-lookup"><span data-stu-id="26632-110">Other clouds are not supported.</span></span>

![Azure 記錄整合][1]

## <a name="what-logs-can-i-integrate"></a><span data-ttu-id="26632-112">可以整合哪些記錄檔？</span><span class="sxs-lookup"><span data-stu-id="26632-112">What logs can I integrate?</span></span>
<span data-ttu-id="26632-113">Azure 會為每項 Azure 服務產生大量記錄。</span><span class="sxs-lookup"><span data-stu-id="26632-113">Azure produces extensive logging for every Azure service.</span></span> <span data-ttu-id="26632-114">這些記錄檔表示三種類型的記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="26632-114">These logs represent three types of logs:</span></span>

* <span data-ttu-id="26632-115">**控制/管理記錄檔**掌握 hello [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) CREATE、 UPDATE 和 DELETE 作業。</span><span class="sxs-lookup"><span data-stu-id="26632-115">**Control/management logs** provide visibility into hello [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) CREATE, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="26632-116">Azure 活動記錄是本類型的一個範例。</span><span class="sxs-lookup"><span data-stu-id="26632-116">Azure Activity Logs is an example of this type of log.</span></span>
* <span data-ttu-id="26632-117">**資料平面記錄**掌握 hello hello 的 Azure 資源的使用方式的一部分引發的事件。</span><span class="sxs-lookup"><span data-stu-id="26632-117">**Data plane logs** provide visibility into hello events raised as part of hello usage of an Azure resource.</span></span> <span data-ttu-id="26632-118">舉例來說，這種類型的記錄檔是 hello Windows 事件檢視器的**系統**，**安全性**，和**應用程式**Windows 虛擬機器中的通道。</span><span class="sxs-lookup"><span data-stu-id="26632-118">An example of this type of log is hello Windows Event Viewer's **System**, **Security**, and **Application** channels in a Windows virtual machine.</span></span> <span data-ttu-id="26632-119">另一個範例是透過 Azure 監視設定的診斷記錄</span><span class="sxs-lookup"><span data-stu-id="26632-119">Another example is  Diagnostics Logging configured through Azure Monitor</span></span>
* <span data-ttu-id="26632-120">**處理事件**提供分析的事件與以您的名義處理的警示資訊。</span><span class="sxs-lookup"><span data-stu-id="26632-120">**Processed events** provide analyzed event and alert information processed on your behalf.</span></span> <span data-ttu-id="26632-121">舉例來說，這種類型是事件的 Azure 安全性中心警示，其中 Azure 資訊安全中心已處理和分析您訂用帳戶 tooprovide 警示相關的 tooyour 目前安全性狀態。</span><span class="sxs-lookup"><span data-stu-id="26632-121">An example of this type of event is Azure Security Center Alerts, where Azure Security Center has processed and analyzed your subscription tooprovide alerts relevant tooyour current security posture.</span></span>

<span data-ttu-id="26632-122">Azure 記錄整合支援 ArcSight、QRadar 及 Splunk。</span><span class="sxs-lookup"><span data-stu-id="26632-122">Azure Log Integration supports ArcSight, QRadar, and Splunk.</span></span> <span data-ttu-id="26632-123">在所有情況下，請洽詢您的 SIEM 廠商 tooassess 它們是否有原生的連接器。</span><span class="sxs-lookup"><span data-stu-id="26632-123">In all circumstances, please check with your SIEM vendor tooassess whether they have a native connector.</span></span> <span data-ttu-id="26632-124">在某些情況下，您不會需要 toouse Azure 記錄檔整合原生連接器可用時。</span><span class="sxs-lookup"><span data-stu-id="26632-124">In some cases, you will not need toouse Azure Log Integration when native connectors are available.</span></span> <span data-ttu-id="26632-125">如需有關支援記錄類型，請瀏覽 hello 常見問題集。</span><span class="sxs-lookup"><span data-stu-id="26632-125">For additional information on supported log types please visit hello FAQ.</span></span>

>[!NOTE]
<span data-ttu-id="26632-126">雖然 Azure 記錄檔整合是可用的解決方案，但是會造成 hello 記錄檔資訊的儲存體的 Azure 儲存體成本。</span><span class="sxs-lookup"><span data-stu-id="26632-126">While Azure Log Integration is a free solution, there are Azure storage costs resulting from hello log file information storage.</span></span>

<span data-ttu-id="26632-127">社群協助是透過 hello [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)。</span><span class="sxs-lookup"><span data-stu-id="26632-127">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="26632-128">hello 論壇提供 hello AzLog 社群 hello 能力 toosupport 彼此問題、 解答、 秘訣和訣竅 tooget hello 最的 Azure 記錄檔整合。</span><span class="sxs-lookup"><span data-stu-id="26632-128">hello forum provides hello AzLog community hello ability toosupport each other with questions, answers, tips, and tricks on how tooget hello most out of Azure Log Integration.</span></span> <span data-ttu-id="26632-129">此外，hello Azure 記錄檔整合小組會監視此論壇，並將說明當我們可以。</span><span class="sxs-lookup"><span data-stu-id="26632-129">In addition, hello Azure Log Integration team monitors this forum and will help whenever we can.</span></span>

<span data-ttu-id="26632-130">您也可以建立[支援要求](../azure-supportability/how-to-create-azure-support-request.md)。</span><span class="sxs-lookup"><span data-stu-id="26632-130">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="26632-131">toodo 這個，請選取**記錄 Integration**為 hello 服務您要求支援。</span><span class="sxs-lookup"><span data-stu-id="26632-131">toodo this, select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26632-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26632-132">Next steps</span></span>
<span data-ttu-id="26632-133">本文件中，您是導入了的 tooAzure 記錄整合。</span><span class="sxs-lookup"><span data-stu-id="26632-133">In this document, you were introduced tooAzure log integration.</span></span> <span data-ttu-id="26632-134">toolearn 有關 Azure 的詳細資訊記錄整合和 hello 種記錄檔支援，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="26632-134">toolearn more about Azure log integration and hello types of logs supported, see hello following:</span></span>

* <span data-ttu-id="26632-135">[Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324) – Azure 記錄整合詳細資料、系統需求和安裝指示的下載中心。</span><span class="sxs-lookup"><span data-stu-id="26632-135">[Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) – Download Center for details, system requirements, and install instructions on Azure log integration.</span></span>
* <span data-ttu-id="26632-136">[開始使用 Azure 記錄整合](security-azure-log-integration-get-started.md) - 本教學課程將逐步引導您安裝 Azure 記錄整合，和來自 Azure WAD 儲存體、Azure 活動記錄、Azure 資訊安全中心警示以及 Azure Active Directory 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="26632-136">[Get started with Azure log integration](security-azure-log-integration-get-started.md) - This tutorial walks you through installation of Azure log integration and integrating logs from Azure WAD storage, Azure Activity Logs, Azure Security Center alerts and Azure Active Directory audit logs.</span></span>
* <span data-ttu-id="26632-137">[夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)– 此部落格文章會示範 tooconfigure Azure 與協力廠商解決方案 Splunk、 HP 討論 ArcSight 和 IBM QRadar 所記錄的整合 toowork。</span><span class="sxs-lookup"><span data-stu-id="26632-137">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – This blog post shows you how tooconfigure Azure log integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span> <span data-ttu-id="26632-138">這篇部落格代表我們的目前位置上設定 hello 協力廠商解決方案。</span><span class="sxs-lookup"><span data-stu-id="26632-138">This blog represents our current position on configuring hello partner solutions.</span></span> <span data-ttu-id="26632-139">在所有情況下，請先參閱 toopartner 解決方案的文件。</span><span class="sxs-lookup"><span data-stu-id="26632-139">In all cases, please refer toopartner solution documentation first.</span></span>
* <span data-ttu-id="26632-140">[活動和 ASC 的警示，透過 syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – 此部落格文章提供 hello 步驟 toosend 活動和 Azure 資訊安全中心警示 syslog tooQRadar</span><span class="sxs-lookup"><span data-stu-id="26632-140">[Activity and ASC alerts over syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – This blog post provides hello steps toosend Activity and Azure Security Center alerts over syslog tooQRadar</span></span>
* <span data-ttu-id="26632-141">[Azure 記錄整合常見問題集 (FAQ)](security-azure-log-integration-faq.md) - 此常見問題集會回答有關 Azure 記錄整合的問題。</span><span class="sxs-lookup"><span data-stu-id="26632-141">[Azure log Integration frequently asked questions (FAQ)](security-azure-log-integration-faq.md) - This FAQ answers questions about Azure log integration.</span></span>
* <span data-ttu-id="26632-142">[整合的資訊安全中心與 Azure 的警示記錄 Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – 本文件說明如何 toosync Azure 資訊安全中心警示搭配 Azure 記錄檔整合。</span><span class="sxs-lookup"><span data-stu-id="26632-142">[Integrating Security Center alerts with Azure log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – This document shows you how toosync Azure Security Center alerts with Azure Log Integration.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
