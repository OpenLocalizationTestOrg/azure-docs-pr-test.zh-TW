---
title: "在 Azure 上的 Linux VM 的使用者 tooa aaaAdd |Microsoft 文件"
description: "新增使用者 tooa Linux VM 在 Azure 上。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>新增使用者 tooan Azure VM
Hello 任何新的 Linux VM 上的首要工作之一是 toocreate 新的使用者。  在本文中，我們加入 SSH 公開金鑰，逐步完成建立 sudo 使用者帳戶、 設定 hello 密碼，並用最後`visudo`tooallow sudo，而且沒有密碼。

必要條件： [Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)， [SSH 公用和私用金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、 Azure 資源群組及 hello Azure CLI 安裝，並切換 tooAzure 資源管理員模式下使用`azure config mode arm`。

## <a name="quick-commands"></a>快速命令
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>詳細的逐步解說
### <a name="introduction"></a>簡介
Tooadd 使用者帳戶與新的伺服器 hello 第一個和最常見工作的其中一個。  根登入，應該停用和 hello 根帳戶本身不應搭配您的 Linux 伺服器，只 sudo。  授予使用者根擴大使用 sudo hello 正確方式 tooadminister 並使用 Linux 的權限。

使用 hello 命令`useradd`我們新增使用者帳戶 toohello Linux VM。  執行 `useradd` 來修改 `/etc/passwd`、`/etc/shadow`、`/etc/group` 及 `/etc/gshadow`。  我們要加入命令列的旗標 toohello `useradd` tooalso 新增 hello 新使用者 toohello 適當 sudo 群組在 Linux 上的命令。  即使你`useradd`建立項目加入`/etc/passwd`它並不授予 hello 新的使用者帳戶密碼。  我們會建立使用 hello 簡單 hello 新使用者的初始密碼`passwd`命令。  hello 最後一個步驟是 toomodify hello sudo 規則 tooallow sudo 權限與該使用者 tooexecute 命令而不需要 tooenter 每個命令的密碼。  登入使用 hello 我們假設該使用者帳戶的私密金鑰時，會安全地從不良執行者，而且即將 tooallow sudo 存取權，而且沒有密碼。  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>加入單一 sudo 使用者 tooan Azure VM
登入 toohello 使用 SSH 金鑰的 Azure VM。  如果您尚未設定 SSH 公開金鑰存取權，請先閱讀完這篇文章： [在 Azure 使用公開金鑰驗證](http://link.to/article)。  

hello`useradd`命令完成下列工作的 hello:

* 建立新的使用者帳戶
* 建立新的使用者群組以 hello 相同的名稱
* 太加入空白的項目`/etc/passwd`
* 太加入空白的項目`/etc/gpasswd`

hello`-G`命令列的旗標會加入 hello 新的使用者帳戶 toohello 適當 Linux 群組授予 hello 新的使用者帳戶根擴大的權限。

#### <a name="add-hello-user"></a>新增 hello 使用者
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>設定密碼
hello`useradd`命令建立 hello 使用者，並將項目 tooboth`/etc/passwd`和`/etc/gpasswd`但不會實際設定 hello 密碼。  hello 密碼加入 toohello 項目使用 hello`passwd`命令。

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

我們現在 hello 伺服器上有具有 sudo 權限的使用者。

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>加入 SSH 公開金鑰 toohello 新使用者帳戶
從您的電腦，使用 hello`ssh-copy-id`命令與 hello 新密碼。

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>使用 visudo tooallow sudo 使用方式不需要密碼
使用`visudo`tooedit hello`/etc/sudoers`檔案新增幾個圖層，防範不正確地修改這個重要的檔案。  在執行時`visudo`，hello`/etc/sudoers`檔案已鎖定的 tooensure 沒有其他使用者可以變更正在進行編輯。  hello`/etc/sudoers`檔案也會檢查錯誤的`visudo`當您嘗試 toosave 或結束，所以您無法儲存中斷的 sudoers 的檔案。

我們已經會有 sudo 存取權的 hello 正確的預設群組中的使用者。  現在我們 tooenable 這些群組 toouse sudo，不含密碼。

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>確認 hello 使用者 ssh 金鑰和 sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
