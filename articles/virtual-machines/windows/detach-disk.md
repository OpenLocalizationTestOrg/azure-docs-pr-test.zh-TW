---
title: "從 Windows VM-Azure 資料磁碟 aaaDetach |Microsoft 文件"
description: "了解 toodetach 從虛擬機器使用 hello Resource Manager 部署模型在 Azure 中的資料磁碟。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 13180343-ac49-4a3a-85d8-0ead95e2028c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: f3f581d3f33329db2ecb7d25a68bc59af7361aad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-windows-virtual-machine"></a>Toodetach 資料從 Windows 虛擬機器的磁碟
當您不再需要的資料磁碟附加的 tooa 虛擬機器時，您可以輕易地中斷。 這會從 hello 虛擬機器，移除 hello 磁碟，但並不會移除從儲存體。

> [!WARNING]
> 將磁碟中斷連結時，並不會自動將它刪除。 如果您已訂閱 tooPremium 儲存體，您將繼續 tooincur hello 磁碟的儲存體費用。 如需詳細資訊，請參閱太[定價和計費時使用進階儲存體](../../storage/common/storage-premium-storage.md#pricing-and-billing)。
>
>

若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的虛擬機器或另一個。

## <a name="detach-a-data-disk-using-hello-portal"></a>卸離資料磁碟使用 hello 入口網站
1. 在 hello 入口網站的中樞，選取 **虛擬機器**。
2. 選取 hello hello toodetach 然後按一下資料磁碟的虛擬機器**停止**toodeallocate hello VM。
3. 在 hello 虛擬機器刀鋒視窗中，選取 **磁碟**。
4. 頂端的 hello hello**磁碟**刀鋒視窗中，選取**編輯**。
5. 在 [hello**磁碟**刀鋒視窗中，最右邊的 hello 資料磁碟，您想 toodetach，toohello 按一下 hello![卸離按鈕影像](./media/detach-disk/detach.png)卸離] 按鈕。
5. Hello 磁碟已被移除後，按一下 [儲存] hello hello 刀鋒視窗的頂端。
6. 在 hello 虛擬機器刀鋒視窗中，按一下 **概觀**然後按一下hello**啟動**在 hello 刀鋒視窗 toorestart hello VM hello 最上方的按鈕。



hello 磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。

## <a name="detach-a-data-disk-using-powershell"></a>使用 PowerShell 來中斷資料磁碟連結
在此範例中，hello 取得 hello 名為虛擬機器的第一個命令**MyVM07**在 hello **RG11**使用 hello Get AzureRmVM cmdlet 的資源群組。 hello 存放區 hello hello 中的虛擬機器的命令**$VirtualMachine**變數。

hello 第二個命令會移除名為 DataDisk3 hello 虛擬機器中移除的 hello 資料磁碟。

hello 最後一個命令會更新 hello hello 虛擬機器 toocomplete hello 程序移除 hello 資料磁碟的狀態。

```powershell
$VirtualMachine = Get-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07"
Remove-AzureRmVMDataDisk -VM $VirtualMachine -Name "DataDisk3"
Update-AzureRmVM -ResourceGroupName "RG11" -Name "MyVM07" -VM $VirtualMachine
```

如需詳細資訊，請參閱 [Remove-AzureRmVMDataDisk](/powershell/module/azurerm.compute/remove-azurermvmdatadisk)。

## <a name="next-steps"></a>後續步驟
如果您想 tooreuse hello 資料磁碟時，您可以直接[將它附加 tooanother VM](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

