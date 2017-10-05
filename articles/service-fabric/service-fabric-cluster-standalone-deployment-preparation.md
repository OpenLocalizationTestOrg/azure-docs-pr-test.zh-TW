---
title: "Azure Service Fabric 獨立叢集部署準備 | Microsoft Docs"
description: "文件說明關於在部署用來處理生產工作負載的叢集之前，需要考慮準備的環境和建立的叢集組態。"
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: f332193f9a53260173a1010b8bf9f08726bea427
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a><span data-ttu-id="aa86d-103">規劃和準備您的 Service Fabric 獨立叢集部署</span><span class="sxs-lookup"><span data-stu-id="aa86d-103">Plan and prepare your Service Fabric standalone cluster deployment</span></span>
<span data-ttu-id="aa86d-104">建立叢集之前，請先執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="aa86d-104">Perform the following steps before you create your cluster.</span></span>

### <a name="step-1-plan-your-cluster-infrastructure"></a><span data-ttu-id="aa86d-105">步驟 1︰規劃叢集基礎結構</span><span class="sxs-lookup"><span data-stu-id="aa86d-105">Step 1: Plan your cluster infrastructure</span></span>
<span data-ttu-id="aa86d-106">您即將在您所擁有的電腦上建立 Service Fabric 叢集，因此您可以決定您希望叢集不受何種失敗的影響。</span><span class="sxs-lookup"><span data-stu-id="aa86d-106">You are about to create a Service Fabric cluster on machines you own, so you can decide what kinds of failures you want the cluster to survive.</span></span> <span data-ttu-id="aa86d-107">例如，您是否需要提供給這些電腦的個別電源線或網際網路連線？</span><span class="sxs-lookup"><span data-stu-id="aa86d-107">For example, do you need separate power lines or Internet connections supplied to these machines?</span></span> <span data-ttu-id="aa86d-108">此外，請考慮這些電腦的實體安全性。</span><span class="sxs-lookup"><span data-stu-id="aa86d-108">In addition, consider the physical security of these machines.</span></span> <span data-ttu-id="aa86d-109">電腦位於何處？哪些人需要存取這些電腦？</span><span class="sxs-lookup"><span data-stu-id="aa86d-109">Where are the machines located and who needs access to them?</span></span> <span data-ttu-id="aa86d-110">您做出這些決定之後，可依據邏輯將電腦對應到多個容錯網域 (請參閱步驟 4)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-110">After you make these decisions, you can logically map the machines to the various fault domains (see Step 4).</span></span> <span data-ttu-id="aa86d-111">生產叢集的基礎結構規劃比起測試叢集更為複雜。</span><span class="sxs-lookup"><span data-stu-id="aa86d-111">The infrastructure planning for production clusters is more involved than for test clusters.</span></span>

### <a name="step-2-prepare-the-machines-to-meet-the-prerequisites"></a><span data-ttu-id="aa86d-112">步驟 2︰準備符合必要條件的電腦</span><span class="sxs-lookup"><span data-stu-id="aa86d-112">Step 2: Prepare the machines to meet the prerequisites</span></span>
<span data-ttu-id="aa86d-113">您想要新增到叢集的每部電腦的必要條件︰</span><span class="sxs-lookup"><span data-stu-id="aa86d-113">Prerequisites for each machine that you want to add to the cluster:</span></span>

