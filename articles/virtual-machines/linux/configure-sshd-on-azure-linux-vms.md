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
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="87bff-103">在 Azure Linux VM 上設定 SSHD</span><span class="sxs-lookup"><span data-stu-id="87bff-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="87bff-104">本文示範 toolockdown hello SSH 伺服器在 Linux、 tooprovide 最佳作法安全性以及 toospeed hello SSH 登入程序使用 SSH 金鑰，而不是密碼的方式。</span><span class="sxs-lookup"><span data-stu-id="87bff-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="87bff-105">toofurther 鎖定 SSHD 我們 toodisable hello 根使用者不能 toologin，限制 hello 使用者允許 toologin 透過已核准的群組清單中，停用 SSH 通訊協定版本 1、 設定最小金鑰位元，以及設定自動登出閒置的使用者。</span><span class="sxs-lookup"><span data-stu-id="87bff-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="87bff-106">這篇文章的 hello 需求： Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和[SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="87bff-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="87bff-107">快速命令</span><span class="sxs-lookup"><span data-stu-id="87bff-107">Quick Commands</span></span>

<span data-ttu-id="87bff-108">設定`/etc/ssh/sshd_config`以 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="87bff-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="87bff-109">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="87bff-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="87bff-110">停用 hello 根使用者的登入</span><span class="sxs-lookup"><span data-stu-id="87bff-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="87bff-111">允許的群組清單</span><span class="sxs-lookup"><span data-stu-id="87bff-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="87bff-112">允許的使用者清單</span><span class="sxs-lookup"><span data-stu-id="87bff-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="87bff-113">停用 SSH 通訊協定第 1 版</span><span class="sxs-lookup"><span data-stu-id="87bff-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="87bff-114">最少金鑰位元數</span><span class="sxs-lookup"><span data-stu-id="87bff-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="87bff-115">中斷連接閒置使用者</span><span class="sxs-lookup"><span data-stu-id="87bff-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="87bff-116">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="87bff-116">Detailed Walkthrough</span></span>

