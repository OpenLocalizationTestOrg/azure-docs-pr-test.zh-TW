---
title: "Azure 基礎結構命名指導方針 - Linux | Microsoft Docs"
description: "了解適合用來在 Azure 基礎結構服務中進行命名的關鍵設計和實作指導方針。"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1b086f0972c02d569a7219820a3d596960b6014b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="4e5a6-103">適用於 Linux VM 的 Azure 基礎結構命名指導方針</span><span class="sxs-lookup"><span data-stu-id="4e5a6-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="4e5a6-104">本文著重於了解各種 Azure 資源的命名慣例做法，以在整個環境中建置一組具邏輯性且可輕鬆識別的資源集合。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="4e5a6-105">命名慣例的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="4e5a6-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="4e5a6-106">决策：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-106">Decisions:</span></span>

* <span data-ttu-id="4e5a6-107">哪些是您的 Azure 資源命名慣例？</span><span class="sxs-lookup"><span data-stu-id="4e5a6-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="4e5a6-108">工作：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-108">Tasks:</span></span>

* <span data-ttu-id="4e5a6-109">定義在資源間使用以維護一致性的詞綴。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="4e5a6-110">定義必須是全域唯一的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="4e5a6-111">記錄要使用並散發給所有相關合作對象的命名慣例，以確保部屬之間的一致性。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="4e5a6-112">命名慣例</span><span class="sxs-lookup"><span data-stu-id="4e5a6-112">Naming conventions</span></span>
<span data-ttu-id="4e5a6-113">在 Azure 中建立任何項目之前，應先建立良好的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="4e5a6-114">命名慣例可確保所有資源都擁有可預測的名稱，有助於降低與這些資源管理相關聯的系統管理負擔。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="4e5a6-115">您可以選擇遵循為整個組織所定義的一組特定命名慣例，或適用於特定 Azure 訂用帳戶或帳戶的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="4e5a6-116">儘管對組織內的個人來說，在使用 Azure 資源時建立隱含規則非常容易，但對於在 Azure 一起工作的小組而言，您需要能夠彈性地調整。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span></span>

<span data-ttu-id="4e5a6-117">預先針對命名慣例組合取得一致的意見。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="4e5a6-118">有些關於命名慣例的考量會牽涉到規則組合。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="4e5a6-119">詞綴</span><span class="sxs-lookup"><span data-stu-id="4e5a6-119">Affixes</span></span>
<span data-ttu-id="4e5a6-120">當您在定義命名慣例時，其中一個決定便是詞綴要位於：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-120">As you look to define a naming convention, one decision is whether the affix is at:</span></span>

* <span data-ttu-id="4e5a6-121">名稱開頭 (前置)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="4e5a6-122">名稱結尾 (後置)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-122">The end of the name (suffix)</span></span>

