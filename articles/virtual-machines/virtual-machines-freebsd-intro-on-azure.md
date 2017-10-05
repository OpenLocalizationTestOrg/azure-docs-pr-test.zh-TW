---
title: "Azure 上的 FreeBSD 簡介 | Microsoft Docs"
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
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="a154d-103">Azure 上的 FreeBSD 簡介</span><span class="sxs-lookup"><span data-stu-id="a154d-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="a154d-104">本主題提供在 Azure 中執行 FreeBSD 虛擬機器的概觀。</span><span class="sxs-lookup"><span data-stu-id="a154d-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="a154d-105">Overview</span><span class="sxs-lookup"><span data-stu-id="a154d-105">Overview</span></span>
<span data-ttu-id="a154d-106">適用於 Microsoft Azure 的 FreeBSD 是一套先進的電腦作業系統，可用來為新式伺服器、桌上型電腦及內嵌平台提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="a154d-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="a154d-107">Microsoft Corporation 目前在 Azure 上提供已預先設定 [Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/)的 FreeBSD 映像。</span><span class="sxs-lookup"><span data-stu-id="a154d-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="a154d-108">目前，Microsoft 以映像形式提供下列 FreeBSD 版本：</span><span class="sxs-lookup"><span data-stu-id="a154d-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="a154d-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="a154d-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="a154d-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="a154d-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="a154d-111">此代理程式會負責 FreeBSD VM 與 Azure 網狀架構之間作業的通訊，例如在第一次使用 VM 時佈建 VM (使用者名稱、密碼或 SSH 金鑰、主機名稱等)，以及啟用選擇性 VM 延伸模組的功能。</span><span class="sxs-lookup"><span data-stu-id="a154d-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="a154d-112">至於未來的 FreeBSD 版本，策略是維持最新狀態，在 FreeBSD 版本工程小組發佈最新版本後不久，便立即提供最新版本。</span><span class="sxs-lookup"><span data-stu-id="a154d-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="a154d-113">部署 FreeBSD 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a154d-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="a154d-114">使用來自 Azure Marketplace 的映像從 Azure 入口網站部署 FreeBSD 虛擬機器相當簡單：</span><span class="sxs-lookup"><span data-stu-id="a154d-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="a154d-115">Azure Marketplace 上的 FreeBSD 10.3</span><span class="sxs-lookup"><span data-stu-id="a154d-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="a154d-116">Azure Marketplace 上的 FreeBSD 11.0</span><span class="sxs-lookup"><span data-stu-id="a154d-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="a154d-117">透過 Azure CLI 2.0 在 FreeBSD 上建立 FreeBSD VM</span><span class="sxs-lookup"><span data-stu-id="a154d-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="a154d-118">首先，您必須透過下列命令在 FreeBSD 電腦上安裝 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="a154d-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="a154d-119">如果您的 FreeBSD 電腦上未安裝 Bash，請先執行下列命令，再進行安裝。</span><span class="sxs-lookup"><span data-stu-id="a154d-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="a154d-120">如果您的 FreeBSD 電腦上未安裝 Python，請先執行下列命令，再進行安裝。</span><span class="sxs-lookup"><span data-stu-id="a154d-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="a154d-121">進行安裝時，系統會向您提出下列問題：`Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`。</span><span class="sxs-lookup"><span data-stu-id="a154d-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="a154d-122">如果您回答 `y` 並輸入 `/etc/rc.conf` 作為 `a path to an rc file to update`，您可能會遇到下列問題：`ERROR: [Errno 13] Permission denied`。</span><span class="sxs-lookup"><span data-stu-id="a154d-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="a154d-123">若要解決此問題，您應該將檔案 `etc/rc.conf` 的寫入權限授與目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="a154d-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="a154d-124">現在您可以登入 Azure 並建立您的 FreeBSD VM。</span><span class="sxs-lookup"><span data-stu-id="a154d-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="a154d-125">以下是一個建立 FreeBSD 11.0 VM 的範例。</span><span class="sxs-lookup"><span data-stu-id="a154d-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="a154d-126">您也可以新增 `--public-ip-address-dns-name` 參數，其中含有新建立之公用 IP 的全域唯一 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="a154d-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="a154d-127">接著，您便可以透過上述部署作業輸出中所列印的 IP 位址來登入您的 FreeBSD VM。</span><span class="sxs-lookup"><span data-stu-id="a154d-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="a154d-128">適用於 FreeBSD 的 VM 擴充功能</span><span class="sxs-lookup"><span data-stu-id="a154d-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="a154d-129">以下為 FreeBSD VM 中支援的 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="a154d-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="a154d-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="a154d-130">VMAccess</span></span>
<span data-ttu-id="a154d-131">[VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) 擴充功能可以：</span><span class="sxs-lookup"><span data-stu-id="a154d-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="a154d-132">重設原始 sudo 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="a154d-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="a154d-133">建立新的 sudo 使用者並指定密碼。</span><span class="sxs-lookup"><span data-stu-id="a154d-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="a154d-134">使用指定的金鑰來設定公開主機金鑰。</span><span class="sxs-lookup"><span data-stu-id="a154d-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="a154d-135">重設 VM 佈建期間所提供的公開主機金鑰 (如果未提供主機金鑰)。</span><span class="sxs-lookup"><span data-stu-id="a154d-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="a154d-136">開啟 SSH 連接埠 (22)，而且如果已將 reset_ssh 設定為 true，則還原 sshd_config。</span><span class="sxs-lookup"><span data-stu-id="a154d-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="a154d-137">移除現有的使用者。</span><span class="sxs-lookup"><span data-stu-id="a154d-137">Remove the existing user.</span></span>
* <span data-ttu-id="a154d-138">檢查磁碟。</span><span class="sxs-lookup"><span data-stu-id="a154d-138">Check disks.</span></span>
* <span data-ttu-id="a154d-139">修復新增的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a154d-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="a154d-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="a154d-140">CustomScript</span></span>
<span data-ttu-id="a154d-141">[CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) 擴充功能可以：</span><span class="sxs-lookup"><span data-stu-id="a154d-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="a154d-142">如果提供，可從 Azure 儲存體或外部公用儲存體 (例如 GitHub) 下載自訂的指令碼。</span><span class="sxs-lookup"><span data-stu-id="a154d-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="a154d-143">執行進入點指令碼。</span><span class="sxs-lookup"><span data-stu-id="a154d-143">Run the entry point script.</span></span>
* <span data-ttu-id="a154d-144">支援內嵌命令。</span><span class="sxs-lookup"><span data-stu-id="a154d-144">Support inline commands.</span></span>
* <span data-ttu-id="a154d-145">自動轉換 Shell 和 Python 指令碼中的 Windows 樣式新行字元。</span><span class="sxs-lookup"><span data-stu-id="a154d-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="a154d-146">自動移除 Shell 和 Python 指令碼中的 BOM。</span><span class="sxs-lookup"><span data-stu-id="a154d-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="a154d-147">保護 CommandToExecute 中的機密資料。</span><span class="sxs-lookup"><span data-stu-id="a154d-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="a154d-148">FreeBSD VM 目前僅支援 CustomScript 1.x 版。</span><span class="sxs-lookup"><span data-stu-id="a154d-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="a154d-149">驗證：使用者名稱、密碼和 SSH 金鑰</span><span class="sxs-lookup"><span data-stu-id="a154d-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="a154d-150">使用 Azure 入口網站來建立 FreeBSD 虛擬機器時，您必須提供使用者名稱、密碼或 SSH 公開金鑰。</span><span class="sxs-lookup"><span data-stu-id="a154d-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="a154d-151">在 Azure 上部署 FreeBSD 虛擬機器時所使用的使用者名稱，不可以和虛擬機器中已存在的系統帳戶 (UID < 100) 名稱相同 (例如 "root")。</span><span class="sxs-lookup"><span data-stu-id="a154d-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="a154d-152">目前只支援 RSA SSH 金鑰。</span><span class="sxs-lookup"><span data-stu-id="a154d-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="a154d-153">多行 SSH 金鑰的開頭必須為 `---- BEGIN SSH2 PUBLIC KEY ----`，結尾為 `---- END SSH2 PUBLIC KEY ----`。</span><span class="sxs-lookup"><span data-stu-id="a154d-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="a154d-154">取得超級使用者權限</span><span class="sxs-lookup"><span data-stu-id="a154d-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="a154d-155">在 Azure 上部署虛擬機器執行個體時所指定的使用者帳戶是特殊權限帳戶。</span><span class="sxs-lookup"><span data-stu-id="a154d-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="a154d-156">sudo 的封裝已安裝於所發佈的 FreeBSD 映像中。</span><span class="sxs-lookup"><span data-stu-id="a154d-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="a154d-157">當您使用此使用者帳戶登入之後，您便能以 root 身分，使用命令語法來執行命令。</span><span class="sxs-lookup"><span data-stu-id="a154d-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="a154d-158">您可以視需要使用 `sudo -s` 來取得 root shell。</span><span class="sxs-lookup"><span data-stu-id="a154d-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a154d-159">已知問題</span><span class="sxs-lookup"><span data-stu-id="a154d-159">Known issues</span></span>
<span data-ttu-id="a154d-160">[Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/) 2.2.2 版有一個[已知問題] (https://github.com/Azure/WALinuxAgent/pull/517)，此問題會導致 Azure 上的 FreeBSD VM 佈建失敗。</span><span class="sxs-lookup"><span data-stu-id="a154d-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="a154d-161">[Azure VM 客體代理程式](https://github.com/Azure/WALinuxAgent/) 2.2.3 版和更新版本已包含這項修正。</span><span class="sxs-lookup"><span data-stu-id="a154d-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a154d-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a154d-162">Next steps</span></span>
* <span data-ttu-id="a154d-163">前往 [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) 以建立 FreeBSD VM。</span><span class="sxs-lookup"><span data-stu-id="a154d-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="a154d-164">如果您想要將自己的 FreeBSD 攜至 Azure，請參閱[建立並上傳 FreeBSD VHD 到 Azure](linux/classic/freebsd-create-upload-vhd.md)。</span><span class="sxs-lookup"><span data-stu-id="a154d-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
