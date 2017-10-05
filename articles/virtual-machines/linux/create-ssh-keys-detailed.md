---
title: "在 Azure 上建立 Linux VM 之 SSH 金鑰組的詳細步驟 | Microsoft Docs"
description: "了解其他步驟，以在 Azure 中為 Linux VM 建立 SSH 公開和私密金鑰組，以及為不同使用案例建立特定憑證。"
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="f0ad7-103">在 Azure 中為 Linux VM 建立 SSH 金鑰組和其他憑證的詳細逐步解說</span><span class="sxs-lookup"><span data-stu-id="f0ad7-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="f0ad7-104">您可以利用 SSH 金鑰組，在預設使用 SSH 金鑰進行驗證的 Azure 上建立虛擬機器，進而免除登入密碼的需求。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="f0ad7-105">密碼有可能被猜到，讓您的 VM 遭到持續不斷的暴力密碼破解嘗試來猜測您的密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="f0ad7-106">使用 Azure CLI 或 Resource Manager 範本建立的 VM，可以將 SSH 公開金鑰納入部署中，進而免於對 SSH 停用密碼登入進行後置部署設定。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="f0ad7-107">針對用於 Linux 虛擬機器之類的憑證，本文提供產生憑證的詳細步驟和其他範例。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="f0ad7-108">如果您想要快速建立和使用 SSH 金鑰組，請參閱[如何在 Azure 中建立 Linux VM 的 SSH 公開和私密金鑰組](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="f0ad7-109">了解 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="f0ad7-109">Understanding SSH keys</span></span>

