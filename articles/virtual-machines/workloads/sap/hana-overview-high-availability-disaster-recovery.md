---
title: "在 Azure （大型執行個體） 上的 SAP HANA 的 aaaHigh 可用性和災害復原 |Microsoft 文件"
description: "建立高可用性並為 SAP HANA on Azure (大型執行個體) 的災害復原做規劃。"
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0967f54cf29bbb275eb7cda9d36608488add9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-high-availability-and-disaster-recovery-on-azure"></a><span data-ttu-id="72dcd-103">SAP Hana (大型執行個體) 在 Azure 上的高可用性和災害復原</span><span class="sxs-lookup"><span data-stu-id="72dcd-103">SAP HANA (large instances) high availability and disaster recovery on Azure</span></span> 

<span data-ttu-id="72dcd-104">高可用性和災害復原對執行具任務關鍵性的 SAP HANA on Azure (大型執行個體) 伺服器來說，是相當重要的層面。</span><span class="sxs-lookup"><span data-stu-id="72dcd-104">High availability and disaster recovery are important aspects of running your mission-critical SAP HANA on Azure (large instances) servers.</span></span> <span data-ttu-id="72dcd-105">它的重要 toowork 與 SAP、 系統整合者，或 Microsoft tooproperly 架構設計和實作 hello 右高的可用性/災害復原策略。</span><span class="sxs-lookup"><span data-stu-id="72dcd-105">It's important toowork with SAP, your system integrator, or Microsoft tooproperly architect and implement hello right high-availability/disaster-recovery strategy.</span></span> <span data-ttu-id="72dcd-106">它也是重要的 tooconsider hello 復原點目標和復原時間目標，也就是特定 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="72dcd-106">It is also important tooconsider hello recovery point objective and recovery time objective, which are specific tooyour environment.</span></span>

## <a name="high-availability"></a><span data-ttu-id="72dcd-107">高可用性</span><span class="sxs-lookup"><span data-stu-id="72dcd-107">High availability</span></span>

<span data-ttu-id="72dcd-108">Microsoft 支援 SAP HANA 高可用性方法 「 現成的 hello，"包括：</span><span class="sxs-lookup"><span data-stu-id="72dcd-108">Microsoft supports SAP HANA high-availability methods "out of hello box," which include:</span></span>

- <span data-ttu-id="72dcd-109">**儲存體複寫：** hello 儲存系統的能力 tooreplicate 所有資料 tooanother 位置 (內或分開，都 hello 相同的資料中心)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-109">**Storage replication:** hello storage system's ability tooreplicate all data tooanother location (within, or separate from, hello same datacenter).</span></span> <span data-ttu-id="72dcd-110">SAP HANA 獨立運作，不依賴此方法。</span><span class="sxs-lookup"><span data-stu-id="72dcd-110">SAP HANA operates independently of this method.</span></span>
- <span data-ttu-id="72dcd-111">**HANA 系統複寫：** hello SAP HANA tooa 不同 SAP HANA 系統中的所有資料複寫。</span><span class="sxs-lookup"><span data-stu-id="72dcd-111">**HANA system replication:** hello replication of all data in SAP HANA tooa separate SAP HANA system.</span></span> <span data-ttu-id="72dcd-112">hello 復原時間目標是透過資料複寫的固定間隔最小化。</span><span class="sxs-lookup"><span data-stu-id="72dcd-112">hello recovery time objective is minimized through data replication at regular intervals.</span></span> <span data-ttu-id="72dcd-113">SAP HANA 支援非同步、 同步在記憶體和同步模式 (僅建議用於 SAP HANA 系統內 hello 相同的資料中心或小於 100 KM 分開的)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-113">SAP HANA supports asynchronous, synchronous in-memory, and synchronous modes (recommended only for SAP HANA systems that are within hello same datacenter or less than 100 KM apart).</span></span> <span data-ttu-id="72dcd-114">HANA 大型執行個體戳記 hello 目前設計，HANA 系統複寫可用於僅限高可用性。</span><span class="sxs-lookup"><span data-stu-id="72dcd-114">In hello current design of HANA large-instance stamps, HANA system replication can be used for high availability only.</span></span>
- <span data-ttu-id="72dcd-115">**裝載自動容錯移轉：**替代 toosystem 複寫為本機的錯誤復原方案 toouse。</span><span class="sxs-lookup"><span data-stu-id="72dcd-115">**Host auto-failover:** A local fault-recovery solution toouse as an alternative toosystem replication.</span></span> <span data-ttu-id="72dcd-116">Hello 主要節點無法使用時，會在向外延展模式設定一或多個待命的 SAP HANA 節點和 SAP HANA 自動容錯移轉 tooanother 節點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-116">When hello master node becomes unavailable, one or more standby SAP HANA nodes are configured in scale-out mode and SAP HANA automatically fails over tooanother node.</span></span>

<span data-ttu-id="72dcd-117">如需有關 SAP HANA 高可用性的詳細資訊，請參閱下列 SAP 資訊 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-117">For more information on SAP HANA high availability, see hello following SAP information:</span></span>

