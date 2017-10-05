---
title: "比較 DevTest Labs 中的自訂映像和公式 | Microsoft Docs"
description: "了解自訂映像與作為 VM 基礎的公式之間的差異，以決定哪一個最適合您的環境。"
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
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="ff2a2-103">比較研發/測試實驗室中的自訂映像和公式</span><span class="sxs-lookup"><span data-stu-id="ff2a2-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="ff2a2-104">[自訂映像](devtest-lab-create-template.md)和[公式](devtest-lab-manage-formulas.md)可以當作[建立新 VM](devtest-lab-add-vm-with-artifacts.md) 的基礎。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="ff2a2-105">不過，自訂映像與公式的主要差別在於自訂映像只是根據 VHD 的映像，而公式是根據 VHD 的映像以及具有預先設定的設定 (例如 VM 大小、虛擬網路、子網路及構件)。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="ff2a2-106">這些預先設定的設定是使用預設值所設定，並且可以在建立 VM 時予以覆寫。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="ff2a2-107">本文說明使用自訂映像與使用公式的一些優缺點。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="ff2a2-108">自訂映像的優缺點</span><span class="sxs-lookup"><span data-stu-id="ff2a2-108">Custom image pros and cons</span></span>
<span data-ttu-id="ff2a2-109">自訂映像提供靜態、不可變的方式，從所需的環境中建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="ff2a2-110">**優點**</span><span class="sxs-lookup"><span data-stu-id="ff2a2-110">**Pros**</span></span>

* <span data-ttu-id="ff2a2-111">從自訂映像進行的 VM 佈建，與從映像啟動 VM 後未進行任何變更一樣地快速。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="ff2a2-112">換句話說，因為自訂映像就是沒有設定的映像，所以不需要套用任何設定。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="ff2a2-113">從單一自訂映像建立的 VM 都相同。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="ff2a2-114">**缺點**</span><span class="sxs-lookup"><span data-stu-id="ff2a2-114">**Cons**</span></span>

* <span data-ttu-id="ff2a2-115">如果您需要更新自訂映像的某些部分，就必須重新建立映像。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="ff2a2-116">公式的優缺點</span><span class="sxs-lookup"><span data-stu-id="ff2a2-116">Formula pros and cons</span></span>
<span data-ttu-id="ff2a2-117">公式提供動態方式，透過所需的組態/設定來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="ff2a2-118">**優點**</span><span class="sxs-lookup"><span data-stu-id="ff2a2-118">**Pros**</span></span>

* <span data-ttu-id="ff2a2-119">透過構件可以即時擷取環境中的變更。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="ff2a2-120">例如，如果您想要已安裝發行管線的最新位元的 VM，或登錄儲存機制中的最新程式碼，只需要指定構件，這個構件部署最新位元，或登錄與目標基本映像一起的公式中的最新程式碼。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="ff2a2-121">只要使用此公式建立 VM，就會將最新位元/程式碼部署/登錄至 VM。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="ff2a2-122">公式可以定義自訂映像無法提供的預設設定 (例如 VM 大小和虛擬網路設定)。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="ff2a2-123">公式中所儲存的設定會顯示為預設值，但是可以在建立 VM 時進行修改。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="ff2a2-124">**缺點**</span><span class="sxs-lookup"><span data-stu-id="ff2a2-124">**Cons**</span></span>

* <span data-ttu-id="ff2a2-125">透過公式建立 VM 所需的時間多於透過自訂映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ff2a2-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="ff2a2-126">相關部落格文章</span><span class="sxs-lookup"><span data-stu-id="ff2a2-126">Related blog posts</span></span>
* [<span data-ttu-id="ff2a2-127">自訂映像或公式？</span><span class="sxs-lookup"><span data-stu-id="ff2a2-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="ff2a2-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff2a2-128">Next steps</span></span>
- [<span data-ttu-id="ff2a2-129">DevTest Labs 常見問題集</span><span class="sxs-lookup"><span data-stu-id="ff2a2-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)