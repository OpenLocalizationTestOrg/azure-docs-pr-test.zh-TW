---
title: "aaaResize hello 傳統部署模型 Azure 中的 Windows VM |Microsoft 文件"
description: "調整 hello 傳統部署模型，使用 Azure Powershell 中建立 Windows 虛擬機器的大小。"
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a><span data-ttu-id="11e35-103">調整 hello 傳統部署模型中建立 Windows VM 的大小</span><span class="sxs-lookup"><span data-stu-id="11e35-103">Resize a Windows VM created in hello classic deployment model</span></span>
<span data-ttu-id="11e35-104">本文章將示範如何 tooresize Windows VM，在建立使用 Azure Powershell hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="11e35-104">This article shows you how tooresize a Windows VM, created in hello classic deployment model using Azure Powershell.</span></span>

<span data-ttu-id="11e35-105">當考量 hello 能力 tooresize VM 時，可控制 hello 範圍大小可用 tooresize hello 虛擬機器的兩個概念。</span><span class="sxs-lookup"><span data-stu-id="11e35-105">When considering hello ability tooresize a VM, there are two concepts which control hello range of sizes available tooresize hello virtual machine.</span></span> <span data-ttu-id="11e35-106">hello 第一個概念是以您的 VM 部署的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="11e35-106">hello first concept is hello region in which your VM is deployed.</span></span> <span data-ttu-id="11e35-107">在區域中可用的 VM 大小 hello 清單是 hello hello Azure 區域 web 頁面的 [服務] 索引標籤下。</span><span class="sxs-lookup"><span data-stu-id="11e35-107">hello list of VM sizes available in region is under hello Services tab of hello Azure Regions web page.</span></span> <span data-ttu-id="11e35-108">hello 第二個概念是 hello 目前裝載的 VM 的實體硬體。</span><span class="sxs-lookup"><span data-stu-id="11e35-108">hello second concept is hello physical hardware currently hosting your VM.</span></span> <span data-ttu-id="11e35-109">hello 實體伺服器裝載的 Vm 中群組在一起的一般實體硬體的叢集。</span><span class="sxs-lookup"><span data-stu-id="11e35-109">hello physical servers hosting VMs are grouped together in clusters of common physical hardware.</span></span> <span data-ttu-id="11e35-110">變更 VM 大小的 hello 方法不同取決於 hello 想要新的 VM 大小支援 hello 硬體叢集目前裝載的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="11e35-110">hello method of changing a VM size differs depending on if hello desired new VM size is supported by hello hardware cluster currently hosting hello VM.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="11e35-111">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="11e35-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="11e35-112">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="11e35-112">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="11e35-113">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="11e35-113">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="11e35-114">您也可以[hello Resource Manager 部署模型中建立 VM 調整](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="11e35-114">You can also [resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="add-your-account"></a><span data-ttu-id="11e35-115">新增帳戶</span><span class="sxs-lookup"><span data-stu-id="11e35-115">Add your account</span></span>
<span data-ttu-id="11e35-116">您必須設定 Azure PowerShell toowork 使用傳統的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="11e35-116">You must configure Azure PowerShell toowork with classic Azure resources.</span></span> <span data-ttu-id="11e35-117">請遵循以下 tooconfigure Azure PowerShell toomanage 傳統資源的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="11e35-117">Follow hello steps below tooconfigure Azure PowerShell toomanage classic resources.</span></span>

1. <span data-ttu-id="11e35-118">在 hello PowerShell 提示字元中輸入`Add-AzureAccount`按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="11e35-118">At hello PowerShell prompt, type `Add-AzureAccount` and click **Enter**.</span></span> 
2. <span data-ttu-id="11e35-119">輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="11e35-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="11e35-120">輸入 hello 您帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="11e35-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="11e35-121">按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="11e35-121">Click **Sign in**.</span></span> 

## <a name="resize-in-hello-same-hardware-cluster"></a><span data-ttu-id="11e35-122">調整在 hello 相同硬體叢集</span><span class="sxs-lookup"><span data-stu-id="11e35-122">Resize in hello same hardware cluster</span></span>
<span data-ttu-id="11e35-123">tooresize VM tooa 大小可用在 hello 硬體叢集中裝載 hello VM，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="11e35-123">tooresize a VM tooa size available in hello hardware cluster hosting hello VM, perform hello following steps.</span></span>

