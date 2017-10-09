---
title: "使用 SMB 的 Linux Vm 上的 Azure 檔案儲存體 aaaMount |Microsoft 文件"
description: "使用 SMB 與 Linux Vm 上的 Azure 檔案儲存體 toomount hello Azure CLI 2.0 的方式"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a>使用 SMB 在 Linux VM 上掛接 Azure 檔案儲存體

本文章將示範如何 tooutilize hello Azure 檔案儲存體服務，使用 SMB 在 Linux VM 上裝載以 hello Azure CLI 2.0。 Azure 檔案儲存體提供使用標準 SMB 通訊協定 hello hello 雲端中的檔案共用。 您也可以執行下列步驟以 hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 hello 需求如下：

- [一個 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)
- [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md)

## <a name="quick-commands"></a>快速命令

* 資源群組
* Azure 虛擬網路
* 具有 SSH 輸入的網路安全性群組
* 子網路
* Azure 儲存體帳戶
* Azure 儲存體帳戶金鑰
* Azure 檔案儲存體共用
* Linux VM

將任何範例換成您自己的設定。

### <a name="create-a-directory-for-hello-local-mount"></a>建立 hello 本機掛接的目錄

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a>掛接 hello 檔案儲存體 SMB 共用 toohello 掛接點

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a>在重新開機後持續 hello 掛接
toodo，加入下列行 toohello hello `/etc/fstab`:

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

檔案存放裝置提供 hello 雲端中的檔案共用使用 hello 標準 SMB 通訊協定。 Hello 最新版本的檔案儲存體中，您也可以從任何作業系統，支援 SMB 3.0 裝載檔案共用。 當您使用 SMB 裝載在 Linux 上時，您取得簡單備份 tooa 穩固、 永久封存儲存體位置的 SLA 支援。

檔案存放裝置上，從裝載 VM tooan SMB 掛接移動檔案是很好的方法 toodebug 記錄。 這是因為可以在本機裝載相同的 SMB 共用的 hello tooyour Mac、 Linux 或 Windows 的工作站。 SMB 不 hello Linux 資料流處理的最佳解決方案，或因為 hello SMB 通訊協定不是應用程式記錄檔即時建置 toohandle 這類大量記錄的責任。 專用的整合記錄層級工具，像是 Fluentd，是比透過 SMB 收集 Linux 和應用程式記錄輸出更好的選擇。

此詳細逐步解說中，我們會建立 hello 必要條件需要 toofirst 建立 hello 檔案存放裝置共用，然後再將它裝載透過 SMB，Linux VM 上。

1. 建立資源群組與[az 群組建立](/cli/azure/group#create)toohold hello 檔案共用。

    資源群組命名為的 toocreate `myResourceGroup` hello 「 美國西部 」 位置，使用下列範例中的 hello:

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. 建立 Azure 儲存體帳戶與[az 儲存體帳戶建立](/cli/azure/storage/account#create)toostore hello 實際檔案。

    toocreate 儲存體帳戶命名 mystorageaccount 使用 hello Standard_LRS 儲存體 SKU，下列範例使用 hello:

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. 顯示 hello 儲存體帳戶金鑰。

    當您建立儲存體帳戶時，會建立 hello 帳戶金鑰組中，讓它們可以旋轉沒有任何服務中斷。 當您切換 toohello 第二個金鑰 hello 配對中時，您會建立新的金鑰組。 新的儲存體帳戶金鑰一律會在配對，確保永遠有至少一個未使用的儲存體帳戶金鑰準備 tooswitch 來建立。

    檢視 hello 儲存體帳戶金鑰，以 hello [az 儲存體帳戶金鑰清單](/cli/azure/storage/account/keys#list)。 hello hello 名為的儲存體帳戶金鑰`mystorageaccount`hello 下列範例所示：

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    tooextract 單一索引鍵，使用 hello`--query`旗標。 hello 下列範例會擷取 hello 第一個索引鍵 (`[0]`):

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. 建立 hello 檔案存放裝置共用。

    hello 檔案存放裝置共用包含的 hello 與 SMB 共用[az 存放裝置共用建立](/cli/azure/storage/share#create)。 hello 配額一律會以表示 (gb)。 從上述 hello 傳入 hello 金鑰的其中之一`az storage account keys list`命令。 建立共用，使用下列範例中的 hello 具名 mystorageshare 具有 10 GB 配額：

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. 建立掛接點目錄。

    在 hello Linux 檔案系統 toomount hello SMB 共用上建立本機目錄。 任何寫入或讀取 hello 本機掛接目錄轉送的 toohello SMB 共用上裝載的檔案存放裝置。 toocreate /mnt/retention/ mymountdirectory，下列範例使用 hello 的本機目錄：

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. 掛接 hello SMB 共用 toohello 本機目錄。

    請提供您自己的儲存體帳戶的使用者名稱和 hello 掛接認證的儲存體帳戶金鑰，如下所示：

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. 保存的 hello SMB 裝載重新開機。

    當您重新啟動 hello Linux VM 時，hello 掛接的 SMB 共用正在卸載所造成關機期間。 SMB 共用的開機，tooremount hello 新增列 toohello Linux /etc/fstab。 Linux 使用 hello fstab 檔案 toolist hello 檔案系統，它需要 toomount hello 開機程序期間。 新增 hello SMB 共用可確保該 hello 檔案存放裝置共用是 hello Linux VM 的永久掛接的檔案系統。 加入 hello 檔案存放裝置的 SMB 共用 tooa 新的 VM 時，可能您使用雲端 init。

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a>後續步驟

- [在建立期間使用雲端 init toocustomize Linux VM](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [新增磁碟 tooa Linux VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [使用 Azure CLI hello 加密 Linux VM 上的磁碟](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
