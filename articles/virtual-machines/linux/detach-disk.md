---
title: "從 Linux VM-Azure 資料磁碟 aaaDetach |Microsoft 文件"
description: "了解 toodetach 從虛擬機器使用 CLI 2.0 或 hello Azure 入口網站在 Azure 中的資料磁碟。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a>Toodetach 資料從 Linux 虛擬機器的磁碟

當您不再需要的資料磁碟附加的 tooa 虛擬機器時，您可以輕易地中斷。 這會從 hello 虛擬機器，移除 hello 磁碟，但並不會移除從儲存體。 

> [!WARNING]
> 將磁碟中斷連結時，並不會自動將它刪除。 如果您已訂閱 tooPremium 儲存體，您將繼續 tooincur hello 磁碟的儲存體費用。 如需詳細資訊，請參閱太[定價和計費時使用進階儲存體](../../storage/common/storage-premium-storage.md#pricing-and-billing)。 
> 
> 

若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的虛擬機器或另一個。  

## <a name="detach-a-data-disk-using-cli-20"></a>使用 CLI 2.0 中斷資料磁碟連結

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。


## <a name="detach-a-data-disk-using-hello-portal"></a>卸離資料磁碟使用 hello 入口網站
1. 在 hello 入口網站的中樞，選取 **虛擬機器**。
2. 選取 hello hello toodetach 然後按一下資料磁碟的虛擬機器**停止**toodeallocate hello VM。
3. 在 hello 虛擬機器刀鋒視窗中，選取 **磁碟**。
4. 頂端的 hello hello**磁碟**刀鋒視窗中，選取**編輯**。
5. 在 [hello**磁碟**刀鋒視窗中，最右邊的 hello 資料磁碟，您想 toodetach，toohello 按一下 hello![卸離按鈕影像](./media/detach-disk/detach.png)卸離] 按鈕。
5. Hello 磁碟已被移除後，按一下 [儲存] hello hello 刀鋒視窗的頂端。
6. 在 hello 虛擬機器刀鋒視窗中，按一下 **概觀**然後按一下hello**啟動**在 hello 刀鋒視窗 toorestart hello VM hello 最上方的按鈕。

hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。








## <a name="next-steps"></a>後續步驟
如果您想 tooreuse hello 資料磁碟時，您可以直接[將它附加 tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

