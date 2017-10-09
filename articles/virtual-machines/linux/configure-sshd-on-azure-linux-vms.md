---
title: "aaaConfigure SSHD Azure Linux 虛擬機器上 |Microsoft 文件"
description: "安全性最佳作法和 toolockdown SSH tooAzure Linux 虛擬機器設定 SSHD。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>在 Azure Linux VM 上設定 SSHD

本文示範 toolockdown hello SSH 伺服器在 Linux、 tooprovide 最佳作法安全性以及 toospeed hello SSH 登入程序使用 SSH 金鑰，而不是密碼的方式。  toofurther 鎖定 SSHD 我們 toodisable hello 根使用者不能 toologin，限制 hello 使用者允許 toologin 透過已核准的群組清單中，停用 SSH 通訊協定版本 1、 設定最小金鑰位元，以及設定自動登出閒置的使用者。  這篇文章的 hello 需求： Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和[SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="quick-commands"></a>快速命令

設定`/etc/ssh/sshd_config`以 hello 下列設定：

### <a name="disable-password-logins"></a>停用密碼登入

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>停用 hello 根使用者的登入

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>允許的群組清單

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>允許的使用者清單

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>停用 SSH 通訊協定第 1 版

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>最少金鑰位元數

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>中斷連接閒置使用者

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說

SSHD 是 SSH 伺服器 hello Linux VM 上執行的 hello。  SSH 是從 MacBook 的殼層、Linux 工作站或 Windows 的 Bash 執行的用戶端。  SSH 也是 hello 通訊協定使用 toosecure 和加密 hello 工作站和 hello 進行 SSH 也 VPN （虛擬私人網路） 的 Linux VM 之間的通訊。

本文中，則會是非常重要的 tookeep 單一登入 tooyour Linux VM 開啟 hello 整個逐步解說。  一旦建立 SSH 連線，則仍會保持為開啟的工作階段，只要未關閉 hello 視窗。  具有一個終端機登入，允許的變更進行 toobe toohello SSHD 服務不被鎖定，如果在進行重大變更。  如果您沒有遭到鎖定而無法以中斷 SSHD 設定 Linux VM，Azure 提供 hello 能力 tooreset hello 中斷的 SSHD 組態[Azure VM 存取延伸](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

基於這個理由開啟兩個終端機和 SSH toohello Linux VM 從這兩種。  我們使用 hello 第一個終端機 toomake hello 變更 tooSSHDs 組態檔，然後重新啟動 hello SSHD 服務。  我們使用 hello 第二個終端機 tootest hello 服務重新啟動後，這些變更。  因為我們要停用 SSH 密碼，而且依賴嚴格 SSH 金鑰，如果 SSH 金鑰不正確，而且您關閉 hello 連接 toohello VM，hello VM 將會永久鎖定，且沒有任何人將可以 toologin tooit 需要 toobe 刪除並重新建立。

## <a name="disable-password-logins"></a>停用密碼登入

hello 最快方式 toosecure 您 Linux VM 是 toodisable 密碼登入。  密碼登入啟用時，bot 編目 hello web 會立即開始嘗試 toobrute 會強制使用 SSH Linux vm 的猜測 hello 密碼。  完全停用密碼登入，可讓 hello SSH 伺服器 tooignore 所有密碼登入嘗試。

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>停用 hello 根使用者的登入

下列 Linux 最佳作法，hello`root`使用者應該永遠不會記錄到透過 SSH 或使用`sudo su`。  透過 hello 應該一律執行所有需要根層級權限的命令`sudo`命令，它會記錄所有動作，供日後稽核。  停用 hello`root`從透過 SSH 登入的使用者是安全性最佳作法步驟，以確保只有授權的使用者允許 tooSSH。

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>允許的群組清單

SSH 提供方法來限制允許或不允許透過 SSH 登入的使用者和群組。  這項功能會使用清單 tooapprove，或從登入拒絕特定使用者和群組。  設定 hello 滾輪群組 toohello `AllowGroups` hello 滾輪群組中的 SSH toojust 使用者帳戶清單會限制的已核准的登入。

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>允許的使用者清單

SSH 登入 toojust 使用者限制為更特定的方式 tooaccomplish hello 相同工作`AllowGroups`是。  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>停用 SSH 通訊協定第 1 版

SSH 通訊協定第 1 版不安全，應該停用。  SSH 通訊協定第 2 版是提供安全的方式 tooSSH tooyour 伺服器 hello 目前版本。  停用 SSH 版本 1 拒絕任何嘗試 tooestablish 的 SSH 用戶端連接使用 SSH 版本 1 的 hello SSH 伺服器。  只允許 toonegotiate SSH 第 2 版連接與 hello SSH 伺服器的連線。

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>最少金鑰位元數

遵循安全性最佳作法，會停用密碼 SSH 登入，而只有 SSH 金鑰允許 toobe tooauthenticate 搭配 hello SSH 伺服器。  這些 SSH 金鑰可能以不同長度的金鑰建立 (以位元為單位)。  最佳做法為 2048 位元長度的索引鍵是 hello 最小的可接受索引鍵強度的狀態。  少於 2048 位元的金鑰在理論上會被破解。  設定 hello`ServerKeyBits`太`2048`允許使用金鑰為 2048 位元或更高的任何連線，並拒絕小於 2048 位元的連線。

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>中斷連接閒置使用者

SSH 有擁有已變得讚賞閒置一段指定的秒數已超過的開啟連接的 hello 能力 toodisconnect 使用者。  保持開啟的工作階段 tooonly active 限制 hello 暴露 hello Linux VM 的那些使用者。

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>重新啟動 SSHD

中的 tooenable hello 設定`/etc/ssh/sshd_config`重新啟動重新啟動 hello SSH 伺服器 hello SSHD 處理序。  hello 使用 toorestart hello SSH 伺服器的終端機視窗而不會遺失 hello 開啟 SSH 工作階段維持開啟的。  tootest hello 新 SSH 伺服器設定，請使用第二個終端機視窗或索引標籤。使用不同的終端機 tootest hello SSH 連線可讓您回到 toogo 和進行其他變更 toohello `/etc/ssh/sshd_config` hello 第一個終端機，而不被中斷 SSHD 變更鎖定中。  

### <a name="on-redhat-centos-and-fedora"></a>在 Redhat、Centos 和 Fedora 上

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>在 Debian 和 Ubuntu 上

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>使用 Azure reset-access 重設 SSHD

如果您從重大變更 toohello SSHD 設定鎖定時，您可以使用 hello Azure VM 存取延伸 tooreset hello SSHD configuration 後 toohello 原始設定。

將任何範例名稱換成您自己的名稱。

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>安裝 Fail2ban

強烈建議 tooinstall 及安裝 hello 開放原始碼應用程式 Fail2ban，哪些區塊重複嘗試 toologin tooyour Linux VM 透過 SSH 使用暴力。  Fail2ban 重複的記錄檔無法透過 SSH 嘗試 toologin，，然後建立防火牆規則 hello 嘗試所源自的 tooblock hello IP 位址。

* [Fail2ban 首頁](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>後續步驟

現在，您有設定，並鎖定 hello SSH 伺服器 Linux VM 上有額外的安全性最佳的作法，您可以遵循。  

* [管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [加密使用 Azure CLI hello 的 Linux VM 上的磁碟](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Azure Resource Manager 範本中的存取和安全性](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
