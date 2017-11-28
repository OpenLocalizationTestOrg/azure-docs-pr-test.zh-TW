---
title: "使用 cloud-init 自訂 Linux VM | Microsoft Docs"
description: "如何透過 Azure CLI 2.0 在建立期間使用 cloud-init 自訂 Linux VM"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="7146e-103">在建立期間使用 cloud-init 自訂 Linux VM</span><span class="sxs-lookup"><span data-stu-id="7146e-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="7146e-104">本文會示範如何透過 Azure CLI 2.0 製作 cloud-init 指令碼來設定主機名稱、更新已安裝的封裝及管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="7146e-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="7146e-105">當您從 Azure CLI 建立虛擬機器 (VM) 時，會呼叫 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="7146e-106">如需更深入的安裝應用程式、撰寫組態檔，以及插入 Key Vault 金鑰的概觀，請參閱[本教學課程 (英文)](tutorial-automate-vm-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="7146e-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="7146e-107">您也可以使用 [Azure CLI 1.0](using-cloud-init-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="7146e-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="7146e-108">快速命令</span><span class="sxs-lookup"><span data-stu-id="7146e-108">Quick commands</span></span>
<span data-ttu-id="7146e-109">建立一個設定主機名稱、更新所有封裝、並將 sudo 使用者新增至 Linux 的 cloud-init.txt 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="7146e-110">使用 [az group create](/cli/azure/group#create) 來建立資源群組以在其中啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="7146e-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7146e-111">下列範例會建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="7146e-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7146e-112">透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM，並使用 cloud-init 在以 `--custom-data` 參數開機期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146e-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="7146e-113">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="7146e-113">Detailed walkthrough</span></span>
<span data-ttu-id="7146e-114">啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。</span><span class="sxs-lookup"><span data-stu-id="7146e-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="7146e-115">[Cloud-init](https://cloudinit.readthedocs.org) 第一次啟動時，會是在 Linux VM 中插入指令碼或組態設定的標準方法。</span><span class="sxs-lookup"><span data-stu-id="7146e-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="7146e-116">Azure 有許多不同的方法可在 Linux VM 部署或開機時進行變更。</span><span class="sxs-lookup"><span data-stu-id="7146e-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="7146e-117">使用 cloud-init 插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="7146e-118">使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md)插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="7146e-119">使用 cloud-init 的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="7146e-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="7146e-120">使用 [CustomScriptExtention](extensions-customscript.md)的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="7146e-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="7146e-121">若開機後隨時要插入指令碼︰</span><span class="sxs-lookup"><span data-stu-id="7146e-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="7146e-122">直接執行命令的 SSH</span><span class="sxs-lookup"><span data-stu-id="7146e-122">SSH to run commands directly</span></span>
* <span data-ttu-id="7146e-123">使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md)，以命令方式或在 Azure 範本中插入指令碼</span><span class="sxs-lookup"><span data-stu-id="7146e-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="7146e-124">組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。</span><span class="sxs-lookup"><span data-stu-id="7146e-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="7146e-125">VMAccess 延伸模組會採用根身分，以及與使用 SSH 時的相同方式執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="7146e-126">不過，使用 VM 延伸模組可視您的案例啟用數個 Azure 提供的實用功能。</span><span class="sxs-lookup"><span data-stu-id="7146e-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="7146e-127">Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰</span><span class="sxs-lookup"><span data-stu-id="7146e-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="7146e-128">Alias</span><span class="sxs-lookup"><span data-stu-id="7146e-128">Alias</span></span> | <span data-ttu-id="7146e-129">發佈者</span><span class="sxs-lookup"><span data-stu-id="7146e-129">Publisher</span></span> | <span data-ttu-id="7146e-130">提供項目</span><span class="sxs-lookup"><span data-stu-id="7146e-130">Offer</span></span> | <span data-ttu-id="7146e-131">SKU</span><span class="sxs-lookup"><span data-stu-id="7146e-131">SKU</span></span> | <span data-ttu-id="7146e-132">版本</span><span class="sxs-lookup"><span data-stu-id="7146e-132">Version</span></span> | <span data-ttu-id="7146e-133">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="7146e-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="7146e-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="7146e-134">CentOS</span></span> |<span data-ttu-id="7146e-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="7146e-135">OpenLogic</span></span> |<span data-ttu-id="7146e-136">Centos</span><span class="sxs-lookup"><span data-stu-id="7146e-136">Centos</span></span> |<span data-ttu-id="7146e-137">7.2</span><span class="sxs-lookup"><span data-stu-id="7146e-137">7.2</span></span> |<span data-ttu-id="7146e-138">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-138">latest</span></span> |<span data-ttu-id="7146e-139">no</span><span class="sxs-lookup"><span data-stu-id="7146e-139">no</span></span> |
| <span data-ttu-id="7146e-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7146e-140">CoreOS</span></span> |<span data-ttu-id="7146e-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7146e-141">CoreOS</span></span> |<span data-ttu-id="7146e-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7146e-142">CoreOS</span></span> |<span data-ttu-id="7146e-143">Stable</span><span class="sxs-lookup"><span data-stu-id="7146e-143">Stable</span></span> |<span data-ttu-id="7146e-144">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-144">latest</span></span> |<span data-ttu-id="7146e-145">yes</span><span class="sxs-lookup"><span data-stu-id="7146e-145">yes</span></span> |
| <span data-ttu-id="7146e-146">Debian</span><span class="sxs-lookup"><span data-stu-id="7146e-146">Debian</span></span> |<span data-ttu-id="7146e-147">credativ</span><span class="sxs-lookup"><span data-stu-id="7146e-147">credativ</span></span> |<span data-ttu-id="7146e-148">Debian</span><span class="sxs-lookup"><span data-stu-id="7146e-148">Debian</span></span> |<span data-ttu-id="7146e-149">8</span><span class="sxs-lookup"><span data-stu-id="7146e-149">8</span></span> |<span data-ttu-id="7146e-150">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-150">latest</span></span> |<span data-ttu-id="7146e-151">no</span><span class="sxs-lookup"><span data-stu-id="7146e-151">no</span></span> |
| <span data-ttu-id="7146e-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7146e-152">openSUSE</span></span> |<span data-ttu-id="7146e-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="7146e-153">SUSE</span></span> |<span data-ttu-id="7146e-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7146e-154">openSUSE</span></span> |<span data-ttu-id="7146e-155">13.2</span><span class="sxs-lookup"><span data-stu-id="7146e-155">13.2</span></span> |<span data-ttu-id="7146e-156">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-156">latest</span></span> |<span data-ttu-id="7146e-157">no</span><span class="sxs-lookup"><span data-stu-id="7146e-157">no</span></span> |
| <span data-ttu-id="7146e-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="7146e-158">RHEL</span></span> |<span data-ttu-id="7146e-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="7146e-159">Redhat</span></span> |<span data-ttu-id="7146e-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="7146e-160">RHEL</span></span> |<span data-ttu-id="7146e-161">7.2</span><span class="sxs-lookup"><span data-stu-id="7146e-161">7.2</span></span> |<span data-ttu-id="7146e-162">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-162">latest</span></span> |<span data-ttu-id="7146e-163">no</span><span class="sxs-lookup"><span data-stu-id="7146e-163">no</span></span> |
| <span data-ttu-id="7146e-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="7146e-164">UbuntuLTS</span></span> |<span data-ttu-id="7146e-165">Canonical</span><span class="sxs-lookup"><span data-stu-id="7146e-165">Canonical</span></span> |<span data-ttu-id="7146e-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="7146e-166">UbuntuServer</span></span> |<span data-ttu-id="7146e-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="7146e-167">14.04.4-LTS</span></span> |<span data-ttu-id="7146e-168">最新</span><span class="sxs-lookup"><span data-stu-id="7146e-168">latest</span></span> |<span data-ttu-id="7146e-169">yes</span><span class="sxs-lookup"><span data-stu-id="7146e-169">yes</span></span> |

<span data-ttu-id="7146e-170">我們正在與合作夥伴合作，以期在他們提供給 Azure 的映像中包含和使用 cloud-init。</span><span class="sxs-lookup"><span data-stu-id="7146e-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="7146e-171">將 cloud-init 指令碼新增至使用 Azure CLI 建立 VM 的作業中</span><span class="sxs-lookup"><span data-stu-id="7146e-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="7146e-172">在 Azure 中建立 VM 時，若要啟動 cloud-init 指令碼，請使用 Azure CLI `--custom-data` 參數來指定 cloud-init 檔案。</span><span class="sxs-lookup"><span data-stu-id="7146e-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="7146e-173">使用 [az group create](/cli/azure/group#create) 來建立資源群組以在其中啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="7146e-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7146e-174">下列範例會建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="7146e-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="7146e-175">透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146e-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="7146e-176">建立 cloud-init 指令碼以設定 Linux VM 的主機名稱</span><span class="sxs-lookup"><span data-stu-id="7146e-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="7146e-177">對任何 Linux VM 而言，其中一個最簡單且最重要的設定就是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="7146e-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="7146e-178">使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。</span><span class="sxs-lookup"><span data-stu-id="7146e-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="7146e-179">名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="7146e-180">在 VM 首次啟動期間，這個 cloud-init 指令碼會將主機名稱設定為 myservername。</span><span class="sxs-lookup"><span data-stu-id="7146e-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="7146e-181">透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146e-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="7146e-182">登入並驗證新 VM 的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="7146e-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="7146e-183">建立 cloud-init 指令碼</span><span class="sxs-lookup"><span data-stu-id="7146e-183">Create a cloud-init script</span></span>
<span data-ttu-id="7146e-184">基於安全性，您希望您的 Ubuntu VM 能在第一次開機時進行更新。</span><span class="sxs-lookup"><span data-stu-id="7146e-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="7146e-185">我們可以使用 cloud-init 和下列指令碼執行這個作業，視您使用的 Linux 散發套件而定。</span><span class="sxs-lookup"><span data-stu-id="7146e-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="7146e-186">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_apt_upgrade.txt`</span><span class="sxs-lookup"><span data-stu-id="7146e-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="7146e-187">在 Linux 開機後，所有已安裝的封裝都會透過 apt-get 更新。</span><span class="sxs-lookup"><span data-stu-id="7146e-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="7146e-188">透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146e-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="7146e-189">登入並驗證所有封裝是否皆已更新。</span><span class="sxs-lookup"><span data-stu-id="7146e-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="7146e-190">建立 cloud-init 指令碼以將使用者新增至 Linux 中</span><span class="sxs-lookup"><span data-stu-id="7146e-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="7146e-191">針對任何新的 Linux VM，首要工作之一就是為您自己新增一位使用者，或是避免使用根身分。</span><span class="sxs-lookup"><span data-stu-id="7146e-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="7146e-192">SSH 金鑰是基於安全性和可用性的最佳作法，它們會隨此 cloud-init 指令碼新增至 ~/.ssh/authorized_keys 檔案。</span><span class="sxs-lookup"><span data-stu-id="7146e-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="7146e-193">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="7146e-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="7146e-194">Linux 開機之後，所有列出的使用者就會建立並加入 sudo 群組。</span><span class="sxs-lookup"><span data-stu-id="7146e-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="7146e-195">透過 [az vm create](/cli/azure/vm#create) 建立 Linux VM 並使用 cloud-init 在開機期間進行設定。</span><span class="sxs-lookup"><span data-stu-id="7146e-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="7146e-196">登入並驗證新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="7146e-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="7146e-197">輸出</span><span class="sxs-lookup"><span data-stu-id="7146e-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="7146e-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7146e-198">Next steps</span></span>
<span data-ttu-id="7146e-199">Cloud-init 已成為在開機時修改 Linux VM 的一種標準方式。</span><span class="sxs-lookup"><span data-stu-id="7146e-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="7146e-200">Azure 也有 VM 延伸模組，可讓您在開機或執行時修改您的 LinuxVM。</span><span class="sxs-lookup"><span data-stu-id="7146e-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="7146e-201">例如，當 VM 執行時，您可以使用 Azure VMAccessExtension 來重設 SSH 或使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="7146e-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="7146e-202">使用 cloud-init，您必須重新開機才能重設密碼。</span><span class="sxs-lookup"><span data-stu-id="7146e-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="7146e-203">有關虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="7146e-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="7146e-204">管理使用者、SSH，並使用 VMAccess 擴充功能檢查或修復 Azure Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="7146e-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)