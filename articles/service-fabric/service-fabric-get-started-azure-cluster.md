---
title: "設定 Azure Service Fabric 叢集 | Microsoft Docs"
description: "快速入門 - 在 Azure 上建立 Windows 或 Linux Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="94d45-103">在 Azure 上建立您的第一個 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="94d45-104">[Service Fabric 叢集](service-fabric-deploy-anywhere.md)是一組由網路連接的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。</span><span class="sxs-lookup"><span data-stu-id="94d45-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="94d45-105">此快速入門可協助您建立包含五個節點的叢集，在短短幾分鐘內透過 [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) 或 [Azure 入口網站](http://portal.azure.com)在 Windows 或 Linux 上執行該叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-105">This quickstart helps you to create a five-node cluster, running on either Windows or Linux, through the [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="94d45-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="94d45-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-the-azure-portal"></a><span data-ttu-id="94d45-107">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="94d45-107">Use the Azure portal</span></span>

<span data-ttu-id="94d45-108">登入 Azure 入口網站，網址是 [http://portal.azure.com](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="94d45-108">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-the-cluster"></a><span data-ttu-id="94d45-109">建立叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-109">Create the cluster</span></span>

1. <span data-ttu-id="94d45-110">按一下 Azure 入口網站左上角的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="94d45-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="94d45-111">選取 [新增] 刀鋒視窗中的 [計算]，然後選取 [計算] 刀鋒視窗中的 [Service Fabric 叢集]。</span><span class="sxs-lookup"><span data-stu-id="94d45-111">Select **Compute** from the **New** blade and then select **Service Fabric Cluster** from the **Compute** blade.</span></span>
3. <span data-ttu-id="94d45-112">填妥 Service Fabric 的 [基本資料] 表單。</span><span class="sxs-lookup"><span data-stu-id="94d45-112">Fill out the Service Fabric **Basics** form.</span></span> <span data-ttu-id="94d45-113">針對 [作業系統]，選取您希望叢集節點執行的 Windows 或 Linux 版本。</span><span class="sxs-lookup"><span data-stu-id="94d45-113">For **Operating system**, select the version of Windows or Linux you want the cluster nodes to run.</span></span> <span data-ttu-id="94d45-114">在此輸入的使用者名稱和密碼用於登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="94d45-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="94d45-115">對於 [資源群組]，建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="94d45-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="94d45-116">資源群組是在其中建立和共同管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="94d45-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="94d45-117">完成時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="94d45-117">When complete, click **OK**.</span></span>

    ![叢集設定輸出][cluster-setup-basics]

4. <span data-ttu-id="94d45-119">填妥 [叢集組態] 表單。</span><span class="sxs-lookup"><span data-stu-id="94d45-119">Fill out the **Cluster configuration** form.</span></span>  <span data-ttu-id="94d45-120">對於 [節點類型計數]，請輸入"1"。</span><span class="sxs-lookup"><span data-stu-id="94d45-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="94d45-121">選取 [節點類型 1 (主要)] 並填妥 [節點類型組態] 表單。</span><span class="sxs-lookup"><span data-stu-id="94d45-121">Select **Node type 1 (Primary)** and fill out the **Node type configuration** form.</span></span>  <span data-ttu-id="94d45-122">輸入節點類型名稱並將[持久性層](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster)設定為「銅級」。</span><span class="sxs-lookup"><span data-stu-id="94d45-122">Enter a node type name and set the [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) to "Bronze."</span></span>  <span data-ttu-id="94d45-123">選取 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="94d45-123">Select a VM size.</span></span>

    <span data-ttu-id="94d45-124">節點類型可定義 VM 大小、VM 數目、自訂端點，以及該類型 VM 的其他設定。</span><span class="sxs-lookup"><span data-stu-id="94d45-124">Node types define the VM size, number of VMs, custom endpoints, and other settings for the VMs of that type.</span></span> <span data-ttu-id="94d45-125">所定義的每個節點類型都會設定為不同的虛擬機器擴展集，以便用集合形式部署和管理虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="94d45-125">Each node type defined is set up as a separate virtual machine scale set, which is used to deploy and managed virtual machines as a set.</span></span> <span data-ttu-id="94d45-126">每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量計量。</span><span class="sxs-lookup"><span data-stu-id="94d45-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="94d45-127">第一個 (或主要) 節點類型就是 Service Fabric 系統服務所在的節點類型，且必須具有 5 部或更多部 VM。</span><span class="sxs-lookup"><span data-stu-id="94d45-127">The first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="94d45-128">對於任何生產部署而言，[容量規劃](service-fabric-cluster-capacity.md)都是一個很重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="94d45-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="94d45-129">不過，在此快速入門中，您不會執行應用程式，因此選取 DS1_v2 Standard VM 大小。</span><span class="sxs-lookup"><span data-stu-id="94d45-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="94d45-130">針對[可靠性層](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster)選取「銀級」，並將初始虛擬機器擴展集容量設定為 5。</span><span class="sxs-lookup"><span data-stu-id="94d45-130">Select "Silver" for the [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="94d45-131">自訂端點會在 Azure Load Balancer 中開啟連接埠，以便與在叢集上執行的應用程式連線。</span><span class="sxs-lookup"><span data-stu-id="94d45-131">Custom endpoints open up ports in the Azure load balancer so that you can connect with applications running on the cluster.</span></span>  <span data-ttu-id="94d45-132">輸入 "80, 8172" 以開啟連接埠 80 和 8172。</span><span class="sxs-lookup"><span data-stu-id="94d45-132">Enter "80, 8172" to open up ports 80 and 8172.</span></span>

    <span data-ttu-id="94d45-133">請勿核取 [進行進階設定] 方塊中，其用於自訂 TCP/HTTP 管理端點、應用程式連接埠範圍、[放置條件約束](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints)和[容量屬性](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="94d45-133">Do not check the **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="94d45-134">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="94d45-134">Select **OK**.</span></span>

6. <span data-ttu-id="94d45-135">在 [叢集組態] 表單中，將 [診斷] 設定為 [開啟]。</span><span class="sxs-lookup"><span data-stu-id="94d45-135">In the **Cluster configuration** form, set **Diagnostics** to **On**.</span></span>  <span data-ttu-id="94d45-136">在此快速入門中，您不需要輸入任何 [Fabric 設定](service-fabric-cluster-fabric-settings.md)屬性。</span><span class="sxs-lookup"><span data-stu-id="94d45-136">For this quickstart, you do not need to enter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="94d45-137">在 [Fabric 版本] 中，選取 [自動] 升級模式，以便 Microsoft 自動更新執行叢集的 Fabric 程式碼版本。</span><span class="sxs-lookup"><span data-stu-id="94d45-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates the version of the fabric code running the cluster.</span></span>  <span data-ttu-id="94d45-138">如果您想要[選擇支援的版本](service-fabric-cluster-upgrade.md) (升級目標)，請將模式設定為 [手動] 。</span><span class="sxs-lookup"><span data-stu-id="94d45-138">Set the mode to **Manual** if you want to [choose a supported version](service-fabric-cluster-upgrade.md) to upgrade to.</span></span> 

    ![節點類型組態][node-type-config]

    <span data-ttu-id="94d45-140">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="94d45-140">Select **OK**.</span></span>

7. <span data-ttu-id="94d45-141">填妥 [安全性] 表單。</span><span class="sxs-lookup"><span data-stu-id="94d45-141">Fill out the **Security** form.</span></span>  <span data-ttu-id="94d45-142">在此快速入門中選取 [不安全]。</span><span class="sxs-lookup"><span data-stu-id="94d45-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="94d45-143">強烈建議您針對生產工作負載建立一個安全的叢集，因為任何人都可以用匿名方式連線到不安全的叢集並執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="94d45-143">It is highly recommended to create a secure cluster for production workloads, however, since anyone can anonymously connect to an unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="94d45-144">憑證是在 Service Fabric 中用來提供驗證與加密，以保護叢集和其應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="94d45-144">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="94d45-145">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="94d45-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="94d45-146">若要使用 Azure Active Directory 進行使用者驗證，或為了應用程式安全性設定憑證，請參閱[從 Resource Manager 範本建立叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="94d45-146">To enable user authentication using Azure Active Directory or to set up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="94d45-147">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="94d45-147">Select **OK**.</span></span>

8. <span data-ttu-id="94d45-148">檢閱摘要。</span><span class="sxs-lookup"><span data-stu-id="94d45-148">Review the summary.</span></span>  <span data-ttu-id="94d45-149">如果您想要下載從您輸入的設定建立的 Resource Manager 範本，請選取 [下載範本和參數]。</span><span class="sxs-lookup"><span data-stu-id="94d45-149">If you'd like to download a Resource Manager template built from the settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="94d45-150">選取 [建立] 以建立叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-150">Select **Create** to create the cluster.</span></span>

    <span data-ttu-id="94d45-151">您可以在通知功能中看到叢集的建立進度。</span><span class="sxs-lookup"><span data-stu-id="94d45-151">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="94d45-152">(請按一下畫面右上角狀態列附近的鈴噹圖示。)如果您在建立叢集時按了 [釘選到「開始面板」]，您會看到 [部署 Service Fabric 叢集] 已釘選到 [開始] 面板。</span><span class="sxs-lookup"><span data-stu-id="94d45-152">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="94d45-153">檢視叢集狀態</span><span class="sxs-lookup"><span data-stu-id="94d45-153">View cluster status</span></span>
<span data-ttu-id="94d45-154">建立叢集之後，您就可以在入口網站的 [概觀] 刀鋒視窗中檢查您的叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-154">Once your cluster is created, you can inspect your cluster in the **Overview** blade in the portal.</span></span> <span data-ttu-id="94d45-155">現在儀表板會顯示叢集的詳細資料，包括叢集的公用端點和 Service Fabric Explorer 的連結。</span><span class="sxs-lookup"><span data-stu-id="94d45-155">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

![叢集狀態][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="94d45-157">使用 Service Fabric Explorer 將叢集視覺化</span><span class="sxs-lookup"><span data-stu-id="94d45-157">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="94d45-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個理想的工具，可將叢集視覺化及管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="94d45-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="94d45-159">Service Fabric Explorer 是在叢集中執行的一項服務。</span><span class="sxs-lookup"><span data-stu-id="94d45-159">Service Fabric Explorer is a service that runs in the cluster.</span></span>  <span data-ttu-id="94d45-160">按一下入口網站中叢集 [概觀]頁面 的 [Service Fabric Explorer] 連結，即可使用網頁瀏覽器進行存取。</span><span class="sxs-lookup"><span data-stu-id="94d45-160">Access it using a web browser by clicking the **Service Fabric Explorer** link of the cluster **Overview** page in the portal.</span></span>  <span data-ttu-id="94d45-161">您也可以直接在瀏覽器中輸入位址︰[http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="94d45-161">You can also enter the address directly into the browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="94d45-162">叢集儀表板會提供您叢集的概觀，包括應用程式和節點健康情況的摘要。</span><span class="sxs-lookup"><span data-stu-id="94d45-162">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="94d45-163">節點檢視會顯示叢集的實體配置。</span><span class="sxs-lookup"><span data-stu-id="94d45-163">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="94d45-164">對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="94d45-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a><span data-ttu-id="94d45-166">使用 PowerShell 連線到叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-166">Connect to the cluster using PowerShell</span></span>
<span data-ttu-id="94d45-167">使用 PowerShell 進行連線，以確認叢集正在執行。</span><span class="sxs-lookup"><span data-stu-id="94d45-167">Verify that the cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="94d45-168">ServiceFabric PowerShell 模組會隨著 [Service Fabric SDK](service-fabric-get-started.md) 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="94d45-168">The ServiceFabric PowerShell module is installed with the [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="94d45-169">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) Cmdlet 會建立叢集連線。</span><span class="sxs-lookup"><span data-stu-id="94d45-169">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="94d45-170">如需連線到叢集的其他範例，請參閱[連線到安全的叢集](service-fabric-connect-to-secure-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="94d45-170">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="94d45-171">連線到叢集之後，使用 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) Cmdlet 來顯示叢集中的節點清單以及每個節點的狀態資訊。</span><span class="sxs-lookup"><span data-stu-id="94d45-171">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="94d45-172">每個節點的 **HealthState** 應該為「正常」。</span><span class="sxs-lookup"><span data-stu-id="94d45-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-the-cluster"></a><span data-ttu-id="94d45-173">移除叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-173">Remove the cluster</span></span>
<span data-ttu-id="94d45-174">Service Fabric 叢集是由叢集資源本身和其他 Azure 資源所構成。</span><span class="sxs-lookup"><span data-stu-id="94d45-174">A Service Fabric cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="94d45-175">因此，若要完全刪除 Service Fabric 叢集，您也必須刪除組成叢集的所有資源。</span><span class="sxs-lookup"><span data-stu-id="94d45-175">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span> <span data-ttu-id="94d45-176">刪除叢集及其取用之所有資源的最簡單方式，就是刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="94d45-176">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> <span data-ttu-id="94d45-177">如需刪除叢集或刪除資源群組中一些 (但並非全部) 資源的其他方式，請參閱[刪除叢集](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="94d45-177">For other ways to delete a cluster or to delete some (but not all) the resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="94d45-178">在 Azure 入口網站中刪除資源群組：</span><span class="sxs-lookup"><span data-stu-id="94d45-178">Delete a resource group in the Azure portal:</span></span>
1. <span data-ttu-id="94d45-179">瀏覽至您想要刪除的 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-179">Navigate to the Service Fabric cluster you want to delete.</span></span>
2. <span data-ttu-id="94d45-180">按一下叢集基本資訊頁面上的 [資源群組] 名稱。</span><span class="sxs-lookup"><span data-stu-id="94d45-180">Click the **Resource Group** name on the cluster essentials page.</span></span>
3. <span data-ttu-id="94d45-181">在 [資源群組基本資訊] 頁面中，按一下 [刪除資源群組] 並遵循該頁面上的指示，以完成資源群組的刪除。</span><span class="sxs-lookup"><span data-stu-id="94d45-181">In the **Resource Group Essentials** page, click **Delete resource group** and follow the instructions on that page to complete the deletion of the resource group.</span></span>
    <span data-ttu-id="94d45-182">![刪除資源群組][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="94d45-182">![Delete the resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a><span data-ttu-id="94d45-183">使用 Azure Powershell 來部署安全的叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-183">Use Azure Powershell to deploy a secure cluster</span></span>
1. <span data-ttu-id="94d45-184">在您的電腦下載 [Azure Powershell 模組 4.0 版或更新版本](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="94d45-184">Download the [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="94d45-185">開啟 Windows PowerShell 視窗並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="94d45-185">Open a Windows PowerShell window, Run the following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="94d45-186">您應該會看到如下所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="94d45-186">You should see an output similar to the following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="94d45-188">登入 Azure 並選取您要建立叢集的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="94d45-188">Login to Azure and Select the subscription to which you want to create the cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="94d45-189">執行下列命令，立即建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-189">Run the following command to now create a secure cluster.</span></span> <span data-ttu-id="94d45-190">別忘了自訂參數。</span><span class="sxs-lookup"><span data-stu-id="94d45-190">Do not forget to customize the parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="94d45-191">此命令可能需要 10 到 30 分鐘的時間才能完成，而在結束時，您應該會取得如下所示的輸出。</span><span class="sxs-lookup"><span data-stu-id="94d45-191">The command can take anywhere from 10 minutes to 30 minutes to complete, at the end of it, you should get an output similar to the following.</span></span> <span data-ttu-id="94d45-192">此輸出包含憑證相關資訊、憑證上傳至的 Key Vault，以及複製憑證的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="94d45-192">The output has information about the certificate, the KeyVault where it was uploaded to, and the local folder where the certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="94d45-194">複製整個輸出並儲存到文字檔，這是我們需要參考的資料。</span><span class="sxs-lookup"><span data-stu-id="94d45-194">Copy the entire output and save to a text file as we need to refer to it.</span></span> <span data-ttu-id="94d45-195">記下輸出中的下列資訊。</span><span class="sxs-lookup"><span data-stu-id="94d45-195">Make a note of the following information from the output.</span></span> 

    - <span data-ttu-id="94d45-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="94d45-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="94d45-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="94d45-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="94d45-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="94d45-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="94d45-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="94d45-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-the-certificate-on-your-local-machine"></a><span data-ttu-id="94d45-200">在本機電腦上安裝憑證</span><span class="sxs-lookup"><span data-stu-id="94d45-200">Install the certificate on your local machine</span></span>
  
<span data-ttu-id="94d45-201">若要連線到叢集，您需要將憑證安裝到目前使用者的個人 (My) 存放區。</span><span class="sxs-lookup"><span data-stu-id="94d45-201">To connect to the cluster, you need to install the certificate into the Personal (My) store of the current user.</span></span> 

<span data-ttu-id="94d45-202">執行下列 PowerShell</span><span class="sxs-lookup"><span data-stu-id="94d45-202">Run the following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="94d45-203">您現在即可連線到您安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-203">You are now ready to connect to your secure cluster.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="94d45-204">連線到安全的叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-204">Connect to a secure cluster</span></span> 

<span data-ttu-id="94d45-205">執行下列 PowerShell 命令來連線到安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-205">Run the following PowerShell command to connect to a secure cluster.</span></span> <span data-ttu-id="94d45-206">憑證詳細資料必須與用來設定叢集的憑證相符。</span><span class="sxs-lookup"><span data-stu-id="94d45-206">The certificate details must match a certificate that was used to set up the cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="94d45-207">下列範例顯示已完成的參數：</span><span class="sxs-lookup"><span data-stu-id="94d45-207">The following example shows the completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="94d45-208">執行下列命令來檢查您連線的叢集是否狀況良好。</span><span class="sxs-lookup"><span data-stu-id="94d45-208">Run the following command to check that you are connected and the cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a><span data-ttu-id="94d45-209">從 Visual Studio 將您的應用程式發佈至叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-209">Publish your apps to your cluster from Visual Studio</span></span>

<span data-ttu-id="94d45-210">您現在已設定好 Azure 叢集，即可依照[發佈至叢集](service-fabric-publish-app-remote-cluster.md)文件中所述，從 Visual Studio 將您的應用程式發佈至該叢集。</span><span class="sxs-lookup"><span data-stu-id="94d45-210">Now that you have set up an Azure cluster, you can publish your applications to it from Visual Studio by following the [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-the-cluster"></a><span data-ttu-id="94d45-211">移除叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-211">Remove the cluster</span></span>
<span data-ttu-id="94d45-212">叢集是由叢集資源本身和其他 Azure 資源所構成。</span><span class="sxs-lookup"><span data-stu-id="94d45-212">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="94d45-213">刪除叢集及其取用之所有資源的最簡單方式，就是刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="94d45-213">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="94d45-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94d45-214">Next steps</span></span>
<span data-ttu-id="94d45-215">您已設定好開發叢集，請嘗試下列作業︰</span><span class="sxs-lookup"><span data-stu-id="94d45-215">Now that you have set up a development cluster, try the following:</span></span>
* [<span data-ttu-id="94d45-216">在入口網站中建立安全的叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-216">Create a secure cluster in the portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="94d45-217">從範本建立叢集</span><span class="sxs-lookup"><span data-stu-id="94d45-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="94d45-218">使用 PowerShell 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="94d45-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
