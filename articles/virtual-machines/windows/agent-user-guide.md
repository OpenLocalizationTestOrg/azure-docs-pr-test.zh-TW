---
title: "aaaAzure 虛擬機器代理程式概觀 |Microsoft 文件"
description: "Azure 虛擬機器代理程式概觀"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: nepeters
ms.openlocfilehash: b03542b9a9c711000fab18ed82e9b17ee5510bbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Azure 虛擬機器代理程式概觀

hello Microsoft Azure 虛擬機器代理程式 （上午代理程式） 是安全的輕量型程序管理 VM 與 hello Azure 網狀架構控制器之間的互動。 hello VM 代理程式已啟用和執行 Azure 虛擬機器擴充功能的主要角色。 VM 擴充功能可啟用虛擬機器的部署後組態，例如安裝和設定軟體。 虛擬機器擴充功能也會啟用復原功能，例如，重設虛擬機器的 hello 系統管理密碼。 沒有 hello Azure VM 代理程式，就無法執行虛擬機器擴充功能。

本文件詳述安裝、 偵測和移除 hello Azure 虛擬機器代理程式。

## <a name="install-hello-vm-agent"></a>安裝 VM 代理程式 hello

### <a name="azure-gallery-image"></a>Azure 資源庫映像

從 Azure 資源庫映像部署任何 Windows 虛擬機器上的預設會安裝 hello Azure VM 代理程式。 部署 Azure 資源庫映像從 hello 入口網站、 PowerShell、 命令列介面或 Azure 資源管理員範本，當 hello Azure VM 代理程式也會安裝。 

### <a name="manual-installation"></a>手動安裝

hello Windows VM 代理程式可以使用 Windows installer 封裝來手動安裝。 建立會部署在 Azure 中的自訂虛擬機器映像時，可能需要手動安裝。 toomanually 安裝 hello Windows VM 代理程式，從這個位置下載 hello VM 代理程式安裝程式[Windows Azure VM 代理程式下載](http://go.microsoft.com/fwlink/?LinkID=394789)。 

hello VM 代理程式可以按兩下 hello windows installer 檔案安裝。 自動或無人看管的 hello VM 代理程式安裝，執行下列命令的 hello。

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>偵測 hello VM 代理程式

### <a name="powershell"></a>PowerShell

hello Azure 資源管理員 PowerShell 模組可以是使用的 tooretrieve 資訊有關 Azure 虛擬機器。 執行`Get-AzureRmVM`傳回相當多的資訊包括 hello 佈建 hello Azure VM 代理程式的狀態。

```PowerShell
Get-AzureRmVM
```

hello 以下是剛 hello 子集`Get-AzureRmVM`輸出。 請注意 hello`ProvisionVMAgent`屬性在巢狀`OSProfile`，這個屬性可以是使用的 toodetermine 如果 hello VM 代理程式已部署的 toohello 虛擬機器。

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

下列指令碼的 hello 可以是使用的 tooreturn hello hello VM 代理程式狀態的虛擬機器名稱簡明清單。

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>手動偵測

登入 Windows Azure VM tooa，工作管理員可以使用的 tooexamine 執行處理程序。 toocheck hello Azure VM 代理程式，開啟 [工作管理員 > 按一下 hello 詳細資料] 索引標籤，並尋找處理程序名稱`WindowsAzureGuestAgent.exe`。 此程序的 hello 存在表示該 hello VM 代理程式安裝。

## <a name="upgrade-hello-vm-agent"></a>升級 hello VM 代理程式

hello Azure VM 代理程式的 Windows 會自動升級。 由於新的虛擬機器是部署的 tooAzure，他們會收到 hello 最新的 VM 代理程式。 自訂 VM 映像應該手動更新的 tooinclude hello 新 VM 代理程式。
