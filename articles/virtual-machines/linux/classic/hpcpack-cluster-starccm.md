---
title: "aaaRun 星狀-CCM + 使用 Linux Vm 上的 HPC Pack |Microsoft 文件"
description: "在 Azure 上部署 Microsoft HPC Pack 叢集，並且跨 RDMA 網路在多個 Linux 計算節點上執行 STAR-CCM+ 作業。"
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="605eb-103">在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="605eb-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="605eb-104">本文將告訴您如何 toodeploy Microsoft HPC Pack 叢集化 Azure 與執行上[CD adapco 星狀-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE)多個互相 InfiniBand Linux 計算節點上的作業。</span><span class="sxs-lookup"><span data-stu-id="605eb-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="605eb-105">Microsoft HPC Pack 提供了功能 toorun 各式各樣的大規模 HPC 和平行應用程式，包括 MPI 應用程式，在 Microsoft Azure 虛擬機器的叢集上。</span><span class="sxs-lookup"><span data-stu-id="605eb-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="605eb-106">HPC Pack 也支援在 HPC Pack 叢集中部署的 Linux 計算節點 VM 上，執行 Linux HPC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="605eb-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="605eb-107">如簡介 toousing Linux 計算節點使用 HPC Pack，請參閱 <<c0> [ 開始使用 Linux 在 Azure 中部署 HPC Pack 叢集中的運算節點](hpcpack-cluster.md)。</span><span class="sxs-lookup"><span data-stu-id="605eb-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="605eb-108">設定 HPC Pack 叢集</span><span class="sxs-lookup"><span data-stu-id="605eb-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="605eb-109">下載 hello HPC Pack IaaS 部署指令碼從 hello[下載中心](https://www.microsoft.com/en-us/download/details.aspx?id=44949)然後在本機解壓縮。</span><span class="sxs-lookup"><span data-stu-id="605eb-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="605eb-110">Azure PowerShell 是必要條件。</span><span class="sxs-lookup"><span data-stu-id="605eb-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="605eb-111">如果您的本機電腦上未設定 PowerShell，請閱讀 hello 文章[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="605eb-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="605eb-112">Hello 撰寫本文時，在 hello Linux 映像從 hello Azure Marketplace （其中包含適用於 Azure 的 hello InfiniBand 驅動程式） 都是 SLES 12、 CentOS 6.5 和 CentOS 7.1。</span><span class="sxs-lookup"><span data-stu-id="605eb-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="605eb-113">這篇文章根據 SLES 12 的 hello 使用量。</span><span class="sxs-lookup"><span data-stu-id="605eb-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="605eb-114">tooretrieve hello 支援 HPC hello Marketplace 中的所有 Linux 映像名稱，您可以執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="605eb-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="605eb-115">hello 輸出會列出這些映像可用以及 hello 映像名稱 hello 位置 (**ImageName**) toobe hello 部署範本中使用的更新版本。</span><span class="sxs-lookup"><span data-stu-id="605eb-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="605eb-116">部署 hello 叢集之前，您有 toobuild HPC Pack 部署範本檔案。</span><span class="sxs-lookup"><span data-stu-id="605eb-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="605eb-117">因為我們的目標小型的叢集，hello 前端節點會 hello 網域控制站並裝載本機 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="605eb-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="605eb-118">hello 下列範本會部署前端節點，請建立名為 XML 檔案**MyCluster.xml**，並取代的 hello 值**SubscriptionId**， **StorageAccount**， **位置**， **VMName**，和**ServiceName**與您。</span><span class="sxs-lookup"><span data-stu-id="605eb-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="605eb-119">在提升權限的命令提示字元中執行 hello PowerShell 命令啟動 hello 前端節點建立：</span><span class="sxs-lookup"><span data-stu-id="605eb-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="605eb-120">20 too30 分鐘之後，應該已經準備好 hello 前端節點。</span><span class="sxs-lookup"><span data-stu-id="605eb-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="605eb-121">您也可以按一下 hello 從 hello Azure 入口網站連線 tooit**連接**hello 虛擬機器的圖示。</span><span class="sxs-lookup"><span data-stu-id="605eb-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="605eb-122">最後，您可能必須 toofix hello DNS 轉寄站。</span><span class="sxs-lookup"><span data-stu-id="605eb-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="605eb-123">因此，toodo 啟動 DNS 管理員。</span><span class="sxs-lookup"><span data-stu-id="605eb-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="605eb-124">以滑鼠右鍵按一下 hello 伺服器名稱的 DNS 管理員中，選取**屬性**，然後按一下hello**轉寄站** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="605eb-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="605eb-125">按一下 hello**編輯**按鈕 tooremove 任何轉寄站，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="605eb-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="605eb-126">請確定該 hello**使用根提示，如果沒有轉寄站可用**核取方塊已選取，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="605eb-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="605eb-127">設定 Linux 計算節點</span><span class="sxs-lookup"><span data-stu-id="605eb-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="605eb-128">使用 hello 部署 hello Linux 計算節點，您會使用 toocreate hello 前端節點相同的部署範本。</span><span class="sxs-lookup"><span data-stu-id="605eb-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="605eb-129">複製 hello 檔案**MyCluster.xml**從您的本機電腦 toohello 前端節點和更新 hello **NodeCount** hello 數目，您想 toodeploy 的節點具有標記 (< = 20)。</span><span class="sxs-lookup"><span data-stu-id="605eb-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="605eb-130">是小心 toohave 足夠可用的核心 Azure 配額，因為每個 A9 執行個體將使用您的訂用帳戶中 16 個核心。</span><span class="sxs-lookup"><span data-stu-id="605eb-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="605eb-131">您可以使用 A8 執行個體 （8 核心） 取代 A9，如果您想 toouse hello 中的多個 Vm 相同的預算。</span><span class="sxs-lookup"><span data-stu-id="605eb-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="605eb-132">Hello 前端節點上，複製 hello HPC Pack IaaS 部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="605eb-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="605eb-133">執行下列 Azure PowerShell 命令，在提升權限的命令提示字元中的 hello:</span><span class="sxs-lookup"><span data-stu-id="605eb-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="605eb-134">執行**Add-azureaccount** tooconnect tooyour Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="605eb-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="605eb-135">如果您有多個訂用帳戶，執行**Get-azuresubscription** toolist 它們。</span><span class="sxs-lookup"><span data-stu-id="605eb-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="605eb-136">設定預設訂用帳戶執行 hello **Select-azuresubscription SubscriptionName xxxx-預設**命令。</span><span class="sxs-lookup"><span data-stu-id="605eb-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="605eb-137">執行**.\New-HPCIaaSCluster.ps1-ConfigFile MyCluster.xml** toostart 部署 Linux 計算節點。</span><span class="sxs-lookup"><span data-stu-id="605eb-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![前端節點部署實務][hndeploy]

<span data-ttu-id="605eb-139">開啟 hello HPC Pack 叢集管理員工具。</span><span class="sxs-lookup"><span data-stu-id="605eb-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="605eb-140">幾分鐘後，Linux 計算節點會定期出現在叢集計算節點的清單中。</span><span class="sxs-lookup"><span data-stu-id="605eb-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="605eb-141">Hello 傳統部署模式中，會以循序方式建立 IaaS Vm。</span><span class="sxs-lookup"><span data-stu-id="605eb-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="605eb-142">因此如果節點的 hello 數目很重要，取得所有部署可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="605eb-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![HPC Pack 叢集管理員中的 Linux 節點][clustermanager]

<span data-ttu-id="605eb-144">既然所有節點都已啟動並執行 hello 叢集中，都有額外的基礎結構設定 toomake。</span><span class="sxs-lookup"><span data-stu-id="605eb-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="605eb-145">為 Windows 和 Linux 節點設定 Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="605eb-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="605eb-146">您可以使用 hello Azure 檔案服務 toostore 指令碼、 應用程式封裝和資料檔案。</span><span class="sxs-lookup"><span data-stu-id="605eb-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="605eb-147">Azure 檔案提供 Azure Blob 儲存體的 CIFS 功能，以當成持續性存放區。</span><span class="sxs-lookup"><span data-stu-id="605eb-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="605eb-148">請注意，這不是 hello 最靈活的解決方案，但它是最簡單的一個 hello，而不需要專用的 Vm。</span><span class="sxs-lookup"><span data-stu-id="605eb-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="605eb-149">建立 Azure 檔案共用 hello 文件中的 hello 指示[開始使用 Azure 檔案儲存在 Windows 上](../../../storage/files/storage-dotnet-how-to-use-files.md)。</span><span class="sxs-lookup"><span data-stu-id="605eb-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="605eb-150">保留 hello 做為儲存體帳戶名稱**saname**，hello 檔案共用名稱做為**sharename**，並為 hello 儲存體帳戶金鑰**sakey**。</span><span class="sxs-lookup"><span data-stu-id="605eb-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="605eb-151">在 hello 前端節點上裝載 hello Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="605eb-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="605eb-152">開啟提升權限的命令提示字元並執行下列命令 toostore hello 認證 hello 本機保存庫中的 hello:</span><span class="sxs-lookup"><span data-stu-id="605eb-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="605eb-153">然後，toomount hello Azure 檔案共用，執行：</span><span class="sxs-lookup"><span data-stu-id="605eb-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="605eb-154">Linux 計算節點上裝載 hello Azure 檔案共用</span><span class="sxs-lookup"><span data-stu-id="605eb-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="605eb-155">一個實用的工具使用 HPC Pack 隨附是 hello clusrun 工具。</span><span class="sxs-lookup"><span data-stu-id="605eb-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="605eb-156">您可以同時使用這個相同命令的命令列工具 toorun hello 組計算節點上。</span><span class="sxs-lookup"><span data-stu-id="605eb-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="605eb-157">在我們的案例，它會使用 toomount hello Azure 檔案共用，並將它保存 toosurvive 重新開機。</span><span class="sxs-lookup"><span data-stu-id="605eb-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="605eb-158">在 hello 前端節點上提高權限命令提示字元中執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="605eb-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="605eb-159">toocreate hello 掛接目錄：</span><span class="sxs-lookup"><span data-stu-id="605eb-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="605eb-160">toomount hello Azure 檔案共用：</span><span class="sxs-lookup"><span data-stu-id="605eb-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="605eb-161">toopersist hello 掛接共用：</span><span class="sxs-lookup"><span data-stu-id="605eb-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="605eb-162">安裝 STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="605eb-162">Install STAR-CCM+</span></span>
<span data-ttu-id="605eb-163">Azure VM 執行個體 A8 和 A9 提供 InfiniBand 支援與 RDMA 功能。</span><span class="sxs-lookup"><span data-stu-id="605eb-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="605eb-164">啟用這些功能的 hello 核心驅動程式可供 Windows Server 2012 R2、 SUSE 12、 CentOS 6.5 和 CentOS 7.1 hello Azure Marketplace 中的映像。</span><span class="sxs-lookup"><span data-stu-id="605eb-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="605eb-165">Microsoft MPI 和 Intel MPI （發行 5.x） 是 hello 兩個 MPI 程式庫在 Azure 中支援這些驅動程式。</span><span class="sxs-lookup"><span data-stu-id="605eb-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="605eb-166">CD-adapco STAR-CCM+ 發行 11.x 和更新版本隨附 Intel MPI 5.x 版，因此含有 Azure 的 InfiniBand 支援。</span><span class="sxs-lookup"><span data-stu-id="605eb-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="605eb-167">取得 hello Linux64 星狀-CCM + 封裝從 hello [CD adapco 入口網站](https://steve.cd-adapco.com)。</span><span class="sxs-lookup"><span data-stu-id="605eb-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="605eb-168">在我們的案例中，以混合精確度使用版本 11.02.010。</span><span class="sxs-lookup"><span data-stu-id="605eb-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="605eb-169">Hello 在前端節點上，hello **/hpcdata** Azure 檔案共用，請建立名為的殼層指令碼**setupstarccm.sh**以 hello 內容之後。</span><span class="sxs-lookup"><span data-stu-id="605eb-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="605eb-170">此指令碼會執行在星狀總每個計算節點 tooset-CCM + 在本機。</span><span class="sxs-lookup"><span data-stu-id="605eb-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="605eb-171">範例 setupstarcm.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="605eb-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="605eb-172">現在，向上星狀 tooset-CCM + 您的所有 Linux 上計算節點，請開啟提升權限的命令提示字元，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="605eb-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="605eb-173">Hello 命令執行時，您可以使用 hello 熱門地圖的 「 叢集管理員來監視 hello CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="605eb-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="605eb-174">幾分鐘後，所有節點應該都會正確設定。</span><span class="sxs-lookup"><span data-stu-id="605eb-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="605eb-175">執行 STAR-CCM+ 作業</span><span class="sxs-lookup"><span data-stu-id="605eb-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="605eb-176">HPC Pack 用於其順序 toorun 星狀中的工作排程器功能-CCM + 作業。</span><span class="sxs-lookup"><span data-stu-id="605eb-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="605eb-177">toodo 因此，我們需要 hello 的幾個指令碼會使用的 toostart hello 作業，而且執行星狀支援-CCM +。</span><span class="sxs-lookup"><span data-stu-id="605eb-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="605eb-178">hello 輸入的資料保留在 hello Azure 檔案共用上為了簡單起見，第一個。</span><span class="sxs-lookup"><span data-stu-id="605eb-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="605eb-179">下列 PowerShell 指令碼的 hello 是使用的 tooqueue 星狀-CCM + 作業。</span><span class="sxs-lookup"><span data-stu-id="605eb-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="605eb-180">它會採用三個引數︰</span><span class="sxs-lookup"><span data-stu-id="605eb-180">It takes three arguments:</span></span>

* <span data-ttu-id="605eb-181">hello 模型名稱</span><span class="sxs-lookup"><span data-stu-id="605eb-181">hello model name</span></span>
* <span data-ttu-id="605eb-182">使用節點 toobe 的 hello 數字</span><span class="sxs-lookup"><span data-stu-id="605eb-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="605eb-183">使用每個節點 toobe 核心的 hello 數量</span><span class="sxs-lookup"><span data-stu-id="605eb-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="605eb-184">因為星狀-CCM + 可以填入 hello 記憶體頻寬，其通常最好 toouse 較少的每個核心計算節點，並加入新節點。</span><span class="sxs-lookup"><span data-stu-id="605eb-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="605eb-185">每個節點的核心 hello 確切數目將取決於 hello 處理器系列和 hello 相互連接速度。</span><span class="sxs-lookup"><span data-stu-id="605eb-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="605eb-186">hello 節點配置專用的 hello 作業並不能與其他工作共用。</span><span class="sxs-lookup"><span data-stu-id="605eb-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="605eb-187">hello 工作未直接啟動為 MPI 工作。</span><span class="sxs-lookup"><span data-stu-id="605eb-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="605eb-188">hello **runstarccm.sh**殼層指令碼會啟動 hello MPI 啟動器。</span><span class="sxs-lookup"><span data-stu-id="605eb-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="605eb-189">hello 輸入模型和 hello **runstarccm.sh**指令碼會儲存在 hello **/hpcdata**先前已裝載的共用。</span><span class="sxs-lookup"><span data-stu-id="605eb-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="605eb-190">記錄檔命名的 hello 作業識別碼，而且會儲存在 hello **/hpcdata 共用**，連同 hello 星狀-CCM + 輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="605eb-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="605eb-191">範例 SubmitStarccmJob.ps1 指令碼</span><span class="sxs-lookup"><span data-stu-id="605eb-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="605eb-192">將 **runner.java** 取代成您偏好的 STAR-CCM+ Java 模型啟動程式與記錄程式碼。</span><span class="sxs-lookup"><span data-stu-id="605eb-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="605eb-193">範例 runstarccm.sh 指令碼</span><span class="sxs-lookup"><span data-stu-id="605eb-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="605eb-194">在我們的測試中，我們使用的是 Power-One-Demand 授權權杖。</span><span class="sxs-lookup"><span data-stu-id="605eb-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="605eb-195">您必須在該語彙基元，tooset hello **$CDLMD_LICENSE_FILE**環境變數太**1999@flex.cd-adapco.com**  hello hello 鍵**-podkey** hello 命令列選項.</span><span class="sxs-lookup"><span data-stu-id="605eb-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="605eb-196">某些在初始化之後，hello 指令碼-從擷取 hello **$CCP_NODES_CORES** HPC Pack 設定-環境變數 hello 節點 toobuild hello MPI 啟動器 hostfile 使用的清單。</span><span class="sxs-lookup"><span data-stu-id="605eb-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="605eb-197">此 hostfile 將包含 hello 的 hello 工作，每行一個名稱會用於計算節點名稱清單。</span><span class="sxs-lookup"><span data-stu-id="605eb-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="605eb-198">hello 格式**$CCP_NODES_CORES**遵循下列模式：</span><span class="sxs-lookup"><span data-stu-id="605eb-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="605eb-199">其中：</span><span class="sxs-lookup"><span data-stu-id="605eb-199">Where:</span></span>

* <span data-ttu-id="605eb-200">`<Number of nodes>`是 hello 配置 toothis 工作的節點數目。</span><span class="sxs-lookup"><span data-stu-id="605eb-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="605eb-201">`<Name of node_n_...>`這是每個節點配置 toothis 作業 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="605eb-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="605eb-202">`<Cores of node_n_...>`是 hello hello 節點配置 toothis 工作上的核心數目。</span><span class="sxs-lookup"><span data-stu-id="605eb-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="605eb-203">hello 的核心數目 (**$NBCORES**) 也是導出根據的 hello 節點數目 (**$NBNODES**) 和 hello 每個節點的核心數目 (當做參數提供**$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="605eb-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="605eb-204">Hello MPI 選項，hello 與 Intel MPI 在 Azure 上搭配使用的是：</span><span class="sxs-lookup"><span data-stu-id="605eb-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="605eb-205">`-mpi intel`toospecify Intel MPI。</span><span class="sxs-lookup"><span data-stu-id="605eb-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="605eb-206">`-fabric UDAPL`toouse Azure 的 InfiniBand 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="605eb-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="605eb-207">`-cpubind bandwidth,v`星形的 MPI toooptimize 頻寬-CCM +。</span><span class="sxs-lookup"><span data-stu-id="605eb-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="605eb-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI 與 Azure 的 InfiniBand 並 tooset hello 所需的每個節點的核心數目。</span><span class="sxs-lookup"><span data-stu-id="605eb-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="605eb-209">`-batch`toostart 星狀-CCM + 批次模式中沒有使用者介面。</span><span class="sxs-lookup"><span data-stu-id="605eb-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="605eb-210">最後，toostart 作業，請確定您的節點正在執行，而且都已上線的叢集管理員 中。</span><span class="sxs-lookup"><span data-stu-id="605eb-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="605eb-211">然後從 PowerShell 命令提示字元中，執行此作業︰</span><span class="sxs-lookup"><span data-stu-id="605eb-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="605eb-212">停止節點</span><span class="sxs-lookup"><span data-stu-id="605eb-212">Stop nodes</span></span>
<span data-ttu-id="605eb-213">稍後您已完成測試之後，您可以使用下列 HPC Pack PowerShell 命令 toostop hello，並啟動節點：</span><span class="sxs-lookup"><span data-stu-id="605eb-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="605eb-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="605eb-214">Next steps</span></span>
<span data-ttu-id="605eb-215">嘗試執行其他 Linux 工作負載。</span><span class="sxs-lookup"><span data-stu-id="605eb-215">Try running other Linux workloads.</span></span> <span data-ttu-id="605eb-216">例如，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="605eb-216">For example, see:</span></span>

* [<span data-ttu-id="605eb-217">在 Azure 中的 Linux 運算節點以 Microsoft HPC Pack 執行 NAMD</span><span class="sxs-lookup"><span data-stu-id="605eb-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="605eb-218">在 Azure 中的 Linux RDMA 叢集以 Microsoft HPC Pack 執行 OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="605eb-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
