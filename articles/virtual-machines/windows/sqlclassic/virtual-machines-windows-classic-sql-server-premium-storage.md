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
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>在虛擬機器上搭配使用 Azure 進階儲存體和 SQL Server
## <a name="overview"></a>概觀
[Azure 高階儲存體](../../../storage/common/storage-premium-storage.md)是 hello 的存放裝置，可提供低延遲、 高輸送量 IO 的下一個層代。 它最適合用於需要大量 IO 的重要工作負載，例如，IaaS [虛擬機器](https://azure.microsoft.com/services/virtual-machines/)上的 SQL Server。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

本文章提供了規劃及移轉執行 SQL Server toouse 高階儲存體的虛擬機器的指引。 這包括 Azure 基礎結構 (網路功能、儲存體) 和客體 Windows VM 步驟。 在 hello hello 範例[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)示範如何改進 toomove 較大 Vm tootake 利用完整的完整結束 tooend 移轉本機 SSD 儲存裝置使用 PowerShell。

它是重要的 toounderstand hello 端對端程序與 IAAS Vm 上的 SQL Server 利用 Azure 高階儲存體。 其中包括：

* Hello 必要條件 toouse 高階儲存體的識別。
* 針對新部署的 IaaS tooPremium 儲存體上部署 SQL Server 的範例。
* 移轉現有部署的範例，其中包括使用 SQL Always On 可用性群組的獨立伺服器和部署。
* 可能的移轉方法。
* 完整端對端範例，示範 hello 移轉現有的 Alwayson 實作 Azure、 Windows 和 SQL Server 的步驟。

如需更多關於 Azure 虛擬機器中 SQL Server 的背景資訊，請參閱 [Azure 虛擬機器中的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。

**作者：**Daniel Sol **技術審稿人員：**Luis Carlos Vargas Herring、Sanjay Mishra、Pravin Mital、Juergen Thomas、Gonzalo Ruiz。

## <a name="prerequisites-for-premium-storage"></a>適用於進階儲存體的必要條件
使用進階儲存體之前，必須具備數個必要條件。

### <a name="machine-size"></a>機器大小
使用進階儲存體，您必須 toouse DS 系列虛擬機器 (VM)。 如果您不在雲端服務，才能使用 DS 系列機器，則必須刪除現有 VM 的 hello、 保持 hello 附加磁碟，並再建立新的雲端服務，再重新建立 hello 與 DS * 角色大小的 VM。 如需虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器和雲端服務大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="cloud-services"></a>雲端服務
如果 DS* VM 和進階儲存體是建立在新的雲端服務中，則您只能搭配使用它們。 如果您在 Azure 中使用 SQL Server Alwayson，hello 一定在接聽程式會參考與雲端服務相關聯的 toohello Azure 內部或外部負載平衡器 IP 位址。 本文著重在如何 toomigrate 維持在這個案例中的可用性。

> [!NOTE]
> DS * 數列必須 hello 第一個 VM 是已部署的 toohello 新的雲端服務。
>
>

### <a name="regional-vnets"></a>區域 VNET
DS * vm，您必須設定虛擬網路 (VNET) 裝載您的 Vm toobe 地區 hello。 這個 「 放大 」 hello VNET tooallow hello 較大 Vm toobe 其他叢集中佈建並允許兩者之間的通訊。 在下列螢幕擷取畫面的 hello，hello 反白顯示的位置會顯示區域 Vnet，而 hello 第一個結果會顯示"narrow"VNET。

![RegionalVNET][1]

您可以提高 Microsoft 支援票證 toomigrate tooa 區域 VNET，Microsoft 將會進行變更，然後 toocomplete hello 移轉 tooregional Vnet，變更 hello 屬性 AffinityGroup hello 網路組態中的。 先匯出 hello 在 PowerShell 中，網路組態，並取代 hello **AffinityGroup**屬性在 hello **VirtualNetworkSite**具有項目**位置**屬性。 指定 `Location = XXXX`，其中 `XXXX` 為 Azure 區域。 然後匯入 hello 新組態。

例如，考慮下列 VNET 組態的 hello:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove 此 tooa 區域 VNET 中西歐，變更下列 hello 組態 toohello:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>儲存體帳戶
您將需要 toocreate Premium 儲存體設定的新儲存體帳戶。 請注意 hello 使用 Premium 儲存體設定在 hello 儲存體帳戶，不能在個別的 Vhd，但使用 DS * 系列 VM 時您可以將 VHD 附加來自 Premium 和標準儲存體帳戶。 如果您不想 tooplace hello OS VHD toohello 高階儲存體帳戶上的，您可以考慮此。

hello 下列**新增 AzureStorageAccountPowerShell**命令與 hello"Premium_LRS"**類型**建立進階儲存體帳戶：

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>VHD 快取設定
hello 之間建立磁碟屬於高階儲存體帳戶的主要差異在於 hello 磁碟快取設定。 針對 SQL Server 資料磁碟區磁碟，建議使用 [讀取快取]。 交易記錄磁碟區，hello 磁碟快取應該設定太 '**無**'。 這點不同於標準儲存體帳戶的 hello 建議。

在附加 hello Vhd 之後，就無法改變 hello 快取設定。 您會需要 toodetach，再重新 hello VHD 附加更新之快取設定。

### <a name="windows-storage-spaces"></a>Windows 儲存空間
您可以使用[Windows 儲存空間](https://technet.microsoft.com/library/hh831739.aspx)一樣與先前標準儲存體，這可讓您 toomigrate 已經利用儲存空間的 VM。 中的 hello 範例[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)（步驟 9 和轉送） 示範 hello Powershell 程式碼 tooextract 並匯入具有多個附加 Vhd 的 VM。

存放集區已使用標準的 Azure 儲存體帳戶 tooenhance 輸送量，並降低延遲。 您可能會在針對新部署測試含有進階儲存體的儲存集區時尋找值，但它們會為儲存體設定增加額外的複雜度。

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>如何 toofind 哪些 Azure 的虛擬磁碟對應 toostorage 集區
附加 vhd 建議不同的快取設定時，您可能決定 toocopy hello Vhd tooa 高階儲存體帳戶。 不過，當您重新附加 toohello 新 DS 系列 VM，您可能需要 tooalter hello 快取設定。 它是簡單 tooapply hello 高階儲存體建議的快取設定，當您有不同的 Vhd 的 hello SQL 資料檔案和記錄檔 （而非同時包含單一 VHD）。

> [!NOTE]
> 如果您擁有的 hello 相同的磁碟區，hello 快取您選擇的選項取決於針對資料庫工作負載的 hello IO 存取模式上的 SQL Server 資料和記錄檔。 只有測試可以示範哪一個快取選項最適合這個案例。
>
>

然而，如果您使用 Windows 儲存空間，其中的多個 Vhd，您必須在 toolook 組成您原始的指令碼 tooidentify 附加 Vhd 是在哪個特定集區，因此您可以再設定 hello 快取設定據以每個磁碟。

如果您不需要原始指令碼可用 tooshow 您 Vhd 對應 toohello 儲存集區，您可以使用下列步驟 toodetermine hello 磁碟/儲存體集區對應的 hello。

每個磁碟，使用下列步驟的 hello:

1. 取得清單的磁碟附加以 hello tooVM **Get-azurevm**命令：

    Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. 請注意 hello Diskname 和 LUN。

    ![DisknameAndLUN][2]
3. 遠端桌面連接到 hello VM 的資訊。 然後跳過**電腦管理** | **裝置管理員** | **磁碟機**。 查看每一個 hello ' Microsoft 虛擬磁碟的' hello 屬性

    ![VirtualDiskProperties][3]
4. hello LUN 編號是您指定當附加 hello VHD toohello VM 參考 toohello LUN 編號。
5. Hello 'Microsoft 虛擬磁碟' go toohello**詳細資料** 索引標籤，然後在 hello**屬性**清單中，跳過**驅動程式機碼**。 在 hello**值**，注意 hello**位移**，也就是在下列螢幕擷取畫面的 hello 0002。 hello 0002 代表 hello PhysicalDisk2 的 hello 存放集區的參考。

    ![VirtualDiskPropertyDetails][4]
6. 對於每個儲存集區，傾印出 hello 相關聯的磁碟：

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

現在您可以使用此資訊 tooassociate 附加 Vhd tooPhysical 磁碟儲存集區中。

一旦您已對應儲存集區，您可以卸離並複製 tooa 高階儲存體帳戶中的 Vhd tooPhysical 磁碟，然後將其連接與 hello 正確快取設定。 在 hello hello 範例，請參閱[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)，步驟 8 到 12。 這些步驟顯示 tooextract VM 連接的 VHD 磁碟組態 tooa CSV 檔案中，如何複製 hello Vhd、 改變 hello 磁碟快取設定，以及最後重新 hello VM 部署為以所有 hello DS 系列 VM 附加磁碟。

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>VM 儲存體頻寬和 VHD 儲存體輸送量
儲存體效能的 hello 數量 hello DS * VM 大小指定與 hello VHD 大小而定。 hello Vm 有不同的額度 hello 可附加和 hello 它們將支援 (MB/s) 的最大頻寬的 Vhd 數目。 Hello 特定頻寬號碼，請參閱[虛擬機器和 Azure 的雲端服務大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

提高 IOPS 可透過更大的磁碟大小來達成。 當您考量移轉路徑時，應將這點納入考慮。 如需詳細資訊， [IOPS 和磁碟類型，請參閱 hello 表格](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets)。

最後，請考量 VM 對於所有連結磁碟支援的磁碟頻寬上限各有不同。 負載過高，您無法 saturate hello 適用於該 VM 角色大小的最大磁碟頻寬。 例如 Standard_DS14 會支援註冊 too512MB/s;因此，您無法使用三個 P30 磁碟 saturate hello 磁碟頻寬的 hello VM。 但在此範例中，hello 輸送量限制可能會超過根據 hello 混合的讀取和寫入 IOs。

## <a name="new-deployments"></a>新的部署
hello 下兩節將示範如何部署 SQL Server Vm tooPremium 儲存體。 如前所述，您不一定需要 tooplace hello OS 磁碟至進階儲存體。 您可以選擇 toodo 這如果在 hello OS VHD 想 tooplace 任何需要大量 IO 工作負載。

hello 第一個範例會示範利用現有的 Azure 資源庫映像。 hello 第二個範例會示範如何 toouse 自訂 VM 映像，您在現有的標準儲存體帳戶。

> [!NOTE]
> 這些範例假設您已經建立區域 VNET。
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>使用資源庫映像建立含有進階儲存體的新 VM
下列的 hello 範例示範如何 tooplace hello OS VHD 至進階儲存體，並附加 Premium 儲存體的 Vhd。 不過，也將 hello OS 磁碟放在標準儲存體帳戶，然後再附加在高階儲存體帳戶中的 Vhd。 以下將示範這兩個案例。

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>步驟 1：建立進階儲存體帳戶
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>步驟 2：建立新的雲端服務
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>步驟 3：保留雲端服務 VIP (選用)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>步驟 4：建立 VM 容器
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>步驟 5：在標準或進階儲存體上放置作業系統 VHD
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>步驟 6：建立 VM
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


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>使用自訂映像建立新的 VM toouse 高階儲存體
這個案例示範您現有的自訂映像是位於標準儲存體帳戶中。 如所述，如果您要 tooplace hello OS VHD 高階儲存體，您將需要 toocopy hello hello 標準儲存體帳戶中存在的映像，並將它們傳送 tooa 高階儲存體，才能使用。 如果您有映像內部部署，您可以也使用此方法 toocopy 直接 toohello 高階儲存體帳戶。

#### <a name="step-1-create-storage-account"></a>步驟 1：建立儲存體帳戶
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>步驟 2：建立雲端服務
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>步驟 3：使用現有的映像
您可以使用現有的映像。 或者，您可以 [取得現有機器的映像](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。 請注意 hello 機器映像沒有 toobe DS * 機器。 一旦您擁有 hello 映像時，下列步驟顯示如何 hello toocopy 它 toohello 高階儲存體帳戶以 hello**開始 AzureStorageBlobCopy** PowerShell 指令程式。

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>步驟 4：在儲存帳戶間複製 Blob
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>步驟 5：定期檢查複製狀態：
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>步驟 6： 加入訂用帳戶中的映像磁碟 tooAzure 磁碟儲存機制
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> 您可能會發現即使 hello 狀態報告為成功，您可能仍然收到磁碟租用錯誤。 在此情況下，請等待大約 10 分鐘的時間。
>
>

#### <a name="step-7--build-hello-vm"></a>步驟 7： 建置 hello VM
這裡您要建立 hello VM 從您的映像和附加兩個 Premium 儲存體的 Vhd:

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

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>未使用 Always On 可用性群組的現有部署
> [!NOTE]
> 現有的部署中，第一次看到 hello[必要條件](#prerequisites-for-premium-storage)本主題一節。
>
>

對於未使用「Always On 可用性群組」的 SQL Server 部署與使用該可用性群組的部署，有不同的考量。 如果您不使用 Always On，且有現有的獨立 SQL Server，您可以使用新的雲端服務和儲存體帳戶來升級 tooPremium 儲存體。 請考慮下列選項的 hello:

* **建立新的 SQL Server VM**。 您可以建立新的 SQL Server VM 來使用進階儲存體帳戶，如＜新的部署＞中所述。 然後備份並還原 SQL Server 設定和使用者資料庫。 hello 的應用程式需要更新 toobe tooreference hello 新的 SQL Server，如果它正在存取內部或外部。 如果當您執行並存 (SxS) SQL Server 移轉您將需要指定 toocopy 所有 '超出 db' 物件。 這包含像是登入、憑證及連結的伺服器等物件。
* **移轉現有的 SQL Server VM**。 這將需要離線 hello SQL Server VM，然後將它傳送 tooa 新雲端服務，其中包括將所有其附加 Vhd toohello 高階儲存體帳戶複製。 當 hello VM 都上線時，hello 應用程式會參考 hello 伺服器主機先前的名稱。 請注意，hello hello 現有磁碟大小會影響 hello 效能特性。 例如，400 GB 磁碟取得無條件進位 tooa P20。 如果您知道您無法重新建立 hello 為 DS 系列 VM 的 VM，並且附加您需要的 hello 大小/效能規格的 Premium 儲存體 Vhd，您不需要該磁碟效能。 您無法卸離，然後重新附加 hello SQL 資料庫檔案。

> [!NOTE]
> 當複製 hello VHD 磁碟，您應該留意 hello 大小而定的 hello 大小表示 Premium 儲存體磁碟類型可將其分為，這會決定磁碟效能規格。 Azure 會無條件向上 toohello 最接近的磁碟大小，因此如果您有 400 GB 的磁碟，這會無條件進位 tooa P20。 根據 hello OS VHD 您現有 IO 需求，您可能不需要 toomigrate 此 tooa 高階儲存體帳戶。
>
>

如果您的 SQL Server 存取外部，hello 雲端服務 VIP 會變更。 您也必須 tooupdate 結束點、 Acl 和 DNS 設定。

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>使用 Always On 可用性群組的現有部署
> [!NOTE]
> 現有的部署中，第一次看到 hello[必要條件](#prerequisites-for-premium-storage)本主題一節。
>
>

在本節一開始，我們將了解 Always On 如何與「Azure 網路」互動。 我們會細分 tootwo 案例中的移轉： 移轉可容許停機一段時間和您必須在此達到最短停機時間的移轉。

內部部署的 SQL Server Always On 可用性群組會使用內部部署的接聽程式，來註冊虛擬 DNS 名稱以及 IP 位址，其可在一或多部 SQL Server 之間共用。 用戶端連線時它們透過 hello 接聽程式 IP toohello 主要 SQL 伺服器進行路由傳送。 這是 hello 伺服器擁有在該時間 hello 一律在 IP 資源。

![DeploymentsUseAlways On][6]

在 Microsoft Azure 中您可以在 hello VM 上的一個 IP 位址指派 tooa NIC 因此在排序 tooachieve hello 相同為在內部部署的抽象層，Azure 利用 hello 分派 toohello 內部/外部負載平衡器 (ILB/ELB) 的 IP 位址。 hello 伺服器之間共用的 hello IP 資源設定 toohello hello ILB/ELB 為相同的 IP。 這會在 hello DNS 中發佈和用戶端流量通過 hello ILB/ELB toohello 主要 SQL Server 複本。 hello ILB/ELB 知道 SQL Server 是主要，因為它會使用探查 tooprobe hello 一律在 IP 資源。 Hello 前一個範例中，它探查每個節點都有參考 hello ELB/ILB 端點為準回應 hello 主要 SQL 伺服器。

> [!NOTE]
> hello ILB 和 ELB 同時指派 tooa 特定的 Azure 雲端服務中，因此在 Azure 中的任何雲端移轉最有可能表示該 hello 負載平衡器 IP 會變更。
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>移轉可允許一段停機時間的 Always On 部署
有兩種策略 toomigrate Always On 的部署，允許一些停機時間：

1. **加入現有一律在叢集的多個次要複本 tooan**
2. **移轉 tooa 新一律上的叢集**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1.新增多個次要複本 tooan 現有一律上的叢集
其中一種策略是 tooadd 多個次要資料庫 toohello Alwayson 可用性群組。 您需要 tooadd 這些新的雲端服務，然後更新 hello 新的負載平衡器 IP hello 接聽程式。

##### <a name="points-of-downtime"></a>停機時間點：
* 叢集驗證。
* 測試適用於新次要項目的 Always On 容錯移轉

如果您使用 Windows 儲存集區 hello VM 內 IO 輸送量，然後這些將會離線期間完整的叢集驗證。 當您新增節點 toohello 叢集需要 hello 驗證測試。 hello toorun hello 測試所花費的時間可能會不同，所以您應該測試這在您的代表測試環境 tooget 這所花多久的大約時間。

您應該佈建，您可以執行手動容錯移轉和 chaos 測試 hello 新加入的節點 tooensure Alwayson 高可用性函式，如預期般的時間。

![DeploymentUseAlways On2][7]

> [!NOTE]
> 您應該停止執行前，先 hello 驗證，其中使用 hello 存放集區的 SQL Server 的所有執行個體。
>
> ##### <a name="high-level-steps"></a>高階步驟
>

1. 在新的雲端服務中，使用連結的進階儲存體來建立兩部新的 SQL Server。
2. 複製完整備份，然後使用 **NORECOVERY**進行還原。
3. 複製「超出使用者 DB 範圍」的相依物件，例如登入等項目。
4. 建立新的內部負載平衡器 (ILB) 或使用外部負載平衡器 (ELB)，然後在這兩個新節點上設定負載平衡的端點。

   > [!NOTE]
   > 檢查所有節點都都 hello 正確的端點組態，然後再繼續
   >
   >
5. （如果使用儲存集區），請停止使用者/應用程式存取 toohello SQL Server。
6. 停止所有節點上的 SQL Server 引擎服務 (如果正在使用儲存集區)。
7. 加入新的節點 toocluster，及執行完整的驗證。
8. 驗證成功之後，啟動所有 SQL Server 服務。
9. 備份交易記錄，然後還原使用者資料庫。
10. 將新節點新增至 hello Alwayson 可用性群組，並將複寫分為**同步**。
11. 新增 hello IP 位址資源的 hello 新雲端服務 ILB/ELB 透過 PowerShell for Always On 根據 hello 多網站範例中 hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。 在 Windows 叢集中，設定 hello**可能的擁有者**的 hello **IP 位址**資源 toohello 新節點舊。 請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。
12. Hello 新節點的容錯移轉 tooone。
13. 請 hello 自動容錯移轉夥伴的新節點，然後測試容錯移轉。
14. 從可用性群組移除原始節點。

##### <a name="advantages"></a>優點
* 新的 SQL 伺服器可以是測試 （SQL Server 和應用程式），再新增 tooAlways 上。
* 您可以變更 hello VM 大小，並自訂 hello 儲存 tooyour 確切需求。 但是，它很有幫助 tookeep 所有都 hello SQL 檔案路徑都 hello 相同。
* 您可以控制 hello 傳送嗨 DB 備份 toohello 次要複本會開始時。 這不同於使用 Azure**開始 AzureStorageBlobCopy** commandlet toocopy Vhd，因為這是非同步複本。

##### <a name="disadvantages"></a>缺點
* 使用 Windows 儲存集區，有時叢集停機期間 hello 完整的叢集驗證 hello 新增加的節點。
* 根據 hello SQL Server 版本和次要複本的 hello 現有數目，您可能會無法 tooadd 但不會移除現有的次要資料庫的多個次要複本。
* 可能有長設定 hello 次要資料庫時，SQL 資料傳輸時間。
* 如果您以平行方式執行新機器，則在移轉期間會產生額外的成本。

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2.移轉 tooa 新一律上的叢集
另一個策略是新的雲端服務，然後重新導向 hello 用戶端 toouse toocreate 全新一律上包含節點的叢集全新它。

##### <a name="points-of-downtime"></a>停機時間點
當您傳送應用程式和使用者 toohello 新 Alwayson 接聽程式時，沒有停機時間。 hello 停機時間取決於：

* hello 時間 toorestore 最後一個交易記錄備份 toodatabases 新伺服器上。
* hello 所花費時間 tooupdate 用戶端應用程式 toouse 新 Alwayson 接聽程式。

##### <a name="advantages"></a>優點
* 您可以測試 hello 實際執行環境，SQL Server 和作業系統組建的變更。
* 您已擁有 hello 選項 toocustomize hello 儲存體和 toopotentially 減少 VM 大小。 這可能會降低成本。
* 您可以在此程序執行期間，更新 SQL Server 的組建或版本。 您也可以升級 hello 作業系統。
* hello 先前一律在叢集可以做為純色的復原目標。

##### <a name="disadvantages"></a>缺點
* 如果您想要同時執行這兩個 Alwayson 叢集，您會需要 hello 接聽程式 toochange hello DNS 名稱。 這會將系統管理額外負荷 hello 移轉期間為用戶端應用程式的字串必須反映 hello 新的接聽程式名稱。
* 您必須實作 hello 以關閉 以可能 toominimize hello 最終同步處理需求，在移轉前兩個環境 tookeep 之間同步處理機制。
* 那里加入成本移轉期間可以執行的 hello 新環境時。

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>利用最少的停機時間移轉 Always On 部署
有兩種策略可利用最少的停機時間來移轉 Always On 部署：

1. **利用現有的次要項目：單一站台**
2. **利用現有的次要項目：多站台**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1.利用現有的次要項目：單一站台
最少停機時間的其中一個策略是 tootake 現有的次要雲端，並移除 hello 目前的雲端服務。 然後將複製 hello Vhd toohello 新 Premium 儲存體帳戶，並建立 hello VM hello 新的雲端服務中。 然後，更新叢集和容錯移轉中的 hello 接聽程式。

##### <a name="points-of-downtime"></a>停機時間點
* 當您更新 hello 最終節點與 hello 負載平衡的端點時，沒有停機時間。
* 根據您的用戶端/DNS 設定而定，用戶端連線可能會延遲。
* 如果您選擇 tootake hello 一律在叢集群組離線 tooswap 出 hello IP 位址，沒有額外的停機時間。 您可以避免這個狀況使用 OR 相依性和可能的擁有者 hello 加入 IP 位址資源。 請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。

> [!NOTE]
> 當您想 hello 做為永遠在容錯移轉夥伴的加入的節點 toopartake 中時，您會需要 tooadd 與負載平衡設定參考 toohello Azure 端點。 當您執行 hello **Add-azureendpoint**命令 toodo 開啟時，此，目前連接 tooremain，但新的連線 toohello 接聽程式將不會建立已更新 hello 負載平衡器，直到可以 toobe。 在測試中，這是所見的 toolast 90 120seconds，這應該進行測試。
>
>

##### <a name="advantages"></a>優點
* 移轉期間不會產生額外的成本。
* 一對一移轉。
* 降低複雜度。
* 允許從進階儲存體 SKU 增加 IOPS。 當磁碟會中斷 hello VM 的連線，並複製 toohello 新雲端服務的 hello 3rd 方工具都可以使用的 tooincrease hello VHD 大小，可提供更高的輸送量。 若要增加 VHD 大小，請參閱這個 [論壇討論](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows)。

##### <a name="disadvantages"></a>缺點
* 移轉期間會暫時遺失 HA 和 DR。
* 因為這是 1:1 移轉，您必須 toouse 最小的 VM 大小將支援您的號碼的 Vhd，因此您不可能會無法 toodownsize Vm。
* 這種情況下會使用 hello Azure**開始 AzureStorageBlobCopy**指令程式，也就是非同步。 複製完成時沒有 SLA。 hello 的 hello 複本的時間會變動，而這取決於它也將取決於資料 tootransfer 的 hello 數量的佇列中等候。 如果傳送嗨即將 tooanother 另一個地區內支援進階儲存體的 Azure 資料中心，會增加 hello 複製時間。 如果您只需要 2 個節點，請考慮可行的因應以防 hello 複製所花的時間比在測試中。 這可能包括下列構想 hello。
  * 加入以同意的停機時間的 hello 移轉前 HA 臨時第 3 個 SQL Server 節點。
  * 執行 Azure 排程的維護期間以外的 hello 移轉。
  * 確保您已正確設定叢集仲裁。  

##### <a name="high-level-steps"></a>高階步驟
這份文件不會示範完整的結束 tooend 範例中，不過 hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)這提供可以運用 tooperform 的詳細資料。

![MinimalDowntime][8]

* 蒐集的磁碟組態，而移除 hello 節點 （不要刪除附加的 Vhd）。
* 建立進階儲存體帳戶並將 Vhd 複製 hello 標準儲存體帳戶
* 建立新的雲端服務，然後重新部署該雲端服務中的 hello SQL2 VM。 建立 hello VM 使用 hello 複製原始的作業系統 VHD 和附加 hello 複製 Vhd。
* 設定 ILB / ELB 並新增端點。
* 使用下列任一種方法來更新接聽程式：
  * 取得 hello Alwayson 群組離線和更新 hello 一定在接聽程式與新的 ILB / ELB IP 位址。
  * 或加入 hello IP 位址資源至 Windows 叢集的新雲端服務 ILB/ELB 透過 PowerShell。 然後組 hello 的可能擁有者 hello IP 位址資源 toohello 移轉 SQL2 節點，並將此設為 hello 網路名稱中的 OR 相依性。 請參見 hello '加入相同子網路上的 IP 位址資源' hello[附錄](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage)。
* 請檢查 DNS 設定/propogation toohello 用戶端。
* 移轉 SQL1 VM，然後執行步驟 2 - 4。
* 如果使用步驟 5ii，然後將 SQL1 加入 hello 的可能擁有者加入 IP 位址資源
* 測試容錯移轉。

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2.利用現有的次要項目：多站台
如果您有多個 Azure 資料中心 (DC) 中的節點，或如果您有混合式環境，您可以使用這個環境 toominimize 停機時間中的 Alwayson 組態。

hello 方法是透過 toothat SQL Server 的 toochange hello Alwayson 同步 tooSynchronous hello 內部部署或次要的 Azure DC，然後容錯移轉。 然後將複製 hello Vhd tooa Premium 儲存體帳戶，並重新部署到新的雲端服務的 hello 機器。 更新 hello 接聽程式，並再進行容錯回復。

##### <a name="points-of-downtime"></a>停機時間點
hello 停機時間是由 hello 時間 toofailover toohello 替代 DC 與上一步所組成。 它也會取決於您的用戶端/DNS 設定，而您的用戶端重新連線可能會延遲。
請考慮下列範例的混合式 Alwayson 設定的 hello:

![MultiSite1][9]

##### <a name="advantages"></a>優點
* 您可以利用現有的基礎結構。
* 第一次在 hello DR Azure DC 上有 hello 選項 toopre 升級 hello Azure 儲存體。
* hello DC DR Azure 儲存體可以重新設定。
* 移轉期間至少有兩個容錯移轉，但不包括測試容錯移轉。
* 請勿需要 toomove SQL Server 資料與備份和還原。

##### <a name="disadvantages"></a>缺點
* 根據用戶端存取 tooSQL 伺服器，可能會有延遲增加的 SQL Server 正在執行替代的 DC toohello 應用程式中時。
* hello 的 Vhd tooPremium 儲存體的複製時間可能較長。 這可能會影響您決定是否 tookeep hello hello 可用性群組中的節點。 請考慮針對此記錄大量工作負載 hello 移轉期間執行時是必要的因為 hello 主要節點將會有 tookeep hello 其交易記錄檔中有未複寫的交易。 因此，這可能會顯著成長。
* 這種情況下會使用 hello Azure**開始 AzureStorageBlobCopy**指令程式，也就是非同步。 完成時沒有 SLA。 hello hello 複本的時間會有所差異，而這取決於等候佇列中，它也將取決於資料 tootransfer 的 hello 數量。 因此您只需要一個節點在第 2 個資料中心，以防 hello 複製所花的時間比在測試中，您應該採取因應步驟。 這可能包括下列構想 hello。
  * 暫存第 2 個 SQL 將節點加入供 HA hello 移轉以同意的停機時間之前。
  * 執行 Azure 排程的維護期間以外的 hello 移轉。
  * 確保您已正確設定叢集仲裁。

此案例假設您有記載您的安裝，並且知道 hello 儲存體中磁碟快取設定的順序 toomake 變更對應的方式。

##### <a name="high-level-steps"></a>高階步驟
![Multisite2][10]

* 請 hello 內部 / 替代 SQL Server 主要 Azure DC hello，並將其 hello 其他自動容錯移轉夥伴 (AFP)。
* 收集從 SQL2 和移除 hello 節點 （不要刪除附加的 Vhd） 的磁碟組態資訊。
* 建立進階儲存體帳戶，並將 Vhd 複製 hello 標準儲存體帳戶。
* 建立新的雲端服務以及建立 hello SQL2 VM 包含附加其 Premiums 存放磁碟。
* 設定 ILB / ELB 並新增端點。
* 更新 hello 一定在接聽程式與新的 ILB / ELB IP 位址和測試容錯移轉。
* 檢查 hello DNS 設定。
* 變更 hello AFP tooSQL2 然後移轉 SQL1 並完成步驟 2 – 5。
* 測試容錯移轉。
* 切換 hello AFP 後 tooSQL1 及 SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>附錄： 移轉多站台一律在叢集 tooPremium 儲存體
hello 本主題其餘部分提供轉換的多站台 Alwayson 叢集 tooPremium 儲存體的詳細的範例。 它也會從使用外部負載平衡器 (ELB) tooan 內部負載平衡 (ILB) 轉換 hello 接聽程式。

### <a name="environment"></a>Environment
* Windows 2k12 / SQL 2k12
* SP 上 1 個 DB 檔案
* 每個節點 2 x 個儲存集區

![Appendix1][11]

### <a name="vm"></a>VM：
在此範例中我們 toodemonstrate 從 ELB tooILB 移動。 ELB，無法再 ILB，因此這會顯示如何在 tooswitch toothis hello 移轉。

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>前置步驟： 連接 tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>步驟 1：建立新的儲存體帳戶和雲端服務
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

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>在資源上允許失敗的步驟 2： 增加 hello<Optional>
屬於 tooyour Alwayson 可用性群組的特定資源上有所限制，可能會發生在一段時間，其中 hello 叢集服務將嘗試 toorestart hello 資源群組中有多少失敗次數。 建議您增加這儘管您會帶您逐步完成此程序，因為如果您不要手動容錯移轉和觸發程序藉由您關閉機器的容錯移轉可以取得關閉 toothis 限制。

它會是審慎的作法 toodouble hello 失敗額度，toodo 這在 [容錯移轉叢集管理員] 中，移 toohello hello Alwayson 資源群組屬性：

![Appendix3][13]

變更最大失敗 too6 hello。

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>步驟 3：新增叢集群組的 IP 位址資源 <Optional>
如果您擁有 hello 叢集群組只能有一個 IP 位址，而且這是對齊的 toohello 雲端子網路，請注意，如果您不小心讓離線 hello 雲端中的所有叢集節點，網路則 hello 叢集 IP 資源和叢集網路名稱將不會無法 toocome線上。 在 hello 事件將會使這個更新 tooother 叢集資源。

#### <a name="step-4-dns-configuration"></a>步驟 4：DNS 設定
tooimplement 平順地轉換取決於 DNS 的正在利用和更新。
安裝 Alwayson 時，它會建立 Windows 叢集資源群組，如果您開啟 容錯移轉叢集管理員，您會看到至少會有三個資源，hello hello 文件的兩指的是 tooare:

* 這是虛擬網路名稱 (VNN) – hello DNS 命名該用戶端連接 toowhen 想 tooconnect tooSQL 透過 Alwayson 的伺服器。
* IP 位址資源 – 這是 IP 位址相關聯 hello VNN hello，您可以有一個以上，和在多站台設定您可以每個站台/子網路的 IP 位址。

當連接 tooSQL 伺服器 hello SQL Server 用戶端驅動程式會擷取 hello 與 hello 接聽程式相關聯的 DNS 記錄，並再試一次 tooconnect tooeach Always On 相關聯的 IP 位址時下, 面我們討論的某些因素會影響這。

hello 並行 hello 接聽程式名稱與相關聯的 DNS 記錄的數目取決於不僅 hello 的 IP 位址相關聯，但如果 hello ' RegisterAllIpProviders'setting hello 一律 ON VNN 資源的容錯移轉叢集中。

當您部署 Alwayson 在 Azure 中有不同的步驟 toocreate hello 接聽程式和 IP 位址、 設定 hello 'RegisterAllIpProviders' too1 toomanually，這是它已設定 too1 其中不同 tooan 內部 Alwayson 部署。

如果 'RegisterAllIpProviders' 是 0，則只會看到與 hello 接聽程式的 DNS 中的 DNS 記錄相關聯：

![Appendix4][14]

如果 ‘RegisterAllIpProviders’ 是 1：

![Appendix5][15]

hello 的下列程式碼會傾印出 hello VNN 設定，並將它設定為您，請附註，hello 變更 tootake 效果，您將需要 tootake hello VNN 離線和線上重新的開啟，這個函式 hello 接聽程式離線導致用戶端連線中斷。

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

在更新版本的移轉步驟中，您將需要 tooupdate hello Alwayson 接聽程式將會參考負載平衡器的更新 IP 位址，這會牽涉到的 IP 位址資源移除和新增。 Hello IP 更新之後，您需要 tooensure hello 新 IP 位址已更新 DNS 區域中，並且在 hello 用戶端要更新其本機 DNS 快取。

如果您的用戶端位於不同的網路區段，並參考不同的 DNS 伺服器，您需要的 tooconsider 會發生什麼事需 DNS 區域傳送 hello 移轉期間，當 hello 應用程式重新連接時間，將會限制由至少 hello 區域傳輸時間hello 接聽程式的任何新的 IP 位址。 如果您是時間條件約束下，您應該討論及測試強制與您的 Windows 團隊增量區域轉送和也放入 hello DNS 主機記錄 tooa 降低時間 tooLive (TTL)，所以 hello 用戶端更新。 如需詳細資訊，請參閱[增量區域傳輸](https://technet.microsoft.com/library/cc958973.aspx)和 [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx)。

預設 hello 與 hello Alwayson 在 Azure 中的接聽程式相關聯的 DNS 記錄的 TTL 為 1200 秒。 您可能希望 tooreduce 這如果您是時間條件約束下，在您移轉 tooensure hello 用戶端的更新其 DNS hello 更新 ip 位址的 hello 接聽程式。 您可以查看，並修改 hello 組態的傾印出 hello VNN hello 設定：

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

請注意，hello 低 hello 'HostRecordTTL'，到更高比例的 DNS 流量就會發生。

##### <a name="client-application-settings"></a>用戶端應用程式設定
如果您的 SQL 用戶端應用程式支援 hello.Net 4.5 SQLClient，則您可以使用 ' MULTISUBNETFAILOVER = TRUE' 關鍵字，這建議 toobe 以它可讓您更快速連線 tooSQL Alwayson 可用性群組容錯移轉期間套用。 它會列舉 hello Alwayson 接聽程式以平行方式，與相關聯的所有 IP 位址，並在容錯移轉期間執行更積極的 TCP 連線重試速度。

如需有關上述 hello 設定的詳細資訊，請參閱[MultiSubnetFailover 關鍵字和相關聯的功能](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover)。 另請參閱[適用於高可用性與災害復原的 SqlClient 支援](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx)。

#### <a name="step-5-cluster-quorum-settings"></a>步驟 5：叢集仲裁設定
當您將 toobe 出下至少一個 SQL Server 進行一次，您應該修改 hello 叢集仲裁設定，如果檔案共用見證 (FSW) 使用 2 個節點時，您應該設定 hello 仲裁 tooallow 節點多數並利用動態投票，而且這是針對 tooallow單一節點 tooremain 時，接手。

    Set-ClusterQuorum -NodeMajority  

如需有關管理以及設定 hello 叢集仲裁的詳細資訊，請參閱[設定和管理 hello Windows Server 2012 容錯移轉叢集中的仲裁](https://technet.microsoft.com/library/jj612870.aspx)。

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>步驟 6：擷取現有的端點和 ACL
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

儲存這些 tooa 文字檔案。

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>步驟 7：變更容錯移轉夥伴和複寫模式
如果您有 2 個以上的 SQL Server，您應該變更 hello 的另一個 dc 的另一個次要複本的容錯移轉，或在內部部署 too'Synchronous' 然後讓它自動容錯移轉夥伴 (AFP)，這是讓您維護高可用性，儘管您要進行變更。 您可以透過 TSQL 執行這個動作，或透過 SSMS 來修改：

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>步驟 8：從雲端服務移除次要的 VM
您應該規劃 toomigrate 雲端的第二個節點第一次，如果這是目前的主要項目，您應該起始手動容錯移轉。

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

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>步驟 9：在 CSV 檔案中變更磁碟快取設定，然後儲存
資料磁碟區，這些應該設定 tooREADONLY。

TLOG 磁碟區，這些應該設定 tooNONE。

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>步驟 10：複製 VHDS
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



您可以檢查 hello hello Vhd toohello 高階儲存體帳戶複製狀態：

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

繼續等待，直到這所有設定都記錄為成功為止。

適用於個別 Blob 的資訊：

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>步驟 11：註冊作業系統磁碟
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

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>步驟 12：將次要項目匯入新的雲端服務
也會使用 hello，加入下列程式碼會 hello 選項這裡您可以匯入 hello 機器，並使用 hello retainable VIP。

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

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>步驟 13：在新的雲端服務上建立 ILB，新增負載平衡的端點和 ACL
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

#### <a name="step-14-update-always-on"></a>步驟 14：更新 Always On
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

現在要移除 hello 舊的雲端服務 IP 位址。

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>步驟 15：DNS 更新檢查
您現在應該檢查 SQL Server 用戶端網路的 DNS 伺服器，並確定叢集已加入 hello hello 額外的主機記錄新增 IP 位址。 如果這些 DNS 伺服器未更新，請考慮進行強制的 DNS 區域轉送，請確認 hello 中有子網路的用戶端可以 tooresolve tooboth 一律在 IP 位址，這是讓您不需要的自動 DNS 複寫 toowait。

#### <a name="step-16-reconfigure-always-on"></a>步驟 16：重新設定 Always On
此時您等候已移轉的 toofully 該節點重新同步處理與 hello 內部節點和切換 toosynchronous 複寫節點，以 hello AFP 次要 hello。  

#### <a name="step-17-migrate-second-node"></a>步驟 17：移轉第二個節點
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

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>步驟 18：在 CSV 檔案中變更磁碟快取設定，然後儲存
資料磁碟區，這些應該設定 tooREADONLY。

TLOG 磁碟區，這些應該設定 tooNONE。

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>步驟 19：為次要節點建立新的獨立儲存體帳戶
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

#### <a name="step-20-copy-vhds"></a>步驟 20：複製 VHDS
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


您可以檢查 hello VHD 複製狀態的所有 Vhd: ForEach (在 $diskobjects $disk) {$lun = $disk。Lun $vhdname = $disk.vhdname $cacheoption = $disk。HostCaching $disklabel = $disk。DiskLabel $diskName = $disk。DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

繼續等待，直到這所有設定都記錄為成功為止。

適用於個別 Blob 的資訊：

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>步驟 21：註冊作業系統磁碟
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

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>步驟 22：新增負載平衡端點和 ACL
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>步驟 23：測試容錯移轉
您現在應該可以讓 hello 移轉的節點與 hello 內部 Alwayson 節點同步處理、 將它放在 toosynchronous 複寫模式中，等候同步處理。 然後從內部 toohello 第一個節點容錯移轉，移轉即 hello AFP。 之後，完成之後，變更 hello 上一次移轉節點 toohello AFP。

您應該測試所有節點之間容錯移轉，並執行中執行但 tooensure 容錯移轉運作會像是 chaos 測試預計會及時 manor。

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>步驟 24：回復叢集仲裁設定 / DNS TTL / 容錯移轉夥伴 / 同步設定
##### <a name="adding-ip-address-resource-on-same-subnet"></a>在同一個子網路上新增 IP 位址資源
如果您有只有 2 的 SQL 伺服器，而且想 toomigrate 它們 tooa 新雲端服務，但想 tookeep 上進行 hello 相同子網路，則可以避免採用 hello 接聽程式永遠離線 toodelete hello 原始 IP 位址新增 hello 新的 IP 位址。 如果您要移轉您不需要 toodo 這將會參照子網路的其他叢集網路的 hello Vm tooanother 子網路。

一旦您擁有帶出 hello 移轉次要資料庫，並加入新雲端服務 hello hello 新 IP 位址資源之前容錯移轉 hello 現有主要，您應該採取 hello 容錯移轉叢集管理員 內的這些步驟：

tooadd 的 IP 位址，請參閱 hello[附錄](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage)，步驟 14。

1. Hello 目前的 IP 位址資源，來變更 hello 可能擁有者 too'Existing 主要 SQL Server'，在下面 'dansqlams4' hello 範例：

    ![Appendix13][23]
2. 新的 IP 位址資源 hello，變更 hello 可能擁有者 too'Migrated 次要 SQL Server'，在下面 'dansqlams5' hello 範例：

    ![Appendix14][24]
3. 這個設定之後，您可以容錯移轉，並讓該節點會加入做為可能的擁有者時，移轉 hello 最後一個節點時編輯 hello 可能的擁有者：

    ![Appendix15][25]

## <a name="additional-resources"></a>其他資源
* [Azure 進階儲存體](../../../storage/common/storage-premium-storage.md)
* [虛擬機器](https://azure.microsoft.com/services/virtual-machines/)
* [Azure 虛擬機器中的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

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
