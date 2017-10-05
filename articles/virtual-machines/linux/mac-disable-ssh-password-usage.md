---
title: "藉由設定 SSHD 停用 Linux VM 上的 SSH 密碼 | Microsoft Docs"
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
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>藉由設定 SSHD 停用 Linux VM 上的 SSH 密碼
本文著重於如何鎖定 Linux VM 的登入安全性。  一旦對外開放 SSH 連接埠 22，bot 便會開始藉由猜測密碼來嘗試登入。  在本中，我們將停用經由 SSH 的密碼登入。  透過完全移除使用密碼的能力，我們能避免 Linux VM 遭受這種暴力密碼破解攻擊。  這種做法還有額外的優點，我們會將 Linux SSHD 設定為只允許透過 SSH 公開和私密金鑰登入，而這是目前最安全的 Linux 登入方法。  由於可能的私密金鑰組合千變萬化，若要在這種情況下猜測，即使利用 bot 來嘗試暴力破解 SSH 金鑰也無濟於事。

## <a name="goals"></a>目標
* 設定 SSHD 以禁止：
  * 密碼登入
  * 根使用者登入
  * 挑戰回應驗證
* 設定 SSHD 以允許：
  * 僅限 SSH 金鑰登入
* 在登入的情況下重新啟動 SSHD
* 測試新 SSHD 組態

## <a name="introduction"></a>簡介
[SSH 定義](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD 是在 Linux VM 上執行的 SSH 伺服器。  SSH 是從 MacBook 或 Linux 工作站之殼層執行的用戶端。  SSH 也是用來保護及加密工作站與 Linux VM 之通訊的通訊協定。

在本文中，請務必開放一個 Linux VM 的登入，讓整個逐步解說得以順暢進行。  有鑑於此，我們將會開啟兩個終端機，並從兩者開啟 Linux VM 的 SSH。  我們將使用第一個終端機來變更 SSHD 組態檔，以及重新啟動 SSHD 服務。  等到服務重新啟動後，我們將使用第二個終端機來測試這些變更。  由於我們要停用 SSH 密碼並重度依賴 SSH 金鑰，所以如果您的 SSH 金鑰不正確而您關閉 VM 連線，VM 將永久遭到鎖定，而且沒有人能夠登入。如此一來，您只能將它刪除後再重新建立。

## <a name="prerequisites"></a>必要條件
* [在 Linux 和 Mac 上為 Azure 中的 Linux VM 建立 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Azure 帳戶
  * [註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/)
  * [Azure 入口網站](http://portal.azure.com)
* 在 Azure 上執行的 Linux VM
* `~/.ssh/` 中的 SSH 公開和私密金鑰組
* Linux VM 之 `~/.ssh/authorized_keys` 中的 SSH 公開金鑰
* VM 上的 sudo 權限
* 連接埠 22 開啟

## <a name="quick-commands"></a>快速命令
只需要 TLDR 版本的資深 Linux 系統管理員可以從這裡開始。其他需要詳細說明和逐步解說的使用者請略過本節。

```bash
sudo vim /etc/ssh/sshd_config
```

編輯組態檔，如下所示：

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

重新啟動 SSHD 服務。 在以 Debian 為基礎的散發套件︰

```bash
sudo service ssh restart
```

在以 Red Hat 為基礎的散發套件︰

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>詳細的逐步解說
在終端機 1 (T1) 上登入 Linux VM。  在終端機 2 (T2) 上登入 Linux VM。

我們要在 T2 上編輯 SSHD 組態檔。  

```bash
sudo vim /etc/ssh/sshd_config
```

在這裡，我們只會編輯設定來停用密碼，以及啟用 SSH 金鑰登入。  這個檔案中有許多值得研究及變更的設定，它們能讓 Linux 和 SSH 的安全性符合您的需求。

#### <a name="disable-password-logins"></a>停用密碼登入

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>啟用公開金鑰驗證

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>停用根登入

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>停用挑戰回應驗證
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>重新啟動 SSHD
從 T1 殼層驗證您是否保持登入。  這個步驟非常重要，由於我們已停用密碼，這樣做能避免 SSH 金鑰不正確時 VM 遭到鎖定。  如果 Linux VM 上有任何不正確的設定，您可以使用 T1 來修正 sshd_config，因為您仍然保持登入狀態，而且 SSH 會在 SSHD 服務重新啟動期間維持連線。

從 T2 執行︰

##### <a name="on-the-debian-family"></a>在 Debian 系列上
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a>在 RedHat 系列上
```bash
sudo service sshd restart
```

VM 上的密碼現已停用，如此將能避免暴力破解密碼的登入嘗試。  由於我們只允許 SSH 金鑰，您將可以利用更快速、更安全的方式登入。

