---
title: "使用 Azure CLI 1.0 建立 Linux VM 的複本 | Microsoft Docs"
description: "了解如何在 Resource Manager 部署模型中，使用 Azure CLI 1.0 建立 Azure Linux 虛擬機器的複本"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="65337-103">使用 Azure CLI 1.0 建立在 Azure 上執行的 Linux 虛擬機器複本</span><span class="sxs-lookup"><span data-stu-id="65337-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="65337-104">本文示範如何使用 Resource Manager 部署模型來建立執行 Linux 的 Azure 虛擬機器 (VM) 複本。</span><span class="sxs-lookup"><span data-stu-id="65337-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="65337-105">首先，您需將作業系統和資料磁碟複製到新容器中，然後設定網路資源並建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="65337-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="65337-106">您也可以[上傳自訂磁碟映像並從這個映像建立 VM](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="65337-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="65337-107">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="65337-107">CLI versions to complete the task</span></span>
<span data-ttu-id="65337-108">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="65337-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="65337-109">Azure CLI 1.0 - 適用於傳統和資源管理部署模型 (本文) 的 CLI</span><span class="sxs-lookup"><span data-stu-id="65337-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="65337-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="65337-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="65337-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="65337-111">Before you begin</span></span>
<span data-ttu-id="65337-112">請先確保符合下列必要條件再開始以下步驟︰</span><span class="sxs-lookup"><span data-stu-id="65337-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="65337-113">您已在電腦上下載及安裝 [Azure CLI](../../cli-install-nodejs.md) 。</span><span class="sxs-lookup"><span data-stu-id="65337-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="65337-114">您也需要現有 Azure Linux VM 的一些相關資訊：</span><span class="sxs-lookup"><span data-stu-id="65337-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="65337-115">來源 VM 資訊</span><span class="sxs-lookup"><span data-stu-id="65337-115">Source VM information</span></span> | <span data-ttu-id="65337-116">從哪裡取得</span><span class="sxs-lookup"><span data-stu-id="65337-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="65337-117">VM 名稱</span><span class="sxs-lookup"><span data-stu-id="65337-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="65337-118">資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="65337-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="65337-119">位置</span><span class="sxs-lookup"><span data-stu-id="65337-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="65337-120">儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="65337-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="65337-121">容器名稱</span><span class="sxs-lookup"><span data-stu-id="65337-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="65337-122">來源 VM VHD 檔案名稱</span><span class="sxs-lookup"><span data-stu-id="65337-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="65337-123">您將需要進行新 VM 的一些相關選擇：   </span><span class="sxs-lookup"><span data-stu-id="65337-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="65337-124">-容器名稱    </span><span class="sxs-lookup"><span data-stu-id="65337-124">-Container name    </span></span><br> <span data-ttu-id="65337-125">-VM 名稱    </span><span class="sxs-lookup"><span data-stu-id="65337-125">-VM name    </span></span><br> <span data-ttu-id="65337-126">-VM 大小    </span><span class="sxs-lookup"><span data-stu-id="65337-126">-VM size    </span></span><br> <span data-ttu-id="65337-127">-vNet 名稱    </span><span class="sxs-lookup"><span data-stu-id="65337-127">-vNet name    </span></span><br> <span data-ttu-id="65337-128">-SubNet 名稱    </span><span class="sxs-lookup"><span data-stu-id="65337-128">-SubNet name    </span></span><br> <span data-ttu-id="65337-129">-IP 名稱    </span><span class="sxs-lookup"><span data-stu-id="65337-129">-IP Name    </span></span><br> <span data-ttu-id="65337-130">-NIC 名稱</span><span class="sxs-lookup"><span data-stu-id="65337-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="65337-131">登入及設定您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="65337-131">Login and set your subscription</span></span>
1. <span data-ttu-id="65337-132">登入 CLI。</span><span class="sxs-lookup"><span data-stu-id="65337-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="65337-133">確定您處於 Resource Manager 模式。</span><span class="sxs-lookup"><span data-stu-id="65337-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="65337-134">設定正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="65337-134">Set the correct subscription.</span></span> <span data-ttu-id="65337-135">您可以使用 'azure account list' 來查看您的所有訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="65337-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="65337-136">停止 VM</span><span class="sxs-lookup"><span data-stu-id="65337-136">Stop the VM</span></span>
<span data-ttu-id="65337-137">將來源 VM 停止並解除配置。</span><span class="sxs-lookup"><span data-stu-id="65337-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="65337-138">您可以使用 'azure vm list' 來取得訂用帳戶中所有 VM 及其資源群組名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="65337-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="65337-139">複製 VHD</span><span class="sxs-lookup"><span data-stu-id="65337-139">Copy the VHD</span></span>
<span data-ttu-id="65337-140">您可以使用 `azure storage blob copy start`將 VHD 從來源儲存體複製到目的地。</span><span class="sxs-lookup"><span data-stu-id="65337-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="65337-141">在此範例中，我們將會把 VHD 複製到相同的儲存體帳戶但不同的容器中。</span><span class="sxs-lookup"><span data-stu-id="65337-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="65337-142">若要將 VHD 複製到相同儲存體帳戶中的另一個容器，請輸入：</span><span class="sxs-lookup"><span data-stu-id="65337-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="65337-143">為新 VM 設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="65337-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="65337-144">為新 VM 設定虛擬網路和 NIC。</span><span class="sxs-lookup"><span data-stu-id="65337-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="65337-145">建立新 VM</span><span class="sxs-lookup"><span data-stu-id="65337-145">Create the new VM</span></span>
<span data-ttu-id="65337-146">您現在可以 [使用 Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) 從已上傳的虛擬磁碟建立 VM，或透過 CLI 藉由輸入下列命令來指定所複製磁碟的 URI 以建立 VM︰</span><span class="sxs-lookup"><span data-stu-id="65337-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="65337-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65337-147">Next steps</span></span>
<span data-ttu-id="65337-148">若要了解如何使用 Azure CLI 來管理新虛擬機器，請參閱 [Azure Resource Manager 的 Azure CLI 命令](../azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="65337-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

