---
title: "aaaCreate 和管理 Linux Vm hello Azure CLI |Microsoft 文件"
description: "教學課程-建立和管理 Linux Vm 與 hello Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 05f7c1cf860f809bc13f110778d3bddd619ac6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-linux-vms-with-hello-azure-cli"></a><span data-ttu-id="9573a-103">建立和管理 Linux Vm 與 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9573a-103">Create and Manage Linux VMs with hello Azure CLI</span></span>

<span data-ttu-id="9573a-104">Azure 虛擬機器提供完全可設定且彈性的計算環境。</span><span class="sxs-lookup"><span data-stu-id="9573a-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="9573a-105">本教學課程涵蓋基本的「Azure 虛擬機器」部署項目，例如選取 VM 大小、選取 VM 映像、部署 VM。</span><span class="sxs-lookup"><span data-stu-id="9573a-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="9573a-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="9573a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9573a-107">建立和連線 tooa VM</span><span class="sxs-lookup"><span data-stu-id="9573a-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="9573a-108">選取及使用 VM 映像</span><span class="sxs-lookup"><span data-stu-id="9573a-108">Select and use VM images</span></span>
> * <span data-ttu-id="9573a-109">檢視及使用特定 VM 大小</span><span class="sxs-lookup"><span data-stu-id="9573a-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="9573a-110">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="9573a-110">Resize a VM</span></span>
> * <span data-ttu-id="9573a-111">檢視及了解 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-111">View and understand VM state</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9573a-112">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9573a-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9573a-113">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="9573a-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9573a-114">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9573a-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-resource-group"></a><span data-ttu-id="9573a-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="9573a-115">Create resource group</span></span>

<span data-ttu-id="9573a-116">建立資源群組以 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="9573a-116">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="9573a-117">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="9573a-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="9573a-118">資源群組必須在虛擬機器之前建立。</span><span class="sxs-lookup"><span data-stu-id="9573a-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="9573a-119">在此範例中，資源群組命名為*myResourceGroupVM*會建立在 hello *eastus*區域。</span><span class="sxs-lookup"><span data-stu-id="9573a-119">In this example, a resource group named *myResourceGroupVM* is created in hello *eastus* region.</span></span> 

```azurecli-interactive 
az group create --name myResourceGroupVM --location eastus
```

<span data-ttu-id="9573a-120">建立或修改 VM，能看到本教學課程時，所指定 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="9573a-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="9573a-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="9573a-121">Create virtual machine</span></span>

