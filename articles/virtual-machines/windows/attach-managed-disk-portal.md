---
title: "受管理的資料磁碟 tooa Windows VM-Azure aaaAttach |Microsoft 文件"
description: "如何 tooattach 新受管理的資料磁碟 tooa hello Azure 入口網站中，使用中的 Windows VM hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach 受管理的資料磁碟 tooa Windows VM hello Azure 入口網站中的方式

本文章將示範如何 tooattach 新的 managed 資料磁碟 tooWindows 透過 hello Azure 入口網站的虛擬機器。 這麼做之前，請先檢閱下列提示：

* hello hello 虛擬機器大小會控制您可以將附加的資料磁碟數目。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。
* 對於新的磁碟，您不需要 toocreate 它第一次因為 Azure 會建立它時將它附加。

您也可以[使用 Powershell 連接資料磁碟](attach-disk-ps.md)。



## <a name="add-a-data-disk"></a>新增資料磁碟
1. 在左側 hello hello 功能表上，按一下**虛擬機器**。
2. 從 [hello] 清單中選取 hello 虛擬機器。
3. 在 hello 虛擬機器刀鋒視窗中，按一下 **磁碟**。
   4. 在 hello**磁碟**刀鋒視窗中，按一下  **+ 新增資料磁碟**。
5. 在 hello hello 新磁碟的下拉式清單中，選取 **建立空白**。
6. 在 hello**建立受管理的磁碟**刀鋒視窗中，輸入 hello 磁碟的名稱，然後調整視 hello 其他設定。 完成之後，請按一下 [建立]。
7. 在 hello**磁碟**刀鋒視窗中，按一下 儲存 toosave hello 新磁碟設定的 hello VM。
6. Azure 會建立 hello 磁碟，並將其附加 toohello 虛擬機器之後下, hello 虛擬機器的磁碟設定 中列為 hello 新磁碟**資料磁碟**。


## <a name="initialize-a-new-data-disk"></a>初始化新的資料磁碟

1. 連接 toohello VM。
1. 按一下 hello VM 內 hello 開始 功能表及類型**diskmgmt.msc**並點擊**Enter**。 這會啟動 hello 磁碟管理嵌入式管理單元。
2. 磁碟管理會辨識您有新的、 未初始化的磁碟，並 hello 初始化磁碟 視窗會隨即快顯。
3. 請確定已選取 hello 新磁碟，然後按一下**確定**tooinitialize 它。
4. hello 新磁碟現在會顯示為**未配置**。 Hello 磁碟上按一下滑鼠右鍵，然後選取**新增簡單磁碟區**。 hello**新增簡單磁碟區精靈**會啟動。
5. 透過 hello 」 精靈，將所有 hello 預設值，當您完成選取移**完成**。
6. 關閉磁碟管理。
7. 您將會得到快顯視窗，您可以使用它之前，需要 tooformat hello 新磁碟。 按一下 [格式化磁碟]。
8. 在 hello**格式新磁碟**對話方塊檢查 hello 設定，然後按一下**啟動**。
9. 您會收到警告，格式化 hello 磁碟將會清除所有 hello 資料中，按一下 **確定**。
10. 完成 hello 格式時，按一下**確定**。

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
