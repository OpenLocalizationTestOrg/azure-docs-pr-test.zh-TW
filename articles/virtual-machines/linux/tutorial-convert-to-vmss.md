---
title: "將 Azure VM 轉換為擴展集 | Microsoft Docs"
description: "使用 Azure CLI 建立及部署 Linux Azure 虛擬機器擴展集。"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 04/05/2017
ms.author: adegeo
ms.openlocfilehash: 8d3376d2791b1349298db618d475ce5573083702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="convert-an-existing-azure-virtual-machine-to-a-scale-set"></a><span data-ttu-id="7091b-103">將現有 Azure 虛擬機器轉換為擴展集</span><span class="sxs-lookup"><span data-stu-id="7091b-103">Convert an existing Azure virtual machine to a scale set</span></span>

<span data-ttu-id="7091b-104">本教學課程說明如何使用 Azure CLI 2.0 將虛擬機器轉換為虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="7091b-104">This tutorial shows you how to use Azure CLI 2.0 to convert a virtual machine to a virtual machine scale set.</span></span> <span data-ttu-id="7091b-105">您也會了解如何自動化擴展集中的虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="7091b-105">You also learn how to automate the configuration of the virtual machines in the scale set.</span></span> <span data-ttu-id="7091b-106">如需有關如何安裝 Azure CLI 2.0 的詳細資訊，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7091b-106">For more information on how to install Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="7091b-107">如需調整集的詳細資訊，請參閱 [虛擬機器調整集](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7091b-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-the-vm"></a><span data-ttu-id="7091b-108">步驟 1- 取消佈建 VM</span><span class="sxs-lookup"><span data-stu-id="7091b-108">Step 1 - Deprovision the VM</span></span>

<span data-ttu-id="7091b-109">使用 SSH 連線到 VM。</span><span class="sxs-lookup"><span data-stu-id="7091b-109">Use SSH to connect to the VM.</span></span>

<span data-ttu-id="7091b-110">使用 Azure VM 代理程式來取消佈建 VM，以刪除相關檔案和資料。</span><span class="sxs-lookup"><span data-stu-id="7091b-110">Deprovision the VM using the Azure VM agent to delete files and data.</span></span> <span data-ttu-id="7091b-111">如需取消佈建的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="7091b-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-the-vm"></a><span data-ttu-id="7091b-112">步驟 2 - 擷取 VM 的映像</span><span class="sxs-lookup"><span data-stu-id="7091b-112">Step 2 - Capture an image of the VM</span></span>

