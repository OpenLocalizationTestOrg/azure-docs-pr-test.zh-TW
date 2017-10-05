---
title: "用來部署 Linux HPC 叢集的 PowerShell 指令碼 | Microsoft Docs"
description: "執行 PowerShell 指令碼，以在 Azure 虛擬機器中部署 Linux HPC Pack 2012 R2 叢集"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: c15dc66718a855e22f8109448cb8c8a23787b9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="0a792-103">使用 HPC Pack IaaS 部署指令碼建立 Linux 高效能運算 (HPC) 叢集</span><span class="sxs-lookup"><span data-stu-id="0a792-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="0a792-104">執行 HPC Pack IaaS 部署 PowerShell 指令碼，以在 Azure 虛擬機器中為 Linux 工作負載部署完整的 HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a792-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="0a792-105">叢集是由加入 Active Directory、且執行 Windows Server 和 Microsoft HPC Pack 的前端節點，以及執行其中一個 HPC Pack 所支援的 Linux 散發套件的計算節點所組成。</span><span class="sxs-lookup"><span data-stu-id="0a792-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="0a792-106">如果您想要在 Azure 中為 Windows 工作負載部署 HPC Pack 叢集，請參閱[使用 HPC Pack IaaS 部署指令碼建立 Windows HPC 叢集](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0a792-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="0a792-107">您也可以使用 Azure 資源管理員範本來部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a792-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="0a792-108">如需範例，請參閱 [使用 Linux 計算節點建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)。</span><span class="sxs-lookup"><span data-stu-id="0a792-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0a792-109">本文中所述的 PowerShell 指令碼會使用傳統部署模型，在 Azure 中建立 Microsoft HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="0a792-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="0a792-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="0a792-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="0a792-111">此外，本文中所述的指令碼不支援 HPC Pack 2016。</span><span class="sxs-lookup"><span data-stu-id="0a792-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="0a792-112">範例組態檔</span><span class="sxs-lookup"><span data-stu-id="0a792-112">Example configuration file</span></span>
<span data-ttu-id="0a792-113">下列組態檔會建立網域控制站和網域樹系並部署 HPC Pack 叢集，此叢集包含 1 個具有本機資料庫的前端節點和 10 個 Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="0a792-113">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="0a792-114">所有雲端服務都直接建立在「東亞」位置中。</span><span class="sxs-lookup"><span data-stu-id="0a792-114">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="0a792-115">Linux 計算節點會建立在 2 個雲端服務和 2 個儲存體帳戶中 (亦即 *MyLnxCNService01* 和 *mylnxstorage01* 中的 *MyLnxCN-0001* 至 *MyLnxCN-0005*，以及 *MyLnxCNService02* 和 *mylnxstorage02* 中的 *MyLnxCN-0006* 至 *MyLnxCN-0010*)。</span><span class="sxs-lookup"><span data-stu-id="0a792-115">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="0a792-116">計算節點會從 OpenLogic CentOS 7.0 版 Linux 映像建立。</span><span class="sxs-lookup"><span data-stu-id="0a792-116">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="0a792-117">請將訂用帳戶名稱和服務及服務名稱取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="0a792-117">Substitute your own values for your subscription name and the account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="0a792-118">疑難排解</span><span class="sxs-lookup"><span data-stu-id="0a792-118">Troubleshooting</span></span>
* <span data-ttu-id="0a792-119">**「VNet 不存在」錯誤**。</span><span class="sxs-lookup"><span data-stu-id="0a792-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="0a792-120">如果您執行 HPC Pack IaaS 部署指令碼來將多個叢集同時部署在 Azure 中的一個訂用帳戶底下，可能會有一或多個部署因發生「VNet *VNet\_Name* 不存在」錯誤而失敗。</span><span class="sxs-lookup"><span data-stu-id="0a792-120">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="0a792-121">如果發生此錯誤，請針對失敗的部署重新執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="0a792-121">If this error occurs, rerun the script for the failed deployment.</span></span>
* <span data-ttu-id="0a792-122">**從 Azure 虛擬網路存取網際網路時發生問題**。</span><span class="sxs-lookup"><span data-stu-id="0a792-122">**Problem accessing the Internet from the Azure virtual network**.</span></span> <span data-ttu-id="0a792-123">如果您藉由使用部署指令碼來建立具有新網域控制站的 HPC Pack 叢集，或是手動將前端節點 VM 升級到網域控制站，則在將 Azure 虛擬網路中的 VM 連接到網際網路時，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="0a792-123">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span></span> <span data-ttu-id="0a792-124">如果在網域控制站上自動設定轉寄站 DNS 伺服器，且這個轉寄站 DNS 伺服器未正確解析，就可能出現這種狀況。</span><span class="sxs-lookup"><span data-stu-id="0a792-124">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="0a792-125">若要解決此問題，請登入網域控制站，並選擇移除轉寄站組態設定，或設定有效的轉寄站 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a792-125">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="0a792-126">若要這樣做，請在伺服器管理員中按一下 [工具]  >  [DNS] 以開啟 DNS 管理員，然後按兩下 [轉寄站]。</span><span class="sxs-lookup"><span data-stu-id="0a792-126">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a792-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a792-127">Next steps</span></span>
* <span data-ttu-id="0a792-128">有關支援的 Linux 散發套件、移動資料，以及使用 Linux 計算節點將工作提交至 HPC Pack 叢集，如需詳細資訊請參閱[開始在 Azure 中的 HPC Pack 叢集使用 Linux 計算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="0a792-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="0a792-129">如需有關使用指令碼來建立叢集和執行 Linux HPC 工作負載的教學課程，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="0a792-129">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="0a792-130">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="0a792-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="0a792-131">在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="0a792-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="0a792-132">在 Azure 中的 Linux 計算節點以 Microsoft HPC Pack 執行 STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="0a792-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

