---
title: "Azure 安全性服務和技術 | Microsoft Docs"
description: "本文提供 Azure 安全性服務和技術經策劃的清單。"
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: a5a7f60a-97e2-49b4-a8c5-7c010ff27ef8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/02/2016
ms.author: yurid
ms.openlocfilehash: 0bea62a43cf6cac9132fe64f2d6c54e52def4c55
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-security-services-and-technologies"></a><span data-ttu-id="26c9a-103">Azure 安全性服務和技術</span><span class="sxs-lookup"><span data-stu-id="26c9a-103">Azure Security Services and Technologies</span></span>
<span data-ttu-id="26c9a-104">在我們與目前和未來的 Azure 客戶的討論中，我們經常被詢問「您有 Azure 提供的所有安全性相關服務和技術的清單嗎？」</span><span class="sxs-lookup"><span data-stu-id="26c9a-104">In our discussions with current and future Azure customers, we’re often asked “do you have a list of all the security related services and technologies that Azure has to offer?”</span></span>

<span data-ttu-id="26c9a-105">我們了解，當您在評估雲端服務提供者技術選項，時機適當時若有這類清單可供您用來更深入發掘會對您有幫助。</span><span class="sxs-lookup"><span data-stu-id="26c9a-105">We understand that when you’re evaluating your cloud service provider technical options, it’s helpful to have such a list available that you can use to dig down deeper when the time is right for you.</span></span>

<span data-ttu-id="26c9a-106">以下是我們提供的初步清單。</span><span class="sxs-lookup"><span data-stu-id="26c9a-106">The following is our initial effort at providing a list.</span></span> <span data-ttu-id="26c9a-107">這份清單會隨著時間變更並成長，正如同 Azure。</span><span class="sxs-lookup"><span data-stu-id="26c9a-107">Over time, this list will change and grow, just as Azure does.</span></span> <span data-ttu-id="26c9a-108">此清單經過分類，而目錄的清單也會隨著時間成長。</span><span class="sxs-lookup"><span data-stu-id="26c9a-108">The list is categorized, and the list of categories will also grow over time.</span></span> <span data-ttu-id="26c9a-109">請務必定期查看此頁面，掌握我們的安全性相關服務和技術。</span><span class="sxs-lookup"><span data-stu-id="26c9a-109">Make sure to check this page on a regular basis to stay up-to-date on our security-related services and technologies.</span></span>

