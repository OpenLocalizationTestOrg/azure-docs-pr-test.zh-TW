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
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="efb5a-103">藉由設定 SSHD 停用 Linux VM 上的 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="efb5a-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="efb5a-104">本文著重在如何 toolock 向您的 Linux VM 的 hello 登入安全性。</span><span class="sxs-lookup"><span data-stu-id="efb5a-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="efb5a-105">只要開啟 SSH 連接埠 22 hello toohello 世界 bot 啟動 toologin 嘗試猜測的密碼。</span><span class="sxs-lookup"><span data-stu-id="efb5a-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="efb5a-106">在本中，我們將停用經由 SSH 的密碼登入。</span><span class="sxs-lookup"><span data-stu-id="efb5a-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="efb5a-107">完全移除 hello 能力 toouse 我們從這種類型的暴力密碼破解保護 hello Linux VM 的密碼會強制攻擊。</span><span class="sxs-lookup"><span data-stu-id="efb5a-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="efb5a-108">hello 加入額外的好處是我們將會設定 Linux SSHD tooonly 允許透過 SSH 公用與私用金鑰的登入到目前為止 hello 最安全的方式 toologin tooLinux。</span><span class="sxs-lookup"><span data-stu-id="efb5a-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="efb5a-109">hello 可能組合，它需要 tooguess hello 私密金鑰非常龐大，以及因此阻止 bot 從甚至終究 tootry toobrute 強制 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="efb5a-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="efb5a-110">目標</span><span class="sxs-lookup"><span data-stu-id="efb5a-110">Goals</span></span>
* <span data-ttu-id="efb5a-111">設定 SSHD toodisallow:</span><span class="sxs-lookup"><span data-stu-id="efb5a-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="efb5a-112">密碼登入</span><span class="sxs-lookup"><span data-stu-id="efb5a-112">Password logins</span></span>
  * <span data-ttu-id="efb5a-113">根使用者登入</span><span class="sxs-lookup"><span data-stu-id="efb5a-113">Root user login</span></span>
  * <span data-ttu-id="efb5a-114">挑戰回應驗證</span><span class="sxs-lookup"><span data-stu-id="efb5a-114">Challenge-response authentication</span></span>
