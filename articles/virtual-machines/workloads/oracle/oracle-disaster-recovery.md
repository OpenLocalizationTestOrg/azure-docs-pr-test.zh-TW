---
title: "Azure 環境中的 Oracle 嚴重損壞修復案例的 aaaOverview |Microsoft 文件"
description: "Azure 環境中 Oracle Database 12c 資料庫的災害復原案例"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="b2d2c-103">Azure 環境中 Oracle Database 12c 資料庫的災害復原</span><span class="sxs-lookup"><span data-stu-id="b2d2c-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="b2d2c-104">假設</span><span class="sxs-lookup"><span data-stu-id="b2d2c-104">Assumptions</span></span>

- <span data-ttu-id="b2d2c-105">您已了解 Oracle Data Guard 的設計和 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="b2d2c-106">目標</span><span class="sxs-lookup"><span data-stu-id="b2d2c-106">Goals</span></span>
- <span data-ttu-id="b2d2c-107">設計 hello 拓撲和組態，您的需求災害復原 (DR)。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-107">Design hello topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="b2d2c-108">案例 1：Azure 上的主要和 DR 站台</span><span class="sxs-lookup"><span data-stu-id="b2d2c-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="b2d2c-109">客戶擁有 Oracle 資料庫設定 hello 主要站台上。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-109">A customer has an Oracle database set up on hello primary site.</span></span> <span data-ttu-id="b2d2c-110">DR 站台位於不同的區域中。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-110">A DR site is in a different region.</span></span> <span data-ttu-id="b2d2c-111">hello 客戶可使用 Oracle 資料保護這些站台間快速復原。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-111">hello customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="b2d2c-112">hello 主要站台也會有次要資料庫以進行報告和其他用途。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-112">hello primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="b2d2c-113">拓撲</span><span class="sxs-lookup"><span data-stu-id="b2d2c-113">Topology</span></span>

<span data-ttu-id="b2d2c-114">Hello Azure 安裝程式的摘要如下：</span><span class="sxs-lookup"><span data-stu-id="b2d2c-114">Here is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="b2d2c-115">兩個站台 (主要站台和 DR 站台)</span><span class="sxs-lookup"><span data-stu-id="b2d2c-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="b2d2c-116">兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-116">Two virtual networks</span></span>
- <span data-ttu-id="b2d2c-117">兩個具有 Data Guard 的 Oracle 資料庫 (主要和待命)</span><span class="sxs-lookup"><span data-stu-id="b2d2c-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="b2d2c-118">兩個具有 Golden Gate 或 Data Guard 的 Oracle 資料庫 (僅限主要站台)</span><span class="sxs-lookup"><span data-stu-id="b2d2c-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="b2d2c-119">兩個應用程式服務，一個主要，一個 hello DR 網站上</span><span class="sxs-lookup"><span data-stu-id="b2d2c-119">Two application services, one primary and one on hello DR site</span></span>
- <span data-ttu-id="b2d2c-120">*可用性設定組，*用 hello 主要站台上的資料庫和應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b2d2c-120">An *availability set,* which is used for database and application service on hello primary site</span></span>
- <span data-ttu-id="b2d2c-121">在每個站台，這會限制存取 toohello 私人網路，並只讓登入系統管理員一個 jumpbox</span><span class="sxs-lookup"><span data-stu-id="b2d2c-121">One jumpbox on each site, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="b2d2c-122">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="b2d2c-123">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="b2d2c-123">NSG enforced on application and database subnets</span></span>

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="b2d2c-125">案例 2：內部部署環境的主要站台和 Azure 上的 DR 站台</span><span class="sxs-lookup"><span data-stu-id="b2d2c-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="b2d2c-126">客戶具有內部部署 Oracle 資料庫設定 (主要站台)。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="b2d2c-127">DR 站台是在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-127">A DR site is on Azure.</span></span> <span data-ttu-id="b2d2c-128">Oracle Data Guard 用於這些站台間的快速復原。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="b2d2c-129">hello 主要站台也會有次要資料庫以進行報告和其他用途。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-129">hello primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="b2d2c-130">這項設定有兩種方法。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a><span data-ttu-id="b2d2c-131">方法 1： 在內部部署與 Azure，需要 hello 防火牆上的開啟 TCP 連接埠之間的直接連接</span><span class="sxs-lookup"><span data-stu-id="b2d2c-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on hello firewall</span></span> 

