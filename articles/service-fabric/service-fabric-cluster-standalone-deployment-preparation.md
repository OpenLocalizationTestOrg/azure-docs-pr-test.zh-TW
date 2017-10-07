---
title: "服務網狀架構獨立叢集部署準備 aaaAzure |Microsoft 文件"
description: "建立 hello 叢集設定時，toobe 考慮先前 toodeploying 叢集用於處理生產工作負載以及相關 toopreparing hello 環境的文件集。"
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
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a><span data-ttu-id="7d990-103">規劃和準備您的 Service Fabric 獨立叢集部署</span><span class="sxs-lookup"><span data-stu-id="7d990-103">Plan and prepare your Service Fabric standalone cluster deployment</span></span>
<span data-ttu-id="7d990-104">執行下列步驟，建立您的叢集之前的 hello。</span><span class="sxs-lookup"><span data-stu-id="7d990-104">Perform hello following steps before you create your cluster.</span></span>

### <a name="step-1-plan-your-cluster-infrastructure"></a><span data-ttu-id="7d990-105">步驟 1︰規劃叢集基礎結構</span><span class="sxs-lookup"><span data-stu-id="7d990-105">Step 1: Plan your cluster infrastructure</span></span>
<span data-ttu-id="7d990-106">您即將 toocreate Service Fabric 叢集，您所擁有的電腦上讓您可以決定何種失敗想 hello 叢集 toosurvive。</span><span class="sxs-lookup"><span data-stu-id="7d990-106">You are about toocreate a Service Fabric cluster on machines you own, so you can decide what kinds of failures you want hello cluster toosurvive.</span></span> <span data-ttu-id="7d990-107">例如，您需要不同的電源線或網際網路連線提供 toothese 機器？</span><span class="sxs-lookup"><span data-stu-id="7d990-107">For example, do you need separate power lines or Internet connections supplied toothese machines?</span></span> <span data-ttu-id="7d990-108">此外，請考慮 hello 這些機器的實體安全性。</span><span class="sxs-lookup"><span data-stu-id="7d990-108">In addition, consider hello physical security of these machines.</span></span> <span data-ttu-id="7d990-109">Hello 機器位於何處，以及需要哪些人存取 toothem？</span><span class="sxs-lookup"><span data-stu-id="7d990-109">Where are hello machines located and who needs access toothem?</span></span> <span data-ttu-id="7d990-110">進行這些決定之後，您可以以邏輯方式對應 hello 機器 toohello （請參閱步驟 4） 的不同容錯網域。</span><span class="sxs-lookup"><span data-stu-id="7d990-110">After you make these decisions, you can logically map hello machines toohello various fault domains (see Step 4).</span></span> <span data-ttu-id="7d990-111">實際執行叢集規劃 hello 基礎結構會比測試叢集的更為複雜。</span><span class="sxs-lookup"><span data-stu-id="7d990-111">hello infrastructure planning for production clusters is more involved than for test clusters.</span></span>

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a><span data-ttu-id="7d990-112">步驟 2： 準備 hello 機器 toomeet hello 必要條件</span><span class="sxs-lookup"><span data-stu-id="7d990-112">Step 2: Prepare hello machines toomeet hello prerequisites</span></span>
<span data-ttu-id="7d990-113">每一部電腦的必要條件，您會想 tooadd toohello 叢集：</span><span class="sxs-lookup"><span data-stu-id="7d990-113">Prerequisites for each machine that you want tooadd toohello cluster:</span></span>

