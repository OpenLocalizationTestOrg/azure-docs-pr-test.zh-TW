---
title: "aaaComparing 自訂映像中的和公式 DevTest Labs |Microsoft 文件"
description: "了解 hello 之間差異的自訂映像和公式為 VM 基底，讓您可以決定哪一種最適合您的環境。"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="73a6d-103">比較研發/測試實驗室中的自訂映像和公式</span><span class="sxs-lookup"><span data-stu-id="73a6d-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="73a6d-104">[自訂映像](devtest-lab-create-template.md)和[公式](devtest-lab-manage-formulas.md)可以當作[建立新 VM](devtest-lab-add-vm-with-artifacts.md) 的基礎。</span><span class="sxs-lookup"><span data-stu-id="73a6d-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="73a6d-105">不過，hello 金鑰區別自訂映像和公式是自訂映像是只根據 VHD，而公式會根據 VHD 映像的映像*除了*預先設定的 VM 大小，虛擬網路，例如子網路和成品。</span><span class="sxs-lookup"><span data-stu-id="73a6d-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="73a6d-106">這些預先設定的設定會設定使用會覆寫 hello VM 建立時的預設值。</span><span class="sxs-lookup"><span data-stu-id="73a6d-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="73a6d-107">這篇文章會說明一些 hello 優點 （專業人員適用），和缺點 (cons) toousing 自訂映像與使用公式。</span><span class="sxs-lookup"><span data-stu-id="73a6d-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="73a6d-108">自訂映像的優缺點</span><span class="sxs-lookup"><span data-stu-id="73a6d-108">Custom image pros and cons</span></span>
<span data-ttu-id="73a6d-109">自訂映像可讓靜態的、 不可變的方式 toocreate Vm 所需的環境。</span><span class="sxs-lookup"><span data-stu-id="73a6d-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="73a6d-110">**優點**</span><span class="sxs-lookup"><span data-stu-id="73a6d-110">**Pros**</span></span>

* <span data-ttu-id="73a6d-111">保持不變 hello VM 調整大小之後從 hello 映像，可快速 VM 佈建的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="73a6d-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="73a6d-112">換句話說，任何設定 tooapply hello 自訂映像的影像沒有設定現況。</span><span class="sxs-lookup"><span data-stu-id="73a6d-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="73a6d-113">從單一自訂映像建立的 VM 都相同。</span><span class="sxs-lookup"><span data-stu-id="73a6d-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="73a6d-114">**缺點**</span><span class="sxs-lookup"><span data-stu-id="73a6d-114">**Cons**</span></span>

* <span data-ttu-id="73a6d-115">如果您需要 tooupdate hello 自訂映像的某些層面，就必須重新建立 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="73a6d-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="73a6d-116">公式的優缺點</span><span class="sxs-lookup"><span data-stu-id="73a6d-116">Formula pros and cons</span></span>
<span data-ttu-id="73a6d-117">公式可動態方式 toocreate Vm 所需的 hello/設定。</span><span class="sxs-lookup"><span data-stu-id="73a6d-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="73a6d-118">**優點**</span><span class="sxs-lookup"><span data-stu-id="73a6d-118">**Pros**</span></span>

* <span data-ttu-id="73a6d-119">可以透過成品 hello 立即擷取 hello 環境中的變更。</span><span class="sxs-lookup"><span data-stu-id="73a6d-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="73a6d-120">例如，如果您想從您的發行管線 hello 最新的位元安裝的 VM，或從您的儲存機制登錄 hello 最新的程式碼，您可以只指定部署 hello 最新的 bits 或登記 hello 搭配 hello 公式中的最新程式碼的成品目標基底映像。</span><span class="sxs-lookup"><span data-stu-id="73a6d-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="73a6d-121">此公式會使用的 toocreate Vm，每當有部署/編列 toohello VM hello 最新的位元/程式碼。</span><span class="sxs-lookup"><span data-stu-id="73a6d-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="73a6d-122">公式可以定義自訂映像無法提供的預設設定 (例如 VM 大小和虛擬網路設定)。</span><span class="sxs-lookup"><span data-stu-id="73a6d-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="73a6d-123">儲存在公式中的 hello 設定為預設值，會顯示，而 hello VM 建立時可以修改。</span><span class="sxs-lookup"><span data-stu-id="73a6d-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="73a6d-124">**缺點**</span><span class="sxs-lookup"><span data-stu-id="73a6d-124">**Cons**</span></span>

* <span data-ttu-id="73a6d-125">透過公式建立 VM 所需的時間多於透過自訂映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="73a6d-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="73a6d-126">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="73a6d-126">Related blog posts</span></span>
* [<span data-ttu-id="73a6d-127">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="73a6d-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="73a6d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73a6d-128">Next steps</span></span>
- [<span data-ttu-id="73a6d-129">DevTest Labs 常見問題集</span><span class="sxs-lookup"><span data-stu-id="73a6d-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)