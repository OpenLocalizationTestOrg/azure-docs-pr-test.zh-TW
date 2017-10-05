---
title: "啟用或停用 Azure VM 監視"
description: "說明如何啟用或停用 Azure VM 監視"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>啟用或停用 Azure VM 監視

本節說明如何在 Azure 上執行的虛擬機器上啟用或停用監視。 您可以使用入口網站或適用於 Mac、Linux 和 Windows (Azure CLI) 的 Azure 命令列介面啟用或停用監視。

> [!IMPORTANT]
> 本文件說明的 Linux 診斷延伸模組 2.3 版已被取代。 至 2018 年 6 月 30 日止就不再支援 2.3 版。
>
> 屆時可以啟用 3.0 版的 Linux 診斷延伸模組。 如需詳細資訊，請參閱[文件](./diagnostic-extension.md)。

## <a name="enable--disable-monitoring-through-the-azure-portal"></a>透過 Azure 入口網站啟用/停用監視

您可以啟用 Azure VM 的監視，在 1 分鐘的期間提供您的執行個體相關資料。 (儲存體變更適用)。 接著，詳細的診斷資料可用於入口網站圖形中的 VM，或透過 API 取得。 根據預設，Azure 入口網站可針對一組有限的計量進行主機監視。 您可以在 VM 正在執行或處於停止狀態時，從 VM 內啟用計量監視。

* 開啟 Azure 入口網站，位址是 [https://portal.azure.com](https://portal.azure.com)。
* 在左側導覽中，按一下 [虛擬機器]。
* 在 [虛擬機器] 清單中，選取執行中或已停止的執行個體。 [虛擬機器] 刀鋒視窗隨即開啟。
* 按一下 [所有設定]。
* 按一下 [診斷]。
* 將狀態變更為 [開啟] 或 [關閉]。 您也可以在此刀鋒視窗中挑選您要為虛擬機器啟用的監視層級詳細資料。

![透過 Azure 入口網站啟用/停用監視。][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>使用 Azure CLI 啟用/停用監視

啟用 Azure VM 的監視。

* 建立檔案，並命名為 PrivateConfig.json：

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* 透過 Azure CLI 啟用延伸模組。

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

如需詳細資訊，請參閱[使用 Linux 診斷延伸模組監視 Linux VM 的效能和診斷資料](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
