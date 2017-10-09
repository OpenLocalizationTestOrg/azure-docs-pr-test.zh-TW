---
title: "aaaUse 雲端 init toocustomize Linux VM |Microsoft 文件"
description: "Linux VM 的期間所建立的 toouse 雲端 init toocustomize hello Azure CLI 2.0 的方式"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="8f849-103">在建立期間使用雲端 init toocustomize Linux VM</span><span class="sxs-lookup"><span data-stu-id="8f849-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="8f849-104">本文章將示範 toomake 雲端初始化指令碼 tooset hello 主機名稱、 更新已安裝的套件，及管理使用者帳戶，以 hello Azure CLI 2.0 的方式。</span><span class="sxs-lookup"><span data-stu-id="8f849-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8f849-105">當您從 Azure CLI 建立虛擬機器 (VM) 時，會呼叫 hello 雲端初始化指令碼。</span><span class="sxs-lookup"><span data-stu-id="8f849-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="8f849-106">如需更深入的安裝應用程式、撰寫組態檔，以及插入 Key Vault 金鑰的概觀，請參閱[本教學課程 (英文)](tutorial-automate-vm-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="8f849-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="8f849-107">您也可以執行下列步驟以 hello [Azure CLI 1.0](using-cloud-init-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="8f849-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="8f849-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="8f849-108">Quick commands</span></span>
<span data-ttu-id="8f849-109">建立雲端 init.txt 指令碼設定 hello 主機名稱，更新所有的封裝，並將 sudo 使用者 tooLinux。</span><span class="sxs-lookup"><span data-stu-id="8f849-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

<span data-ttu-id="8f849-110">建立資源群組 toolaunch Vm 到[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="8f849-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8f849-111">hello 下列範例會建立名為 「 hello 資源群組*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8f849-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8f849-112">建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它以 hello 開機期間`--custom-data`參數。</span><span class="sxs-lookup"><span data-stu-id="8f849-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8f849-113">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="8f849-113">Detailed walkthrough</span></span>
<span data-ttu-id="8f849-114">啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。</span><span class="sxs-lookup"><span data-stu-id="8f849-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="8f849-115">[雲端 init](https://cloudinit.readthedocs.org)開機 hello 註冊第一次該 Linux VM 的指令碼或組態設定是標準方式 tooinject。</span><span class="sxs-lookup"><span data-stu-id="8f849-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="8f849-116">在 Azure 上，有幾個不同的方式 toomake 變更到 Linux VM 上的以在部署或啟動。</span><span class="sxs-lookup"><span data-stu-id="8f849-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="8f849-117">使用 cloud-init 插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="8f849-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="8f849-118">插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="8f849-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="8f849-119">使用 cloud-init 的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="8f849-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="8f849-120">使用 [CustomScriptExtention](extensions-customscript.md)的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="8f849-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="8f849-121">開機後隨時 tooinject 指令碼：</span><span class="sxs-lookup"><span data-stu-id="8f849-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="8f849-122">直接 SSH toorun 命令</span><span class="sxs-lookup"><span data-stu-id="8f849-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="8f849-123">插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md)，以命令方式或在 Azure 範本</span><span class="sxs-lookup"><span data-stu-id="8f849-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="8f849-124">組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。</span><span class="sxs-lookup"><span data-stu-id="8f849-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="8f849-125">VMAccess 擴充功能執行指令碼為根 hello 中相同方式使用 SSH 可以。</span><span class="sxs-lookup"><span data-stu-id="8f849-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="8f849-126">不過，使用 hello VM 延伸模組可讓數個功能非常適合您的案例而定，Azure 優惠。</span><span class="sxs-lookup"><span data-stu-id="8f849-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="8f849-127">Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰</span><span class="sxs-lookup"><span data-stu-id="8f849-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="8f849-128">Alias</span><span class="sxs-lookup"><span data-stu-id="8f849-128">Alias</span></span> | <span data-ttu-id="8f849-129">發佈者</span><span class="sxs-lookup"><span data-stu-id="8f849-129">Publisher</span></span> | <span data-ttu-id="8f849-130">提供項目</span><span class="sxs-lookup"><span data-stu-id="8f849-130">Offer</span></span> | <span data-ttu-id="8f849-131">SKU</span><span class="sxs-lookup"><span data-stu-id="8f849-131">SKU</span></span> | <span data-ttu-id="8f849-132">版本</span><span class="sxs-lookup"><span data-stu-id="8f849-132">Version</span></span> | <span data-ttu-id="8f849-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="8f849-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="8f849-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="8f849-134">CentOS</span></span> |<span data-ttu-id="8f849-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="8f849-135">OpenLogic</span></span> |<span data-ttu-id="8f849-136">Centos</span><span class="sxs-lookup"><span data-stu-id="8f849-136">Centos</span></span> |<span data-ttu-id="8f849-137">7.2</span><span class="sxs-lookup"><span data-stu-id="8f849-137">7.2</span></span> |<span data-ttu-id="8f849-138">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-138">latest</span></span> |<span data-ttu-id="8f849-139">no</span><span class="sxs-lookup"><span data-stu-id="8f849-139">no</span></span> |
| <span data-ttu-id="8f849-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="8f849-140">CoreOS</span></span> |<span data-ttu-id="8f849-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="8f849-141">CoreOS</span></span> |<span data-ttu-id="8f849-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="8f849-142">CoreOS</span></span> |<span data-ttu-id="8f849-143">Stable</span><span class="sxs-lookup"><span data-stu-id="8f849-143">Stable</span></span> |<span data-ttu-id="8f849-144">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-144">latest</span></span> |<span data-ttu-id="8f849-145">yes</span><span class="sxs-lookup"><span data-stu-id="8f849-145">yes</span></span> |
| <span data-ttu-id="8f849-146">Debian</span><span class="sxs-lookup"><span data-stu-id="8f849-146">Debian</span></span> |<span data-ttu-id="8f849-147">credativ</span><span class="sxs-lookup"><span data-stu-id="8f849-147">credativ</span></span> |<span data-ttu-id="8f849-148">Debian</span><span class="sxs-lookup"><span data-stu-id="8f849-148">Debian</span></span> |<span data-ttu-id="8f849-149">8</span><span class="sxs-lookup"><span data-stu-id="8f849-149">8</span></span> |<span data-ttu-id="8f849-150">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-150">latest</span></span> |<span data-ttu-id="8f849-151">no</span><span class="sxs-lookup"><span data-stu-id="8f849-151">no</span></span> |
| <span data-ttu-id="8f849-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="8f849-152">openSUSE</span></span> |<span data-ttu-id="8f849-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="8f849-153">SUSE</span></span> |<span data-ttu-id="8f849-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="8f849-154">openSUSE</span></span> |<span data-ttu-id="8f849-155">13.2</span><span class="sxs-lookup"><span data-stu-id="8f849-155">13.2</span></span> |<span data-ttu-id="8f849-156">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-156">latest</span></span> |<span data-ttu-id="8f849-157">no</span><span class="sxs-lookup"><span data-stu-id="8f849-157">no</span></span> |
| <span data-ttu-id="8f849-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="8f849-158">RHEL</span></span> |<span data-ttu-id="8f849-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="8f849-159">Redhat</span></span> |<span data-ttu-id="8f849-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="8f849-160">RHEL</span></span> |<span data-ttu-id="8f849-161">7.2</span><span class="sxs-lookup"><span data-stu-id="8f849-161">7.2</span></span> |<span data-ttu-id="8f849-162">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-162">latest</span></span> |<span data-ttu-id="8f849-163">no</span><span class="sxs-lookup"><span data-stu-id="8f849-163">no</span></span> |
| <span data-ttu-id="8f849-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="8f849-164">UbuntuLTS</span></span> |<span data-ttu-id="8f849-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="8f849-165">Canonical</span></span> |<span data-ttu-id="8f849-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="8f849-166">UbuntuServer</span></span> |<span data-ttu-id="8f849-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="8f849-167">14.04.4-LTS</span></span> |<span data-ttu-id="8f849-168">最新</span><span class="sxs-lookup"><span data-stu-id="8f849-168">latest</span></span> |<span data-ttu-id="8f849-169">yes</span><span class="sxs-lookup"><span data-stu-id="8f849-169">yes</span></span> |

<span data-ttu-id="8f849-170">我們會使用我們合作夥伴 tooget 雲端 for-init 包含以及他們提供 tooAzure hello 映像中的工作。</span><span class="sxs-lookup"><span data-stu-id="8f849-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="8f849-171">加入雲端初始化指令碼 toohello 建立 VM 以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8f849-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="8f849-172">toolaunch 雲端初始化指令碼在 Azure 中建立 VM 時指定 hello 雲端初始化檔案，使用 Azure CLI hello`--custom-data`切換。</span><span class="sxs-lookup"><span data-stu-id="8f849-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="8f849-173">建立資源群組 toolaunch Vm 到[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="8f849-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8f849-174">hello 下列範例會建立名為 「 hello 資源群組*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="8f849-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="8f849-175">建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="8f849-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="8f849-176">建立 Linux VM 雲端初始化指令碼 tooset hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="8f849-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="8f849-177">其中一個最簡單的 hello 和任何 Linux VM 的最重要的設定是 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8f849-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="8f849-178">使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。</span><span class="sxs-lookup"><span data-stu-id="8f849-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="8f849-179">名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8f849-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="8f849-180">在 hello 的 hello VM 的初始啟動，此雲端初始化指令碼設定為 hello 主機名稱太*myservername*。</span><span class="sxs-lookup"><span data-stu-id="8f849-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="8f849-181">建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="8f849-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="8f849-182">登入，並確認 hello hostname hello 的新 VM。</span><span class="sxs-lookup"><span data-stu-id="8f849-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="8f849-183">建立 cloud-init 指令碼</span><span class="sxs-lookup"><span data-stu-id="8f849-183">Create a cloud-init script</span></span>
<span data-ttu-id="8f849-184">為了安全性，您會想 hello 第一次開機程式 Ubuntu VM tooupdate。</span><span class="sxs-lookup"><span data-stu-id="8f849-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="8f849-185">使用雲端 init 我們可以執行以 hello 遵循指令碼，根據您使用的 hello Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="8f849-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="8f849-186">範例雲端初始化指令碼`cloud_config_apt_upgrade.txt`hello Debian 系列</span><span class="sxs-lookup"><span data-stu-id="8f849-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="8f849-187">Linux 開機之後，所有的 hello 安裝套件會更新透過**apt get**。</span><span class="sxs-lookup"><span data-stu-id="8f849-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="8f849-188">建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="8f849-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="8f849-189">登入並驗證所有封裝是否皆已更新。</span><span class="sxs-lookup"><span data-stu-id="8f849-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="8f849-190">建立雲端初始化指令碼 tooadd 使用者 tooLinux</span><span class="sxs-lookup"><span data-stu-id="8f849-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="8f849-191">Hello 任何新的 Linux VM 上的首要工作之一是 tooadd 使用者提供您自己或 tooavoid 使用*根*。</span><span class="sxs-lookup"><span data-stu-id="8f849-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="8f849-192">SSH 金鑰是針對安全性和可用性的最佳作法，並且會新增 toohello *~/.ssh/authorized_keys*這個雲端初始化指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="8f849-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="8f849-193">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="8f849-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="8f849-194">Linux 開機之後，所有的 hello 列出使用者都是建立和加入 toohello sudo 群組。</span><span class="sxs-lookup"><span data-stu-id="8f849-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="8f849-195">建立 Linux VM 與[az vm 建立](/cli/azure/vm#create)使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="8f849-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="8f849-196">登入，並確認 hello 新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="8f849-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="8f849-197">輸出</span><span class="sxs-lookup"><span data-stu-id="8f849-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="8f849-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8f849-198">Next steps</span></span>
<span data-ttu-id="8f849-199">雲端 init 變得一標準方式 toomodify Linux VM 上開機。</span><span class="sxs-lookup"><span data-stu-id="8f849-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="8f849-200">Azure 也有 VM 擴充功能，可讓您 toomodify 您 LinuxVM 開機或執行時。</span><span class="sxs-lookup"><span data-stu-id="8f849-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="8f849-201">例如，您可以使用 hello Azure VMAccessExtension tooreset SSH 或使用者資訊 hello VM 正在執行時。</span><span class="sxs-lookup"><span data-stu-id="8f849-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="8f849-202">與雲端初始化，您將需要重新開機 tooreset hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="8f849-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="8f849-203">有關虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="8f849-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="8f849-204">管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="8f849-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
