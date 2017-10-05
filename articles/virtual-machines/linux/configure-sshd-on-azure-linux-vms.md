---
title: "在 Azure Linux 虛擬機器上設定 SSHD | Microsoft Docs"
description: "設定 SSHD 以提供安全性最佳做法和封鎖以 SSH 登入 Azure Linux 虛擬機器。"
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
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="51ce5-103">在 Azure Linux VM 上設定 SSHD</span><span class="sxs-lookup"><span data-stu-id="51ce5-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="51ce5-104">本文說明如何在 Linux 上鎖定 SSH 伺服器、提供最佳做法安全性，以及使用 SSH 金鑰 (而不是密碼) 來加速 SSH 登入程序。</span><span class="sxs-lookup"><span data-stu-id="51ce5-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="51ce5-105">為了進一步鎖定 SSHD，我們將禁止根使用者登入、限制允許透過核准群組清單登入的使用者、停用 SSH 通訊協定第 1 版、設定最多金鑰位元數，以及設定自動登出閒置使用者。</span><span class="sxs-lookup"><span data-stu-id="51ce5-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="51ce5-106">這篇文章的需求如下︰Azure 帳戶 ([取得免費試用](https://azure.microsoft.com/pricing/free-trial/)) 和 [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51ce5-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="51ce5-107">快速命令</span><span class="sxs-lookup"><span data-stu-id="51ce5-107">Quick Commands</span></span>

<span data-ttu-id="51ce5-108">使用下列設定來設定 `/etc/ssh/sshd_config`︰</span><span class="sxs-lookup"><span data-stu-id="51ce5-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="51ce5-109">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="51ce5-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="51ce5-110">停用根使用者登入</span><span class="sxs-lookup"><span data-stu-id="51ce5-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="51ce5-111">允許的群組清單</span><span class="sxs-lookup"><span data-stu-id="51ce5-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="51ce5-112">允許的使用者清單</span><span class="sxs-lookup"><span data-stu-id="51ce5-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="51ce5-113">停用 SSH 通訊協定第 1 版</span><span class="sxs-lookup"><span data-stu-id="51ce5-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="51ce5-114">最少金鑰位元數</span><span class="sxs-lookup"><span data-stu-id="51ce5-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="51ce5-115">中斷連接閒置使用者</span><span class="sxs-lookup"><span data-stu-id="51ce5-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="51ce5-116">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="51ce5-116">Detailed Walkthrough</span></span>

<span data-ttu-id="51ce5-117">SSHD 是在 Linux VM 上執行的 SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="51ce5-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="51ce5-118">SSH 是從 MacBook 的殼層、Linux 工作站或 Windows 的 Bash 執行的用戶端。</span><span class="sxs-lookup"><span data-stu-id="51ce5-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="51ce5-119">SSH 也是用來保護和加密工作站與 Linux VM 之間通訊的通訊協定，這使得 SSH 也成為 VPN (虛擬私人網站)。</span><span class="sxs-lookup"><span data-stu-id="51ce5-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="51ce5-120">在本文中，務必為整個逐步解說開放 Linux VM 的一個登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="51ce5-121">建立 SSH 連接之後，只要未關閉視窗，就會保持為開啟的工作階段。</span><span class="sxs-lookup"><span data-stu-id="51ce5-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="51ce5-122">只要登入一個終端機，就可以變更 SSHD 服務，而不會因為錯誤的變更而遭鎖定。</span><span class="sxs-lookup"><span data-stu-id="51ce5-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="51ce5-123">如果您因為錯誤的 SSHD 設定而被鎖在 Linux VM 外，Azure 可讓您使用 [Azure VM 存取擴充](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來重設錯誤的 SSHD 設定。</span><span class="sxs-lookup"><span data-stu-id="51ce5-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="51ce5-124">有鑑於此，我們開啟兩個終端機，並同時從這兩者以 SSH 登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="51ce5-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="51ce5-125">我們使用第一個終端機來變更 SSHD 設定檔，以及重新啟動 SSHD 服務。</span><span class="sxs-lookup"><span data-stu-id="51ce5-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="51ce5-126">等到服務重新啟動後，我們會使用第二個終端機來測試這些變更。</span><span class="sxs-lookup"><span data-stu-id="51ce5-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="51ce5-127">由於我們要停用 SSH 密碼並重度依賴 SSH 金鑰，所以如果您的 SSH 金鑰不正確而您關閉 VM 連線，VM 將永久遭到鎖定，而且沒有人能夠登入。如此一來，您只能將它刪除後再重新建立。</span><span class="sxs-lookup"><span data-stu-id="51ce5-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="51ce5-128">停用密碼登入</span><span class="sxs-lookup"><span data-stu-id="51ce5-128">Disable password logins</span></span>

