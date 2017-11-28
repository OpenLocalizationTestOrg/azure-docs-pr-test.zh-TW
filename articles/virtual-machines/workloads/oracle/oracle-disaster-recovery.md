---
title: "Azure 環境中的 Oracle 災害復原案例概觀 | Microsoft Docs"
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
ms.openlocfilehash: f17ebb2b74cd7ad872f88483ed7cdb4f239ee069
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a><span data-ttu-id="8e4bc-103">Azure 環境中 Oracle Database 12c 資料庫的災害復原</span><span class="sxs-lookup"><span data-stu-id="8e4bc-103">Disaster recovery for an Oracle Database 12c database in an Azure environment</span></span>

## <a name="assumptions"></a><span data-ttu-id="8e4bc-104">假設</span><span class="sxs-lookup"><span data-stu-id="8e4bc-104">Assumptions</span></span>

- <span data-ttu-id="8e4bc-105">您已了解 Oracle Data Guard 的設計和 Azure 環境。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-105">You have an understanding of Oracle Data Guard design and Azure environments.</span></span>


## <a name="goals"></a><span data-ttu-id="8e4bc-106">目標</span><span class="sxs-lookup"><span data-stu-id="8e4bc-106">Goals</span></span>
- <span data-ttu-id="8e4bc-107">設計符合您災害復原 (DR) 需求的拓撲和設定。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-107">Design the topology and configuration that meet your disaster recovery (DR) requirements.</span></span>

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a><span data-ttu-id="8e4bc-108">案例 1：Azure 上的主要和 DR 站台</span><span class="sxs-lookup"><span data-stu-id="8e4bc-108">Scenario 1: Primary and DR sites on Azure</span></span>

<span data-ttu-id="8e4bc-109">客戶將 Oracle 資料庫設定在主要站台上。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-109">A customer has an Oracle database set up on the primary site.</span></span> <span data-ttu-id="8e4bc-110">DR 站台位於不同的區域中。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-110">A DR site is in a different region.</span></span> <span data-ttu-id="8e4bc-111">客戶使用 Oracle Data Guard 在這些站台間快速地進行復原。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-111">The customer uses Oracle Data Guard for quick recovery between these sites.</span></span> <span data-ttu-id="8e4bc-112">主要站台另外還擁有次要資料庫以供進行報告和其他用途。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-112">The primary site also has a secondary database for reporting and other uses.</span></span> 

### <a name="topology"></a><span data-ttu-id="8e4bc-113">拓撲</span><span class="sxs-lookup"><span data-stu-id="8e4bc-113">Topology</span></span>

<span data-ttu-id="8e4bc-114">以下是 Azure 設定的摘要：</span><span class="sxs-lookup"><span data-stu-id="8e4bc-114">Here is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e4bc-115">兩個站台 (主要站台和 DR 站台)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-115">Two sites (a primary site and a DR site)</span></span>
- <span data-ttu-id="8e4bc-116">兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-116">Two virtual networks</span></span>
- <span data-ttu-id="8e4bc-117">兩個具有 Data Guard 的 Oracle 資料庫 (主要和待命)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-117">Two Oracle databases with Data Guard (primary and standby)</span></span>
- <span data-ttu-id="8e4bc-118">兩個具有 Golden Gate 或 Data Guard 的 Oracle 資料庫 (僅限主要站台)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-118">Two Oracle databases with Golden Gate or Data Guard (primary site only)</span></span>
- <span data-ttu-id="8e4bc-119">兩個應用程式服務，一個在主要站台上，一個在 DR 站台上</span><span class="sxs-lookup"><span data-stu-id="8e4bc-119">Two application services, one primary and one on the DR site</span></span>
- <span data-ttu-id="8e4bc-120">一個可用性設定組，用於主要站台上的資料庫和應用程式服務</span><span class="sxs-lookup"><span data-stu-id="8e4bc-120">An *availability set,* which is used for database and application service on the primary site</span></span>
- <span data-ttu-id="8e4bc-121">每個站台上有一個 Jumpbox，其只能存取私人網路，並只允許系統管理員登入</span><span class="sxs-lookup"><span data-stu-id="8e4bc-121">One jumpbox on each site, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e4bc-122">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-122">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e4bc-123">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="8e4bc-123">NSG enforced on application and database subnets</span></span>

