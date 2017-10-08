---
title: "aaaInstall PowerShell for Azure 堆疊 |Microsoft 文件"
description: "深入了解如何 tooinstall PowerShell for Azure 堆疊。"
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
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: 60995af2168348638e2513ab941a4125ca5c624a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-powershell-for-azure-stack"></a>安裝適用於 Azure Stack 的 PowerShell  

Azure 堆疊相容 Azure PowerShell 模組是與 Azure 堆疊的必要的 toowork。 本指南中，我們逐步引導您 hello 步驟需要 tooinstall PowerShell 的 Azure 堆疊。 您可以使用本文從 hello Azure 堆疊開發套件，或是從 windows 的外部用戶端中所述，如果您透過 VPN 連線的 hello 步驟。

這篇文章包含詳細指示 tooinstall PowerShell 的 Azure 堆疊。 不過，如果您想 tooquickly 安裝並設定 PowerShell 時，您可以使用 hello 指令碼中的 hello 提供[取得啟動並執行使用 PowerShell](azure-stack-powershell-configure-quickstart.md)主題。 

> [!NOTE]
> 下列步驟的 hello 需要 PowerShell 5.0。 toocheck 您的版本、 執行 $PSVersionTable.PSVersion 和比較 hello 「 主要 」 版本。

Azure 堆疊的 PowerShell 命令會透過 hello PowerShell 資源庫進行安裝。 tooregiser hello PSGallery 儲存機制、 開啟提升權限的 PowerShell 工作階段從 hello 開發套件，或從 windows 的外部用戶端透過 VPN 連線，然後執行下列命令的 hello:

```powershell
Set-PSRepository `
  -Name "PSGallery" `
  -InstallationPolicy Trusted
```

## <a name="uninstall-existing-versions-of-powershell"></a>解除安裝現有的 PowerShell 版本

在安裝之前 hello 必要的版本，請確定您在解除安裝任何現有的 Azure PowerShell 模組。 您可以使用其中一種 hello 下列兩種方法來解除安裝這些設定：

* 如果您計劃 tooestablish VPN 連線，toouninstall hello 現有 PowerShell 模組，會登入 toohello development kit 或 toohello Windows 架構的外部用戶端。 關閉所有 hello 作用中的 PowerShell 工作階段和執行下列命令的 hello: 

   ```powershell
   Get-Module -ListAvailable | where-Object {$_.Name -like “Azure*”} | Uninstall-Module
   ```

* 登入 toohello development kit 或 toohello Windows 架構的外部用戶端如果您計劃 tooestablish VPN 連線。 刪除從 hello 以"Azure"開頭的所有 hello 資料夾`C:\Program Files (x86)\WindowsPowerShell\Modules`和`C:\Users\AzureStackAdmin\Documents\WindowsPowerShell\Modules`資料夾。 刪除這些資料夾中移除任何現有的 PowerShell 模組，從 hello"AzureStackAdmin 」 與 「 全域 」 的使用者領域。 

hello 下列各節說明 hello 步驟需要的 tooinstall PowerShell for Azure 堆疊。 可在連線、部分連線或中斷連線案例中，於 Azure Stack 上安裝 PowerShell。 

## <a name="install-powershell-in-a-connected-scenario"></a>在連線案例中安裝 PowerShell 

透過 API 版本設定檔安裝 Azure Stack 相容的 AzureRM 模組。 Azure 堆疊需要 hello **2017年-03-09-設定檔**API 版本設定檔，也就是可用安裝 hello AzureRM.Bootstrapper 模組。 API 版本設定檔和 hello cmdlet，提供關於 toolearn 參考 toohello[管理 API 版本設定檔](azure-stack-version-profiles.md)。 在加法 toohello AzureRM 模組中，您也應該安裝 hello Azure 堆疊專屬 PowerShell 模組。 在開發工作站上執行下列 PowerShell 指令碼 tooinstall hello 這些模組：

  ```powershell
  # Install hello AzureRM.Bootstrapper module. Select Yes when prompted tooinstall NuGet 
  Install-Module `
    -Name AzureRm.BootStrapper

  # Install and import hello API Version Profile required by Azure Stack into hello current PowerShell session.
  Use-AzureRmProfile `
    -Profile 2017-03-09-profile -Force

  Install-Module `
    -Name AzureStack `
    -RequiredVersion 1.2.10
  ```

tooconfirm hello 安裝，請執行下列命令的 hello:

  ```powershell
  Get-Module `
    -ListAvailable | where-Object {$_.Name -like “Azure*”}
  ```
  如果 hello 安裝成功，會顯示 hello AzureRM 和 AzureStack 模組 hello 輸出中。

## <a name="install-powershell-in-a-disconnected-or-in-a-partially-connected-scenario"></a>在已中斷連線或部分連線案例中安裝 PowerShell

在中斷連線的案例中，您必須先下載 hello PowerShell 模組 tooa 電腦具有網際網路連線，然後將其傳送 toohello Azure 堆疊開發套件進行安裝。

1. 登入 tooa 電腦，而且您的網際網路連線，使用下列指令碼 toodownload hello AzureRM，hello AzureStack 封裝到您的本機電腦上：

   ```powershell
   $Path = "<Path that is used toosave hello packages>"

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureRM `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10

   Save-Package `
     -ProviderName NuGet `
     -Source https://www.powershellgallery.com/api/v2 `
     -Name AzureStack `
     -Path $Path `
     -Force `
     -RequiredVersion 1.2.10 
   ```

2. 複製 hello tooa USB 裝置透過下載封裝。

3. 登入 toohello 開發套件，並從 hello USB 裝置 tooa 位置 hello 開發套件複製 hello 封裝。 

4. 現在您必須註冊此位置為 hello 預設儲存機制，並從這個儲存機制安裝 hello AzureRM 和 AzureStack 模組：

   ```powershell
   $SourceLocation = "<Location on hello development kit that contains hello PowerShell packages>"
   $RepoName = "MyNuGetSource"

   Register-PSRepository `
     -Name $RepoName `
     -SourceLocation $SourceLocation `
     -InstallationPolicy Trusted

   ```powershell
   Install-Module AzureRM `
     -Repository $RepoName

   Install-Module AzureStack `
     -Repository $RepoName 
   ```

## <a name="next-steps"></a>後續步驟

* [從 GitHub 下載 Azure Stack 工具](azure-stack-powershell-download.md)
* [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md)  
* [設定 hello Azure 堆疊操作員的 PowerShell 環境](azure-stack-powershell-configure-admin.md) 
* [在 Azure Stack 中管理 API 版本設定檔](azure-stack-version-profiles.md)  
