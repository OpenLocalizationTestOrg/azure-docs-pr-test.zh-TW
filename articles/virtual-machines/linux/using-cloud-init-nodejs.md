---
title: "在 Azure 中的建立期間使用 cloud-init 自訂 Linux VM | Microsoft Docs"
description: "如何透過 Azure CLI 1.0 在建立期間使用 cloud-init 自訂 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: 0b6150bca333188666935b3c9aa02c4b33690db9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation-with-the-azure-cli-10"></a><span data-ttu-id="2449d-103">透過 Azure CLI 1.0 在建立期間使用 cloud-init 自訂 Linux VM</span><span class="sxs-lookup"><span data-stu-id="2449d-103">Use cloud-init to customize a Linux VM during creation with the Azure CLI 1.0</span></span>
<span data-ttu-id="2449d-104">本文中示範如何製作 cloud-init 指令碼來設定主機名稱、更新已安裝的封裝及管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2449d-104">This article shows how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="2449d-105">在 VM 建立期間，會從 Azure CLI 呼叫 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-105">The cloud-init scripts are called during the VM creation from Azure CLI.</span></span>  <span data-ttu-id="2449d-106">本文需要：</span><span class="sxs-lookup"><span data-stu-id="2449d-106">The article requires:</span></span>

* <span data-ttu-id="2449d-107">一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。</span><span class="sxs-lookup"><span data-stu-id="2449d-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="2449d-108">使用 `azure login` 登入的 [Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="2449d-108">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="2449d-109">Azure CLI *必須處於* Azure Resource Manager 模式 `azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="2449d-109">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="2449d-110">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="2449d-110">CLI versions to complete the task</span></span>
<span data-ttu-id="2449d-111">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="2449d-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="2449d-112">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="2449d-112">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2449d-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="2449d-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="2449d-114">快速命令</span><span class="sxs-lookup"><span data-stu-id="2449d-114">Quick Commands</span></span>
<span data-ttu-id="2449d-115">建立一個設定主機名稱、更新所有封裝、並將 sudo 使用者新增至 Linux 的 cloud-init.txt 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-115">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

