---
title: "aaaAzure 磁碟加密，適用於 Windows 和 Linux IaaS Vm |Microsoft 文件"
description: "本文提供 Windows 和 Linux IaaS VM 適用的 Microsoft Azure 磁碟加密概觀。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="e1c1e-103">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="e1c1e-104">Microsoft Azure 是強式認可的 tooensuring 資料隱私權，資料 sovereignty 和 toocontrol 您的 Azure 託管可讓您透過的進階的技術 tooencrypt 範圍資料控制和管理加密金鑰控制和稽核資料的存取。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="e1c1e-105">這會提供 Azure 客戶 hello 彈性 toochoose hello 解決方案以最符合其商務需求。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="e1c1e-106">本文中，我們將介紹新技術解決方案 tooa 「 適用於 Windows 和 Linux IaaS VM 的 Azure 磁碟加密 」 toohelp 保護與防衛資料 toomeet 您組織的安全性與相容性承諾。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="e1c1e-107">hello 紙張提供詳細的指引 toouse hello Azure 磁碟加密功能，包括 hello 如何支援案例和 hello 使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-108">某些建議可能會增加資料、網路或計算資源的使用量，導致額外的授權或訂用帳戶成本。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="e1c1e-109">概觀</span><span class="sxs-lookup"><span data-stu-id="e1c1e-109">Overview</span></span>
<span data-ttu-id="e1c1e-110">Azure 磁碟加密是協助您加密 Windows 和 Linux IaaS 虛擬機器磁碟的新功能。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="e1c1e-111">Azure 磁碟加密會利用 hello 業界標準[BitLocker](https://technet.microsoft.com/library/cc732774.aspx)功能的 Windows 和 hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) Linux tooprovide 磁碟區加密 hello OS 與 hello 資料磁碟的功能。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="e1c1e-112">與整合 hello 方案[Azure 金鑰保存庫](https://azure.microsoft.com/documentation/services/key-vault/)toohelp 您控制和管理您金鑰保存庫的訂用帳戶中的 hello 磁碟加密金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="e1c1e-113">hello 方案也能確保 hello 虛擬機器磁碟上的所有資料會留在您 Azure 儲存體都加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="e1c1e-114">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密現已在所有 Azure 公用區域和 AzureGov 區域**正式推出**，可供用於標準 VM 和具有高階儲存體的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="e1c1e-115">加密案例</span><span class="sxs-lookup"><span data-stu-id="e1c1e-115">Encryption scenarios</span></span>
<span data-ttu-id="e1c1e-116">hello Azure 磁碟加密解決方案支援下列客戶案例 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="e1c1e-117">對透過加密的 VHD 和加密金鑰建立的新 IaaS VM 啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="e1c1e-118">在 從支援的 hello Azure 資源庫映像建立新的 IaaS Vm 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="e1c1e-119">在 Azure 中執行的現有 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="e1c1e-120">在 Windows IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="e1c1e-121">在 Linux IaaS VM 的資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="e1c1e-122">允許加密受管理磁碟 VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="e1c1e-123">現有已加密非高階儲存體 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="e1c1e-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="e1c1e-124">備份與還原以金鑰加密金鑰進行加密的已加密 VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="e1c1e-125">hello 解決方案支援 IaaS Vm 的下列案例，當啟用 Microsoft Azure 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="e1c1e-126">與 Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="e1c1e-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="e1c1e-127">標準層 VM：[A、D、DS、G、GS、F 等系列 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="e1c1e-128">在 Windows 和 Linux IaaS Vm 和 hello 從受管理的磁碟 Vm 上啟用加密支援 Azure 資源庫映像</span><span class="sxs-lookup"><span data-stu-id="e1c1e-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="e1c1e-129">在 Windows IaaS VM 與受管理磁碟 VM 的作業系統與資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="e1c1e-130">在 Linux IaaS VM 與受管理磁碟 VM 的資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="e1c1e-131">在執行 Windows Client OS 的 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="e1c1e-132">在具有掛接路徑的磁碟區上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="e1c1e-133">使用 mdadm 在設定了磁碟串接 (RAID) 的 Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="e1c1e-134">使用資料磁碟適用的 LVM 在 Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="e1c1e-135">在設定了儲存空間的 Windows VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="e1c1e-136">現有已加密非高階儲存體 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="e1c1e-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="e1c1e-137">支援所有 Azure 公用區域與 AzureGov 區域</span><span class="sxs-lookup"><span data-stu-id="e1c1e-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="e1c1e-138">hello 方案不支援下列案例、 功能和技術的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="e1c1e-139">基本層 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="e1c1e-140">在 Linux IaaS VM 的 OS 磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="e1c1e-141">停用加密資料磁碟機上的，如果 hello 作業系統磁碟機已加密適用於 Linux Iaas Vm</span><span class="sxs-lookup"><span data-stu-id="e1c1e-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="e1c1e-142">使用 hello 傳統 VM 建立方法所建立的 IaaS Vm</span><span class="sxs-lookup"><span data-stu-id="e1c1e-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="e1c1e-143">「不」支援透過 Windows 和 Linux IaaS VM 客戶自訂映像上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="e1c1e-144">目前不支援在 Linux LVM OS 磁碟機上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="e1c1e-145">此支援會立即出現。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-145">This support will come soon.</span></span>
* <span data-ttu-id="e1c1e-146">與您的內部部署金鑰管理服務整合</span><span class="sxs-lookup"><span data-stu-id="e1c1e-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="e1c1e-147">Azure 檔案 (共用檔案系統)、網路檔案系統 (NFS)、動態磁碟區和以軟體型 RAID 系統所設定的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="e1c1e-148">備份與還原不以金鑰加密金鑰進行加密的已加密 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="e1c1e-149">現有已加密高階儲存體 VM 的更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-150">備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e1c1e-151">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e1c1e-152">KEK 是啟用 VM 加密的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="e1c1e-153">即將提供此支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-153">This support is coming soon.</span></span>
> <span data-ttu-id="e1c1e-154">不支援現有已加密高階儲存體 VM 的更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="e1c1e-155">即將提供此支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="e1c1e-156">加密功能</span><span class="sxs-lookup"><span data-stu-id="e1c1e-156">Encryption features</span></span>
<span data-ttu-id="e1c1e-157">當您啟用並部署 Azure IaaS Vm 的 Azure 磁碟加密時，hello 下列功能已啟用，根據提供的 hello 組態：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="e1c1e-158">Hello OS 磁碟區 tooprotect hello 開機磁碟區的存放裝置中的靜止的加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="e1c1e-159">資料磁碟區 tooprotect hello 資料磁碟區的存放裝置中的靜止的加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="e1c1e-160">適用於 Windows 的 IaaS Vm 停用加密 hello OS 和資料磁碟機</span><span class="sxs-lookup"><span data-stu-id="e1c1e-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="e1c1e-161">停用加密 hello 的資料磁碟機適用於 Linux IaaS Vm （只有當作業系統不是加密磁碟機）</span><span class="sxs-lookup"><span data-stu-id="e1c1e-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="e1c1e-162">保護 hello 加密金鑰和金鑰保存庫訂用帳戶中的密碼</span><span class="sxs-lookup"><span data-stu-id="e1c1e-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="e1c1e-163">報告 hello hello 加密狀態加密 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="e1c1e-164">磁碟加密組態設定從 hello IaaS 虛擬機器之移除</span><span class="sxs-lookup"><span data-stu-id="e1c1e-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="e1c1e-165">備份和還原的加密 Vm 使用 hello Azure 備份服務</span><span class="sxs-lookup"><span data-stu-id="e1c1e-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-166">備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e1c1e-167">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e1c1e-168">KEK 是啟用 VM 加密的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="e1c1e-169">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密解決方案包含：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="e1c1e-170">適用於 Windows hello 磁碟加密延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="e1c1e-171">適用於 Linux hello 磁碟加密延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="e1c1e-172">hello 磁碟加密 PowerShell 指令程式。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="e1c1e-173">hello 磁碟加密 Azure 命令列介面 (CLI) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="e1c1e-174">hello 磁碟加密 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="e1c1e-175">hello Azure 磁碟加密解決方案可支援執行 Windows 或 Linux 作業系統的 IaaS Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="e1c1e-176">如需支援的 hello 作業系統的詳細資訊，請參閱 hello < 先決條件 > 一節。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-177">使用 Azure 磁碟加密來加密 VM 磁碟完全免費。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="e1c1e-178">價值主張</span><span class="sxs-lookup"><span data-stu-id="e1c1e-178">Value proposition</span></span>
<span data-ttu-id="e1c1e-179">當您套用 hello Azure 磁碟加密管理解決方案時，可以滿足下列商務需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="e1c1e-180">IaaS Vm 保護待用，因為您可以使用業界標準加密技術 tooaddress 組織的安全性與相容性的需求。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="e1c1e-181">IaaS VM 會在客戶控制的金鑰和原則下開機，且您可以在金鑰保存庫中稽核其使用狀況。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="e1c1e-182">加密工作流程</span><span class="sxs-lookup"><span data-stu-id="e1c1e-182">Encryption workflow</span></span>
<span data-ttu-id="e1c1e-183">適用於 Windows 和 Linux Vm tooenable 磁碟加密 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-184">選擇加密的情況下從 hello 之前加密案例。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="e1c1e-185">參加 tooenabling 磁碟加密透過 hello Azure 磁碟加密 Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令，並指定 hello 加密組態。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="e1c1e-186">Hello 客戶加密 VHD 案例中上, 傳加密的 hello VHD tooyour 儲存體帳戶和 hello 加密金鑰材料 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="e1c1e-187">然後，提供新的 IaaS VM 上的 hello 加密組態 tooenable 加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="e1c1e-188">針對新的 Vm 中建立的 hello Marketplace 並已在 Azure 中執行的現有 Vm，提供 hello 加密組態 tooenable 加密上 hello IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="e1c1e-189">授與存取 toohello Azure 平台 tooread hello 加密金鑰材料 （BitLocker 加密金鑰的 Windows 系統），適用於 Linux 的複雜密碼從您的金鑰保存庫 tooenable 加密 hello IaaS VM 上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="e1c1e-190">提供 hello Azure Active Directory (Azure AD) 應用程式識別 toowrite hello 加密金鑰材料 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="e1c1e-191">如此可讓上述步驟 2 中的 hello 案例 hello IaaS VM 上的加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="e1c1e-192">Azure 會加密與 hello 金鑰保存庫設定，會更新 hello VM 服務模型，並設定加密 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="e1c1e-194">解密工作流程</span><span class="sxs-lookup"><span data-stu-id="e1c1e-194">Decryption workflow</span></span>
<span data-ttu-id="e1c1e-195">對於 IaaS Vm，完成下列高層級步驟的 hello toodisable 磁碟加密：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="e1c1e-196">在 Azure 中執行的 IaaS VM 上選擇 toodisable 加密 （解密），透過 hello Azure 磁碟加密 Resource Manager 範本或 PowerShell 指令程式，並指定 hello 解密組態。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="e1c1e-197">此步驟會停用加密 hello OS 或 hello 資料磁碟區上或兩者都執行 Windows IaaS VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="e1c1e-198">不過，如 hello 前一節中所述，停用作業系統磁碟加密 for Linux 不支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="e1c1e-199">hello 解密步驟只適用於 Linux Vm 上的資料磁碟機，只要 hello OS 磁碟不會加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="e1c1e-200">更新 azure hello VM 服務模型，且會標示解密 hello IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="e1c1e-201">hello VM hello 內容已不再加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-202">hello 停用加密作業不會刪除您金鑰保存庫和 hello 加密金鑰內容 （BitLocker 加密金鑰適用於 Windows 系統） 或適用於 Linux 的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="e1c1e-203">不支援停用 Linux 適用的作業系統磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="e1c1e-204">hello 解密步驟只適用於 Linux Vm 上的資料磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="e1c1e-205">不支援停用適用於 Linux 的資料磁碟加密，如果 hello 作業系統磁碟機已加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1c1e-206">必要條件</span><span class="sxs-lookup"><span data-stu-id="e1c1e-206">Prerequisites</span></span>
<span data-ttu-id="e1c1e-207">您可以啟用 Azure IaaS Vm 上的 Azure 磁碟加密 hello < 概觀 > 一節中所討論的 hello 支援案例之前，請參閱 hello 下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="e1c1e-208">您必須擁有有效的作用中 Azure 訂用 toocreate 資源 hello 支援地區的 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="e1c1e-209">支援 azure 磁碟加密： hello 遵循 Windows Server 版本： Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2 和 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="e1c1e-210">支援 azure 磁碟加密： hello 遵循 Windows 用戶端版本： Windows 8 用戶端和 Windows 10 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-211">針對 Windows Server 2008 R2，您必須先安裝 .NET Framework 4.5，才能在 Azure 中啟用加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="e1c1e-212">安裝從 Windows Update 安裝 hello 選用更新適用於 Windows Server 2008 R2 x64 型系統的 Microsoft.NET Framework 4.5.2 ([KB2901983](https://support.microsoft.com/kb/2901983))。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="e1c1e-213">支援 azure 磁碟加密 hello 下列 Azure 資源庫依據的 Linux 伺服器發行，版本：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="e1c1e-214">Linux 散發套件</span><span class="sxs-lookup"><span data-stu-id="e1c1e-214">Linux Distribution</span></span> | <span data-ttu-id="e1c1e-215">版本</span><span class="sxs-lookup"><span data-stu-id="e1c1e-215">Version</span></span> | <span data-ttu-id="e1c1e-216">支援加密的磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="e1c1e-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="e1c1e-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1c1e-217">Ubuntu</span></span> | <span data-ttu-id="e1c1e-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="e1c1e-219">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-219">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1c1e-220">Ubuntu</span></span> | <span data-ttu-id="e1c1e-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="e1c1e-222">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-222">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1c1e-223">Ubuntu</span></span> | <span data-ttu-id="e1c1e-224">12.10</span><span class="sxs-lookup"><span data-stu-id="e1c1e-224">12.10</span></span> | <span data-ttu-id="e1c1e-225">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-225">Data disk</span></span> |
| <span data-ttu-id="e1c1e-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e1c1e-226">Ubuntu</span></span> | <span data-ttu-id="e1c1e-227">12.04</span><span class="sxs-lookup"><span data-stu-id="e1c1e-227">12.04</span></span> | <span data-ttu-id="e1c1e-228">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-228">Data disk</span></span> |
| <span data-ttu-id="e1c1e-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-229">RHEL</span></span> | <span data-ttu-id="e1c1e-230">7.3</span><span class="sxs-lookup"><span data-stu-id="e1c1e-230">7.3</span></span> | <span data-ttu-id="e1c1e-231">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-231">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-232">RHEL</span></span> | <span data-ttu-id="e1c1e-233">7.2</span><span class="sxs-lookup"><span data-stu-id="e1c1e-233">7.2</span></span> | <span data-ttu-id="e1c1e-234">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-234">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-235">RHEL</span></span> | <span data-ttu-id="e1c1e-236">6.8</span><span class="sxs-lookup"><span data-stu-id="e1c1e-236">6.8</span></span> | <span data-ttu-id="e1c1e-237">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-237">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-238">RHEL</span></span> | <span data-ttu-id="e1c1e-239">6.7</span><span class="sxs-lookup"><span data-stu-id="e1c1e-239">6.7</span></span> | <span data-ttu-id="e1c1e-240">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-240">Data disk</span></span> |
| <span data-ttu-id="e1c1e-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-241">CentOS</span></span> | <span data-ttu-id="e1c1e-242">7.3</span><span class="sxs-lookup"><span data-stu-id="e1c1e-242">7.3</span></span> | <span data-ttu-id="e1c1e-243">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-243">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-244">CentOS</span></span> | <span data-ttu-id="e1c1e-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="e1c1e-245">7.2n</span></span> | <span data-ttu-id="e1c1e-246">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-246">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-247">CentOS</span></span> | <span data-ttu-id="e1c1e-248">6.8</span><span class="sxs-lookup"><span data-stu-id="e1c1e-248">6.8</span></span> | <span data-ttu-id="e1c1e-249">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-249">OS and Data disk</span></span> |
| <span data-ttu-id="e1c1e-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-250">CentOS</span></span> | <span data-ttu-id="e1c1e-251">7.1</span><span class="sxs-lookup"><span data-stu-id="e1c1e-251">7.1</span></span> | <span data-ttu-id="e1c1e-252">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-252">Data disk</span></span> |
| <span data-ttu-id="e1c1e-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-253">CentOS</span></span> | <span data-ttu-id="e1c1e-254">7.0</span><span class="sxs-lookup"><span data-stu-id="e1c1e-254">7.0</span></span> | <span data-ttu-id="e1c1e-255">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-255">Data disk</span></span> |
| <span data-ttu-id="e1c1e-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-256">CentOS</span></span> | <span data-ttu-id="e1c1e-257">6.7</span><span class="sxs-lookup"><span data-stu-id="e1c1e-257">6.7</span></span> | <span data-ttu-id="e1c1e-258">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-258">Data disk</span></span> |
| <span data-ttu-id="e1c1e-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-259">CentOS</span></span> | <span data-ttu-id="e1c1e-260">6.6</span><span class="sxs-lookup"><span data-stu-id="e1c1e-260">6.6</span></span> | <span data-ttu-id="e1c1e-261">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-261">Data disk</span></span> |
| <span data-ttu-id="e1c1e-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="e1c1e-262">CentOS</span></span> | <span data-ttu-id="e1c1e-263">6.5</span><span class="sxs-lookup"><span data-stu-id="e1c1e-263">6.5</span></span> | <span data-ttu-id="e1c1e-264">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-264">Data disk</span></span> |
| <span data-ttu-id="e1c1e-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e1c1e-265">openSUSE</span></span> | <span data-ttu-id="e1c1e-266">13.2</span><span class="sxs-lookup"><span data-stu-id="e1c1e-266">13.2</span></span> | <span data-ttu-id="e1c1e-267">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-267">Data disk</span></span> |
| <span data-ttu-id="e1c1e-268">SLES</span><span class="sxs-lookup"><span data-stu-id="e1c1e-268">SLES</span></span> | <span data-ttu-id="e1c1e-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="e1c1e-269">12 SP1</span></span> | <span data-ttu-id="e1c1e-270">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-270">Data disk</span></span> |
| <span data-ttu-id="e1c1e-271">SLES</span><span class="sxs-lookup"><span data-stu-id="e1c1e-271">SLES</span></span> | <span data-ttu-id="e1c1e-272">12-SP1 (高階)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="e1c1e-273">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-273">Data disk</span></span> |
| <span data-ttu-id="e1c1e-274">SLES</span><span class="sxs-lookup"><span data-stu-id="e1c1e-274">SLES</span></span> | <span data-ttu-id="e1c1e-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="e1c1e-275">HPC 12</span></span> | <span data-ttu-id="e1c1e-276">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-276">Data disk</span></span> |
| <span data-ttu-id="e1c1e-277">SLES</span><span class="sxs-lookup"><span data-stu-id="e1c1e-277">SLES</span></span> | <span data-ttu-id="e1c1e-278">11-SP4 (高階)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="e1c1e-279">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-279">Data disk</span></span> |
| <span data-ttu-id="e1c1e-280">SLES</span><span class="sxs-lookup"><span data-stu-id="e1c1e-280">SLES</span></span> | <span data-ttu-id="e1c1e-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="e1c1e-281">11 SP4</span></span> | <span data-ttu-id="e1c1e-282">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-282">Data disk</span></span> |

* <span data-ttu-id="e1c1e-283">Azure 磁碟加密需要，您的金鑰保存庫和 Vm 位於 hello 相同 Azure 地區和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-284">在不同的區域中設定 hello 資源會導致失敗啟用 hello Azure 磁碟加密 」 功能。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="e1c1e-285">tooset 和 Azure 磁碟加密設定金鑰保存庫，請參閱 > 一節**設定安裝及設定 Azure 磁碟加密金鑰保存庫**在 hello*必要條件*本文一節。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e1c1e-286">tooset 和設定 Azure Active directory 中的 Azure AD 應用程式，Azure 磁碟加密，請參閱 > 一節**設定 Azure Active Directory 中的 hello Azure AD 應用程式**在 hello*必要條件*本文一節。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e1c1e-287">tooset 和設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則，請參閱 > 一節**設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則**在 hello*必要條件*區段這篇文章。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e1c1e-288">tooprepare 預先加密的 Windows VHD，請參閱 > 一節**準備預先加密的 Windows VHD**在 hello*附錄*。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="e1c1e-289">tooprepare 預先加密的 Linux VHD，請參閱 > 一節**準備預先加密的 Linux VHD**在 hello*附錄*。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="e1c1e-290">hello Azure 平台需要存取 toohello 加密金鑰或密碼中您金鑰保存庫 toomake 它們可用 toohello 虛擬機器開機和解密 hello 虛擬機器作業系統磁碟區時。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="e1c1e-291">toogrant 權限 tooAzure 平台組 hello **EnabledForDiskEncryption** hello 金鑰保存庫中的屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="e1c1e-292">如需詳細資訊，請參閱**設定安裝及設定 Azure 磁碟加密金鑰保存庫**hello 附錄中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="e1c1e-293">您的金鑰保存庫密碼和 KEK URL 必須已設定版本。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="e1c1e-294">Azure 會強制執行設定版本的這項限制。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="e1c1e-295">有效的密碼及 KEK Url，請參閱下列範例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="e1c1e-296">有效祕密 URL 的範例︰https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e1c1e-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="e1c1e-297">有效 KEK URL 的範例：https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e1c1e-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="e1c1e-298">Azure 磁碟加密不支援將連接埠號碼指定為金鑰保存庫密碼和 KEK URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="e1c1e-299">如需不支援和支援的金鑰保存庫 Url 的範例，請參閱 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="e1c1e-300">無法接受的金鑰保存庫 URL https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e1c1e-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="e1c1e-301">可接受的金鑰保存庫 URL：https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e1c1e-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="e1c1e-302">tooenable hello Azure 磁碟加密 」 功能，hello IaaS Vm 必須符合下列網路端點的組態需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="e1c1e-303">tooget 語彙基元 tooconnect tooyour 金鑰保存庫，hello IaaS VM 必須是 Azure Active Directory 無法 tooconnect tooan 的端點， \[login.microsoftonline.com\]。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="e1c1e-304">toowrite hello 加密金鑰 tooyour 金鑰保存庫，hello IaaS VM 必須是能夠 tooconnect toohello 金鑰保存庫端點。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="e1c1e-305">hello IaaS VM 必須能夠 tooconnect tooan Azure 儲存體端點主機 hello Azure 延伸模組儲存機制和主機 hello VHD 檔案的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e1c1e-306">如果您的安全性原則會限制從 Azure Vm toohello 網際網路存取，您可以解決 hello 前面的 URI，並設定特定規則 tooallow 的傳出連線 toohello Ip。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="e1c1e-307">tooconfigure 和防火牆 (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) 存取 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="e1c1e-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="e1c1e-308">使用 Azure PowerShell SDK 版本 tooconfigure Azure 磁碟加密 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="e1c1e-309">下載 hello 最新版本[Azure PowerShell 版本](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="e1c1e-310">[Azure PowerShell SDK 1.1.0 版](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)不支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="e1c1e-311">如果您收到錯誤與相關 toousing Azure PowerShell 1.1.0，請參閱[Azure 磁碟加密相關錯誤 tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="e1c1e-312">toorun 任何 Azure CLI 命令並將它與您 Azure 訂用帳戶產生關聯，您必須先安裝 Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="e1c1e-313">tooinstall Azure CLI 和與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 及設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="e1c1e-314">toouse Azure CLI Mac、 Linux 和 Windows 使用 Azure 資源管理員中，請參閱[Resource Manager 模式中的 Azure CLI 命令](../virtual-machines/azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="e1c1e-315">加密受管理的磁碟，時必要的先決條件 tootake hello 管理磁碟的快照集或 Azure 磁碟加密先前 tooenabling 加密之外的 hello 磁碟的備份。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="e1c1e-316">若未備妥備份，任何未預期的失敗期間加密可能會讓 hello 磁碟和 VM 不含修復選項無法存取。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="e1c1e-317">設定 AzureRmVMDiskEncryptionExtension 目前未不受管理的磁碟備份，然後會發生錯誤，如果使用針對受管理的磁碟，除非已指定 hello-skipVmBackup 參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="e1c1e-318">這個參數是不安全的 toouse 除非之外 Azure 磁碟加密已進行過備份。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="e1c1e-319">指定 hello-skipVmBackup 參數時，hello cmdlet 不會使受管理的 hello 磁碟先前 tooencryption 的備份。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="e1c1e-320">基於這個理由，則會視為確定 hello 受管理磁碟 VM 處於位置先前 tooenabling Azure 磁碟加密修復是更新的備份所需的必要先決條件 toomake。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="e1c1e-321">除非快照集或備份已發出 Azure 磁碟加密外，應該永遠不會使用 hello-skipVmBackup 參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="e1c1e-322">hello Azure 磁碟加密解決方案會使用適用於 Windows 的 IaaS Vm hello BitLocker 外部金鑰保護裝置。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="e1c1e-323">對於加入網域的 VM，請勿推送任何會強制使用 TPM 保護裝置的群組原則。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="e1c1e-324">在不含相容 TPM 的允許 BitLocker"hello 群組原則的相關資訊，請參閱[BitLocker 群組原則參考](https://technet.microsoft.com/library/ee706521)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="e1c1e-325">已加入網域的虛擬機器上的 Bitlocker 原則的自訂群組原則必須包含下列設定的 hello:`Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`當 Azure 磁碟加密 Bitlocker 的自訂群組原則設定不相容時，將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="e1c1e-326">在沒有 hello 的機器上可能需要正確的原則設定，套用 hello 新原則，強制新原則 tooupdate hello (gpupdate.exe /force) 並再重新啟動。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="e1c1e-327">toocreate Azure AD 應用程式中，建立金鑰保存庫，或設定現有的金鑰保存庫並啟用加密，請參閱 hello[必要條件 PowerShell 指令碼的 Azure 磁碟加密](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="e1c1e-328">請參閱 < 使用 Azure CLI hello tooconfigure 磁碟加密必要條件[此 Bash 指令碼](https://github.com/ejarvi/ade-cli-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="e1c1e-329">toouse hello Azure 備份服務 tooback 向上及還原加密的 Vm，啟用加密時使用 Azure 磁碟加密，請使用 hello Azure 磁碟加密金鑰組態來加密您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="e1c1e-330">hello 備份服務支援 KEK 設定只會使用加密的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="e1c1e-331">請參閱[tooback 向上及還原加密使用 Azure 備份加密的虛擬機器](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="e1c1e-332">加密的 Linux 作業系統磁碟區，請注意，在 VM 重新啟動目前需要在 hello hello 程序的結尾。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="e1c1e-333">這可以透過 hello 入口網站、 powershell 或 CLI 來完成。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="e1c1e-334">tootrack hello 進度的加密，會定期輪詢 hello Get AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus 所傳回的狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="e1c1e-335">一旦完成加密，此命令傳回 hello hello 狀態訊息會指出這。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="e1c1e-336">例如，"ProgressMessage： 成功地加密作業系統磁碟，請重新啟動 hello VM"在 VM 可重新啟動及使用此點 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="e1c1e-337">適用於 Linux 的 azure 磁碟加密要求資料磁碟 toohave Linux 先前 tooencryption 掛接的檔案系統</span><span class="sxs-lookup"><span data-stu-id="e1c1e-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="e1c1e-338">以遞迴方式掛接的磁碟不會受到 hello Azure 磁碟加密適用於 Linux 的資料。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="e1c1e-339">例如，如果 hello 目標系統已掛接的磁碟上 /foo/bar，然後另 /foo/bar/baz，/foo/bar/baz hello 加密將會成功，但加密/foo/列將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="e1c1e-340">Azure 磁碟加密才支援在符合 hello 上述必要條件的支援的 Azure 資源庫映像上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="e1c1e-341">由於 toocustom 資料分割配置和處理程序的行為可能存在於這些映像不支援客戶的自訂映像。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="e1c1e-342">此外，即使以資源庫映像為基礎的 VM 一開始符合必要條件，但如果該 VM 在建立之後做過修改，則也可能會變得不相容。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="e1c1e-343">，因此，hello 建議加密 Linux VM 的程序是從全新的組件庫映像 toostart、 加密 hello VM，然後再將自訂軟體或資料 toohello 所需的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="e1c1e-344">備份與還原加密的 Vm 支援只會加密與 hello KEK 組態的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e1c1e-345">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e1c1e-346">KEK 是啟用 VM 的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="e1c1e-347">Hello Azure AD 應用程式中設定 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1c1e-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="e1c1e-348">當您需要在 Azure 中執行中的 VM 上啟用加密 toobe 時，會產生 Azure 磁碟加密，並寫入 hello 加密金鑰 tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="e1c1e-349">在金鑰保存庫中管理加密金鑰需要 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="e1c1e-350">基於此目的，請建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="e1c1e-351">您可以找到詳細的步驟槲崞紵錭 hello 「 hello 應用程式取得身分識別 」 一節中 hello 部落格文章[Azure 金鑰保存庫-Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="e1c1e-352">這篇文章也包含一些有關安裝及設定金鑰保存庫的實用範例。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="e1c1e-353">針對驗證目的，您可以使用用戶端密碼式驗證或用戶端憑證式 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="e1c1e-354">Azure AD 的用戶端密碼式驗證</span><span class="sxs-lookup"><span data-stu-id="e1c1e-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="e1c1e-355">hello 以下各節可協助您設定 Azure AD 的用戶端密碼型驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="e1c1e-356">使用 Azure PowerShell 來建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1c1e-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="e1c1e-357">使用下列 PowerShell 指令程式 toocreate Azure AD 應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="e1c1e-358">$azureAdApplication.ApplicationId hello Azure AD ClientID，而 $aadClientSecret hello 用戶端密碼，您應該使用更新版本 tooenable Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="e1c1e-359">適當地保護 hello Azure AD 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="e1c1e-360">從 hello Azure 傳統入口網站設定 hello Azure AD 用戶端識別碼和密碼</span><span class="sxs-lookup"><span data-stu-id="e1c1e-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="e1c1e-361">您也可以設定您的 Azure AD 用戶端識別碼和密碼使用 hello [Azure 傳統入口網站]( https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="e1c1e-362">tooperform 這項工作，請勿遵循 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-363">按一下 hello **Active Directory**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-363">Click hello **Active Directory** tab.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="e1c1e-365">按一下**新增應用程式**，然後類型 hello 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="e1c1e-367">按一下 hello 箭號按鈕，然後設定 hello 應用程式屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="e1c1e-369">按一下 hello 較低的左上的角 toofinish hello 核取記號。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="e1c1e-370">hello 應用程式組態 頁面隨即出現，並在 hello hello 頁面底部會顯示 hello Azure AD 用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="e1c1e-372">按一下 hello 儲存 hello Azure AD 用戶端密碼**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="e1c1e-373">請注意在 hello 索引鍵 文字方塊中的 hello Azure AD 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="e1c1e-374">適當地保護該密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-374">Safeguard it appropriately.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="e1c1e-376">hello Azure 傳統入口網站不支援 hello 上述流程。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="e1c1e-377">使用現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="e1c1e-377">Use an existing application</span></span>
<span data-ttu-id="e1c1e-378">tooexecute hello 下列命令，取得及使用 hello [Azure AD PowerShell 模組](https://technet.microsoft.com/library/jj151815.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-379">hello 下列命令必須從執行新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="e1c1e-380">請勿使用 Azure PowerShell 或 hello Azure 資源管理員視窗 tooexecute hello 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="e1c1e-381">我們建議您使用這種方法，因為這些 cmdlet 在 hello MSOnline 模組或 Azure AD PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="e1c1e-382">Azure AD 的憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="e1c1e-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="e1c1e-383">Linux VM 目前不支援 Azure AD 憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="e1c1e-384">hello 以下各節顯示如何 tooconfigure Azure AD 的憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="e1c1e-385">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1c1e-385">Create an Azure AD application</span></span>
<span data-ttu-id="e1c1e-386">toocreate Azure AD 應用程式中，執行下列 PowerShell 指令程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-387">取代下列 hello`yourpassword`安全密碼，並保護 hello 密碼的字串。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="e1c1e-388">在您完成此步驟之後上, 傳 PFX 檔案 tooyour 金鑰保存庫，並讓 hello 存取所需的原則 toodeploy 該憑證 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="e1c1e-389">使用現有的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1c1e-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="e1c1e-390">如果您要設定現有的應用程式的憑證驗證，請使用如下所示的 hello PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="e1c1e-391">要確定 tooexecute 其新的 PowerShell 視窗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="e1c1e-392">在您完成此步驟之後上, 傳 PFX 檔案 tooyour 金鑰保存庫，並啟用 hello toodeploy hello 憑證 tooa VM 所需的存取原則。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="e1c1e-393">上傳 PFX 檔案 tooyour 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="e1c1e-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="e1c1e-394">此程序的詳細說明，請參閱[hello 官方 Azure 金鑰保存庫團隊部落格](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="e1c1e-395">不過，hello 下列 PowerShell 指令程式是您只需要 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="e1c1e-396">要確定 tooexecute 從 Azure PowerShell 主控台。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-397">取代下列 hello`yourpassword`安全密碼，並保護 hello 密碼的字串。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="e1c1e-398">部署您的金鑰保存庫 tooan 現有的 VM 中的憑證</span><span class="sxs-lookup"><span data-stu-id="e1c1e-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="e1c1e-399">完成上傳 hello PFX 之後，部署 hello 金鑰保存庫 tooan hello 下列現有 VM 中的憑證：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="e1c1e-400">設定 hello hello Azure AD 應用程式的金鑰保存庫的存取原則</span><span class="sxs-lookup"><span data-stu-id="e1c1e-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="e1c1e-401">Azure AD 應用程式需要權限 tooaccess hello 金鑰或 hello 保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="e1c1e-402">使用 hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant toohello 應用程式權限，使用 hello 用戶端識別碼 （這產生 hello 應用程式註冊時） 為 hello _– ServicePrincipalName_參數值。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="e1c1e-403">toolearn 詳細資訊，請參閱 hello 部落格文章[Azure 金鑰保存庫-Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="e1c1e-404">以下是範例如何 tooperform 這工作透過 PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="e1c1e-405">Azure 磁碟加密會需要下列存取原則 tooyour Azure AD 用戶端應用程式的 tooconfigure hello: _WrapKey_和_設定_權限。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="e1c1e-406">術語</span><span class="sxs-lookup"><span data-stu-id="e1c1e-406">Terminology</span></span>
<span data-ttu-id="e1c1e-407">toounderstand 某些 hello 的通用詞彙使用這項技術，使用 hello 下術語表：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="e1c1e-408">術語</span><span class="sxs-lookup"><span data-stu-id="e1c1e-408">Terminology</span></span> | <span data-ttu-id="e1c1e-409">定義</span><span class="sxs-lookup"><span data-stu-id="e1c1e-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1c1e-410">Azure AD</span></span> | <span data-ttu-id="e1c1e-411">Azure AD 是 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="e1c1e-412">Azure AD 帳戶是從金鑰保存庫驗證、儲存和擷取密碼的必要條件。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="e1c1e-413">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="e1c1e-413">Azure Key Vault</span></span> | <span data-ttu-id="e1c1e-414">Key Vault 是密碼編譯金鑰管理服務，它是基於美國聯邦資訊處理標準 (FIPS) 驗證的硬體安全性模組，可協助您保護密碼編譯金鑰和敏感性密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="e1c1e-415">如需詳細資訊，請參閱 [Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="e1c1e-416">ARM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-416">ARM</span></span> | <span data-ttu-id="e1c1e-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e1c1e-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="e1c1e-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="e1c1e-418">BitLocker</span></span> |<span data-ttu-id="e1c1e-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx)是業界公認的 Windows 磁碟區加密技術，Windows IaaS Vm 上已使用 tooenable 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="e1c1e-420">BEK</span><span class="sxs-lookup"><span data-stu-id="e1c1e-420">BEK</span></span> | <span data-ttu-id="e1c1e-421">BitLocker 加密金鑰是使用的 tooencrypt hello OS 開機磁碟區和資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="e1c1e-422">hello BitLocker 金鑰會受金鑰保存庫中，為機密資料。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="e1c1e-423">CLI</span><span class="sxs-lookup"><span data-stu-id="e1c1e-423">CLI</span></span> | <span data-ttu-id="e1c1e-424">請參閱 [Azure 命令列介面](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="e1c1e-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="e1c1e-425">DM-Crypt</span></span> |<span data-ttu-id="e1c1e-426">[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt)是 Linux IaaS Vm 已使用 tooenable 磁碟加密的 hello 以 Linux 為基礎、 透明磁碟加密子系統。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="e1c1e-427">KEK</span><span class="sxs-lookup"><span data-stu-id="e1c1e-427">KEK</span></span> | <span data-ttu-id="e1c1e-428">Hello 非對稱金鑰 (RSA 2048)，您可以使用 tooprotect 或換行 hello 秘密金鑰加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="e1c1e-429">您可以提供硬體安全性模組 (HSM) 保護的金鑰或軟體保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="e1c1e-430">如需詳細資訊，請參閱 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="e1c1e-431">PS Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e1c1e-431">PS cmdlets</span></span> | <span data-ttu-id="e1c1e-432">請參閱 [Azure PowerShell Cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="e1c1e-433">針對 Azure 磁碟加密安裝及設定您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="e1c1e-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="e1c1e-434">Azure 磁碟加密協助保護 hello 磁碟加密金鑰和金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="e1c1e-435">Azure 磁碟加密金鑰保存庫註冊 tooset，完成 hello 每 hello 下列各節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="e1c1e-436">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="e1c1e-436">Create a key vault</span></span>
<span data-ttu-id="e1c1e-437">toocreate 金鑰保存庫，可使用其中一種 hello 下列選項：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="e1c1e-438">"101-Key-Vault-Create" Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e1c1e-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="e1c1e-439">Azure PowerShell 金鑰保存庫 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e1c1e-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="e1c1e-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e1c1e-440">Azure Resource Manager</span></span>
* <span data-ttu-id="e1c1e-441">如何太[安全金鑰保存庫](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-442">如果您已經有設定金鑰保存庫，您訂用帳戶，略過 toohello 下一節。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="e1c1e-444">設定金鑰加密金鑰 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="e1c1e-445">如果您想要 toouse KEK 額外的 hello BitLocker 加密金鑰的安全性，新增 KEK tooyour 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="e1c1e-446">使用 hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello 金鑰保存庫中的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="e1c1e-447">您也可以從內部部署金鑰管理 HSM 匯入 KEK。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="e1c1e-448">如需詳細資訊，請參閱 [Key Vault 文件](https://azure.microsoft.com/documentation/services/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="e1c1e-449">您可以加入 hello KEK 移 tooAzure 資源管理員，或使用您金鑰保存庫的介面。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="e1c1e-451">設定金鑰保存庫的權限</span><span class="sxs-lookup"><span data-stu-id="e1c1e-451">Set key vault permissions</span></span>
<span data-ttu-id="e1c1e-452">hello Azure 平台需要存取 toohello 加密金鑰或密碼中您金鑰保存庫 toomake 它們可用 toohello 開機和解密 hello 磁碟區的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="e1c1e-453">toogrant 權限 toohello Azure 平台組 hello **EnabledForDiskEncryption** hello 機碼中的屬性保存庫使用 hello 金鑰保存庫 PowerShell cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="e1c1e-454">您也可以設定 hello **EnabledForDiskEncryption**屬性，方法是瀏覽 hello [Azure 資源總管](https://resources.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="e1c1e-455">如先前所述，您必須設定 hello **EnabledForDiskEncryption**金鑰保存庫上的屬性。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="e1c1e-456">否則，hello 部署將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="e1c1e-457">您可以設定存取原則的 Azure AD 應用程式與 hello 金鑰保存庫的介面，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="e1c1e-460">在 hello**進階存取權原則**索引標籤上，請確定您的金鑰保存庫已啟用 Azure 磁碟加密：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="e1c1e-462">磁碟加密部署案例和使用者體驗</span><span class="sxs-lookup"><span data-stu-id="e1c1e-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="e1c1e-463">您可以啟用多個磁碟加密案例，並 hello 步驟可能會相應 toohello 案例而有所不同。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="e1c1e-464">hello 下列各節涵蓋 hello 更詳細的案例。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="e1c1e-465">在新建立的 hello Marketplace IaaS Vm 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="e1c1e-466">您可以啟用 hello Azure 中的服務商場中的新 IaaS Windows VM 上的磁碟加密使用 hello [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="e1c1e-467">Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e1c1e-468">Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密新的 IaaS VM 上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-469">此範本會建立新的加密的 Windows VM 使用 Windows Server 2012 hello 資源庫映像。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="e1c1e-470">您可以使用此 [Resource Manager 範本](https://aka.ms/fde-rhel)，在具有 200 GB RAID-0 陣列的新 IaaS RedHat Linux 7.2 VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="e1c1e-471">部署 hello 範本之後，請使用 hello 確認 hello VM 加密狀態`Get-AzureRmVmDiskEncryptionStatus`cmdlet，如中所述[加密作業系統磁碟機上執行的 Linux VM](#encrypting-os-drive-on-a-running-linux-vm)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="e1c1e-472">Hello 機器時傳回狀態_VMRestartPending_，重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="e1c1e-473">hello 下表列出 hello 資源管理員範本參數的新 Vm 從 hello Marketplace 案例使用 Azure AD 用戶端識別碼：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="e1c1e-474">參數</span><span class="sxs-lookup"><span data-stu-id="e1c1e-474">Parameter</span></span> | <span data-ttu-id="e1c1e-475">說明</span><span class="sxs-lookup"><span data-stu-id="e1c1e-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-476">adminUserName</span></span> | <span data-ttu-id="e1c1e-477">Hello 虛擬機器的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="e1c1e-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="e1c1e-478">adminPassword</span></span> | <span data-ttu-id="e1c1e-479">Hello 虛擬機器的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="e1c1e-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-480">newStorageAccountName</span></span> | <span data-ttu-id="e1c1e-481">Hello 儲存體帳戶 toostore OS 和資料 Vhd 的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="e1c1e-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="e1c1e-482">vmSize</span></span> | <span data-ttu-id="e1c1e-483">Hello VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-483">Size of hello VM.</span></span> <span data-ttu-id="e1c1e-484">目前僅支援標準的 A、D 和 G 系列。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="e1c1e-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-485">virtualNetworkName</span></span> | <span data-ttu-id="e1c1e-486">Hello VNet 該 hello VM NIC 的名稱都必須屬於。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e1c1e-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-487">subnetName</span></span> | <span data-ttu-id="e1c1e-488">Hello 在 hello VNet 該 hello VM NIC 的子網路名稱都必須屬於。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e1c1e-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e1c1e-489">AADClientID</span></span> | <span data-ttu-id="e1c1e-490">Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e1c1e-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e1c1e-491">AADClientSecret</span></span> | <span data-ttu-id="e1c1e-492">Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e1c1e-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-493">keyVaultURL</span></span> | <span data-ttu-id="e1c1e-494">URL 的 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e1c1e-495">您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="e1c1e-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e1c1e-497">URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰 （選擇性）。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="e1c1e-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e1c1e-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="e1c1e-499">Hello 金鑰保存庫的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="e1c1e-500">vmName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-500">vmName</span></span> | <span data-ttu-id="e1c1e-501">Hello hello 加密作業的 VM 名稱是 toobe 上執行。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="e1c1e-502">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e1c1e-503">您可以整合您自己 KEK toofurther 保護 hello 資料加密金鑰 （複雜密碼） 在金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="e1c1e-504">在透過客戶加密 VHD 和加密金鑰所建立的新 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="e1c1e-505">在此案例中，您可以啟用加密使用 hello Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="e1c1e-506">hello 下列各節說明在更詳細的 hello Resource Manager 範本和 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="e1c1e-507">從其中一個預先加密可以在 Azure 中使用的映像準備陳述式的這些章節，請遵循 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="e1c1e-508">建立 hello 映像之後，您可以使用下一個區段 toocreate hello 加密的 Azure VM 中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="e1c1e-509">準備已預先加密的 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="e1c1e-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="e1c1e-510">準備已預先加密的 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="e1c1e-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="e1c1e-511">使用 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e1c1e-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="e1c1e-512">您也可以使用 hello 加密 VHD 上啟用磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="e1c1e-513">Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e1c1e-514">Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密 hello 新 IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="e1c1e-515">hello 下表列出 hello 資源管理員範本參數的加密 VHD:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="e1c1e-516">參數</span><span class="sxs-lookup"><span data-stu-id="e1c1e-516">Parameter</span></span> | <span data-ttu-id="e1c1e-517">說明</span><span class="sxs-lookup"><span data-stu-id="e1c1e-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-518">newStorageAccountName</span></span> | <span data-ttu-id="e1c1e-519">名稱的 hello 儲存體帳戶 toostore hello 加密 OS VHD。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="e1c1e-520">這個儲存體帳戶應該已經建立 hello 中相同的資源群組和 hello VM 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="e1c1e-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="e1c1e-521">osVhdUri</span></span> | <span data-ttu-id="e1c1e-522">Hello OS VHD 從 hello 儲存體帳戶的 URI。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="e1c1e-523">osType</span><span class="sxs-lookup"><span data-stu-id="e1c1e-523">osType</span></span> | <span data-ttu-id="e1c1e-524">作業系統產品類型 (Windows/Linux)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="e1c1e-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-525">virtualNetworkName</span></span> | <span data-ttu-id="e1c1e-526">Hello VNet 該 hello VM NIC 的名稱都必須屬於。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="e1c1e-527">hello 名稱應該已經建立 hello 中相同的資源群組和 hello VM 相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="e1c1e-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-528">subnetName</span></span> | <span data-ttu-id="e1c1e-529">Hello hello VNet 該 hello VM NIC 上的子網路名稱都必須屬於。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e1c1e-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="e1c1e-530">vmSize</span></span> | <span data-ttu-id="e1c1e-531">Hello VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-531">Size of hello VM.</span></span> <span data-ttu-id="e1c1e-532">目前僅支援標準的 A、D 和 G 系列。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="e1c1e-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="e1c1e-533">keyVaultResourceID</span></span> | <span data-ttu-id="e1c1e-534">hello ResourceID 識別 hello Azure 資源管理員中的金鑰保存庫資源。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="e1c1e-535">您可以使用 hello PowerShell cmdlet 來取得`(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="e1c1e-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="e1c1e-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="e1c1e-537">設定 hello 金鑰保存庫中的 hello 磁碟加密金鑰的 URL。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="e1c1e-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="e1c1e-538">keyVaultKekUrl</span></span> | <span data-ttu-id="e1c1e-539">Hello hello 產生磁碟加密金鑰加密的金鑰的加密金鑰的 URL。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="e1c1e-540">vmName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-540">vmName</span></span> | <span data-ttu-id="e1c1e-541">Hello IaaS VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="e1c1e-542">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e1c1e-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="e1c1e-543">您也可以使用 hello PowerShell cmdlet 在您已加密的 VHD 上啟用磁碟加密[ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="e1c1e-544">使用 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="e1c1e-544">Using CLI commands</span></span>
<span data-ttu-id="e1c1e-545">tooenable 磁碟加密，此案例中使用 CLI 命令，不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-546">設定金鑰保存庫的存取原則：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="e1c1e-547">設定 hello **EnabledForDiskEncryption**旗標：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="e1c1e-548">設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="e1c1e-549">在現有或未執行 VM，型別上 tooenable 加密：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="e1c1e-550">取得加密狀態：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="e1c1e-551">新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="e1c1e-552">在 Azure 中現有或執行中的 IaaS Windows VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="e1c1e-553">在此案例中，您可以啟用加密使用 hello Resource Manager 範本、 PowerShell cmdlet 或 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="e1c1e-554">hello 下列各節詳細說明如何 tooenable 它使用 hello Resource Manager 範本和 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="e1c1e-555">使用 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="e1c1e-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="e1c1e-556">您可以啟用現有的或使用 hello 在 Azure 中執行 IaaS Windows Vm 上的磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="e1c1e-557">Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 加密組態**參數**刀鋒視窗中，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e1c1e-558">Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable hello 現有或執行 IaaS VM 上的加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="e1c1e-559">hello 下表列出針對現有的或執行 Vm 所使用的 Azure AD 用戶端識別碼 hello 資源管理員範本參數：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="e1c1e-560">參數</span><span class="sxs-lookup"><span data-stu-id="e1c1e-560">Parameter</span></span> | <span data-ttu-id="e1c1e-561">說明</span><span class="sxs-lookup"><span data-stu-id="e1c1e-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e1c1e-562">AADClientID</span></span> | <span data-ttu-id="e1c1e-563">Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e1c1e-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e1c1e-564">AADClientSecret</span></span> | <span data-ttu-id="e1c1e-565">Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e1c1e-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-566">keyVaultName</span></span> | <span data-ttu-id="e1c1e-567">名稱 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e1c1e-568">您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="e1c1e-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e1c1e-570">URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="e1c1e-571">這個參數是選擇性，如果您選取**nokek** hello UseExistingKek 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="e1c1e-572">如果您選取**kek**在 hello UseExistingKek 下拉式清單中，您必須輸入 hello _keyEncryptionKeyURL_值。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="e1c1e-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="e1c1e-573">volumeType</span></span> | <span data-ttu-id="e1c1e-574">Hello 加密作業執行的磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="e1c1e-575">有效值為 _OS_、_Data_ 和 _All_。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="e1c1e-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e1c1e-576">sequenceVersion</span></span> | <span data-ttu-id="e1c1e-577">序列版的 hello BitLocker 作業。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e1c1e-578">每次磁碟加密作業不會對 hello 遞增此版本號碼相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="e1c1e-579">vmName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-579">vmName</span></span> | <span data-ttu-id="e1c1e-580">Hello hello 加密作業的 VM 名稱是 toobe 上執行。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="e1c1e-581">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e1c1e-582">您可以將自己 KEK toofurther 保護 hello 資料加密金鑰 （BitLocker 加密機密） 帶入 hello 金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="e1c1e-583">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e1c1e-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="e1c1e-584">如需使用 PowerShell cmdlet 來啟用與 Azure 磁碟加密的加密資訊，請參閱 hello 部落格文章[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="e1c1e-585">使用 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="e1c1e-585">Using CLI commands</span></span>
<span data-ttu-id="e1c1e-586">在現有的或使用 CLI 命令，在 Azure 中執行 IaaS Windows VM 上 tooenable 加密 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-587">tooset hello 金鑰保存庫中的存取原則：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="e1c1e-588">設定 hello **EnabledForDiskEncryption**旗標：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="e1c1e-589">設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="e1c1e-590">在現有或未執行 VM 上 tooenable 加密：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="e1c1e-591">tooget 加密的狀態：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="e1c1e-592">新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="e1c1e-593">在 Azure 中現有或執行中的 IaaS Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="e1c1e-594">您可以啟用磁碟上現有的或執行 IaaS Linux VM 在 Azure 中的加密使用 hello [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="e1c1e-595">按一下**部署 tooAzure** hello Azure 快速入門在範本上，輸入 hello 加密組態上 hello**參數**刀鋒視窗中，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e1c1e-596">Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable hello 現有或執行 IaaS VM 上的加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="e1c1e-597">hello 下表列出針對現有的或執行 Vm，使用 Azure AD 用戶端識別碼，資源管理員範本參數：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="e1c1e-598">參數</span><span class="sxs-lookup"><span data-stu-id="e1c1e-598">Parameter</span></span> | <span data-ttu-id="e1c1e-599">說明</span><span class="sxs-lookup"><span data-stu-id="e1c1e-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e1c1e-600">AADClientID</span></span> | <span data-ttu-id="e1c1e-601">Hello Azure AD 應用程式，其權限 toowrite 密碼 toohello 金鑰保存庫的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e1c1e-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e1c1e-602">AADClientSecret</span></span> | <span data-ttu-id="e1c1e-603">Hello Azure AD 應用程式，其權限 toowrite 密碼 tooyour 金鑰保存庫的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e1c1e-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-604">keyVaultName</span></span> | <span data-ttu-id="e1c1e-605">名稱 hello 金鑰保存庫的 BitLocker 金鑰應該上傳至該 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e1c1e-606">您可以使用 hello cmdlet 來取得`(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="e1c1e-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e1c1e-608">URL 是使用的 tooencrypt hello 的 hello 金鑰的加密金鑰的產生 BitLocker 金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="e1c1e-609">這個參數是選擇性，如果您選取**nokek** hello UseExistingKek 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="e1c1e-610">如果您選取**kek**在 hello UseExistingKek 下拉式清單中，您必須輸入 hello _keyEncryptionKeyURL_值。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="e1c1e-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="e1c1e-611">volumeType</span></span> | <span data-ttu-id="e1c1e-612">Hello 加密作業執行的磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="e1c1e-613">支援的有效值為 _OS_ 或 _All_ (適用於 RHEL 7.2、CentOS 7.2 和 Ubuntu 16.04)，和 _Data_ (適用於所有其他的散發套件)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="e1c1e-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e1c1e-614">sequenceVersion</span></span> | <span data-ttu-id="e1c1e-615">序列版的 hello BitLocker 作業。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e1c1e-616">每次磁碟加密作業不會對 hello 遞增此版本號碼相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="e1c1e-617">vmName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-617">vmName</span></span> | <span data-ttu-id="e1c1e-618">Hello hello 加密作業的 VM 名稱是 toobe 上執行。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="e1c1e-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="e1c1e-619">passPhrase</span></span> | <span data-ttu-id="e1c1e-620">輸入強式複雜密碼做為 hello 資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="e1c1e-621">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e1c1e-622">您可以整合您自己 KEK toofurther 保護 hello 資料加密金鑰 （複雜密碼） 在金鑰保存庫中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="e1c1e-623">CLI 命令</span><span class="sxs-lookup"><span data-stu-id="e1c1e-623">CLI commands</span></span>
<span data-ttu-id="e1c1e-624">您可以啟用磁碟加密加密 VHD 上安裝和使用 hello [CLI 命令](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="e1c1e-625">在現有的或使用 CLI 命令，在 Azure 中執行 IaaS Linux Vm 上 tooenable 加密 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-626">Hello 金鑰保存庫中設定存取原則：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="e1c1e-627">設定 hello **EnabledForDiskEncryption**旗標：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="e1c1e-628">設定權限 tooAzure AD 應用程式 toowrite 密碼 tooyour 金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="e1c1e-629">在現有或未執行 VM 上 tooenable 加密：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="e1c1e-630">取得加密狀態：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="e1c1e-631">新的 VM，從您加密 VHD，使用下列參數以 hello 的 hello tooenable 加密`azure vm create`命令：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="e1c1e-632">取得加密的 IaaS VM hello 加密狀態</span><span class="sxs-lookup"><span data-stu-id="e1c1e-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="e1c1e-633">您可以使用 Azure 資源管理員，取得 hello 加密狀態[PowerShell cmdlet](/powershell/azure/overview)，或 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="e1c1e-634">hello 下列各節說明 toouse hello Azure 傳統入口網站和 CLI 命令 tooget hello 加密狀態。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="e1c1e-635">使用 Azure 資源管理員取得加密的 Windows VM hello 加密狀態</span><span class="sxs-lookup"><span data-stu-id="e1c1e-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="e1c1e-636">您可以藉由 hello 下列取得 hello 加密的 hello IaaS VM 的狀態從 Azure 資源管理員：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="e1c1e-637">登入 toohello [Azure 傳統入口網站](https://portal.azure.com/)，然後按一下**虛擬機器**hello 左的窗格 toosee hello 您訂用帳戶中的虛擬機器的摘要檢視中。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="e1c1e-638">您可以篩選 hello 虛擬機器 檢視中 hello 選取 hello 訂用帳戶名稱**訂用帳戶**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="e1c1e-639">頂端的 hello hello**虛擬機器**頁面上，按一下**資料行**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="e1c1e-640">在 hello**選擇資料行**刀鋒視窗中，選取**磁碟加密**，然後按一下**更新**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="e1c1e-641">您應該會看到 hello 磁碟加密資料行顯示 hello 加密狀態_啟用_或_未啟用_針對每個 VM，hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="e1c1e-643">使用 hello 磁碟加密 PowerShell cmdlet 來取得 hello 加密的加密 (Windows/Linux) IaaS VM 的狀態</span><span class="sxs-lookup"><span data-stu-id="e1c1e-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="e1c1e-644">您可以從 hello 磁碟加密 PowerShell cmdlet 來取得 hello IaaS VM hello 加密狀態`Get-AzureRmVMDiskEncryptionStatus`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="e1c1e-645">tooget hello 加密設定，讓您的 VM，請輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="e1c1e-646">您可以檢查的 hello 輸出_Get AzureRmVMDiskEncryptionStatus_加密金鑰的 Url。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="e1c1e-647">hello OSVolumeEncrypted 和 DataVolumesEncrypted 設定值會設定 too_Encrypted_，會顯示這兩個磁碟區使用 Azure 磁碟加密進行加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="e1c1e-648">如需使用 PowerShell cmdlet 來啟用與 Azure 磁碟加密的加密資訊，請參閱 hello 部落格文章[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[瀏覽 Azure 磁碟加密使用 Azure PowerShell-第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-649">Linux Vm 上花費三 toofour 分鐘 hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello 加密狀態。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="e1c1e-650">收到 hello 磁碟加密 CLI 命令的 hello IaaS VM 的 hello 加密狀態</span><span class="sxs-lookup"><span data-stu-id="e1c1e-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="e1c1e-651">您可以使用 hello 磁碟加密 CLI 命令，以取得 IaaS VM hello hello 加密狀態`azure vm show-disk-encryption-status`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="e1c1e-652">tooget hello 加密設定，讓您的 VM，請輸入您的 Azure CLI 工作階段：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="e1c1e-653">在執行中 Windows IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="e1c1e-654">您可以停用加密透過 hello Azure 磁碟加密 Resource Manager 範本或 PowerShell cmdlet 執行的 Windows 或 Linux IaaS VM，並指定 hello 解密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="e1c1e-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-655">Windows VM</span></span>
<span data-ttu-id="e1c1e-656">hello 停用加密步驟會停用加密 hello OS、 hello 資料磁碟區，或兩者上執行 Windows IaaS VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="e1c1e-657">您無法停用 hello OS 磁碟區，並保留 hello 資料磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="e1c1e-658">Hello 停用加密步驟執行時，hello Azure 傳統部署模型更新 hello VM 的服務模型，且會標示解密 hello Windows IaaS VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="e1c1e-659">hello VM hello 內容已不再加密在靜止。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="e1c1e-660">hello 解密並不會刪除您金鑰保存庫和 hello 加密金鑰內容 （BitLocker 加密金鑰適用於 Windows 和 Linux 的複雜密碼）。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="e1c1e-661">Linux VM</span><span class="sxs-lookup"><span data-stu-id="e1c1e-661">Linux VM</span></span>
<span data-ttu-id="e1c1e-662">hello 停用加密步驟會停用加密 hello hello 執行 Linux IaaS VM 上的資料量。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="e1c1e-663">如果 hello OS 磁碟未加密，僅適用於此步驟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-664">在 Linux Vm 上不允許停用加密 hello OS 磁碟上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="e1c1e-665">在現有或執行中 IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="e1c1e-666">您可以停用對於執行 Windows IaaS Vm 中使用 hello 磁碟加密[Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="e1c1e-667">Hello Azure 快速入門在範本上，按一下 **部署 tooAzure**，hello 上輸入 hello 解密組態**參數**刀鋒視窗中，然後再按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e1c1e-668">Hello 訂用帳戶、 資源群組、 資源群組位置、 法律條款和協議中，選取，然後按一下**建立**tooenable 加密新的 IaaS VM 上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="e1c1e-669">適用於 Linux Vm，您可以使用停用加密 hello[停用執行中的 Linux VM 上的加密](https://aka.ms/decrypt-linuxvm)範本。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="e1c1e-670">hello 下表列出用來停用加密，在執行中的 IaaS VM 上的資源管理員範本參數：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="e1c1e-671">參數</span><span class="sxs-lookup"><span data-stu-id="e1c1e-671">Parameter</span></span> | <span data-ttu-id="e1c1e-672">說明</span><span class="sxs-lookup"><span data-stu-id="e1c1e-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1c1e-673">vmName</span><span class="sxs-lookup"><span data-stu-id="e1c1e-673">vmName</span></span> | <span data-ttu-id="e1c1e-674">Hello hello 加密作業的 VM 名稱是 toobe 上執行。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="e1c1e-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="e1c1e-675">volumeType</span></span> | <span data-ttu-id="e1c1e-676">執行解密作業所在磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="e1c1e-677">有效值為 _OS_、_Data_ 和 _All_。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="e1c1e-678">您無法停用加密不在執行上 Windows IaaS VM OS/開機磁碟區停用加密 hello_資料_磁碟區。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="e1c1e-679">也請注意，停用加密 hello OS 磁碟上不允許在 Linux Vm 上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="e1c1e-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e1c1e-680">sequenceVersion</span></span> | <span data-ttu-id="e1c1e-681">序列版的 hello BitLocker 作業。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e1c1e-682">每次磁碟解密作業不會對 hello 遞增此版本號碼相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="e1c1e-683">在現有或執行中 IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="e1c1e-684">toodisable 加密上現有的或執行 IaaS VM 使用 hello PowerShell cmdlet，請參閱[ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="e1c1e-685">此 Cmdlet 同時支援 Windows 和 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="e1c1e-686">toodisable 加密，它會在 hello 虛擬機器上安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="e1c1e-687">如果 hello_名稱_未指定參數，hello 預設名稱的延伸模組_Windows Vm AzureDiskEncryption_建立。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="e1c1e-688">在 Linux Vm 上使用 hello AzureDiskEncryptionForLinux 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="e1c1e-689">此 cmdlet 會重新啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e1c1e-690">在具有 Azure 受管理磁碟且預先加密的 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="e1c1e-691">使用加密的 VM，從使用 hello ARM 範本預先加密的 VHD 位於 hello Azure 受管理磁碟臂範本 toocreate</span><span class="sxs-lookup"><span data-stu-id="e1c1e-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="e1c1e-692">[從預先加密的 VHD/儲存體 blob 建立新的已加密受管理磁碟] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e1c1e-693">在具有 Azure 受管理磁碟的新 Linux IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="e1c1e-694">使用新的加密使用 hello ARM 範本位於 Linux IaaS VM 的 hello Azure 受管理磁碟臂範本 toocreate</span><span class="sxs-lookup"><span data-stu-id="e1c1e-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="e1c1e-695">[使用完整磁碟加密部署 RHEL 7.2] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e1c1e-696">在具有 Azure 受管理磁碟的新 Windows IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="e1c1e-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="e1c1e-697">使用新的加密使用 hello ARM 範本位於 Linux IaaS VM 的 hello Azure 受管理磁碟臂範本 toocreate</span><span class="sxs-lookup"><span data-stu-id="e1c1e-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="e1c1e-698">[從資源庫映像建立新的已加密 Windows IaaS 受管理磁碟 VM] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="e1c1e-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="e1c1e-699">它是強制性 toosnapshot 及/或備份的受管理的磁碟基礎的外部 VM 執行個體和先前 tooenabling Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="e1c1e-700">Hello 受管理磁碟的快照集可以取自 hello 入口網站，或可以使用 Azure 備份。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="e1c1e-701">備份確保復原選項可以在 hello 案例中的任何未預期的失敗期間加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="e1c1e-702">建立備份之後，hello 組 AzureRmVMDiskEncryptionExtension 指令程式可以藉由指定 hello-skipVmBackup 參數是使用的 tooencrypt 管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="e1c1e-703">在建立好備份並指定了這個參數之前，對以受控磁碟為基礎的 VM 執行這個命令都將會失敗。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="e1c1e-704">現有已加密非高階 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="e1c1e-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="e1c1e-705">使用 hello 現有 Azure 磁碟加密支援的介面執行 VM [PS 指令程式，CLI 或 ARM 範本] tooupdate hello 加密設定喜歡 AAD 用戶端識別碼/密碼、 加密金鑰 [KEK]，Windows VM 或複雜密碼的 BitLocker 加密金鑰只有非 premium 儲存體所支援的 Vm 支援 Linux VM 等 hello 更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="e1c1e-706">不支援高階儲存體所支援 VM 的。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="e1c1e-707">附錄</span><span class="sxs-lookup"><span data-stu-id="e1c1e-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="e1c1e-708">連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e1c1e-708">Connect tooyour subscription</span></span>
<span data-ttu-id="e1c1e-709">在繼續之前，檢閱 hello*必要條件*〉 一節。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="e1c1e-710">確定已符合所有必要條件之後，請進行 hello 下列連接 tooyour 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="e1c1e-711">啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="e1c1e-712">如果您有多個訂用帳戶，而且想 toospecify 一個 toouse，輸入下列帳戶 toosee hello 訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="e1c1e-713">您想 toouse，toospecify hello 訂用帳戶類型：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="e1c1e-714">tooverify hello 訂用帳戶設定正確無誤，輸入：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="e1c1e-715">tooconfirm hello Azure 磁碟加密會安裝 cmdlet，類型：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="e1c1e-716">hello 下列輸出會確認 hello Azure 磁碟加密 PowerShell 安裝：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="e1c1e-717">準備已預先加密的 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="e1c1e-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="e1c1e-718">hello 以下各節是必要的 tooprepare 預先加密為加密的 VHD 在 Azure IaaS 中部署 Windows VHD。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="e1c1e-719">使用 hello 資訊 tooprepare 和開機全新 Windows VM (VHD)，在 Azure Site Recovery 或 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="e1c1e-720">更新群組原則 tooallow 非 TPM OS 保護</span><span class="sxs-lookup"><span data-stu-id="e1c1e-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="e1c1e-721">設定 hello BitLocker 群組原則設定**BitLocker 磁碟機加密**，這會在下看到**本機電腦原則** > **電腦設定**  > **系統管理範本** > **Windows 元件**。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="e1c1e-722">變更此設定太**作業系統磁碟機** > **需要在啟動時的其他驗證** > **不含相容 TPM允許使用BitLocker**hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="e1c1e-724">安裝 BitLocker 功能元件</span><span class="sxs-lookup"><span data-stu-id="e1c1e-724">Install BitLocker feature components</span></span>
<span data-ttu-id="e1c1e-725">Windows Server 2012 和更新版本中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="e1c1e-726">Windows Server 2008 R2，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="e1c1e-727">使用 BitLocker 的準備 hello OS 磁碟區`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="e1c1e-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="e1c1e-728">toocompress hello OS 磁碟分割和 BitLocker 的準備 hello 機器，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="e1c1e-729">使用 BitLocker 來保護 hello OS 磁碟區</span><span class="sxs-lookup"><span data-stu-id="e1c1e-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="e1c1e-730">使用 hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx)命令 tooenable 加密使用外部的金鑰保護裝置 hello 開機磁碟區上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="e1c1e-731">此外 hello 外接式磁碟機或磁碟區上放置 hello 外部索引鍵 （.bek 檔案）。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="e1c1e-732">Hello 下次重新開機後 hello 系統/開機磁碟區上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="e1c1e-733">做好使用 BitLocker 取得 hello 外部索引鍵與個別資料/資源 VHD hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="e1c1e-734">在執行中的 Linux VM 上加密 OS 磁碟機</span><span class="sxs-lookup"><span data-stu-id="e1c1e-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="e1c1e-735">加密作業系統磁碟機上執行的 Linux VM 的支援下列散發 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="e1c1e-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="e1c1e-736">RHEL 7.2</span></span>
* <span data-ttu-id="e1c1e-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="e1c1e-737">CentOS 7.2</span></span>
* <span data-ttu-id="e1c1e-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e1c1e-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="e1c1e-739">OS 磁碟加密的必要條件</span><span class="sxs-lookup"><span data-stu-id="e1c1e-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="e1c1e-740">從 Marketplace 映像 hello Azure 資源管理員中，必須先建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="e1c1e-741">具有至少 4 GB RAM 的 Azure VM (建議大小為 7 GB)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="e1c1e-742">(適用於 RHEL 和 CentOS) 停用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="e1c1e-743">toodisable SELinux，請參閱 「 4.4.2。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="e1c1e-744">以停用 SELinux"hello [SELinux 使用者和系統管理員指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux)hello VM 上。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="e1c1e-745">停用 SELinux 之後，重新啟動 hello VM 至少一次。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="e1c1e-746">步驟</span><span class="sxs-lookup"><span data-stu-id="e1c1e-746">Steps</span></span>
1. <span data-ttu-id="e1c1e-747">建立 VM 使用其中一種 hello 先前指定的分佈。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="e1c1e-748">若為 CentOS 7.2，支援透過特殊映像加密 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="e1c1e-749">toouse 此映像，指定 「 7.2n"hello SKU，當您建立 hello VM 為：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="e1c1e-750">設定 hello VM 相應 tooyour 需求。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="e1c1e-751">如果您正在 tooencrypt hello （OS + 資料） 的所有磁碟機，hello 資料磁碟機就會需要 toobe 指定和從 /etc/fstab 裝載。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="e1c1e-752">使用 UUID =...toospecify /etc/hosts fstab 而不是指定 hello 區塊裝置名稱 (例如，/dev/sdb1) 中的資料磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="e1c1e-753">在加密期間，hello hello VM 上的磁碟機變更的順序。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="e1c1e-754">如果您的 VM 依賴封鎖裝置的特定順序，它將會失敗 toomount 它們加密之後。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="e1c1e-755">登出 hello SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="e1c1e-756">tooencrypt hello 的作業系統上，指定做為 volumeType**所有**或**OS**時您[啟用加密](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="e1c1e-757">未以 `systemd` 服務的形式執行的所有使用者空間程序皆應使用 `SIGKILL` 來終止。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="e1c1e-758">重新啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-758">Reboot hello VM.</span></span> <span data-ttu-id="e1c1e-759">當您在執行中的 VM 上啟用 OS 磁碟加密時，請規劃 VM 停機時間。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="e1c1e-760">定期監視加密進度 hello 使用 hello hello 指示[下一節](#monitoring-os-encryption-progress)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="e1c1e-761">Get AzureRmVmDiskEncryptionStatus 顯示 「 VMRestartPending 」 之後，重新啟動您的 VM 在 tooit 登入或使用 hello 入口網站、 PowerShell 或 CLI。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="e1c1e-762">您重新開機之前，我們建議您儲存[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="e1c1e-763">監視 OS 加密進度</span><span class="sxs-lookup"><span data-stu-id="e1c1e-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="e1c1e-764">有三種方式可監視 OS 加密進度：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="e1c1e-765">使用 hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet，並檢查 hello ProgressMessage 欄位：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="e1c1e-766">Hello VM 達到 「 作業系統磁碟加密已啟動 」 之後，它會有約 40 too50 分鐘高階儲存體的備份 VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="e1c1e-767">由於 WALinuxAgent 發生 [388 號問題](https://github.com/Azure/WALinuxAgent/issues/388)，某些散發套件的 `OsVolumeEncrypted` 和 `DataVolumesEncrypted` 會顯示為 `Unknown`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="e1c1e-768">若使用 WALinuxAgent 2.1.5 和更新版本，就會自動修正此問題。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="e1c1e-769">如果您看到`Unknown`在 hello 輸出中，您可以使用 hello Azure 資源總管確認磁碟加密狀態。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="e1c1e-770">跳過[Azure 資源總管](https://resources.azure.com/)，然後展開左側 hello 選取面板中的此階層：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="e1c1e-771">在 hello InstanceView，捲動 toosee hello 加密狀態，您的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![VM 執行個體檢視](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="e1c1e-773">查看[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="e1c1e-774">訊息從 hello ADE 延伸前面應該要有`[AzureDiskEncryption]`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="e1c1e-775">登入 toohello 透過 SSH 的 VM，並取得 hello 延伸模組中的記錄檔：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="e1c1e-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="e1c1e-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="e1c1e-777">我們建議，您沒有登入 toohello VM OS 加密進行中時。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="e1c1e-778">Hello 其他兩個方法都失敗時才複製 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="e1c1e-779">準備已預先加密的 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="e1c1e-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="e1c1e-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="e1c1e-780">Ubuntu 16</span></span>
<span data-ttu-id="e1c1e-781">設定加密 hello 發佈安裝期間執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="e1c1e-782">選取**設定加密的磁碟區**當您分割 hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="e1c1e-784">另外建立一個不得加密的開機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="e1c1e-785">加密根磁碟機。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="e1c1e-787">提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-787">Provide a passphrase.</span></span> <span data-ttu-id="e1c1e-788">這是您上傳 toohello 金鑰保存庫的 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="e1c1e-790">完成分割。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="e1c1e-792">當您啟動 hello VM，並會要求輸入複雜密碼時，使用您在步驟 3 中提供的 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="e1c1e-794">將上傳至 Azure 中，使用準備 hello VM[這些指示](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="e1c1e-795">請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="e1c1e-796">設定使用 Azure 加密 toowork 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="e1c1e-797">建立 hello 下列指令碼中的 hello 內容 /usr/local/sbin/azure_crypt_key.sh 下的檔案。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="e1c1e-798">因為它是供 Azure hello 複雜密碼的檔案名稱，請特別注意 toohello KeyFileName。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="e1c1e-799">變更中的 hello crypt config */etc/hosts crypttab*。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="e1c1e-800">它看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="e1c1e-801">如果您要編輯*azure_crypt_key.sh* Windows 和您在複製它 tooLinux，執行`dos2unix /usr/local/sbin/azure_crypt_key.sh`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="e1c1e-802">加入可執行檔的權限 toohello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="e1c1e-803">以加上程式碼行的方式編輯 /etc/initramfs-tools/modules：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="e1c1e-804">執行`update-initramfs -u -k all`tooupdate hello initramfs toomake hello`keyscript`才會生效。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="e1c1e-805">現在您可以取消佈建 hello VM。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-805">Now you can deprovision hello VM.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="e1c1e-807">繼續下一個步驟中 toohello 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="e1c1e-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="e1c1e-808">openSUSE 13.2</span></span>
<span data-ttu-id="e1c1e-809">tooconfigure 加密 hello 發佈在安裝期間，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="e1c1e-810">當您分割 hello 磁碟時，請選取**加密磁碟區群組**，然後輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="e1c1e-811">這是您要上傳 tooyour 金鑰保存庫的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="e1c1e-813">開機 hello VM 使用您的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-813">Boot hello VM using your password.</span></span>

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="e1c1e-815">準備 hello VM 中的 hello 指示上載 tooAzure [SLES 或 openSUSE 虛擬機器做好 Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="e1c1e-816">請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="e1c1e-817">有了 Azure，tooconfigure 加密 toowork hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="e1c1e-818">編輯 hello /etc/dracut.conf 並加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="e1c1e-819">Hello hello 結束這行程式碼的註解檔案 /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="e1c1e-820">附加在 hello 檔案 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 開頭的行下 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="e1c1e-821">變更所有出現的：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="e1c1e-822">至：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="e1c1e-823">編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh，並將其附加到太 「 # 開啟 LUKS 裝置 」:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="e1c1e-824">執行`/usr/sbin/dracut -f -v`tooupdate hello initrd。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="e1c1e-825">現在您可以取消佈建 hello VM 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="e1c1e-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="e1c1e-826">CentOS 7</span></span>
<span data-ttu-id="e1c1e-827">tooconfigure 加密 hello 發佈在安裝期間，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="e1c1e-828">在分割磁碟時選取 [加密資料]。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="e1c1e-830">確定已為根分割選取 [加密]。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="e1c1e-832">提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-832">Provide a passphrase.</span></span> <span data-ttu-id="e1c1e-833">這是您要上傳 tooyour 金鑰保存庫的 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="e1c1e-835">當您啟動 hello VM，並會要求輸入複雜密碼時，使用您在步驟 3 中提供的 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="e1c1e-837">上傳至 Azure，使用中的 hello"CentOS 7.0 + 」 指示準備 hello VM [CentOS 為基礎的虛擬機器做好 Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="e1c1e-838">請勿執行 hello 最後一個步驟 (解除佈建 hello VM)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="e1c1e-839">現在您可以取消佈建 hello VM 和[上傳 VHD](#upload-encrypted-vhd-to-an-azure-storage-account)至 Azure。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="e1c1e-840">有了 Azure，tooconfigure 加密 toowork hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="e1c1e-841">編輯 hello /etc/dracut.conf 並加入以下的 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="e1c1e-842">Hello hello 結束這行程式碼的註解檔案 /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="e1c1e-843">附加在 hello 檔案 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello 開頭的行下 hello:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="e1c1e-844">變更所有出現的：</span><span class="sxs-lookup"><span data-stu-id="e1c1e-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="e1c1e-845">to</span><span class="sxs-lookup"><span data-stu-id="e1c1e-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="e1c1e-846">編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 並附加之後 hello 「 # 開啟 LUKS 裝置 」:</span><span class="sxs-lookup"><span data-stu-id="e1c1e-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="e1c1e-847">執行 hello"/ usr/來啟動/dracut-f-v"tooupdate hello initrd。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="e1c1e-849">上傳加密的 VHD tooan Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e1c1e-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="e1c1e-850">在啟用 BitLocker 加密或 DM Crypt 加密之後，hello 本機加密 VHD 需要上傳 toobe tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="e1c1e-851">上傳 hello 預先加密 VM tooyour 金鑰保存庫的 hello 磁碟加密密碼</span><span class="sxs-lookup"><span data-stu-id="e1c1e-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="e1c1e-852">您所取得的 hello 磁碟加密密碼之前必須上傳做為金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="e1c1e-853">hello 金鑰保存庫需要 toohave 磁碟加密，並啟用您的 Azure AD 用戶端權限。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="e1c1e-854">未使用 KEK 加密的磁碟加密密碼</span><span class="sxs-lookup"><span data-stu-id="e1c1e-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="e1c1e-855">註冊您的金鑰保存庫，使用中的 hello 密碼 tooset[組 AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="e1c1e-856">如果您有 Windows 虛擬機器，hello bek 檔案編碼為 base64 字串，然後再上傳 tooyour 金鑰保存庫使用 hello `Set-AzureKeyVaultSecret` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="e1c1e-857">適用於 Linux，hello 複雜密碼會編碼為 base64 字串，然後再上傳 toohello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="e1c1e-858">此外，請確定下列標記該 hello 會設定當您建立 hello 金鑰保存庫中的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="e1c1e-859">使用 hello `$secretUrl` hello 下一個步驟中[附加 hello OS 磁碟，而不使用 KEK](#without-using-a-kek)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="e1c1e-860">使用 KEK 加密的磁碟加密密碼</span><span class="sxs-lookup"><span data-stu-id="e1c1e-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="e1c1e-861">您上傳 hello toohello 秘密金鑰保存庫之前，您可以選擇性地加密它所使用的加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="e1c1e-862">使用 hello 包裝[API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst 加密 hello 使用 hello 金鑰的加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="e1c1e-863">hello 這個 wrap 作業的輸出是 base64 URL 編碼字串，如此您可以再使用上傳做為密碼 hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="e1c1e-864">使用`$KeyEncryptionKey`和`$secretUrl`hello 下一個步驟中[附加 hello OS 磁碟使用 KEK](#using-a-kek)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="e1c1e-865">連接 OS 磁碟時，指定密碼的 URL</span><span class="sxs-lookup"><span data-stu-id="e1c1e-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="e1c1e-866">不使用 KEK</span><span class="sxs-lookup"><span data-stu-id="e1c1e-866">Without using a KEK</span></span>
<span data-ttu-id="e1c1e-867">雖然您正在附加 hello OS 磁碟，您需要 toopass `$secretUrl`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="e1c1e-868">產生 hello 「 未加密的 KEK 與磁碟加密密碼 」 一節中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="e1c1e-869">使用 KEK</span><span class="sxs-lookup"><span data-stu-id="e1c1e-869">Using a KEK</span></span>
<span data-ttu-id="e1c1e-870">當您附加 hello OS 磁碟時，傳遞`$KeyEncryptionKey`和`$secretUrl`。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="e1c1e-871">產生 hello 「 未加密的 KEK 與磁碟加密密碼 」 一節中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="e1c1e-872">下載此指南</span><span class="sxs-lookup"><span data-stu-id="e1c1e-872">Download this guide</span></span>
<span data-ttu-id="e1c1e-873">您可以下載本指南從 hello [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)。</span><span class="sxs-lookup"><span data-stu-id="e1c1e-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="e1c1e-874">取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e1c1e-874">For more information</span></span>
[<span data-ttu-id="e1c1e-875">探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 1 部分</span><span class="sxs-lookup"><span data-stu-id="e1c1e-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="e1c1e-876">探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分</span><span class="sxs-lookup"><span data-stu-id="e1c1e-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