## <a name="azure-security---general"></a><span data-ttu-id="26c9a-110">Azure 安全性 - 一般</span><span class="sxs-lookup"><span data-stu-id="26c9a-110">Azure Security - General</span></span>
* [<span data-ttu-id="26c9a-111">Azure 資訊安全中心</span><span class="sxs-lookup"><span data-stu-id="26c9a-111">Azure Security Center</span></span>](https://azure.microsoft.com/documentation/services/security-center/)
* [<span data-ttu-id="26c9a-112">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="26c9a-112">Azure Key Vault</span></span>](https://azure.microsoft.com/documentation/services/key-vault/)
* [<span data-ttu-id="26c9a-113">Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-113">Azure Disk Encryption</span></span>](azure-security-disk-encryption.md)
* [<span data-ttu-id="26c9a-114">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="26c9a-114">Log Analytics</span></span>](../log-analytics/log-analytics-overview.md)
* [<span data-ttu-id="26c9a-115">Azure 開發/測試實驗室</span><span class="sxs-lookup"><span data-stu-id="26c9a-115">Azure Dev/Test Labs</span></span>](https://azure.microsoft.com/documentation/services/devtest-lab/)

## <a name="azure-storage-security"></a><span data-ttu-id="26c9a-116">Azure 儲存體安全性</span><span class="sxs-lookup"><span data-stu-id="26c9a-116">Azure Storage Security</span></span>
* [<span data-ttu-id="26c9a-117">Azure 儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-117">Azure Storage Service Encryption</span></span>](../storage/common/storage-service-encryption.md)
* [<span data-ttu-id="26c9a-118">StorSimple 加密混合式儲存體</span><span class="sxs-lookup"><span data-stu-id="26c9a-118">StorSimple Encrypted Hybrid Storage</span></span>](https://azure.microsoft.com/documentation/services/storsimple/)
* [<span data-ttu-id="26c9a-119">Azure 用戶端加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-119">Azure Client-Side Encryption</span></span>](../storage/common/storage-client-side-encryption.md)
* [<span data-ttu-id="26c9a-120">Azure 儲存體共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="26c9a-120">Azure Storage Shared Access Signatures</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="26c9a-121">Azure 儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="26c9a-121">Azure Storage Account Keys</span></span>](../storage/common/storage-create-storage-account.md)
* [<span data-ttu-id="26c9a-122">採用 SMB 3.0 加密的 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="26c9a-122">Azure File shares with SMB 3.0 Encryption</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="26c9a-123">Azure 儲存體分析</span><span class="sxs-lookup"><span data-stu-id="26c9a-123">Azure Storage Analytics</span></span>](https://msdn.microsoft.com/library/hh343270.aspx)

## <a name="azure-database-security"></a><span data-ttu-id="26c9a-124">Azure 資料庫安全性</span><span class="sxs-lookup"><span data-stu-id="26c9a-124">Azure Database Security</span></span>
* [<span data-ttu-id="26c9a-125">Azure SQL 防火牆</span><span class="sxs-lookup"><span data-stu-id="26c9a-125">Azure SQL Firewall</span></span>](../sql-database/sql-database-firewall-configure.md)
* [<span data-ttu-id="26c9a-126">Azure SQL 資料格層級加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-126">Azure SQL Cell Level Encryption</span></span>](https://blogs.msdn.microsoft.com/sqlsecurity/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database/)
* [<span data-ttu-id="26c9a-127">Azure SQL 連線加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-127">Azure SQL Connection Encryption</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="26c9a-128">Azure SQL 驗證</span><span class="sxs-lookup"><span data-stu-id="26c9a-128">Azure SQL Authentication</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="26c9a-129">Azure SQL 一律加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-129">Azure SQL Always Encryption</span></span>](https://msdn.microsoft.com/library/mt163865.aspx)
* [<span data-ttu-id="26c9a-130">Azure SQL 資料行層級加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-130">Azure SQL Column Level Encryption</span></span>](https://msdn.microsoft.com/library/ms179331.aspx)
* [<span data-ttu-id="26c9a-131">Azure SQL 透明資料加密</span><span class="sxs-lookup"><span data-stu-id="26c9a-131">Azure SQL Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/dn948096.aspx)
* [<span data-ttu-id="26c9a-132">Azure SQL Database 稽核</span><span class="sxs-lookup"><span data-stu-id="26c9a-132">Azure SQL Database Auditing</span></span>](../sql-database/sql-database-auditing.md)

## <a name="azure-identity-and-access-management"></a><span data-ttu-id="26c9a-133">Azure 身分識別與存取管理</span><span class="sxs-lookup"><span data-stu-id="26c9a-133">Azure Identity and Access Management</span></span>
* [<span data-ttu-id="26c9a-134">Azure 角色型存取控制</span><span class="sxs-lookup"><span data-stu-id="26c9a-134">Azure Role Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
* [<span data-ttu-id="26c9a-135">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26c9a-135">Azure Active Directory</span></span>](../active-directory/active-directory-whatis.md)
* [<span data-ttu-id="26c9a-136">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="26c9a-136">Azure Active Directory B2C</span></span>](../active-directory-b2c/active-directory-b2c-get-started.md)
* [<span data-ttu-id="26c9a-137">Azure Active Directory 網域服務</span><span class="sxs-lookup"><span data-stu-id="26c9a-137">Azure Active Directory Domain Services</span></span>](../active-directory-domain-services/active-directory-ds-overview.md)
* [<span data-ttu-id="26c9a-138">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="26c9a-138">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="backup-and-disaster-recovery"></a><span data-ttu-id="26c9a-139">備份和災害復原</span><span class="sxs-lookup"><span data-stu-id="26c9a-139">Backup and Disaster Recovery</span></span>
* [<span data-ttu-id="26c9a-140">Azure 備份</span><span class="sxs-lookup"><span data-stu-id="26c9a-140">Azure Backup</span></span>](https://azure.microsoft.com/documentation/services/backup/)
* [<span data-ttu-id="26c9a-141">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="26c9a-141">Azure Site Recovery</span></span>](https://azure.microsoft.com/documentation/services/site-recovery/)

## <a name="azure-networking"></a><span data-ttu-id="26c9a-142">Azure 網路</span><span class="sxs-lookup"><span data-stu-id="26c9a-142">Azure Networking</span></span>
* [<span data-ttu-id="26c9a-143">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="26c9a-143">Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="26c9a-144">Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="26c9a-144">Azure VPN Gateway</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="26c9a-145">Azure 應用程式閘道</span><span class="sxs-lookup"><span data-stu-id="26c9a-145">Azure Application Gateway</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="26c9a-146">Azure 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="26c9a-146">Azure Load Balancer</span></span>](../load-balancer/load-balancer-overview.md)
* [<span data-ttu-id="26c9a-147">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="26c9a-147">Azure ExpressRoute</span></span>](../expressroute/expressroute-introduction.md)
* [<span data-ttu-id="26c9a-148">Azure 流量管理員</span><span class="sxs-lookup"><span data-stu-id="26c9a-148">Azure Traffic Manager</span></span>](../traffic-manager/traffic-manager-overview.md)
* [<span data-ttu-id="26c9a-149">Azure 應用程式 Proxy</span><span class="sxs-lookup"><span data-stu-id="26c9a-149">Azure Application Proxy</span></span>](../active-directory/active-directory-application-proxy-enable.md)