<span data-ttu-id="9573a-122">建立虛擬機器以 hello [az vm 建立](https://docs.microsoft.com/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="9573a-122">Create a virtual machine with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="9573a-123">建立虛擬機器時，有數個可用的選項，例如作業系統映像、磁碟大小及系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="9573a-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="9573a-124">在此範例中，是使用 myVM 名稱來建立執行 Ubuntu Server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-124">In this example, a virtual machine is created with a name of *myVM* running Ubuntu Server.</span></span> 

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="9573a-125">一次在建立 VM 的 hello，hello Azure CLI 輸出 hello VM 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9573a-125">Once hello VM has been created, hello Azure CLI outputs information about hello VM.</span></span> <span data-ttu-id="9573a-126">記下 hello `publicIpAddress`，此位址可以是使用的 tooaccess hello 虛擬機器...</span><span class="sxs-lookup"><span data-stu-id="9573a-126">Take note of hello `publicIpAddress`, this address can be used tooaccess hello virtual machine..</span></span> 

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroupVM/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroupVM"
}
```

## <a name="connect-toovm"></a><span data-ttu-id="9573a-127">連接 tooVM</span><span class="sxs-lookup"><span data-stu-id="9573a-127">Connect tooVM</span></span>

<span data-ttu-id="9573a-128">您現在可以連接 toohello VM 使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="9573a-128">You can now connect toohello VM using SSH.</span></span> <span data-ttu-id="9573a-129">Hello 範例 IP 位址取代成 hello `publicIpAddress` hello 上一個步驟中所述。</span><span class="sxs-lookup"><span data-stu-id="9573a-129">Replace hello example IP address with hello `publicIpAddress` noted in hello previous step.</span></span>

```bash
ssh 52.174.34.95
```

<span data-ttu-id="9573a-130">一旦完成以 hello VM，請關閉 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9573a-130">Once finished with hello VM, close hello SSH session.</span></span> 

```bash
exit
```

## <a name="understand-vm-images"></a><span data-ttu-id="9573a-131">了解 VM 映像</span><span class="sxs-lookup"><span data-stu-id="9573a-131">Understand VM images</span></span>

<span data-ttu-id="9573a-132">hello Azure marketplace 包括許多可以使用的 toocreate Vm 的映像。</span><span class="sxs-lookup"><span data-stu-id="9573a-132">hello Azure marketplace includes many images that can be used toocreate VMs.</span></span> <span data-ttu-id="9573a-133">在 hello 先前步驟中，已使用 Ubuntu 映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-133">In hello previous steps, a virtual machine was created using an Ubuntu image.</span></span> <span data-ttu-id="9573a-134">在此步驟中，hello Azure CLI 會使用的 toosearch hello marketplace 中的一個 CentOS 映像，就會使用 toodeploy 第二個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-134">In this step, hello Azure CLI is used toosearch hello marketplace for a CentOS image, which is then used toodeploy a second virtual machine.</span></span>  

<span data-ttu-id="9573a-135">一份 hello toosee 最常使用的映像，請使用 hello [az vm 映像清單](/cli/azure/vm/image#list)命令。</span><span class="sxs-lookup"><span data-stu-id="9573a-135">toosee a list of hello most commonly used images, use hello [az vm image list](/cli/azure/vm/image#list) command.</span></span>

```azurecli-interactive 
az vm image list --output table
```

<span data-ttu-id="9573a-136">hello 命令輸出傳回 hello 最受歡迎的 VM 映像，在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="9573a-136">hello command output returns hello most popular VM images on Azure.</span></span>

```bash
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
WindowsServer  MicrosoftWindowsServer  2016-Datacenter     MicrosoftWindowsServer:WindowsServer:2016-Datacenter:latest     Win2016Datacenter    latest
WindowsServer  MicrosoftWindowsServer  2012-R2-Datacenter  MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest  Win2012R2Datacenter  latest
WindowsServer  MicrosoftWindowsServer  2008-R2-SP1         MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:latest         Win2008R2SP1         latest
WindowsServer  MicrosoftWindowsServer  2012-Datacenter     MicrosoftWindowsServer:WindowsServer:2012-Datacenter:latest     Win2012Datacenter    latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
```

<span data-ttu-id="9573a-137">無法看到完整清單，請加入 hello`--all`引數。</span><span class="sxs-lookup"><span data-stu-id="9573a-137">A full list can be seen by adding hello `--all` argument.</span></span> <span data-ttu-id="9573a-138">hello 影像清單也可以篩選由`--publisher`或`–-offer`。</span><span class="sxs-lookup"><span data-stu-id="9573a-138">hello image list can also be filtered by `--publisher` or `–-offer`.</span></span> <span data-ttu-id="9573a-139">在此範例中，篩選與符合方案的所有映像 hello 清單*CentOS*。</span><span class="sxs-lookup"><span data-stu-id="9573a-139">In this example, hello list is filtered for all images with an offer that matches *CentOS*.</span></span> 

```azurecli-interactive 
az vm image list --offer CentOS --all --output table
```

<span data-ttu-id="9573a-140">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="9573a-140">Partial output:</span></span>

```azurecli-interactive 
Offer             Publisher         Sku   Urn                                     Version
----------------  ----------------  ----  --------------------------------------  -----------
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201501         6.5.201501
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201503         6.5.201503
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.201506         6.5.201506
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20150904       6.5.20150904
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20160309       6.5.20160309
CentOS            OpenLogic         6.5   OpenLogic:CentOS:6.5:6.5.20170207       6.5.20170207
```

<span data-ttu-id="9573a-141">使用特定的映像的 VM toodeploy 記 hello 值中 hello *Urn*資料行。</span><span class="sxs-lookup"><span data-stu-id="9573a-141">toodeploy a VM using a specific image, take note of hello value in hello *Urn* column.</span></span> <span data-ttu-id="9573a-142">當指定 hello 映像，hello 映像的版本號碼可以被取代 「 最新 」，以選取 hello hello 分配的最新的版本。</span><span class="sxs-lookup"><span data-stu-id="9573a-142">When specifying hello image, hello image version number can be replaced with “latest”, which selects hello latest version of hello distribution.</span></span> <span data-ttu-id="9573a-143">在此範例中，hello`--image`引數是使用的 toospecify hello 最新版本的 CentOS 6.5 映像。</span><span class="sxs-lookup"><span data-stu-id="9573a-143">In this example, hello `--image` argument is used toospecify hello latest version of a CentOS 6.5 image.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroupVM --name myVM2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="9573a-144">了解 VM 大小</span><span class="sxs-lookup"><span data-stu-id="9573a-144">Understand VM sizes</span></span>

<span data-ttu-id="9573a-145">虛擬機器大小會決定 hello 量，例如 CPU、 GPU，以及記憶體都會提供 toohello 虛擬機器的計算資源。</span><span class="sxs-lookup"><span data-stu-id="9573a-145">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="9573a-146">虛擬機器必須 toobe hello 預期工作負載的適當調整大小。</span><span class="sxs-lookup"><span data-stu-id="9573a-146">Virtual machines need toobe sized appropriately for hello expected work load.</span></span> <span data-ttu-id="9573a-147">如果工作負載增加，可以調整現有虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="9573a-147">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="9573a-148">VM 大小</span><span class="sxs-lookup"><span data-stu-id="9573a-148">VM Sizes</span></span>

<span data-ttu-id="9573a-149">下表中的 hello 將大小分類成使用案例。</span><span class="sxs-lookup"><span data-stu-id="9573a-149">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="9573a-150">類型</span><span class="sxs-lookup"><span data-stu-id="9573a-150">Type</span></span>                     | <span data-ttu-id="9573a-151">大小</span><span class="sxs-lookup"><span data-stu-id="9573a-151">Sizes</span></span>           |    <span data-ttu-id="9573a-152">說明</span><span class="sxs-lookup"><span data-stu-id="9573a-152">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="9573a-153">一般用途</span><span class="sxs-lookup"><span data-stu-id="9573a-153">General purpose</span></span>](sizes-general.md)         |<span data-ttu-id="9573a-154">Dsv3、Dv3、DSv2、Dv2、DS、D、Av2、A0-7</span><span class="sxs-lookup"><span data-stu-id="9573a-154">Dsv3, Dv3, DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="9573a-155">平衡的 CPU 對記憶體。</span><span class="sxs-lookup"><span data-stu-id="9573a-155">Balanced CPU-to-memory.</span></span> <span data-ttu-id="9573a-156">適用於開發 / 測試及小型 toomedium 應用程式和資料解決方案。</span><span class="sxs-lookup"><span data-stu-id="9573a-156">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| [<span data-ttu-id="9573a-157">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="9573a-157">Compute optimized</span></span>](sizes-compute.md)   | <span data-ttu-id="9573a-158">Fs、F</span><span class="sxs-lookup"><span data-stu-id="9573a-158">Fs, F</span></span>             | <span data-ttu-id="9573a-159">CPU 與記憶體的比例高。</span><span class="sxs-lookup"><span data-stu-id="9573a-159">High CPU-to-memory.</span></span> <span data-ttu-id="9573a-160">適用於中流量應用程式、網路設備，以及批次處理。</span><span class="sxs-lookup"><span data-stu-id="9573a-160">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| [<span data-ttu-id="9573a-161">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="9573a-161">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)    | <span data-ttu-id="9573a-162">Esv3、Ev3、M、GS、G、DSv2、DS、Dv2、D</span><span class="sxs-lookup"><span data-stu-id="9573a-162">Esv3, Ev3, M, GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="9573a-163">記憶體與核心的比例高。</span><span class="sxs-lookup"><span data-stu-id="9573a-163">High memory-to-core.</span></span> <span data-ttu-id="9573a-164">太棒了關聯式資料庫、 中度 toolarge 快取，以及記憶體中分析。</span><span class="sxs-lookup"><span data-stu-id="9573a-164">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| [<span data-ttu-id="9573a-165">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="9573a-165">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)      | <span data-ttu-id="9573a-166">Ls</span><span class="sxs-lookup"><span data-stu-id="9573a-166">Ls</span></span>                | <span data-ttu-id="9573a-167">高磁碟輸送量及 IO。</span><span class="sxs-lookup"><span data-stu-id="9573a-167">High disk throughput and IO.</span></span> <span data-ttu-id="9573a-168">適用於巨量資料、SQL 及 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9573a-168">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| [<span data-ttu-id="9573a-169">GPU</span><span class="sxs-lookup"><span data-stu-id="9573a-169">GPU</span></span>](sizes-gpu.md)          | <span data-ttu-id="9573a-170">NV、NC</span><span class="sxs-lookup"><span data-stu-id="9573a-170">NV, NC</span></span>            | <span data-ttu-id="9573a-171">以大量圖形轉譯和視訊編輯為目標的特製化 VM。</span><span class="sxs-lookup"><span data-stu-id="9573a-171">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| [<span data-ttu-id="9573a-172">高效能</span><span class="sxs-lookup"><span data-stu-id="9573a-172">High performance</span></span>](sizes-hpc.md) | <span data-ttu-id="9573a-173">H、A8-11</span><span class="sxs-lookup"><span data-stu-id="9573a-173">H, A8-11</span></span>          | <span data-ttu-id="9573a-174">我們的最強大 CPU VM，可搭配選用的高輸送量網路介面 (RDMA)。</span><span class="sxs-lookup"><span data-stu-id="9573a-174">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="9573a-175">尋找可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="9573a-175">Find available VM sizes</span></span>

<span data-ttu-id="9573a-176">在特定區域大小可用 toosee VM 的清單，請使用 hello [az vm 清單大小](/cli/azure/vm#list-sizes)命令。</span><span class="sxs-lookup"><span data-stu-id="9573a-176">toosee a list of VM sizes available in a particular region, use hello [az vm list-sizes](/cli/azure/vm#list-sizes) command.</span></span> 

```azurecli-interactive 
az vm list-sizes --location eastus --output table
```

<span data-ttu-id="9573a-177">部分輸出：</span><span class="sxs-lookup"><span data-stu-id="9573a-177">Partial output:</span></span>

```azurecli-interactive 
  MaxDataDiskCount    MemoryInMb  Name                      NumberOfCores    OsDiskSizeInMb    ResourceDiskSizeInMb
