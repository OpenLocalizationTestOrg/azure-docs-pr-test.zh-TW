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
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="03486-103">藉由設定 SSHD 停用 Linux VM 上的 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="03486-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="03486-104">本文著重於如何鎖定 Linux VM 的登入安全性。</span><span class="sxs-lookup"><span data-stu-id="03486-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="03486-105">一旦對外開放 SSH 連接埠 22，bot 便會開始藉由猜測密碼來嘗試登入。</span><span class="sxs-lookup"><span data-stu-id="03486-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="03486-106">在本中，我們將停用經由 SSH 的密碼登入。</span><span class="sxs-lookup"><span data-stu-id="03486-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="03486-107">透過完全移除使用密碼的能力，我們能避免 Linux VM 遭受這種暴力密碼破解攻擊。</span><span class="sxs-lookup"><span data-stu-id="03486-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="03486-108">這種做法還有額外的優點，我們會將 Linux SSHD 設定為只允許透過 SSH 公開和私密金鑰登入，而這是目前最安全的 Linux 登入方法。</span><span class="sxs-lookup"><span data-stu-id="03486-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="03486-109">由於可能的私密金鑰組合千變萬化，若要在這種情況下猜測，即使利用 bot 來嘗試暴力破解 SSH 金鑰也無濟於事。</span><span class="sxs-lookup"><span data-stu-id="03486-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="03486-110">目標</span><span class="sxs-lookup"><span data-stu-id="03486-110">Goals</span></span>
* <span data-ttu-id="03486-111">設定 SSHD 以禁止：</span><span class="sxs-lookup"><span data-stu-id="03486-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="03486-112">密碼登入</span><span class="sxs-lookup"><span data-stu-id="03486-112">Password logins</span></span>
  * <span data-ttu-id="03486-113">根使用者登入</span><span class="sxs-lookup"><span data-stu-id="03486-113">Root user login</span></span>
  * <span data-ttu-id="03486-114">挑戰回應驗證</span><span class="sxs-lookup"><span data-stu-id="03486-114">Challenge-response authentication</span></span>