1. <span data-ttu-id="11e35-124">執行下列 PowerShell 命令裝載 hello 雲端服務可包含的 hello 硬體叢集中可用的 toolist hello VM 大小 hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="11e35-124">Run hello following PowerShell command toolist hello VM sizes available in hello hardware cluster hosting hello cloud service which contains hello VM.</span></span>
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. <span data-ttu-id="11e35-125">執行下列命令 tooresize hello VM hello。</span><span class="sxs-lookup"><span data-stu-id="11e35-125">Run hello following commands tooresize hello VM.</span></span>
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a><span data-ttu-id="11e35-126">在新的硬體叢集上調整大小</span><span class="sxs-lookup"><span data-stu-id="11e35-126">Resize on a new hardware cluster</span></span>
<span data-ttu-id="11e35-127">tooresize VM tooa 大小不適用於裝載的 hello 硬體叢集 hello VM，hello 雲端服務和 hello 雲端服務中的所有 Vm 都必須重新建立。</span><span class="sxs-lookup"><span data-stu-id="11e35-127">tooresize a VM tooa size not available in hello hardware cluster hosting hello VM, hello cloud service and all VMs in hello cloud service must be recreated.</span></span> <span data-ttu-id="11e35-128">每個雲端服務被裝載在單一硬體叢集上，因此 hello 雲端服務中的所有 Vm 都必須支援硬體叢集的大小。</span><span class="sxs-lookup"><span data-stu-id="11e35-128">Each cloud service is hosted on a single hardware cluster so all VMs in hello cloud service must be a size that is supported on a hardware cluster.</span></span> <span data-ttu-id="11e35-129">hello 下列步驟將說明如何刪除，然後重新建立 VM tooresize hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="11e35-129">hello following steps will describe how tooresize a VM by deleting and then recreating hello cloud service.</span></span>

1. <span data-ttu-id="11e35-130">執行下列 PowerShell 命令 toolist hello VM 大小可用 hello 區域中的 hello。</span><span class="sxs-lookup"><span data-stu-id="11e35-130">Run hello following PowerShell command toolist hello VM sizes available in hello region.</span></span> 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. <span data-ttu-id="11e35-131">記下包含調整大小的 hello VM toobe hello 雲端服務中每個 VM 的所有組態設定。</span><span class="sxs-lookup"><span data-stu-id="11e35-131">Make note of all configuration settings for each VM in hello cloud service which contains hello VM toobe resized.</span></span> 
3. <span data-ttu-id="11e35-132">刪除 hello hello 選項 tooretain hello 磁碟選取每個 VM 的雲端服務中的所有 Vm。</span><span class="sxs-lookup"><span data-stu-id="11e35-132">Delete all VMs in hello cloud service selecting hello option tooretain hello disks for each VM.</span></span>
4. <span data-ttu-id="11e35-133">重新建立 hello VM toobe 調整使用 hello 所需的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="11e35-133">Recreate hello VM toobe resized using hello desired VM size.</span></span>
5. <span data-ttu-id="11e35-134">重新建立所有已使用 hello 硬體叢集現在裝載 hello 雲端服務中可用的 VM 大小的 hello 雲端服務中的其他 Vm。</span><span class="sxs-lookup"><span data-stu-id="11e35-134">Recreate all other VMs which were in hello cloud service using a VM size available in hello hardware cluster now hosting hello cloud service.</span></span>

<span data-ttu-id="11e35-135">您可以在[這裡](https://github.com/Azure/azure-vm-scripts)找到刪除雲端服務並使用新 VM 大小重新建立雲端服務的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="11e35-135">A sample script for deleting and recreating a cloud service using a new VM size can be found [here](https://github.com/Azure/azure-vm-scripts).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="11e35-136">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11e35-136">Next steps</span></span>
* <span data-ttu-id="11e35-137">[調整大小 hello Resource Manager 部署模型中建立的 VM](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="11e35-137">[Resize a VM created in hello Resource Manager deployment model](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

