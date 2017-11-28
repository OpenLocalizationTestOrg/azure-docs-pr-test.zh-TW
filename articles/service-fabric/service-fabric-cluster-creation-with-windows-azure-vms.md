---
title: "包含執行 Windows Azure Vm 叢集 aaaCreate 獨立 |Microsoft 文件"
description: "深入了解如何 toocreate 和管理執行 Windows Server 的 Azure 虛擬機器上的 Azure Service Fabric 叢集。"
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
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="92c32-103">建立三個具有執行 Windows Server 之 Azure 虛擬機器的節點獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="92c32-104">本文說明如何 toocreate 的 windows Azure 虛擬機器 (Vm) 上的叢集，使用 hello 獨立 Service Fabric 安裝程式的 Windows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="92c32-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="92c32-105">hello 案例是特殊案例[建立和管理 Windows Server 上執行叢集](service-fabric-cluster-creation-for-windows-server.md)hello Vm 所在[執行 Windows Server 的 Azure Vm](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)，但是您不需要建立[Azure以雲端為基礎的 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="92c32-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="92c32-106">遵循此模式中的 hello 差異並沒有那麼 hello 步驟所建立的 hello 獨立 Service Fabric 叢集完全受您，而管理的 hello Azure 雲端服務網狀架構叢集，並由 hello Service Fabric 升級資源提供者。</span><span class="sxs-lookup"><span data-stu-id="92c32-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="92c32-107">步驟 toocreate hello 獨立叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="92c32-108">登入 toohello Azure 入口網站，並在資源群組中建立新的 Windows Server 2012 R2 Datacenter 或 Windows Server 2016 資料中心的 VM。</span><span class="sxs-lookup"><span data-stu-id="92c32-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="92c32-109">閱讀文章 hello [hello Azure 入口網站中建立的 Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="92c32-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="92c32-110">加入一些其他的 Vm toohello 相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="92c32-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="92c32-111">請確定每個 hello Vm 有 hello 相同的系統管理員使用者名稱和密碼時建立。</span><span class="sxs-lookup"><span data-stu-id="92c32-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="92c32-112">您應該會看見 hello 中的所有三個 Vm 建立之後相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92c32-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="92c32-113">連接的 hello Vm tooeach 並關閉 Windows 防火牆使用 hello hello[伺服器管理員 中，本機伺服器儀表板](https://technet.microsoft.com/library/jj134147.aspx)。</span><span class="sxs-lookup"><span data-stu-id="92c32-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="92c32-114">這可確保 hello 網路流量，可以 hello 機器之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="92c32-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="92c32-115">連接的 tooeach 機器時，請開啟命令提示字元並輸入取得 hello 的 IP 位址`ipconfig`。</span><span class="sxs-lookup"><span data-stu-id="92c32-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="92c32-116">或者，您可以看到 hello IP hello 入口網站中，選取 hello hello 資源群組的虛擬網路資源，並檢查這些機器的每個建立的 hello 網路介面上的每部機器的位址。</span><span class="sxs-lookup"><span data-stu-id="92c32-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="92c32-117">連接的 hello Vm tooone 和測試，您可以 ping 成功 hello 其他兩個 Vm。</span><span class="sxs-lookup"><span data-stu-id="92c32-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="92c32-118">連接的 hello Vm tooone 和[hello 獨立 Service Fabric 封裝下載適用於 Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) hello 上的新資料夾到電腦，並擷取 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="92c32-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="92c32-119">開啟 hello *ClusterConfig.Unsecure.MultiMachine.json* [記事本] 中，並編輯 hello 機器 hello 三個 IP 位址與每個節點。</span><span class="sxs-lookup"><span data-stu-id="92c32-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="92c32-120">變更在 hello 頂端 hello 叢集名稱，並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="92c32-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="92c32-121">Hello 叢集資訊清單的部分範例如下所示。</span><span class="sxs-lookup"><span data-stu-id="92c32-121">A partial example of hello cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="92c32-122">如果您想要這個 toobe 安全的叢集，決定 hello 安全性措施，toouse 然後遵循 hello hello 步驟相關聯的連結： [X509 憑證](service-fabric-windows-cluster-x509-security.md)或[Windows 安全性](service-fabric-windows-cluster-windows-security.md)。</span><span class="sxs-lookup"><span data-stu-id="92c32-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="92c32-123">如果設定使用 Windows 安全性的 hello 叢集，您必須設定 Active Directory 網域控制站 toomanage tooset。</span><span class="sxs-lookup"><span data-stu-id="92c32-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="92c32-124">請注意，不支援使用網域控制站電腦做為 Service Fabric 節點。</span><span class="sxs-lookup"><span data-stu-id="92c32-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="92c32-125">開啟 [PowerShell ISE 視窗](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。</span><span class="sxs-lookup"><span data-stu-id="92c32-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="92c32-126">瀏覽 toohello 資料夾您擷取 hello 下載的獨立安裝程式封裝並儲存 hello 叢集組態檔。</span><span class="sxs-lookup"><span data-stu-id="92c32-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="92c32-127">執行下列 PowerShell 命令 toodeploy hello 叢集 hello:</span><span class="sxs-lookup"><span data-stu-id="92c32-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="92c32-128">hello 指令碼都會從遠端設定 hello Service Fabric 叢集，而且應該報告進度，因為透過復原部署。</span><span class="sxs-lookup"><span data-stu-id="92c32-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="92c32-129">約一分鐘，您可以檢查如果 hello 叢集運作藉由連接 toohello 之後 Service Fabric 總管使用其中一種 hello 機器的 IP 位址，例如使用`http://10.1.0.5:19080/Explorer/index.html`。</span><span class="sxs-lookup"><span data-stu-id="92c32-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="92c32-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92c32-130">Next steps</span></span>
* [<span data-ttu-id="92c32-131">在 Windows Server 或 Linux 上建立獨立的 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="92c32-132">新增或移除節點 tooa 獨立 Service Fabric 叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="92c32-133">獨立 Windows 叢集的組態設定</span><span class="sxs-lookup"><span data-stu-id="92c32-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="92c32-134">使用 Windows 安全性保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="92c32-135">使用 X509 憑證保護 Windows 上的獨立叢集</span><span class="sxs-lookup"><span data-stu-id="92c32-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

