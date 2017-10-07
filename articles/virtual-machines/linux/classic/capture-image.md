---
title: "aaaCapture Linux VM 的映像 |Microsoft 文件"
description: "了解如何 toocapture Linux 型 Azure 虛擬機器 (VM) 的映像建立 hello 傳統部署模型。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>如何 toocapture 傳統 Linux 虛擬機器做為映像
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

本文章將示範如何 toocapture 傳統 Azure 虛擬機器 (VM) 執行 Linux 映像 toocreate 為其他虛擬機器。 此映像包含 hello OS 磁碟和資料磁碟附加 toohello VM。 它不包含網路設定，因此您需要 tooconfigure，當您建立 hello 其他 VM 從 hello 映像。

Azure 的存放區 hello 下方影像**映像**，以及任何您已上傳的映像。 如需映像的詳細資訊，請參閱[關於 Azure 中的虛擬機器映像][About Virtual Machine Images in Azure]。

## <a name="before-you-begin"></a>開始之前
這些步驟假設，您已經建立 Azure VM 使用 hello 傳統部署模型和設定的 hello 作業系統，包括附加的任何資料磁碟。 如果您需要 toocreate VM，請閱讀[如何 tooCreate Linux 虛擬機器][How tooCreate a Linux Virtual Machine]。

## <a name="capture-hello-virtual-machine"></a>擷取 hello 虛擬機器
1. [連接 toohello VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)使用您選擇的 SSH 用戶端。
2. 在 hello SSH 視窗中，輸入下列命令的 hello。 從輸出 hello`waagent`根據 hello 版本，此公用程式可能會稍微不同：

    ```bash
    sudo waagent -deprovision+user
    ```

    hello 前述的命令嘗試 tooclean hello 系統，也適合用來重新佈建。 這項作業會執行下列工作的 hello:

   * 移除 SSH 主機金鑰 （如果 Provisioning.RegenerateSshHostKeyPair 'y' hello 組態檔中）
   * 清除 /etc/resolv.conf 中的名稱伺服器設定
   * 移除 hello`root`使用者密碼從 /etc/hosts 陰影 （如果 Provisioning.DeleteRootPassword 'y' hello 組態檔中）
   * 移除快取的 DHCP 用戶端租用
   * 重設主機名稱 toolocalhost.localdomain
   * 刪除 hello （取自 /var/lib/waagent） 最後一個佈建的使用者帳戶**和相關聯資料**。

     > [!NOTE]
     > 取消佈建會刪除檔案和資料太""hello 映像一般化。 只執行您想要為新的映像範本 toocapture 此命令在 VM 上。 它並不保證該 hello 映像會清除所有的機密資訊或適用於轉散發 toothird 合作對象。

3. 型別**y** toocontinue。 您可以新增 hello`-force`參數 tooavoid 此確認步驟。
4. 型別**結束**tooclose hello SSH 用戶端。

   > [!NOTE]
   > hello 其餘步驟假設您已經有[安裝 hello Azure CLI](../../../cli-install-nodejs.md)用戶端電腦上。 所有步驟的 hello 還可以在 hello [Azure 入口網站](http://portal.azure.com)。

5. 從用戶端電腦，開啟 Azure CLI 和登入 tooyour Azure 訂用帳戶。 如需詳細資訊，請參閱[tooan Azure 訂用帳戶連線從 hello Azure CLI](../../../xplat-cli-connect.md)。

   > [!NOTE]
   > 在 hello Azure 入口網站，登入 toohello 入口網站。

6. 請確定您是處於服務管理模式中：

    ```azurecli
    azure config mode asm
    ```

7. 關閉 hello 已解除佈建的 VM。 hello 下例關閉 hello 名為 VM `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   如有需要您可以檢視所有 hello Vm 都建立您的訂用帳戶中使用的清單`azure vm list`

   > [!NOTE]
   > 如果您使用 hello Azure 入口網站，選取 hello VM，然後按一下**停止**關閉 hello VM。

8. Hello VM 停止時，擷取 hello 映像。 下列範例會擷取 hello hello 名為 VM`myVM`並建立名為一般化映像`myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    hello`-t`刪除 hello 原始虛擬機器的子命令。

    > [!NOTE]
    > 在 hello Azure 入口網站，您可以藉由選取擷取映像**映像**從 hello 中樞功能表中。 您需要下列資訊 hello 映像的 toosupply hello： 名稱、 資源群組、 位置、 作業系統類型和儲存體 blob 的路徑。

9. 現在在 hello 清單中的映像可能是使用 tooconfigure 任何新的 VM，就會是 hello 新映像。 您可以檢視它與 hello 命令：

   ```azurecli
   azure vm image list
   ```

   在 hello [Azure 入口網站](http://portal.azure.com)，hello 新映像會出現在 hello **VM 映像 （傳統）**的所屬 toohello**計算**服務。 您可以存取**VM 映像 （傳統）**按一下_更多服務_底部 hello hello Azure 服務 清單中，並再查看 hello**計算**服務。   

   ![成功擷取映像](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>後續步驟
hello 映像已準備好用的 toobe toocreate Vm。 您可以使用 hello Azure CLI 命令`azure vm create`和您所建立的供應 hello 映像名稱。 如需詳細資訊，請參閱[與傳統部署模型使用 hello Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。

或者，使用 hello [Azure 入口網站](http://portal.azure.com)toocreate 自訂 VM 使用 hello**映像**方法，然後選取 hello 映像所建立。 如需詳細資訊，請參閱[如何 tooCreate 自訂 VM][How tooCreate a Custom Virtual Machine]。

**另請參閱：** [Azure Linux 代理程式使用者指南](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
