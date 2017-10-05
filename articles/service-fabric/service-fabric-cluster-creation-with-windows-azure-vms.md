---
title: "建立具有執行 Windows 之 Azure VM 的獨立叢集 | Microsoft Docs"
description: "了解如何在執行 Windows Server 的 Azure 虛擬機器上建立和管理 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="6681b-103">建立三個具有執行 Windows Server 之 Azure 虛擬機器的節點獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="6681b-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="6681b-104">本文說明如何使用適用於 Windows Server 的獨立 Service Fabric 安裝程式，在 Windows 型 Azure 虛擬機器 (VM) 上建立叢集。</span><span class="sxs-lookup"><span data-stu-id="6681b-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="6681b-105">這此案例為[建立和管理在 Windows Server 上執行的叢集](service-fabric-cluster-creation-for-windows-server.md)的特殊案例，其 VM 是[執行 Windows Server 的 Azure VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，但您不是在建立 [Azure 雲端型 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6681b-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="6681b-106">遵循此模式的差別，在於透過下列步驟所建立的獨立 Service Fabric 叢集是完全由您管理，而 Azure 雲端型 Service Fabric 叢集則是由 Service Fabric 資源提供者來管理和升級。</span><span class="sxs-lookup"><span data-stu-id="6681b-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="6681b-107">獨立叢集的建立步驟</span><span class="sxs-lookup"><span data-stu-id="6681b-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="6681b-108">登入 Azure 入口網站，並在資源群組中建立新的 Windows Server 2012 R2 Datacenter 或 Windows Server 2016 Datacenter VM。</span><span class="sxs-lookup"><span data-stu-id="6681b-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="6681b-109">如需詳細資訊，請閱讀[在 Azure 入口網站中建立 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 一文。</span><span class="sxs-lookup"><span data-stu-id="6681b-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="6681b-110">將數個額外的 VM 新增至相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6681b-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="6681b-111">確定每個 VM 在建立時具有相同的系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6681b-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="6681b-112">一旦建立好，您應該會在相同的虛擬網路中看到這三個 VM。</span><span class="sxs-lookup"><span data-stu-id="6681b-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="6681b-113">使用 [[伺服器管理員] &gt; [本機伺服器]](https://technet.microsoft.com/library/jj134147.aspx)儀表板連接到每個 VM 並關閉 Windows 防火牆。</span><span class="sxs-lookup"><span data-stu-id="6681b-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="6681b-114">這可確保網路流量可在電腦之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="6681b-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="6681b-115">在連接到每個電腦時，透過開啟命令提示字元並輸入 `ipconfig`來取得 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6681b-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="6681b-116">或者您可以在入口網站上看見每一部機器的 IP 位址，方法是選取資源群組的虛擬網路資源，並檢查為這些機器建立的網路介面。</span><span class="sxs-lookup"><span data-stu-id="6681b-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="6681b-117">連接到其中一個 VM，並測試您是否可以成功 ping 到其他兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="6681b-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="6681b-118">連接到其中一個 VM，並 [下載適用於 Windows Server 的獨立 Service Fabric 封裝](http://go.microsoft.com/fwlink/?LinkId=730690) 到電腦上的新資料夾，然後解壓縮封裝。</span><span class="sxs-lookup"><span data-stu-id="6681b-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="6681b-119">在記事本開啟「ClusterConfig.Unsecure.MultiMachine.json」  檔案，然後使用電腦的三個 IP 位址編輯每個節點。</span><span class="sxs-lookup"><span data-stu-id="6681b-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="6681b-120">在頂端變更叢集名稱，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="6681b-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="6681b-121">叢集資訊清單的部分範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="6681b-121">A partial example of the cluster manifest is shown below.</span></span>
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. <span data-ttu-id="6681b-122">若您想要讓此叢集成為安全的叢集，請決定您要使用的安全性措施，並遵循相關連結的步驟：[X509 憑證](service-fabric-windows-cluster-x509-security.md)或 [Windows 安全性](service-fabric-windows-cluster-windows-security.md)。</span><span class="sxs-lookup"><span data-stu-id="6681b-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="6681b-123">若使用 Windows 安全性設定叢集，您必須設定網域控制站以管理 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="6681b-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="6681b-124">請注意，不支援使用網域控制站電腦做為 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="6681b-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="6681b-125">開啟 [PowerShell ISE 視窗](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。</span><span class="sxs-lookup"><span data-stu-id="6681b-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="6681b-126">瀏覽至所下載獨立安裝程式封裝的解壓縮資料夾，然後儲存叢集設定檔案。</span><span class="sxs-lookup"><span data-stu-id="6681b-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="6681b-127">執行下列 PowerShell 命令來部署叢集：</span><span class="sxs-lookup"><span data-stu-id="6681b-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="6681b-128">該指令碼將會於遠端設定 Service Fabric 叢集，並應該會隨著部署推出報告進度。</span><span class="sxs-lookup"><span data-stu-id="6681b-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="6681b-129">大約 1 分鐘過後，您就可以透過使用其中一部電腦的 IP 位址連接到 Service Fabric Explorer (例如使用 `http://10.1.0.5:19080/Explorer/index.html`)，來檢查叢集是否已運作。</span><span class="sxs-lookup"><span data-stu-id="6681b-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6681b-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6681b-130">Next steps</span></span>
* [<span data-ttu-id="6681b-131">在 Windows Server 或 Linux 上建立獨立的 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="6681b-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="6681b-132">在獨立 Service Fabric 叢集中新增或移除節點</span><span class="sxs-lookup"><span data-stu-id="6681b-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="6681b-133">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="6681b-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="6681b-134">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="6681b-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="6681b-135">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="6681b-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

