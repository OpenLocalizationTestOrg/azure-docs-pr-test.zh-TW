---
title: "在 Azure 中疑難排解 aaaDetailed 遠端桌面 |Microsoft 文件"
description: "檢閱您不能在 Azure 中的 tooa Windows 虛擬機器的遠端桌面錯誤的詳細疑難排解步驟"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
keywords: "無法連接 tooremote 桌面，疑難排解遠端桌面，遠端桌面無法連線，遠端桌面的錯誤、 遠端桌面疑難排解、 遠端桌面問題"
ms.assetid: 9da36f3d-30dd-44af-824b-8ce5ef07e5e0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: fcb0d06aa66b748f3ebbbbe3431471d3cbe7c60d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-troubleshooting-steps-for-remote-desktop-connection-issues-toowindows-vms-in-azure"></a>遠端桌面連線的詳細疑難排解步驟發出 tooWindows Azure 中的 Vm
本文章提供詳細的疑難排解步驟 toodiagnose 及修正複雜的遠端桌面錯誤為 windows Azure 虛擬機器。

> [!IMPORTANT]
> tooeliminate hello 更常見的遠端桌面錯誤，請確定 tooread [hello 基本的疑難排解文章遠端桌面](troubleshoot-rdp-connection.md)後再繼續。

您可能會遇到不相似 hello 特定錯誤訊息的錯誤訊息中涵蓋的遠端桌面[hello 疑難排解指南的基本遠端桌面](troubleshoot-rdp-connection.md)。 請遵循這些步驟 toodetermine，hello 遠端桌面 (RDP) 用戶端為何無法 tooconnect toohello RDP 服務 hello Azure VM 上。

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。 或者，您也可以提出 Azure 支援事件。 移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)按一下**取得支援**。 使用 Azure 支援的相關資訊，請參閱 hello [Microsoft Azure 支援常見問題集](https://azure.microsoft.com/support/faq/)。

## <a name="components-of-a-remote-desktop-connection"></a>遠端桌面連線的元件
RDP 連線涉及 hello 下列元件：

![](./media/detailed-troubleshoot-rdp/tshootrdp_0.png)

繼續之前，它可能有助於 toomentally 檢閱 hello 最後一個成功遠端桌面連線 toohello VM 以來的變更。 例如：

* hello hello VM 或 hello 雲端服務包含 hello VM 的公用 IP 位址 (也稱為虛擬 IP 位址 hello [VIP](https://en.wikipedia.org/wiki/Virtual_IP_address)) 已變更。 hello RDP 失敗可能是因為您的 DNS 用戶端快取仍然具有 hello*舊的 IP 位址*hello DNS 名稱登錄。 排清您的 DNS 用戶端快取，然後再試一次連接 hello VM。 或嘗試使用 hello 新 VIP 直接連接。
* 您正在使用協力廠商應用程式 toomanage 遠端桌面連線，而不使用 hello hello Azure 入口網站所產生的連線。 請確認該 hello 應用程式組態包含 hello 正確 TCP 通訊埠 hello 遠端桌面流量。 您可以檢查這個連接埠為傳統的虛擬機器在 hello [Azure 入口網站](https://portal.azure.com)，依序按一下 hello VM 的設定 > 端點。

## <a name="preliminary-steps"></a>預備步驟
繼續之前 toohello 詳細的疑難排解，

* 檢查 hello hello hello Azure 入口網站有任何明顯的問題中的虛擬機器狀態。
* 請遵循 hello[快速修正常見 RDP 錯誤 hello 基本疑難排解步驟引導](troubleshoot-rdp-connection.md#quick-troubleshooting-steps)。

嘗試完成這些步驟之後重新連接 toohello 透過遠端桌面的 VM。

## <a name="detailed-troubleshooting-steps"></a>詳細的疑難排解步驟
hello 遠端桌面用戶端可能無法 hello Azure VM 上的無法 tooreach hello 遠端桌面服務到期 tooissues 在 hello 下列來源：

* [遠端桌面用戶端電腦](#source-1-remote-desktop-client-computer)
* [組織內部網路的邊緣裝置](#source-2-organization-intranet-edge-device)
* [雲端服務端點和存取控制清單 (ACL)](#source-3-cloud-service-endpoint-and-acl)
* [網路安全性群組](#source-4-network-security-groups)
* [以 Windows 為基礎的 Azure VM](#source-5-windows-based-azure-vm)

## <a name="source-1-remote-desktop-client-computer"></a>來源 1：遠端桌面用戶端電腦
請確認您的電腦，可以進行遠端桌面連線 tooanother 內部，Windows 型電腦。

![](./media/detailed-troubleshoot-rdp/tshootrdp_1.png)

如果您無法檢查下列設定，在您的電腦上的 hello:

* 目前封鎖「遠端桌面」流量的本機防火牆設定。
* 目前阻止「遠端桌面」連線的本機安裝用戶端 Proxy 軟體。
* 目前阻止「遠端桌面」連線的本機安裝網路監視軟體。
* 目前阻止「遠端桌面」連線的其他類型安全性軟體，這些軟體會監視流量或允許/不允許特定類型的流量。

在這些情況下，請暫時停用 hello 軟體，然後再試一次 tooconnect tooan 在內部部署電腦上透過遠端桌面。 如此一來，您可以找出 hello 實際原因中，如果使用您的網路系統管理員 toocorrect hello 軟體設定 tooallow 遠端桌面連線。

## <a name="source-2-organization-intranet-edge-device"></a>來源 2：組織內部網路的邊緣裝置
請確認電腦直接連線的 toohello 網際網路可讓遠端桌面連線 tooyour Azure 虛擬機器。

![](./media/detailed-troubleshoot-rdp/tshootrdp_2.png)

如果您沒有直接連接的 toohello 網際網路的電腦，建立並使用新的 Azure 虛擬機器資源群組或雲端服務中進行測試。 如需詳細資訊，請參閱 [在 Azure 中建立執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)。 Hello 測試之後，您可以刪除 hello 虛擬機器和 hello 資源群組或 hello 的雲端服務。

如果您可以建立與電腦的遠端桌面連接直接連接 toohello 網際網路，請檢查您的組織內部網路的邊緣裝置進行：

* 內部防火牆封鎖 HTTPS 連線 toohello 網際網路。
* 目前阻止「遠端桌面」連線的 Proxy 伺服器。
* 目前在邊緣網路中的裝置上執行且阻止「遠端桌面」連線的入侵偵測或網路監視軟體。

使用您組織內部網路邊緣裝置 tooallow HTTPS 為基礎的遠端桌面連線 toohello 網際網路的網路系統管理員 toocorrect hello 設定。

## <a name="source-3-cloud-service-endpoint-and-acl"></a>來源 3：雲端服務端點和 ACL
進行建立的 Vm 使用 hello 傳統部署模型，請確認您的是另一個 Azure VM 中 hello 相同雲端服務或虛擬網路可讓遠端桌面連線 tooyour Azure VM。

![](./media/detailed-troubleshoot-rdp/tshootrdp_3.png)

> [!NOTE]
> 建立資源管理員 中的虛擬機器，請跳過[來源 4： 網路安全性群組](#source-4-network-security-groups)。

如果您沒有另一個虛擬機器在 hello 相同雲端服務或虛擬網路，請建立一個。 中的 hello 步驟[建立在 Azure 中執行 Windows 的虛擬機器](../virtual-machines-windows-hero-tutorial.md)。 Hello 測試完成後，請刪除 hello 測試虛擬機器。

如果您可以透過遠端桌面中的 hello tooa 虛擬主機連接相同雲端服務或虛擬網路中，檢查這些設定：

* hello hello 目標 VM 上的遠端桌面流量的端點組態： hello 私人 TCP 連接埠的 hello 端點必須符合 hello 的 hello VM 的遠端桌面服務所接聽的 TCP 連接埠 （預設值為 3389）。
* hello 遠端桌面流量端點 hello 目標 VM 上的 ACL hello: Acl 可讓您 toospecify 允許或拒絕連入流量從 hello 網際網路根據來源 IP 位址。 設定不正確的 Acl 可以防止內送的遠端桌面流量 toohello 端點。 請檢查您在允許的公用 IP 位址的 proxy 或其他的邊緣伺服器連入流量的 Acl tooensure。 如需詳細資訊，請參閱 [什麼是網路存取控制清單 (ACL)？](../../virtual-network/virtual-networks-acl.md)

toocheck hello 端點是否 hello 問題的來源 hello，移除 hello 目前端點，以及建立新的連線，選擇隨機連接埠在 hello 範圍 49152 – 65535 hello 外部連接埠號碼。 如需詳細資訊，請參閱[如何端點 tooa 虛擬機器 tooset](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="source-4-network-security-groups"></a>來源 4：網路安全性群組
網路安全性群組能夠更精確地控制受允許的輸入和輸出流量。 您可以在 Azure 虛擬網路中建立跨越子網路和雲端服務的規則。

使用[IP 流量確認](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md)tooconfirm 如果網路安全性群組中的規則會封鎖從虛擬機器的流量 tooor。 您也可以檢閱有效安全性群組規則 tooensure 輸入 「 允許 」 NSG 規則存在，而且已設定優先權的 RDP 連接埠 （預設值為 3389）。 如需詳細資訊，請參閱[使用有效的安全性規則 tootroubleshoot VM 流量流程](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow)。

## <a name="source-5-windows-based-azure-vm"></a>來源 5：以 Windows 為基礎的 Azure VM
![](./media/detailed-troubleshoot-rdp/tshootrdp_5.png)

請依照下列中的 hello 指示[本文](reset-rdp.md)。 這篇文章會重設 hello hello 虛擬機器上的遠端桌面服務：

* 啟用 hello 「 遠端桌面 」 Windows 防火牆預設規則 （TCP 連接埠 3389）。
* 藉由設定 hello HKLM\System\CurrentControlSet\Control\Terminal Server\fDenyTSConnections 登錄值 too0 啟用遠端桌面連線。

請嘗試 hello 連線從您的電腦一次。 如果您仍然無法 tooconnect 透過遠端桌面，請檢查下列可能的問題的 hello:

* hello 遠端桌面服務未在 hello 目標 VM 上執行。
* hello 遠端桌面服務不會接聽 TCP 連接埠 3389。
* Windows 防火牆或另一個本機防火牆有阻止遠端桌面流量的輸出規則。
* 入侵偵測或網路監視 hello Azure 虛擬機器上執行的軟體防止遠端桌面連接。

對於使用 hello 傳統部署模型所建立的 Vm，您可以使用遠端的 Azure PowerShell 工作階段 toohello Azure 虛擬機器。 首先，您需要 tooinstall 憑證 hello 虛擬機器的主機的雲端服務。 跳過[設定安全的遠端 PowerShell 存取 tooAzure 虛擬機器](http://gallery.technet.microsoft.com/scriptcenter/Configures-Secure-Remote-b137f2fe)並下載 hello **InstallWinRMCertAzureVM.ps1**指令碼檔案 tooyour 本機電腦。

接下來，如果尚未安裝 Azure PowerShell，則請先安裝。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

接下來，開啟 Azure PowerShell 命令提示字元並變更 hello 資料夾 toohello 的目前位置 hello **InstallWinRMCertAzureVM.ps1**指令碼檔案。 toorun Azure PowerShell 指令碼，您必須設定 hello 正確的執行原則。 執行 hello **Get-executionpolicy**命令 toodetermine 目前的原則層級。 如需設定 hello 適當層級的資訊，請參閱[Set-executionpolicy](https://technet.microsoft.com/library/hh849812.aspx)。

接下來，填寫您的 Azure 訂用帳戶名稱、 hello 雲端服務名稱和 （移除 hello < 和 > 字元） 的虛擬機器名稱，然後執行下列命令。

```powershell
$subscr="<Name of your Azure subscription>"
$serviceName="<Name of hello cloud service that contains hello target virtual machine>"
$vmName="<Name of hello target virtual machine>"
.\InstallWinRMCertAzureVM.ps1 -SubscriptionName $subscr -ServiceName $serviceName -Name $vmName
```

您可以從 hello 取得 hello 正確的訂用帳戶名稱*訂用帳戶名稱*屬性 hello 顯示 hello **Get-azuresubscription**命令。 您可以從 hello 取得 hello hello 虛擬機器的雲端服務名稱*ServiceName*資料行中的 hello hello 顯示**Get-azurevm**命令。

檢查是否有 hello 新憑證。 開啟 hello 目前使用者憑證 嵌入式管理單元，然後查看 hello**受信任的根 Certification Authorities\Certificates**資料夾。 您應該會看到您的雲端服務中發行 toocolumn hello hello DNS 名稱的憑證 (範例： cloudservice4testing.cloudapp.net)。

接下來，使用這些命令起始遠端 Azure PowerShell 工作階段。

```powershell
$uri = Get-AzureWinRMUri -ServiceName $serviceName -Name $vmName
$creds = Get-Credential
Enter-PSSession -ConnectionUri $uri -Credential $creds
```

輸入有效的系統管理員認證之後, 您應該會看到類似 toohello 下列 Azure PowerShell 命令提示字元：

```powershell
[cloudservice4testing.cloudapp.net]: PS C:\Users\User1\Documents>
```

此提示 hello 第一個部分是您的雲端服務名稱，其中包含可能是不同於 「 cloudservice4testing.cloudapp.net"hello 目標 VM。 您現在可以發出 Azure PowerShell 命令，此雲端服務 tooinvestigate hello 問題所述，並更正 hello 設定。

### <a name="toomanually-correct-hello-remote-desktop-services-listening-tcp-port"></a>toomanually 正確 hello 遠端桌面服務接聽的 TCP 連接埠
Hello 遠端 Azure PowerShell 工作階段命令提示字元，執行此命令。

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

hello PortNumber 屬性顯示 hello 目前的連接埠號碼。 如有需要請使用此命令變更 hello 遠端桌面連接埠號碼後 tooits 預設值 (為 3389)。

```powershell
Set-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber" -Value 3389
```

確認 hello 連接埠已變更的 too3389 使用這個命令。

```powershell
Get-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name "PortNumber"
```

使用這個命令來結束 hello 遠端的 Azure PowerShell 工作階段。

```powershell
Exit-PSSession
```

請確認該 hello hello Azure VM 的遠端桌面端點也使用 TCP 連接埠 3398 做為其內部的連接埠。 重新啟動 hello Azure VM，然後再試一次 hello 遠端桌面連線。

## <a name="additional-resources"></a>其他資源
[如何 tooreset 密碼或 hello 遠端桌面服務的 Windows 虛擬機器](reset-rdp.md)

[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)

[疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[疑難排解 Azure 虛擬機器上執行的存取 tooan 應用程式](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

