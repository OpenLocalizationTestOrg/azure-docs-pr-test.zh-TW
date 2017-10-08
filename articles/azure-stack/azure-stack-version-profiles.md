---
title: "在 Azure 堆疊 aaaUsing API 版本設定檔 |Microsoft 文件"
description: "了解 Azure Stack 中的 API 版本設定檔。"
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
ms.date: 03/21/2017
ms.author: sngun
ms.openlocfilehash: cb54a683054f08fd123bcb6245d88aaa30c29882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-api-version-profiles-in-azure-stack"></a>管理 Azure Stack 中的 API 版本設定檔

API 版本設定檔提供方式 toomanage Azure 和 Azure 堆疊之間的版本差異。 API 版本設定檔是一組具有特定 API 版本的 AzureRM PowerShell 模組。 每個雲端平台都有一組支援的 API 版本設定檔。 例如，Azure 堆疊支援特定的日期設定檔版本例如**2017年-03-09-設定檔**，和 Azure 支援 hello**最新**API 版本設定檔。 當您安裝設定檔時，hello 對應 toohello 的 AzureRM PowerShell 模組指定設定檔會安裝。

## <a name="install-hello-powershell-module-required-toouse-api-version-profiles"></a>安裝 hello PowerShell 模組所需 toouse API 版本設定檔

hello **AzureRM.Bootstrapper**可透過 PowerShell 資源庫 hello 的模組提供 PowerShell cmdlet 的必要的 toowork 使用的 API 版本設定檔。 使用下列 cmdlet tooinstall hello AzureRM.Bootstrapper 模組 hello:

```PowerShell
Install-Module -Name AzureRm.BootStrapper
```
hello AzureRM.Bootstrapper 模組目前處於預覽狀態。詳細資料和功能會主旨 toochange。 toodownload 並安裝 hello 最新版本中執行下列 cmdlet 的 hello hello PowerShell 資源庫，此模組：

```PowerShell
Update-Module -Name "AzureRm.BootStrapper"
```

## <a name="install-a-profile"></a>安裝設定檔

使用 hello**安裝 AzureRmProfile** cmdlet 搭配 hello **2017年-03-09-設定檔**API 版本設定檔 tooinstall hello AzureRM 模組所需的 Azure 堆疊。 請注意，hello Azure 堆疊雲端系統管理員模組不會安裝這個應用程式開發介面版本設定檔，而且應該先安裝它們個別的 hello hello 步驟 3 中指定[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)發行項。

```PowerShell 
Install-AzureRMProfile -Profile 2017-03-09-profile
```
## <a name="install-and-import-modules-in-a-profile"></a>安裝並匯入設定檔中的模組

使用 hello**使用 AzureRmProfile**的 API 版本設定檔相關聯的 cmdlet tooinstall 和匯入模組。 在一個 PowerShell 工作階段中只能匯入一個 API 版本設定檔。 tooimport 不同的應用程式開發介面版本設定檔，您就必須開啟新的 PowerShell 工作階段。 hello 使用 AzureRMProfile 指令程式會執行下列工作的 hello:  
1. 檢查如果 hello 與相關聯的 hello PowerShell 模組指定的 API 版本設定檔會安裝在 hello 目前範圍中。  
2. 下載並安裝 hello 模組，如果尚未安裝。   
3. 匯入到目前 PowerShell 工作階段 hello hello 模組。 

```PowerShell
# Installs and imports hello specified API version profile into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser

# Installs and imports hello specified API version profile into hello current PowerShell session without any prompts
Use-AzureRmProfile -Profile 2017-03-09-profile -Scope CurrentUser -Force
```

tooinstall 和匯入選取的 API 版本設定檔，執行 hello 使用 AzureRMProfile 指令程式以 hello AzureRM 模組**模組**參數：

```PowerShell
# Installs and imports hello compute, Storage and Network modules from hello specified API version profile into your current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile -Module AzureRM.Compute, AzureRM.Storage, AzureRM.Network
```

## <a name="get-hello-installed-profiles"></a>取得安裝的 hello 設定檔

使用 hello **Get AzureRmProfile** cmdlet tooget hello 清單可用的 API 版本設定檔： 

```PowerShell
# lists all API version profiles provided by hello AzureRM.BootStrapper module.
Get-AzureRmProfile -ListAvailable 

# lists hello API version profiles which are installed on your machine
Get-AzureRmProfile
```
## <a name="update-profiles"></a>更新設定檔

使用 hello**更新 AzureRmProfile**模組中可用的 API 版本設定檔 toohello 最新版本中的 cmdlet tooupdate hello 模組 hello PSGallery。 建議 tooalways 執行 hello**更新 AzureRmProfile**匯入模組時，指令程式在新的 PowerShell 工作階段 tooavoid 相衝突。 hello 更新 AzureRmProfile 指令程式會執行下列工作的 hello:

1. 檢查是否 hello 最新版本的模組會安裝在 hello hello 目前領域中指定 API 版本設定檔。  
2. 會提示您 tooinstall 如果尚未安裝。  
3. 安裝和更新的 hello 模組匯入到 hello 目前 PowerShell 工作階段。  

```PowerShell
Update-AzureRmProfile -Profile 2017-03-09-profile
```

tooremove hello 先前已安裝版本的 hello 模組，然後再更新 toohello 最新可用版本，就會使用 hello 更新 AzureRmProfile cmdlet，以及 hello **-RemovePreviousVersions**參數：

```PowerShell 
Update-AzureRmProfile -Profile 2017-03-09-profile -RemovePreviousVersions
```

此 cmdlet 會執行下列工作的 hello:  

1. 檢查是否 hello 最新版本的模組會安裝在 hello hello 目前領域中指定 API 版本設定檔。  
2. 從目前的 API 版本設定檔 hello 和 hello 目前 PowerShell 工作階段中移除 hello 較舊版本的模組。  
4. 會提示您 tooinstall hello 最新版本。  
5. 安裝和更新的 hello 模組匯入到 hello 目前 PowerShell 工作階段。  
 
## <a name="uninstall-profiles"></a>將設定檔解除安裝

使用 hello**解除安裝 AzureRmProfile** cmdlet toouninstall hello 指定 API 版本設定檔。

```PowerShell 
Uninstall-AzureRmProfile -Profile 2017-03-09-profile
```

## <a name="next-steps"></a>後續步驟
* [安裝 Azure Stack 適用的 PowerShell](azure-stack-powershell-install.md)
* [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)  
