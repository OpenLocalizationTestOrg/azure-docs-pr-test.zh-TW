---
title: "適用於 Linux Vm 在 Azure 中的常見問題 aaaFrequently |Microsoft 文件"
description: "提供有關使用 hello 資源管理員的模型建立的 Linux 虛擬機器的 hello 常見問題的解答 toosome。"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="1aa49-103">Linux 虛擬機器的常見問題</span><span class="sxs-lookup"><span data-stu-id="1aa49-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="1aa49-104">本文使用 hello Resource Manager 部署模型在 Azure 中建立的 Linux 虛擬機器的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="1aa49-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="1aa49-105">本主題的 hello Windows 版本，請參閱[常見問題集有關 Windows 虛擬機器的問題](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1aa49-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="1aa49-106">我可以在 Azure VM 上執行什麼？</span><span class="sxs-lookup"><span data-stu-id="1aa49-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="1aa49-107">所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。</span><span class="sxs-lookup"><span data-stu-id="1aa49-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="1aa49-108">如需詳細資訊，請參閱 [經 Azure 背書之配送映像上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="1aa49-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="1aa49-109">我可以使用多少的儲存體搭配虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="1aa49-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="1aa49-110">每個資料磁碟可以是 up too1 TB。</span><span class="sxs-lookup"><span data-stu-id="1aa49-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="1aa49-111">您可以使用的資料磁碟的 hello 數目取決於 hello hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="1aa49-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="1aa49-112">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1aa49-113">Azure 儲存體帳戶提供 hello 作業系統磁碟和任何資料磁碟的儲存體。</span><span class="sxs-lookup"><span data-stu-id="1aa49-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="1aa49-114">每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="1aa49-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="1aa49-115">如需定價的詳細資料，請參閱 [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="1aa49-116">如何存取我的虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="1aa49-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="1aa49-117">建立遠端連線 toolog toohello 虛擬機器上，使用安全殼層 (SSH)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="1aa49-118">請參閱如何 hello 指示 tooconnect[從 Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或[從 Linux 和 Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1aa49-119">根據預設，SSH 允許最多 10 個並行連線。</span><span class="sxs-lookup"><span data-stu-id="1aa49-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="1aa49-120">您可以增加這個數字藉由編輯 hello 設定檔。</span><span class="sxs-lookup"><span data-stu-id="1aa49-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="1aa49-121">如果您遇到問題，請參閱 [疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="1aa49-122">可以使用 hello 暫存磁碟 (/ 開發/sdb1) toostore 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="1aa49-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="1aa49-123">請勿使用 hello 暫存磁碟 (/ 開發/sdb1) toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="1aa49-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="1aa49-124">它只是用於暫時儲存。</span><span class="sxs-lookup"><span data-stu-id="1aa49-124">It is only there for temporary storage.</span></span> <span data-ttu-id="1aa49-125">您可能會遺失資料且無法復原。</span><span class="sxs-lookup"><span data-stu-id="1aa49-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="1aa49-126">我是否可以複製或再製現有的 Azure VM？</span><span class="sxs-lookup"><span data-stu-id="1aa49-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="1aa49-127">是。</span><span class="sxs-lookup"><span data-stu-id="1aa49-127">Yes.</span></span> <span data-ttu-id="1aa49-128">如需指示，請參閱[toocreate Linux 虛擬機器中的 hello Resource Manager 部署模型的方式](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="1aa49-129">為什麼我在 Azure Resource Manager 中沒看到加拿大中部和加拿大東部區域？</span><span class="sxs-lookup"><span data-stu-id="1aa49-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="1aa49-130">hello 兩個新的區域加拿大中央和加拿大東部不會自動註冊現有的 Azure 訂用帳戶建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1aa49-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="1aa49-131">透過部署虛擬機器時自動完成此項登錄 hello Azure 入口網站 tooany 使用 Azure 資源管理員的其他區域。</span><span class="sxs-lookup"><span data-stu-id="1aa49-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="1aa49-132">虛擬機器後是已部署的 tooany 其他 Azure 地區，hello 新區域應該可用於後續的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="1aa49-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="1aa49-133">會在建立之後可以加入 NIC toomy VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="1aa49-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="1aa49-134">是的，目前可行。</span><span class="sxs-lookup"><span data-stu-id="1aa49-134">Yes, this is now possible.</span></span> <span data-ttu-id="1aa49-135">hello VM 第一個需求 toobe 停止取消配置。</span><span class="sxs-lookup"><span data-stu-id="1aa49-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="1aa49-136">然後您可以新增或移除 NIC (除非它是 hello hello VM 上的最後一個 NIC)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="1aa49-137">是否有任何電腦名稱需求？</span><span class="sxs-lookup"><span data-stu-id="1aa49-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="1aa49-138">是。</span><span class="sxs-lookup"><span data-stu-id="1aa49-138">Yes.</span></span> <span data-ttu-id="1aa49-139">hello 電腦名稱可以是最多 64 個字元的長度。</span><span class="sxs-lookup"><span data-stu-id="1aa49-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="1aa49-140">如需命名資源相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="1aa49-141">是否有任何資源群組名稱需求？</span><span class="sxs-lookup"><span data-stu-id="1aa49-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="1aa49-142">是。</span><span class="sxs-lookup"><span data-stu-id="1aa49-142">Yes.</span></span> <span data-ttu-id="1aa49-143">hello 資源群組名稱可以是 90 中的字元長度最多。</span><span class="sxs-lookup"><span data-stu-id="1aa49-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="1aa49-144">如需資源群組相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1aa49-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="1aa49-145">建立 VM 時，有哪些 hello username 需求？</span><span class="sxs-lookup"><span data-stu-id="1aa49-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="1aa49-146">使用者名稱必須是長度在 1 - 64 之間的字元。</span><span class="sxs-lookup"><span data-stu-id="1aa49-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="1aa49-147">不允許下列使用者名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="1aa49-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-148">administrator</span><span class="sxs-lookup"><span data-stu-id="1aa49-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-149">admin</span><span class="sxs-lookup"><span data-stu-id="1aa49-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-150">user</span><span class="sxs-lookup"><span data-stu-id="1aa49-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-151">user1</span><span class="sxs-lookup"><span data-stu-id="1aa49-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-152">test</span><span class="sxs-lookup"><span data-stu-id="1aa49-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-153">user2</span><span class="sxs-lookup"><span data-stu-id="1aa49-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-154">test1</span><span class="sxs-lookup"><span data-stu-id="1aa49-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-155">user3</span><span class="sxs-lookup"><span data-stu-id="1aa49-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-156">admin1</span><span class="sxs-lookup"><span data-stu-id="1aa49-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-157">1</span><span class="sxs-lookup"><span data-stu-id="1aa49-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-158">123</span><span class="sxs-lookup"><span data-stu-id="1aa49-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-159">a</span><span class="sxs-lookup"><span data-stu-id="1aa49-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-160">actuser</span><span class="sxs-lookup"><span data-stu-id="1aa49-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="1aa49-161">adm</span><span class="sxs-lookup"><span data-stu-id="1aa49-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-162">admin2</span><span class="sxs-lookup"><span data-stu-id="1aa49-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="1aa49-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-164">backup</span><span class="sxs-lookup"><span data-stu-id="1aa49-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-165">console</span><span class="sxs-lookup"><span data-stu-id="1aa49-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-166">david</span><span class="sxs-lookup"><span data-stu-id="1aa49-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-167">guest</span><span class="sxs-lookup"><span data-stu-id="1aa49-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-168">john</span><span class="sxs-lookup"><span data-stu-id="1aa49-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-169">owner</span><span class="sxs-lookup"><span data-stu-id="1aa49-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-170">root</span><span class="sxs-lookup"><span data-stu-id="1aa49-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-171">伺服器</span><span class="sxs-lookup"><span data-stu-id="1aa49-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-172">sql</span><span class="sxs-lookup"><span data-stu-id="1aa49-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-173">支援</span><span class="sxs-lookup"><span data-stu-id="1aa49-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="1aa49-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-175">sys</span><span class="sxs-lookup"><span data-stu-id="1aa49-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="1aa49-176">test2</span><span class="sxs-lookup"><span data-stu-id="1aa49-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-177">test3</span><span class="sxs-lookup"><span data-stu-id="1aa49-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-178">user4</span><span class="sxs-lookup"><span data-stu-id="1aa49-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="1aa49-179">user5</span><span class="sxs-lookup"><span data-stu-id="1aa49-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="1aa49-180">建立 VM 時，有哪些 hello 密碼需求？</span><span class="sxs-lookup"><span data-stu-id="1aa49-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="1aa49-181">密碼必須是長度為 6 72 個字元，且符合 3 超出 hello 下列 4 的複雜性需求：</span><span class="sxs-lookup"><span data-stu-id="1aa49-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="1aa49-182">包含小寫字元</span><span class="sxs-lookup"><span data-stu-id="1aa49-182">Have lower characters</span></span>
* <span data-ttu-id="1aa49-183">包含大小字元</span><span class="sxs-lookup"><span data-stu-id="1aa49-183">Have upper characters</span></span>
* <span data-ttu-id="1aa49-184">包含數字</span><span class="sxs-lookup"><span data-stu-id="1aa49-184">Have a digit</span></span>
* <span data-ttu-id="1aa49-185">包含特殊字元 (Regex match [\W_])</span><span class="sxs-lookup"><span data-stu-id="1aa49-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="1aa49-186">不允許 hello 下列密碼：</span><span class="sxs-lookup"><span data-stu-id="1aa49-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="1aa49-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="1aa49-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="1aa49-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="1aa49-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="1aa49-189">Password!</span><span class="sxs-lookup"><span data-stu-id="1aa49-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="1aa49-190">Password1</span><span class="sxs-lookup"><span data-stu-id="1aa49-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="1aa49-191">Password22</span><span class="sxs-lookup"><span data-stu-id="1aa49-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="1aa49-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="1aa49-192">iloveyou!</span></span></td>
    </tr>
</table>
