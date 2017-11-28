---
title: "aaaPowerShell 指令碼 toodeploy Windows HPC 叢集 |Microsoft 文件"
description: "在 Azure 虛擬機器中執行 PowerShell 指令碼 toodeploy Windows HPC Pack 2012 R2 叢集"
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
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="5e576-103">Hello HPC Pack IaaS 部署指令碼以建立 Windows 高效能運算 (HPC) 叢集</span><span class="sxs-lookup"><span data-stu-id="5e576-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="5e576-104">在 Azure 虛擬機器中執行 hello HPC Pack IaaS 部署 PowerShell 指令碼 toodeploy 完整的 HPC Pack 2012 R2 叢集，針對 Windows 工作負載。</span><span class="sxs-lookup"><span data-stu-id="5e576-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="5e576-105">hello 叢集包含已加入 Active Directory 的前端節點執行 Windows Server 和 Microsoft HPC Pack，而其他視窗計算您所指定的資源。</span><span class="sxs-lookup"><span data-stu-id="5e576-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="5e576-106">如果您想要在 Azure 中的 HPC Pack 叢集 toodeploy Linux 工作負載，請參閱[hello HPC Pack IaaS 部署指令碼以建立 Linux HPC 叢集](../../linux/classic/hpcpack-cluster-powershell-script.md)。</span><span class="sxs-lookup"><span data-stu-id="5e576-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="5e576-107">您也可以使用 Azure Resource Manager 範本 toodeploy HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e576-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="5e576-108">如需範例，請參閱[建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/)和[使用自訂的計算節點映像建立 HPC 叢集](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/)。</span><span class="sxs-lookup"><span data-stu-id="5e576-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="5e576-109">hello 本文中所述的 PowerShell 指令碼會建立 Microsoft HPC Pack 2012 R2 叢集，在 Azure 中使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5e576-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="5e576-110">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="5e576-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="5e576-111">此外，本文中所述的 hello 指令碼不支援使用 HPC Pack 2016。</span><span class="sxs-lookup"><span data-stu-id="5e576-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="5e576-112">範例組態檔</span><span class="sxs-lookup"><span data-stu-id="5e576-112">Example configuration files</span></span>
<span data-ttu-id="5e576-113">Hello 在下列範例中，會取代您自己的值，您的訂用帳戶識別碼或名稱和 hello 帳戶和服務名稱。</span><span class="sxs-lookup"><span data-stu-id="5e576-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="5e576-114">範例 1</span><span class="sxs-lookup"><span data-stu-id="5e576-114">Example 1</span></span>
<span data-ttu-id="5e576-115">hello 下列組態檔來部署 HPC Pack 叢集前端節點具有本機資料庫和執行 Windows Server 2012 R2 作業系統 hello 的五個計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e576-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="5e576-116">所有的 hello 雲端服務都會直接建立在 hello 美國西部的位置。</span><span class="sxs-lookup"><span data-stu-id="5e576-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="5e576-117">hello 前端節點做為 hello 網域樹系的網域控制站。</span><span class="sxs-lookup"><span data-stu-id="5e576-117">hello head node acts as domain controller of hello domain forest.</span></span>

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

### <a name="example-2"></a><span data-ttu-id="5e576-118">範例 2</span><span class="sxs-lookup"><span data-stu-id="5e576-118">Example 2</span></span>
<span data-ttu-id="5e576-119">下列組態檔的 hello 部署現有的網域樹系中的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e576-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e576-120">hello 叢集有 1 個前端節點具有本機資料庫，而且 12 個運算節點以 hello 套用 BGInfo VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5e576-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="5e576-121">自動安裝 Windows 更新已停用所有 hello hello 網域樹系中的 Vm。</span><span class="sxs-lookup"><span data-stu-id="5e576-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="5e576-122">所有的 hello 雲端服務都會直接建立在東亞 」 位置。</span><span class="sxs-lookup"><span data-stu-id="5e576-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="5e576-123">hello 運算節點會建立三個雲端服務和三個儲存體帳戶中： *Myhpccnservice01 0001*太*myhpccn-0005*中*MyHPCCNService01*和*mycnstorage01*;*中的 myhpccn-0006*太*MyHPCCN0010*中*MyHPCCNService02*和*mycnstorage02*; 和*MyHPCCN-0011*太*Myhpccnservice01 0012*中*MyHPCCNService03*和*mycnstorage03*)。</span><span class="sxs-lookup"><span data-stu-id="5e576-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="5e576-124">hello 運算節點會從擷取自運算節點的現有私人映像建立。</span><span class="sxs-lookup"><span data-stu-id="5e576-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="5e576-125">hello 自動擴增和縮減服務已啟用，預設值擴增和縮減的間隔。</span><span class="sxs-lookup"><span data-stu-id="5e576-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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

### <a name="example-3"></a><span data-ttu-id="5e576-126">範例 3</span><span class="sxs-lookup"><span data-stu-id="5e576-126">Example 3</span></span>
<span data-ttu-id="5e576-127">下列組態檔的 hello 部署現有的網域樹系中的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e576-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e576-128">hello 叢集包含一個前端節點、 使用 500 GB 資料磁碟，一部資料庫伺服器執行 hello Windows Server 2012 R2 作業系統，以及執行 Windows Server 2012 R2 作業系統 hello 的五個計算節點的兩個 broker 節點。</span><span class="sxs-lookup"><span data-stu-id="5e576-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="5e576-129">雲端服務 MyHPCCNService 會建立 hello 同質群組中的 hello *myibaffinitygroup 中*，且 hello 其他雲端服務會建立在 hello 同質群組*myaffinitygroup 中*。</span><span class="sxs-lookup"><span data-stu-id="5e576-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="5e576-130">hello 前端節點上啟用 hello HPC 工作排程器 REST API 和 HPC web 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5e576-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

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



