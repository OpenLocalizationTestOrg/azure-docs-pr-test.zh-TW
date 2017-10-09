---
title: "aaaDetailed 步驟 toocreate SSH 金鑰組，在 Azure 中的 Linux Vm 的 |Microsoft 文件"
description: "適用於 Linux Vm 在 Azure 中，瞭解其他步驟 toocreate SSH 公開金鑰和私密金鑰組，以及特定憑證的不同使用案例。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Toocreate 的 SSH 金鑰組和其他 Linux VM 在 Azure 中憑證的詳細的逐步
SSH 金鑰組，您可以預設 toousing SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 上建立虛擬機器。 密碼可以猜到，並開啟 Vm toorelentless 暴力嘗試 tooguess 註冊您的密碼。 Hello Azure CLI 或資源管理員範本所建立的 Vm 可以包含 SSH 公開金鑰 hello 部署中，移除停用 SSH 密碼登入的 post 部署組態步驟的一部分。 針對用於 Linux 虛擬機器之類的憑證，本文提供產生憑證的詳細步驟和其他範例。 如果您想 tooquickly 建立及使用 SSH 金鑰組，請參閱[toocreate SSH 公用和私用金鑰配對適用於 Linux Vm 在 Azure 中的方式](mac-create-ssh-keys.md)。

## <a name="understanding-ssh-keys"></a>了解 SSH 金鑰

