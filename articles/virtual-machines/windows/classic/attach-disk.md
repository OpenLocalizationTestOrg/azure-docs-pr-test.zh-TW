---
title: "aaaAttach 磁碟 tooa 傳統 Azure VM |Microsoft 文件"
description: "連接資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型，然後將它初始化。"
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>附加資料磁碟 tooa 建立 Windows 虛擬機器與 hello 傳統部署模型
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

本文章將示範如何 tooattach 新的和現有磁碟建立 hello 傳統部署模型 tooa Windows 虛擬機器使用 hello Azure 入口網站。

您也可以[附加 hello Azure 入口網站中的資料磁碟 tooa Linux VM](../../linux/attach-disk-portal.md)。

連接磁碟之前，請檢閱下列提示︰

* hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。 如需詳細資訊，請參閱 [虛擬機器的大小](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

* toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。 您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。 僅特定地區可用進階儲存體。 如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

* 對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。

您也可以[使用 Powershell 連接資料磁碟](../../virtual-machines-windows-attach-disk-ps.md)。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。

## <a name="find-hello-virtual-machine"></a>尋找 hello 虛擬機器
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取 hello hello 儀表板上所列的 hello 資源從虛擬機器。
3. Hello 下的左窗格中**設定**，按一下 **磁碟**。

    ![開啟磁碟設定](./media/attach-disk/virtualmachinedisks.png)

接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。

## <a name="option-1-attach-and-initialize-a-new-disk"></a>選項 1：連接新磁碟並進行初始化

1. 在 hello**磁碟**刀鋒視窗中，按一下 **附加新**。
2. 檢閱 hello 預設設定，如有必要，更新，然後按一下**確定**。

   ![檢閱磁碟設定](./media/attach-disk/attach-new.png)

3. Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。

### <a name="initialize-a-new-data-disk"></a>初始化新的資料磁碟

1. Toohello 虛擬機器連線。 如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
2. 您登入 toohello 虛擬機器之後，請開啟**伺服器管理員**。 Hello 左窗格中，選取**檔案和存放服務**。

    ![開啟伺服器管理員](../media/attach-disk-portal/fileandstorageservices.png)

3. 選取 [磁碟]。
4. hello**磁碟**區段會列出 hello 磁碟。 多數情況下，虛擬機器會有磁碟 0、磁碟 1 和磁碟 2。 磁碟 0 是 hello 作業系統磁碟、 磁碟 1 是 hello 暫存磁碟，以及磁碟 2 是新 hello 資料磁碟連接的 toohello 虛擬機器。 hello 資料磁碟清單 hello 與磁碟分割**未知**。

 Hello 磁碟上按一下滑鼠右鍵，然後選取**初始化**。

5. 您收到 hello 磁碟初始化時，將被清除所有資料。 按一下**是**tooacknowledge hello 警告和初始化 hello 磁碟。 Hello partition 完成後，會被列為**GPT**。 Hello 磁碟上按一下滑鼠右鍵，然後選取**新的磁碟區**。

6. 完成 hello 精靈使用 hello 預設值。 當 hello 精靈完成時，hello**磁碟區**區段會列出 hello 新磁碟區。 hello 磁碟現在已上線並備妥 toostore 資料。

    ![成功初始化磁碟區](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a>選項 2：連接現有磁碟
1. 在 hello**磁碟**刀鋒視窗中，按一下 **附加現有**。
2. 在 [連接現有磁碟] 底下，按一下 [位置]。

   ![連接現有磁碟](./media/attach-disk/attachexistingdisksettings.png)
3. 在下**儲存體帳戶**，選取 hello 帳戶和容器，其中含有 hello.vhd 檔案。

   ![尋找 VHD 位置](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. 選取 hello.vhd 檔案。
5. 在下**將現有磁碟**，您只選取的 hello 檔案列在**VHD 檔案**。 按一下 [確定] 。
6. Azure 將 hello 磁碟 toohello 虛擬機器之後，它會列在下方的 hello 虛擬機器的磁碟設定**資料磁碟**。

## <a name="use-trim-with-standard-storage"></a>搭配使用 TRIM 與標準儲存體

如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。 空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。 使用 TRIM 可以節省成本，包括刪除大型檔案時所產生的未使用區塊。

您可以執行此命令 toocheck hello 修剪設定。 在您的 Windows VM 上開啟命令提示字元並輸入︰

```
fsutil behavior query DisableDeleteNotify
```

Hello 命令傳回 0，如果已正確啟用修剪。 如果它傳回 1，執行下列命令 tooenable TRIM hello:
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a>後續步驟
如果您的應用程式需要 toouse hello d： 磁碟機 toostore 資料時，您可以[變更 hello hello Windows 暫存磁碟的磁碟機代號](../../virtual-machines-windows-change-drive-letter.md)。

## <a name="additional-resources"></a>其他資源
[有關虛擬機器的磁碟和 VHD](../../virtual-machines-linux-about-disks-vhds.md)
