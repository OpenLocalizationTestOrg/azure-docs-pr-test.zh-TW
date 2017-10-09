---
title: "從 Azure Linux VHD aaaDownload |Microsoft 文件"
description: "下載 Linux VHD 使用 hello Azure CLI 和 hello Azure 入口網站。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>從 Azure 下載 Linux VHD

在本文中，您將學習如何 toodownload [Linux 虛擬硬碟 (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)檔案從 Azure 中，使用 hello Azure CLI 和 Azure 入口網站。 

Azure 的使用中的虛擬機器 (Vm)[磁碟](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)位置 toostore 作業系統、 應用程式，以及資料。 所有 Azure VM 都至少有兩個磁碟：一個 Windows 作業系統磁碟和一個暫存磁碟。 從映像，一開始建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會儲存在 Azure 儲存體帳戶的 Vhd。 虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。

如果尚未安裝 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)，請先安裝。

## <a name="stop-hello-vm"></a>停止 hello VM

如果它已附加，無法從 Azure 下載 VHD tooa 執行 VM。 您需要 toostop hello VM toodownload VHD。 如果您想 toouse VHD 當做[映像](tutorial-custom-images.md)toocreate 其他 Vm 使用新磁碟時，需要 toodeprovision 和一般化 hello 中所包含的 hello 作業系統檔案，並停止 hello VM。 toouse hello VHD 現有的 VM 或資料磁碟的新執行個體的磁碟，您只需要 toostop 和解除配置 hello VM。

toouse hello 做為映像 toocreate 其他 Vm 的 VHD，請完成下列步驟：

1. 使用 SSH、 hello 帳戶名稱，以及的 hello VM tooconnect tooit hello 公用 IP 位址和取消佈建它。 hello + 使用者參數也會移除 hello 最後一個佈建的使用者帳戶。 如果您將 toohello VM 中的帳戶認證，會省略這 + user 參數。 hello 下列範例會移除 hello 最後一個佈建的使用者帳戶：

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. 使用的 Azure 帳戶登入 tooyour [az 登入](https://docs.microsoft.com/cli/azure/#login)。
3. 停止並取消配置 hello VM。

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. 一般化 hello VM。 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello 做為現有的 VM 或資料磁碟的新執行個體磁碟的 VHD 會完成下列步驟：

1.  登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2.  在 hello 中樞功能表中，按一下 **虛擬機器**。
3.  Hello 清單中選取 hello VM。
4.  Hello VM hello] 刀鋒視窗，按一下 [**停止**。

    ![停止 VM](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>產生 SAS URL

toodownload hello VHD 檔案，您需要 toogenerate[共用的存取簽章 (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL。 當產生 hello URL 時，到期時間會指派 toohello URL。

1.  在 hello VM 的 hello 刀鋒視窗的 [hello] 功能表上按一下**磁碟**。
2.  選取 VM，hello hello 作業系統磁碟，然後按一下**匯出**。
3.  按一下 [產生 URL]。

    ![產生 URL](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>下載 VHD

1.  下所產生的 hello URL，按一下 下載 hello VHD 檔案。

    ![下載 VHD](./media/download-vhd/export-download.png)

2.  您可能需要 tooclick**儲存**hello 瀏覽器 toostart hello 下載中。 hello hello VHD 檔案的預設名稱是*abcd*。

    ![Hello 瀏覽器中，按一下 [儲存]](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>後續步驟

- 了解如何太[上傳並從自訂的磁碟以 hello Azure CLI 2.0 建立 Linux VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 
- [管理 Azure 磁碟 hello Azure CLI](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