![DR 拓撲頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a><span data-ttu-id="8e4bc-125">案例 2：內部部署環境的主要站台和 Azure 上的 DR 站台</span><span class="sxs-lookup"><span data-stu-id="8e4bc-125">Scenario 2: Primary site on-premises and DR site on Azure</span></span>

<span data-ttu-id="8e4bc-126">客戶具有內部部署 Oracle 資料庫設定 (主要站台)。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-126">A customer has an on-premises Oracle database setup (primary site).</span></span> <span data-ttu-id="8e4bc-127">DR 站台是在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-127">A DR site is on Azure.</span></span> <span data-ttu-id="8e4bc-128">Oracle Data Guard 用於這些站台間的快速復原。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-128">Oracle Data Guard is used for quick recovery between these sites.</span></span> <span data-ttu-id="8e4bc-129">主要站台另外還擁有次要資料庫以供進行報告和其他用途。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-129">The primary site also has a secondary database for reporting and other uses.</span></span> 

<span data-ttu-id="8e4bc-130">這項設定有兩種方法。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-130">There are two approaches for this setup.</span></span>

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-the-firewall"></a><span data-ttu-id="8e4bc-131">方法 1：讓內部部署環境與 Azure 直接連線，此方法需要在防火牆上開啟 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="8e4bc-131">Approach 1: Direct connections between on-premises and Azure, requiring open TCP ports on the firewall</span></span> 

<span data-ttu-id="8e4bc-132">不建議直接連線，因為這些連線會將 TCP 連接埠對外公開。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-132">We don't recommend direct connections because they expose the TCP ports to the outside world.</span></span>

#### <a name="topology"></a><span data-ttu-id="8e4bc-133">拓撲</span><span class="sxs-lookup"><span data-stu-id="8e4bc-133">Topology</span></span>

<span data-ttu-id="8e4bc-134">以下是 Azure 設定的摘要：</span><span class="sxs-lookup"><span data-stu-id="8e4bc-134">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e4bc-135">一個 DR 站台</span><span class="sxs-lookup"><span data-stu-id="8e4bc-135">One DR site</span></span> 
- <span data-ttu-id="8e4bc-136">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-136">One virtual network</span></span>
- <span data-ttu-id="8e4bc-137">一個具有 Data Guard 的 Oracle 資料庫 (使用中)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-137">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e4bc-138">DR 站台上的一個應用程式服務</span><span class="sxs-lookup"><span data-stu-id="8e4bc-138">One application service on the DR site</span></span>
- <span data-ttu-id="8e4bc-139">一個 Jumpbox，其只能存取私人網路，並只允許系統管理員登入</span><span class="sxs-lookup"><span data-stu-id="8e4bc-139">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e4bc-140">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-140">A jumpbox, application service, database, and VPN gateway on separate subnets</span></span>
- <span data-ttu-id="8e4bc-141">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="8e4bc-141">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e4bc-142">NSG 原則/規則，以允許輸入 TCP 連接埠 1521 (或使用者定義的連接埠)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-142">An NSG policy/rule to allow inbound TCP port 1521 (or a user-defined port)</span></span>
- <span data-ttu-id="8e4bc-143">NSG 原則/規則，以便限制只有內部部署 IP 位址 (DB 或應用程式) 可以存取虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-143">An NSG policy/rule to restrict only the IP address/addresses on-premises (DB or application) to access the virtual network</span></span>

![DR 拓撲頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a><span data-ttu-id="8e4bc-145">方法 2：站對站 VPN</span><span class="sxs-lookup"><span data-stu-id="8e4bc-145">Approach 2: Site-to-site VPN</span></span>
<span data-ttu-id="8e4bc-146">站對站 VPN 是更好的方法。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-146">Site-to-site VPN is a better approach.</span></span> <span data-ttu-id="8e4bc-147">如需設定 VPN 的詳細資訊，請參閱[使用 CLI 建立具有站對站 VPN 連線的虛擬網路](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。</span><span class="sxs-lookup"><span data-stu-id="8e4bc-147">For more information about setting up a VPN, see [Create a virtual network with a Site-to-Site VPN connection using CLI](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span>

#### <a name="topology"></a><span data-ttu-id="8e4bc-148">拓撲</span><span class="sxs-lookup"><span data-stu-id="8e4bc-148">Topology</span></span>

<span data-ttu-id="8e4bc-149">以下是 Azure 設定的摘要：</span><span class="sxs-lookup"><span data-stu-id="8e4bc-149">Following is a summary of the Azure setup:</span></span>

- <span data-ttu-id="8e4bc-150">一個 DR 站台</span><span class="sxs-lookup"><span data-stu-id="8e4bc-150">One DR site</span></span> 
- <span data-ttu-id="8e4bc-151">一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-151">One virtual network</span></span> 
- <span data-ttu-id="8e4bc-152">一個具有 Data Guard 的 Oracle 資料庫 (使用中)</span><span class="sxs-lookup"><span data-stu-id="8e4bc-152">One Oracle database with Data Guard (active)</span></span>
- <span data-ttu-id="8e4bc-153">DR 站台上的一個應用程式服務</span><span class="sxs-lookup"><span data-stu-id="8e4bc-153">One application service on the DR site</span></span>
- <span data-ttu-id="8e4bc-154">一個 Jumpbox，其只能存取私人網路，並只允許系統管理員登入</span><span class="sxs-lookup"><span data-stu-id="8e4bc-154">One jumpbox, which restricts access to the private network and only allows sign-in by an administrator</span></span>
- <span data-ttu-id="8e4bc-155">Jumpbox、應用程式服務、資料庫和 VPN 閘道位於不同的子網路</span><span class="sxs-lookup"><span data-stu-id="8e4bc-155">A jumpbox, application service, database, and VPN gateway are on separate subnets</span></span>
- <span data-ttu-id="8e4bc-156">對應用程式和資料庫子網路強制執行 NSG</span><span class="sxs-lookup"><span data-stu-id="8e4bc-156">NSG enforced on application and database subnets</span></span>
- <span data-ttu-id="8e4bc-157">內部部署與 Azure 之間的站對站 VPN 連線</span><span class="sxs-lookup"><span data-stu-id="8e4bc-157">Site-to-site VPN connection between on-premises and Azure</span></span>

![DR 拓撲頁面的螢幕擷取畫面](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a><span data-ttu-id="8e4bc-159">其他閱讀資料</span><span class="sxs-lookup"><span data-stu-id="8e4bc-159">Additional reading</span></span>

- [<span data-ttu-id="8e4bc-160">在 Azure 上設計和實作 Oracle 資料庫</span><span class="sxs-lookup"><span data-stu-id="8e4bc-160">Design and implement an Oracle database on Azure</span></span>](oracle-design.md)
- [<span data-ttu-id="8e4bc-161">設定 Oracle Data Guard</span><span class="sxs-lookup"><span data-stu-id="8e4bc-161">Configure Oracle Data Guard</span></span>](configure-oracle-dataguard.md)
- [<span data-ttu-id="8e4bc-162">設定 Oracle Golden Gate</span><span class="sxs-lookup"><span data-stu-id="8e4bc-162">Configure Oracle Golden Gate</span></span>](configure-oracle-golden-gate.md)
- [<span data-ttu-id="8e4bc-163">Oracle 備份和復原</span><span class="sxs-lookup"><span data-stu-id="8e4bc-163">Oracle backup and recovery</span></span>](oracle-backup-recovery.md)


## <a name="next-steps"></a><span data-ttu-id="8e4bc-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8e4bc-164">Next steps</span></span>

- [<span data-ttu-id="8e4bc-165">教學課程︰建立高可用性 VM</span><span class="sxs-lookup"><span data-stu-id="8e4bc-165">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)
- [<span data-ttu-id="8e4bc-166">瀏覽 VM 部署 Azure CLI 範例</span><span class="sxs-lookup"><span data-stu-id="8e4bc-166">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
