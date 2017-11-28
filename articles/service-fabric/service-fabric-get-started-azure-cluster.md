---
title: "Azure Service Fabric 叢集 aaaSet |Microsoft 文件"
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
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="9c033-103">在 Azure 上建立您的第一個 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="9c033-104">[Service Fabric 叢集](service-fabric-deploy-anywhere.md)是一組由網路連接的虛擬或實體機器，可用來將您的微服務部署到其中並進行管理。</span><span class="sxs-lookup"><span data-stu-id="9c033-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="9c033-105">本快速入門可協助您 toocreate 五個節點的叢集，執行 Windows 或 Linux 上透過 hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248)或[Azure 入口網站](http://portal.azure.com)短短幾分鐘內。</span><span class="sxs-lookup"><span data-stu-id="9c033-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="9c033-106">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="9c033-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="9c033-107">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9c033-107">Use hello Azure portal</span></span>

<span data-ttu-id="9c033-108">登入 toohello 在 Azure 入口網站[http://portal.azure.com](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="9c033-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="9c033-109">建立 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-109">Create hello cluster</span></span>

1. <span data-ttu-id="9c033-110">按一下 hello**新增**hello 的左上角 hello Azure 入口網站上找到的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9c033-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="9c033-111">選取**計算**從 hello**新增**刀鋒視窗，然後選取**Service Fabric 叢集**從 hello**計算**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c033-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="9c033-112">填寫 hello Service Fabric**基本概念**表單。</span><span class="sxs-lookup"><span data-stu-id="9c033-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="9c033-113">如**作業系統**，選取為 Windows 或 Linux 想 hello 叢集節點 toorun hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9c033-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="9c033-114">在此輸入 hello 使用者名稱和密碼是使用的 toolog toohello 虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="9c033-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="9c033-115">對於 [資源群組]，建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c033-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="9c033-116">資源群組是在其中建立和共同管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="9c033-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="9c033-117">完成時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9c033-117">When complete, click **OK**.</span></span>

    ![叢集設定輸出][cluster-setup-basics]

4. <span data-ttu-id="9c033-119">填寫 hello**叢集設定**表單。</span><span class="sxs-lookup"><span data-stu-id="9c033-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="9c033-120">對於 [節點類型計數]，請輸入"1"。</span><span class="sxs-lookup"><span data-stu-id="9c033-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="9c033-121">選取**節點類型 1 （主要）**然後填寫 hello**節點型別設定**表單。</span><span class="sxs-lookup"><span data-stu-id="9c033-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="9c033-122">輸入節點型別名稱，並設定 hello[持久性層](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster)太"銅。 」</span><span class="sxs-lookup"><span data-stu-id="9c033-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="9c033-123">選取 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="9c033-123">Select a VM size.</span></span>

    <span data-ttu-id="9c033-124">節點型別定義 hello VM 大小的 Vm，自訂的端點數目，和其他設定 hello 該類型的 Vm。</span><span class="sxs-lookup"><span data-stu-id="9c033-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="9c033-125">定義每個節點型別設定為不同的虛擬機器規模集，也就是使用的 toodeploy 和受管理的虛擬機器所設定。</span><span class="sxs-lookup"><span data-stu-id="9c033-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="9c033-126">每個節點類型可以獨立相應增加或相應減少，可以開啟不同組的連接埠，並可以有不同的容量計量。</span><span class="sxs-lookup"><span data-stu-id="9c033-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="9c033-127">hello 第一次，或主要節點類型是服務網狀架構系統服務會裝載和必須有五個或多個 Vm 的位置。</span><span class="sxs-lookup"><span data-stu-id="9c033-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="9c033-128">對於任何生產部署而言，[容量規劃](service-fabric-cluster-capacity.md)都是一個很重要的步驟。</span><span class="sxs-lookup"><span data-stu-id="9c033-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="9c033-129">不過，在此快速入門中，您不會執行應用程式，因此選取 DS1_v2 Standard VM 大小。</span><span class="sxs-lookup"><span data-stu-id="9c033-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="9c033-130">選取 「 銀級 」 hello[可靠性層](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster)和初始虛擬機器規模集容量是 5。</span><span class="sxs-lookup"><span data-stu-id="9c033-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="9c033-131">自訂端點開啟 hello Azure 負載平衡器中的連接埠，以便您可以在 hello 叢集上執行的應用程式連接。</span><span class="sxs-lookup"><span data-stu-id="9c033-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="9c033-132">輸入連接埠 80 和 8172"80，8172"tooopen。</span><span class="sxs-lookup"><span data-stu-id="9c033-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="9c033-133">不會檢查 hello**設定進階設定** 方塊中，用於自訂 TCP/HTTP 管理端點，應用程式連接埠範圍，[位置條件約束](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints)，和[容量屬性](service-fabric-cluster-resource-manager-metrics.md)。</span><span class="sxs-lookup"><span data-stu-id="9c033-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="9c033-134">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9c033-134">Select **OK**.</span></span>

6. <span data-ttu-id="9c033-135">在 hello**叢集設定**表單中，設定**診斷**太**上**。</span><span class="sxs-lookup"><span data-stu-id="9c033-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="9c033-136">本快速入門中，您就不需要 tooenter 任何[網狀架構設定](service-fabric-cluster-fabric-settings.md)屬性。</span><span class="sxs-lookup"><span data-stu-id="9c033-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="9c033-137">在**Fabric 版本**，選取**自動**升級模式，以便讓 Microsoft 自動更新 hello hello 網狀架構程式碼執行 hello 叢集版本。</span><span class="sxs-lookup"><span data-stu-id="9c033-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="9c033-138">將 hello 模式設定為太**手動**如果您想太[選擇支援的版本](service-fabric-cluster-upgrade.md)tooupgrade 至。</span><span class="sxs-lookup"><span data-stu-id="9c033-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![節點類型組態][node-type-config]

    <span data-ttu-id="9c033-140">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9c033-140">Select **OK**.</span></span>

7. <span data-ttu-id="9c033-141">填寫 hello**安全性**表單。</span><span class="sxs-lookup"><span data-stu-id="9c033-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="9c033-142">在此快速入門中選取 [不安全]。</span><span class="sxs-lookup"><span data-stu-id="9c033-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="9c033-143">它強烈建議使用 toocreate 安全的叢集，針對生產工作負載，不過，因為任何人都可以匿名連接 tooan 不安全的叢集，並執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="9c033-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="9c033-144">憑證用於 Service Fabric tooprovide 驗證和加密 toosecure 叢集，而它的應用程式的各個層面。</span><span class="sxs-lookup"><span data-stu-id="9c033-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="9c033-145">如需如何在 Service Fabric 中使用憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例](service-fabric-cluster-security.md)。</span><span class="sxs-lookup"><span data-stu-id="9c033-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="9c033-146">tooenable 使用者驗證應用程式安全性為使用 Azure Active Directory 或憑證 tooset[從資源管理員範本建立叢集](service-fabric-cluster-creation-via-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="9c033-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="9c033-147">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9c033-147">Select **OK**.</span></span>

