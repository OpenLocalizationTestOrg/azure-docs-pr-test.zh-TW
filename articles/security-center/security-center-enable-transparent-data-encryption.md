---
title: "aaaEnable Azure 資訊安全中心中的透明資料加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議事項 * * 啟用透明資料加密 * *。"
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
ms.openlocfilehash: 94c6e9a1feddaa48faac6c835d416c4d131cd5c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-in-azure-security-center"></a><span data-ttu-id="af367-103">在 Azure 資訊安全中心啟用透明資料加密</span><span class="sxs-lookup"><span data-stu-id="af367-103">Enable Transparent Data Encryption in Azure Security Center</span></span>
<span data-ttu-id="af367-104">如果尚未啟用 TDE，Azure 資訊安全中心將建議您在 SQL Database 上啟用透明資料加密 (TDE)。</span><span class="sxs-lookup"><span data-stu-id="af367-104">Azure Security Center will recommend that you enable Transparent Data Encryption (TDE) on SQL databases if TDE is not already enabled.</span></span> <span data-ttu-id="af367-105">TDE 會保護資料，並協助您符合法規遵循需求加密資料庫、 相關聯的備份以及交易記錄檔，在其餘部分，而不需要變更 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="af367-105">TDE protects your data and helps you meet compliance requirements by encrypting your database, associated backups, and transaction log files at rest, without requiring changes tooyour application.</span></span> <span data-ttu-id="af367-106">toolearn 更看到[Azure SQL Database 的透明資料加密](https://msdn.microsoft.com/library/dn948096)。</span><span class="sxs-lookup"><span data-stu-id="af367-106">toolearn more see [Transparent Data Encryption with Azure SQL Database](https://msdn.microsoft.com/library/dn948096).</span></span>

<span data-ttu-id="af367-107">這項建議適用於 toohello; 僅限 Azure SQL 服務不包含 SQL 虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="af367-107">This recommendation applies toohello Azure SQL service only; doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="af367-108">本文件介紹 hello 服務使用的範例部署。</span><span class="sxs-lookup"><span data-stu-id="af367-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="af367-109">這不是逐步指南。</span><span class="sxs-lookup"><span data-stu-id="af367-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="af367-110">實作 hello 建議</span><span class="sxs-lookup"><span data-stu-id="af367-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="af367-111">在 hello**建議**刀鋒視窗中，選取**啟用透明資料加密**。</span><span class="sxs-lookup"><span data-stu-id="af367-111">In hello **Recommendations** blade, select **Enable Transparent Data Encryption**.</span></span>
   <span data-ttu-id="af367-112">![啟用透明資料加密][1]</span><span class="sxs-lookup"><span data-stu-id="af367-112">![Enable Transparent Data Encryption][1]</span></span>
2. <span data-ttu-id="af367-113">這會開啟 hello **SQL 資料庫上啟用透明資料加密**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="af367-113">This opens hello **Enable Transparent Data Encryption on SQL databases** blade.</span></span> <span data-ttu-id="af367-114">選取上的 SQL 資料庫 tooenable TDE。</span><span class="sxs-lookup"><span data-stu-id="af367-114">Select a SQL database tooenable TDE on.</span></span>
   <span data-ttu-id="af367-115">![選取上的 SQL DB tooenable TDE][2]</span><span class="sxs-lookup"><span data-stu-id="af367-115">![Select SQL DB tooenable TDE on][2]</span></span>
3. <span data-ttu-id="af367-116">在 [hello**透明資料加密**刀鋒視窗中，選取**ON**下資料加密，然後選取**儲存**hello hello] 刀鋒視窗的頂端功能區中。</span><span class="sxs-lookup"><span data-stu-id="af367-116">On hello **Transparent data encryption** blade, select **ON** under Data encryption and select **Save** in hello top ribbon of hello blade.</span></span>
   <span data-ttu-id="af367-117">![開啟 TDE][3]</span><span class="sxs-lookup"><span data-stu-id="af367-117">![Turn on TDE][3]</span></span>

   <span data-ttu-id="af367-118">一旦啟用了 TDE hello 選取 SQL 資料庫 hello**加密狀態**也會變更**加密**。</span><span class="sxs-lookup"><span data-stu-id="af367-118">Once TDE is enabled on hello selected SQL database, hello **Encryption status** will change too**Encrypted**.</span></span>    

   ![加密狀態][4]

## <a name="see-also"></a><span data-ttu-id="af367-120">另請參閱</span><span class="sxs-lookup"><span data-stu-id="af367-120">See also</span></span>
<span data-ttu-id="af367-121">本文章向您說明如何 tooimplement 會 hello 資訊安全中心建議 「 啟用透明資料加密 」。</span><span class="sxs-lookup"><span data-stu-id="af367-121">This article showed you how tooimplement hello Security Center recommendation "Enable Transparent Data Encryption."</span></span> <span data-ttu-id="af367-122">toolearn 深入了解 SQL TDE，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="af367-122">toolearn more about SQL TDE, see hello following:</span></span>

* [<span data-ttu-id="af367-123">Azure SQL Database 的透明資料加密</span><span class="sxs-lookup"><span data-stu-id="af367-123">Transparent Data Encryption with Azure SQL Database</span></span>](https://msdn.microsoft.com/library/dn948096)
* [<span data-ttu-id="af367-124">開始使用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="af367-124">Get started with Transparent Data Encryption (TDE)</span></span>](../sql-data-warehouse/sql-data-warehouse-encryption-tde.md)

<span data-ttu-id="af367-125">toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="af367-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="af367-126">[在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="af367-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="af367-127">[管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="af367-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="af367-128">[在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。</span><span class="sxs-lookup"><span data-stu-id="af367-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="af367-129">[在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。</span><span class="sxs-lookup"><span data-stu-id="af367-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="af367-130">[監視與 Azure 資訊安全中心的協力廠商解決方案](security-center-partner-solutions.md)-了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="af367-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="af367-131">[Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。</span><span class="sxs-lookup"><span data-stu-id="af367-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="af367-132">[Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/)-取得最新 Azure 安全性消息 hello 和資訊。</span><span class="sxs-lookup"><span data-stu-id="af367-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-tde-on-sql-databases/enable-tde.png
[2]:./media/security-center-enable-tde-on-sql-databases/transparent-data-encryption-blade.png
[3]: ./media/security-center-enable-tde-on-sql-databases/turn-on-tde.png
[4]: ./media/security-center-enable-tde-on-sql-databases/encrypted.png
