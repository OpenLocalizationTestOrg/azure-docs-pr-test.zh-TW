---
title: "適用於 Linux Vm aaaUse SSH 金鑰與 Windows |Microsoft 文件"
description: "了解如何 toogenerate 及使用 SSH 金鑰的 Windows 電腦 tooconnect tooa Linux 虛擬機器上 Azure。"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="9b97a-103">TooUse SSH 與 Windows Azure 上的索引鍵</span><span class="sxs-lookup"><span data-stu-id="9b97a-103">How tooUse SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b97a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="9b97a-104">Windows</span></span>](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [<span data-ttu-id="9b97a-105">Linux/Mac</span><span class="sxs-lookup"><span data-stu-id="9b97a-105">Linux/Mac</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="9b97a-106">當您連接 tooLinux Azure 虛擬機器 (Vm) 中時，您應該使用[公開金鑰密碼編譯](https://wikipedia.org/wiki/Public-key_cryptography)tooprovide 更安全的方式 toolog tooyour Linux VM 中。</span><span class="sxs-lookup"><span data-stu-id="9b97a-106">When you connect tooLinux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide a more secure way toolog in tooyour Linux VM.</span></span> <span data-ttu-id="9b97a-107">此程序牽涉到自行使用 hello 安全殼層 (SSH) 命令 tooauthenticate，而不使用者名稱和密碼的公用和私用金鑰交換。</span><span class="sxs-lookup"><span data-stu-id="9b97a-107">This process involves a public and private key exchange using hello secure shell (SSH) command tooauthenticate yourself rather than a username and password.</span></span> <span data-ttu-id="9b97a-108">密碼是很容易遭受 toobrute 強制的攻擊，尤其是在網際網路對向 Vm，例如網頁伺服器上。</span><span class="sxs-lookup"><span data-stu-id="9b97a-108">Passwords are vulnerable toobrute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="9b97a-109">本文提供的 SSH 金鑰和 toogenerate hello 適當的 Windows 電腦上的索引鍵的方式的概觀。</span><span class="sxs-lookup"><span data-stu-id="9b97a-109">This article provides an overview of SSH keys and how toogenerate hello appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="9b97a-110">SSH 和金鑰的概觀</span><span class="sxs-lookup"><span data-stu-id="9b97a-110">Overview of SSH and keys</span></span>
<span data-ttu-id="9b97a-111">您可以安全地登入 tooyour Linux VM 使用公開和私密金鑰：</span><span class="sxs-lookup"><span data-stu-id="9b97a-111">You can securely log in tooyour Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="9b97a-112">hello**公開金鑰**置於 Linux VM 或您想 toouse 公開金鑰加密中使用的任何其他服務。</span><span class="sxs-lookup"><span data-stu-id="9b97a-112">hello **public key** is placed on your Linux VM, or any other service that you wish toouse with public-key cryptography.</span></span>
* <span data-ttu-id="9b97a-113">hello**私密金鑰**時，您有 tooyour Linux VM 登入時，tooverify 您的身分識別。</span><span class="sxs-lookup"><span data-stu-id="9b97a-113">hello **private key** is what you present tooyour Linux VM when you log in, tooverify your identity.</span></span> <span data-ttu-id="9b97a-114">保護此私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-114">Protect this private key.</span></span> <span data-ttu-id="9b97a-115">不要共用它。</span><span class="sxs-lookup"><span data-stu-id="9b97a-115">Do not share it.</span></span>

<span data-ttu-id="9b97a-116">這些公用和私密金鑰可以使用於多個 VM 和服務。</span><span class="sxs-lookup"><span data-stu-id="9b97a-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="9b97a-117">您不需要針對每個 VM 或服務想 tooaccess 的金鑰組。</span><span class="sxs-lookup"><span data-stu-id="9b97a-117">You do not need a pair of keys for each VM or service you wish tooaccess.</span></span> <span data-ttu-id="9b97a-118">如需更詳細的概觀，請參閱[公開金鑰加密](https://wikipedia.org/wiki/Public-key_cryptography)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="9b97a-119">SSH 是允許透過不安全的連線進行安全登入的加密連線通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b97a-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="9b97a-120">它是在 Azure 中裝載的 Linux Vm 的 hello 預設連線通訊協定。</span><span class="sxs-lookup"><span data-stu-id="9b97a-120">It is hello default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="9b97a-121">雖然本身 SSH 提供加密的連接，但是使用 SSH 連線的密碼會保留 hello VM 很容易遭受 toobrute 強制攻擊或破解的密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves hello VM vulnerable toobrute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="9b97a-122">使用 SSH 的 VM 是使用這些公用和私用金鑰，也稱為 SSH 金鑰連接 tooa 更為安全且慣用方法。</span><span class="sxs-lookup"><span data-stu-id="9b97a-122">A more secure and preferred method of connecting tooa VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="9b97a-123">如果您不想 toouse SSH 金鑰，您仍然可以記錄 tooyour Linux Vm 使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-123">If you do not wish toouse SSH keys, you can still log in tooyour Linux VMs using a password.</span></span> <span data-ttu-id="9b97a-124">如果您的 VM 不公開的 toohello 網際網路，請使用密碼可能不足。</span><span class="sxs-lookup"><span data-stu-id="9b97a-124">If your VM is not exposed toohello Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="9b97a-125">不過，您仍然需要為每個 Linux VM toomanage 您的密碼，並維護狀況良好的密碼原則和作法，例如最小密碼長度和定期更新它們。</span><span class="sxs-lookup"><span data-stu-id="9b97a-125">However, you still need toomanage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="9b97a-126">hello 使用 SSH 金鑰可降低管理跨多個 Vm 的個別認證 hello 複雜性。</span><span class="sxs-lookup"><span data-stu-id="9b97a-126">hello use of SSH keys reduces hello complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="9b97a-127">Windows 套件和 SSH 用戶端</span><span class="sxs-lookup"><span data-stu-id="9b97a-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="9b97a-128">連接 tooand 管理 Linux Vm 在 Azure 中使用**SSH 用戶端**。</span><span class="sxs-lookup"><span data-stu-id="9b97a-128">You connect tooand manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="9b97a-129">Windows 電腦通常不會安裝 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="9b97a-130">Windows 10 年度更新 hello 加入撞 for Windows，並 hello 最新的 Windows 10 建立者更新提供其他的更新。</span><span class="sxs-lookup"><span data-stu-id="9b97a-130">hello Windows 10 Anniversary Update added Bash for Windows, and hello latest Windows 10 Creators Update provides additional updates.</span></span> <span data-ttu-id="9b97a-131">這個適用於 Linux 的 Windows 子系統，可讓您 toorun 及存取公用程式，例如 Bash 殼層中的原生的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-131">This Windows Subsystem for Linux allows you toorun and access utilities such as an SSH client natively within a Bash shell.</span></span> <span data-ttu-id="9b97a-132">您可以依照任何 hello Linux 文件，例如[如何 toogenerate SSH 金鑰組適用於 Linux](mac-create-ssh-keys.md)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-132">You can then follow any of hello Linux docs, such as [How toogenerate SSH key pairs for Linux](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="9b97a-133">Bash for Windows 仍處於開發階段，而且被視為測試版。</span><span class="sxs-lookup"><span data-stu-id="9b97a-133">Bash for Windows is still under development, and is considered a beta release.</span></span> <span data-ttu-id="9b97a-134">如需 Bash for Windows 的詳細資訊，請參閱 [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-134">For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="9b97a-135">如果您想 toouse 東西撞適用於 Windows 以外，一般 Windows SSH 用戶端可以安裝包含下列封裝的 hello:</span><span class="sxs-lookup"><span data-stu-id="9b97a-135">If you wish toouse something other than Bash for Windows, common Windows SSH clients you can install are included in hello following packages:</span></span>

* [<span data-ttu-id="9b97a-136">Git For Windows</span><span class="sxs-lookup"><span data-stu-id="9b97a-136">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="9b97a-137">puTTY</span><span class="sxs-lookup"><span data-stu-id="9b97a-137">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="9b97a-138">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="9b97a-138">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="9b97a-139">Cygwin</span><span class="sxs-lookup"><span data-stu-id="9b97a-139">Cygwin</span></span>](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a><span data-ttu-id="9b97a-140">金鑰檔需要 toocreate 嗎？</span><span class="sxs-lookup"><span data-stu-id="9b97a-140">Which key files do you need toocreate?</span></span>
<span data-ttu-id="9b97a-141">Azure 需要至少 2048 位元的 **ssh-rsa** 格式公開和私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-141">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="9b97a-142">如果您管理 Azure 資源使用 hello 傳統部署模型，您也需要 toogenerate PEM (`.pem`檔案)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-142">If you are managing Azure resources using hello Classic deployment model, you also need toogenerate a PEM (`.pem` file).</span></span>

<span data-ttu-id="9b97a-143">以下是 hello 部署案例，以及您使用在每個檔案的 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="9b97a-143">Here are hello deployment scenarios, and hello types of files you use in each:</span></span>

1. <span data-ttu-id="9b97a-144">**ssh rsa**金鑰所需的任何部署使用 hello [Azure 入口網站](https://portal.azure.com)，並使用 hello 的資源管理員部署[Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-144">**ssh-rsa** keys are required for any deployment using hello [Azure portal](https://portal.azure.com), and Resource Manager deployments using hello [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="9b97a-145">通常大部分的人都需要這些金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-145">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="9b97a-146">A`.pem`檔案是使用 hello 傳統部署的必要的 toocreate Vm。</span><span class="sxs-lookup"><span data-stu-id="9b97a-146">A `.pem` file is required toocreate VMs using hello Classic deployment.</span></span> <span data-ttu-id="9b97a-147">在傳統部署支援這些索引鍵時使用 hello [Azure 入口網站](https://portal.azure.com)或[Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-147">These keys are supported in Classic deployments when using hello [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="9b97a-148">您只需要 toocreate 這些額外的金鑰和憑證如果您要管理使用 hello 傳統部署模型所建立的資源。</span><span class="sxs-lookup"><span data-stu-id="9b97a-148">You only need toocreate these additional keys and certificates if you are managing resources created using hello Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="9b97a-149">安裝 Git for Windows</span><span class="sxs-lookup"><span data-stu-id="9b97a-149">Install Git for Windows</span></span>
<span data-ttu-id="9b97a-150">hello 上一節中列出數個封裝，包括 hello`openssl`適用於 Windows 的工具。</span><span class="sxs-lookup"><span data-stu-id="9b97a-150">hello preceding section listed several packages that include hello `openssl` tool for Windows.</span></span> <span data-ttu-id="9b97a-151">此工具是需要的 toocreate 公用和私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-151">This tool is needed toocreate public and private keys.</span></span> <span data-ttu-id="9b97a-152">hello 如何遵循範例詳細資料 tooinstall 並用**Git for Windows**，但是您可以選擇任何您偏好的套件。</span><span class="sxs-lookup"><span data-stu-id="9b97a-152">hello following examples detail how tooinstall and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="9b97a-153">**Git for Windows**可讓您存取 toosome 其他開放原始碼軟體 ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) 工具和公用程式，當您使用 Linux Vm 可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="9b97a-153">**Git for Windows** gives you access toosome additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="9b97a-154">下載並安裝**Git for Windows**從下列位置的 hello: [https://git-for-windows.github.io/](https://git-for-windows.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-154">Download and install **Git for Windows** from hello following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="9b97a-155">接受 hello hello 期間的預設選項安裝程序，除非您特別需要 toochange 它們。</span><span class="sxs-lookup"><span data-stu-id="9b97a-155">Accept hello default options during hello install process unless you specifically need toochange them.</span></span>
3. <span data-ttu-id="9b97a-156">執行**Git Bash**從 hello**開始功能表** > **Git** > **Git Bash**。</span><span class="sxs-lookup"><span data-stu-id="9b97a-156">Run **Git Bash** from hello **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="9b97a-157">hello 主控台看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="9b97a-157">hello console looks similar toohello following example:</span></span>

    ![Git for Windows Bash Shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="9b97a-159">建立私密金鑰</span><span class="sxs-lookup"><span data-stu-id="9b97a-159">Create a private key</span></span>
1. <span data-ttu-id="9b97a-160">在您**Git Bash**  視窗中，使用`openssl.exe`toocreate 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-160">In your **Git Bash** window, use `openssl.exe` toocreate a private key.</span></span> <span data-ttu-id="9b97a-161">hello 下列範例會建立名為`myPrivateKey`和名為憑證`myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="9b97a-161">hello following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="9b97a-162">hello 輸出看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="9b97a-162">hello output looks similar toohello following example:</span></span>

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   <span data-ttu-id="9b97a-163">如果 Bash 報告錯誤，嘗試以提高的權限開啟新的 **Git Bash** 視窗。</span><span class="sxs-lookup"><span data-stu-id="9b97a-163">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="9b97a-164">然後，重新執行 hello`openssl`命令。</span><span class="sxs-lookup"><span data-stu-id="9b97a-164">Then, rerun hello `openssl` command.</span></span>

2. <span data-ttu-id="9b97a-165">回應 hello 提示國家/地區名稱、 位置、 組織名稱等等。</span><span class="sxs-lookup"><span data-stu-id="9b97a-165">Answer hello prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="9b97a-166">您的私密金鑰和憑證已建立在您目前的工作目錄中。</span><span class="sxs-lookup"><span data-stu-id="9b97a-166">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="9b97a-167">基於安全性考量，您應該在您的私密金鑰設定 hello 權，讓您只可以存取它：</span><span class="sxs-lookup"><span data-stu-id="9b97a-167">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="9b97a-168">hello[下一節](#create-a-private-key-for-putty)使用 Ssh-keygen tooboth 詳細資料檢視和使用 hello 公開金鑰，並建立適合使用 PuTTY tooSSH tooLinux Vm 的私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-168">hello [next section](#create-a-private-key-for-putty) details using PuTTYgen tooboth view and use hello public key, and create a private key specific for using PuTTY tooSSH tooLinux VMs.</span></span> <span data-ttu-id="9b97a-169">hello 下列命令會產生名為的公開金鑰檔案`myPublicKey.key`，您可以立即使用：</span><span class="sxs-lookup"><span data-stu-id="9b97a-169">hello following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="9b97a-170">如果您也需要 toomanage 傳統資源，將轉換 hello`myCert.pem`太`myCert.cer`(DER 編碼 X509 憑證)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-170">If you also need toomanage Classic resources, convert hello `myCert.pem` too`myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="9b97a-171">執行此選擇性步驟中，只有當您需要 toospecifically 管理較舊的傳統資源。</span><span class="sxs-lookup"><span data-stu-id="9b97a-171">Perform this optional step only if you need toospecifically manage older Classic resources.</span></span>

    <span data-ttu-id="9b97a-172">轉換使用下列命令的 hello hello 憑證：</span><span class="sxs-lookup"><span data-stu-id="9b97a-172">Convert hello certificate using hello following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="9b97a-173">建立 PuTTY 的私密金鑰</span><span class="sxs-lookup"><span data-stu-id="9b97a-173">Create a private key for PuTTY</span></span>
<span data-ttu-id="9b97a-174">PuTTY 是適用於 Windows 的常見 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-174">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="9b97a-175">您是免費 toouse 任何您想要的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-175">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="9b97a-176">toouse PuTTY，您需要 toocreate 其他類型的索引鍵-PuTTY 私用金鑰 (PPK)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-176">toouse PuTTY, you need toocreate an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="9b97a-177">如果您不想 toouse PuTTY，略過本節。</span><span class="sxs-lookup"><span data-stu-id="9b97a-177">If you do not wish toouse PuTTY, skip this section.</span></span>

<span data-ttu-id="9b97a-178">hello 下列範例會建立專為 PuTTY toouse 這個額外私密金鑰：</span><span class="sxs-lookup"><span data-stu-id="9b97a-178">hello following example creates this additional private key specifically for PuTTY toouse:</span></span>

1. <span data-ttu-id="9b97a-179">使用**Git Bash** tooconvert 私人金鑰到 RSA 私密金鑰 Ssh-keygen 可以了解。</span><span class="sxs-lookup"><span data-stu-id="9b97a-179">Use **Git Bash** tooconvert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="9b97a-180">hello 下列範例會建立名為`myPrivateKey_rsa`從名為 hello 現有索引鍵`myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="9b97a-180">hello following example creates a key named `myPrivateKey_rsa` from hello existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="9b97a-181">基於安全性考量，您應該在您的私密金鑰設定 hello 權，讓您只可以存取它：</span><span class="sxs-lookup"><span data-stu-id="9b97a-181">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="9b97a-182">下載並執行從下列位置的 hello Ssh-keygen: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="9b97a-182">Download and run PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="9b97a-183">按一下 [hello] 功能表：**檔案** > **負載私密金鑰**</span><span class="sxs-lookup"><span data-stu-id="9b97a-183">Click hello menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="9b97a-184">找出您的私密金鑰 (`myPrivateKey_rsa` hello 前一個範例中)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-184">Locate your private key (`myPrivateKey_rsa` in hello previous example).</span></span> <span data-ttu-id="9b97a-185">當您啟動 hello 預設目錄**Git Bash**是`C:\Users\%username%`。</span><span class="sxs-lookup"><span data-stu-id="9b97a-185">hello default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="9b97a-186">變更 hello 檔案篩選器 tooshow**所有檔案 (\*。\*)**:</span><span class="sxs-lookup"><span data-stu-id="9b97a-186">Change hello file filter tooshow **All Files (\*.\*)**:</span></span>

    ![載入 Ssh-keygen hello 現有的私密金鑰](./media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="9b97a-188">按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="9b97a-188">Click **Open**.</span></span> <span data-ttu-id="9b97a-189">提示表示該 hello 金鑰已成功匯入：</span><span class="sxs-lookup"><span data-stu-id="9b97a-189">A prompt indicates that hello key has been successfully imported:</span></span>

    ![已成功匯入金鑰 tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="9b97a-191">按一下**確定**tooclose hello 提示字元。</span><span class="sxs-lookup"><span data-stu-id="9b97a-191">Click **OK** tooclose hello prompt.</span></span>
7. <span data-ttu-id="9b97a-192">hello 公開金鑰會顯示在 hello hello 頂端**Ssh-keygen**視窗。</span><span class="sxs-lookup"><span data-stu-id="9b97a-192">hello public key is displayed at hello top of hello **PuTTYgen** window.</span></span> <span data-ttu-id="9b97a-193">您複製並貼入此公開金鑰 hello Azure 入口網站或 Azure Resource Manager 範本當您建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="9b97a-193">You copy and paste this public key into hello Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="9b97a-194">您也可以按一下**儲存公開金鑰**toosave 複製 tooyour 電腦：</span><span class="sxs-lookup"><span data-stu-id="9b97a-194">You can also click **Save public key** toosave a copy tooyour computer:</span></span>

    ![儲存 PuTTY 公用金鑰檔案](./media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="9b97a-196">hello 下列範例顯示如何您會複製並貼到 hello Azure 入口網站的這個公開金鑰，當您建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="9b97a-196">hello following example shows how you would copy and paste this public key into hello Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="9b97a-197">hello 公開金鑰然後通常儲存在`~/.ssh/authorized_keys`新 VM 上。</span><span class="sxs-lookup"><span data-stu-id="9b97a-197">hello public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Hello Azure 入口網站中建立 VM 時使用的公開金鑰](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="9b97a-199">回到 **PuTTYgen**，按一下 [儲存私密金鑰]：</span><span class="sxs-lookup"><span data-stu-id="9b97a-199">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![儲存 PuTTY 私密金鑰檔案](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > <span data-ttu-id="9b97a-201">出現提示要求您是否想 toocontinue，而不需輸入金鑰複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-201">A prompt asks if you wish toocontinue without entering a passphrase for your key.</span></span> <span data-ttu-id="9b97a-202">複雜密碼就像是密碼附加的 tooyour 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="9b97a-202">A passphrase is like a password attached tooyour private key.</span></span> <span data-ttu-id="9b97a-203">即使其他人為 tooobtain 私密金鑰，它們仍不會使用只 hello 金鑰無法 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="9b97a-203">Even if someone were tooobtain your private key, they still would not be able tooauthenticate using just hello key.</span></span> <span data-ttu-id="9b97a-204">它們也需要 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-204">They would also need hello passphrase.</span></span> <span data-ttu-id="9b97a-205">如果沒有複雜密碼，如果有人取得您的私密金鑰，他們可以登入 tooany VM 或服務使用該索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9b97a-205">Without a passphrase, if someone obtains your private key, they can log in tooany VM or service that uses that key.</span></span> <span data-ttu-id="9b97a-206">我們建議您建立複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-206">We recommend you create a passphrase.</span></span> <span data-ttu-id="9b97a-207">不過，如果您忘記 hello 複雜密碼，沒有任何方式 toorecover 它。</span><span class="sxs-lookup"><span data-stu-id="9b97a-207">However, if you forget hello passphrase, there is no way toorecover it.</span></span>
   >
   >

    <span data-ttu-id="9b97a-208">如果您想 tooenter 複雜密碼，按一下**否**hello 主要 Ssh-keygen 視窗中輸入的複雜密碼，然後按**儲存私密金鑰**一次。</span><span class="sxs-lookup"><span data-stu-id="9b97a-208">If you wish tooenter a passphrase, click **No**, enter a passphrase in hello main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="9b97a-209">否則，請按一下**是**toocontinue 而不需提供 hello 選用的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9b97a-209">Otherwise, click **Yes** toocontinue without providing hello optional passphrase.</span></span>
9. <span data-ttu-id="9b97a-210">輸入名稱和位置 toosave PPK 檔案。</span><span class="sxs-lookup"><span data-stu-id="9b97a-210">Enter a name and location toosave your PPK file.</span></span>

## <a name="use-putty-toossh-tooa-linux-machine"></a><span data-ttu-id="9b97a-211">使用 Putty tooSSH tooa Linux 機器</span><span class="sxs-lookup"><span data-stu-id="9b97a-211">Use Putty tooSSH tooa Linux Machine</span></span>
<span data-ttu-id="9b97a-212">同樣地，PuTTY 是適用於 Windows 的常見 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-212">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="9b97a-213">您是免費 toouse 任何您想要的 SSH 用戶端。</span><span class="sxs-lookup"><span data-stu-id="9b97a-213">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="9b97a-214">hello 如何遵循步驟詳細 toouse 您與使用 SSH Azure VM 的私用金鑰 tooauthenticate。</span><span class="sxs-lookup"><span data-stu-id="9b97a-214">hello following steps detail how toouse your private key tooauthenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="9b97a-215">hello 步驟的很類似其他 SSH 金鑰的用戶端方面需要 tooload 您私用金鑰 tooauthenticate hello SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="9b97a-215">hello steps are similar in other SSH key clients in terms of needing tooload your private key tooauthenticate hello SSH connection.</span></span>

1. <span data-ttu-id="9b97a-216">下載並執行的 putty 從下列位置的 hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="9b97a-216">Download and run putty from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="9b97a-217">填滿 hello 主機名稱或 IP 位址，您的 VM 從 hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="9b97a-217">Fill in hello host name or IP address of your VM from hello Azure portal:</span></span>

    ![開啟新的 PuTTY 連線](./media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="9b97a-219">選取 [開啟] 之前，按一下 [連線] > [SSH] > [Auth] 索引標籤。瀏覽 tooand 選取您的私密金鑰：</span><span class="sxs-lookup"><span data-stu-id="9b97a-219">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse tooand select your private key:</span></span>

    ![選取您的 PuTTY 私密金鑰進行驗證](./media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="9b97a-221">按一下**開啟**tooconnect tooyour 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9b97a-221">Click **Open** tooconnect tooyour virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b97a-222">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9b97a-222">Next steps</span></span>
<span data-ttu-id="9b97a-223">您也可以產生 hello 公用和私用金鑰[使用 OS X 和 Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-223">You can also generate hello public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9b97a-224">如需撞 for Windows 和 Windows 電腦上擁有 OSS 工具方便的 hello 優點的詳細資訊，請參閱[撞在 Windows 上的 Ubuntu 上](https://msdn.microsoft.com/commandline/wsl/about)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-224">For more information about Bash for Windows and hello benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="9b97a-225">如果您有使用 SSH tooconnect tooyour Linux Vm 時發生問題，請參閱[疑難排解 SSH 連線 tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9b97a-225">If you have trouble using SSH tooconnect tooyour Linux VMs, see [Troubleshoot SSH connections tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
