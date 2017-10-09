---
title: "關於 Azure IaaS VM 磁碟的常見問題集 (FAQ) | Microsoft Docs"
description: "關於 Azure IaaS VM 磁碟和進階磁碟 (受控和非受控) 的常見問題集"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="e4fc8-103">關於 Azure IaaS VM 磁碟及受控和非受控進階磁碟的常見問題集</span><span class="sxs-lookup"><span data-stu-id="e4fc8-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="e4fc8-104">此文章將回答有關 Azure 受控磁碟和 Azure 進階儲存體的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="e4fc8-105">受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e4fc8-105">Managed Disks</span></span>

<span data-ttu-id="e4fc8-106">**何謂 Azure 受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="e4fc8-107">受控磁碟是可以為您管理儲存體帳戶而簡化 Azure IaaS VM 磁碟管理的一項功能。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="e4fc8-108">如需詳細資訊，請參閱 hello[管理磁碟概觀](storage-managed-disks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="e4fc8-109">**如果我從現有的 VHD (大小為 80 GB) 建立標準受控磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="e4fc8-110">80 GB VHD 從建立標準受管理的磁碟視為與 hello 下一個可用的標準磁碟大小，也就是 S10 磁碟相同。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="e4fc8-111">相應 toohello S10 磁碟價格收費。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="e4fc8-112">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e4fc8-113">**標準受控磁碟有任何交易成本嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="e4fc8-114">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-114">Yes.</span></span> <span data-ttu-id="e4fc8-115">我們會根據每一筆交易向您收費。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-115">You're charged for each transaction.</span></span> <span data-ttu-id="e4fc8-116">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e4fc8-117">**標準的受管理磁碟要收費 hello hello hello 磁碟資料的實際大小或佈建的 hello hello 磁碟容量？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="e4fc8-118">收費根據佈建的 hello hello 磁碟容量。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="e4fc8-119">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e4fc8-120">**進階受控磁碟和非受控磁碟的價格有何不同？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="e4fc8-121">hello 定價的受管理的高階磁碟是 hello 與未受管理的高階磁碟相同。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="e4fc8-122">**可以變更 hello 儲存體帳戶類型 （Standard 或 Premium） 的 我的受管理磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="e4fc8-123">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-123">Yes.</span></span> <span data-ttu-id="e4fc8-124">您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 變更 hello 儲存體帳戶類型的受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="e4fc8-125">**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="e4fc8-126">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-126">Yes.</span></span> <span data-ttu-id="e4fc8-127">您可以使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI 匯出受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="e4fc8-128">**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案與不同的訂用帳戶嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="e4fc8-129">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-129">No.</span></span>

<span data-ttu-id="e4fc8-130">**可以使用 Azure 儲存體帳戶 toocreate 受管理磁碟的 VHD 檔案位於不同的區域嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="e4fc8-131">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-131">No.</span></span>

<span data-ttu-id="e4fc8-132">**客戶使用受控磁碟時是否有任何規模限制？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="e4fc8-133">受管理的磁碟排除 hello 限制與儲存體帳戶相關聯。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="e4fc8-134">不過，每個訂閱受管理的磁碟的 hello 數目為有限的 too2，根據預設 000。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="e4fc8-135">您可以呼叫支援 tooincrease 這個數字。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="e4fc8-136">**我是否可以建立受控磁碟的增量快照集？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="e4fc8-137">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-137">No.</span></span> <span data-ttu-id="e4fc8-138">hello 目前的快照集功能可讓受管理磁碟的完整複本。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="e4fc8-139">不過，我們正計劃在未來的 hello toosupport 增量快照。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="e4fc8-140">**可用性設定組中的 VM 是否可以由受控和非受控磁碟混合組成？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="e4fc8-141">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-141">No.</span></span> <span data-ttu-id="e4fc8-142">所有受管理的磁碟或未受管理的所有磁碟，必須使用可用性設定組中的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="e4fc8-143">當您建立可用性設定組時，您可以選擇哪一種磁碟想 toouse。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="e4fc8-144">**管理磁碟 hello 預設選項處於 hello Azure 入口網站？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="e4fc8-145">目前不可以，但是它會變成 hello 預設，在未來的 hello。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="e4fc8-146">**我是否可以建立空的受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="e4fc8-147">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-147">Yes.</span></span> <span data-ttu-id="e4fc8-148">您可以建立空的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-148">You can create an empty disk.</span></span> <span data-ttu-id="e4fc8-149">受管理的磁碟可以建立獨立 VM，比方說，而不用附加它 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="e4fc8-150">**什麼是支援的 hello 容錯網域計數的可用性設定組來使用受管理磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="e4fc8-151">依據 hello hello 可用性設定組來使用受管理磁碟所在的地區，hello 支援容錯網域計數是 2 或 3。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="e4fc8-152">**如何為 hello 診斷設定的標準儲存體帳戶？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="e4fc8-153">您需要為 VM 診斷設定私人儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="e4fc8-154">我們計劃在未來的 hello，tooswitch 診斷也 tooManaged 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="e4fc8-155">**受控磁碟適用何種角色型存取控制支援？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="e4fc8-156">受控磁碟支援三個主要預設角色︰</span><span class="sxs-lookup"><span data-stu-id="e4fc8-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="e4fc8-157">擁有者：可以管理所有項目，包括存取</span><span class="sxs-lookup"><span data-stu-id="e4fc8-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="e4fc8-158">參與者：可以管理存取以外的所有項目</span><span class="sxs-lookup"><span data-stu-id="e4fc8-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="e4fc8-159">讀取者：可以檢視所有項目，但是無法進行變更</span><span class="sxs-lookup"><span data-stu-id="e4fc8-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="e4fc8-160">**有我可以複製或匯出受管理的磁碟 tooa 私人儲存體帳戶的方法嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="e4fc8-161">您可以取得 toocopy hello 內容 tooa 私用儲存體帳戶或內部部署儲存體的唯讀共用的存取簽章 URI hello 管理磁碟，並使用它。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="e4fc8-162">**我是否可以建立受控磁碟的複本？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="e4fc8-163">客戶可以擷取受管理的磁碟的快照，然後再使用 hello 快照 toocreate 受管理的另一個磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="e4fc8-164">**是否仍然支援非受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="e4fc8-165">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-165">Yes.</span></span> <span data-ttu-id="e4fc8-166">我們支援受控磁碟和非受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="e4fc8-167">我們建議您針對新的工作負載使用受管理的磁碟，並移轉您目前的工作負載 toomanaged 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="e4fc8-168">**如果我建立 128 GB 的磁碟，然後再增加 hello 大小 too130 GB，將我支付 hello 下一個磁碟的大小 (512 GB)？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="e4fc8-169">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-169">Yes.</span></span>

<span data-ttu-id="e4fc8-170">**我是否可以建立本地備援儲存體、異地備援儲存體和區域備援儲存體受控磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="e4fc8-171">Azure 受控磁碟目前只支援本地備援儲存體受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="e4fc8-172">**我是否可以壓縮受控磁碟或縮減其大小？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="e4fc8-173">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-173">No.</span></span> <span data-ttu-id="e4fc8-174">目前不受支援此功能。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="e4fc8-175">**當特殊的 （不使用 hello 系統準備工具所建立或一般化） 操作系統磁碟使用的 tooprovision VM 可以變更 hello 電腦 name 屬性嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="e4fc8-176">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-176">No.</span></span> <span data-ttu-id="e4fc8-177">您無法更新 hello 電腦名稱 屬性。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-177">You can't update hello computer name property.</span></span> <span data-ttu-id="e4fc8-178">hello 新的 VM 會繼承它 hello 父 VM，這是使用的 toocreate hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="e4fc8-179">**哪裡可以找到範例 Azure Resource Manager 範本 toocreate 與受管理磁碟 Vm？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="e4fc8-180">使用受控磁碟的範本清單</span><span class="sxs-lookup"><span data-stu-id="e4fc8-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="e4fc8-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="e4fc8-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="e4fc8-182">受控磁碟和儲存體服務加密</span><span class="sxs-lookup"><span data-stu-id="e4fc8-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="e4fc8-183">**當我建立受控磁碟時，依預設是否啟用 Azure 儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="e4fc8-184">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-184">Yes.</span></span>

<span data-ttu-id="e4fc8-185">**使用者管理 hello 加密金鑰？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="e4fc8-186">Microsoft 會管理 hello 加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="e4fc8-187">**我是否可以停用受控磁碟的儲存體服務加密？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="e4fc8-188">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-188">No.</span></span>

<span data-ttu-id="e4fc8-189">**儲存體服務加密是否僅供特定地區使用？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="e4fc8-190">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-190">No.</span></span> <span data-ttu-id="e4fc8-191">它提供了管理磁碟可使用的所有 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="e4fc8-192">受控磁碟在所有公開區域和德國都有提供。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="e4fc8-193">**如何查看我的受控磁碟是否加密？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="e4fc8-194">您可以找出 hello hello Azure 入口網站、 hello Azure CLI 和 PowerShell 從受管理的磁碟建立時的時間。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="e4fc8-195">如果 hello 時間之後 2017 年 6 月 9，便會加密您的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="e4fc8-196">**如何加密我在 2017 年 6 月 10 日之前建立的現有磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="e4fc8-197">自 2017 年 6 月 10 寫入 tooexisting 管理磁碟的新資料會自動加密。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="e4fc8-198">我們也想要規劃 tooencrypt 現有的資料，並在 hello 背景中將會以非同步方式發生 hello 加密。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="e4fc8-199">如果您現在必須加密現有資料，請建立一份磁碟複本。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="e4fc8-200">新的磁碟將會加密。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="e4fc8-201">使用 Azure CLI hello 複製受管理的磁碟</span><span class="sxs-lookup"><span data-stu-id="e4fc8-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="e4fc8-202">使用 PowerShell 複製受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e4fc8-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e4fc8-203">**受管理的快照集和映像是否加密？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="e4fc8-204">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-204">Yes.</span></span> <span data-ttu-id="e4fc8-205">2017 年 6 月 9 日後建立之所有受管理的快照集和映像都將自動加密。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="e4fc8-206">**可以轉換 Vm 與位於儲存體帳戶，或已 toomanaged 先前加密的磁碟的 unmanaged 磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="e4fc8-207">是</span><span class="sxs-lookup"><span data-stu-id="e4fc8-207">Yes</span></span>

<span data-ttu-id="e4fc8-208">**從受控磁碟或快照集匯出的 VHD 是否也會加密？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="e4fc8-209">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-209">No.</span></span> <span data-ttu-id="e4fc8-210">但如果您匯出 VHD tooan 加密的加密受管理的磁碟或快照集，儲存體帳戶，然後它會加密。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="e4fc8-211">進階磁碟：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="e4fc8-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="e4fc8-212">**如果 VM 使用的大小系列支援進階儲存體，例如 DSv2，我是否可以同時連結進階和標準資料磁碟？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="e4fc8-213">是。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-213">Yes.</span></span>

<span data-ttu-id="e4fc8-214">**可以附加 premium 和 standard 磁碟 tooa 大小之資料數列不支援進階儲存體，例如 D、 Dv2、 G 或 F 數列嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="e4fc8-215">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-215">No.</span></span> <span data-ttu-id="e4fc8-216">您可以附加只標準資料磁碟 tooVMs 針對未使用支援進階儲存體大小數列。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="e4fc8-217">**如果我從現有的 VHD (大小為 80 GB) 建立進階資料磁碟，需要多少費用？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="e4fc8-218">80 GB VHD 從建立高階資料磁碟會被視為 hello 下一個可用的 premium 磁碟大小，也就是 P10 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="e4fc8-219">相應 toohello P10 磁碟價格收費。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="e4fc8-220">**是否有交易成本 toouse 高階儲存體？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="e4fc8-221">依 IOPS 和輸送量的特定限制而佈建的每個磁碟大小，都有固定成本。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="e4fc8-222">hello 其他成本包含傳出的頻寬和快照集的容量，如果適用的話。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="e4fc8-223">如需詳細資訊，請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/storage)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e4fc8-224">**IOPS 及輸送量我可以從 hello 磁碟快取中取得的 hello 限制有哪些？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="e4fc8-225">hello 結合的限制快取和本機 SSD DS 系列的每個核心的 4,000 IOPS 和每個核心每秒的 33 MB。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="e4fc8-226">hello GS 系列提供每個核心 5,000 IOPS 和每個核心每秒 50 MB。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="e4fc8-227">**為的 hello 本機 SSD 支援受管理磁碟 VM？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="e4fc8-228">hello 本機 SSD 是隨附於受管理磁碟 VM 的暫存位置。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="e4fc8-229">暫時儲存體不需額外的成本。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="e4fc8-230">我們建議您不要使用此本機 SSD toostore 應用程式資料不是保存在 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="e4fc8-231">**會那里任何影響 hello 的空白位置修剪上使用高階磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="e4fc8-232">Azure 磁碟上是高階或標準磁碟上的空白位置修剪沒有缺點 toohello 使用了。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="e4fc8-233">新磁碟大小：受控和非受控</span><span class="sxs-lookup"><span data-stu-id="e4fc8-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="e4fc8-234">**Hello 支援作業系統和資料磁碟最大磁碟大小為何？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="e4fc8-235">Azure 支援的作業系統磁碟的 hello 磁碟分割類型為 hello 主開機記錄 (MBR)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="e4fc8-236">hello MBR 格式支援向上 too2 TB 的磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="e4fc8-237">hello Azure 支援的作業系統磁碟的最大大小為 2 TB。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="e4fc8-238">Azure 支援 too4 TB 的資料磁碟上。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="e4fc8-239">**支援的 hello 最大頁面 blob 大小為何？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="e4fc8-240">Azure 支援的 hello 最大分頁 blob 大小為 8 TB (8,191 GB)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="e4fc8-241">我們不支援大於 4 TB (4095 GB) 附加 tooa VM 做為作業系統磁碟或資料的分頁 blob。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="e4fc8-242">**我需要 toouse 新版本的 Azure tools toocreate 附加、 調整大小，並上傳大於 1 TB 的磁碟嗎？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="e4fc8-243">您不需要 tooupgrade 現有的 Azure tools toocreate、 附加，或調整大小大於 1 TB 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="e4fc8-244">您的 VHD 檔案從 tooupload 內部直接 tooAzure 做為分頁 blob 或未受管理的磁碟，您需要 toouse hello 最新工具組：</span><span class="sxs-lookup"><span data-stu-id="e4fc8-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="e4fc8-245">Azure 工具</span><span class="sxs-lookup"><span data-stu-id="e4fc8-245">Azure tools</span></span>      | <span data-ttu-id="e4fc8-246">支援的版本</span><span class="sxs-lookup"><span data-stu-id="e4fc8-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="e4fc8-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4fc8-247">Azure PowerShell</span></span> | <span data-ttu-id="e4fc8-248">版本號碼 4.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="e4fc8-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="e4fc8-249">Azure CLI v1</span><span class="sxs-lookup"><span data-stu-id="e4fc8-249">Azure CLI v1</span></span>     | <span data-ttu-id="e4fc8-250">版本號碼 0.10.13：2017 年 5 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="e4fc8-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="e4fc8-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="e4fc8-251">AzCopy</span></span>           | <span data-ttu-id="e4fc8-252">版本號碼 6.1.0：2017 年 6 月發行或更新版本</span><span class="sxs-lookup"><span data-stu-id="e4fc8-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="e4fc8-253">Azure CLI v2 和 Azure 儲存體總管的 hello 支援即將推出。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="e4fc8-254">**針對非受控磁碟或分頁 Blob，是否支援 P4 和 P6 磁碟大小？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="e4fc8-255">否。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-255">No.</span></span> <span data-ttu-id="e4fc8-256">只有受控磁碟才支援 P4 (32 GB) 和 P6 (64 GB) 磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="e4fc8-257">即將支援非受控磁碟和分頁 Blob。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="e4fc8-258">**如果我管理的現有 premium 磁碟小於 hello 少數磁碟啟用 （大約是 2017 年 6 月 15) 之前，已建立 64 GB，如何為它收費？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="e4fc8-259">現有的小型高階磁碟不超過 64 GB 繼續計費 toobe 相應 toohello P10 定價層。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="e4fc8-260">**我可以切換 hello 磁碟層小於 64 GB 的小型高階磁碟從 P10 tooP4 或 P6？**</span><span class="sxs-lookup"><span data-stu-id="e4fc8-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="e4fc8-261">您可以擷取您的小型磁碟的快照，然後建立 定價層 tooP4 磁碟 tooautomatically 交換器 hello 或 P6 根據 hello 佈建大小。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="e4fc8-262">如果這裡沒有解答我的問題該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="e4fc8-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="e4fc8-263">如果這裡未列出您的問題，請告訴我們，我們將協助您找到答案。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="e4fc8-264">您可以將在 hello 本文結尾處將問題張貼 hello 註解中。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="e4fc8-265">tooengage 與 hello Azure 儲存體小組及其他社群成員關於本文中，使用 hello MSDN [Azure 儲存體論壇](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="e4fc8-266">toorequest 功能提交您的要求和意見 toohello [Azure 儲存體意見反應論壇](https://feedback.azure.com/forums/217298-storage)。</span><span class="sxs-lookup"><span data-stu-id="e4fc8-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
