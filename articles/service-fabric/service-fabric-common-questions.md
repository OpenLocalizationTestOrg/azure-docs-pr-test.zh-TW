---
title: "Microsoft Azure Service Fabric 的 aaaCommon 疑問 |Microsoft 文件"
description: "和 Service Fabric 有關的常見問題集和解答"
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 5a179703-ff0c-4b8e-98cd-377253295d12
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: chackdan
ms.openlocfilehash: 4cbe92d2a03f7a1ea5d077807fdc982288220a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="commonly-asked-service-fabric-questions"></a>Service Fabric 的常見問題

和 Service Fabric 的功能及使用方式有關的常見問題很多。 本文件涵蓋許多這類問題和解答。

## <a name="cluster-setup-and-management"></a>叢集設定和管理

### <a name="can-i-create-a-cluster-that-spans-multiple-azure-regions-or-my-own-datacenters"></a>我能否建立跨多個 Azure 區域或自有資料中心的叢集？

是。 

可以使用的 toocombine 機器於任何地方執行 hello world hello 核心 Service Fabric 叢集技術，只要有網路連線 tooeach 其他。 不過，建置和執行這類叢集的程序很複雜。

如果您想要在此案例中，我們鼓勵您 tooget 連絡透過 hello[服務網狀架構 Github 問題清單](https://github.com/azure/service-fabric-issues)或透過您在順序 tooobtain 其他指南中的支援人員。 hello Service Fabric 小組 tooprovide 其他清晰度、 指引和建議這種情況下的處理。 

某些事項 tooconsider: 

1. hello Azure Service Fabric 叢集資源今天是地區，因為 hello 虛擬機器擴展集該 hello 叢集上建立。 這表示 hello 地區失敗事件中您可能會遺失 hello 能力 toomanage hello 叢集 hello Azure 資源管理員透過或 hello Azure 入口網站。 即使 hello 叢集仍繼續執行，而系統會直接將無法與它 toointeract，也可能會發生。 此外，Azure 目前不提供 hello 能力 toohave 跨區域可供使用的單一虛擬網路。 這表示，在 Azure 中的多地區叢集需要[hello VM 規模集的每個 VM 的公用 IP 位址](../virtual-machine-scale-sets/virtual-machine-scale-sets-networking.md#public-ipv4-per-virtual-machine)或[Azure VPN 閘道](../vpn-gateway/vpn-gateway-about-vpngateways.md)。 這些網路選擇在成本、 效能及 toosome 程度應用程式設計，擁有不同的影響，因此這類環境是在幾之前，需要仔細分析和規劃。
2. hello 維護、 管理和監視這些電腦可能會變得複雜，特別是當跨越_類型_的環境，例如不同雲端提供者之間，或在內部部署資源和 Azure 之間. 必須小心 tooensure 升級、 監視、 管理和診斷執行這類環境中的實際執行工作負載之前，了解 hello 叢集和 hello 應用程式。 如果您對於在 Azure 或您自己的資料中心內解決這些問題已有豐富經驗，則在建置或執行 Service Fabric 叢集時或許也可以套用同樣的一套解決方案。 

### <a name="do-service-fabric-nodes-automatically-receive-os-updates"></a>Service Fabric 節點是否會自動接收作業系統更新？

不今天，但這也是 Azure 打算 toodeliver 最常見的要求。

Hello 過渡版，有[提供應用程式](service-fabric-patch-orchestration-application.md)hello 作業系統在 Service Fabric 節點下面保持修補和 toodate 組成。

與作業系統更新的 hello 挑戰是它們通常需要重新開機的 hello 機器，會導致失去暫存的可用性。 單獨使用時，不是問題，因為 Service Fabric 會自動將流量重新導向的那些服務 tooother 節點。 不過，如果 OS 更新不會協調 hello 叢集中，是許多節點到下一次的 hello 可能性。 這類同時重新啟動會造成服務，或至少造成某個特定分割 (如果為具狀態服務) 完全失去可用性。

在 hello 未來，我們計劃 toosupport OS 更新原則完全自動化並協調跨越更新網域，確保即使重新啟動和其他非預期的失敗都能維持可用性。

### <a name="can-i-use-large-virtual-machine-scale-sets-in-my-sf-cluster"></a>我可以在 SF 叢集中使用大型虛擬機器擴展集嗎？ 

**簡短回答** - 否。 

**長時間回答**-雖然 hello 大型虛擬機器擴展集可讓您 tooscale 的虛擬機器擴展集最多 1000 VM 執行個體，它會 hello 使用放置群組 (PGs)。 容錯網域 (Fd) 和升級網域 (Ud) 只一致內放置群組服務網狀架構會使用您的服務複本/服務執行個體的 Fd 和 Ud toomake 設置決策。 因為 hello Fd 和 Ud 是比較只能放置在群組內是 SF 無法使用它。 例如，如果 VM1 PG1 中的擁有的 FD 拓撲 = 0 和 VM9 PG2 中的擁有的 FD 拓撲 = 4，並不表示 VM1 和 vm2 的情況是在兩個不同硬體機架，因此 SF 時，無法在此案例 toomake 設置決策中使用 hello FD 值。

大型虛擬機器規模集的其他問題目前沒有，像是層級 4 的 hello 缺乏負載平衡支援。 請參閱 toofor[大型的詳細資訊的調整規模設定](../virtual-machine-scale-sets/virtual-machine-scale-sets-placement-groups.md)



### <a name="what-is-hello-minimum-size-of-a-service-fabric-cluster-why-cant-it-be-smaller"></a>Hello Service Fabric 叢集的最小的大小為何？ 為什麼無法更小？

hello 支援最小執行生產工作負載的 Service Fabric 叢集是五個節點。 針對開發/測試案例，我們支援三個節點的叢集。

這些最小值存在，因為 hello Service Fabric 叢集會執行一組可設定狀態系統服務，包括 hello 命名服務和 hello 容錯移轉管理員。 這些服務，追蹤服務都已部署 toohello 叢集，而且在目前裝載它們，取決於強式一致性。 該強式一致性，接著，取決於 hello 能力 tooacquire*仲裁*取得任何給定的更新 toohello 狀態，這些服務，其中仲裁代表 hello 複本 (N/2 + 1) 指定服務的嚴格多數。

了解該背景後，讓我們來檢查一些可能的叢集組態：

**一個節點**： 這個選項不提供高可用性，因為 hello 遺失 hello 單一節點因任何原因表示 hello hello 整個叢集遺失。

**兩個節點**︰跨兩個節點 (N = 2) 部署的服務，仲裁為 2 (2/2 + 1 = 2)。 遺失的單一複本時，它是不可能 toocreate 仲裁。 由於執行服務升級時需要暫時關閉複本，因此這不是有用的組態。

**三個節點**： 三個節點 (N = 3)，與 hello 需求 toocreate 仲裁仍然是兩個節點 (3/2 + 1 = 2)。 這表示您可以遺失一個單一節點，並且仍維持仲裁。

hello 三個節點叢集組態支援開發/測試安全無虞地執行升級，並不受個別的節點失敗，因為只要它們不同時進行。 對於生產工作負載，您必須是具有恢復功能 toosuch 同時失敗，因此五個節點都是必要。

### <a name="can-i-turn-off-my-cluster-at-nightweekends-toosave-costs"></a>我可以關閉我在晚上/週末 toosave 成本的叢集嗎？

一般而言不行。 Service Fabric 將狀態儲存在本機的暫時磁碟上，這表示，如果 hello 虛擬機器移動的 tooa 不同的主機，hello 資料不會移動它。 在正常作業中，，並不是問題如 hello 新節點處於向上 toodate，由其他節點。 不過，如果您停止所有節點，並稍後再重新啟動，是重要的可能性 hello 節點的最新的主機上啟動，並進行 hello 系統無法 toorecover。

如果您想要 toocreate 叢集部署之前測試應用程式，我們建議您以動態方式建立這些叢集的一部分您[連續連續整合/部署管線](service-fabric-set-up-continuous-integration.md)。


### <a name="how-do-i-upgrade-my-operating-system-for-example-from-windows-server-2012-toowindows-server-2016"></a>如何升級我的作業系統 （例如從 Windows Server 2012 tooWindows Server 2016)？

我們在處理時的增強經驗，現在，您必須負責 hello 升級。 您必須先升級 hello OS 映像 hello 上的一次叢集一個 VM 的虛擬機器的 hello。 

## <a name="container-support"></a>容器支援

### <a name="why-are-my-containers-that-are-deployed-toosf-unable-tooresolve-dns-addresses"></a>為何我容器部署的 tooSF 無法 tooresolve DNS 位址？

已有人針對 5.6.204.9494 版的叢集回報這個問題 

**風險降低**： 遵循[這份文件](service-fabric-dnsservice.md)tooenable hello DNS 服務在叢集中的網狀架構服務。

**修正**： 支援的升級 tooa 叢集版本高於 5.6.204.9494，可供使用。 如果您的叢集設定 tooautomatic 升級，hello 叢集將會自動升級 toohello 版本已修正此問題。

  
## <a name="application-design"></a>應用程式設計

### <a name="whats-hello-best-way-tooquery-data-across-partitions-of-a-reliable-collection"></a>什麼是最佳方式 tooquery 資料 hello 可靠集合的資料分割

可靠的集合通常是[分割](service-fabric-concepts-partitioning.md)tooenable 向外延展的更大的效能和輸送量。 這表示特定服務的 hello 狀態可能散佈 10s 或 100 的機器。 透過完整資料集 tooperform 作業，您有幾個選項：

- 建立查詢的另一個服務 toopull hello 所需的資料中的所有資料分割的服務。
- 建立可接收來自另一個服務所有分割之資料的服務。
- 從每個服務 tooan 外部儲存區定期推播資料。 這個方法僅適用於您要執行 hello 查詢不是核心商務邏輯的一部分。


### <a name="whats-hello-best-way-tooquery-data-across-my-actors"></a>什麼是我執行者跨 hello 最佳方式 tooquery 資料

執行者是設計的 toobe 獨立單位的狀態和計算，所以不建議使用 tooperform 廣泛查詢在執行階段的動作項目狀態。 如果您有需要 tooquery 跨 hello 整組動作項目狀態時，您應該考慮是：

- 使 hello 的網路要求數目 toogather 所有資料從服務中的資料分割的執行者 toohello 數目的 hello 數目取代可靠的服務可設定狀態，您的行動服務。
- 設計您執行者 tooperiodically 推入其狀態 tooan 外部存放區查詢更容易。 為上方，這種方法才可行，如果您要執行 hello 查詢不是必要的執行階段行為。

### <a name="how-much-data-can-i-store-in-a-reliable-collection"></a>可靠的集合中能夠儲存多少資料？

可靠的服務通常會進行分割，因此您可以儲存的 hello 量只受限於 hello 您擁有 hello 叢集中的機器的數目和 hello 可用記憶體數量在電腦上。

例如，假設您在服務中擁有的可靠集合含有 100 個分割及 3 個複本，儲存的物件大小平均為 1kb。 現在，假設您有 10 部機器的叢集，每部機器均含有 16GB 記憶體。 為了簡化和 toobe 的非常保守，假設 hello 作業系統和系統服務、 hello Service Fabric 執行階段，以及您的服務使用 6 gb 的離開 hello 叢集的每部電腦，可用的 10 gb 或 100 gb。

請記住，每個物件必須儲存三次 (一次主要，兩次複本)，在以完整容量運作的情況下，您會有足夠的記憶體提供您集合中大約 3500 萬個物件使用。 不過，我們建議的彈性 toohello 同時遺失的故障網域和升級網域，代表約 1/3 的容量，並且會減少 hello 數字 tooroughly 23 百萬個。

請注意，這項計算也假設：

- Hello hello 資料分割的資料分佈是大約一致，或您正在回報負載度量 toohello 叢集資源管理員。 根據預設，Service Fabric 會根據複本數量進行負載平衡。 在上述範例中，，它會施加 hello 叢集中的每個節點上的 10 個主要複本和 20 的次要複本。 適用於已平均分配 hello 資料分割的負載。 如果負載是不在偶數，您必須回報負載，讓 hello 資源管理員可以封裝在一起的較小的複本並允許較大的複本 tooconsume 上的個別節點的更多記憶體。

- Hello 可靠的服務有問題的 hello 只能有一個儲存的狀態 hello 叢集中。 由於您可以部署多個服務 tooa 叢集時，您必須 toobe 表達 hello 資源，則每個將會需要 toorun，並管理其狀態。

- 該 hello 叢集本身不是擴大或縮小。 如果您加入更多電腦，Service Fabric 會重新平衡您複本 tooleverage hello 額外容量直到 hello 機器的數目超出您的服務中的資料分割的 hello 數目，因為的個別複本無法跨越電腦。 相反地，如果您藉由移除機器減少 hello hello 叢集大小，複本將會更緊密地壓縮，並具有較少的整體容量。

### <a name="how-much-data-can-i-store-in-an-actor"></a>動作項目中可儲存多少資料？

如同可靠的服務資料，您可以儲存在行動服務中的 hello 數量只受限於 hello 總磁碟空間和可用記憶體 hello 您的叢集節點之間。 不過，個別的執行者時最有效時，它們使用的 tooencapsulate 少量的狀態和相關聯的商務邏輯。 一般而言，個別的動作項目應該會有以 kb 為單位所測量的狀態。

## <a name="other-questions"></a>其他問題

### <a name="how-does-service-fabric-relate-toocontainers"></a>Service Fabric 如何與 toocontainers？

容器可提供簡單的方式 toopackage 服務和其相依性以一致的方式在所有的環境中執行，並且可以在單一電腦上隔離的方式運作。 Service Fabric 提供方式 toodeploy 及管理服務，包括[已包裝在容器中的服務](service-fabric-containers-overview.md)。

### <a name="are-you-planning-tooopen-source-service-fabric"></a>您計劃 tooopen 來源 Service Fabric 嗎？

我們想在 GitHub 上的 tooopen 來源 hello 可靠的服務和可靠的動作項目架構並將接受社群投稿文章 toothose 專案。 請遵循 hello [Service Fabric 部落格](https://blogs.msdn.microsoft.com/azureservicefabric/)如需詳細資訊，因為它們宣布。

hello 是目前沒有計劃 tooopen 來源 hello Service Fabric 執行階段。

## <a name="next-steps"></a>後續步驟

- [深入了解核心 Service Fabric 概念和最佳做法 (英文)](https://mva.microsoft.com/en-us/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965)