<span data-ttu-id="51ce5-129">保護 Linux VM 的最快方式就是停用密碼登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="51ce5-130">密碼登入啟用時，耙梳 Web 的 Bot 會立即開始嘗試暴力猜測 Linux VM (使用 SSH) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="51ce5-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="51ce5-131">完全停用密碼登入可讓 SSH 伺服器忽略所有密碼登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="51ce5-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="51ce5-132">停用根使用者登入</span><span class="sxs-lookup"><span data-stu-id="51ce5-132">Disable login by the root user</span></span>

<span data-ttu-id="51ce5-133">根據 Linux 最佳做法，`root` 使用者永遠不可能透過 SSH 或使用 `sudo su` 來登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="51ce5-134">應該永遠透過 `sudo` 命令執行需要根層級權限的所有命令，此命令會記錄所有動作供未來稽核。</span><span class="sxs-lookup"><span data-stu-id="51ce5-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="51ce5-135">禁止 `root` 使用者透過 SSH 登入是一項安全性最做作法步驟，可確保只有授權的使用者才能透過 SSH 登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="51ce5-136">允許的群組清單</span><span class="sxs-lookup"><span data-stu-id="51ce5-136">Allowed groups list</span></span>

<span data-ttu-id="51ce5-137">SSH 提供方法來限制允許或不允許透過 SSH 登入的使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="51ce5-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="51ce5-138">這項功能使用清單來核准或拒絕特定使用者和群組登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="51ce5-139">將 wheel 群組設為 `AllowGroups` 清單可限制只有 wheel 群組中的使用者帳戶，才核准透過 SSH 登入。</span><span class="sxs-lookup"><span data-stu-id="51ce5-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="51ce5-140">允許的使用者清單</span><span class="sxs-lookup"><span data-stu-id="51ce5-140">Allowed users list</span></span>

<span data-ttu-id="51ce5-141">同樣是完成這件工作，但將 SSH 登入限制為使用者比 `AllowGroups` 的做法更具體。</span><span class="sxs-lookup"><span data-stu-id="51ce5-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="51ce5-142">停用 SSH 通訊協定第 1 版</span><span class="sxs-lookup"><span data-stu-id="51ce5-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="51ce5-143">SSH 通訊協定第 1 版不安全，應該停用。</span><span class="sxs-lookup"><span data-stu-id="51ce5-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="51ce5-144">SSH 通訊協定第 2 版是目前的版本，提供安全的方式來透過 SSH 登入伺服器。</span><span class="sxs-lookup"><span data-stu-id="51ce5-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="51ce5-145">停用 SSH 第 1 版會拒絕任何 SSH 用戶端嘗試使用 SSH 第 1 版來建立 SSH 伺服器的連接。</span><span class="sxs-lookup"><span data-stu-id="51ce5-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="51ce5-146">只允許 SSH 第 2 版與 SSH 伺服器交涉連接。</span><span class="sxs-lookup"><span data-stu-id="51ce5-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="51ce5-147">最少金鑰位元數</span><span class="sxs-lookup"><span data-stu-id="51ce5-147">Minimum key bits</span></span>

<span data-ttu-id="51ce5-148">根據安全性最佳做法，密碼 SSH 登入會停用，只允許使用 SSH 金鑰向 SSH 伺服器進行驗證。</span><span class="sxs-lookup"><span data-stu-id="51ce5-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="51ce5-149">這些 SSH 金鑰可能以不同長度的金鑰建立 (以位元為單位)。</span><span class="sxs-lookup"><span data-stu-id="51ce5-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="51ce5-150">最佳做法規定長度 2048 位元的金鑰是可接受的最小金鑰強度。</span><span class="sxs-lookup"><span data-stu-id="51ce5-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="51ce5-151">少於 2048 位元的金鑰在理論上會被破解。</span><span class="sxs-lookup"><span data-stu-id="51ce5-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="51ce5-152">將 `ServerKeyBits` 設定為 `2048` 可允許任何使用 2048 位元或更大金鑰的連接，並拒絕少於 2048 位元的連接。</span><span class="sxs-lookup"><span data-stu-id="51ce5-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="51ce5-153">中斷連接閒置使用者</span><span class="sxs-lookup"><span data-stu-id="51ce5-153">Disconnect idle users</span></span>

