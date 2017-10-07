---
title: "aaaMigrating Vm tooAzure 高階儲存體 |Microsoft 文件"
description: "移轉您現有的 Vm tooAzure 高階儲存體。 「進階儲存體」可針對在「Azure 虛擬機器」上執行且需要大量 I/O 的工作負載，提供高效能、低延遲的磁碟支援。"
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>移轉 tooAzure 高階儲存體 （Unmanaged 磁碟）

> [!NOTE]
> 本文將討論如何使用未受管理的標準磁碟 tooa VM 來使用的 VM，toomigrate unmanaged 高階磁碟。 我們建議您對於新的 Vm，使用 Azure 受管理的磁碟，並將轉換上一個 unmanaged 的磁碟 toomanaged 磁碟。 管理磁碟控制代碼 hello 基礎儲存體帳戶，因此您不需要。 如需詳細資訊，請參閱[受控磁碟概觀](../../virtual-machines/windows/managed-disks-overview.md)。
>

針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。 移轉您的應用程式的 VM 磁碟 tooAzure 高階儲存體，您可以利用 hello 速度的與這些磁碟的效能。

本指南用途 hello 是 toohelp 更好的 Azure 高階儲存體的新使用者準備 toomake 平順地轉換從其目前的系統 tooPremium 儲存體。 hello 指南來解決此程序中的 hello 主要元件中的三種：

