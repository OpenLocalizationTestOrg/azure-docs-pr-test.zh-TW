---
title: "aaaReset hello 密碼或 Windows VM 上的遠端桌面組態 |Microsoft 文件"
description: "了解如何 tooreset 帳戶密碼或 Windows VM，使用遠端桌面服務 hello Azure 入口網站或 Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>如何 tooreset hello 遠端桌面服務或 Windows VM 中的其登入密碼
如果您無法連接 tooa Windows 虛擬機器 (VM)，您可以重設 hello 本機系統管理員密碼，或重設 hello 遠端桌面服務設定。 您可以使用任一 hello Azure 入口網站或 hello VM 存取擴充功能在 Azure PowerShell tooreset hello 密碼。 如果您使用 PowerShell，請確定您擁有 hello[最新的 PowerShell 模組安裝並設定](/powershell/azure/overview)和登入 tooyour Azure 訂用帳戶。 您也可以[針對與 hello 傳統部署模型所建立的 Vm 執行這些步驟](reset-rdp.md)。

## <a name="ways-tooreset-configuration-or-credentials"></a>方式 tooreset 組態或認證
根據您的需求而定，您可以透過數種不同方式來重設遠端桌面服務和認證：

- [使用 hello Azure 入口網站重設](#azure-portal)
- [使用 Azure PowerShell 重設](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure 入口網站
tooexpand hello 入口網站功能表上，按一下 hello 三條 hello 左上角，然後按一下**虛擬機器**:

![瀏覽您的 Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**重設 hello 本機系統管理員帳戶密碼**

選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。 hello 密碼重設 刀鋒視窗會顯示：

![密碼重設頁面](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

輸入 hello 使用者名稱和新的密碼，然後按一下 **更新**。 請再次嘗試連線 tooyour VM。

### <a name="reset-hello-remote-desktop-service-configuration"></a>**重設 hello 遠端桌面服務設定**

選取您的 Windows 虛擬機器，然後按一下 [支援與疑難排解] > [重設密碼]。 hello 密碼重設 刀鋒視窗會顯示。 

![重設 RDP 組態](./media/reset-rdp/Portal-RM-RDP-Reset.png)

選取**只能重設組態**從 hello 下拉式選單，然後按一下**更新**。 請再次嘗試連線 tooyour VM。


## <a name="vmaccess-extension-and-powershell"></a>VMAccess 延伸模組和 PowerShell
請確定您擁有 hello[最新的 PowerShell 模組安裝並設定](/powershell/azure/overview)和登入 Azure 訂用帳戶以 hello tooyour `Login-AzureRmAccount` cmdlet。

### <a name="reset-hello-local-administrator-account-password"></a>**重設 hello 本機系統管理員帳戶密碼**
重設 hello 系統管理員密碼或使用者名稱與 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。 建立您的帳戶認證，如下所示：

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> 如果您在 VM 上輸入 hello 目前的本機系統管理員帳戶與不同的名稱，hello VMAccess 擴充功能就會重新命名 hello 本機系統管理員帳戶、 指派您指定的密碼 toothat 的帳戶，以及發出遠端桌面登出事件。 Hello VM 上的本機系統管理員帳戶已停用，hello VMAccess 擴充功能可讓它。

下列範例會更新 hello hello 名為 VM `myVM` hello 資源群組中名為`myResourceGroup`toohello 指定的認證。

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**重設 hello 遠端桌面服務設定**
重設遠端存取 tooyour VM 以 hello[組 AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet。 hello 下列範例會重設名為 hello 存取延伸`myVMAccess`hello 名為 VM 上`myVM`在 hello`myResourceGroup`資源群組：

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> 不論如何，一部 VM 只能有一個 VM 存取代理程式。 tooset hello VM 存取代理程式內容成功，hello`-ForceRerun`選項才能使用。 當使用`-ForceRerun`，請確定 toouse hello hello VM 存取代理程式在任何先前命令中使用相同的名稱。

如果您仍然無法連線遠端 tooyour 虛擬機器，請參閱 < 在多個步驟 tootry[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


## <a name="next-steps"></a>後續步驟
如果 hello Azure VM 存取擴充功能不會回應並無法 tooreset hello 密碼，您可以[重設 hello 本機 Windows 密碼離線](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 這個方法是更進階的程序，並要求您 tooconnect hello 虛擬硬碟的問題 VM tooanother hello VM。 首先，本文章中所述步驟 hello 和就只能嘗試 hello 離線密碼重設方法的最後手段。

[Azure VM 延伸模組與功能](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[透過 RDP 或 SSH 連接 tooan Azure 虛擬機器](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

