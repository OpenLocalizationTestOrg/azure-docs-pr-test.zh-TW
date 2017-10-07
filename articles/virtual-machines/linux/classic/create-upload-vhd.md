---
title: "aaaCreate 並上傳 Linux VHD tooAzure |Microsoft 文件"
description: "建立及上傳 Azure 虛擬硬碟 (VHD)，其中包含使用 hello 傳統部署模型將 hello Linux 作業系統"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>建立和上傳的虛擬硬碟包含 hello Linux 作業系統
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 您也可以[使用 Azure Resource Manager 上傳自訂磁碟映像](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

本文章將示範如何在 toocreate 和上傳虛擬硬碟 (VHD)，您可以將它當做自己映像 toocreate 在 Azure 虛擬機器。 了解如何 tooprepare hello 作業系統讓您可以使用它 toocreate 多部虛擬機器基礎映像上。 


## <a name="prerequisites"></a>必要條件
本文假設您有下列項目 hello:

* **安裝.vhd 檔案中的 Linux 作業系統**-您已安裝[支援 Azure 的 linux Linux 發佈](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(或參閱[非背書發佈資訊](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa 虛擬磁碟hello VHD 格式。 VM 和 VHD toocreate 有多個工具：
  * 安裝和設定[QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU)或[KVM](http://www.linux-kvm.org/page/RunningKVM)，小心 toouse VHD 作為映像格式。 如有需要，您可以使用 `qemu-img convert` 來[轉換映像](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)。
  * 您也可以在 [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) 或 [Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx) 上使用 Hyper-V。

> [!NOTE]
> 在 Azure 中不支援 hello 較新的 VHDX 格式。 當您建立 VM 時，指定 hello 格式 VHD。 如有需要您可以將轉換使用的 VHDX 磁碟 tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats)或 hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet。 此外，Azure 不支援將動態 Vhd 上, 傳，以便您需要 tooconvert 這類磁碟 toostatic Vhd 上傳之前。 您可以使用工具，例如[Azure VHD 公用程式 GO](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert 動態磁碟上傳 tooAzure hello 程序期間。

* **Azure 命令列介面**-最新安裝 hello [Azure 命令列介面](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)tooupload hello VHD。

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>步驟 1： 準備上傳的 hello 映像 toobe
Azure 支援各種 Linux 散發套件 (請參閱 [背書的散發套件](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))。 hello 下列文章會引導您完成 tooprepare hello Azure 所支援各種 Linux 散發套件的方式。 完成 hello 下列指南中的 hello 步驟之後，再回到這裡之後準備 tooupload tooAzure 的 VHD 檔案：

* **[CentOS 型散發套件](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES 和 openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[其他：非背書散發套件](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> hello Azure 平台 SLA 套用 toovirtual 機器中執行 Linux 作業系統，其中一個 hello 背書分佈時，才會搭配 hello 設定詳細資料，以指定在支援版本的 hello [Linux Azure-Endorsed 發佈](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Hello Azure 映像庫中的所有 Linux 散發套件都是背書分佈利用 hello 必要的設定。
> 
> 

另請參閱 hello  **[Linux 安裝注意事項](../create-upload-generic.md#general-linux-installation-notes)**如需有關準備 Azure Linux 映像的多個一般秘訣。

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>步驟 2： 準備 hello 連接 tooAzure
請確定您使用 hello 傳統部署模型中的 hello Azure CLI (`azure config mode asm`)，然後登入 tooyour 帳戶：

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>步驟 3： 上傳 hello 映像 tooAzure
您需要儲存體帳戶 tooupload 您的 VHD 檔案。 您可以選取現有的儲存體帳戶或[建立新帳戶](../../../storage/common/storage-create-storage-account.md)。

使用下列命令的 hello 使用 hello Azure CLI tooupload hello 映像：

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

在 hello 前一個範例中：

* **BlobStorageURL**是您計劃 toouse hello 儲存體帳戶的 hello URL
* **YourImagesFolder**是 hello blob 儲存容器所在 toostore 您的映像
* **VHDName** hello 標籤出現在入口網站 tooidentify hello 虛擬硬碟中。
* **PathToVHDFile**是 hello 完整路徑和名稱在您的電腦上的 hello.vhd 檔案。

下列命令的 hello 示範完整的範例：

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>步驟 4： 從 hello 映像建立 VM
您建立 VM 使用`azure vm create`在 hello 與規則 VM 相同的方式。 指定您為您的映像提供 hello 上一個步驟中的 hello 名稱。 在下列範例的 hello，我們會使用 hello **myImage** hello 上一個步驟中提供的映像名稱：

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate Vm，提供您自己的使用者名稱 + 密碼、 位置、 DNS 名稱和映像名稱。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱[hello Azure 傳統部署模型的 Azure CLI 參考](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
