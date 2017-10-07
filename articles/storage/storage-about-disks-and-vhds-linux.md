---
title: "aaaAbout 磁碟和 Microsoft Azure Linux Vm 的 Vhd |Microsoft 文件"
description: "深入了解 hello Azure 中 Linux 虛擬機器磁碟和 Vhd 的基本概念。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7be8dd52-98f7-4187-9b78-55197915bc9b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 1155d773136677553d263c17fbf8b224035d96bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-disks-and-vhds-for-azure-linux-vms"></a>關於 Azure Linux VM 的磁碟和 VHD
就像任何其他電腦一樣在 Azure 虛擬機器會使用磁碟進行 toostore 作業系統、 應用程式和資料。 所有 Azure 虛擬機器都至少有兩個磁碟 – Linux 作業系統磁碟和暫存磁碟。 從映像，建立 hello 作業系統磁碟和 hello 作業系統磁碟和 hello 映像會實際虛擬硬碟 (Vhd) 儲存在 Azure 儲存體帳戶。 虛擬機器也可以有一或多個資料磁碟，而這些磁碟也會儲存成 VHD。 

在本文中，即將討論 hello 不同用法 hello 磁碟，及再討論 hello 不同類型的磁碟，您可以建立及使用。 本文也適用於 [Windows 虛擬機器](storage-about-disks-and-vhds-windows.md)。

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="disks-used-by-vms"></a>VM 使用的磁碟

讓我們看看如何使用 hello Vm hello 磁碟。

## <a name="operating-system-disk"></a>作業系統磁碟
每個虛擬機器都有一個連接的作業系統磁碟。 它會註冊為 SATA 磁碟機，並預設標示為 /dev/sda。 此磁碟具有 2048 GB 的最大容量。 

## <a name="temporary-disk"></a>暫存磁碟
每個 VM 都包含一個暫存磁碟。 hello 暫存磁碟的應用程式和處理序提供短期儲存，預期的 tooonly 存放區資料，例如分頁檔。 Hello 暫存磁碟上的資料可能會遺失期間[維護事件](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime)或當您[重新部署 VM](../virtual-machines/linux/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。 Hello VM 標準重開機，應保存 hello hello 暫存磁碟機上的資料。

Linux 的虛擬機器上 hello 磁碟通常是**/開發/sdb** is 格式化及裝載太**/mnt**由 hello Azure Linux 代理程式。 hello hello 暫存磁碟的大小會根據 hello hello 虛擬機器大小而不同。 如需詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。

如需有關 Azure 的 hello 暫存磁碟的使用方式的詳細資訊，請參閱[了解 hello 暫存磁碟機上的 Microsoft Azure 虛擬機器](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>資料磁碟
資料磁碟是附加的 tooa 虛擬機器 toostore 應用程式資料，或需要 tookeep 其他資料的 VHD。 資料磁碟註冊為 SCSI 磁碟機，並以您選擇的字母標示。 每個資料磁碟具有 4095 GB 的最大容量。 hello hello 虛擬機器的大小會決定您可以將附加的儲存體，您可以使用 tooit 與 hello 類型的資料磁碟數目 toohost hello 磁碟。

> [!NOTE]
> 如需有關虛擬機器容量的詳細資訊，請參閱 [Linux 虛擬機器的大小](../virtual-machines/linux/sizes.md)。
> 

當您從映像建立虛擬機器時，Azure 會建立作業系統磁碟。 如果您使用包含資料磁碟的映像時，Azure 也會建立 hello 資料磁碟時，它會建立 hello 虛擬機器。 否則，您建立 hello 虛擬機器之後加入資料磁碟。

您可以新增任何時候，資料磁碟 tooa 虛擬機器由**附加**hello 磁碟 toohello 虛擬機器。 您可以使用您已上傳或複製 tooyour 儲存體帳戶，或其中一個，Azure 會為您建立的 VHD。 連接資料磁碟 hello VHD 檔案將與關聯 hello VM，將 「 租用 」 放置在 hello VHD，因此無法加以刪除仍附加時從儲存體。

[!INCLUDE [storage-about-vhds-and-disks-windows-and-linux](../../includes/storage-about-vhds-and-disks-windows-and-linux.md)]

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [virtual-machines-linux-lunzero](../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>後續步驟
* [將磁碟連接](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)vm tooadd 額外的存放裝置。
* [設定軟體 RAID](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 以提供備援。
* [擷取 Linux 虛擬機器](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)以便快速部署額外的 VM。

