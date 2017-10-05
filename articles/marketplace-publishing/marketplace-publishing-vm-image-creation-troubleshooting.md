---
title: "如何針對 VHD 建立常見問題進行疑難排解 | Microsoft Docs"
description: "VHD 建立常見疑難排解問題的解答。"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="3057a-103">如何針對 VHD 建立常見問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3057a-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="3057a-104">這篇文章可協助 Azure Marketplace 發行者和 (或) 共同管理員解決在發行或管理其虛擬機器解決方案時發生的問題或常見問題。</span><span class="sxs-lookup"><span data-stu-id="3057a-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="3057a-105">如何變更主機的名稱？</span><span class="sxs-lookup"><span data-stu-id="3057a-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="3057a-106">建立 VM 之後，使用者就無法更新主機的名稱。</span><span class="sxs-lookup"><span data-stu-id="3057a-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="3057a-107">如何重設遠端桌面服務或其登入密碼？</span><span class="sxs-lookup"><span data-stu-id="3057a-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="3057a-108">Windows VM 的參考</span><span class="sxs-lookup"><span data-stu-id="3057a-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="3057a-109">Linux VM 的參考</span><span class="sxs-lookup"><span data-stu-id="3057a-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="3057a-110">如何產生新 ssh 憑證？</span><span class="sxs-lookup"><span data-stu-id="3057a-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="3057a-111">請參閱連結：[https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="3057a-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="3057a-112">如何設定開放式 VPN 憑證？</span><span class="sxs-lookup"><span data-stu-id="3057a-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="3057a-113">請參閱連結：[https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="3057a-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="3057a-114">在 Microsoft Azure 虛擬機器環境中執行 Microsoft 伺服器軟體的支援原則為何 (infrastructure-as-a-service)？</span><span class="sxs-lookup"><span data-stu-id="3057a-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="3057a-115">請參閱連結：[https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="3057a-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="3057a-116">虛擬機器是否有任何唯一識別碼？</span><span class="sxs-lookup"><span data-stu-id="3057a-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="3057a-117">Azure 會編碼每個 VM 中的 Azure VM 唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="3057a-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="3057a-118">請參閱這個部落格和文件中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3057a-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="3057a-119">在 VM 中，如何在啟動工作中管理自訂指令碼延伸模組？</span><span class="sxs-lookup"><span data-stu-id="3057a-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="3057a-120">請參閱連結：[https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="3057a-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="3057a-121">如何使用上傳至進階儲存體的 VHD 從 Azure 入口網站建立 VM？</span><span class="sxs-lookup"><span data-stu-id="3057a-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="3057a-122">我們尚未支援這項功能。</span><span class="sxs-lookup"><span data-stu-id="3057a-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="3057a-123">Azure Marketplace 中是否支援 32 位元應用程式？</span><span class="sxs-lookup"><span data-stu-id="3057a-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="3057a-124">如需支援原則的詳細資料，請參閱連結︰[https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="3057a-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="3057a-125">每次嘗試從我的 VHD 建立映像時都會在 PowerShell 中收到錯誤「.VHD 已經在映像儲存機制上註冊為資源」。</span><span class="sxs-lookup"><span data-stu-id="3057a-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="3057a-126">我之前未建立任何映像，也在 Azure 中找不到任何具有這個名稱的映像。</span><span class="sxs-lookup"><span data-stu-id="3057a-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="3057a-127">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="3057a-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="3057a-128">如果使用者已從這個 VHD 佈建 VM，並且鎖定該 VHD，則通常會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="3057a-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="3057a-129">請確認未從這個 VHD 配置任何 VM。</span><span class="sxs-lookup"><span data-stu-id="3057a-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="3057a-130">如果錯誤仍然存在，則請使用這個連結或從發佈入口網站提出這個錯誤的支援票證 (第 11 個問題的答案會提供詳細資料)。</span><span class="sxs-lookup"><span data-stu-id="3057a-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>