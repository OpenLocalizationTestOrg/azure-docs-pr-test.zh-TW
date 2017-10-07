---
title: "新增 Azure Vm tooan 現有可用性設定組的 aaaSupportability |Microsoft 文件"
description: "新增 Azure Vm tooan 現有可用性設定組的支援能力。"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a><span data-ttu-id="e7167-103">新增 Azure Vm tooan 現有可用性設定組的支援能力</span><span class="sxs-lookup"><span data-stu-id="e7167-103">Supportability of adding Azure VMs tooan existing availability set</span></span>

<span data-ttu-id="e7167-104">當您新增新虛擬機器 (Vm) tooan 現有的可用性集合時，您可能偶爾會遇到限制。</span><span class="sxs-lookup"><span data-stu-id="e7167-104">You may occasionally encounter limitations when you add new virtual machines (VMs) tooan existing availability set.</span></span> <span data-ttu-id="e7167-105">hello 下列圖表中，您可以混合的 VM 系列 hello 相同可用性設定組的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e7167-105">hello following chart details which VM series you can mix in hello same availability set.</span></span>

<span data-ttu-id="e7167-106">以下是 hello 可支援性矩陣 toomix 不同類型的 Vm:</span><span class="sxs-lookup"><span data-stu-id="e7167-106">Here is hello supportability matrix toomix different types of VMs:</span></span>

<span data-ttu-id="e7167-107">系列與可用性設定組</span><span class="sxs-lookup"><span data-stu-id="e7167-107">Series & Availability Set</span></span>|<span data-ttu-id="e7167-108">第二部 VM</span><span class="sxs-lookup"><span data-stu-id="e7167-108">Second VM</span></span>|<span data-ttu-id="e7167-109">具有使用 </span><span class="sxs-lookup"><span data-stu-id="e7167-109">A</span></span>|<span data-ttu-id="e7167-110">Av2</span><span class="sxs-lookup"><span data-stu-id="e7167-110">Av2</span></span>|<span data-ttu-id="e7167-111">D</span><span class="sxs-lookup"><span data-stu-id="e7167-111">D</span></span>|<span data-ttu-id="e7167-112">Dv2</span><span class="sxs-lookup"><span data-stu-id="e7167-112">Dv2</span></span>|<span data-ttu-id="e7167-113">Dv3</span><span class="sxs-lookup"><span data-stu-id="e7167-113">Dv3</span></span>|
|---|---|---|---|---|---|---|
|<span data-ttu-id="e7167-114">第一部 VM</span><span class="sxs-lookup"><span data-stu-id="e7167-114">First VM</span></span>|||||||
|<span data-ttu-id="e7167-115">具有使用 </span><span class="sxs-lookup"><span data-stu-id="e7167-115">A</span></span>||<span data-ttu-id="e7167-116">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-116">OK</span></span>|<span data-ttu-id="e7167-117">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-117">OK</span></span>|<span data-ttu-id="e7167-118">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-118">OK</span></span>|<span data-ttu-id="e7167-119">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-119">OK</span></span>|<span data-ttu-id="e7167-120">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-120">OK</span></span>|
|<span data-ttu-id="e7167-121">Av2</span><span class="sxs-lookup"><span data-stu-id="e7167-121">Av2</span></span>||<span data-ttu-id="e7167-122">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-122">OK</span></span>|<span data-ttu-id="e7167-123">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-123">OK</span></span>|<span data-ttu-id="e7167-124">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-124">OK</span></span>|<span data-ttu-id="e7167-125">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-125">OK</span></span>|<span data-ttu-id="e7167-126">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-126">OK</span></span>|
|<span data-ttu-id="e7167-127">D</span><span class="sxs-lookup"><span data-stu-id="e7167-127">D</span></span>||<span data-ttu-id="e7167-128">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-128">OK</span></span>|<span data-ttu-id="e7167-129">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-129">OK</span></span>|<span data-ttu-id="e7167-130">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-130">OK</span></span>|<span data-ttu-id="e7167-131">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-131">OK</span></span>|<span data-ttu-id="e7167-132">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-132">OK</span></span>|
|<span data-ttu-id="e7167-133">Dv2</span><span class="sxs-lookup"><span data-stu-id="e7167-133">Dv2</span></span>||<span data-ttu-id="e7167-134">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-134">OK</span></span>|<span data-ttu-id="e7167-135">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-135">OK</span></span>|<span data-ttu-id="e7167-136">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-136">OK</span></span>|<span data-ttu-id="e7167-137">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-137">OK</span></span>|<span data-ttu-id="e7167-138">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-138">OK</span></span>|
|<span data-ttu-id="e7167-139">Dv3</span><span class="sxs-lookup"><span data-stu-id="e7167-139">Dv3</span></span>||<span data-ttu-id="e7167-140">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-140">OK</span></span>|<span data-ttu-id="e7167-141">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-141">OK</span></span>|<span data-ttu-id="e7167-142">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-142">OK</span></span>|<span data-ttu-id="e7167-143">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-143">OK</span></span>|<span data-ttu-id="e7167-144">OK</span><span class="sxs-lookup"><span data-stu-id="e7167-144">OK</span></span>|

<span data-ttu-id="e7167-145">在相同可用性設定組，因為它們需要特定硬體的 hello 中找不到其他所有數列。</span><span class="sxs-lookup"><span data-stu-id="e7167-145">All other series could not be in hello same availability set because they require a specific hardware.</span></span>
