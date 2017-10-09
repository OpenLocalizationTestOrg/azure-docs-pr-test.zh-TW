---
title: "命名方針-Windows aaaAzure 基礎結構 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作命名指導方針 Azure 基礎結構服務中。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="73191-103">適用於 Windows VM 的 Azure 基礎結構命名指導方針</span><span class="sxs-lookup"><span data-stu-id="73191-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="73191-104">本文著重在了解如何針對所有的邏輯和容易識別您各種 Azure 資源 toobuild tooapproach 命名慣例設定的資源整個環境。</span><span class="sxs-lookup"><span data-stu-id="73191-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="73191-105">命名慣例的實作指導方針</span><span class="sxs-lookup"><span data-stu-id="73191-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="73191-106">决策：</span><span class="sxs-lookup"><span data-stu-id="73191-106">Decisions:</span></span>

* <span data-ttu-id="73191-107">哪些是您的 Azure 資源命名慣例？</span><span class="sxs-lookup"><span data-stu-id="73191-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="73191-108">工作：</span><span class="sxs-lookup"><span data-stu-id="73191-108">Tasks:</span></span>

* <span data-ttu-id="73191-109">定義您的資源 toomaintain 一致性 hello affixes toouse。</span><span class="sxs-lookup"><span data-stu-id="73191-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="73191-110">定義指定名稱 hello 需求它們 toobe 全域唯一的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="73191-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="73191-111">文件 hello 命名慣例 toobe 使用，而且將 tooall 合作對象所涉及的 tooensure 一致性分散到部署。</span><span class="sxs-lookup"><span data-stu-id="73191-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="73191-112">命名慣例</span><span class="sxs-lookup"><span data-stu-id="73191-112">Naming conventions</span></span>
<span data-ttu-id="73191-113">在 Azure 中建立任何項目之前，應先建立良好的命名慣例。</span><span class="sxs-lookup"><span data-stu-id="73191-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="73191-114">命名慣例可確保所有的 hello 資源都有一個可預測的名稱，可協助降低與管理這些資源相關聯的 hello 系統管理負擔。</span><span class="sxs-lookup"><span data-stu-id="73191-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="73191-115">您可以選擇 toofollow 一組特定的命名慣例定義整個組織或是特定的 Azure 訂用帳戶或帳戶。</span><span class="sxs-lookup"><span data-stu-id="73191-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="73191-116">雖然小組需要在 Azure 上的專案上 toowork 時使用的 Azure 資源時，它很容易組織 tooestablish 隱含規則內的個人版，該模型無法妥善調整。</span><span class="sxs-lookup"><span data-stu-id="73191-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="73191-117">預先針對命名慣例組合取得一致的意見。</span><span class="sxs-lookup"><span data-stu-id="73191-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="73191-118">有些關於命名慣例的考量會牽涉到這組規則。</span><span class="sxs-lookup"><span data-stu-id="73191-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="73191-119">詞綴</span><span class="sxs-lookup"><span data-stu-id="73191-119">Affixes</span></span>
<span data-ttu-id="73191-120">瀏覽 toodefine 命名慣例，一個決策會出現在 hello label 是否：</span><span class="sxs-lookup"><span data-stu-id="73191-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="73191-121">hello 名稱 （前置詞） 的 hello 開頭</span><span class="sxs-lookup"><span data-stu-id="73191-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="73191-122">hello hello 名稱 （尾碼） 的結尾</span><span class="sxs-lookup"><span data-stu-id="73191-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="73191-123">比方說，以下是兩個可能的名稱，資源群組使用 hello`rg`附加：</span><span class="sxs-lookup"><span data-stu-id="73191-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="73191-124">Rg-WebApp (前置)</span><span class="sxs-lookup"><span data-stu-id="73191-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="73191-125">WebApp-Rg (後置)</span><span class="sxs-lookup"><span data-stu-id="73191-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="73191-126">Affixes 可以參考描述 hello 特定資源的 toodifferent 層面。</span><span class="sxs-lookup"><span data-stu-id="73191-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="73191-127">hello 下表顯示一些常用的範例。</span><span class="sxs-lookup"><span data-stu-id="73191-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="73191-128">層面</span><span class="sxs-lookup"><span data-stu-id="73191-128">Aspect</span></span> | <span data-ttu-id="73191-129">範例</span><span class="sxs-lookup"><span data-stu-id="73191-129">Examples</span></span> | <span data-ttu-id="73191-130">注意事項</span><span class="sxs-lookup"><span data-stu-id="73191-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="73191-131">Environment</span><span class="sxs-lookup"><span data-stu-id="73191-131">Environment</span></span> |<span data-ttu-id="73191-132">dev、stg、prod</span><span class="sxs-lookup"><span data-stu-id="73191-132">dev, stg, prod</span></span> |<span data-ttu-id="73191-133">根據 hello 用途和每個環境的名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="73191-134">位置</span><span class="sxs-lookup"><span data-stu-id="73191-134">Location</span></span> |<span data-ttu-id="73191-135">usw (West US)、use (East US 2)</span><span class="sxs-lookup"><span data-stu-id="73191-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="73191-136">根據 hello hello 資料中心或 hello hello 組織區域的區域。</span><span class="sxs-lookup"><span data-stu-id="73191-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="73191-137">Azure 元件、服務或產品</span><span class="sxs-lookup"><span data-stu-id="73191-137">Azure component, service, or product</span></span> |<span data-ttu-id="73191-138">Rg (適用於資源群組)、VNet (適用於虛擬網路)</span><span class="sxs-lookup"><span data-stu-id="73191-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="73191-139">根據資源會提供哪些 hello 產品支援。</span><span class="sxs-lookup"><span data-stu-id="73191-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="73191-140">角色</span><span class="sxs-lookup"><span data-stu-id="73191-140">Role</span></span> |<span data-ttu-id="73191-141">sql、ora、sp、iis</span><span class="sxs-lookup"><span data-stu-id="73191-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="73191-142">根據 hello hello 虛擬機器角色。</span><span class="sxs-lookup"><span data-stu-id="73191-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="73191-143">執行個體</span><span class="sxs-lookup"><span data-stu-id="73191-143">Instance</span></span> |<span data-ttu-id="73191-144">01、02 和 03 等</span><span class="sxs-lookup"><span data-stu-id="73191-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="73191-145">適用於有一個以上執行個體的資源。</span><span class="sxs-lookup"><span data-stu-id="73191-145">For resources that have more than one instance.</span></span> <span data-ttu-id="73191-146">例如，雲端服務中負載平衡的 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="73191-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="73191-147">在建立您的命名慣例，請確定，它們清楚的 affixes toouse 每種類型的資源，並在哪個位置 （前置詞與尾碼）。</span><span class="sxs-lookup"><span data-stu-id="73191-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="73191-148">日期</span><span class="sxs-lookup"><span data-stu-id="73191-148">Dates</span></span>
<span data-ttu-id="73191-149">它通常是從 hello 名稱建立一個資源重要 toodetermine hello 日期。</span><span class="sxs-lookup"><span data-stu-id="73191-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="73191-150">我們建議 hello YYYYMMDD 日期格式。</span><span class="sxs-lookup"><span data-stu-id="73191-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="73191-151">此格式可確保不只記錄 hello 完整日期，但是該兩個名稱只有在 hello 日期不同的資源也在 hello 排序依字母順序，依時間先後順序相同的時間。</span><span class="sxs-lookup"><span data-stu-id="73191-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="73191-152">命名資源</span><span class="sxs-lookup"><span data-stu-id="73191-152">Naming resources</span></span>
<span data-ttu-id="73191-153">每種類型的資源定義中 hello 命名慣例，其中應該有定義如何 tooassign 名稱 tooeach 資源的規則建立。</span><span class="sxs-lookup"><span data-stu-id="73191-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="73191-154">這些規則應該套用 tooall 類型的資源，例如：</span><span class="sxs-lookup"><span data-stu-id="73191-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="73191-155">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="73191-155">Subscriptions</span></span>
* <span data-ttu-id="73191-156">帳戶</span><span class="sxs-lookup"><span data-stu-id="73191-156">Accounts</span></span>
* <span data-ttu-id="73191-157">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="73191-157">Storage accounts</span></span>
* <span data-ttu-id="73191-158">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="73191-158">Virtual networks</span></span>
* <span data-ttu-id="73191-159">子網路</span><span class="sxs-lookup"><span data-stu-id="73191-159">Subnets</span></span>
* <span data-ttu-id="73191-160">可用性設定組</span><span class="sxs-lookup"><span data-stu-id="73191-160">Availability sets</span></span>
* <span data-ttu-id="73191-161">資源群組</span><span class="sxs-lookup"><span data-stu-id="73191-161">Resource groups</span></span>
* <span data-ttu-id="73191-162">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="73191-162">Virtual machines</span></span>
* <span data-ttu-id="73191-163">端點</span><span class="sxs-lookup"><span data-stu-id="73191-163">Endpoints</span></span>
* <span data-ttu-id="73191-164">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="73191-164">Network security groups</span></span>
* <span data-ttu-id="73191-165">角色</span><span class="sxs-lookup"><span data-stu-id="73191-165">Roles</span></span>