使用 SSH 公開金鑰和私密金鑰的金鑰是 hello 最簡單方式 toolog tooyour Linux 伺服器中。 [公開金鑰加密](https://en.wikipedia.org/wiki/Public-key_cryptography)比密碼，可以是暴力密碼破解強制更輕鬆地提供更安全的方式 toolog tooyour Linux 中或在 Azure 中的 BSD VM。

公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。  hello SSH 私密金鑰應有[非常安全的密碼](https://www.xkcd.com/936/)(來源：[xkcd.com](https://xkcd.com)) toosafeguard 它。  此密碼是只 tooaccess hello 私用 SSH 金鑰檔案並**不**hello 使用者帳戶密碼。  當您新增密碼 tooyour SSH 金鑰時，它 hello 私密金鑰加密使用 128 位元 AES 使 hello 私用金鑰變成毫無用處，而不 hello 密碼 toodecrypt 它。  如果攻擊者偷走了您的私密金鑰，且索引鍵沒有密碼，其方式是根據可以 toouse，私用金鑰 toolog tooany 伺服器具有 hello 對應的公開金鑰。  如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。

這篇文章建立 SSH 通訊協定版本 2 RSA 公用和私用金鑰的檔案組 （也參考的 tooas"ssh rsa"索引鍵），這建議用於部署與 Azure 資源管理員。 *ssh rsa* hello 上需要索引鍵[入口網站](https://portal.azure.com)傳統和資源管理員部署。

## <a name="ssh-keys-use-and-benefits"></a>SSH 金鑰的使用和好處

Azure 需要有至少 2048年位元，SSH 通訊協定第 2 版 RSA 格式公用和私用金鑰。hello 公開金鑰檔案具有 hello`.pub`容器格式。 toocreate hello 索引鍵使用`ssh-keygen`，這會要求一系列的問題，並再將私用金鑰和對應的公開金鑰。 建立 Azure VM 時，Azure 複本 hello 公用金鑰 toohello `~/.ssh/authorized_keys` hello VM 上的資料夾。 SSH 金鑰在`~/.ssh/authorized_keys`會使用的 toochallenge hello 用戶端 toomatch hello 對應的私密金鑰上 SSH 登入連線。  Azure Linux VM 建立時使用 SSH 金鑰進行驗證，Azure 會設定 hello SSHD 伺服器 toonot 允許密碼登入，則只有 SSH 金鑰。  因此，藉由使用 SSH 金鑰建立 Azure Linux Vm，您可以協助保護 hello VM 部署，並儲存您自己的停用密碼的 hello hello 一般的部署後設定步驟**sshd_config**檔案。

## <a name="using-ssh-keygen"></a>使用 ssh-keygen

此命令會建立保護 （加密） 使用 2048年位元 RSA 的 SSH 金鑰組的密碼，而且它會取消註 tooeasily 識別它。  

SSH 金鑰依預設，會保留在 hello`~/.ssh`目錄。  如果您不需要`~/.ssh`目錄、 hello`ssh-keygen`命令就會為您建立以 hello 正確的權限。

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*命令的說明*

`ssh-keygen`= hello 用程式 toocreate hello 金鑰

`-t rsa`= 索引鍵 toocreate hello RSA 格式 [維基百科] 的型別[括弧結尾](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
 `-b 2048` = 位元的 hello 金鑰

`-C "azureuser@myserver"`= 附加的 toohello 結尾 hello 公開金鑰檔案 tooeasily 識別該註解。  通常一封電子郵件做為 hello 註解，但您可以使用任何最適合您的基礎結構。

## <a name="classic-deploy-using-asm"></a>使用 `asm` 進行傳統部署

如果您使用 hello 傳統部署模型 (`asm` hello CLI 中的模式)，您可以使用 SSH RSA 公開金鑰或 RFC4716 格式化的 pem 容器中的索引鍵。  hello SSH RSA 公開金鑰是稍早在此發行項使用中已建立的內容`ssh-keygen`。

toocreate RFC4716 格式化從現有的 SSH 公開金鑰的金鑰：

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen 的範例

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

已儲存金鑰檔案：

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

這個發行項的 hello 金鑰組名稱。  具有名為的金鑰組**id_rsa**是 hello 預設值，而且某些工具可能預期 hello **id_rsa**私密金鑰檔案名稱，因此保留其中一個是個不錯的主意。 hello 目錄`~/.ssh/`是 hello SSH 金鑰組和 hello SSH 組態檔的預設位置。  如果未指定具有完整路徑， `ssh-keygen` hello 的目前工作目錄，而不是 hello 預設中建立 hello 金鑰`~/.ssh`。

Hello 清單`~/.ssh`目錄。

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

金鑰密碼︰

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`指 hello 私密金鑰檔案的 tooa 密碼是做為 「 複雜密碼。 」  它是*強*建議 tooadd 密碼 tooyour 私用金鑰。 不使用密碼保護 hello 金鑰檔案，與 hello 檔案的任何人都可以使用它 toolog tooany 伺服器具有 hello 對應的公開金鑰。 新增密碼 （複雜） 提供更多的保護，以防其他人可以 toogain 存取 tooyour 私密金鑰檔案，提供您時間 toochange hello 索引鍵用於 tooauthenticate 您。

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>使用 ssh 代理 toostore 私用金鑰密碼

tooavoid 輸入私密金鑰檔案密碼的每一個 SSH 登入，您可以使用`ssh-agent`toocache 您私密金鑰檔案的密碼。 如果您使用的 Mac，hello OSX Keychain 會安全地儲存 hello 私用金鑰的密碼當您叫用`ssh-agent`。

驗證及使用 ssh 代理程式並 ssh-加入 hello 金鑰檔案的相關 tooinform hello SSH 系統以便 hello 複雜密碼不需要以互動方式使用 toobe。

```bash
eval "$(ssh-agent -s)"
```

現在，加入 hello 私密金鑰太`ssh-agent`使用 hello 命令`ssh-add`。

```bash
ssh-add ~/.ssh/id_rsa
```

hello 私密金鑰密碼現在儲存在`ssh-agent`。

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>使用`ssh-copy-id`toocopy hello 金鑰 tooan 現有的 VM
如果您已經建立 VM，您就可以安裝 hello 新 SSH 公用金鑰 tooyour Linux VM 使用：

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>建立和設定 SSH 組態檔

它是建議的最佳作法 toocreate 及設定`~/.ssh/config`向上檔案 toospeed 登入並最佳化您的 SSH 用戶端行為。

下列範例中的 hello 顯示標準的設定。

### <a name="create-hello-file"></a>建立 hello 檔案

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>編輯 hello 檔案 tooadd hello 新 SSH 組態：

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>範例 `~/.ssh/config` 檔案︰

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

這的 SSH 組態讓您區段的每個伺服器 tooenable 每個 toohave 自己專用的金鑰組。 hello 預設設定 (`Host *`)，適用於不符合任何 hello 特定主機的高的層級 hello 設定檔中的任何主機。

### <a name="config-file-explained"></a>組態檔的說明

`Host`= hello hello 主機上呼叫 hello 終端機名稱。  `ssh fedora22`會告知`SSH`toouse 標示為 hello settings 區塊中的 hello 值`Host fedora22`附註： 主機可供您使用的邏輯，且不代表 hello 的任何伺服器的實際主機名稱的任何標籤。

`Hostname 102.160.203.241`= hello IP 位址或 DNS 名稱而存取的 hello 伺服器。

`User ahmet`登入時 toohello server = hello 遠端使用者帳戶 toouse。

`PubKeyAuthentication yes`= 告訴 SSH 想 toouse SSH 金鑰 toolog 中。

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH 私密金鑰與對應公用金鑰 toouse 進行驗證。

## <a name="ssh-into-linux-without-a-password"></a>使用 SSH 登入 Linux 而不提供密碼

現在您擁有的 SSH 金鑰組與設定的 SSH 組態檔，您就可以 toolog tooyour Linux VM 中的快速且安全的方式。 hello 第一次登入使用 SSH 金鑰 hello 命令提示字元 tooa 伺服器您 hello 複雜密碼，該金鑰的檔案。

```bash
ssh fedora22
```

### <a name="command-explained"></a>命令的說明

當`ssh fedora22`執行 SSH 先找出並載入任何設定，從 hello`Host fedora22`區塊，然後按一下 所有 hello 剩餘 hello 最後一個區塊中，從設定載入`Host *`。

## <a name="next-steps"></a>後續步驟

接下來向上 toocreate Azure Linux Vm 使用 hello 新 SSH 公開金鑰。  SSH 公開金鑰為 hello 登入，以建立 azure Vm 是比較安全比 hello 預設登入方法，密碼建立的 Vm。  使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。

* [使用 Azure 範本建立安全的 Linux VM](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [建立安全的 Linux VM，使用 hello Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [建立安全的 Linux VM，使用 Azure CLI hello](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