------------------  ------------  ----------------------  ---------------  ----------------  ----------------------
                 2          3584  Standard_DS1                          1           1047552                    7168
                 4          7168  Standard_DS2                          2           1047552                   14336
                 8         14336  Standard_DS3                          4           1047552                   28672
                16         28672  Standard_DS4                          8           1047552                   57344
                 4         14336  Standard_DS11                         2           1047552                   28672
                 8         28672  Standard_DS12                         4           1047552                   57344
                16         57344  Standard_DS13                         8           1047552                  114688
                32        114688  Standard_DS14                        16           1047552                  229376
                 1           768  Standard_A0                           1           1047552                   20480
                 2          1792  Standard_A1                           1           1047552                   71680
                 4          3584  Standard_A2                           2           1047552                  138240
                 8          7168  Standard_A3                           4           1047552                  291840
                 4         14336  Standard_A5                           2           1047552                  138240
                16         14336  Standard_A4                           8           1047552                  619520
                 8         28672  Standard_A6                           4           1047552                  291840
                16         57344  Standard_A7                           8           1047552                  619520
```

### <a name="create-vm-with-specific-size"></a><span data-ttu-id="9573a-178">建立特定大小的 VM</span><span class="sxs-lookup"><span data-stu-id="9573a-178">Create VM with specific size</span></span>

<span data-ttu-id="9573a-179">在 hello 先前 VM 建立範例中，大小未提供，而這可能導致預設大小。</span><span class="sxs-lookup"><span data-stu-id="9573a-179">In hello previous VM creation example, a size was not provided, which results in a default size.</span></span> <span data-ttu-id="9573a-180">VM 大小可以選取在建立階段使用[az vm 建立](/cli/azure/vm#create)和 hello`--size`引數。</span><span class="sxs-lookup"><span data-stu-id="9573a-180">A VM size can be selected at creation time using [az vm create](/cli/azure/vm#create) and hello `--size` argument.</span></span> 

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupVM \
    --name myVM3 \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
```

