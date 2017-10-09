---
title: "部署 Windows Azure 中的虛擬機器問題 aaaTroubleshoot |Microsoft 文件"
description: "針對 Azure Resource Manager 部署模型中的 Windows 虛擬機器部署問題進行疑難排解。"
services: virtual-machines-windows
documentationcenter: 
author: genlin
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="288b6-103">針對 Azure 中的 Windows 虛擬機器部署問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="288b6-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="288b6-104">tootroubleshoot 虛擬機器 (VM) 部署問題，在 Azure 中，檢閱 hello[排名最前面的問題](#top-issues)常見失敗和解決方式。</span><span class="sxs-lookup"><span data-stu-id="288b6-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="288b6-105">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="288b6-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="288b6-106">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="288b6-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="288b6-107">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="288b6-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="288b6-108">常見問題</span><span class="sxs-lookup"><span data-stu-id="288b6-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="288b6-109">無法支援 hello 叢集 hello 要求的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="288b6-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="288b6-110">重試 hello 要求使用較小的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="288b6-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="288b6-111">如果 hello hello 的大小會要求無法變更 VM:</span><span class="sxs-lookup"><span data-stu-id="288b6-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="288b6-112">停止 hello 可用性設定組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="288b6-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="288b6-113">按一下 [資源群組] > 您的資源群組 > [資源] > 您的可用性設定組 > [虛擬機器] > 您的虛擬機器 > [停止]。</span><span class="sxs-lookup"><span data-stu-id="288b6-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="288b6-114">在所有 hello Vm 停止，並建立 hello VM hello 預期大小。</span><span class="sxs-lookup"><span data-stu-id="288b6-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="288b6-115">啟動第一次，hello 新的 VM，並選取每個 hello 停止 Vm，然後按一下 [開始]。</span><span class="sxs-lookup"><span data-stu-id="288b6-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="288b6-116">hello 叢集沒有可用的資源</span><span class="sxs-lookup"><span data-stu-id="288b6-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="288b6-117">稍後再重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="288b6-117">Retry hello request later.</span></span>
- <span data-ttu-id="288b6-118">如果 hello 新的 VM 可以屬於不同的可用性設定嗎</span><span class="sxs-lookup"><span data-stu-id="288b6-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="288b6-119">在不同的可用性設定組中建立 VM (hello 中相同的區域)。</span><span class="sxs-lookup"><span data-stu-id="288b6-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="288b6-120">加入新 VM toohello hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="288b6-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="288b6-121">我要如何使用 Windows 用戶端映像並將其部署到 Azure 中？</span><span class="sxs-lookup"><span data-stu-id="288b6-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="288b6-122">如果您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 來進行開發/測試案例。</span><span class="sxs-lookup"><span data-stu-id="288b6-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="288b6-123">這[文章](client-images.md)外框 hello 中 Azure，並使用 hello Azure 資源庫映像執行 Windows 用戶端資格需求。</span><span class="sxs-lookup"><span data-stu-id="288b6-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="288b6-124">如何部署虛擬機器使用 hello 混合使用權益 （集線器）？</span><span class="sxs-lookup"><span data-stu-id="288b6-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="288b6-125">有幾個不同的方式以 hello Azure 混合式使用權益 toodeploy Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="288b6-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="288b6-126">針對 Enterprise 合約訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="288b6-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="288b6-127">•   從已使用 Azure Hybrid Use Benefit 來預先設定的特定 Marketplace 映象部署 VM。</span><span class="sxs-lookup"><span data-stu-id="288b6-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="288b6-128">針對 Enterprise 合約：</span><span class="sxs-lookup"><span data-stu-id="288b6-128">For Enterprise agreement:</span></span>

