---
title: "aaaAzure Linux Vm 與 Azure 儲存體 |Microsoft 文件"
description: "描述 Azure 標準和進階儲存體以及 Linux 虛擬機器的受控和非受控磁碟。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Azure 和 Linux VM 儲存體
Azure 儲存體是 hello 雲端儲存體解決方案，依賴持續性、 可用性和延展性 toomeet hello 需求的客戶的現代應用程式。  在加法 toomaking 它讓開發人員 toobuild 大規模的應用程式 toosupport 新案例，Azure 儲存體也提供 hello 儲存體基礎適用於 Azure 虛擬機器。

## <a name="managed-disks"></a>受控磁碟

Azure Vm 現在都可以透過[Azure 受管理磁碟](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，讓您 toocreate Vm 而無須建立或管理任何[Azure 儲存體帳戶](../../storage/common/storage-introduction.md)自己。 指定是否要 Premium 或應該是標準儲存體和多大的 hello 磁碟，以及 Azure hello VM 磁碟會為您建立。 具有受控磁碟的 VM 都有許多重要的功能，包括︰

- 自動延展性支援。 Azure 會建立 hello 磁碟，並管理 hello 基礎儲存體 toosupport too10，註冊每個訂閱 000 磁碟。
- 提高可用性設定組的可靠性。 Azure 可確保可用性設定組內的 VM 磁碟會自動彼此隔離。
- 提高存取控制權。 受控磁碟會公開由 [Azure 角色型存取控制 (RBAC)](../../active-directory/role-based-access-control-what-is.md) 所控制的各種作業。

受控磁碟與非受控磁碟的價格不同。 如需該資訊，請參閱[受控磁碟的價格和計費](../windows/managed-disks-overview.md#pricing-and-billing)。

您可以轉換現有的 Vm，並且使用與未受管理的磁碟管理 toouse 磁碟[az vm 轉換](/cli/azure/vm#convert)。 如需詳細資訊，請參閱[如何 tooconvert 從 unmanaged Linux VM 磁碟 tooAzure 管理磁碟](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 您無法將未受管理的磁碟轉換成受管理的磁碟，如果 hello unmanaged 的磁碟儲存體帳戶，或在任何時間已經過，請使用加密[Azure 儲存體服務加密 (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 下列步驟詳細資料如何 tootooconvert unmanaged 磁碟，或已加密的儲存體帳戶中的 hello:

- 使用複製 hello 虛擬硬碟 (VHD) [az 儲存體 blob 複製開始](/cli/azure/storage/blob/copy#start)tooa 從未啟用 Azure 儲存體服務加密的儲存體帳戶。
- 建立使用受控磁碟的 VM，並在透過 [az vm create](/cli/azure/vm#create) 建立期間指定該 VHD 檔案，或
- 附加 hello 複製 VHD [az vm 磁碟附加](/cli/azure/vm/disk#attach)tooa 執行 VM 與管理的磁碟。


## <a name="azure-storage-standard-and-premium"></a>Azure 儲存體：標準和進階
Azure VM (不論是使用受控或非受控磁碟) 可以標準儲存體磁碟或進階儲存體磁碟做為建置基礎。 使用 hello 入口 toochoose VM 時，您必須切換 hello 下拉式清單中**基本概念**螢幕 tooview 標準和進階磁碟。 當已切換之的 tooSSD，premium 儲存體啟用的 Vm，也會顯示所有支援的 SSD 磁碟機。  當已切換之的 tooHDD，標準儲存體啟用 Vm 由轉動磁碟機，會顯示與高階儲存體 SSD 所支援的 Vm。

從 hello 建立 VM 時`azure-cli`時選擇透過 hello hello VM 大小，您可以選擇 standard 和 premium 之間`-z`或`--vm-size`cli 旗標。

## <a name="creating-a-vm-with-a-managed-disk"></a>建立具有受控磁碟的 VM

hello 下列範例要求 hello Azure CLI 2.0，您可以[這裡安裝](/cli/azure/install-azure-cli)。

首先，建立資源與資源群組 toomanage hello [az 群組建立](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

現在建立 hello 與 VM [az vm 建立](/cli/azure/vm#create)。 指定唯一的 `--public-ip-address-dns-name` 引數，因為可能接受 `mypublicdns`。

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

hello 前一個範例中的標準儲存體帳戶的受管理的磁碟建立的 VM。 toouse Premium 儲存體帳戶，新增 hello`--storage-sku Premium_LRS`引數，例如下列範例中的 hello:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>標準儲存體
Azure 的標準儲存體是儲存體 hello 預設類型。  標準儲存體符合成本效益同時仍然能夠發揮效能。  

## <a name="premium-storage"></a>進階儲存體
針對執行時需要大量 I/O 之工作負載的虛擬機器，「Azure 進階儲存體」可提供高效能、低延遲的磁碟支援。 使用「進階儲存體」的虛擬機器 (VM) 會將資料儲存在固態硬碟 (SSD) 上。 您可以移轉您的應用程式的 VM 磁碟 tooAzure 高階儲存體 tootake 的 hello 速度與這些磁碟的效能。

進階儲存體功能：

* 高階儲存體磁碟： Azure 高階儲存體支援可附加的 tooDS、 DSv2 或 GS 系列 Azure Vm 的 VM 磁碟。
* Premium 分頁 Blob： 進階儲存體支援 Azure 分頁 Blob，也就是使用的 toohold 永續性磁碟的 Azure 虛擬機器 (Vm)。
* 本機備援進階儲存體： 高階儲存體帳戶只支援本機備援儲存體 (LRS) 做為 hello 複寫選項和單一區域內保留三份 hello 資料。
* [進階儲存體](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>進階儲存體支援的 VM
「進階儲存體」支援 DS 系列、DSv2 系列、GS 系列及 Fs 系列的 Azure 虛擬機器 (VM)。 您可以將「標準」和「進階」儲存體磁碟與「進階儲存體」支援的 VM 搭配使用。 但是不能將「進階儲存體」磁碟與非「進階儲存體」相容的 VM 系列搭配使用。

以下是 hello 的 Linux 發行的我們驗證進階儲存體。

| 配送映像 | 版本 | 支援的核心 |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x、8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+、7.2+ | |

## <a name="azure-file-storage"></a>Azure 檔案儲存體
Azure 檔案儲存體提供使用標準 SMB 通訊協定 hello hello 雲端中的檔案共用。 Azure 檔案時，您可以移轉檔案伺服器 tooAzure 所依賴的企業應用程式。 在 Azure 中執行的應用程式可以從執行 Linux 的 Azure 虛擬機器輕鬆地掛接檔案共用。 和 hello 最新版本的檔案儲存體中，您也可以掛上檔案共用來源支援 SMB 3.0 的內部部署應用程式。  由於檔案共用為 SMB 共用，因此您可以透過標準檔案系統 API 存取它們。

檔案存放裝置是建置在 hello 與 Blob、 資料表和佇列儲存體，因此檔案存放裝置提供 hello 可用性、 持續性、 延展性及異地備援的相同技術內建 hello Azure 儲存體的平台。 如需有關檔案儲存體效能目標和限制的詳細資訊，請參閱「Azure 儲存體延展性和效能目標」。

* [如何 toouse Linux 的 Azure 檔案儲存體](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>經常性存取儲存體
hello Azure 熱儲存層最佳化儲存經常存取的資料。  熱的儲存體是 hello 預設 blob 存放區的儲存類型。

## <a name="cool-storage"></a>非經常性儲存體
hello Azure 酷炫的儲存層最佳化儲存不常存取且長時間執行的資料。 非經常性儲存體的使用案例範例包括備份、媒體內容、科學資料、規範和封存資料。 一般情況下，很少存取的任何資料是非經常性儲存體的完美候選項目。

|  | 經常性存取儲存層 | 非經常性存取儲存層 |
|:--- |:---:|:---:|
| Availability |99.9% |99% |
| 可用性 (RA-GRS 讀取) |99.99% |99.9% |
| 使用費用 |儲存成本較高 |儲存成本較低 |
| 較低的存取 |較高的存取 | |
| 和交易成本 |和交易成本 | |

## <a name="redundancy"></a>備援性
儲存體帳戶一定是您在 Microsoft Azure 中的 hello 資料複寫 tooensure 耐久性與高可用性，會議 hello Azure 儲存體 SLA，即使在暫時性硬體故障的 hello 字體。

當您建立儲存體帳戶時，您必須選取其中一個 hello 下列複寫選項：

* 本機備援儲存體 (LRS)
* 區域備援儲存體 (ZRS)
* 異地備援儲存體 (GRS)
* 讀取權限異地備援儲存體 (RA-GRS)

### <a name="locally-redundant-storage"></a>本地備援儲存體
本機備援儲存體 (LRS) 會將複寫您的資料，您可以在其中建立儲存體帳戶的 hello 區域內。 toomaximize 持久性，對儲存體帳戶中的資料提出的每個要求會複寫三次。 這三個複本會各自位於不同的容錯網域和升級網域中。  只有已寫入的 tooall 三個複本後，則要求會傳回成功。

### <a name="zone-redundant-storage"></a>區域備援儲存體
區域備援儲存體 (ZRS) 會將您的資料複寫到兩個 toothree 設備，可能在單一區域或跨兩個區域，持久性比 LRS 更高。 儲存體帳戶已啟用 ZRS，如果您的資料是永久性，即使在 hello 的 hello 設備的其中一個失敗的情況下。

### <a name="geo-redundant-storage"></a>異地備援儲存體
地理備援儲存體 (GRS) 會將複寫您資料 tooa 次要區域相隔數百英哩 hello 主要區域。 如果儲存體帳戶已啟用 GRS，則是持久即使在 hello 的全面性地區中斷或災害中的 hello 主要區域是無法復原的情況下您的資料。

### <a name="read-access-geo-redundant-storage"></a>讀取權限異地備援儲存體
藉由提供唯讀存取 toohello 資料在 hello 次要位置中，此外 toohello 複寫，跨兩個區域 GRS 所提供的讀取權限的地理備援儲存體 (RA-GRS) 最大化的可用性的儲存體帳戶。 萬一 hello hello 主要區域中的資料變成無法使用，您的應用程式可以讀取資料，從 hello 次要區域。

針對 Azure 儲存體備援性的深入探討，請參閱︰

* [Azure 儲存體複寫](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>延展性
讓您可以儲存並處理數百個 tb 的科學、 財務分析和媒體應用程式所需的資料 toosupport hello 巨量資料案例，是可大幅擴充，azure 儲存體。 或者您可以儲存 hello 少量資料所需的小型企業網站。 只要是落在您的需求，您只針對付費 hello 打算儲存的資料。 Azure 儲存體目前儲存了數十兆的獨特客戶物件，且平均每秒處理上百萬個要求。

標準儲存體帳戶：標準儲存體帳戶的總要求率上限為 20000 IOPS。 hello 跨所有的標準儲存體帳戶中的虛擬機器磁碟的 IOPS 總數不應超過此限制。

進階儲存體帳戶：進階儲存體帳戶的總輸送量速率上限為 50 Gbps。 hello 跨所有的 VM 磁碟的總輸送量不應超過此限制。

## <a name="availability"></a>Availability
我們保證，至少 99.99%（99.9%的酷炫的存取層) 的 hello 時間，我們將來自讀取權限地理備援儲存體 (RA-GRS) 帳戶已成功處理要求 tooread 資料，前提是無法嘗試 tooread 資料從 hello 主要區域重試 hello 次要區域。

我們保證，至少 99.9%（99%的酷炫的存取層) 的 hello 時間，我們將會成功處理序要求 tooread 資料從本機備援儲存體 (LRS)、 區域備援儲存體 (ZRS)，以及地理備援儲存體 (GRS) 帳戶。

我們保證，至少 99.9%（99%的酷炫的存取層) 的 hello 時間，我們將會成功處理要求 toowrite 資料 tooLocally 備援儲存體 (LRS)、 區域備援儲存體 (ZRS)，和地理備援儲存體 (GRS) 帳戶及讀取權限地理備援儲存體 (RA-GRS) 帳戶。

* [儲存體的 Azure SLA](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>區域
Azure 已正式 30 hello 世界各地的區域中，並且已宣布 4 其他地區的計劃。 地理擴充是 Azure 的優先權，因為它可讓我們的客戶 tooachieve 較高的效能，並支援其的需求和喜好設定的相關資料的位置。  最新區域 toolaunch azures 是境內的德國人。

hello Microsoft 雲端德國提供差異的選項 toohello 已提供的 Microsoft 雲端服務在歐洲，德國建立增加的機會創新和高管制的協力廠商的經濟成長及客戶hello 歐盟 (EU) 和 hello 歐洲自由貿易關聯 (EFTA)。

Hello 控制資料信任者、 T 系統國際、 獨立德文版的公司和 Deutsche Telekom 的管理中這些新的資料中心中 Magdeburg 和法蘭克福，客戶資料。 Microsoft 商業雲端服務，這些資料中心內遵守 tooGerman 資料處理規定，並為客戶提供額外的處理方式和位置資料的選項。

* [Azure 區域對應](https://azure.microsoft.com/regions/)

## <a name="security"></a>安全性
Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。 可以使用角色型存取控制與 Azure Active Directory 來保護本身的 hello 儲存體帳戶。 您可以使用用戶端加密、HTTP 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。 資料可以設定自動加密 toobe 寫入 tooAzure 使用儲存體服務加密 (SSE) 中的儲存體時。 虛擬機器所使用的作業系統和資料磁碟可以設定 toobe 使用 Azure 磁碟加密進行加密。 Azure 儲存體中的委派的存取 toohello 資料物件可以使用共用存取簽章授與。

### <a name="management-plane-security"></a>管理平面安全性
hello 管理平面 hello 使用資源 toomanage 包含儲存體帳戶。 在本節中，我們將討論 hello Azure Resource Manager 部署模型和 toouse 角色型存取控制 (RBAC) toocontrol tooyour 儲存體帳戶的存取方式。 我們也會討論管理儲存體帳戶金鑰以及如何 tooregenerate 它們。

### <a name="data-plane-security"></a>資料平面安全性
在本節中，我們將查看允許存取 toohello 實際的資料物件，在儲存體帳戶，例如 blob、 檔案、 佇列和資料表，使用共用存取簽章和預存存取原則。 我們將涵蓋服務層級的 SAS 和帳戶層級的 SAS。 我們也會看到如何 toolimit 存取 tooa 特定 IP 位址 （或 IP 位址範圍）、 toolimit hello 通訊協定使用 tooHTTPS，以及如何不需等到它的共用存取簽章 toorevoke tooexpire。

## <a name="encryption-in-transit"></a>傳輸中加密
本章節將討論如何 toosecure 資料時可以傳送傳入或傳出 Azure 儲存體。 我們將討論建議使用 HTTPS 和 hello 加密使用 Azure 檔案共用的 SMB 3.0 的 hello。 我們也將看看用戶端加密，可讓您 tooencrypt hello 資料傳輸到儲存體用戶端應用程式之前和 toodecrypt hello 資料超出儲存體傳輸後。

## <a name="encryption-at-rest"></a>待用加密
我們會討論儲存體服務加密 (SSE) 中，和如何加以啟用儲存體帳戶，導致您的區塊 blob，分頁 blob，並附加寫入 tooAzure 存放裝置時自動加密的 blob。 我們也將探討如何使用 Azure 磁碟加密，並瀏覽 hello 基本差異和與用戶端加密與 SSE 磁碟加密的情況。 我們將簡短探討美國政府電腦適用的 FIPS 相符性。

* [Azure 儲存體安全性指南](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>暫存磁碟
每個 VM 都包含一個暫存磁碟。 hello 暫存磁碟的應用程式和處理序提供短期儲存，預期的 tooonly 存放區資料，例如分頁檔。 Hello 暫存磁碟上的資料可能會遺失期間[維護事件](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)或當您[重新部署 VM](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 Hello VM 標準重開機，應保存 hello hello 暫存磁碟機上的資料。

Linux 的虛擬機器上 hello 磁碟通常是**/開發/sdb** is 格式化及裝載太**/mnt**由 hello Azure Linux 代理程式。 hello hello 暫存磁碟的大小會根據 hello hello 虛擬機器大小而不同。 如需詳細資訊，請參閱 [Linux 虛擬機器的大小](sizes.md)。

如需有關 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>節省成本
* [儲存成本](https://azure.microsoft.com/pricing/details/storage/)
* [儲存成本計算機](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>儲存體限制
* [儲存體服務限制](../../azure-subscription-service-limits.md#storage-limits)
