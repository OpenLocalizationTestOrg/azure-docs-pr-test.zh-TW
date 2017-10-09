---
title: "Azure Vm aaaSpecific RDP 的錯誤訊息 |Microsoft 文件"
description: "了解特定的錯誤訊息，您可能會收到時，嘗試在 Azure 中使用遠端桌面連線 tooa Windows 虛擬機器"
keywords: "遠端桌面的錯誤，遠端桌面連線錯誤，無法連接 tooVM，遠端桌面的疑難排解"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 5feb1d64-ee6f-4907-949a-a7cffcbc6153
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8e1551be23e696bd60adbd76c3e1ea86d9dd11aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-specific-rdp-error-messages-tooa-windows-vm-in-azure"></a>疑難排解特定的 RDP 錯誤訊息 tooa Windows Azure 中的 VM
在 Azure 中使用遠端桌面連線 tooa Windows 虛擬機器 (VM) 時，您可能會收到特定的錯誤訊息。 本文詳細說明的某些 hello 較常見的錯誤訊息發生，以及疑難排解步驟 tooresolve 它們。 如果您在連接時發生問題 tooyour VM 不使用 RDP 但發生特定的錯誤訊息，請參閱 hello[疑難排解指南針對遠端桌面](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

如需特定的錯誤訊息資訊，請參閱 hello 下列：

* [hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器的可用 tooprovide 授權](#rdplicense)。
* [遠端桌面找不到 hello 電腦 「 名稱 」](#rdpname)。
* [發生驗證錯誤。hello 本機安全性授權無法連絡](#rdpauth)。
* [Windows 安全性錯誤：您的認證無法運作](#wincred)。
* [這部電腦無法連線遠端電腦的 toohello](#rdpconnect)。

<a id="rdplicense"></a>

## <a name="hello-remote-session-was-disconnected-because-there-are-no-remote-desktop-license-servers-available-tooprovide-a-license"></a>hello 遠端工作階段中斷，因為沒有任何遠端桌面授權伺服器使用 tooprovide 授權。
原因： hello 120 天授權寬限期 hello 遠端桌面伺服器角色已過期，您需要 tooinstall 授權。

因應措施，儲存 hello RDP 檔案的本機副本從 hello 入口網站並執行此命令在 PowerShell 命令提示字元 tooconnect。 此步驟只會停用該連線的授權：

        mstsc <File name>.RDP /admin

如果您實際上不需要超過兩個同時遠端桌面連線 toohello VM，您可以使用伺服器管理員 tooremove hello 遠端桌面伺服器角色。

如需詳細資訊，請參閱 hello 部落格文章[失敗 」 沒有遠端桌面授權伺服器可以使用 「 Azure VM](https://blogs.msdn.microsoft.com/mast/2014/01/21/rdp-to-azure-vm-fails-with-no-remote-desktop-license-servers-available/)。

<a id="rdpname"></a>

## <a name="remote-desktop-cant-find-hello-computer-name"></a>遠端桌面找不到 hello 電腦 「 名稱 」。
原因： hello 遠端桌面用戶端電腦上的無法解析 hello hello 設定 hello RDP 檔案中的 hello 電腦名稱。

可能的解決方案：

* 如果您在組織內部網路上，請確定您的電腦具有存取 toohello proxy 伺服器，並且可以傳送 HTTPS 流量 tooit。
* 如果您使用儲存在本機上的 RDP 檔案，請嘗試使用 hello 一個 hello 入口網站所產生。 這個步驟可確保您擁有 hello 正確的 DNS 名稱 hello 虛擬機器，或 hello 雲端服務和 hello VM hello 端點連接埠。 以下是 hello 入口網站所產生的範例 RDP 檔案：
  
        full address:s:tailspin-azdatatier.cloudapp.net:55919
        prompt for credentials:i:1

具有此 RDP 檔 hello 位址部分：

* hello 完整 hello 包含 hello VM (「 tailspin-azdatatier.cloudapp.net 「 在此範例中) 的雲端服務的網域名稱。
* hello 外部 TCP 連接埠的遠端桌面流量 (55919) hello 端點。

<a id="rdpauth"></a>

## <a name="an-authentication-error-has-occurred-hello-local-security-authority-cannot-be-contacted"></a>發生驗證錯誤。 無法連絡 hello 本機安全性授權。
原因： hello 目標 VM 找不到您的認證 hello 使用者名稱部分中的 hello 安全性授權。

當您的使用者名稱處於 hello 表單*SecurityAuthority*\\*UserName* (範例： CORP\User1)，hello *SecurityAuthority*部分為任一 hello VM（適用於 hello 本機安全性授權） 的電腦名稱或 Active Directory 網域名稱。

可能的解決方案：

* 如果 hello 帳戶是本機 toohello VM，請確定該 hello VM 名稱拼寫正確。
* 如果 hello 帳戶位於 Active Directory 網域，請檢查 hello hello 網域名稱。
* 如果這是 Active Directory 網域帳戶，而且 hello 網域名稱的拼字正確，請確認該網域中的網域控制站為可用。 其為包含網域控制站的 Azure 虛擬網路中常見的問題，網域控制站無法使用的原因是其尚未啟動為因應措施。 您可以使用本機系統管理員帳戶做為因應措施，而非網域帳戶。

<a id="wincred"></a>

## <a name="windows-security-error-your-credentials-did-not-work"></a>Windows 安全性錯誤：您的認證無法運作。
原因： hello 目標 VM 無法驗證您的帳戶名稱和密碼。

Windows 的電腦可以驗證 hello 的本機帳戶或網域帳戶的認證。

* 對於本機帳戶，請使用 hello *ComputerName*\\*UserName*語法 (範例： SQL1\Admin4798)。
* 網域帳戶使用 hello *DomainName*\\*UserName*語法 (範例： CONTOSO\peterodman)。

如果您升級新的 Active Directory 樹系中 VM tooa 網域控制站，會轉換 hello 本機系統管理員帳戶登入的 tooan 對等帳戶以 hello 相同 hello 新樹系和網域中的密碼。 然後刪除 hello 本機帳戶。

例如，如果在 hello 本機帳戶 DC1\DCAdmin，登入，然後為新樹系中的 hello corp.contoso.com 網域的網域控制站升級 hello 虛擬機器 hello 的 DC1\DCAdmin 本機帳戶已刪除和新的網域帳戶 (CORP\DCAdmin) 會透過 hello 相同密碼。

請確定該 hello 帳戶名稱就會確認 hello 虛擬機器可以驗證為有效的帳戶，而且 hello 密碼是正確的名稱。

如果您需要 toochange hello hello 本機系統管理員帳戶密碼，請參閱[tooreset 密碼或 hello 遠端桌面服務的 Windows 虛擬機器的方式](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

<a id="rdpconnect"></a>

## <a name="this-computer-cant-connect-toohello-remote-computer"></a>這部電腦無法連線 toohello 遠端電腦。
原因： 用 tooconnect hello 帳戶並沒有遠端桌面登入權限。

每一部 Windows 電腦有遠端桌面使用者本機群組，其中包含 hello 帳戶和群組，可以從遠端登入它。 Hello 本機 administrators 群組的成員具有存取，即使這些帳戶不會列在 hello 遠端桌面使用者本機群組。 已加入網域的機器，hello 本機 administrators 群組也包含 hello hello 網域的網域系統管理員。

請確定您使用與 tooconnect hello 帳戶具有遠端桌面登入權限。 因應措施是，使用網域或本機系統管理員帳戶 tooconnect 透過遠端桌面。 tooadd hello 所需的帳戶 toohello 遠端桌面使用者本機群組，請使用 hello Microsoft Management Console 嵌入式管理單元 (**系統工具 > 本機使用者和群組 > 群組 > Remote Desktop Users**)。

## <a name="next-steps"></a>後續步驟
如果無這些錯誤發生，而且有未知的問題，與使用 RDP 連線，請參閱 hello[疑難排解指南針對遠端桌面](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

* 如需疑難排解存取 VM 上執行的應用程式的步驟，請參閱[疑難排解存取 tooan 應用程式在 Azure VM 上執行](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
* 如果您有使用安全殼層 (SSH) tooconnect tooa Linux VM 在 Azure 中的問題，請參閱[疑難排解 SSH 連線 tooa 在 Azure 中的 Linux VM](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

