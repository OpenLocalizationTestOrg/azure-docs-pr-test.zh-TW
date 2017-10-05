---
title: "叢集資源管理員叢集描述 | Microsoft Docs"
description: "將容錯網域、升級網域、節點屬性和節點容量指定給叢集資源管理員，以描述 Service Fabric 叢集。"
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
ms.openlocfilehash: e517eda4d3ff7ad81998003688c3cca78f76e179
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="describing-a-service-fabric-cluster"></a><span data-ttu-id="2f15a-103">描述 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="2f15a-103">Describing a service fabric cluster</span></span>
<span data-ttu-id="2f15a-104">Service Fabric 叢集資源管理員提供數種機制，來描述叢集。</span><span class="sxs-lookup"><span data-stu-id="2f15a-104">The Service Fabric Cluster Resource Manager provides several mechanisms for describing a cluster.</span></span> <span data-ttu-id="2f15a-105">在執行階段，叢集資源管理員會使用此資訊，以確保叢集中執行之服務的高可用性。</span><span class="sxs-lookup"><span data-stu-id="2f15a-105">During runtime, the Cluster Resource Manager uses this information to ensure high availability of the services running in the cluster.</span></span> <span data-ttu-id="2f15a-106">在強制執行這些重要規則時，它也會嘗試將叢集的資源消耗量最佳化。</span><span class="sxs-lookup"><span data-stu-id="2f15a-106">While enforcing these important rules, it also attempts to optimize the resource consumption within the cluster.</span></span>

## <a name="key-concepts"></a><span data-ttu-id="2f15a-107">重要概念</span><span class="sxs-lookup"><span data-stu-id="2f15a-107">Key concepts</span></span>
<span data-ttu-id="2f15a-108">叢集資源管理員支援數個描述叢集的功能︰</span><span class="sxs-lookup"><span data-stu-id="2f15a-108">The Cluster Resource Manager supports several features that describe a cluster:</span></span>

* <span data-ttu-id="2f15a-109">容錯網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-109">Fault Domains</span></span>
* <span data-ttu-id="2f15a-110">升級網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-110">Upgrade Domains</span></span>
* <span data-ttu-id="2f15a-111">節點屬性</span><span class="sxs-lookup"><span data-stu-id="2f15a-111">Node Properties</span></span>
* <span data-ttu-id="2f15a-112">節點容量</span><span class="sxs-lookup"><span data-stu-id="2f15a-112">Node Capacities</span></span>

## <a name="fault-domains"></a><span data-ttu-id="2f15a-113">容錯網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-113">Fault domains</span></span>
<span data-ttu-id="2f15a-114">容錯網域是任何連鎖故障區域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-114">A Fault Domain is any area of coordinated failure.</span></span> <span data-ttu-id="2f15a-115">單一電腦是一個容錯網域 (因為它本身可能因各種原因而失敗，例如電源供應器故障、磁碟機故障或 NIC 韌體不正確)。</span><span class="sxs-lookup"><span data-stu-id="2f15a-115">A single machine is a Fault Domain (since it can fail on its own for various reasons, from power supply failures to drive failures to bad NIC firmware).</span></span> <span data-ttu-id="2f15a-116">連線至相同乙太網路交換器的電腦位於相同的容錯網域，共用單一位置之單一電源的電腦也是如此。</span><span class="sxs-lookup"><span data-stu-id="2f15a-116">Machines connected to the same Ethernet switch are in the same Fault Domain, as are machines sharing a single source of power or in a single location.</span></span> <span data-ttu-id="2f15a-117">由於硬體故障天生就會重疊，容錯網域本質上就具備階層性，且在 Service Fabric 中以 URI 表示。</span><span class="sxs-lookup"><span data-stu-id="2f15a-117">Since it's natural for hardware faults to overlap, Fault Domains are inherently hierarchal and are represented as URIs in Service Fabric.</span></span>

<span data-ttu-id="2f15a-118">必須正確設定容錯網域，因為 Service Fabric 會使用這項資訊來安全地放置服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-118">It is important that Fault Domains are set up correctly since Service Fabric uses this information to safely place services.</span></span> <span data-ttu-id="2f15a-119">Service Fabric 放置服務時會注意不要因為遺失容錯網域 (某個元件失敗所造成) 而導致服務中斷。</span><span class="sxs-lookup"><span data-stu-id="2f15a-119">Service Fabric doesn't want to place services such that the loss of a Fault Domain (caused by the failure of some component) causes a service to go down.</span></span> <span data-ttu-id="2f15a-120">在 Azure 環境中，Service Fabric 會使用環境所提供的容錯網域資訊，代替您正確地設定叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-120">In the Azure environment Service Fabric uses the Fault Domain information provided by the environment to correctly configure the nodes in the cluster on your behalf.</span></span> <span data-ttu-id="2f15a-121">對於 Service Fabric Standalone，容錯網域會在叢集設定時定義。</span><span class="sxs-lookup"><span data-stu-id="2f15a-121">For Service Fabric Standalone, Fault Domains are defined at the time that the cluster is set up</span></span> 

