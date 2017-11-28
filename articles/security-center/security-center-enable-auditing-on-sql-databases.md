---
title: "在 Azure 資訊安全中心的 SQL Database 上啟用稽核與威脅偵測 | Microsoft Docs"
description: "本文件將示範如何實作 Azure 資訊安全中心建議 * * 啟用稽核和威脅的偵測，在 SQL 資料庫 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 8f4febdaa4497fee0dc690b59cd6eaa415c5e5cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="78d31-103">在 Azure 資訊安全中心的 SQL Database 上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="78d31-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="78d31-104">如果尚未啟用稽核與威脅偵測，Azure 資訊安全中心將建議您針對所有 SQL Database 開啟稽核與威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="78d31-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="78d31-105">稽核與威脅偵測可協助您保持符合法規、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="78d31-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="78d31-106">一旦開啟稽核之後，您就可以設定威脅偵測設定和電子郵件來接收安全性警示。</span><span class="sxs-lookup"><span data-stu-id="78d31-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="78d31-107">威脅偵測會偵測異常資料庫活動，指出資料庫有潛在的安全性威脅。</span><span class="sxs-lookup"><span data-stu-id="78d31-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="78d31-108">這可讓您在發生潛在威脅時偵測到它們並加以回應。</span><span class="sxs-lookup"><span data-stu-id="78d31-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="78d31-109">此建議僅適用於 Azure SQL 服務，不包含在虛擬機器上執行的 SQL。</span><span class="sxs-lookup"><span data-stu-id="78d31-109">This recommendation applies to the Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="78d31-110">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="78d31-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="78d31-111">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="78d31-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="78d31-112">實作建議</span><span class="sxs-lookup"><span data-stu-id="78d31-112">Implement the recommendation</span></span>
1. <span data-ttu-id="78d31-113">在 [建議] 刀鋒視窗中，選取 [在 SQL Database 上啟用稽核與威脅偵測]。</span><span class="sxs-lookup"><span data-stu-id="78d31-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="78d31-114">這會開啟 [在 SQL Database 上啟用稽核與威脅偵測]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="78d31-114">This opens the **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![在 SQL Database 上啟用稽核][1]
2. <span data-ttu-id="78d31-116">選取要在其上啟用稽核的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="78d31-116">Select a SQL database to enable auditing on.</span></span> <span data-ttu-id="78d31-117">這會開啟 [稽核與威脅偵測] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="78d31-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="78d31-118">在 [稽核與威脅偵測] 刀鋒視窗上，選取 [稽核] 下方的 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="78d31-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![開啟稽核與脅偵測][2]
4. <span data-ttu-id="78d31-120">遵循 [Azure 入口網站中的 SQL Database 威脅偵測](../sql-database/sql-database-threat-detection-portal.md)的步驟，來開啟並設定威脅偵測，以及設定將在偵測到異常活動時接收到安全性警示的電子郵件清單。</span><span class="sxs-lookup"><span data-stu-id="78d31-120">Follow the steps in [SQL Database Threat Detection in the Azure portal](../sql-database/sql-database-threat-detection-portal.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="78d31-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="78d31-121">See also</span></span>
<span data-ttu-id="78d31-122">本文說明了如何實作資訊安全中心建議的「在 SQL Database 上啟用稽核與威脅偵測」。</span><span class="sxs-lookup"><span data-stu-id="78d31-122">This article showed you how to implement the Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="78d31-123">若要深入了解如何保護您的 SQL Database，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="78d31-123">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="78d31-124">保護您的 SQL Database</span><span class="sxs-lookup"><span data-stu-id="78d31-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="78d31-125">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="78d31-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="78d31-126">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="78d31-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="78d31-127">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="78d31-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="78d31-128">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="78d31-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="78d31-129">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="78d31-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="78d31-130">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="78d31-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="78d31-131">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="78d31-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="78d31-132">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="78d31-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
