---
title: "aaaUsing 雲端 init toocustomize Linux VM 在 Azure 中建立期間 |Microsoft 文件"
description: "Linux VM 的期間所建立的 toouse 雲端 init toocustomize hello Azure CLI 1.0 的方式"
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
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="b4680-103">使用雲端 init toocustomize Linux VM 建立 hello Azure CLI 1.0 與期間</span><span class="sxs-lookup"><span data-stu-id="b4680-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="b4680-104">本文示範 toomake 雲端初始化指令碼 tooset 如何 hello 主機名稱，更新已安裝的封裝，並管理使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4680-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="b4680-105">在 hello Azure CLI 從 VM 建立期間呼叫 hello 雲端初始化指令碼。</span><span class="sxs-lookup"><span data-stu-id="b4680-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="b4680-106">hello 文章需要：</span><span class="sxs-lookup"><span data-stu-id="b4680-106">hello article requires:</span></span>

* <span data-ttu-id="b4680-107">一個 Azure 帳戶 ([取得免費試用帳戶](https://azure.microsoft.com/pricing/free-trial/))。</span><span class="sxs-lookup"><span data-stu-id="b4680-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b4680-108">hello [Azure CLI](../../cli-install-nodejs.md)登入的`azure login`。</span><span class="sxs-lookup"><span data-stu-id="b4680-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b4680-109">hello Azure CLI*必須在*Azure Resource Manager 模式`azure config mode arm`。</span><span class="sxs-lookup"><span data-stu-id="b4680-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b4680-110">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="b4680-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="b4680-111">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="b4680-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="b4680-112">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="b4680-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b4680-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="b4680-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="b4680-114">快速命令</span><span class="sxs-lookup"><span data-stu-id="b4680-114">Quick Commands</span></span>
<span data-ttu-id="b4680-115">建立雲端 init.txt 指令碼設定 hello 主機名稱，更新所有的封裝，並將 sudo 使用者 tooLinux。</span><span class="sxs-lookup"><span data-stu-id="b4680-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

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
<span data-ttu-id="b4680-116">建立資源群組 toolaunch 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="b4680-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b4680-117">建立 Linux VM，使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="b4680-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="b4680-118">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="b4680-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="b4680-119">簡介</span><span class="sxs-lookup"><span data-stu-id="b4680-119">Introduction</span></span>
<span data-ttu-id="b4680-120">啟動新的 Linux VM 時，Linux VM 會是標準模式，沒有自訂或符合您需求的選項。</span><span class="sxs-lookup"><span data-stu-id="b4680-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="b4680-121">[雲端 init](https://cloudinit.readthedocs.org)開機 hello 註冊第一次該 Linux VM 的指令碼或組態設定是標準方式 tooinject。</span><span class="sxs-lookup"><span data-stu-id="b4680-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="b4680-122">在 Azure 上，有三種不同方式 toomake 變更到 Linux VM 上的以在部署或啟動。</span><span class="sxs-lookup"><span data-stu-id="b4680-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="b4680-123">使用 cloud-init 插入指令碼。</span><span class="sxs-lookup"><span data-stu-id="b4680-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="b4680-124">插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b4680-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="b4680-125">使用 cloud-init 的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="b4680-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="b4680-126">使用 [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)的 Azure 範本。</span><span class="sxs-lookup"><span data-stu-id="b4680-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b4680-127">開機後隨時 tooinject 指令碼：</span><span class="sxs-lookup"><span data-stu-id="b4680-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="b4680-128">直接 SSH toorun 命令</span><span class="sxs-lookup"><span data-stu-id="b4680-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="b4680-129">插入指令碼使用 hello Azure [VMAccess 擴充功能](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，以命令方式或在 Azure 範本</span><span class="sxs-lookup"><span data-stu-id="b4680-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="b4680-130">組態管理工具，例如 Ansible、Salt、Chef 及 Puppet。</span><span class="sxs-lookup"><span data-stu-id="b4680-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="b4680-131">: VMAccess 擴充功能執行指令碼為根 hello 中相同方式使用 SSH 可以。</span><span class="sxs-lookup"><span data-stu-id="b4680-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="b4680-132">不過，使用 hello VM 延伸模組可讓數個功能非常適合您的案例而定，Azure 優惠。</span><span class="sxs-lookup"><span data-stu-id="b4680-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="b4680-133">Cloud-init 在 Azure VM quick-create 映像別名上的可用性︰</span><span class="sxs-lookup"><span data-stu-id="b4680-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="b4680-134">Alias</span><span class="sxs-lookup"><span data-stu-id="b4680-134">Alias</span></span> | <span data-ttu-id="b4680-135">發佈者</span><span class="sxs-lookup"><span data-stu-id="b4680-135">Publisher</span></span> | <span data-ttu-id="b4680-136">提供項目</span><span class="sxs-lookup"><span data-stu-id="b4680-136">Offer</span></span> | <span data-ttu-id="b4680-137">SKU</span><span class="sxs-lookup"><span data-stu-id="b4680-137">SKU</span></span> | <span data-ttu-id="b4680-138">版本</span><span class="sxs-lookup"><span data-stu-id="b4680-138">Version</span></span> | <span data-ttu-id="b4680-139">Cloud-init</span><span class="sxs-lookup"><span data-stu-id="b4680-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b4680-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="b4680-140">CentOS</span></span> |<span data-ttu-id="b4680-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="b4680-141">OpenLogic</span></span> |<span data-ttu-id="b4680-142">Centos</span><span class="sxs-lookup"><span data-stu-id="b4680-142">Centos</span></span> |<span data-ttu-id="b4680-143">7.2</span><span class="sxs-lookup"><span data-stu-id="b4680-143">7.2</span></span> |<span data-ttu-id="b4680-144">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-144">latest</span></span> |<span data-ttu-id="b4680-145">no</span><span class="sxs-lookup"><span data-stu-id="b4680-145">no</span></span> |
| <span data-ttu-id="b4680-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4680-146">CoreOS</span></span> |<span data-ttu-id="b4680-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4680-147">CoreOS</span></span> |<span data-ttu-id="b4680-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="b4680-148">CoreOS</span></span> |<span data-ttu-id="b4680-149">Stable</span><span class="sxs-lookup"><span data-stu-id="b4680-149">Stable</span></span> |<span data-ttu-id="b4680-150">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-150">latest</span></span> |<span data-ttu-id="b4680-151">yes</span><span class="sxs-lookup"><span data-stu-id="b4680-151">yes</span></span> |
| <span data-ttu-id="b4680-152">Debian</span><span class="sxs-lookup"><span data-stu-id="b4680-152">Debian</span></span> |<span data-ttu-id="b4680-153">credativ</span><span class="sxs-lookup"><span data-stu-id="b4680-153">credativ</span></span> |<span data-ttu-id="b4680-154">Debian</span><span class="sxs-lookup"><span data-stu-id="b4680-154">Debian</span></span> |<span data-ttu-id="b4680-155">8</span><span class="sxs-lookup"><span data-stu-id="b4680-155">8</span></span> |<span data-ttu-id="b4680-156">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-156">latest</span></span> |<span data-ttu-id="b4680-157">no</span><span class="sxs-lookup"><span data-stu-id="b4680-157">no</span></span> |
| <span data-ttu-id="b4680-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b4680-158">openSUSE</span></span> |<span data-ttu-id="b4680-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="b4680-159">SUSE</span></span> |<span data-ttu-id="b4680-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="b4680-160">openSUSE</span></span> |<span data-ttu-id="b4680-161">13.2</span><span class="sxs-lookup"><span data-stu-id="b4680-161">13.2</span></span> |<span data-ttu-id="b4680-162">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-162">latest</span></span> |<span data-ttu-id="b4680-163">no</span><span class="sxs-lookup"><span data-stu-id="b4680-163">no</span></span> |
| <span data-ttu-id="b4680-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4680-164">RHEL</span></span> |<span data-ttu-id="b4680-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="b4680-165">Redhat</span></span> |<span data-ttu-id="b4680-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="b4680-166">RHEL</span></span> |<span data-ttu-id="b4680-167">7.2</span><span class="sxs-lookup"><span data-stu-id="b4680-167">7.2</span></span> |<span data-ttu-id="b4680-168">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-168">latest</span></span> |<span data-ttu-id="b4680-169">no</span><span class="sxs-lookup"><span data-stu-id="b4680-169">no</span></span> |
| <span data-ttu-id="b4680-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="b4680-170">UbuntuLTS</span></span> |<span data-ttu-id="b4680-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="b4680-171">Canonical</span></span> |<span data-ttu-id="b4680-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b4680-172">UbuntuServer</span></span> |<span data-ttu-id="b4680-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="b4680-173">14.04.4-LTS</span></span> |<span data-ttu-id="b4680-174">最新</span><span class="sxs-lookup"><span data-stu-id="b4680-174">latest</span></span> |<span data-ttu-id="b4680-175">yes</span><span class="sxs-lookup"><span data-stu-id="b4680-175">yes</span></span> |

<span data-ttu-id="b4680-176">Microsoft 會使用我們合作夥伴 tooget 雲端 for-init 包含以及他們提供 tooAzure hello 映像中的工作。</span><span class="sxs-lookup"><span data-stu-id="b4680-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="b4680-177">加入雲端初始化指令碼 toohello 建立 VM 以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4680-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="b4680-178">toolaunch 雲端初始化指令碼在 Azure 中建立 VM 時指定 hello 雲端初始化檔案，使用 Azure CLI hello`--custom-data`切換。</span><span class="sxs-lookup"><span data-stu-id="b4680-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="b4680-179">建立資源群組 toolaunch 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="b4680-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="b4680-180">建立 Linux VM，使用雲端 init tooconfigure 它在開機期間。</span><span class="sxs-lookup"><span data-stu-id="b4680-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

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

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="b4680-181">建立 Linux VM 雲端初始化指令碼 tooset hello 主機名稱</span><span class="sxs-lookup"><span data-stu-id="b4680-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="b4680-182">其中一個最簡單的 hello 和任何 Linux VM 的最重要的設定是 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b4680-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="b4680-183">使用 cloud-init 和這個指令碼就可以輕鬆地設定這個項目。</span><span class="sxs-lookup"><span data-stu-id="b4680-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="b4680-184">名為 `cloud_config_hostname.txt`的範例 cloud-init 指令碼。</span><span class="sxs-lookup"><span data-stu-id="b4680-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="b4680-185">在 hello 的 hello VM 的初始啟動，此雲端初始化指令碼設定為 hello 主機名稱太`myservername`。</span><span class="sxs-lookup"><span data-stu-id="b4680-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

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

<span data-ttu-id="b4680-186">登入，並確認 hello hostname hello 的新 VM。</span><span class="sxs-lookup"><span data-stu-id="b4680-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="b4680-187">建立雲端初始化指令碼 tooupdate Linux</span><span class="sxs-lookup"><span data-stu-id="b4680-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="b4680-188">為了安全性，您會想 hello 第一次開機程式 Ubuntu VM tooupdate。</span><span class="sxs-lookup"><span data-stu-id="b4680-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="b4680-189">使用雲端 init 我們可以執行以 hello 遵循指令碼，根據您使用的 hello Linux 散發套件。</span><span class="sxs-lookup"><span data-stu-id="b4680-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="b4680-190">範例雲端初始化指令碼`cloud_config_apt_upgrade.txt`hello Debian 系列</span><span class="sxs-lookup"><span data-stu-id="b4680-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="b4680-191">Linux 開機之後，所有的 hello 安裝套件會更新透過`apt-get`。</span><span class="sxs-lookup"><span data-stu-id="b4680-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

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

<span data-ttu-id="b4680-192">登入並驗證所有封裝是否皆已更新。</span><span class="sxs-lookup"><span data-stu-id="b4680-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="b4680-193">建立雲端初始化指令碼 tooadd 使用者 tooLinux</span><span class="sxs-lookup"><span data-stu-id="b4680-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="b4680-194">Hello 任何新的 Linux VM 上的首要工作之一是 tooadd 使用者提供您自己或 tooavoid 使用`root`。</span><span class="sxs-lookup"><span data-stu-id="b4680-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="b4680-195">SSH 金鑰是針對安全性和可用性的最佳作法，並且會新增 toohello`~/.ssh/authorized_keys`這個雲端初始化指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="b4680-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="b4680-196">適用於 Debian 系列的範例 cloud-init 指令碼 `cloud_config_add_users.txt`</span><span class="sxs-lookup"><span data-stu-id="b4680-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="b4680-197">Linux 開機之後，所有的 hello 列出使用者都是建立和加入 toohello sudo 群組。</span><span class="sxs-lookup"><span data-stu-id="b4680-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

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

<span data-ttu-id="b4680-198">登入，並確認 hello 新建立的使用者。</span><span class="sxs-lookup"><span data-stu-id="b4680-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="b4680-199">輸出</span><span class="sxs-lookup"><span data-stu-id="b4680-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="b4680-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4680-200">Next Steps</span></span>
<span data-ttu-id="b4680-201">雲端 init 變得一標準方式 toomodify Linux VM 上開機。</span><span class="sxs-lookup"><span data-stu-id="b4680-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="b4680-202">Azure 也有 VM 擴充功能，可讓您 toomodify 您 LinuxVM 開機或執行時。</span><span class="sxs-lookup"><span data-stu-id="b4680-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="b4680-203">例如，您可以使用 hello Azure VMAccessExtension tooreset SSH 或使用者資訊 hello VM 正在執行時。</span><span class="sxs-lookup"><span data-stu-id="b4680-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="b4680-204">與雲端初始化，您將需要重新開機 tooreset hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="b4680-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="b4680-205">有關虛擬機器擴充功能和功能</span><span class="sxs-lookup"><span data-stu-id="b4680-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b4680-206">管理使用者、 SSH 和核取，或使用 Azure Linux Vm 上的修復磁片 hello VMAccess 擴充功能</span><span class="sxs-lookup"><span data-stu-id="b4680-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