8. <span data-ttu-id="9c033-148">檢閱 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="9c033-148">Review hello summary.</span></span>  <span data-ttu-id="9c033-149">如果您想要 toodownload 輸入從 hello 設定所建立的資源管理員範本，請選取**下載範本和參數**。</span><span class="sxs-lookup"><span data-stu-id="9c033-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="9c033-150">選取**建立**toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9c033-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="9c033-151">您可以看到在 hello 通知 hello 建立進度。</span><span class="sxs-lookup"><span data-stu-id="9c033-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="9c033-152">（按一下 hello 狀態列會在 hello 右上角螢幕附近的 hello"鈴鐺 」 圖示）。如果您按下**Pin tooStartboard**同時建立 hello 叢集，您會看到**部署 Service Fabric 叢集**釘選 toohello**啟動**面板。</span><span class="sxs-lookup"><span data-stu-id="9c033-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="9c033-153">檢視叢集狀態</span><span class="sxs-lookup"><span data-stu-id="9c033-153">View cluster status</span></span>
<span data-ttu-id="9c033-154">一旦建立您的叢集，您可以檢查您的叢集在 hello**概觀**hello 入口網站中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9c033-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="9c033-155">您現在可以看到您的叢集 hello 儀表板，包括 hello 叢集的公用端點及連結 tooService Fabric 總管中的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9c033-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![叢集狀態][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="9c033-157">使用 Service Fabric 總管 中的 hello 叢集以視覺化方式檢視</span><span class="sxs-lookup"><span data-stu-id="9c033-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="9c033-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) 是一個理想的工具，可將叢集視覺化及管理應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c033-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="9c033-159">Service Fabric 總管是 hello 叢集中執行的服務。</span><span class="sxs-lookup"><span data-stu-id="9c033-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="9c033-160">Hello，即可使用網頁瀏覽器存取**Service Fabric 總管**hello 叢集的連結**概觀**hello 入口網站頁面中的。</span><span class="sxs-lookup"><span data-stu-id="9c033-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="9c033-161">您也可以直接在 hello 瀏覽器輸入 hello 位址： [http://quickstartcluster.westus.cloudapp.azure.com:19080/總管](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="9c033-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="9c033-162">hello 叢集儀表板提供您的叢集，包括應用程式和節點健全狀況摘要的概觀。</span><span class="sxs-lookup"><span data-stu-id="9c033-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="9c033-163">hello 節點檢視會顯示 hello 實體 hello 叢集配置。</span><span class="sxs-lookup"><span data-stu-id="9c033-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="9c033-164">對於指定的節點，您可以檢查已經在該節點上部署程式碼的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c033-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="9c033-166">Toohello 叢集使用 PowerShell 連線</span><span class="sxs-lookup"><span data-stu-id="9c033-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="9c033-167">請確認該 hello 叢集正在執行使用 PowerShell 連線。</span><span class="sxs-lookup"><span data-stu-id="9c033-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="9c033-168">hello ServiceFabric PowerShell 模組會隨 hello [Service Fabric SDK](service-fabric-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9c033-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="9c033-169">hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet 建立連線 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="9c033-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="9c033-170">請參閱[連接 tooa 安全叢集](service-fabric-connect-to-secure-cluster.md)連接 tooa 叢集的其他範例。</span><span class="sxs-lookup"><span data-stu-id="9c033-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="9c033-171">在連接 toohello 叢集中之後, 使用 hello [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 叢集和狀態資訊的每個節點中的節點清單。</span><span class="sxs-lookup"><span data-stu-id="9c033-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="9c033-172">每個節點的 **HealthState** 應該為「正常」。</span><span class="sxs-lookup"><span data-stu-id="9c033-172">**HealthState** should be *OK* for each node.</span></span>

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

### <a name="remove-hello-cluster"></a><span data-ttu-id="9c033-173">移除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-173">Remove hello cluster</span></span>
<span data-ttu-id="9c033-174">Service Fabric 叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。</span><span class="sxs-lookup"><span data-stu-id="9c033-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="9c033-175">因此 toocompletely 刪除 Service Fabric 叢集，您也需要的 toodelete 所有 hello 則由的資源。</span><span class="sxs-lookup"><span data-stu-id="9c033-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="9c033-176">hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c033-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="9c033-177">如叢集或 toodelete 資源群組中的某些 （但並非所有） hello 資源，請參閱其他方式 toodelete[刪除叢集](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="9c033-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="9c033-178">刪除資源群組 hello Azure 入口網站中：</span><span class="sxs-lookup"><span data-stu-id="9c033-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="9c033-179">瀏覽您想 toodelete toohello Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="9c033-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="9c033-180">按一下 hello**資源群組**hello 叢集 essentials 頁面上的名稱。</span><span class="sxs-lookup"><span data-stu-id="9c033-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="9c033-181">在 hello**資源群組 Essentials**頁面上，按一下**刪除資源群組**依該頁面 toocomplete hello 刪除 hello 資源群組中的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="9c033-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="9c033-182">![刪除 hello 資源群組][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="9c033-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="9c033-183">使用 Azure Powershell toodeploy 安全叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="9c033-184">下載 hello [Azure Powershell 模組版本 4.0 或更新版本](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="9c033-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="9c033-185">開啟 Windows PowerShell 視窗中，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c033-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="9c033-186">您應該會看到類似 toohello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="9c033-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="9c033-188">登入 tooAzure 和選取 hello 訂用帳戶 toowhich 想 toocreate hello 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="9c033-189">執行下列命令 toonow 的 hello 建立安全的叢集。</span><span class="sxs-lookup"><span data-stu-id="9c033-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="9c033-190">不要忘記 toocustomize hello 參數。</span><span class="sxs-lookup"><span data-stu-id="9c033-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="9c033-191">hello 命令可能需要 10 分鐘 too30 分鐘 toocomplete，hello 結尾處，您應該會收到類似 toohello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="9c033-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="9c033-192">hello hello 憑證，它已上傳，所以 KeyVault hello 的相關資訊及輸出 hello 複製 hello 憑證所在的本機資料夾。</span><span class="sxs-lookup"><span data-stu-id="9c033-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="9c033-194">複製 hello 整個輸出並儲存 tooa 文字檔案，因為我們需要 toorefer tooit。</span><span class="sxs-lookup"><span data-stu-id="9c033-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="9c033-195">記下 hello hello 輸出中的下列資訊。</span><span class="sxs-lookup"><span data-stu-id="9c033-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="9c033-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="9c033-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="9c033-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="9c033-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="9c033-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="9c033-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="9c033-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="9c033-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="9c033-200">在您的本機電腦上安裝 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="9c033-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="9c033-201">tooconnect toohello 叢集中，您會需要 tooinstall hello 憑證到 hello hello 目前使用者的個人 (My) 存放區。</span><span class="sxs-lookup"><span data-stu-id="9c033-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="9c033-202">執行下列 PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="9c033-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="9c033-203">現在您已經準備就緒 tooconnect tooyour 安全叢集。</span><span class="sxs-lookup"><span data-stu-id="9c033-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="9c033-204">Tooa 安全叢集連線</span><span class="sxs-lookup"><span data-stu-id="9c033-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="9c033-205">執行下列 PowerShell 命令 tooconnect tooa 安全叢集的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c033-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="9c033-206">hello 憑證詳細資料必須符合已使用的 tooset hello 叢集的憑證。</span><span class="sxs-lookup"><span data-stu-id="9c033-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="9c033-207">下列範例顯示 hello hello completed 參數：</span><span class="sxs-lookup"><span data-stu-id="9c033-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="9c033-208">執行下列命令 toocheck 您所連接的 hello 且 hello 叢集狀況良好。</span><span class="sxs-lookup"><span data-stu-id="9c033-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="9c033-209">發行您從 Visual Studio 的應用程式 tooyour 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="9c033-210">既然您已設定 Azure 的叢集，您可以發佈您的應用程式 tooit 從 Visual Studio 的下列 hello[發行 tooan 叢集](service-fabric-publish-app-remote-cluster.md)文件。</span><span class="sxs-lookup"><span data-stu-id="9c033-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="9c033-211">移除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-211">Remove hello cluster</span></span>
<span data-ttu-id="9c033-212">叢集所組成的其他 Azure 資源此外 toohello 叢集資源本身。</span><span class="sxs-lookup"><span data-stu-id="9c033-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="9c033-213">hello 最簡單方式 toodelete hello 叢集及它會取用所有 hello 資源是 toodelete hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c033-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="9c033-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c033-214">Next steps</span></span>
<span data-ttu-id="9c033-215">既然您已設定開發叢集，請嘗試下列 hello:</span><span class="sxs-lookup"><span data-stu-id="9c033-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="9c033-216">Hello 入口網站中建立安全的叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="9c033-217">從範本建立叢集</span><span class="sxs-lookup"><span data-stu-id="9c033-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="9c033-218">使用 PowerShell 部署應用程式</span><span class="sxs-lookup"><span data-stu-id="9c033-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
