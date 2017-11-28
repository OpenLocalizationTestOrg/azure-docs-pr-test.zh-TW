---
title: "對 Azure 上的 Linux VM 加入使用者 | Microsoft Docs"
description: "將使用者加入 Azure 上的 Linux VM。"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: a95157f57c0cbd1f2a9ed68a0fe83140d7c9ec40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-user-to-an-azure-vm"></a><span data-ttu-id="78ad6-103">將使用者加入 Azure VM 中</span><span class="sxs-lookup"><span data-stu-id="78ad6-103">Add a user to an Azure VM</span></span>
<span data-ttu-id="78ad6-104">在任何新 Linux VM 上的首要工作之一，就是建立新的使用者。</span><span class="sxs-lookup"><span data-stu-id="78ad6-104">One of the first tasks on any new Linux VM is to create a new user.</span></span>  <span data-ttu-id="78ad6-105">在本文中，我們會逐步建立 sudo 使用者帳戶、設定密碼、新增 SSH 公開金鑰，最後使用 `visudo` 來允許在沒有密碼的情況下使用 sudo。</span><span class="sxs-lookup"><span data-stu-id="78ad6-105">In this article, we walk through creating a sudo user account, setting the password, adding SSH Public Keys, and finally use `visudo` to allow sudo without a password.</span></span>

