---
title: "aaaUpload 自訂 Linux 映像與 Azure CLI 1.0 |Microsoft 文件"
description: "建立並上載虛擬硬碟 (VHD) tooAzure 與自訂 Linux 映像使用 hello Resource Manager 部署模型和 hello Azure CLI 1.0。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>上傳和自訂的磁碟映像建立 Linux VM，請使用 Azure CLI 1.0 hello
本文章將示範如何使用虛擬硬碟 (VHD) tooAzure tooupload hello Resource Manager 部署模型並從這個自訂映像建立 Linux Vm。 這項功能可讓您 tooinstall 和設定 Linux distro tooyour 需求，然後使用該 VHD tooquickly 建立 Azure 虛擬機器 (Vm)。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="quick-commands"></a>快速命令
如果您需要 tooquickly 完成 hello 工作，請在下列章節詳細資料 hello hello 基底命令 tooupload VM tooAzure。 詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#requirements)。

請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。

首先，建立資源群組。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUs`位置：

```azurecli
azure group create myResourceGroup --location "WestUS"
```

建立儲存體帳戶 toohold 虛擬磁碟。 hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

清單 hello 儲存體帳戶的存取金鑰。 記下 `key1`：

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

建立使用您所取得的 hello 儲存體金鑰的儲存體帳戶內的容器。 hello 下列範例會建立名為的容器`myimages`使用 hello 從儲存體金鑰值`key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

最後上, 傳您所建立的 VHD toohello 容器。 指定 hello 本機路徑 tooyour VHD 下`/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

您現在可以 [使用 Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd)，從上傳的虛擬磁碟建立 VM。 您也可以藉由指定 hello URI tooyour 磁碟使用 hello CLI (`--image-urn`)。 hello 下列範例會建立名為的 VM`myVM`使用 hello 先前上傳的虛擬磁碟：

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

hello 目的地儲存體帳戶有 toobe 相同 hello 做為您上傳至您的虛擬磁碟。 您也需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數`azure vm create`命令，例如虛擬網路、 公用 IP 位址、 使用者名稱和 SSH 金鑰。 閱讀更多有關 hello[可用 CLI 資源管理員參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。

## <a name="requirements"></a>需求
toocomplete hello 下列步驟，您需要：

* **安裝.vhd 檔案中的 Linux 作業系統**-安裝[支援 Azure 的 linux Linux 發佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa hello VHD 中的虛擬磁碟格式。 VM 和 VHD toocreate 有多個工具：
  * 安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。 如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。
  * 您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。

> [!NOTE]
> 在 Azure 中不支援 hello 較新的 VHDX 格式。 當您建立 VM 時，指定 hello 格式 VHD。 如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。 此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。 您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。
> 
> 

* 從您的自訂映像建立 Vm 必須位在 hello 相同儲存體帳戶做為本身 hello 映像
  * 建立儲存體帳戶和容器 toohold，您的自訂映像和建立的 Vm
  * 建立所有 VM 之後，您即可放心地刪除您的映像

請確定您有[hello Azure CLI 1.0](../../cli-install-nodejs.md)登入，並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myimages`。

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>準備上傳的 hello 映像 toobe
Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式：

