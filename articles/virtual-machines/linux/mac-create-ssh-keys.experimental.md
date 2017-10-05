---
title: "在 Azure 上建立 Linux VM 的 SSH 金鑰組 | Microsoft Docs"
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
ms.openlocfilehash: 19acd4efca7ef043f31b436b96f9129caee9591b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="a6fa4-103">建立 Linux VM 的 SSH 公用和私用金鑰組</span><span class="sxs-lookup"><span data-stu-id="a6fa4-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="a6fa4-104">本文說明如何產生可與 Linux VM 搭配使用的 SSH 通訊協定第 2 版 RSA 公開和私密金鑰檔案組。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="a6fa4-105">您可以利用 SSH 金鑰組，在預設使用 SSH 金鑰進行驗證的 Azure 上建立虛擬機器，進而免除登入密碼的需求。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="a6fa4-106">密碼有可能被猜到，讓您的 VM 遭到持續不斷的暴力密碼破解嘗試來猜測您的密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="a6fa4-107">使用 Azure 範本或 `azure-cli` 建立的 VM 可以將 SSH 公開金鑰納入部署中，進而免於對 SSH 停用密碼登入進行後置部署設定。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a6fa4-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="a6fa4-108">Quick Commands</span></span>

<span data-ttu-id="a6fa4-109">透過 Bash 殼層執行下列命令中，以您自己的選項取代範例。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="a6fa4-110">SSH 公開金鑰檔預設會建立在 `~/.ssh/id_rsa.pub`。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="a6fa4-111">使用下列命令時若出現提示，您應該建立「複雜密碼」來保護您的私密金鑰 </span><span class="sxs-lookup"><span data-stu-id="a6fa4-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="a6fa4-112">(此複雜密碼是用來加密私密金鑰的密碼)。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="a6fa4-113">將新建立的索引鍵新增至 `ssh-agent`：</span><span class="sxs-lookup"><span data-stu-id="a6fa4-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="a6fa4-114">上述命令可在幾乎所有發行版本的 Linux 作業系統上運作，但不一定可在容器中運作，因為環境可能徹底受限。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="a6fa4-115">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="a6fa4-115">Detailed Walkthrough</span></span>