<span data-ttu-id="51ce5-154">如果使用者開啟的連接已閒置超過一段設定的秒數，SSH 能夠中斷連接這些使用者。</span><span class="sxs-lookup"><span data-stu-id="51ce5-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="51ce5-155">只讓作用中的使用者保持開啟的工作階段可限制 Linux VM 暴露。</span><span class="sxs-lookup"><span data-stu-id="51ce5-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="51ce5-156">重新啟動 SSHD</span><span class="sxs-lookup"><span data-stu-id="51ce5-156">Restart SSHD</span></span>

<span data-ttu-id="51ce5-157">若要啟用 `/etc/ssh/sshd_config` 中的設定，請重新啟動 SSHD 處理序以重新啟動 SSH 伺服器。</span><span class="sxs-lookup"><span data-stu-id="51ce5-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="51ce5-158">您用來重新啟動 SSH 伺服器的終端機視窗會保持開啟，不會遺失已開啟的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="51ce5-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="51ce5-159">若要測試新的 SSH 伺服器設定，請使用第二個終端機視窗或索引標籤。</span><span class="sxs-lookup"><span data-stu-id="51ce5-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="51ce5-160">如果使用不同的終端機來測試 SSH 連接，您可以返回第一個終端機來進一步變更 `/etc/ssh/sshd_config`，不會因為 SSHD 變更錯誤而遭鎖定。</span><span class="sxs-lookup"><span data-stu-id="51ce5-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="51ce5-161">在 Redhat、Centos 和 Fedora 上</span><span class="sxs-lookup"><span data-stu-id="51ce5-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="51ce5-162">在 Debian 和 Ubuntu 上</span><span class="sxs-lookup"><span data-stu-id="51ce5-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="51ce5-163">使用 Azure reset-access 重設 SSHD</span><span class="sxs-lookup"><span data-stu-id="51ce5-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="51ce5-164">如果您因為錯誤變更 SSHD 設定而遭鎖定，您可以使用 Azure VM 存取擴充，將 SSHD 設定重設回原始設定。</span><span class="sxs-lookup"><span data-stu-id="51ce5-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="51ce5-165">將任何範例名稱換成您自己的名稱。</span><span class="sxs-lookup"><span data-stu-id="51ce5-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="51ce5-166">安裝 Fail2ban</span><span class="sxs-lookup"><span data-stu-id="51ce5-166">Install Fail2ban</span></span>

<span data-ttu-id="51ce5-167">強烈建議安裝和設定開放原始碼應用程式 Fail2ban，它會封鎖重複嘗試以暴力密碼破解透過 SSH 來登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="51ce5-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="51ce5-168">Fail2ban 會記錄重複嘗試透過 SSH 登入的失敗情況，然後建立防火牆規則來封鎖這些嘗試的來源 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51ce5-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="51ce5-169">Fail2ban 首頁</span><span class="sxs-lookup"><span data-stu-id="51ce5-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="51ce5-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51ce5-170">Next Steps</span></span>

<span data-ttu-id="51ce5-171">既然您已在 Linux VM 上設定並鎖定 SSH 伺服器，您還可以採取更多的安全性最佳做法。</span><span class="sxs-lookup"><span data-stu-id="51ce5-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="51ce5-172">管理使用者、SSH，並使用 VMAccess 擴充功能檢查或修復 Azure Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="51ce5-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="51ce5-173">使用 Azure CLI 將 Linux VM 上的磁碟加密</span><span class="sxs-lookup"><span data-stu-id="51ce5-173">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="51ce5-174">Azure Resource Manager 範本中的存取和安全性</span><span class="sxs-lookup"><span data-stu-id="51ce5-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
