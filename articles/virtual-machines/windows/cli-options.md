---
title: "aaaUsing hello Windows 上的 Azure CLI |Microsoft 文件"
description: "使用 Windows hello Azure CLI"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>使用 Windows hello Azure CLI

hello Azure 命令列介面 (CLI) 會提供命令列和指令碼環境來建立和管理 Azure 資源。 hello Azure CLI 可用 macOS、 Linux 及 Windows 作業系統。 在這些作業系統，hello CLI 命令是相同的但是可以在不同作業系統特定的指令碼語法。

Hello Azure CLI 此文件詳細資料 hello 方法可以安裝和執行 Windows 和詳細資料每個語法的考量。 如需深入的 Azure CLI 文件，請參閱 [Azure CLI 文件]( https://docs.microsoft.com/en-us/cli/azure/overview) (英文)。

## <a name="windows-subsystem-for-linux"></a>適用於 Linux 的 Windows 子系統

hello Windows 子系統 Linux (WSL) 提供 Windows 10 年度和更新版本上的 Ubuntu Linux 環境。 啟用時，WSL 會提供原生 Bash 體驗，以供用來建立和執行 Azure CLI 指令碼。 因為 WSL 會提供原生 Bash 體驗，Azure CLI 指令碼可以在 Mac OS、Linux 和 Windows 之間共用而不需要修改。

toouse hello Azure CLI 中 WSL，完成下列 hello。

|Task | 範例的指示 |
|---|---|
| 啟用 WSL | [安裝 WSL 文件](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| 安裝 hello Azure CLI |[WSL/Ubuntu 14.04 上安裝 hello CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

hello Azure CLI 可以在 Windows 中的原生方式執行。 在此組態中，hello Windows 作業系統上安裝 hello Azure CLI 封裝，可以從 PowerShell 執行命令。 在此組態中，Azure CLI 命令和指令碼可以執行於任何受支援的 Windows 版本，但必須使用平台特定的指令碼語法。 因此，指令碼不一定能在 Mac OS、Linux 和 Windows 之間共用而不需要修改。

toouse hello Azure CLI 在 Windows 中，安裝使用這些指示，hello 封裝[安裝 hello Windows 上的 CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows)。

## <a name="docker-image"></a>Docker 映像

當使用 Docker for Windows，Docker 映像可以啟動包含 hello Azure CLI。 此映像是以 Linux 為基礎，並包含原生 Bash 體驗。  當使用 Docker for Windows 和 hello Azure CLI 映像、 指令碼 toobe macOS、 Linux 及 Windows 之間共用。 

Docker for Windows 正在執行，並執行下列命令的 hello，請確定 toouse hello Azure CLI Docker for Windows 上。

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

一旦完成，也就是啟動工作階段，將 Bash 預先載入 hello Azure CLI 工具。

## <a name="next-steps"></a>後續步驟

[Azure 虛擬機器的 CLI 範例](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure Web Apps 的 CLI 範例](../../app-service-web/app-service-cli-samples.md)

[Azure SQL 的 CLI 範例](../../sql-database/sql-database-cli-samples.md)
