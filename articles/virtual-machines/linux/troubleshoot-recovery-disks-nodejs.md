---
title: "Linux VM 疑難排解以 hello Azure CLI 1.0 的 aaaUse |Microsoft 文件"
description: "了解如何連接 hello OS 磁碟 tooa 復原 VM 使用發出 Linux VM 的 tootroubleshoot hello Azure CLI 1.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a>疑難排解 Linux VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 hello Azure CLI 1.0
如果您的 Linux 虛擬機器 (VM) 會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。 常見範例是無效的項目中`/etc/fstab`，防止 hello VM 可以 tooboot 成功。 本文詳細說明如何 toouse hello Azure CLI 1.0 tooconnect 虛擬硬碟磁碟 tooanother Linux VM toofix 任何錯誤，然後重新建立原始 VM。


## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作
您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](#recovery-process-overview) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）
- [Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI


## <a name="recovery-process-overview"></a>復原程序概觀
hello 疑難排解程序如下所示：

1. 刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。
2. 附加和掛接 hello Linux VM 的虛擬硬碟 tooanother 供疑難排解之用。
3. 連接 toohello 疑難排解 VM。 編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。
4. 取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。
5. 使用建立 VM hello 原始虛擬硬碟。

請確定您有[hello 最新的 Azure CLI 1.0](../../cli-install-nodejs.md)安裝並登入並使用 Resource Manager 模式：

```azurecli
azure config mode arm
```

在 hello 下列範例中，會取代您自己的值的參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。


## <a name="determine-boot-issues"></a>判斷開機問題
請檢查您的 VM 為何不能 tooboot 正確 hello 序列輸出 toodetermine。 常見範例是無效的項目中`/etc/fstab`，或 hello 基礎虛擬硬碟正在刪除或移動。

hello 下列範例會取得 hello 序列輸出從名為 VM hello `myVM` hello 資源群組中名為`myResourceGroup`:

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

檢閱 hello 序列輸出的 toodetermine hello VM 失敗 tooboot 的原因。 如果 hello 序列輸出不提供任何資訊指出，您可能需要 tooreview 記錄檔中的`/var/log`一旦您擁有 hello 虛擬硬碟連接 tooa 疑難排解 VM。


## <a name="view-existing-virtual-hard-disk-details"></a>檢視現有的虛擬硬碟詳細資料
您可以將附加您的虛擬硬碟 tooanother VM 之前，您會需要 tooidentify hello hello 虛擬硬碟 (VHD) 名稱。 

hello 下列範例會取得名為 VM hello 資訊`myVM`hello 資源群組中名為`myResourceGroup`:

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

尋找`Vhd URI`hello hello 前面命令輸出中。 hello 下列截斷的範例輸出顯示 hello `Vhd URI` hello 最後一行：

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a>刪除現有的 VM
虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。 虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。 hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。 每個虛擬硬碟已連接時，指派租用 tooa VM。 雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。 hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。

hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。 刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。 刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。

下列範例刪除 hello hello 名為 VM`myVM`從名為 hello 資源群組`myResourceGroup`:

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。 hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>附加現有的虛擬硬碟 tooanother VM
如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。 附加 hello 疑難排解 VM toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。 此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。 選擇或建立另一個 VM toouse 供疑難排解之用。

當您附加 hello 現有虛擬硬碟時，指定在 hello 上述中取得的 hello URL toohello 磁碟`azure vm show`命令。 hello 下列範例會附加疑難排解名為 VM 的現有虛擬硬碟 toohello `myVMRecovery` hello 資源群組中名為`myResourceGroup`:

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a>掛接 hello 連接的資料磁碟

> [!NOTE]
> hello 下列範例詳細說明 hello Ubuntu 虛擬機器上所需的步驟。 如果您使用不同的 Linux distro，例如 Red Hat Enterprise Linux 或 SUSE，hello 記錄檔位置和`mount`命令可能會稍有不同。 如需您特定 distro hello 命令中的適當變更，請參閱 toohello 文件。

1. SSH tooyour 疑難排解 VM 使用 hello 適當的認證。 如果這個磁碟是 hello 第一個資料磁碟附加 tooyour 疑難排解 VM，hello 磁碟的連接可能太`/dev/sdc`。 使用`dmseg`tooview 連接的磁碟：

    ```bash
    dmesg | grep SCSI
    ```

    hello 輸出是 toohello 類似下列範例程式碼：

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    在上述範例中的 hello，hello OS 磁碟位於`/dev/sda`和 hello 暫存磁碟提供給每個 VM 位於`/dev/sdb`。 如果您有多個資料磁碟，它們應該是位於 `/dev/sdd`、`/dev/sde`，依此類推。

2. 建立目錄 toomount 您現有的虛擬硬碟。 hello 下列範例會建立一個名為目錄`troubleshootingdisk`:

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. 如果您在現有的虛擬硬碟上有多個資料分割，裝載所需的 hello 磁碟分割。 hello 下列範例會 hello 第一個主要磁碟分割在`/dev/sdc1`:

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > 最佳作法是 toomount 資料磁碟上的 Vm 在 Azure 中使用 hello hello 虛擬硬碟的通用唯一識別碼 (UUID)。 針對這個簡短的疑難排解案例，不需要掛接 hello 虛擬硬碟使用 hello UUID。 但是，在正常使用，編輯`/etc/fstab`toomount 虛擬硬碟使用的裝置名稱，而非可能會造成 UUID hello VM toofail tooboot。


## <a name="fix-issues-on-original-virtual-hard-disk"></a>修正原始虛擬硬碟的問題
與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。 一旦解決 hello 問題之後，繼續進行步驟 hello。


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>卸載並中斷連結原始虛擬硬碟
一旦解決的錯誤，您會卸載，並中斷您疑難排解的 VM 中的 hello 現有虛擬硬碟。 您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。

1. 從 hello SSH 工作階段 tooyour 疑難排解 VM，卸載 hello 現有虛擬硬碟。 第一次變更超出您掛接點的 hello 父目錄：

    ```bash
    cd /
    ```

    現在取消掛接 hello 現有虛擬硬碟。 hello 下例取消掛接在 hello 裝置`/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

2. 現在您可以卸離 hello 虛擬硬碟從 hello VM。 結束 hello SSH 工作階段 tooyour 疑難排解 VM。 在 hello Azure CLI，第一個清單 hello 會附加資料磁碟 tooyour 疑難排解 VM。 hello 下列範例列出 hello 資料磁碟附加 toohello 名為 VM `myVMRecovery` hello 資源群組中名為`myResourceGroup`:

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    請注意 hello`Lun`您現有的虛擬硬碟的值。 hello 下列範例命令輸出顯示 hello 現有的虛擬磁碟連接到 LUN 0:

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    卸離 hello 資料磁碟，從您的 VM 使用 hello 適用`Lun`值：

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a>從原始硬碟建立 VM
toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)。 hello 實際的 JSON 範本位於 hello 下列連結：

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json

hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。 hello 下列範例會將部署 hello 範本 toohello 資源群組名稱`myResourceGroup`:

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

回應 hello 提示 hello 範本，例如 VM 名稱 (`myDeployedVM` hello 下列範例)，OS 類型 (`Linux`)，與 VM 大小 (`Standard_DS1_v2`)。 hello `osDiskVhdUri` hello 如先前附加時會使用 hello 疑難排解 VM 現有虛擬硬碟 toohello 相同。 Hello 命令的輸出，並提示使用者的範例如下所示：

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a>重新啟用開機診斷

當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。 hello 下列範例會啟用 hello hello 名為 VM 上的診斷延伸模組`myDeployedVM`hello 資源群組中名為`myResourceGroup`:

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，請參閱[疑難排解 SSH 連線 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Linux VM 上的應用程式連線問題進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