<span data-ttu-id="7091b-113">如需擷取的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="7091b-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="7091b-114">使用 [az vm deallocate](/cli/azure/vm#deallocate) 解除配置 VM：</span><span class="sxs-lookup"><span data-stu-id="7091b-114">Deallocate the VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7091b-115">使用 [az vm generalize](/cli/azure/vm#generalize) 將 VM 一般化：</span><span class="sxs-lookup"><span data-stu-id="7091b-115">Generalize the VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="7091b-116">使用 [az image create](/cli/azure/image#create) 從 VM 資源建立映像：</span><span class="sxs-lookup"><span data-stu-id="7091b-116">Create an image from the VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-the-scale-set"></a><span data-ttu-id="7091b-117">步驟 3 - 建立擴展集</span><span class="sxs-lookup"><span data-stu-id="7091b-117">Step 3 - Create the scale set</span></span>

<span data-ttu-id="7091b-118">取得映像的 **ID**。</span><span class="sxs-lookup"><span data-stu-id="7091b-118">Get the **id** of the image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="7091b-119">使用 [az vmss create](/cli/azure/vmss#create) 從映像資源建立 VM：</span><span class="sxs-lookup"><span data-stu-id="7091b-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="7091b-120">此命令也會連結 10 GB 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7091b-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="7091b-121">請注意，根據選擇的 VM 大小 (我們使用 **Standard_DS1_v2**)，允許的資料磁碟數目也會不同。</span><span class="sxs-lookup"><span data-stu-id="7091b-121">Keep in mind that depending on the VM size chosen (we used **Standard_DS1_v2**), the number of data disks allowed is different.</span></span> <span data-ttu-id="7091b-122">如需詳細資訊，請檢閱[虛擬機器大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="7091b-122">For more information, review the [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="7091b-123">當擴展集完成之後，與它連線。</span><span class="sxs-lookup"><span data-stu-id="7091b-123">Once the scale set finishes, connect to it.</span></span> <span data-ttu-id="7091b-124">使用 [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info)取得 SSH 之執行個體的 IP 位址清單：</span><span class="sxs-lookup"><span data-stu-id="7091b-124">Get a list of IP addresses for the instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="7091b-125">您現在可以連線到虛擬機器執行個體，以初始化資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7091b-125">Now you can connect to the virtual machine instance to initialize the data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-the-data-disk"></a><span data-ttu-id="7091b-126">步驟 4 - 初始化資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7091b-126">Step 4 - Initialize the data disk</span></span>

<span data-ttu-id="7091b-127">連線到虛擬機器時，使用 `fdisk` 對磁碟進行磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="7091b-127">While connected to the virtual machine, partition the disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="7091b-128">使用 `mkfs` 命令將檔案系統寫入至磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="7091b-128">Write a file system to the partition with the `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="7091b-129">掛接新磁碟，使其可在作業系統中供存取︰</span><span class="sxs-lookup"><span data-stu-id="7091b-129">Mount the new disk so that it is accessible in the operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="7091b-130">現在可以透過 datadrive 掛接點存取磁碟，掛接點可以使用 `ls /datadrive/` 來驗證。</span><span class="sxs-lookup"><span data-stu-id="7091b-130">The disk can now be accesses through the datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="7091b-131">結束 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="7091b-131">End the SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="7091b-132">步驟 5 - 設定防火牆</span><span class="sxs-lookup"><span data-stu-id="7091b-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="7091b-133">透過防火牆對擴展集所裝載的 Web 伺服器製造一個漏洞。</span><span class="sxs-lookup"><span data-stu-id="7091b-133">Punch a hole through the firewall to the webserver hosted by the scale set.</span></span> <span data-ttu-id="7091b-134">擴展集建立時，也會建立負載平衡器，您使用它以 **SSH** 到個別虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7091b-134">When the scale set was created, a load balancer was also created, and you used it **SSH** to the individual virtual machines.</span></span> <span data-ttu-id="7091b-135">若要開啟連接埠，您需要兩項資訊，可以使用 Azure CLI 取得。</span><span class="sxs-lookup"><span data-stu-id="7091b-135">To open a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="7091b-136">**前端 IP 位址集區**</span><span class="sxs-lookup"><span data-stu-id="7091b-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="7091b-137">**後端 IP 位址集區**</span><span class="sxs-lookup"><span data-stu-id="7091b-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="7091b-138">使用這兩個名稱，您可以開啟連接埠 **80**。</span><span class="sxs-lookup"><span data-stu-id="7091b-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="7091b-139">步驟 6 - 自動化組態</span><span class="sxs-lookup"><span data-stu-id="7091b-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="7091b-140">必須在每個虛擬機器執行個體上設定資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7091b-140">The data disk needs to be configured on each virtual machine instance.</span></span> <span data-ttu-id="7091b-141">我們可以使用 **CustomScript** 擴充功能來自動化虛擬機器的組態。</span><span class="sxs-lookup"><span data-stu-id="7091b-141">We can automate the configuration of the virtual machine with the **CustomScript** extension.</span></span>

<span data-ttu-id="7091b-142">首先，建立 *.sh* 指令碼，其中包含磁碟格式命令。</span><span class="sxs-lookup"><span data-stu-id="7091b-142">First, create a *.sh* script that includes the disk format commands.</span></span>

```sh
#!/bin/bash

# Setup the data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="7091b-143">接下來，將該指令碼檔案上傳到 **CustomScript** 擴充功能可以存取它的位置。</span><span class="sxs-lookup"><span data-stu-id="7091b-143">Next, upload that script file to where the **CustomScript** extension can access it.</span></span> <span data-ttu-id="7091b-144">複本可以在[這裡](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)取得。</span><span class="sxs-lookup"><span data-stu-id="7091b-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="7091b-145">建立名為 **settings.json** 的本機檔案，並且在其中放置下列 JSON 區塊。</span><span class="sxs-lookup"><span data-stu-id="7091b-145">Create a local file named **settings.json** and put the following JSON block in it.</span></span> <span data-ttu-id="7091b-146">`flieUris` 屬性應該設為指令碼檔案上傳的位置。</span><span class="sxs-lookup"><span data-stu-id="7091b-146">The `flieUris` property should be set to where your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="7091b-147">使用 **CustomScript** 擴充功能將此命令部署至您的擴展集，參考我們剛剛建立的 **settings.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="7091b-147">Deploy this command to your scale set with the **CustomScript** extension, referencing the **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="7091b-148">此擴充功能會在所有目前執行個體和稍後藉由調整所建立的任何執行個體上自動執行。</span><span class="sxs-lookup"><span data-stu-id="7091b-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="7091b-149">步驟 7 - 設定自動調整規則</span><span class="sxs-lookup"><span data-stu-id="7091b-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="7091b-150">目前，Azure CLI 中無法設定自動調整規則。</span><span class="sxs-lookup"><span data-stu-id="7091b-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="7091b-151">使用 [Azure 入口網站](https://portal.azure.com)以設定自動調整。</span><span class="sxs-lookup"><span data-stu-id="7091b-151">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="7091b-152">步驟 8 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="7091b-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="7091b-153">在擴展集生命週期中，您可能需要執行一或多個管理工作。</span><span class="sxs-lookup"><span data-stu-id="7091b-153">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="7091b-154">此外，您可能想要建立會自動化各種生命週期工作的指令碼，Azure CLI 提供快速的方式來執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="7091b-154">Additionally, you may want to create scripts that automate various lifecycle-tasks, and the Azure CLI provides a quick way to do those tasks.</span></span> <span data-ttu-id="7091b-155">以下是一些常見工作。</span><span class="sxs-lookup"><span data-stu-id="7091b-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="7091b-156">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="7091b-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="7091b-157">設定執行個體計數 (手動調整)</span><span class="sxs-lookup"><span data-stu-id="7091b-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="7091b-158">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="7091b-158">Delete resource group</span></span>

<span data-ttu-id="7091b-159">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7091b-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7091b-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7091b-160">Next steps</span></span>
<span data-ttu-id="7091b-161">若要深入了解本教學課程中介紹的虛擬機器擴展集功能，請參閱下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="7091b-161">To learn more about some of the virtual machine scale set features introduced in this tutorial, see the following information:</span></span>

- [<span data-ttu-id="7091b-162">Azure 虛擬機器擴展集概觀</span><span class="sxs-lookup"><span data-stu-id="7091b-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="7091b-163">Azure 負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="7091b-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="7091b-164">使用網路安全性群組來控制網路流量</span><span class="sxs-lookup"><span data-stu-id="7091b-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)