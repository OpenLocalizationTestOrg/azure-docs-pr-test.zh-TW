---
title: "aaaAutomating 虛擬機器擴充功能的應用程式部署 |Microsoft 文件"
description: "Azure 虛擬機器 DotNet 核心教學課程"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a>使用適用於 Windows VM 的 Azure Resource Manager 範本進行應用程式部署

一旦所有 Azure 基礎結構需求有已找出並轉譯成部署範本，hello 實際的應用程式部署將需要 toobe 定址。 此應用程式部署指 tooinstalling hello 實際的應用程式二進位檔拖曳至 Azure 資源。 Hello 音樂商店範例中，.Net Core 和 IIS 需要 toobe 每部虛擬機器上安裝和設定。 預先建立 hello Music Store 二進位檔需要 toobe hello 的虛擬機器，安裝和 hello 音樂存放區資料庫。

這份文件詳細說明虛擬機器擴充功能可以自動化應用程式部署和設定 tooAzure 虛擬機器的方式。 所有相依項目和獨特的設定都會以醒目提示的方式標示。 Hello 獲得最佳經驗，針對預先部署 hello 方案 tooyour Azure 訂用帳戶和與 hello Azure Resource Manager 範本一起工作的執行個體。 hello 完成範本可以在這裡 – 找到[音樂存放部署在 Windows 上](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows)。

## <a name="configuration-script"></a>組態指令碼
虛擬機器擴充功能是針對虛擬機器 tooprovide 組態自動化來執行的特定的程式。 針對許多特定用途 (防毒、記錄組態及 Docker 組態) 都有擴充功能可供使用。 hello 自訂指令碼延伸可以是使用的 toorun 任何指令碼的虛擬機器。 與 hello 音樂商店範例中，它已啟動 toohello 自訂指令碼延伸 tooconfigure hello Windows 虛擬機器，並安裝 hello Music Store 應用程式。

然後再詳細說明如何將虛擬機器擴充功能宣告 Azure Resource Manager 範本中，檢查 hello 指令碼執行。 此指令碼會設定 hello Windows 虛擬機器 toohost hello Music Store 應用程式。 Hello 指令碼執行時，安裝所需的所有軟體，請安裝從原始檔控制的 hello 音樂市集應用程式並準備 hello 資料庫。 

> 此範例僅供示範之用。

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a>VM 指令碼擴充功能
VM 擴充功能可以執行的虛擬機器在建立時期 hello 延伸模組資源併入 hello Azure Resource Manager 範本。 hello Visual Studio 新增資源精靈，或藉由將有效的 JSON 插入 hello 範本可以加入 hello 延伸模組。 hello 虛擬機器資源; 巢狀 hello 指令碼擴充功能資源這可以在下列範例中的 hello 看到。

請依照此連結 toosee hello JSON 範例內 hello Resource Manager 範本 – [VM 指令碼延伸](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339)。 

請注意，在 hello 下方 hello 指令碼的 JSON 儲存在 GitHub 中。 此指令碼也可以儲存在 Azure Blob 儲存體中。 此外，Azure 資源管理員範本可讓 hello 指令碼執行字串 toobe 建構，例如範本參數的值可用來當作參數執行指令碼。 部署 hello 範本時，在此情況下提供資料並執行 hello 指令碼時，可以接著使用這些值。

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

如上面所述，也是您的自訂指令碼在 Azure Blob 儲存體可能 toostore。 有兩個選項，用來儲存 blob 儲存體; 中的 hello 指令碼資源讓 hello 公用容器/指令碼，並遵循的 hello 上述相同方式，或是它可以保留私用 blob 儲存體，這需要您 tooprovide hello storageAccountName 及 storageAccountKey toohello CustomScriptExtension 資源定義中。

在 hello 面範例中我們已經步驟進一步。 雖然可能 tooprovide hello 儲存體帳戶名稱和金鑰做為參數或變數在部署期間，資源管理員範本提供 hello`listKeys`函式可以取得 hello 儲存體帳戶金鑰以程式設計方式，並將它插 toohello讓您在部署階段的範本。

Azure 儲存體帳戶呼叫 hello 範例 CustomScriptExtension 資源定義，我們的自訂指令碼已經過上傳的 tooan`mystorageaccount9999`位於另一個資源群組，稱為`mysa999rgname`。 當部署包含此資源的範本時，hello`listKeys`函式以程式設計方式取得 hello hello 儲存體帳戶的儲存體帳戶金鑰`mystorageaccount9999`hello 資源群組中`mysa999rgname`，並將它插入我們 toohello 範本。

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

hello 這個方法的主要優點是它不需要您 toochange 您的範本，或部署的 hello 事件中的參數 hello 儲存體帳戶金鑰變更。

如需有關使用 hello 自訂指令碼延伸模組的詳細資訊，請參閱[自訂指令碼延伸模組與資源管理員範本](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

## <a name="next-step"></a>後續步驟
<hr>

[探索其他 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates)

