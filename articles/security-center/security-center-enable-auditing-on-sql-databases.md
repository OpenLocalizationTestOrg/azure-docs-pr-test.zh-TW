---
title: "aaaEnable 稽核和威脅偵測 SQL 資料庫中 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用稽核和威脅的偵測，在 SQL 資料庫 * *。"
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
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="95147-103">在 Azure 資訊安全中心的 SQL Database 上啟用稽核與威脅偵測</span><span class="sxs-lookup"><span data-stu-id="95147-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="95147-104">如果尚未啟用稽核與威脅偵測，Azure 資訊安全中心將建議您針對所有 SQL Database 開啟稽核與威脅偵測。</span><span class="sxs-lookup"><span data-stu-id="95147-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="95147-105">稽核與威脅偵測可協助您保持符合法規、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。</span><span class="sxs-lookup"><span data-stu-id="95147-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="95147-106">一旦您已開啟稽核，您可以設定威脅偵測設定和電子郵件 tooreceive 安全性警示。</span><span class="sxs-lookup"><span data-stu-id="95147-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="95147-107">威脅偵測偵測到潛在的安全性威脅 toohello 資料庫異常資料庫活動。</span><span class="sxs-lookup"><span data-stu-id="95147-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="95147-108">這可讓您 toodetect，並在發生回應 toopotential 威脅。</span><span class="sxs-lookup"><span data-stu-id="95147-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="95147-109">這項建議適用於 toohello; 僅限 Azure SQL 服務它不包含 SQL 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="95147-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="95147-110">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="95147-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="95147-111">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="95147-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="95147-112">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="95147-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="95147-113">在 hello**建議**刀鋒視窗中，選取**SQL 資料庫上的啟用稽核與威脅偵測**。</span><span class="sxs-lookup"><span data-stu-id="95147-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="95147-114">這會開啟 hello **SQL 資料庫上的啟用稽核與威脅偵測**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="95147-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![在 SQL Database 上啟用稽核][1]
2. <span data-ttu-id="95147-116">選取 SQL 資料庫 tooenable 上的稽核。</span><span class="sxs-lookup"><span data-stu-id="95147-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="95147-117">這會開啟 hello**稽核與威脅偵測**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="95147-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="95147-118">在 hello**稽核與威脅偵測**刀鋒視窗中，選取**ON**下**稽核**。</span><span class="sxs-lookup"><span data-stu-id="95147-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![開啟稽核與脅偵測][2]
4. <span data-ttu-id="95147-120">中的 hello 步驟[hello Azure 入口網站中的 SQL Database 威脅偵測](../sql-database/sql-database-threat-detection-portal.md)tooturn 上的及設定威脅偵測和 tooconfigure hello 清單將會收到偵測的異常活動時的安全性警示的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="95147-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="95147-121">另請參閱</span><span class="sxs-lookup"><span data-stu-id="95147-121">See also</span></span>
<span data-ttu-id="95147-122">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 」 啟用稽核與威脅偵測 SQL 資料庫。 」</span><span class="sxs-lookup"><span data-stu-id="95147-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="95147-123">toolearn 深入了解保護您的 SQL 資料庫，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="95147-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="95147-124">保護您的 SQL Database</span><span class="sxs-lookup"><span data-stu-id="95147-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="95147-125">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="95147-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="95147-126">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="95147-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="95147-127">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="95147-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="95147-128">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="95147-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="95147-129">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="95147-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="95147-130">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="95147-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="95147-131">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="95147-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="95147-132">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="95147-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
