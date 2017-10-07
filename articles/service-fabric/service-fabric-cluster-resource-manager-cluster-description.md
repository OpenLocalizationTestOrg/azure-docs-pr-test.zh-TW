---
title: "aaaCluster 資源管理員叢集描述 |Microsoft 文件"
description: "藉由指定容錯網域、 升級 」 網域，節點屬性，以及節點容量 hello 叢集資源管理員說明 Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="f4164-103">描述 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="f4164-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="f4164-104">hello Service Fabric 叢集資源管理員會提供數種機制，用來描述叢集。</span><span class="sxs-lookup"><span data-stu-id="f4164-104">hello Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="f4164-105">在執行階段 hello 叢集資源管理員會使用此資訊 tooensure 高可用性的 hello 服務 hello 叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="f4164-105">During runtime, hello Cluster Resource Manager uses this information tooensure high availability of hello services running in hello cluster.</span></span> <span data-ttu-id="f4164-106">同時強制執行這些重要的規則，它也會嘗試 hello 叢集內的 toooptimize hello 資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="f4164-106">While enforcing these important rules, it also attempts toooptimize hello resource consumption within hello cluster.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="f4164-107">重要概念</span><span class="sxs-lookup"><span data-stu-id="f4164-107">Key concepts</span></span>
<span data-ttu-id="f4164-108">hello 叢集資源管理員支援數個特徵來描述叢集：</span><span class="sxs-lookup"><span data-stu-id="f4164-108">hello Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="f4164-109">容錯網域</span><span class="sxs-lookup"><span data-stu-id="f4164-109">Fault Domains</span></span>
* <span data-ttu-id="f4164-110">升級網域</span><span class="sxs-lookup"><span data-stu-id="f4164-110">Upgrade Domains</span></span>
* <span data-ttu-id="f4164-111">節點屬性</span><span class="sxs-lookup"><span data-stu-id="f4164-111">Node Properties</span></span>
* <span data-ttu-id="f4164-112">節點容量</span><span class="sxs-lookup"><span data-stu-id="f4164-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="f4164-113">容錯網域</span><span class="sxs-lookup"><span data-stu-id="f4164-113">Fault domains</span></span>
<span data-ttu-id="f4164-114">容錯網域是任何連鎖故障區域。</span><span class="sxs-lookup"><span data-stu-id="f4164-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="f4164-115">一部電腦是 「 故障 」 網域，（因為它可能無法在它自己的各種理由，從電源供應器失敗 toodrive 失敗 toobad NIC 韌體）。</span><span class="sxs-lookup"><span data-stu-id="f4164-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures toodrive failures toobad NIC firmware).</span></span> <span data-ttu-id="f4164-116">機器相同的乙太網路交換器是能力的中的連接的 toohello hello 做為相同容錯網域，是能力的共用單一來源，或在單一位置的機器。</span><span class="sxs-lookup"><span data-stu-id="f4164-116">Machines connected toohello same Ethernet switch are in hello same Fault Domain, as are machines sharing a single source of power or in a single location.</span></span> <span data-ttu-id="f4164-117">因為這是理所當然的硬體錯誤 toooverlap，容錯網域是原本就是以階層方式和它們以服務的網狀架構中的 Uri。</span><span class="sxs-lookup"><span data-stu-id="f4164-117">Since it's natural for hardware faults toooverlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="f4164-118">請務必確認容錯網域中正確設定了因為服務網狀架構會使用此資訊 toosafely 位置服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-118">It is important that Fault Domains are set up correctly since Service Fabric uses this information toosafely place services.</span></span> <span data-ttu-id="f4164-119">Service Fabric 不希望 tooplace 服務，例如 hello 遺失的 「 故障 」 網域 （某個元件的 hello 失敗所造成） 會導致服務 toogo 向下。</span><span class="sxs-lookup"><span data-stu-id="f4164-119">Service Fabric doesn't want tooplace services such that hello loss of a Fault Domain (caused by hello failure of some component) causes a service toogo down.</span></span> <span data-ttu-id="f4164-120">在 hello Azure Service Fabric 會使用所提供的 hello 環境 toocorrectly hello 容錯網域資訊的環境設定 hello hello 叢集中的節點代表您。</span><span class="sxs-lookup"><span data-stu-id="f4164-120">In hello Azure environment Service Fabric uses hello Fault Domain information provided by hello environment toocorrectly configure hello nodes in hello cluster on your behalf.</span></span> <span data-ttu-id="f4164-121">服務網狀架構獨立的容錯網域會定義在 hello 階段設定該 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="f4164-121">For Service Fabric Standalone, Fault Domains are defined at hello time that hello cluster is set up</span></span> 

> [!WARNING]
> <span data-ttu-id="f4164-122">請務必該 hello 容錯網域資訊提供 tooService 網狀架構的精確度。</span><span class="sxs-lookup"><span data-stu-id="f4164-122">It is important that hello Fault Domain information provided tooService Fabric is accurate.</span></span> <span data-ttu-id="f4164-123">例如，假設 Service Fabric 叢集是在 10 部虛擬機器上執行，這些虛擬機器是在五個實體主機上執行。</span><span class="sxs-lookup"><span data-stu-id="f4164-123">For example, let's say that your Service Fabric cluster's nodes are running inside 10 virtual machines, running on five physical hosts.</span></span> <span data-ttu-id="f4164-124">在此情況下，即使有 10 部虛擬機器，也只有 5 個不同的 (最上層) 容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-124">In this case, even though there are 10 virtual machines, there's only 5 different (top level) fault domains.</span></span> <span data-ttu-id="f4164-125">共用相同的實體主機造成的 hello Vm tooshare hello 相同的根容錯網域，因為 Vm 經驗 hello 協調失敗，其實體主機失敗時。</span><span class="sxs-lookup"><span data-stu-id="f4164-125">Sharing hello same physical host causes VMs tooshare hello same root fault domain, since hello VMs experience coordinated failure if their physical host fails.</span></span>  
>
> <span data-ttu-id="f4164-126">因為 Service Fabric 需要 hello 不 toochange 節點的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-126">Since Service Fabric expects hello Fault Domain of a node not toochange.</span></span> <span data-ttu-id="f4164-127">確保高可用性的 hello 的 Vm，這類的其他機制[HA Vm](https://technet.microsoft.com/en-us/library/cc967323.aspx)，使用從一部主機 tooanother 透明移轉 Vm。</span><span class="sxs-lookup"><span data-stu-id="f4164-127">Other mechanisms of ensuring high availability of hello VMs, such as [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use transparent migration of VMs from one host tooanother.</span></span> <span data-ttu-id="f4164-128">這些機制不要重新設定或通知 hello 執行 hello VM 內的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f4164-128">These mechanisms do not reconfigure or notify hello running code inside hello VM.</span></span> <span data-ttu-id="f4164-129">因此，它們**不支援**作為執行中 Service Fabric 叢集的環境。</span><span class="sxs-lookup"><span data-stu-id="f4164-129">As such, they are **not supported** as environments for running Service Fabric clusters.</span></span> <span data-ttu-id="f4164-130">Service Fabric 應該採用的 hello 僅高可用性技術。</span><span class="sxs-lookup"><span data-stu-id="f4164-130">Service Fabric should be hello only high-availability technology employed.</span></span> <span data-ttu-id="f4164-131">不需要像是即時 VM 移轉、SAN 或其他項目的機制。</span><span class="sxs-lookup"><span data-stu-id="f4164-131">Mechanisms like live VM migration, SANs, or others are not necessary.</span></span> <span data-ttu-id="f4164-132">如果與 Service Fabric 搭配使用，這些機制會_減少_應用程式可用性和可靠性，因為它們會導致額外的複雜性、新增集中式失敗來源，並且使用與 Service Fabric 衝突的可靠性和可用性策略。</span><span class="sxs-lookup"><span data-stu-id="f4164-132">If used in conjunction with Service Fabric, these mechanisms _reduce_ application availability and reliability because they introduce additional complexity, add centralized sources of failure, and utilize reliability and availability strategies that conflict with those in Service Fabric.</span></span> 
>
>

<span data-ttu-id="f4164-133">在 hello 圖所示我們色彩所有 hello 實體構成 tooFault 網域及清單所有 hello 所產生的不同容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-133">In hello graphic below we color all hello entities that contribute tooFault Domains and list all hello different Fault Domains that result.</span></span> <span data-ttu-id="f4164-134">在此範例中，我們有資料中心 ("DC")、機架 ("R") 和刀鋒伺服器 ("B")。</span><span class="sxs-lookup"><span data-stu-id="f4164-134">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="f4164-135">理論上，如果每個刀鋒視窗會保留多個虛擬機器，可能有另一個圖層 hello 容錯網域階層中。</span><span class="sxs-lookup"><span data-stu-id="f4164-135">Conceivably, if each blade holds more than one virtual machine, there could be another layer in hello Fault Domain hierarchy.</span></span>

