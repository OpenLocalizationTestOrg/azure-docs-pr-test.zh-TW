---
title: "在 Azure 資訊安全中心啟用透明資料加密 | Microsoft Docs"
description: "本文件說明如何實作 Azure 資訊安全中心建議的「啟用透明資料加密」。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e4be8a0e-2118-4ee9-a266-69e52d9f7f8e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 2a2963affdbff3710ad08f86c6ed4e6304335559
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="75099-103">在 Azure 資訊安全中心啟用透明資料加密</span><span class="sxs-lookup"><span data-stu-id="75099-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="75099-104">如果尚未啟用 TDE，Azure 資訊安全中心將建議您在 SQL Database 上啟用透明資料加密 (TDE)。</span><span class="sxs-lookup"><span data-stu-id="75099-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="75099-105">TDE 可保護您的資料，並在無須變更您應用程式的情況下，加密不在作用中的資料庫、相關聯的備份以及交易記錄檔，以協助您符合法規遵循需求。</span><span class="sxs-lookup"><span data-stu-id="75099-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes to your application.</span></span> <span data-ttu-id="75099-106">若要深入了解，請參閱 [Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/dn948096)。</span><span class="sxs-lookup"><span data-stu-id="75099-106">To learn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="75099-107">此建議僅適用於 Azure SQL 服務；不包含在虛擬機器上執行的 SQL。</span><span class="sxs-lookup"><span data-stu-id="75099-107">This recommendation applies to the Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="75099-108">本文件將使用範例部署來介紹服務。</span><span class="sxs-lookup"><span data-stu-id="75099-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="75099-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="75099-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="75099-110">實作建議</span><span class="sxs-lookup"><span data-stu-id="75099-110">Implement the recommendation</span></span>
1. <span data-ttu-id="75099-111">在 [建議] 刀鋒視窗中，選取 [啟用透明資料加密]。</span><span class="sxs-lookup"><span data-stu-id="75099-111">In the **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="75099-112">![啟用透明資料加密][1]</span><span class="sxs-lookup"><span data-stu-id="75099-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="75099-113">這會開啟 [在 SQL 資料庫上啟用透明資料加密]  刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="75099-113">This opens the **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="75099-114">選取要在其上啟用 TDE 的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="75099-114">Select a SQL database to enable TDE on.</span></span>
   <span data-ttu-id="75099-115">![選取要在其上啟用 TDE 的 SQL DB][2]</span><span class="sxs-lookup"><span data-stu-id="75099-115">![Select SQL DB to enable TDE on][2]</span></span>
3. <span data-ttu-id="75099-116">在 [透明資料加密] 刀鋒視窗中，選取 [資料加密] 下方的 [開啟]，然後選取刀鋒視窗頂端功能區中的 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="75099-116">On the **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in the top ribbon of the blade.</span></span>
   <span data-ttu-id="75099-117">![開啟 TDE][3]</span><span class="sxs-lookup"><span data-stu-id="75099-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="75099-118">一旦在所選取的 SQL Database 上啟用 TDE 後，[加密狀態] 就會變成 [已加密]。</span><span class="sxs-lookup"><span data-stu-id="75099-118">Once TDE is enabled on the selected SQL database, the **Encryption status** will change to **Encrypted**.</span></span>    

   ![加密狀態][4]

## <a name="see-also"></a><span data-ttu-id="75099-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="75099-120">See also</span></span>
<span data-ttu-id="75099-121">本文說明了如何實作資訊安全中心建議的「啟用透明資料加密」。</span><span class="sxs-lookup"><span data-stu-id="75099-121">This article showed you how to implement the Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="75099-122">如要深入了解 SQL TDE，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="75099-122">To learn more about SQL TDE, see the following:</span></span>

* [<span data-ttu-id="75099-123">Azure SQL Database 的透明資料加密</span><span class="sxs-lookup"><span data-stu-id="75099-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="75099-124">開始使用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="75099-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="75099-125">如要深入了解資訊安全中心，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="75099-125">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="75099-126">[在 Azure 資訊安全中心設定安全性原則](security-center-policies.md) --了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。</span><span class="sxs-lookup"><span data-stu-id="75099-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="75099-127">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="75099-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="75099-128">[Azure 資訊安全中心的安全性健全狀況監視](security-center-monitoring.md) -- 了解如何監視 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="75099-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="75099-129">[管理與回應 Azure 資訊安全中心的安全性警示](security-center-managing-and-responding-alerts.md) -- 了解如何管理與回應安全性警示。</span><span class="sxs-lookup"><span data-stu-id="75099-129">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="75099-130">[使用 Azure 資訊安全中心監視合作夥伴解決方案](security-center-partner-solutions.md) -- 了解如何監視合作夥伴解決方案的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="75099-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="75099-131">[Azure 資訊安全中心常見問題集](security-center-faq.md) -- 尋找有關使用服務的常見問題。</span><span class="sxs-lookup"><span data-stu-id="75099-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="75099-132">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 取得最新的 Azure 安全性新聞和資訊。</span><span class="sxs-lookup"><span data-stu-id="75099-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
