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
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="8310e-103">建立 Linux VM 的 SSH 公用和私用金鑰組</span><span class="sxs-lookup"><span data-stu-id="8310e-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="8310e-104">本文章將示範如何 toogenerate SSH 通訊協定第 2 版 RSA 公用和私用金鑰檔案對 toouse 使用 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="8310e-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="8310e-105">SSH 金鑰組，您可以預設 toousing SSH 金鑰進行驗證，免除對密碼 toolog 中的 hello 需要的 Azure 上建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8310e-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="8310e-106">密碼可以猜到，並開啟 Vm toorelentless 暴力嘗試 tooguess 註冊您的密碼。</span><span class="sxs-lookup"><span data-stu-id="8310e-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="8310e-107">建立與 Azure 範本或 hello Vm`azure-cli`可以包含 SSH 公開金鑰，做為 hello 部署中，移除停用 SSH 密碼登入的 post 部署組態步驟的一部分。</span><span class="sxs-lookup"><span data-stu-id="8310e-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8310e-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="8310e-108">Quick Commands</span></span>

<span data-ttu-id="8310e-109">執行 hello Bash 殼層中的下列命令，以自己選擇取代 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="8310e-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="8310e-110">SSH 公開金鑰檔預設會建立在 `~/.ssh/id_rsa.pub`。</span><span class="sxs-lookup"><span data-stu-id="8310e-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="8310e-111">當系統提示您使用下列命令的 hello，您應該建立 「 複雜密碼 」 toosecure 您的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="8310e-112">（hello 複雜密碼是使用密碼 tooencrypt 您的私密金鑰）。</span><span class="sxs-lookup"><span data-stu-id="8310e-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="8310e-113">加入新建立的 hello 金鑰太`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="8310e-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="8310e-114">hello Linux 作業系統的幾乎所有的發佈，在上述命令但不是一定能在容器中，做為 hello 環境可以徹底條件約束。</span><span class="sxs-lookup"><span data-stu-id="8310e-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="8310e-115">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="8310e-115">Detailed Walkthrough</span></span>

