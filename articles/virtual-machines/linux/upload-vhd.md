---
title: "aaaUpload 或複製自訂的 Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "上傳或複製自訂的虛擬機器使用 hello Resource Manager 部署模型和 hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>從自訂的磁碟以 hello Azure CLI 2.0 建立 Linux VM

<!-- rename toocreate-vm-specialized -->

本文章將示範如何 tooupload 自訂虛擬硬碟 (VHD) 或複製在 Azure 中現有的 VHD，並從 hello 自訂磁碟建立新的 Linux 虛擬機器 (Vm)。 您可以安裝和設定 Linux distro tooyour 需求，然後使用該 VHD tooquickly 建立新的 Azure 虛擬機器。

如果您想 toocreate 多個 Vm 從自訂磁碟，您應該從您的 VM 或 VHD 建立映像。 如需詳細資訊，請參閱[建立自訂映像的 Azure VM 使用 hello CLI](tutorial-custom-images.md)。

您有兩個選擇：
* [上傳 VHD](#option-1-upload-a-specialized-vhd)
* [複製現有的 Azure VM](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>快速命令

當建立新的 VM 使用[az vm 建立](/cli/azure/vm#create)從自訂或特定磁碟您**附加**hello 磁碟 (-附加 os 磁碟) 而不是指定的自訂或 marketplace 映像 (-映像)。 hello 下列範例會建立名為的 VM *myVM*使用 hello 受管理的名為磁碟*myManagedDisk*建立從自訂的 VHD:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>需求
toocomplete hello 下列步驟，您需要：

* 一部已準備好用於 Azure 中的 Linux 虛擬機器。 hello[準備 hello VM](#prepare-the-vm)這篇文章的章節將涵蓋如何 toofind distro 特定安裝資訊 hello Azure Linux 代理程式 (waagent) 才能正確地在 Azure 中的 hello VM toowork 以及您 toobe 無法 tooconnect使用 SSH tooit。
* hello VHD 檔案從現有[支援 Azure 的 linux Linux 發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 格式的虛擬磁碟。 VM 和 VHD toocreate 有多個工具：
  * 安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。 如有需要，您可以使用 **qemu-img convert** 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) \(英文\)。
  * 您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。

> [!NOTE]
> 在 Azure 中不支援 hello 較新的 VHDX 格式。 當您建立 VM 時，指定 hello 格式 VHD。 如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [qemu img 轉換](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [CONVERT-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。 此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。 您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。
> 
> 


* 請確定您擁有 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 myResourceGroup、mystorageaccount 和 mydisks。

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>準備 VM hello

Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式：

* [CentOS 型發行版本](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [其他：非背書的發行版本](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

另請參閱 hello [Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)如需有關準備 Azure Linux 映像的多個一般秘訣。

> [!NOTE]
> hello [Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)適用於僅當其中一個 hello 背書分佈會搭配 hello 設定詳細資料，指定在支援版本底下執行 Linux 的 tooVMs [Linux 上支援 Azure 的 Linux分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
> 
> 

## <a name="option-1-upload-a-vhd"></a>選項 1：上傳 VHD

您可以上傳已在本機電腦上執行或從另一個雲端匯出的自訂 VHD。 toouse hello VHD toocreate 新的 Azure VM，您需要 tooupload hello VHD tooa 儲存體帳戶，並從 hello VHD 建立受管理的磁碟。 

### <a name="create-a-resource-group"></a>建立資源群組

上傳您自訂的磁碟和之前建立的 Vm，您必須先 toocreate 的資源群組與[az 群組建立](/cli/azure/group#create)。

hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *eastus*位置： [Azure 受管理磁碟概觀](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>建立儲存體帳戶

使用 [az storage account create](/cli/azure/storage/account#create) 為自訂磁碟和 VM 建立儲存體帳戶。 

hello 下列範例會建立名為的儲存體帳戶*mystorageaccount* hello 先前建立的資源群組中：

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>列出儲存體帳戶金鑰
Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。 驗證 toohello 儲存體帳戶，例如一波波的寫入作業時，會使用這些存取金鑰。 深入了解[管理存取 toostorage 這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)。 檢視與 hello 便捷鍵[az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。

檢視 hello hello 您所建立的儲存體帳戶的存取金鑰：

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

hello 輸出如下：

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
請記下**key1**因為您可以將 toointeract hello 後續步驟中儲存體帳戶。

### <a name="create-a-storage-container"></a>建立儲存體容器
在 hello 中建立不同的目錄 toologically 相同方式，組織您的本機檔案系統，您建立儲存體帳戶 tooorganize 內的容器，您的磁碟。 儲存體帳戶可以包含任意數目的容器。 使用 [az storage container create](/cli/azure/storage/container#create) 來建立容器。

hello 下列範例會建立名為的容器*mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>上傳 VHD hello
現在您可以使用 [az storage blob upload](/cli/azure/storage/blob#upload) 上傳您的自訂磁碟。 您上傳並將您的自訂磁碟儲存為分頁 Blob。

指定您的存取金鑰，您在 hello 前一個步驟中建立的 hello 容器，然後 hello 路徑 toohello 自訂磁碟在本機電腦上：

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
正在上傳 hello VHD，可能需要一些時間。

### <a name="create-a-managed-disk"></a>建立受控磁碟


建立受管理的磁碟 hello VHD 使用[az 磁碟建立](/cli/azure/disk#create)。 hello 下列範例會建立名為受管理的磁碟*myManagedDisk*從 hello VHD 上傳 tooyour 名為儲存體帳戶和容器：

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>選項 2：複製現有的 VM

您也可以建立 hello 自訂的 Azure，然後複製 hello OS 磁碟 VM，並將它附加新 VM toocreate tooa 另一份複本。 這是正常進行測試，但如果您想要 toouse 現有的 Azure VM hello 模型為多個新的 Vm，您實際上應該建立**映像**改為。 如需有關如何從現有的 Azure VM 建立映像的詳細資訊，請參閱[建立 Azure VM 使用 hello CLI 的自訂映像](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>建立快照集

這個範例會在名為 myResourceGroup 資源群組中建立名為 myVM 的 VM 快照集，並建立名為 osDiskSnapshot 的快照集。

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>建立 hello 受管理的磁碟

建立新的受管理的磁碟從 hello 快照集。

取得 hello 識別碼 hello 快照集。 在此範例中，名為 hello 快照*osDiskSnapshot* hello，且*myResourceGroup*資源群組。

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

建立 hello 受管理的磁碟。 在此範例中，我們將從快照集中建立名為 myManagedDisk 的受控磁碟，其在標準儲存體中大小為 128 GB。

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>建立 hello VM

現在，建立具有您 VM [az vm 建立](/cli/azure/vm#create)與附加 (-附加 os 磁碟) hello 管理 hello OS 磁碟的磁碟。 hello 下列範例會建立名為的 VM *myNewVM*使用 hello 管理從您上傳的 VHD 建立磁碟：

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

您應該能夠 tooSSH hello VM 到 hello 來源 VM 使用 hello 認證。 

## <a name="next-steps"></a>後續步驟
在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。 您也可以太[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooyour 新 Vm。 如果您有 Vm 上執行，您需要 tooaccess 應用程式，請務必太[開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

