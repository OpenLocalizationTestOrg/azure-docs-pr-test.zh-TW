---
title: "關於 Azure 中的 Windows Vm aaaFAQ |Microsoft 文件"
description: "提供有關使用 hello 資源管理員的模型建立的 Windows 虛擬機器的 hello 常見問題的解答 toosome。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 757da816-a050-4889-a010-6f75d7978eb7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: cynthn
ms.openlocfilehash: ee366a04bda347ce2be07bde4fc6bad306cc1da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-windows-virtual-machines"></a><span data-ttu-id="a2530-103">Windows 虛擬機器的常見問題</span><span class="sxs-lookup"><span data-stu-id="a2530-103">Frequently asked question about Windows Virtual Machines</span></span>
<span data-ttu-id="a2530-104">本文使用 hello Resource Manager 部署模型在 Azure 中建立 Windows 虛擬機器的一些常見問題。</span><span class="sxs-lookup"><span data-stu-id="a2530-104">This article addresses some common questions about Windows virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a2530-105">本主題的 hello Linux 版本，請參閱[常見問題集 Linux 虛擬機器的相關問題](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a2530-105">For hello Linux version of this topic, see [Frequently asked question about Linux Virtual Machines](../linux/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="a2530-106">我可以在 Azure VM 上執行什麼？</span><span class="sxs-lookup"><span data-stu-id="a2530-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="a2530-107">所有的訂閱者都可以在 Azure 虛擬機器上執行伺服器軟體。</span><span class="sxs-lookup"><span data-stu-id="a2530-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="a2530-108">在 Azure 中執行的 Microsoft 伺服器軟體的 hello 支援原則的相關資訊，請參閱[Microsoft server software 支援適用於 Azure 虛擬機器](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="a2530-108">For information about hello support policy for running Microsoft server software in Azure, see [Microsoft server software support for Azure Virtual Machines](https://support.microsoft.com/kb/2721672)</span></span>

<span data-ttu-id="a2530-109">特定版本的 Windows 7、 Windows 8.1 和 Windows 10 為可用 tooMSDN Azure 權益訂閱者和 MSDN 開發和測試隨用隨付 」 訂閱者開發和測試工作。</span><span class="sxs-lookup"><span data-stu-id="a2530-109">Certain versions of Windows 7, Windows 8.1, and Windows 10 are available tooMSDN Azure benefit subscribers and MSDN Dev and Test Pay-As-You-Go subscribers, for development and test tasks.</span></span> <span data-ttu-id="a2530-110">如需詳細資訊 (包括指示和限制)，請參閱 [MSDN 訂閱者的 Windows 用戶端映像](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/)。</span><span class="sxs-lookup"><span data-stu-id="a2530-110">For details, including instructions and limitations, see [Windows Client images for MSDN subscribers](http://azure.microsoft.com/blog/2014/05/29/windows-client-images-on-azure/).</span></span> 

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="a2530-111">我可以使用多少的儲存體搭配虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="a2530-111">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="a2530-112">每個資料磁碟可以是 up too1 TB。</span><span class="sxs-lookup"><span data-stu-id="a2530-112">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="a2530-113">您可以使用的資料磁碟的 hello 數目取決於 hello hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="a2530-113">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="a2530-114">如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-114">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a2530-115">Azure 受管理的磁碟是 hello 新和建議的磁碟儲存體的供應項目用於使用 Azure 虛擬機器永續性儲存體的資料。</span><span class="sxs-lookup"><span data-stu-id="a2530-115">Azure Managed Disks are hello new and recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data.</span></span> <span data-ttu-id="a2530-116">每部虛擬機器可使用多部受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a2530-116">You can use multiple Managed Disks with each Virtual Machine.</span></span> <span data-ttu-id="a2530-117">受控磁碟提供兩種耐久的儲存體選項：進階與標準受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a2530-117">Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.</span></span> <span data-ttu-id="a2530-118">如需定價資訊，請參閱[受控磁碟定價](https://azure.microsoft.com/pricing/details/managed-disks)。</span><span class="sxs-lookup"><span data-stu-id="a2530-118">For pricing information, see [Managed Disks Pricing](https://azure.microsoft.com/pricing/details/managed-disks).</span></span>

<span data-ttu-id="a2530-119">Azure 儲存體帳戶也可以提供儲存體 hello 作業系統磁碟和任何資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a2530-119">Azure storage accounts can also provide storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="a2530-120">每個磁碟是以分頁 Blob 方式儲存的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="a2530-120">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="a2530-121">如需定價的詳細資料，請參閱 [儲存體定價詳細資料](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="a2530-121">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="a2530-122">如何存取我的虛擬機器？</span><span class="sxs-lookup"><span data-stu-id="a2530-122">How can I access my virtual machine?</span></span>
<span data-ttu-id="a2530-123">使用遠端桌面連線 (RDP) 為 Windows VM 建立遠端連線。</span><span class="sxs-lookup"><span data-stu-id="a2530-123">Establish a remote connection using Remote Desktop Connection (RDP) for a Windows VM.</span></span> <span data-ttu-id="a2530-124">如需指示，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-124">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a2530-125">支援兩個並行連線的最大值，除非 hello 伺服器設定為遠端桌面服務工作階段主機。</span><span class="sxs-lookup"><span data-stu-id="a2530-125">A maximum of two concurrent connections are supported, unless hello server is configured as a Remote Desktop Services session host.</span></span>  

<span data-ttu-id="a2530-126">如果您有遠端桌面的問題，請參閱[疑難排解遠端桌面連線 tooa windows Azure 虛擬機器](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-126">If you’re having problems with Remote Desktop, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="a2530-127">如果您熟悉 HYPER-V，您可能會尋找工具類似 tooVMConnect。</span><span class="sxs-lookup"><span data-stu-id="a2530-127">If you’re familiar with Hyper-V, you might be looking for a tool similar tooVMConnect.</span></span> <span data-ttu-id="a2530-128">Azure 不提供類似的工具，因為不支援主控台存取 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2530-128">Azure doesn’t offer a similar tool because console access tooa virtual machine isn’t supported.</span></span>

## <a name="can-i-use-hello-temporary-disk-hello-d-drive-by-default-toostore-data"></a><span data-ttu-id="a2530-129">可以使用 hello 暫存磁碟 (d： 磁碟機預設 hello) toostore 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="a2530-129">Can I use hello temporary disk (hello D: drive by default) toostore data?</span></span>
<span data-ttu-id="a2530-130">請勿使用 hello 暫存磁碟 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="a2530-130">Don’t use hello temporary disk toostore data.</span></span> <span data-ttu-id="a2530-131">暫存磁碟僅提供暫存空間，因此您會有遺失資料且無法復原的風險。</span><span class="sxs-lookup"><span data-stu-id="a2530-131">It is only temporary storage, so you would risk losing data that can’t be recovered.</span></span> <span data-ttu-id="a2530-132">Hello 虛擬機器會移動 tooa 不同的主機時，就可能發生資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a2530-132">Data loss can occur when hello virtual machine moves tooa different host.</span></span> <span data-ttu-id="a2530-133">調整虛擬機器的大小，更新 hello 主機或硬體失敗 hello 主機上的是一些虛擬機器可能移動的 hello 原因。</span><span class="sxs-lookup"><span data-stu-id="a2530-133">Resizing a virtual machine, updating hello host, or a hardware failure on hello host are some of hello reasons a virtual machine might move.</span></span>

<span data-ttu-id="a2530-134">如果您需要 toouse hello d： 磁碟機代號的應用程式，您可以重新指派磁碟機代號，因此 hello 暫存磁碟會使用 d： 以外的項目。</span><span class="sxs-lookup"><span data-stu-id="a2530-134">If you have an application that needs toouse hello D: drive letter, you can reassign drive letters so that hello temporary disk uses something other than D:.</span></span> <span data-ttu-id="a2530-135">如需指示，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-135">For instructions, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>


## <a name="how-can-i-change-hello-drive-letter-of-hello-temporary-disk"></a><span data-ttu-id="a2530-136">如何變更 hello hello 暫存磁碟的磁碟機代號？</span><span class="sxs-lookup"><span data-stu-id="a2530-136">How can I change hello drive letter of hello temporary disk?</span></span>
<span data-ttu-id="a2530-137">您可以變更 hello 所移動的 hello 分頁檔的磁碟機代號和重新指派磁碟機代號，但需要 toomake 確定您執行 hello 以特定順序的步驟。</span><span class="sxs-lookup"><span data-stu-id="a2530-137">You can change hello drive letter by moving hello page file and reassigning drive letters, but you need toomake sure you do hello steps in a specific order.</span></span> <span data-ttu-id="a2530-138">如需指示，請參閱[hello Windows 暫存磁碟的變更 hello 磁碟機代號](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-138">For instructions, see [Change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="can-i-add-an-existing-vm-tooan-availability-set"></a><span data-ttu-id="a2530-139">可以加入現有的 VM tooan 可用性集嗎？</span><span class="sxs-lookup"><span data-stu-id="a2530-139">Can I add an existing VM tooan availability set?</span></span>
<span data-ttu-id="a2530-140">否。</span><span class="sxs-lookup"><span data-stu-id="a2530-140">No.</span></span> <span data-ttu-id="a2530-141">如果您想可用性設定組您 VM toobe 部分，您會需要 toocreate hello VM hello 集內。</span><span class="sxs-lookup"><span data-stu-id="a2530-141">If you want your VM toobe part of an availability set, you need toocreate hello VM within hello set.</span></span> <span data-ttu-id="a2530-142">目前沒有任何方式 tooadd 之後已建立設定的 VM tooan 可用性。</span><span class="sxs-lookup"><span data-stu-id="a2530-142">There currently isn't a way tooadd a VM tooan availability set after it has been created.</span></span>

## <a name="can-i-upload-a-virtual-machine-tooazure"></a><span data-ttu-id="a2530-143">可以上傳虛擬機器 tooAzure 嗎？</span><span class="sxs-lookup"><span data-stu-id="a2530-143">Can I upload a virtual machine tooAzure?</span></span>
<span data-ttu-id="a2530-144">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-144">Yes.</span></span> <span data-ttu-id="a2530-145">如需指示，請參閱[移轉內部部署 Vm tooAzure](on-prem-to-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="a2530-145">For instructions, see [Migrating on-premises VMs tooAzure](on-prem-to-azure.md).</span></span>

## <a name="can-i-resize-hello-os-disk"></a><span data-ttu-id="a2530-146">可調整大小 hello OS 磁碟嗎？</span><span class="sxs-lookup"><span data-stu-id="a2530-146">Can I resize hello OS disk?</span></span>
<span data-ttu-id="a2530-147">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-147">Yes.</span></span> <span data-ttu-id="a2530-148">如需指示，請參閱[tooexpand hello Azure 資源群組中的虛擬機器的作業系統磁碟機的方式](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-148">For instructions, see [How tooexpand hello OS drive of a Virtual Machine in an Azure Resource Group](expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="a2530-149">我是否可以複製或再製現有的 Azure VM？</span><span class="sxs-lookup"><span data-stu-id="a2530-149">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="a2530-150">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-150">Yes.</span></span> <span data-ttu-id="a2530-151">您可以使用受管理的映像，來建立虛擬機器的映像，然後使用多個新的 Vm hello 映像 toobuild 項目。</span><span class="sxs-lookup"><span data-stu-id="a2530-151">Using managed images, you can create an image of a virtual machine and then use hello image toobuild multiple new VMs.</span></span> <span data-ttu-id="a2530-152">如需指示，請參閱[建立 VM 的自訂映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="a2530-152">For instructions, see [Create a custom image of a VM](tutorial-custom-images.md).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="a2530-153">為什麼我在 Azure Resource Manager 中沒看到加拿大中部和加拿大東部區域？</span><span class="sxs-lookup"><span data-stu-id="a2530-153">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>

<span data-ttu-id="a2530-154">hello 兩個新的區域加拿大中央和加拿大東部不會自動註冊現有的 Azure 訂用帳戶建立的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2530-154">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="a2530-155">透過部署虛擬機器時自動完成此項登錄 hello Azure 入口網站 tooany 使用 Azure 資源管理員的其他區域。</span><span class="sxs-lookup"><span data-stu-id="a2530-155">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="a2530-156">虛擬機器後是已部署的 tooany 其他 Azure 地區，hello 新區域應該可用於後續的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a2530-156">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="does-azure-support-linux-vms"></a><span data-ttu-id="a2530-157">Azure 是否支援 Linux VM？</span><span class="sxs-lookup"><span data-stu-id="a2530-157">Does Azure support Linux VMs?</span></span>
<span data-ttu-id="a2530-158">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-158">Yes.</span></span> <span data-ttu-id="a2530-159">tooquickly 建立時，請參閱 Linux VM tootry[使用 hello 入口網站在 Azure 上建立 Linux VM](../linux/quick-create-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="a2530-159">tooquickly create a Linux VM tootry out, see [Create a Linux VM on Azure using hello Portal](../linux/quick-create-portal.md).</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="a2530-160">會在建立之後可以加入 NIC toomy VM 嗎？</span><span class="sxs-lookup"><span data-stu-id="a2530-160">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="a2530-161">是的，目前可行。</span><span class="sxs-lookup"><span data-stu-id="a2530-161">Yes, this is now possible.</span></span> <span data-ttu-id="a2530-162">hello VM 第一個需求 toobe 停止取消配置。</span><span class="sxs-lookup"><span data-stu-id="a2530-162">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="a2530-163">然後您可以新增或移除 NIC (除非它是 hello hello VM 上的最後一個 NIC)。</span><span class="sxs-lookup"><span data-stu-id="a2530-163">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="a2530-164">是否有任何電腦名稱需求？</span><span class="sxs-lookup"><span data-stu-id="a2530-164">Are there any computer name requirements?</span></span>
<span data-ttu-id="a2530-165">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-165">Yes.</span></span> <span data-ttu-id="a2530-166">hello 電腦名稱可以是最多 15 個字元長度。</span><span class="sxs-lookup"><span data-stu-id="a2530-166">hello computer name can be a maximum of 15 characters in length.</span></span> <span data-ttu-id="a2530-167">如需命名資源相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-167">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="a2530-168">是否有任何資源群組名稱需求？</span><span class="sxs-lookup"><span data-stu-id="a2530-168">Are there any resource group name requirements?</span></span>
<span data-ttu-id="a2530-169">是。</span><span class="sxs-lookup"><span data-stu-id="a2530-169">Yes.</span></span> <span data-ttu-id="a2530-170">hello 資源群組名稱可以是 90 中的字元長度最多。</span><span class="sxs-lookup"><span data-stu-id="a2530-170">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="a2530-171">如需資源群組相關詳細資訊，請參閱[命名慣例規則與限制](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a2530-171">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="a2530-172">建立 VM 時，有哪些 hello username 需求？</span><span class="sxs-lookup"><span data-stu-id="a2530-172">What are hello username requirements when creating a VM?</span></span>

<span data-ttu-id="a2530-173">使用者名稱長度最多為 20 個字元，而且不能以句號 (".") 結尾。</span><span class="sxs-lookup"><span data-stu-id="a2530-173">Usernames can be a maximum of 20 characters in length and cannot end in a period (".").</span></span> 


<span data-ttu-id="a2530-174">不允許下列使用者名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="a2530-174">hello following usernames are not allowed:</span></span>
<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-175">administrator</span><span class="sxs-lookup"><span data-stu-id="a2530-175">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-176">admin</span><span class="sxs-lookup"><span data-stu-id="a2530-176">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-177">user</span><span class="sxs-lookup"><span data-stu-id="a2530-177">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-178">user1</span><span class="sxs-lookup"><span data-stu-id="a2530-178">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-179">test</span><span class="sxs-lookup"><span data-stu-id="a2530-179">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-180">user2</span><span class="sxs-lookup"><span data-stu-id="a2530-180">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-181">test1</span><span class="sxs-lookup"><span data-stu-id="a2530-181">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-182">user3</span><span class="sxs-lookup"><span data-stu-id="a2530-182">user3</span></span></td>
    </tr>    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-183">admin1</span><span class="sxs-lookup"><span data-stu-id="a2530-183">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-184">1</span><span class="sxs-lookup"><span data-stu-id="a2530-184">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-185">123</span><span class="sxs-lookup"><span data-stu-id="a2530-185">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-186">a</span><span class="sxs-lookup"><span data-stu-id="a2530-186">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-187">actuser</span><span class="sxs-lookup"><span data-stu-id="a2530-187">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="a2530-188">adm</span><span class="sxs-lookup"><span data-stu-id="a2530-188">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-189">admin2</span><span class="sxs-lookup"><span data-stu-id="a2530-189">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-190">aspnet</span><span class="sxs-lookup"><span data-stu-id="a2530-190">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-191">backup</span><span class="sxs-lookup"><span data-stu-id="a2530-191">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-192">console</span><span class="sxs-lookup"><span data-stu-id="a2530-192">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-193">david</span><span class="sxs-lookup"><span data-stu-id="a2530-193">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-194">guest</span><span class="sxs-lookup"><span data-stu-id="a2530-194">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-195">john</span><span class="sxs-lookup"><span data-stu-id="a2530-195">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-196">owner</span><span class="sxs-lookup"><span data-stu-id="a2530-196">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-197">root</span><span class="sxs-lookup"><span data-stu-id="a2530-197">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-198">伺服器</span><span class="sxs-lookup"><span data-stu-id="a2530-198">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-199">sql</span><span class="sxs-lookup"><span data-stu-id="a2530-199">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-200">支援</span><span class="sxs-lookup"><span data-stu-id="a2530-200">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-201">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="a2530-201">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-202">sys</span><span class="sxs-lookup"><span data-stu-id="a2530-202">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="a2530-203">test2</span><span class="sxs-lookup"><span data-stu-id="a2530-203">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-204">test3</span><span class="sxs-lookup"><span data-stu-id="a2530-204">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-205">user4</span><span class="sxs-lookup"><span data-stu-id="a2530-205">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="a2530-206">user5</span><span class="sxs-lookup"><span data-stu-id="a2530-206">user5</span></span></td>
    </tr>
</table>

## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="a2530-207">建立 VM 時，有哪些 hello 密碼需求？</span><span class="sxs-lookup"><span data-stu-id="a2530-207">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="a2530-208">密碼必須是長度為 12-123 個字元，且符合 3 超出 hello 下列 4 的複雜性需求：</span><span class="sxs-lookup"><span data-stu-id="a2530-208">Passwords must be 12 - 123 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="a2530-209">包含小寫字元</span><span class="sxs-lookup"><span data-stu-id="a2530-209">Have lower characters</span></span>
* <span data-ttu-id="a2530-210">包含大小字元</span><span class="sxs-lookup"><span data-stu-id="a2530-210">Have upper characters</span></span>
* <span data-ttu-id="a2530-211">包含數字</span><span class="sxs-lookup"><span data-stu-id="a2530-211">Have a digit</span></span>
* <span data-ttu-id="a2530-212">包含特殊字元 (Regex match [\W_])</span><span class="sxs-lookup"><span data-stu-id="a2530-212">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="a2530-213">不允許 hello 下列密碼：</span><span class="sxs-lookup"><span data-stu-id="a2530-213">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td>abc@123 </td>
        <td><span data-ttu-id="a2530-214">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="a2530-214">P@$$w0rd</span></span> </td>
        <td>P@ssw0rd </td>
        <td>P@ssword123 </td>
        <td><span data-ttu-id="a2530-215">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="a2530-215">Pa$$word</span></span> </td>
    </tr>
    <tr>
        <td>pass@word1 </td>
        <td><span data-ttu-id="a2530-216">Password!</span><span class="sxs-lookup"><span data-stu-id="a2530-216">Password!</span></span> </td>
        <td><span data-ttu-id="a2530-217">Password1</span><span class="sxs-lookup"><span data-stu-id="a2530-217">Password1</span></span> </td>
        <td><span data-ttu-id="a2530-218">Password22</span><span class="sxs-lookup"><span data-stu-id="a2530-218">Password22</span></span> </td>
        <td><span data-ttu-id="a2530-219">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="a2530-219">iloveyou!</span></span> </td>
    </tr>
</table>