* <span data-ttu-id="7d990-114">建議至少 16 GB RAM。</span><span class="sxs-lookup"><span data-stu-id="7d990-114">A minimum of 16 GB of RAM is recommended.</span></span>
* <span data-ttu-id="7d990-115">建議至少 40 GB 的可用磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="7d990-115">A minimum of 40 of GB available disk space is recommended.</span></span>
* <span data-ttu-id="7d990-116">建議 4 核心或以上的 CPU。</span><span class="sxs-lookup"><span data-stu-id="7d990-116">A 4 core or greater CPU is recommended.</span></span>
* <span data-ttu-id="7d990-117">連線 tooa 安全的網路或網路上的所有機器。</span><span class="sxs-lookup"><span data-stu-id="7d990-117">Connectivity tooa secure network or networks for all machines.</span></span>
* <span data-ttu-id="7d990-118">Windows Server 2012 R2 或 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="7d990-118">Windows Server 2012 R2 or Windows Server 2016.</span></span> 
* <span data-ttu-id="7d990-119">[.NET Framework 4.5.1 或更高版本](https://www.microsoft.com/download/details.aspx?id=40773)，完整安裝。</span><span class="sxs-lookup"><span data-stu-id="7d990-119">[.NET Framework 4.5.1 or higher](https://www.microsoft.com/download/details.aspx?id=40773), full install.</span></span>
* <span data-ttu-id="7d990-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell)。</span><span class="sxs-lookup"><span data-stu-id="7d990-120">[Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).</span></span>
* <span data-ttu-id="7d990-121">hello[遠端登錄服務](https://technet.microsoft.com/library/cc754820)應該 hello 的所有電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="7d990-121">hello [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) should be running on all hello machines.</span></span>

<span data-ttu-id="7d990-122">hello 叢集系統管理員部署和設定 hello 叢集必須有[系統管理員權限](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx)每部 hello 電腦上。</span><span class="sxs-lookup"><span data-stu-id="7d990-122">hello cluster administrator deploying and configuring hello cluster must have [administrator privileges](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) on each of hello machines.</span></span> <span data-ttu-id="7d990-123">您無法在網域控制站上安裝 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="7d990-123">You cannot install Service Fabric on a domain controller.</span></span>

### <a name="step-3-determine-hello-initial-cluster-size"></a><span data-ttu-id="7d990-124">步驟 3： 決定 hello 最初的叢集大小</span><span class="sxs-lookup"><span data-stu-id="7d990-124">Step 3: Determine hello initial cluster size</span></span>
<span data-ttu-id="7d990-125">獨立 Service Fabric 叢集中的每個節點都 hello Service Fabric 執行階段部署，hello 叢集的成員。</span><span class="sxs-lookup"><span data-stu-id="7d990-125">Each node in a standalone Service Fabric cluster has hello Service Fabric runtime deployed and is a member of hello cluster.</span></span> <span data-ttu-id="7d990-126">在一般生產部署中，每個作業系統執行個體 (實體或虛擬) 都有一個節點。</span><span class="sxs-lookup"><span data-stu-id="7d990-126">In a typical production deployment, there is one node per OS instance (physical or virtual).</span></span> <span data-ttu-id="7d990-127">hello 叢集大小取決於您的業務需求。</span><span class="sxs-lookup"><span data-stu-id="7d990-127">hello cluster size is determined by your business needs.</span></span> <span data-ttu-id="7d990-128">不過，您必須有三個節點 (電腦或虛擬機器) 的最小叢集大小。</span><span class="sxs-lookup"><span data-stu-id="7d990-128">However, you must have a minimum cluster size of three nodes (machines or virtual machines).</span></span>
<span data-ttu-id="7d990-129">基於開發目的，在一部指定的電腦上可以有多個節點。</span><span class="sxs-lookup"><span data-stu-id="7d990-129">For development purposes, you can have more than one node on a given machine.</span></span> <span data-ttu-id="7d990-130">在生產環境中，對於每個實體或虛擬機器，Service Fabric 只支援一個節點。</span><span class="sxs-lookup"><span data-stu-id="7d990-130">In a production environment, Service Fabric supports only one node per physical or virtual machine.</span></span>

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a><span data-ttu-id="7d990-131">步驟 4： 決定 hello 數目容錯網域和升級網域</span><span class="sxs-lookup"><span data-stu-id="7d990-131">Step 4: Determine hello number of fault domains and upgrade domains</span></span>
<span data-ttu-id="7d990-132">A*容錯網域*(FD) 失敗的實體單位，而直接相關的 toohello hello 資料中心內實體基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7d990-132">A *fault domain* (FD) is a physical unit of failure and is directly related toohello physical infrastructure in hello data centers.</span></span> <span data-ttu-id="7d990-133">容錯網域是由共用單一失敗點的硬體元件 (電腦、交換器、網路等) 所組成。</span><span class="sxs-lookup"><span data-stu-id="7d990-133">A fault domain consists of hardware components (computers, switches, networks, and more) that share a single point of failure.</span></span> <span data-ttu-id="7d990-134">雖然容錯網域和機架之間沒有 1:1 對應，但是大致上來說，可以將每個機架視為一個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="7d990-134">Although there is no 1:1 mapping between fault domains and racks, loosely speaking, each rack can be considered a fault domain.</span></span> <span data-ttu-id="7d990-135">在考慮 hello 叢集中的節點時，我們強烈建議 hello 節點會散佈到至少三個容錯網域。</span><span class="sxs-lookup"><span data-stu-id="7d990-135">When considering hello nodes in your cluster, we strongly recommend that hello nodes be distributed among at least three fault domains.</span></span>

<span data-ttu-id="7d990-136">當您指定 Fd 如此時，您可以選擇每個 FD hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7d990-136">When you specify FDs in ClusterConfig.json, you can choose hello name for each FD.</span></span> <span data-ttu-id="7d990-137">Service Fabric 支援階層式 FD，因此，您可以在 FD 中反映您的基礎結構拓撲。</span><span class="sxs-lookup"><span data-stu-id="7d990-137">Service Fabric supports hierarchical FDs, so you can reflect your infrastructure topology in them.</span></span>  <span data-ttu-id="7d990-138">例如，下列 Fd hello 是有效的：</span><span class="sxs-lookup"><span data-stu-id="7d990-138">For example, hello following FDs are valid:</span></span>

* <span data-ttu-id="7d990-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span><span class="sxs-lookup"><span data-stu-id="7d990-139">"faultDomain": "fd:/Room1/Rack1/Machine1"</span></span>
* <span data-ttu-id="7d990-140">"faultDomain": "fd:/FD1"</span><span class="sxs-lookup"><span data-stu-id="7d990-140">"faultDomain": "fd:/FD1"</span></span>
* <span data-ttu-id="7d990-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span><span class="sxs-lookup"><span data-stu-id="7d990-141">"faultDomain": "fd:/Room1/Rack1/PDU1/M1"</span></span>

<span data-ttu-id="7d990-142">*升級網域* (UD) 是節點的邏輯單元。</span><span class="sxs-lookup"><span data-stu-id="7d990-142">An *upgrade domain* (UD) is a logical unit of nodes.</span></span> <span data-ttu-id="7d990-143">Service Fabric 協調在升級期間 （應用程式升級或叢集升級），UD 中的所有節點會都被降 tooperform hello 升級，但在其他 Ud 節點仍保持可用 tooserve 要求。</span><span class="sxs-lookup"><span data-stu-id="7d990-143">During Service Fabric orchestrated upgrades (either an application upgrade or a cluster upgrade), all nodes in a UD are taken down tooperform hello upgrade while nodes in other UDs remain available tooserve requests.</span></span> <span data-ttu-id="7d990-144">hello 您執行您的電腦的韌體升級不接受 Ud，因此您必須執行這些其中一個電腦一次。</span><span class="sxs-lookup"><span data-stu-id="7d990-144">hello firmware upgrades you perform on your machines do not honor UDs, so you must do them one machine at a time.</span></span>

<span data-ttu-id="7d990-145">hello 最簡單方式 toothink 有關這些概念是 tooconsider Fd hello 未計劃的失敗和單位 Ud 當做 hello 的計劃性維護的單位。</span><span class="sxs-lookup"><span data-stu-id="7d990-145">hello simplest way toothink about these concepts is tooconsider FDs as hello unit of unplanned failure and UDs as hello unit of planned maintenance.</span></span>

<span data-ttu-id="7d990-146">當您指定 Ud 如此時，您可以選擇每個 UD hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="7d990-146">When you specify UDs in ClusterConfig.json, you can choose hello name for each UD.</span></span> <span data-ttu-id="7d990-147">例如，下列名稱的 hello 是有效的：</span><span class="sxs-lookup"><span data-stu-id="7d990-147">For example, hello following names are valid:</span></span>

* <span data-ttu-id="7d990-148">"upgradeDomain": "UD0"</span><span class="sxs-lookup"><span data-stu-id="7d990-148">"upgradeDomain": "UD0"</span></span>
* <span data-ttu-id="7d990-149">"upgradeDomain": "UD1A"</span><span class="sxs-lookup"><span data-stu-id="7d990-149">"upgradeDomain": "UD1A"</span></span>
* <span data-ttu-id="7d990-150">"upgradeDomain": "DomainRed"</span><span class="sxs-lookup"><span data-stu-id="7d990-150">"upgradeDomain": "DomainRed"</span></span>
* <span data-ttu-id="7d990-151">"upgradeDomain": "Blue"</span><span class="sxs-lookup"><span data-stu-id="7d990-151">"upgradeDomain": "Blue"</span></span>

<span data-ttu-id="7d990-152">如需升級網域和容錯網域的詳細資訊，請參閱[描述 Service Fabric 叢集](service-fabric-cluster-resource-manager-cluster-description.md)。</span><span class="sxs-lookup"><span data-stu-id="7d990-152">For more detailed information on upgrade domains and fault domains, see [Describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md).</span></span>

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a><span data-ttu-id="7d990-153">步驟 5： 下載適用於 Windows Server hello Service Fabric 獨立封裝</span><span class="sxs-lookup"><span data-stu-id="7d990-153">Step 5: Download hello Service Fabric standalone package for Windows Server</span></span>
<span data-ttu-id="7d990-154">[下載連結的 Service Fabric 獨立封裝的 Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)並解壓縮 hello 封裝，任一 tooa 部署機器也就不是屬於 hello 叢集或 tooone 的 hello 機器將成為叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="7d990-154">[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) and unzip hello package, either tooa deployment machine that is not part of hello cluster, or tooone of hello machines that will be a part of your cluster.</span></span>

### <a name="step-6-modify-cluster-configuration"></a><span data-ttu-id="7d990-155">步驟 6︰修改叢集組態</span><span class="sxs-lookup"><span data-stu-id="7d990-155">Step 6: Modify cluster configuration</span></span>
<span data-ttu-id="7d990-156">toocreate 您擁有 toocreate 獨立叢集設定追蹤檔案，其中描述 hello 規格 hello 叢集的獨立叢集。</span><span class="sxs-lookup"><span data-stu-id="7d990-156">toocreate a standalone cluster you have toocreate a standalone cluster configuration ClusterConfig.json file, which describes hello specification of hello cluster.</span></span> <span data-ttu-id="7d990-157">您可以根據 hello 範本，請參閱下面的連結 hello hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="7d990-157">You can base hello configuration file on hello templates found at hello below link.</span></span> <br><span data-ttu-id="7d990-158">
[獨立叢集組態](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="7d990-158">
[Standalone Cluster Configurations](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<span data-ttu-id="7d990-159">如需這個檔案中的 hello 區段的詳細資訊，請參閱[獨立 Windows 叢集的組態設定](service-fabric-cluster-manifest.md)。</span><span class="sxs-lookup"><span data-stu-id="7d990-159">For details on hello sections in this file, see [Configuration settings for standalone Windows cluster](service-fabric-cluster-manifest.md).</span></span>

<span data-ttu-id="7d990-160">開啟其中一個 hello 追蹤檔案從您下載的 hello 封裝，並修改下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="7d990-160">Open one of hello ClusterConfig.json files from hello package you downloaded and modify hello following settings:</span></span>
| <span data-ttu-id="7d990-161">**組態設定**</span><span class="sxs-lookup"><span data-stu-id="7d990-161">**Configuration Setting**</span></span> | <span data-ttu-id="7d990-162">**說明**</span><span class="sxs-lookup"><span data-stu-id="7d990-162">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="7d990-163">**NodeTypes**</span><span class="sxs-lookup"><span data-stu-id="7d990-163">**NodeTypes**</span></span> |<span data-ttu-id="7d990-164">節點型別可讓您 tooseparate 成不同群組的叢集節點。</span><span class="sxs-lookup"><span data-stu-id="7d990-164">Node types allow you tooseparate your cluster nodes into various groups.</span></span> <span data-ttu-id="7d990-165">一個叢集至少必須有一個節點類型。</span><span class="sxs-lookup"><span data-stu-id="7d990-165">A cluster must have at least one NodeType.</span></span> <span data-ttu-id="7d990-166">在群組中的所有節點都有 hello 遵循共同的特性：</span><span class="sxs-lookup"><span data-stu-id="7d990-166">All nodes in a group have hello following common characteristics:</span></span> <br> <span data-ttu-id="7d990-167">**名稱**-這是 hello 節點類型名稱。</span><span class="sxs-lookup"><span data-stu-id="7d990-167">**Name** - This is hello node type name.</span></span> <br><span data-ttu-id="7d990-168">**Endpoint Ports** - 這些是與這個節點類型相關聯的各種具名端點 (連接埠)。</span><span class="sxs-lookup"><span data-stu-id="7d990-168">**Endpoint Ports** - These are various named end points (ports) that are associated with this node type.</span></span> <span data-ttu-id="7d990-169">您可以使用任何您想，只要未與此資訊清單中的其他任何項目發生衝突，並不存在於任何 hello 機器/VM 上執行的應用程式所使用的通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="7d990-169">You can use any port number that you wish, as long as they do not conflict with anything else in this manifest and are not already in use by any other application running on hello machine/VM.</span></span> <br> <span data-ttu-id="7d990-170">**放置屬性**-其中說明您用於作為位置限制 hello 系統服務或您的服務此節點類型的屬性。</span><span class="sxs-lookup"><span data-stu-id="7d990-170">**Placement Properties** - These describe properties for this node type that you use as placement constraints for hello system services or your services.</span></span> <span data-ttu-id="7d990-171">這些屬性是使用者定義的索引鍵/值組，可針對指定節點提供額外的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7d990-171">These properties are user-defined key/value pairs that provide extra meta data for a given node.</span></span> <span data-ttu-id="7d990-172">節點屬性的範例是 hello 節點是否有硬碟機或圖形卡、 hello 的磁針數中的硬碟機、 核心和其他實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="7d990-172">Examples of node properties would be whether hello node has a hard drive or graphics card, hello number of spindles in its hard drive, cores, and other physical properties.</span></span> <br> <span data-ttu-id="7d990-173">**容量**-節點容量定義 hello 名稱和特定資源數量確認特定的節點都有可供取用。</span><span class="sxs-lookup"><span data-stu-id="7d990-173">**Capacities** - Node capacities define hello name and amount of a particular resource that a particular node has available for consumption.</span></span> <span data-ttu-id="7d990-174">例如，節點可能會定義它具有名為 "MemoryInMb" 的度量容量，而且預設有 2048 MB 的可用記憶體。</span><span class="sxs-lookup"><span data-stu-id="7d990-174">For example, a node may define that it has capacity for a metric called “MemoryInMb” and that it has 2048 MB available by default.</span></span> <span data-ttu-id="7d990-175">這些容量會用在執行階段 tooensure，需要特定的大量資源的服務節點上的位置 hello，具有這些 hello 中可用的資源需要金額。</span><span class="sxs-lookup"><span data-stu-id="7d990-175">These capacities are used at runtime tooensure that services that require particular amounts of resources are placed on hello nodes that have those resources available in hello required amounts.</span></span><br><span data-ttu-id="7d990-176">**IsPrimary** -如果您有多個定義的 NodeType 確定只有一個已設定 hello 值 tooprimary *true*，也就是 services hello 系統執行。</span><span class="sxs-lookup"><span data-stu-id="7d990-176">**IsPrimary** - If you have more than one NodeType defined ensure that only one is set tooprimary with hello value *true*, which is where hello system services run.</span></span> <span data-ttu-id="7d990-177">所有其他節點型別應該設定 toohello 值*false*</span><span class="sxs-lookup"><span data-stu-id="7d990-177">All other node types should be set toohello value *false*</span></span> |
| <span data-ttu-id="7d990-178">**Nodes**</span><span class="sxs-lookup"><span data-stu-id="7d990-178">**Nodes**</span></span> |<span data-ttu-id="7d990-179">這些是 hello 的每個屬於 hello 叢集 （節點型別、 節點名稱、 IP 位址、 容錯網域和升級網域的 hello 節點） 的 hello 節點的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7d990-179">These are hello details for each of hello nodes that are part of hello cluster (node type, node name, IP address, fault domain, and upgrade domain of hello node).</span></span> <span data-ttu-id="7d990-180">hello 機器想 hello 叢集 toobe 需要 toobe 此處列出其 IP 位址上建立。</span><span class="sxs-lookup"><span data-stu-id="7d990-180">hello machines you want hello cluster toobe created on need toobe listed here with their IP addresses.</span></span> <br> <span data-ttu-id="7d990-181">如果您使用的 hello 建立所有 hello 節點，則其中一個方塊叢集相同的 IP 位址時，您可以基於測試目的使用。</span><span class="sxs-lookup"><span data-stu-id="7d990-181">If you use hello same IP address for all hello nodes, then a one-box cluster is created, which you can use for testing purposes.</span></span> <span data-ttu-id="7d990-182">不要使用一整體叢集部署生產工作負載。</span><span class="sxs-lookup"><span data-stu-id="7d990-182">Do not use One-box clusters for deploying production workloads.</span></span> |

<span data-ttu-id="7d990-183">Hello 叢集組態中有了所有設定 toohello 環境後，可以針對 hello （步驟 7） 的叢集環境進行測試。</span><span class="sxs-lookup"><span data-stu-id="7d990-183">After hello cluster configuration has had all settings configured toohello environment, it can be tested against hello cluster environment (step 7).</span></span>

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a><span data-ttu-id="7d990-184">步驟 7.</span><span class="sxs-lookup"><span data-stu-id="7d990-184">Step 7.</span></span> <span data-ttu-id="7d990-185">環境設定</span><span class="sxs-lookup"><span data-stu-id="7d990-185">Environment setup</span></span>

<span data-ttu-id="7d990-186">在叢集系統管理員設定獨立 Service Fabric 叢集，hello 環境時需要 toobe 設置 hello 下列準則：</span><span class="sxs-lookup"><span data-stu-id="7d990-186">When a cluster administrator configures a Service Fabric standalone cluster, hello environment is needs toobe set up with hello following criteria:</span></span> <br>
1. <span data-ttu-id="7d990-187">建立 hello 叢集的 hello 使用者必須具備系統管理員層級的安全性權限 tooall 機器列為 hello 叢集組態檔中的節點。</span><span class="sxs-lookup"><span data-stu-id="7d990-187">hello user creating hello cluster should have administrator-level security privileges tooall machines that are listed as nodes in hello cluster configuration file.</span></span>
2. <span data-ttu-id="7d990-188">電腦中的 hello 建立叢集，以及每個叢集節點電腦必須：</span><span class="sxs-lookup"><span data-stu-id="7d990-188">Machine from which hello cluster is created, as well as each cluster node machine must:</span></span>
* <span data-ttu-id="7d990-189">已將 Service Fabric SDK 解除安裝</span><span class="sxs-lookup"><span data-stu-id="7d990-189">Have Service Fabric SDK uninstalled</span></span>
* <span data-ttu-id="7d990-190">已將 Service Fabric 執行階段解除安裝</span><span class="sxs-lookup"><span data-stu-id="7d990-190">Have Service Fabric runtime uninstalled</span></span> 
* <span data-ttu-id="7d990-191">Hello Windows 防火牆服務 (mpssvc) 啟用</span><span class="sxs-lookup"><span data-stu-id="7d990-191">Have hello Windows Firewall service (mpssvc) enabled</span></span>
* <span data-ttu-id="7d990-192">已啟用的 hello 遠端登錄服務 (remoteregistry)</span><span class="sxs-lookup"><span data-stu-id="7d990-192">Have hello Remote Registry Service (remoteregistry) enabled</span></span>
* <span data-ttu-id="7d990-193">已啟用檔案共用 (SMB)</span><span class="sxs-lookup"><span data-stu-id="7d990-193">Have file sharing (SMB) enabled</span></span>
* <span data-ttu-id="7d990-194">已根據叢集組態的連接埠，開啟必要的連接埠</span><span class="sxs-lookup"><span data-stu-id="7d990-194">Have necessary ports opened, based on cluster configuration ports</span></span>
* <span data-ttu-id="7d990-195">已經開啟 Windows SMB 和遠端登錄服務的必要通訊埠︰135、137、138、139 和 445</span><span class="sxs-lookup"><span data-stu-id="7d990-195">Have necessary ports opened for Windows SMB and Remote Registry service: 135, 137, 138, 139, and 445</span></span>
* <span data-ttu-id="7d990-196">具有網路連線 tooone 另一個</span><span class="sxs-lookup"><span data-stu-id="7d990-196">Have network connectivity tooone another</span></span>
3. <span data-ttu-id="7d990-197">無 hello 叢集節點電腦應該是網域控制站。</span><span class="sxs-lookup"><span data-stu-id="7d990-197">None of hello cluster node machines should be a Domain Controller.</span></span>
4. <span data-ttu-id="7d990-198">如果部署的 hello 叢集 toobe 是安全的叢集，驗證 hello 必要條件已位置，以及針對 hello 組態已正確設定必要的安全性。</span><span class="sxs-lookup"><span data-stu-id="7d990-198">If hello cluster toobe deployed is a secure cluster, validate hello necessary security prerequisites are in place, and are configured correctly against hello configuration.</span></span>
5. <span data-ttu-id="7d990-199">Hello 叢集機器並不是可存取網際網路時，如果在 hello 組 hello 下列叢集設定：</span><span class="sxs-lookup"><span data-stu-id="7d990-199">If hello cluster machines are not internet-accessible, set hello following in hello cluster configuration:</span></span>
* <span data-ttu-id="7d990-200">停用遙測：在 *properties* 下設定 *"enableTelemetry": false*</span><span class="sxs-lookup"><span data-stu-id="7d990-200">Disable telemetry:   Under *properties* set   *"enableTelemetry": false*</span></span>
* <span data-ttu-id="7d990-201">停用自動網狀架構版本下載該 hello 目前叢集版本即將結束支援的通知： 下*屬性*設定*"fabricClusterAutoupgradeEnabled": false*</span><span class="sxs-lookup"><span data-stu-id="7d990-201">Disable automatic Fabric version downloading & notifications that hello current cluster version is nearing end of support:   Under *properties* set   *"fabricClusterAutoupgradeEnabled": false*</span></span>
* <span data-ttu-id="7d990-202">或者如果有限的 toowhite 列出網域網路存取網際網路，以下的 hello 網域所需的自動升級： go.microsoft.com download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7d990-202">Alternatively if network internet access is limited toowhite-listed domains, hello domains below are required for automatic upgrade:   go.microsoft.com   download.microsoft.com</span></span>

6. <span data-ttu-id="7d990-203">設定適當的 Service Fabric 防毒排除項目︰</span><span class="sxs-lookup"><span data-stu-id="7d990-203">Set appropriate Service Fabric antivirus exclusions:</span></span>

| <span data-ttu-id="7d990-204">**防毒排除目錄**</span><span class="sxs-lookup"><span data-stu-id="7d990-204">**Antivirus Excluded directories**</span></span> |
| --- |
| <span data-ttu-id="7d990-205">Program Files\Microsoft Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7d990-205">Program Files\Microsoft Service Fabric</span></span> |
| <span data-ttu-id="7d990-206">FabricDataRoot (從叢集組態)</span><span class="sxs-lookup"><span data-stu-id="7d990-206">FabricDataRoot (from cluster configuration)</span></span> |
| <span data-ttu-id="7d990-207">FabricLogRoot (從叢集組態)</span><span class="sxs-lookup"><span data-stu-id="7d990-207">FabricLogRoot (from cluster configuration)</span></span> |

| <span data-ttu-id="7d990-208">**防毒排除處理序**</span><span class="sxs-lookup"><span data-stu-id="7d990-208">**Antivirus Excluded processes**</span></span> |
| --- |
| <span data-ttu-id="7d990-209">Fabric.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-209">Fabric.exe</span></span> |
| <span data-ttu-id="7d990-210">FabricHost.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-210">FabricHost.exe</span></span> |
| <span data-ttu-id="7d990-211">FabricInstallerService.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-211">FabricInstallerService.exe</span></span> |
| <span data-ttu-id="7d990-212">FabricSetup.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-212">FabricSetup.exe</span></span> |
| <span data-ttu-id="7d990-213">FabricDeployer.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-213">FabricDeployer.exe</span></span> |
| <span data-ttu-id="7d990-214">ImageBuilder.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-214">ImageBuilder.exe</span></span> |
| <span data-ttu-id="7d990-215">FabricGateway.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-215">FabricGateway.exe</span></span> |
| <span data-ttu-id="7d990-216">FabricDCA.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-216">FabricDCA.exe</span></span> |
| <span data-ttu-id="7d990-217">FabricFAS.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-217">FabricFAS.exe</span></span> |
| <span data-ttu-id="7d990-218">FabricUOS.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-218">FabricUOS.exe</span></span> |
| <span data-ttu-id="7d990-219">FabricRM.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-219">FabricRM.exe</span></span> |
| <span data-ttu-id="7d990-220">FileStoreService.exe</span><span class="sxs-lookup"><span data-stu-id="7d990-220">FileStoreService.exe</span></span> |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a><span data-ttu-id="7d990-221">步驟 8。</span><span class="sxs-lookup"><span data-stu-id="7d990-221">Step 8.</span></span> <span data-ttu-id="7d990-222">使用 TestConfiguration 指令碼驗證環境</span><span class="sxs-lookup"><span data-stu-id="7d990-222">Validate environment using TestConfiguration script</span></span>
<span data-ttu-id="7d990-223">hello 獨立封裝中可以找到 hello TestConfiguration.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7d990-223">hello TestConfiguration.ps1 script can be found in hello standalone package.</span></span> <span data-ttu-id="7d990-224">它是做為最佳做法分析程式 toovalidate 上述 hello 條件部分，應該用於為例行性檢查 toovalidate 是否可供指定的環境上部署叢集。</span><span class="sxs-lookup"><span data-stu-id="7d990-224">It is used as a Best Practices Analyzer toovalidate some of hello criteria above and should be used as a sanity check toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="7d990-225">如果有任何失敗，請參閱底下 toohello 清單[環境設定](service-fabric-cluster-standalone-deployment-preparation.md)進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="7d990-225">If there is any failure, refer toohello list under [Environment Setup](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting.</span></span> 

<span data-ttu-id="7d990-226">此指令碼可以在任何電腦具有系統管理員存取 tooall hello 機器列為 hello 叢集組態檔中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="7d990-226">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="7d990-227">hello 機器上執行此指令碼並沒有 toobe hello 叢集的一部分。</span><span class="sxs-lookup"><span data-stu-id="7d990-227">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

<span data-ttu-id="7d990-228">目前此組態的測試模組並不會驗證 hello 安全性設定，因此這會有 toobe 獨立完成。</span><span class="sxs-lookup"><span data-stu-id="7d990-228">Currently this configuration testing module does not validate hello security configuration so this has toobe done independently.</span></span>  

> [!NOTE]
> <span data-ttu-id="7d990-229">我們會持續改良 toomake 此模組來說更為完整，因此如果沒有錯誤或遺漏案例您認為這不目前攔截 TestConfiguration，請讓我們知道透過我們[支援通道](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)。</span><span class="sxs-lookup"><span data-stu-id="7d990-229">We are continually making improvements toomake this module more robust, so if there is a faulty or missing case which you believe isn't currently caught by TestConfiguration, please let us know through our [support channels](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>   
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7d990-230">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d990-230">Next steps</span></span>
* [<span data-ttu-id="7d990-231">建立在 Windows Server 上執行的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="7d990-231">Create a standalone cluster running on Windows Server</span></span>](service-fabric-cluster-creation-for-windows-server.md)