<span data-ttu-id="f4164-136"><center>
![透過容錯網域組織的節點][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-136"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="f4164-137">在執行階段 hello Service Fabric 叢集資源管理員會考慮 hello hello 叢集中的容錯網域，並計劃配置。</span><span class="sxs-lookup"><span data-stu-id="f4164-137">During runtime, hello Service Fabric Cluster Resource Manager considers hello Fault Domains in hello cluster and plans layouts.</span></span> <span data-ttu-id="f4164-138">hello 可設定狀態的複本或無狀態的執行個體指定服務的已發佈，讓它們位於不同的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-138">hello stateful replicas or stateless instances for a given service are distributed so they are in separate Fault Domains.</span></span> <span data-ttu-id="f4164-139">容錯網域之間分散 hello 服務可確保在 hello 階層的任何層級的容錯網域失敗時，不會洩露 hello hello 服務可用性。</span><span class="sxs-lookup"><span data-stu-id="f4164-139">Distributing hello service across fault domains ensures hello availability of hello service is not compromised when a Fault Domain fails at any level of hello hierarchy.</span></span>

<span data-ttu-id="f4164-140">Service Fabric 叢集資源管理員不在意 hello 容錯網域階層中有多少層級。</span><span class="sxs-lookup"><span data-stu-id="f4164-140">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in hello Fault Domain hierarchy.</span></span> <span data-ttu-id="f4164-141">不過，它會嘗試 hello 遺失 hello 階層中任何一個部分不會影響執行中服務的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="f4164-141">However, it tries tooensure that hello loss of any one portion of hello hierarchy doesn’t impact services running in it.</span></span> 

<span data-ttu-id="f4164-142">建議您最好有 hello 深度 hello 容錯網域階層中的每個層級的節點數目相同。</span><span class="sxs-lookup"><span data-stu-id="f4164-142">It is best if there are hello same number of nodes at each level of depth in hello Fault Domain hierarchy.</span></span> <span data-ttu-id="f4164-143">如果 hello 「 樹 」 的容錯網域是在叢集中不平衡，難 hello 叢集資源管理員 toofigure 出 hello 的服務的最佳配置。</span><span class="sxs-lookup"><span data-stu-id="f4164-143">If hello “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for hello Cluster Resource Manager toofigure out hello best allocation of services.</span></span> <span data-ttu-id="f4164-144">不平衡的容錯網域配置表示的某些網域 hello 損失影響 hello 可用性的服務，比其他網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-144">Imbalanced Fault Domains layouts mean that hello loss of some domains impact hello availability of services more than other domains.</span></span> <span data-ttu-id="f4164-145">如此一來，兩個目標之間損毀 hello 叢集資源管理員： 它想要將服務放在他們的 toouse 「 大量 」 網域中的 hello 機器和其想 tooplace 其他網域中的服務，讓網域中的 hello 遺失並不會造成問題。</span><span class="sxs-lookup"><span data-stu-id="f4164-145">As a result, hello Cluster Resource Manager is torn between two goals: It wants toouse hello machines in that “heavy” domain by placing services on them, and it wants tooplace services in other domains so that hello loss of a domain doesn’t cause problems.</span></span> 

<span data-ttu-id="f4164-146">不平衡網域外觀為何？</span><span class="sxs-lookup"><span data-stu-id="f4164-146">What do imbalanced domains look like?</span></span> <span data-ttu-id="f4164-147">Hello 在圖中，我們會示範兩個不同的叢集配置。</span><span class="sxs-lookup"><span data-stu-id="f4164-147">In hello diagram below, we show two different cluster layouts.</span></span> <span data-ttu-id="f4164-148">在 hello 第一個範例中，hello 節點平均分佈在 hello 容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-148">In hello first example, hello nodes are distributed evenly across hello Fault Domains.</span></span> <span data-ttu-id="f4164-149">Hello 第二個範例中，在一個 「 故障 」 網域會有許多節點 hello 超過其他容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-149">In hello second example, one Fault Domain has many more nodes than hello other Fault Domains.</span></span> 

<span data-ttu-id="f4164-150"><center>
![兩個不同的叢集配置][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-150"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="f4164-151">在 Azure 中，為您管理的容錯網域包含節點的 hello 選擇。</span><span class="sxs-lookup"><span data-stu-id="f4164-151">In Azure, hello choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="f4164-152">不過，根據 hello 您佈建的節點數目您可以仍然得到容錯網域與它們比其他的多個節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-152">However, depending on hello number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="f4164-153">例如，假設您有五個 hello 叢集中的容錯網域，但會以給定的 NodeType 佈建七個節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-153">For example, say you have five Fault Domains in hello cluster but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="f4164-154">在此情況下，hello 前兩個容錯網域得到更多的節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-154">In this case, hello first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="f4164-155">如果您只有幾個執行個體與多個 NodeTypes 繼續 toodeploy，hello 問題取得較差。</span><span class="sxs-lookup"><span data-stu-id="f4164-155">If you continue toodeploy more NodeTypes with only a couple instances, hello problem gets worse.</span></span> <span data-ttu-id="f4164-156">基於這個理由，建議您該 hello 中每個節點類型的節點數目是 hello 容錯網域數目的倍數。</span><span class="sxs-lookup"><span data-stu-id="f4164-156">For this reason it's recommended that hello number of nodes in each node type is a multiple of hello number of Fault Domains.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="f4164-157">升級網域</span><span class="sxs-lookup"><span data-stu-id="f4164-157">Upgrade domains</span></span>
<span data-ttu-id="f4164-158">升級網域是另一項功能，可協助 hello Service Fabric 叢集資源管理員了解 hello 叢集的 hello 版面配置。</span><span class="sxs-lookup"><span data-stu-id="f4164-158">Upgrade Domains are another feature that helps hello Service Fabric Cluster Resource Manager understand hello layout of hello cluster.</span></span> <span data-ttu-id="f4164-159">升級網域會定義在 hello 升級的節點集相同的時間。</span><span class="sxs-lookup"><span data-stu-id="f4164-159">Upgrade Domains define sets of nodes that are upgraded at hello same time.</span></span> <span data-ttu-id="f4164-160">升級的網域說明 hello 叢集資源管理員了解，以及協調管理作業，例如升級。</span><span class="sxs-lookup"><span data-stu-id="f4164-160">Upgrade Domains help hello Cluster Resource Manager understand and orchestrate management operations like upgrades.</span></span>

<span data-ttu-id="f4164-161">升級網域非常類似容錯網域，但是有幾個主要的差異。</span><span class="sxs-lookup"><span data-stu-id="f4164-161">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="f4164-162">首先，協調硬體失敗的區域會定義容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-162">First, areas of coordinated hardware failures define Fault Domains.</span></span> <span data-ttu-id="f4164-163">升級網域、 在 hello 相反，由原則所定義。</span><span class="sxs-lookup"><span data-stu-id="f4164-163">Upgrade Domains, on hello other hand, are defined by policy.</span></span> <span data-ttu-id="f4164-164">您取得 toodecide 多少想，而不是它聽寫 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="f4164-164">You get toodecide how many you want, rather than it being dictated by hello environment.</span></span> <span data-ttu-id="f4164-165">您可能會有與節點一樣多的升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-165">You could have as many Upgrade Domains as you do nodes.</span></span> <span data-ttu-id="f4164-166">容錯網域和升級網域的另一個差異在於升級網域不是階層式。</span><span class="sxs-lookup"><span data-stu-id="f4164-166">Another difference between Fault Domains and Upgrade Domains is that Upgrade Domains are not hierarchical.</span></span> <span data-ttu-id="f4164-167">相反地，它們更像是簡單的標記。</span><span class="sxs-lookup"><span data-stu-id="f4164-167">Instead, they are more like a simple tag.</span></span> 

<span data-ttu-id="f4164-168">hello 下列圖表顯示三個升級網域會等量分散於三個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-168">hello following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="f4164-169">其中也顯示不具狀態服務的三個不同複本有一個可能的位置，而每一個最後都在不同的容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-169">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="f4164-170">這個位置可讓 「 故障 」 網域中的服務升級的 hello 中間時的 hello 遺失，並且仍然擁有一份 hello 程式碼和資料。</span><span class="sxs-lookup"><span data-stu-id="f4164-170">This placement allows hello loss of a Fault Domain while in hello middle of a service upgrade and still have one copy of hello code and data.</span></span>  

<span data-ttu-id="f4164-171"><center>
容錯網域和升級網域的位置![][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-171"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="f4164-172">有優缺點 toohaving 大量的升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-172">There are pros and cons toohaving large numbers of Upgrade Domains.</span></span> <span data-ttu-id="f4164-173">多個升級網域代表 hello 升級的每個步驟是更精細，因此會影響較少的節點或服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-173">More Upgrade Domains means each step of hello upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="f4164-174">如此一來，較少的服務有 toomove 一次引入 hello 系統較少變換。</span><span class="sxs-lookup"><span data-stu-id="f4164-174">As a result, fewer services have toomove at a time, introducing less churn into hello system.</span></span> <span data-ttu-id="f4164-175">這通常會 tooimprove 可靠性，因為小於 hello 服務在 hello 升級過程中引用的任何問題所致。</span><span class="sxs-lookup"><span data-stu-id="f4164-175">This tends tooimprove reliability, since less of hello service is impacted by any issue introduced during hello upgrade.</span></span> <span data-ttu-id="f4164-176">多個升級網域也表示您需要較少的 hello 其他節點 toohandle hello 影響上的可用緩衝區升級。</span><span class="sxs-lookup"><span data-stu-id="f4164-176">More Upgrade Domains also means that you need less available buffer on other nodes toohandle hello impact of hello upgrade.</span></span> <span data-ttu-id="f4164-177">例如，如果您有五個升級網域，hello 節點中每個處理大約 20%的流量。</span><span class="sxs-lookup"><span data-stu-id="f4164-177">For example, if you have five Upgrade Domains, hello nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="f4164-178">如果您需要關閉該升級網域 tootake 升級時，該負載通常需要 toogo 某處。</span><span class="sxs-lookup"><span data-stu-id="f4164-178">If you need tootake down that Upgrade Domain for an upgrade, that load usually needs toogo somewhere.</span></span> <span data-ttu-id="f4164-179">因為您有四個剩餘的升級網域，每一個都必須有 hello 總流量的大約 5%的空間。</span><span class="sxs-lookup"><span data-stu-id="f4164-179">Since you have four remaining Upgrade Domains, each must have room for about 5% of hello total traffic.</span></span> <span data-ttu-id="f4164-180">多個升級網域會表示您需要較少的緩衝區 hello hello 叢集中節點上。</span><span class="sxs-lookup"><span data-stu-id="f4164-180">More Upgrade Domains means you need less buffer on hello nodes in hello cluster.</span></span> <span data-ttu-id="f4164-181">例如，請考慮如果您擁有 10 個升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-181">For example, consider if you had 10 Upgrade Domains instead.</span></span> <span data-ttu-id="f4164-182">在此情況下，每個 UD 會只處理 hello 總流量的大約 10%。</span><span class="sxs-lookup"><span data-stu-id="f4164-182">In that case, each UD would only be handling about 10% of hello total traffic.</span></span> <span data-ttu-id="f4164-183">當透過 hello 叢集升級步驟時，每個網域只需要 toohave hello 總流量的大約 1.1%的空間。</span><span class="sxs-lookup"><span data-stu-id="f4164-183">When an upgrade steps through hello cluster, each domain would only need toohave room for about 1.1% of hello total traffic.</span></span> <span data-ttu-id="f4164-184">多個升級網域通常可讓您 toorun 您在高使用率，因為您需要較低的保留容量的節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-184">More Upgrade Domains generally allow you toorun your nodes at higher utilization, since you need less reserved capacity.</span></span> <span data-ttu-id="f4164-185">hello 也適用於容錯網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-185">hello same is true for Fault Domains.</span></span>  

<span data-ttu-id="f4164-186">有許多的 「 升級 」 網域 hello 缺點是升級傾向 tootake 長。</span><span class="sxs-lookup"><span data-stu-id="f4164-186">hello downside of having many Upgrade Domains is that upgrades tend tootake longer.</span></span> <span data-ttu-id="f4164-187">Service Fabric 等候一段時間之後升級網域會完成，而且會執行啟動 tooupgrade hello 之前檢查下一個。</span><span class="sxs-lookup"><span data-stu-id="f4164-187">Service Fabric waits a short period of time after an Upgrade Domain is completed and performs checks before starting tooupgrade hello next one.</span></span> <span data-ttu-id="f4164-188">這些延遲啟用偵測 hello 升級所導入，才會繼續執行 hello 升級的問題。</span><span class="sxs-lookup"><span data-stu-id="f4164-188">These delays enable detecting issues introduced by hello upgrade before hello upgrade proceeds.</span></span> <span data-ttu-id="f4164-189">hello 代價是可接受的因為它會防止不正確的變更會影響到太多的 hello 服務一次。</span><span class="sxs-lookup"><span data-stu-id="f4164-189">hello tradeoff is acceptable because it prevents bad changes from affecting too much of hello service at a time.</span></span>

<span data-ttu-id="f4164-190">升級網域太少有許多負面的副作用 - 當個別升級網域關閉來升級時，整體容量會有一大部分無法使用。</span><span class="sxs-lookup"><span data-stu-id="f4164-190">Too few Upgrade Domains has many negative side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="f4164-191">例如，若您只有三個升級網域，則一次就關閉大約 1/3 的整體服務或叢集容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-191">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="f4164-192">因為您在叢集 toohandle hello 工作負載的 hello 其餘部分有 toohave 足夠的容量，一次向下有非常多的服務不需要這樣做。</span><span class="sxs-lookup"><span data-stu-id="f4164-192">Having so much of your service down at once isn’t desirable since you have toohave enough capacity in hello rest of your cluster toohandle hello workload.</span></span> <span data-ttu-id="f4164-193">維護該緩衝區表示這些節點在一般作業期間的負載比其他期間少。</span><span class="sxs-lookup"><span data-stu-id="f4164-193">Maintaining that buffer means that during normal operation those nodes are less loaded than they would be otherwise.</span></span> <span data-ttu-id="f4164-194">這會增加執行您的服務中的 hello 成本。</span><span class="sxs-lookup"><span data-stu-id="f4164-194">This increases hello cost of running your service.</span></span>

<span data-ttu-id="f4164-195">沒有任何實際限制 toohello 總數錯誤 」 或 「 升級 」 網域環境中，或條件約束上重疊的方式。</span><span class="sxs-lookup"><span data-stu-id="f4164-195">There’s no real limit toohello total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="f4164-196">話雖如此，有幾個常見模式：</span><span class="sxs-lookup"><span data-stu-id="f4164-196">That said, there are several common patterns:</span></span>

- <span data-ttu-id="f4164-197">1:1 對應的容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="f4164-197">Fault Domains and Upgrade Domains mapped 1:1</span></span>
- <span data-ttu-id="f4164-198">每個節點 (實體或虛擬作業系統執行個體) 一個升級網域</span><span class="sxs-lookup"><span data-stu-id="f4164-198">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
- <span data-ttu-id="f4164-199">其中 hello 容錯網域和升級網域形成矩陣與機器通常會執行下 hello 對角線"等量 」 或 「 矩陣 」 模型</span><span class="sxs-lookup"><span data-stu-id="f4164-199">A “striped” or “matrix” model where hello Fault Domains and Upgrade Domains form a matrix with machines usually running down hello diagonals</span></span>

<span data-ttu-id="f4164-200"><center>
![容錯網域和升級網域配置][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-200"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="f4164-201">有沒有最佳回答哪些配置 toochoose，各有一些優點和缺點。</span><span class="sxs-lookup"><span data-stu-id="f4164-201">There’s no best answer which layout toochoose, each has some pros and cons.</span></span> <span data-ttu-id="f4164-202">例如，hello 1FD:1UD 模型會是簡單 tooset 最多。</span><span class="sxs-lookup"><span data-stu-id="f4164-202">For example, hello 1FD:1UD model is simple tooset up.</span></span> <span data-ttu-id="f4164-203">hello 1 的升級網域，每個節點的模型是最接近哪些人只是要使用。</span><span class="sxs-lookup"><span data-stu-id="f4164-203">hello 1 Upgrade Domain per Node model is most like what people are used to.</span></span> <span data-ttu-id="f4164-204">在升級期間每個節點會獨立更新。</span><span class="sxs-lookup"><span data-stu-id="f4164-204">During upgrades each node is updated independently.</span></span> <span data-ttu-id="f4164-205">這是類似 toohow 少量的機器已在過去的 hello 手動升級。</span><span class="sxs-lookup"><span data-stu-id="f4164-205">This is similar toohow small sets of machines were upgraded manually in hello past.</span></span> 

<span data-ttu-id="f4164-206">hello FD/UD 矩陣，其中 hello Fd 和 Ud 形成資料表，而節點都放置啟動沿著 hello 對角線 hello 最常見的模型。</span><span class="sxs-lookup"><span data-stu-id="f4164-206">hello most common model is hello FD/UD matrix, where hello FDs and UDs form a table and nodes are placed starting along hello diagonal.</span></span> <span data-ttu-id="f4164-207">這是預設會在 Azure 中的 Service Fabric 叢集所使用的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="f4164-207">This is hello model used by default in Service Fabric clusters in Azure.</span></span> <span data-ttu-id="f4164-208">對具有許多節點的叢集的所有項目最後會看起來就像是上述的 hello 密集矩陣模式。</span><span class="sxs-lookup"><span data-stu-id="f4164-208">For clusters with many nodes everything ends up looking like hello dense matrix pattern above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="f4164-209">容錯網域和升級網域的條件約束和導致的行為</span><span class="sxs-lookup"><span data-stu-id="f4164-209">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="f4164-210">hello 叢集資源管理員會將 hello desire tookeep 服務平衡故障 」 和 「 升級 」 網域做為條件約束。</span><span class="sxs-lookup"><span data-stu-id="f4164-210">hello Cluster Resource Manager treats hello desire tookeep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="f4164-211">您可以在 [這篇文章](service-fabric-cluster-resource-manager-management-integration.md)中深入了解條件約束。</span><span class="sxs-lookup"><span data-stu-id="f4164-211">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="f4164-212">hello 容錯和升級網域的條件約束狀態: 「 指定的服務資料分割應該不會在發現差異*大於一*在 hello 的服務物件 （無狀態服務執行個體或可設定狀態的服務複本）兩個網域。 」</span><span class="sxs-lookup"><span data-stu-id="f4164-212">hello Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in hello number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span> <span data-ttu-id="f4164-213">這可防止違反這個條件約束的特定移動或排列方式。</span><span class="sxs-lookup"><span data-stu-id="f4164-213">This prevents certain moves or arrangements that violate this constraint.</span></span>

<span data-ttu-id="f4164-214">讓我們來看看一個範例。</span><span class="sxs-lookup"><span data-stu-id="f4164-214">Let's look at one example.</span></span> <span data-ttu-id="f4164-215">假設我們的叢集有六個節點，且已設定五個容錯網域和五個升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-215">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="f4164-216">FD0</span><span class="sxs-lookup"><span data-stu-id="f4164-216">FD0</span></span> | <span data-ttu-id="f4164-217">FD1</span><span class="sxs-lookup"><span data-stu-id="f4164-217">FD1</span></span> | <span data-ttu-id="f4164-218">FD2</span><span class="sxs-lookup"><span data-stu-id="f4164-218">FD2</span></span> | <span data-ttu-id="f4164-219">FD3</span><span class="sxs-lookup"><span data-stu-id="f4164-219">FD3</span></span> | <span data-ttu-id="f4164-220">FD4</span><span class="sxs-lookup"><span data-stu-id="f4164-220">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="f4164-221">**UD0**</span><span class="sxs-lookup"><span data-stu-id="f4164-221">**UD0**</span></span> |<span data-ttu-id="f4164-222">N1</span><span class="sxs-lookup"><span data-stu-id="f4164-222">N1</span></span> | | | | |
| <span data-ttu-id="f4164-223">**UD1**</span><span class="sxs-lookup"><span data-stu-id="f4164-223">**UD1**</span></span> |<span data-ttu-id="f4164-224">N6</span><span class="sxs-lookup"><span data-stu-id="f4164-224">N6</span></span> |<span data-ttu-id="f4164-225">N2</span><span class="sxs-lookup"><span data-stu-id="f4164-225">N2</span></span> | | | |
| <span data-ttu-id="f4164-226">**UD2**</span><span class="sxs-lookup"><span data-stu-id="f4164-226">**UD2**</span></span> | | |<span data-ttu-id="f4164-227">N3</span><span class="sxs-lookup"><span data-stu-id="f4164-227">N3</span></span> | | |
| <span data-ttu-id="f4164-228">**UD3**</span><span class="sxs-lookup"><span data-stu-id="f4164-228">**UD3**</span></span> | | | |<span data-ttu-id="f4164-229">N4</span><span class="sxs-lookup"><span data-stu-id="f4164-229">N4</span></span> | |
| <span data-ttu-id="f4164-230">**UD4**</span><span class="sxs-lookup"><span data-stu-id="f4164-230">**UD4**</span></span> | | | | |<span data-ttu-id="f4164-231">N5</span><span class="sxs-lookup"><span data-stu-id="f4164-231">N5</span></span> |

<span data-ttu-id="f4164-232">現在假設我們建立 TargetReplicaSetSize (或者對於無狀態服務是 InstanceCount) 為五的服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-232">Now let's say that we create a service with a TargetReplicaSetSize (or, for a stateless service an InstanceCount) of five.</span></span> <span data-ttu-id="f4164-233">N1 N5 進入 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="f4164-233">hello replicas land on N1-N5.</span></span> <span data-ttu-id="f4164-234">事實上，不論建立多少像這樣的服務，都不會用到 N6。</span><span class="sxs-lookup"><span data-stu-id="f4164-234">In fact, N6 is never used no matter how many services like this you create.</span></span> <span data-ttu-id="f4164-235">原因為何？</span><span class="sxs-lookup"><span data-stu-id="f4164-235">But why?</span></span> <span data-ttu-id="f4164-236">讓我們看看 hello 目前的配置和選擇 N6，則會發生什麼事的 hello 差異。</span><span class="sxs-lookup"><span data-stu-id="f4164-236">Let's look at hello difference between hello current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="f4164-237">以下是我們了及 hello 複本，每個容錯和升級網域總數的 hello 版面配置：</span><span class="sxs-lookup"><span data-stu-id="f4164-237">Here's hello layout we got and hello total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="f4164-238">FD0</span><span class="sxs-lookup"><span data-stu-id="f4164-238">FD0</span></span> | <span data-ttu-id="f4164-239">FD1</span><span class="sxs-lookup"><span data-stu-id="f4164-239">FD1</span></span> | <span data-ttu-id="f4164-240">FD2</span><span class="sxs-lookup"><span data-stu-id="f4164-240">FD2</span></span> | <span data-ttu-id="f4164-241">FD3</span><span class="sxs-lookup"><span data-stu-id="f4164-241">FD3</span></span> | <span data-ttu-id="f4164-242">FD4</span><span class="sxs-lookup"><span data-stu-id="f4164-242">FD4</span></span> | <span data-ttu-id="f4164-243">UDTotal</span><span class="sxs-lookup"><span data-stu-id="f4164-243">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="f4164-244">**UD0**</span><span class="sxs-lookup"><span data-stu-id="f4164-244">**UD0**</span></span> |<span data-ttu-id="f4164-245">R1</span><span class="sxs-lookup"><span data-stu-id="f4164-245">R1</span></span> | | | | |<span data-ttu-id="f4164-246">1</span><span class="sxs-lookup"><span data-stu-id="f4164-246">1</span></span> |
| <span data-ttu-id="f4164-247">**UD1**</span><span class="sxs-lookup"><span data-stu-id="f4164-247">**UD1**</span></span> | |<span data-ttu-id="f4164-248">R2</span><span class="sxs-lookup"><span data-stu-id="f4164-248">R2</span></span> | | | |<span data-ttu-id="f4164-249">1</span><span class="sxs-lookup"><span data-stu-id="f4164-249">1</span></span> |
| <span data-ttu-id="f4164-250">**UD2**</span><span class="sxs-lookup"><span data-stu-id="f4164-250">**UD2**</span></span> | | |<span data-ttu-id="f4164-251">R3</span><span class="sxs-lookup"><span data-stu-id="f4164-251">R3</span></span> | | |<span data-ttu-id="f4164-252">1</span><span class="sxs-lookup"><span data-stu-id="f4164-252">1</span></span> |
| <span data-ttu-id="f4164-253">**UD3**</span><span class="sxs-lookup"><span data-stu-id="f4164-253">**UD3**</span></span> | | | |<span data-ttu-id="f4164-254">R4</span><span class="sxs-lookup"><span data-stu-id="f4164-254">R4</span></span> | |<span data-ttu-id="f4164-255">1</span><span class="sxs-lookup"><span data-stu-id="f4164-255">1</span></span> |
| <span data-ttu-id="f4164-256">**UD4**</span><span class="sxs-lookup"><span data-stu-id="f4164-256">**UD4**</span></span> | | | | |<span data-ttu-id="f4164-257">R5</span><span class="sxs-lookup"><span data-stu-id="f4164-257">R5</span></span> |<span data-ttu-id="f4164-258">1</span><span class="sxs-lookup"><span data-stu-id="f4164-258">1</span></span> |
| <span data-ttu-id="f4164-259">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="f4164-259">**FDTotal**</span></span> |<span data-ttu-id="f4164-260">1</span><span class="sxs-lookup"><span data-stu-id="f4164-260">1</span></span> |<span data-ttu-id="f4164-261">1</span><span class="sxs-lookup"><span data-stu-id="f4164-261">1</span></span> |<span data-ttu-id="f4164-262">1</span><span class="sxs-lookup"><span data-stu-id="f4164-262">1</span></span> |<span data-ttu-id="f4164-263">1</span><span class="sxs-lookup"><span data-stu-id="f4164-263">1</span></span> |<span data-ttu-id="f4164-264">1</span><span class="sxs-lookup"><span data-stu-id="f4164-264">1</span></span> |- |

<span data-ttu-id="f4164-265">就每個容錯網域和升級網域的節點數而論，在此配置達到平衡。</span><span class="sxs-lookup"><span data-stu-id="f4164-265">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="f4164-266">它也是由平衡 hello 數的每個容錯和升級網域的複本。</span><span class="sxs-lookup"><span data-stu-id="f4164-266">It is also balanced in terms of hello number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="f4164-267">每個網域有節點數目相同的 hello 和 hello 相同數目的複本。</span><span class="sxs-lookup"><span data-stu-id="f4164-267">Each domain has hello same number of nodes and hello same number of replicas.</span></span>

<span data-ttu-id="f4164-268">現在，讓我們看看改用 N6 而不使用 N2 的情況。</span><span class="sxs-lookup"><span data-stu-id="f4164-268">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="f4164-269">會 hello 複本要如何散發然後？</span><span class="sxs-lookup"><span data-stu-id="f4164-269">How would hello replicas be distributed then?</span></span>

|  | <span data-ttu-id="f4164-270">FD0</span><span class="sxs-lookup"><span data-stu-id="f4164-270">FD0</span></span> | <span data-ttu-id="f4164-271">FD1</span><span class="sxs-lookup"><span data-stu-id="f4164-271">FD1</span></span> | <span data-ttu-id="f4164-272">FD2</span><span class="sxs-lookup"><span data-stu-id="f4164-272">FD2</span></span> | <span data-ttu-id="f4164-273">FD3</span><span class="sxs-lookup"><span data-stu-id="f4164-273">FD3</span></span> | <span data-ttu-id="f4164-274">FD4</span><span class="sxs-lookup"><span data-stu-id="f4164-274">FD4</span></span> | <span data-ttu-id="f4164-275">UDTotal</span><span class="sxs-lookup"><span data-stu-id="f4164-275">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="f4164-276">**UD0**</span><span class="sxs-lookup"><span data-stu-id="f4164-276">**UD0**</span></span> |<span data-ttu-id="f4164-277">R1</span><span class="sxs-lookup"><span data-stu-id="f4164-277">R1</span></span> | | | | |<span data-ttu-id="f4164-278">1</span><span class="sxs-lookup"><span data-stu-id="f4164-278">1</span></span> |
| <span data-ttu-id="f4164-279">**UD1**</span><span class="sxs-lookup"><span data-stu-id="f4164-279">**UD1**</span></span> |<span data-ttu-id="f4164-280">R5</span><span class="sxs-lookup"><span data-stu-id="f4164-280">R5</span></span> | | | | |<span data-ttu-id="f4164-281">1</span><span class="sxs-lookup"><span data-stu-id="f4164-281">1</span></span> |
| <span data-ttu-id="f4164-282">**UD2**</span><span class="sxs-lookup"><span data-stu-id="f4164-282">**UD2**</span></span> | | |<span data-ttu-id="f4164-283">R2</span><span class="sxs-lookup"><span data-stu-id="f4164-283">R2</span></span> | | |<span data-ttu-id="f4164-284">1</span><span class="sxs-lookup"><span data-stu-id="f4164-284">1</span></span> |
| <span data-ttu-id="f4164-285">**UD3**</span><span class="sxs-lookup"><span data-stu-id="f4164-285">**UD3**</span></span> | | | |<span data-ttu-id="f4164-286">R3</span><span class="sxs-lookup"><span data-stu-id="f4164-286">R3</span></span> | |<span data-ttu-id="f4164-287">1</span><span class="sxs-lookup"><span data-stu-id="f4164-287">1</span></span> |
| <span data-ttu-id="f4164-288">**UD4**</span><span class="sxs-lookup"><span data-stu-id="f4164-288">**UD4**</span></span> | | | | |<span data-ttu-id="f4164-289">R4</span><span class="sxs-lookup"><span data-stu-id="f4164-289">R4</span></span> |<span data-ttu-id="f4164-290">1</span><span class="sxs-lookup"><span data-stu-id="f4164-290">1</span></span> |
| <span data-ttu-id="f4164-291">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="f4164-291">**FDTotal**</span></span> |<span data-ttu-id="f4164-292">2</span><span class="sxs-lookup"><span data-stu-id="f4164-292">2</span></span> |<span data-ttu-id="f4164-293">0</span><span class="sxs-lookup"><span data-stu-id="f4164-293">0</span></span> |<span data-ttu-id="f4164-294">1</span><span class="sxs-lookup"><span data-stu-id="f4164-294">1</span></span> |<span data-ttu-id="f4164-295">1</span><span class="sxs-lookup"><span data-stu-id="f4164-295">1</span></span> |<span data-ttu-id="f4164-296">1</span><span class="sxs-lookup"><span data-stu-id="f4164-296">1</span></span> |- |

<span data-ttu-id="f4164-297">此配置命名為違反我們 hello 容錯網域條件約束的定義。</span><span class="sxs-lookup"><span data-stu-id="f4164-297">This layout violates our definition for hello Fault Domain constraint.</span></span> <span data-ttu-id="f4164-298">FD0 具有兩個複本，而 FD1 零，讓 hello FD0 和差異 FD1 總共有兩個。</span><span class="sxs-lookup"><span data-stu-id="f4164-298">FD0 has two replicas, while FD1 has zero, making hello difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="f4164-299">hello 叢集資源管理員不允許這種排列方式。</span><span class="sxs-lookup"><span data-stu-id="f4164-299">hello Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="f4164-300">同樣地，如果挑選 N2 和 N6 (而不是 N1 和 N2)，則會得到：</span><span class="sxs-lookup"><span data-stu-id="f4164-300">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="f4164-301">FD0</span><span class="sxs-lookup"><span data-stu-id="f4164-301">FD0</span></span> | <span data-ttu-id="f4164-302">FD1</span><span class="sxs-lookup"><span data-stu-id="f4164-302">FD1</span></span> | <span data-ttu-id="f4164-303">FD2</span><span class="sxs-lookup"><span data-stu-id="f4164-303">FD2</span></span> | <span data-ttu-id="f4164-304">FD3</span><span class="sxs-lookup"><span data-stu-id="f4164-304">FD3</span></span> | <span data-ttu-id="f4164-305">FD4</span><span class="sxs-lookup"><span data-stu-id="f4164-305">FD4</span></span> | <span data-ttu-id="f4164-306">UDTotal</span><span class="sxs-lookup"><span data-stu-id="f4164-306">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="f4164-307">**UD0**</span><span class="sxs-lookup"><span data-stu-id="f4164-307">**UD0**</span></span> | | | | | |<span data-ttu-id="f4164-308">0</span><span class="sxs-lookup"><span data-stu-id="f4164-308">0</span></span> |
| <span data-ttu-id="f4164-309">**UD1**</span><span class="sxs-lookup"><span data-stu-id="f4164-309">**UD1**</span></span> |<span data-ttu-id="f4164-310">R5</span><span class="sxs-lookup"><span data-stu-id="f4164-310">R5</span></span> |<span data-ttu-id="f4164-311">R1</span><span class="sxs-lookup"><span data-stu-id="f4164-311">R1</span></span> | | | |<span data-ttu-id="f4164-312">2</span><span class="sxs-lookup"><span data-stu-id="f4164-312">2</span></span> |
| <span data-ttu-id="f4164-313">**UD2**</span><span class="sxs-lookup"><span data-stu-id="f4164-313">**UD2**</span></span> | | |<span data-ttu-id="f4164-314">R2</span><span class="sxs-lookup"><span data-stu-id="f4164-314">R2</span></span> | | |<span data-ttu-id="f4164-315">1</span><span class="sxs-lookup"><span data-stu-id="f4164-315">1</span></span> |
| <span data-ttu-id="f4164-316">**UD3**</span><span class="sxs-lookup"><span data-stu-id="f4164-316">**UD3**</span></span> | | | |<span data-ttu-id="f4164-317">R3</span><span class="sxs-lookup"><span data-stu-id="f4164-317">R3</span></span> | |<span data-ttu-id="f4164-318">1</span><span class="sxs-lookup"><span data-stu-id="f4164-318">1</span></span> |
| <span data-ttu-id="f4164-319">**UD4**</span><span class="sxs-lookup"><span data-stu-id="f4164-319">**UD4**</span></span> | | | | |<span data-ttu-id="f4164-320">R4</span><span class="sxs-lookup"><span data-stu-id="f4164-320">R4</span></span> |<span data-ttu-id="f4164-321">1</span><span class="sxs-lookup"><span data-stu-id="f4164-321">1</span></span> |
| <span data-ttu-id="f4164-322">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="f4164-322">**FDTotal**</span></span> |<span data-ttu-id="f4164-323">1</span><span class="sxs-lookup"><span data-stu-id="f4164-323">1</span></span> |<span data-ttu-id="f4164-324">1</span><span class="sxs-lookup"><span data-stu-id="f4164-324">1</span></span> |<span data-ttu-id="f4164-325">1</span><span class="sxs-lookup"><span data-stu-id="f4164-325">1</span></span> |<span data-ttu-id="f4164-326">1</span><span class="sxs-lookup"><span data-stu-id="f4164-326">1</span></span> |<span data-ttu-id="f4164-327">1</span><span class="sxs-lookup"><span data-stu-id="f4164-327">1</span></span> |- |

<span data-ttu-id="f4164-328">此配置就容錯網域而言是平衡的。</span><span class="sxs-lookup"><span data-stu-id="f4164-328">This layout is balanced in terms of Fault Domains.</span></span> <span data-ttu-id="f4164-329">不過，現在它會違反 hello 升級網域條件約束。</span><span class="sxs-lookup"><span data-stu-id="f4164-329">However, now it's violating hello Upgrade Domain constraint.</span></span> <span data-ttu-id="f4164-330">這是因為 UD0 有零個複本，而 UD1 有兩個複本。</span><span class="sxs-lookup"><span data-stu-id="f4164-330">This is because UD0 has zero replicas while UD1 has two.</span></span> <span data-ttu-id="f4164-331">因此，此配置命名為也不正確，而且不會挑選 hello 叢集資源管理員所。</span><span class="sxs-lookup"><span data-stu-id="f4164-331">Therefore, this layout is also invalid and won't be picked by hello Cluster Resource Manager.</span></span> 

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="f4164-332">設定容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="f4164-332">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="f4164-333">Azure 託管的 Service Fabric 部署中會自動定義容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="f4164-333">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="f4164-334">Service Fabric 拾取，並使用從 Azure 的 hello 環境資訊。</span><span class="sxs-lookup"><span data-stu-id="f4164-334">Service Fabric picks up and uses hello environment information from Azure.</span></span>

<span data-ttu-id="f4164-335">如果您正在建立您自己的叢集 （或想 toorun 特定拓撲中開發），您可以自行提供 hello 容錯網域和升級網域的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4164-335">If you’re creating your own cluster (or want toorun a particular topology in development), you can provide hello Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="f4164-336">在此範例中，我們定義本機開發叢集，具有九個節點，且跨越三個「資料中心」(各有三個機架)。</span><span class="sxs-lookup"><span data-stu-id="f4164-336">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="f4164-337">此叢集也有三個升級網域等量分散於這些三個資料中心。</span><span class="sxs-lookup"><span data-stu-id="f4164-337">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="f4164-338">Hello 組態的範例如下：</span><span class="sxs-lookup"><span data-stu-id="f4164-338">An example of hello configuration is below:</span></span> 

<span data-ttu-id="f4164-339">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f4164-339">ClusterManifest.xml</span></span>

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

<span data-ttu-id="f4164-340">獨立部署透過 ClusterConfig.json</span><span class="sxs-lookup"><span data-stu-id="f4164-340">via ClusterConfig.json for Standalone deployments</span></span>

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> <span data-ttu-id="f4164-341">透過 Azure Resource Manager 定義叢集時，容錯網域和升級網域會由 Azure 指派。</span><span class="sxs-lookup"><span data-stu-id="f4164-341">When defining clusters via Azure Resource Manager, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="f4164-342">因此，Azure Resource Manager 範本中的 hello 定義的節點型別和虛擬機器規模集不包含容錯網域 」 或 「 升級 」 網域資訊。</span><span class="sxs-lookup"><span data-stu-id="f4164-342">Therefore, hello definition of your Node Types and Virtual Machine Scale Sets in your Azure Resource Manager template does not include Fault Domain or Upgrade Domain information.</span></span>
>

## <a name="node-properties-and-placement-constraints"></a><span data-ttu-id="f4164-343">節點屬性和放置條件約束</span><span class="sxs-lookup"><span data-stu-id="f4164-343">Node properties and placement constraints</span></span>
<span data-ttu-id="f4164-344">您有時 （事實上，大部分的 hello 時間） 將只在特定類型的 hello 叢集中的節點執行某些工作負載的 toowant tooensure。</span><span class="sxs-lookup"><span data-stu-id="f4164-344">Sometimes (in fact, most of hello time) you’re going toowant tooensure that certain workloads run only on certain types of nodes in hello cluster.</span></span> <span data-ttu-id="f4164-345">例如，某些工作負載可能需要 GPU 或 SSD，而有些則不用。</span><span class="sxs-lookup"><span data-stu-id="f4164-345">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="f4164-346">目標硬體 tooparticular 工作負載的絕佳範例是有幾乎每個多層式架構。</span><span class="sxs-lookup"><span data-stu-id="f4164-346">A great example of targeting hardware tooparticular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="f4164-347">特定電腦做為 hello 前端或 API 伺服端 hello 應用程式和公開的 toohello 用戶端或 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f4164-347">Certain machines serve as hello front end or API serving side of hello application and are exposed toohello clients or hello internet.</span></span> <span data-ttu-id="f4164-348">不同的電腦，通常會使用不同的硬體資源，且處理 hello 運算或儲存層的 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="f4164-348">Different machines, often with different hardware resources, handle hello work of hello compute or storage layers.</span></span> <span data-ttu-id="f4164-349">這些通常是_不_直接公開 tooclients 或 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="f4164-349">These are usually _not_ directly exposed tooclients or hello internet.</span></span> <span data-ttu-id="f4164-350">Service Fabric 需要有特定的工作負載需要特定硬體組態上的 toorun 情況。</span><span class="sxs-lookup"><span data-stu-id="f4164-350">Service Fabric expects that there are cases where particular workloads need toorun on particular hardware configurations.</span></span> <span data-ttu-id="f4164-351">例如：</span><span class="sxs-lookup"><span data-stu-id="f4164-351">For example:</span></span>

* <span data-ttu-id="f4164-352">現有的多層式架構應用程式已「提升並移轉」到 Service Fabric 環境</span><span class="sxs-lookup"><span data-stu-id="f4164-352">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="f4164-353">工作負載需要 toorun 於特定硬體的效能、 小數位數或隔離的理由</span><span class="sxs-lookup"><span data-stu-id="f4164-353">a workload wants toorun on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="f4164-354">基於原則或資源耗用量的理由，工作負載應該彼此隔離</span><span class="sxs-lookup"><span data-stu-id="f4164-354">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="f4164-355">toosupport 組態，這類服務網狀架構有可以套用的 toonodes 標記的第一個類別的概念。</span><span class="sxs-lookup"><span data-stu-id="f4164-355">toosupport these sorts of configurations, Service Fabric has a first class notion of tags that can be applied toonodes.</span></span> <span data-ttu-id="f4164-356">這些標記稱為**節點屬性**。</span><span class="sxs-lookup"><span data-stu-id="f4164-356">These tags are called **node properties**.</span></span> <span data-ttu-id="f4164-357">**位置條件約束**是 hello 陳述式附加 tooindividual 服務選取一或多個節點的屬性。</span><span class="sxs-lookup"><span data-stu-id="f4164-357">**Placement constraints** are hello statements attached tooindividual services that select for one or more node properties.</span></span> <span data-ttu-id="f4164-358">放置條件約束會定義應該執行服務的位置。</span><span class="sxs-lookup"><span data-stu-id="f4164-358">Placement constraints define where services should run.</span></span> <span data-ttu-id="f4164-359">hello 一組條件約束可延伸-任何索引鍵/值組可以運作。</span><span class="sxs-lookup"><span data-stu-id="f4164-359">hello set of constraints is extensible - any key/value pair can work.</span></span> 

<span data-ttu-id="f4164-360"><center>
![叢集配置不同工作負載][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-360"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

### <a name="built-in-node-properties"></a><span data-ttu-id="f4164-361">內建節點屬性</span><span class="sxs-lookup"><span data-stu-id="f4164-361">Built in node properties</span></span>
<span data-ttu-id="f4164-362">服務網狀架構定義可以自動使用不含 hello 使用者具有 toodefine 某些預設節點屬性它們。</span><span class="sxs-lookup"><span data-stu-id="f4164-362">Service Fabric defines some default node properties that can be used automatically without hello user having toodefine them.</span></span> <span data-ttu-id="f4164-363">hello 預設屬性，定義每個節點是 hello **NodeType**和 hello **NodeName**。</span><span class="sxs-lookup"><span data-stu-id="f4164-363">hello default properties defined at each node are hello **NodeType** and hello **NodeName**.</span></span> <span data-ttu-id="f4164-364">例如，您可以將放置條件約束撰寫成 `"(NodeType == NodeType03)"`。</span><span class="sxs-lookup"><span data-stu-id="f4164-364">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="f4164-365">通常我們找到了 NodeType toobe hello 最常使用的屬性之一。</span><span class="sxs-lookup"><span data-stu-id="f4164-365">Generally we have found NodeType toobe one of hello most commonly used properties.</span></span> <span data-ttu-id="f4164-366">因為它與機器類型的對應是 1:1，所以很有用。</span><span class="sxs-lookup"><span data-stu-id="f4164-366">It is useful since it corresponds 1:1 with a type of a machine.</span></span> <span data-ttu-id="f4164-367">機器的每個型別對應 tooa 傳統的多層式架構應用程式中的工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="f4164-367">Each type of machine corresponds tooa type of workload in a traditional n-tier application.</span></span>

<span data-ttu-id="f4164-368"><center>
![放置條件約束和節點屬性][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-368"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

## <a name="placement-constraint-and-node-property-syntax"></a><span data-ttu-id="f4164-369">放置條件約束和節點屬性語法</span><span class="sxs-lookup"><span data-stu-id="f4164-369">Placement Constraint and Node Property Syntax</span></span> 
<span data-ttu-id="f4164-370">hello hello 節點屬性中指定的值可以是字串，bool，或帶正負號長時間。</span><span class="sxs-lookup"><span data-stu-id="f4164-370">hello value specified in hello node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="f4164-371">在 hello 服務的 hello 陳述式會呼叫放置*條件約束*因為它會限制 hello 服務可讓 hello 叢集中執行。</span><span class="sxs-lookup"><span data-stu-id="f4164-371">hello statement at hello service is called a placement *constraint* since it constrains where hello service can run in hello cluster.</span></span> <span data-ttu-id="f4164-372">hello 條件約束可以是任何 hello hello 叢集中的另一個節點屬性運作的布林陳述式。</span><span class="sxs-lookup"><span data-stu-id="f4164-372">hello constraint can be any Boolean statement that operates on hello different node properties in hello cluster.</span></span> <span data-ttu-id="f4164-373">這些布林值的陳述式中的 hello 有效選取器為：</span><span class="sxs-lookup"><span data-stu-id="f4164-373">hello valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="f4164-374">建立特定陳述式的條件式檢查</span><span class="sxs-lookup"><span data-stu-id="f4164-374">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="f4164-375">陳述式</span><span class="sxs-lookup"><span data-stu-id="f4164-375">Statement</span></span> | <span data-ttu-id="f4164-376">語法</span><span class="sxs-lookup"><span data-stu-id="f4164-376">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="f4164-377">「等於」</span><span class="sxs-lookup"><span data-stu-id="f4164-377">"equal to"</span></span> | <span data-ttu-id="f4164-378">"=="</span><span class="sxs-lookup"><span data-stu-id="f4164-378">"=="</span></span> |
| <span data-ttu-id="f4164-379">「不等於」</span><span class="sxs-lookup"><span data-stu-id="f4164-379">"not equal to"</span></span> | <span data-ttu-id="f4164-380">"!="</span><span class="sxs-lookup"><span data-stu-id="f4164-380">"!="</span></span> |
| <span data-ttu-id="f4164-381">「大於」</span><span class="sxs-lookup"><span data-stu-id="f4164-381">"greater than"</span></span> | <span data-ttu-id="f4164-382">">"</span><span class="sxs-lookup"><span data-stu-id="f4164-382">">"</span></span> |
| <span data-ttu-id="f4164-383">「大於或等於」</span><span class="sxs-lookup"><span data-stu-id="f4164-383">"greater than or equal to"</span></span> | <span data-ttu-id="f4164-384">">="</span><span class="sxs-lookup"><span data-stu-id="f4164-384">">="</span></span> |
| <span data-ttu-id="f4164-385">「小於」</span><span class="sxs-lookup"><span data-stu-id="f4164-385">"less than"</span></span> | <span data-ttu-id="f4164-386">"<"</span><span class="sxs-lookup"><span data-stu-id="f4164-386">"<"</span></span> |
| <span data-ttu-id="f4164-387">「小於或等於」</span><span class="sxs-lookup"><span data-stu-id="f4164-387">"less than or equal to"</span></span> | <span data-ttu-id="f4164-388">"<="</span><span class="sxs-lookup"><span data-stu-id="f4164-388">"<="</span></span> |

2) <span data-ttu-id="f4164-389">分組和邏輯運算的布林值陳述式</span><span class="sxs-lookup"><span data-stu-id="f4164-389">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="f4164-390">陳述式</span><span class="sxs-lookup"><span data-stu-id="f4164-390">Statement</span></span> | <span data-ttu-id="f4164-391">語法</span><span class="sxs-lookup"><span data-stu-id="f4164-391">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="f4164-392">「和」</span><span class="sxs-lookup"><span data-stu-id="f4164-392">"and"</span></span> | <span data-ttu-id="f4164-393">"&&"</span><span class="sxs-lookup"><span data-stu-id="f4164-393">"&&"</span></span> |
| <span data-ttu-id="f4164-394">「或」</span><span class="sxs-lookup"><span data-stu-id="f4164-394">"or"</span></span> | <span data-ttu-id="f4164-395">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="f4164-395">"&#124;&#124;"</span></span> |
| <span data-ttu-id="f4164-396">「否」</span><span class="sxs-lookup"><span data-stu-id="f4164-396">"not"</span></span> | <span data-ttu-id="f4164-397">"!"</span><span class="sxs-lookup"><span data-stu-id="f4164-397">"!"</span></span> |
| <span data-ttu-id="f4164-398">「組成單一陳述式」</span><span class="sxs-lookup"><span data-stu-id="f4164-398">"group as single statement"</span></span> | <span data-ttu-id="f4164-399">"()"</span><span class="sxs-lookup"><span data-stu-id="f4164-399">"()"</span></span> |

<span data-ttu-id="f4164-400">以下是基本條件約束陳述式的一些範例。</span><span class="sxs-lookup"><span data-stu-id="f4164-400">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="f4164-401">只有其中 hello 整體放置 constraint 陳述式會評估太"，則為 True 」 的節點可以有 hello 置於其上的服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-401">Only nodes where hello overall placement constraint statement evaluates too“True” can have hello service placed on it.</span></span> <span data-ttu-id="f4164-402">未定義屬性的節點不符合包含該屬性的任何放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="f4164-402">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="f4164-403">假設該屬性定義指定的節點類型的節點的後的 hello:</span><span class="sxs-lookup"><span data-stu-id="f4164-403">Let’s say that hello following node properties were defined for a given node type:</span></span>

<span data-ttu-id="f4164-404">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f4164-404">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="f4164-405">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。</span><span class="sxs-lookup"><span data-stu-id="f4164-405">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

> [!NOTE]
> <span data-ttu-id="f4164-406">在您的 Azure Resource Manager 範本 hello 節點型別通常已參數化。</span><span class="sxs-lookup"><span data-stu-id="f4164-406">In your Azure Resource Manager template hello node type is usually parameterized.</span></span> <span data-ttu-id="f4164-407">它看起來會是 "[parameters('vmNodeType1Name')]"，而不是 "NodeType01"。</span><span class="sxs-lookup"><span data-stu-id="f4164-407">It would look like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

<span data-ttu-id="f4164-408">您可以針對服務建立服務放置「條件約束」，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f4164-408">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="f4164-409">C#</span><span class="sxs-lookup"><span data-stu-id="f4164-409">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="f4164-410">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f4164-410">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="f4164-411">如果 NodeType01 的所有節點都是有效的您也可以選取該節點型別中的 hello 條件約束"(NodeType == NodeType01)"。</span><span class="sxs-lookup"><span data-stu-id="f4164-411">If all nodes of NodeType01 are valid, you can also select that node type with hello constraint "(NodeType == NodeType01)".</span></span>

<span data-ttu-id="f4164-412">其中一個 hello 酷事情，關於服務的位置限制式是可以進行更新以動態方式在執行階段。</span><span class="sxs-lookup"><span data-stu-id="f4164-412">One of hello cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="f4164-413">因此如果需要您可以在 hello 叢集移動服務、 加入和移除需求等。Service Fabric 會負責確保，hello 服務停留和可用即使當這類的變更進行。</span><span class="sxs-lookup"><span data-stu-id="f4164-413">So if you need to, you can move a service around in hello cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that hello service stays up and available even when these types of changes are made.</span></span>

<span data-ttu-id="f4164-414">C#：</span><span class="sxs-lookup"><span data-stu-id="f4164-414">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="f4164-415">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f4164-415">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="f4164-416">放置條件約束會針對每個不同的具名服務執行個體指定。</span><span class="sxs-lookup"><span data-stu-id="f4164-416">Placement constraints are specified for every different named service instance.</span></span> <span data-ttu-id="f4164-417">更新一定要進行 hello 取代 （覆寫） 先前指定什麼。</span><span class="sxs-lookup"><span data-stu-id="f4164-417">Updates always take hello place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="f4164-418">hello 叢集定義定義 hello 屬性節點上。</span><span class="sxs-lookup"><span data-stu-id="f4164-418">hello cluster definition defines hello properties on a node.</span></span> <span data-ttu-id="f4164-419">變更節點的屬性需要叢集設定升級。</span><span class="sxs-lookup"><span data-stu-id="f4164-419">Changing a node's properties requires a cluster configuration upgrade.</span></span> <span data-ttu-id="f4164-420">升級的節點屬性需要每個受影響的節點 toorestart tooreport 其新的屬性。</span><span class="sxs-lookup"><span data-stu-id="f4164-420">Upgrading a node's properties requires each affected node toorestart tooreport its new properties.</span></span> <span data-ttu-id="f4164-421">這些輪流升級是由 Service Fabric 管理。</span><span class="sxs-lookup"><span data-stu-id="f4164-421">These rolling upgrades are managed by Service Fabric.</span></span>

## <a name="describing-and-managing-cluster-resources"></a><span data-ttu-id="f4164-422">描述與管理叢集資源</span><span class="sxs-lookup"><span data-stu-id="f4164-422">Describing and Managing Cluster Resources</span></span>
<span data-ttu-id="f4164-423">其中一個最重要的任何 orchestrator 工作是 toohelp hello 管理 hello 叢集中的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="f4164-423">One of hello most important jobs of any orchestrator is toohelp manage resource consumption in hello cluster.</span></span> <span data-ttu-id="f4164-424">管理叢集資源可以表示幾個不同的項目。</span><span class="sxs-lookup"><span data-stu-id="f4164-424">Managing cluster resources can mean a couple of different things.</span></span> <span data-ttu-id="f4164-425">首先，確保電腦不會多載。</span><span class="sxs-lookup"><span data-stu-id="f4164-425">First, there's ensuring that machines are not overloaded.</span></span> <span data-ttu-id="f4164-426">這表示確定電腦不會執行比它們能夠處理還多的服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-426">This means making sure that machines aren't running more services than they can handle.</span></span> <span data-ttu-id="f4164-427">第二，也無需平衡即重大 toorunning 服務有效率地最佳化。</span><span class="sxs-lookup"><span data-stu-id="f4164-427">Second, there's balancing and optimization which is critical toorunning services efficiently.</span></span> <span data-ttu-id="f4164-428">符合成本的效益或效能的敏感服務供應項目不允許某些節點 toobe 熱有些則是陌生。</span><span class="sxs-lookup"><span data-stu-id="f4164-428">Cost effective or performance sensitive service offerings can't allow some nodes toobe hot while others are cold.</span></span> <span data-ttu-id="f4164-429">Tooresource 競爭與效能不佳，和冷節點代表浪費資源並增加的成本，會導致最忙碌的節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-429">Hot nodes lead tooresource contention and poor performance, and cold nodes represent wasted resources and increased costs.</span></span> 

<span data-ttu-id="f4164-430">Service Fabric 以 `Metrics` 表示資源。</span><span class="sxs-lookup"><span data-stu-id="f4164-430">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="f4164-431">度量資訊是您想 toodescribe tooService 網狀架構的任何邏輯或實體資源。</span><span class="sxs-lookup"><span data-stu-id="f4164-431">Metrics are any logical or physical resource that you want toodescribe tooService Fabric.</span></span> <span data-ttu-id="f4164-432">度量的範例是例如「WorkQueueDepth」或「MemoryInMb」的項目。</span><span class="sxs-lookup"><span data-stu-id="f4164-432">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="f4164-433">在節點上 hello Service Fabric 可以管理的實體資源的相關資訊，請參閱[資源控管](service-fabric-resource-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="f4164-433">For information about hello physical resources that Service Fabric can govern on nodes, see [resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="f4164-434">如需設定自訂計量及其用法的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="f4164-434">For information on configuring custom metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="f4164-435">計量不同於放置條件約束和節點屬性。</span><span class="sxs-lookup"><span data-stu-id="f4164-435">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="f4164-436">節點屬性都是靜態的描述元的 hello 節點本身。</span><span class="sxs-lookup"><span data-stu-id="f4164-436">Node properties are static descriptors of hello nodes themselves.</span></span> <span data-ttu-id="f4164-437">計量說明節點所擁有的資源，以及在節點上執行時取用的服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-437">Metrics describe resources that nodes have and that services consume when they are run on a node.</span></span> <span data-ttu-id="f4164-438">節點屬性可以是"HasSSD 」，而且無法將設定 tootrue 或 false。</span><span class="sxs-lookup"><span data-stu-id="f4164-438">A node property could be "HasSSD" and could be set tootrue or false.</span></span> <span data-ttu-id="f4164-439">hello 數量的可用空間的 SSD 和多少由服務上是類似"DriveSpaceInMb 」 的度量。</span><span class="sxs-lookup"><span data-stu-id="f4164-439">hello amount of space available on that SSD and how much is consumed by services would be a metric like “DriveSpaceInMb”.</span></span> 

<span data-ttu-id="f4164-440">如同位置條件約束和節點屬性 hello Service Fabric 叢集資源管理員不了解哪些 hello 的名稱 hello 度量的平均值的重要 toonote 它。</span><span class="sxs-lookup"><span data-stu-id="f4164-440">It is important toonote that just like for placement constraints and node properties, hello Service Fabric Cluster Resource Manager doesn't understand what hello names of hello metrics mean.</span></span> <span data-ttu-id="f4164-441">計量名稱只是字串。</span><span class="sxs-lookup"><span data-stu-id="f4164-441">Metric names are just strings.</span></span> <span data-ttu-id="f4164-442">它是很好的作法 toodeclare 單位可能是模稜兩可時，您建立的 hello 度量名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="f4164-442">It is a good practice toodeclare units as a part of hello metric names that you create when it could be ambiguous.</span></span>

## <a name="capacity"></a><span data-ttu-id="f4164-443">容量</span><span class="sxs-lookup"><span data-stu-id="f4164-443">Capacity</span></span>
<span data-ttu-id="f4164-444">如果您關閉所有資源「平衡」，Service Fabric 的叢集資源管理員仍會確保節點不超出其容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-444">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="f4164-445">管理容量溢位是可能的除非 hello 叢集已滿或 hello 工作負載大於任何節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-445">Managing capacity overruns is possible unless hello cluster is too full or hello workload is larger than any node.</span></span> <span data-ttu-id="f4164-446">容量是另一個*條件約束*該 hello 叢集資源管理員會使用 toounderstand 有多少節點的資源。</span><span class="sxs-lookup"><span data-stu-id="f4164-446">Capacity is another *constraint* that hello Cluster Resource Manager uses toounderstand how much of a resource a node has.</span></span> <span data-ttu-id="f4164-447">剩餘容量也會追蹤 hello 叢集的整體。</span><span class="sxs-lookup"><span data-stu-id="f4164-447">Remaining capacity is also tracked for hello cluster as a whole.</span></span> <span data-ttu-id="f4164-448">度量都以表示 hello 容量和 hello hello 服務層級的耗用量。</span><span class="sxs-lookup"><span data-stu-id="f4164-448">Both hello capacity and hello consumption at hello service level are expressed in terms of metrics.</span></span> <span data-ttu-id="f4164-449">例如，hello 度量可能"ClientConnections 」，而且在指定的節點可能有 「 ClientConnections"32768 的容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-449">So for example, hello metric might be "ClientConnections" and a given Node may have a capacity for "ClientConnections" of 32768.</span></span> <span data-ttu-id="f4164-450">其他節點可以有一些服務，可以為節點上執行假設它目前耗用 32256 hello 標準 「 ClientConnections 」 的其他限制。</span><span class="sxs-lookup"><span data-stu-id="f4164-450">Other nodes can have other limits Some service running on that node can say it is currently consuming 32256 of hello metric "ClientConnections".</span></span>

<span data-ttu-id="f4164-451">在執行階段 hello 叢集資源管理員會追蹤剩餘容量 hello 叢集中，並在節點上。</span><span class="sxs-lookup"><span data-stu-id="f4164-451">During runtime, hello Cluster Resource Manager tracks remaining capacity in hello cluster and on nodes.</span></span> <span data-ttu-id="f4164-452">在順序 tootrack 容量 hello 叢集資源管理員會減去每個服務的使用方式從 hello 服務執行所在之節點的容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-452">In order tootrack capacity hello Cluster Resource Manager subtracts each service's usage from node's capacity where hello service runs.</span></span> <span data-ttu-id="f4164-453">利用此資訊，hello Service Fabric 叢集資源管理員可找出哪裡 tooplace 或移動複本，讓節點不討論容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-453">With this information, hello Service Fabric Cluster Resource Manager can figure out where tooplace or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="f4164-454"><center>
![叢集節點和容量][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="f4164-454"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="f4164-455">C#：</span><span class="sxs-lookup"><span data-stu-id="f4164-455">C#:</span></span>

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="f4164-456">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="f4164-456">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

<span data-ttu-id="f4164-457">您可以看到 hello 叢集資訊清單中定義的容量：</span><span class="sxs-lookup"><span data-stu-id="f4164-457">You can see capacities defined in hello cluster manifest:</span></span>

<span data-ttu-id="f4164-458">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f4164-458">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="f4164-459">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。</span><span class="sxs-lookup"><span data-stu-id="f4164-459">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

<span data-ttu-id="f4164-460">服務的負載通常會動態變更。</span><span class="sxs-lookup"><span data-stu-id="f4164-460">Commonly a service’s load changes dynamically.</span></span> <span data-ttu-id="f4164-461">說出複本的負載"ClientConnections 」 的變更從 1024 too2048，但是它上執行，則只有該標準剩餘的 512 容量 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-461">Say that a replica's load of "ClientConnections" changed from 1024 too2048, but hello node it was running on then only had 512 capacity remaining for that metric.</span></span> <span data-ttu-id="f4164-462">現在，該複本或執行個體的放置已無效，因為該節點上沒有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="f4164-462">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="f4164-463">hello 叢集資源管理員中有 tookick 和取得回下方容量 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="f4164-463">hello Cluster Resource Manager has tookick in and get hello node back below capacity.</span></span> <span data-ttu-id="f4164-464">它可減少從該節點 tooother 節點移動一或多個 hello 複本或執行個體是透過容量的 hello 節點上的負載。</span><span class="sxs-lookup"><span data-stu-id="f4164-464">It reduces load on hello node that is over capacity by moving one or more of hello replicas or instances from that node tooother nodes.</span></span> <span data-ttu-id="f4164-465">當您移動複本，hello 叢集資源管理員會嘗試這些移動 toominimize hello 成本。</span><span class="sxs-lookup"><span data-stu-id="f4164-465">When moving replicas, hello Cluster Resource Manager tries toominimize hello cost of those movements.</span></span> <span data-ttu-id="f4164-466">移動成本述[本文](service-fabric-cluster-resource-manager-movement-cost.md)更多有關 hello 叢集資源管理員的重新平衡策略和規則描述[這裡](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="f4164-466">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md) and more about hello Cluster Resource Manager's rebalancing strategies and rules is described [here](service-fabric-cluster-resource-manager-metrics.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="f4164-467">叢集容量</span><span class="sxs-lookup"><span data-stu-id="f4164-467">Cluster capacity</span></span>
<span data-ttu-id="f4164-468">如何沒有 hello Service Fabric 叢集資源管理員保留 hello 整體叢集不要太滿？</span><span class="sxs-lookup"><span data-stu-id="f4164-468">So how does hello Service Fabric Cluster Resource Manager keep hello overall cluster from being too full?</span></span> <span data-ttu-id="f4164-469">使用動態負載的話，它並沒有太多可以執行的工作。</span><span class="sxs-lookup"><span data-stu-id="f4164-469">Well, with dynamic load there’s not a lot it can do.</span></span> <span data-ttu-id="f4164-470">服務可以有獨立 hello 叢集資源管理員所採取的動作其負載突然增加。</span><span class="sxs-lookup"><span data-stu-id="f4164-470">Services can have their load spike independently of actions taken by hello Cluster Resource Manager.</span></span> <span data-ttu-id="f4164-471">因此，您的叢集今天有充足的空餘空間，明天就可能因為出名而後繼無力。</span><span class="sxs-lookup"><span data-stu-id="f4164-471">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="f4164-472">話雖如此，還有一些會燒 tooprevent 問題的控制項。</span><span class="sxs-lookup"><span data-stu-id="f4164-472">That said, there are some controls that are baked in tooprevent problems.</span></span> <span data-ttu-id="f4164-473">我們可以進行 hello 第一件事是防止 hello 建立新的工作負載，可能導致 hello 叢集 toobecome 完整。</span><span class="sxs-lookup"><span data-stu-id="f4164-473">hello first thing we can do is prevent hello creation of new workloads that would cause hello cluster toobecome full.</span></span>

<span data-ttu-id="f4164-474">假設您建立無狀態服務，而它有一些與它相關聯的負載。</span><span class="sxs-lookup"><span data-stu-id="f4164-474">Say that you create a stateless service and it has some load associated with it.</span></span> <span data-ttu-id="f4164-475">讓我們假設 hello 服務重視 hello"DiskSpaceInMb"度量。</span><span class="sxs-lookup"><span data-stu-id="f4164-475">Let’s say that hello service cares about hello "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="f4164-476">我們也假設它是 「 DiskSpaceInMb 「 每個執行個體的 hello 服務的持續 tooconsume 五個單位。</span><span class="sxs-lookup"><span data-stu-id="f4164-476">Let's also say that it is going tooconsume five units of "DiskSpaceInMb" for every instance of hello service.</span></span> <span data-ttu-id="f4164-477">您想 toocreate hello 服務的三個執行個體。</span><span class="sxs-lookup"><span data-stu-id="f4164-477">You want toocreate three instances of hello service.</span></span> <span data-ttu-id="f4164-478">太棒了！</span><span class="sxs-lookup"><span data-stu-id="f4164-478">Great!</span></span> <span data-ttu-id="f4164-479">如此一來，表示我們需要 15 單位 」 DiskSpaceInMb"toobe hello 叢集中，為了讓我們 tooeven 是無法 toocreate 這些服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="f4164-479">So that means that we need 15 units of "DiskSpaceInMb" toobe present in hello cluster in order for us tooeven be able toocreate these service instances.</span></span> <span data-ttu-id="f4164-480">hello 叢集資源管理員持續計算 hello 容量和每個度量的耗用量，因此它可以判斷 hello hello 叢集中的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-480">hello Cluster Resource Manager continually calculates hello capacity and consumption of each metric so it can determine hello remaining capacity in hello cluster.</span></span> <span data-ttu-id="f4164-481">如果沒有足夠的空間，叢集資源管理員拒絕 hello hello 建立服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="f4164-481">If there isn't enough space, hello Cluster Resource Manager rejects hello create service call.</span></span>

<span data-ttu-id="f4164-482">由於 hello 需求，但是有可用 15 的單位，此空間無法配置許多不同的方式。</span><span class="sxs-lookup"><span data-stu-id="f4164-482">Since hello requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="f4164-483">例如，15 個不同節點上可能剩餘一個單位的容量，或五個不同節點上剩餘三個單位的容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-483">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="f4164-484">如果 hello 叢集資源管理員可以重新排列項目，讓三個節點上有可用的五個單位的就會將 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-484">If hello Cluster Resource Manager can rearrange things so there's five units available on three nodes, it places hello service.</span></span> <span data-ttu-id="f4164-485">除非 hello 叢集幾乎已滿或無法合併 hello 現有服務，因為某些原因，是通常可以重新排列 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="f4164-485">Rearranging hello cluster is usually possible unless hello cluster is almost full or hello existing services can't be consolidated for some reason.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="f4164-486">緩衝處理的容量</span><span class="sxs-lookup"><span data-stu-id="f4164-486">Buffered Capacity</span></span>
<span data-ttu-id="f4164-487">緩衝的容量是 hello 的另一項功能叢集資源管理員。</span><span class="sxs-lookup"><span data-stu-id="f4164-487">Buffered capacity is another feature of hello Cluster Resource Manager.</span></span> <span data-ttu-id="f4164-488">它可讓 hello 的某些部分的保留整體節點容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-488">It allows reservation of some portion of hello overall node capacity.</span></span> <span data-ttu-id="f4164-489">這個容量緩衝區是唯一使用的 tooplace services 升級和節點失敗時。</span><span class="sxs-lookup"><span data-stu-id="f4164-489">This capacity buffer is only used tooplace services during upgrades and node failures.</span></span> <span data-ttu-id="f4164-490">緩衝處理的容量是針對所有節點的每個計量進行全域指定。</span><span class="sxs-lookup"><span data-stu-id="f4164-490">Buffered Capacity is specified globally per metric for all nodes.</span></span> <span data-ttu-id="f4164-491">您挑選 hello 保留容量的 hello 值為 hello 容錯和您擁有 hello 叢集中的升級網域數目的函式。</span><span class="sxs-lookup"><span data-stu-id="f4164-491">hello value you pick for hello reserved capacity is a function of hello number of Fault and Upgrade Domains you have in hello cluster.</span></span> <span data-ttu-id="f4164-492">容錯網域和升級網域越多，表示您可以挑選較小的緩衝容量。</span><span class="sxs-lookup"><span data-stu-id="f4164-492">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="f4164-493">如果您有多個網域，您可以升級與失敗時，預期較少量的叢集 toobe 無法使用。</span><span class="sxs-lookup"><span data-stu-id="f4164-493">If you have more domains, you can expect smaller amounts of your cluster toobe unavailable during upgrades and failures.</span></span> <span data-ttu-id="f4164-494">指定緩衝處理的容量才有意義如果您另有指定的 hello 節點容量標準。</span><span class="sxs-lookup"><span data-stu-id="f4164-494">Specifying Buffered Capacity only makes sense if you have also specified hello node capacity for a metric.</span></span>

<span data-ttu-id="f4164-495">以下是如何 toospecify 緩衝處理容量的範例：</span><span class="sxs-lookup"><span data-stu-id="f4164-495">Here's an example of how toospecify buffered capacity:</span></span>

<span data-ttu-id="f4164-496">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="f4164-496">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="f4164-497">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="f4164-497">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

<span data-ttu-id="f4164-498">hello 叢集超出標準緩衝容量時，就會失敗 hello 建立新的服務。</span><span class="sxs-lookup"><span data-stu-id="f4164-498">hello creation of new services fails when hello cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="f4164-499">防止 hello 建立新的服務 toopreserve hello 緩衝區，可確保的升級和失敗不會使節點 toogo 低於產能。</span><span class="sxs-lookup"><span data-stu-id="f4164-499">Preventing hello creation of new services toopreserve hello buffer ensures that upgrades and failures don’t cause nodes toogo over capacity.</span></span> <span data-ttu-id="f4164-500">緩衝容量是選擇性，但建議用在已定義計量容量的任何叢集。</span><span class="sxs-lookup"><span data-stu-id="f4164-500">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="f4164-501">hello 叢集資源管理員會公開此載入資訊。</span><span class="sxs-lookup"><span data-stu-id="f4164-501">hello Cluster Resource Manager exposes this load information.</span></span> <span data-ttu-id="f4164-502">對於每個計量，這項資訊包括：</span><span class="sxs-lookup"><span data-stu-id="f4164-502">For each metric, this information includes:</span></span> 
  - <span data-ttu-id="f4164-503">hello 緩衝處理的容量設定</span><span class="sxs-lookup"><span data-stu-id="f4164-503">hello buffered capacity settings</span></span>
  - <span data-ttu-id="f4164-504">hello 總容量</span><span class="sxs-lookup"><span data-stu-id="f4164-504">hello total capacity</span></span>
  - <span data-ttu-id="f4164-505">hello 目前的耗用量</span><span class="sxs-lookup"><span data-stu-id="f4164-505">hello current consumption</span></span>
  - <span data-ttu-id="f4164-506">每個計量是否被視為平衡</span><span class="sxs-lookup"><span data-stu-id="f4164-506">whether each metric is considered balanced or not</span></span>
  - <span data-ttu-id="f4164-507">hello 標準差的相關統計資料</span><span class="sxs-lookup"><span data-stu-id="f4164-507">statistics about hello standard deviation</span></span>
  - <span data-ttu-id="f4164-508">具有大部分和最少負載 hello hello 節點</span><span class="sxs-lookup"><span data-stu-id="f4164-508">hello nodes which have hello most and least load</span></span>  
  
<span data-ttu-id="f4164-509">我們可以看到該輸出的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="f4164-509">Below we see an example of that output:</span></span>

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a><span data-ttu-id="f4164-510">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4164-510">Next steps</span></span>
* <span data-ttu-id="f4164-511">如 hello 叢集資源管理員中的 hello 架構和資訊流程的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="f4164-511">For information on hello architecture and information flow within hello Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="f4164-512">定義磁碟重組度量資訊是其中一種方式 tooconsolidate 負載，而不是分配的節點上。toolearn 如何 tooconfigure 磁碟重組，請參閱太[這篇文章](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="f4164-512">Defining Defragmentation Metrics is one way tooconsolidate load on nodes instead of spreading it out. toolearn how tooconfigure defragmentation, refer too[this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="f4164-513">Hello 從頭開始並[取得簡介 toohello Service Fabric 叢集資源管理員](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f4164-513">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="f4164-514">toofind 出 hello 叢集資源管理員如何管理和 hello 叢集中的負載平衡簽出 hello 發行項上[平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="f4164-514">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
