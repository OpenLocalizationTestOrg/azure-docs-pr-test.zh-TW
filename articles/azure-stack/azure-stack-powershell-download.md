---
title: "從 GitHub 下載 Azure Stack 工具 | Microsoft Docs"
description: "瞭解如何下載必要的工具來處理 Azure Stack。"
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
ms.openlocfilehash: 589d2ea1ffed9f8ac82793132d9c91efcc60a5fe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="download-azure-stack-tools-from-github"></a>從 GitHub 下載 Azure Stack 工具

AzureStack-Tools 是裝載 PowerShell 模組的 GitHub 存放庫，可用來管理和部署至 Azure Stack 的資源。 您可以針對 Azure Stack 開發套件，或針對以 Windows 為基礎的外部用戶端 (如果您打算建立 VPN 連線能力) 下載並使用這些 PowerShell 模組。 若要取得這些工具，請複製 GitHub 存放庫或下載 AzureStack-Tools 資料夾。 

若要複製存放庫，請下載 [Git](https://git-scm.com/download/win) for Windows，開啟命令提示字元視窗，然後執行下列指令碼：

```PowerShell
# Change directory to the root directory 
cd \

# clone the repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change to the tools directory
cd AzureStack-Tools
```

若要下載工具資料夾，請執行下列指令碼：

```PowerShell
# Change directory to the root directory 
cd \

# Download the tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-the-modules"></a>模組所提供的功能

AzureStack-Tools 存放庫包含 PowerShell 模組，其支援下列 Azure Stack 功能：  

| 功能 | 說明 | 可以使用此模組的人員？ |
| --- | --- | --- |
| [雲端功能](azure-stack-validate-templates.md) | 使用此模組來取得雲端的雲端功能。 例如，您可以針對 Azure Stack 和使用此模組的 Azure 雲端取得雲端功能，例如 API 版本、Azure Resource Manager 資源、VM 擴充功能等。 | 雲端系統管理員和使用者。 |
| [Azure Stack 計算系統管理](azure-stack-add-vm-image.md) | 使用此模組，從 Azure Stack Marketplace 新增或移除 VM 映像。 | 雲端系統管理員。 |
| [Azure Stack 基礎結構系統管理](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | 使用此模組來管理 Azure Stack 基礎結構 VM、警示、更新等。 |  雲端系統管理員。|
| [適用於 Azure Stack 的 Resource Manager 原則](azure-stack-policy-module.md) | 使用此模組來設定 Azure 訂用帳戶或 Azure 資源群組，包含與 Azure Stack 相同的版本和服務可用性。 | 雲端系統管理員和使用者 |
| [註冊 Azure](azure-stack-register.md) | 搭配使用此模組與 Azure 來註冊您的開發套件執行個體。 註冊之後，您可以從 Azure 下載 Marketplace 項目，並在 Azure Stack 中使用它們。 | 雲端系統管理員 |
| [Azure Stack 部署](azure-stack-run-powershell-script.md) | 搭配使用此模組與 Azure Stack 虛擬硬碟 (VHD) 映像，準備要部署與重新部署的 Azure Stack 主機電腦。 | 雲端系統管理員。 |
| [連線至 Azure Stack](azure-stack-connect-powershell.md) | 使用此模組，透過 PowerShell 連線至 Azure Stack 執行個體，並設定 Azure Stack 的 VPN 連線。 | 雲端系統管理員和使用者 |
| [Azure Stack 服務系統管理](azure-stack-create-offer.md) | Azure 堆疊系統管理員可以使用此模組建立跨計算、 儲存體、 網路和金鑰保存庫服務預設租用戶提供無限制的配額。   | 雲端系統管理員。|
| [範本驗證程式](azure-stack-validate-templates.md) | 使用此模組來確認現有或新範本是否可以部署到 Azure Stack。 | 雲端系統管理員和使用者 |


## <a name="next-steps"></a>後續步驟
* [設定 Azure Stack 使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)   
* [透過 VPN 連線至 Azure Stack 開發套件](azure-stack-connect-azure-stack.md)  