### <a name="example-4"></a><span data-ttu-id="5e576-131">範例 4</span><span class="sxs-lookup"><span data-stu-id="5e576-131">Example 4</span></span>
<span data-ttu-id="5e576-132">下列組態檔的 hello 部署現有的網域樹系中的 HPC Pack 叢集。</span><span class="sxs-lookup"><span data-stu-id="5e576-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="5e576-133">hello 叢集有兩個具有本機資料庫的前端節點，會建立兩個 Azure 節點範本，以及三個的大小中 Azure 節點建立 Azure 節點範本*AzureTemplate1*。</span><span class="sxs-lookup"><span data-stu-id="5e576-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="5e576-134">Hello 前端節點設定後，可 hello 前端節點上執行的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="5e576-134">A script file runs on hello head node after hello head node is configured.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="5e576-135">疑難排解</span><span class="sxs-lookup"><span data-stu-id="5e576-135">Troubleshooting</span></span>
* <span data-ttu-id="5e576-136">**「 VNet 不存在 」 錯誤**-如果您 hello 指令碼 toodeploy 多個叢集在 Azure 中同時執行一個訂用帳戶，一或多個部署可能會失敗，錯誤碼為 hello 「 VNet *VNet\_名稱*不存在 」。</span><span class="sxs-lookup"><span data-stu-id="5e576-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="5e576-137">如果發生這個錯誤，執行一次 hello hello 無法部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="5e576-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="5e576-138">**問題存取 hello Azure 虛擬網路從 hello 網際網路**-如果以新的網域控制站建立叢集使用 hello 部署指令碼，或您手動升級前端節點 VM toodomain 控制站，您可能會遇到的問題連接 hello Vm toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="5e576-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="5e576-139">如果 hello 網域控制站，會自動設定轉寄站 DNS 伺服器，而且未正確解析此轉寄站 DNS 伺服器，可能會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="5e576-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="5e576-140">toowork 解決這個問題，請設定有效的轉寄站 DNS 伺服器，或登入 toohello 網域控制站，移除 hello 轉寄站組態設定。</span><span class="sxs-lookup"><span data-stu-id="5e576-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="5e576-141">這項設定，在 伺服器管理員 中按一下的 tooconfigure**工具** >
    **DNS** tooopen DNS 管理員 中，然後按兩下**轉寄站**。</span><span class="sxs-lookup"><span data-stu-id="5e576-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="5e576-142">**從大量計算 Vm 存取 RDMA 網路的問題**-如果您新增 Windows Server 計算或 broker 節點如 A8 或 A9 大小使用具備 RDMA 功能的 Vm，您可能會遇到這些 Vm toohello RDMA 應用程式網路連線問題。</span><span class="sxs-lookup"><span data-stu-id="5e576-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="5e576-143">發生這個問題的其中一個原因是如果 hello HpcVmDrivers 延伸模組未正確安裝 hello Vm 加入 toohello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="5e576-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="5e576-144">例如，擴充功能可能會卡在 hello 安裝狀態。</span><span class="sxs-lookup"><span data-stu-id="5e576-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="5e576-145">此問題，hello Vm 中的 hello 延伸模組的第一個核取 hello 狀態 toowork。</span><span class="sxs-lookup"><span data-stu-id="5e576-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="5e576-146">如果 hello 擴充功能未正確安裝，請嘗試從 hello HPC 叢集中移除 hello 節點，並將 hello 節點的一次。</span><span class="sxs-lookup"><span data-stu-id="5e576-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="5e576-147">例如，您可以新增計算節點 Vm hello 前端節點上執行 hello Add-hpciaasnode.ps1 指令碼。</span><span class="sxs-lookup"><span data-stu-id="5e576-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e576-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5e576-148">Next steps</span></span>
* <span data-ttu-id="5e576-149">請嘗試在 hello 叢集上執行測試工作負載。</span><span class="sxs-lookup"><span data-stu-id="5e576-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="5e576-150">如需範例，請參閱 hello HPC Pack[入門指南](https://technet.microsoft.com/library/jj884144)。</span><span class="sxs-lookup"><span data-stu-id="5e576-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="5e576-151">教學課程 tooscript hello 叢集部署和執行 HPC 工作負載，請參閱[開始使用 Azure toorun Excel 和 SOA 工作負載中的 HPC Pack 叢集](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5e576-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5e576-152">HPC Pack 工具 toostart 再試一次、 停止、 新增和移除您所建立的叢集計算節點。</span><span class="sxs-lookup"><span data-stu-id="5e576-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="5e576-153">請參閱 [在 Azure 中管理 HPC Pack 叢集的計算節點](hpcpack-cluster-node-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="5e576-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="5e576-154">tooget toosubmit 作業 toohello 叢集設定從本機電腦，請參閱[提交 HPC 作業，從內部部署電腦 tooan HPC Pack 叢集在 Azure 中](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5e576-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

