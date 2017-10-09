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
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="fc5a3-103">Toocreate 的 SSH 金鑰組和其他 Linux VM 在 Azure 中憑證的詳細的逐步</span><span class="sxs-lookup"><span data-stu-id="fc5a3-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="fc5a3-104">SSH 金鑰組，您可以預設 toousing SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 上建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="fc5a3-105">密碼可以猜到，並開啟 Vm toorelentless 暴力嘗試 tooguess 註冊您的密碼。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="fc5a3-106">Hello Azure CLI 或資源管理員範本所建立的 Vm 可以包含 SSH 公開金鑰 hello 部署中，移除停用 SSH 密碼登入的 post 部署組態步驟的一部分。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="fc5a3-107">針對用於 Linux 虛擬機器之類的憑證，本文提供產生憑證的詳細步驟和其他範例。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="fc5a3-108">如果您想 tooquickly 建立及使用 SSH 金鑰組，請參閱[toocreate SSH 公用和私用金鑰配對適用於 Linux Vm 在 Azure 中的方式](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="fc5a3-109">了解 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="fc5a3-109">Understanding SSH keys</span></span>

<span data-ttu-id="fc5a3-110">使用 SSH 公開金鑰和私密金鑰的金鑰是 hello 最簡單方式 toolog tooyour Linux 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="fc5a3-111">[公開金鑰加密](https://en.wikipedia.org/wiki/Public-key_cryptography)比密碼，可以是暴力密碼破解強制更輕鬆地提供更安全的方式 toolog tooyour Linux 中或在 Azure 中的 BSD VM。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="fc5a3-112">公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="fc5a3-113">hello SSH 私密金鑰應有[非常安全的密碼](https://www.xkcd.com/936/)(來源：[xkcd.com](https://xkcd.com)) toosafeguard 它。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="fc5a3-114">此密碼是只 tooaccess hello 私用 SSH 金鑰檔案並**不**hello 使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="fc5a3-115">當您新增密碼 tooyour SSH 金鑰時，它 hello 私密金鑰加密使用 128 位元 AES 使 hello 私用金鑰變成毫無用處，而不 hello 密碼 toodecrypt 它。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="fc5a3-116">如果攻擊者偷走了您的私密金鑰，且索引鍵沒有密碼，其方式是根據可以 toouse，私用金鑰 toolog tooany 伺服器具有 hello 對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="fc5a3-117">如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="fc5a3-118">這篇文章建立 SSH 通訊協定版本 2 RSA 公用和私用金鑰的檔案組 （也參考的 tooas"ssh rsa"索引鍵），這建議用於部署與 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="fc5a3-119">*ssh rsa* hello 上需要索引鍵[入口網站](https://portal.azure.com)傳統和資源管理員部署。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="fc5a3-120">SSH 金鑰的使用和好處</span><span class="sxs-lookup"><span data-stu-id="fc5a3-120">SSH keys use and benefits</span></span>

<span data-ttu-id="fc5a3-121">Azure 需要有至少 2048年位元，SSH 通訊協定第 2 版 RSA 格式公用和私用金鑰。hello 公開金鑰檔案具有 hello`.pub`容器格式。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="fc5a3-122">toocreate hello 索引鍵使用`ssh-keygen`，這會要求一系列的問題，並再將私用金鑰和對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="fc5a3-123">建立 Azure VM 時，Azure 複本 hello 公用金鑰 toohello `~/.ssh/authorized_keys` hello VM 上的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="fc5a3-124">SSH 金鑰在`~/.ssh/authorized_keys`會使用的 toochallenge hello 用戶端 toomatch hello 對應的私密金鑰上 SSH 登入連線。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="fc5a3-125">Azure Linux VM 建立時使用 SSH 金鑰進行驗證，Azure 會設定 hello SSHD 伺服器 toonot 允許密碼登入，則只有 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="fc5a3-126">因此，藉由使用 SSH 金鑰建立 Azure Linux Vm，您可以協助保護 hello VM 部署，並儲存您自己的停用密碼的 hello hello 一般的部署後設定步驟**sshd_config**檔案。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="fc5a3-127">使用 ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="fc5a3-127">Using ssh-keygen</span></span>

<span data-ttu-id="fc5a3-128">此命令會建立保護 （加密） 使用 2048年位元 RSA 的 SSH 金鑰組的密碼，而且它會取消註 tooeasily 識別它。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="fc5a3-129">SSH 金鑰依預設，會保留在 hello`~/.ssh`目錄。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="fc5a3-130">如果您不需要`~/.ssh`目錄、 hello`ssh-keygen`命令就會為您建立以 hello 正確的權限。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="fc5a3-131">*命令的說明*</span><span class="sxs-lookup"><span data-stu-id="fc5a3-131">*Command explained*</span></span>

<span data-ttu-id="fc5a3-132">`ssh-keygen`= hello 用程式 toocreate hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="fc5a3-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="fc5a3-133">`-t rsa`= 索引鍵 toocreate hello RSA 格式 [維基百科] 的型別[括弧結尾](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
 `-b 2048` = 位元的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="fc5a3-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="fc5a3-134">`-C "azureuser@myserver"`= 附加的 toohello 結尾 hello 公開金鑰檔案 tooeasily 識別該註解。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="fc5a3-135">通常一封電子郵件做為 hello 註解，但您可以使用任何最適合您的基礎結構。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="fc5a3-136">使用 `asm` 進行傳統部署</span><span class="sxs-lookup"><span data-stu-id="fc5a3-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="fc5a3-137">如果您使用 hello 傳統部署模型 (`asm` hello CLI 中的模式)，您可以使用 SSH RSA 公開金鑰或 RFC4716 格式化的 pem 容器中的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="fc5a3-138">hello SSH RSA 公開金鑰是稍早在此發行項使用中已建立的內容`ssh-keygen`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="fc5a3-139">toocreate RFC4716 格式化從現有的 SSH 公開金鑰的金鑰：</span><span class="sxs-lookup"><span data-stu-id="fc5a3-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="fc5a3-140">ssh-keygen 的範例</span><span class="sxs-lookup"><span data-stu-id="fc5a3-140">Example of ssh-keygen</span></span>

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

<span data-ttu-id="fc5a3-141">已儲存金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="fc5a3-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="fc5a3-142">這個發行項的 hello 金鑰組名稱。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-142">hello key pair name for this article.</span></span>  <span data-ttu-id="fc5a3-143">具有名為的金鑰組**id_rsa**是 hello 預設值，而且某些工具可能預期 hello **id_rsa**私密金鑰檔案名稱，因此保留其中一個是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="fc5a3-144">hello 目錄`~/.ssh/`是 hello SSH 金鑰組和 hello SSH 組態檔的預設位置。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="fc5a3-145">如果未指定具有完整路徑， `ssh-keygen` hello 的目前工作目錄，而不是 hello 預設中建立 hello 金鑰`~/.ssh`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="fc5a3-146">Hello 清單`~/.ssh`目錄。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="fc5a3-147">金鑰密碼︰</span><span class="sxs-lookup"><span data-stu-id="fc5a3-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="fc5a3-148">`ssh-keygen`指 hello 私密金鑰檔案的 tooa 密碼是做為 「 複雜密碼。 」</span><span class="sxs-lookup"><span data-stu-id="fc5a3-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="fc5a3-149">它是*強*建議 tooadd 密碼 tooyour 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="fc5a3-150">不使用密碼保護 hello 金鑰檔案，與 hello 檔案的任何人都可以使用它 toolog tooany 伺服器具有 hello 對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="fc5a3-151">新增密碼 （複雜） 提供更多的保護，以防其他人可以 toogain 存取 tooyour 私密金鑰檔案，提供您時間 toochange hello 索引鍵用於 tooauthenticate 您。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="fc5a3-152">使用 ssh 代理 toostore 私用金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="fc5a3-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="fc5a3-153">tooavoid 輸入私密金鑰檔案密碼的每一個 SSH 登入，您可以使用`ssh-agent`toocache 您私密金鑰檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="fc5a3-154">如果您使用的 Mac，hello OSX Keychain 會安全地儲存 hello 私用金鑰的密碼當您叫用`ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="fc5a3-155">驗證及使用 ssh 代理程式並 ssh-加入 hello 金鑰檔案的相關 tooinform hello SSH 系統以便 hello 複雜密碼不需要以互動方式使用 toobe。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="fc5a3-156">現在，加入 hello 私密金鑰太`ssh-agent`使用 hello 命令`ssh-add`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="fc5a3-157">hello 私密金鑰密碼現在儲存在`ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="fc5a3-158">使用`ssh-copy-id`toocopy hello 金鑰 tooan 現有的 VM</span><span class="sxs-lookup"><span data-stu-id="fc5a3-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="fc5a3-159">如果您已經建立 VM，您就可以安裝 hello 新 SSH 公用金鑰 tooyour Linux VM 使用：</span><span class="sxs-lookup"><span data-stu-id="fc5a3-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="fc5a3-160">建立和設定 SSH 組態檔</span><span class="sxs-lookup"><span data-stu-id="fc5a3-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="fc5a3-161">它是建議的最佳作法 toocreate 及設定`~/.ssh/config`向上檔案 toospeed 登入並最佳化您的 SSH 用戶端行為。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="fc5a3-162">下列範例中的 hello 顯示標準的設定。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="fc5a3-163">建立 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="fc5a3-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="fc5a3-164">編輯 hello 檔案 tooadd hello 新 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="fc5a3-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="fc5a3-165">範例 `~/.ssh/config` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="fc5a3-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="fc5a3-166">這的 SSH 組態讓您區段的每個伺服器 tooenable 每個 toohave 自己專用的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="fc5a3-167">hello 預設設定 (`Host *`)，適用於不符合任何 hello 特定主機的高的層級 hello 設定檔中的任何主機。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="fc5a3-168">組態檔的說明</span><span class="sxs-lookup"><span data-stu-id="fc5a3-168">Config file explained</span></span>

<span data-ttu-id="fc5a3-169">`Host`= hello hello 主機上呼叫 hello 終端機名稱。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="fc5a3-170">`ssh fedora22`會告知`SSH`toouse 標示為 hello settings 區塊中的 hello 值`Host fedora22`附註： 主機可供您使用的邏輯，且不代表 hello 的任何伺服器的實際主機名稱的任何標籤。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="fc5a3-171">`Hostname 102.160.203.241`= hello IP 位址或 DNS 名稱而存取的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="fc5a3-172">`User ahmet`登入時 toohello server = hello 遠端使用者帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="fc5a3-173">`PubKeyAuthentication yes`= 告訴 SSH 想 toouse SSH 金鑰 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="fc5a3-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH 私密金鑰與對應公用金鑰 toouse 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="fc5a3-175">使用 SSH 登入 Linux 而不提供密碼</span><span class="sxs-lookup"><span data-stu-id="fc5a3-175">SSH into Linux without a password</span></span>

<span data-ttu-id="fc5a3-176">現在您擁有的 SSH 金鑰組與設定的 SSH 組態檔，您就可以 toolog tooyour Linux VM 中的快速且安全的方式。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="fc5a3-177">hello 第一次登入使用 SSH 金鑰 hello 命令提示字元 tooa 伺服器您 hello 複雜密碼，該金鑰的檔案。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="fc5a3-178">命令的說明</span><span class="sxs-lookup"><span data-stu-id="fc5a3-178">Command explained</span></span>

<span data-ttu-id="fc5a3-179">當`ssh fedora22`執行 SSH 先找出並載入任何設定，從 hello`Host fedora22`區塊，然後按一下 所有 hello 剩餘 hello 最後一個區塊中，從設定載入`Host *`。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc5a3-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc5a3-180">Next Steps</span></span>

<span data-ttu-id="fc5a3-181">接下來向上 toocreate Azure Linux Vm 使用 hello 新 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="fc5a3-182">SSH 公開金鑰為 hello 登入，以建立 azure Vm 是比較安全比 hello 預設登入方法，密碼建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="fc5a3-183">使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。</span><span class="sxs-lookup"><span data-stu-id="fc5a3-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="fc5a3-184">使用 Azure 範本建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="fc5a3-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fc5a3-185">建立安全的 Linux VM，使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fc5a3-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="fc5a3-186">建立安全的 Linux VM，使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="fc5a3-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