<span data-ttu-id="8310e-116">使用 SSH 公開金鑰和私密金鑰的金鑰是 hello 最簡單方式 toolog tooyour Linux 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="8310e-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="8310e-117">[公開金鑰加密](https://en.wikipedia.org/wiki/Public-key_cryptography)比密碼，可以是暴力密碼破解強制更輕鬆地提供更安全的方式 toolog tooyour Linux 中或在 Azure 中的 BSD VM。</span><span class="sxs-lookup"><span data-stu-id="8310e-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8310e-118">公開金鑰可以與任何人共用；但只有您 (或您的本機安全性基礎結構) 會擁有私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="8310e-119">hello SSH 私密金鑰應有[非常安全的密碼](https://www.xkcd.com/936/)(來源：[xkcd.com](https://xkcd.com)) toosafeguard 它。</span><span class="sxs-lookup"><span data-stu-id="8310e-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="8310e-120">此密碼是只 tooaccess hello SSH 私密金鑰和**不**hello 使用者帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="8310e-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="8310e-121">當您新增密碼 tooyour SSH 金鑰時，它 hello 私密金鑰加密使用 128 位元 AES 使 hello 私用金鑰變成毫無用處，而不 hello 密碼 toodecrypt 它。</span><span class="sxs-lookup"><span data-stu-id="8310e-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="8310e-122">如果攻擊者偷走了您的私密金鑰，且索引鍵沒有密碼，其方式是根據可以 toouse，私用金鑰 toolog tooany 伺服器具有 hello 對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="8310e-123">如果私密金鑰受密碼保護，攻擊者就無法使用該金鑰，進而為您在 Azure 上的基礎結構提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="8310e-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="8310e-124">這篇文章建立 SSH 通訊協定版本 2 RSA 公用和私密金鑰檔案，這建議的作法 hello 資源管理員的部署。</span><span class="sxs-lookup"><span data-stu-id="8310e-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="8310e-125">*ssh rsa* hello 上需要索引鍵[入口網站](https://portal.azure.com)傳統和資源管理員部署。</span><span class="sxs-lookup"><span data-stu-id="8310e-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="8310e-126">藉由設定 SSH 金鑰來停用 SSH 密碼</span><span class="sxs-lookup"><span data-stu-id="8310e-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="8310e-127">Azure 需要至少 2048 位元的 ssh-rsa 格式公開和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="8310e-128">toocreate hello 索引鍵使用`ssh-keygen`，這會要求一系列的問題，並再將私用金鑰和對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="8310e-129">建立 Azure VM 時，會太複製 hello 公開金鑰`~/.ssh/authorized_keys`。</span><span class="sxs-lookup"><span data-stu-id="8310e-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="8310e-130">SSH 金鑰在`~/.ssh/authorized_keys`會使用的 toochallenge hello 用戶端 toomatch hello 對應的私密金鑰上 SSH 登入連線。</span><span class="sxs-lookup"><span data-stu-id="8310e-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="8310e-131">Azure Linux VM 建立時使用 SSH 金鑰進行驗證，Azure 會設定 hello SSHD 伺服器 toonot 允許密碼登入，則只有 SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="8310e-132">因此，您可以藉由使用 SSH 金鑰建立 Azure Linux Vm，協助安全 hello VM 部署及儲存自行停用密碼 hello sshd_config 組態檔中的 hello 一般的部署後設定步驟。</span><span class="sxs-lookup"><span data-stu-id="8310e-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="8310e-133">使用 ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="8310e-133">Using ssh-keygen</span></span>

<span data-ttu-id="8310e-134">此命令會建立保護 （加密） 使用 2048年位元 RSA 的 SSH 金鑰組的密碼，而且它會取消註 tooeasily 識別它。</span><span class="sxs-lookup"><span data-stu-id="8310e-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="8310e-135">SSH 金鑰依預設，會保留在 hello`~/.ssh`目錄。</span><span class="sxs-lookup"><span data-stu-id="8310e-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="8310e-136">如果您不需要`~/.ssh`目錄、 hello`ssh-keygen`命令就會為您建立以 hello 正確的權限。</span><span class="sxs-lookup"><span data-stu-id="8310e-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="8310e-137">*命令的說明*</span><span class="sxs-lookup"><span data-stu-id="8310e-137">*Command explained*</span></span>

<span data-ttu-id="8310e-138">`ssh-keygen`= hello 用程式 toocreate hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="8310e-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="8310e-139">`-t rsa`= 索引鍵 toocreate hello RSA 格式的類型 [維基百科](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="8310e-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="8310e-140">`-b 2048`= 位元的 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="8310e-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="8310e-141">傳統入口網站和 X.509 憑證</span><span class="sxs-lookup"><span data-stu-id="8310e-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="8310e-142">如果您使用 hello Azure[傳統入口網站](https://manage.windowsazure.com/)，hello SSH 金鑰需要 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="8310e-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="8310e-143">不允許任何其他類型的 SSH 公開金鑰，而「必須」是 X.509 憑證。</span><span class="sxs-lookup"><span data-stu-id="8310e-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="8310e-144">toocreate 從您現有的 SSH RSA 私密金鑰的 X.509 憑證：</span><span class="sxs-lookup"><span data-stu-id="8310e-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="8310e-145">使用 `asm` 進行傳統部署</span><span class="sxs-lookup"><span data-stu-id="8310e-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="8310e-146">如果您使用 hello 傳統部署模型 (Azure 服務管理 CLI `asm`)，您可以使用 SSH RSA 公開金鑰或 RFC4716 格式中的索引鍵**.pem**容器。</span><span class="sxs-lookup"><span data-stu-id="8310e-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="8310e-147">hello SSH RSA 公開金鑰是稍早在此發行項使用中已建立的內容`ssh-keygen`。</span><span class="sxs-lookup"><span data-stu-id="8310e-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="8310e-148">toocreate RFC4716 格式化從現有的 SSH 公開金鑰的金鑰：</span><span class="sxs-lookup"><span data-stu-id="8310e-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="8310e-149">ssh-keygen 的範例</span><span class="sxs-lookup"><span data-stu-id="8310e-149">Example of ssh-keygen</span></span>

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

<span data-ttu-id="8310e-150">已儲存金鑰檔案：</span><span class="sxs-lookup"><span data-stu-id="8310e-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="8310e-151">這個發行項的 hello 金鑰組名稱。</span><span class="sxs-lookup"><span data-stu-id="8310e-151">hello key pair name for this article.</span></span>  <span data-ttu-id="8310e-152">具有名為的金鑰組**id_rsa**是 hello 預設值，而且某些工具可能預期 hello **id_rsa**私密金鑰檔案名稱，因此保留其中一個是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="8310e-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="8310e-153">hello 目錄`~/.ssh/`是 hello SSH 金鑰組和 hello SSH 組態檔的預設位置。</span><span class="sxs-lookup"><span data-stu-id="8310e-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="8310e-154">如果未指定具有完整路徑，`ssh-keygen`將 hello 目前工作目錄中建立 hello 金鑰、 不 hello 預設`~/.ssh`。</span><span class="sxs-lookup"><span data-stu-id="8310e-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="8310e-155">Hello 清單`~/.ssh`目錄。</span><span class="sxs-lookup"><span data-stu-id="8310e-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="8310e-156">金鑰密碼︰</span><span class="sxs-lookup"><span data-stu-id="8310e-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="8310e-157">`ssh-keygen`參考 tooa 用密碼 tooencrypt hello 私用金鑰做為 「 複雜密碼。 」</span><span class="sxs-lookup"><span data-stu-id="8310e-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="8310e-158">它是*強*建議 tooadd 複雜密碼 tooyour 金鑰組。</span><span class="sxs-lookup"><span data-stu-id="8310e-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="8310e-159">不需要複雜密碼保護 hello 私用金鑰，與 hello 金鑰檔案的任何人都可以使用它 toolog tooany server 中具有 hello 對應的公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="8310e-160">加入複雜密碼提供更多的保護，以防其他人可以 toogain 存取 tooyour 私密金鑰檔案，讓您時間 toochange hello 索引鍵用於 tooauthenticate 您。</span><span class="sxs-lookup"><span data-stu-id="8310e-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="8310e-161">使用 ssh 代理 toostore 私用金鑰密碼</span><span class="sxs-lookup"><span data-stu-id="8310e-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="8310e-162">tooavoid 輸入您的私密金鑰檔案的複雜密碼與每個 SSH 登入，您可以使用`ssh-agent`toocache 您私密金鑰檔案的密碼。</span><span class="sxs-lookup"><span data-stu-id="8310e-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="8310e-163">如果您使用的 Mac，hello OSX Keychain 會安全地儲存 hello 私用金鑰的密碼當您叫用`ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="8310e-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="8310e-164">驗證並使用`ssh-agent`和`ssh-add`tooinform hello SSH hello 金鑰檔案的相關的系統，以便 hello 複雜密碼不需要以互動方式使用 toobe。</span><span class="sxs-lookup"><span data-stu-id="8310e-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="8310e-165">現在，加入 hello 私密金鑰太`ssh-agent`使用 hello 命令`ssh-add`。</span><span class="sxs-lookup"><span data-stu-id="8310e-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="8310e-166">hello 私密金鑰密碼現在儲存在`ssh-agent`。</span><span class="sxs-lookup"><span data-stu-id="8310e-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="8310e-167">使用`ssh-copy-id`tooinstall hello 新金鑰</span><span class="sxs-lookup"><span data-stu-id="8310e-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="8310e-168">如果您已經建立 VM 您可以使用下列命令，以您自己的值取代 hello VM 使用者名稱和 hello 伺服器位址的 hello 安裝 hello 新 SSH 公用金鑰 tooyour Linux VM:</span><span class="sxs-lookup"><span data-stu-id="8310e-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="8310e-169">建立和設定 SSH 組態檔</span><span class="sxs-lookup"><span data-stu-id="8310e-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="8310e-170">它是最佳的作法 toocreate 及設定`~/.ssh/config`向上檔案 toospeed 登入並最佳化您的 SSH 用戶端行為。</span><span class="sxs-lookup"><span data-stu-id="8310e-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="8310e-171">下列範例中的 hello 顯示標準的設定。</span><span class="sxs-lookup"><span data-stu-id="8310e-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="8310e-172">建立 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="8310e-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="8310e-173">編輯 hello 檔案 tooadd hello 新 SSH 組態：</span><span class="sxs-lookup"><span data-stu-id="8310e-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="8310e-174">範例 `~/.ssh/config` 檔案︰</span><span class="sxs-lookup"><span data-stu-id="8310e-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="8310e-175">這的 SSH 組態讓您區段的每個伺服器 tooenable 每個 toohave 自己專用的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="8310e-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="8310e-176">hello 預設設定 (`Host *`)，適用於不符合任何 hello 特定主機的高的層級 hello 設定檔中的任何主機。</span><span class="sxs-lookup"><span data-stu-id="8310e-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="8310e-177">組態檔的說明</span><span class="sxs-lookup"><span data-stu-id="8310e-177">Config file explained</span></span>

<span data-ttu-id="8310e-178">`Host`= hello hello 主機上呼叫 hello 終端機名稱。</span><span class="sxs-lookup"><span data-stu-id="8310e-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="8310e-179">`ssh fedora22`會告知`SSH`toouse 標示為 hello settings 區塊中的 hello 值`Host fedora22`附註： 主機可供您使用的邏輯，且不代表 hello 的任何伺服器的實際主機名稱的任何標籤。</span><span class="sxs-lookup"><span data-stu-id="8310e-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="8310e-180">`Hostname 102.160.203.241`= hello IP 位址或 DNS 名稱而存取的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8310e-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="8310e-181">`User ahmet`登入時 toohello server = hello 遠端使用者帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="8310e-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="8310e-182">`PubKeyAuthentication yes`= 告訴 SSH 想 toouse SSH 金鑰 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="8310e-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="8310e-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= hello SSH 私密金鑰與對應公用金鑰 toouse 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="8310e-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="8310e-184">使用 SSH 登入 Linux 而不提供密碼</span><span class="sxs-lookup"><span data-stu-id="8310e-184">SSH into Linux without a password</span></span>

<span data-ttu-id="8310e-185">現在您擁有的 SSH 金鑰組與設定的 SSH 組態檔，您就可以 toolog tooyour Linux VM 中的快速且安全的方式。</span><span class="sxs-lookup"><span data-stu-id="8310e-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="8310e-186">hello 第一次登入使用 SSH 金鑰 hello 命令提示字元 tooa 伺服器您 hello 複雜密碼，該金鑰的檔案。</span><span class="sxs-lookup"><span data-stu-id="8310e-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="8310e-187">命令的說明</span><span class="sxs-lookup"><span data-stu-id="8310e-187">Command explained</span></span>

<span data-ttu-id="8310e-188">當`ssh fedora22`執行 SSH 先找出並載入任何設定，從 hello`Host fedora22`區塊，然後按一下 所有 hello 剩餘 hello 最後一個區塊中，從設定載入`Host *`。</span><span class="sxs-lookup"><span data-stu-id="8310e-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8310e-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8310e-189">Next Steps</span></span>

<span data-ttu-id="8310e-190">接下來向上 toocreate Azure Linux Vm 使用 hello 新 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="8310e-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="8310e-191">SSH 公開金鑰為 hello 登入，以建立 azure Vm 是比較安全比 hello 預設登入方法，密碼建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8310e-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="8310e-192">使用 SSH 金鑰建立的 Azure VM 預設會設定為停用密碼，避免遭到暴力猜測嘗試。</span><span class="sxs-lookup"><span data-stu-id="8310e-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="8310e-193">如果您需要更多協助建立您的 SSH 金鑰組，或需要其他憑證，例如，針對搭配 hello 傳統入口網站，請參閱[詳細步驟 toocreate SSH 金鑰組和憑證](create-ssh-keys-detailed.md)。</span><span class="sxs-lookup"><span data-stu-id="8310e-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="8310e-194">使用 Azure 範本建立安全的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="8310e-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8310e-195">建立安全的 Linux VM，使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8310e-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="8310e-196">建立安全的 Linux VM，使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="8310e-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
