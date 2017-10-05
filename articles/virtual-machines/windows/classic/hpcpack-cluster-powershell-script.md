---
title: "用來部署 Windows HPC 叢集的 PowerShell 指令碼 | Microsoft Docs"
description: "執行 PowerShell 指令碼，以在 Azure 虛擬機器中部署 Windows HPC Pack 2012 R2 叢集"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 85b125ab19671b61d2541af6378c95feb88bf952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="5e053-103">使用 HPC Pack IaaS 部署指令碼建立 Windows 高效能運算 (HPC) 叢集</span><span class="sxs-lookup"><span data-stu-id="5e053-103">Create a Windows high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="5e053-104">執行 HPC Pack IaaS 部署 PowerShell 指令碼，以在 Azure 虛擬機器中為 Windows 工作負載部署完整的 HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="5e053-105">叢集是由加入 Active Directory、且執行 Windows Server 和 Microsoft HPC Pack 的前端節點，以及您指定的其他 Windows 計算資源所組成。</span><span class="sxs-lookup"><span data-stu-id="5e053-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="5e053-106">如果您想要在 Azure 中為 Linux 工作負載部署 HPC Pack 叢集，請參閱 [使用 HPC Pack IaaS 部署指令碼建立 Linux HPC 叢集](../../linux/classic/hpcpack-cluster-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="5e053-106">If you want to deploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="5e053-107">您也可以使用 Azure 資源管理員範本來部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="5e053-108">如需範例，請參閱[建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)和[使用自訂的計算節點映像建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)。</span><span class="sxs-lookup"><span data-stu-id="5e053-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5e053-109">本文中所述的 PowerShell 指令碼會使用傳統部署模型，在 Azure 中建立 Microsoft HPC Pack 2012 R2 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="5e053-110">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="5e053-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="5e053-111">此外，本文中所述的指令碼不支援 HPC Pack 2016。</span><span class="sxs-lookup"><span data-stu-id="5e053-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="5e053-112">範例組態檔</span><span class="sxs-lookup"><span data-stu-id="5e053-112">Example configuration files</span></span>
<span data-ttu-id="5e053-113">在下列範例中，請將訂用帳戶 ID 或名稱及帳戶和服務名稱取代為您自己的值。</span><span class="sxs-lookup"><span data-stu-id="5e053-113">In the following examples, substitute your own values for your subscription Id or name and the account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="5e053-114">範例 1</span><span class="sxs-lookup"><span data-stu-id="5e053-114">Example 1</span></span>
<span data-ttu-id="5e053-115">下列組態檔會部署一個 HPC Pack 叢集，其中包含一個具有本機資料庫的前端節點，以及五個執行 Windows Server 2012 R2 作業系統的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-115">The following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="5e053-116">所有雲端服務都直接建立在「美國西部」位置。</span><span class="sxs-lookup"><span data-stu-id="5e053-116">All the cloud services are created directly in the West US location.</span></span> <span data-ttu-id="5e053-117">前端節點會做為網域樹系的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="5e053-117">The head node acts as domain controller of the domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="5e053-118">範例 2</span><span class="sxs-lookup"><span data-stu-id="5e053-118">Example 2</span></span>
<span data-ttu-id="5e053-119">下列組態檔會在現有的網域樹系中部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-119">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e053-120">叢集中有 1 個具有本機資料庫的前端節點，和 12 個套用了 BGInfo VM 延伸模組的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-120">The cluster has 1 head node with local databases and 12 compute nodes with the BGInfo VM extension applied.</span></span>
<span data-ttu-id="5e053-121">對於網域樹系中的所有 VM，都會停用 Windows 更新的自動安裝。</span><span class="sxs-lookup"><span data-stu-id="5e053-121">Automatic installation of Windows updates is disabled for all the VMs in the domain forest.</span></span> <span data-ttu-id="5e053-122">所有雲端服務都直接建立在「東亞」位置中。</span><span class="sxs-lookup"><span data-stu-id="5e053-122">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="5e053-123">計算節點會建立在三個雲端服務和三個儲存體帳戶中：*MyHPCCNService01* 和 *mycnstorage01* 中的 *MyHPCCN-0001* 至*MyHPCCN-0005*；*MyHPCCNService02* 和 *mycnstorage02* 中的 *MyHPCCN-0006* 至 *MyHPCCN0010*；以及 *MyHPCCNService03* 和 *mycnstorage03* 中的 *MyHPCCN-0011* 至 *MyHPCCN-0012*)。</span><span class="sxs-lookup"><span data-stu-id="5e053-123">The compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* to *MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* to *MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* to *MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="5e053-124">計算節點會從擷取自雲端節點的現有私人映像建立。</span><span class="sxs-lookup"><span data-stu-id="5e053-124">The compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="5e053-125">自動增加和縮減服務會根據預設的增加和縮減間隔來啟用。</span><span class="sxs-lookup"><span data-stu-id="5e053-125">The auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="5e053-126">範例 3</span><span class="sxs-lookup"><span data-stu-id="5e053-126">Example 3</span></span>
<span data-ttu-id="5e053-127">下列組態檔會在現有的網域樹系中部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-127">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e053-128">叢集中包含 1 個前端節點、1 個具有 500 GB 資料磁碟的資料庫伺服器、2 個執行 Windows Server 2012 R2 作業系統的訊息代理程式節點，以及 5 個執行 Windows Server 2012 R2 作業系統的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-128">The cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running the Windows Server 2012 R2 operating system, and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="5e053-129">MyHPCCNService 雲端服務會建立在同質群組 *MyIBAffinityGroup* 中，其他雲端服務則是建立在同質群組 *MyAffinityGroup* 中。</span><span class="sxs-lookup"><span data-stu-id="5e053-129">The cloud service MyHPCCNService is created in the affinity group *MyIBAffinityGroup*, and the other cloud services are created in the affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="5e053-130">前端節點上會啟用 HPC 工作排程器 REST API 和 HPC Web 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5e053-130">The HPC Job Scheduler REST API and HPC web portal are enabled on the head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="5e053-131">範例 4</span><span class="sxs-lookup"><span data-stu-id="5e053-131">Example 4</span></span>
<span data-ttu-id="5e053-132">下列組態檔會在現有的網域樹系中部署 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e053-132">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e053-133">叢集中包含兩個具有本機資料庫的前端節點、建立了兩個 Azure 節點範本，且針對 Azure 節點範本 *AzureTemplate1*建立了 3 個中型大小的 Azure 節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-133">The cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="5e053-134">在設定完前端節點之後，指令檔會在前端節點上執行。</span><span class="sxs-lookup"><span data-stu-id="5e053-134">A script file runs on the head node after the head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="5e053-135">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e053-135">Troubleshooting</span></span>
* <span data-ttu-id="5e053-136">**「VNet 不存在」錯誤** - 如果您執行指令碼將多個叢集同時部署在 Azure 中的一個訂用帳戶底下，可能會有一或多個部署因發生「VNet *VNet\_Name* 不存在」錯誤而失敗。</span><span class="sxs-lookup"><span data-stu-id="5e053-136">**“VNet doesn’t exist” error** - If you run the script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="5e053-137">如果發生此錯誤，請針對失敗的部署重新執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="5e053-137">If this error occurs, run the script again for the failed deployment.</span></span>
* <span data-ttu-id="5e053-138">**從 Azure 虛擬網路存取網際網路時發生問題** - 如果您使用部署指令碼建立具有新網域控制站的叢集，或手動將前端節點 VM 升級到網域控制站，則在將 VM 連接到網際網路時，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="5e053-138">**Problem accessing the Internet from the Azure virtual network** - If you create a cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs to the Internet.</span></span> <span data-ttu-id="5e053-139">如果網域控制站上自動設定了轉寄站 DNS 伺服器，而此轉寄站 DNS 伺服器未正確解析，就可能發生這種問題。</span><span class="sxs-lookup"><span data-stu-id="5e053-139">This problem can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="5e053-140">若要解決此問題，請登入網域控制站，並選擇移除轉寄站組態設定，或設定有效的轉寄站 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5e053-140">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="5e053-141">若要設定這項設定，請在「伺服器管理員」中按一下 [工具]**** >
    [DNS]**** 以開啟 [DNS 管理員]，然後按兩下 [轉寄站]****。</span><span class="sxs-lookup"><span data-stu-id="5e053-141">To configure this setting, in Server Manager click **Tools** >
    **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="5e053-142">**從計算密集型 VM 存取 RDMA 網路時發生問題** - 如果您使用支援 RDMA 大小 (例如 A8 或 A9) 的 VM 來新增 Windows Server 計算節點 VM 或訊息代理程式節點 VM，則在將這些 VM 連接到 RDMA 應用程式網路時，可能會發生問題。</span><span class="sxs-lookup"><span data-stu-id="5e053-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs to the RDMA application network.</span></span> <span data-ttu-id="5e053-143">之所以會發生此問題，其中一個原因是在將 VM 新增到叢集時，未正確安裝 HpcVmDrivers 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5e053-143">One reason this problem occurs is if the HpcVmDrivers extension is not properly installed when the VMs are added to the cluster.</span></span> <span data-ttu-id="5e053-144">比方說，延伸模組可能卡在安裝中狀態。</span><span class="sxs-lookup"><span data-stu-id="5e053-144">For example, the extension might be stuck in the installing state.</span></span>
  
    <span data-ttu-id="5e053-145">若要解決這個問題，請先檢查 VM 中的延伸模組狀態。</span><span class="sxs-lookup"><span data-stu-id="5e053-145">To work around this problem, first check the state of the extension in the VMs.</span></span> <span data-ttu-id="5e053-146">如果延伸模組未正確安裝，請嘗試從 HPC 叢集中移除節點，然後重新新增節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-146">If the extension is not properly installed, try removing the nodes from the HPC cluster and then add the nodes again.</span></span> <span data-ttu-id="5e053-147">例如，您可以在前端節點上執行 Add-HpcIaaSNode.ps1 指令碼，以新增計算節點 VM。</span><span class="sxs-lookup"><span data-stu-id="5e053-147">For example, you can add compute node VMs by running the Add-HpcIaaSNode.ps1 script on the head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e053-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e053-148">Next steps</span></span>
* <span data-ttu-id="5e053-149">嘗試在叢集上執行測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="5e053-149">Try running a test workload on the cluster.</span></span> <span data-ttu-id="5e053-150">如需範例，請參閱 HPC Pack [快速入門指南](https://technet.microsoft.com/library/jj884144)。</span><span class="sxs-lookup"><span data-stu-id="5e053-150">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="5e053-151">如需編寫叢集部署指令碼及執行 HPC 工作負載的教學課程，請參閱 [開始使用 Azure 中的 HPC Pack 叢集執行 Excel 和 SOA 工作負載](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5e053-151">For a tutorial to script the cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5e053-152">嘗試以 HPC Pack 的工具啟動、停止、新增和移除您所建立之叢集中的計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e053-152">Try HPC Pack's tools to start, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="5e053-153">請參閱 [在 Azure 中管理 HPC Pack 叢集的計算節點](hpcpack-cluster-node-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="5e053-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="5e053-154">若要設定將工作從本機電腦提交至叢集，請參閱 [將 HPC 工作從內部部署電腦提交至 Azure 中的 HPC Pack 叢集](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5e053-154">To get set up to submit jobs to the cluster from a local computer, see [Submit HPC jobs from an on-premises computer to an HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

