---
title: "aaaAbout 磁碟和 Microsoft Azure Windows Vm 的 Vhd |Microsoft 文件"
description: "深入了解磁碟和 Vhd 適用於 Windows Azure 虛擬機器中的 hello 基本概念。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 0142c64d-5e8c-4d62-aa6f-06d6261f485a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 859e564dc74240bd7c70fec33255b8d071c4acf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-windows-vms"></a>關於 Azure Windows VM 的磁碟和 VHD
就像任何其他電腦一樣在 Azure 虛擬機器會使用磁碟進行 toostore 作業系統、 應用程式和資料。 所有 Azure 虛擬機器都至少有兩個磁碟 - 一個 Windows 作業系統磁碟和一個暫存磁碟。 從映像，建立 hello 作業系統磁碟，而 hello 作業系統磁碟和 hello 映像的虛擬硬碟 (Vhd) 儲存在 Azure 儲存體帳戶。 虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。 

在本文中，即將討論 hello 不同用法 hello 磁碟，及再討論 hello 不同類型的磁碟，您可以建立及使用。 本文也適用於 [Linux 虛擬機器](storage-about-disks-and-vhds-linux.md)。

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>VM 使用的磁碟

讓我們看看如何使用 hello Vm hello 磁碟。

### <a name="operating-system-disk"></a>作業系統磁碟
每個虛擬機器都有一個連接的作業系統磁碟。 它已註冊為 SATA 磁碟機，並標示為預設的 hello c： 磁碟機。 此磁碟的最大容量為 2048 GB。 

### <a name="temporary-disk"></a>暫存磁碟
每個 VM 都包含一個暫存磁碟。 hello 暫存磁碟的應用程式和處理序提供短期儲存，預期的 tooonly 存放區資料，例如分頁檔。 Hello 暫存磁碟上的資料可能會遺失期間[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)或當您[重新部署 VM](../virtual-machines/windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 Hello VM 標準重開機，應保存 hello hello 暫存磁碟機上的資料。

hello 暫存磁碟標示為 hello d： 磁碟機上，依預設，它用來儲存 pagefile.sys。 tooremap 這個磁碟 tooa 不同磁碟機代號，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](../virtual-machines/windows/change-drive-letter.md)。 hello hello 暫存磁碟的大小會根據 hello hello 虛擬機器大小而不同。 如需詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。

如需有關 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)


### <a name="data-disk"></a>資料磁碟
資料磁碟是附加的 tooa 虛擬機器 toostore 應用程式資料，或需要 tookeep 其他資料的 VHD。 資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。 每個資料磁碟具有 4095 GB 的最大容量。 hello hello 虛擬機器的大小會決定您可以將附加的儲存體，您可以使用 tooit 與 hello 類型的資料磁碟數目 toohost hello 磁碟。

> [!NOTE]
> 如需有關虛擬機器容量的詳細資訊，請參閱 [Windows 虛擬機器的大小](../virtual-machines/windows/sizes.md)。
> 

當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。 如果您使用包含資料磁碟的映像時，Azure 也會建立 hello 資料磁碟時，它會建立 hello 虛擬機器。 否則，您建立 hello 虛擬機器之後加入資料磁碟。

您可以新增任何時候，資料磁碟 tooa 虛擬機器由**附加**hello 磁碟 toohello 虛擬機器。 您可以使用您已上傳或複製 tooyour 儲存體帳戶，或其中一個，Azure 會為您建立的 VHD。 連接資料磁碟 hello VHD 檔案將與關聯 hello VM 「 租用 」 置於 hello VHD，因此無法加以刪除仍附加時從儲存體。


[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="one-last-recommendation-use-trim-with-unmanaged-standard-disks"></a>最後一個建議：對非受控標準磁碟使用 TRIM 

如果您使用非受控標準儲存體 (HDD)，您應該啟用 TRIM。 空白位置修剪會捨棄 hello 磁碟上未使用的區塊，因此您只支付您實際使用的儲存體。 如果您建立大型檔案，然後將它們刪除，這便可節省成本。 

您可以執行此命令 toocheck hello 修剪設定。 在您的 Windows VM 上開啟命令提示字元並輸入︰


```
fsutil behavior query DisableDeleteNotify
```

Hello 命令傳回 0，如果已正確啟用修剪。 如果它傳回 1，執行下列命令 tooenable TRIM hello:

```
fsutil behavior set DisableDeleteNotify 0
```

> [!NOTE]
> 注意： 修剪支援啟動與 Windows Server 2012 / Windows 8 （含） 以上版本，請參閱請參閱[新 API 可讓應用程式 toosend"修剪和取消對應 」 提示 toostorage 媒體](https://msdn.microsoft.com/windows/compatibility/new-api-allows-apps-to-send-trim-and-unmap-hints)。
> 

<!-- Might want toomatch next-steps from overview of managed disks -->
## <a name="next-steps"></a>後續步驟
* [將磁碟連接](../virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)vm tooadd 額外的存放裝置。
* [變更 hello 磁碟機代號 hello Windows 暫存磁碟](../virtual-machines/windows/change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)讓您的應用程式的資料可以使用 hello d： 磁碟機。

