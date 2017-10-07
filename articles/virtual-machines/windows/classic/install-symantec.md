---
title: "在 Azure 中的 Windows VM 上的 Symantec Endpoint Protection aaaInstall |Microsoft 文件"
description: "深入了解如何 tooinstall 及設定新的 hello Symantec Endpoint Protection 安全性延伸模組，或現有的 Azure VM 建立與 hello 傳統部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>如何 tooinstall 及 Windows VM 上設定 Symantec Endpoint Protection
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

本文章將示範如何 tooinstall 和設定現有的虛擬機器 (VM) 執行 Windows Server 上 hello Symantec Endpoint Protection 用戶端。 此完整用戶端包括服務 (例如病毒和間諜軟體防護、防火牆及入侵防禦)。 hello 會安裝用戶端的安全性延伸模組為使用 hello VM 代理程式。

如果您有內部部署解決方案 symantec 提供的現有訂閱，您可以使用它 tooprotect Azure 虛擬機器。 如果您還不是 Symantec 客戶，您可以註冊試用訂用帳戶。 如需此解決方案的詳細資訊，請參閱 [Microsoft Azure 平台上的 Symantec Endpoint Protection][Symantec]。 這個網頁也有連結 toolicensing 資訊和指示安裝 hello 用戶端，如果您已經 Symantec 客戶。

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>在現有 VM 上安裝 Symantec Endpoint Protection
在開始之前，您需要下列 hello:

* hello Azure PowerShell 模組、 0.8.2 版或更新版本，在您的工作電腦。 您可以檢查 hello 版本的 Azure PowerShell 安裝與 hello **Get-module azure | 格式資料表版本**命令。 如需指示和連結 toohello 最新版本，請參閱[如何 tooInstall 和設定 Azure PowerShell][PS]。 登入 tooyour Azure 訂用帳戶使用`Add-AzureAccount`。
* hello VM 代理程式上執行 hello Azure 虛擬機器。

首先，確認該 hello hello 虛擬機器已安裝 VM 代理程式。 填寫 hello 雲端服務名稱和虛擬機器名稱，然後執行下列命令，以系統管理員層級 Azure PowerShell 命令提示字元的 hello。 取代 hello 引號，包括 hello < 和 > 字元內的所有內容。

> [!TIP]
> 如果您不知道 hello 雲端服務和虛擬機器名稱，執行**Get-azurevm** toolist hello 您目前的訂用帳戶中的所有虛擬機器的名稱。

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

如果 hello**寫入主機**命令便會顯示**True**，hello 安裝 VM 代理程式。 如果它顯示**False**，請參閱 hello 指示與下載 hello Azure 部落格文章中的連結 toohello [VM 代理程式和擴充功能-第 2 部分][Agent]。

如果已安裝 VM 代理程式 hello，執行這些命令 tooinstall hello Symantec Endpoint Protection 代理程式。

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

hello Symantec 安全性延伸模組的 tooverify 已安裝且是最新的：

1. 登入 toohello 虛擬機器。 如需指示，請參閱[如何 tooa 執行 Windows Server 的虛擬機器上的 tooLog][Logon]。
2. 在 Windows Server 2008 R2 中，按一下 [開始] > [Symantec Endpoint Protection]。 如需 Windows Server 2012 或 Windows Server 2012 R2，從 hello [開始] 畫面，輸入**Symantec**，然後按一下 **Symantec Endpoint Protection**。
3. 從 hello**狀態** 索引標籤的 hello**狀態 Symantec Endpoint Protection**視窗中，套用更新，或視需要重新啟動。

## <a name="additional-resources"></a>其他資源
[如何 tooLog tooa 執行 Windows Server 的虛擬機器上][Logon]

[Azure VM 擴充功能與功能][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