```sh
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
<span data-ttu-id="2449d-116">建立資源群組，以將 VM 啟動至其中。</span><span class="sxs-lookup"><span data-stu-id="2449d-116">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="2449d-117">使用 cloud-init 建立一個 Linux VM 以在開機時進行設定。</span><span class="sxs-lookup"><span data-stu-id="2449d-117">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="2449d-118">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="2449d-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="2449d-119">簡介</span><span class="sxs-lookup"><span data-stu-id="2449d-119">Introduction</span></span>
<span data-ttu-id="2449d-120">啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。</span><span class="sxs-lookup"><span data-stu-id="2449d-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="2449d-121">[Cloud-init](https://cloudinit.readthedocs.org) 第一次啟動時，會是在 Linux VM 中插入指令碼或組態設定的標準方法。</span><span class="sxs-lookup"><span data-stu-id="2449d-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="2449d-122">Azure 有三種不同的方法可在 Linux VM 部署或啟動時進行變更。</span><span class="sxs-lookup"><span data-stu-id="2449d-122">On Azure, there are a three different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="2449d-123">使用 cloud-init 插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="2449d-124">使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-124">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="2449d-125">使用 cloud-init 的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="2449d-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="2449d-126">使用 [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="2449d-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2449d-127">若開機後隨時要插入指令碼︰</span><span class="sxs-lookup"><span data-stu-id="2449d-127">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="2449d-128">直接執行命令的 SSH</span><span class="sxs-lookup"><span data-stu-id="2449d-128">SSH to run commands directly</span></span>
* <span data-ttu-id="2449d-129">使用 Azure [VMAccess 延伸模組](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，以命令方式或在 Azure 範本中插入指令碼</span><span class="sxs-lookup"><span data-stu-id="2449d-129">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="2449d-130">組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。</span><span class="sxs-lookup"><span data-stu-id="2449d-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="2449d-131">：VMAccess 延伸模組會以 root 身分，以使用 SSH 時的相同方式執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-131">: VMAccess Extension executes a script as root in the same way using SSH can.</span></span>  <span data-ttu-id="2449d-132">不過，使用 VM 延伸模組可視您的案例啟用數個 Azure 提供的實用功能。</span><span class="sxs-lookup"><span data-stu-id="2449d-132">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="2449d-133">Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰</span><span class="sxs-lookup"><span data-stu-id="2449d-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="2449d-134">Alias</span><span class="sxs-lookup"><span data-stu-id="2449d-134">Alias</span></span> | <span data-ttu-id="2449d-135">發佈者</span><span class="sxs-lookup"><span data-stu-id="2449d-135">Publisher</span></span> | <span data-ttu-id="2449d-136">提供項目</span><span class="sxs-lookup"><span data-stu-id="2449d-136">Offer</span></span> | <span data-ttu-id="2449d-137">SKU</span><span class="sxs-lookup"><span data-stu-id="2449d-137">SKU</span></span> | <span data-ttu-id="2449d-138">版本</span><span class="sxs-lookup"><span data-stu-id="2449d-138">Version</span></span> | <span data-ttu-id="2449d-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="2449d-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="2449d-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="2449d-140">CentOS</span></span> |<span data-ttu-id="2449d-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="2449d-141">OpenLogic</span></span> |<span data-ttu-id="2449d-142">Centos</span><span class="sxs-lookup"><span data-stu-id="2449d-142">Centos</span></span> |<span data-ttu-id="2449d-143">7.2</span><span class="sxs-lookup"><span data-stu-id="2449d-143">7.2</span></span> |<span data-ttu-id="2449d-144">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-144">latest</span></span> |<span data-ttu-id="2449d-145">no</span><span class="sxs-lookup"><span data-stu-id="2449d-145">no</span></span> |
| <span data-ttu-id="2449d-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2449d-146">CoreOS</span></span> |<span data-ttu-id="2449d-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2449d-147">CoreOS</span></span> |<span data-ttu-id="2449d-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="2449d-148">CoreOS</span></span> |<span data-ttu-id="2449d-149">Stable</span><span class="sxs-lookup"><span data-stu-id="2449d-149">Stable</span></span> |<span data-ttu-id="2449d-150">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-150">latest</span></span> |<span data-ttu-id="2449d-151">yes</span><span class="sxs-lookup"><span data-stu-id="2449d-151">yes</span></span> |
| <span data-ttu-id="2449d-152">Debian</span><span class="sxs-lookup"><span data-stu-id="2449d-152">Debian</span></span> |<span data-ttu-id="2449d-153">credativ</span><span class="sxs-lookup"><span data-stu-id="2449d-153">credativ</span></span> |<span data-ttu-id="2449d-154">Debian</span><span class="sxs-lookup"><span data-stu-id="2449d-154">Debian</span></span> |<span data-ttu-id="2449d-155">8</span><span class="sxs-lookup"><span data-stu-id="2449d-155">8</span></span> |<span data-ttu-id="2449d-156">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-156">latest</span></span> |<span data-ttu-id="2449d-157">no</span><span class="sxs-lookup"><span data-stu-id="2449d-157">no</span></span> |
| <span data-ttu-id="2449d-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="2449d-158">openSUSE</span></span> |<span data-ttu-id="2449d-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="2449d-159">SUSE</span></span> |<span data-ttu-id="2449d-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="2449d-160">openSUSE</span></span> |<span data-ttu-id="2449d-161">13.2</span><span class="sxs-lookup"><span data-stu-id="2449d-161">13.2</span></span> |<span data-ttu-id="2449d-162">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-162">latest</span></span> |<span data-ttu-id="2449d-163">no</span><span class="sxs-lookup"><span data-stu-id="2449d-163">no</span></span> |
| <span data-ttu-id="2449d-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="2449d-164">RHEL</span></span> |<span data-ttu-id="2449d-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="2449d-165">Redhat</span></span> |<span data-ttu-id="2449d-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="2449d-166">RHEL</span></span> |<span data-ttu-id="2449d-167">7.2</span><span class="sxs-lookup"><span data-stu-id="2449d-167">7.2</span></span> |<span data-ttu-id="2449d-168">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-168">latest</span></span> |<span data-ttu-id="2449d-169">no</span><span class="sxs-lookup"><span data-stu-id="2449d-169">no</span></span> |
| <span data-ttu-id="2449d-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="2449d-170">UbuntuLTS</span></span> |<span data-ttu-id="2449d-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="2449d-171">Canonical</span></span> |<span data-ttu-id="2449d-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="2449d-172">UbuntuServer</span></span> |<span data-ttu-id="2449d-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="2449d-173">14.04.4-LTS</span></span> |<span data-ttu-id="2449d-174">最新</span><span class="sxs-lookup"><span data-stu-id="2449d-174">latest</span></span> |<span data-ttu-id="2449d-175">yes</span><span class="sxs-lookup"><span data-stu-id="2449d-175">yes</span></span> |

<span data-ttu-id="2449d-176">Microsoft 正與我們的合作夥伴合作，以期在他們提供給 Azure 的映像中包含和使用 cloud-init。</span><span class="sxs-lookup"><span data-stu-id="2449d-176">Microsoft is working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="adding-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="2449d-177">將 cloud-init 指令碼加入使用 Azure CLI 建立 VM 的作業中</span><span class="sxs-lookup"><span data-stu-id="2449d-177">Adding a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="2449d-178">在 Azure 中建立 VM 時，若要啟動 cloud-init 指令碼，請使用 Azure CLI `--custom-data` 參數來指定 cloud-init 檔案。</span><span class="sxs-lookup"><span data-stu-id="2449d-178">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="2449d-179">建立資源群組，以將 VM 啟動至其中。</span><span class="sxs-lookup"><span data-stu-id="2449d-179">Create a resource group to launch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="2449d-180">使用 cloud-init 建立一個 Linux VM 以在開機時進行設定。</span><span class="sxs-lookup"><span data-stu-id="2449d-180">Create a Linux VM using cloud-init to configure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="2449d-181">建立 cloud-init 指令碼設定 Linux VM 的主機名稱</span><span class="sxs-lookup"><span data-stu-id="2449d-181">Creating a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="2449d-182">對任何 Linux VM 而言，其中一個最簡單且最重要的設定就是主機名稱。</span><span class="sxs-lookup"><span data-stu-id="2449d-182">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="2449d-183">使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。</span><span class="sxs-lookup"><span data-stu-id="2449d-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="2449d-184">名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="2449d-185">在 VM 首次啟動期間，這個 cloud-init 指令碼會將主機名稱設定為 `myservername`。</span><span class="sxs-lookup"><span data-stu-id="2449d-185">During the initial startup of the VM, this cloud-init script sets the hostname to `myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="2449d-186">登入並驗證新 VM 的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="2449d-186">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-to-update-linux"></a><span data-ttu-id="2449d-187">建立 cloud-init 指令碼以更新 Linux </span><span class="sxs-lookup"><span data-stu-id="2449d-187">Creating a cloud-init script to update Linux</span></span>
<span data-ttu-id="2449d-188">基於安全性，您希望您的 Ubuntu VM 能在第一次開機時進行更新。</span><span class="sxs-lookup"><span data-stu-id="2449d-188">For security, you want your Ubuntu VM to update on the first boot.</span></span>  <span data-ttu-id="2449d-189">我們可以使用 cloud-init 和下列指令碼執行這個作業，視您使用的 Linux 散發套件而定。</span><span class="sxs-lookup"><span data-stu-id="2449d-189">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="2449d-190">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_apt_upgrade.txt`</span><span class="sxs-lookup"><span data-stu-id="2449d-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="2449d-191">在 Linux 開機後，所有已安裝的封裝都會透過 `apt-get`更新。</span><span class="sxs-lookup"><span data-stu-id="2449d-191">After Linux has booted, all the installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="2449d-192">登入並驗證所有封裝是否皆已更新。</span><span class="sxs-lookup"><span data-stu-id="2449d-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="2449d-193">建立 cloud-init 指令碼將使用者加入 Linux 中</span><span class="sxs-lookup"><span data-stu-id="2449d-193">Creating a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="2449d-194">針對任何新的 Linux VM，首要工作之一就是為您自己新增一位使用者，或是避免使用 `root`。</span><span class="sxs-lookup"><span data-stu-id="2449d-194">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using `root`.</span></span> <span data-ttu-id="2449d-195">SSH 金鑰是基於安全性和可用性的最佳作法，它們會隨此 cloud-init 指令碼新增至 `~/.ssh/authorized_keys` 檔案。</span><span class="sxs-lookup"><span data-stu-id="2449d-195">SSH keys are best practice for security and for usability and they are added to the `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="2449d-196">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="2449d-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="2449d-197">Linux 開機之後，所有列出的使用者就會建立並加入 sudo 群組。</span><span class="sxs-lookup"><span data-stu-id="2449d-197">After Linux has booted, all the listed users are created and added to the sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="2449d-198">登入並驗證新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="2449d-198">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="2449d-199">輸出</span><span class="sxs-lookup"><span data-stu-id="2449d-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="2449d-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2449d-200">Next Steps</span></span>
<span data-ttu-id="2449d-201">Cloud-init 已成為在開機時修改 Linux VM 的一種標準方式。</span><span class="sxs-lookup"><span data-stu-id="2449d-201">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="2449d-202">Azure 也有 VM 延伸模組，可讓您在開機或執行時修改您的 LinuxVM。</span><span class="sxs-lookup"><span data-stu-id="2449d-202">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="2449d-203">例如，當 VM 執行時，您可以使用 Azure VMAccessExtension 來重設 SSH 或使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="2449d-203">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="2449d-204">使用 cloud-init，您必須重新開機才能重設密碼。</span><span class="sxs-lookup"><span data-stu-id="2449d-204">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="2449d-205">有關虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="2449d-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="2449d-206">管理使用者、SSH，並使用 VMAccess 擴充功能檢查或修復 Azure Linux VM 上的磁碟</span><span class="sxs-lookup"><span data-stu-id="2449d-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