<span data-ttu-id="73191-166">hello 名稱的 tooensure 提供它所參考的足夠資訊 toodetermine toowhich 資源，您應該使用描述性的名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="73191-167">電腦名稱</span><span class="sxs-lookup"><span data-stu-id="73191-167">Computer names</span></span>
<span data-ttu-id="73191-168">當您建立虛擬機器 (VM) 時，Microsoft Azure 需要有 VM 名稱的總 too15 字元用於 hello 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="73191-169">Azure 會使用 hello hello 安裝的作業系統 hello VM 在相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="73191-170">不過，這些名稱可能不一定是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="73191-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="73191-171">如果 VM 從已包含作業系統的.vhd 映像檔建立的在 Azure 中的 hello VM 名稱可能不同於 hello VM 的作業系統的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="73191-172">這種情況下可以加入某種程度的困難 tooVM 管理，因此不建議。</span><span class="sxs-lookup"><span data-stu-id="73191-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="73191-173">指派 hello Azure VM 資源 hello 相同的名稱，做為您指派該 VM toohello 作業系統 hello 電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="73191-174">我們建議 hello Azure VM 名稱是 hello 與 hello 基礎作業系統的電腦名稱相同。</span><span class="sxs-lookup"><span data-stu-id="73191-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="73191-175">儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="73191-175">Storage account names</span></span>
<span data-ttu-id="73191-176">本節不適太[Azure 受管理磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="73191-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="73191-177">對於非受控磁碟，儲存體帳戶具備負責管理其名稱的特殊規則。</span><span class="sxs-lookup"><span data-stu-id="73191-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="73191-178">您只能使用小寫字母和數字。</span><span class="sxs-lookup"><span data-stu-id="73191-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="73191-179">如需詳細資訊，請參閱[建立儲存體帳戶](../../storage/storage-create-storage-account.md#create-a-storage-account)。</span><span class="sxs-lookup"><span data-stu-id="73191-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="73191-180">此外，hello 儲存體帳戶名稱，以及 core.windows.net，應該是全域有效且唯一的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="73191-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="73191-181">比方說，如果 hello 儲存體帳戶呼叫 mystorageaccount，hello 下列產生的 DNS 名稱應該是唯一：</span><span class="sxs-lookup"><span data-stu-id="73191-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="73191-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="73191-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="73191-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="73191-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="73191-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="73191-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="73191-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="73191-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

