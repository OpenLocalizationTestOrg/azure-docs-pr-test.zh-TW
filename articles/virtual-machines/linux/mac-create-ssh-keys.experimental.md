---
title: "aaaCreate SSH 金鑰組，適用於 Linux Vm 在 Azure 上 |Microsoft 文件"
description: "安全地建立 Azure Linux VM 的 SSH 公開和私密金鑰組。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a>建立 Linux VM 的 SSH 公用和私用金鑰組

本文章將示範如何 toogenerate SSH 通訊協定第 2 版 RSA 公用和私用金鑰檔案對 toouse 使用 Linux Vm。  SSH 金鑰組，您可以預設 toousing SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 上建立虛擬機器。  密碼可以猜到，並開啟 Vm toorelentless 暴力嘗試 tooguess 註冊您的密碼。 建立與 Azure 範本或 hello Vm`azure-cli`可以包含 SSH 公開金鑰，做為 hello 部署中，移除停用 SSH 密碼登入的 post 部署組態步驟的一部分。

## <a name="quick-commands"></a>快速命令

執行 hello Bash 殼層中的下列命令，以自己選擇取代 hello 範例。

SSH 公開金鑰檔預設會建立在 `~/.ssh/id_rsa.pub`。 當系統提示您使用下列命令的 hello，您應該建立 「 複雜密碼 」 toosecure 您的私密金鑰。 （hello 複雜密碼是使用密碼 tooencrypt 您的私密金鑰）。

```bash
ssh-keygen -t rsa -b 2048 
```

加入新建立的 hello 金鑰太`ssh-agent`:

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> hello Linux 作業系統的幾乎所有的發佈，在上述命令但不是一定能在容器中，做為 hello 環境可以徹底條件約束。 

## <a name="detailed-walkthrough"></a>詳細的逐步解說

