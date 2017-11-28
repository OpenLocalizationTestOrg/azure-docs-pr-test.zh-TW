---
title: "部署在 Azure 中的 Linux 虛擬機器問題 aaaTroubleshoot |Microsoft 文件"
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
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="e8374-103">針對 Azure 中的 Linux 虛擬機器部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="e8374-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="e8374-104">tootroubleshoot 虛擬機器 (VM) 部署問題，在 Azure 中，檢閱 hello[排名最前面的問題](#top-issues)常見失敗和解決方式。</span><span class="sxs-lookup"><span data-stu-id="e8374-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="e8374-105">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="e8374-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e8374-106">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="e8374-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e8374-107">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="e8374-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="e8374-108">常見問題</span><span class="sxs-lookup"><span data-stu-id="e8374-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="e8374-109">無法支援 hello 叢集 hello 要求的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="e8374-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="e8374-110">重試 hello 要求使用較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="e8374-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="e8374-111">如果 hello hello 的大小會要求無法變更 VM:</span><span class="sxs-lookup"><span data-stu-id="e8374-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="e8374-112">停止 hello 可用性設定組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="e8374-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="e8374-113">按一下 [資源群組] > 您的資源群組 > [資源] > 您的可用性設定組 > [虛擬機器] > 您的虛擬機器 > [停止]。</span><span class="sxs-lookup"><span data-stu-id="e8374-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="e8374-114">在所有 hello Vm 停止，並建立 hello VM hello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="e8374-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="e8374-115">啟動第一次，hello 新的 VM，並選取每個 hello 停止 Vm，然後按一下 [開始]。</span><span class="sxs-lookup"><span data-stu-id="e8374-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="e8374-116">hello 叢集沒有可用的資源</span><span class="sxs-lookup"><span data-stu-id="e8374-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="e8374-117">稍後再重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="e8374-117">Retry hello request later.</span></span>
- <span data-ttu-id="e8374-118">如果 hello 新的 VM 可以屬於不同的可用性設定嗎</span><span class="sxs-lookup"><span data-stu-id="e8374-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="e8374-119">在不同的可用性設定組中建立 VM (hello 中相同的區域)。</span><span class="sxs-lookup"><span data-stu-id="e8374-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="e8374-120">加入新 VM toohello hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8374-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="e8374-121">我要如何啟用我的 Visual Studio Enterprise (BizSpark) 每月點數</span><span class="sxs-lookup"><span data-stu-id="e8374-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="e8374-122">tooactivate 您每月信用額度，請參閱此[文章](https://azure.microsoft.com/offers/ms-azr-0064p/)。</span><span class="sxs-lookup"><span data-stu-id="e8374-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="e8374-123">為什麼我不安裝 hello GPU 驅動程式為 Ubuntu NV VM？</span><span class="sxs-lookup"><span data-stu-id="e8374-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="e8374-124">目前，Linux GPU 支援僅適用於執行 Ubuntu Server 16.04 LTS 的 Azure NC VM。</span><span class="sxs-lookup"><span data-stu-id="e8374-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="e8374-125">如需詳細資訊，請參閱[為執行 Linux 的 N 系列 VM 設定 GPU 驅動程式](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="e8374-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="e8374-126">我的 Linux N 系列 VM 遺失驅動程式</span><span class="sxs-lookup"><span data-stu-id="e8374-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="e8374-127">Linux 型 VM 的驅動程式位於[這裡](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="e8374-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="e8374-128">在我的 N 系列 VM 內找不到 GPU 執行個體</span><span class="sxs-lookup"><span data-stu-id="e8374-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="e8374-129">tootake 利用 hello GPU 功能的 Azure N 系列 Vm 執行 Windows Server 2016 或 Windows Server 2012 R2，您必須安裝在每個 VM 上 NVIDIA 圖形驅動程式部署之後。</span><span class="sxs-lookup"><span data-stu-id="e8374-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="e8374-130">您可以取得 [Windows VM](../windows/n-series-driver-setup.md) 和 [Linux VM](n-series-driver-setup.md) 的驅動程式設定資訊。</span><span class="sxs-lookup"><span data-stu-id="e8374-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="e8374-131">我的區域是否有提供 N 系列 VM？</span><span class="sxs-lookup"><span data-stu-id="e8374-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="e8374-132">您可以檢查來自 hello 的 hello 可用性[產品依區域 」 資料表提供](https://azure.microsoft.com/regions/services)，和定價[這裡](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)。</span><span class="sxs-lookup"><span data-stu-id="e8374-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="e8374-133">我不能 toosee VM 大小系列我想要調整大小時我的 VM。</span><span class="sxs-lookup"><span data-stu-id="e8374-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="e8374-134">執行 VM 時，它會是已部署的 tooa 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="e8374-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="e8374-135">hello Azure 區域中的實體伺服器分組的常見的實體硬體的叢集。</span><span class="sxs-lookup"><span data-stu-id="e8374-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="e8374-136">調整大小需要 hello VM toobe 移動 toodifferent 硬體叢集的 VM 是哪一個部署模型所使用的 toodeploy hello VM 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e8374-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="e8374-137">在傳統部署模型，hello 雲端服務部署中部署 Vm 必須移除並重新部署在另一個大小家族 toochange hello Vm tooa 大小。</span><span class="sxs-lookup"><span data-stu-id="e8374-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="e8374-138">在資源管理員部署模型所部署的 Vm，您必須停止所有 Vm hello 可用性設定組之前變更 hello hello 可用性設定組中的任何 VM 大小中。</span><span class="sxs-lookup"><span data-stu-id="e8374-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="e8374-139">hello 列出的 VM 大小不支援同時將部署在可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="e8374-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="e8374-140">選擇 hello 可用性設定組的叢集支援的大小。</span><span class="sxs-lookup"><span data-stu-id="e8374-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="e8374-141">建議建立時的可用性集合 toochoose hello 最大 VM 大小您認為需要並且已是您第一種部署 toohello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="e8374-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="e8374-142">Azure 上支援哪些 Linux 散發套件/版本？</span><span class="sxs-lookup"><span data-stu-id="e8374-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="e8374-143">您可以找到 Linux 在 hello 清單[Azure-Endorsed 分佈](endorsed-distros.md)。</span><span class="sxs-lookup"><span data-stu-id="e8374-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="e8374-144">可以加入現有的傳統 VM tooan 可用性集嗎？</span><span class="sxs-lookup"><span data-stu-id="e8374-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="e8374-145">是。</span><span class="sxs-lookup"><span data-stu-id="e8374-145">Yes.</span></span> <span data-ttu-id="e8374-146">您可以加入現有傳統 VM tooa 新或現有的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="e8374-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="e8374-147">如需詳細資訊，請參閱[加入現有的虛擬機器 tooan 可用性集](../windows/classic/configure-availability.md#addmachine)。</span><span class="sxs-lookup"><span data-stu-id="e8374-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8374-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8374-148">Next steps</span></span>
<span data-ttu-id="e8374-149">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="e8374-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="e8374-150">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="e8374-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e8374-151">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="e8374-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