* <span data-ttu-id="efb5a-115">設定 SSHD tooallow:</span><span class="sxs-lookup"><span data-stu-id="efb5a-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="efb5a-116">僅限 SSH 金鑰登入</span><span class="sxs-lookup"><span data-stu-id="efb5a-116">only SSH key logins</span></span>
* <span data-ttu-id="efb5a-117">在登入的情況下重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="efb5a-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="efb5a-118">測試 hello 新 SSHD 組態</span><span class="sxs-lookup"><span data-stu-id="efb5a-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="efb5a-119">簡介</span><span class="sxs-lookup"><span data-stu-id="efb5a-119">Introduction</span></span>
[<span data-ttu-id="efb5a-120">SSH 定義</span><span class="sxs-lookup"><span data-stu-id="efb5a-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="efb5a-121">SSHD 是 SSH 伺服器 hello Linux VM 上執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="efb5a-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="efb5a-122">SSH 是從 MacBook 或 Linux 工作站之殼層執行的用戶端。</span><span class="sxs-lookup"><span data-stu-id="efb5a-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="efb5a-123">SSH 也是 hello 通訊協定使用 toosecure 和加密 hello 工作站和 hello Linux VM 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="efb5a-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="efb5a-124">這篇文章則是非常重要的 tookeep Linux VM 開啟以供整個 hello 逐步執行一個登入 tooyour。</span><span class="sxs-lookup"><span data-stu-id="efb5a-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="efb5a-125">因此我們會從這兩種開啟兩個終端機和 SSH toohello Linux VM。</span><span class="sxs-lookup"><span data-stu-id="efb5a-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="efb5a-126">我們將使用 hello 第一個終端機 toomake hello 變更 tooSSHDs 組態檔，並重新啟動 hello SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="efb5a-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="efb5a-127">我們將使用 hello 第二個終端機 tootest hello 服務重新啟動後，這些變更。</span><span class="sxs-lookup"><span data-stu-id="efb5a-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="efb5a-128">因為我們要停用 SSH 密碼，而且依賴嚴格 SSH 金鑰，如果 SSH 金鑰不正確，而且您關閉 hello 連接 toohello VM，hello VM 將會永久鎖定，且沒有任何人將可以 toologin tooit 需要 toobe 刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="efb5a-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efb5a-129">必要條件</span><span class="sxs-lookup"><span data-stu-id="efb5a-129">Prerequisites</span></span>
* [<span data-ttu-id="efb5a-130">在 Linux 和 Mac 上為 Azure 中的 Linux VM 建立 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="efb5a-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="efb5a-131">Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="efb5a-131">Azure account</span></span>
  * [<span data-ttu-id="efb5a-132">註冊免費試用版</span><span class="sxs-lookup"><span data-stu-id="efb5a-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="efb5a-133">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="efb5a-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="efb5a-134">在 Azure 上執行的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="efb5a-134">Linux VM running on azure</span></span>
* <span data-ttu-id="efb5a-135">`~/.ssh/` 中的 SSH 公開和私密金鑰組</span><span class="sxs-lookup"><span data-stu-id="efb5a-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="efb5a-136">中的 SSH 公開金鑰`~/.ssh/authorized_keys`hello Linux VM 上</span><span class="sxs-lookup"><span data-stu-id="efb5a-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="efb5a-137">Hello VM Sudo 權限</span><span class="sxs-lookup"><span data-stu-id="efb5a-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="efb5a-138">連接埠 22 開啟</span><span class="sxs-lookup"><span data-stu-id="efb5a-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="efb5a-139">快速命令</span><span class="sxs-lookup"><span data-stu-id="efb5a-139">Quick Commands</span></span>
<span data-ttu-id="efb5a-140">*從這裡開始經驗豐富的 Linux 系統管理員只是想 hello TLDR 版本。每個人都想 hello 詳細的說明並逐步執行略過本節。*</span><span class="sxs-lookup"><span data-stu-id="efb5a-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="efb5a-141">編輯 hello 設定檔，如下所示：</span><span class="sxs-lookup"><span data-stu-id="efb5a-141">Edit hello config file as follows:</span></span>

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

<span data-ttu-id="efb5a-142">重新啟動 hello SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="efb5a-142">Restart hello SSHD service.</span></span> <span data-ttu-id="efb5a-143">在以 Debian 為基礎的散發套件︰</span><span class="sxs-lookup"><span data-stu-id="efb5a-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="efb5a-144">在以 Red Hat 為基礎的散發套件︰</span><span class="sxs-lookup"><span data-stu-id="efb5a-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="efb5a-145">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="efb5a-145">Detailed Walk Through</span></span>
<span data-ttu-id="efb5a-146">登入 toohello Linux VM 上終端機 1 (T1)。</span><span class="sxs-lookup"><span data-stu-id="efb5a-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="efb5a-147">登入 toohello Linux VM 上終端機 2 (T2)。</span><span class="sxs-lookup"><span data-stu-id="efb5a-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="efb5a-148">在 T2 我們 tooedit hello SSHD 組態檔。</span><span class="sxs-lookup"><span data-stu-id="efb5a-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="efb5a-149">從這裡，我們會編輯只 hello 設定 toodisable 密碼，並啟用 SSH 金鑰的登入。</span><span class="sxs-lookup"><span data-stu-id="efb5a-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="efb5a-150">有許多的設定，您應該研究並變更 toomake Linux SSH 安全您需要此檔案中。</span><span class="sxs-lookup"><span data-stu-id="efb5a-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="efb5a-151">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="efb5a-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="efb5a-152">啟用公開金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="efb5a-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="efb5a-153">停用根登入</span><span class="sxs-lookup"><span data-stu-id="efb5a-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="efb5a-154">停用挑戰回應驗證</span><span class="sxs-lookup"><span data-stu-id="efb5a-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="efb5a-155">重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="efb5a-155">Restart SSHD</span></span>
<span data-ttu-id="efb5a-156">從 hello T1 殼層，請確認您仍登入。</span><span class="sxs-lookup"><span data-stu-id="efb5a-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="efb5a-157">這個步驟非常重要，由於我們已停用密碼，這樣做能避免 SSH 金鑰不正確時 VM 遭到鎖定。</span><span class="sxs-lookup"><span data-stu-id="efb5a-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="efb5a-158">如果任何設定不正確，您仍可登入以及 SSH 會保持 hello 連線運作 hello SSHD 服務期間，您可以使用 T1 toofix sshd_config Linux VM 上重新啟動。</span><span class="sxs-lookup"><span data-stu-id="efb5a-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="efb5a-159">從 T2 執行︰</span><span class="sxs-lookup"><span data-stu-id="efb5a-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="efb5a-160">在 hello Debian 系列</span><span class="sxs-lookup"><span data-stu-id="efb5a-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="efb5a-161">在 hello RedHat 系列</span><span class="sxs-lookup"><span data-stu-id="efb5a-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="efb5a-162">VM 上的密碼現已停用，如此將能避免暴力破解密碼的登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="efb5a-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="efb5a-163">只有 SSH 金鑰允許您將無法 toologin 更快且更安全。</span><span class="sxs-lookup"><span data-stu-id="efb5a-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