### <a name="resize-a-vm"></a><span data-ttu-id="9573a-181">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="9573a-181">Resize a VM</span></span>

<span data-ttu-id="9573a-182">已部署 VM 之後，它可以是調整過大小的 tooincrease 或減少資源配置。</span><span class="sxs-lookup"><span data-stu-id="9573a-182">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="9573a-183">調整 VM 大小時之前, 檢查是否 hello 所需的大小在 hello 目前 Azure 叢集上使用。</span><span class="sxs-lookup"><span data-stu-id="9573a-183">Before resizing a VM, check if hello desired size is available on hello current Azure cluster.</span></span> <span data-ttu-id="9573a-184">hello [az vm 清單-vm-調整大小的選項](/cli/azure/vm#list-vm-resize-options)命令傳回 hello 大小清單。</span><span class="sxs-lookup"><span data-stu-id="9573a-184">hello [az vm list-vm-resize-options](/cli/azure/vm#list-vm-resize-options) command returns hello list of sizes.</span></span> 

```azurecli-interactive 
az vm list-vm-resize-options --resource-group myResourceGroupVM --name myVM --query [].name
```
<span data-ttu-id="9573a-185">如果 hello 所需的大小是可用，hello VM 可以調整大小，從開機的狀態，不過 hello 作業期間重新開機。</span><span class="sxs-lookup"><span data-stu-id="9573a-185">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span> <span data-ttu-id="9573a-186">使用 hello [az vm 調整]( /cli/azure/vm#resize)命令 tooperform hello 調整大小。</span><span class="sxs-lookup"><span data-stu-id="9573a-186">Use hello [az vm resize]( /cli/azure/vm#resize) command tooperform hello resize.</span></span>

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_DS4_v2
```

<span data-ttu-id="9573a-187">如果 hello 所需的大小不 hello 目前在叢集上，hello VM toobe hello 的調整大小作業之前取消配置可能會發生的需求。</span><span class="sxs-lookup"><span data-stu-id="9573a-187">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="9573a-188">使用 hello [az vm 解除配置]( /cli/azure/vm#deallocate)命令 toostop 及取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="9573a-188">Use hello [az vm deallocate]( /cli/azure/vm#deallocate) command toostop and deallocate hello VM.</span></span> <span data-ttu-id="9573a-189">請注意，當 hello VM 的電源已回復，可能會移除 hello 暫存磁碟上的任何資料。</span><span class="sxs-lookup"><span data-stu-id="9573a-189">Note, when hello VM is powered back on, any data on hello temp disk may be removed.</span></span> <span data-ttu-id="9573a-190">hello 公用 IP 位址也會變更除非正在使用的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9573a-190">hello public IP address also changes unless a static IP address is being used.</span></span> 

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupVM --name myVM
```

<span data-ttu-id="9573a-191">一旦取消配置，可能會發生 hello 調整大小。</span><span class="sxs-lookup"><span data-stu-id="9573a-191">Once deallocated, hello resize can occur.</span></span> 

```azurecli-interactive 
az vm resize --resource-group myResourceGroupVM --name myVM --size Standard_GS1
```

<span data-ttu-id="9573a-192">Hello 調整大小之後，就可以啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="9573a-192">After hello resize, hello VM can be started.</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

## <a name="vm-power-states"></a><span data-ttu-id="9573a-193">VM 電源狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-193">VM power states</span></span>

<span data-ttu-id="9573a-194">Azure VM 的電源狀態可以是許多電源狀態的其中一種。</span><span class="sxs-lookup"><span data-stu-id="9573a-194">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="9573a-195">此狀態表示 hello 目前 hello VM 的狀態從 hello hypervisor hello 觀點來看。</span><span class="sxs-lookup"><span data-stu-id="9573a-195">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="9573a-196">電源狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-196">Power states</span></span>

| <span data-ttu-id="9573a-197">電源狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-197">Power State</span></span> | <span data-ttu-id="9573a-198">說明</span><span class="sxs-lookup"><span data-stu-id="9573a-198">Description</span></span>
|----|----|
| <span data-ttu-id="9573a-199">啟動中</span><span class="sxs-lookup"><span data-stu-id="9573a-199">Starting</span></span> | <span data-ttu-id="9573a-200">指出正在啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-200">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="9573a-201">執行中</span><span class="sxs-lookup"><span data-stu-id="9573a-201">Running</span></span> | <span data-ttu-id="9573a-202">指出該 hello 虛擬機器正在執行。</span><span class="sxs-lookup"><span data-stu-id="9573a-202">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="9573a-203">停止中</span><span class="sxs-lookup"><span data-stu-id="9573a-203">Stopping</span></span> | <span data-ttu-id="9573a-204">表示正在停止該 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-204">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="9573a-205">已停止</span><span class="sxs-lookup"><span data-stu-id="9573a-205">Stopped</span></span> | <span data-ttu-id="9573a-206">表示該 hello 虛擬機器已停止。</span><span class="sxs-lookup"><span data-stu-id="9573a-206">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="9573a-207">在 hello 停止狀態的虛擬機器仍會產生計算費用。</span><span class="sxs-lookup"><span data-stu-id="9573a-207">Virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="9573a-208">正在解除配置</span><span class="sxs-lookup"><span data-stu-id="9573a-208">Deallocating</span></span> | <span data-ttu-id="9573a-209">表示已解除配置該 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-209">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="9573a-210">已解除配置</span><span class="sxs-lookup"><span data-stu-id="9573a-210">Deallocated</span></span> | <span data-ttu-id="9573a-211">表示該 hello 虛擬機器移除從 hello hypervisor 但 hello 控制平面中仍然可用。</span><span class="sxs-lookup"><span data-stu-id="9573a-211">Indicates that hello virtual machine is removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="9573a-212">Hello 取消配置狀態中的虛擬機器不會產生計算費用。</span><span class="sxs-lookup"><span data-stu-id="9573a-212">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="9573a-213">表示 hello hello 虛擬機器的電源狀態不明。</span><span class="sxs-lookup"><span data-stu-id="9573a-213">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="9573a-214">尋找電源狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-214">Find power state</span></span>

<span data-ttu-id="9573a-215">特定的 VM，使用 hello tooretrieve hello 狀態[az vm 取得執行個體檢視](/cli/azure/vm#get-instance-view)命令。</span><span class="sxs-lookup"><span data-stu-id="9573a-215">tooretrieve hello state of a particular VM, use hello [az vm get instance-view](/cli/azure/vm#get-instance-view) command.</span></span> <span data-ttu-id="9573a-216">為確定 toospecify 虛擬機器與資源群組的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="9573a-216">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```azurecli-interactive 
az vm get-instance-view \
    --name myVM \
    --resource-group myResourceGroupVM \
    --query instanceView.statuses[1] --output table
```

<span data-ttu-id="9573a-217">輸出：</span><span class="sxs-lookup"><span data-stu-id="9573a-217">Output:</span></span>

```azurecli-interactive 
ode                DisplayStatus    Level
------------------  ---------------  -------
PowerState/running  VM running       Info
```

## <a name="management-tasks"></a><span data-ttu-id="9573a-218">管理工作</span><span class="sxs-lookup"><span data-stu-id="9573a-218">Management tasks</span></span>

<span data-ttu-id="9573a-219">在 hello 生命週期的虛擬機器，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9573a-219">During hello life-cycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="9573a-220">此外，您可能想 toocreate 指令碼 tooautomate 重複或複雜工作。</span><span class="sxs-lookup"><span data-stu-id="9573a-220">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="9573a-221">使用 Azure CLI hello，許多常見的管理工作可以執行從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="9573a-221">Using hello Azure CLI, many common management tasks can be run from hello command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="9573a-222">取得 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9573a-222">Get IP address</span></span>

<span data-ttu-id="9573a-223">此命令會傳回虛擬機器的 hello 私人和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9573a-223">This command returns hello private and public IP addresses of a virtual machine.</span></span>  

```azurecli-interactive 
az vm list-ip-addresses --resource-group myResourceGroupVM --name myVM --output table
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="9573a-224">停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9573a-224">Stop virtual machine</span></span>

```azurecli-interactive 
az vm stop --resource-group myResourceGroupVM --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="9573a-225">啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="9573a-225">Start virtual machine</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupVM --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="9573a-226">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="9573a-226">Delete resource group</span></span>

<span data-ttu-id="9573a-227">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="9573a-227">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroupVM --no-wait --yes
```

## <a name="next-steps"></a><span data-ttu-id="9573a-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9573a-228">Next steps</span></span>

<span data-ttu-id="9573a-229">在本教學課程中，您已了解基本的 VM 建立和管理，像是如何：</span><span class="sxs-lookup"><span data-stu-id="9573a-229">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9573a-230">建立和連線 tooa VM</span><span class="sxs-lookup"><span data-stu-id="9573a-230">Create and connect tooa VM</span></span>
> * <span data-ttu-id="9573a-231">選取及使用 VM 映像</span><span class="sxs-lookup"><span data-stu-id="9573a-231">Select and use VM images</span></span>
> * <span data-ttu-id="9573a-232">檢視及使用特定 VM 大小</span><span class="sxs-lookup"><span data-stu-id="9573a-232">View and use specific VM sizes</span></span>
> * <span data-ttu-id="9573a-233">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="9573a-233">Resize a VM</span></span>
> * <span data-ttu-id="9573a-234">檢視及了解 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="9573a-234">View and understand VM state</span></span>

<span data-ttu-id="9573a-235">前進 toohello 下一個教學課程的 toolearn 有關 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9573a-235">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="9573a-236">建立和管理 VM 磁碟</span><span class="sxs-lookup"><span data-stu-id="9573a-236">Create and Manage VM disks</span></span>](./tutorial-manage-disks.md)
