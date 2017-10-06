---
title: "在 Azure 上的 aaaIntroduction tooFreeBSD |Microsoft 文件"
description: "了解如何使用 Azure 上的 FreeBSD 虛擬機器"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="fc29b-103">在 Azure 上的簡介 tooFreeBSD</span><span class="sxs-lookup"><span data-stu-id="fc29b-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="fc29b-104">本主題提供在 Azure 中執行 FreeBSD 虛擬機器的概觀。</span><span class="sxs-lookup"><span data-stu-id="fc29b-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="fc29b-105">概觀</span><span class="sxs-lookup"><span data-stu-id="fc29b-105">Overview</span></span>
<span data-ttu-id="fc29b-106">Microsoft azure FreeBSD 是進階的電腦作業系統使用 toopower 最新的伺服器、 桌上型電腦，以及內嵌的平台。</span><span class="sxs-lookup"><span data-stu-id="fc29b-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="fc29b-107">Microsoft Corporation 提供 FreeBSD 的映像在 Azure 上以 hello [Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)預先設定。</span><span class="sxs-lookup"><span data-stu-id="fc29b-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="fc29b-108">目前，hello 下列 FreeBSD 版本會提供當做映像的 Microsoft:</span><span class="sxs-lookup"><span data-stu-id="fc29b-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="fc29b-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="fc29b-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="fc29b-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="fc29b-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="fc29b-111">hello 代理程式負責 hello FreeBSD VM 之間的通訊和進行運算，例如佈建 Azure 網狀架構 hello hello VM （使用者名稱、 密碼或 SSH 金鑰、 主機名稱等） 的第一次使用和啟用的功能，用於選擇性的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fc29b-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="fc29b-112">FreeBSD 的未來版本中，與 hello 策略是目前 toostay 並提供 hello 最新版本的 hello FreeBSD 版本工程小組會在發行後不久。</span><span class="sxs-lookup"><span data-stu-id="fc29b-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="fc29b-113">部署 FreeBSD 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fc29b-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="fc29b-114">部署 FreeBSD 虛擬機器是簡單的程序，使用從 hello Azure 入口網站中的 hello Azure Marketplace 映像：</span><span class="sxs-lookup"><span data-stu-id="fc29b-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="fc29b-115">FreeBSD 10.3 hello Azure Marketplace 上</span><span class="sxs-lookup"><span data-stu-id="fc29b-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="fc29b-116">FreeBSD 11.0 hello Azure Marketplace 上</span><span class="sxs-lookup"><span data-stu-id="fc29b-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="fc29b-117">透過 Azure CLI 2.0 在 FreeBSD 上建立 FreeBSD VM</span><span class="sxs-lookup"><span data-stu-id="fc29b-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="fc29b-118">首先，您必須 tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)雖然 FreeBSD 機器上，下列命令。</span><span class="sxs-lookup"><span data-stu-id="fc29b-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="fc29b-119">如果未安裝 bash FreeBSD 機器上，執行下列命令之前 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="fc29b-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="fc29b-120">如果未安裝 python FreeBSD 機器上，執行下列命令之前 hello 安裝。</span><span class="sxs-lookup"><span data-stu-id="fc29b-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="fc29b-121">Hello 在安裝期間，系統會要求您`Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`。</span><span class="sxs-lookup"><span data-stu-id="fc29b-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="fc29b-122">如果您回答`y`輸入`/etc/rc.conf`為`a path tooan rc file tooupdate`，您可能會符合 hello 問題`ERROR: [Errno 13] Permission denied`。</span><span class="sxs-lookup"><span data-stu-id="fc29b-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="fc29b-123">tooresolve 這個問題，您應該授與對 hello 檔 hello 寫入右 toocurrent 使用者`etc/rc.conf`。</span><span class="sxs-lookup"><span data-stu-id="fc29b-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="fc29b-124">現在您可以登入 Azure 並建立您的 FreeBSD VM。</span><span class="sxs-lookup"><span data-stu-id="fc29b-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="fc29b-125">以下是範例 toocreate FreeBSD 11.0 VM。</span><span class="sxs-lookup"><span data-stu-id="fc29b-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="fc29b-126">您也可以加入 hello 參數`--public-ip-address-dns-name`全域唯一的 DNS 名稱，新建立的公用 ip。</span><span class="sxs-lookup"><span data-stu-id="fc29b-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="fc29b-127">然後您可以登入 tooyour FreeBSD VM 透過 hello 列印 hello 上述輸出中的部署中的 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="fc29b-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="fc29b-128">適用於 FreeBSD 的 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="fc29b-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="fc29b-129">以下為 FreeBSD VM 中支援的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="fc29b-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="fc29b-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="fc29b-130">VMAccess</span></span>
<span data-ttu-id="fc29b-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess)延伸模組可以：</span><span class="sxs-lookup"><span data-stu-id="fc29b-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="fc29b-132">重設 hello hello 原始 sudo 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="fc29b-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="fc29b-133">建立新 sudo 的使用者與 hello 指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="fc29b-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="fc29b-134">設定與指定索引鍵的 hello hello 公開主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc29b-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="fc29b-135">重設期間如果未提供 hello 主機金鑰佈建的 VM 提供 hello 公開主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc29b-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="fc29b-136">開啟 hello SSH 連接埠 (22)，並還原 hello sshd_config 如果 reset_ssh 設定 tootrue。</span><span class="sxs-lookup"><span data-stu-id="fc29b-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="fc29b-137">移除 hello 現有使用者。</span><span class="sxs-lookup"><span data-stu-id="fc29b-137">Remove hello existing user.</span></span>
* <span data-ttu-id="fc29b-138">檢查磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc29b-138">Check disks.</span></span>
* <span data-ttu-id="fc29b-139">修復新增的磁碟。</span><span class="sxs-lookup"><span data-stu-id="fc29b-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="fc29b-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="fc29b-140">CustomScript</span></span>
<span data-ttu-id="fc29b-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript)延伸模組可以：</span><span class="sxs-lookup"><span data-stu-id="fc29b-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="fc29b-142">如果提供，下載 hello 自訂指令碼從 Azure 儲存體或外部的公開儲存體 (例如，GitHub)。</span><span class="sxs-lookup"><span data-stu-id="fc29b-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="fc29b-143">執行 hello 進入點指令碼。</span><span class="sxs-lookup"><span data-stu-id="fc29b-143">Run hello entry point script.</span></span>
* <span data-ttu-id="fc29b-144">支援內嵌命令。</span><span class="sxs-lookup"><span data-stu-id="fc29b-144">Support inline commands.</span></span>
* <span data-ttu-id="fc29b-145">自動轉換 Shell 和 Python 指令碼中的 Windows 樣式新行字元。</span><span class="sxs-lookup"><span data-stu-id="fc29b-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="fc29b-146">自動移除 Shell 和 Python 指令碼中的 BOM。</span><span class="sxs-lookup"><span data-stu-id="fc29b-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="fc29b-147">保護 CommandToExecute 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="fc29b-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="fc29b-148">FreeBSD VM 目前僅支援 CustomScript 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="fc29b-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="fc29b-149">驗證：使用者名稱、密碼和 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="fc29b-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="fc29b-150">當您使用 hello Azure 入口網站建立 FreeBSD 虛擬機器時，您必須提供使用者名稱、 密碼或 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc29b-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="fc29b-151">部署在 Azure 上 FreeBSD 虛擬機器的使用者名稱必須符合的系統帳戶的名稱 (UID < 100) 已經存在於 hello 虛擬機器 （「 根 」，例如） 中。</span><span class="sxs-lookup"><span data-stu-id="fc29b-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="fc29b-152">目前支援僅 hello RSA SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="fc29b-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="fc29b-153">多行 SSH 金鑰的開頭必須為 `---- BEGIN SSH2 PUBLIC KEY ----`，結尾為 `---- END SSH2 PUBLIC KEY ----`。</span><span class="sxs-lookup"><span data-stu-id="fc29b-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="fc29b-154">取得超級使用者權限</span><span class="sxs-lookup"><span data-stu-id="fc29b-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="fc29b-155">hello 在 Azure 上的虛擬機器執行個體部署期間指定的使用者帳戶是特殊權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="fc29b-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="fc29b-156">hello sudo 的安裝封裝中 hello 發行 FreeBSD 映像。</span><span class="sxs-lookup"><span data-stu-id="fc29b-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="fc29b-157">透過此使用者帳戶登入之後，您可以使用 hello 命令語法為根目錄執行命令。</span><span class="sxs-lookup"><span data-stu-id="fc29b-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="fc29b-158">您可以視需要使用 `sudo -s` 來取得 root shell。</span><span class="sxs-lookup"><span data-stu-id="fc29b-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="fc29b-159">已知問題</span><span class="sxs-lookup"><span data-stu-id="fc29b-159">Known issues</span></span>
<span data-ttu-id="fc29b-160">hello [Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)2.2.2 有 [已知的問題] 的版本 (https://github.com/Azure/WALinuxAgent/pull/517)，會導致 hello 佈建失敗 FreeBSD vm 在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="fc29b-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="fc29b-161">hello 修正的擷取方式[Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)2.2.3 版本和更新版本。</span><span class="sxs-lookup"><span data-stu-id="fc29b-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fc29b-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc29b-162">Next steps</span></span>
* <span data-ttu-id="fc29b-163">跳過[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate FreeBSD VM。</span><span class="sxs-lookup"><span data-stu-id="fc29b-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="fc29b-164">如果您想 toobring 自己 FreeBSD tooAzure，請參閱太[建立並上傳 VHD FreeBSD tooAzure](linux/classic/freebsd-create-upload-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="fc29b-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
