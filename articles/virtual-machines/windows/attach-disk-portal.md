---
title: "未受管理的資料磁碟 tooa Windows VM-Azure aaaAttach |Microsoft 文件"
description: "如何 tooattach 新的或現有的 unmanaged 的資料磁碟 tooa Windows VM 在 Azure 入口網站中，使用 hello hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach 未受管理的資料磁碟 tooa Windows VM hello Azure 入口網站中的方式

本文將說明 tooattach 新的和現有的受管理磁碟 tooWindows 透過 hello Azure 入口網站的虛擬機器。 您也可以[使用 PowerShell 連結資料磁碟](./attach-disk-ps.md)。 這麼做之前，請先檢閱下列提示：

* hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。
* toouse 高階儲存體，您需要將 DS 系列或 GS 系列虛擬機器。 您可以使用進階或標準儲存體帳戶的磁碟搭配這些虛擬機器。 僅特定地區可用進階儲存體。 如需詳細資訊，請參閱[進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
* 對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。


您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。


## <a name="find-hello-virtual-machine"></a>尋找 hello 虛擬機器
1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 在左側 hello hello 功能表上，按一下**虛擬機器**。
3. 從 [hello] 清單中選取 hello 虛擬機器。
4. 在 hello 虛擬機器刀鋒視窗中，按一下 **磁碟**。
   
接著，依照指示來連接[新的磁碟](#option-1-attach-a-new-disk)或[現有的磁碟](#option-2-attach-an-existing-disk)。

## <a name="option-1-attach-and-initialize-a-new-disk"></a>選項 1：連接新磁碟並進行初始化
1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 在 hello**附加受管理的磁碟**刀鋒視窗中，輸入的名稱中的 hello 磁碟**名稱**，然後選取  **（空的磁碟） 新增**中**來源類型**。
3. 在下**儲存體容器**，按一下 hello**瀏覽**按鈕，然後瀏覽 toohello 儲存體帳戶和容器，您會在其中喜歡 hello 儲存新 VHD toobe，然後按一下**選取**. 
  
   ![檢閱磁碟設定](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. 當您完成 hello hello 資料磁碟的設定之後時，按一下**確定**。
4. 在 hello**磁碟**刀鋒視窗中，按一下 **儲存**tooadd hello 磁碟 toohello VM 組態。


### <a name="initialize-a-new-data-disk"></a>初始化新的資料磁碟

1. Toohello 虛擬機器連線。 如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
1. 按一下 hello**啟動**hello VM 和型別內的功能表**diskmgmt.msc**並點擊**Enter**。 這樣會啟動 hello 磁碟管理嵌入式管理單元。
2. 磁碟管理會辨識您有新的、 未初始化的磁碟 hello 初始化磁碟 視窗會隨即快顯。
3. 請確定已選取 hello 新磁碟，然後按一下**確定**tooinitialize 它。
4. hello 新磁碟隨即顯示當做**未配置**。 Hello 磁碟上按一下滑鼠右鍵，然後選取**新增簡單磁碟區**。 hello**新增簡單磁碟區精靈**啟動。
5. 透過 hello 」 精靈，將所有 hello 預設值，當您完成選取移**完成**。
6. 關閉磁碟管理。
7. 您會得到快顯視窗，您可以使用它之前，需要 tooformat hello 新磁碟。 按一下 [格式化磁碟]。
8. 在 hello**格式新磁碟**對話方塊檢查 hello 設定，然後按一下**啟動**。
9. 您會收到警告，格式化 hello 磁碟會清除所有 hello 資料，請按一下**確定**。
10. 完成 hello 格式時，按一下**確定**。


## <a name="option-2-attach-an-existing-disk"></a>選項 2：連接現有磁碟
1. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
2. 在 hello**連接未受管理的磁碟**刀鋒視窗，請在**來源類型**選取**現有 blob**。

    ![檢閱磁碟設定](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. 按一下**瀏覽**toonavigate toohello 儲存體帳戶和容器 hello 現有 VHD 的位置。 按一下並 hello VHD，然後按一下**選取**。
4. 按一下**確定**在 hello**附加 unmanaged 的磁碟**刀鋒視窗。
5. 在 hello**磁碟**刀鋒視窗中，按一下 **儲存**tooadd hello 磁碟 toohello 組態 hello VM。
   


## <a name="use-trim-with-standard-storage"></a>搭配使用 TRIM 與標準儲存體

如果您使用標準儲存體 (HDD)，您應該啟用 TRIM。 空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。 如果您建立大型檔案，然後將它們刪除，這便可節省成本。 

您可以執行此命令 toocheck hello 修剪設定。 在您的 Windows VM 上開啟命令提示字元並輸入︰

```
fsutil behavior query DisableDeleteNotify
```

Hello 命令傳回 0，如果已正確啟用修剪。 如果它傳回 1，執行下列命令 tooenable TRIM hello:
```
fsutil behavior set DisableDeleteNotify 0
```

從磁碟中刪除資料之後, 您就可以確保 hello 修剪作業排清正確藉由執行磁碟重組與修剪：

```
defrag.exe <volume:> -l
```

您也可以確保修剪 hello 整個磁碟區格式化 hello 磁碟區。


## <a name="next-steps"></a>後續步驟
如果您的應用程式需要 toouse hello d： 磁碟機 toostore 資料時，您可以[變更 hello hello Windows 暫存磁碟的磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