<span data-ttu-id="b2d2c-132">我們不建議直接連接，因為其會公開外部 world hello TCP 連接埠 toohello。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-132">We don't recommend direct connections because they expose hello TCP ports toohello outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="b2d2c-133">拓撲</span><span class="sxs-lookup"><span data-stu-id="b2d2c-133">Topology</span></span>

<span data-ttu-id="b2d2c-134">以下是 hello Azure 安裝程式的摘要：</span><span class="sxs-lookup"><span data-stu-id="b2d2c-134">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="b2d2c-135">一個 DR 站台</span><span class="sxs-lookup"><span data-stu-id="b2d2c-135">One DR site</span></span> 
- <span data-ttu-id="b2d2c-136">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-136">One virtual network</span></span>
- <span data-ttu-id="b2d2c-137">一個具有 Data Guard 的 Oracle 資料庫 (使用中)</span><span class="sxs-lookup"><span data-stu-id="b2d2c-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="b2d2c-138">Hello DR 網站上的一個應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b2d2c-138">One application service on hello DR site</span></span>
- <span data-ttu-id="b2d2c-139">一個 jumpbox，這會限制存取 toohello 私人網路，並只讓登入系統管理員</span><span class="sxs-lookup"><span data-stu-id="b2d2c-139">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="b2d2c-140">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="b2d2c-141">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="b2d2c-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="b2d2c-142">NSG 規則原則/tooallow 輸入 TCP 連接埠 1521年 （或使用者定義的連接埠）</span><span class="sxs-lookup"><span data-stu-id="b2d2c-142">An NSG policy/rule tooallow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="b2d2c-143">NSG 規則原則/toorestrict 只有 hello IP 位址/位址在內部部署 （資料庫或應用程式） tooaccess hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-143">An NSG policy/rule toorestrict only hello IP address/addresses on-premises (DB or application) tooaccess hello virtual network</span></span>

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="b2d2c-145">方法 2：站對站 VPN</span><span class="sxs-lookup"><span data-stu-id="b2d2c-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="b2d2c-146">站對站 VPN 是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="b2d2c-147">如需設定 VPN 的詳細資訊，請參閱[使用 CLI 建立具有站對站 VPN 連線的虛擬網路](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。</span><span class="sxs-lookup"><span data-stu-id="b2d2c-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="b2d2c-148">拓撲</span><span class="sxs-lookup"><span data-stu-id="b2d2c-148">Topology</span></span>

<span data-ttu-id="b2d2c-149">以下是 hello Azure 安裝程式的摘要：</span><span class="sxs-lookup"><span data-stu-id="b2d2c-149">Following is a summary of hello Azure setup:</span></span>

- <span data-ttu-id="b2d2c-150">一個 DR 站台</span><span class="sxs-lookup"><span data-stu-id="b2d2c-150">One DR site</span></span> 
- <span data-ttu-id="b2d2c-151">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-151">One virtual network</span></span> 
- <span data-ttu-id="b2d2c-152">一個具有 Data Guard 的 Oracle 資料庫 (使用中)</span><span class="sxs-lookup"><span data-stu-id="b2d2c-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="b2d2c-153">Hello DR 網站上的一個應用程式服務</span><span class="sxs-lookup"><span data-stu-id="b2d2c-153">One application service on hello DR site</span></span>
- <span data-ttu-id="b2d2c-154">一個 jumpbox，這會限制存取 toohello 私人網路，並只讓登入系統管理員</span><span class="sxs-lookup"><span data-stu-id="b2d2c-154">One jumpbox, which restricts access toohello private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="b2d2c-155">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="b2d2c-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="b2d2c-156">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="b2d2c-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="b2d2c-157">內部部署與 Azure 之間的站對站 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="b2d2c-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![Hello DR 拓樸 頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="b2d2c-159">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="b2d2c-159">Additional reading</span></span>

- [<span data-ttu-id="b2d2c-160">在 Azure 上設計和實作 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="b2d2c-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="b2d2c-161">設定 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="b2d2c-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="b2d2c-162">設定 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="b2d2c-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="b2d2c-163">Oracle 備份和復原</span><span class="sxs-lookup"><span data-stu-id="b2d2c-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="b2d2c-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b2d2c-164">Next steps</span></span>

- [<span data-ttu-id="b2d2c-165">教學課程︰建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="b2d2c-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="b2d2c-166">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="b2d2c-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
