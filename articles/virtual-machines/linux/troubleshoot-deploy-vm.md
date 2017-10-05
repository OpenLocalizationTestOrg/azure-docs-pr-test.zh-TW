---
title: "針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解 | Microsoft Docs"
description: "針對 Azure Resource Manager 部署模型中的 Linux 虛擬機器部署問題進行疑難排解。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 8bc9de90a49caf9155073caaa160585c6cc3728b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="6bab3-103">針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="6bab3-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="6bab3-104">若要針對 Azure 中的虛擬機器 (VM) 部署問題進行疑難排解，請檢閱[常見問題](#top-issues)以了解常見的失敗和解決方式。</span><span class="sxs-lookup"><span data-stu-id="6bab3-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="6bab3-105">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="6bab3-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="6bab3-106">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="6bab3-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6bab3-107">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="6bab3-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="6bab3-108">常見問題</span><span class="sxs-lookup"><span data-stu-id="6bab3-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="6bab3-109">叢集無法支援要求的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="6bab3-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="6bab3-110">以較小的 VM 大小重試要求。</span><span class="sxs-lookup"><span data-stu-id="6bab3-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="6bab3-111">如果無法變更要求的 VM 的大小︰</span><span class="sxs-lookup"><span data-stu-id="6bab3-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="6bab3-112">停止可用性設定組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="6bab3-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="6bab3-113">按一下 [資源群組] > 您的資源群組 > [資源] > 您的可用性設定組 > [虛擬機器] > 您的虛擬機器 > [停止]。</span><span class="sxs-lookup"><span data-stu-id="6bab3-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="6bab3-114">在所有 VM 都停止後，建立所需大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="6bab3-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="6bab3-115">先啟動新的 VM，然後選取每個已停止的 VM 並按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="6bab3-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="6bab3-116">叢集沒有可用的資源</span><span class="sxs-lookup"><span data-stu-id="6bab3-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="6bab3-117">稍後再重試要求。</span><span class="sxs-lookup"><span data-stu-id="6bab3-117">Retry the request later.</span></span>
- <span data-ttu-id="6bab3-118">如果新的 VM 可以屬於不同的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="6bab3-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="6bab3-119">在不同的可用性設定組 (位於相同區域) 中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6bab3-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="6bab3-120">將新的 VM 加入相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6bab3-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="6bab3-121">我要如何啟用我的 Visual Studio Enterprise (BizSpark) 每月點數</span><span class="sxs-lookup"><span data-stu-id="6bab3-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="6bab3-122">若要啟用您的每月點數，請參閱這篇[文章](https://azure.microsoft.com/offers/ms-azr-0064p/)。</span><span class="sxs-lookup"><span data-stu-id="6bab3-122">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-the-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="6bab3-123">為什麼我可以不安裝適用於 Ubuntu NV VM 的 GPU 驅動程式？</span><span class="sxs-lookup"><span data-stu-id="6bab3-123">Why can I not install the GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="6bab3-124">目前，Linux GPU 支援僅適用於執行 Ubuntu Server 16.04 LTS 的 Azure NC VM。</span><span class="sxs-lookup"><span data-stu-id="6bab3-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="6bab3-125">如需詳細資訊，請參閱[為執行 Linux 的 N 系列 VM 設定 GPU 驅動程式](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="6bab3-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="6bab3-126">我的 Linux N 系列 VM 遺失驅動程式</span><span class="sxs-lookup"><span data-stu-id="6bab3-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="6bab3-127">Linux 型 VM 的驅動程式位於[這裡](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="6bab3-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="6bab3-128">在我的 N 系列 VM 內找不到 GPU 執行個體</span><span class="sxs-lookup"><span data-stu-id="6bab3-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="6bab3-129">若要利用 Azure N 系列 VM (執行 Windows Server 2016 或 Windows Server 2012 R2) 的 GPU 功能，您必須在部署之後於每個 VM 上安裝 NVIDIA 圖形驅動程式。</span><span class="sxs-lookup"><span data-stu-id="6bab3-129">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="6bab3-130">您可以取得 [Windows VM](../windows/n-series-driver-setup.md) 和 [Linux VM](n-series-driver-setup.md) 的驅動程式設定資訊。</span><span class="sxs-lookup"><span data-stu-id="6bab3-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="6bab3-131">我的區域是否有提供 N 系列 VM？</span><span class="sxs-lookup"><span data-stu-id="6bab3-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="6bab3-132">您可以從[依區域提供的產品表](https://azure.microsoft.com/regions/services)查看是否有提供該產品，以及從[這裡](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)查看定價。</span><span class="sxs-lookup"><span data-stu-id="6bab3-132">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="6bab3-133">我在調整 VM 大小時，看不到所要的 VM 大小系列。</span><span class="sxs-lookup"><span data-stu-id="6bab3-133">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="6bab3-134">執行 VM 時，會將 VM 部署到實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="6bab3-134">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="6bab3-135">Azure 區域中的實體伺服器會群組成共同的實體硬體叢集。</span><span class="sxs-lookup"><span data-stu-id="6bab3-135">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="6bab3-136">調整 VM 大小時如果需要將 VM 移到不同的硬體叢集，將會依部署 VM 時所用的部署模型而有不同的做法。</span><span class="sxs-lookup"><span data-stu-id="6bab3-136">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="6bab3-137">如果 VM 是以「傳統」部署模型部署的，就必須移除雲端服務部署後再重新部署，才能將 VM 變更成另一個大小系列中的大小。</span><span class="sxs-lookup"><span data-stu-id="6bab3-137">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="6bab3-138">如果 VM 是以 Resource Manager 部署模型部署的，您就必須先停止可用性設定組中的所有 VM，才能變更該可用性設定組中任何 VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="6bab3-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="6bab3-139">部署在可用性設定組中時，不支援所列的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="6bab3-139">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="6bab3-140">請選擇可用性設定組叢集上支援的大小。</span><span class="sxs-lookup"><span data-stu-id="6bab3-140">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="6bab3-141">建議您在建立可用性設定組時，選擇您認為所需的最大 VM 大小，並且以它作為您的第一個可用性設定組部署項目。</span><span class="sxs-lookup"><span data-stu-id="6bab3-141">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="6bab3-142">Azure 上支援哪些 Linux 散發套件/版本？</span><span class="sxs-lookup"><span data-stu-id="6bab3-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="6bab3-143">您可以在[經 Azure 背書的散發套件](endorsed-distros.md)上找到 Linux 的清單。</span><span class="sxs-lookup"><span data-stu-id="6bab3-143">You can find the list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="6bab3-144">我是否可以將現有的傳統 VM 新增到可用性設定組？</span><span class="sxs-lookup"><span data-stu-id="6bab3-144">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="6bab3-145">是。</span><span class="sxs-lookup"><span data-stu-id="6bab3-145">Yes.</span></span> <span data-ttu-id="6bab3-146">您可以將現有的傳統 VM 新增到新的或現有的「可用性設定組」。</span><span class="sxs-lookup"><span data-stu-id="6bab3-146">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="6bab3-147">如需詳細資訊，請參閱[將現有的虛擬機器新增至可用性設定組](../windows/classic/configure-availability.md#addmachine)。</span><span class="sxs-lookup"><span data-stu-id="6bab3-147">For more information see [Add an existing virtual machine to an availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="6bab3-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bab3-148">Next steps</span></span>
<span data-ttu-id="6bab3-149">如果您在本文中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="6bab3-149">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="6bab3-150">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="6bab3-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="6bab3-151">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="6bab3-151">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