<span data-ttu-id="4e5a6-123">例如，針對使用 `rg` 詞綴的資源群組，以下是兩個可能的名稱：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="4e5a6-124">Rg-WebApp (前置)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="4e5a6-125">WebApp-Rg (後置)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="4e5a6-126">詞綴指的是可說明特定資源的各個層面。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="4e5a6-127">下列表格顯示一些常用範例。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="4e5a6-128">層面</span><span class="sxs-lookup"><span data-stu-id="4e5a6-128">Aspect</span></span> | <span data-ttu-id="4e5a6-129">範例</span><span class="sxs-lookup"><span data-stu-id="4e5a6-129">Examples</span></span> | <span data-ttu-id="4e5a6-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="4e5a6-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4e5a6-131">Environment</span><span class="sxs-lookup"><span data-stu-id="4e5a6-131">Environment</span></span> |<span data-ttu-id="4e5a6-132">dev、stg、prod</span><span class="sxs-lookup"><span data-stu-id="4e5a6-132">dev, stg, prod</span></span> |<span data-ttu-id="4e5a6-133">取決於每個環境的用途與名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="4e5a6-134">位置</span><span class="sxs-lookup"><span data-stu-id="4e5a6-134">Location</span></span> |<span data-ttu-id="4e5a6-135">usw (West US)、use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="4e5a6-136">取決於資料中心的區域或組織的區域。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="4e5a6-137">Azure 元件、服務或產品</span><span class="sxs-lookup"><span data-stu-id="4e5a6-137">Azure component, service, or product</span></span> |<span data-ttu-id="4e5a6-138">Rg (適用於資源群組)、VNet (適用於虛擬網路)</span><span class="sxs-lookup"><span data-stu-id="4e5a6-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="4e5a6-139">取決於資源提供支援的產品。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="4e5a6-140">角色</span><span class="sxs-lookup"><span data-stu-id="4e5a6-140">Role</span></span> |<span data-ttu-id="4e5a6-141">db、app、web</span><span class="sxs-lookup"><span data-stu-id="4e5a6-141">db, app, web</span></span> |<span data-ttu-id="4e5a6-142">取決於虛擬機器的角色。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="4e5a6-143">執行個體</span><span class="sxs-lookup"><span data-stu-id="4e5a6-143">Instance</span></span> |<span data-ttu-id="4e5a6-144">01、02 和 03 等</span><span class="sxs-lookup"><span data-stu-id="4e5a6-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="4e5a6-145">適用於有一個以上執行個體的資源。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-145">For resources that have more than one instance.</span></span> <span data-ttu-id="4e5a6-146">例如，雲端服務中負載平衡的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="4e5a6-147">建立命名慣例時，請確定它們會清楚描述要針對每個資源類型使用哪些詞綴，以及使用的位置 (前置或後置)。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="4e5a6-148">日期</span><span class="sxs-lookup"><span data-stu-id="4e5a6-148">Dates</span></span>
<span data-ttu-id="4e5a6-149">從資源名稱來判斷建立日期通常非常重要。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="4e5a6-150">我們建議使用 YYYYMMDD 日期格式。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="4e5a6-151">此格式可確保不僅會記錄完整的日期，而且這兩個名稱只有日期不同的資源會以依字母順序和依時間先後順序的方式來排序。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="4e5a6-152">命名資源</span><span class="sxs-lookup"><span data-stu-id="4e5a6-152">Naming resources</span></span>
<span data-ttu-id="4e5a6-153">在命名慣例中定義每個資源類型，慣例中應包含規則來定義為每個所建立資源指派名稱的方式。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="4e5a6-154">這些規則應套用到所有資源類型，例如：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="4e5a6-155">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4e5a6-155">Subscriptions</span></span>
* <span data-ttu-id="4e5a6-156">帳戶</span><span class="sxs-lookup"><span data-stu-id="4e5a6-156">Accounts</span></span>
* <span data-ttu-id="4e5a6-157">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4e5a6-157">Storage accounts</span></span>
* <span data-ttu-id="4e5a6-158">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4e5a6-158">Virtual networks</span></span>
* <span data-ttu-id="4e5a6-159">子網路</span><span class="sxs-lookup"><span data-stu-id="4e5a6-159">Subnets</span></span>
* <span data-ttu-id="4e5a6-160">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="4e5a6-160">Availability sets</span></span>
* <span data-ttu-id="4e5a6-161">資源群組</span><span class="sxs-lookup"><span data-stu-id="4e5a6-161">Resource groups</span></span>
* <span data-ttu-id="4e5a6-162">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4e5a6-162">Virtual machines</span></span>
* <span data-ttu-id="4e5a6-163">端點</span><span class="sxs-lookup"><span data-stu-id="4e5a6-163">Endpoints</span></span>
* <span data-ttu-id="4e5a6-164">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="4e5a6-164">Network security groups</span></span>
* <span data-ttu-id="4e5a6-165">角色</span><span class="sxs-lookup"><span data-stu-id="4e5a6-165">Roles</span></span>

<span data-ttu-id="4e5a6-166">若要確保名稱可提供足夠的資訊來判斷其指稱的是哪一個資源，您應使用描述性名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="4e5a6-167">電腦名稱</span><span class="sxs-lookup"><span data-stu-id="4e5a6-167">Computer names</span></span>
<span data-ttu-id="4e5a6-168">當您建立虛擬機器 (VM) 時，Azure 會要求一個由最多 64 個字元組成的 VM 名稱，這會用來做為資源名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span></span> <span data-ttu-id="4e5a6-169">Azure 會針對安裝在 VM 中的作業系統使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="4e5a6-170">但是，這些名稱不一定相同。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="4e5a6-171">若 VM 是從已經包含作業系統的 .vhd 映像檔所建立，Azure 中的 VM 名稱可能會與 VM 的作業系統電腦名稱不同。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="4e5a6-172">這種情況可能會增加 VM 管理的困難度，因此我們不建議使用。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="4e5a6-173">將 Azure VM 資源的名稱指派為該 VM 作業系統上所指派的相同電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="4e5a6-174">我們建議讓 Azure VM 名稱與基礎作業系統電腦名稱相同。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="4e5a6-175">儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="4e5a6-175">Storage account names</span></span>
<span data-ttu-id="4e5a6-176">本節不適用 [Azure 受控磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="4e5a6-177">對於非受控磁碟，儲存體帳戶具備負責管理其名稱的特殊規則。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="4e5a6-178">您只能使用小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="4e5a6-179">如需詳細資訊，請參閱[建立儲存體帳戶](../../storage/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="4e5a6-180">此外，儲存體帳戶名稱 (含 core.windows.net) 應是全域有效的唯一 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="4e5a6-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="4e5a6-181">例如，如果儲存體帳戶名稱為 mystorageaccount，則以下產生的 DNS 名稱應該是唯一的：</span><span class="sxs-lookup"><span data-stu-id="4e5a6-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="4e5a6-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e5a6-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="4e5a6-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e5a6-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="4e5a6-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="4e5a6-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e5a6-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e5a6-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

