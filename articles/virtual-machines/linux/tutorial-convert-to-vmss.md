---
title: "aaaConvert Azure VM tooa 規模調整集合 |Microsoft 文件"
description: "建立並部署以 hello Azure CLI 設定 Linux 的 Azure 虛擬機器規模。"
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
ms.openlocfilehash: e228282ac4855cef589b8500e74e9d461f9aed84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-an-existing-azure-virtual-machine-tooa-scale-set"></a><span data-ttu-id="f14e3-103">轉換現有的 Azure 虛擬機器 tooa 規模集</span><span class="sxs-lookup"><span data-stu-id="f14e3-103">Convert an existing Azure virtual machine tooa scale set</span></span>

<span data-ttu-id="f14e3-104">本教學課程會示範如何 toouse Azure CLI 2.0 tooconvert 虛擬機器 tooa 虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="f14e3-104">This tutorial shows you how toouse Azure CLI 2.0 tooconvert a virtual machine tooa virtual machine scale set.</span></span> <span data-ttu-id="f14e3-105">您也可以學習如何 tooautomate hello hello hello 小數位數中的虛擬機器的設定。</span><span class="sxs-lookup"><span data-stu-id="f14e3-105">You also learn how tooautomate hello configuration of hello virtual machines in hello scale set.</span></span> <span data-ttu-id="f14e3-106">如需有關如何 tooinstall Azure CLI 2.0，請參閱[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="f14e3-106">For more information on how tooinstall Azure CLI 2.0, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).</span></span> <span data-ttu-id="f14e3-107">如需調整集的詳細資訊，請參閱 [虛擬機器調整集](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f14e3-107">For more information about scale sets, see [Virtual Machine Scale Sets](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span>

## <a name="step-1---deprovision-hello-vm"></a><span data-ttu-id="f14e3-108">步驟 1-取消佈建 VM hello</span><span class="sxs-lookup"><span data-stu-id="f14e3-108">Step 1 - Deprovision hello VM</span></span>

<span data-ttu-id="f14e3-109">使用 SSH tooconnect toohello VM。</span><span class="sxs-lookup"><span data-stu-id="f14e3-109">Use SSH tooconnect toohello VM.</span></span>

<span data-ttu-id="f14e3-110">取消佈建 hello VM 使用 hello Azure VM 代理程式 toodelete 檔案和資料。</span><span class="sxs-lookup"><span data-stu-id="f14e3-110">Deprovision hello VM using hello Azure VM agent toodelete files and data.</span></span> <span data-ttu-id="f14e3-111">如需取消佈建的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="f14e3-111">For a detailed overview of deprovisioning, see [Capture a Linux virtual machine](capture-image.md).</span></span>

```bash
sudo waagent -deprovision+user -force
exit
```

## <a name="step-2---capture-an-image-of-hello-vm"></a><span data-ttu-id="f14e3-112">步驟 2-擷取 hello VM 映像</span><span class="sxs-lookup"><span data-stu-id="f14e3-112">Step 2 - Capture an image of hello VM</span></span>

<span data-ttu-id="f14e3-113">如需擷取的詳細概觀，請參閱[擷取 Linux 虛擬機器](capture-image.md)。</span><span class="sxs-lookup"><span data-stu-id="f14e3-113">For a detailed overview of capturing, see [Capture a Linux virtual machine](capture-image.md).</span></span>

<span data-ttu-id="f14e3-114">解除配置 hello 與 VM [az vm 解除配置](/cli/azure/vm#deallocate):</span><span class="sxs-lookup"><span data-stu-id="f14e3-114">Deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate):</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f14e3-115">一般化 hello 與 VM [az vm 一般化](/cli/azure/vm#generalize):</span><span class="sxs-lookup"><span data-stu-id="f14e3-115">Generalize hello VM with [az vm generalize](/cli/azure/vm#generalize):</span></span>

```azurecli
az vm generalize --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f14e3-116">建立映像從 hello VM 資源[az 映像建立](/cli/azure/image#create):</span><span class="sxs-lookup"><span data-stu-id="f14e3-116">Create an image from hello VM resource with [az image create](/cli/azure/image#create):</span></span>

```azurecli
az image create --resource-group myResourceGroup --name myImage --source myVM
```

## <a name="step-3---create-hello-scale-set"></a><span data-ttu-id="f14e3-117">步驟 3-建立 hello 規模集</span><span class="sxs-lookup"><span data-stu-id="f14e3-117">Step 3 - Create hello scale set</span></span>

<span data-ttu-id="f14e3-118">取得 hello**識別碼**hello 映像。</span><span class="sxs-lookup"><span data-stu-id="f14e3-118">Get hello **id** of hello image.</span></span>

```azurecli
az image show --resource-group myResourceGroup --name myImage --query id
```

```json
"/subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage"
```

<span data-ttu-id="f14e3-119">使用 [az vmss create](/cli/azure/vmss#create) 從映像資源建立 VM：</span><span class="sxs-lookup"><span data-stu-id="f14e3-119">Create a VM from your image resource with [az vmss create](/cli/azure/vmss#create):</span></span>

```azurecli
az vmss create --resource-group myResourceGroup --name myScaleSet --image /subscriptions/afbdaf8b-9188-4651-bce1-9115dd57c98b/resourceGroups/vmtest/providers/Microsoft.Compute/images/myImage --upgrade-policy-mode automatic --vm-sku Standard_DS1_v2 --data-disk-sizes-gb 10 --admin-username azureuser --generate-ssh-keys
```

<span data-ttu-id="f14e3-120">此命令也會連結 10 GB 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f14e3-120">This command also attached a 10gb data disk.</span></span> <span data-ttu-id="f14e3-121">請注意，根據 hello VM 所選大小 (我們使用**Standard_DS1_v2**)，允許的資料磁碟的 hello 數目會不同。</span><span class="sxs-lookup"><span data-stu-id="f14e3-121">Keep in mind that depending on hello VM size chosen (we used **Standard_DS1_v2**), hello number of data disks allowed is different.</span></span> <span data-ttu-id="f14e3-122">如需詳細資訊，請檢閱 hello[虛擬機器大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="f14e3-122">For more information, review hello [virtual machine sizes](sizes.md).</span></span>

<span data-ttu-id="f14e3-123">一旦 hello 小數位數設定完成，則連接 tooit。</span><span class="sxs-lookup"><span data-stu-id="f14e3-123">Once hello scale set finishes, connect tooit.</span></span> <span data-ttu-id="f14e3-124">取得與 SSH hello 執行個體的 IP 位址清單[az vmss 清單執行個體的連接-資訊](/cli/azure/vmss#list-instance-connection-info):</span><span class="sxs-lookup"><span data-stu-id="f14e3-124">Get a list of IP addresses for hello instances for SSH with [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info):</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

```json
[
  "52.183.00.000:50000",
  "52.183.00.000:50003"
]
```

<span data-ttu-id="f14e3-125">現在您可以連線 toohello 虛擬機器執行個體 tooinitialize hello 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="f14e3-125">Now you can connect toohello virtual machine instance tooinitialize hello data disk</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub -p 50000 azureuser@52.183.00.000
```

## <a name="step-4---initialize-hello-data-disk"></a><span data-ttu-id="f14e3-126">步驟 4-初始化 hello 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="f14e3-126">Step 4 - Initialize hello data disk</span></span>

<span data-ttu-id="f14e3-127">同時連接的 toohello 虛擬機器，分割 hello 磁碟`fdisk`:</span><span class="sxs-lookup"><span data-stu-id="f14e3-127">While connected toohello virtual machine, partition hello disk with `fdisk`:</span></span>

```bash
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | sudo fdisk /dev/sdc
```

<span data-ttu-id="f14e3-128">寫入檔案系統 toohello 磁碟分割以 hello`mkfs`命令：</span><span class="sxs-lookup"><span data-stu-id="f14e3-128">Write a file system toohello partition with hello `mkfs` command:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="f14e3-129">掛接 hello 新磁碟，使其在 hello 作業系統中存取：</span><span class="sxs-lookup"><span data-stu-id="f14e3-129">Mount hello new disk so that it is accessible in hello operating system:</span></span>

```bash
sudo mkdir /datadrive ; sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="f14e3-130">hello 磁碟現在可以存取透過 hello datadrive 掛接，您可以使用驗證`ls /datadrive/`。</span><span class="sxs-lookup"><span data-stu-id="f14e3-130">hello disk can now be accesses through hello datadrive mountpoint, which can be verified with `ls /datadrive/`.</span></span>

<span data-ttu-id="f14e3-131">結束 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="f14e3-131">End hello SSH session.</span></span>


## <a name="step-5---configure-firewall"></a><span data-ttu-id="f14e3-132">步驟 5 - 設定防火牆</span><span class="sxs-lookup"><span data-stu-id="f14e3-132">Step 5 - Configure firewall</span></span>

<span data-ttu-id="f14e3-133">打孔 hello 防火牆 toohello hello 規模調整集合所裝載的 web 伺服器上一個洞。</span><span class="sxs-lookup"><span data-stu-id="f14e3-133">Punch a hole through hello firewall toohello webserver hosted by hello scale set.</span></span> <span data-ttu-id="f14e3-134">Hello 規模集建立時，會一併建立負載平衡器，您可以使用它**SSH** toohello 個別的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f14e3-134">When hello scale set was created, a load balancer was also created, and you used it **SSH** toohello individual virtual machines.</span></span> <span data-ttu-id="f14e3-135">tooopen 連接埠，您需要兩項資訊，就可以使用 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="f14e3-135">tooopen a port, you need two pieces of information, which you can get using Azure CLI.</span></span>

* <span data-ttu-id="f14e3-136">**前端 IP 位址集區**</span><span class="sxs-lookup"><span data-stu-id="f14e3-136">**Frontend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query frontendIpConfigurations[0].name`

* <span data-ttu-id="f14e3-137">**後端 IP 位址集區**</span><span class="sxs-lookup"><span data-stu-id="f14e3-137">**Backend IP address pool**</span></span>  
`az network lb show --resource-group myResourceGroup --name myScaleSetLB --output table --query backendAddressPools[0].name`

<span data-ttu-id="f14e3-138">使用這兩個名稱，您可以開啟連接埠 **80**。</span><span class="sxs-lookup"><span data-stu-id="f14e3-138">With those two names, you can open port **80**.</span></span>

```azurecli
az network lb rule create --backend-pool-name myScaleSetLBBEPool --backend-port 80 --frontend-ip-name loadBalancerFrontEnd --frontend-port 80 --name webserver --protocol tcp --resource-group myResourceGroup --lb-name myScaleSetLB
```


## <a name="step-6---automate-configuration"></a><span data-ttu-id="f14e3-139">步驟 6 - 自動化組態</span><span class="sxs-lookup"><span data-stu-id="f14e3-139">Step 6 - Automate configuration</span></span>

<span data-ttu-id="f14e3-140">hello 資料磁碟需要 toobe 每個虛擬機器執行個體上設定。</span><span class="sxs-lookup"><span data-stu-id="f14e3-140">hello data disk needs toobe configured on each virtual machine instance.</span></span> <span data-ttu-id="f14e3-141">我們可以自動化 hello hello hello 虛擬機器設定**CustomScript**延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f14e3-141">We can automate hello configuration of hello virtual machine with hello **CustomScript** extension.</span></span>

<span data-ttu-id="f14e3-142">首先，建立*.sh*包含 hello 磁碟格式的命令的指令碼。</span><span class="sxs-lookup"><span data-stu-id="f14e3-142">First, create a *.sh* script that includes hello disk format commands.</span></span>

```sh
#!/bin/bash

# Setup hello data disk
(echo n; echo p; echo 1; echo  ; echo  ; echo w) | fdisk /dev/sdc
fdisk /dev/sdc
mkfs -t ext4 /dev/sdc1
mkdir /datadrive
mount /dev/sdc1 /datadrive

exit 0
```

<span data-ttu-id="f14e3-143">接下來上, 傳該指令碼檔案 toowhere hello **CustomScript**延伸模組可以存取它。</span><span class="sxs-lookup"><span data-stu-id="f14e3-143">Next, upload that script file toowhere hello **CustomScript** extension can access it.</span></span> <span data-ttu-id="f14e3-144">複本可以在[這裡](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4)取得。</span><span class="sxs-lookup"><span data-stu-id="f14e3-144">A copy is available [here](https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4).</span></span>

<span data-ttu-id="f14e3-145">建立名為本機檔案**settings.json**和 put hello 下列 JSON 區塊中。</span><span class="sxs-lookup"><span data-stu-id="f14e3-145">Create a local file named **settings.json** and put hello following JSON block in it.</span></span> <span data-ttu-id="f14e3-146">hello`flieUris`屬性應該設定指令碼檔案上傳到 toowhere。</span><span class="sxs-lookup"><span data-stu-id="f14e3-146">hello `flieUris` property should be set toowhere your script file was uploaded to.</span></span>

```json
{
  "fileUris": ["https://gist.githubusercontent.com/Thraka/ab1d8b78ac4b23722f3d3c1c03ac5df4/raw/3ac6e385010ac675e23ce583ce27b1a752f1b482/prep-vmss.sh"],
  "commandToExecute": "bash prep-vmss.sh" 
}
```

<span data-ttu-id="f14e3-147">部署設定以 hello 這個命令 tooyour 標尺**CustomScript**延伸模組，參考 hello **settings.json**剛才所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="f14e3-147">Deploy this command tooyour scale set with hello **CustomScript** extension, referencing hello **settings.json** file we just created.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

<span data-ttu-id="f14e3-148">此擴充功能會在所有目前執行個體和稍後藉由調整所建立的任何執行個體上自動執行。</span><span class="sxs-lookup"><span data-stu-id="f14e3-148">This extension automatically runs on all current instances, and any instances later created by scaling.</span></span>

## <a name="step-7---configure-autoscale-rules"></a><span data-ttu-id="f14e3-149">步驟 7 - 設定自動調整規則</span><span class="sxs-lookup"><span data-stu-id="f14e3-149">Step 7 - Configure autoscale rules</span></span>

<span data-ttu-id="f14e3-150">目前，Azure CLI 中無法設定自動調整規則。</span><span class="sxs-lookup"><span data-stu-id="f14e3-150">Currently, autoscale rules cannot be set in Azure CLI.</span></span> <span data-ttu-id="f14e3-151">使用 hello [Azure 入口網站](https://portal.azure.com)tooconfigure 自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="f14e3-151">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

## <a name="step-8---management-tasks"></a><span data-ttu-id="f14e3-152">步驟 8 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="f14e3-152">Step 8 - Management tasks</span></span>

<span data-ttu-id="f14e3-153">整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。</span><span class="sxs-lookup"><span data-stu-id="f14e3-153">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="f14e3-154">此外，您可能會想 toocreate 指令碼自動化各種生命週期的工作，與 hello Azure CLI 提供快速的方式 toodo 這些工作。</span><span class="sxs-lookup"><span data-stu-id="f14e3-154">Additionally, you may want toocreate scripts that automate various lifecycle-tasks, and hello Azure CLI provides a quick way toodo those tasks.</span></span> <span data-ttu-id="f14e3-155">以下是一些常見工作。</span><span class="sxs-lookup"><span data-stu-id="f14e3-155">Here are a few common tasks.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="f14e3-156">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="f14e3-156">Get connection info</span></span>

```azurecli
az vmss list-instance-connection-info --resource-group myResourceGroup --name myScaleSet
```

### <a name="set-instance-count-manual-scale"></a><span data-ttu-id="f14e3-157">設定執行個體計數 (手動調整)</span><span class="sxs-lookup"><span data-stu-id="f14e3-157">Set instance count (manual scale)</span></span>

```azurecli
az vmss scale --resource-group myResourceGroup --name myScaleSet --new-capacity 4
```

### <a name="delete-resource-group"></a><span data-ttu-id="f14e3-158">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="f14e3-158">Delete resource group</span></span>

<span data-ttu-id="f14e3-159">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f14e3-159">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f14e3-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f14e3-160">Next steps</span></span>
<span data-ttu-id="f14e3-161">toolearn 一些 hello 虛擬機器擴展集功能引入在此教學課程中，請參閱下列資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="f14e3-161">toolearn more about some of hello virtual machine scale set features introduced in this tutorial, see hello following information:</span></span>

- [<span data-ttu-id="f14e3-162">Azure 虛擬機器擴展集概觀</span><span class="sxs-lookup"><span data-stu-id="f14e3-162">Azure Virtual Machine Scale Sets overview</span></span>](../../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)
- [<span data-ttu-id="f14e3-163">Azure 負載平衡器概觀</span><span class="sxs-lookup"><span data-stu-id="f14e3-163">Azure Load Balancer overview</span></span>](../../load-balancer/load-balancer-overview.md)
- [<span data-ttu-id="f14e3-164">使用網路安全性群組來控制網路流量</span><span class="sxs-lookup"><span data-stu-id="f14e3-164">Control network traffic flow with network security groups</span></span>](../../virtual-network/virtual-networks-nsg.md)