<span data-ttu-id="78ad6-106">必要條件︰[Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/)、[SSH 公開金鑰與私密金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、Azure 資源群組，且已安裝 Azure CLI 同時使用 `azure config mode arm` 切換至 Azure Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="78ad6-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and the Azure CLI installed and switched to Azure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="78ad6-107">快速命令</span><span class="sxs-lookup"><span data-stu-id="78ad6-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy the SSH Public Key to the new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers to allow no password
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify the SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="78ad6-108">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="78ad6-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="78ad6-109">簡介</span><span class="sxs-lookup"><span data-stu-id="78ad6-109">Introduction</span></span>
<span data-ttu-id="78ad6-110">新伺服器最常見的首要工作之一，就是新增使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="78ad6-110">One of the first and most common task with a new server is to add a user account.</span></span>  <span data-ttu-id="78ad6-111">根登入應該一律停用，根帳戶本身不應與您的 Linux 伺服器搭配使用，只能與 sudo 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="78ad6-111">Root logins should be disabled and the root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="78ad6-112">使用 sudo 來為使用者提供根擴大權限才是管理及使用 Linux 的正確方法。</span><span class="sxs-lookup"><span data-stu-id="78ad6-112">Giving a user root escalation privileges using sudo it the proper way to administer and use Linux.</span></span>

<span data-ttu-id="78ad6-113">我們會使用命令 `useradd` 來將使用者帳戶新增到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="78ad6-113">Using the command `useradd` we are adding user accounts to the Linux VM.</span></span>  <span data-ttu-id="78ad6-114">執行 `useradd` 來修改 `/etc/passwd`、`/etc/shadow`、`/etc/group` 及 `/etc/gshadow`。</span><span class="sxs-lookup"><span data-stu-id="78ad6-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="78ad6-115">我們會在 `useradd` 命令中新增命令列旗標，以將新使用者一併新增到 Linux 上適當的 sudo 群組。</span><span class="sxs-lookup"><span data-stu-id="78ad6-115">We are adding a command-line flag to the `useradd` command to also add the new user to the proper sudo group on Linux.</span></span>  <span data-ttu-id="78ad6-116">雖然 `useradd` 會在 `/etc/passwd` 中建立項目，但卻不會為新的使用者帳戶提供密碼。</span><span class="sxs-lookup"><span data-stu-id="78ad6-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give the new user account a password.</span></span>  <span data-ttu-id="78ad6-117">我們會使用簡單的 `passwd` 命令，為新的使用者建立初始密碼。</span><span class="sxs-lookup"><span data-stu-id="78ad6-117">We are creating an initial password for the new user using the simple `passwd` command.</span></span>  <span data-ttu-id="78ad6-118">最後一個步驟是修改 sudo 規則，以允許該使用者以 sudo 權限執行命令，而不必為每個命令輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="78ad6-118">The last step is to modify the sudo rules to allow that user to execute commands with sudo privileges without having to enter a password for every command.</span></span>  <span data-ttu-id="78ad6-119">使用私密金鑰登入時，我們會假設該使用者帳戶非意圖不良的執行者，因此會允許他不需密碼即可使用 sudo 存取。</span><span class="sxs-lookup"><span data-stu-id="78ad6-119">Logging in using the Private key we are assuming that user account is safe from bad actors and are going to allow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-to-an-azure-vm"></a><span data-ttu-id="78ad6-120">將單一 sudo 使用者加入 Azure VM 中</span><span class="sxs-lookup"><span data-stu-id="78ad6-120">Adding a single sudo user to an Azure VM</span></span>
<span data-ttu-id="78ad6-121">使用 SSH 金鑰登入 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="78ad6-121">Log in to the Azure VM using SSH keys.</span></span>  <span data-ttu-id="78ad6-122">如果您尚未設定 SSH 公開金鑰存取權，請先閱讀完這篇文章： [在 Azure 使用公開金鑰驗證](http://link.to/article)。</span><span class="sxs-lookup"><span data-stu-id="78ad6-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="78ad6-123">`useradd` 命令會完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="78ad6-123">The `useradd` command completes the following tasks:</span></span>

* <span data-ttu-id="78ad6-124">建立新的使用者帳戶</span><span class="sxs-lookup"><span data-stu-id="78ad6-124">create a new user account</span></span>
* <span data-ttu-id="78ad6-125">以相同的名稱建立新的使用者群組</span><span class="sxs-lookup"><span data-stu-id="78ad6-125">create a new user group with the same name</span></span>
* <span data-ttu-id="78ad6-126">在 `/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="78ad6-126">add a blank entry to `/etc/passwd`</span></span>
* <span data-ttu-id="78ad6-127">在 `/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="78ad6-127">add a blank entry to `/etc/gpasswd`</span></span>

<span data-ttu-id="78ad6-128">`-G` 命令列旗標會將新的使用者帳戶新增到適當的 Linux 群組中，為該新使用者帳戶提供根擴大權限。</span><span class="sxs-lookup"><span data-stu-id="78ad6-128">The `-G` command-line flag adds the new user account to the proper Linux group giving the new user account root escalation privileges.</span></span>

#### <a name="add-the-user"></a><span data-ttu-id="78ad6-129">加入使用者</span><span class="sxs-lookup"><span data-stu-id="78ad6-129">Add the user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="78ad6-130">設定密碼</span><span class="sxs-lookup"><span data-stu-id="78ad6-130">Set a password</span></span>
<span data-ttu-id="78ad6-131">`useradd` 命令會建立使用者，並將 `/etc/passwd` 和 `/etc/gpasswd` 中都新增項目，但不會實際設定密碼。</span><span class="sxs-lookup"><span data-stu-id="78ad6-131">The `useradd` command creates the user and adds an entry to both `/etc/passwd` and `/etc/gpasswd` but does not actually set the password.</span></span>  <span data-ttu-id="78ad6-132">將密碼新增到項目中時是使用 `passwd` 命令。</span><span class="sxs-lookup"><span data-stu-id="78ad6-132">The password is added to the entry using the `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="78ad6-133">我們在伺服器上已有具備 sudo 權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="78ad6-133">We now have a user with sudo privileges on the server.</span></span>

### <a name="add-your-ssh-public-key-to-the-new-user-account"></a><span data-ttu-id="78ad6-134">請將您的 SSH 公開金鑰加入新的使用者帳戶中</span><span class="sxs-lookup"><span data-stu-id="78ad6-134">Add your SSH Public Key to the new user account</span></span>
<span data-ttu-id="78ad6-135">從您的電腦，使用 `ssh-copy-id` 命令搭配新密碼。</span><span class="sxs-lookup"><span data-stu-id="78ad6-135">From your machine, use the `ssh-copy-id` command with the new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-to-allow-sudo-usage-without-a-password"></a><span data-ttu-id="78ad6-136">使用 visudo 以允許在沒有密碼的情況下使用 sudo</span><span class="sxs-lookup"><span data-stu-id="78ad6-136">Using visudo to allow sudo usage without a password</span></span>
<span data-ttu-id="78ad6-137">使用 `visudo` 來編輯 `/etc/sudoers` 檔案可增加幾層的保護，防止不正確地修改這個重要的檔案。</span><span class="sxs-lookup"><span data-stu-id="78ad6-137">Using `visudo` to edit the `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="78ad6-138">執行 `visudo` 時會鎖住 `/etc/sudoers` 檔案，以確保沒有任何其他使用者能在檔案處於編輯狀態時對檔案進行變更。</span><span class="sxs-lookup"><span data-stu-id="78ad6-138">Upon executing `visudo`, the `/etc/sudoers` file is locked to ensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="78ad6-139">當您嘗試儲存或結束 `/etc/sudoers` 檔案時，`visudo` 也會檢查該檔案是否有錯誤，讓您儲存的不會是損毀的 sudoers 檔案。</span><span class="sxs-lookup"><span data-stu-id="78ad6-139">The `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt to save or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="78ad6-140">我們在正確的預設群組中，已有使用者可進行 sudo 存取。</span><span class="sxs-lookup"><span data-stu-id="78ad6-140">We already have users in the correct default group for sudo access.</span></span>  <span data-ttu-id="78ad6-141">現在，我們將讓這些群組能夠在沒有密碼的情況下使用 sudo。</span><span class="sxs-lookup"><span data-stu-id="78ad6-141">Now we are going to enable those groups to use sudo with no password.</span></span>

```bash
# Execute visudo as root to edit the /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# to this
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL

# to this
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-the-user-ssh-keys-and-sudo"></a><span data-ttu-id="78ad6-142">驗證使用者、SSH 金鑰及 sudo</span><span class="sxs-lookup"><span data-stu-id="78ad6-142">Verify the user, ssh keys, and sudo</span></span>
```bash
# Verify the SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