* [規劃 hello 移轉 tooPremium 儲存體](#plan-the-migration-to-premium-storage)
* [準備和複製虛擬硬碟 (Vhd) tooPremium 儲存體](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [使用進階儲存體來建立 Azure 虛擬機器](#create-azure-virtual-machine-using-premium-storage)

您可以從其他平台 tooAzure 高階儲存體移轉 Vm，或從標準儲存體 tooPremium 存放裝置移轉現有的 Azure Vm。 本指南涵蓋這兩種案例的步驟。 請遵循 hello hello 相關區段，根據您的案例中指定的步驟。

> [!NOTE]
> 如需進階儲存體的功能概觀和價格，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)。 我們建議您移轉任何 hello 最佳效能，您的應用程式需要高 IOPS tooAzure 高階儲存體的虛擬機器磁碟。 如果您的磁碟不需要高 IOPS，您可以在「標準儲存體」中維護它來限制成本，這會將虛擬機器磁碟資料儲存在「硬碟機 (HDD)」上而非 SSD 上。
>

完成完整的 hello 移轉程序可能需要執行其他動作之前和之後提供本指南中的 hello 步驟。 範例包括設定虛擬網路或端點或 hello 應用程式本身可能需要在您的應用程式停機一段時間內的程式碼變更。 這些動作唯一 tooeach 應用程式，而且您應該提供此指南 toomake hello 完整的轉換 tooPremium 盡可能的緊密性儲存體中的 hello 步驟以及完成。

## <a name="plan-the-migration-to-premium-storage"></a>規劃 hello 移轉 tooPremium 儲存體
本節可確保您已準備好 toofollow hello 移轉步驟，在本文中，並協助您 toomake hello 最佳決定 VM 和磁碟類型。

### <a name="prerequisites"></a>必要條件
* 您將需要 Azure 訂用帳戶。 如果您沒有訂用帳戶，可以建立一個月的[免費試用](https://azure.microsoft.com/pricing/free-trial/)訂用帳戶，或造訪 [Azure 價格](https://azure.microsoft.com/pricing/)以了解其他選項。
* tooexecute PowerShell cmdlet，您將需要 hello Microsoft Azure PowerShell 模組。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 安裝點和安裝指示。
* 當您計劃 toouse 高階儲存體上執行的 Azure Vm 時，您會需要 toouse hello 高階儲存體功能的 Vm。 您可以將「標準」和「進階」儲存體磁碟與支援「進階儲存體」的 VM 搭配使用。 高階儲存體磁碟將會提供更多的 VM 類型，在未來的 hello。 如需所有可用 Azure VM 磁碟類型和大小的詳細資訊，請參閱[虛擬機器的大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)和[雲端服務的大小](../../cloud-services/cloud-services-sizes-specs.md)。

### <a name="considerations"></a>考量
Azure VM 支援附加數個進階儲存體磁碟，以便您的應用程式可以有向上 too256 TB 的每個 VM 的存放空間。 使用「進階儲存體」時，您應用程式的每一 VM 可達到 80,000 IOPS (每秒輸入/輸出作業)，而每一 VM 的每秒磁碟輸送量為 2000 MB，且讀取作業的延遲極低。 您有各種 VM 和磁碟的選項。 這個區段是 toohelp toofind 最適合您的工作負載選項。

#### <a name="vm-sizes"></a>VM 大小
hello Azure VM 大小規格中所列[虛擬機器的大小](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 檢閱 hello 使用進階儲存體和選擇 hello 最適當的 VM 大小最適合您的工作負載的虛擬機器的效能特性。 請確定有足夠的頻寬可用的 VM toodrive hello 磁碟流量。

#### <a name="disk-sizes"></a>磁碟大小
有五種類型的磁碟可以搭配您的 VM 使用，而且每種都有特定的 IOP 和輸送量限制。 請考量這些限制時選擇您的 VM hello 磁碟類型根據 hello 產能、 效能、 延展性方面的應用程式需求和尖峰負載。

| 進階磁碟類型  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| 磁碟大小           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| 每一磁碟的 IOPS       | 500   | 2300  | 5000           | 7500           | 7500           | 
| 每一磁碟的輸送量 | 每秒 100 MB | 每秒 150 MB | 每秒 200 MB | 每秒 250 MB | 每秒 250 MB |

根據您的工作負載，決定您的 VM 是否需要額外的資料磁碟。 您可以附加數個永續性資料磁碟 tooyour VM。 如有需要您可以等量分割跨 hello 磁碟 tooincrease hello 容量和效能的 hello 磁碟區。 (請參閱[這裡](storage-premium-storage-performance.md#disk-striping)的磁碟等量化說明。)如果您使用[儲存空間][4]等量進階儲存體資料磁碟，應該對所使用的每個磁碟中的每個資料行進行設定。 否則，hello 整體 hello 等量磁碟區的效能可能會低於預期到期 toouneven 流量分散在 hello 磁碟。 適用於 Linux Vm，您可以使用 hello *mdadm*公用程式 tooachieve hello 相同。 如需詳細資訊，請參閱文章 [在 Linux 上設定軟體 RAID](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 。

#### <a name="storage-account-scalability-targets"></a>儲存體帳戶延展性目標
進階儲存體帳戶有下列加法 toohello 中的延展性目標的 hello [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。 如果應用程式的需求超過單一儲存體帳戶的 hello 延展性目標時，建置您的應用程式 toouse 多個儲存體帳戶，並分割這些儲存體帳戶間的資料。

| 總帳戶容量 | 本地備援儲存體帳戶總頻寬 |
|:--- |:--- |
| 磁碟容量：35 TB<br />快照容量：10 TB |設定輸入 + 輸出每秒的 too50 gb |

如 hello 高階儲存體規格的詳細資訊，請簽出[延展性和效能目標時使用進階儲存體](storage-premium-storage.md#scalability-and-performance-targets)。

#### <a name="disk-caching-policy"></a>磁碟快取原則
根據預設，快取原則的磁碟是*唯讀*針對所有 hello 高階資料磁碟，和*讀寫*hello Premium 作業系統磁碟附加 toohello VM。 此組態設定，建議您使用 IOs 應用程式的 tooachieve hello 達到最佳效能。 對於頻繁寫入或唯寫的資料磁碟 (例如 SQL Server 記錄檔)，停用磁碟快取可獲得更佳的應用程式效能。 可以使用更新現有的資料磁碟的 hello 快取設定[Azure 入口網站](https://portal.azure.com)或 hello *-HostCaching* hello 參數*Set-azuredatadisk* cmdlet。

#### <a name="location"></a>位置
挑選 Azure 進階儲存體可用的位置。 如需可使用 Azure 服務之地點的最新資訊，請參閱[依區域提供的 Azure 服務](https://azure.microsoft.com/regions/#services)。 Vm 位於 hello 相同為 hello 的 hello VM 會提供較佳的效能比如果它們位於不同的區域儲存區，hello 磁碟的儲存體帳戶地區。

#### <a name="other-azure-vm-configuration-settings"></a>其他 Azure VM 組態設定
建立 Azure VM 時，您將會詢問 tooconfigure 特定 VM 設定。 請記住，一些設定固定 hello 存留期的 hello VM，而您可以修改，或稍後新增其他項目。 檢閱這些 Azure VM 組態設定，並確定這些是適當設定 toomatch 工作負載需求。

### <a name="optimization"></a>最佳化
[Azure 進階儲存體︰針對高效能進行設計](storage-premium-storage-performance.md)提供使用 Azure 進階儲存體來建置高效能應用程式的指導方針。 您可以遵循 hello 結合效能最佳作法適用於 tootechnologies 應用程式所使用的指導方針。

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>準備和複製虛擬硬碟 (Vhd) tooPremium 儲存體
hello 之後 > 一節提供準備從您的 VM 的 Vhd 和複製 Vhd tooAzure 儲存體的指導方針。

* [案例 1: 「 我正在移轉現有的 Azure Vm tooAzure 高階儲存體。 」](#scenario1)
* [案例 2: 「 我正在移轉 Vm 從其他平台 tooAzure 高階儲存體。 」](#scenario2)

### <a name="prerequisites"></a>必要條件
tooprepare hello Vhd 進行移轉，您將需要：

* Azure 訂用帳戶、 儲存體帳戶和該儲存體容器中的帳戶 toowhich 您可以複製您的 VHD。 請注意 hello 目的地儲存體帳戶可以依照個人需求的 Standard 或 Premium 儲存體帳戶。
* 工具 toogeneralize hello VHD，如果您計劃 toocreate 從它的多個 VM 執行個體。 例如，適用於 Windows 的 sysprep 或適用於 Ubuntu 的 virt-sysprep。
* 工具 tooupload hello VHD 檔案 toohello 儲存體帳戶。 請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)或使用[Azure 儲存體總管](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx)。 本指南說明複製 VHD 使用 hello AzCopy 工具。

> [!NOTE]
> 如果您選擇使用 AzCopy，以獲得最佳效能的同步複本選項複製 VHD 從 Azure VM 中 hello 執行這些工具的其中一個 hello 目的地儲存體帳戶與相同的區域。 如果從不同區域的 Azure VM 複製 VHD，您的效能可能會變慢。
>
> 透過有限頻寬中複製大量資料，請考慮[使用 hello Azure 匯入/匯出服務 tootransfer 資料 tooBlob 儲存體](../storage-import-export-service.md); 這可讓您 tootransfer 傳送硬碟資料磁碟機 tooan Azure資料中心。 您可以使用 Azure 匯入/匯出服務 toocopy 資料 tooa 標準儲存體帳戶只 hello。 一旦 hello 資料是在標準儲存體帳戶，您可以使用任一 hello[複製 Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)或 AzCopy tootransfer hello 資料 tooyour 進階儲存體帳戶。
>
> 請注意，Microsoft Azure 僅支援固定大小的 VHD 檔案。 不支援 VHDX 檔案或動態 VHD。 如果您有動態 VHD，您可以將它轉換使用 hello toofixed 大小[CONVERT-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet。
>
>

### <a name="scenario1"></a>案例 1: 「 我正在移轉現有的 Azure Vm tooAzure 高階儲存體。 」
如果您要移轉現有的 Azure Vm，停止 hello VM，準備 Vhd，每個您想，VHD 的 hello 類型，然後複製 hello VHD 利用 AzCopy 或 PowerShell。

hello VM 需要 toobe 完全關閉 toomigrate 乾淨的狀態。 Hello 移轉作業完成之前，將會中斷。

#### <a name="step-1-prepare-vhds-for-migration"></a>步驟 1. 準備 VHD 進行移轉
如果您要移轉現有的 Azure Vm tooPremium 存放裝置，可能是您的 VHD:

* 一般化作業系統映像
* 唯一的作業系統磁碟
* 資料磁碟

下面將逐步解說準備 VHD 的 3 個案例。

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>使用一般化的作業系統 VHD toocreate 多個 VM 執行個體
如果您要上傳的 VHD，將會使用的 toocreate 多個一般的 Azure VM 執行個體，您必須先一般化 VHD 使用 sysprep 公用程式。 這適用於 tooa 是在內部部署的 VHD 或 hello 雲端中。 Sysprep 會移除 hello VHD 中的任何電腦特定的資訊。

> [!IMPORTANT]
> 將 VM 一般化之前，請先擷取快照或備份。 執行 sysprep 將會停止並取消配置 hello VM 執行個體。 請遵循以下 toosysprep Windows OS VHD 的步驟。 請注意，執行 hello Sysprep 命令將會要求您 tooshut 關閉 hello 虛擬機器。 如需 Sysprep 的詳細資訊，請參閱 [Sysprep 概觀](http://technet.microsoft.com/library/hh825209.aspx)或 [Sysprep 技術參考](http://technet.microsoft.com/library/cc766049.aspx)。
>
>

1. 以系統管理員身分開啟 [命令提示字元] 視窗。
2. 輸入下列命令 tooopen Sysprep hello:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Hello 系統準備工具，在選取進入系統的全新體驗 (OOBE)，選取 hello 一般化核取方塊，選取**關機**，然後按一下**確定**hello 圖所示。 Sysprep 會一般化 hello 作業系統，並關閉 hello 系統。

    ![][1]

Ubuntu vm，使用 virt sysprep tooachieve hello 相同。 如需詳細資訊，請參閱 [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) 。 另請參閱 hello 開放原始碼的某些[佈建的 Linux 伺服器軟體](http://www.cyberciti.biz/tips/server-provisioning-software.html)針對其他 Linux 作業系統。

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>使用唯一的作業系統 VHD toocreate 單一 VM 執行個體
如果您有 hello 的 vm 需要 hello 機器特定資料上執行的應用程式時，請勿一般化 hello VHD。 非一般化的 VHD 可以是使用的 toocreate 唯一的 Azure VM 執行個體。 例如，如果您的 VHD 上有網域控制站，執行 sysprep 將會使它與網域控制站一樣沒有效率。 檢閱 hello 上 VM 與 hello 影響您在其上執行 sysprep 一般化 hello VHD 之前執行的應用程式。

##### <a name="register-data-disk-vhd"></a>註冊資料磁碟 VHD
如果您有 Azure toobe 中的資料磁碟移轉，您必須先確定 hello Vm 使用這些磁碟都已關閉的資料。

請依照下述 toocopy VHD tooAzure 高階儲存體的 hello 步驟並註冊為佈建的資料磁碟。

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>步驟 2. 建立 VHD 的 hello 目的地
建立儲存體帳戶來維護您的 VHD。 請考慮下列點的規劃位置時的 hello toostore 您的 Vhd:

* hello 目標進階儲存體帳戶。
* hello 儲存體帳戶位置必須是相同高階儲存體在 hello 最後階段中，您將建立能夠 Azure Vm。 您無法複製 tooa 新的儲存體帳戶或計劃 toouse hello 相同儲存體帳戶會根據您的需求。
* 複製並儲存 hello 儲存體帳戶金鑰的 hello 目的地儲存體帳戶的 hello 下一個階段。

針對資料磁碟，您可以選擇 tookeep 某些資料磁碟標準儲存體帳戶 （例如，磁碟有溫度更低的儲存體），但我們強烈建議您移動生產工作負載 toouse premium 儲存體的所有資料。

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>步驟 3. 使用 AzCopy 或 PowerShell 複製 VHD
您將需要 toofind 容器路徑及儲存體帳戶金鑰 tooprocess 這兩個選項之一。 容器路徑和儲存體帳戶金鑰位於 **Azure 入口網站** > **儲存體**。 hello 容器 URL 會類似"https://myaccount.blob.core.windows.net/mycontainer/"。

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>選項 1︰使用 AzCopy 複製 VHD (非同步複製)
使用 AzCopy，您可以輕鬆地上載透過 hello 網際網路 hello VHD。 Hello hello Vhd 大小而定，這可能需要時間。 使用此選項時，請記住 toocheck hello 儲存體帳戶入口/出口限制。 如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。

1. 從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)
2. 開啟 Azure PowerShell，並移 toohello AzCopy 安裝所在的資料夾。
3. 使用 hello 下列命令 toocopy hello VHD 檔案從 「 來源 」 太 「 目的地 」。

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    範例：

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    以下是 hello AzCopy 命令中使用的 hello 參數的描述：

   * **/ 來源： *&lt;來源&gt;:***  hello 資料夾或包含 hello VHD 的儲存體容器 URL 的位置。
   * **/ SourceKey: *&lt;來源帳戶金鑰&gt;:***  hello 來源儲存體帳戶的儲存體帳戶金鑰。
   * **/ 目的地： *&lt;目的地&gt;:*** 儲存體容器 URL toocopy hello VHD。
   * **/ DestKey: *&lt;目的地帳戶金鑰&gt;:***  hello 目的地儲存體帳戶的儲存體帳戶金鑰。
   * **/ 模式： *&lt;檔案名稱&gt;:***  hello VHD toocopy 指定 hello 檔案名稱。

如需詳細資訊，使用 AzCopy 工具，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>選項 2：使用 PowerShell 複製 VHD (同步處理的複製)
您也可以複製使用 hello PowerShell cmdlet 開始 AzureStorageBlobCopy hello VHD 檔案。 使用下列命令，在 Azure PowerShell toocopy VHD 上的 hello。 取代 hello <> 的來源和目的地儲存體帳戶中的對應值。 此命令時，您必須在目的地儲存體帳戶中稱為 vhd 容器 toouse。 如果 hello 容器不存在，建立一個執行 hello 命令之前。

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

範例：

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>案例 2: 「 我正在移轉 Vm 從其他平台 tooAzure 高階儲存體。 」
如果您從非 Azure 雲端儲存體 tooAzure 移轉 VHD，您必須先匯出 hello VHD tooa 本機目錄。 Hello 完整的來源路徑的 VHD 儲存位置很方便，hello 本機目錄，然後再使用 AzCopy tooupload 它 tooAzure 儲存體。

#### <a name="step-1-export-vhd-tooa-local-directory"></a>步驟 1. 匯出 VHD tooa 本機目錄
##### <a name="copy-a-vhd-from-aws"></a>從 AWS 複製 VHD
1. 如果您使用 AWS，匯出 hello EC2 執行個體 tooa Amazon S3 貯體中的 VHD。 請遵循 hello hello Amazon 匯出 Amazon EC2 執行個體 tooinstall hello Amazon EC2 命令列介面 (CLI) 工具的文件中所述的步驟，並執行 hello 建立執行個體-匯出的工作命令 tooexport hello EC2 執行個體 tooa VHD 檔案。 要確定 toouse **VHD** hello 磁碟 #95; 映像 &#95;格式的變數時執行 hello**建立執行個體-匯出的工作**命令。 hello 匯出的 VHD 檔案會儲存在您指定在此過程中的 hello Amazon S3 貯體。

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Hello VHD 檔案下載從 hello S3 貯體。 選取 hello VHD 檔案，然後**動作** > **下載**。

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>從其他非 Azure 雲端複製 VHD
如果您從非 Azure 雲端儲存體 tooAzure 移轉 VHD，您必須先匯出 hello VHD tooa 本機目錄。 複製 hello 本機目錄儲存 VHD 的 hello 完整的來源的路徑。

##### <a name="copy-a-vhd-from-on-premises"></a>從內部部署複製 VHD
如果您要移轉 VHD 從內部部署環境，您必須儲存 VHD 的 hello 完整的來源路徑。 hello 來源路徑可能是伺服器位置或檔案共用。

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>步驟 2. 建立 VHD 的 hello 目的地
建立儲存體帳戶來維護您的 VHD。 請考慮下列點的規劃位置時的 hello toostore 您的 Vhd:

* hello 目標儲存體帳戶可能是根據您的應用程式需求的標準或進階儲存體。
* hello 儲存體帳戶區域必須是相同高階儲存體在 hello 最後階段中，您將建立能夠 Azure Vm。 您無法複製 tooa 新的儲存體帳戶或計劃 toouse hello 相同儲存體帳戶會根據您的需求。
* 複製並儲存 hello 儲存體帳戶金鑰的 hello 目的地儲存體帳戶的 hello 下一個階段。

我們強烈建議您移動生產工作負載 toouse premium 儲存體的所有資料。

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>步驟 3. 上傳 hello VHD tooAzure 儲存體
現在，您會將您的 VHD 在 hello 本機目錄，您可以使用 AzCopy 或 AzurePowerShell tooupload hello.vhd 檔案 tooAzure 儲存體。 下面提供兩個選項︰

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>選項 1： 使用 Azure PowerShell Add-azurevhd tooupload hello.vhd 檔案

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

範例 <Uri> 可能是 ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***。 範例 <FileInfo> 可能是 ***"C:\path\to\upload.vhd"***。

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>選項 2： 使用 AzCopy tooupload hello.vhd 檔案
使用 AzCopy，您可以輕鬆地上載透過 hello 網際網路 hello VHD。 Hello hello Vhd 大小而定，這可能需要時間。 使用此選項時，請記住 toocheck hello 儲存體帳戶入口/出口限制。 如需詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md) 。

1. 從這裡下載並安裝 AzCopy： [AzCopy 的最新版本](http://aka.ms/downloadazcopy)
2. 開啟 Azure PowerShell，並移 toohello AzCopy 安裝所在的資料夾。
3. 使用 hello 下列命令 toocopy hello VHD 檔案從 「 來源 」 太 「 目的地 」。

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    範例：

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    以下是 hello AzCopy 命令中使用的 hello 參數的描述：

   * **/ 來源： *&lt;來源&gt;:***  hello 資料夾或包含 hello VHD 的儲存體容器 URL 的位置。
   * **/ SourceKey: *&lt;來源帳戶金鑰&gt;:***  hello 來源儲存體帳戶的儲存體帳戶金鑰。
   * **/ 目的地： *&lt;目的地&gt;:*** 儲存體容器 URL toocopy hello VHD。
   * **/ DestKey: *&lt;目的地帳戶金鑰&gt;:***  hello 目的地儲存體帳戶的儲存體帳戶金鑰。
   * **/ BlobType： 頁面：**指定該 hello 目的地是分頁 blob。
   * **/ 模式： *&lt;檔案名稱&gt;:***  hello VHD toocopy 指定 hello 檔案名稱。

如需詳細資訊，使用 AzCopy 工具，請參閱[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

##### <a name="other-options-for-uploading-a-vhd"></a>上傳 VHD 的其他選項
您也可以上傳 VHD tooyour 儲存體帳戶使用其中一種 hello 下列方法：

* [Azure 儲存體複製 Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Azure 儲存體總管上傳 Blob](https://azurestorageexplorer.codeplex.com/)
* [儲存體匯入/匯出服務 REST API 參考](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> 如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。 您可以使用[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello 時間資料的大小和傳輸的單位。
>
> 可以匯入/匯出用 toocopy tooa 標準儲存體帳戶。 您必須從標準儲存體 toopremium 儲存體帳戶，使用 AzCopy 這類工具 toocopy。
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>使用進階儲存體建立 Azure VM
Hello VHD 上傳或複製 toohello 需要儲存體帳戶之後，請遵循此節 tooregister hello VHD 中的 hello 指示做為作業系統映像或根據您的案例的作業系統磁碟，然後從它建立的 VM 執行個體。 hello 資料磁碟 VHD 可以附加的 toohello VM 建立之後。
本節的 hello 結尾會提供範例移轉指令碼。 這個簡單的指令碼不符合所有案例。 您可能需要 tooupdate hello 指令碼 toomatch 與您特定案例。 toosee 如果此指令碼適用於 tooyour 案例中，請參閱下面的[範例移轉指令碼](#a-sample-migration-script)。

### <a name="checklist"></a>檢查清單
1. 等候所有 hello VHD 磁碟複製已完成。
2. 請確認您要移轉至 hello 區域中，進階儲存體可供使用。
3. 決定 hello 您要將新 VM 系列。 它應該是支援、 高階儲存體，而 hello 大小應該根據 hello 區域中的 hello 可用性並根據您的需求。
4. 決定 hello 您將使用完全 VM 大小。 VM 大小需要 toobe 夠大 toosupport hello 您擁有的資料磁碟數目。 例如 如果您有 4 個資料磁碟，hello VM 必須有 2 個以上的核心。 也請考慮處理能力、記憶體和網路頻寬需求。
5. Hello 目標區域中建立進階儲存體帳戶。 這是您將用於 hello hello 帳戶新的 VM。
6. 有 hello 目前 VM 詳細資料很方便，包括 hello 磁碟清單及其對應的 VHD blob。

為您的應用程式做好停機準備。 toodo 全新的移轉，您必須 toostop 所有 hello 處理 hello 目前系統中。 唯有如此，您可以取得它 tooconsistent 狀態，您可以移轉 toohello 新的平台。 停機持續時間將取決於 hello hello 磁碟 toomigrate 中的資料數量。

> [!NOTE]
> 如果您要從特定的 VHD 磁碟建立 Azure 資源管理員 VM，請參閱太[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)部署使用現有的磁碟資源管理員 VM。
>
>

### <a name="register-your-vhd"></a>註冊 VHD
將 VM 從 OS VHD 或 tooattach 資料磁碟 tooa toocreate 新的 VM，您必須先註冊它們。 根據您的 VHD 案例，遵循以下步驟。

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>一般化作業系統 VHD toocreate 多個 Azure VM 執行個體
一般化的作業系統映像的 VHD 是上傳 toohello 儲存體帳戶之後，註冊為**Azure VM 映像**，讓您可以從它建立一個或多個 VM 執行個體。 使用下列 PowerShell cmdlet tooregister hello VHD 做為 Azure VM 的 OS 映像。 提供 VHD 複製到其中的 hello 完整容器 URL。

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

複製並儲存 hello 這個新的 Azure VM 映像名稱。 在 hello 上述範例中，它是*OSImageName*。

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>唯一的作業系統 VHD toocreate 單一 Azure VM 執行個體
Hello 唯一 OS VHD 後上傳的 toohello 儲存體帳戶，做為其註冊**Azure 作業系統磁碟**，讓您可以從它建立的 VM 執行個體。 使用這些 PowerShell cmdlet tooregister VHD 當做 Azure 作業系統磁碟。 提供 VHD 複製到其中的 hello 完整容器 URL。

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

複製並儲存 hello 這個新的 Azure 作業系統磁碟名稱。 在 hello 上述範例中，它是*OSDisk*。

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>資料磁碟 VHD toobe 附加 toonew Azure VM 執行個體
Hello 資料磁碟，vhd 上傳 toostorage 帳戶之後，其註冊為 Azure 資料磁碟，讓它可以是附加的 tooyour 新 DS 系列、 DSv2 系列或 GS 系列 Azure VM 執行個體。

使用這些 PowerShell cmdlet tooregister VHD 當做 Azure 資料磁碟。 提供 VHD 複製到其中的 hello 完整容器 URL。

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

複製並儲存 hello 這個新的 Azure 資料磁碟的名稱。 在 hello 上述範例中，它是*DataDisk*。

### <a name="create-a-premium-storage-capable-vm"></a>建立可支援進階儲存體的 VM
一次 hello OS 映像或作業系統磁碟會註冊，建立新的 DS 系列、 DSv2 系列或 GS 系列 VM。 您將使用 hello 作業系統映像或作業系統磁碟名稱註冊。 從 hello 高階儲存體層選取 hello VM 類型。 在下列範例中，我們會使用 hello *Standard_DS2* VM 大小。

> [!NOTE]
> 更新 hello 磁碟大小 toomake 確定它符合您的容量和效能需求和 hello 可用的 Azure 磁碟大小。
>
>

遵循以下 toocreate hello 逐步解說 PowerShell cmdlet hello 新的 VM。 首先，設定 hello 一般參數：

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

首先，建立您將在當中裝載新 VM 的雲端服務。

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

接下來，根據您的案例，請從任一 hello 作業系統映像或作業系統磁碟的註冊，讓您建立 hello Azure VM 執行個體。

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>一般化作業系統 VHD toocreate 多個 Azure VM 執行個體
建立一或多個新 DS 系列 Azure VM 執行個體使用 hello hello **Azure OS 映像**您註冊。 如下所示，建立新的 VM 時，請在 hello VM 組態中指定此作業系統映像名稱。

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>唯一的作業系統 VHD toocreate 單一 Azure VM 執行個體
建立新 DS 系列 Azure VM 執行個體使用 hello **Azure 作業系統磁碟**您註冊。 當建立 hello 新的 VM，如下所示，請在 hello VM 組態中指定此作業系統磁碟名稱。

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

指定其他 Azure VM 資訊，例如雲端服務、區域、儲存體帳戶、可用性設定組以及快取原則。 請注意，hello VM 執行個體必須位於相同位置與相關聯的作業系統或資料磁碟，因此 hello 選取雲端服務、 區域和儲存體帳戶必須是在 hello 與 hello 基礎這些磁碟的 Vhd 相同的位置。

### <a name="attach-data-disk"></a>連結資料磁碟
最後，如果您已註冊資料磁碟 Vhd，將它們附加 toohello 新 Premium 儲存體支援 Azure VM。

使用下列 PowerShell 指令程式 tooattach 資料磁碟 toohello 新的 VM，並指定 hello 快取原則。 在下例 hello 快取原則設定太*ReadOnly*。

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> 可能有額外的步驟需要 toosupport 的應用程式不會涵蓋本指南。
>
>

### <a name="checking-and-plan-backup"></a>檢查和規劃備份
一次 hello 新的 VM 已啟動且正在執行，它使用 hello 相同的登入識別碼和密碼的存取為 hello 原始 VM，並確認一切運作正常。 所有的 hello 設定，包括 hello 等量磁碟區，就會出現在 hello 新的 VM。

hello 最後一個步驟是 tooplan hello 應用程式的需求為基礎的新 VM 的備份和維護排程。

### <a name="a-sample-migration-script"></a>範例移轉指令碼
如果您有多個 Vm toomigrate，透過 PowerShell 指令碼自動化會很有用。 以下是範例指令碼自動化 hello 移轉虛擬機器。 請注意，以下的指令碼是只是範例，而且有幾個有關 hello 目前 VM 磁碟所做的假設。 您可能需要 tooupdate hello 指令碼 toomatch 與您特定案例。

hello 假設如下：

* 您正在建立傳統 Azure VM。
* 您的來源作業系統磁碟和來源資料磁碟位於相同儲存體帳戶和相同容器中。 如果您的 OS 磁碟和資料磁碟不在 hello 相同放置，您可以使用 AzCopy 或 Azure PowerShell toocopy Vhd 透過儲存體帳戶和容器。 Toohello 上一個步驟，請參閱：[利用 AzCopy 或 PowerShell 的複製 VHD](#copy-vhd-with-azcopy-or-powershell)。 編輯這個指令碼 toomeet 您的案例是另一個選擇，但建議使用 AzCopy 或 PowerShell，因為它是更方便且快速。

hello 自動化指令碼如下所示。 文字取代成您的資訊並 hello 指令碼 toomatch 以更新您的特定案例。

> [!NOTE]
> 使用 hello 現有指令碼不會保存 hello 您來源 VM 網路設定。 您必須在您移轉的 Vm 上 toore-config hello 網路設定。
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>最佳化
目前的 VM 組態可自訂特別 toowork 與標準磁碟。 比方說，tooincrease hello 效能等量磁碟區中使用多個磁碟。 例如，而不是在進階儲存體分別使用 4 個磁碟，您可能會無法 toooptimize hello 成本具有單一磁碟。 最佳化處理以案例為基礎的這個需求 toobe 等 hello 移轉之後需要自訂的步驟。 此外，請注意，此程序也不適用於資料庫和應用程式相依於定義 hello 安裝程式中的 hello 磁碟配置。

##### <a name="preparation"></a>準備工作
1. 完成 hello hello 中所述的簡單移轉前一節。 最佳化會對 hello hello 移轉之後的新 VM。
2. 定義 hello hello 最佳化設定所需新磁碟大小。
3. 判斷對應的 hello 目前磁碟/磁碟區 toohello 新磁碟的規格。

##### <a name="execution-steps"></a>執行步驟
1. 建立新的磁碟 hello 與 hello hello Premium 儲存體 VM 上的正確大小。
2. 登入 toohello VM 與複製 hello 資料從 hello 目前磁碟區 toohello 新磁碟對應 toothat 磁碟區。 所有 hello 目前磁碟區的 toomap tooa 新磁碟才能執行這項都操作。
3. 接著，變更 hello 應用程式設定 tooswitch toohello 新磁碟，並卸離 hello 舊的磁碟區。

微調 hello 以提升磁碟效能的應用程式，請參閱太[最佳化應用程式效能](storage-premium-storage-performance.md#optimizing-application-performance)。

### <a name="application-migrations"></a>應用程式移轉
資料庫與其他複雜的應用程式可能需要特殊步驟，hello hello 移轉的應用程式提供者所定義。 請參閱 toorespective 應用程式文件。 例如 資料庫通常可透過備份和還原來移轉。

## <a name="next-steps"></a>後續步驟
請參閱下列資源來移轉虛擬機器的特定案例的 hello:

* [在儲存體帳戶之間移轉 Azure 虛擬機器](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [建立並上傳 Windows Server VHD tooAzure。](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [建立和上傳的虛擬硬碟包含 hello Linux 作業系統](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [從 Amazon AWS tooMicrosoft Azure 移轉的虛擬機器](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

另請參閱下列資源 toolearn 深入了解 Azure 儲存體和 Azure 虛擬機器的 hello:

* [Azure 儲存體](https://azure.microsoft.com/documentation/services/storage/)
* [Azure 虛擬機器](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