使用 SSH 公開金鑰和私密金鑰的金鑰是 hello 最簡單方式 toolog tooyour Linux 伺服器中。 [公開金鑰加密](https://en.wikipedia.org/wiki/Public-key_cryptography)比密碼，可以是暴力密碼破解強制更輕鬆地提供更安全的方式 toolog tooyour Linux 中或在 Azure 中的 BSD VM。

> [!IMPORTANT]
> 公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。  hello SSH 私密金鑰應有[非常安全的密碼](https://www.xkcd.com/936/)(來源：[xkcd.com](https://xkcd.com)) toosafeguard 它。  此密碼是只 tooaccess hello SSH 私密金鑰和**不**hello 使用者帳戶密碼。  當您新增密碼 tooyour SSH 金鑰時，它 hello 私密金鑰加密使用 128 位元 AES 使 hello 私用金鑰變成毫無用處，而不 hello 密碼 toodecrypt 它。  如果攻擊者偷走了您的私密金鑰，且索引鍵沒有密碼，其方式是根據可以 toouse，私用金鑰 toolog tooany 伺服器具有 hello 對應的公開金鑰。  如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。

這篇文章建立 SSH 通訊協定版本 2 RSA 公用和私密金鑰檔案，這建議的作法 hello 資源管理員的部署。  *ssh rsa* hello 上需要索引鍵[入口網站](https://portal.azure.com)傳統和資源管理員部署。

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a>藉由設定 SSH 金鑰來停用 SSH 密碼

Azure 需要至少 2048 位元的 ssh-rsa 格式公開和私密金鑰。 toocreate hello 索引鍵使用`ssh-keygen`，這會要求一系列的問題，並再將私用金鑰和對應的公開金鑰。 建立 Azure VM 時，會太複製 hello 公開金鑰`~/.ssh/authorized_keys`。  SSH 金鑰在`~/.ssh/authorized_keys`會使用的 toochallenge hello 用戶端 toomatch hello 對應的私密金鑰上 SSH 登入連線。  Azure Linux VM 建立時使用 SSH 金鑰進行驗證，Azure 會設定 hello SSHD 伺服器 toonot 允許密碼登入，則只有 SSH 金鑰。  因此，您可以藉由使用 SSH 金鑰建立 Azure Linux Vm，協助安全 hello VM 部署及儲存自行停用密碼 hello sshd_config 組態檔中的 hello 一般的部署後設定步驟。

## <a name="using-ssh-keygen"></a>使用 ssh-keygen

此命令會建立保護 （加密） 使用 2048年位元 RSA 的 SSH 金鑰組的密碼，而且它會取消註 tooeasily 識別它。  

SSH 金鑰依預設，會保留在 hello`~/.ssh`目錄。  如果您不需要`~/.ssh`目錄、 hello`ssh-keygen`命令就會為您建立以 hello 正確的權限。

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

*命令的說明*

`ssh-keygen`= hello 用程式 toocreate hello 金鑰

`-t rsa`= 索引鍵 toocreate hello RSA 格式的類型 [維基百科](https://en.wikipedia.org/wiki/RSA_(cryptosystem)

`-b 2048`= 位元的 hello 金鑰


## <a name="classic-portal-and-x509-certs"></a>傳統入口網站和 X.509 憑證

如果您使用 hello Azure[傳統入口網站](https://manage.windowsazure.com/)，hello SSH 金鑰需要 X.509 憑證。  不允許任何其他類型的 SSH 公開金鑰，而「必須」是 X.509 憑證。

toocreate 從您現有的 SSH RSA 私密金鑰的 X.509 憑證：

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a>使用 `asm` 進行傳統部署

如果您使用 hello 傳統部署模型 (Azure 服務管理 CLI `asm`)，您可以使用 SSH RSA 公開金鑰或 RFC4716 格式中的索引鍵**.pem**容器。  hello SSH RSA 公開金鑰是稍早在此發行項使用中已建立的內容`ssh-keygen`。

toocreate RFC4716 格式化從現有的 SSH 公開金鑰的金鑰：

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>ssh-keygen 的範例

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

這個發行項的 hello 金鑰組名稱。  具有名為的金鑰組**id_rsa**是 hello 預設值，而且某些工具可能預期 hello **id_rsa**私密金鑰檔案名稱，因此保留其中一個是個不錯的主意。 hello 目錄`~/.ssh/`是 hello SSH 金鑰組和 hello SSH 組態檔的預設位置。  如果未指定具有完整路徑，`ssh-keygen`將 hello 目前工作目錄中建立 hello 金鑰、 不 hello 預設`~/.ssh`。

Hello 清單`~/.ssh`目錄。

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

金鑰密碼︰

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`參考 tooa 用密碼 tooencrypt hello 私用金鑰做為 「 複雜密碼。 」  它是*強*建議 tooadd 複雜密碼 tooyour 金鑰組。 不需要複雜密碼保護 hello 私用金鑰，與 hello 金鑰檔案的任何人都可以使用它 toolog tooany server 中具有 hello 對應的公開金鑰。 加入複雜密碼提供更多的保護，以防其他人可以 toogain 存取 tooyour 私密金鑰檔案，讓您時間 toochange hello 索引鍵用於 tooauthenticate 您。

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>使用 ssh 代理 toostore 私用金鑰密碼

tooavoid 輸入您的私密金鑰檔案的複雜密碼與每個 SSH 登入，您可以使用`ssh-agent`toocache 您私密金鑰檔案的密碼。 如果您使用的 Mac，hello OSX Keychain 會安全地儲存 hello 私用金鑰的密碼當您叫用`ssh-agent`。

驗證並使用`ssh-agent`和`ssh-add`tooinform hello SSH hello 金鑰檔案的相關的系統，以便 hello 複雜密碼不需要以互動方式使用 toobe。

```bash
eval "$(ssh-agent -s)"
```

現在，加入 hello 私密金鑰太`ssh-agent`使用 hello 命令`ssh-add`。

```bash
ssh-add ~/.ssh/id_rsa
```

hello 私密金鑰密碼現在儲存在`ssh-agent`。

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a>使用`ssh-copy-id`tooinstall hello 新金鑰
如果您已經建立 VM 您可以使用下列命令，以您自己的值取代 hello VM 使用者名稱和 hello 伺服器位址的 hello 安裝 hello 新 SSH 公用金鑰 tooyour Linux VM:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>建立和設定 SSH 組態檔

它是最佳的作法 toocreate 及設定`~/.ssh/config`向上檔案 toospeed 登入並最佳化您的 SSH 用戶端行為。

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

接下來向上 toocreate Azure Linux Vm 使用 hello 新 SSH 公開金鑰。  SSH 公開金鑰為 hello 登入，以建立 azure Vm 是比較安全比 hello 預設登入方法，密碼建立的 Vm。  使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。 如果您需要更多協助建立您的 SSH 金鑰組，或需要其他憑證，例如，針對搭配 hello 傳統入口網站，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。

* [使用 Azure 範本建立安全的 Linux VM](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [建立安全的 Linux VM，使用 hello Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [建立安全的 Linux VM，使用 Azure CLI hello](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
