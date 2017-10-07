---
title: "aaaReset hello 密碼或在 Azure 中的 Windows VM 上的遠端桌面組態 |Microsoft 文件"
description: "了解如何使用 hello 傳統部署模型使用的帳戶密碼或 Windows VM 上的遠端桌面服務建立的 tooreset hello Azure 入口網站或 Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>如何 tooreset hello 遠端桌面服務或其登入密碼的 Windows VM 中建立使用 hello 傳統部署模型
> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 您也可以[針對與 hello 資源管理員部署模型所建立的 Vm 執行這些步驟](../reset-rdp.md)。

如果您無法連接 tooa Windows 虛擬機器 (VM)，您可以重設 hello 本機系統管理員密碼，或重設 hello 遠端桌面服務設定。 您可以使用任一 hello Azure 入口網站或 hello VM 存取擴充功能在 Azure PowerShell tooreset hello 密碼。

## <a name="ways-tooreset-configuration-or-credentials"></a>方式 tooreset 組態或認證
根據您的需求而定，您可以透過數種不同方式來重設遠端桌面服務和認證：

- [使用 hello Azure 入口網站重設](#azure-portal)
- [使用 Azure PowerShell 重設](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure 入口網站
您可以使用 hello [Azure 入口網站](https://portal.azure.com)tooreset hello 遠端桌面服務。 tooexpand hello 入口網站功能表上，按一下 hello 三條 hello 左上角，然後按一下**虛擬機器 （傳統）**:

![瀏覽您的 Azure VM](./media/reset-rdp/Portal-Select-Classic-VM.png)

選取您的 Windows 虛擬機器，然後按一下**重設遠端...**。 hello 會出現下列對話方塊 tooreset hello 遠端桌面組態：

![重設 RDP 組態頁面](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

您也可以重設 hello 使用者名稱和密碼的 hello 本機系統管理員帳戶。 從您的 VM，按一下 [支援與疑難排解] > [重設密碼]。 hello 密碼重設 刀鋒視窗會顯示：

![密碼重設頁面](./media/reset-rdp/Portal-PW-Reset-Windows.png)

您輸入 hello 新的使用者名稱和密碼之後，請按一下**儲存**。

## <a name="vmaccess-extension-and-powershell"></a>VMAccess 延伸模組和 PowerShell
請確定 hello hello 虛擬機器安裝 VM 代理程式。 hello VMAccess 擴充功能不需要 toobe 安裝之前，您可以使用它，只要 hello VM 代理程式可用。 請確認已安裝 VM 代理程式使用下列命令的 hello 該 hello。 （取代"myCloudService"和"myVM"hello 您雲端服務名稱及您的 VM，分別。 您可以執行不搭配任何參數的 `Get-AzureVM` 來知道這些名稱)。

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

如果 hello**寫入主機**命令便會顯示**True**，hello 安裝 VM 代理程式。 如果它顯示**False**，請參閱 hello 指示及在 hello 下載連結 toohello [VM 代理程式和擴充功能-第 2 部分](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409)Azure 部落格文章。

如果您使用 hello 入口網站建立 hello 虛擬機器，請檢查是否`$vm.GetInstance().ProvisionGuestAgent`傳回**True**。 否則，請使用此命令加以設定︰

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

此命令可防止下列錯誤，如果您執行 hello hello**組 AzureVMExtension**命令 hello 接下來的步驟: 「 佈建客體代理程式上必須啟用 hello VM 物件才能設定 IaaS VM 存取擴充功能。 」

### <a name="reset-hello-local-administrator-account-password"></a>**重設 hello 本機系統管理員帳戶密碼**
建立登入認證與 hello 目前本機系統管理員帳戶名稱和新的密碼，然後再執行 hello `Set-AzureVMAccessExtension` ，如下所示。

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

如果您輸入 hello 目前的帳戶不同的名稱，hello VMAccess 擴充功能就會重新命名 hello 本機系統管理員帳戶、 指派 toothat hello 密碼的帳戶，以及發出登出遠端桌面。Hello 本機系統管理員帳戶已停用，hello VMAccess 擴充功能可讓它。

這些命令也會重設 hello 遠端桌面服務設定。

### <a name="reset-hello-remote-desktop-service-configuration"></a>**重設 hello 遠端桌面服務設定**
tooreset hello 遠端桌面服務組態，執行下列命令的 hello:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

hello VMAccess 擴充功能 hello 虛擬機器上執行兩個命令：

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

此命令會啟用 hello 內建的 Windows 防火牆群組允許連入的遠端桌面流量，會使用 TCP 連接埠 3389。

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

此命令會設定 hello fDenyTSConnections 登錄值 too0，啟用遠端桌面連線。

## <a name="next-steps"></a>後續步驟
如果 hello Azure VM 存取擴充功能不會回應並無法 tooreset hello 密碼，您可以[重設 hello 本機 Windows 密碼離線](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 這個方法是更進階的程序，並要求您 tooconnect hello 虛擬硬碟的問題 VM tooanother hello VM。 首先，本文章中所述步驟 hello 和就只能嘗試 hello 離線密碼重設方法的最後手段。

[Azure VM 延伸模組與功能](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[透過 RDP 或 SSH 連接 tooan Azure 虛擬機器](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