<span data-ttu-id="288b6-129">•   上傳自訂的 VM 並使用 Resource Manager 範本或 Azure PowerShell 來進行部署。</span><span class="sxs-lookup"><span data-stu-id="288b6-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="288b6-130">如需詳細資訊，請參閱下列資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="288b6-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="288b6-131">Azure Hybrid Use Benefit 概觀</span><span class="sxs-lookup"><span data-stu-id="288b6-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - <span data-ttu-id="288b6-132">[可下載的常見問題集](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf) \(英文\)</span><span class="sxs-lookup"><span data-stu-id="288b6-132">[Downloadable FAQ](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)</span></span>

 - <span data-ttu-id="288b6-133">[適用於 Windows Server 和 Windows 用戶端的 Azure Hybrid Use Benefit](hybrid-use-benefit-licensing.md)。</span><span class="sxs-lookup"><span data-stu-id="288b6-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="288b6-134">如何使用 Azure 中的 hello 混合使用好處</span><span class="sxs-lookup"><span data-stu-id="288b6-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="288b6-135">我要如何啟用我的 Visual Studio Enterprise (BizSpark) 每月點數</span><span class="sxs-lookup"><span data-stu-id="288b6-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="288b6-136">tooactivate 您每月信用額度，請參閱此[文章](https://azure.microsoft.com/offers/ms-azr-0064p/)。</span><span class="sxs-lookup"><span data-stu-id="288b6-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="288b6-137">如何 tooadd 企業開發/測試 toomy Enterprise 合約 (EA) tooget 存取 tooWindow 用戶端映像？</span><span class="sxs-lookup"><span data-stu-id="288b6-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="288b6-138">hello 能力 toocreate hello 企業開發/測試為基礎的訂用帳戶提供的是受限制的 tooAccount 擁有者獲得權限 toodo 是由企業系統管理員。</span><span class="sxs-lookup"><span data-stu-id="288b6-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="288b6-139">hello 帳戶擁有者建立 hello Azure 帳戶入口網站，透過訂閱，然後再應該加入為共同管理員作用中的 Visual Studio 訂閱者。</span><span class="sxs-lookup"><span data-stu-id="288b6-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="288b6-140">使他們可以管理和使用 hello 資源所需的開發和測試。</span><span class="sxs-lookup"><span data-stu-id="288b6-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="288b6-141">如需詳細資訊，請參閱 [Enterprise 開發/測試](https://azure.microsoft.com/offers/ms-azr-0148p/)。</span><span class="sxs-lookup"><span data-stu-id="288b6-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="288b6-142">我的 Windows N 系列 VM 遺失驅動程式</span><span class="sxs-lookup"><span data-stu-id="288b6-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="288b6-143">Windows 型 VM 的驅動程式位於[這裡](n-series-driver-setup.md)。</span><span class="sxs-lookup"><span data-stu-id="288b6-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="288b6-144">在我的 N 系列 VM 內找不到 GPU 執行個體</span><span class="sxs-lookup"><span data-stu-id="288b6-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="288b6-145">tootake 利用 hello GPU 功能的 Azure N 系列 Vm 執行 Windows Server 2016 或 Windows Server 2012 R2，您必須安裝在每個 VM 上 NVIDIA 圖形驅動程式部署之後。</span><span class="sxs-lookup"><span data-stu-id="288b6-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="288b6-146">您可以取得 [Windows VM](n-series-driver-setup.md) 和 [Linux VM](../linux/n-series-driver-setup.md) 的驅動程式設定資訊。</span><span class="sxs-lookup"><span data-stu-id="288b6-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="288b6-147">是否支援 N 系列的用戶端映像？</span><span class="sxs-lookup"><span data-stu-id="288b6-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="288b6-148">目前 Azure 僅支援執行 Windows Server 和 Linux 作業系統之 VM 上的 N 系列。</span><span class="sxs-lookup"><span data-stu-id="288b6-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="288b6-149">我的區域是否有提供 N 系列 VM？</span><span class="sxs-lookup"><span data-stu-id="288b6-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="288b6-150">您可以檢查來自 hello 的 hello 可用性[產品依區域 」 資料表提供](https://azure.microsoft.com/regions/services)，和定價[這裡](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series)。</span><span class="sxs-lookup"><span data-stu-id="288b6-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="288b6-151">哪些用戶端映像使用和部署在 Azure 和 tooI 如何取得它們？</span><span class="sxs-lookup"><span data-stu-id="288b6-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="288b6-152">假設您有適當的 Visual Studio (先前稱為 MSDN) 訂用帳戶，您可以在 Azure 中使用 Windows 7、Windows 8 或 Windows 10 進行開發/測試案例。</span><span class="sxs-lookup"><span data-stu-id="288b6-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="288b6-153">Windows 10 映像可供從 hello Azure 組件庫內[適合開發/測試提供](client-images.md#eligible-offers)。</span><span class="sxs-lookup"><span data-stu-id="288b6-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="288b6-154">提供項目的任何型別中的 visual Studio 訂閱者也可以[可以充分地準備及建立](prepare-for-upload-vhd-image.md)64 位元 Windows 7、 Windows 8 或 Windows 10 映像，然後[上載 tooAzure](upload-generalized-managed.md)。</span><span class="sxs-lookup"><span data-stu-id="288b6-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="288b6-155">hello 使用仍有限的 toodev/測試的方法是使用 Visual Studio 的 「 訂閱者 」。</span><span class="sxs-lookup"><span data-stu-id="288b6-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="288b6-156">這[文章](client-images.md)外框 hello 在 Azure 中並使用 hello 的 Azure 資源庫映像執行 Windows 用戶端資格需求。</span><span class="sxs-lookup"><span data-stu-id="288b6-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="288b6-157">我不能 toosee VM 大小系列我想要調整大小時我的 VM。</span><span class="sxs-lookup"><span data-stu-id="288b6-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="288b6-158">執行 VM 時，它會是已部署的 tooa 實體伺服器。</span><span class="sxs-lookup"><span data-stu-id="288b6-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="288b6-159">hello Azure 區域中的實體伺服器分組的常見的實體硬體的叢集。</span><span class="sxs-lookup"><span data-stu-id="288b6-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="288b6-160">調整大小需要 hello VM toobe 移動 toodifferent 硬體叢集的 VM 是哪一個部署模型所使用的 toodeploy hello VM 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="288b6-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="288b6-161">在傳統部署模型，hello 雲端服務部署中部署 Vm 必須移除並重新部署在另一個大小家族 toochange hello Vm tooa 大小。</span><span class="sxs-lookup"><span data-stu-id="288b6-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="288b6-162">在資源管理員部署模型所部署的 Vm，您必須停止所有 Vm hello 可用性設定組之前變更 hello hello 可用性設定組中的任何 VM 大小中。</span><span class="sxs-lookup"><span data-stu-id="288b6-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="288b6-163">hello 列出的 VM 大小不支援同時將部署在可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="288b6-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="288b6-164">選擇 hello 可用性設定組的叢集支援的大小。</span><span class="sxs-lookup"><span data-stu-id="288b6-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="288b6-165">建議建立時的可用性集合 toochoose hello 最大 VM 大小您認為需要並且已是您第一種部署 toohello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="288b6-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="288b6-166">可以加入現有的傳統 VM tooan 可用性集嗎？</span><span class="sxs-lookup"><span data-stu-id="288b6-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="288b6-167">是。</span><span class="sxs-lookup"><span data-stu-id="288b6-167">Yes.</span></span> <span data-ttu-id="288b6-168">您可以加入現有傳統 VM tooa 新或現有的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="288b6-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="288b6-169">如需詳細資訊，請參閱[加入現有的虛擬機器 tooan 可用性集](classic/configure-availability.md#addmachine)。</span><span class="sxs-lookup"><span data-stu-id="288b6-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="288b6-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="288b6-170">Next steps</span></span>
<span data-ttu-id="288b6-171">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="288b6-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="288b6-172">或者，您可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="288b6-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="288b6-173">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="288b6-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
