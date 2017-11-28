---
title: "使用 Azure CLI 1.0 來建立 Linux VM | Microsoft Docs"
description: "使用 Azure CLI 1.0 在 Azure 上建立 Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="84bad-103">使用 Azure CLI 1.0 來建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="84bad-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="84bad-104">本文示範如何使用 Azure 命令列介面 (CLI) 中的 `azure vm quick-create` 命令，在 Azure 上快速部署 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="84bad-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="84bad-105">`quick-create` 命令會將 VM 部署在基本且安全的基礎結構內，可讓您快速地建立原型或測試概念。</span><span class="sxs-lookup"><span data-stu-id="84bad-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="84bad-106">若要使用 Azure CLI 2.0 來建立 VM，請參閱[使用 Azure CLI 來建立 VM](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="84bad-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="84bad-107">您也可以使用 [Azure 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)來快速部署 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="84bad-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="84bad-108">本文需要 [SSH 公開金鑰和私密金鑰檔案](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="84bad-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="84bad-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="84bad-109">Quick commands</span></span>

<span data-ttu-id="84bad-110">以下範例示範如何部署 CoreOS VM，並附加您的安全殼層 (SSH) 金鑰 (您的引數可能會不同)：</span><span class="sxs-lookup"><span data-stu-id="84bad-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="84bad-111">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="84bad-111">Detailed walkthrough</span></span>

<span data-ttu-id="84bad-112">下列逐步解說包含要部署的 UbuntuLTS VM，說明每個步驟的執行內容。</span><span class="sxs-lookup"><span data-stu-id="84bad-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="84bad-113">VM quick-create 別名</span><span class="sxs-lookup"><span data-stu-id="84bad-113">VM quick-create aliases</span></span>

<span data-ttu-id="84bad-114">使用對應到常見作業系統散發版本的 Azure CLI 別名，可以快速選擇版本。</span><span class="sxs-lookup"><span data-stu-id="84bad-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="84bad-115">下表列出別名 (依 Azure CLI 0.10 版)。</span><span class="sxs-lookup"><span data-stu-id="84bad-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="84bad-116">所有使用 `quick-create` 建立的 VM 預設都是由固態硬碟 (SSD) 儲存空間支援，SSD 提供更快的佈建及高效能磁碟存取。</span><span class="sxs-lookup"><span data-stu-id="84bad-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="84bad-117">(這些別名代表 Azure 上可用 OS 散發版本的一小部分。</span><span class="sxs-lookup"><span data-stu-id="84bad-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="84bad-118">[在 PowerShell 中](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)、[Web 上](https://azure.microsoft.com/marketplace/virtual-machines/)搜尋映像以在 Azure Marketplace 中尋找更多映像，或者[可以上傳您自己的自訂映像](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。)</span><span class="sxs-lookup"><span data-stu-id="84bad-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="84bad-119">Alias</span><span class="sxs-lookup"><span data-stu-id="84bad-119">Alias</span></span> | <span data-ttu-id="84bad-120">發佈者</span><span class="sxs-lookup"><span data-stu-id="84bad-120">Publisher</span></span> | <span data-ttu-id="84bad-121">提供項目</span><span class="sxs-lookup"><span data-stu-id="84bad-121">Offer</span></span> | <span data-ttu-id="84bad-122">SKU</span><span class="sxs-lookup"><span data-stu-id="84bad-122">SKU</span></span> | <span data-ttu-id="84bad-123">版本</span><span class="sxs-lookup"><span data-stu-id="84bad-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="84bad-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="84bad-124">CentOS</span></span> |<span data-ttu-id="84bad-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="84bad-125">OpenLogic</span></span> |<span data-ttu-id="84bad-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="84bad-126">CentOS</span></span> |<span data-ttu-id="84bad-127">7.2</span><span class="sxs-lookup"><span data-stu-id="84bad-127">7.2</span></span> |<span data-ttu-id="84bad-128">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-128">latest</span></span> |
| <span data-ttu-id="84bad-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="84bad-129">CoreOS</span></span> |<span data-ttu-id="84bad-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="84bad-130">CoreOS</span></span> |<span data-ttu-id="84bad-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="84bad-131">CoreOS</span></span> |<span data-ttu-id="84bad-132">Stable</span><span class="sxs-lookup"><span data-stu-id="84bad-132">Stable</span></span> |<span data-ttu-id="84bad-133">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-133">latest</span></span> |
| <span data-ttu-id="84bad-134">Debian</span><span class="sxs-lookup"><span data-stu-id="84bad-134">Debian</span></span> |<span data-ttu-id="84bad-135">credativ</span><span class="sxs-lookup"><span data-stu-id="84bad-135">credativ</span></span> |<span data-ttu-id="84bad-136">Debian</span><span class="sxs-lookup"><span data-stu-id="84bad-136">Debian</span></span> |<span data-ttu-id="84bad-137">8</span><span class="sxs-lookup"><span data-stu-id="84bad-137">8</span></span> |<span data-ttu-id="84bad-138">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-138">latest</span></span> |
| <span data-ttu-id="84bad-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="84bad-139">openSUSE</span></span> |<span data-ttu-id="84bad-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="84bad-140">SUSE</span></span> |<span data-ttu-id="84bad-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="84bad-141">openSUSE</span></span> |<span data-ttu-id="84bad-142">13.2</span><span class="sxs-lookup"><span data-stu-id="84bad-142">13.2</span></span> |<span data-ttu-id="84bad-143">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-143">latest</span></span> |
| <span data-ttu-id="84bad-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="84bad-144">RHEL</span></span> |<span data-ttu-id="84bad-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="84bad-145">Red Hat</span></span> |<span data-ttu-id="84bad-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="84bad-146">RHEL</span></span> |<span data-ttu-id="84bad-147">7.2</span><span class="sxs-lookup"><span data-stu-id="84bad-147">7.2</span></span> |<span data-ttu-id="84bad-148">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-148">latest</span></span> |
| <span data-ttu-id="84bad-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="84bad-149">UbuntuLTS</span></span> |<span data-ttu-id="84bad-150">Canonical</span><span class="sxs-lookup"><span data-stu-id="84bad-150">Canonical</span></span> |<span data-ttu-id="84bad-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="84bad-151">Ubuntu Server</span></span> |<span data-ttu-id="84bad-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="84bad-152">14.04.4-LTS</span></span> |<span data-ttu-id="84bad-153">最新</span><span class="sxs-lookup"><span data-stu-id="84bad-153">latest</span></span> |

<span data-ttu-id="84bad-154">以下範例使用 **ImageURN** 選項 (`-Q`) 的 `UbuntuLTS` 別名來部署 Ubuntu 14.04.4 LTS Server。</span><span class="sxs-lookup"><span data-stu-id="84bad-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="84bad-155">先前的 `quick-create` 範例只呼叫 `-M` 旗標來識別要上傳的 SSH 公開金鑰，且同時停用 SSH 密碼，因此系統會提示您輸入下列引數：</span><span class="sxs-lookup"><span data-stu-id="84bad-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="84bad-156">資源群組名稱 (任何字串一般都適用於您的第一個 Azure 資源群組)</span><span class="sxs-lookup"><span data-stu-id="84bad-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="84bad-157">VM 名稱</span><span class="sxs-lookup"><span data-stu-id="84bad-157">VM name</span></span>
* <span data-ttu-id="84bad-158">位置 (`westus` 或 `westeurope` 都是不錯的預設值)</span><span class="sxs-lookup"><span data-stu-id="84bad-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="84bad-159">Linux (讓 Azure 知道您要的作業系統)</span><span class="sxs-lookup"><span data-stu-id="84bad-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="84bad-160">username</span><span class="sxs-lookup"><span data-stu-id="84bad-160">username</span></span>

<span data-ttu-id="84bad-161">下列範例會指定所有值，因此不會有進一步的提示。</span><span class="sxs-lookup"><span data-stu-id="84bad-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="84bad-162">只要您有 ssh-rsa 格式公開金鑰檔案的 `~/.ssh/id_rsa.pub`，它就會如預期運作：</span><span class="sxs-lookup"><span data-stu-id="84bad-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="84bad-163">輸出應該看起來像下列的輸出區塊：</span><span class="sxs-lookup"><span data-stu-id="84bad-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="84bad-164">登入新的 VM</span><span class="sxs-lookup"><span data-stu-id="84bad-164">Log in to the new VM</span></span>
<span data-ttu-id="84bad-165">使用輸出中所列的公用 IP 位址登入您的 VM。</span><span class="sxs-lookup"><span data-stu-id="84bad-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="84bad-166">您也可以使用其中列出的完整網域名稱 (FQDN)：</span><span class="sxs-lookup"><span data-stu-id="84bad-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="84bad-167">登入程序應該類似下列輸出區塊：</span><span class="sxs-lookup"><span data-stu-id="84bad-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="84bad-168">後續步驟</span><span class="sxs-lookup"><span data-stu-id="84bad-168">Next steps</span></span>
<span data-ttu-id="84bad-169">`azure vm quick-create` 命令是快速部署 VM 的方法，讓您可以登入 bash 殼層並開始使用。</span><span class="sxs-lookup"><span data-stu-id="84bad-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="84bad-170">不過，使用 `vm quick-create` 不會提供您進一步的控制權，也無法讓您能夠建立更複雜的環境。</span><span class="sxs-lookup"><span data-stu-id="84bad-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="84bad-171">若要部署為您的基礎結構自訂的 Linux VM，您可以依照下列任一篇文章執行：</span><span class="sxs-lookup"><span data-stu-id="84bad-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="84bad-172">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="84bad-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="84bad-173">使用範本在 Azure 上建立 SSH 保護的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="84bad-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="84bad-174">您也可以[搭配使用 `docker-machine` Azure 驅動程式與各種命令以快速建立當作 Docker 主機的 Linux VM](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="84bad-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
