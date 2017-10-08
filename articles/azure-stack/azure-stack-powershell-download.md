---
title: "從 GitHub 工具 aaaDownload Azure 堆疊 |Microsoft 文件"
description: "了解需要 Azure 堆疊 toowork 如何 toodownload 工具。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a>從 GitHub 下載 Azure Stack 工具

AzureStack 工具是主控的 PowerShell 模組，您可以使用 toomanage 及部署資源 tooAzure 堆疊的 GitHub 儲存機制。 您可以下載並使用這些 PowerShell 模組 toohello Azure 堆疊開發套件或 tooa windows 外部用戶端，如果您計劃 tooestablish VPN 連線能力。 這些工具，tooobtain 複製 hello GitHub 儲存機制或下載 hello AzureStack 工具資料夾。 

tooclone hello 儲存機制上，下載[Git](https://git-scm.com/download/win)適用於 Windows、 開啟 命令提示字元視窗並執行下列指令碼的 hello:

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

toodownload hello 工具資料夾中，執行下列指令碼的 hello:

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a>Hello 模組所提供的功能

hello AzureStack 工具儲存機制包含 PowerShell 模組，支援下列功能的 Azure 堆疊 hello:  

| 功能 | 說明 | 可以使用此模組的人員？ |
| --- | --- | --- |
| [雲端功能](azure-stack-validate-templates.md) | 使用此模組 tooget hello 雲端功能的雲端。 例如，您可以取得 hello 雲端功能，例如應用程式開發介面版本、 Azure 資源管理員資源、 VM 擴充功能等 Azure 堆疊] 和 [使用此模組的 Azure 雲端。 | 雲端系統管理員和使用者。 |
| [Azure Stack 計算系統管理](azure-stack-add-vm-image.md) | 使用此模組 tooadd 或商場 hello Azure 堆疊移除的 VM 映像。 | 雲端系統管理員。 |
| [Azure Stack 基礎結構系統管理](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | 使用此模組 toomanage 堆疊 Azure 基礎結構的 Vm、 警示、 更新等。 |  雲端系統管理員。|
| [適用於 Azure Stack 的 Resource Manager 原則](azure-stack-policy-module.md) | 使用此模組 tooconfigure Azure 訂用帳戶或 Azure 資源群組以 hello 相同 Azure 堆疊的版本控制和服務可用性。 | 雲端系統管理員和使用者 |
| [註冊 Azure](azure-stack-register.md) | 搭配 Azure 使用此模組 tooregister 開發的組件執行個體。 在註冊之後，您可以下載從 Azure 的 hello marketplace 項目，並在 Azure 堆疊中使用它們。 | 雲端系統管理員 |
| [Azure Stack 部署](azure-stack-run-powershell-script.md) | 使用此模組 tooprepare hello Azure 堆疊主機電腦 toodeploy，並使用 hello Azure 堆疊的虛擬硬碟 Disk(VHD) 映像重新部署。 | 雲端系統管理員。 |
| [連接 tooAzure 堆疊](azure-stack-connect-powershell.md) | 使用此模組 tooconnect tooan Azure 堆疊執行個體透過 PowerShell 和 tooconfigure VPN 連線能力 tooAzure 堆疊。 | 雲端系統管理員和使用者 |
| [Azure Stack 服務系統管理](azure-stack-create-offer.md) | Azure 堆疊系統管理員可以使用跨計算、 儲存體、 網路和金鑰保存庫服務預設租用戶提供本模組 toocreate 無限制的配額。   | 雲端系統管理員。|
| [範本驗證程式](azure-stack-validate-templates.md) | 如果現有或新的範本可以部署的 tooAzure 堆疊，請使用此模組 tooverify。 | 雲端系統管理員和使用者 |


## <a name="next-steps"></a>後續步驟
* [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)   
* [透過 VPN 連接 tooAzure 堆疊開發套件](azure-stack-connect-azure-stack.md)  