<span data-ttu-id="a6fa4-116">想要登入 Linux 伺服器，最簡單的方式是使用 SSH 公開和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="a6fa4-117">[公開金鑰密碼編譯](https://en.wikipedia.org/wiki/Public-key_cryptography) 會安全得多，因為密碼非常容易遭到暴力破解。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6fa4-118">公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="a6fa4-119">SSH 私密金鑰應該有[非常安全的密碼](https://www.xkcd.com/936/) (來源︰[xkcd.com](https://xkcd.com)) 來保護它。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="a6fa4-120">此密碼只能用於存取 SSH 私密金鑰，而 **不是** 使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="a6fa4-121">當您將密碼新增至 SSH 金鑰時，便會使用 128位元的 AES 來加密私密金鑰，而未利用密碼解密的私密金鑰沒有用處。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="a6fa4-122">如果攻擊者竊取您的私密金鑰，而且該金鑰沒有密碼，他們就能使用該私密金鑰來登入有對應公開金鑰的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="a6fa4-123">如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="a6fa4-124">本文會建立 SSH 通訊協定第 2 版 RSA 公開和私密金鑰檔案，這些檔案建議用於 Resource Manager 上的部署。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="a6fa4-125">ssh-rsa  金鑰是在[入口網站](https://portal.azure.com)上進行傳統部署和 Resource Manager 部署時的必要項目。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="a6fa4-126">藉由設定 SSH 金鑰來停用 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="a6fa4-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="a6fa4-127">Azure 需要至少 2048 位元的 ssh-rsa 格式公開和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="a6fa4-128">若要建立金鑰，請使用 `ssh-keygen`，在詢問一系列問題後，它便會編寫私密金鑰和對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="a6fa4-129">建立 Azure VM 時，公開金鑰會複製到 `~/.ssh/authorized_keys`。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="a6fa4-130">`~/.ssh/authorized_keys` 中的 SSH 金鑰用於挑戰用戶端，以符合 SSH 登入連線上的對應私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="a6fa4-131">使用用於驗證的 SSH 金鑰進行建立 Azure Linux VM 時，Azure 會將 SSHD 伺服器設定為不允許密碼登入，僅允許以 SSH 金鑰登入。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="a6fa4-132">因此，建立具 SSH 金鑰的 Azure Linux VM，即可協助保護 VM 部署的安全，並免除在 sshd_config 組態檔中停用密碼的標準部署後設定步驟。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="a6fa4-133">使用 ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="a6fa4-133">Using ssh-keygen</span></span>

<span data-ttu-id="a6fa4-134">此命令會使用 2048 位元 RSA 建立密碼保護 (加密) 的 SSH 金鑰組，並為其加上註解以供輕鬆識別。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="a6fa4-135">依預設，SSH 金鑰會保留在 `~/.ssh` 目錄中。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="a6fa4-136">如果您沒有 `~/.ssh` 目錄，`ssh-keygen` 命令會使用正確的權限為您建立。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="a6fa4-137">*命令的說明*</span><span class="sxs-lookup"><span data-stu-id="a6fa4-137">*Command explained*</span></span>

<span data-ttu-id="a6fa4-138">`ssh-keygen` = 用來建立金鑰的程式</span><span class="sxs-lookup"><span data-stu-id="a6fa4-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="a6fa4-139">`-t rsa` = 要建立的金鑰類型，也就是 RSA 格式 [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="a6fa4-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="a6fa4-140">`-b 2048` = 金鑰的位元</span><span class="sxs-lookup"><span data-stu-id="a6fa4-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="a6fa4-141">傳統入口網站和 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="a6fa4-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="a6fa4-142">如果您使用 Azure [傳統入口網站](https://manage.windowsazure.com/)，則需要適用於 SSH 金鑰的 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="a6fa4-143">不允許任何其他類型的 SSH 公開金鑰，而「必須」是 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="a6fa4-144">若要從現有的 SSH-RSA 私密金鑰建立 X.509 憑證︰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="a6fa4-145">使用 `asm` 進行傳統部署</span><span class="sxs-lookup"><span data-stu-id="a6fa4-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="a6fa4-146">如果您使用傳統部署模型 (Azure 服務管理 CLI `asm`)，您可以在 **.pem** 容器中使用 SSH-RSA 公開金鑰或 RFC4716 格式化的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="a6fa4-147">SSH-RSA 公開金鑰是稍早在本文中使用 `ssh-keygen` 建立的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="a6fa4-148">若要從現有的 SSH 公開金鑰建立 RFC4716 格式的金鑰︰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="a6fa4-149">ssh-keygen 的範例</span><span class="sxs-lookup"><span data-stu-id="a6fa4-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="a6fa4-150">已儲存金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="a6fa4-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="a6fa4-151">本文中的金鑰組名稱。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-151">The key pair name for this article.</span></span>  <span data-ttu-id="a6fa4-152">預設會有名為 **id_rsa** 的金鑰組，而且有些工具可能會預期私密金鑰的檔案名稱為 **id_rsa**，所以最好有此金鑰組。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="a6fa4-153">`~/.ssh/` 目錄是 SSH 金鑰組和 SSH 組態檔的預設位置。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="a6fa4-154">如果未指定完整路徑，則 `ssh-keygen` 會在目前的工作目錄 (而不是預設 `~/.ssh`) 中建立金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="a6fa4-155">`~/.ssh` 。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="a6fa4-156">金鑰密碼︰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="a6fa4-157">`ssh-keygen` 將用來加密私密金鑰的密碼稱為「複雜密碼」。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="a6fa4-158">「強烈」建議為金鑰組加上複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="a6fa4-159">若沒有使用複雜密碼來保護私密金鑰，任何人只要擁有該金鑰檔案，就可以用它登入具有對應公開金鑰的任何伺服器。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="a6fa4-160">新增複雜密碼可提升防護能力，以防有人能夠取得您的私密金鑰檔案，讓您有時間變更用來對您進行驗證的金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="a6fa4-161">使用 ssh-agent 來儲存您的私密金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="a6fa4-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="a6fa4-162">若要避免在每次 SSH 登入時輸入私密金鑰檔案複雜密碼，您可以使用 `ssh-agent` 來快取您的私密金鑰檔案密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="a6fa4-163">如果您使用 Mac，則 OSX 金鑰鏈會在您叫用 `ssh-agent`時安全地儲存私密金鑰密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="a6fa4-164">確認並使用 `ssh-agent` 和 `ssh-add` 將金鑰檔案通知 SSH 系統，才不需要以互動方式使用複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="a6fa4-165">現在使用 `ssh-add` 命令將私密金鑰加入至 `ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="a6fa4-166">私密金鑰密碼現已儲存在 `ssh-agent` 中。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="a6fa4-167">使用 `ssh-copy-id` 安裝新的金鑰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="a6fa4-168">如果您已建立 VM，您可以使用下列命令並以您自己的值取代 VM 使用者名稱和伺服器位址，來將新的 SSH 公開金鑰安裝至 Linux VM︰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="a6fa4-169">建立和設定 SSH 組態檔</span><span class="sxs-lookup"><span data-stu-id="a6fa4-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="a6fa4-170">最佳做法是建立及設定 `~/.ssh/config` 檔案來加速登入，並且最佳化您的 SSH 用戶端行為。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="a6fa4-171">下列範例將示範標準組態。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="a6fa4-172">建立檔案</span><span class="sxs-lookup"><span data-stu-id="a6fa4-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="a6fa4-173">編輯檔案以加入新的 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="a6fa4-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="a6fa4-174">範例 `~/.ssh/config` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="a6fa4-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="a6fa4-175">此 SSH 組態可讓您將各個伺服器分段，讓它們各自擁有專用的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="a6fa4-176">預設設定 (`Host *`) 適用於不符合組態檔中任何提升之特定主機的任何主機。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="a6fa4-177">組態檔的說明</span><span class="sxs-lookup"><span data-stu-id="a6fa4-177">Config file explained</span></span>

<span data-ttu-id="a6fa4-178">`Host` = 在終端機上所呼叫的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="a6fa4-179">`ssh fedora22` 會指示 `SSH` 使用設定區塊中標示為 `Host fedora22` 的值。注意︰這可以是符合您用途的任何標籤，並不代表任何伺服器的實際主機名稱。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="a6fa4-180">`Hostname 102.160.203.241` = 所存取伺服器的 IP 位址或 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="a6fa4-181">`User ahmet` = 登入伺服器時要使用的遠端使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="a6fa4-182">`PubKeyAuthentication yes` = 向 SSH 指出您想要使用 SSH 金鑰來登入。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="a6fa4-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = 要用於驗證的 SSH 私密金鑰和對應公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="a6fa4-184">使用 SSH 登入 Linux 而不提供密碼</span><span class="sxs-lookup"><span data-stu-id="a6fa4-184">SSH into Linux without a password</span></span>

<span data-ttu-id="a6fa4-185">您現在已擁有 SSH 金鑰組和設定好的 SSH 組態檔，因此能夠快速且安全地登入 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="a6fa4-186">第一次使用 SSH 金鑰登入伺服器時，命令會提示您輸入該金鑰檔案的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="a6fa4-187">命令的說明</span><span class="sxs-lookup"><span data-stu-id="a6fa4-187">Command explained</span></span>

<span data-ttu-id="a6fa4-188">在執行 `ssh fedora22` 後，SSH 會先從 `Host fedora22` 區塊中找出所有設定並加以載入，再從最後一個區塊 `Host *` 中載入所有其餘設定。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6fa4-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a6fa4-189">Next Steps</span></span>

<span data-ttu-id="a6fa4-190">接下來是使用新的 SSH 公開金鑰建立 Azure Linux VM。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="a6fa4-191">相較於以預設登入方法密碼建立的 VM，以 SSH 公開金鑰作為登入所建立的 Azure VM 比較安全。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="a6fa4-192">使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="a6fa4-193">如果您需要更多關於建立 SSH 金鑰組的協助，或需要其他憑證，例如以便用於傳統入口網站，請參閱[建立 SSH 金鑰組和憑證的詳細步驟](create-ssh-keys-detailed.md)。</span><span class="sxs-lookup"><span data-stu-id="a6fa4-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="a6fa4-194">使用 Azure 範本建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a6fa4-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a6fa4-195">使用 Azure 入口網站建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a6fa4-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="a6fa4-196">使用 Azure CLI 建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a6fa4-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