<span data-ttu-id="87bff-117">SSHD 是 SSH 伺服器 hello Linux VM 上執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="87bff-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="87bff-118">SSH 是從 MacBook 的殼層、Linux 工作站或 Windows 的 Bash 執行的用戶端。</span><span class="sxs-lookup"><span data-stu-id="87bff-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="87bff-119">SSH 也是 hello 通訊協定使用 toosecure 和加密 hello 工作站和 hello 進行 SSH 也 VPN （虛擬私人網路） 的 Linux VM 之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="87bff-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="87bff-120">本文中，則會是非常重要的 tookeep 單一登入 tooyour Linux VM 開啟 hello 整個逐步解說。</span><span class="sxs-lookup"><span data-stu-id="87bff-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="87bff-121">一旦建立 SSH 連線，則仍會保持為開啟的工作階段，只要未關閉 hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="87bff-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="87bff-122">具有一個終端機登入，允許的變更進行 toobe toohello SSHD 服務不被鎖定，如果在進行重大變更。</span><span class="sxs-lookup"><span data-stu-id="87bff-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="87bff-123">如果您沒有遭到鎖定而無法以中斷 SSHD 設定 Linux VM，Azure 提供 hello 能力 tooreset hello 中斷的 SSHD 組態[Azure VM 存取延伸](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="87bff-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="87bff-124">基於這個理由開啟兩個終端機和 SSH toohello Linux VM 從這兩種。</span><span class="sxs-lookup"><span data-stu-id="87bff-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="87bff-125">我們使用 hello 第一個終端機 toomake hello 變更 tooSSHDs 組態檔，然後重新啟動 hello SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="87bff-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="87bff-126">我們使用 hello 第二個終端機 tootest hello 服務重新啟動後，這些變更。</span><span class="sxs-lookup"><span data-stu-id="87bff-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="87bff-127">因為我們要停用 SSH 密碼，而且依賴嚴格 SSH 金鑰，如果 SSH 金鑰不正確，而且您關閉 hello 連接 toohello VM，hello VM 將會永久鎖定，且沒有任何人將可以 toologin tooit 需要 toobe 刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="87bff-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="87bff-128">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="87bff-128">Disable password logins</span></span>

<span data-ttu-id="87bff-129">hello 最快方式 toosecure 您 Linux VM 是 toodisable 密碼登入。</span><span class="sxs-lookup"><span data-stu-id="87bff-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="87bff-130">密碼登入啟用時，bot 編目 hello web 會立即開始嘗試 toobrute 會強制使用 SSH Linux vm 的猜測 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="87bff-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="87bff-131">完全停用密碼登入，可讓 hello SSH 伺服器 tooignore 所有密碼登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="87bff-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="87bff-132">停用 hello 根使用者的登入</span><span class="sxs-lookup"><span data-stu-id="87bff-132">Disable login by hello root user</span></span>

<span data-ttu-id="87bff-133">下列 Linux 最佳作法，hello`root`使用者應該永遠不會記錄到透過 SSH 或使用`sudo su`。</span><span class="sxs-lookup"><span data-stu-id="87bff-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="87bff-134">透過 hello 應該一律執行所有需要根層級權限的命令`sudo`命令，它會記錄所有動作，供日後稽核。</span><span class="sxs-lookup"><span data-stu-id="87bff-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="87bff-135">停用 hello`root`從透過 SSH 登入的使用者是安全性最佳作法步驟，以確保只有授權的使用者允許 tooSSH。</span><span class="sxs-lookup"><span data-stu-id="87bff-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="87bff-136">允許的群組清單</span><span class="sxs-lookup"><span data-stu-id="87bff-136">Allowed groups list</span></span>

<span data-ttu-id="87bff-137">SSH 提供方法來限制允許或不允許透過 SSH 登入的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="87bff-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="87bff-138">這項功能會使用清單 tooapprove，或從登入拒絕特定使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="87bff-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="87bff-139">設定 hello 滾輪群組 toohello `AllowGroups` hello 滾輪群組中的 SSH toojust 使用者帳戶清單會限制的已核准的登入。</span><span class="sxs-lookup"><span data-stu-id="87bff-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="87bff-140">允許的使用者清單</span><span class="sxs-lookup"><span data-stu-id="87bff-140">Allowed users list</span></span>

<span data-ttu-id="87bff-141">SSH 登入 toojust 使用者限制為更特定的方式 tooaccomplish hello 相同工作`AllowGroups`是。</span><span class="sxs-lookup"><span data-stu-id="87bff-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="87bff-142">停用 SSH 通訊協定第 1 版</span><span class="sxs-lookup"><span data-stu-id="87bff-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="87bff-143">SSH 通訊協定第 1 版不安全，應該停用。</span><span class="sxs-lookup"><span data-stu-id="87bff-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="87bff-144">SSH 通訊協定第 2 版是提供安全的方式 tooSSH tooyour 伺服器 hello 目前版本。</span><span class="sxs-lookup"><span data-stu-id="87bff-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="87bff-145">停用 SSH 版本 1 拒絕任何嘗試 tooestablish 的 SSH 用戶端連接使用 SSH 版本 1 的 hello SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="87bff-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="87bff-146">只允許 toonegotiate SSH 第 2 版連接與 hello SSH 伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="87bff-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="87bff-147">最少金鑰位元數</span><span class="sxs-lookup"><span data-stu-id="87bff-147">Minimum key bits</span></span>

<span data-ttu-id="87bff-148">遵循安全性最佳作法，會停用密碼 SSH 登入，而只有 SSH 金鑰允許 toobe tooauthenticate 搭配 hello SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="87bff-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="87bff-149">這些 SSH 金鑰可能以不同長度的金鑰建立 (以位元為單位)。</span><span class="sxs-lookup"><span data-stu-id="87bff-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="87bff-150">最佳做法為 2048 位元長度的索引鍵是 hello 最小的可接受索引鍵強度的狀態。</span><span class="sxs-lookup"><span data-stu-id="87bff-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="87bff-151">少於 2048 位元的金鑰在理論上會被破解。</span><span class="sxs-lookup"><span data-stu-id="87bff-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="87bff-152">設定 hello`ServerKeyBits`太`2048`允許使用金鑰為 2048 位元或更高的任何連線，並拒絕小於 2048 位元的連線。</span><span class="sxs-lookup"><span data-stu-id="87bff-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="87bff-153">中斷連接閒置使用者</span><span class="sxs-lookup"><span data-stu-id="87bff-153">Disconnect idle users</span></span>

<span data-ttu-id="87bff-154">SSH 有擁有已變得讚賞閒置一段指定的秒數已超過的開啟連接的 hello 能力 toodisconnect 使用者。</span><span class="sxs-lookup"><span data-stu-id="87bff-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="87bff-155">保持開啟的工作階段 tooonly active 限制 hello 暴露 hello Linux VM 的那些使用者。</span><span class="sxs-lookup"><span data-stu-id="87bff-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="87bff-156">重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="87bff-156">Restart SSHD</span></span>

<span data-ttu-id="87bff-157">中的 tooenable hello 設定`/etc/ssh/sshd_config`重新啟動重新啟動 hello SSH 伺服器 hello SSHD 處理序。</span><span class="sxs-lookup"><span data-stu-id="87bff-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="87bff-158">hello 使用 toorestart hello SSH 伺服器的終端機視窗而不會遺失 hello 開啟 SSH 工作階段維持開啟的。</span><span class="sxs-lookup"><span data-stu-id="87bff-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="87bff-159">tootest hello 新 SSH 伺服器設定，請使用第二個終端機視窗或索引標籤。使用不同的終端機 tootest hello SSH 連線可讓您回到 toogo 和進行其他變更 toohello `/etc/ssh/sshd_config` hello 第一個終端機，而不被中斷 SSHD 變更鎖定中。</span><span class="sxs-lookup"><span data-stu-id="87bff-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="87bff-160">在 Redhat、Centos 和 Fedora 上</span><span class="sxs-lookup"><span data-stu-id="87bff-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="87bff-161">在 Debian 和 Ubuntu 上</span><span class="sxs-lookup"><span data-stu-id="87bff-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="87bff-162">使用 Azure reset-access 重設 SSHD</span><span class="sxs-lookup"><span data-stu-id="87bff-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="87bff-163">如果您從重大變更 toohello SSHD 設定鎖定時，您可以使用 hello Azure VM 存取延伸 tooreset hello SSHD configuration 後 toohello 原始設定。</span><span class="sxs-lookup"><span data-stu-id="87bff-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="87bff-164">將任何範例名稱換成您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="87bff-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="87bff-165">安裝 Fail2ban</span><span class="sxs-lookup"><span data-stu-id="87bff-165">Install Fail2ban</span></span>

<span data-ttu-id="87bff-166">強烈建議 tooinstall 及安裝 hello 開放原始碼應用程式 Fail2ban，哪些區塊重複嘗試 toologin tooyour Linux VM 透過 SSH 使用暴力。</span><span class="sxs-lookup"><span data-stu-id="87bff-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="87bff-167">Fail2ban 重複的記錄檔無法透過 SSH 嘗試 toologin，，然後建立防火牆規則 hello 嘗試所源自的 tooblock hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="87bff-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="87bff-168">Fail2ban 首頁</span><span class="sxs-lookup"><span data-stu-id="87bff-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="87bff-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87bff-169">Next Steps</span></span>

<span data-ttu-id="87bff-170">現在，您有設定，並鎖定 hello SSH 伺服器 Linux VM 上有額外的安全性最佳的作法，您可以遵循。</span><span class="sxs-lookup"><span data-stu-id="87bff-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="87bff-171">管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="87bff-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="87bff-172">加密使用 Azure CLI hello 的 Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="87bff-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="87bff-173">Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="87bff-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
