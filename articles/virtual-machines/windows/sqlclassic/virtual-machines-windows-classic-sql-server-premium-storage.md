---
title: "aaaUse Azure 高階儲存體與 SQL Server |Microsoft 文件"
description: "這篇文章會使用與 hello 傳統部署模型，建立的資源，並提供指引 Azure 虛擬機器上執行的 SQL Server 搭配使用 Azure 高階儲存體。"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a><span data-ttu-id="5bc7b-103">在虛擬機器上搭配使用 Azure 進階儲存體和 SQL Server</span><span class="sxs-lookup"><span data-stu-id="5bc7b-103">Use Azure Premium Storage with SQL Server on Virtual Machines</span></span>
## <a name="overview"></a><span data-ttu-id="5bc7b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="5bc7b-104">Overview</span></span>
<span data-ttu-id="5bc7b-105">[Azure 高階儲存體](../../../storage/common/storage-premium-storage.md)是 hello 的存放裝置，可提供低延遲、 高輸送量 IO 的下一個層代。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-105">[Azure Premium Storage](../../../storage/common/storage-premium-storage.md) is hello next generation of storage that provides low latency and high throughput IO.</span></span> <span data-ttu-id="5bc7b-106">它最適合用於需要大量 IO 的重要工作負載，例如，IaaS [虛擬機器](https://azure.microsoft.com/services/virtual-machines/)上的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-106">It works best for key IO intensive workloads, such as SQL Server on IaaS [Virtual Machines](https://azure.microsoft.com/services/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bc7b-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5bc7b-108">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5bc7b-109">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="5bc7b-110">本文章提供了規劃及移轉執行 SQL Server toouse 高階儲存體的虛擬機器的指引。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-110">This article provides planning and guidance for migrating a Virtual Machine running SQL Server toouse Premium Storage.</span></span> <span data-ttu-id="5bc7b-111">這包括 Azure 基礎結構 (網路功能、儲存體) 和客體 Windows VM 步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-111">This includes Azure infrastructure (networking, storage) and guest Windows VM steps.</span></span> <span data-ttu-id="5bc7b-112">在 hello hello 範例[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)示範如何改進 toomove 較大 Vm tootake 利用完整的完整結束 tooend 移轉本機 SSD 儲存裝置使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-112">hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) shows a full comprehensive end tooend migration of how toomove larger VMs tootake advantage of improved local SSD storage with PowerShell.</span></span>

<span data-ttu-id="5bc7b-113">它是重要的 toounderstand hello 端對端程序與 IAAS Vm 上的 SQL Server 利用 Azure 高階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-113">It is important toounderstand hello end-to-end process of utilizing Azure Premium Storage with SQL Server on IAAS VMs.</span></span> <span data-ttu-id="5bc7b-114">其中包括：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-114">This includes:</span></span>

* <span data-ttu-id="5bc7b-115">Hello 必要條件 toouse 高階儲存體的識別。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-115">Identification of hello prerequisites toouse Premium Storage.</span></span>
* <span data-ttu-id="5bc7b-116">針對新部署的 IaaS tooPremium 儲存體上部署 SQL Server 的範例。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-116">Examples of deploying SQL Server on IaaS tooPremium Storage for new deployments.</span></span>
* <span data-ttu-id="5bc7b-117">移轉現有部署的範例，其中包括使用 SQL Always On 可用性群組的獨立伺服器和部署。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-117">Examples of migrating existing deployments, both stand-alone servers and deployments using SQL Always On Availability Groups.</span></span>
* <span data-ttu-id="5bc7b-118">可能的移轉方法。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-118">Possible migration approaches.</span></span>
* <span data-ttu-id="5bc7b-119">完整端對端範例，示範 hello 移轉現有的 Alwayson 實作 Azure、 Windows 和 SQL Server 的步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-119">Full end-to-end example showing Azure, Windows, and SQL Server steps for hello migration of an existing Always On implementation.</span></span>

<span data-ttu-id="5bc7b-120">如需更多關於 Azure 虛擬機器中 SQL Server 的背景資訊，請參閱 [Azure 虛擬機器中的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-120">For more background information on SQL Server in Azure Virtual Machines, see [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

<span data-ttu-id="5bc7b-121">**作者：**Daniel Sol **技術審稿人員：**Luis Carlos Vargas Herring、Sanjay Mishra、Pravin Mital、Juergen Thomas、Gonzalo Ruiz。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-121">**Author:** Daniel Sol **Technical Reviewers:** Luis Carlos Vargas Herring, Sanjay Mishra, Pravin Mital, Juergen Thomas, Gonzalo Ruiz.</span></span>

## <a name="prerequisites-for-premium-storage"></a><span data-ttu-id="5bc7b-122">適用於進階儲存體的必要條件</span><span class="sxs-lookup"><span data-stu-id="5bc7b-122">Prerequisites for Premium Storage</span></span>
<span data-ttu-id="5bc7b-123">使用進階儲存體之前，必須具備數個必要條件。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-123">There are several prerequisites for using Premium Storage.</span></span>

### <a name="machine-size"></a><span data-ttu-id="5bc7b-124">機器大小</span><span class="sxs-lookup"><span data-stu-id="5bc7b-124">Machine size</span></span>
<span data-ttu-id="5bc7b-125">使用進階儲存體，您必須 toouse DS 系列虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-125">For using Premium Storage you will need toouse DS series Virtual Machines (VM).</span></span> <span data-ttu-id="5bc7b-126">如果您不在雲端服務，才能使用 DS 系列機器，則必須刪除現有 VM 的 hello、 保持 hello 附加磁碟，並再建立新的雲端服務，再重新建立 hello 與 DS * 角色大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-126">If you have not used DS Series machines in your cloud service before, you must delete hello existing VM, keep hello attached disks, and then create a new cloud service before recreating hello VM as DS* role size.</span></span> <span data-ttu-id="5bc7b-127">如需虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器和雲端服務大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-127">For more information on Virtual Machine sizes, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="cloud-services"></a><span data-ttu-id="5bc7b-128">雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bc7b-128">Cloud services</span></span>
<span data-ttu-id="5bc7b-129">如果 DS* VM 和進階儲存體是建立在新的雲端服務中，則您只能搭配使用它們。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-129">You can only use DS* VMs with Premium Storage when they are created in a new cloud service.</span></span> <span data-ttu-id="5bc7b-130">如果您在 Azure 中使用 SQL Server Alwayson，hello 一定在接聽程式會參考與雲端服務相關聯的 toohello Azure 內部或外部負載平衡器 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-130">If you are using SQL Server Always On in Azure, hello Always On Listener will refer toohello Azure Internal or External Load Balancer IP address that is associated with a cloud service.</span></span> <span data-ttu-id="5bc7b-131">本文著重在如何 toomigrate 維持在這個案例中的可用性。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-131">This article focuses on how toomigrate while maintaining availability in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-132">DS * 數列必須 hello 第一個 VM 是已部署的 toohello 新的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-132">A DS* Series must be hello first VM that is deployed toohello new Cloud Service.</span></span>
>
>

### <a name="regional-vnets"></a><span data-ttu-id="5bc7b-133">區域 VNET</span><span class="sxs-lookup"><span data-stu-id="5bc7b-133">Regional VNETS</span></span>
<span data-ttu-id="5bc7b-134">DS * vm，您必須設定虛擬網路 (VNET) 裝載您的 Vm toobe 地區 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-134">For DS* VMs you must configure hello Virtual Network (VNET) hosting your VMs toobe regional.</span></span> <span data-ttu-id="5bc7b-135">這個 「 放大 」 hello VNET tooallow hello 較大 Vm toobe 其他叢集中佈建並允許兩者之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-135">This “widens” hello VNET is tooallow hello larger VMs toobe provisioned in other clusters and allow communication between them.</span></span> <span data-ttu-id="5bc7b-136">在下列螢幕擷取畫面的 hello，hello 反白顯示的位置會顯示區域 Vnet，而 hello 第一個結果會顯示"narrow"VNET。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-136">In hello following screenshot, hello highlighted Location shows regional VNETs, whereas hello first result shows a “narrow” VNET.</span></span>

![RegionalVNET][1]

<span data-ttu-id="5bc7b-138">您可以提高 Microsoft 支援票證 toomigrate tooa 區域 VNET，Microsoft 將會進行變更，然後 toocomplete hello 移轉 tooregional Vnet，變更 hello 屬性 AffinityGroup hello 網路組態中的。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-138">You can raise a Microsoft support ticket toomigrate tooa regional VNET, Microsoft will make a change, then toocomplete hello migration tooregional VNETs, change hello property AffinityGroup in hello network configuration.</span></span> <span data-ttu-id="5bc7b-139">先匯出 hello 在 PowerShell 中，網路組態，並取代 hello **AffinityGroup**屬性在 hello **VirtualNetworkSite**具有項目**位置**屬性。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-139">First export hello Network Configuration in PowerShell, and then replace hello **AffinityGroup** property in hello **VirtualNetworkSite** element with a **Location** property.</span></span> <span data-ttu-id="5bc7b-140">指定 `Location = XXXX`，其中 `XXXX` 為 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-140">Specify `Location = XXXX` where `XXXX` is an Azure region.</span></span> <span data-ttu-id="5bc7b-141">然後匯入 hello 新組態。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-141">Then import hello new configuration.</span></span>

<span data-ttu-id="5bc7b-142">例如，考慮下列 VNET 組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-142">For example, considering hello following VNET configuration:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

<span data-ttu-id="5bc7b-143">toomove 此 tooa 區域 VNET 中西歐，變更下列 hello 組態 toohello:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-143">toomove this tooa regional VNET in West Europe, change hello configuration toohello following:</span></span>

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a><span data-ttu-id="5bc7b-144">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bc7b-144">Storage accounts</span></span>
<span data-ttu-id="5bc7b-145">您將需要 toocreate Premium 儲存體設定的新儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-145">You will need toocreate a new storage account that is configured for Premium Storage.</span></span> <span data-ttu-id="5bc7b-146">請注意 hello 使用 Premium 儲存體設定在 hello 儲存體帳戶，不能在個別的 Vhd，但使用 DS * 系列 VM 時您可以將 VHD 附加來自 Premium 和標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-146">Note that hello use of Premium Storage is set at hello storage account, not on individual VHDs, however when using a DS* Series VM you can attach VHD’s from Premium and Standard Storage accounts.</span></span> <span data-ttu-id="5bc7b-147">如果您不想 tooplace hello OS VHD toohello 高階儲存體帳戶上的，您可以考慮此。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-147">You may consider this if you do not want tooplace hello OS VHD on toohello Premium Storage account.</span></span>

<span data-ttu-id="5bc7b-148">hello 下列**新增 AzureStorageAccountPowerShell**命令與 hello"Premium_LRS"**類型**建立進階儲存體帳戶：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-148">hello following **New-AzureStorageAccountPowerShell** command with hello "Premium_LRS" **Type** creates a Premium Storage Account:</span></span>

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a><span data-ttu-id="5bc7b-149">VHD 快取設定</span><span class="sxs-lookup"><span data-stu-id="5bc7b-149">VHDs Cache Settings</span></span>
<span data-ttu-id="5bc7b-150">hello 之間建立磁碟屬於高階儲存體帳戶的主要差異在於 hello 磁碟快取設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-150">hello main difference between creating disks that are part of a Premium Storage account is hello disk cache setting.</span></span> <span data-ttu-id="5bc7b-151">針對 SQL Server 資料磁碟區磁碟，建議使用 [讀取快取]。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-151">For SQL Server Data volume disks it is recommended that you use ‘**Read Caching**’.</span></span> <span data-ttu-id="5bc7b-152">交易記錄磁碟區，hello 磁碟快取應該設定太 '**無**'。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-152">For Transaction log volumes, hello disk cache setting should be set too‘**None**’.</span></span> <span data-ttu-id="5bc7b-153">這點不同於標準儲存體帳戶的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-153">This is different from hello recommendations for Standard Storage accounts.</span></span>

<span data-ttu-id="5bc7b-154">在附加 hello Vhd 之後，就無法改變 hello 快取設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-154">Once hello VHDs have been attached, hello cache setting cannot be altered.</span></span> <span data-ttu-id="5bc7b-155">您會需要 toodetach，再重新 hello VHD 附加更新之快取設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-155">You would need toodetach and reattach hello VHD with an updated cache setting.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="5bc7b-156">Windows 儲存空間</span><span class="sxs-lookup"><span data-stu-id="5bc7b-156">Windows storage spaces</span></span>
<span data-ttu-id="5bc7b-157">您可以使用[Windows 儲存空間](https://technet.microsoft.com/library/hh831739.aspx)一樣與先前標準儲存體，這可讓您 toomigrate 已經利用儲存空間的 VM。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-157">You can use [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) as you did with previous Standard Storage, this will allow you toomigrate a VM that is already utilizing Storage Spaces.</span></span> <span data-ttu-id="5bc7b-158">中的 hello 範例[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)（步驟 9 和轉送） 示範 hello Powershell 程式碼 tooextract 並匯入具有多個附加 Vhd 的 VM。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-158">hello example in [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (step 9 and forward) demonstrates hello Powershell code tooextract and import a VM with multiple attached VHDs.</span></span>

<span data-ttu-id="5bc7b-159">存放集區已使用標準的 Azure 儲存體帳戶 tooenhance 輸送量，並降低延遲。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-159">Storage Pools were used with Standard Azure storage account tooenhance throughput and reduce latency.</span></span> <span data-ttu-id="5bc7b-160">您可能會在針對新部署測試含有進階儲存體的儲存集區時尋找值，但它們會為儲存體設定增加額外的複雜度。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-160">You might find value in testing Storage Pools with Premium Storage for new deployments, but they do add additional complexity with storage setup.</span></span>

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a><span data-ttu-id="5bc7b-161">如何 toofind 哪些 Azure 的虛擬磁碟對應 toostorage 集區</span><span class="sxs-lookup"><span data-stu-id="5bc7b-161">How toofind which Azure Virtual Disks map toostorage pools</span></span>
<span data-ttu-id="5bc7b-162">附加 vhd 建議不同的快取設定時，您可能決定 toocopy hello Vhd tooa 高階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-162">As there are different cache setting recommendations for attached VHDs, you might decide toocopy hello VHDs tooa Premium Storage account.</span></span> <span data-ttu-id="5bc7b-163">不過，當您重新附加 toohello 新 DS 系列 VM，您可能需要 tooalter hello 快取設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-163">However, when you reattach them toohello new DS series VM, you might need tooalter hello cache settings.</span></span> <span data-ttu-id="5bc7b-164">它是簡單 tooapply hello 高階儲存體建議的快取設定，當您有不同的 Vhd 的 hello SQL 資料檔案和記錄檔 （而非同時包含單一 VHD）。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-164">It is simpler tooapply hello Premium Storage recommended cache settings when you have separate VHDs for hello SQL Data files and log files (rather than a single VHD that contains both).</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-165">如果您擁有的 hello 相同的磁碟區，hello 快取您選擇的選項取決於針對資料庫工作負載的 hello IO 存取模式上的 SQL Server 資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-165">If you have SQL Server data and log files on hello same volume, hello caching option you choose depends on hello IO access patterns for your database workloads.</span></span> <span data-ttu-id="5bc7b-166">只有測試可以示範哪一個快取選項最適合這個案例。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-166">Only testing can demonstrate which caching option is best for this scenario.</span></span>
>
>

<span data-ttu-id="5bc7b-167">然而，如果您使用 Windows 儲存空間，其中的多個 Vhd，您必須在 toolook 組成您原始的指令碼 tooidentify 附加 Vhd 是在哪個特定集區，因此您可以再設定 hello 快取設定據以每個磁碟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-167">However, if you are using Windows Storage Spaces which are made up of multiple VHDs you will need toolook at your original scripts tooidentify which attached VHDs are in what specific pool, so you can then set hello cache settings accordingly for each disk.</span></span>

<span data-ttu-id="5bc7b-168">如果您不需要原始指令碼可用 tooshow 您 Vhd 對應 toohello 儲存集區，您可以使用下列步驟 toodetermine hello 磁碟/儲存體集區對應的 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-168">If you do not have original script available tooshow you which VHDs map toohello storage pool, you can use hello following steps toodetermine hello disk/storage pool mapping.</span></span>

<span data-ttu-id="5bc7b-169">每個磁碟，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-169">For each disk, use hello following steps:</span></span>

1. <span data-ttu-id="5bc7b-170">取得清單的磁碟附加以 hello tooVM **Get-azurevm**命令：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-170">Get list of disks attached tooVM with hello **Get-AzureVM** command:</span></span>

    <span data-ttu-id="5bc7b-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span><span class="sxs-lookup"><span data-stu-id="5bc7b-171">Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk</span></span>
2. <span data-ttu-id="5bc7b-172">請注意 hello Diskname 和 LUN。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-172">Note hello Diskname and LUN.</span></span>

    ![DisknameAndLUN][2]
3. <span data-ttu-id="5bc7b-174">遠端桌面連接到 hello VM 的資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-174">Remote desktop into hello VM.</span></span> <span data-ttu-id="5bc7b-175">然後跳過**電腦管理** | **裝置管理員** | **磁碟機**。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-175">Then go too**Computer Management** | **Device Manager** | **Disk Drives**.</span></span> <span data-ttu-id="5bc7b-176">查看每一個 hello ' Microsoft 虛擬磁碟的' hello 屬性</span><span class="sxs-lookup"><span data-stu-id="5bc7b-176">Look at hello properties of each of hello ‘Microsoft Virtual Disks’</span></span>

    ![VirtualDiskProperties][3]
4. <span data-ttu-id="5bc7b-178">hello LUN 編號是您指定當附加 hello VHD toohello VM 參考 toohello LUN 編號。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-178">hello LUN number here is a reference toohello LUN number you specify when attaching hello VHD toohello VM.</span></span>
5. <span data-ttu-id="5bc7b-179">Hello 'Microsoft 虛擬磁碟' go toohello**詳細資料** 索引標籤，然後在 hello**屬性**清單中，跳過**驅動程式機碼**。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-179">For hello ‘Microsoft Virtual Disk’ go toohello **Details** tab, then in hello **Property** list, go too**Driver Key**.</span></span> <span data-ttu-id="5bc7b-180">在 hello**值**，注意 hello**位移**，也就是在下列螢幕擷取畫面的 hello 0002。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-180">In hello **Value**, note hello **Offset**, which is 0002 in hello following screenshot.</span></span> <span data-ttu-id="5bc7b-181">hello 0002 代表 hello PhysicalDisk2 的 hello 存放集區的參考。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-181">hello 0002 denotes hello PhysicalDisk2 that hello storage pool references.</span></span>

    ![VirtualDiskPropertyDetails][4]
6. <span data-ttu-id="5bc7b-183">對於每個儲存集區，傾印出 hello 相關聯的磁碟：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-183">For each storage pool, dump out hello associated disks:</span></span>

    <span data-ttu-id="5bc7b-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span><span class="sxs-lookup"><span data-stu-id="5bc7b-184">Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk</span></span>

    ![GetStoragePool][5]

<span data-ttu-id="5bc7b-186">現在您可以使用此資訊 tooassociate 附加 Vhd tooPhysical 磁碟儲存集區中。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-186">Now you can use this information tooassociate attached VHDs tooPhysical Disks in Storage Pools.</span></span>

<span data-ttu-id="5bc7b-187">一旦您已對應儲存集區，您可以卸離並複製 tooa 高階儲存體帳戶中的 Vhd tooPhysical 磁碟，然後將其連接與 hello 正確快取設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-187">Once you have mapped VHDs tooPhysical Disks in Storage Pools you can then detach and copy them over tooa Premium Storage account, then attach them with hello correct cache setting.</span></span> <span data-ttu-id="5bc7b-188">在 hello hello 範例，請參閱[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)，步驟 8 到 12。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-188">Please see hello example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), steps 8 through 12.</span></span> <span data-ttu-id="5bc7b-189">這些步驟顯示 tooextract VM 連接的 VHD 磁碟組態 tooa CSV 檔案中，如何複製 hello Vhd、 改變 hello 磁碟快取設定，以及最後重新 hello VM 部署為以所有 hello DS 系列 VM 附加磁碟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-189">These steps show how tooextract a VM-attached VHD disk configuration tooa CSV file, copy hello VHDs, alter hello disk configuration cache settings, and finally redeploy hello VM as a DS series VM with all hello attached disks.</span></span>

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a><span data-ttu-id="5bc7b-190">VM 儲存體頻寬和 VHD 儲存體輸送量</span><span class="sxs-lookup"><span data-stu-id="5bc7b-190">VM storage bandwidth and VHD storage throughput</span></span>
<span data-ttu-id="5bc7b-191">儲存體效能的 hello 數量 hello DS * VM 大小指定與 hello VHD 大小而定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-191">hello amount of storage performance depends on hello DS* VM size specified and hello VHD sizes.</span></span> <span data-ttu-id="5bc7b-192">hello Vm 有不同的額度 hello 可附加和 hello 它們將支援 (MB/s) 的最大頻寬的 Vhd 數目。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-192">hello VMs have different allowances for hello number of VHDs that can be attached and hello maximum bandwidth they will support (MB/s).</span></span> <span data-ttu-id="5bc7b-193">Hello 特定頻寬號碼，請參閱[虛擬機器和 Azure 的雲端服務大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-193">For hello specific bandwidth numbers, see [Virtual Machine and Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5bc7b-194">提高 IOPS 可透過更大的磁碟大小來達成。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-194">Increased IOPS are achieved with larger disk sizes.</span></span> <span data-ttu-id="5bc7b-195">當您考量移轉路徑時，應將這點納入考慮。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-195">You should consider this when you think about your migration path.</span></span> <span data-ttu-id="5bc7b-196">如需詳細資訊， [IOPS 和磁碟類型，請參閱 hello 表格](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-196">For details, [see hello table for IOPS and Disk Types](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).</span></span>

<span data-ttu-id="5bc7b-197">最後，請考量 VM 對於所有連結磁碟支援的磁碟頻寬上限各有不同。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-197">Finally, consider that VMs have different maximum disk bandwidths they will support for all disks attached.</span></span> <span data-ttu-id="5bc7b-198">負載過高，您無法 saturate hello 適用於該 VM 角色大小的最大磁碟頻寬。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-198">Under high load, you could saturate hello maximum disk bandwidth available for that VM role size.</span></span> <span data-ttu-id="5bc7b-199">例如 Standard_DS14 會支援註冊 too512MB/s;因此，您無法使用三個 P30 磁碟 saturate hello 磁碟頻寬的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-199">For example a Standard_DS14 will support up too512MB/s; therefore, with three P30 disks you could saturate hello disk bandwidth of hello VM.</span></span> <span data-ttu-id="5bc7b-200">但在此範例中，hello 輸送量限制可能會超過根據 hello 混合的讀取和寫入 IOs。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-200">But in this example, hello throughput limit could be exceeded depending on hello mix of read and write IOs.</span></span>

## <a name="new-deployments"></a><span data-ttu-id="5bc7b-201">新的部署</span><span class="sxs-lookup"><span data-stu-id="5bc7b-201">New deployments</span></span>
<span data-ttu-id="5bc7b-202">hello 下兩節將示範如何部署 SQL Server Vm tooPremium 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-202">hello next two sections demonstrate how you can deploy SQL Server VMs tooPremium Storage.</span></span> <span data-ttu-id="5bc7b-203">如前所述，您不一定需要 tooplace hello OS 磁碟至進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-203">As mentioned before, you do not necessarily need tooplace hello OS disk onto Premium storage.</span></span> <span data-ttu-id="5bc7b-204">您可以選擇 toodo 這如果在 hello OS VHD 想 tooplace 任何需要大量 IO 工作負載。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-204">You might choose toodo this if you are intending tooplace any intensive IO workloads on hello OS VHD.</span></span>

<span data-ttu-id="5bc7b-205">hello 第一個範例會示範利用現有的 Azure 資源庫映像。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-205">hello first example demonstrates utilizing existing Azure Gallery Images.</span></span> <span data-ttu-id="5bc7b-206">hello 第二個範例會示範如何 toouse 自訂 VM 映像，您在現有的標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-206">hello second example shows how toouse a custom VM image that you have in an existing Standard storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-207">這些範例假設您已經建立區域 VNET。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-207">These examples assume that you have already created a Regional VNET.</span></span>
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a><span data-ttu-id="5bc7b-208">使用資源庫映像建立含有進階儲存體的新 VM</span><span class="sxs-lookup"><span data-stu-id="5bc7b-208">Create a new VM with Premium Storage with Gallery Image</span></span>
<span data-ttu-id="5bc7b-209">下列的 hello 範例示範如何 tooplace hello OS VHD 至進階儲存體，並附加 Premium 儲存體的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-209">hello example below shows how tooplace hello OS VHD onto premium storage and attach Premium Storage VHDs.</span></span> <span data-ttu-id="5bc7b-210">不過，也將 hello OS 磁碟放在標準儲存體帳戶，然後再附加在高階儲存體帳戶中的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-210">However, you can also place hello OS disk in a Standard Storage account and then attach VHDs that reside in a Premium Storage account.</span></span> <span data-ttu-id="5bc7b-211">以下將示範這兩個案例。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-211">Both scenarios are demonstrated.</span></span>

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a><span data-ttu-id="5bc7b-212">步驟 1：建立進階儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bc7b-212">Step 1: Create a Premium Storage Account</span></span>
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a><span data-ttu-id="5bc7b-213">步驟 2：建立新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bc7b-213">Step 2: Create a New Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a><span data-ttu-id="5bc7b-214">步驟 3：保留雲端服務 VIP (選用)</span><span class="sxs-lookup"><span data-stu-id="5bc7b-214">Step 3: Reserve a Cloud Service VIP (Optional)</span></span>
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a><span data-ttu-id="5bc7b-215">步驟 4：建立 VM 容器</span><span class="sxs-lookup"><span data-stu-id="5bc7b-215">Step 4: Create a VM Container</span></span>
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a><span data-ttu-id="5bc7b-216">步驟 5：在標準或進階儲存體上放置作業系統 VHD</span><span class="sxs-lookup"><span data-stu-id="5bc7b-216">Step 5: Placing OS VHD on Standard or Premium Storage</span></span>
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a><span data-ttu-id="5bc7b-217">步驟 6：建立 VM</span><span class="sxs-lookup"><span data-stu-id="5bc7b-217">Step 6: Create VM</span></span>
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a><span data-ttu-id="5bc7b-218">使用自訂映像建立新的 VM toouse 高階儲存體</span><span class="sxs-lookup"><span data-stu-id="5bc7b-218">Create a new VM toouse Premium Storage with a custom image</span></span>
<span data-ttu-id="5bc7b-219">這個案例示範您現有的自訂映像是位於標準儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-219">This scenario demonstrates where you have existing customized images that reside in a Standard Storage account.</span></span> <span data-ttu-id="5bc7b-220">如所述，如果您要 tooplace hello OS VHD 高階儲存體，您將需要 toocopy hello hello 標準儲存體帳戶中存在的映像，並將它們傳送 tooa 高階儲存體，才能使用。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-220">As mentioned if you want tooplace hello OS VHD on Premium Storage you will need toocopy hello image that exists in hello Standard Storage account and transfer them tooa Premium Storage before it can be used.</span></span> <span data-ttu-id="5bc7b-221">如果您有映像內部部署，您可以也使用此方法 toocopy 直接 toohello 高階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-221">If you have an image on-premises, you can also use this method toocopy that directly toohello Premium Storage account.</span></span>

#### <a name="step-1-create-storage-account"></a><span data-ttu-id="5bc7b-222">步驟 1：建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bc7b-222">Step 1: Create Storage Account</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a><span data-ttu-id="5bc7b-223">步驟 2：建立雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bc7b-223">Step 2 Create Cloud Service</span></span>
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a><span data-ttu-id="5bc7b-224">步驟 3：使用現有的映像</span><span class="sxs-lookup"><span data-stu-id="5bc7b-224">Step 3: Use existing image</span></span>
<span data-ttu-id="5bc7b-225">您可以使用現有的映像。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-225">You can use an existing image.</span></span> <span data-ttu-id="5bc7b-226">或者，您可以 [取得現有機器的映像](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-226">Or, you can [take an image of an existing machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="5bc7b-227">請注意 hello 機器映像沒有 toobe DS * 機器。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-227">Note hello machine you image does not have toobe DS* machine.</span></span> <span data-ttu-id="5bc7b-228">一旦您擁有 hello 映像時，下列步驟顯示如何 hello toocopy 它 toohello 高階儲存體帳戶以 hello**開始 AzureStorageBlobCopy** PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-228">Once you have hello image, hello following steps show how toocopy it toohello Premium Storage account with hello **Start-AzureStorageBlobCopy** PowerShell commandlet.</span></span>

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a><span data-ttu-id="5bc7b-229">步驟 4：在儲存帳戶間複製 Blob</span><span class="sxs-lookup"><span data-stu-id="5bc7b-229">Step 4: Copy Blob between Storage Accounts</span></span>
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a><span data-ttu-id="5bc7b-230">步驟 5：定期檢查複製狀態：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-230">Step 5: Regularly check copy status:</span></span>
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a><span data-ttu-id="5bc7b-231">步驟 6： 加入訂用帳戶中的映像磁碟 tooAzure 磁碟儲存機制</span><span class="sxs-lookup"><span data-stu-id="5bc7b-231">Step 6: Add Image disk tooAzure disk Repository in Subscription</span></span>
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> <span data-ttu-id="5bc7b-232">您可能會發現即使 hello 狀態報告為成功，您可能仍然收到磁碟租用錯誤。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-232">You may find that even though hello status reports as success, you could still get a disk lease error.</span></span> <span data-ttu-id="5bc7b-233">在此情況下，請等待大約 10 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-233">In this case, wait about 10 minutes.</span></span>
>
>

#### <a name="step-7--build-hello-vm"></a><span data-ttu-id="5bc7b-234">步驟 7： 建置 hello VM</span><span class="sxs-lookup"><span data-stu-id="5bc7b-234">Step 7:  Build hello VM</span></span>
<span data-ttu-id="5bc7b-235">這裡您要建立 hello VM 從您的映像和附加兩個 Premium 儲存體的 Vhd:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-235">Here you are building hello VM from your image and attaching two Premium Storage VHDs:</span></span>

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a><span data-ttu-id="5bc7b-236">未使用 Always On 可用性群組的現有部署</span><span class="sxs-lookup"><span data-stu-id="5bc7b-236">Existing deployments that do not use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="5bc7b-237">現有的部署中，第一次看到 hello[必要條件](#prerequisites-for-premium-storage)本主題一節。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-237">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="5bc7b-238">對於未使用「Always On 可用性群組」的 SQL Server 部署與使用該可用性群組的部署，有不同的考量。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-238">There are different considerations for SQL Server deployments that do not use Always On Availability Groups and those that do.</span></span> <span data-ttu-id="5bc7b-239">如果您不使用 Always On，且有現有的獨立 SQL Server，您可以使用新的雲端服務和儲存體帳戶來升級 tooPremium 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-239">If you are not using Always On and have an existing standalone SQL Server, you can upgrade tooPremium Storage by using a new cloud service and storage account.</span></span> <span data-ttu-id="5bc7b-240">請考慮下列選項的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-240">Consider hello following options:</span></span>

* <span data-ttu-id="5bc7b-241">**建立新的 SQL Server VM**。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-241">**Create a new SQL Server VM**.</span></span> <span data-ttu-id="5bc7b-242">您可以建立新的 SQL Server VM 來使用進階儲存體帳戶，如＜新的部署＞中所述。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-242">You can create a new SQL Server VM that uses a Premium Storage account, as documented in New Deployments.</span></span> <span data-ttu-id="5bc7b-243">然後備份並還原 SQL Server 設定和使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-243">Then backup and restore your SQL Server configuration and user databases.</span></span> <span data-ttu-id="5bc7b-244">hello 的應用程式需要更新 toobe tooreference hello 新的 SQL Server，如果它正在存取內部或外部。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-244">hello application will need toobe updated tooreference hello new SQL Server if it is being accessed internally or externally.</span></span> <span data-ttu-id="5bc7b-245">如果當您執行並存 (SxS) SQL Server 移轉您將需要指定 toocopy 所有 '超出 db' 物件。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-245">You would need toocopy all ‘out of db’ objects as if you were doing a Side by Side (SxS) SQL Server migration.</span></span> <span data-ttu-id="5bc7b-246">這包含像是登入、憑證及連結的伺服器等物件。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-246">This includes objects such as logins, certificates, and linked servers.</span></span>
* <span data-ttu-id="5bc7b-247">**移轉現有的 SQL Server VM**。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-247">**Migrate an existing SQL Server VM**.</span></span> <span data-ttu-id="5bc7b-248">這將需要離線 hello SQL Server VM，然後將它傳送 tooa 新雲端服務，其中包括將所有其附加 Vhd toohello 高階儲存體帳戶複製。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-248">This will require taking hello SQL Server VM offline, then transferring it tooa new cloud service, which includes copying all of its attached VHDs toohello Premium Storage account.</span></span> <span data-ttu-id="5bc7b-249">當 hello VM 都上線時，hello 應用程式會參考 hello 伺服器主機先前的名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-249">When hello VM comes online, hello application will reference hello server host name as before.</span></span> <span data-ttu-id="5bc7b-250">請注意，hello hello 現有磁碟大小會影響 hello 效能特性。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-250">Be aware that hello size of hello existing disk will affect hello performance characteristics.</span></span> <span data-ttu-id="5bc7b-251">例如，400 GB 磁碟取得無條件進位 tooa P20。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-251">For example, a 400 GB disk gets rounded up tooa P20.</span></span> <span data-ttu-id="5bc7b-252">如果您知道您無法重新建立 hello 為 DS 系列 VM 的 VM，並且附加您需要的 hello 大小/效能規格的 Premium 儲存體 Vhd，您不需要該磁碟效能。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-252">If you know that you do not require that disk performance, then you could recreate hello VM as a DS Series VM, and attach Premium Storage VHDs of hello size/performance specification you require.</span></span> <span data-ttu-id="5bc7b-253">您無法卸離，然後重新附加 hello SQL 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-253">Then you could detach and reattach hello SQL DB files.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-254">當複製 hello VHD 磁碟，您應該留意 hello 大小而定的 hello 大小表示 Premium 儲存體磁碟類型可將其分為，這會決定磁碟效能規格。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-254">When copying hello VHD disks you should be aware of hello size, depending on hello size will mean what Premium Storage Disk type they fall into, this determines disk performance specification.</span></span> <span data-ttu-id="5bc7b-255">Azure 會無條件向上 toohello 最接近的磁碟大小，因此如果您有 400 GB 的磁碟，這會無條件進位 tooa P20。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-255">Azure will round up toohello nearest disk size, so if you have a 400GB disk, this will be rounded up tooa P20.</span></span> <span data-ttu-id="5bc7b-256">根據 hello OS VHD 您現有 IO 需求，您可能不需要 toomigrate 此 tooa 高階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-256">Depending on your existing IO requirements of hello OS VHD, you might not need toomigrate this tooa Premium Storage account.</span></span>
>
>

<span data-ttu-id="5bc7b-257">如果您的 SQL Server 存取外部，hello 雲端服務 VIP 會變更。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-257">If your SQL Server is accessed externally, then hello cloud service VIP will change.</span></span> <span data-ttu-id="5bc7b-258">您也必須 tooupdate 結束點、 Acl 和 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-258">You will also have tooupdate end points, ACLs, and DNS settings.</span></span>

## <a name="existing-deployments-that-use-always-on-availability-groups"></a><span data-ttu-id="5bc7b-259">使用 Always On 可用性群組的現有部署</span><span class="sxs-lookup"><span data-stu-id="5bc7b-259">Existing deployments that use Always On Availability Groups</span></span>
> [!NOTE]
> <span data-ttu-id="5bc7b-260">現有的部署中，第一次看到 hello[必要條件](#prerequisites-for-premium-storage)本主題一節。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-260">For existing deployments, first see hello [Prerequisites](#prerequisites-for-premium-storage) section of this topic.</span></span>
>
>

<span data-ttu-id="5bc7b-261">在本節一開始，我們將了解 Always On 如何與「Azure 網路」互動。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-261">Initially in this section we will look at how Always On interacts with Azure Networking.</span></span> <span data-ttu-id="5bc7b-262">我們會細分 tootwo 案例中的移轉： 移轉可容許停機一段時間和您必須在此達到最短停機時間的移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-262">We will then break down migrations in tootwo scenarios: migrations where some downtime can be tolerated and migrations where you must achieve minimal downtime.</span></span>

<span data-ttu-id="5bc7b-263">內部部署的 SQL Server Always On 可用性群組會使用內部部署的接聽程式，來註冊虛擬 DNS 名稱以及 IP 位址，其可在一或多部 SQL Server 之間共用。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-263">On-premises SQL Server Always On Availability Groups use a Listener on-premises that registers a virtual DNS name along with an IP address that is shared between one or more SQL Servers.</span></span> <span data-ttu-id="5bc7b-264">用戶端連線時它們透過 hello 接聽程式 IP toohello 主要 SQL 伺服器進行路由傳送。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-264">When clients connect they are routed through hello listener IP toohello Primary SQL Server.</span></span> <span data-ttu-id="5bc7b-265">這是 hello 伺服器擁有在該時間 hello 一律在 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-265">This is hello server that owns hello Always On IP resource at that time.</span></span>

![DeploymentsUseAlways On][6]

<span data-ttu-id="5bc7b-267">在 Microsoft Azure 中您可以在 hello VM 上的一個 IP 位址指派 tooa NIC 因此在排序 tooachieve hello 相同為在內部部署的抽象層，Azure 利用 hello 分派 toohello 內部/外部負載平衡器 (ILB/ELB) 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-267">In Microsoft Azure you can have only one IP address assigned tooa NIC on hello VM, so in order tooachieve hello same layer of abstraction as on-premises, Azure utilizes hello IP address that is assigned toohello Internal/External Load Balancers (ILB/ELB).</span></span> <span data-ttu-id="5bc7b-268">hello 伺服器之間共用的 hello IP 資源設定 toohello hello ILB/ELB 為相同的 IP。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-268">hello IP resource that is shared between hello servers is set toohello same IP as hello ILB/ELB.</span></span> <span data-ttu-id="5bc7b-269">這會在 hello DNS 中發佈和用戶端流量通過 hello ILB/ELB toohello 主要 SQL Server 複本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-269">This is published in hello DNS, and client traffic is passed through hello ILB/ELB toohello Primary SQL Server replica.</span></span> <span data-ttu-id="5bc7b-270">hello ILB/ELB 知道 SQL Server 是主要，因為它會使用探查 tooprobe hello 一律在 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-270">hello ILB/ELB knows which SQL Server is primary since it uses probes tooprobe hello Always On IP resource.</span></span> <span data-ttu-id="5bc7b-271">Hello 前一個範例中，它探查每個節點都有參考 hello ELB/ILB 端點為準回應 hello 主要 SQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-271">In hello previous example, it probes each node that has an endpoint referenced by hello ELB/ILB, whichever responds is hello Primary SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-272">hello ILB 和 ELB 同時指派 tooa 特定的 Azure 雲端服務中，因此在 Azure 中的任何雲端移轉最有可能表示該 hello 負載平衡器 IP 會變更。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-272">hello ILB and ELB are both assigned tooa particular Azure cloud service, therefore any cloud migration in Azure will most likely mean that hello Load Balancer IP will change.</span></span>
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a><span data-ttu-id="5bc7b-273">移轉可允許一段停機時間的 Always On 部署</span><span class="sxs-lookup"><span data-stu-id="5bc7b-273">Migrating Always On deployments that can allow some downtime</span></span>
<span data-ttu-id="5bc7b-274">有兩種策略 toomigrate Always On 的部署，允許一些停機時間：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-274">There are two strategies toomigrate Always On deployments that allow for some downtime:</span></span>

1. <span data-ttu-id="5bc7b-275">**加入現有一律在叢集的多個次要複本 tooan**</span><span class="sxs-lookup"><span data-stu-id="5bc7b-275">**Add more secondary replicas tooan existing Always On Cluster**</span></span>
2. <span data-ttu-id="5bc7b-276">**移轉 tooa 新一律上的叢集**</span><span class="sxs-lookup"><span data-stu-id="5bc7b-276">**Migrate tooa new Always On Cluster**</span></span>

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a><span data-ttu-id="5bc7b-277">1.新增多個次要複本 tooan 現有一律上的叢集</span><span class="sxs-lookup"><span data-stu-id="5bc7b-277">1. Add more Secondary Replicas tooan Existing Always On Cluster</span></span>
<span data-ttu-id="5bc7b-278">其中一種策略是 tooadd 多個次要資料庫 toohello Alwayson 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-278">One strategy is tooadd more secondaries toohello Always On Availability Group.</span></span> <span data-ttu-id="5bc7b-279">您需要 tooadd 這些新的雲端服務，然後更新 hello 新的負載平衡器 IP hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-279">You need tooadd these into a new cloud service and update hello listener with hello new load balancer IP.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="5bc7b-280">停機時間點：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-280">Points of downtime:</span></span>
* <span data-ttu-id="5bc7b-281">叢集驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-281">Cluster Validation.</span></span>
* <span data-ttu-id="5bc7b-282">測試適用於新次要項目的 Always On 容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5bc7b-282">Testing Always On failovers for New Secondaries.</span></span>

<span data-ttu-id="5bc7b-283">如果您使用 Windows 儲存集區 hello VM 內 IO 輸送量，然後這些將會離線期間完整的叢集驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-283">If you are using Windows Storage Pools within hello VM for higher IO throughput, then these will be taken offline during a Full Cluster Validation.</span></span> <span data-ttu-id="5bc7b-284">當您新增節點 toohello 叢集需要 hello 驗證測試。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-284">hello validation test is required when you add nodes toohello cluster.</span></span> <span data-ttu-id="5bc7b-285">hello toorun hello 測試所花費的時間可能會不同，所以您應該測試這在您的代表測試環境 tooget 這所花多久的大約時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-285">hello time it takes toorun hello test can vary, so you should test this in your representative test environment tooget an approximate time of how long this will take.</span></span>

<span data-ttu-id="5bc7b-286">您應該佈建，您可以執行手動容錯移轉和 chaos 測試 hello 新加入的節點 tooensure Alwayson 高可用性函式，如預期般的時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-286">You should provision time where you can perform manual failover and chaos testing on hello newly added nodes tooensure Always On High Availability functions as expected.</span></span>

![DeploymentUseAlways On2][7]

> [!NOTE]
> <span data-ttu-id="5bc7b-288">您應該停止執行前，先 hello 驗證，其中使用 hello 存放集區的 SQL Server 的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-288">You should stop all instances of SQL Server where hello Storage Pools are used before hello Validation runs.</span></span>
>
> ##### <a name="high-level-steps"></a><span data-ttu-id="5bc7b-289">高階步驟</span><span class="sxs-lookup"><span data-stu-id="5bc7b-289">High-level steps</span></span>
>

1. <span data-ttu-id="5bc7b-290">在新的雲端服務中，使用連結的進階儲存體來建立兩部新的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-290">Create two new SQL Servers in new cloud service with attached Premium Storage.</span></span>
2. <span data-ttu-id="5bc7b-291">複製完整備份，然後使用 **NORECOVERY**進行還原。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-291">Copy over FULL backups and restore with **NORECOVERY**.</span></span>
3. <span data-ttu-id="5bc7b-292">複製「超出使用者 DB 範圍」的相依物件，例如登入等項目。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-292">Copy over ‘out of user DB’ dependent objects, such as logins etc.</span></span>
4. <span data-ttu-id="5bc7b-293">建立新的內部負載平衡器 (ILB) 或使用外部負載平衡器 (ELB)，然後在這兩個新節點上設定負載平衡的端點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-293">Create new a new Internal Load Balancer (ILB) or use an External Load Balancer (ELB), and then set up Load Balanced Endpoints on both new nodes.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5bc7b-294">檢查所有節點都都 hello 正確的端點組態，然後再繼續</span><span class="sxs-lookup"><span data-stu-id="5bc7b-294">Check all Nodes have hello correct Endpoint configuration before you continue</span></span>
   >
   >
5. <span data-ttu-id="5bc7b-295">（如果使用儲存集區），請停止使用者/應用程式存取 toohello SQL Server。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-295">Stop User/Application Access toohello SQL Server (if using Storage Pools).</span></span>
6. <span data-ttu-id="5bc7b-296">停止所有節點上的 SQL Server 引擎服務 (如果正在使用儲存集區)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-296">Stop SQL Server Engine Services on All Nodes (if using Storage Pools).</span></span>
7. <span data-ttu-id="5bc7b-297">加入新的節點 toocluster，及執行完整的驗證。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-297">Add new Nodes toocluster and run full validation.</span></span>
8. <span data-ttu-id="5bc7b-298">驗證成功之後，啟動所有 SQL Server 服務。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-298">Once Validation is successful, start all SQL Server Services.</span></span>
9. <span data-ttu-id="5bc7b-299">備份交易記錄，然後還原使用者資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-299">Backup Transaction logs, and restore user databases.</span></span>
10. <span data-ttu-id="5bc7b-300">將新節點新增至 hello Alwayson 可用性群組，並將複寫分為**同步**。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-300">Add new nodes into hello Always On Availability Group and place replication into **Synchronous**.</span></span>
11. <span data-ttu-id="5bc7b-301">新增 hello IP 位址資源的 hello 新雲端服務 ILB/ELB 透過 PowerShell for Always On 根據 hello 多網站範例中 hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-301">Add hello IP address resource of hello new Cloud Service ILB/ELB through PowerShell for Always On based on hello Multi-site example in hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span> <span data-ttu-id="5bc7b-302">在 Windows 叢集中，設定 hello**可能的擁有者**的 hello **IP 位址**資源 toohello 新節點舊。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-302">In Windows clustering, set hello **Possible owners** of hello **IP Address** resource toohello new nodes old.</span></span> <span data-ttu-id="5bc7b-303">請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-303">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
12. <span data-ttu-id="5bc7b-304">Hello 新節點的容錯移轉 tooone。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-304">Failover tooone of hello new nodes.</span></span>
13. <span data-ttu-id="5bc7b-305">請 hello 自動容錯移轉夥伴的新節點，然後測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-305">Make hello new nodes Auto Failover Partners and test failovers.</span></span>
14. <span data-ttu-id="5bc7b-306">從可用性群組移除原始節點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-306">Remove original nodes from Availability Group.</span></span>

##### <a name="advantages"></a><span data-ttu-id="5bc7b-307">優點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-307">Advantages</span></span>
* <span data-ttu-id="5bc7b-308">新的 SQL 伺服器可以是測試 （SQL Server 和應用程式），再新增 tooAlways 上。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-308">New SQL Servers can be tested (SQL Server and Application) before they are added tooAlways On.</span></span>
* <span data-ttu-id="5bc7b-309">您可以變更 hello VM 大小，並自訂 hello 儲存 tooyour 確切需求。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-309">You can change hello VM size and customize hello storage tooyour exact requirements.</span></span> <span data-ttu-id="5bc7b-310">但是，它很有幫助 tookeep 所有都 hello SQL 檔案路徑都 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-310">However, it would be beneficial tookeep all hello SQL file paths hello same.</span></span>
* <span data-ttu-id="5bc7b-311">您可以控制 hello 傳送嗨 DB 備份 toohello 次要複本會開始時。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-311">You can control when hello transfer of hello DB backups toohello Secondary Replicas are started.</span></span> <span data-ttu-id="5bc7b-312">這不同於使用 Azure**開始 AzureStorageBlobCopy** commandlet toocopy Vhd，因為這是非同步複本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-312">This differs from using Azure **Start-AzureStorageBlobCopy** commandlet toocopy VHDs, because that is an asynchronous copy.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="5bc7b-313">缺點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-313">Disadvantages</span></span>
* <span data-ttu-id="5bc7b-314">使用 Windows 儲存集區，有時叢集停機期間 hello 完整的叢集驗證 hello 新增加的節點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-314">When using Windows Storage Pools, there is Cluster downtime during hello Full Cluster Validation for hello new additional nodes.</span></span>
* <span data-ttu-id="5bc7b-315">根據 hello SQL Server 版本和次要複本的 hello 現有數目，您可能會無法 tooadd 但不會移除現有的次要資料庫的多個次要複本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-315">Depending on hello SQL Server Version and hello existing number of secondary replicas, you might not be able tooadd more secondary replicas without removing existing secondaries.</span></span>
* <span data-ttu-id="5bc7b-316">可能有長設定 hello 次要資料庫時，SQL 資料傳輸時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-316">There could be long SQL data transfer time while setting up hello secondaries.</span></span>
* <span data-ttu-id="5bc7b-317">如果您以平行方式執行新機器，則在移轉期間會產生額外的成本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-317">There is additional cost during migration while you have new machines running in parallel.</span></span>

#### <a name="2-migrate-tooa-new-always-on-cluster"></a><span data-ttu-id="5bc7b-318">2.移轉 tooa 新一律上的叢集</span><span class="sxs-lookup"><span data-stu-id="5bc7b-318">2. Migrate tooa new Always On Cluster</span></span>
<span data-ttu-id="5bc7b-319">另一個策略是新的雲端服務，然後重新導向 hello 用戶端 toouse toocreate 全新一律上包含節點的叢集全新它。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-319">Another strategy is toocreate a brand new Always On Cluster with brand new nodes in new cloud service and then redirect hello clients toouse it.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="5bc7b-320">停機時間點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-320">Points of downtime</span></span>
<span data-ttu-id="5bc7b-321">當您傳送應用程式和使用者 toohello 新 Alwayson 接聽程式時，沒有停機時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-321">There is downtime when you transfer applications and users toohello new Always On listener.</span></span> <span data-ttu-id="5bc7b-322">hello 停機時間取決於：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-322">hello downtime depends on:</span></span>

* <span data-ttu-id="5bc7b-323">hello 時間 toorestore 最後一個交易記錄備份 toodatabases 新伺服器上。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-323">hello time taken toorestore final transaction log backups toodatabases on new servers.</span></span>
* <span data-ttu-id="5bc7b-324">hello 所花費時間 tooupdate 用戶端應用程式 toouse 新 Alwayson 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-324">hello time taken tooupdate client applications toouse new Always On listener.</span></span>

##### <a name="advantages"></a><span data-ttu-id="5bc7b-325">優點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-325">Advantages</span></span>
* <span data-ttu-id="5bc7b-326">您可以測試 hello 實際執行環境，SQL Server 和作業系統組建的變更。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-326">You can test hello actual production environment, SQL Server, and OS build changes.</span></span>
* <span data-ttu-id="5bc7b-327">您已擁有 hello 選項 toocustomize hello 儲存體和 toopotentially 減少 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-327">You have hello option toocustomize hello storage and toopotentially reduce size of VM.</span></span> <span data-ttu-id="5bc7b-328">這可能會降低成本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-328">This could result in cost reduction.</span></span>
* <span data-ttu-id="5bc7b-329">您可以在此程序執行期間，更新 SQL Server 的組建或版本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-329">You can update your SQL Server build or version during this process.</span></span> <span data-ttu-id="5bc7b-330">您也可以升級 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-330">You can also upgrade hello Operating System.</span></span>
* <span data-ttu-id="5bc7b-331">hello 先前一律在叢集可以做為純色的復原目標。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-331">hello previous Always On Cluster can act as a solid rollback target.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="5bc7b-332">缺點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-332">Disadvantages</span></span>
* <span data-ttu-id="5bc7b-333">如果您想要同時執行這兩個 Alwayson 叢集，您會需要 hello 接聽程式 toochange hello DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-333">You need toochange hello DNS name of hello listener if you want both Always On clusters running simultaneously.</span></span> <span data-ttu-id="5bc7b-334">這會將系統管理額外負荷 hello 移轉期間為用戶端應用程式的字串必須反映 hello 新的接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-334">This adds administration overhead during hello migration as client application strings must reflect hello new Listener name.</span></span>
* <span data-ttu-id="5bc7b-335">您必須實作 hello 以關閉 以可能 toominimize hello 最終同步處理需求，在移轉前兩個環境 tookeep 之間同步處理機制。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-335">You must implement a synchronization mechanism between hello two environments tookeep them as close as possible toominimize hello final synchronization requirements before migration.</span></span>
* <span data-ttu-id="5bc7b-336">那里加入成本移轉期間可以執行的 hello 新環境時。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-336">There is added cost during migration while you have hello new environment running.</span></span>

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a><span data-ttu-id="5bc7b-337">利用最少的停機時間移轉 Always On 部署</span><span class="sxs-lookup"><span data-stu-id="5bc7b-337">Migrating Always On Deployments for minimal downtime</span></span>
<span data-ttu-id="5bc7b-338">有兩種策略可利用最少的停機時間來移轉 Always On 部署：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-338">There are two strategies for migrating Always On deployments for minimal downtime:</span></span>

1. <span data-ttu-id="5bc7b-339">**利用現有的次要項目：單一站台**</span><span class="sxs-lookup"><span data-stu-id="5bc7b-339">**Utilize an Existing Secondary: Single-Site**</span></span>
2. <span data-ttu-id="5bc7b-340">**利用現有的次要項目：多站台**</span><span class="sxs-lookup"><span data-stu-id="5bc7b-340">**Utilize Existing Secondary Replica(s): Multi-Site**</span></span>

#### <a name="1-utilize-an-existing-secondary-single-site"></a><span data-ttu-id="5bc7b-341">1.利用現有的次要項目：單一站台</span><span class="sxs-lookup"><span data-stu-id="5bc7b-341">1. Utilize an existing secondary: Single-Site</span></span>
<span data-ttu-id="5bc7b-342">最少停機時間的其中一個策略是 tootake 現有的次要雲端，並移除 hello 目前的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-342">One strategy for minimal downtime is tootake an existing cloud secondary and remove it from hello current cloud service.</span></span> <span data-ttu-id="5bc7b-343">然後將複製 hello Vhd toohello 新 Premium 儲存體帳戶，並建立 hello VM hello 新的雲端服務中。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-343">Then copy hello VHDs toohello new Premium Storage account, and create hello VM in hello new cloud service.</span></span> <span data-ttu-id="5bc7b-344">然後，更新叢集和容錯移轉中的 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-344">Then update hello listener in clustering and failover.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="5bc7b-345">停機時間點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-345">Points of downtime</span></span>
* <span data-ttu-id="5bc7b-346">當您更新 hello 最終節點與 hello 負載平衡的端點時，沒有停機時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-346">There is downtime when you update hello final node with hello Load Balanced endpoint.</span></span>
* <span data-ttu-id="5bc7b-347">根據您的用戶端/DNS 設定而定，用戶端連線可能會延遲。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-347">Your client reconnection might be delayed depending on your client/DNS configuration.</span></span>
* <span data-ttu-id="5bc7b-348">如果您選擇 tootake hello 一律在叢集群組離線 tooswap 出 hello IP 位址，沒有額外的停機時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-348">There is additional downtime if you choose tootake hello Always On Cluster group offline tooswap out hello IP addresses.</span></span> <span data-ttu-id="5bc7b-349">您可以避免這個狀況使用 OR 相依性和可能的擁有者 hello 加入 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-349">You can avoid this by using an OR dependency and Possible Owners for hello added IP Address resource.</span></span> <span data-ttu-id="5bc7b-350">請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-350">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>

> [!NOTE]
> <span data-ttu-id="5bc7b-351">當您想 hello 做為永遠在容錯移轉夥伴的加入的節點 toopartake 中時，您會需要 tooadd 與負載平衡設定參考 toohello Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-351">When you want hello added node toopartake in as an Always On Failover Partner, you need tooadd an Azure Endpoint with a reference toohello Load Balanced Set.</span></span> <span data-ttu-id="5bc7b-352">當您執行 hello **Add-azureendpoint**命令 toodo 開啟時，此，目前連接 tooremain，但新的連線 toohello 接聽程式將不會建立已更新 hello 負載平衡器，直到可以 toobe。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-352">When you run hello **Add-AzureEndpoint** command toodo this, current connections tooremain open, but new connections toohello listener will not be able toobe established until hello load balancer has updated.</span></span> <span data-ttu-id="5bc7b-353">在測試中，這是所見的 toolast 90 120seconds，這應該進行測試。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-353">In testing this was seen toolast 90-120seconds, this should be tested.</span></span>
>
>

##### <a name="advantages"></a><span data-ttu-id="5bc7b-354">優點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-354">Advantages</span></span>
* <span data-ttu-id="5bc7b-355">移轉期間不會產生額外的成本。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-355">No extra cost incurred during migration.</span></span>
* <span data-ttu-id="5bc7b-356">一對一移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-356">A one-to-one migration.</span></span>
* <span data-ttu-id="5bc7b-357">降低複雜度。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-357">Reduced complexity.</span></span>
* <span data-ttu-id="5bc7b-358">允許從進階儲存體 SKU 增加 IOPS。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-358">Allows for increased IOPS from Premium Storage SKUs.</span></span> <span data-ttu-id="5bc7b-359">當磁碟會中斷 hello VM 的連線，並複製 toohello 新雲端服務的 hello 3rd 方工具都可以使用的 tooincrease hello VHD 大小，可提供更高的輸送量。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-359">When hello disks are detached from hello VM and copied toohello new cloud service, a 3rd party tool can be used tooincrease hello VHD size, which provides higher throughputs.</span></span> <span data-ttu-id="5bc7b-360">若要增加 VHD 大小，請參閱這個 [論壇討論](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-360">For increasing VHD sizes, see this [forum discussion](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="5bc7b-361">缺點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-361">Disadvantages</span></span>
* <span data-ttu-id="5bc7b-362">移轉期間會暫時遺失 HA 和 DR。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-362">There is a temporary loss of HA and DR during migration.</span></span>
* <span data-ttu-id="5bc7b-363">因為這是 1:1 移轉，您必須 toouse 最小的 VM 大小將支援您的號碼的 Vhd，因此您不可能會無法 toodownsize Vm。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-363">As this is a 1:1 migration, you will have toouse a minimum VM size that will support your number of VHDs, so you might not be able toodownsize your VMs.</span></span>
* <span data-ttu-id="5bc7b-364">這種情況下會使用 hello Azure**開始 AzureStorageBlobCopy**指令程式，也就是非同步。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-364">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="5bc7b-365">複製完成時沒有 SLA。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-365">There is no SLA on copy completion.</span></span> <span data-ttu-id="5bc7b-366">hello 的 hello 複本的時間會變動，而這取決於它也將取決於資料 tootransfer 的 hello 數量的佇列中等候。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-366">hello time of hello copies varies, while this depends on wait in queue it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="5bc7b-367">如果傳送嗨即將 tooanother 另一個地區內支援進階儲存體的 Azure 資料中心，會增加 hello 複製時間。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-367">hello copy time increases if hello transfer is going tooanother Azure data center that supports Premium Storage in another region.</span></span> <span data-ttu-id="5bc7b-368">如果您只需要 2 個節點，請考慮可行的因應以防 hello 複製所花的時間比在測試中。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-368">If you just have 2 nodes, consider a possible mitigation in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="5bc7b-369">這可能包括下列構想 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-369">This could include hello following ideas.</span></span>
  * <span data-ttu-id="5bc7b-370">加入以同意的停機時間的 hello 移轉前 HA 臨時第 3 個 SQL Server 節點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-370">Add a temporary 3rd SQL Server node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="5bc7b-371">執行 Azure 排程的維護期間以外的 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-371">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="5bc7b-372">確保您已正確設定叢集仲裁。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-372">Ensure you have configured your cluster quorum correctly.</span></span>  

##### <a name="high-level-steps"></a><span data-ttu-id="5bc7b-373">高階步驟</span><span class="sxs-lookup"><span data-stu-id="5bc7b-373">High-level steps</span></span>
<span data-ttu-id="5bc7b-374">這份文件不會示範完整的結束 tooend 範例中，不過 hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)這提供可以運用 tooperform 的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-374">This document does not demonstrate a complete end tooend example, however hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) provides details that can be leveraged tooperform this.</span></span>

![MinimalDowntime][8]

* <span data-ttu-id="5bc7b-376">蒐集的磁碟組態，而移除 hello 節點 （不要刪除附加的 Vhd）。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-376">Gather disk configuration, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="5bc7b-377">建立進階儲存體帳戶並將 Vhd 複製 hello 標準儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bc7b-377">Create a Premium Storage account and copy VHDs from hello Standard Storage account</span></span>
* <span data-ttu-id="5bc7b-378">建立新的雲端服務，然後重新部署該雲端服務中的 hello SQL2 VM。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-378">Create new cloud service and redeploy hello SQL2 VM in that cloud service.</span></span> <span data-ttu-id="5bc7b-379">建立 hello VM 使用 hello 複製原始的作業系統 VHD 和附加 hello 複製 Vhd。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-379">Create hello VM using hello copied original OS VHD and attaching hello copied VHDs.</span></span>
* <span data-ttu-id="5bc7b-380">設定 ILB / ELB 並新增端點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-380">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="5bc7b-381">使用下列任一種方法來更新接聽程式：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-381">Update Listener by either:</span></span>
  * <span data-ttu-id="5bc7b-382">取得 hello Alwayson 群組離線和更新 hello 一定在接聽程式與新的 ILB / ELB IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-382">Taking hello Always On Group offline and updating hello Always On Listener with new ILB / ELB IP address.</span></span>
  * <span data-ttu-id="5bc7b-383">或加入 hello IP 位址資源至 Windows 叢集的新雲端服務 ILB/ELB 透過 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-383">Or adding hello IP address resource of new Cloud Service ILB/ELB through PowerShell into Windows clustering.</span></span> <span data-ttu-id="5bc7b-384">然後組 hello 的可能擁有者 hello IP 位址資源 toohello 移轉 SQL2 節點，並將此設為 hello 網路名稱中的 OR 相依性。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-384">Then set hello Possible owners of hello IP Address resource toohello migrated node, SQL2, and set this as OR dependency in hello Network Name.</span></span> <span data-ttu-id="5bc7b-385">請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-385">See hello ‘Adding IP Address Resource on Same Subnet’ section of hello [Appendix](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).</span></span>
* <span data-ttu-id="5bc7b-386">請檢查 DNS 設定/propogation toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-386">Check DNS configuration/propogation toohello clients.</span></span>
* <span data-ttu-id="5bc7b-387">移轉 SQL1 VM，然後執行步驟 2 - 4。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-387">Migrate SQL1 VM, and go through steps 2 – 4.</span></span>
* <span data-ttu-id="5bc7b-388">如果使用步驟 5ii，然後將 SQL1 加入 hello 的可能擁有者加入 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="5bc7b-388">If using steps 5ii, then add SQL1 as a Possible Owner for hello added IP Address Resource</span></span>
* <span data-ttu-id="5bc7b-389">測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-389">Test failovers.</span></span>

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a><span data-ttu-id="5bc7b-390">2.利用現有的次要項目：多站台</span><span class="sxs-lookup"><span data-stu-id="5bc7b-390">2. Utilize existing secondary replica(s): Multi-Site</span></span>
<span data-ttu-id="5bc7b-391">如果您有多個 Azure 資料中心 (DC) 中的節點，或如果您有混合式環境，您可以使用這個環境 toominimize 停機時間中的 Alwayson 組態。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-391">If you have nodes in more than one Azure datacenter (DC) or if you have a hybrid environment, then you can use an Always On configuration in this environment toominimize downtime.</span></span>

<span data-ttu-id="5bc7b-392">hello 方法是透過 toothat SQL Server 的 toochange hello Alwayson 同步 tooSynchronous hello 內部部署或次要的 Azure DC，然後容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-392">hello approach is toochange hello Always On synchronization tooSynchronous for hello on-premises or secondary Azure DC, and then failover over toothat SQL Server.</span></span> <span data-ttu-id="5bc7b-393">然後將複製 hello Vhd tooa Premium 儲存體帳戶，並重新部署到新的雲端服務的 hello 機器。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-393">Then copy hello VHDs tooa Premium Storage account, and redeploy hello machine into a new cloud service.</span></span> <span data-ttu-id="5bc7b-394">更新 hello 接聽程式，並再進行容錯回復。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-394">Update hello listener, and then fail back.</span></span>

##### <a name="points-of-downtime"></a><span data-ttu-id="5bc7b-395">停機時間點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-395">Points of downtime</span></span>
<span data-ttu-id="5bc7b-396">hello 停機時間是由 hello 時間 toofailover toohello 替代 DC 與上一步所組成。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-396">hello downtime consists of hello time toofailover toohello alternative DC and back.</span></span> <span data-ttu-id="5bc7b-397">它也會取決於您的用戶端/DNS 設定，而您的用戶端重新連線可能會延遲。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-397">It also depends on your client/DNS configuration and your client reconnection may be delayed.</span></span>
<span data-ttu-id="5bc7b-398">請考慮下列範例的混合式 Alwayson 設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-398">Consider hello following example of a hybrid Always On configuration:</span></span>

![MultiSite1][9]

##### <a name="advantages"></a><span data-ttu-id="5bc7b-400">優點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-400">Advantages</span></span>
* <span data-ttu-id="5bc7b-401">您可以利用現有的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-401">You can utilize existing infrastructure.</span></span>
* <span data-ttu-id="5bc7b-402">第一次在 hello DR Azure DC 上有 hello 選項 toopre 升級 hello Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-402">You have hello option toopre-upgrade hello Azure storage on hello DR Azure DC first.</span></span>
* <span data-ttu-id="5bc7b-403">hello DC DR Azure 儲存體可以重新設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-403">hello DR Azure DC storage can be reconfigured.</span></span>
* <span data-ttu-id="5bc7b-404">移轉期間至少有兩個容錯移轉，但不包括測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-404">There is a minimum of two failovers during migration, excluding test failovers.</span></span>
* <span data-ttu-id="5bc7b-405">請勿需要 toomove SQL Server 資料與備份和還原。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-405">You do not need toomove SQL Server data with backup and restore.</span></span>

##### <a name="disadvantages"></a><span data-ttu-id="5bc7b-406">缺點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-406">Disadvantages</span></span>
* <span data-ttu-id="5bc7b-407">根據用戶端存取 tooSQL 伺服器，可能會有延遲增加的 SQL Server 正在執行替代的 DC toohello 應用程式中時。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-407">Depending on client access tooSQL Server, there might be increased latency when SQL Server is running in an alternative DC toohello application.</span></span>
* <span data-ttu-id="5bc7b-408">hello 的 Vhd tooPremium 儲存體的複製時間可能較長。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-408">hello copy time of VHDs tooPremium storage could be long.</span></span> <span data-ttu-id="5bc7b-409">這可能會影響您決定是否 tookeep hello hello 可用性群組中的節點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-409">This might affect your decision on whether tookeep hello node in hello Availability Group.</span></span> <span data-ttu-id="5bc7b-410">請考慮針對此記錄大量工作負載 hello 移轉期間執行時是必要的因為 hello 主要節點將會有 tookeep hello 其交易記錄檔中有未複寫的交易。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-410">Consider this for when log intensive work loads are running during hello migration is required, since hello Primary node will have tookeep hello unreplicated transactions in its transaction log.</span></span> <span data-ttu-id="5bc7b-411">因此，這可能會顯著成長。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-411">Therefore this could grow significantly.</span></span>
* <span data-ttu-id="5bc7b-412">這種情況下會使用 hello Azure**開始 AzureStorageBlobCopy**指令程式，也就是非同步。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-412">This scenario would use hello Azure **Start-AzureStorageBlobCopy** commandlet, which is asynchronous.</span></span> <span data-ttu-id="5bc7b-413">完成時沒有 SLA。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-413">There is no SLA on completion.</span></span> <span data-ttu-id="5bc7b-414">hello hello 複本的時間會有所差異，而這取決於等候佇列中，它也將取決於資料 tootransfer 的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-414">hello time of hello copies varies, while this depends on wait in queue, it will also depend on hello amount of data tootransfer.</span></span> <span data-ttu-id="5bc7b-415">因此您只需要一個節點在第 2 個資料中心，以防 hello 複製所花的時間比在測試中，您應該採取因應步驟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-415">Therefore you just have one node in your 2nd data center, you should take mitigation steps in case hello copy takes longer than in testing.</span></span> <span data-ttu-id="5bc7b-416">這可能包括下列構想 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-416">This could include hello following ideas.</span></span>
  * <span data-ttu-id="5bc7b-417">暫存第 2 個 SQL 將節點加入供 HA hello 移轉以同意的停機時間之前。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-417">Add a temporary 2nd SQL node for HA before hello migration with agreed downtime.</span></span>
  * <span data-ttu-id="5bc7b-418">執行 Azure 排程的維護期間以外的 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-418">Run hello migration outside of Azure scheduled maintenance.</span></span>
  * <span data-ttu-id="5bc7b-419">確保您已正確設定叢集仲裁。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-419">Ensure you have configured your cluster quorum correctly.</span></span>

<span data-ttu-id="5bc7b-420">此案例假設您有記載您的安裝，並且知道 hello 儲存體中磁碟快取設定的順序 toomake 變更對應的方式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-420">This scenario assumes that you have documented your install and know how hello storage is mapped in order toomake changes for optimal disk cache settings.</span></span>

##### <a name="high-level-steps"></a><span data-ttu-id="5bc7b-421">高階步驟</span><span class="sxs-lookup"><span data-stu-id="5bc7b-421">High-level steps</span></span>
![Multisite2][10]

* <span data-ttu-id="5bc7b-423">請 hello 內部 / 替代 SQL Server 主要 Azure DC hello，並將其 hello 其他自動容錯移轉夥伴 (AFP)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-423">Make hello on-premises / alternate Azure DC hello SQL Server Primary, and make it hello other Auto Failover Partner (AFP).</span></span>
* <span data-ttu-id="5bc7b-424">收集從 SQL2 和移除 hello 節點 （不要刪除附加的 Vhd） 的磁碟組態資訊。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-424">Gather disk configuration information from SQL2, and remove hello node (do not delete attached VHDs).</span></span>
* <span data-ttu-id="5bc7b-425">建立進階儲存體帳戶，並將 Vhd 複製 hello 標準儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-425">Create a Premium Storage account and copy VHDs from hello Standard Storage account.</span></span>
* <span data-ttu-id="5bc7b-426">建立新的雲端服務以及建立 hello SQL2 VM 包含附加其 Premiums 存放磁碟。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-426">Create a new cloud service and create hello SQL2 VM with its Premiums Storage disks attached.</span></span>
* <span data-ttu-id="5bc7b-427">設定 ILB / ELB 並新增端點。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-427">Configure ILB / ELB and add Endpoints.</span></span>
* <span data-ttu-id="5bc7b-428">更新 hello 一定在接聽程式與新的 ILB / ELB IP 位址和測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-428">Update hello Always On Listener with new ILB / ELB IP address and test failover.</span></span>
* <span data-ttu-id="5bc7b-429">檢查 hello DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-429">Check hello DNS configuration.</span></span>
* <span data-ttu-id="5bc7b-430">變更 hello AFP tooSQL2 然後移轉 SQL1 並完成步驟 2 – 5。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-430">Change hello AFP tooSQL2, and then migrate SQL1 and go through steps 2 – 5.</span></span>
* <span data-ttu-id="5bc7b-431">測試容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-431">Test failovers.</span></span>
* <span data-ttu-id="5bc7b-432">切換 hello AFP 後 tooSQL1 及 SQL2</span><span class="sxs-lookup"><span data-stu-id="5bc7b-432">Switch hello AFP back tooSQL1 and SQL2</span></span>

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a><span data-ttu-id="5bc7b-433">附錄： 移轉多站台一律在叢集 tooPremium 儲存體</span><span class="sxs-lookup"><span data-stu-id="5bc7b-433">Appendix: Migrating a Multisite Always On Cluster tooPremium Storage</span></span>
<span data-ttu-id="5bc7b-434">hello 本主題其餘部分提供轉換的多站台 Alwayson 叢集 tooPremium 儲存體的詳細的範例。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-434">hello remainder of this topic provides a detailed example of converting a multi-site Always On cluster tooPremium storage.</span></span> <span data-ttu-id="5bc7b-435">它也會從使用外部負載平衡器 (ELB) tooan 內部負載平衡 (ILB) 轉換 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-435">It also converts hello Listener from using an external load balancer (ELB) tooan internal load balancer (ILB).</span></span>

### <a name="environment"></a><span data-ttu-id="5bc7b-436">Environment</span><span class="sxs-lookup"><span data-stu-id="5bc7b-436">Environment</span></span>
* <span data-ttu-id="5bc7b-437">Windows 2k12 / SQL 2k12</span><span class="sxs-lookup"><span data-stu-id="5bc7b-437">Windows 2k12 / SQL 2k12</span></span>
* <span data-ttu-id="5bc7b-438">SP 上 1 個 DB 檔案</span><span class="sxs-lookup"><span data-stu-id="5bc7b-438">1 DB Files on SP</span></span>
* <span data-ttu-id="5bc7b-439">每個節點 2 x 個儲存集區</span><span class="sxs-lookup"><span data-stu-id="5bc7b-439">2 x Storage Pools per Node</span></span>

![Appendix1][11]

### <a name="vm"></a><span data-ttu-id="5bc7b-441">VM：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-441">VM:</span></span>
<span data-ttu-id="5bc7b-442">在此範例中我們 toodemonstrate 從 ELB tooILB 移動。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-442">In this example we are going toodemonstrate moving from an ELB tooILB.</span></span> <span data-ttu-id="5bc7b-443">ELB，無法再 ILB，因此這會顯示如何在 tooswitch toothis hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-443">ELB was available before ILB, so this shows how tooswitch toothis during hello migration.</span></span>

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a><span data-ttu-id="5bc7b-445">前置步驟： 連接 tooSubscription</span><span class="sxs-lookup"><span data-stu-id="5bc7b-445">Pre Steps: Connect tooSubscription</span></span>
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a><span data-ttu-id="5bc7b-446">步驟 1：建立新的儲存體帳戶和雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bc7b-446">Step 1: Create New Storage Account and Cloud Service</span></span>
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a><span data-ttu-id="5bc7b-447">在資源上允許失敗的步驟 2： 增加 hello<Optional></span><span class="sxs-lookup"><span data-stu-id="5bc7b-447">Step 2: Increase hello permitted failures on resources <Optional></span></span>
<span data-ttu-id="5bc7b-448">屬於 tooyour Alwayson 可用性群組的特定資源上有所限制，可能會發生在一段時間，其中 hello 叢集服務將嘗試 toorestart hello 資源群組中有多少失敗次數。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-448">On certain resources that belong tooyour Always On Availability Group there are limits on how many failures that can occur in a period, where hello cluster service will attempt toorestart hello resource group.</span></span> <span data-ttu-id="5bc7b-449">建議您增加這儘管您會帶您逐步完成此程序，因為如果您不要手動容錯移轉和觸發程序藉由您關閉機器的容錯移轉可以取得關閉 toothis 限制。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-449">It is recommended you increase this whilst you are walking through this procedure, since if you don’t manually failover and trigger failovers by shutting down machines you can get close toothis limit.</span></span>

<span data-ttu-id="5bc7b-450">它會是審慎的作法 toodouble hello 失敗額度，toodo 這在 [容錯移轉叢集管理員] 中，移 toohello hello Alwayson 資源群組屬性：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-450">It would be prudent toodouble hello failure allowance, toodo this in Failover Cluster Manager, go toohello Properties of hello Always On resource group:</span></span>

![Appendix3][13]

<span data-ttu-id="5bc7b-452">變更最大失敗 too6 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-452">Change hello Maximum Failures too6.</span></span>

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a><span data-ttu-id="5bc7b-453">步驟 3：新增叢集群組的 IP 位址資源 <Optional></span><span class="sxs-lookup"><span data-stu-id="5bc7b-453">Step 3: Addition IP Address resource for Cluster Group <Optional></span></span>
<span data-ttu-id="5bc7b-454">如果您擁有 hello 叢集群組只能有一個 IP 位址，而且這是對齊的 toohello 雲端子網路，請注意，如果您不小心讓離線 hello 雲端中的所有叢集節點，網路則 hello 叢集 IP 資源和叢集網路名稱將不會無法 toocome線上。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-454">If you have only one IP address for hello Cluster Group and this is aligned toohello cloud subnet, beware, if you accidentally take offline all cluster nodes in hello cloud on that network then hello Cluster IP resource and Cluster Network Name will not be able toocome online.</span></span> <span data-ttu-id="5bc7b-455">在 hello 事件將會使這個更新 tooother 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-455">In hello event of this it will prevent updates tooother cluster resources.</span></span>

#### <a name="step-4-dns-configuration"></a><span data-ttu-id="5bc7b-456">步驟 4：DNS 設定</span><span class="sxs-lookup"><span data-stu-id="5bc7b-456">Step 4: DNS configuration</span></span>
<span data-ttu-id="5bc7b-457">tooimplement 平順地轉換取決於 DNS 的正在利用和更新。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-457">tooimplement a smooth transition depends on how DNS is being utilized and updated.</span></span>
<span data-ttu-id="5bc7b-458">安裝 Alwayson 時，它會建立 Windows 叢集資源群組，如果您開啟 容錯移轉叢集管理員，您會看到至少會有三個資源，hello hello 文件的兩指的是 tooare:</span><span class="sxs-lookup"><span data-stu-id="5bc7b-458">When Always On is installed, it creates a Windows Cluster Resource group, if you open Failover Cluster Manager, you will see that at a minimum it will have three resources, hello two that hello document refers tooare:</span></span>

* <span data-ttu-id="5bc7b-459">這是虛擬網路名稱 (VNN) – hello DNS 命名該用戶端連接 toowhen 想 tooconnect tooSQL 透過 Alwayson 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-459">Virtual Network Name (VNN) – This is hello DNS name that client connect toowhen wanting tooconnect tooSQL Servers via Always On.</span></span>
* <span data-ttu-id="5bc7b-460">IP 位址資源 – 這是 IP 位址相關聯 hello VNN hello，您可以有一個以上，和在多站台設定您可以每個站台/子網路的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-460">IP Address Resource – This is hello IP address that associated with hello VNN, you can have more than one, and in a multisite configuration you will have an IP address per site/subnet.</span></span>

<span data-ttu-id="5bc7b-461">當連接 tooSQL 伺服器 hello SQL Server 用戶端驅動程式會擷取 hello 與 hello 接聽程式相關聯的 DNS 記錄，並再試一次 tooconnect tooeach Always On 相關聯的 IP 位址時下, 面我們討論的某些因素會影響這。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-461">When connecting tooSQL Server, hello SQL Server Client driver will retrieve hello DNS records associated with hello listener and try tooconnect tooeach Always On associated IP address, below we discuss some factors that can influence this.</span></span>

<span data-ttu-id="5bc7b-462">hello 並行 hello 接聽程式名稱與相關聯的 DNS 記錄的數目取決於不僅 hello 的 IP 位址相關聯，但如果 hello ' RegisterAllIpProviders'setting hello 一律 ON VNN 資源的容錯移轉叢集中。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-462">hello number of concurrent DNS records that are associated with hello listener name depends not only on hello number of IP addresses associated, but hello ‘RegisterAllIpProviders’setting in Failover Clustering for hello Always ON VNN resource.</span></span>

<span data-ttu-id="5bc7b-463">當您部署 Alwayson 在 Azure 中有不同的步驟 toocreate hello 接聽程式和 IP 位址、 設定 hello 'RegisterAllIpProviders' too1 toomanually，這是它已設定 too1 其中不同 tooan 內部 Alwayson 部署。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-463">When you deploy Always On in Azure there are different steps toocreate hello Listener and IP Addresses, you have toomanually configure hello ‘RegisterAllIpProviders’ too1, this is different tooan on-premises Always On deployment where it is already set too1.</span></span>

<span data-ttu-id="5bc7b-464">如果 'RegisterAllIpProviders' 是 0，則只會看到與 hello 接聽程式的 DNS 中的 DNS 記錄相關聯：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-464">If ‘RegisterAllIpProviders’ is 0, then you will only see one DNS record in DNS associated with hello Listener:</span></span>

![Appendix4][14]

<span data-ttu-id="5bc7b-466">如果 ‘RegisterAllIpProviders’ 是 1：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-466">If ‘RegisterAllIpProviders’ is 1:</span></span>

![Appendix5][15]

<span data-ttu-id="5bc7b-468">hello 的下列程式碼會傾印出 hello VNN 設定，並將它設定為您，請附註，hello 變更 tootake 效果，您將需要 tootake hello VNN 離線和線上重新的開啟，這個函式 hello 接聽程式離線導致用戶端連線中斷。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-468">hello code below will dump out hello VNN settings and set it for you, please note, for hello change tootake effect you will need tootake hello VNN offline and turn it back online, this taking hello Listener offline causing client connectivity disruption.</span></span>

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

<span data-ttu-id="5bc7b-469">在更新版本的移轉步驟中，您將需要 tooupdate hello Alwayson 接聽程式將會參考負載平衡器的更新 IP 位址，這會牽涉到的 IP 位址資源移除和新增。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-469">In a later migration step you will need tooupdate hello Always On listener with an updated IP address that will reference a load balancer, this will involve an IP Address resource removal and addition.</span></span> <span data-ttu-id="5bc7b-470">Hello IP 更新之後，您需要 tooensure hello 新 IP 位址已更新 DNS 區域中，並且在 hello 用戶端要更新其本機 DNS 快取。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-470">After hello IP update, you need tooensure hello new IP address has been updated in DNS Zone and that hello clients are updating their local DNS cache.</span></span>

<span data-ttu-id="5bc7b-471">如果您的用戶端位於不同的網路區段，並參考不同的 DNS 伺服器，您需要的 tooconsider 會發生什麼事需 DNS 區域傳送 hello 移轉期間，當 hello 應用程式重新連接時間，將會限制由至少 hello 區域傳輸時間hello 接聽程式的任何新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-471">If your clients reside in a different network segment and reference a different DNS server, you need tooconsider what happens about DNS Zone Transfer during hello migration, as hello application reconnect time will be constrained by at least hello Zone Transfer Time of any new IP addresses for hello listener.</span></span> <span data-ttu-id="5bc7b-472">如果您是時間條件約束下，您應該討論及測試強制與您的 Windows 團隊增量區域轉送和也放入 hello DNS 主機記錄 tooa 降低時間 tooLive (TTL)，所以 hello 用戶端更新。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-472">If you are under time constraint here, you should discuss and test forcing an incremental zone transfer with your Windows teams, and also put hello DNS host record tooa lower Time tooLive (TTL), so hello clients update.</span></span> <span data-ttu-id="5bc7b-473">如需詳細資訊，請參閱[增量區域傳輸](https://technet.microsoft.com/library/cc958973.aspx)和 [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-473">For more information, see [Incremental Zone Transfers](https://technet.microsoft.com/library/cc958973.aspx) and [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).</span></span>

<span data-ttu-id="5bc7b-474">預設 hello 與 hello Alwayson 在 Azure 中的接聽程式相關聯的 DNS 記錄的 TTL 為 1200 秒。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-474">By default hello TTL for DNS Record that is associated with hello Listener in Always On in Azure is 1200 seconds.</span></span> <span data-ttu-id="5bc7b-475">您可能希望 tooreduce 這如果您是時間條件約束下，在您移轉 tooensure hello 用戶端的更新其 DNS hello 更新 ip 位址的 hello 接聽程式。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-475">You may wish tooreduce this if you are under time constraint during your migration tooensure hello clients update their DNS with hello updated IP address for hello listener.</span></span> <span data-ttu-id="5bc7b-476">您可以查看，並修改 hello 組態的傾印出 hello VNN hello 設定：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-476">You can see and modify hello configuration by dumping out hello configuration of hello VNN:</span></span>

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

<span data-ttu-id="5bc7b-477">請注意，hello 低 hello 'HostRecordTTL'，到更高比例的 DNS 流量就會發生。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-477">Please note, hello lower hello ‘HostRecordTTL’, a higher amount of DNS traffic will occur.</span></span>

##### <a name="client-application-settings"></a><span data-ttu-id="5bc7b-478">用戶端應用程式設定</span><span class="sxs-lookup"><span data-stu-id="5bc7b-478">Client application settings</span></span>
<span data-ttu-id="5bc7b-479">如果您的 SQL 用戶端應用程式支援 hello.Net 4.5 SQLClient，則您可以使用 ' MULTISUBNETFAILOVER = TRUE' 關鍵字，這建議 toobe 以它可讓您更快速連線 tooSQL Alwayson 可用性群組容錯移轉期間套用。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-479">If your SQL client application supports hello .Net 4.5 SQLClient, then you can use ‘MULTISUBNETFAILOVER=TRUE’ keyword, this is recommended toobe applied as it allows for faster connection tooSQL Always On Availability Group during failover.</span></span> <span data-ttu-id="5bc7b-480">它會列舉 hello Alwayson 接聽程式以平行方式，與相關聯的所有 IP 位址，並在容錯移轉期間執行更積極的 TCP 連線重試速度。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-480">It enumerates through all IP addresses associated with hello Always On listener in parallel, and performs a more aggressive TCP connection retry speed during a failover.</span></span>

<span data-ttu-id="5bc7b-481">如需有關上述 hello 設定的詳細資訊，請參閱[MultiSubnetFailover 關鍵字和相關聯的功能](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-481">For more information regarding hello settings above, please see [MultiSubnetFailover Keyword and Associated Features](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover).</span></span> <span data-ttu-id="5bc7b-482">另請參閱[適用於高可用性與災害復原的 SqlClient 支援](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-482">Also see [SqlClient Support for High Availability, Disaster Recovery](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).</span></span>

#### <a name="step-5-cluster-quorum-settings"></a><span data-ttu-id="5bc7b-483">步驟 5：叢集仲裁設定</span><span class="sxs-lookup"><span data-stu-id="5bc7b-483">Step 5: Cluster quorum settings</span></span>
<span data-ttu-id="5bc7b-484">當您將 toobe 出下至少一個 SQL Server 進行一次，您應該修改 hello 叢集仲裁設定，如果檔案共用見證 (FSW) 使用 2 個節點時，您應該設定 hello 仲裁 tooallow 節點多數並利用動態投票，而且這是針對 tooallow單一節點 tooremain 時，接手。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-484">As you are going toobe taking out at least one SQL Server down at a time, you should modify hello cluster quorum setting, if using File Share Witness (FSW) with 2 nodes, you should set hello quorum tooallow node majority and utilize dynamic voting, and this is tooallow for a single node tooremain standing.</span></span>

    Set-ClusterQuorum -NodeMajority  

<span data-ttu-id="5bc7b-485">如需有關管理以及設定 hello 叢集仲裁的詳細資訊，請參閱[設定和管理 hello Windows Server 2012 容錯移轉叢集中的仲裁](https://technet.microsoft.com/library/jj612870.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-485">For more information on managing and configuring hello cluster quorum, please see [Configure and Manage hello Quorum in a Windows Server 2012 Failover Cluster](https://technet.microsoft.com/library/jj612870.aspx).</span></span>

#### <a name="step-6-extract-existing-endpoints-and-acls"></a><span data-ttu-id="5bc7b-486">步驟 6：擷取現有的端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="5bc7b-486">Step 6: Extract Existing Endpoints and ACLs</span></span>
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

<span data-ttu-id="5bc7b-487">儲存這些 tooa 文字檔案。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-487">Save these tooa text file.</span></span>

#### <a name="step-7-change-failover-partners-and-replication-modes"></a><span data-ttu-id="5bc7b-488">步驟 7：變更容錯移轉夥伴和複寫模式</span><span class="sxs-lookup"><span data-stu-id="5bc7b-488">Step 7: Change Failover Partners and Replication Modes</span></span>
<span data-ttu-id="5bc7b-489">如果您有 2 個以上的 SQL Server，您應該變更 hello 的另一個 dc 的另一個次要複本的容錯移轉，或在內部部署 too'Synchronous' 然後讓它自動容錯移轉夥伴 (AFP)，這是讓您維護高可用性，儘管您要進行變更。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-489">If you have more than 2 SQL Servers, you should change hello failover of another secondary in another DC or on-premises too‘Synchronous’ and make it an Automatic Failover Partner (AFP), this is so you maintain HA whilst you are making changes.</span></span> <span data-ttu-id="5bc7b-490">您可以透過 TSQL 執行這個動作，或透過 SSMS 來修改：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-490">You can do this through TSQL of modify though SSMS:</span></span>

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a><span data-ttu-id="5bc7b-492">步驟 8：從雲端服務移除次要的 VM</span><span class="sxs-lookup"><span data-stu-id="5bc7b-492">Step 8: Remove Secondary VM from cloud service</span></span>
<span data-ttu-id="5bc7b-493">您應該規劃 toomigrate 雲端的第二個節點第一次，如果這是目前的主要項目，您應該起始手動容錯移轉。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-493">You should be planning toomigrate a cloud secondary node first, if this is currently primary, you should initiate a manual failover.</span></span>

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="5bc7b-494">步驟 9：在 CSV 檔案中變更磁碟快取設定，然後儲存</span><span class="sxs-lookup"><span data-stu-id="5bc7b-494">Step 9: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="5bc7b-495">資料磁碟區，這些應該設定 tooREADONLY。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-495">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="5bc7b-496">TLOG 磁碟區，這些應該設定 tooNONE。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-496">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a><span data-ttu-id="5bc7b-498">步驟 10：複製 VHDS</span><span class="sxs-lookup"><span data-stu-id="5bc7b-498">Step 10: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



<span data-ttu-id="5bc7b-499">您可以檢查 hello hello Vhd toohello 高階儲存體帳戶複製狀態：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-499">You can check hello copy status of hello VHDs toohello Premium Storage account:</span></span>

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

<span data-ttu-id="5bc7b-501">繼續等待，直到這所有設定都記錄為成功為止。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-501">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="5bc7b-502">適用於個別 Blob 的資訊：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-502">For information for individual blobs:</span></span>

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a><span data-ttu-id="5bc7b-503">步驟 11：註冊作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="5bc7b-503">Step 11: Register OS disk</span></span>
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a><span data-ttu-id="5bc7b-504">步驟 12：將次要項目匯入新的雲端服務</span><span class="sxs-lookup"><span data-stu-id="5bc7b-504">Step 12: Import secondary into new cloud service</span></span>
<span data-ttu-id="5bc7b-505">也會使用 hello，加入下列程式碼會 hello 選項這裡您可以匯入 hello 機器，並使用 hello retainable VIP。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-505">hello code below also uses hello added option here you can import hello machine and use hello retainable VIP.</span></span>

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="5bc7b-506">步驟 13：在新的雲端服務上建立 ILB，新增負載平衡的端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="5bc7b-506">Step 13: Create ILB on New Cloud Svc, Add Load Balanced Endpoints and ACLs</span></span>
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a><span data-ttu-id="5bc7b-507">步驟 14：更新 Always On</span><span class="sxs-lookup"><span data-stu-id="5bc7b-507">Step 14: Update Always On</span></span>
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

<span data-ttu-id="5bc7b-509">現在要移除 hello 舊的雲端服務 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-509">Now remove hello old cloud service IP Address.</span></span>

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a><span data-ttu-id="5bc7b-511">步驟 15：DNS 更新檢查</span><span class="sxs-lookup"><span data-stu-id="5bc7b-511">Step 15: DNS update check</span></span>
<span data-ttu-id="5bc7b-512">您現在應該檢查 SQL Server 用戶端網路的 DNS 伺服器，並確定叢集已加入 hello hello 額外的主機記錄新增 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-512">You should now check DNS Servers on your SQL Server client networks and make sure that clustering has added hello extra host record for hello added IP address.</span></span> <span data-ttu-id="5bc7b-513">如果這些 DNS 伺服器未更新，請考慮進行強制的 DNS 區域轉送，請確認 hello 中有子網路的用戶端可以 tooresolve tooboth 一律在 IP 位址，這是讓您不需要的自動 DNS 複寫 toowait。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-513">If those DNS servers have not updated, consider forcing a DNS Zone transfer and ensure that hello clients in there subnet are able tooresolve tooboth Always On IP Addresses, this is so you do not need toowait for automatic DNS replication.</span></span>

#### <a name="step-16-reconfigure-always-on"></a><span data-ttu-id="5bc7b-514">步驟 16：重新設定 Always On</span><span class="sxs-lookup"><span data-stu-id="5bc7b-514">Step 16: Reconfigure Always On</span></span>
<span data-ttu-id="5bc7b-515">此時您等候已移轉的 toofully 該節點重新同步處理與 hello 內部節點和切換 toosynchronous 複寫節點，以 hello AFP 次要 hello。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-515">At this point you wait for hello secondary that node that was migrated toofully resynchronize with hello on-premises node and switch toosynchronous replication node and make it hello AFP.</span></span>  

#### <a name="step-17-migrate-second-node"></a><span data-ttu-id="5bc7b-516">步驟 17：移轉第二個節點</span><span class="sxs-lookup"><span data-stu-id="5bc7b-516">Step 17: Migrate second node</span></span>
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a><span data-ttu-id="5bc7b-517">步驟 18：在 CSV 檔案中變更磁碟快取設定，然後儲存</span><span class="sxs-lookup"><span data-stu-id="5bc7b-517">Step 18: Change disk caching settings in CSV file and save</span></span>
<span data-ttu-id="5bc7b-518">資料磁碟區，這些應該設定 tooREADONLY。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-518">For data volumes these should be set tooREADONLY.</span></span>

<span data-ttu-id="5bc7b-519">TLOG 磁碟區，這些應該設定 tooNONE。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-519">For TLOG volumes these should be set tooNONE.</span></span>

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a><span data-ttu-id="5bc7b-521">步驟 19：為次要節點建立新的獨立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="5bc7b-521">Step 19: Create New Independent Storage Account for Secondary Node</span></span>
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a><span data-ttu-id="5bc7b-522">步驟 20：複製 VHDS</span><span class="sxs-lookup"><span data-stu-id="5bc7b-522">Step 20: Copy VHDS</span></span>
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


<span data-ttu-id="5bc7b-523">您可以檢查 hello VHD 複製狀態的所有 Vhd: ForEach (在 $diskobjects $disk) {$lun = $disk。Lun $vhdname = $disk.vhdname $cacheoption = $disk。HostCaching $disklabel = $disk。DiskLabel $diskName = $disk。DiskName</span><span class="sxs-lookup"><span data-stu-id="5bc7b-523">You can check hello VHD copy status for all VHDs: ForEach ($disk in $diskobjects) { $lun = $disk.Lun $vhdname = $disk.vhdname $cacheoption = $disk.HostCaching $disklabel = $disk.DiskLabel $diskName = $disk.DiskName</span></span>

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

<span data-ttu-id="5bc7b-525">繼續等待，直到這所有設定都記錄為成功為止。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-525">Wait until all these are recorded as success.</span></span>

<span data-ttu-id="5bc7b-526">適用於個別 Blob 的資訊：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-526">For information for individual blobs:</span></span>

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a><span data-ttu-id="5bc7b-527">步驟 21：註冊作業系統磁碟</span><span class="sxs-lookup"><span data-stu-id="5bc7b-527">Step 21: Register OS disk</span></span>
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a><span data-ttu-id="5bc7b-528">步驟 22：新增負載平衡端點和 ACL</span><span class="sxs-lookup"><span data-stu-id="5bc7b-528">Step 22: Add Load Balanced Endpoints and ACLs</span></span>
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a><span data-ttu-id="5bc7b-529">步驟 23：測試容錯移轉</span><span class="sxs-lookup"><span data-stu-id="5bc7b-529">Step 23: Test failover</span></span>
<span data-ttu-id="5bc7b-530">您現在應該可以讓 hello 移轉的節點與 hello 內部 Alwayson 節點同步處理、 將它放在 toosynchronous 複寫模式中，等候同步處理。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-530">You should now let hello migrated node synchronize with hello on-premises Always On node, place it in toosynchronous replication mode and wait until it is synchronized.</span></span> <span data-ttu-id="5bc7b-531">然後從內部 toohello 第一個節點容錯移轉，移轉即 hello AFP。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-531">Then failover from on-prem toohello first node migrated, which is hello AFP.</span></span> <span data-ttu-id="5bc7b-532">之後，完成之後，變更 hello 上一次移轉節點 toohello AFP。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-532">Once that has worked, change hello last migrated node toohello AFP.</span></span>

<span data-ttu-id="5bc7b-533">您應該測試所有節點之間容錯移轉，並執行中執行但 tooensure 容錯移轉運作會像是 chaos 測試預計會及時 manor。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-533">You should test failovers between all nodes and run though chaos tests tooensure failovers work as expected and in a timely manor.</span></span>

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a><span data-ttu-id="5bc7b-534">步驟 24：回復叢集仲裁設定 / DNS TTL / 容錯移轉夥伴 / 同步設定</span><span class="sxs-lookup"><span data-stu-id="5bc7b-534">Step 24: Put back cluster quorum settings / DNS TTL / Failover Pntrs / Sync Settings</span></span>
##### <a name="adding-ip-address-resource-on-same-subnet"></a><span data-ttu-id="5bc7b-535">在同一個子網路上新增 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="5bc7b-535">Adding IP Address Resource on Same Subnet</span></span>
<span data-ttu-id="5bc7b-536">如果您有只有 2 的 SQL 伺服器，而且想 toomigrate 它們 tooa 新雲端服務，但想 tookeep 上進行 hello 相同子網路，則可以避免採用 hello 接聽程式永遠離線 toodelete hello 原始 IP 位址新增 hello 新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-536">If you have only 2 SQL Servers and want toomigrate them tooa new cloud service, but want tookeep them on hello same subnet, you can avoid taking hello listener offline toodelete hello original Always On IP Address and add hello New IP Address.</span></span> <span data-ttu-id="5bc7b-537">如果您要移轉您不需要 toodo 這將會參照子網路的其他叢集網路的 hello Vm tooanother 子網路。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-537">If you are migrating hello VMs tooanother subnet you will not need toodo this as there will be an additional cluster network that will reference that subnet.</span></span>

<span data-ttu-id="5bc7b-538">一旦您擁有帶出 hello 移轉次要資料庫，並加入新雲端服務 hello hello 新 IP 位址資源之前容錯移轉 hello 現有主要，您應該採取 hello 容錯移轉叢集管理員 內的這些步驟：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-538">Once you have brought up hello migrated secondary and added in hello new IP Address resource for hello new cloud service before failover hello existing Primary, you should take these steps within hello Cluster Failover Manager:</span></span>

<span data-ttu-id="5bc7b-539">tooadd 的 IP 位址，請參閱 hello[附錄](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage)，步驟 14。</span><span class="sxs-lookup"><span data-stu-id="5bc7b-539">tooadd in IP Address, see hello [Appendix](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), step 14.</span></span>

1. <span data-ttu-id="5bc7b-540">Hello 目前的 IP 位址資源，來變更 hello 可能擁有者 too'Existing 主要 SQL Server'，在下面 'dansqlams4' hello 範例：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-540">For hello current IP Address resource, change hello possible owner too‘Existing Primary SQL Server’, in hello example below, ‘dansqlams4’:</span></span>

    ![Appendix13][23]
2. <span data-ttu-id="5bc7b-542">新的 IP 位址資源 hello，變更 hello 可能擁有者 too'Migrated 次要 SQL Server'，在下面 'dansqlams5' hello 範例：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-542">For hello new IP Address resource, change hello possible owner too‘Migrated secondary SQL Server’, in hello example below, ‘dansqlams5’:</span></span>

    ![Appendix14][24]
3. <span data-ttu-id="5bc7b-544">這個設定之後，您可以容錯移轉，並讓該節點會加入做為可能的擁有者時，移轉 hello 最後一個節點時編輯 hello 可能的擁有者：</span><span class="sxs-lookup"><span data-stu-id="5bc7b-544">Once this is set you can failover, and when hello last node is migrated hello Possible Owners should be edited so that node is added as a Possible Owner:</span></span>

    ![Appendix15][25]

## <a name="additional-resources"></a><span data-ttu-id="5bc7b-546">其他資源</span><span class="sxs-lookup"><span data-stu-id="5bc7b-546">Additional resources</span></span>
* [<span data-ttu-id="5bc7b-547">Azure 進階儲存體</span><span class="sxs-lookup"><span data-stu-id="5bc7b-547">Azure Premium Storage</span></span>](../../../storage/common/storage-premium-storage.md)
* [<span data-ttu-id="5bc7b-548">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5bc7b-548">Virtual Machines</span></span>](https://azure.microsoft.com/services/virtual-machines/)
* [<span data-ttu-id="5bc7b-549">Azure 虛擬機器中的 SQL Server</span><span class="sxs-lookup"><span data-stu-id="5bc7b-549">SQL Server in Azure Virtual Machines</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
