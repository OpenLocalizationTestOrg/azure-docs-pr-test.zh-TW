---
title: "使用 Azure CLI 1.0 建立 Linux VM 的不同方式 | Microsoft Docs"
description: "了解在 Azure 上建立 Linux 虛擬機器的不同方式，包含每種方法的工具和教學課程連結。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="3609b-103">在 Azure 中建立 Linux 虛擬機器的不同方式</span><span class="sxs-lookup"><span data-stu-id="3609b-103">Different ways to create a Linux virtual machine in Azure</span></span>
<span data-ttu-id="3609b-104">您在 Azure 中可選擇使用您習慣的工具和工作流程來建立 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="3609b-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="3609b-105">本文摘要說明這些差異以及建立 Linux VM 的範例。</span><span class="sxs-lookup"><span data-stu-id="3609b-105">This article summarizes these differences and examples for creating your Linux VMs.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="3609b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3609b-106">Azure CLI</span></span>
<span data-ttu-id="3609b-107">您可以在 Azure 中使用下列其中一個 CLI 版本建立 VM︰</span><span class="sxs-lookup"><span data-stu-id="3609b-107">You can create VMs in Azure using one of the following CLI versions:</span></span>

- <span data-ttu-id="3609b-108">Azure CLI 1.0 - 適用於傳統和資源管理部署模型 (本文) 的 CLI</span><span class="sxs-lookup"><span data-stu-id="3609b-108">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="3609b-109">[Azure CLI 2.0](../windows/creation-choices.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="3609b-109">[Azure CLI 2.0](../windows/creation-choices.md) - our next generation CLI for the resource management deployment model</span></span>

<span data-ttu-id="3609b-110">Azure CLI 1.0 可透過 npm 套件、散發版本提供的套件或 Docker 容器，跨平台適用。</span><span class="sxs-lookup"><span data-stu-id="3609b-110">The Azure CLI 1.0 is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="3609b-111">您可以深入了解 [如何安裝和設定 Azure CLI](../../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="3609b-111">You can read more about [how to install and configure the Azure CLI](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="3609b-112">下列教學課程提供有關使用 Azure CLI 1.0 的範例。</span><span class="sxs-lookup"><span data-stu-id="3609b-112">The following tutorials provide examples on using the Azure CLI 1.0.</span></span> <span data-ttu-id="3609b-113">如需以下 CLI 快速入門命令的詳細資訊，請閱讀每篇文章：</span><span class="sxs-lookup"><span data-stu-id="3609b-113">Read each article for more details on the CLI quick-start commands shown:</span></span>

* [<span data-ttu-id="3609b-114">從 Azure CLI 建立用於開發和測試的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="3609b-114">Create a Linux VM from the Azure CLI for dev and test</span></span>](quick-create-cli-nodejs.md)
  
  * <span data-ttu-id="3609b-115">下列範例使用名為 azure_id_rsa.pub 的公開金鑰建立 CoreOS VM：</span><span class="sxs-lookup"><span data-stu-id="3609b-115">The following example creates a CoreOS VM using a public key named *azure_id_rsa.pub*:</span></span>
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [<span data-ttu-id="3609b-116">使用 Azure 範本建立受保護的 Linux VM</span><span class="sxs-lookup"><span data-stu-id="3609b-116">Create a secured Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="3609b-117">下列範例使用 GitHub 上儲存的範本來建立 VM：</span><span class="sxs-lookup"><span data-stu-id="3609b-117">The following example creates a VM using a template stored on GitHub:</span></span>
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [<span data-ttu-id="3609b-118">使用 Azure CLI 建立完整的 Linux 環境</span><span class="sxs-lookup"><span data-stu-id="3609b-118">Create a complete Linux environment using the Azure CLI</span></span>](create-cli-complete-nodejs.md)
  
  * <span data-ttu-id="3609b-119">包含在可用性設定組中建立負載平衡器和多個 VM。</span><span class="sxs-lookup"><span data-stu-id="3609b-119">Includes creating a load balancer and multiple VMs in an availability set.</span></span>
* [<span data-ttu-id="3609b-120">在 Linux VM 中新增磁碟</span><span class="sxs-lookup"><span data-stu-id="3609b-120">Add a disk to a Linux VM</span></span>](add-disk.md)
  
  * <span data-ttu-id="3609b-121">下列範例會將 5 Gb 磁碟新增至名為 myVM 的現有 VM：</span><span class="sxs-lookup"><span data-stu-id="3609b-121">The following example adds a *5* Gb disk to an existing VM named *myVM*:</span></span>
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a><span data-ttu-id="3609b-122">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="3609b-122">Azure portal</span></span>
<span data-ttu-id="3609b-123">[Azure 入口網站](https://portal.azure.com) 可讓您快速建立 VM，因為您的系統不需安裝任何項目。</span><span class="sxs-lookup"><span data-stu-id="3609b-123">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="3609b-124">使用 Azure 入口網站來建立 VM：</span><span class="sxs-lookup"><span data-stu-id="3609b-124">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="3609b-125">使用 Azure 入口網站建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="3609b-125">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a><span data-ttu-id="3609b-126">作業系統和映像選項</span><span class="sxs-lookup"><span data-stu-id="3609b-126">Operating system and image choices</span></span>
<span data-ttu-id="3609b-127">建立 VM 時，根據您想要執行的作業系統來選擇映像。</span><span class="sxs-lookup"><span data-stu-id="3609b-127">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="3609b-128">Azure 與其合作夥伴提供許多映像，其中有些包括已預先安裝的應用程式和工具。</span><span class="sxs-lookup"><span data-stu-id="3609b-128">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="3609b-129">或者，上傳您自己的其中一個映像 (請參閱 [下一節](#use-your-own-image))。</span><span class="sxs-lookup"><span data-stu-id="3609b-129">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="3609b-130">Azure 映像</span><span class="sxs-lookup"><span data-stu-id="3609b-130">Azure images</span></span>
<span data-ttu-id="3609b-131">使用 `azure vm image` CLI 命令，查看可用的發佈者、散發版本和組建。</span><span class="sxs-lookup"><span data-stu-id="3609b-131">Use the `azure vm image` CLI commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="3609b-132">列出可用的發佈者，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3609b-132">List available publishers as follows:</span></span>

```azurecli
azure vm image list-publishers --location eastus
```

<span data-ttu-id="3609b-133">列出特定發佈者的可用產品 (提供項目)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3609b-133">List available products (offers) for a given publisher as follows:</span></span>

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

<span data-ttu-id="3609b-134">列出特定提供項目的可用 SKU (散發版本)，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3609b-134">List available SKUs (distro releases) of a given offer as follows:</span></span>

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

<span data-ttu-id="3609b-135">列出特定版本的所有可用映像，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3609b-135">List all available images for a given release follows:</span></span>

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

<span data-ttu-id="3609b-136">`azure vm quick-create` 和 `azure vm create` 命令有一些別名，您可以用來快速存取更多常見的散發版本及其最新版本。</span><span class="sxs-lookup"><span data-stu-id="3609b-136">The `azure vm quick-create` and `azure vm create` commands have aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="3609b-137">使用別名通常比每次建立 VM 時指定發佈者、提供項目、SKU 和版本還要快速：</span><span class="sxs-lookup"><span data-stu-id="3609b-137">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="3609b-138">Alias</span><span class="sxs-lookup"><span data-stu-id="3609b-138">Alias</span></span> | <span data-ttu-id="3609b-139">發佈者</span><span class="sxs-lookup"><span data-stu-id="3609b-139">Publisher</span></span> | <span data-ttu-id="3609b-140">提供項目</span><span class="sxs-lookup"><span data-stu-id="3609b-140">Offer</span></span> | <span data-ttu-id="3609b-141">SKU</span><span class="sxs-lookup"><span data-stu-id="3609b-141">SKU</span></span> | <span data-ttu-id="3609b-142">版本</span><span class="sxs-lookup"><span data-stu-id="3609b-142">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="3609b-143">CentOS</span><span class="sxs-lookup"><span data-stu-id="3609b-143">CentOS</span></span> |<span data-ttu-id="3609b-144">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="3609b-144">OpenLogic</span></span> |<span data-ttu-id="3609b-145">Centos</span><span class="sxs-lookup"><span data-stu-id="3609b-145">Centos</span></span> |<span data-ttu-id="3609b-146">7.2</span><span class="sxs-lookup"><span data-stu-id="3609b-146">7.2</span></span> |<span data-ttu-id="3609b-147">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-147">latest</span></span> |
| <span data-ttu-id="3609b-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3609b-148">CoreOS</span></span> |<span data-ttu-id="3609b-149">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3609b-149">CoreOS</span></span> |<span data-ttu-id="3609b-150">CoreOS</span><span class="sxs-lookup"><span data-stu-id="3609b-150">CoreOS</span></span> |<span data-ttu-id="3609b-151">Stable</span><span class="sxs-lookup"><span data-stu-id="3609b-151">Stable</span></span> |<span data-ttu-id="3609b-152">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-152">latest</span></span> |
| <span data-ttu-id="3609b-153">Debian</span><span class="sxs-lookup"><span data-stu-id="3609b-153">Debian</span></span> |<span data-ttu-id="3609b-154">credativ</span><span class="sxs-lookup"><span data-stu-id="3609b-154">credativ</span></span> |<span data-ttu-id="3609b-155">Debian</span><span class="sxs-lookup"><span data-stu-id="3609b-155">Debian</span></span> |<span data-ttu-id="3609b-156">8</span><span class="sxs-lookup"><span data-stu-id="3609b-156">8</span></span> |<span data-ttu-id="3609b-157">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-157">latest</span></span> |
| <span data-ttu-id="3609b-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3609b-158">openSUSE</span></span> |<span data-ttu-id="3609b-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="3609b-159">SUSE</span></span> |<span data-ttu-id="3609b-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="3609b-160">openSUSE</span></span> |<span data-ttu-id="3609b-161">13.2</span><span class="sxs-lookup"><span data-stu-id="3609b-161">13.2</span></span> |<span data-ttu-id="3609b-162">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-162">latest</span></span> |
| <span data-ttu-id="3609b-163">RHEL</span><span class="sxs-lookup"><span data-stu-id="3609b-163">RHEL</span></span> |<span data-ttu-id="3609b-164">Redhat</span><span class="sxs-lookup"><span data-stu-id="3609b-164">Redhat</span></span> |<span data-ttu-id="3609b-165">RHEL</span><span class="sxs-lookup"><span data-stu-id="3609b-165">RHEL</span></span> |<span data-ttu-id="3609b-166">7.2</span><span class="sxs-lookup"><span data-stu-id="3609b-166">7.2</span></span> |<span data-ttu-id="3609b-167">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-167">latest</span></span> |
| <span data-ttu-id="3609b-168">SLES</span><span class="sxs-lookup"><span data-stu-id="3609b-168">SLES</span></span> |<span data-ttu-id="3609b-169">SLES</span><span class="sxs-lookup"><span data-stu-id="3609b-169">SLES</span></span> |<span data-ttu-id="3609b-170">SLES</span><span class="sxs-lookup"><span data-stu-id="3609b-170">SLES</span></span> |<span data-ttu-id="3609b-171">12-SP1</span><span class="sxs-lookup"><span data-stu-id="3609b-171">12-SP1</span></span> |<span data-ttu-id="3609b-172">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-172">latest</span></span> |
| <span data-ttu-id="3609b-173">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="3609b-173">UbuntuLTS</span></span> |<span data-ttu-id="3609b-174">Canonical</span><span class="sxs-lookup"><span data-stu-id="3609b-174">Canonical</span></span> |<span data-ttu-id="3609b-175">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="3609b-175">UbuntuServer</span></span> |<span data-ttu-id="3609b-176">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="3609b-176">14.04.4-LTS</span></span> |<span data-ttu-id="3609b-177">最新</span><span class="sxs-lookup"><span data-stu-id="3609b-177">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="3609b-178">使用您自己的映像</span><span class="sxs-lookup"><span data-stu-id="3609b-178">Use your own image</span></span>
<span data-ttu-id="3609b-179">如果您需要特定自訂項目，可以「擷取」  現有的 Azure VM，使用以該 VM 為基礎的映像。</span><span class="sxs-lookup"><span data-stu-id="3609b-179">If you require specific customizations, you can use an image based on an existing Azure VM by *capturing* that VM.</span></span> <span data-ttu-id="3609b-180">也可以上傳在內部部署建立的映像。</span><span class="sxs-lookup"><span data-stu-id="3609b-180">You can also upload an image created on-premises.</span></span> <span data-ttu-id="3609b-181">如需有關支援的散發版本以及如何使用自己的映像的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="3609b-181">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="3609b-182">Azure 背書的散發套件</span><span class="sxs-lookup"><span data-stu-id="3609b-182">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="3609b-183">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="3609b-183">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* [<span data-ttu-id="3609b-184">上傳自訂磁碟映像並從這個映像建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="3609b-184">Upload and create a Linux VM from custom disk image</span></span>](upload-vhd.md)
* <span data-ttu-id="3609b-185">[如何擷取 Linux 虛擬機器以做為 Resource Manager 範本](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="3609b-185">[How to capture a Linux virtual machine as a Resource Manager template](capture-image.md).</span></span>
  
  * <span data-ttu-id="3609b-186">用來擷取現有 VM 的快速入門範例命令：</span><span class="sxs-lookup"><span data-stu-id="3609b-186">Quick-start example commands to capture an existing VM:</span></span>
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a><span data-ttu-id="3609b-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3609b-187">Next steps</span></span>
* <span data-ttu-id="3609b-188">透過[入口網站](quick-create-portal.md)、[CLI](quick-create-cli.md) 或 [Azure Resource Manager 範本](../windows/cli-deploy-templates.md)建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="3609b-188">Create a Linux VM from the [portal](quick-create-portal.md), with the [CLI](quick-create-cli.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="3609b-189">在建立 Linux VM 後， [新增資料磁碟](add-disk.md)。</span><span class="sxs-lookup"><span data-stu-id="3609b-189">After creating a Linux VM, [add a data disk](add-disk.md).</span></span>
* <span data-ttu-id="3609b-190">[重設密碼或 SSH 金鑰及管理使用者](using-vmaccess-extension.md)</span><span class="sxs-lookup"><span data-stu-id="3609b-190">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md)</span></span>