> [!WARNING]
> <span data-ttu-id="2f15a-122">將正確的容錯網域資訊提供給 Service Fabric 相當重要。</span><span class="sxs-lookup"><span data-stu-id="2f15a-122">It is important that the Fault Domain information provided to Service Fabric is accurate.</span></span> <span data-ttu-id="2f15a-123">例如，假設 Service Fabric 叢集是在 10 部虛擬機器上執行，這些虛擬機器是在五個實體主機上執行。</span><span class="sxs-lookup"><span data-stu-id="2f15a-123">For example, let's say that your Service Fabric cluster's nodes are running inside 10 virtual machines, running on five physical hosts.</span></span> <span data-ttu-id="2f15a-124">在此情況下，即使有 10 部虛擬機器，也只有 5 個不同的 (最上層) 容錯網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-124">In this case, even though there are 10 virtual machines, there's only 5 different (top level) fault domains.</span></span> <span data-ttu-id="2f15a-125">共用相同的實體主機會造成 VM 共用相同的根容錯網域，因為如果其實體主機失敗，VM 會遇到協調失敗。</span><span class="sxs-lookup"><span data-stu-id="2f15a-125">Sharing the same physical host causes VMs to share the same root fault domain, since the VMs experience coordinated failure if their physical host fails.</span></span>  
>
> <span data-ttu-id="2f15a-126">因為 Service Fabric 預期節點的容錯網域不會變更。</span><span class="sxs-lookup"><span data-stu-id="2f15a-126">Since Service Fabric expects the Fault Domain of a node not to change.</span></span> <span data-ttu-id="2f15a-127">確保 VM (例如 [HA-VM](https://technet.microsoft.com/en-us/library/cc967323.aspx)) 高可用性的其他機制，是使用從一台主機到另一台主機的 VM 透明移轉。</span><span class="sxs-lookup"><span data-stu-id="2f15a-127">Other mechanisms of ensuring high availability of the VMs, such as [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use transparent migration of VMs from one host to another.</span></span> <span data-ttu-id="2f15a-128">這些機制不會重新設定或通知在 VM 內的執行中程式碼。</span><span class="sxs-lookup"><span data-stu-id="2f15a-128">These mechanisms do not reconfigure or notify the running code inside the VM.</span></span> <span data-ttu-id="2f15a-129">因此，它們**不支援**作為執行中 Service Fabric 叢集的環境。</span><span class="sxs-lookup"><span data-stu-id="2f15a-129">As such, they are **not supported** as environments for running Service Fabric clusters.</span></span> <span data-ttu-id="2f15a-130">Service Fabric 應該僅採用高可用性技術。</span><span class="sxs-lookup"><span data-stu-id="2f15a-130">Service Fabric should be the only high-availability technology employed.</span></span> <span data-ttu-id="2f15a-131">不需要像是即時 VM 移轉、SAN 或其他項目的機制。</span><span class="sxs-lookup"><span data-stu-id="2f15a-131">Mechanisms like live VM migration, SANs, or others are not necessary.</span></span> <span data-ttu-id="2f15a-132">如果與 Service Fabric 搭配使用，這些機制會_減少_應用程式可用性和可靠性，因為它們會導致額外的複雜性、新增集中式失敗來源，並且使用與 Service Fabric 衝突的可靠性和可用性策略。</span><span class="sxs-lookup"><span data-stu-id="2f15a-132">If used in conjunction with Service Fabric, these mechanisms _reduce_ application availability and reliability because they introduce additional complexity, add centralized sources of failure, and utilize reliability and availability strategies that conflict with those in Service Fabric.</span></span> 
>
>

<span data-ttu-id="2f15a-133">下圖中，我們將所有參與容錯網域的實體塗上顏色，並列出形成的所有不同容錯網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-133">In the graphic below we color all the entities that contribute to Fault Domains and list all the different Fault Domains that result.</span></span> <span data-ttu-id="2f15a-134">在此範例中，我們有資料中心 ("DC")、機架 ("R") 和刀鋒伺服器 ("B")。</span><span class="sxs-lookup"><span data-stu-id="2f15a-134">In this example, we have datacenters ("DC"), racks ("R"), and blades ("B").</span></span> <span data-ttu-id="2f15a-135">如果每個刀鋒伺服器包含一個以上的虛擬機器，可以預料，容錯網域階層中還會有另一層。</span><span class="sxs-lookup"><span data-stu-id="2f15a-135">Conceivably, if each blade holds more than one virtual machine, there could be another layer in the Fault Domain hierarchy.</span></span>

<span data-ttu-id="2f15a-136"><center>
![透過容錯網域組織的節點][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-136"><center>
![Nodes organized via Fault Domains][Image1]
</center></span></span>

<span data-ttu-id="2f15a-137">在執行階段，Service Fabric 叢集資源管理員會考慮叢集中的容錯網域，並規劃配置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-137">During runtime, the Service Fabric Cluster Resource Manager considers the Fault Domains in the cluster and plans layouts.</span></span> <span data-ttu-id="2f15a-138">指定服務的具狀態複本或無狀態執行個體會分散，讓它們位在不同的容錯網域中。</span><span class="sxs-lookup"><span data-stu-id="2f15a-138">The stateful replicas or stateless instances for a given service are distributed so they are in separate Fault Domains.</span></span> <span data-ttu-id="2f15a-139">跨容錯網域分散服務，可確保當容錯網域在階層的任何層級失敗時，服務的可用性不會受到危害。</span><span class="sxs-lookup"><span data-stu-id="2f15a-139">Distributing the service across fault domains ensures the availability of the service is not compromised when a Fault Domain fails at any level of the hierarchy.</span></span>

<span data-ttu-id="2f15a-140">Service Fabric 的叢集資源管理員不在乎容錯網域階層中有多少層。</span><span class="sxs-lookup"><span data-stu-id="2f15a-140">Service Fabric’s Cluster Resource Manager doesn’t care how many layers there are in the Fault Domain hierarchy.</span></span> <span data-ttu-id="2f15a-141">不過，當階層的任何一部分遺失時，它會嘗試確保這不會影響上方執行的服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-141">However, it tries to ensure that the loss of any one portion of the hierarchy doesn’t impact services running in it.</span></span> 

<span data-ttu-id="2f15a-142">在容錯網域階層中每個深度上，最好有相同的節點數目。</span><span class="sxs-lookup"><span data-stu-id="2f15a-142">It is best if there are the same number of nodes at each level of depth in the Fault Domain hierarchy.</span></span> <span data-ttu-id="2f15a-143">如果叢集中的容錯網域「樹狀結構」不平衡，叢集資源管理員會很難找出服務的最佳配置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-143">If the “tree” of Fault Domains is unbalanced in your cluster, it makes it harder for the Cluster Resource Manager to figure out the best allocation of services.</span></span> <span data-ttu-id="2f15a-144">不平衡的容錯網域配置表示遺失某些網域時，服務可用性受影響的程度可能大於其他網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-144">Imbalanced Fault Domains layouts mean that the loss of some domains impact the availability of services more than other domains.</span></span> <span data-ttu-id="2f15a-145">因此，叢集資源管理員在兩個目標之間掙扎︰希望將服務放在該「重負荷」網域中的電腦上以使用這些電腦，也希望在其他網域放置服務時不要因為遺失網域而造成問題。</span><span class="sxs-lookup"><span data-stu-id="2f15a-145">As a result, the Cluster Resource Manager is torn between two goals: It wants to use the machines in that “heavy” domain by placing services on them, and it wants to place services in other domains so that the loss of a domain doesn’t cause problems.</span></span> 

<span data-ttu-id="2f15a-146">不平衡網域外觀為何？</span><span class="sxs-lookup"><span data-stu-id="2f15a-146">What do imbalanced domains look like?</span></span> <span data-ttu-id="2f15a-147">下圖中，我們顯示兩個不同的叢集配置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-147">In the diagram below, we show two different cluster layouts.</span></span> <span data-ttu-id="2f15a-148">在第一個範例中，節點平均分散至容錯網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-148">In the first example, the nodes are distributed evenly across the Fault Domains.</span></span> <span data-ttu-id="2f15a-149">在第二個範例中，一個容錯網域比其他容錯網域具有更多節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-149">In the second example, one Fault Domain has many more nodes than the other Fault Domains.</span></span> 

<span data-ttu-id="2f15a-150"><center>
![兩個不同的叢集配置][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-150"><center>
![Two different cluster layouts][Image2]
</center></span></span>

<span data-ttu-id="2f15a-151">在 Azure 中會替您選擇哪一個容錯網域包含節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-151">In Azure, the choice of which Fault Domain contains a node is managed for you.</span></span> <span data-ttu-id="2f15a-152">不過，根據您佈建的節點數目而定，某些容錯網域的節點最後仍可能比其他容錯網域更多。</span><span class="sxs-lookup"><span data-stu-id="2f15a-152">However, depending on the number of nodes that you provision you can still end up with Fault Domains with more nodes in them than others.</span></span> <span data-ttu-id="2f15a-153">例如，假設您在叢集中有五個容錯網域，但佈建特定 NodeType 的七個節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-153">For example, say you have five Fault Domains in the cluster but provision seven nodes for a given NodeType.</span></span> <span data-ttu-id="2f15a-154">在此情況下，前兩個容錯網域最後會有較多節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-154">In this case, the first two Fault Domains end up with more nodes.</span></span> <span data-ttu-id="2f15a-155">如果您繼續部署多個 NodeType，但只有幾個執行個體，則問題會更糟。</span><span class="sxs-lookup"><span data-stu-id="2f15a-155">If you continue to deploy more NodeTypes with only a couple instances, the problem gets worse.</span></span> <span data-ttu-id="2f15a-156">基於這個原因，建議每個節點類型中的節點數目是容錯網域數目的倍數。</span><span class="sxs-lookup"><span data-stu-id="2f15a-156">For this reason it's recommended that the number of nodes in each node type is a multiple of the number of Fault Domains.</span></span>

## <a name="upgrade-domains"></a><span data-ttu-id="2f15a-157">升級網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-157">Upgrade domains</span></span>
<span data-ttu-id="2f15a-158">升級網域是另一項功能，可協助 Service Fabric 叢集資源管理員了解叢集的配置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-158">Upgrade Domains are another feature that helps the Service Fabric Cluster Resource Manager understand the layout of the cluster.</span></span> <span data-ttu-id="2f15a-159">升級網域定義一組同時升級的節點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-159">Upgrade Domains define sets of nodes that are upgraded at the same time.</span></span> <span data-ttu-id="2f15a-160">升級網域可協助叢集資源管理員了解及協調例如升級的管理作業。</span><span class="sxs-lookup"><span data-stu-id="2f15a-160">Upgrade Domains help the Cluster Resource Manager understand and orchestrate management operations like upgrades.</span></span>

<span data-ttu-id="2f15a-161">升級網域非常類似容錯網域，但是有幾個主要的差異。</span><span class="sxs-lookup"><span data-stu-id="2f15a-161">Upgrade Domains are a lot like Fault Domains, but with a couple key differences.</span></span> <span data-ttu-id="2f15a-162">首先，協調硬體失敗的區域會定義容錯網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-162">First, areas of coordinated hardware failures define Fault Domains.</span></span> <span data-ttu-id="2f15a-163">另一方面，升級網域會定義原則。</span><span class="sxs-lookup"><span data-stu-id="2f15a-163">Upgrade Domains, on the other hand, are defined by policy.</span></span> <span data-ttu-id="2f15a-164">您應該決定想要多少個節點，而不是取決於環境。</span><span class="sxs-lookup"><span data-stu-id="2f15a-164">You get to decide how many you want, rather than it being dictated by the environment.</span></span> <span data-ttu-id="2f15a-165">您可能會有與節點一樣多的升級網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-165">You could have as many Upgrade Domains as you do nodes.</span></span> <span data-ttu-id="2f15a-166">容錯網域和升級網域的另一個差異在於升級網域不是階層式。</span><span class="sxs-lookup"><span data-stu-id="2f15a-166">Another difference between Fault Domains and Upgrade Domains is that Upgrade Domains are not hierarchical.</span></span> <span data-ttu-id="2f15a-167">相反地，它們更像是簡單的標記。</span><span class="sxs-lookup"><span data-stu-id="2f15a-167">Instead, they are more like a simple tag.</span></span> 

<span data-ttu-id="2f15a-168">下圖顯示三個升級網域等量分佈在三個容錯網域上。</span><span class="sxs-lookup"><span data-stu-id="2f15a-168">The following diagram shows three Upgrade Domains are striped across three Fault Domains.</span></span> <span data-ttu-id="2f15a-169">其中也顯示不具狀態服務的三個不同複本有一個可能的位置，而每一個最後都在不同的容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-169">It also shows one possible placement for three different replicas of a stateful service, where each ends up in different Fault and Upgrade Domains.</span></span> <span data-ttu-id="2f15a-170">在服務升級期間，即使遺失容錯網域，這個位置可讓我們仍然保有一份程式碼和資料。</span><span class="sxs-lookup"><span data-stu-id="2f15a-170">This placement allows the loss of a Fault Domain while in the middle of a service upgrade and still have one copy of the code and data.</span></span>  

<span data-ttu-id="2f15a-171"><center>
容錯網域和升級網域的位置![][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-171"><center>
![Placement With Fault and Upgrade Domains][Image3]
</center></span></span>

<span data-ttu-id="2f15a-172">大量升級網域有其利弊。</span><span class="sxs-lookup"><span data-stu-id="2f15a-172">There are pros and cons to having large numbers of Upgrade Domains.</span></span> <span data-ttu-id="2f15a-173">升級網域越多表示每個升級步驟會更輕微，因此受影響的節點或服務較少。</span><span class="sxs-lookup"><span data-stu-id="2f15a-173">More Upgrade Domains means each step of the upgrade is more granular and therefore affects a smaller number of nodes or services.</span></span> <span data-ttu-id="2f15a-174">因為必須一次移動的服務較少，對系統的影響較小。</span><span class="sxs-lookup"><span data-stu-id="2f15a-174">As a result, fewer services have to move at a time, introducing less churn into the system.</span></span> <span data-ttu-id="2f15a-175">這樣較容易改善可靠性，因為升級期間發生的任何問題會影響較少的服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-175">This tends to improve reliability, since less of the service is impacted by any issue introduced during the upgrade.</span></span> <span data-ttu-id="2f15a-176">升級網域越多，也表示其他節點上需要較少的可用緩衝區來處理升級的影響。</span><span class="sxs-lookup"><span data-stu-id="2f15a-176">More Upgrade Domains also means that you need less available buffer on other nodes to handle the impact of the upgrade.</span></span> <span data-ttu-id="2f15a-177">例如，若您有五個升級網域，則每個網域的節點可處理大約 20% 的流量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-177">For example, if you have five Upgrade Domains, the nodes in each are handling roughly 20% of your traffic.</span></span> <span data-ttu-id="2f15a-178">如果您需要關閉升級網域以進行升級，則負載通常必須移至別處。</span><span class="sxs-lookup"><span data-stu-id="2f15a-178">If you need to take down that Upgrade Domain for an upgrade, that load usually needs to go somewhere.</span></span> <span data-ttu-id="2f15a-179">因為您有四個剩餘的升級網域，每一個都必須有大約總流量 5% 的空間。</span><span class="sxs-lookup"><span data-stu-id="2f15a-179">Since you have four remaining Upgrade Domains, each must have room for about 5% of the total traffic.</span></span> <span data-ttu-id="2f15a-180">多個升級網域表示您在叢集之節點上需要較少的緩衝區。</span><span class="sxs-lookup"><span data-stu-id="2f15a-180">More Upgrade Domains means you need less buffer on the nodes in the cluster.</span></span> <span data-ttu-id="2f15a-181">例如，請考慮如果您擁有 10 個升級網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-181">For example, consider if you had 10 Upgrade Domains instead.</span></span> <span data-ttu-id="2f15a-182">在此情況下，每個 UD 只會處理大約總流量的 10%。</span><span class="sxs-lookup"><span data-stu-id="2f15a-182">In that case, each UD would only be handling about 10% of the total traffic.</span></span> <span data-ttu-id="2f15a-183">當升級步驟是透過叢集時，每個網域只需要有大約總流量 1.1% 的空間。</span><span class="sxs-lookup"><span data-stu-id="2f15a-183">When an upgrade steps through the cluster, each domain would only need to have room for about 1.1% of the total traffic.</span></span> <span data-ttu-id="2f15a-184">多個升級網域通常可讓您在更高的使用率之下執行您的節點，因為您需要較少的保留容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-184">More Upgrade Domains generally allow you to run your nodes at higher utilization, since you need less reserved capacity.</span></span> <span data-ttu-id="2f15a-185">同樣的作法也適用於容錯網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-185">The same is true for Fault Domains.</span></span>  

<span data-ttu-id="2f15a-186">擁有許多升級網域的缺點是升級通常需要較長的時間。</span><span class="sxs-lookup"><span data-stu-id="2f15a-186">The downside of having many Upgrade Domains is that upgrades tend to take longer.</span></span> <span data-ttu-id="2f15a-187">Service Fabric 會在升級網域完成之後等候一段時間，並且在開始升級下一個升級網域之前執行檢查。</span><span class="sxs-lookup"><span data-stu-id="2f15a-187">Service Fabric waits a short period of time after an Upgrade Domain is completed and performs checks before starting to upgrade the next one.</span></span> <span data-ttu-id="2f15a-188">這些延遲可讓系統在升級繼續之前偵測由升級帶來的問題。</span><span class="sxs-lookup"><span data-stu-id="2f15a-188">These delays enable detecting issues introduced by the upgrade before the upgrade proceeds.</span></span> <span data-ttu-id="2f15a-189">缺點是可接受的，因為它會防止不良的變更一次影響到太多服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-189">The tradeoff is acceptable because it prevents bad changes from affecting too much of the service at a time.</span></span>

<span data-ttu-id="2f15a-190">升級網域太少有許多負面的副作用 - 當個別升級網域關閉來升級時，整體容量會有一大部分無法使用。</span><span class="sxs-lookup"><span data-stu-id="2f15a-190">Too few Upgrade Domains has many negative side effects – while each individual Upgrade Domain is down and being upgraded a large portion of your overall capacity is unavailable.</span></span> <span data-ttu-id="2f15a-191">例如，若您只有三個升級網域，則一次就關閉大約 1/3 的整體服務或叢集容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-191">For example, if you only have three Upgrade Domains you are taking down about 1/3 of your overall service or cluster capacity at a time.</span></span> <span data-ttu-id="2f15a-192">服務不宜一下子就關閉這麼多，因為叢集的剩餘部分必須有足夠容量來處理工作負載。</span><span class="sxs-lookup"><span data-stu-id="2f15a-192">Having so much of your service down at once isn’t desirable since you have to have enough capacity in the rest of your cluster to handle the workload.</span></span> <span data-ttu-id="2f15a-193">維護該緩衝區表示這些節點在一般作業期間的負載比其他期間少。</span><span class="sxs-lookup"><span data-stu-id="2f15a-193">Maintaining that buffer means that during normal operation those nodes are less loaded than they would be otherwise.</span></span> <span data-ttu-id="2f15a-194">這會增加執行服務的成本。</span><span class="sxs-lookup"><span data-stu-id="2f15a-194">This increases the cost of running your service.</span></span>

<span data-ttu-id="2f15a-195">環境中的容錯網域或升級網域總數沒有實際限制，它們的重疊方式也不受約束。</span><span class="sxs-lookup"><span data-stu-id="2f15a-195">There’s no real limit to the total number of fault or Upgrade Domains in an environment, or constraints on how they overlap.</span></span> <span data-ttu-id="2f15a-196">話雖如此，有幾個常見模式：</span><span class="sxs-lookup"><span data-stu-id="2f15a-196">That said, there are several common patterns:</span></span>

- <span data-ttu-id="2f15a-197">1:1 對應的容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-197">Fault Domains and Upgrade Domains mapped 1:1</span></span>
- <span data-ttu-id="2f15a-198">每個節點 (實體或虛擬作業系統執行個體) 一個升級網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-198">One Upgrade Domain per Node (physical or virtual OS instance)</span></span>
- <span data-ttu-id="2f15a-199">「等量」或「矩陣」模型，其中的容錯網域和升級網域形成一個矩陣，而電腦通常沿著對角線排列。</span><span class="sxs-lookup"><span data-stu-id="2f15a-199">A “striped” or “matrix” model where the Fault Domains and Upgrade Domains form a matrix with machines usually running down the diagonals</span></span>

<span data-ttu-id="2f15a-200"><center>
![容錯網域和升級網域配置][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-200"><center>
![Fault and Upgrade Domain Layouts][Image4]
</center></span></span>

<span data-ttu-id="2f15a-201">對於選擇哪個配置並沒有最佳答案，每個答案都各有優缺點。</span><span class="sxs-lookup"><span data-stu-id="2f15a-201">There’s no best answer which layout to choose, each has some pros and cons.</span></span> <span data-ttu-id="2f15a-202">例如，1FD:1UD 模型相當容易設定。</span><span class="sxs-lookup"><span data-stu-id="2f15a-202">For example, the 1FD:1UD model is simple to set up.</span></span> <span data-ttu-id="2f15a-203">每個節點 1 個升級網域模型，是使用者最常使用的模型。</span><span class="sxs-lookup"><span data-stu-id="2f15a-203">The 1 Upgrade Domain per Node model is most like what people are used to.</span></span> <span data-ttu-id="2f15a-204">在升級期間每個節點會獨立更新。</span><span class="sxs-lookup"><span data-stu-id="2f15a-204">During upgrades each node is updated independently.</span></span> <span data-ttu-id="2f15a-205">這類似於以往手動升級小型集合機器的方式。</span><span class="sxs-lookup"><span data-stu-id="2f15a-205">This is similar to how small sets of machines were upgraded manually in the past.</span></span> 

<span data-ttu-id="2f15a-206">最常見的模型是 FD/UD 矩陣，其中 FD 和 UD 形成一個表格，而節點沿著對角線開始放置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-206">The most common model is the FD/UD matrix, where the FDs and UDs form a table and nodes are placed starting along the diagonal.</span></span> <span data-ttu-id="2f15a-207">這是在 Azure 中的 Service Fabric 叢集預設使用的模型。</span><span class="sxs-lookup"><span data-stu-id="2f15a-207">This is the model used by default in Service Fabric clusters in Azure.</span></span> <span data-ttu-id="2f15a-208">對於具有許多節點的叢集，所有項目最後看起來就像是上述的密集矩陣模式。</span><span class="sxs-lookup"><span data-stu-id="2f15a-208">For clusters with many nodes everything ends up looking like the dense matrix pattern above.</span></span>

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a><span data-ttu-id="2f15a-209">容錯網域和升級網域的條件約束和導致的行為</span><span class="sxs-lookup"><span data-stu-id="2f15a-209">Fault and Upgrade Domain constraints and resulting behavior</span></span>
<span data-ttu-id="2f15a-210">為了讓服務在容錯網域和升級網域之間保持平衡，叢集資源管理員會將這種期望當成一種條件約束。</span><span class="sxs-lookup"><span data-stu-id="2f15a-210">The Cluster Resource Manager treats the desire to keep a service balanced across fault and Upgrade Domains as a constraint.</span></span> <span data-ttu-id="2f15a-211">您可以在 [這篇文章](service-fabric-cluster-resource-manager-management-integration.md)中深入了解條件約束。</span><span class="sxs-lookup"><span data-stu-id="2f15a-211">You can find out more about constraints in [this article](service-fabric-cluster-resource-manager-management-integration.md).</span></span> <span data-ttu-id="2f15a-212">容錯網域和升級網域的條件約束表示：「針對特定的服務資料分割，兩個網域之間的服務物件數目 (無狀態服務或具狀態服務副本) 差異決不能「大於一」。</span><span class="sxs-lookup"><span data-stu-id="2f15a-212">The Fault and Upgrade Domain constraints state: "For a given service partition there should never be a difference *greater than one* in the number of service objects (stateless service instances or stateful service replicas) between two domains."</span></span> <span data-ttu-id="2f15a-213">這可防止違反這個條件約束的特定移動或排列方式。</span><span class="sxs-lookup"><span data-stu-id="2f15a-213">This prevents certain moves or arrangements that violate this constraint.</span></span>

<span data-ttu-id="2f15a-214">讓我們來看看一個範例。</span><span class="sxs-lookup"><span data-stu-id="2f15a-214">Let's look at one example.</span></span> <span data-ttu-id="2f15a-215">假設我們的叢集有六個節點，且已設定五個容錯網域和五個升級網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-215">Let's say that we have a cluster with six nodes, configured with five Fault Domains and five Upgrade Domains.</span></span>

|  | <span data-ttu-id="2f15a-216">FD0</span><span class="sxs-lookup"><span data-stu-id="2f15a-216">FD0</span></span> | <span data-ttu-id="2f15a-217">FD1</span><span class="sxs-lookup"><span data-stu-id="2f15a-217">FD1</span></span> | <span data-ttu-id="2f15a-218">FD2</span><span class="sxs-lookup"><span data-stu-id="2f15a-218">FD2</span></span> | <span data-ttu-id="2f15a-219">FD3</span><span class="sxs-lookup"><span data-stu-id="2f15a-219">FD3</span></span> | <span data-ttu-id="2f15a-220">FD4</span><span class="sxs-lookup"><span data-stu-id="2f15a-220">FD4</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2f15a-221">**UD0**</span><span class="sxs-lookup"><span data-stu-id="2f15a-221">**UD0**</span></span> |<span data-ttu-id="2f15a-222">N1</span><span class="sxs-lookup"><span data-stu-id="2f15a-222">N1</span></span> | | | | |
| <span data-ttu-id="2f15a-223">**UD1**</span><span class="sxs-lookup"><span data-stu-id="2f15a-223">**UD1**</span></span> |<span data-ttu-id="2f15a-224">N6</span><span class="sxs-lookup"><span data-stu-id="2f15a-224">N6</span></span> |<span data-ttu-id="2f15a-225">N2</span><span class="sxs-lookup"><span data-stu-id="2f15a-225">N2</span></span> | | | |
| <span data-ttu-id="2f15a-226">**UD2**</span><span class="sxs-lookup"><span data-stu-id="2f15a-226">**UD2**</span></span> | | |<span data-ttu-id="2f15a-227">N3</span><span class="sxs-lookup"><span data-stu-id="2f15a-227">N3</span></span> | | |
| <span data-ttu-id="2f15a-228">**UD3**</span><span class="sxs-lookup"><span data-stu-id="2f15a-228">**UD3**</span></span> | | | |<span data-ttu-id="2f15a-229">N4</span><span class="sxs-lookup"><span data-stu-id="2f15a-229">N4</span></span> | |
| <span data-ttu-id="2f15a-230">**UD4**</span><span class="sxs-lookup"><span data-stu-id="2f15a-230">**UD4**</span></span> | | | | |<span data-ttu-id="2f15a-231">N5</span><span class="sxs-lookup"><span data-stu-id="2f15a-231">N5</span></span> |

<span data-ttu-id="2f15a-232">現在假設我們建立 TargetReplicaSetSize (或者對於無狀態服務是 InstanceCount) 為五的服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-232">Now let's say that we create a service with a TargetReplicaSetSize (or, for a stateless service an InstanceCount) of five.</span></span> <span data-ttu-id="2f15a-233">複本將會落在 N1-N5 上。</span><span class="sxs-lookup"><span data-stu-id="2f15a-233">The replicas land on N1-N5.</span></span> <span data-ttu-id="2f15a-234">事實上，不論建立多少像這樣的服務，都不會用到 N6。</span><span class="sxs-lookup"><span data-stu-id="2f15a-234">In fact, N6 is never used no matter how many services like this you create.</span></span> <span data-ttu-id="2f15a-235">原因為何？</span><span class="sxs-lookup"><span data-stu-id="2f15a-235">But why?</span></span> <span data-ttu-id="2f15a-236">讓我們看看目前的配置和選擇 N6 時情況如何之間的差異。</span><span class="sxs-lookup"><span data-stu-id="2f15a-236">Let's look at the difference between the current layout and what would happen if N6 is chosen.</span></span>

<span data-ttu-id="2f15a-237">以下是我們的配置，以及每個容錯網域和升級網域的複本總數。</span><span class="sxs-lookup"><span data-stu-id="2f15a-237">Here's the layout we got and the total number of replicas per Fault and Upgrade Domain:</span></span>

|  | <span data-ttu-id="2f15a-238">FD0</span><span class="sxs-lookup"><span data-stu-id="2f15a-238">FD0</span></span> | <span data-ttu-id="2f15a-239">FD1</span><span class="sxs-lookup"><span data-stu-id="2f15a-239">FD1</span></span> | <span data-ttu-id="2f15a-240">FD2</span><span class="sxs-lookup"><span data-stu-id="2f15a-240">FD2</span></span> | <span data-ttu-id="2f15a-241">FD3</span><span class="sxs-lookup"><span data-stu-id="2f15a-241">FD3</span></span> | <span data-ttu-id="2f15a-242">FD4</span><span class="sxs-lookup"><span data-stu-id="2f15a-242">FD4</span></span> | <span data-ttu-id="2f15a-243">UDTotal</span><span class="sxs-lookup"><span data-stu-id="2f15a-243">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2f15a-244">**UD0**</span><span class="sxs-lookup"><span data-stu-id="2f15a-244">**UD0**</span></span> |<span data-ttu-id="2f15a-245">R1</span><span class="sxs-lookup"><span data-stu-id="2f15a-245">R1</span></span> | | | | |<span data-ttu-id="2f15a-246">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-246">1</span></span> |
| <span data-ttu-id="2f15a-247">**UD1**</span><span class="sxs-lookup"><span data-stu-id="2f15a-247">**UD1**</span></span> | |<span data-ttu-id="2f15a-248">R2</span><span class="sxs-lookup"><span data-stu-id="2f15a-248">R2</span></span> | | | |<span data-ttu-id="2f15a-249">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-249">1</span></span> |
| <span data-ttu-id="2f15a-250">**UD2**</span><span class="sxs-lookup"><span data-stu-id="2f15a-250">**UD2**</span></span> | | |<span data-ttu-id="2f15a-251">R3</span><span class="sxs-lookup"><span data-stu-id="2f15a-251">R3</span></span> | | |<span data-ttu-id="2f15a-252">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-252">1</span></span> |
| <span data-ttu-id="2f15a-253">**UD3**</span><span class="sxs-lookup"><span data-stu-id="2f15a-253">**UD3**</span></span> | | | |<span data-ttu-id="2f15a-254">R4</span><span class="sxs-lookup"><span data-stu-id="2f15a-254">R4</span></span> | |<span data-ttu-id="2f15a-255">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-255">1</span></span> |
| <span data-ttu-id="2f15a-256">**UD4**</span><span class="sxs-lookup"><span data-stu-id="2f15a-256">**UD4**</span></span> | | | | |<span data-ttu-id="2f15a-257">R5</span><span class="sxs-lookup"><span data-stu-id="2f15a-257">R5</span></span> |<span data-ttu-id="2f15a-258">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-258">1</span></span> |
| <span data-ttu-id="2f15a-259">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="2f15a-259">**FDTotal**</span></span> |<span data-ttu-id="2f15a-260">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-260">1</span></span> |<span data-ttu-id="2f15a-261">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-261">1</span></span> |<span data-ttu-id="2f15a-262">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-262">1</span></span> |<span data-ttu-id="2f15a-263">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-263">1</span></span> |<span data-ttu-id="2f15a-264">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-264">1</span></span> |- |

<span data-ttu-id="2f15a-265">就每個容錯網域和升級網域的節點數而論，在此配置達到平衡。</span><span class="sxs-lookup"><span data-stu-id="2f15a-265">This layout is balanced in terms of nodes per Fault Domain and Upgrade Domain.</span></span> <span data-ttu-id="2f15a-266">在每個容錯網域和升級網域的複本數目方面也達到平衡。</span><span class="sxs-lookup"><span data-stu-id="2f15a-266">It is also balanced in terms of the number of replicas per Fault and Upgrade Domain.</span></span> <span data-ttu-id="2f15a-267">每個網域都擁有相同數量的節點，以及相同數量的複本。</span><span class="sxs-lookup"><span data-stu-id="2f15a-267">Each domain has the same number of nodes and the same number of replicas.</span></span>

<span data-ttu-id="2f15a-268">現在，讓我們看看改用 N6 而不使用 N2 的情況。</span><span class="sxs-lookup"><span data-stu-id="2f15a-268">Now, let's look at what would happen if we'd used N6 instead of N2.</span></span> <span data-ttu-id="2f15a-269">複本將會如何散佈？</span><span class="sxs-lookup"><span data-stu-id="2f15a-269">How would the replicas be distributed then?</span></span>

|  | <span data-ttu-id="2f15a-270">FD0</span><span class="sxs-lookup"><span data-stu-id="2f15a-270">FD0</span></span> | <span data-ttu-id="2f15a-271">FD1</span><span class="sxs-lookup"><span data-stu-id="2f15a-271">FD1</span></span> | <span data-ttu-id="2f15a-272">FD2</span><span class="sxs-lookup"><span data-stu-id="2f15a-272">FD2</span></span> | <span data-ttu-id="2f15a-273">FD3</span><span class="sxs-lookup"><span data-stu-id="2f15a-273">FD3</span></span> | <span data-ttu-id="2f15a-274">FD4</span><span class="sxs-lookup"><span data-stu-id="2f15a-274">FD4</span></span> | <span data-ttu-id="2f15a-275">UDTotal</span><span class="sxs-lookup"><span data-stu-id="2f15a-275">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2f15a-276">**UD0**</span><span class="sxs-lookup"><span data-stu-id="2f15a-276">**UD0**</span></span> |<span data-ttu-id="2f15a-277">R1</span><span class="sxs-lookup"><span data-stu-id="2f15a-277">R1</span></span> | | | | |<span data-ttu-id="2f15a-278">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-278">1</span></span> |
| <span data-ttu-id="2f15a-279">**UD1**</span><span class="sxs-lookup"><span data-stu-id="2f15a-279">**UD1**</span></span> |<span data-ttu-id="2f15a-280">R5</span><span class="sxs-lookup"><span data-stu-id="2f15a-280">R5</span></span> | | | | |<span data-ttu-id="2f15a-281">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-281">1</span></span> |
| <span data-ttu-id="2f15a-282">**UD2**</span><span class="sxs-lookup"><span data-stu-id="2f15a-282">**UD2**</span></span> | | |<span data-ttu-id="2f15a-283">R2</span><span class="sxs-lookup"><span data-stu-id="2f15a-283">R2</span></span> | | |<span data-ttu-id="2f15a-284">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-284">1</span></span> |
| <span data-ttu-id="2f15a-285">**UD3**</span><span class="sxs-lookup"><span data-stu-id="2f15a-285">**UD3**</span></span> | | | |<span data-ttu-id="2f15a-286">R3</span><span class="sxs-lookup"><span data-stu-id="2f15a-286">R3</span></span> | |<span data-ttu-id="2f15a-287">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-287">1</span></span> |
| <span data-ttu-id="2f15a-288">**UD4**</span><span class="sxs-lookup"><span data-stu-id="2f15a-288">**UD4**</span></span> | | | | |<span data-ttu-id="2f15a-289">R4</span><span class="sxs-lookup"><span data-stu-id="2f15a-289">R4</span></span> |<span data-ttu-id="2f15a-290">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-290">1</span></span> |
| <span data-ttu-id="2f15a-291">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="2f15a-291">**FDTotal**</span></span> |<span data-ttu-id="2f15a-292">2</span><span class="sxs-lookup"><span data-stu-id="2f15a-292">2</span></span> |<span data-ttu-id="2f15a-293">0</span><span class="sxs-lookup"><span data-stu-id="2f15a-293">0</span></span> |<span data-ttu-id="2f15a-294">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-294">1</span></span> |<span data-ttu-id="2f15a-295">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-295">1</span></span> |<span data-ttu-id="2f15a-296">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-296">1</span></span> |- |

<span data-ttu-id="2f15a-297">此配置違反容錯網域條件約束的定義。</span><span class="sxs-lookup"><span data-stu-id="2f15a-297">This layout violates our definition for the Fault Domain constraint.</span></span> <span data-ttu-id="2f15a-298">FD0 有兩個複本，FD1 沒有複本，所以 FD0 和 FD1 之間的差異合計為 2。</span><span class="sxs-lookup"><span data-stu-id="2f15a-298">FD0 has two replicas, while FD1 has zero, making the difference between FD0 and FD1 a total of two.</span></span> <span data-ttu-id="2f15a-299">叢集資源管理員不允許這種安排。</span><span class="sxs-lookup"><span data-stu-id="2f15a-299">The Cluster Resource Manager does not allow this arrangement.</span></span> <span data-ttu-id="2f15a-300">同樣地，如果挑選 N2 和 N6 (而不是 N1 和 N2)，則會得到：</span><span class="sxs-lookup"><span data-stu-id="2f15a-300">Similarly if we picked N2 and N6 (instead of N1 and N2) we'd get:</span></span>

|  | <span data-ttu-id="2f15a-301">FD0</span><span class="sxs-lookup"><span data-stu-id="2f15a-301">FD0</span></span> | <span data-ttu-id="2f15a-302">FD1</span><span class="sxs-lookup"><span data-stu-id="2f15a-302">FD1</span></span> | <span data-ttu-id="2f15a-303">FD2</span><span class="sxs-lookup"><span data-stu-id="2f15a-303">FD2</span></span> | <span data-ttu-id="2f15a-304">FD3</span><span class="sxs-lookup"><span data-stu-id="2f15a-304">FD3</span></span> | <span data-ttu-id="2f15a-305">FD4</span><span class="sxs-lookup"><span data-stu-id="2f15a-305">FD4</span></span> | <span data-ttu-id="2f15a-306">UDTotal</span><span class="sxs-lookup"><span data-stu-id="2f15a-306">UDTotal</span></span> |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| <span data-ttu-id="2f15a-307">**UD0**</span><span class="sxs-lookup"><span data-stu-id="2f15a-307">**UD0**</span></span> | | | | | |<span data-ttu-id="2f15a-308">0</span><span class="sxs-lookup"><span data-stu-id="2f15a-308">0</span></span> |
| <span data-ttu-id="2f15a-309">**UD1**</span><span class="sxs-lookup"><span data-stu-id="2f15a-309">**UD1**</span></span> |<span data-ttu-id="2f15a-310">R5</span><span class="sxs-lookup"><span data-stu-id="2f15a-310">R5</span></span> |<span data-ttu-id="2f15a-311">R1</span><span class="sxs-lookup"><span data-stu-id="2f15a-311">R1</span></span> | | | |<span data-ttu-id="2f15a-312">2</span><span class="sxs-lookup"><span data-stu-id="2f15a-312">2</span></span> |
| <span data-ttu-id="2f15a-313">**UD2**</span><span class="sxs-lookup"><span data-stu-id="2f15a-313">**UD2**</span></span> | | |<span data-ttu-id="2f15a-314">R2</span><span class="sxs-lookup"><span data-stu-id="2f15a-314">R2</span></span> | | |<span data-ttu-id="2f15a-315">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-315">1</span></span> |
| <span data-ttu-id="2f15a-316">**UD3**</span><span class="sxs-lookup"><span data-stu-id="2f15a-316">**UD3**</span></span> | | | |<span data-ttu-id="2f15a-317">R3</span><span class="sxs-lookup"><span data-stu-id="2f15a-317">R3</span></span> | |<span data-ttu-id="2f15a-318">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-318">1</span></span> |
| <span data-ttu-id="2f15a-319">**UD4**</span><span class="sxs-lookup"><span data-stu-id="2f15a-319">**UD4**</span></span> | | | | |<span data-ttu-id="2f15a-320">R4</span><span class="sxs-lookup"><span data-stu-id="2f15a-320">R4</span></span> |<span data-ttu-id="2f15a-321">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-321">1</span></span> |
| <span data-ttu-id="2f15a-322">**FDTotal**</span><span class="sxs-lookup"><span data-stu-id="2f15a-322">**FDTotal**</span></span> |<span data-ttu-id="2f15a-323">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-323">1</span></span> |<span data-ttu-id="2f15a-324">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-324">1</span></span> |<span data-ttu-id="2f15a-325">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-325">1</span></span> |<span data-ttu-id="2f15a-326">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-326">1</span></span> |<span data-ttu-id="2f15a-327">1</span><span class="sxs-lookup"><span data-stu-id="2f15a-327">1</span></span> |- |

<span data-ttu-id="2f15a-328">此配置就容錯網域而言是平衡的。</span><span class="sxs-lookup"><span data-stu-id="2f15a-328">This layout is balanced in terms of Fault Domains.</span></span> <span data-ttu-id="2f15a-329">不過，現在它會違反升級網域條件約束。</span><span class="sxs-lookup"><span data-stu-id="2f15a-329">However, now it's violating the Upgrade Domain constraint.</span></span> <span data-ttu-id="2f15a-330">這是因為 UD0 有零個複本，而 UD1 有兩個複本。</span><span class="sxs-lookup"><span data-stu-id="2f15a-330">This is because UD0 has zero replicas while UD1 has two.</span></span> <span data-ttu-id="2f15a-331">因此，此配置也無效，而且不會被叢集資源管理員挑選。</span><span class="sxs-lookup"><span data-stu-id="2f15a-331">Therefore, this layout is also invalid and won't be picked by the Cluster Resource Manager.</span></span> 

## <a name="configuring-fault-and-upgrade-domains"></a><span data-ttu-id="2f15a-332">設定容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="2f15a-332">Configuring fault and Upgrade Domains</span></span>
<span data-ttu-id="2f15a-333">Azure 託管的 Service Fabric 部署中會自動定義容錯網域和升級網域。</span><span class="sxs-lookup"><span data-stu-id="2f15a-333">Defining Fault Domains and Upgrade Domains is done automatically in Azure hosted Service Fabric deployments.</span></span> <span data-ttu-id="2f15a-334">Service Fabric 會從 Azure 中取用環境資訊。</span><span class="sxs-lookup"><span data-stu-id="2f15a-334">Service Fabric picks up and uses the environment information from Azure.</span></span>

<span data-ttu-id="2f15a-335">如果想要建立您自己的叢集 (或想要在開發環境中執行特定拓撲)，您可以自行提供容錯網域和升級網域資訊。</span><span class="sxs-lookup"><span data-stu-id="2f15a-335">If you’re creating your own cluster (or want to run a particular topology in development), you can provide the Fault Domain and Upgrade Domain information yourself.</span></span> <span data-ttu-id="2f15a-336">在此範例中，我們定義本機開發叢集，具有九個節點，且跨越三個「資料中心」(各有三個機架)。</span><span class="sxs-lookup"><span data-stu-id="2f15a-336">In this example, we define a nine node local development cluster that spans three “datacenters” (each with three racks).</span></span> <span data-ttu-id="2f15a-337">此叢集也有三個升級網域等量分散於這些三個資料中心。</span><span class="sxs-lookup"><span data-stu-id="2f15a-337">This cluster also has three Upgrade Domains striped across those three datacenters.</span></span> <span data-ttu-id="2f15a-338">設定的範例如下：</span><span class="sxs-lookup"><span data-stu-id="2f15a-338">An example of the configuration is below:</span></span> 

<span data-ttu-id="2f15a-339">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="2f15a-339">ClusterManifest.xml</span></span>

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

<span data-ttu-id="2f15a-340">獨立部署透過 ClusterConfig.json</span><span class="sxs-lookup"><span data-stu-id="2f15a-340">via ClusterConfig.json for Standalone deployments</span></span>

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
> <span data-ttu-id="2f15a-341">透過 Azure Resource Manager 定義叢集時，容錯網域和升級網域會由 Azure 指派。</span><span class="sxs-lookup"><span data-stu-id="2f15a-341">When defining clusters via Azure Resource Manager, Fault Domains and Upgrade Domains are assigned by Azure.</span></span> <span data-ttu-id="2f15a-342">因此，Azure Resource Manager 範本中的節點類型和虛擬機器擴展集定義不包含容錯網域或升級網域資訊。</span><span class="sxs-lookup"><span data-stu-id="2f15a-342">Therefore, the definition of your Node Types and Virtual Machine Scale Sets in your Azure Resource Manager template does not include Fault Domain or Upgrade Domain information.</span></span>
>

## <a name="node-properties-and-placement-constraints"></a><span data-ttu-id="2f15a-343">節點屬性和放置條件約束</span><span class="sxs-lookup"><span data-stu-id="2f15a-343">Node properties and placement constraints</span></span>
<span data-ttu-id="2f15a-344">有時候 (事實上是大部分的情況下) 您會想要確保工作負載只在叢集中的特定節點類型上執行。</span><span class="sxs-lookup"><span data-stu-id="2f15a-344">Sometimes (in fact, most of the time) you’re going to want to ensure that certain workloads run only on certain types of nodes in the cluster.</span></span> <span data-ttu-id="2f15a-345">例如，某些工作負載可能需要 GPU 或 SSD，而有些則不用。</span><span class="sxs-lookup"><span data-stu-id="2f15a-345">For example, some workload may require GPUs or SSDs while others may not.</span></span> <span data-ttu-id="2f15a-346">將硬體專用於特定工作負載的最佳例子幾乎都是多層式架構。</span><span class="sxs-lookup"><span data-stu-id="2f15a-346">A great example of targeting hardware to particular workloads is almost every n-tier architecture out there.</span></span> <span data-ttu-id="2f15a-347">特定電腦作為應用程式的前端或 API 供應端，並且公開至用戶端或網際網路。</span><span class="sxs-lookup"><span data-stu-id="2f15a-347">Certain machines serve as the front end or API serving side of the application and are exposed to the clients or the internet.</span></span> <span data-ttu-id="2f15a-348">其他電腦 (通常有不同的硬體資源) 處理計算層或儲存層的工作。</span><span class="sxs-lookup"><span data-stu-id="2f15a-348">Different machines, often with different hardware resources, handle the work of the compute or storage layers.</span></span> <span data-ttu-id="2f15a-349">它們通常_不會_直接公開至用戶端或網際網路。</span><span class="sxs-lookup"><span data-stu-id="2f15a-349">These are usually _not_ directly exposed to clients or the internet.</span></span> <span data-ttu-id="2f15a-350">Service Fabric 認為特定的工作負載有時需要在特定硬體設定上執行。</span><span class="sxs-lookup"><span data-stu-id="2f15a-350">Service Fabric expects that there are cases where particular workloads need to run on particular hardware configurations.</span></span> <span data-ttu-id="2f15a-351">例如：</span><span class="sxs-lookup"><span data-stu-id="2f15a-351">For example:</span></span>

* <span data-ttu-id="2f15a-352">現有的多層式架構應用程式已「提升並移轉」到 Service Fabric 環境</span><span class="sxs-lookup"><span data-stu-id="2f15a-352">an existing n-tier application has been “lifted and shifted” into a Service Fabric environment</span></span>
* <span data-ttu-id="2f15a-353">針對效能、級別或安全性隔離原因而想要在特定硬體上執行的工作負載</span><span class="sxs-lookup"><span data-stu-id="2f15a-353">a workload wants to run on specific hardware for performance, scale, or security isolation reasons</span></span>
* <span data-ttu-id="2f15a-354">基於原則或資源耗用量的理由，工作負載應該彼此隔離</span><span class="sxs-lookup"><span data-stu-id="2f15a-354">A workload should be isolated from other workloads for policy or resource consumption reasons</span></span>

<span data-ttu-id="2f15a-355">為了支援這種設定，Service Fabric 有一流的標籤概念可運用在節點上。</span><span class="sxs-lookup"><span data-stu-id="2f15a-355">To support these sorts of configurations, Service Fabric has a first class notion of tags that can be applied to nodes.</span></span> <span data-ttu-id="2f15a-356">這些標記稱為**節點屬性**。</span><span class="sxs-lookup"><span data-stu-id="2f15a-356">These tags are called **node properties**.</span></span> <span data-ttu-id="2f15a-357">**條件約束**是陳述式，會附加至針對一或多個節點屬性選取的個別服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-357">**Placement constraints** are the statements attached to individual services that select for one or more node properties.</span></span> <span data-ttu-id="2f15a-358">放置條件約束會定義應該執行服務的位置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-358">Placement constraints define where services should run.</span></span> <span data-ttu-id="2f15a-359">條件約束集可延伸 - 任何索引鍵/值組都沒問題。</span><span class="sxs-lookup"><span data-stu-id="2f15a-359">The set of constraints is extensible - any key/value pair can work.</span></span> 

<span data-ttu-id="2f15a-360"><center>
![叢集配置不同工作負載][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-360"><center>
![Cluster Layout Different Workloads][Image5]
</center></span></span>

### <a name="built-in-node-properties"></a><span data-ttu-id="2f15a-361">內建節點屬性</span><span class="sxs-lookup"><span data-stu-id="2f15a-361">Built in node properties</span></span>
<span data-ttu-id="2f15a-362">Service Fabric 定義一些預設節點屬性，可自動使用，而不需要由使用者定義。</span><span class="sxs-lookup"><span data-stu-id="2f15a-362">Service Fabric defines some default node properties that can be used automatically without the user having to define them.</span></span> <span data-ttu-id="2f15a-363">每個節點上定義的預設屬性是 **NodeType** 和 **NodeName**。</span><span class="sxs-lookup"><span data-stu-id="2f15a-363">The default properties defined at each node are the **NodeType** and the **NodeName**.</span></span> <span data-ttu-id="2f15a-364">例如，您可以將放置條件約束撰寫成 `"(NodeType == NodeType03)"`。</span><span class="sxs-lookup"><span data-stu-id="2f15a-364">So for example you could write a placement constraint as `"(NodeType == NodeType03)"`.</span></span> <span data-ttu-id="2f15a-365">我們大致上發現 NodeType 是其中一個最常用的屬性。</span><span class="sxs-lookup"><span data-stu-id="2f15a-365">Generally we have found NodeType to be one of the most commonly used properties.</span></span> <span data-ttu-id="2f15a-366">因為它與機器類型的對應是 1:1，所以很有用。</span><span class="sxs-lookup"><span data-stu-id="2f15a-366">It is useful since it corresponds 1:1 with a type of a machine.</span></span> <span data-ttu-id="2f15a-367">每個機器類型都對應至傳統多層式架構應用程式中的工作負載類型。</span><span class="sxs-lookup"><span data-stu-id="2f15a-367">Each type of machine corresponds to a type of workload in a traditional n-tier application.</span></span>

<span data-ttu-id="2f15a-368"><center>
![放置條件約束和節點屬性][Image6]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-368"><center>
![Placement Constraints and Node Properties][Image6]
</center></span></span>

## <a name="placement-constraint-and-node-property-syntax"></a><span data-ttu-id="2f15a-369">放置條件約束和節點屬性語法</span><span class="sxs-lookup"><span data-stu-id="2f15a-369">Placement Constraint and Node Property Syntax</span></span> 
<span data-ttu-id="2f15a-370">節點屬性中指定的值可以是字串、bool，或帶正負號長值。</span><span class="sxs-lookup"><span data-stu-id="2f15a-370">The value specified in the node property can be a string, bool, or signed long.</span></span> <span data-ttu-id="2f15a-371">服務的陳述式稱為放置「條件約束」，因為它會限制服務在叢集中可執行的位置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-371">The statement at the service is called a placement *constraint* since it constrains where the service can run in the cluster.</span></span> <span data-ttu-id="2f15a-372">條件約束可以是任何在叢集中於不同節點上運作的布林值陳述式。</span><span class="sxs-lookup"><span data-stu-id="2f15a-372">The constraint can be any Boolean statement that operates on the different node properties in the cluster.</span></span> <span data-ttu-id="2f15a-373">這些布林值陳述式中的有效選取器如下：</span><span class="sxs-lookup"><span data-stu-id="2f15a-373">The valid selectors in these boolean statements are:</span></span>

1) <span data-ttu-id="2f15a-374">建立特定陳述式的條件式檢查</span><span class="sxs-lookup"><span data-stu-id="2f15a-374">conditional checks for creating particular statements</span></span>

| <span data-ttu-id="2f15a-375">陳述式</span><span class="sxs-lookup"><span data-stu-id="2f15a-375">Statement</span></span> | <span data-ttu-id="2f15a-376">語法</span><span class="sxs-lookup"><span data-stu-id="2f15a-376">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="2f15a-377">「等於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-377">"equal to"</span></span> | <span data-ttu-id="2f15a-378">"=="</span><span class="sxs-lookup"><span data-stu-id="2f15a-378">"=="</span></span> |
| <span data-ttu-id="2f15a-379">「不等於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-379">"not equal to"</span></span> | <span data-ttu-id="2f15a-380">"!="</span><span class="sxs-lookup"><span data-stu-id="2f15a-380">"!="</span></span> |
| <span data-ttu-id="2f15a-381">「大於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-381">"greater than"</span></span> | <span data-ttu-id="2f15a-382">">"</span><span class="sxs-lookup"><span data-stu-id="2f15a-382">">"</span></span> |
| <span data-ttu-id="2f15a-383">「大於或等於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-383">"greater than or equal to"</span></span> | <span data-ttu-id="2f15a-384">">="</span><span class="sxs-lookup"><span data-stu-id="2f15a-384">">="</span></span> |
| <span data-ttu-id="2f15a-385">「小於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-385">"less than"</span></span> | <span data-ttu-id="2f15a-386">"<"</span><span class="sxs-lookup"><span data-stu-id="2f15a-386">"<"</span></span> |
| <span data-ttu-id="2f15a-387">「小於或等於」</span><span class="sxs-lookup"><span data-stu-id="2f15a-387">"less than or equal to"</span></span> | <span data-ttu-id="2f15a-388">"<="</span><span class="sxs-lookup"><span data-stu-id="2f15a-388">"<="</span></span> |

2) <span data-ttu-id="2f15a-389">分組和邏輯運算的布林值陳述式</span><span class="sxs-lookup"><span data-stu-id="2f15a-389">boolean statements for grouping and logical operations</span></span>

| <span data-ttu-id="2f15a-390">陳述式</span><span class="sxs-lookup"><span data-stu-id="2f15a-390">Statement</span></span> | <span data-ttu-id="2f15a-391">語法</span><span class="sxs-lookup"><span data-stu-id="2f15a-391">Syntax</span></span> |
| --- |:---:|
| <span data-ttu-id="2f15a-392">「和」</span><span class="sxs-lookup"><span data-stu-id="2f15a-392">"and"</span></span> | <span data-ttu-id="2f15a-393">"&&"</span><span class="sxs-lookup"><span data-stu-id="2f15a-393">"&&"</span></span> |
| <span data-ttu-id="2f15a-394">「或」</span><span class="sxs-lookup"><span data-stu-id="2f15a-394">"or"</span></span> | <span data-ttu-id="2f15a-395">"&#124;&#124;"</span><span class="sxs-lookup"><span data-stu-id="2f15a-395">"&#124;&#124;"</span></span> |
| <span data-ttu-id="2f15a-396">「否」</span><span class="sxs-lookup"><span data-stu-id="2f15a-396">"not"</span></span> | <span data-ttu-id="2f15a-397">"!"</span><span class="sxs-lookup"><span data-stu-id="2f15a-397">"!"</span></span> |
| <span data-ttu-id="2f15a-398">「組成單一陳述式」</span><span class="sxs-lookup"><span data-stu-id="2f15a-398">"group as single statement"</span></span> | <span data-ttu-id="2f15a-399">"()"</span><span class="sxs-lookup"><span data-stu-id="2f15a-399">"()"</span></span> |

<span data-ttu-id="2f15a-400">以下是基本條件約束陳述式的一些範例。</span><span class="sxs-lookup"><span data-stu-id="2f15a-400">Here are some examples of basic constraint statements.</span></span>

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

<span data-ttu-id="2f15a-401">服務只能放置在整體放置條件約束陳述式評估為 "True" 的節點上。</span><span class="sxs-lookup"><span data-stu-id="2f15a-401">Only nodes where the overall placement constraint statement evaluates to “True” can have the service placed on it.</span></span> <span data-ttu-id="2f15a-402">未定義屬性的節點不符合包含該屬性的任何放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="2f15a-402">Nodes that do not have a property defined do not match any placement constraint containing that property.</span></span>

<span data-ttu-id="2f15a-403">假設某個節點類型已定義下列節點屬性︰</span><span class="sxs-lookup"><span data-stu-id="2f15a-403">Let’s say that the following node properties were defined for a given node type:</span></span>

<span data-ttu-id="2f15a-404">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="2f15a-404">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

<span data-ttu-id="2f15a-405">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。</span><span class="sxs-lookup"><span data-stu-id="2f15a-405">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

> [!NOTE]
> <span data-ttu-id="2f15a-406">在您的 Azure Resource Manager 範本中，節點類型通常已參數化。</span><span class="sxs-lookup"><span data-stu-id="2f15a-406">In your Azure Resource Manager template the node type is usually parameterized.</span></span> <span data-ttu-id="2f15a-407">它看起來會是 "[parameters('vmNodeType1Name')]"，而不是 "NodeType01"。</span><span class="sxs-lookup"><span data-stu-id="2f15a-407">It would look like "[parameters('vmNodeType1Name')]" rather than "NodeType01".</span></span>
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

<span data-ttu-id="2f15a-408">您可以針對服務建立服務放置「條件約束」，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="2f15a-408">You can create service placement *constraints* for a service like as follows:</span></span>

<span data-ttu-id="2f15a-409">C#</span><span class="sxs-lookup"><span data-stu-id="2f15a-409">C#</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="2f15a-410">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="2f15a-410">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

<span data-ttu-id="2f15a-411">如果 NodeType01 的所有節點都是有效的，您也可以使用條件約束 "(NodeType == NodeType01)" 選取該節點類型。</span><span class="sxs-lookup"><span data-stu-id="2f15a-411">If all nodes of NodeType01 are valid, you can also select that node type with the constraint "(NodeType == NodeType01)".</span></span>

<span data-ttu-id="2f15a-412">服務放置條件約束其中很棒的一點是它們可以在執行階段動態更新。</span><span class="sxs-lookup"><span data-stu-id="2f15a-412">One of the cool things about a service’s placement constraints is that they can be updated dynamically during runtime.</span></span> <span data-ttu-id="2f15a-413">所以如果您需要，可以在叢集中移動服務、加入和移除需求等等。Service Fabric 會負責確保服務保持執行且可用，即使進行這類變更。</span><span class="sxs-lookup"><span data-stu-id="2f15a-413">So if you need to, you can move a service around in the cluster, add and remove requirements, etc. Service Fabric takes care of ensuring that the service stays up and available even when these types of changes are made.</span></span>

<span data-ttu-id="2f15a-414">C#：</span><span class="sxs-lookup"><span data-stu-id="2f15a-414">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

<span data-ttu-id="2f15a-415">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="2f15a-415">Powershell:</span></span>

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

<span data-ttu-id="2f15a-416">放置條件約束會針對每個不同的具名服務執行個體指定。</span><span class="sxs-lookup"><span data-stu-id="2f15a-416">Placement constraints are specified for every different named service instance.</span></span> <span data-ttu-id="2f15a-417">更新一律會取代 (覆寫) 先前指定的項目。</span><span class="sxs-lookup"><span data-stu-id="2f15a-417">Updates always take the place of (overwrite) what was previously specified.</span></span>

<span data-ttu-id="2f15a-418">叢集定義會定義節點上的屬性。</span><span class="sxs-lookup"><span data-stu-id="2f15a-418">The cluster definition defines the properties on a node.</span></span> <span data-ttu-id="2f15a-419">變更節點的屬性需要叢集設定升級。</span><span class="sxs-lookup"><span data-stu-id="2f15a-419">Changing a node's properties requires a cluster configuration upgrade.</span></span> <span data-ttu-id="2f15a-420">升級節點的屬性需要每個受影響的節點重新啟動，以報告其新的屬性。</span><span class="sxs-lookup"><span data-stu-id="2f15a-420">Upgrading a node's properties requires each affected node to restart to report its new properties.</span></span> <span data-ttu-id="2f15a-421">這些輪流升級是由 Service Fabric 管理。</span><span class="sxs-lookup"><span data-stu-id="2f15a-421">These rolling upgrades are managed by Service Fabric.</span></span>

## <a name="describing-and-managing-cluster-resources"></a><span data-ttu-id="2f15a-422">描述與管理叢集資源</span><span class="sxs-lookup"><span data-stu-id="2f15a-422">Describing and Managing Cluster Resources</span></span>
<span data-ttu-id="2f15a-423">任何 Orchestrator 的其中一個最重要的作業是協助管理叢集中的資源耗用量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-423">One of the most important jobs of any orchestrator is to help manage resource consumption in the cluster.</span></span> <span data-ttu-id="2f15a-424">管理叢集資源可以表示幾個不同的項目。</span><span class="sxs-lookup"><span data-stu-id="2f15a-424">Managing cluster resources can mean a couple of different things.</span></span> <span data-ttu-id="2f15a-425">首先，確保電腦不會多載。</span><span class="sxs-lookup"><span data-stu-id="2f15a-425">First, there's ensuring that machines are not overloaded.</span></span> <span data-ttu-id="2f15a-426">這表示確定電腦不會執行比它們能夠處理還多的服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-426">This means making sure that machines aren't running more services than they can handle.</span></span> <span data-ttu-id="2f15a-427">第二，平衡和最佳化，對於有效率地執行服務很重要。</span><span class="sxs-lookup"><span data-stu-id="2f15a-427">Second, there's balancing and optimization which is critical to running services efficiently.</span></span> <span data-ttu-id="2f15a-428">符合成本效益或效能的敏感服務供應項目不允許某些節點忙碌，而其他節點閒置。</span><span class="sxs-lookup"><span data-stu-id="2f15a-428">Cost effective or performance sensitive service offerings can't allow some nodes to be hot while others are cold.</span></span> <span data-ttu-id="2f15a-429">忙碌節點會導致資源爭用和效能不佳，而閒置節點代表浪費資源和增加成本。</span><span class="sxs-lookup"><span data-stu-id="2f15a-429">Hot nodes lead to resource contention and poor performance, and cold nodes represent wasted resources and increased costs.</span></span> 

<span data-ttu-id="2f15a-430">Service Fabric 以 `Metrics` 表示資源。</span><span class="sxs-lookup"><span data-stu-id="2f15a-430">Service Fabric represents resources as `Metrics`.</span></span> <span data-ttu-id="2f15a-431">度量是您想要向 Service Fabric 描述的任何邏輯或實體資源。</span><span class="sxs-lookup"><span data-stu-id="2f15a-431">Metrics are any logical or physical resource that you want to describe to Service Fabric.</span></span> <span data-ttu-id="2f15a-432">度量的範例是例如「WorkQueueDepth」或「MemoryInMb」的項目。</span><span class="sxs-lookup"><span data-stu-id="2f15a-432">Examples of metrics are things like “WorkQueueDepth” or “MemoryInMb”.</span></span> <span data-ttu-id="2f15a-433">如需 Service Fabric 可以在節點上管理之實體資源的詳細資訊，請參閱[資源管理](service-fabric-resource-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="2f15a-433">For information about the physical resources that Service Fabric can govern on nodes, see [resource governance](service-fabric-resource-governance.md).</span></span> <span data-ttu-id="2f15a-434">如需設定自訂計量及其用法的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="2f15a-434">For information on configuring custom metrics and their uses, see [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

<span data-ttu-id="2f15a-435">計量不同於放置條件約束和節點屬性。</span><span class="sxs-lookup"><span data-stu-id="2f15a-435">Metrics are different from placements constraints and node properties.</span></span> <span data-ttu-id="2f15a-436">節點屬性是節點本身的靜態描述項。</span><span class="sxs-lookup"><span data-stu-id="2f15a-436">Node properties are static descriptors of the nodes themselves.</span></span> <span data-ttu-id="2f15a-437">計量說明節點所擁有的資源，以及在節點上執行時取用的服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-437">Metrics describe resources that nodes have and that services consume when they are run on a node.</span></span> <span data-ttu-id="2f15a-438">節點屬性可能是 "HasSSD"，可設為 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="2f15a-438">A node property could be "HasSSD" and could be set to true or false.</span></span> <span data-ttu-id="2f15a-439">該 SSD 上可用 (和服務所耗用) 的空間數量是像 "DriveSpaceInMb" 之類的計量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-439">The amount of space available on that SSD and how much is consumed by services would be a metric like “DriveSpaceInMb”.</span></span> 

<span data-ttu-id="2f15a-440">必須注意，就像放置條件約束和節點屬性一樣，Service Fabric 叢集資源管理員也不了解計量名稱的意義。</span><span class="sxs-lookup"><span data-stu-id="2f15a-440">It is important to note that just like for placement constraints and node properties, the Service Fabric Cluster Resource Manager doesn't understand what the names of the metrics mean.</span></span> <span data-ttu-id="2f15a-441">計量名稱只是字串。</span><span class="sxs-lookup"><span data-stu-id="2f15a-441">Metric names are just strings.</span></span> <span data-ttu-id="2f15a-442">如果您建立的計量名稱可能引起歧義，最好宣告單位。</span><span class="sxs-lookup"><span data-stu-id="2f15a-442">It is a good practice to declare units as a part of the metric names that you create when it could be ambiguous.</span></span>

## <a name="capacity"></a><span data-ttu-id="2f15a-443">容量</span><span class="sxs-lookup"><span data-stu-id="2f15a-443">Capacity</span></span>
<span data-ttu-id="2f15a-444">如果您關閉所有資源「平衡」，Service Fabric 的叢集資源管理員仍會確保節點不超出其容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-444">If you turned off all resource *balancing*, Service Fabric’s Cluster Resource Manager would still ensure that no node ended up over its capacity.</span></span> <span data-ttu-id="2f15a-445">除非叢集已滿或工作負載大於任何節點，否則管理容量溢位是可能的。</span><span class="sxs-lookup"><span data-stu-id="2f15a-445">Managing capacity overruns is possible unless the cluster is too full or the workload is larger than any node.</span></span> <span data-ttu-id="2f15a-446">容量是另一個「條件約束」，可讓叢集資源管理員了解節點使用某項資源的多寡。</span><span class="sxs-lookup"><span data-stu-id="2f15a-446">Capacity is another *constraint* that the Cluster Resource Manager uses to understand how much of a resource a node has.</span></span> <span data-ttu-id="2f15a-447">另外也會追蹤整個叢集的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-447">Remaining capacity is also tracked for the cluster as a whole.</span></span> <span data-ttu-id="2f15a-448">服務層級的容量和耗用量均以度量來表示。</span><span class="sxs-lookup"><span data-stu-id="2f15a-448">Both the capacity and the consumption at the service level are expressed in terms of metrics.</span></span> <span data-ttu-id="2f15a-449">例如，計量可能是 "ClientConnections"，而某個節點的 "ClientConnections" 容量可能是 32768。</span><span class="sxs-lookup"><span data-stu-id="2f15a-449">So for example, the metric might be "ClientConnections" and a given Node may have a capacity for "ClientConnections" of 32768.</span></span> <span data-ttu-id="2f15a-450">其他節點可以有其他限制。在該節點上執行的某些服務可以說它目前耗用 32256 個計量 "ClientConnections"。</span><span class="sxs-lookup"><span data-stu-id="2f15a-450">Other nodes can have other limits Some service running on that node can say it is currently consuming 32256 of the metric "ClientConnections".</span></span>

<span data-ttu-id="2f15a-451">在執行階段期間，叢集資源管理員會追蹤叢集中和節點上的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-451">During runtime, the Cluster Resource Manager tracks remaining capacity in the cluster and on nodes.</span></span> <span data-ttu-id="2f15a-452">為了追蹤容量，叢集資源管理員會從服務執行所在的節點容量減去每個服務的使用量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-452">In order to track capacity the Cluster Resource Manager subtracts each service's usage from node's capacity where the service runs.</span></span> <span data-ttu-id="2f15a-453">利用此資訊，Service Fabric 叢集資源管理員即可決定將複本放置或移至何處，不會讓節點超出容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-453">With this information, the Service Fabric Cluster Resource Manager can figure out where to place or move replicas so that nodes don’t go over capacity.</span></span>

<span data-ttu-id="2f15a-454"><center>
![叢集節點和容量][Image7]
</center></span><span class="sxs-lookup"><span data-stu-id="2f15a-454"><center>
![Cluster nodes and capacity][Image7]
</center></span></span>

<span data-ttu-id="2f15a-455">C#：</span><span class="sxs-lookup"><span data-stu-id="2f15a-455">C#:</span></span>

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

<span data-ttu-id="2f15a-456">PowerShell：</span><span class="sxs-lookup"><span data-stu-id="2f15a-456">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

<span data-ttu-id="2f15a-457">您可以看到叢集資訊清單中定義的容量︰</span><span class="sxs-lookup"><span data-stu-id="2f15a-457">You can see capacities defined in the cluster manifest:</span></span>

<span data-ttu-id="2f15a-458">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="2f15a-458">ClusterManifest.xml</span></span>

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

<span data-ttu-id="2f15a-459">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json。</span><span class="sxs-lookup"><span data-stu-id="2f15a-459">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters.</span></span> 

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

<span data-ttu-id="2f15a-460">服務的負載通常會動態變更。</span><span class="sxs-lookup"><span data-stu-id="2f15a-460">Commonly a service’s load changes dynamically.</span></span> <span data-ttu-id="2f15a-461">假設複本的負載 "ClientConnections" 從 1024 變成 2048，但它執行所在的節點只剩下該計量的 512 個容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-461">Say that a replica's load of "ClientConnections" changed from 1024 to 2048, but the node it was running on then only had 512 capacity remaining for that metric.</span></span> <span data-ttu-id="2f15a-462">現在，該複本或執行個體的放置已無效，因為該節點上沒有足夠的空間。</span><span class="sxs-lookup"><span data-stu-id="2f15a-462">Now that replica or instance's placement is invalid, since there's not enough room on that node.</span></span> <span data-ttu-id="2f15a-463">叢集資源管理員必須介入讓節點回到容量以下。</span><span class="sxs-lookup"><span data-stu-id="2f15a-463">The Cluster Resource Manager has to kick in and get the node back below capacity.</span></span> <span data-ttu-id="2f15a-464">它可以透過將一或多個複本或執行個體從該節點移至其他節點，來減少超過容量之節點上的負載。</span><span class="sxs-lookup"><span data-stu-id="2f15a-464">It reduces load on the node that is over capacity by moving one or more of the replicas or instances from that node to other nodes.</span></span> <span data-ttu-id="2f15a-465">移動複本時，叢集資源管理員會嘗試以最低成本來進行這些移動。</span><span class="sxs-lookup"><span data-stu-id="2f15a-465">When moving replicas, the Cluster Resource Manager tries to minimize the cost of those movements.</span></span> <span data-ttu-id="2f15a-466">移動成本在[這篇文章](service-fabric-cluster-resource-manager-movement-cost.md)中說明，叢集資源管理員之重新平衡策略和規則的詳細資訊則在[這裡](service-fabric-cluster-resource-manager-metrics.md)說明。</span><span class="sxs-lookup"><span data-stu-id="2f15a-466">Movement cost is discussed in [this article](service-fabric-cluster-resource-manager-movement-cost.md) and more about the Cluster Resource Manager's rebalancing strategies and rules is described [here](service-fabric-cluster-resource-manager-metrics.md).</span></span>

## <a name="cluster-capacity"></a><span data-ttu-id="2f15a-467">叢集容量</span><span class="sxs-lookup"><span data-stu-id="2f15a-467">Cluster capacity</span></span>
<span data-ttu-id="2f15a-468">那麼 Service Fabric 叢集資源管理員如何保持不讓整體叢集太滿？</span><span class="sxs-lookup"><span data-stu-id="2f15a-468">So how does the Service Fabric Cluster Resource Manager keep the overall cluster from being too full?</span></span> <span data-ttu-id="2f15a-469">使用動態負載的話，它並沒有太多可以執行的工作。</span><span class="sxs-lookup"><span data-stu-id="2f15a-469">Well, with dynamic load there’s not a lot it can do.</span></span> <span data-ttu-id="2f15a-470">服務的負載可能突然增加，而無視於叢集資源管理員所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="2f15a-470">Services can have their load spike independently of actions taken by the Cluster Resource Manager.</span></span> <span data-ttu-id="2f15a-471">因此，您的叢集今天有充足的空餘空間，明天就可能因為出名而後繼無力。</span><span class="sxs-lookup"><span data-stu-id="2f15a-471">As a result, your cluster with plenty of headroom today may be underpowered when you become famous tomorrow.</span></span> <span data-ttu-id="2f15a-472">話雖如此，但有一些現成的控制可防止問題。</span><span class="sxs-lookup"><span data-stu-id="2f15a-472">That said, there are some controls that are baked in to prevent problems.</span></span> <span data-ttu-id="2f15a-473">我們可以做的第一件事是防止建立新的工作負載，該工作負載會導致叢集空間變滿。</span><span class="sxs-lookup"><span data-stu-id="2f15a-473">The first thing we can do is prevent the creation of new workloads that would cause the cluster to become full.</span></span>

<span data-ttu-id="2f15a-474">假設您建立無狀態服務，而它有一些與它相關聯的負載。</span><span class="sxs-lookup"><span data-stu-id="2f15a-474">Say that you create a stateless service and it has some load associated with it.</span></span> <span data-ttu-id="2f15a-475">假設服務很注重 "DiskSpaceInMb" 計量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-475">Let’s say that the service cares about the "DiskSpaceInMb" metric.</span></span> <span data-ttu-id="2f15a-476">另外也假設服務的每個執行個體會耗用五個單位的 "DiskSpaceInMb"。</span><span class="sxs-lookup"><span data-stu-id="2f15a-476">Let's also say that it is going to consume five units of "DiskSpaceInMb" for every instance of the service.</span></span> <span data-ttu-id="2f15a-477">您想要建立服務的三個執行個體。</span><span class="sxs-lookup"><span data-stu-id="2f15a-477">You want to create three instances of the service.</span></span> <span data-ttu-id="2f15a-478">太棒了！</span><span class="sxs-lookup"><span data-stu-id="2f15a-478">Great!</span></span> <span data-ttu-id="2f15a-479">這表示叢集中需要有 15 個單位的 "DiskSpaceInMb"，我們才能建立這些服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="2f15a-479">So that means that we need 15 units of "DiskSpaceInMb" to be present in the cluster in order for us to even be able to create these service instances.</span></span> <span data-ttu-id="2f15a-480">叢集資源管理員持續計算容量和每個計量的耗用量，讓它可以判斷叢集中的剩餘容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-480">The Cluster Resource Manager continually calculates the capacity and consumption of each metric so it can determine the remaining capacity in the cluster.</span></span> <span data-ttu-id="2f15a-481">如果沒有足夠的空間，叢集資源管理員會拒絕建立服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="2f15a-481">If there isn't enough space, the Cluster Resource Manager rejects the create service call.</span></span>

<span data-ttu-id="2f15a-482">由於只是要求有 15 個單位可用，有許多不同方式可配置此空間。</span><span class="sxs-lookup"><span data-stu-id="2f15a-482">Since the requirement is only that there be 15 units available, this space could be allocated many different ways.</span></span> <span data-ttu-id="2f15a-483">例如，15 個不同節點上可能剩餘一個單位的容量，或五個不同節點上剩餘三個單位的容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-483">For example, there could be one remaining unit of capacity on 15 different nodes, or three remaining units of capacity on five different nodes.</span></span> <span data-ttu-id="2f15a-484">如果叢集資源管理員能夠重新安排讓三個節點上有五個單位可用，就會放置此服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-484">If the Cluster Resource Manager can rearrange things so there's five units available on three nodes, it places the service.</span></span> <span data-ttu-id="2f15a-485">重新安排叢集通常都可行，除非叢集幾乎已滿，或因為某些原因致使現有服務無法合併。</span><span class="sxs-lookup"><span data-stu-id="2f15a-485">Rearranging the cluster is usually possible unless the cluster is almost full or the existing services can't be consolidated for some reason.</span></span>

## <a name="buffered-capacity"></a><span data-ttu-id="2f15a-486">緩衝處理的容量</span><span class="sxs-lookup"><span data-stu-id="2f15a-486">Buffered Capacity</span></span>
<span data-ttu-id="2f15a-487">緩衝處理的容量是叢集資源管理員的另一項功能。</span><span class="sxs-lookup"><span data-stu-id="2f15a-487">Buffered capacity is another feature of the Cluster Resource Manager.</span></span> <span data-ttu-id="2f15a-488">它可以保留整體節點容量的某些部分。</span><span class="sxs-lookup"><span data-stu-id="2f15a-488">It allows reservation of some portion of the overall node capacity.</span></span> <span data-ttu-id="2f15a-489">這個容量緩衝區只用來在升級和節點失敗期間放置服務。</span><span class="sxs-lookup"><span data-stu-id="2f15a-489">This capacity buffer is only used to place services during upgrades and node failures.</span></span> <span data-ttu-id="2f15a-490">緩衝處理的容量是針對所有節點的每個計量進行全域指定。</span><span class="sxs-lookup"><span data-stu-id="2f15a-490">Buffered Capacity is specified globally per metric for all nodes.</span></span> <span data-ttu-id="2f15a-491">您挑選的保留容量值取決於叢集中的容錯網域和升級網域數目。</span><span class="sxs-lookup"><span data-stu-id="2f15a-491">The value you pick for the reserved capacity is a function of the number of Fault and Upgrade Domains you have in the cluster.</span></span> <span data-ttu-id="2f15a-492">容錯網域和升級網域越多，表示您可以挑選較小的緩衝容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-492">More Fault and Upgrade Domains means that you can pick a lower number for your buffered capacity.</span></span> <span data-ttu-id="2f15a-493">如果您有較多網域，則在升級和失敗期間，無法使用的叢集部分當然會比較少。</span><span class="sxs-lookup"><span data-stu-id="2f15a-493">If you have more domains, you can expect smaller amounts of your cluster to be unavailable during upgrades and failures.</span></span> <span data-ttu-id="2f15a-494">指定緩衝處理的容量時，必須同時指定計量的節點容量，這樣才有意義。</span><span class="sxs-lookup"><span data-stu-id="2f15a-494">Specifying Buffered Capacity only makes sense if you have also specified the node capacity for a metric.</span></span>

<span data-ttu-id="2f15a-495">以下是指定緩衝處理容量的方式：</span><span class="sxs-lookup"><span data-stu-id="2f15a-495">Here's an example of how to specify buffered capacity:</span></span>

<span data-ttu-id="2f15a-496">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="2f15a-496">ClusterManifest.xml</span></span>

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

<span data-ttu-id="2f15a-497">獨立部署透過 ClusterConfig.json，Azure 託管叢集透過 Template.json：</span><span class="sxs-lookup"><span data-stu-id="2f15a-497">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="2f15a-498">當叢集耗盡計量的緩衝容量時，建立新的服務會失敗。</span><span class="sxs-lookup"><span data-stu-id="2f15a-498">The creation of new services fails when the cluster is out of buffered capacity for a metric.</span></span> <span data-ttu-id="2f15a-499">防止建立新服務以保留緩衝區，可確保升級和失敗不會造成節點超出容量。</span><span class="sxs-lookup"><span data-stu-id="2f15a-499">Preventing the creation of new services to preserve the buffer ensures that upgrades and failures don’t cause nodes to go over capacity.</span></span> <span data-ttu-id="2f15a-500">緩衝容量是選擇性，但建議用在已定義計量容量的任何叢集。</span><span class="sxs-lookup"><span data-stu-id="2f15a-500">Buffered capacity is optional but is recommended in any cluster that defines a capacity for a metric.</span></span>

<span data-ttu-id="2f15a-501">叢集資源管理員會公開此負載資訊。</span><span class="sxs-lookup"><span data-stu-id="2f15a-501">The Cluster Resource Manager exposes this load information.</span></span> <span data-ttu-id="2f15a-502">對於每個計量，這項資訊包括：</span><span class="sxs-lookup"><span data-stu-id="2f15a-502">For each metric, this information includes:</span></span> 
  - <span data-ttu-id="2f15a-503">緩衝處理的容量設定</span><span class="sxs-lookup"><span data-stu-id="2f15a-503">the buffered capacity settings</span></span>
  - <span data-ttu-id="2f15a-504">總容量</span><span class="sxs-lookup"><span data-stu-id="2f15a-504">the total capacity</span></span>
  - <span data-ttu-id="2f15a-505">目前的耗用量</span><span class="sxs-lookup"><span data-stu-id="2f15a-505">the current consumption</span></span>
  - <span data-ttu-id="2f15a-506">每個計量是否被視為平衡</span><span class="sxs-lookup"><span data-stu-id="2f15a-506">whether each metric is considered balanced or not</span></span>
  - <span data-ttu-id="2f15a-507">標準差的統計資料</span><span class="sxs-lookup"><span data-stu-id="2f15a-507">statistics about the standard deviation</span></span>
  - <span data-ttu-id="2f15a-508">具有最大和最小負載的節點</span><span class="sxs-lookup"><span data-stu-id="2f15a-508">the nodes which have the most and least load</span></span>  
  
<span data-ttu-id="2f15a-509">我們可以看到該輸出的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="2f15a-509">Below we see an example of that output:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2f15a-510">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f15a-510">Next steps</span></span>
* <span data-ttu-id="2f15a-511">如需叢集資源管理員內的架構和資訊流程的相關資訊，請參閱[這篇文章](service-fabric-cluster-resource-manager-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="2f15a-511">For information on the architecture and information flow within the Cluster Resource Manager, check out [this article ](service-fabric-cluster-resource-manager-architecture.md)</span></span>
* <span data-ttu-id="2f15a-512">定義重組度量是合併 (而不是擴增) 節點上負載的一種方式。若要了解如何設定重組，請參閱 [這篇文章](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="2f15a-512">Defining Defragmentation Metrics is one way to consolidate load on nodes instead of spreading it out. To learn how to configure defragmentation, refer to [this article](service-fabric-cluster-resource-manager-defragmentation-metrics.md)</span></span>
* <span data-ttu-id="2f15a-513">從頭開始，並 [取得 Service Fabric 叢集資源管理員的簡介](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="2f15a-513">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
* <span data-ttu-id="2f15a-514">若要了解叢集資源管理員如何管理並平衡叢集中的負載，請查看關於 [平衡負載](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="2f15a-514">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