* **[CentOS 型散發套件](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES 和 openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[其他：非背書散發套件](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

另請參閱 hello  **[Linux 安裝注意事項](create-upload-generic.md#general-linux-installation-notes)**如需有關準備 Azure Linux 映像的多個一般秘訣。

> [!NOTE]
> hello [Azure 平台 SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/)適用於僅當其中一個 hello 背書分佈會搭配 hello 設定詳細資料，指定在支援版本底下執行 Linux 的 tooVMs [Linux 上支援 Azure 的 Linux分佈](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。


## <a name="create-a-resource-group"></a>建立資源群組
資源群組以邏輯方式結合所有 hello Azure 資源 toosupport 您的虛擬機器，例如 hello 虛擬網路和儲存體。 從 [這裡](../../azure-resource-manager/resource-group-overview.md)深入了解 Azure 資源群組。 之前上傳您的自訂磁碟映像建立 Vm，您必須先 toocreate 資源群組。 

hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`WestUS`位置：

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>建立儲存體帳戶
VM 會以分頁 Blob 的形式儲存在儲存體帳戶內。 從[這裡](../../storage/common/storage-introduction.md#blob-storage)深入了解 Azure Blob 儲存體。 您要為自訂磁碟映像和 VM 建立儲存體帳戶。 在您自訂的磁碟映像需要 toobe 從您建立的所有 Vm 都 hello 做為該映像的相同儲存體帳戶。

hello 下列範例會建立名為的儲存體帳戶`mystorageaccount`hello 先前建立的資源群組中：

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>列出儲存體帳戶金鑰
Azure 會為每個儲存體帳戶產生兩個 512 位元的存取金鑰。 驗證 toohello 儲存體帳戶，例如 toocarry 寫入作業時，會使用這些存取金鑰。 深入了解[管理存取 toostorage 這裡](../../storage/common/storage-create-storage-account.md#manage-your-storage-account)。 您可以檢視便捷鍵以 hello`azure storage account keys list`命令。

檢視 hello hello 您所建立的儲存體帳戶的存取金鑰：

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
請記下`key1`因為您可以將 toointeract hello 後續步驟中儲存體帳戶。

## <a name="create-a-storage-container"></a>建立儲存體容器
在 hello 中建立不同的目錄 toologically 相同方式，組織您的本機檔案系統，您的虛擬磁碟和映像，建立儲存體帳戶 tooorganize 內的容器。 儲存體帳戶可以包含任意數目的容器。 

hello 下列範例會建立名為的容器`myimages`，指定 hello 便捷鍵 hello 上一個步驟中取得 (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>上傳 VHD
現在您可以實際上傳您的自訂磁碟映像。 與 VM 使用的所有虛擬磁碟相同，您會以分頁 Blob 的形式上傳及儲存您的自訂磁碟映像。

指定您的存取金鑰，您在 hello 前一個步驟中建立的 hello 容器，然後再 hello 路徑 toohello 自訂的磁碟映像，在本機電腦上：

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>從自訂映像建立 VM
當您從您的自訂磁碟映像建立 Vm 時，請指定 hello URI toohello 磁碟映像。 請確定該 hello 目的地儲存體帳戶儲存您的自訂磁碟映像的相符項目。 您可以建立您的 VM 使用 hello Azure CLI 或資源管理員 JSON 範本。

### <a name="create-a-vm-using-hello-azure-cli"></a>使用 Azure CLI hello 建立 VM
您指定 hello`--image-urn`參數以 hello`azure vm create`命令 toopoint tooyour 自訂的磁碟映像。 請確認`--storage-account-name`相符項目 hello 儲存您的自訂磁碟映像的儲存體帳戶。 您沒有 toouse hello 相同容器 hello 自訂的磁碟映像 toostore 為您的 Vm。 請確定 toocreate hello 中任何其他容器相同方式與上傳您的自訂磁碟映像之前 hello 先前的步驟。

hello 下列範例會建立名為的 VM`myVM`從您的自訂磁碟映像：

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

您仍然需要 toospecify，或回答會提示您輸入時，所有 hello hello 所需的其他參數`azure vm create`命令，例如虛擬網路、 公用 IP 位址、 使用者名稱和 SSH 金鑰。 深入了解 hello[可用 CLI 資源管理員參數](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines)。

### <a name="create-a-vm-using-a-json-template"></a>使用 JSON 範本來建立 VM
Azure 資源管理員範本會定義您想 toobuild hello 環境的 JavaScript Object Notation (JSON) 檔案。 hello 範本會細分 toodifferent 資源提供者，例如計算或網路中。 您可以使用現有的範本或自行撰寫範本。 深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。

Hello 內`Microsoft.Compute/virtualMachines`範本的提供者，您有`storageProfile`節點，包含您的 VM hello 設定詳細資料。 hello 兩個主要的參數 tooedit 是 hello`image`和`vhd`點 tooyour 自訂的磁碟映像，您的新 VM 的虛擬磁碟的 Uri。 hello 下列顯示 hello JSON 的範例使用自訂的磁碟映像：

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

您可以使用[這個現有的範本 toocreate 從自訂映像的 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image)或閱讀有關[建立您自己的 Azure Resource Manager 範本](../../azure-resource-manager/resource-group-authoring-templates.md)。 

設定範本之後，您會建立 Vm 使用 hello`azure group deployment create`命令。 指定 hello JSON 範本的 URI 與 hello`--template-uri`參數：

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

如果您有 JSON 檔案儲存在本機電腦上，您可以使用 hello`--template-file`參數改為：

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>後續步驟
在您備妥並上傳自訂虛擬磁碟之後，您可以深入了解如何 [使用 Resource Manager 和範本](../../azure-resource-manager/resource-group-overview.md)。 您也可以太[新增資料磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooyour 新 Vm。 如果您有 Vm 上執行，您需要 tooaccess 應用程式，請務必太[開啟連接埠和端點](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