- [<span data-ttu-id="72dcd-118">SAP HANA 高可用性白皮書</span><span class="sxs-lookup"><span data-stu-id="72dcd-118">SAP HANA High-Availability Whitepaper</span></span>](http://go.sap.com/documents/2016/05/f8e5eeba-737c-0010-82c7-eda71af511fa.html)
- [<span data-ttu-id="72dcd-119">SAP HANA 管理指南</span><span class="sxs-lookup"><span data-stu-id="72dcd-119">SAP HANA Administration Guide</span></span>](http://help.sap.com/hana/SAP_HANA_Administration_Guide_en.pdf)
- [<span data-ttu-id="72dcd-120">SAP Academy 的 SAP HANA 系統複寫影片</span><span class="sxs-lookup"><span data-stu-id="72dcd-120">SAP Academy Video on SAP HANA System Replication</span></span>](http://scn.sap.com/community/hana-in-memory/blog/2015/05/19/sap-hana-system-replication)
- [<span data-ttu-id="72dcd-121">SAP 支援附註 #1999880 - SAP HANA 系統複寫常見問題集</span><span class="sxs-lookup"><span data-stu-id="72dcd-121">SAP Support Note #1999880 – FAQ on SAP HANA System Replication</span></span>](https://bcs.wdf.sap.corp/sap/support/notes/1999880)
- <span data-ttu-id="72dcd-122">[SAP 支援附註 #2165547 - SAP HANA 系統複寫環境內的 SAP HANA 備份與還原](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span><span class="sxs-lookup"><span data-stu-id="72dcd-122">[SAP Support Note #2165547 – SAP HANA Backup and Restore within SAP HANA System Replication Environment](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3231363535343726)</span></span>
- <span data-ttu-id="72dcd-123">[SAP 支援附註 #1984882 - 使用 SAP HANA 系統複寫以最短/零停機時間的方式進行硬體交換](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span><span class="sxs-lookup"><span data-stu-id="72dcd-123">[SAP Support Note #1984882 – Using SAP HANA System Replication for Hardware Exchange with Minimum/Zero Downtime](https://websmp230.sap-ag.de/sap(bD1lbiZjPTAwMQ==)/bc/bsp/sno/ui_entry/entry.htm?param=69765F6D6F64653D3030312669765F7361706E6F7465735F6E756D6265723D3139383438383226)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="72dcd-124">災害復原</span><span class="sxs-lookup"><span data-stu-id="72dcd-124">Disaster recovery</span></span>

<span data-ttu-id="72dcd-125">在一個地緣政治區域的兩個 Azure 區域中提供 SAP HANA on Azure (大型執行個體)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-125">SAP HANA on Azure (large instances) is offered in two Azure regions in a geopolitical region.</span></span> <span data-ttu-id="72dcd-126">介於兩個不同區域的 hello 兩個大型執行個體戳記是嚴重損壞修復期間，複寫資料的直接連線。</span><span class="sxs-lookup"><span data-stu-id="72dcd-126">Between hello two large-instance stamps of two different regions is a direct network connectivity for replicating data during disaster recovery.</span></span> <span data-ttu-id="72dcd-127">hello 複寫 hello 資料是儲存體基礎結構基礎。</span><span class="sxs-lookup"><span data-stu-id="72dcd-127">hello replication of hello data is storage-infrastructure based.</span></span> <span data-ttu-id="72dcd-128">依預設不進行 hello 複寫。</span><span class="sxs-lookup"><span data-stu-id="72dcd-128">hello replication is not done by default.</span></span> <span data-ttu-id="72dcd-129">它是基於排序 hello 嚴重損壞修復的 hello 客戶組態。</span><span class="sxs-lookup"><span data-stu-id="72dcd-129">It is done for hello customer configurations that ordered hello disaster recovery.</span></span> <span data-ttu-id="72dcd-130">在目前的設計，hello HANA 系統複寫不用於災害復原。</span><span class="sxs-lookup"><span data-stu-id="72dcd-130">In hello current design, HANA system replication can't be used for disaster recovery.</span></span>

<span data-ttu-id="72dcd-131">不過，tootake 利用 hello 災害復原時，您需要 toostart toodesign hello 網路連線 toohello 兩個不同的 Azure 地區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-131">However, tootake advantage of hello disaster recovery, you need toostart toodesign hello network connectivity toohello two different Azure regions.</span></span> <span data-ttu-id="72dcd-132">toodo 因此，您需要從內部部署的 Azure ExpressRoute 電路連接您的主要 Azure 地區和在內部部署 tooyour 嚴重損壞修復區域中的另一個循環連接中。</span><span class="sxs-lookup"><span data-stu-id="72dcd-132">toodo so, you need an Azure ExpressRoute circuit connection from on-premises in your main Azure region and another circuit connection from on-premises tooyour disaster-recovery region.</span></span> <span data-ttu-id="72dcd-133">此措施可解決整個 Azure 區域 (包含 Microsoft Enterprise Edge (MSEE) 路由器位置) 發生問題的情況。</span><span class="sxs-lookup"><span data-stu-id="72dcd-133">This measure would cover a situation in which a complete Azure region, including a Microsoft enterprise edge router (MSEE) location, has an issue.</span></span>

<span data-ttu-id="72dcd-134">做為第二個量值，您可以連接連接 tooSAP HANA Azure （大型執行個體） 上的所有 Azure 虛擬網路中的 hello 區域 tooboth 這些 ExpressRoute 電路的其中一個。</span><span class="sxs-lookup"><span data-stu-id="72dcd-134">As a second measure, you can connect all Azure virtual networks that connect tooSAP HANA on Azure (large instances) in one of hello regions tooboth of those ExpressRoute circuits.</span></span> <span data-ttu-id="72dcd-135">此量值說明的案例，下班，只有其中一個 hello MSEE 位置與 Azure 連線在內部部署位置的地方。</span><span class="sxs-lookup"><span data-stu-id="72dcd-135">This measure addresses a case where only one of hello MSEE locations that connects your on-premises location with Azure goes off duty.</span></span>

<span data-ttu-id="72dcd-136">hello 下圖顯示 hello 災害復原的最佳組態：</span><span class="sxs-lookup"><span data-stu-id="72dcd-136">hello following figure shows hello optimal configuration for disaster recovery:</span></span>

![災害復原的最佳組態](./media/hana-overview-high-availability-disaster-recovery/image1-optimal-configuration.png)

<span data-ttu-id="72dcd-138">hello 的 hello 網路的災害復原設定的最佳狀況會從內部部署 toohello 兩個不同的 Azure 地區 toohave 兩個 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="72dcd-138">hello optimal case for a disaster-recovery configuration of hello network is toohave two ExpressRoute circuits from on-premises toohello two different Azure regions.</span></span> <span data-ttu-id="72dcd-139">一個循環會 tooregion #1 執行的實際執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-139">One circuit goes tooregion #1, running a production instance.</span></span> <span data-ttu-id="72dcd-140">第二個 ExpressRoute 電路 hello 進入 tooregion #2 中，執行某些非生產 HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-140">hello second ExpressRoute circuit goes tooregion #2, running some non-production HANA instances.</span></span> <span data-ttu-id="72dcd-141">（這是重要事項如果整個 Azure 地區，包括 hello MSEE 和大型執行個體的戳記，會關閉 hello 方格）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-141">(This is important if an entire Azure region, including hello MSEE and large-instance stamp, goes off hello grid.)</span></span>

<span data-ttu-id="72dcd-142">第二個量值為 hello 各種虛擬網路是連線的 toohello 各種連線的 tooSAP HANA Azure （大型執行個體） 上的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="72dcd-142">As a second measure, hello various virtual networks are connected toohello various ExpressRoute circuits that are connected tooSAP HANA on Azure (large instances).</span></span> <span data-ttu-id="72dcd-143">我們稍後討論，您可以略過 MSEE 失敗，或您可以降低的嚴重損壞修復的 hello 復原點目標的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-143">You can bypass hello location where an MSEE is failing, or you can lower hello recovery point objective for disaster recovery, as we discuss later.</span></span>

<span data-ttu-id="72dcd-144">hello 下一個災害復原安裝程式需求如下：</span><span class="sxs-lookup"><span data-stu-id="72dcd-144">hello next requirements for a disaster-recovery setup are:</span></span>

- <span data-ttu-id="72dcd-145">在 Azure （大型執行個體） 的相同大小與生產環境的 Sku，並將其部署 hello 嚴重損壞修復區域中的 hello 的 Sku 上的 SAP HANA 都必須排序。</span><span class="sxs-lookup"><span data-stu-id="72dcd-145">You must order SAP HANA on Azure (large instances) SKUs of hello same size as your production SKUs and deploy them in hello disaster-recovery region.</span></span> <span data-ttu-id="72dcd-146">這些執行個體可以使用的 toorun 測試、 沙箱或 QA HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-146">These instances can be used toorun test, sandbox, or QA HANA instances.</span></span>
- <span data-ttu-id="72dcd-147">您必須排序災害復原設定檔針對每個您在 Azure （大型執行個體） 的 Sku 上的 SAP HANA 的 toorecover hello 災害復原站台，如有必要。</span><span class="sxs-lookup"><span data-stu-id="72dcd-147">You must order a disaster-recovery profile for each of your SAP HANA on Azure (large instances) SKUs that you want toorecover in hello disaster-recovery site, if necessary.</span></span> <span data-ttu-id="72dcd-148">這個動作會導致 toohello 配置的存放磁碟區，也就是從您的生產地區到 hello 嚴重損壞修復區域的 hello 儲存體複寫 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="72dcd-148">This action leads toohello allocation of storage volumes, which are hello target of hello storage replication from your production region into hello disaster-recovery region.</span></span>

<span data-ttu-id="72dcd-149">符合上述需求的 hello 之後，就有責任 toostart hello 儲存體複寫。</span><span class="sxs-lookup"><span data-stu-id="72dcd-149">After you meet hello preceding requirements, it is your responsibility toostart hello storage replication.</span></span> <span data-ttu-id="72dcd-150">用於在 Azure （大型執行個體） 上的 SAP HANA hello 儲存體基礎結構，在 hello 的儲存體複寫的基礎都是儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-150">In hello storage infrastructure used for SAP HANA on Azure (large instances), hello basis of storage replication is storage snapshots.</span></span> <span data-ttu-id="72dcd-151">toostart hello 災害復原的複寫，您需要 tooperform:</span><span class="sxs-lookup"><span data-stu-id="72dcd-151">toostart hello disaster-recovery replication, you need tooperform:</span></span>

- <span data-ttu-id="72dcd-152">開機 LUN 的快照集 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-152">A snapshot of your boot LUN, as described earlier.</span></span>
- <span data-ttu-id="72dcd-153">HANA 相關磁碟區的快照集 (如先前所述)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-153">A snapshot of your HANA-related volumes, as described earlier.</span></span>

<span data-ttu-id="72dcd-154">執行這些快照之後，hello 磁碟區的初始複本是植入 hello 與您 hello 嚴重損壞修復區域中的災害復原設定檔相關聯的磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="72dcd-154">After you execute these snapshots, an initial replica of hello volumes is seeded on hello volumes that are associated with your disaster-recovery profile in hello disaster-recovery region.</span></span>

<span data-ttu-id="72dcd-155">接著，hello 最新儲存體使用快照集是每小時 hello 存放磁碟區開發的 tooreplicate hello 差異。</span><span class="sxs-lookup"><span data-stu-id="72dcd-155">Subsequently, hello most recent storage snapshot is used every hour tooreplicate hello deltas that develop on hello storage volumes.</span></span>

<span data-ttu-id="72dcd-156">hello 達成這項設定的復原點目標是從 60 too90 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="72dcd-156">hello recovery point objective that's achieved with this configuration is from 60 too90 minutes.</span></span> <span data-ttu-id="72dcd-157">tooachieve 更佳的復原點目標，在 hello 災害復原情況下，複製 hello HANA 交易記錄備份從 SAP HANA toohello Azure （大型執行個體） 上其他的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="72dcd-157">tooachieve a better recovery point objective in hello disaster-recovery case, copy hello HANA transaction log backups from SAP HANA on Azure (large instances) toohello other Azure region.</span></span> <span data-ttu-id="72dcd-158">tooachieve 此復原點目標，執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-158">tooachieve this recovery point objective, do hello following:</span></span>

1. <span data-ttu-id="72dcd-159">備份 hello HANA 交易記錄的頻率儘可能太/hana/記錄檔/備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-159">Back up hello HANA transaction log as frequently as possible too/hana/log/backup.</span></span>
2. <span data-ttu-id="72dcd-160">在完成的 tooan Azure 的虛擬機器 (VM)，也就是已連接 toohello SAP HANA Azure （大型執行個體） 的伺服器上的虛擬網路中時，請複製 hello 交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-160">Copy hello transaction log backups when they are finished tooan Azure virtual machine (VM), which is in a virtual network that's connected toohello SAP HANA on Azure (large instances) server.</span></span>
3. <span data-ttu-id="72dcd-161">從該 VM 上，複製到 hello 備份 tooa hello 嚴重損壞修復區域中的虛擬網路中的 VM。</span><span class="sxs-lookup"><span data-stu-id="72dcd-161">From that VM, copy hello backup tooa VM that's in a virtual network in hello disaster-recovery region.</span></span>
4. <span data-ttu-id="72dcd-162">請在 hello VM hello 交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-162">Keep hello transaction log backups in that region in hello VM.</span></span>

<span data-ttu-id="72dcd-163">發生嚴重損壞時，實際的伺服器上部署 hello 災害復原設定檔之後，複製 hello 交易記錄備份從 hello VM toohello Azure （大型執行個體），就是在 hello 嚴重損壞修復區域中，現在 hello 主要伺服器上的 SAP HANA 和還原這些備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-163">In case of disaster, after hello disaster-recovery profile has been deployed on an actual server, copy hello transaction log backups from hello VM toohello SAP HANA on Azure (large instances) that is now hello primary server in hello disaster-recovery region, and restore those backups.</span></span> <span data-ttu-id="72dcd-164">此復原可能是因為 HANA hello 嚴重損壞修復磁碟上的 hello 狀態是 HANA 快照。</span><span class="sxs-lookup"><span data-stu-id="72dcd-164">This recovery is possible because hello state of HANA on hello disaster-recovery disks is that of a HANA snapshot.</span></span> <span data-ttu-id="72dcd-165">這是 hello 位移進一步的交易記錄備份的還原點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-165">This is hello offset point for further restorations of transaction log backups.</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="72dcd-166">備份與還原</span><span class="sxs-lookup"><span data-stu-id="72dcd-166">Backup and restore</span></span>

<span data-ttu-id="72dcd-167">其中一個 hello 最重要的層面 toooperating 資料庫確定 hello 資料庫可以保護各種重大事件。</span><span class="sxs-lookup"><span data-stu-id="72dcd-167">One of hello most important aspects toooperating databases is making sure hello database can be protected from various catastrophic events.</span></span> <span data-ttu-id="72dcd-168">這些事件可以是所造成的任何項目天然災害 toosimple 使用者錯誤。</span><span class="sxs-lookup"><span data-stu-id="72dcd-168">These events can be caused by anything from natural disasters toosimple user errors.</span></span>

<span data-ttu-id="72dcd-169">將資料庫備份，與 hello 能力 toorestore 它 tooany 點的時間 (例如有人已刪除的重要資料之前)，可讓還原 tooa 狀態可盡量 toohello 當時的 hello 中斷發生之前。</span><span class="sxs-lookup"><span data-stu-id="72dcd-169">Backing up a database, with hello ability toorestore it tooany point in time (such as before somebody deleted critical data), allows restoration tooa state that is as close as possible toohello way it was before hello disruption occurred.</span></span>

<span data-ttu-id="72dcd-170">必須執行兩種類型的備份，才能獲得最佳結果：</span><span class="sxs-lookup"><span data-stu-id="72dcd-170">Two types of backups must be performed for best results:</span></span>

- <span data-ttu-id="72dcd-171">資料庫備份</span><span class="sxs-lookup"><span data-stu-id="72dcd-171">Database backups</span></span>
- <span data-ttu-id="72dcd-172">交易記錄備份</span><span class="sxs-lookup"><span data-stu-id="72dcd-172">Transaction log backups</span></span>

<span data-ttu-id="72dcd-173">除了執行的應用程式層級 toofull 資料庫備份，您可以更徹底執行與儲存快照集備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-173">In addition toofull database backups performed at an application-level, you can be even more thorough by performing backups with storage snapshots.</span></span> <span data-ttu-id="72dcd-174">執行記錄備份也是很重要的還原 hello 資料庫 （和 tooempty hello 已認可的交易記錄檔）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-174">Performing log backups is also important for restoring hello database (and tooempty hello logs from already committed transactions).</span></span>

<span data-ttu-id="72dcd-175">SAP HANA on Azure (大型執行個體) 提供兩個備份和還原選項：</span><span class="sxs-lookup"><span data-stu-id="72dcd-175">SAP HANA on Azure (large instances) offers two backup and restore options:</span></span>

- <span data-ttu-id="72dcd-176">自己動手做 (DIY)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-176">Do it yourself (DIY).</span></span> <span data-ttu-id="72dcd-177">計算 tooensure 足夠的磁碟空間後，請使用磁碟備份方法 （toothose 磁碟） 以執行完整的資料庫和記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-177">After you calculate tooensure enough disk space, perform full database and log backups by using disk backup methods (toothose disks).</span></span> <span data-ttu-id="72dcd-178">經過一段時間，hello 備份複製的 tooan （之後您將幾乎不受限制的儲存體與 Azure 為基礎的檔案伺服器設定） 的 Azure 儲存體帳戶，或使用 Azure 備份保存庫或 Azure 冷儲存體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-178">Over time, hello backups are copied tooan Azure storage account (after you set up an Azure-based file server with virtually unlimited storage), or use an Azure Backup vault or Azure cold storage.</span></span> <span data-ttu-id="72dcd-179">另一個選項是 toouse 第三方資料保護工具，例如 Commvault，toostore hello 備份之後複製 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="72dcd-179">Another option is toouse a third-party data protection tool, such as Commvault, toostore hello backups after they are copied tooa storage account.</span></span> <span data-ttu-id="72dcd-180">hello DIY 備份的選項也可能需要將需要 toobe 較長的時間規範和稽核用途所儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="72dcd-180">hello DIY backup option might also be necessary for data that needs toobe stored for longer periods for compliancy and auditing purposes.</span></span>
- <span data-ttu-id="72dcd-181">使用 hello 備份和還原 hello Azure （大型執行個體） 上的 SAP HANA 的基礎結構的功能提供。</span><span class="sxs-lookup"><span data-stu-id="72dcd-181">Use hello backup and restore functionality that hello underlying infrastructure of SAP HANA on Azure (large instances) provides.</span></span> <span data-ttu-id="72dcd-182">此選項，可滿足 hello 需要進行備份，而它會使得手動備份幾乎過時 （除了備份資料是為了相容性用途）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-182">This option fulfills hello need for backups, and it makes manual backups nearly obsolete (except where data backups are required for compliance purposes).</span></span> <span data-ttu-id="72dcd-183">本章節將說明 hello 其餘 hello 備份和還原 HANA （大型執行個體） 提供的功能。</span><span class="sxs-lookup"><span data-stu-id="72dcd-183">hello rest of this section addresses hello backup and restore functionality that's offered with HANA (large instances).</span></span>

> [!NOTE]
> <span data-ttu-id="72dcd-184">hello 快照集技術，可由 hello 的 HANA （大型執行個體） 的基礎結構會相依於 SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-184">hello snapshot technology that is used by hello underlying infrastructure of HANA (large instances) has a dependency on SAP HANA snapshots.</span></span> <span data-ttu-id="72dcd-185">SAP HANA 快照集無法搭配 SAP HANA 多租用戶資料庫容器一起使用。</span><span class="sxs-lookup"><span data-stu-id="72dcd-185">SAP HANA snapshots do not work in conjunction with SAP HANA Multitenant Database Containers.</span></span> <span data-ttu-id="72dcd-186">如此一來，這種備份方法不能使用的 toodeploy SAP HANA 多租用戶資料庫容器。</span><span class="sxs-lookup"><span data-stu-id="72dcd-186">As a result, this method of backup cannot be used toodeploy SAP HANA Multitenant Database Containers.</span></span>

### <a name="using-storage-snapshots-of-sap-hana-on-azure-large-instances"></a><span data-ttu-id="72dcd-187">使用 SAP HANA on Azure (大型執行個體) 的儲存體快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-187">Using storage snapshots of SAP HANA on Azure (large instances)</span></span>

<span data-ttu-id="72dcd-188">hello 基礎 Azure （大型執行個體） 上的 SAP HANA 的儲存體基礎結構支援儲存體的快照集磁碟區的 hello 的概念。</span><span class="sxs-lookup"><span data-stu-id="72dcd-188">hello storage infrastructure underlying SAP HANA on Azure (large instances) supports hello notion of a storage snapshot of volumes.</span></span> <span data-ttu-id="72dcd-189">備份和還原的特定磁碟區支援，以 hello 下列考量：</span><span class="sxs-lookup"><span data-stu-id="72dcd-189">Both backup and restoration of a particular volume are supported, with hello following considerations:</span></span>

- <span data-ttu-id="72dcd-190">系統會經常建立存放磁碟區快照，而不是進行資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-190">Instead of database backups, storage volume snapshots are taken on a frequent basis.</span></span>
- <span data-ttu-id="72dcd-191">hello 儲存快照集執行 hello 儲存快照集之前，會起始 SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-191">hello storage snapshot initiates an SAP HANA snapshot before it executes hello storage snapshot.</span></span> <span data-ttu-id="72dcd-192">此 SAP HANA 快照之後復原 hello 儲存快照集的最後記錄還原的 hello 安裝點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-192">This SAP HANA snapshot is hello setup point for eventual log restorations after recovery of hello storage snapshot.</span></span>
- <span data-ttu-id="72dcd-193">在 hello hello 儲存快照集已順利執行的時間點，則刪除 hello SAP HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-193">At hello point where hello storage snapshot is executed successfully, hello SAP HANA snapshot is deleted.</span></span>
- <span data-ttu-id="72dcd-194">經常建立記錄備份，並儲存在 hello 記錄備份的磁碟區，或在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="72dcd-194">Log backups are taken frequently and stored in hello log backup volume or in Azure.</span></span>
- <span data-ttu-id="72dcd-195">如果必須還原 hello 資料庫 tooa 特定時間點，提出要求 Azure 服務管理 toorestore tooa tooMicrosoft Azure 支援 （實際執行中斷的狀況） 或 SAP HANA 特定儲存體快照集 （例如，規劃還原的沙箱系統tooits 原始狀態）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-195">If hello database must be restored tooa certain point in time, a request is made tooMicrosoft Azure Support (production outage) or SAP HANA on Azure Service Management toorestore tooa certain storage snapshot (for example, a planned restoration of a sandbox system tooits original state).</span></span>
- <span data-ttu-id="72dcd-196">hello SAP HANA 快照集包含在 hello 儲存快照集是套用記錄備份已執行並儲存製作 hello 儲存快照集之後的位移的點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-196">hello SAP HANA snapshot that's included in hello storage snapshot is an offset point for applying log backups that have been executed and stored after hello storage snapshot was taken.</span></span>
- <span data-ttu-id="72dcd-197">這些記錄備份 toorestore hello 資料庫回復 tooa 特定時間點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-197">These log backups are taken toorestore hello database back tooa certain point in time.</span></span>

<span data-ttu-id="72dcd-198">指定 hello 備份\_名稱建立快照的下列磁碟區的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-198">Specifying hello backup\_name creates a snapshot of hello following volumes:</span></span>

- <span data-ttu-id="72dcd-199">hana/data</span><span class="sxs-lookup"><span data-stu-id="72dcd-199">hana/data</span></span>
- <span data-ttu-id="72dcd-200">hana/log</span><span class="sxs-lookup"><span data-stu-id="72dcd-200">hana/log</span></span>
- <span data-ttu-id="72dcd-201">hana/log\_backup (以備份形式掛接到 hana/log 中)</span><span class="sxs-lookup"><span data-stu-id="72dcd-201">hana/log\_backup (mounted as backup into hana/log)</span></span>
- <span data-ttu-id="72dcd-202">hana/shared</span><span class="sxs-lookup"><span data-stu-id="72dcd-202">hana/shared</span></span>

### <a name="storage-snapshot-considerations"></a><span data-ttu-id="72dcd-203">儲存體快照考量事項</span><span class="sxs-lookup"><span data-stu-id="72dcd-203">Storage snapshot considerations</span></span>

>[!NOTE]
><span data-ttu-id="72dcd-204">儲存體快照集「不是」免費提供的功能，因為必須配置額外的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="72dcd-204">Storage snapshots are _not_ provided free of charge, because additional storage space must be allocated.</span></span>

<span data-ttu-id="72dcd-205">hello 的儲存體 Azure （大型執行個體） 上的 SAP HANA 的快照集的特定技巧包括：</span><span class="sxs-lookup"><span data-stu-id="72dcd-205">hello specific mechanics of storage snapshots for SAP HANA on Azure (large instances) include:</span></span>

- <span data-ttu-id="72dcd-206">特定的儲存體快照集 （在 hello 當它拍攝的時間點） 會耗用很少的儲存體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-206">A specific storage snapshot (at hello point in time when it is taken) consumes very little storage.</span></span>
- <span data-ttu-id="72dcd-207">為資料內容變更 hello hello 存放磁碟區的檔案變更的 SAP HANA 資料內容，hello 快照需要 toostore hello 原始區塊內容。</span><span class="sxs-lookup"><span data-stu-id="72dcd-207">As data content changes and hello content in SAP HANA data files change on hello storage volume, hello snapshot needs toostore hello original block content.</span></span>
- <span data-ttu-id="72dcd-208">hello 儲存快照集的大小會增加。</span><span class="sxs-lookup"><span data-stu-id="72dcd-208">hello storage snapshot increases in size.</span></span> <span data-ttu-id="72dcd-209">hello 長 hello 快照集存在，會變成 hello 較大 hello 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-209">hello longer hello snapshot exists, hello larger hello storage snapshot becomes.</span></span>
- <span data-ttu-id="72dcd-210">hello hello 存留期的儲存體的快照集的多個所做的變更 toohello SAP HANA 資料庫磁碟區，會變成 hello 較大 hello 空間耗用量的 hello 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-210">hello more changes made toohello SAP HANA database volume over hello lifetime of a storage snapshot, hello larger hello space consumption of hello storage snapshot becomes.</span></span>

<span data-ttu-id="72dcd-211">在 Azure （大型執行個體） 上的 SAP HANA 隨附 hello SAP HANA 資料和記錄磁碟區的固定磁碟區大小。</span><span class="sxs-lookup"><span data-stu-id="72dcd-211">SAP HANA on Azure (large instances) comes with fixed volume sizes for hello SAP HANA data and log volume.</span></span> <span data-ttu-id="72dcd-212">執行這些磁碟區的快照會吞掉的磁碟區空間中，所以您必須負責 tooschedule 存放裝置內的快照集 （hello SAP HANA Azure [大型執行個體] 處理序上)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-212">Performing snapshots of those volumes eats into your volume space, so it is your responsibility tooschedule storage snapshots (within hello SAP HANA on Azure [large instances] process).</span></span>

<span data-ttu-id="72dcd-213">hello 下列各節提供資訊來執行這些快照集，包括一般建議：</span><span class="sxs-lookup"><span data-stu-id="72dcd-213">hello following sections provide information for performing these snapshots, including general recommendations:</span></span>

- <span data-ttu-id="72dcd-214">雖然 hello 硬體可承受 255 的快照集，每個磁碟區，我們強烈建議您維持低於這個數字。</span><span class="sxs-lookup"><span data-stu-id="72dcd-214">Though hello hardware can sustain 255 snapshots per volume, we highly recommend that you stay well below this number.</span></span>
- <span data-ttu-id="72dcd-215">執行儲存體快照集之前，請監視並追蹤可用空間。</span><span class="sxs-lookup"><span data-stu-id="72dcd-215">Before you perform storage snapshots, monitor and keep track of free space.</span></span>
- <span data-ttu-id="72dcd-216">較低 hello 儲存快照集數目取決於可用的空間。</span><span class="sxs-lookup"><span data-stu-id="72dcd-216">Lower hello number of storage snapshots based on free space.</span></span> <span data-ttu-id="72dcd-217">您可能需要的保留，快照集 toolower hello 數目，或者您可能需要 tooextend hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-217">You might need toolower hello number of snapshots that you keep, or you might need tooextend hello volumes.</span></span> <span data-ttu-id="72dcd-218">(您可以訂購額外的儲存空間，以 1-TB 為單位)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-218">(You can order additional storage in 1-TB units.)</span></span>
- <span data-ttu-id="72dcd-219">在進行活動的期間，例如使用系統移轉工具 (使用 R3load) 將資料移到 SAP HANA (或是從備份還原 SAP HANA 資料庫)，強烈建議您不要執行任何儲存體快照集 </span><span class="sxs-lookup"><span data-stu-id="72dcd-219">During activities such as moving data into SAP HANA with system migration tools (with R3load, or by restoring SAP HANA databases from backups), we highly recommended that you not perform any storage snapshots.</span></span> <span data-ttu-id="72dcd-220">（如果新的 SAP HANA 系統上執行系統移轉，儲存快照集不需要執行 toobe。）</span><span class="sxs-lookup"><span data-stu-id="72dcd-220">(If a system migration is being done on a new SAP HANA system, storage snapshots would not need toobe performed.)</span></span>
- <span data-ttu-id="72dcd-221">在進行較大規模的 SAP HANA 資料表重組期間，應儘可能避免執行儲存體快照。</span><span class="sxs-lookup"><span data-stu-id="72dcd-221">During larger reorganizations of SAP HANA tables, storage snapshots should be avoided if possible.</span></span>
- <span data-ttu-id="72dcd-222">儲存體的快照集是在 Azure （大型執行個體） 上的 SAP HANA 必要條件 tooengaging hello 災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="72dcd-222">Storage snapshots are a prerequisite tooengaging hello disaster-recovery capabilities of SAP HANA on Azure (large instances).</span></span>

### <a name="setting-up-storage-snapshots"></a><span data-ttu-id="72dcd-223">設定儲存體快照</span><span class="sxs-lookup"><span data-stu-id="72dcd-223">Setting up storage snapshots</span></span>

1. <span data-ttu-id="72dcd-224">請確定 Perl 會安裝在 hello Linux 伺服器上作業系統 hello HANA （大型執行個體）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-224">Make sure that Perl is installed in hello Linux operating system on hello HANA (large instances) server.</span></span>
2. <span data-ttu-id="72dcd-225">修改 /etc/hosts ssh/ssh\_config tooadd hello 列_Mac hmac sha1_。</span><span class="sxs-lookup"><span data-stu-id="72dcd-225">Modify /etc/ssh/ssh\_config tooadd hello line _MACs hmac-sha1_.</span></span>
3. <span data-ttu-id="72dcd-226">建立 hello 每個 SAP HANA 執行個體 （如果適用） 執行您的主要節點上的 SAP HANA 備份使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="72dcd-226">Create an SAP HANA backup user account on hello master node for each SAP HANA instance you are running (if applicable).</span></span>
4. <span data-ttu-id="72dcd-227">SAP HANA （大型執行個體） 的所有伺服器上必須安裝 hello SAP HANA HDB 用戶端。</span><span class="sxs-lookup"><span data-stu-id="72dcd-227">hello SAP HANA HDB client must be installed on all SAP HANA (large instances) servers.</span></span>
5. <span data-ttu-id="72dcd-228">Hello 第一個 SAP HANA （大型執行個體） 伺服器上的每個區域，公開金鑰必須建立 tooaccess hello 基礎控制快照集建立的儲存體基礎結構。</span><span class="sxs-lookup"><span data-stu-id="72dcd-228">On hello first SAP HANA (large instances) server of each region, a public key must be created tooaccess hello underlying storage infrastructure that controls snapshot creation.</span></span>
6. <span data-ttu-id="72dcd-229">將 azure 的 hello 指令碼複製\_hana\_從 /scripts toohello 位置 backup.pl **hdbsql** hello SAP HANA 安裝。</span><span class="sxs-lookup"><span data-stu-id="72dcd-229">Copy hello script azure\_hana\_backup.pl from /scripts toohello location of **hdbsql** of hello SAP HANA installation.</span></span>
7. <span data-ttu-id="72dcd-230">複製 hello HANABackupDetails.txt 檔案從 /scripts toohello 相同 hello Perl 指令碼的位置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-230">Copy hello HANABackupDetails.txt file from /scripts toohello same location as hello Perl script.</span></span>
8. <span data-ttu-id="72dcd-231">修改視 hello 適當客戶規格 hello HANABackupDetails.txt 檔案。</span><span class="sxs-lookup"><span data-stu-id="72dcd-231">Modify hello HANABackupDetails.txt file as necessary for hello appropriate customer specifications.</span></span>

### <a name="step-1-install-sap-hana-hdbclient"></a><span data-ttu-id="72dcd-232">步驟 1：安裝 SAP HANA HDBClient</span><span class="sxs-lookup"><span data-stu-id="72dcd-232">Step 1: Install SAP HANA HDBClient</span></span>

<span data-ttu-id="72dcd-233">hello Linux 安裝在 Azure （大型執行個體） 上的 SAP HANA 包括 hello 資料夾和指令碼進行備份和災害復原的必要 tooexecute SAP HANA 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-233">hello Linux installed on SAP HANA on Azure (large instances) includes hello folders and scripts necessary tooexecute SAP HANA storage snapshots for backup and disaster-recovery purposes.</span></span> <span data-ttu-id="72dcd-234">不過，它是您的責任 tooinstall SAP HANA HDBclient 安裝 SAP HANA 時。</span><span class="sxs-lookup"><span data-stu-id="72dcd-234">However, it is your responsibility tooinstall SAP HANA HDBclient while you are installing SAP HANA.</span></span> <span data-ttu-id="72dcd-235">（hello HDBclient 和 SAP HANA 都不會安裝 Microsoft）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-235">(Microsoft installs neither hello HDBclient nor SAP HANA.)</span></span>

### <a name="step-2-change-etcsshsshconfig"></a><span data-ttu-id="72dcd-236">步驟 2：變更 /etc/ssh/ssh\_config</span><span class="sxs-lookup"><span data-stu-id="72dcd-236">Step 2: Change /etc/ssh/ssh\_config</span></span>

<span data-ttu-id="72dcd-237">在 /etc/ssh/ssh\_config 中新增 _MACs hmac-sha1_ 這一行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="72dcd-237">Change /etc/ssh/ssh\_config by adding _MACs hmac-sha1_ line as shown here:</span></span>
```
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   GSSAPIKeyExchange no
#   GSSAPITrustDNS no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
Protocol 2
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
MACs hmac-sha1
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
#   ProxyCommand ssh -q -W %h:%p gateway.example.com
```

### <a name="step-3-create-a-public-key"></a><span data-ttu-id="72dcd-238">步驟 3︰建立公開金鑰</span><span class="sxs-lookup"><span data-stu-id="72dcd-238">Step 3: Create a public key</span></span>

<span data-ttu-id="72dcd-239">Hello 上每個 Azure 區域，在 Azure （大型執行個體） 伺服器上的第一個 SAP HANA 建立使用公用金鑰 toobe tooaccess hello 儲存體基礎結構，讓您可以建立快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-239">On hello first SAP HANA on Azure (large instances) server in each Azure region, create a public key toobe used tooaccess hello storage infrastructure so that you can create snapshots.</span></span> <span data-ttu-id="72dcd-240">密碼不需要的 toosign toohello 儲存體中，而且不會保留密碼認證，可確保 hello 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="72dcd-240">hello public key ensures that a password is not required toosign in toohello storage and that password credentials are not maintained.</span></span> <span data-ttu-id="72dcd-241">在 Linux hello SAP HANA （大型執行個體） 伺服器上，執行下列命令 toogenerate hello 公開金鑰 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-241">In Linux on hello SAP HANA (large instances) server, execute hello following command toogenerate hello public key:</span></span>
```
  ssh-keygen –t dsa –b 1024
```
<span data-ttu-id="72dcd-242">hello 新的位置是 _/root/.ssh/id\_dsa.pub。</span><span class="sxs-lookup"><span data-stu-id="72dcd-242">hello new location is _/root/.ssh/id\_dsa.pub.</span></span> <span data-ttu-id="72dcd-243">請勿輸入實際的複雜密碼，否則您將會需要的 tooenter hello 複雜密碼每次您登入。</span><span class="sxs-lookup"><span data-stu-id="72dcd-243">Do not enter an actual passphrase, or else you will be required tooenter hello passphrase each time you sign in.</span></span> <span data-ttu-id="72dcd-244">反之，請按**Enter**兩次 tooremove hello 輸入複雜密碼來登入的需求。</span><span class="sxs-lookup"><span data-stu-id="72dcd-244">Instead, press **Enter** twice tooremove hello enter passphrase requirement for signing in.</span></span>

<span data-ttu-id="72dcd-245">請確定該 hello 公開金鑰已更正依照預期方式變更 too/root/.ssh/ 資料夾，然後再執行 hello toomake **ls**命令。</span><span class="sxs-lookup"><span data-stu-id="72dcd-245">Check toomake sure that hello public key was corrected as expected by changing folders too/root/.ssh/ and then executing hello **ls** command.</span></span> <span data-ttu-id="72dcd-246">如果 hello 機碼存在，您可以將它複製藉由執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-246">If hello key is present, you can copy it by running hello following command:</span></span>

![執行此命令即可複製公開金鑰](./media/hana-overview-high-availability-disaster-recovery/image2-public-key.png)

<span data-ttu-id="72dcd-248">此時，請連絡 Azure 服務管理上的 SAP HANA，並提供 hello 金鑰。</span><span class="sxs-lookup"><span data-stu-id="72dcd-248">At this point, contact SAP HANA on Azure Service Management and provide hello key.</span></span> <span data-ttu-id="72dcd-249">hello 服務代表通話，會使用 hello 公用金鑰 tooregister hello 基礎儲存體基礎結構中。</span><span class="sxs-lookup"><span data-stu-id="72dcd-249">hello service representative uses hello public key tooregister it in hello underlying storage infrastructure.</span></span>

### <a name="step-4-create-an-sap-hana-user-account"></a><span data-ttu-id="72dcd-250">步驟 4：建立 SAP HANA 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="72dcd-250">Step 4: Create an SAP HANA user account</span></span>

<span data-ttu-id="72dcd-251">在 SAP HANA Studio 中建立 SAP HANA 使用者帳戶以供備份使用。</span><span class="sxs-lookup"><span data-stu-id="72dcd-251">Create an SAP HANA user account within SAP HANA Studio for backup purposes.</span></span> <span data-ttu-id="72dcd-252">此帳戶必須具有下列權限的 hello:_備份管理員_和_目錄讀取_。</span><span class="sxs-lookup"><span data-stu-id="72dcd-252">This account must have hello following privileges: _Backup Admin_ and _Catalog Read_.</span></span> <span data-ttu-id="72dcd-253">在此範例中，建立 SCADMIN hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="72dcd-253">In this example, hello username SCADMIN is created.</span></span>

![在 HANA Studio 中建立使用者](./media/hana-overview-high-availability-disaster-recovery/image3-creating-user.png)

### <a name="step-5-authorize-hello-sap-hana-user-account"></a><span data-ttu-id="72dcd-255">步驟 5： 授權 hello SAP HANA 使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="72dcd-255">Step 5: Authorize hello SAP HANA user account</span></span>

<span data-ttu-id="72dcd-256">授權 hello SAP HANA 使用者帳戶 (toobe hello 指令碼使用而不需要授權，每次執行 hello 指令碼時)。</span><span class="sxs-lookup"><span data-stu-id="72dcd-256">Authorize hello SAP HANA user account (toobe used by hello scripts without requiring authorization every time hello script is run).</span></span> <span data-ttu-id="72dcd-257">hello SAP HANA 命令`hdbuserstore`允許 hello SAP HANA 使用者金鑰，並儲存在一個或多個 SAP HANA 節點上建立。</span><span class="sxs-lookup"><span data-stu-id="72dcd-257">hello SAP HANA command `hdbuserstore` allows hello creation of an SAP HANA user key, which is stored on one or more SAP HANA nodes.</span></span> <span data-ttu-id="72dcd-258">hello 使用者金鑰也允許 hello 使用者 tooaccess SAP HANA，而不需要將密碼從 toomanage 內 hello 指令碼處理程序，稍後再討論。</span><span class="sxs-lookup"><span data-stu-id="72dcd-258">hello user key also allows hello user tooaccess SAP HANA without having toomanage passwords from within hello scripting process that's discussed later.</span></span>

>[!IMPORTANT]
><span data-ttu-id="72dcd-259">執行 hello 下列命令為`_root_`。</span><span class="sxs-lookup"><span data-stu-id="72dcd-259">Run hello following command as `_root_`.</span></span> <span data-ttu-id="72dcd-260">否則，hello 指令碼無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="72dcd-260">Otherwise, hello script cannot work properly.</span></span>

<span data-ttu-id="72dcd-261">輸入 hello`hdbuserstore`命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="72dcd-261">Enter hello `hdbuserstore` command as follows:</span></span>

![輸入 hello hdbuserstore 命令](./media/hana-overview-high-availability-disaster-recovery/image4-hdbuserstore-command.png)

<span data-ttu-id="72dcd-263">在下列的範例，其中 hello 使用者 SCADMIN01，hello 的主機名稱是 lhanad01 hello hello 命令為：</span><span class="sxs-lookup"><span data-stu-id="72dcd-263">In hello following example, where hello user is SCADMIN01 and hello hostname is lhanad01, hello command is:</span></span>
```
hdbuserstore set SCADMIN01 lhanad01:30115 <backup username> <password>
```
<span data-ttu-id="72dcd-264">針對相應放大 HANA 執行個體，從單一伺服器管理所有指令碼處理。</span><span class="sxs-lookup"><span data-stu-id="72dcd-264">Manage all scripting from a single server for scale-out HANA instances.</span></span> <span data-ttu-id="72dcd-265">在此範例中，必須為每個主機會反映為相關的 toohello 鍵 hello 主機的方式改變 hello SAP HANA 金鑰 SCADMIN01。</span><span class="sxs-lookup"><span data-stu-id="72dcd-265">In this example, hello SAP HANA key SCADMIN01 must be altered for each host in a way that reflects hello host that is related toohello key.</span></span> <span data-ttu-id="72dcd-266">SAP HANA 備份帳戶 hello 與 hello HANA DB hello 執行個體數目的修改也就是**lhanad**。</span><span class="sxs-lookup"><span data-stu-id="72dcd-266">That is, hello SAP HANA backup account is amended with hello instance number of hello HANA DB, **lhanad**.</span></span> <span data-ttu-id="72dcd-267">hello 金鑰必須 hello 分派它的主機上具有系統管理權限，並向外延展的 hello 備份使用者必須具有存取權限 tooall SAP HANA 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-267">hello key must have administrative privileges on hello host it is assigned to, and hello backup user for scale-out must have access rights tooall SAP HANA instances.</span></span>
```
hdbuserstore set SCADMIN01 lhanad:30015 SCADMIN <password>
hdbuserstore set SCADMIN02 lhanad:30115 SCADMIN <password>
hdbuserstore set SCADMIN03 lhanad:30215 SCADMIN <password>
```

### <a name="step-6-copy-items-from-hello-scripts-folder"></a><span data-ttu-id="72dcd-268">步驟 6: Hello /scripts 資料夾複製項目</span><span class="sxs-lookup"><span data-stu-id="72dcd-268">Step 6: Copy items from hello /scripts folder</span></span>

<span data-ttu-id="72dcd-269">複製 hello 下列項目從 hello/指令碼資料夾 （包含在 hello 安裝的 hello 黃金映像） toohello 工作目錄**hdbsql**。</span><span class="sxs-lookup"><span data-stu-id="72dcd-269">Copy hello following items from hello /scripts folder (included on hello gold image of hello installation) toohello working directory for **hdbsql**.</span></span> <span data-ttu-id="72dcd-270">就目前的 HANA 安裝而言，這個目錄是 /hana/shared/D01/exe/linuxx86\_64/hdb。</span><span class="sxs-lookup"><span data-stu-id="72dcd-270">For current HANA installations, this directory is /hana/shared/D01/exe/linuxx86\_64/hdb.</span></span>
```
azure\_hana\_backup.pl
testHANAConnection.pl
testStorageSnapshotConnection.pl
removeTestStorageSnapshot.pl
HANABackupCustomerDetails.txt
```
<span data-ttu-id="72dcd-271">複製下列項目，若其執行向外延展的 hello 或 OLAP:</span><span class="sxs-lookup"><span data-stu-id="72dcd-271">Copy hello following items if they are running scale-out or OLAP:</span></span>
```
azure\_hana\_backup\_bw.pl
testHANAConnectionBW.pl
testStorageSnapshotConnectionBW.pl
removeTestStorageSnapshotBW.pl
HANABackupCustomerDetailsBW.txt
```
<span data-ttu-id="72dcd-272">hello HANABackupCustomerDetails.txt 檔案是可修改的向上延展部署，如下所示。</span><span class="sxs-lookup"><span data-stu-id="72dcd-272">hello HANABackupCustomerDetails.txt file is modifiable as follows for a scale-up deployment.</span></span> <span data-ttu-id="72dcd-273">這是執行 hello 儲存快照集的 hello 指令碼的 hello 控制項和組態檔案。</span><span class="sxs-lookup"><span data-stu-id="72dcd-273">It is hello control and configuration file for hello script that runs hello storage snapshots.</span></span> <span data-ttu-id="72dcd-274">您應該會收到 hello_儲存體的備份名稱_和_存放裝置的 IP 位址_從 Azure 服務管理時部署您的執行個體上的 SAP HANA。</span><span class="sxs-lookup"><span data-stu-id="72dcd-274">You should have received hello _Storage Backup Name_ and _Storage IP Address_ from SAP HANA on Azure Service Management when your instances were deployed.</span></span> <span data-ttu-id="72dcd-275">您無法修改 hello 順序排序，或無法正常執行的任何 hello 變數或 hello 指令碼的間距。</span><span class="sxs-lookup"><span data-stu-id="72dcd-275">You cannot modify hello sequence, ordering, or spacing of any of hello variables, or hello script does not run properly.</span></span>

<span data-ttu-id="72dcd-276">向上延展部署，hello 組態檔應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="72dcd-276">For a scale-up deployment, hello configuration file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Created by customer using hdbuserstore
HANA Backup Name: SCADMIND01
```
<span data-ttu-id="72dcd-277">針對向外延展組態，hello HANABackupCustomerDetailsBW.txt 檔案應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="72dcd-277">For a scale-out configuration, hello HANABackupCustomerDetailsBW.txt file would look like:</span></span>
```
#Provided by Microsoft Service Management
Storage Backup Name: lhanad01backup
Storage IP Address: 10.250.20.21
#Node IP addresses, instance numbers, and HANA backup name
#provided by customer.  HANA backup name created using
#hdbuserstore utility.
Node 1 IP Address: 10.254.15.21
Node 1 HANA instance number: 01
Node 1 HANA Backup Name: SCADMIN01
Node 2 IP Address: 10.254.15.22
Node 2 HANA instance number: 02
Node 2 HANA Backup Name: SCADMIN02
Node 3 IP Address: 10.254.15.23
Node 3 HANA instance number: 03
Node 3 HANA Backup Name: SCADMIN03
Node 4 IP Address: 10.254.15.24
Node 4 HANA instance number: 04
Node 4 HANA Backup Name: SCADMIN04
Node 5 IP Address: 10.254.15.25
Node 5 HANA instance number: 05
Node 5 HANA Backup Name: SCADMIN05
Node 6 IP Address: 10.254.15.26
Node 6 HANA instance number: 06
Node 6 HANA Backup Name: SCADMIN06
Node 7 IP Address: 10.254.15.27
Node 7 HANA instance number: 07
Node 7 HANA Backup Name: SCADMIN07
Node 8 IP Address: 10.254.15.28
Node 8 HANA instance number: 08
Node 8 HANA Backup Name: SCADMIN08
```
>[!NOTE]
><span data-ttu-id="72dcd-278">目前，只有在節點 1 詳細資料會用於 hello 實際 HANA 儲存快照集指令碼。</span><span class="sxs-lookup"><span data-stu-id="72dcd-278">Currently, only Node 1 details are used in hello actual HANA storage snapshot script.</span></span> <span data-ttu-id="72dcd-279">我們建議您測試存取 tooor HANA 所有的節點，使 hello 主要備份節點變更，如果您已經可藉任何其他節點，可以修改節點 1 中的 hello 詳細資料來取代它的位置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-279">We recommend that you test access tooor from all HANA nodes so that, if hello master backup node ever changes, you have already ensured that any other node can take its place by modifying hello details in Node 1.</span></span>

<span data-ttu-id="72dcd-280">toocheck hello 設定檔或適當的連線能力 toohello HANA 執行個體，執行下列指令碼的 hello hello 正確設定：</span><span class="sxs-lookup"><span data-stu-id="72dcd-280">toocheck for hello correct configurations in hello configuration file or proper connectivity toohello HANA instances, run either of hello following scripts:</span></span>
- <span data-ttu-id="72dcd-281">如果是相應增加組態 (與 SAP 工作負載無關)︰</span><span class="sxs-lookup"><span data-stu-id="72dcd-281">For a scale-up configuration (independent on SAP workload):</span></span>

 ```
testHANAConnection.pl
```
- <span data-ttu-id="72dcd-282">如果是相應放大組態：</span><span class="sxs-lookup"><span data-stu-id="72dcd-282">For a scale-out configuration:</span></span>

 ```
testHANAConnectionBW.pl
```

<span data-ttu-id="72dcd-283">請確定該 hello 主要 HANA 執行個體都有存取必要的 tooall HANA 伺服器。</span><span class="sxs-lookup"><span data-stu-id="72dcd-283">Ensure that hello master HANA instance has access tooall required HANA servers.</span></span> <span data-ttu-id="72dcd-284">沒有任何參數 toohello 指令碼，但您必須先完成 hello 適當 HANABackupCustomerDetails / HANABackupCustomerDetailsBW 檔案的 hello 指令碼 toorun 正確。</span><span class="sxs-lookup"><span data-stu-id="72dcd-284">There are no parameters toohello script, but you must complete hello appropriate HANABackupCustomerDetails/ HANABackupCustomerDetailsBW file for hello script toorun properly.</span></span> <span data-ttu-id="72dcd-285">只有 hello 殼層命令會傳回錯誤碼，因為它不可能的 hello 指令碼 tooerror 核取每個執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-285">Because only hello shell command error codes are returned, it is not possible for hello script tooerror-check every instance.</span></span> <span data-ttu-id="72dcd-286">即便如此，hello 指令碼並提供您 toodouble 檢查一些很有幫助的註解。</span><span class="sxs-lookup"><span data-stu-id="72dcd-286">Even so, hello script does provide some helpful comments for you toodouble-check.</span></span>

<span data-ttu-id="72dcd-287">toorun hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="72dcd-287">toorun hello script:</span></span>
```
 ./testHANAConnection.pl
```
 <span data-ttu-id="72dcd-288">如果 hello 指令碼已成功取得 hello hello HANA 執行個體的狀態，它會顯示 hello HANA 連線成功的訊息。</span><span class="sxs-lookup"><span data-stu-id="72dcd-288">If hello script successfully obtains hello status of hello HANA instance, it displays a message that hello HANA connection was successful.</span></span>

<span data-ttu-id="72dcd-289">此外，還有第二個類型的指令碼可以使用 toocheck hello 主要 HANA server 執行個體的能力 toosign toohello 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="72dcd-289">Additionally, there is a second type of script you can use toocheck hello master HANA instance server's ability toosign in toohello storage.</span></span> <span data-ttu-id="72dcd-290">在執行 hello azure 之前\_hana\_備份 (\_bw).pl 指令碼，您必須執行 hello 下一個指令碼。</span><span class="sxs-lookup"><span data-stu-id="72dcd-290">Before you execute hello azure\_hana\_backup(\_bw).pl script, you must execute hello next script.</span></span> <span data-ttu-id="72dcd-291">如果磁碟區不包含任何快照集，則不可能 toodetermine 是否 hello 磁碟區是只是空的或沒有 ssh 失敗 tooobtain hello 快照詳細資料。</span><span class="sxs-lookup"><span data-stu-id="72dcd-291">If a volume contains no snapshots, it is impossible toodetermine whether hello volume is simply empty or there is an ssh failure tooobtain hello snapshot details.</span></span> <span data-ttu-id="72dcd-292">基於這個理由，hello 指令碼會執行兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="72dcd-292">For this reason, hello script executes two steps:</span></span>

- <span data-ttu-id="72dcd-293">它會驗證該 hello 儲存主控台是可存取。</span><span class="sxs-lookup"><span data-stu-id="72dcd-293">It verifies that hello storage console is accessible.</span></span>
- <span data-ttu-id="72dcd-294">依 HANA 執行個體，為每個磁碟區建立測試 (或虛設) 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-294">It creates a test, or dummy, snapshot for each volume by HANA instance.</span></span>

<span data-ttu-id="72dcd-295">基於這個理由，hello HANA 執行個體隨附做為引數。</span><span class="sxs-lookup"><span data-stu-id="72dcd-295">For this reason, hello HANA instance is included as an argument.</span></span> <span data-ttu-id="72dcd-296">同樣地，不可能 tooprovide 錯誤檢查 hello 儲存體連線，但是 hello 指令碼提供有用的提示，如果 hello 執行作業失敗。</span><span class="sxs-lookup"><span data-stu-id="72dcd-296">Again, it is not possible tooprovide error checking for hello storage connection, but hello script provides helpful hints if hello execution fails.</span></span>

<span data-ttu-id="72dcd-297">hello 指令碼是以執行：</span><span class="sxs-lookup"><span data-stu-id="72dcd-297">hello script is run as:</span></span>
```
 ./testStorageSnapshotConnection.pl <hana instance>
```
<span data-ttu-id="72dcd-298">或執行為︰</span><span class="sxs-lookup"><span data-stu-id="72dcd-298">Or it is run as:</span></span>
```
./testStorageSnapshotConnectionBW.pl <hana instance>
```
<span data-ttu-id="72dcd-299">hello 指令碼也會顯示訊息指出您無法 toosign 適當 tooyour 部署儲存體租用戶中，其組織方式周圍 hello 邏輯單元編號 (Lun)，可供您擁有 hello 伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-299">hello script also displays a message that you are able toosign in appropriately tooyour deployed storage tenant, which is organized around hello logical unit numbers (LUNs) that are used by hello server instances you own.</span></span>

<span data-ttu-id="72dcd-300">執行 hello 第一個儲存體的快照集為基礎的備份之前，先執行 hello 下一個指令碼 toomake 該 hello 組態正確。</span><span class="sxs-lookup"><span data-stu-id="72dcd-300">Before you execute hello first storage snapshot-based backups, run hello next scripts toomake sure that hello configuration is correct.</span></span>

<span data-ttu-id="72dcd-301">執行這些指令碼之後, 您可以藉由執行刪除 hello 快照集：</span><span class="sxs-lookup"><span data-stu-id="72dcd-301">After running these scripts, you can delete hello snapshots by executing:</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```
<span data-ttu-id="72dcd-302">或</span><span class="sxs-lookup"><span data-stu-id="72dcd-302">Or</span></span>
```
./removeTestStorageSnapshot.pl <hana instance>
```

### <a name="step-7-perform-on-demand-snapshots"></a><span data-ttu-id="72dcd-303">步驟 7：執行隨選快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-303">Step 7: Perform on-demand snapshots</span></span>

<span data-ttu-id="72dcd-304">執行隨選快照集 (以及使用 cron 來排程一般快照集） 如下所示。</span><span class="sxs-lookup"><span data-stu-id="72dcd-304">Perform on-demand snapshots (as well as schedule regular snapshots by using cron) as described here.</span></span>

<span data-ttu-id="72dcd-305">向上延展的組態，執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-305">For scale-up configurations, execute hello following script:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="72dcd-306">對於向外延展組態，執行下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-306">For scale-out configurations, execute hello following script:</span></span>
```
./azure_hana_backup_bw.pl lhanad01 customer 20
```
<span data-ttu-id="72dcd-307">hello 向外延展指令碼會確定可存取所有 HANA 伺服器，且所有 HANA 執行個體都傳回適當的狀態，再繼續建立 SAP HANA 或儲存體的快照集的 hello 執行個體的一些額外檢查 toomake。</span><span class="sxs-lookup"><span data-stu-id="72dcd-307">hello scale-out script does some additional checking toomake sure that all HANA servers can be accessed, and all HANA instances return appropriate status of hello instance before proceeding with creating SAP HANA or storage snapshots.</span></span>

<span data-ttu-id="72dcd-308">hello 下列引數是必要的：</span><span class="sxs-lookup"><span data-stu-id="72dcd-308">hello following arguments are required:</span></span>

- <span data-ttu-id="72dcd-309">hello HANA 執行個體需要備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-309">hello HANA instance requiring backup.</span></span>
- <span data-ttu-id="72dcd-310">hello hello 儲存快照集的快照集前置詞。</span><span class="sxs-lookup"><span data-stu-id="72dcd-310">hello snapshot prefix for hello storage snapshot.</span></span>
- <span data-ttu-id="72dcd-311">hello hello 特定前置詞保留的快照集 toobe 數目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-311">hello number of snapshots toobe kept for hello specific prefix.</span></span>

```
./azure_hana_backup.pl lhanad01 customer 20
```

<span data-ttu-id="72dcd-312">hello 執行 hello 指令碼會在這三個不同的階段建立 hello 儲存快照集：</span><span class="sxs-lookup"><span data-stu-id="72dcd-312">hello execution of hello script creates hello storage snapshot in these three distinct phases:</span></span>

- <span data-ttu-id="72dcd-313">執行 HANA 快照。</span><span class="sxs-lookup"><span data-stu-id="72dcd-313">Execute a HANA snapshot.</span></span>
- <span data-ttu-id="72dcd-314">執行儲存體快照。</span><span class="sxs-lookup"><span data-stu-id="72dcd-314">Execute a storage snapshot.</span></span>
- <span data-ttu-id="72dcd-315">移除 hello HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-315">Remove hello HANA snapshot.</span></span>

<span data-ttu-id="72dcd-316">藉由呼叫 hello HDB 可執行檔之資料夾中將它複製到執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="72dcd-316">Execute hello script by calling it from hello HDB executable folder that it was copied to.</span></span> <span data-ttu-id="72dcd-317">它將備份至少 hello 下列磁碟區，但它也會在 hello 磁碟區名稱中有 hello 明確 SAP HANA 執行個體名稱的任何磁碟區備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-317">It backs up at least hello following volumes, but it also backs up any volume that has hello explicit SAP HANA instance name in hello volume name.</span></span>
```
hana_data_<hana instance>_prod_t020_vol
hana_log_<hana instance>_prod_t020_vol
hana_log_backup_<hana instance>_prod_t020_vol
hana_shared_<hana instance>_prod_t020_vol
```
<span data-ttu-id="72dcd-318">hello 保留期限是嚴格管理，快照集時，您執行 hello 指令碼 （例如 20，先前所示)，做為參數提交的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-318">hello retention period is strictly administered, with hello number of snapshots submitted as a parameter when you execute hello script (such as 20, shown previously).</span></span> <span data-ttu-id="72dcd-319">因此 hello 一段時間是 hello 段 hello 呼叫 hello 指令碼中的快照集的執行與 hello 數目的函式。</span><span class="sxs-lookup"><span data-stu-id="72dcd-319">So hello amount of time is a function of hello period of execution and hello number of snapshots in hello call of hello script.</span></span> <span data-ttu-id="72dcd-320">如果保留的快照集的 hello 數目超過 hello 數字會命名為 hello 呼叫 hello 指令碼中的參數，hello 此標籤的最舊的儲存體快照集 (在上一個案例中，_自訂_) 刪除新的快照集之前執行。</span><span class="sxs-lookup"><span data-stu-id="72dcd-320">If hello number of snapshots that are kept exceeds hello number that are named as a parameter in hello call of hello script, hello oldest storage snapshot of this label (in our previous case, _custom_) is deleted before a new snapshot is executed.</span></span> <span data-ttu-id="72dcd-321">這表示您提供為 hello hello 呼叫的最後一個參數是您可以使用快照集 toocontrol hello 數目 hello 數目 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-321">This means hello number you give as hello last parameter of hello call is hello number you can use toocontrol hello number of snapshots.</span></span>

>[!NOTE]
><span data-ttu-id="72dcd-322">只要您變更 hello 標籤時，計算 hello 再次啟動。</span><span class="sxs-lookup"><span data-stu-id="72dcd-322">As soon as you change hello label, hello counting starts again.</span></span>

<span data-ttu-id="72dcd-323">您需要 tooinclude hello HANA 執行個體名稱所提供的 Azure 服務管理上的 SAP HANA 做為引數如果它們在多節點的環境中建立快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-323">You need tooinclude hello HANA instance name that's provided by SAP HANA on Azure Service Management as an argument if they are creating snapshots in multi-node environments.</span></span> <span data-ttu-id="72dcd-324">單一節點在環境中，Azure （大型執行個體） 單位上的 SAP HANA hello hello 名稱即已足夠，但仍建議 hello HANA 執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="72dcd-324">In single-node environments, hello name of hello SAP HANA on Azure (large instances) unit is sufficient, but hello HANA instance name is still recommended.</span></span>

<span data-ttu-id="72dcd-325">此外，您可以備份使用的開機 volumes\LUNs hello 相同指令碼。</span><span class="sxs-lookup"><span data-stu-id="72dcd-325">Additionally, you can back up boot volumes\LUNs by using hello same script.</span></span> <span data-ttu-id="72dcd-326">第一次執行 HANA 時，您必須至少備份開機磁碟區一次，但建議以 cron 進行每週或每晚開機備份排程。</span><span class="sxs-lookup"><span data-stu-id="72dcd-326">You must back up your boot volume at least once when you first run HANA, although we recommend a weekly or nightly backup schedule for booting in cron.</span></span> <span data-ttu-id="72dcd-327">不用新增的 SAP HANA 的執行個體名稱，而是插入_開機_，如下所示為 hello 指令碼 hello 引數為：</span><span class="sxs-lookup"><span data-stu-id="72dcd-327">Rather than add an SAP HANA instance name, insert _boot_ as hello argument into hello script as follows:</span></span>
```
./azure_hana_backup boot customer 20
```
<span data-ttu-id="72dcd-328">hello 相同保留原則是可以用 toohello 開機磁碟。</span><span class="sxs-lookup"><span data-stu-id="72dcd-328">hello same retention policy is afforded toohello boot volume as well.</span></span> <span data-ttu-id="72dcd-329">使用視快照集，做為描述之前，針對某些特殊情況下，例如 SAP 的增強功能 (EHP) 在封裝升級期間，或當您需要 toocreate 相異儲存體的快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-329">Use on-demand snapshots, as described previously, for special cases only, such as during an SAP enhancement package (EHP) upgrade, or when you need toocreate a distinct storage snapshot.</span></span>

<span data-ttu-id="72dcd-330">我們建議您排定 tooperform 儲存快照集使用 cron，並建議您針對所有的備份和災害復原需求 (修改 hello 指令碼輸入 toomatch hello 各種要求備份時間) 使用相同指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="72dcd-330">We encourage you tooperform scheduled storage snapshots using cron, and we recommend that you use hello same script for all backups and disaster-recovery needs (modifying hello script inputs toomatch hello various requested backup times).</span></span> <span data-ttu-id="72dcd-331">這些在 cron 中都會根據其執行時間以不同方式排定：每小時、12 小時、每天或每週。</span><span class="sxs-lookup"><span data-stu-id="72dcd-331">These are all scheduled differently in cron depending on their execution time: hourly, 12-hour, daily, or weekly.</span></span> <span data-ttu-id="72dcd-332">hello cron 排程是設計的 toocreate 儲存快照集符合先前所討論的 hello 進行長期離站備份的保留標記。</span><span class="sxs-lookup"><span data-stu-id="72dcd-332">hello cron schedule is designed toocreate storage snapshots that match hello previously discussed retention labeling for long-term off-site backup.</span></span> <span data-ttu-id="72dcd-333">hello 指令碼包含所有的實際執行磁碟區，根據其要求的頻率 （資料和記錄檔備份每小時、 每天備份 hello 開機磁碟區而） 命令 tooback。</span><span class="sxs-lookup"><span data-stu-id="72dcd-333">hello script includes commands tooback up all production volumes, depending on their requested frequency (data and log files are backed up hourly, whereas hello boot volume is backed up daily).</span></span>

<span data-ttu-id="72dcd-334">hello hello 遵循 cron 指令碼中的項目執行的每個小時 hello 十分鐘，每隔 12 小時在 hello 十分鐘，和每日 hello 十分鐘。</span><span class="sxs-lookup"><span data-stu-id="72dcd-334">hello entries in hello following cron script run every hour at hello tenth minute, every 12 hours at hello tenth minute, and daily at hello tenth minute.</span></span> <span data-ttu-id="72dcd-335">作業會在這種方式建立 hello cron 只有一個 SAP HANA 儲存快照集期間會進行任何特定的小時，以便 hello 每小時和每日備份不會發生在 hello 相同的時間 （上午 12:10）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-335">hello cron jobs are created in such a way that only one SAP HANA storage snapshot takes place during any particular hour, so that hello hourly and daily backups do not occur at hello same time (12:10 AM).</span></span> <span data-ttu-id="72dcd-336">toohelp 最佳化您的建立快照集和複寫，並在 Azure 服務管理上的 SAP HANA 提供 hello 建議您 toorun 時間備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-336">toohelp optimize your snapshot creation and replication, SAP HANA on Azure Service Management provides hello recommended time for you toorun your backups.</span></span>

<span data-ttu-id="72dcd-337">排程中 /etc/crontab hello 預設 cron 如下所示：</span><span class="sxs-lookup"><span data-stu-id="72dcd-337">hello default cron scheduling in /etc/crontab is as follows:</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 14
```
<span data-ttu-id="72dcd-338">在前述 cron 指示 hello，hello HANA 磁碟區 （不含開機磁碟區） 會取得快照集與 hello 標籤以每小時。</span><span class="sxs-lookup"><span data-stu-id="72dcd-338">In hello previous cron instructions, hello HANA volumes (without boot volume) get an hourly snapshot with hello label.</span></span> <span data-ttu-id="72dcd-339">在這些快照中，會保留 66 個。</span><span class="sxs-lookup"><span data-stu-id="72dcd-339">Of these snapshots, 66 are retained.</span></span> <span data-ttu-id="72dcd-340">此外，會保留 14 的快照集與 hello 12 小時制的標籤。</span><span class="sxs-lookup"><span data-stu-id="72dcd-340">Additionally, 14 snapshots with hello 12-hour label are retained.</span></span> <span data-ttu-id="72dcd-341">您可能取得三天的每小時快照集，加上另外四天的 12 小時快照集，您就有整週的快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-341">You potentially get hourly snapshots for three days, plus 12-hour snapshots for another four days, which gives you an entire week of snapshots.</span></span>

<span data-ttu-id="72dcd-342">Cron 內排程可能很困難，因為只有一個指令碼應該執行任何特定時間，除非 hello 指令碼會交錯的幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="72dcd-342">Scheduling within cron can be tricky, because only one script should be executed at any particular time, unless hello scripts are staggered by several minutes.</span></span> <span data-ttu-id="72dcd-343">如果您想要每日備份長期保存，12 小時制快照集 （具有保留的計數七個每個），以及保留每日快照集，或 hello 每小時的快照集是交錯的 tootake 位置 10 分鐘後。</span><span class="sxs-lookup"><span data-stu-id="72dcd-343">If you want daily backups for long-term retention, either a daily snapshot is kept along with a 12-hour snapshot (with a retention count of seven each), or hello hourly snapshot is staggered tootake place 10 minutes later.</span></span> <span data-ttu-id="72dcd-344">只有一個每日快照集都會保存在 hello 實際磁碟區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-344">Only one daily snapshot is kept in hello production volume.</span></span>
```
10 1-11,13-23 * * * ./azure_hana_backup.pl lhanad01 hourly 66
10 12 * * *  ./azure_hana_backup.pl lhanad01 12hour 7
10 0 * * * ./azure_hana_backup.pl lhanad01 daily 7
```
<span data-ttu-id="72dcd-345">此處所列的 hello 頻率僅為範例。</span><span class="sxs-lookup"><span data-stu-id="72dcd-345">hello frequencies listed here are only examples.</span></span> <span data-ttu-id="72dcd-346">tooderive 您最佳的數目快照集，使用下列準則的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-346">tooderive your optimum number of snapshots, use hello following criteria:</span></span>

- <span data-ttu-id="72dcd-347">時間點復原的復原時間目標中的需求。</span><span class="sxs-lookup"><span data-stu-id="72dcd-347">Requirements in recovery time objective for point-in-time recovery.</span></span>
- <span data-ttu-id="72dcd-348">空間使用量。</span><span class="sxs-lookup"><span data-stu-id="72dcd-348">Space usage.</span></span>
- <span data-ttu-id="72dcd-349">潛在災害復原的復原點目標和復原時間目標中的需求。</span><span class="sxs-lookup"><span data-stu-id="72dcd-349">Requirements in recovery point objective and recovery time objective for potential disaster recovery.</span></span>
- <span data-ttu-id="72dcd-350">對磁碟執行的最終 HANA 完整資料庫備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-350">Eventual execution of HANA full database backups against disks.</span></span> <span data-ttu-id="72dcd-351">只要磁碟上，針對完整資料庫備份或_backint_介面，是執行，hello 儲存快照集執行作業失敗。</span><span class="sxs-lookup"><span data-stu-id="72dcd-351">Whenever a full database backup against disks, or _backint_ interface, is performed, hello execution of storage snapshots fails.</span></span> <span data-ttu-id="72dcd-352">如果您計劃 tooexecute 之上儲存快照集的完整資料庫備份，請確定在這段期間已停用的儲存體的快照集的 hello 執行。</span><span class="sxs-lookup"><span data-stu-id="72dcd-352">If you plan tooexecute full database backups on top of storage snapshots, make sure that hello execution of storage snapshots is disabled during this time.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="72dcd-353">只有在搭配 SAP HANA 記錄備份執行 hello 快照集時 hello 使用 SAP HANA 備份儲存體的快照集無效。</span><span class="sxs-lookup"><span data-stu-id="72dcd-353">hello use of storage snapshots for SAP HANA backups is valid only when hello snapshots are performed in conjunction with SAP HANA log backups.</span></span> <span data-ttu-id="72dcd-354">這些記錄備份需要 toobe 無法 toocover hello hello 儲存體快照之間的時間週期。</span><span class="sxs-lookup"><span data-stu-id="72dcd-354">These log backups need toobe able toocover hello time periods between hello storage snapshots.</span></span> <span data-ttu-id="72dcd-355">如果您已經設定承諾 toousers 的 30 天的時間點復原，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-355">If you've set a commitment toousers of a point-in-time recovery of 30 days, you need hello following:</span></span>

- <span data-ttu-id="72dcd-356">能力 tooaccess 是 30 天的儲存體快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-356">Ability tooaccess a storage snapshot that is 30 days old.</span></span>
- <span data-ttu-id="72dcd-357">透過 hello 過去 30 天內的連續記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-357">Contiguous log backups over hello last 30 days.</span></span>

<span data-ttu-id="72dcd-358">在 hello 範圍中的記錄檔備份，建立以及 hello 備份記錄檔磁碟區的快照。</span><span class="sxs-lookup"><span data-stu-id="72dcd-358">In hello range of log backups, create a snapshot of hello backup log volume as well.</span></span> <span data-ttu-id="72dcd-359">不過，是確定 tooperform 定期記錄備份，讓您可以：</span><span class="sxs-lookup"><span data-stu-id="72dcd-359">However, be sure tooperform regular log backups so that you can:</span></span>

- <span data-ttu-id="72dcd-360">Hello 連續記錄備份，需要 tooperform 時間點復原。</span><span class="sxs-lookup"><span data-stu-id="72dcd-360">Have hello contiguous log backups needed tooperform point-in-time recoveries.</span></span>
- <span data-ttu-id="72dcd-361">防止 hello SAP HANA 記錄磁碟區空間用盡。</span><span class="sxs-lookup"><span data-stu-id="72dcd-361">Prevent hello SAP HANA log volume from running out of space.</span></span>

<span data-ttu-id="72dcd-362">其中一個 hello 最後幾個步驟是在 SAP HANA Studio tooschedule SAP HANA 備份記錄。</span><span class="sxs-lookup"><span data-stu-id="72dcd-362">One of hello last steps is tooschedule SAP HANA backup logs in SAP HANA Studio.</span></span> <span data-ttu-id="72dcd-363">hello SAP HANA 備份記錄檔目標目的地是特別建立的 hello hana/記錄檔\_/hana/log/backups hello 掛接點的備份磁碟區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-363">hello SAP HANA backup log target destination is hello specially created hana/log\_backups volume with hello mount point of /hana/log/backups.</span></span>

![在 SAP HANA Studio 中排定 SAP HANA 備份記錄](./media/hana-overview-high-availability-disaster-recovery/image5-schedule-backup.png)

<span data-ttu-id="72dcd-365">您可以選擇比每隔 15 分鐘更頻繁的備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-365">You can choose backups that are more frequent than every 15 minutes.</span></span> <span data-ttu-id="72dcd-366">有些使用者甚至每分鐘都執行記錄備份，但我們不建議「超過」15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="72dcd-366">Some users even perform log backups every minute, although we do not recommend going _over_ 15 minutes.</span></span>

<span data-ttu-id="72dcd-367">hello 最後一個步驟是以檔案為基礎的 tooperform （hello 初始安裝後的 SAP HANA） 備份 toocreate 必須存在於 hello 備份類別目錄的單一備份項目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-367">hello final step is tooperform a file-based backup (after hello initial installation of SAP HANA) toocreate a single backup entry that must exist within hello backup catalog.</span></span> <span data-ttu-id="72dcd-368">否則，SAP HANA 無法起始您指定的記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-368">Otherwise SAP HANA cannot initiate your specified log backups.</span></span>

![請以檔案為基礎的備份 toocreate 單一備份項目](./media/hana-overview-high-availability-disaster-recovery/image6-make-backup.png)

### <a name="monitoring-hello-number-and-size-of-snapshots-on-hello-disk-volume"></a><span data-ttu-id="72dcd-370">監視 hello 數目和大小的 hello 磁碟區上的快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-370">Monitoring hello number and size of snapshots on hello disk volume</span></span>

<span data-ttu-id="72dcd-371">在特定的存放磁碟區，您可以監視 hello 快照集和 hello 存放裝置耗用量的快照集數目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-371">On a particular storage volume, you can monitor hello number of snapshots and hello storage consumption of snapshots.</span></span> <span data-ttu-id="72dcd-372">hello`ls`命令不會顯示 hello 快照集目錄或檔案。</span><span class="sxs-lookup"><span data-stu-id="72dcd-372">hello `ls` command doesn't show hello snapshot directory or files.</span></span> <span data-ttu-id="72dcd-373">不過，hello Linux 作業系統命令`du`用途，下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="72dcd-373">However, hello Linux OS command `du` does, with hello following commands:</span></span>

- <span data-ttu-id="72dcd-374">`du –sh .snapshot`提供所有快照集內 hello 快照集目錄的總計。</span><span class="sxs-lookup"><span data-stu-id="72dcd-374">`du –sh .snapshot` provides a total of all snapshots within hello snapshot directory.</span></span>
- <span data-ttu-id="72dcd-375">`du –sh --max-depth=1`列出所有儲存在 hello.snapshot 資料夾和 hello 每個快照集大小的快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-375">`du –sh --max-depth=1` lists all snapshots that are saved in hello .snapshot folder and hello size of each snapshot.</span></span>
- <span data-ttu-id="72dcd-376">`du –hc`提供所有快照集所使用的 hello 總大小。</span><span class="sxs-lookup"><span data-stu-id="72dcd-376">`du –hc` provides hello total size used by all snapshots.</span></span>

<span data-ttu-id="72dcd-377">使用這些命令 toomake 確定 hello 拍攝且儲存的快照集不會耗用 hello 磁碟區上的所有 hello 存放裝置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-377">Use these commands toomake sure that hello snapshots that are taken and stored are not consuming all hello storage on hello volumes.</span></span>

### <a name="reducing-hello-number-of-snapshots-on-a-server"></a><span data-ttu-id="72dcd-378">減少伺服器上的快照集的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="72dcd-378">Reducing hello number of snapshots on a server</span></span>

<span data-ttu-id="72dcd-379">如前所述，您可以減少 hello 數目的快照集儲存特定標籤。</span><span class="sxs-lookup"><span data-stu-id="72dcd-379">As explained earlier, you can reduce hello number of certain labels of snapshots that you store.</span></span> <span data-ttu-id="72dcd-380">hello 最後一個 tooretain hello 命令 tooinitiate 快照集是您想要的快照集標籤和 hello 數目的兩個參數。</span><span class="sxs-lookup"><span data-stu-id="72dcd-380">hello last two parameters of hello command tooinitiate a snapshot are a label and hello number of snapshots you want tooretain.</span></span>
```
./azure_hana_backup.pl lhanad01 customer 20
```
<span data-ttu-id="72dcd-381">Hello 上述範例中，在 hello 快照標籤是_客戶_而且 hello 數目快照集與保留此標籤 toobe _20_。</span><span class="sxs-lookup"><span data-stu-id="72dcd-381">In hello previous example, hello snapshot label is _customer_ and hello number of snapshots with this label toobe retained is _20_.</span></span> <span data-ttu-id="72dcd-382">當您回應 toodisk 空間耗用量，您可能想 tooreduce hello 數量的預存的快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-382">As you respond toodisk space consumption, you might want tooreduce hello number of stored snapshots.</span></span> <span data-ttu-id="72dcd-383">hello tooreduce hello 數目的快照集是 toorun hello 指令碼，最後一個參數集 too5 hello 與簡單的方法：</span><span class="sxs-lookup"><span data-stu-id="72dcd-383">hello easy way tooreduce hello number of snapshots is toorun hello script with hello last parameter set too5:</span></span>
```
./azure_hana_backup.pl lhanad01 customer 5
```
<span data-ttu-id="72dcd-384">執行 hello 指令碼可使用這項設定，因為快照集，包括快照集，hello 新儲存體的 hello 數目了_5_。</span><span class="sxs-lookup"><span data-stu-id="72dcd-384">As a result of running hello script with this setting, hello number of snapshots, including hello new storage snapshot, is _5_.</span></span>

 >[!NOTE]
 > <span data-ttu-id="72dcd-385">只有 hello 最新的上一個快照是超過 1 小時前，此指令碼就會減少 hello 快照集數目。</span><span class="sxs-lookup"><span data-stu-id="72dcd-385">This script reduces hello number of snapshots only if hello most recent previous snapshot is more than one hour old.</span></span> <span data-ttu-id="72dcd-386">hello 指令碼不會刪除少於 1 小時前的快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-386">hello script does not delete snapshots that are less than one hour old.</span></span>

<span data-ttu-id="72dcd-387">這些限制會提供相關的 toohello 選擇性的災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="72dcd-387">These restrictions are related toohello optional disaster-recovery functionality offered.</span></span>

<span data-ttu-id="72dcd-388">如果您不想再 toomaintain 一組前置詞開頭的快照集，您可以執行與 hello 指令碼_0_為 hello 保留編號 tooremove 比對該前置詞的所有快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-388">If you no longer want toomaintain a set of snapshots with that prefix, you can execute hello script with _0_ as hello retention number tooremove all snapshots matching that prefix.</span></span> <span data-ttu-id="72dcd-389">不過，移除所有的快照集可能會影響 hello 災害復原功能。</span><span class="sxs-lookup"><span data-stu-id="72dcd-389">However, removing all snapshots can affect hello capabilities of disaster recovery.</span></span>

### <a name="recovering-toohello-most-recent-hana-snapshot"></a><span data-ttu-id="72dcd-390">復原 toohello 最近 HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-390">Recovering toohello most recent HANA snapshot</span></span>

<span data-ttu-id="72dcd-391">Hello 事件中可以為 Azure 服務管理上的 SAP HANA 客戶事件起始您遇到下實際執行案例、 復原從儲存體的快照集的 「 hello 」 程序。</span><span class="sxs-lookup"><span data-stu-id="72dcd-391">In hello event that you experience a production-down scenario, hello process of recovering from a storage snapshot can be initiated as a customer incident with SAP HANA on Azure Service Management.</span></span> <span data-ttu-id="72dcd-392">如果實際執行系統和 hello 唯一方式 tooretrieve hello 資料是 toorestore hello 生產資料庫中已刪除資料這類的未預期的案例可能高急迫性內容。</span><span class="sxs-lookup"><span data-stu-id="72dcd-392">Such an unexpected scenario might be a high-urgency matter if data was deleted in a production system and hello only way tooretrieve hello data is toorestore hello production database.</span></span>

<span data-ttu-id="72dcd-393">在 hello 相反地，時間點復原可能是低急迫性，天事先計劃。</span><span class="sxs-lookup"><span data-stu-id="72dcd-393">On hello other hand, a point-in-time recovery could be low urgency and planned for days in advance.</span></span> <span data-ttu-id="72dcd-394">您可以使用「SAP HANA on Azure 服務管理」來規劃此復原，以避免引發高優先性的問題。</span><span class="sxs-lookup"><span data-stu-id="72dcd-394">You can plan this recovery with SAP HANA on Azure Service Management instead of raising a high-priority issue.</span></span> <span data-ttu-id="72dcd-395">例如，您可能會藉由套用新的增強功能套件，而且您規劃 tootry hello SAP 軟體升級，然後需要 toorevert 回 tooa 快照集，表示 hello hello EHP 升級前的狀態。</span><span class="sxs-lookup"><span data-stu-id="72dcd-395">For example, you might be planning tootry an upgrade of hello SAP software by applying a new enhancement package, and you then need toorevert back tooa snapshot that represents hello state before hello EHP upgrade.</span></span>

<span data-ttu-id="72dcd-396">發出 hello 要求之前，您需要 toodo 一些準備工作。</span><span class="sxs-lookup"><span data-stu-id="72dcd-396">Before you issue hello request, you need toodo some preparation.</span></span> <span data-ttu-id="72dcd-397">Azure 服務管理小組的 SAP HANA 可以然後處理 hello 要求，並提供 hello 還原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-397">SAP HANA on Azure Service Management team can then handle hello request and provide hello restored volumes.</span></span> <span data-ttu-id="72dcd-398">之後，它是 tooyou toorestore hello HANA 資料庫依據 hello 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-398">Afterward, it is up tooyou toorestore hello HANA database based on hello snapshots.</span></span> <span data-ttu-id="72dcd-399">以下是如何 hello tooprepare 要求：</span><span class="sxs-lookup"><span data-stu-id="72dcd-399">Here is how tooprepare for hello request:</span></span>

>[!NOTE]
><span data-ttu-id="72dcd-400">下列螢幕擷取畫面，根據您使用的 SAP HANA 發行 hello hello 使用者介面可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="72dcd-400">Your user interface might vary from hello following screenshots, depending on hello SAP HANA release you are using.</span></span>

1. <span data-ttu-id="72dcd-401">決定哪些快照 toorestore。</span><span class="sxs-lookup"><span data-stu-id="72dcd-401">Decide which snapshot toorestore.</span></span> <span data-ttu-id="72dcd-402">只有 hello hana/資料磁碟區可以回復，除非所指示。</span><span class="sxs-lookup"><span data-stu-id="72dcd-402">Only hello hana/data volume would be restored unless you are instructed otherwise.</span></span>

2. <span data-ttu-id="72dcd-403">關閉 hello HANA 執行個體。</span><span class="sxs-lookup"><span data-stu-id="72dcd-403">Shut down hello HANA instance.</span></span>

 ![關閉 hello HANA 執行個體](./media/hana-overview-high-availability-disaster-recovery/image7-shutdown-hana.png)

3. <span data-ttu-id="72dcd-405">卸載 hello 資料磁碟區上的每個 HANA 資料庫節點。</span><span class="sxs-lookup"><span data-stu-id="72dcd-405">Unmount hello data volumes on each HANA database node.</span></span> <span data-ttu-id="72dcd-406">無法卸載 hello 資料磁碟區時，就會失敗 hello hello 快照集還原。</span><span class="sxs-lookup"><span data-stu-id="72dcd-406">hello restoration of hello snapshot fails if hello data volumes are not unmounted.</span></span>

 ![卸載 hello 資料磁碟區上每個 HANA 資料庫 節點](./media/hana-overview-high-availability-disaster-recovery/image8-unmount-data-volumes.png)

4. <span data-ttu-id="72dcd-408">開啟 Azure 支援人員要求 tooinstruct hello 還原的特定快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-408">Open an Azure support request tooinstruct hello restoration of a specific snapshot.</span></span>

 - <span data-ttu-id="72dcd-409">Hello 還原期間： Azure 服務管理上的 SAP HANA 可能會要求您 tooattend 沒有資料會迷失方向電話會議 tooensure。</span><span class="sxs-lookup"><span data-stu-id="72dcd-409">During hello restoration: SAP HANA on Azure Service Management might ask you tooattend a conference call tooensure that no data is getting lost.</span></span>

 - <span data-ttu-id="72dcd-410">Hello 還原後： hello 儲存體快照還原時 Azure 服務管理上的 SAP HANA 通知您。</span><span class="sxs-lookup"><span data-stu-id="72dcd-410">After hello restoration: SAP HANA on Azure Service Management notifies you when hello storage snapshot has been restored.</span></span>

5. <span data-ttu-id="72dcd-411">Hello 還原程序完成之後，重新掛接所有資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="72dcd-411">After hello restoration process is complete, remount all data volumes.</span></span>

 ![重新掛接所有資料磁碟區](./media/hana-overview-high-availability-disaster-recovery/image9-remount-data-volumes.png)

6. <span data-ttu-id="72dcd-413">如果它們沒有自動顯示當您重新連接到 SAP HANA Studio tooHANA DB，請選取 SAP HANA Studio 中的復原選項。</span><span class="sxs-lookup"><span data-stu-id="72dcd-413">Select recovery options within SAP HANA Studio, if they do not automatically come up when you reconnect tooHANA DB through SAP HANA Studio.</span></span> <span data-ttu-id="72dcd-414">hello 下列範例顯示還原 toohello 最後 HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-414">hello following example shows a restoration toohello last HANA snapshot.</span></span> <span data-ttu-id="72dcd-415">儲存體的快照集嵌入一個 HANA 快照集，且如果您要還原 toohello 最新的儲存體快照集，應 hello 最近 HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-415">A storage snapshot embeds one HANA snapshot, and if you are restoring toohello most recent storage snapshot, it should be hello most recent HANA snapshot.</span></span> <span data-ttu-id="72dcd-416">(如果您要還原 tooolder 儲存快照集，您需要 toolocate hello HANA 根據 hello 時間 hello 儲存快照集的快照。)</span><span class="sxs-lookup"><span data-stu-id="72dcd-416">(If you are restoring tooolder storage snapshots, you need toolocate hello HANA snapshot based on hello time hello storage snapshot was taken.)</span></span>

 ![選取 SAP HANA Studio 內的復原選項](./media/hana-overview-high-availability-disaster-recovery/image10-recover-options-a.png)

7. <span data-ttu-id="72dcd-418">選取**復原 hello 資料庫 tooa 特定資料備份或儲存體快照集**。</span><span class="sxs-lookup"><span data-stu-id="72dcd-418">Select **Recover hello database tooa specific data backup or storage snapshot**.</span></span>

 ![hello [指定復原類型] 視窗](./media/hana-overview-high-availability-disaster-recovery/image11-recover-options-b.png)

8. <span data-ttu-id="72dcd-420">選取 [指定不含目錄的備份]。</span><span class="sxs-lookup"><span data-stu-id="72dcd-420">Select **Specify backup without catalog**.</span></span>

 ![hello [指定備份位置] 視窗](./media/hana-overview-high-availability-disaster-recovery/image12-recover-options-c.png)

9. <span data-ttu-id="72dcd-422">在 hello**目的型別**清單中，選取**快照**。</span><span class="sxs-lookup"><span data-stu-id="72dcd-422">In hello **Destination Type** list, select **Snapshot**.</span></span>

 ![hello 」 指定 hello 備份 tooRecover 」 視窗](./media/hana-overview-high-availability-disaster-recovery/image13-recover-options-d.png)

10. <span data-ttu-id="72dcd-424">按一下**完成**toostart hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="72dcd-424">Click **Finish** toostart hello recovery process.</span></span>

 ![按一下 [完成] 的 toostart hello 復原程序](./media/hana-overview-high-availability-disaster-recovery/image14-recover-options-e.png)

11. <span data-ttu-id="72dcd-426">hello HANA 資料庫還原並復原 toohello HANA 快照集包含在 hello 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-426">hello HANA database is restored and recovered toohello HANA snapshot that's included in hello storage snapshot.</span></span>

 ![HANA 資料庫會還原並復原 toohello HANA 快照集](./media/hana-overview-high-availability-disaster-recovery/image15-recover-options-f.png)

### <a name="recovering-toohello-most-recent-state"></a><span data-ttu-id="72dcd-428">復原 toohello 最新狀態</span><span class="sxs-lookup"><span data-stu-id="72dcd-428">Recovering toohello most recent state</span></span>

<span data-ttu-id="72dcd-429">hello 下列程序還原 hello HANA 快照集包含在 hello 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-429">hello following process restores hello HANA snapshot that is included in hello storage snapshot.</span></span> <span data-ttu-id="72dcd-430">然後會還原 hello 儲存快照集之前先還原 hello 交易記錄備份 toohello 最近 hello 資料庫狀態。</span><span class="sxs-lookup"><span data-stu-id="72dcd-430">It then restores hello transaction log backups toohello most recent state of hello database before restoring hello storage snapshot.</span></span>

>[!IMPORTANT]
><span data-ttu-id="72dcd-431">繼續進行之前，請先確定您擁有一串完整且連續的交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-431">Before you proceed, make sure that you have a complete and contiguous chain of transaction log backups.</span></span> <span data-ttu-id="72dcd-432">沒有這些備份，您無法還原 hello hello 資料庫目前狀態。</span><span class="sxs-lookup"><span data-stu-id="72dcd-432">Without these backups, you cannot restore hello current state of hello database.</span></span>

1. <span data-ttu-id="72dcd-433">完成步驟 1-6 的 hello 前面程序在 「 正在復原 toohello 最近 HANA 快照集。 」</span><span class="sxs-lookup"><span data-stu-id="72dcd-433">Complete steps 1-6 of hello preceding procedure in "Recovering toohello most recent HANA snapshot."</span></span>

2. <span data-ttu-id="72dcd-434">選取**復原 hello 資料庫 tooits 最新狀態**。</span><span class="sxs-lookup"><span data-stu-id="72dcd-434">Select **Recover hello database tooits most recent state**.</span></span>

 ![選取 「 Recover hello 資料庫 tooits 最新狀態 」](./media/hana-overview-high-availability-disaster-recovery/image16-recover-database-a.png)

3. <span data-ttu-id="72dcd-436">指定 hello hello 最近 HANA 記錄備份的位置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-436">Specify hello location of hello most recent HANA log backups.</span></span> <span data-ttu-id="72dcd-437">hello 位置需要 toocontain 所有 HANA 交易記錄備份，從 hello HANA 快照 toohello 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="72dcd-437">hello location needs toocontain all HANA transaction log backups from hello HANA snapshot toohello most recent state.</span></span>

 ![指定 hello hello 最近 HANA 記錄備份的位置](./media/hana-overview-high-availability-disaster-recovery/image17-recover-database-b.png)

4. <span data-ttu-id="72dcd-439">選取的備份當做基底從哪一個 toorecover hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="72dcd-439">Select a backup as a base from which toorecover hello database.</span></span> <span data-ttu-id="72dcd-440">在本例中，這是隨附在 hello 儲存快照集的 hello HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-440">In our example, this is hello HANA snapshot that was included in hello storage snapshot.</span></span> <span data-ttu-id="72dcd-441">（只有一個快照集被列在下列螢幕擷取畫面的 hello）。</span><span class="sxs-lookup"><span data-stu-id="72dcd-441">(Only one snapshot is listed in hello following screenshot.)</span></span>

 ![選取的備份當做基底從哪一個 toorecover hello 資料庫](./media/hana-overview-high-availability-disaster-recovery/image18-recover-database-c.png)

5. <span data-ttu-id="72dcd-443">清除 hello**使用差異備份**核取方塊，當 hello hello HANA 快照集時間 hello 最新狀態之間沒有差異。</span><span class="sxs-lookup"><span data-stu-id="72dcd-443">Clear hello **Use Delta Backups** check box if deltas do not exist between hello time of hello HANA snapshot and hello most recent state.</span></span>

 ![如果沒有差異存在清除 hello < 使用差異備份 」 核取方塊](./media/hana-overview-high-availability-disaster-recovery/image19-recover-database-d.png)

6. <span data-ttu-id="72dcd-445">在 hello 摘要畫面中，按一下 **完成**toostart hello 還原程序。</span><span class="sxs-lookup"><span data-stu-id="72dcd-445">On hello summary screen, click **Finish** toostart hello restoration procedure.</span></span>

 ![Hello 摘要畫面上，按一下 [完成]](./media/hana-overview-high-availability-disaster-recovery/image20-recover-database-e.png)

### <a name="recovering-tooanother-point-in-time"></a><span data-ttu-id="72dcd-447">復原時間 tooanother 點</span><span class="sxs-lookup"><span data-stu-id="72dcd-447">Recovering tooanother point in time</span></span>
<span data-ttu-id="72dcd-448">toorecover tooa hello HANA 快照集 （包含在 hello 儲存快照集） 之間，則晚於 hello HANA 快照集時間點復原的時間點 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="72dcd-448">toorecover tooa point in time between hello HANA snapshot (included in hello storage snapshot) and one that is later than hello HANA snapshot point-in-time recovery, do hello following:</span></span>

1. <span data-ttu-id="72dcd-449">請確定您有從您想要 toorecover hello HANA 快照集 toohello 時間的所有交易記錄備份。</span><span class="sxs-lookup"><span data-stu-id="72dcd-449">Make sure that you have all transaction log backups from hello HANA snapshot toohello time you want toorecover.</span></span>
2. <span data-ttu-id="72dcd-450">開始 hello 程序在 「 正在復原 toohello 最新狀態。 」</span><span class="sxs-lookup"><span data-stu-id="72dcd-450">Begin hello procedure under "Recovering toohello most recent state."</span></span>
3. <span data-ttu-id="72dcd-451">在步驟 2 中 hello hello 程序，**指定復原類型**視窗中，選取**時間點復原 hello 資料庫 toohello 下列**，指定的時間，hello 點，然後完成 步驟 3 到 6。</span><span class="sxs-lookup"><span data-stu-id="72dcd-451">In step 2 of hello procedure, in hello **Specify Recovery Type** window, select **Recover hello database toohello following point in time**, specify hello point in time, and then complete steps 3-6.</span></span>

## <a name="monitoring-hello-execution-of-snapshots"></a><span data-ttu-id="72dcd-452">監視 hello 執行快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-452">Monitoring hello execution of snapshots</span></span>

<span data-ttu-id="72dcd-453">您需要儲存體的快照集 toomonitor hello 的執行。</span><span class="sxs-lookup"><span data-stu-id="72dcd-453">You need toomonitor hello execution of storage snapshots.</span></span> <span data-ttu-id="72dcd-454">hello 指令碼執行的儲存體快照集將寫入輸出 tooa 檔案，然後將它儲存 toohello hello Perl 指令碼相同的位置。</span><span class="sxs-lookup"><span data-stu-id="72dcd-454">hello script that executes a storage snapshot writes output tooa file and then saves it toohello same location as hello Perl scripts.</span></span> <span data-ttu-id="72dcd-455">針對每個快照都會寫入一個個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="72dcd-455">A separate file is written for each snapshot.</span></span> <span data-ttu-id="72dcd-456">每個檔案的 hello 輸出會清楚地顯示 hello hello 快照集指令碼執行的各階段：</span><span class="sxs-lookup"><span data-stu-id="72dcd-456">hello output of each file clearly shows hello various phases that hello snapshot script executes:</span></span>

- <span data-ttu-id="72dcd-457">尋找需要 toocreate hello 磁碟區快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-457">Finding hello volumes that need toocreate a snapshot</span></span>
- <span data-ttu-id="72dcd-458">尋找 hello 取自這些磁碟區的快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-458">Finding hello snapshots taken from these volumes</span></span>
- <span data-ttu-id="72dcd-459">刪除最終現有快照集 toomatch hello 的快照集數目指定</span><span class="sxs-lookup"><span data-stu-id="72dcd-459">Deleting eventual existing snapshots toomatch hello number of snapshots you specified</span></span>
- <span data-ttu-id="72dcd-460">建立 HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-460">Creating a HANA snapshot</span></span>
- <span data-ttu-id="72dcd-461">Hello 磁碟區上建立 hello 儲存快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-461">Creating hello storage snapshot over hello volumes</span></span>
- <span data-ttu-id="72dcd-462">刪除 hello HANA 快照集</span><span class="sxs-lookup"><span data-stu-id="72dcd-462">Deleting hello HANA snapshot</span></span>
- <span data-ttu-id="72dcd-463">重新命名 hello 最新快照集太**.0**</span><span class="sxs-lookup"><span data-stu-id="72dcd-463">Renaming hello most recent snapshot too**.0**</span></span>

<span data-ttu-id="72dcd-464">這是最重要的部分 hello hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="72dcd-464">hello most important part of hello script is this:</span></span>
```
**********************Creating HANA snapshot**********************
Creating hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data create snapshot"" ...
HANA snapshot created successfully.
**********************Creating Storage snapshot**********************
Taking snapshot hourly.recent for hana_data_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_backup_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_log_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for hana_shared_lhanad01_t020_vol ...
Snapshot created successfully.
Taking snapshot hourly.recent for sapmnt_lhanad01_t020_vol ...
Snapshot created successfully.
**********************Deleting HANA snapshot**********************
Deleting hello HANA snapshot with command: "./hdbsql -n localhost -i 01 -U SCADMIN01 "backup data drop snapshot"" ...
HANA snapshot deletion successfully.
```
<span data-ttu-id="72dcd-465">您可以看到與此範例如何 hello 指令碼記錄 hello hello HANA 快照集建立。</span><span class="sxs-lookup"><span data-stu-id="72dcd-465">You can see from this sample how hello script records hello creation of hello HANA snapshot.</span></span> <span data-ttu-id="72dcd-466">在 hello 向外延展的情況下，此程序被起始 hello 主要節點上。</span><span class="sxs-lookup"><span data-stu-id="72dcd-466">In hello scale-out case, this process is initiated on hello master node.</span></span> <span data-ttu-id="72dcd-467">hello 主要節點會起始 hello 同步建立 hello 快照集，每個 hello 背景工作節點上。</span><span class="sxs-lookup"><span data-stu-id="72dcd-467">hello master node initiates hello synchronous creation of hello snapshots on each of hello worker nodes.</span></span> <span data-ttu-id="72dcd-468">然後會採取 hello 儲存快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-468">Then hello storage snapshot is taken.</span></span> <span data-ttu-id="72dcd-469">Hello 成功執行之後 hello 儲存快照集，會刪除 hello HANA 快照集。</span><span class="sxs-lookup"><span data-stu-id="72dcd-469">After hello successful execution of hello storage snapshots, hello HANA snapshot is deleted.</span></span>