* <span data-ttu-id="03486-115">設定 SSHD 以允許：</span><span class="sxs-lookup"><span data-stu-id="03486-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="03486-116">僅限 SSH 金鑰登入</span><span class="sxs-lookup"><span data-stu-id="03486-116">only SSH key logins</span></span>
* <span data-ttu-id="03486-117">在登入的情況下重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="03486-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="03486-118">測試新 SSHD 組態</span><span class="sxs-lookup"><span data-stu-id="03486-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="03486-119">簡介</span><span class="sxs-lookup"><span data-stu-id="03486-119">Introduction</span></span>
[<span data-ttu-id="03486-120">SSH 定義</span><span class="sxs-lookup"><span data-stu-id="03486-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="03486-121">SSHD 是在 Linux VM 上執行的 SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="03486-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="03486-122">SSH 是從 MacBook 或 Linux 工作站之殼層執行的用戶端。</span><span class="sxs-lookup"><span data-stu-id="03486-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="03486-123">SSH 也是用來保護及加密工作站與 Linux VM 之通訊的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="03486-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="03486-124">在本文中，請務必開放一個 Linux VM 的登入，讓整個逐步解說得以順暢進行。</span><span class="sxs-lookup"><span data-stu-id="03486-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="03486-125">有鑑於此，我們將會開啟兩個終端機，並從兩者開啟 Linux VM 的 SSH。</span><span class="sxs-lookup"><span data-stu-id="03486-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="03486-126">我們將使用第一個終端機來變更 SSHD 組態檔，以及重新啟動 SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="03486-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="03486-127">等到服務重新啟動後，我們將使用第二個終端機來測試這些變更。</span><span class="sxs-lookup"><span data-stu-id="03486-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="03486-128">由於我們要停用 SSH 密碼並重度依賴 SSH 金鑰，所以如果您的 SSH 金鑰不正確而您關閉 VM 連線，VM 將永久遭到鎖定，而且沒有人能夠登入。如此一來，您只能將它刪除後再重新建立。</span><span class="sxs-lookup"><span data-stu-id="03486-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03486-129">必要條件</span><span class="sxs-lookup"><span data-stu-id="03486-129">Prerequisites</span></span>
* [<span data-ttu-id="03486-130">在 Linux 和 Mac 上為 Azure 中的 Linux VM 建立 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="03486-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="03486-131">Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="03486-131">Azure account</span></span>
  * [<span data-ttu-id="03486-132">註冊免費試用版</span><span class="sxs-lookup"><span data-stu-id="03486-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="03486-133">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="03486-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="03486-134">在 Azure 上執行的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="03486-134">Linux VM running on azure</span></span>
* <span data-ttu-id="03486-135">`~/.ssh/` 中的 SSH 公開和私密金鑰組</span><span class="sxs-lookup"><span data-stu-id="03486-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="03486-136">Linux VM 之 `~/.ssh/authorized_keys` 中的 SSH 公開金鑰</span><span class="sxs-lookup"><span data-stu-id="03486-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="03486-137">VM 上的 sudo 權限</span><span class="sxs-lookup"><span data-stu-id="03486-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="03486-138">連接埠 22 開啟</span><span class="sxs-lookup"><span data-stu-id="03486-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="03486-139">快速命令</span><span class="sxs-lookup"><span data-stu-id="03486-139">Quick Commands</span></span>
<span data-ttu-id="03486-140">只需要 TLDR 版本的資深 Linux 系統管理員可以從這裡開始。其他需要詳細說明和逐步解說的使用者請略過本節。</span><span class="sxs-lookup"><span data-stu-id="03486-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="03486-141">編輯組態檔，如下所示：</span><span class="sxs-lookup"><span data-stu-id="03486-141">Edit the config file as follows:</span></span>

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

<span data-ttu-id="03486-142">重新啟動 SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="03486-142">Restart the SSHD service.</span></span> <span data-ttu-id="03486-143">在以 Debian 為基礎的散發套件︰</span><span class="sxs-lookup"><span data-stu-id="03486-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="03486-144">在以 Red Hat 為基礎的散發套件︰</span><span class="sxs-lookup"><span data-stu-id="03486-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="03486-145">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="03486-145">Detailed Walk Through</span></span>
<span data-ttu-id="03486-146">在終端機 1 (T1) 上登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="03486-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="03486-147">在終端機 2 (T2) 上登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="03486-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="03486-148">我們要在 T2 上編輯 SSHD 組態檔。</span><span class="sxs-lookup"><span data-stu-id="03486-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="03486-149">在這裡，我們只會編輯設定來停用密碼，以及啟用 SSH 金鑰登入。</span><span class="sxs-lookup"><span data-stu-id="03486-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="03486-150">這個檔案中有許多值得研究及變更的設定，它們能讓 Linux 和 SSH 的安全性符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="03486-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="03486-151">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="03486-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="03486-152">啟用公開金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="03486-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="03486-153">停用根登入</span><span class="sxs-lookup"><span data-stu-id="03486-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="03486-154">停用挑戰回應驗證</span><span class="sxs-lookup"><span data-stu-id="03486-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="03486-155">重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="03486-155">Restart SSHD</span></span>
<span data-ttu-id="03486-156">從 T1 殼層驗證您是否保持登入。</span><span class="sxs-lookup"><span data-stu-id="03486-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="03486-157">這個步驟非常重要，由於我們已停用密碼，這樣做能避免 SSH 金鑰不正確時 VM 遭到鎖定。</span><span class="sxs-lookup"><span data-stu-id="03486-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="03486-158">如果 Linux VM 上有任何不正確的設定，您可以使用 T1 來修正 sshd_config，因為您仍然保持登入狀態，而且 SSH 會在 SSHD 服務重新啟動期間維持連線。</span><span class="sxs-lookup"><span data-stu-id="03486-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="03486-159">從 T2 執行︰</span><span class="sxs-lookup"><span data-stu-id="03486-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="03486-160">在 Debian 系列上</span><span class="sxs-lookup"><span data-stu-id="03486-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="03486-161">在 RedHat 系列上</span><span class="sxs-lookup"><span data-stu-id="03486-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="03486-162">VM 上的密碼現已停用，如此將能避免暴力破解密碼的登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="03486-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="03486-163">由於我們只允許 SSH 金鑰，您將可以利用更快速、更安全的方式登入。</span><span class="sxs-lookup"><span data-stu-id="03486-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