<span data-ttu-id="f0ad7-110">想要登入 Linux 伺服器，最簡單的方式是使用 SSH 公開和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="f0ad7-111">[公開金鑰密碼編譯](https://en.wikipedia.org/wiki/Public-key_cryptography) 會安全得多，因為密碼非常容易遭到暴力破解。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="f0ad7-112">公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="f0ad7-113">SSH 私密金鑰應該有[非常安全的密碼](https://www.xkcd.com/936/) (來源︰[xkcd.com](https://xkcd.com)) 來保護它。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="f0ad7-114">此密碼只能用於存取 SSH 私密金鑰檔，而**不是**使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="f0ad7-115">當您將密碼新增至 SSH 金鑰時，便會使用 128位元的 AES 來加密私密金鑰，而未利用密碼解密的私密金鑰沒有用處。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="f0ad7-116">如果攻擊者竊取您的私密金鑰，而且該金鑰沒有密碼，他們就能使用該私密金鑰來登入有對應公開金鑰的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="f0ad7-117">如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="f0ad7-118">本文會建立 SSH 通訊協定第 2 版的 RSA 公開和私密金鑰檔組合 (也稱為「ssh-rsa」金鑰)，這是使用 Azure Resource Manager 進行部署時的建議方式。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="f0ad7-119">ssh-rsa  金鑰是在[入口網站](https://portal.azure.com)上進行傳統部署和 Resource Manager 部署時的必要項目。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="f0ad7-120">SSH 金鑰的使用和好處</span><span class="sxs-lookup"><span data-stu-id="f0ad7-120">SSH keys use and benefits</span></span>

<span data-ttu-id="f0ad7-121">Azure 需要至少 2048 位元、SSH 通訊協定第 2 版 RSA 格式的公開和私密金鑰；公開金鑰檔具有 `.pub` 容器格式 </span><span class="sxs-lookup"><span data-stu-id="f0ad7-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="f0ad7-122">若要建立金鑰，請使用 `ssh-keygen`，在詢問一系列問題後，它便會編寫私密金鑰和對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="f0ad7-123">建立 Azure VM 時，Azure 會將公開金鑰複製到 VM 上的 `~/.ssh/authorized_keys` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="f0ad7-124">`~/.ssh/authorized_keys` 中的 SSH 金鑰用於挑戰用戶端，以符合 SSH 登入連線上的對應私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="f0ad7-125">使用用於驗證的 SSH 金鑰進行建立 Azure Linux VM 時，Azure 會將 SSHD 伺服器設定為不允許密碼登入，僅允許以 SSH 金鑰登入。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="f0ad7-126">因此，建立具 SSH 金鑰的 Azure Linux VM，即可協助保護 VM 部署的安全，並免除在 **sshd_config** 檔中停用密碼的標準部署後設定步驟。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="f0ad7-127">使用 ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="f0ad7-127">Using ssh-keygen</span></span>

<span data-ttu-id="f0ad7-128">此命令會使用 2048 位元 RSA 建立密碼保護 (加密) 的 SSH 金鑰組，並為其加上註解以供輕鬆識別。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="f0ad7-129">依預設，SSH 金鑰會保留在 `~/.ssh` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="f0ad7-130">如果您沒有 `~/.ssh` 目錄，`ssh-keygen` 命令會使用正確的權限為您建立。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="f0ad7-131">*命令的說明*</span><span class="sxs-lookup"><span data-stu-id="f0ad7-131">*Command explained*</span></span>

<span data-ttu-id="f0ad7-132">`ssh-keygen` = 用來建立金鑰的程式</span><span class="sxs-lookup"><span data-stu-id="f0ad7-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="f0ad7-133">`-t rsa` = 要建立的金鑰類型 (採用 RSA 格式) [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = 金鑰的位元</span><span class="sxs-lookup"><span data-stu-id="f0ad7-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="f0ad7-134">`-C "azureuser@myserver"` = 附加至公開金鑰檔案結尾以便輕鬆識別的註解。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="f0ad7-135">通常會以一封電子郵件做為註解，但您可以使用任何最適合您的基礎結構的事物。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="f0ad7-136">使用 `asm` 進行傳統部署</span><span class="sxs-lookup"><span data-stu-id="f0ad7-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="f0ad7-137">如果您使用傳統部署模型 (CLI 中的 `asm` 模式)，則可以在 pem 容器中使用 SSH-RSA 公開金鑰或 RFC4716 格式的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="f0ad7-138">SSH-RSA 公開金鑰是稍早在本文中使用 `ssh-keygen` 建立的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="f0ad7-139">若要從現有的 SSH 公開金鑰建立 RFC4716 格式的金鑰︰</span><span class="sxs-lookup"><span data-stu-id="f0ad7-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="f0ad7-140">ssh-keygen 的範例</span><span class="sxs-lookup"><span data-stu-id="f0ad7-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="f0ad7-141">已儲存金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="f0ad7-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="f0ad7-142">本文中的金鑰組名稱。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-142">The key pair name for this article.</span></span>  <span data-ttu-id="f0ad7-143">預設會有名為 **id_rsa** 的金鑰組，而且有些工具可能會預期私密金鑰的檔案名稱為 **id_rsa**，所以最好有此金鑰組。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="f0ad7-144">`~/.ssh/` 目錄是 SSH 金鑰組和 SSH 組態檔的預設位置。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="f0ad7-145">如果未指定完整路徑，則 `ssh-keygen` 會在目前的工作目錄 (而不是預設 `~/.ssh`) 中建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="f0ad7-146">`~/.ssh` 。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="f0ad7-147">金鑰密碼︰</span><span class="sxs-lookup"><span data-stu-id="f0ad7-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="f0ad7-148">`ssh-keygen` 將私密金鑰檔案的密碼稱為「複雜密碼」。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="f0ad7-149">「強烈」建議為私密金鑰加上密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="f0ad7-150">若沒有使用密碼來保護金鑰檔，任何人只要擁有該檔案，就可以用它登入具有對應公開金鑰的任何伺服器。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="f0ad7-151">新增密碼 (複雜密碼) 可提升防護能力，以防有人能夠取得您的私密金鑰檔案，讓您有時間變更用來對您進行驗證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="f0ad7-152">使用 ssh-agent 來儲存您的私密金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="f0ad7-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="f0ad7-153">若要避免在每次 SSH 登入時輸入私密金鑰檔案密碼，您可以使用 `ssh-agent` 來快取您的私密金鑰檔案密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="f0ad7-154">如果您使用 Mac，則 OSX 金鑰鏈會在您叫用 `ssh-agent`時安全地儲存私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="f0ad7-155">確認並使用 ssh-agent 和 ssh-add 將金鑰檔案通知 SSH 系統，才不需要以互動方式使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="f0ad7-156">現在使用 `ssh-add` 命令將私密金鑰加入至 `ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="f0ad7-157">私密金鑰密碼現已儲存在 `ssh-agent` 中。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="f0ad7-158">使用 `ssh-copy-id` 將金鑰複製到現有 VM</span><span class="sxs-lookup"><span data-stu-id="f0ad7-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="f0ad7-159">如果您已經建立 VM，您可以將新的 SSH 公開金鑰安裝至 Linux VM：</span><span class="sxs-lookup"><span data-stu-id="f0ad7-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="f0ad7-160">建立和設定 SSH 組態檔</span><span class="sxs-lookup"><span data-stu-id="f0ad7-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="f0ad7-161">建議的最佳作法是建立及設定 `~/.ssh/config` 檔案來加速登入，並且最佳化您的 SSH 用戶端行為。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="f0ad7-162">下列範例將示範標準組態。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="f0ad7-163">建立檔案</span><span class="sxs-lookup"><span data-stu-id="f0ad7-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="f0ad7-164">編輯檔案以加入新的 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="f0ad7-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="f0ad7-165">範例 `~/.ssh/config` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="f0ad7-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="f0ad7-166">此 SSH 組態可讓您將各個伺服器分段，讓它們各自擁有專用的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="f0ad7-167">預設設定 (`Host *`) 適用於不符合組態檔中任何提升之特定主機的任何主機。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="f0ad7-168">組態檔的說明</span><span class="sxs-lookup"><span data-stu-id="f0ad7-168">Config file explained</span></span>

<span data-ttu-id="f0ad7-169">`Host` = 在終端機上所呼叫的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="f0ad7-170">`ssh fedora22` 會指示 `SSH` 使用設定區塊中標示為 `Host fedora22` 的值。注意︰這可以是符合您用途的任何標籤，並不代表任何伺服器的實際主機名稱。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="f0ad7-171">`Hostname 102.160.203.241` = 所存取伺服器的 IP 位址或 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="f0ad7-172">`User ahmet` = 登入伺服器時要使用的遠端使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="f0ad7-173">`PubKeyAuthentication yes` = 向 SSH 指出您想要使用 SSH 金鑰來登入。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="f0ad7-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = 要用於驗證的 SSH 私密金鑰和對應公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="f0ad7-175">使用 SSH 登入 Linux 而不提供密碼</span><span class="sxs-lookup"><span data-stu-id="f0ad7-175">SSH into Linux without a password</span></span>

<span data-ttu-id="f0ad7-176">您現在已擁有 SSH 金鑰組和設定好的 SSH 組態檔，因此能夠快速且安全地登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="f0ad7-177">第一次使用 SSH 金鑰登入伺服器時，命令會提示您輸入該金鑰檔案的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="f0ad7-178">命令的說明</span><span class="sxs-lookup"><span data-stu-id="f0ad7-178">Command explained</span></span>

<span data-ttu-id="f0ad7-179">在執行 `ssh fedora22` 後，SSH 會先從 `Host fedora22` 區塊中找出所有設定並加以載入，再從最後一個區塊 `Host *` 中載入所有其餘設定。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0ad7-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0ad7-180">Next Steps</span></span>

<span data-ttu-id="f0ad7-181">接下來是使用新的 SSH 公開金鑰建立 Azure Linux VM。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="f0ad7-182">相較於以預設登入方法密碼建立的 VM，以 SSH 公開金鑰作為登入所建立的 Azure VM 比較安全。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="f0ad7-183">使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。</span><span class="sxs-lookup"><span data-stu-id="f0ad7-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="f0ad7-184">使用 Azure 範本建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f0ad7-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f0ad7-185">使用 Azure 入口網站建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f0ad7-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f0ad7-186">使用 Azure CLI 建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f0ad7-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
