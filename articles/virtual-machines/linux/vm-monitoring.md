---
title: "aaaEnable 或停用 Azure VM 監視"
description: "描述如何 tooEnable] 或 [停用 Azure VM 監視"
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>啟用或停用 Azure VM 監視

本章節描述如何 tooenable 或停用監視上虛擬機器在 Azure 上執行。 您可以啟用或停用監視使用 hello 入口網站或 Azure 命令列介面的 Mac、 Linux 及 Windows (hello Azure CLI)。

> [!IMPORTANT]
> 本文件說明 2.3 版 hello Linux 診斷延伸，其中已被取代。 至 2018 年 6 月 30 日止就不再支援 2.3 版。
>
> 3.0 版的 hello Linux 診斷延伸模組可以改為啟用。 如需詳細資訊，請參閱[hello 文件](./diagnostic-extension.md)。

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>啟用/停用監視 hello 透過 Azure 入口網站

您可以啟用 Azure VM 的監視，在 1 分鐘的期間提供您的執行個體相關資料。 (儲存體變更適用)。 然後使用 hello VM hello 入口網站圖表或透過 hello API 詳細的診斷資料。 根據預設，Azure 入口網站可針對一組有限的計量進行主機監視。 您可以啟用來自 hello 執行 VM 時或在已停止狀態，在 VM 內的度量的監視。

* 開啟 hello Azure 入口網站在[https://portal.azure.com](https://portal.azure.com)。
* 在左瀏覽 hello，按一下 虛擬機器。
* 在 hello 列出虛擬機器，選取 執行中或已停止的執行個體。 hello 「 虛擬機器 」 刀鋒視窗隨即開啟。
* 按一下 [所有設定]。
* 按一下 [診斷]。
* 變更狀態 tooOn 或設為 Off。 您也可以挑選此刀鋒視窗 hello 層級監視您想要 tooenable 虛擬機器的詳細資料中。

![啟用/停用透過 hello Azure 入口網站的監視。][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>使用 Azure CLI 啟用/停用監視

tooenable 監視的 Azure VM。

* 建立檔案，並命名為 PrivateConfig.json：

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* 啟用透過 Azure CLI hello 延伸模組。

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

如需詳細資訊，請參閱[使用 Linux 診斷延伸模組 tooMonitor Linux VM 的效能和診斷資料](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)。

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
