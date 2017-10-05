---
title: "Azure 中 Linux VM 的常見問題集 | Microsoft Docs"
description: "針對以 Resource Manager 模型建立的 Linux 虛擬機器，提供一些相關常見問題的解答。"
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
ms.openlocfilehash: 0e06d21bd0b6ef807f38e41dcd50c9cd715607a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="2a793-103">Linux 虛擬機器的常見問題</span><span class="sxs-lookup"><span data-stu-id="2a793-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="2a793-104">本文可解決在 Azure 中使用 Resource Manager 部署模型建立之 Linux 虛擬機器的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="2a793-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="2a793-105">如需本主題的 Windows 版本，請參閱 [Windows 虛擬機器的常見問題](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2a793-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="2a793-106">我可以在 Azure VM 上執行什麼？</span><span class="sxs-lookup"><span data-stu-id="2a793-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="2a793-107">所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。</span><span class="sxs-lookup"><span data-stu-id="2a793-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="2a793-108">如需詳細資訊，請參閱 [經 Azure 背書之配送映像上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2a793-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="2a793-109">我可以使用多少的儲存體搭配虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="2a793-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="2a793-110">每個資料磁碟最多可達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="2a793-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="2a793-111">可使用的資料磁碟數量取決於虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="2a793-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="2a793-112">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2a793-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2a793-113">Azure 儲存體帳戶提供作業系統磁碟和任何資料磁碟的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="2a793-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="2a793-114">每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="2a793-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="2a793-115">如需定價的詳細資料，請參閱 [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="2a793-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="2a793-116">如何存取我的虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="2a793-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="2a793-117">使用安全殼層 (SSH) 建立遠端連線來登入虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2a793-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="2a793-118">請參閱如何[從 Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 或[從 Linux 及 Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 連線的指示。</span><span class="sxs-lookup"><span data-stu-id="2a793-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2a793-119">根據預設，SSH 允許最多 10 個並行連線。</span><span class="sxs-lookup"><span data-stu-id="2a793-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="2a793-120">您可以編輯組態檔以增加這個數字。</span><span class="sxs-lookup"><span data-stu-id="2a793-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="2a793-121">如果您遇到問題，請參閱 [疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2a793-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="2a793-122">我可以使用暫存磁碟 (/dev/sdb1) 儲存資料嗎？</span><span class="sxs-lookup"><span data-stu-id="2a793-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="2a793-123">請勿使用暫存磁碟 (/dev/sdb1) 來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="2a793-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="2a793-124">它只是用於暫時儲存。</span><span class="sxs-lookup"><span data-stu-id="2a793-124">It is only there for temporary storage.</span></span> <span data-ttu-id="2a793-125">您可能會遺失資料且無法復原。</span><span class="sxs-lookup"><span data-stu-id="2a793-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="2a793-126">我是否可以複製或再製現有的 Azure VM？</span><span class="sxs-lookup"><span data-stu-id="2a793-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="2a793-127">是。</span><span class="sxs-lookup"><span data-stu-id="2a793-127">Yes.</span></span> <span data-ttu-id="2a793-128">如需相關指示，請參閱 [如何在 Resource Manager 部署模型中建立 Linux 虛擬機器的複本](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2a793-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="2a793-129">為什麼我透過 Azure Resource Manager 沒看到加拿大中部和加拿大東部區域？</span><span class="sxs-lookup"><span data-stu-id="2a793-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="2a793-130">針對現有 Azure 訂用帳戶所建立的虛擬機器，不會自動註冊加拿大中部和加拿大東部這兩個新的區域。</span><span class="sxs-lookup"><span data-stu-id="2a793-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="2a793-131">當虛擬機器透過 Azure 入口網站使用 Azure Resource Manager 部署到任何其他區域時，就會自動完成註冊。</span><span class="sxs-lookup"><span data-stu-id="2a793-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="2a793-132">將虛擬機器部署到任何其他 Azure 區域之後，新的區域即可供後續的虛擬機器使用。</span><span class="sxs-lookup"><span data-stu-id="2a793-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="2a793-133">我可以在建立 VM 之後將 NIC 新增至此 VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="2a793-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="2a793-134">是的，目前可行。</span><span class="sxs-lookup"><span data-stu-id="2a793-134">Yes, this is now possible.</span></span> <span data-ttu-id="2a793-135">您必須先停止解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="2a793-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="2a793-136">然後您可以新增或移除 NIC (除非它是 VM 上的最後一個 NIC)。</span><span class="sxs-lookup"><span data-stu-id="2a793-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="2a793-137">是否有任何電腦名稱需求？</span><span class="sxs-lookup"><span data-stu-id="2a793-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="2a793-138">是。</span><span class="sxs-lookup"><span data-stu-id="2a793-138">Yes.</span></span> <span data-ttu-id="2a793-139">電腦名稱的長度最多可以有 64 個字元。</span><span class="sxs-lookup"><span data-stu-id="2a793-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="2a793-140">如需命名資源相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2a793-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="2a793-141">是否有任何資源群組名稱需求？</span><span class="sxs-lookup"><span data-stu-id="2a793-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="2a793-142">是。</span><span class="sxs-lookup"><span data-stu-id="2a793-142">Yes.</span></span> <span data-ttu-id="2a793-143">資源群組名稱長度最多可以有 90 個字元。</span><span class="sxs-lookup"><span data-stu-id="2a793-143">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="2a793-144">如需資源群組相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2a793-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="2a793-145">建立 VM 時的使用者名稱需求為何？</span><span class="sxs-lookup"><span data-stu-id="2a793-145">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="2a793-146">使用者名稱必須是長度在 1 - 64 之間的字元。</span><span class="sxs-lookup"><span data-stu-id="2a793-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="2a793-147">不允許下列使用者名稱︰</span><span class="sxs-lookup"><span data-stu-id="2a793-147">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-148">administrator</span><span class="sxs-lookup"><span data-stu-id="2a793-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-149">admin</span><span class="sxs-lookup"><span data-stu-id="2a793-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-150">user</span><span class="sxs-lookup"><span data-stu-id="2a793-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-151">user1</span><span class="sxs-lookup"><span data-stu-id="2a793-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-152">test</span><span class="sxs-lookup"><span data-stu-id="2a793-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-153">user2</span><span class="sxs-lookup"><span data-stu-id="2a793-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-154">test1</span><span class="sxs-lookup"><span data-stu-id="2a793-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-155">user3</span><span class="sxs-lookup"><span data-stu-id="2a793-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-156">admin1</span><span class="sxs-lookup"><span data-stu-id="2a793-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-157">1</span><span class="sxs-lookup"><span data-stu-id="2a793-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-158">123</span><span class="sxs-lookup"><span data-stu-id="2a793-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-159">a</span><span class="sxs-lookup"><span data-stu-id="2a793-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-160">actuser</span><span class="sxs-lookup"><span data-stu-id="2a793-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="2a793-161">adm</span><span class="sxs-lookup"><span data-stu-id="2a793-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-162">admin2</span><span class="sxs-lookup"><span data-stu-id="2a793-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-163">aspnet</span><span class="sxs-lookup"><span data-stu-id="2a793-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-164">backup</span><span class="sxs-lookup"><span data-stu-id="2a793-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-165">console</span><span class="sxs-lookup"><span data-stu-id="2a793-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-166">david</span><span class="sxs-lookup"><span data-stu-id="2a793-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-167">guest</span><span class="sxs-lookup"><span data-stu-id="2a793-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-168">john</span><span class="sxs-lookup"><span data-stu-id="2a793-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-169">owner</span><span class="sxs-lookup"><span data-stu-id="2a793-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-170">root</span><span class="sxs-lookup"><span data-stu-id="2a793-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-171">伺服器</span><span class="sxs-lookup"><span data-stu-id="2a793-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-172">sql</span><span class="sxs-lookup"><span data-stu-id="2a793-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-173">支援</span><span class="sxs-lookup"><span data-stu-id="2a793-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="2a793-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-175">sys</span><span class="sxs-lookup"><span data-stu-id="2a793-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="2a793-176">test2</span><span class="sxs-lookup"><span data-stu-id="2a793-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-177">test3</span><span class="sxs-lookup"><span data-stu-id="2a793-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-178">user4</span><span class="sxs-lookup"><span data-stu-id="2a793-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="2a793-179">user5</span><span class="sxs-lookup"><span data-stu-id="2a793-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="2a793-180">建立 VM 時的密碼需求為何？</span><span class="sxs-lookup"><span data-stu-id="2a793-180">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="2a793-181">密碼必須是長度在 6 - 72 之間的字元，且符合下列 4 個複雜性需求的其中 3 個：</span><span class="sxs-lookup"><span data-stu-id="2a793-181">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="2a793-182">包含小寫字元</span><span class="sxs-lookup"><span data-stu-id="2a793-182">Have lower characters</span></span>
* <span data-ttu-id="2a793-183">包含大小字元</span><span class="sxs-lookup"><span data-stu-id="2a793-183">Have upper characters</span></span>
* <span data-ttu-id="2a793-184">包含數字</span><span class="sxs-lookup"><span data-stu-id="2a793-184">Have a digit</span></span>
* <span data-ttu-id="2a793-185">包含特殊字元 (Regex match [\W_])</span><span class="sxs-lookup"><span data-stu-id="2a793-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="2a793-186">不允許下列密碼︰</span><span class="sxs-lookup"><span data-stu-id="2a793-186">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="2a793-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="2a793-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="2a793-188">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="2a793-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="2a793-189">Password!</span><span class="sxs-lookup"><span data-stu-id="2a793-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a793-190">Password1</span><span class="sxs-lookup"><span data-stu-id="2a793-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a793-191">Password22</span><span class="sxs-lookup"><span data-stu-id="2a793-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="2a793-192">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="2a793-192">iloveyou!</span></span></td>
    </tr>
</table>
