---
title: "在 Azure 中建立 Linux VM 的不同方式 | Microsoft Azure"
description: "了解在 Azure 上建立 Linux 虛擬機器的不同方式，包含每種方法的工具和教學課程連結。"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: b2f93579eb1c7a69d0dbd1b0ef112aed9b2168c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-linux-vm"></a><span data-ttu-id="f9e6b-103">建立 Linux VM 的不同方式</span><span class="sxs-lookup"><span data-stu-id="f9e6b-103">Different ways to create a Linux VM</span></span>
<span data-ttu-id="f9e6b-104">您在 Azure 中可選擇使用您習慣的工具和工作流程來建立 Linux 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-104">You have the flexibility in Azure to create a Linux virtual machine (VM) using tools and workflows comfortable to you.</span></span> <span data-ttu-id="f9e6b-105">本文摘要說明這些差異以及建立 Linux VM 的範例，包括 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-105">This article summarizes these differences and examples for creating your Linux VMs, including the Azure CLI 2.0.</span></span> <span data-ttu-id="f9e6b-106">您也可以檢視建立選項，包括 [Azure CLI 1.0](creation-choices-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-106">You can also view creation choices including the [Azure CLI 1.0](creation-choices-nodejs.md).</span></span>

<span data-ttu-id="f9e6b-107">[Azure CLI 2.0](/cli/azure/install-az-cli2) 可透過 npm 套件、散發版本提供的套件或 Docker 容器，在各個平台上提供使用。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-107">The [Azure CLI 2.0](/cli/azure/install-az-cli2) is available across platforms via an npm package, distro-provided packages, or Docker container.</span></span> <span data-ttu-id="f9e6b-108">安裝最適合環境的組建，並使用 [az login](/cli/azure/#login) 登入 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="f9e6b-108">Install the most appropriate build for your environment and log in to an Azure account using [az login](/cli/azure/#login)</span></span>

* [<span data-ttu-id="f9e6b-109">使用 Azure CLI 2.0 來建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9e6b-109">Create a Linux VM with the Azure CLI 2.0</span></span>](quick-create-cli.md)
  
  * <span data-ttu-id="f9e6b-110">使用名為 myResourceGroup 的 [az group create](/cli/azure/group#create) 來建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-110">Create a resource group with [az group create](/cli/azure/group#create) named *myResourceGroup*:</span></span> 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * <span data-ttu-id="f9e6b-111">使用最新的 UbuntuLTS 映像，透過名為 myVM 的 [az vm create](/cli/azure/vm#create) 來建立 VM，如果 ~/.ssh 中還沒有 SSH 金鑰，則請產生 SSH 金鑰：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-111">Create a VM with [az vm create](/cli/azure/vm#create) named *myVM* using the latest *UbuntuLTS* image and generate SSH keys if they do not already exist in *~/.ssh*:</span></span>

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [<span data-ttu-id="f9e6b-112">使用 Azure 範本建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9e6b-112">Create a Linux VM with an Azure template</span></span>](create-ssh-secured-vm-from-template.md)
  
  * <span data-ttu-id="f9e6b-113">下列範例使用 [az group deployment create](/cli/azure/group/deployment#create)，從儲存在 GitHub 上的範本建立 VM︰</span><span class="sxs-lookup"><span data-stu-id="f9e6b-113">The following example uses [az group deployment create](/cli/azure/group/deployment#create) to create a VM from a template stored on GitHub:</span></span>
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [<span data-ttu-id="f9e6b-114">建立 Linux VM，並使用 cloud-init 進行自訂</span><span class="sxs-lookup"><span data-stu-id="f9e6b-114">Create a Linux VM and customize with cloud-init</span></span>](tutorial-automate-vm-deployment.md)

* [<span data-ttu-id="f9e6b-115">在多個 Linux VM 上建立負載平衡和高可用性的應用程式</span><span class="sxs-lookup"><span data-stu-id="f9e6b-115">Create a load balanced and highly available application on multiple Linux VMs</span></span>](tutorial-load-balancer.md)


## <a name="azure-portal"></a><span data-ttu-id="f9e6b-116">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f9e6b-116">Azure portal</span></span>
<span data-ttu-id="f9e6b-117">[Azure 入口網站](https://portal.azure.com) 可讓您快速建立 VM，因為您的系統不需安裝任何項目。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-117">The [Azure portal](https://portal.azure.com) allows you to quickly create a VM since there is nothing to install on your system.</span></span> <span data-ttu-id="f9e6b-118">使用 Azure 入口網站來建立 VM：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-118">Use the Azure portal to create the VM:</span></span>

* [<span data-ttu-id="f9e6b-119">使用 Azure 入口網站建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f9e6b-119">Create a Linux VM using the Azure portal</span></span>](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a><span data-ttu-id="f9e6b-120">作業系統和映像選項</span><span class="sxs-lookup"><span data-stu-id="f9e6b-120">Operating system and image choices</span></span>
<span data-ttu-id="f9e6b-121">建立 VM 時，根據您想要執行的作業系統來選擇映像。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-121">When creating a VM, you choose an image based on the operating system you want to run.</span></span> <span data-ttu-id="f9e6b-122">Azure 與其合作夥伴提供許多映像，其中有些包括已預先安裝的應用程式和工具。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-122">Azure and its partners offer many images, some of which include applications and tools pre-installed.</span></span> <span data-ttu-id="f9e6b-123">或者，上傳您自己的其中一個映像 (請參閱 [下一節](#use-your-own-image))。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-123">Or, upload one of your own images (see [the following section](#use-your-own-image)).</span></span>

### <a name="azure-images"></a><span data-ttu-id="f9e6b-124">Azure 映像</span><span class="sxs-lookup"><span data-stu-id="f9e6b-124">Azure images</span></span>
<span data-ttu-id="f9e6b-125">使用 [az vm image](/cli/azure/vm/image) 命令，依發佈者、散發版本和組建來查看可用的映像。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-125">Use the [az vm image](/cli/azure/vm/image) commands to see what's available by publisher, distro release, and builds.</span></span>

<span data-ttu-id="f9e6b-126">列出可用的發佈者：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-126">List available publishers:</span></span>

```azurecli
az vm image list-publishers --location eastus
```

<span data-ttu-id="f9e6b-127">列出特定發佈者的可用產品 (提供項目)︰</span><span class="sxs-lookup"><span data-stu-id="f9e6b-127">List available products (offers) for a given publisher:</span></span>

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

<span data-ttu-id="f9e6b-128">清單特定提供項目的可用 SKU (散發版本)︰</span><span class="sxs-lookup"><span data-stu-id="f9e6b-128">List available SKUs (distro releases) of a given offer:</span></span>

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

<span data-ttu-id="f9e6b-129">列出特定版本的所有可用映像︰</span><span class="sxs-lookup"><span data-stu-id="f9e6b-129">List all available images for a given release:</span></span>

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

<span data-ttu-id="f9e6b-130">如需有關瀏覽和使用可用映像的更多範例，請參閱 [使用 Azure CLI 瀏覽和選取 Azure 虛擬機器映像](cli-ps-findimage.md)。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-130">For more examples on browsing and using available images, see [Navigate and select Azure virtual machine images with the Azure CLI](cli-ps-findimage.md).</span></span>

<span data-ttu-id="f9e6b-131">[az vm create](/cli/azure/vm#create) 命令有一些別名可用來快速存取更常見的散發版本及其最新版本。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-131">The [az vm create](/cli/azure/vm#create) command has aliases you can use to quickly access the more common distros and their latest releases.</span></span> <span data-ttu-id="f9e6b-132">使用別名通常比每次建立 VM 時指定發佈者、提供項目、SKU 和版本還要快速：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-132">Using aliases is often quicker than specifying the publisher, offer, SKU, and version each time you create a VM:</span></span>

| <span data-ttu-id="f9e6b-133">Alias</span><span class="sxs-lookup"><span data-stu-id="f9e6b-133">Alias</span></span> | <span data-ttu-id="f9e6b-134">發佈者</span><span class="sxs-lookup"><span data-stu-id="f9e6b-134">Publisher</span></span> | <span data-ttu-id="f9e6b-135">提供項目</span><span class="sxs-lookup"><span data-stu-id="f9e6b-135">Offer</span></span> | <span data-ttu-id="f9e6b-136">SKU</span><span class="sxs-lookup"><span data-stu-id="f9e6b-136">SKU</span></span> | <span data-ttu-id="f9e6b-137">版本</span><span class="sxs-lookup"><span data-stu-id="f9e6b-137">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="f9e6b-138">CentOS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-138">CentOS</span></span> |<span data-ttu-id="f9e6b-139">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="f9e6b-139">OpenLogic</span></span> |<span data-ttu-id="f9e6b-140">Centos</span><span class="sxs-lookup"><span data-stu-id="f9e6b-140">Centos</span></span> |<span data-ttu-id="f9e6b-141">7.2</span><span class="sxs-lookup"><span data-stu-id="f9e6b-141">7.2</span></span> |<span data-ttu-id="f9e6b-142">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-142">latest</span></span> |
| <span data-ttu-id="f9e6b-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-143">CoreOS</span></span> |<span data-ttu-id="f9e6b-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-144">CoreOS</span></span> |<span data-ttu-id="f9e6b-145">CoreOS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-145">CoreOS</span></span> |<span data-ttu-id="f9e6b-146">Stable</span><span class="sxs-lookup"><span data-stu-id="f9e6b-146">Stable</span></span> |<span data-ttu-id="f9e6b-147">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-147">latest</span></span> |
| <span data-ttu-id="f9e6b-148">Debian</span><span class="sxs-lookup"><span data-stu-id="f9e6b-148">Debian</span></span> |<span data-ttu-id="f9e6b-149">credativ</span><span class="sxs-lookup"><span data-stu-id="f9e6b-149">credativ</span></span> |<span data-ttu-id="f9e6b-150">Debian</span><span class="sxs-lookup"><span data-stu-id="f9e6b-150">Debian</span></span> |<span data-ttu-id="f9e6b-151">8</span><span class="sxs-lookup"><span data-stu-id="f9e6b-151">8</span></span> |<span data-ttu-id="f9e6b-152">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-152">latest</span></span> |
| <span data-ttu-id="f9e6b-153">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f9e6b-153">openSUSE</span></span> |<span data-ttu-id="f9e6b-154">SUSE</span><span class="sxs-lookup"><span data-stu-id="f9e6b-154">SUSE</span></span> |<span data-ttu-id="f9e6b-155">openSUSE</span><span class="sxs-lookup"><span data-stu-id="f9e6b-155">openSUSE</span></span> |<span data-ttu-id="f9e6b-156">13.2</span><span class="sxs-lookup"><span data-stu-id="f9e6b-156">13.2</span></span> |<span data-ttu-id="f9e6b-157">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-157">latest</span></span> |
| <span data-ttu-id="f9e6b-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="f9e6b-158">RHEL</span></span> |<span data-ttu-id="f9e6b-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="f9e6b-159">Redhat</span></span> |<span data-ttu-id="f9e6b-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="f9e6b-160">RHEL</span></span> |<span data-ttu-id="f9e6b-161">7.2</span><span class="sxs-lookup"><span data-stu-id="f9e6b-161">7.2</span></span> |<span data-ttu-id="f9e6b-162">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-162">latest</span></span> |
| <span data-ttu-id="f9e6b-163">SLES</span><span class="sxs-lookup"><span data-stu-id="f9e6b-163">SLES</span></span> |<span data-ttu-id="f9e6b-164">SLES</span><span class="sxs-lookup"><span data-stu-id="f9e6b-164">SLES</span></span> |<span data-ttu-id="f9e6b-165">SLES</span><span class="sxs-lookup"><span data-stu-id="f9e6b-165">SLES</span></span> |<span data-ttu-id="f9e6b-166">12-SP1</span><span class="sxs-lookup"><span data-stu-id="f9e6b-166">12-SP1</span></span> |<span data-ttu-id="f9e6b-167">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-167">latest</span></span> |
| <span data-ttu-id="f9e6b-168">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-168">UbuntuLTS</span></span> |<span data-ttu-id="f9e6b-169">Canonical</span><span class="sxs-lookup"><span data-stu-id="f9e6b-169">Canonical</span></span> |<span data-ttu-id="f9e6b-170">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="f9e6b-170">UbuntuServer</span></span> |<span data-ttu-id="f9e6b-171">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="f9e6b-171">14.04.4-LTS</span></span> |<span data-ttu-id="f9e6b-172">最新</span><span class="sxs-lookup"><span data-stu-id="f9e6b-172">latest</span></span> |

### <a name="use-your-own-image"></a><span data-ttu-id="f9e6b-173">使用您自己的映像</span><span class="sxs-lookup"><span data-stu-id="f9e6b-173">Use your own image</span></span>
<span data-ttu-id="f9e6b-174">如果您需要特定的自訂，可以擷取該 VM，根據現有的 Azure VM 使用映像。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-174">If you require specific customizations, you can use an image based on an existing Azure VM by capturing that VM.</span></span> <span data-ttu-id="f9e6b-175">也可以上傳在內部部署建立的映像。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-175">You can also upload an image created on-premises.</span></span> <span data-ttu-id="f9e6b-176">如需有關支援的散發版本以及如何使用自己的映像的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="f9e6b-176">For more information on supported distros and how to use your own images, see the following articles:</span></span>

* [<span data-ttu-id="f9e6b-177">Azure 背書的散發套件</span><span class="sxs-lookup"><span data-stu-id="f9e6b-177">Azure endorsed distributions</span></span>](endorsed-distros.md)
* [<span data-ttu-id="f9e6b-178">非背書散發套件的資訊</span><span class="sxs-lookup"><span data-stu-id="f9e6b-178">Information for non-endorsed distributions</span></span>](create-upload-generic.md)
* <span data-ttu-id="f9e6b-179">[如何從現有的 Azure VM 建立映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-179">[How to create an image from an existing Azure VM](tutorial-custom-images.md).</span></span>
  
  * <span data-ttu-id="f9e6b-180">可從現有 Azure VM 建立映像的快速入門範例命令︰</span><span class="sxs-lookup"><span data-stu-id="f9e6b-180">Quick-start example commands to create an image from an existing Azure VM:</span></span>
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a><span data-ttu-id="f9e6b-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f9e6b-181">Next steps</span></span>
* <span data-ttu-id="f9e6b-182">透過 [CLI](quick-create-cli.md)、[入口網站](quick-create-portal.md)或使用 [Azure Resource Manager 範本](../windows/cli-deploy-templates.md)建立 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-182">Create a Linux VM with the [CLI](quick-create-cli.md), from the [portal](quick-create-portal.md), or using an [Azure Resource Manager template](../windows/cli-deploy-templates.md).</span></span>
* <span data-ttu-id="f9e6b-183">建立 Linux VM 之後，[深入了解 Azure 磁碟與儲存體](tutorial-manage-disks.md)。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-183">After creating a Linux VM, [learn about Azure disks and storage](tutorial-manage-disks.md).</span></span>
* <span data-ttu-id="f9e6b-184">[重設密碼或 SSH 金鑰及管理使用者](using-vmaccess-extension.md)的快速步驟。</span><span class="sxs-lookup"><span data-stu-id="f9e6b-184">Quick steps to [reset a password or SSH keys and manage users](using-vmaccess-extension.md).</span></span>
