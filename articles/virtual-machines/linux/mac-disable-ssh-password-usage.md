---
title: "藉由設定 SSHD Linux VM 上的 aaaDisable SSH 密碼 |Microsoft 文件"
description: "藉由停用 SSH 的密碼登入來保護 Azure 上的 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>藉由設定 SSHD 停用 Linux VM 上的 SSH 密碼
本文著重在如何 toolock 向您的 Linux VM 的 hello 登入安全性。  只要開啟 SSH 連接埠 22 hello toohello 世界 bot 啟動 toologin 嘗試猜測的密碼。  在本中，我們將停用經由 SSH 的密碼登入。  完全移除 hello 能力 toouse 我們從這種類型的暴力密碼破解保護 hello Linux VM 的密碼會強制攻擊。  hello 加入額外的好處是我們將會設定 Linux SSHD tooonly 允許透過 SSH 公用與私用金鑰的登入到目前為止 hello 最安全的方式 toologin tooLinux。  hello 可能組合，它需要 tooguess hello 私密金鑰非常龐大，以及因此阻止 bot 從甚至終究 tootry toobrute 強制 SSH 金鑰。

## <a name="goals"></a>目標
* 設定 SSHD toodisallow:
  * 密碼登入
  * 根使用者登入
  * 挑戰回應驗證
* 設定 SSHD tooallow:
  * 僅限 SSH 金鑰登入
* 在登入的情況下重新啟動 SSHD
* 測試 hello 新 SSHD 組態

## <a name="introduction"></a>簡介
[SSH 定義](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD 是 SSH 伺服器 hello Linux VM 上執行的 hello。  SSH 是從 MacBook 或 Linux 工作站之殼層執行的用戶端。  SSH 也是 hello 通訊協定使用 toosecure 和加密 hello 工作站和 hello Linux VM 之間的通訊。

這篇文章則是非常重要的 tookeep Linux VM 開啟以供整個 hello 逐步執行一個登入 tooyour。  因此我們會從這兩種開啟兩個終端機和 SSH toohello Linux VM。  我們將使用 hello 第一個終端機 toomake hello 變更 tooSSHDs 組態檔，並重新啟動 hello SSHD 服務。  我們將使用 hello 第二個終端機 tootest hello 服務重新啟動後，這些變更。  因為我們要停用 SSH 密碼，而且依賴嚴格 SSH 金鑰，如果 SSH 金鑰不正確，而且您關閉 hello 連接 toohello VM，hello VM 將會永久鎖定，且沒有任何人將可以 toologin tooit 需要 toobe 刪除並重新建立。

## <a name="prerequisites"></a>必要條件
* [在 Linux 和 Mac 上為 Azure 中的 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure 帳戶
  * [註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure 入口網站](http://portal.azure.com)
* 在 Azure 上執行的 Linux VM
* `~/.ssh/` 中的 SSH 公開和私密金鑰組
* 中的 SSH 公開金鑰`~/.ssh/authorized_keys`hello Linux VM 上
* Hello VM Sudo 權限
* 連接埠 22 開啟

## <a name="quick-commands"></a>快速命令
*從這裡開始經驗豐富的 Linux 系統管理員只是想 hello TLDR 版本。每個人都想 hello 詳細的說明並逐步執行略過本節。*

```bash
sudo vim /etc/ssh/sshd_config
```

編輯 hello 設定檔，如下所示：

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

重新啟動 hello SSHD 服務。 在以 Debian 為基礎的散發套件︰

```bash
sudo service ssh restart
```

在以 Red Hat 為基礎的散發套件︰

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>詳細的逐步解說
登入 toohello Linux VM 上終端機 1 (T1)。  登入 toohello Linux VM 上終端機 2 (T2)。

在 T2 我們 tooedit hello SSHD 組態檔。  

```bash
sudo vim /etc/ssh/sshd_config
```

從這裡，我們會編輯只 hello 設定 toodisable 密碼，並啟用 SSH 金鑰的登入。  有許多的設定，您應該研究並變更 toomake Linux SSH 安全您需要此檔案中。

#### <a name="disable-password-logins"></a>停用密碼登入

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>啟用公開金鑰驗證

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>停用根登入

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>停用挑戰回應驗證
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>重新啟動 SSHD
從 hello T1 殼層，請確認您仍登入。  這個步驟非常重要，由於我們已停用密碼，這樣做能避免 SSH 金鑰不正確時 VM 遭到鎖定。  如果任何設定不正確，您仍可登入以及 SSH 會保持 hello 連線運作 hello SSHD 服務期間，您可以使用 T1 toofix sshd_config Linux VM 上重新啟動。

從 T2 執行︰

##### <a name="on-hello-debian-family"></a>在 hello Debian 系列
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>在 hello RedHat 系列
```bash
sudo service sshd restart
```

VM 上的密碼現已停用，如此將能避免暴力破解密碼的登入嘗試。  只有 SSH 金鑰允許您將無法 toologin 更快且更安全。