* <span data-ttu-id="aa86d-114">建議至少 16 GB RAM。</span><span class="sxs-lookup"><span data-stu-id="aa86d-114">A minimum of 16 GB of RAM is recommended.</span></span>
* <span data-ttu-id="aa86d-115">建議至少 40 GB 的可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="aa86d-115">A minimum of 40 of GB available disk space is recommended.</span></span>
* <span data-ttu-id="aa86d-116">建議 4 核心或以上的 CPU。</span><span class="sxs-lookup"><span data-stu-id="aa86d-116">A 4 core or greater CPU is recommended.</span></span>
* <span data-ttu-id="aa86d-117">所有電腦的安全網路連線。</span><span class="sxs-lookup"><span data-stu-id="aa86d-117">Connectivity to a secure network or networks for all machines.</span></span>
* <span data-ttu-id="aa86d-118">Windows Server 2012 R2 或 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="aa86d-118">Windows Server 2012 R2 or Windows Server 2016.</span></span> 
* <span data-ttu-id="aa86d-119">[.NET Framework 4.5.1 或更高版本](https://www.microsoft.com/download/details.aspx?id=40773)，完整安裝。</span><span class="sxs-lookup"><span data-stu-id="aa86d-119">[.NET Framework 4.5.1 or higher](https://www.microsoft.com/download/details.aspx?id=40773), full install.</span></span>
* <span data-ttu-id="aa86d-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).</span></span>
* <span data-ttu-id="aa86d-121">[RemoteRegistry 服務](https://technet.microsoft.com/library/cc754820) 應該在所有電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="aa86d-121">The [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) should be running on all the machines.</span></span>

<span data-ttu-id="aa86d-122">部署和設定叢集的叢集系統管理員必須擁有每部電腦的 [系統管理員權限](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="aa86d-122">The cluster administrator deploying and configuring the cluster must have [administrator privileges](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) on each of the machines.</span></span> <span data-ttu-id="aa86d-123">您無法在網域控制站上安裝 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="aa86d-123">You cannot install Service Fabric on a domain controller.</span></span>

### <a name="step-3-determine-the-initial-cluster-size"></a><span data-ttu-id="aa86d-124">步驟 3︰決定初始叢集大小</span><span class="sxs-lookup"><span data-stu-id="aa86d-124">Step 3: Determine the initial cluster size</span></span>
<span data-ttu-id="aa86d-125">獨立 Service Fabric 叢集中的每個節點都已部署 Service Fabric 執行階段，並且是叢集的成員。</span><span class="sxs-lookup"><span data-stu-id="aa86d-125">Each node in a standalone Service Fabric cluster has the Service Fabric runtime deployed and is a member of the cluster.</span></span> <span data-ttu-id="aa86d-126">在一般生產部署中，每個作業系統執行個體 (實體或虛擬) 都有一個節點。</span><span class="sxs-lookup"><span data-stu-id="aa86d-126">In a typical production deployment, there is one node per OS instance (physical or virtual).</span></span> <span data-ttu-id="aa86d-127">叢集大小取決於您的業務需求。</span><span class="sxs-lookup"><span data-stu-id="aa86d-127">The cluster size is determined by your business needs.</span></span> <span data-ttu-id="aa86d-128">不過，您必須有三個節點 (電腦或虛擬機器) 的最小叢集大小。</span><span class="sxs-lookup"><span data-stu-id="aa86d-128">However, you must have a minimum cluster size of three nodes (machines or virtual machines).</span></span>
<span data-ttu-id="aa86d-129">基於開發目的，在一部指定的電腦上可以有多個節點。</span><span class="sxs-lookup"><span data-stu-id="aa86d-129">For development purposes, you can have more than one node on a given machine.</span></span> <span data-ttu-id="aa86d-130">在生產環境中，對於每個實體或虛擬機器，Service Fabric 只支援一個節點。</span><span class="sxs-lookup"><span data-stu-id="aa86d-130">In a production environment, Service Fabric supports only one node per physical or virtual machine.</span></span>

### <a name="step-4-determine-the-number-of-fault-domains-and-upgrade-domains"></a><span data-ttu-id="aa86d-131">步驟 4︰決定容錯網域和升級網域的數目</span><span class="sxs-lookup"><span data-stu-id="aa86d-131">Step 4: Determine the number of fault domains and upgrade domains</span></span>
<span data-ttu-id="aa86d-132">*容錯網域* (FD) 是故障的實體單元，而且與資料中心內的實體基礎結構直接相關。</span><span class="sxs-lookup"><span data-stu-id="aa86d-132">A *fault domain* (FD) is a physical unit of failure and is directly related to the physical infrastructure in the data centers.</span></span> <span data-ttu-id="aa86d-133">容錯網域是由共用單一失敗點的硬體元件 (電腦、交換器、網路等) 所組成。</span><span class="sxs-lookup"><span data-stu-id="aa86d-133">A fault domain consists of hardware components (computers, switches, networks, and more) that share a single point of failure.</span></span> <span data-ttu-id="aa86d-134">雖然容錯網域和機架之間沒有 1:1 對應，但是大致上來說，可以將每個機架視為一個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="aa86d-134">Although there is no 1:1 mapping between fault domains and racks, loosely speaking, each rack can be considered a fault domain.</span></span> <span data-ttu-id="aa86d-135">考慮叢集中的節點時，強烈建議至少在三個容錯網域之間散佈節點。</span><span class="sxs-lookup"><span data-stu-id="aa86d-135">When considering the nodes in your cluster, we strongly recommend that the nodes be distributed among at least three fault domains.</span></span>

<span data-ttu-id="aa86d-136">當您在 ClusterConfig.json 中指定 FD 時，可以選擇每個 FD 的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa86d-136">When you specify FDs in ClusterConfig.json, you can choose the name for each FD.</span></span> <span data-ttu-id="aa86d-137">Service Fabric 支援階層式 FD，因此，您可以在 FD 中反映您的基礎結構拓撲。</span><span class="sxs-lookup"><span data-stu-id="aa86d-137">Service Fabric supports hierarchical FDs, so you can reflect your infrastructure topology in them.</span></span>  <span data-ttu-id="aa86d-138">例如，下列 FD 有效：</span><span class="sxs-lookup"><span data-stu-id="aa86d-138">For example, the following FDs are valid:</span></span>

* <span data-ttu-id="aa86d-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span><span class="sxs-lookup"><span data-stu-id="aa86d-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span></span>
* <span data-ttu-id="aa86d-140">"faultDomain": "fd:/FD1"</span><span class="sxs-lookup"><span data-stu-id="aa86d-140">"faultDomain": "fd:/FD1"</span></span>
* <span data-ttu-id="aa86d-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span><span class="sxs-lookup"><span data-stu-id="aa86d-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span></span>

<span data-ttu-id="aa86d-142">*升級網域* (UD) 是節點的邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="aa86d-142">An *upgrade domain* (UD) is a logical unit of nodes.</span></span> <span data-ttu-id="aa86d-143">在 Service Fabric 協調式升級 (應用程式升級或叢集升級) 期間，會關閉 UD 中的所有節點來執行升級，而其他 UD 中的節點則仍然可用來提供要求。</span><span class="sxs-lookup"><span data-stu-id="aa86d-143">During Service Fabric orchestrated upgrades (either an application upgrade or a cluster upgrade), all nodes in a UD are taken down to perform the upgrade while nodes in other UDs remain available to serve requests.</span></span> <span data-ttu-id="aa86d-144">您對電腦所進行的韌體升級不會接受 UD，因此您必須一次在一部電腦上進行。</span><span class="sxs-lookup"><span data-stu-id="aa86d-144">The firmware upgrades you perform on your machines do not honor UDs, so you must do them one machine at a time.</span></span>

<span data-ttu-id="aa86d-145">思考這些概念最簡單的方式就是將 FD 視為非計劃性故障的單元，並將 UD 視為計劃性維護的單元。</span><span class="sxs-lookup"><span data-stu-id="aa86d-145">The simplest way to think about these concepts is to consider FDs as the unit of unplanned failure and UDs as the unit of planned maintenance.</span></span>

<span data-ttu-id="aa86d-146">當您在 ClusterConfig.json 中指定 UD 時，可以選擇每個 UD 的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa86d-146">When you specify UDs in ClusterConfig.json, you can choose the name for each UD.</span></span> <span data-ttu-id="aa86d-147">例如，下列名稱有效：</span><span class="sxs-lookup"><span data-stu-id="aa86d-147">For example, the following names are valid:</span></span>

* <span data-ttu-id="aa86d-148">"upgradeDomain": "UD0"</span><span class="sxs-lookup"><span data-stu-id="aa86d-148">"upgradeDomain": "UD0"</span></span>
* <span data-ttu-id="aa86d-149">"upgradeDomain": "UD1A"</span><span class="sxs-lookup"><span data-stu-id="aa86d-149">"upgradeDomain": "UD1A"</span></span>
* <span data-ttu-id="aa86d-150">"upgradeDomain": "DomainRed"</span><span class="sxs-lookup"><span data-stu-id="aa86d-150">"upgradeDomain": "DomainRed"</span></span>
* <span data-ttu-id="aa86d-151">"upgradeDomain": "Blue"</span><span class="sxs-lookup"><span data-stu-id="aa86d-151">"upgradeDomain": "Blue"</span></span>

<span data-ttu-id="aa86d-152">如需升級網域和容錯網域的詳細資訊，請參閱[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-152">For more detailed information on upgrade domains and fault domains, see [Describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>

### <a name="step-5-download-the-service-fabric-standalone-package-for-windows-server"></a><span data-ttu-id="aa86d-153">步驟 5︰下載適用於 Windows Server 的 Service Fabric 獨立封裝</span><span class="sxs-lookup"><span data-stu-id="aa86d-153">Step 5: Download the Service Fabric standalone package for Windows Server</span></span>
<span data-ttu-id="aa86d-154">[下載連結 - Service Fabric 獨立封裝 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)，並將封裝解壓縮至不屬於叢集一部分的部署電腦，或解壓縮至將屬於叢集的其中一部電腦。</span><span class="sxs-lookup"><span data-stu-id="aa86d-154">[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip the package, either to a deployment machine that is not part of the cluster, or to one of the machines that will be a part of your cluster.</span></span>

### <a name="step-6-modify-cluster-configuration"></a><span data-ttu-id="aa86d-155">步驟 6︰修改叢集組態</span><span class="sxs-lookup"><span data-stu-id="aa86d-155">Step 6: Modify cluster configuration</span></span>
<span data-ttu-id="aa86d-156">若要建立獨立叢集，您必須建立獨立叢集組態 ClusterConfig.json 檔案，其中描述叢集的規格。</span><span class="sxs-lookup"><span data-stu-id="aa86d-156">To create a standalone cluster you have to create a standalone cluster configuration ClusterConfig.json file, which describes the specification of the cluster.</span></span> <span data-ttu-id="aa86d-157">您可以根據可在下面連結找到的範本來建立組態檔。</span><span class="sxs-lookup"><span data-stu-id="aa86d-157">You can base the configuration file on the templates found at the below link.</span></span> <br><span data-ttu-id="aa86d-158">
[獨立叢集組態](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="aa86d-158">
[Standalone Cluster Configurations](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<span data-ttu-id="aa86d-159">如需此檔案中各個區段的詳細資訊，請參閱[獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-159">For details on the sections in this file, see [Configuration settings for standalone Windows cluster](service-fabric-cluster-manifest.md).</span></span>

<span data-ttu-id="aa86d-160">從您下載的封裝中開啟其中一個 ClusterConfig.json 檔案，然後修改下列設定︰</span><span class="sxs-lookup"><span data-stu-id="aa86d-160">Open one of the ClusterConfig.json files from the package you downloaded and modify the following settings:</span></span>
| <span data-ttu-id="aa86d-161">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="aa86d-161">**Configuration Setting**</span></span> | <span data-ttu-id="aa86d-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="aa86d-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="aa86d-163">**NodeTypes**</span><span class="sxs-lookup"><span data-stu-id="aa86d-163">**NodeTypes**</span></span> |<span data-ttu-id="aa86d-164">節點類型可讓您將叢集節點分成不同的群組。</span><span class="sxs-lookup"><span data-stu-id="aa86d-164">Node types allow you to separate your cluster nodes into various groups.</span></span> <span data-ttu-id="aa86d-165">一個叢集至少必須有一個節點類型。</span><span class="sxs-lookup"><span data-stu-id="aa86d-165">A cluster must have at least one NodeType.</span></span> <span data-ttu-id="aa86d-166">群組中的所有節點都有下列共同的特性：</span><span class="sxs-lookup"><span data-stu-id="aa86d-166">All nodes in a group have the following common characteristics:</span></span> <br> <span data-ttu-id="aa86d-167">**Name** - 這是節點類型名稱。</span><span class="sxs-lookup"><span data-stu-id="aa86d-167">**Name** - This is the node type name.</span></span> <br><span data-ttu-id="aa86d-168">**Endpoint Ports** - 這些是與這個節點類型相關聯的各種具名端點 (連接埠)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-168">**Endpoint Ports** - These are various named end points (ports) that are associated with this node type.</span></span> <span data-ttu-id="aa86d-169">您可以使用任何您想要的連接埠號碼，只要該號碼未與此資訊清單中的其他任何號碼衝突，而且目前沒有任何其他在電腦/VM 上執行的應用程式在使用該號碼即可。</span><span class="sxs-lookup"><span data-stu-id="aa86d-169">You can use any port number that you wish, as long as they do not conflict with anything else in this manifest and are not already in use by any other application running on the machine/VM.</span></span> <br> <span data-ttu-id="aa86d-170">**Placement Properties** - 此節點類型的這些屬性是用來做為系統服務或您的服務的放置條件約束。</span><span class="sxs-lookup"><span data-stu-id="aa86d-170">**Placement Properties** - These describe properties for this node type that you use as placement constraints for the system services or your services.</span></span> <span data-ttu-id="aa86d-171">這些屬性是使用者定義的索引鍵/值組，可針對指定節點提供額外的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="aa86d-171">These properties are user-defined key/value pairs that provide extra meta data for a given node.</span></span> <span data-ttu-id="aa86d-172">節點屬性的範例包括節點是否有硬碟機或圖形卡、其硬碟機的磁針數、核心，以及其他實體屬性。</span><span class="sxs-lookup"><span data-stu-id="aa86d-172">Examples of node properties would be whether the node has a hard drive or graphics card, the number of spindles in its hard drive, cores, and other physical properties.</span></span> <br> <span data-ttu-id="aa86d-173">**Capacities** - 節點容量會定義特定節點可以使用的特定資源名稱和數量。</span><span class="sxs-lookup"><span data-stu-id="aa86d-173">**Capacities** - Node capacities define the name and amount of a particular resource that a particular node has available for consumption.</span></span> <span data-ttu-id="aa86d-174">例如，節點可能會定義它具有名為 "MemoryInMb" 的度量容量，而且預設有 2048 MB 的可用記憶體。</span><span class="sxs-lookup"><span data-stu-id="aa86d-174">For example, a node may define that it has capacity for a metric called “MemoryInMb” and that it has 2048 MB available by default.</span></span> <span data-ttu-id="aa86d-175">這些容量會在執行階段使用，以確保需要特定資源數量的服務會放在需要的數量中有這些資源的節點上。</span><span class="sxs-lookup"><span data-stu-id="aa86d-175">These capacities are used at runtime to ensure that services that require particular amounts of resources are placed on the nodes that have those resources available in the required amounts.</span></span><br><span data-ttu-id="aa86d-176">**IsPrimary** - 如果有一個以上已定義的節點類型，請確定只有一個設為主要 (且值為 *true*)，這是系統服務執行的位置。</span><span class="sxs-lookup"><span data-stu-id="aa86d-176">**IsPrimary** - If you have more than one NodeType defined ensure that only one is set to primary with the value *true*, which is where the system services run.</span></span> <span data-ttu-id="aa86d-177">其他所有節點類型應該設定為值 *false*</span><span class="sxs-lookup"><span data-stu-id="aa86d-177">All other node types should be set to the value *false*</span></span> |
| <span data-ttu-id="aa86d-178">**Nodes**</span><span class="sxs-lookup"><span data-stu-id="aa86d-178">**Nodes**</span></span> |<span data-ttu-id="aa86d-179">這些是屬於叢集一部分的每個節點的詳細資料 (節點類型、節點名稱、IP 位址、節點的容錯網域和升級網域)。</span><span class="sxs-lookup"><span data-stu-id="aa86d-179">These are the details for each of the nodes that are part of the cluster (node type, node name, IP address, fault domain, and upgrade domain of the node).</span></span> <span data-ttu-id="aa86d-180">您想要建立叢集所在的電腦必須與其 IP 位址一起列在這裡。</span><span class="sxs-lookup"><span data-stu-id="aa86d-180">The machines you want the cluster to be created on need to be listed here with their IP addresses.</span></span> <br> <span data-ttu-id="aa86d-181">如果您為所有節點使用相同的 IP 位址，則會建立一整體叢集，您可以將此叢集用於測試之用。</span><span class="sxs-lookup"><span data-stu-id="aa86d-181">If you use the same IP address for all the nodes, then a one-box cluster is created, which you can use for testing purposes.</span></span> <span data-ttu-id="aa86d-182">不要使用一整體叢集部署生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="aa86d-182">Do not use One-box clusters for deploying production workloads.</span></span> |

<span data-ttu-id="aa86d-183">完成設定叢集組態的所有設定之後，即可針對叢集環境 (步驟 7) 進行測試。</span><span class="sxs-lookup"><span data-stu-id="aa86d-183">After the cluster configuration has had all settings configured to the environment, it can be tested against the cluster environment (step 7).</span></span>

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a><span data-ttu-id="aa86d-184">步驟 7.</span><span class="sxs-lookup"><span data-stu-id="aa86d-184">Step 7.</span></span> <span data-ttu-id="aa86d-185">環境設定</span><span class="sxs-lookup"><span data-stu-id="aa86d-185">Environment setup</span></span>

<span data-ttu-id="aa86d-186">當叢集系統管理員設定 Service Fabric 獨立叢集時，必須根據下列準則設定環境︰</span><span class="sxs-lookup"><span data-stu-id="aa86d-186">When a cluster administrator configures a Service Fabric standalone cluster, the environment is needs to be set up with the following criteria:</span></span> <br>
1. <span data-ttu-id="aa86d-187">對叢集組態檔中列為節點的所有電腦，建立叢集的使用者應擁有系統管理員層級的安全性權限。</span><span class="sxs-lookup"><span data-stu-id="aa86d-187">The user creating the cluster should have administrator-level security privileges to all machines that are listed as nodes in the cluster configuration file.</span></span>
2. <span data-ttu-id="aa86d-188">所建立叢集中的機器以及每個叢集節點電腦都必須︰</span><span class="sxs-lookup"><span data-stu-id="aa86d-188">Machine from which the cluster is created, as well as each cluster node machine must:</span></span>
* <span data-ttu-id="aa86d-189">已將 Service Fabric SDK 解除安裝</span><span class="sxs-lookup"><span data-stu-id="aa86d-189">Have Service Fabric SDK uninstalled</span></span>
* <span data-ttu-id="aa86d-190">已將 Service Fabric 執行階段解除安裝</span><span class="sxs-lookup"><span data-stu-id="aa86d-190">Have Service Fabric runtime uninstalled</span></span> 
* <span data-ttu-id="aa86d-191">已啟用 Windows 防火牆服務 (mpssvc)</span><span class="sxs-lookup"><span data-stu-id="aa86d-191">Have the Windows Firewall service (mpssvc) enabled</span></span>
* <span data-ttu-id="aa86d-192">已啟用遠端登錄服務 (remoteregistry)</span><span class="sxs-lookup"><span data-stu-id="aa86d-192">Have the Remote Registry Service (remoteregistry) enabled</span></span>
* <span data-ttu-id="aa86d-193">已啟用檔案共用 (SMB)</span><span class="sxs-lookup"><span data-stu-id="aa86d-193">Have file sharing (SMB) enabled</span></span>
* <span data-ttu-id="aa86d-194">已根據叢集組態的連接埠，開啟必要的連接埠</span><span class="sxs-lookup"><span data-stu-id="aa86d-194">Have necessary ports opened, based on cluster configuration ports</span></span>
* <span data-ttu-id="aa86d-195">已經開啟 Windows SMB 和遠端登錄服務的必要通訊埠︰135、137、138、139 和 445</span><span class="sxs-lookup"><span data-stu-id="aa86d-195">Have necessary ports opened for Windows SMB and Remote Registry service: 135, 137, 138, 139, and 445</span></span>
* <span data-ttu-id="aa86d-196">網路已彼此連線</span><span class="sxs-lookup"><span data-stu-id="aa86d-196">Have network connectivity to one another</span></span>
3. <span data-ttu-id="aa86d-197">叢集節點電腦應無一是網域控制站。</span><span class="sxs-lookup"><span data-stu-id="aa86d-197">None of the cluster node machines should be a Domain Controller.</span></span>
4. <span data-ttu-id="aa86d-198">如果要部署的叢集是安全叢集，驗證安全性必要條件已就緒，並已正確設定組態。</span><span class="sxs-lookup"><span data-stu-id="aa86d-198">If the cluster to be deployed is a secure cluster, validate the necessary security prerequisites are in place, and are configured correctly against the configuration.</span></span>
5. <span data-ttu-id="aa86d-199">如果叢集電腦不可存取網際網路，在叢集組態中設定下列各項：</span><span class="sxs-lookup"><span data-stu-id="aa86d-199">If the cluster machines are not internet-accessible, set the following in the cluster configuration:</span></span>
* <span data-ttu-id="aa86d-200">停用遙測：在 *properties* 下設定 *"enableTelemetry": false*</span><span class="sxs-lookup"><span data-stu-id="aa86d-200">Disable telemetry:   Under *properties* set   *"enableTelemetry": false*</span></span>
* <span data-ttu-id="aa86d-201">停用自動的 Fabric 版本下載，以及目前叢集版本接近終止支援的通知：在 [屬性] 底下，設定 *"fabricClusterAutoupgradeEnabled": false*</span><span class="sxs-lookup"><span data-stu-id="aa86d-201">Disable automatic Fabric version downloading & notifications that the current cluster version is nearing end of support:   Under *properties* set   *"fabricClusterAutoupgradeEnabled": false*</span></span>
* <span data-ttu-id="aa86d-202">或者，如果網路的網際網路存取僅限於允許清單上的網域，則自動升級將需要下列網域：   go.microsoft.com   download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="aa86d-202">Alternatively if network internet access is limited to white-listed domains, the domains below are required for automatic upgrade:   go.microsoft.com   download.microsoft.com</span></span>

6. <span data-ttu-id="aa86d-203">設定適當的 Service Fabric 防毒排除項目︰</span><span class="sxs-lookup"><span data-stu-id="aa86d-203">Set appropriate Service Fabric antivirus exclusions:</span></span>

| <span data-ttu-id="aa86d-204">**防毒排除目錄**</span><span class="sxs-lookup"><span data-stu-id="aa86d-204">**Antivirus Excluded directories**</span></span> |
| --- |
| <span data-ttu-id="aa86d-205">Program Files\Microsoft Service Fabric</span><span class="sxs-lookup"><span data-stu-id="aa86d-205">Program Files\Microsoft Service Fabric</span></span> |
| <span data-ttu-id="aa86d-206">FabricDataRoot (從叢集組態)</span><span class="sxs-lookup"><span data-stu-id="aa86d-206">FabricDataRoot (from cluster configuration)</span></span> |
| <span data-ttu-id="aa86d-207">FabricLogRoot (從叢集組態)</span><span class="sxs-lookup"><span data-stu-id="aa86d-207">FabricLogRoot (from cluster configuration)</span></span> |

| <span data-ttu-id="aa86d-208">**防毒排除處理序**</span><span class="sxs-lookup"><span data-stu-id="aa86d-208">**Antivirus Excluded processes**</span></span> |
| --- |
| <span data-ttu-id="aa86d-209">Fabric.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-209">Fabric.exe</span></span> |
| <span data-ttu-id="aa86d-210">FabricHost.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-210">FabricHost.exe</span></span> |
| <span data-ttu-id="aa86d-211">FabricInstallerService.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-211">FabricInstallerService.exe</span></span> |
| <span data-ttu-id="aa86d-212">FabricSetup.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-212">FabricSetup.exe</span></span> |
| <span data-ttu-id="aa86d-213">FabricDeployer.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-213">FabricDeployer.exe</span></span> |
| <span data-ttu-id="aa86d-214">ImageBuilder.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-214">ImageBuilder.exe</span></span> |
| <span data-ttu-id="aa86d-215">FabricGateway.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-215">FabricGateway.exe</span></span> |
| <span data-ttu-id="aa86d-216">FabricDCA.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-216">FabricDCA.exe</span></span> |
| <span data-ttu-id="aa86d-217">FabricFAS.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-217">FabricFAS.exe</span></span> |
| <span data-ttu-id="aa86d-218">FabricUOS.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-218">FabricUOS.exe</span></span> |
| <span data-ttu-id="aa86d-219">FabricRM.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-219">FabricRM.exe</span></span> |
| <span data-ttu-id="aa86d-220">FileStoreService.exe</span><span class="sxs-lookup"><span data-stu-id="aa86d-220">FileStoreService.exe</span></span> |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a><span data-ttu-id="aa86d-221">步驟 8。</span><span class="sxs-lookup"><span data-stu-id="aa86d-221">Step 8.</span></span> <span data-ttu-id="aa86d-222">使用 TestConfiguration 指令碼驗證環境</span><span class="sxs-lookup"><span data-stu-id="aa86d-222">Validate environment using TestConfiguration script</span></span>
<span data-ttu-id="aa86d-223">您可以在獨立封裝中找到 TestConfiguration.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="aa86d-223">The TestConfiguration.ps1 script can be found in the standalone package.</span></span> <span data-ttu-id="aa86d-224">它可做為「最佳做法分析程式」用來驗證上述的一些準則，並應做為例行性檢查用來驗證是否能在指定的環境上部署叢集。</span><span class="sxs-lookup"><span data-stu-id="aa86d-224">It is used as a Best Practices Analyzer to validate some of the criteria above and should be used as a sanity check to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="aa86d-225">如果發生任何錯誤，請參閱[環境設定](service-fabric-cluster-standalone-deployment-preparation.md)下的清單進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="aa86d-225">If there is any failure, refer to the list under [Environment Setup](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting.</span></span> 

<span data-ttu-id="aa86d-226">此指令碼可以在以系統管理員身分存取叢集組態檔中列為節點的所有電腦的任何電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="aa86d-226">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="aa86d-227">執行此指令碼所在的電腦不一定是叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="aa86d-227">The machine that this script is run on does not have to be part of the cluster.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

<span data-ttu-id="aa86d-228">目前此組態測試模組並不會驗證安全性設定，因此這必須獨立完成。</span><span class="sxs-lookup"><span data-stu-id="aa86d-228">Currently this configuration testing module does not validate the security configuration so this has to be done independently.</span></span>  

> [!NOTE]
> <span data-ttu-id="aa86d-229">我們會持續進行改進，以讓此模組更穩健，因此如果您認為目前有 TestConfiguration 攔截不到的錯誤或有疏漏之處，請透過我們的[支援通道](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)來告訴我們。</span><span class="sxs-lookup"><span data-stu-id="aa86d-229">We are continually making improvements to make this module more robust, so if there is a faulty or missing case which you believe isn't currently caught by TestConfiguration, please let us know through our [support channels](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>   
> 
> 

## <a name="next-steps"></a><span data-ttu-id="aa86d-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa86d-230">Next steps</span></span>
* [<span data-ttu-id="aa86d-231">建立在 Windows Server 上執行的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="aa86d-231">Create a standalone cluster running on Windows Server</span></span>](service-fabric-cluster-creation-for-windows-server.md)
