---
title: "Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密 | Microsoft Docs"
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
ms.openlocfilehash: a4f20fc19ae40561d042d5cff744a030014f75c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="6d1ca-103">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="6d1ca-104">Microsoft Azure 強烈承諾確保您的資料隱私權、資料主權，並透過一系列進階技術來加密、控制和管理加密金鑰、控制和稽核資料存取，讓您控制您的 Azure 託管資料。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-104">Microsoft Azure is strongly committed to ensuring your data privacy, data sovereignty and enables you to control your Azure hosted data through a range of advanced technologies to encrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="6d1ca-105">這會提供 Azure 客戶靈活度，可選擇最符合其商務需求的解決方案。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-105">This provides Azure customers the flexibility to choose the solution that best meets their business needs.</span></span> <span data-ttu-id="6d1ca-106">本文中，我們將為您介紹新的技術解決方案「Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密」，以協助保護及保障您的資料，以便符合組織的安全性和符合性的承諾。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-106">In this paper, we will introduce you to a new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” to help protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="6d1ca-107">本文提供有關如何使用 Azure 磁碟加密功能的詳細指引，包括支援的案例和使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-107">The paper provides detailed guidance on how to use the Azure disk encryption features including the supported scenarios and the user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-108">某些建議可能會增加資料、網路或計算資源的使用量，導致額外的授權或訂用帳戶成本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="6d1ca-109">概觀</span><span class="sxs-lookup"><span data-stu-id="6d1ca-109">Overview</span></span>
<span data-ttu-id="6d1ca-110">Azure 磁碟加密是協助您加密 Windows 和 Linux IaaS 虛擬機器磁碟的新功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="6d1ca-111">Azure 磁碟加密利用 Windows 的業界標準 [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) 功能和 Linux 的 [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 功能，為 OS 和資料磁碟提供磁碟區加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-111">Azure Disk Encryption leverages the industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and the [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux to provide volume encryption for the OS and the data disks.</span></span> <span data-ttu-id="6d1ca-112">此解決方案與 [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) 整合，協助您控制及管理金鑰保存庫訂用帳戶中的磁碟加密金鑰與密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-112">The solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) to help you control and manage the disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="6d1ca-113">此解決方案也可確保虛擬機器磁碟上的所有待用資料都會在您的 Azure 儲存體中加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-113">The solution also ensures that all data on the virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="6d1ca-114">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密現已在所有 Azure 公用區域和 AzureGov 區域**正式推出**，可供用於標準 VM 和具有高階儲存體的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="6d1ca-115">加密案例</span><span class="sxs-lookup"><span data-stu-id="6d1ca-115">Encryption scenarios</span></span>
<span data-ttu-id="6d1ca-116">Azure 磁碟加密解決方案支援下列客戶案例：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-116">The Azure Disk Encryption solution supports the following customer scenarios:</span></span>

* <span data-ttu-id="6d1ca-117">對透過加密的 VHD 和加密金鑰建立的新 IaaS VM 啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="6d1ca-118">對透過受支援 Azure 資源庫映像建立的新 IaaS VM 啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-118">Enable encryption on new IaaS VMs created from the supported Azure Gallery images</span></span>
* <span data-ttu-id="6d1ca-119">在 Azure 中執行的現有 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="6d1ca-120">在 Windows IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="6d1ca-121">在 Linux IaaS VM 的資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="6d1ca-122">允許加密受管理磁碟 VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="6d1ca-123">現有已加密非高階儲存體 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="6d1ca-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="6d1ca-124">備份與還原以金鑰加密金鑰進行加密的已加密 VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="6d1ca-125">在 Microsoft Azure 中啟用時，解決方案會對 IaaS VM 支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-125">The solution supports the following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="6d1ca-126">與 Azure 金鑰保存庫整合</span><span class="sxs-lookup"><span data-stu-id="6d1ca-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="6d1ca-127">標準層 VM：[A、D、DS、G、GS、F 等系列 IaaS VM](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="6d1ca-128">對透過受支援 Azure 資源庫映像的 Windows 和 Linux IaaS VM 以及受控磁碟 VM 啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from the supported Azure Gallery images</span></span>
* <span data-ttu-id="6d1ca-129">在 Windows IaaS VM 與受管理磁碟 VM 的作業系統與資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="6d1ca-130">在 Linux IaaS VM 與受管理磁碟 VM 的資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="6d1ca-131">在執行 Windows Client OS 的 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="6d1ca-132">在具有掛接路徑的磁碟區上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="6d1ca-133">使用 mdadm 在設定了磁碟串接 (RAID) 的 Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="6d1ca-134">使用資料磁碟適用的 LVM 在 Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="6d1ca-135">在設定了儲存空間的 Windows VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="6d1ca-136">現有已加密非高階儲存體 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="6d1ca-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="6d1ca-137">支援所有 Azure 公用區域與 AzureGov 區域</span><span class="sxs-lookup"><span data-stu-id="6d1ca-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="6d1ca-138">此解決方案不支援下列案例、功能和技術：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-138">The solution does not support the following scenarios, features, and technology:</span></span>

* <span data-ttu-id="6d1ca-139">基本層 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="6d1ca-140">在 Linux IaaS VM 的 OS 磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="6d1ca-141">如果已加密 Linux IaaS VM 的 OS 磁碟機，請將資料磁碟機上的加密停用</span><span class="sxs-lookup"><span data-stu-id="6d1ca-141">Disabling encryption on a data drive if the OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="6d1ca-142">使用傳統 VM 建立方法所建立的 IaaS VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-142">IaaS VMs that are created by using the classic VM creation method</span></span>
* <span data-ttu-id="6d1ca-143">「不」支援透過 Windows 和 Linux IaaS VM 客戶自訂映像上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="6d1ca-144">目前不支援在 Linux LVM OS 磁碟機上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="6d1ca-145">此支援會立即出現。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-145">This support will come soon.</span></span>
* <span data-ttu-id="6d1ca-146">與您的內部部署金鑰管理服務整合</span><span class="sxs-lookup"><span data-stu-id="6d1ca-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="6d1ca-147">Azure 檔案 (共用檔案系統)、網路檔案系統 (NFS)、動態磁碟區和以軟體型 RAID 系統所設定的 Windows VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="6d1ca-148">備份與還原不以金鑰加密金鑰進行加密的已加密 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="6d1ca-149">現有已加密高階儲存體 VM 的更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-150">只有使用 KEK 組態加密的 VM 支援備份和還原已加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="6d1ca-151">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="6d1ca-152">KEK 是啟用 VM 加密的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="6d1ca-153">即將提供此支援。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-153">This support is coming soon.</span></span>
> <span data-ttu-id="6d1ca-154">不支援現有已加密高階儲存體 VM 的更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="6d1ca-155">即將提供此支援。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="6d1ca-156">加密功能</span><span class="sxs-lookup"><span data-stu-id="6d1ca-156">Encryption features</span></span>
<span data-ttu-id="6d1ca-157">為 Azure IaaS VM 啟用並部署 Azure 磁碟加密時，會啟用下列功能，視提供的組態而定：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, the following capabilities are enabled, depending on the configuration provided:</span></span>

* <span data-ttu-id="6d1ca-158">加密 OS 磁碟區以保護儲存體中的待用開機磁碟區</span><span class="sxs-lookup"><span data-stu-id="6d1ca-158">Encryption of the OS volume to protect the boot volume at rest in your storage</span></span>
* <span data-ttu-id="6d1ca-159">加密資料磁碟區以保護儲存體中的待用資料磁碟區</span><span class="sxs-lookup"><span data-stu-id="6d1ca-159">Encryption of data volumes to protect the data volumes at rest in your storage</span></span>
* <span data-ttu-id="6d1ca-160">在 Windows IaaS VM 的 OS 和資料磁碟機上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-160">Disabling encryption on the OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="6d1ca-161">在 Linux IaaS VM 的資料磁碟機上停用加密 (僅在 OS 磁碟機「並未」加密時)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-161">Disabling encryption on the data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="6d1ca-162">保護金鑰保存庫訂用帳戶中的加密金鑰和密碼</span><span class="sxs-lookup"><span data-stu-id="6d1ca-162">Safeguarding the encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="6d1ca-163">報告已加密 IaaS VM 的加密狀態</span><span class="sxs-lookup"><span data-stu-id="6d1ca-163">Reporting the encryption status of the encrypted IaaS VM</span></span>
* <span data-ttu-id="6d1ca-164">從 IaaS 虛擬機器移除磁碟加密組態設定</span><span class="sxs-lookup"><span data-stu-id="6d1ca-164">Removal of disk-encryption configuration settings from the IaaS virtual machine</span></span>
* <span data-ttu-id="6d1ca-165">使用 Azure 備份服務來備份和還原已加密的 VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-165">Backup and restore of encrypted VMs by using the Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-166">只有使用 KEK 組態加密的 VM 支援備份和還原已加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="6d1ca-167">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="6d1ca-168">KEK 是啟用 VM 加密的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="6d1ca-169">Windows 和 Linux IaaS VM 適用的 Azure 磁碟加密解決方案包含：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="6d1ca-170">Windows 的磁碟加密擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-170">The disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="6d1ca-171">Linux 的磁碟加密擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-171">The disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="6d1ca-172">磁碟加密 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-172">The disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="6d1ca-173">磁碟加密 Azure 命令列介面 (CLI) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-173">The disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="6d1ca-174">磁碟加密 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-174">The disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="6d1ca-175">執行 Windows 或 Linux OS 的 IaaS VM 支援 Azure 磁碟加密解決方案。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-175">The Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="6d1ca-176">如需支援的作業系統相關詳細資訊，請參閱「必要條件」一節。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-176">For more information about the supported operating systems, see the "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-177">使用 Azure 磁碟加密來加密 VM 磁碟完全免費。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="6d1ca-178">價值主張</span><span class="sxs-lookup"><span data-stu-id="6d1ca-178">Value proposition</span></span>
<span data-ttu-id="6d1ca-179">當您套用 Azure 磁碟加密管理解決方案時，可滿足下列商務需求：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-179">When you apply the Azure Disk Encryption-management solution, you can satisfy the following business needs:</span></span>

* <span data-ttu-id="6d1ca-180">待用 IaaS VM 會受到保護，因您使用了業界標準的加密技術解決組織安全性和合規性的需求。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology to address organizational security and compliance requirements.</span></span>
* <span data-ttu-id="6d1ca-181">IaaS VM 會在客戶控制的金鑰和原則下開機，且您可以在金鑰保存庫中稽核其使用狀況。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="6d1ca-182">加密工作流程</span><span class="sxs-lookup"><span data-stu-id="6d1ca-182">Encryption workflow</span></span>
<span data-ttu-id="6d1ca-183">若要啟用 Windows 和 Linux VM 的磁碟加密，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-183">To enable disk encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="6d1ca-184">從先前的加密案例中選擇一個加密案例。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-184">Choose an encryption scenario from among the preceding encryption scenarios.</span></span>
2. <span data-ttu-id="6d1ca-185">選擇透過 Azure 磁碟加密 Resource Manager 範本、PowerShell Cmdlet 或 CLI 命令啟用磁碟加密，並指定加密組態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-185">Opt in to enabling disk encryption via the Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify the encryption configuration.</span></span>

   * <span data-ttu-id="6d1ca-186">針對客戶加密的 VHD 案例，請將加密的 VHD 上傳至儲存體帳戶並將加密金鑰資料上傳至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-186">For the customer-encrypted VHD scenario, upload the encrypted VHD to your storage account and the encryption key material to your key vault.</span></span> <span data-ttu-id="6d1ca-187">接著，提供加密組態資訊以在新的 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-187">Then, provide the encryption configuration to enable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="6d1ca-188">針對透過 Marketplace 所建立的新 VM 和已在 Azure 中執行的現有 VM，提供加密組態以在 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-188">For new VMs that are created from the Marketplace and existing VMs that are already running in Azure, provide the encryption configuration to enable encryption on the IaaS VM.</span></span>

3. <span data-ttu-id="6d1ca-189">授與存取至 Azure 平台，以從您的金鑰保存庫讀取加密金鑰資料 (Windows 系統的 BitLocker 加密金鑰和 Linux 的複雜密碼)，藉以在 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-189">Grant access to the Azure platform to read the encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault to enable encryption on the IaaS VM.</span></span>

4. <span data-ttu-id="6d1ca-190">提供 Azure Active Directory (Azure AD) 應用程式身分識別，以將加密金鑰資料寫入至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-190">Provide the Azure Active Directory (Azure AD) application identity to write the encryption key material to your key vault.</span></span> <span data-ttu-id="6d1ca-191">如此可針對步驟 2 中所述的案例在 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-191">Doing so enables encryption on the IaaS VM for the scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="6d1ca-192">Azure 會使用加密和金鑰保存庫組態更新 VM 服務模型，並建立加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-192">Azure updates the VM service model with encryption and the key vault configuration, and sets up your encrypted VM.</span></span>

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="6d1ca-194">解密工作流程</span><span class="sxs-lookup"><span data-stu-id="6d1ca-194">Decryption workflow</span></span>
<span data-ttu-id="6d1ca-195">若要停用 IaaS VM 的磁碟加密，請完成下列高階步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-195">To disable disk encryption for IaaS VMs, complete the following high-level steps:</span></span>

1. <span data-ttu-id="6d1ca-196">選擇透過 Azure 磁碟加密 Resource Manager 範本或 PowerShell Cmdlet，在 Azure 中的執行中 IaaS VM 上停用加密 (解密)，並指定解密組態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-196">Choose to disable encryption (decryption) on a running IaaS VM in Azure via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify the decryption configuration.</span></span>

 <span data-ttu-id="6d1ca-197">此步驟會在執行中 Windows IaaS VM 上停用 OS 或資料磁碟區或兩者的加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-197">This step disables encryption of the OS or the data volume or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="6d1ca-198">但是如前一節所述，並不支援停用 Linux 的 OS 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-198">However, as mentioned in the previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="6d1ca-199">只要 OS 磁碟機未加密，就只允許對 Linux VM 上的資料磁碟機執行解密步驟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-199">The decryption step is allowed only for data drives on Linux VMs as long as the OS disk is not encrypted.</span></span>
2. <span data-ttu-id="6d1ca-200">Azure 會更新 VM 服務模型，且 IaaS VM 會標示為已解密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-200">Azure updates the VM service model, and the IaaS VM is marked decrypted.</span></span> <span data-ttu-id="6d1ca-201">VM 的待用內容不會再加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-201">The contents of the VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-202">停用加密作業並不會刪除您的金鑰保存庫和加密金鑰資料 (Windows 系統的 BitLocker 加密金鑰或 Linux 的複雜密碼)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-202">The disable-encryption operation does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="6d1ca-203">不支援停用 Linux 適用的作業系統磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="6d1ca-204">只允許對 Linux VM 上的資料磁碟機執行解密步驟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-204">The decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="6d1ca-205">如果 OS 磁碟機已加密，就不支援將 Linux 的資料磁碟加密停用。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-205">Disabling data disk encryption for Linux is not supported if the OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d1ca-206">必要條件</span><span class="sxs-lookup"><span data-stu-id="6d1ca-206">Prerequisites</span></span>
<span data-ttu-id="6d1ca-207">針對「概觀」一節所提到支援的案例，在 Azure IaaS VM 上啟用 Azure 磁碟加密之前，請參閱下列必要條件：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for the supported scenarios that were discussed in the "Overview" section, see the following prerequisites:</span></span>

* <span data-ttu-id="6d1ca-208">您必須擁有有效的作用中 Azure 訂用帳戶，才能在 Azure 支援的區域中建立資源。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-208">You must have a valid active Azure subscription to create resources in Azure in the supported regions.</span></span>
* <span data-ttu-id="6d1ca-209">下列 Windows Server 版本支援 Azure 磁碟加密：Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 和 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-209">Azure Disk Encryption is supported on the following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="6d1ca-210">下列 Windows 用戶端版本支援 Azure 磁碟加密：Windows 8 Client 和 Windows 10 Client。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-210">Azure Disk Encryption is supported on the following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-211">針對 Windows Server 2008 R2，您必須先安裝 .NET Framework 4.5，才能在 Azure 中啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="6d1ca-212">您可以透過安裝選用的更新 Windows Server 2008 R2 x64 型系統的 Microsoft .NET Framework 4.5.2 ([KB2901983](https://support.microsoft.com/kb/2901983))，從 Windows Update 安裝它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-212">You can install it from Windows Update by installing the optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="6d1ca-213">在下列以 Azure 資源庫為基礎的 Linux 伺服器散發套件和版本上支援 Azure 磁碟加密︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-213">Azure Disk Encryption is supported on the following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="6d1ca-214">Linux 散發套件</span><span class="sxs-lookup"><span data-stu-id="6d1ca-214">Linux Distribution</span></span> | <span data-ttu-id="6d1ca-215">版本</span><span class="sxs-lookup"><span data-stu-id="6d1ca-215">Version</span></span> | <span data-ttu-id="6d1ca-216">支援加密的磁碟區類型</span><span class="sxs-lookup"><span data-stu-id="6d1ca-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="6d1ca-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d1ca-217">Ubuntu</span></span> | <span data-ttu-id="6d1ca-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="6d1ca-219">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-219">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d1ca-220">Ubuntu</span></span> | <span data-ttu-id="6d1ca-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="6d1ca-222">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-222">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d1ca-223">Ubuntu</span></span> | <span data-ttu-id="6d1ca-224">12.10</span><span class="sxs-lookup"><span data-stu-id="6d1ca-224">12.10</span></span> | <span data-ttu-id="6d1ca-225">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-225">Data disk</span></span> |
| <span data-ttu-id="6d1ca-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d1ca-226">Ubuntu</span></span> | <span data-ttu-id="6d1ca-227">12.04</span><span class="sxs-lookup"><span data-stu-id="6d1ca-227">12.04</span></span> | <span data-ttu-id="6d1ca-228">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-228">Data disk</span></span> |
| <span data-ttu-id="6d1ca-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-229">RHEL</span></span> | <span data-ttu-id="6d1ca-230">7.3</span><span class="sxs-lookup"><span data-stu-id="6d1ca-230">7.3</span></span> | <span data-ttu-id="6d1ca-231">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-231">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-232">RHEL</span></span> | <span data-ttu-id="6d1ca-233">7.2</span><span class="sxs-lookup"><span data-stu-id="6d1ca-233">7.2</span></span> | <span data-ttu-id="6d1ca-234">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-234">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-235">RHEL</span></span> | <span data-ttu-id="6d1ca-236">6.8</span><span class="sxs-lookup"><span data-stu-id="6d1ca-236">6.8</span></span> | <span data-ttu-id="6d1ca-237">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-237">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-238">RHEL</span></span> | <span data-ttu-id="6d1ca-239">6.7</span><span class="sxs-lookup"><span data-stu-id="6d1ca-239">6.7</span></span> | <span data-ttu-id="6d1ca-240">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-240">Data disk</span></span> |
| <span data-ttu-id="6d1ca-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-241">CentOS</span></span> | <span data-ttu-id="6d1ca-242">7.3</span><span class="sxs-lookup"><span data-stu-id="6d1ca-242">7.3</span></span> | <span data-ttu-id="6d1ca-243">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-243">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-244">CentOS</span></span> | <span data-ttu-id="6d1ca-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="6d1ca-245">7.2n</span></span> | <span data-ttu-id="6d1ca-246">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-246">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-247">CentOS</span></span> | <span data-ttu-id="6d1ca-248">6.8</span><span class="sxs-lookup"><span data-stu-id="6d1ca-248">6.8</span></span> | <span data-ttu-id="6d1ca-249">作業系統和資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-249">OS and Data disk</span></span> |
| <span data-ttu-id="6d1ca-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-250">CentOS</span></span> | <span data-ttu-id="6d1ca-251">7.1</span><span class="sxs-lookup"><span data-stu-id="6d1ca-251">7.1</span></span> | <span data-ttu-id="6d1ca-252">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-252">Data disk</span></span> |
| <span data-ttu-id="6d1ca-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-253">CentOS</span></span> | <span data-ttu-id="6d1ca-254">7.0</span><span class="sxs-lookup"><span data-stu-id="6d1ca-254">7.0</span></span> | <span data-ttu-id="6d1ca-255">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-255">Data disk</span></span> |
| <span data-ttu-id="6d1ca-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-256">CentOS</span></span> | <span data-ttu-id="6d1ca-257">6.7</span><span class="sxs-lookup"><span data-stu-id="6d1ca-257">6.7</span></span> | <span data-ttu-id="6d1ca-258">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-258">Data disk</span></span> |
| <span data-ttu-id="6d1ca-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-259">CentOS</span></span> | <span data-ttu-id="6d1ca-260">6.6</span><span class="sxs-lookup"><span data-stu-id="6d1ca-260">6.6</span></span> | <span data-ttu-id="6d1ca-261">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-261">Data disk</span></span> |
| <span data-ttu-id="6d1ca-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="6d1ca-262">CentOS</span></span> | <span data-ttu-id="6d1ca-263">6.5</span><span class="sxs-lookup"><span data-stu-id="6d1ca-263">6.5</span></span> | <span data-ttu-id="6d1ca-264">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-264">Data disk</span></span> |
| <span data-ttu-id="6d1ca-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6d1ca-265">openSUSE</span></span> | <span data-ttu-id="6d1ca-266">13.2</span><span class="sxs-lookup"><span data-stu-id="6d1ca-266">13.2</span></span> | <span data-ttu-id="6d1ca-267">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-267">Data disk</span></span> |
| <span data-ttu-id="6d1ca-268">SLES</span><span class="sxs-lookup"><span data-stu-id="6d1ca-268">SLES</span></span> | <span data-ttu-id="6d1ca-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="6d1ca-269">12 SP1</span></span> | <span data-ttu-id="6d1ca-270">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-270">Data disk</span></span> |
| <span data-ttu-id="6d1ca-271">SLES</span><span class="sxs-lookup"><span data-stu-id="6d1ca-271">SLES</span></span> | <span data-ttu-id="6d1ca-272">12-SP1 (高階)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="6d1ca-273">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-273">Data disk</span></span> |
| <span data-ttu-id="6d1ca-274">SLES</span><span class="sxs-lookup"><span data-stu-id="6d1ca-274">SLES</span></span> | <span data-ttu-id="6d1ca-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="6d1ca-275">HPC 12</span></span> | <span data-ttu-id="6d1ca-276">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-276">Data disk</span></span> |
| <span data-ttu-id="6d1ca-277">SLES</span><span class="sxs-lookup"><span data-stu-id="6d1ca-277">SLES</span></span> | <span data-ttu-id="6d1ca-278">11-SP4 (高階)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="6d1ca-279">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-279">Data disk</span></span> |
| <span data-ttu-id="6d1ca-280">SLES</span><span class="sxs-lookup"><span data-stu-id="6d1ca-280">SLES</span></span> | <span data-ttu-id="6d1ca-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="6d1ca-281">11 SP4</span></span> | <span data-ttu-id="6d1ca-282">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-282">Data disk</span></span> |

* <span data-ttu-id="6d1ca-283">Azure 磁碟加密需要您的金鑰保存庫和 VM 位於相同的 Azure 區域和訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-283">Azure Disk Encryption requires that your key vault and VMs reside in the same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-284">若在不同的區域設定資源，會導致 Azure 磁碟加密功能啟用失敗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-284">Configuring the resources in separate regions causes a failure in enabling the Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="6d1ca-285">若要安裝及設定 Azure 磁碟加密的金鑰保存庫，請參閱本文＜必要條件＞一節中的**安裝及設定 Azure 磁碟加密的金鑰保存庫**。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-285">To set up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="6d1ca-286">若要針對 Azure 磁碟加密在 Azure Active Directory 中安裝與設定 Azure AD 應用程式 ，請參閱本文＜必要條件＞一節中的**在 Azure Active Directory 中設定 Azure AD 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-286">To set up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up the Azure AD application in Azure Active Directory** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="6d1ca-287">若要針對 Azure AD 應用程式安裝與設定金鑰保存庫存取原則，請參閱本文＜必要條件＞一節中的**設定 Azure AD 應用程式的金鑰保存庫存取原則**</span><span class="sxs-lookup"><span data-stu-id="6d1ca-287">To set up and configure the key vault access policy for the Azure AD application, see section **Set up the key vault access policy for the Azure AD application** in the *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="6d1ca-288">若要準備預先加密的 Windows VHD，請參閱＜附錄＞中的**準備預先加密的 Windows VHD** 一節。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-288">To prepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="6d1ca-289">若要準備預先加密的 Linux VHD，請參閱＜附錄＞中的**準備預先加密的 Linux VHD** 一節。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-289">To prepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in the *Appendix*.</span></span>
* <span data-ttu-id="6d1ca-290">Azure 平台需要存取您金鑰保存庫中的加密金鑰或密碼，讓它們可供虛擬機器用來開機和解密虛擬機器作業系統磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-290">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the virtual machine when it boots and decrypts the virtual machine OS volume.</span></span> <span data-ttu-id="6d1ca-291">若要授與權限至 Azure 平台，請設定金鑰保存庫中的 **EnabledForDiskEncryption** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-291">To grant permissions to Azure platform, set the **EnabledForDiskEncryption** property in the key vault.</span></span> <span data-ttu-id="6d1ca-292">如需詳細資訊，請參閱＜附錄＞中的**安裝及設定 Azure 磁碟加密的金鑰保存庫**。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in the Appendix.</span></span>
* <span data-ttu-id="6d1ca-293">您的金鑰保存庫密碼和 KEK URL 必須已設定版本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="6d1ca-294">Azure 會強制執行設定版本的這項限制。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="6d1ca-295">針對有效的密碼和 KEK URL，請參閱下列範例︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-295">For valid secret and KEK URLs, see the following examples:</span></span>

  * <span data-ttu-id="6d1ca-296">有效祕密 URL 的範例︰https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d1ca-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="6d1ca-297">有效 KEK URL 的範例：https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d1ca-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="6d1ca-298">Azure 磁碟加密不支援將連接埠號碼指定為金鑰保存庫密碼和 KEK URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="6d1ca-299">如需不支援和支援的金鑰保存庫 URL 範例，請參閱下列各項︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-299">For examples of non-supported and supported key vault URLs, see the following:</span></span>

  * <span data-ttu-id="6d1ca-300">無法接受的金鑰保存庫 URL https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d1ca-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="6d1ca-301">可接受的金鑰保存庫 URL：https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="6d1ca-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="6d1ca-302">若要啟用 Azure 磁碟加密功能，IaaS VM 必須符合下列網路端點組態需求：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-302">To enable the Azure Disk Encryption feature, the IaaS VMs must meet the following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="6d1ca-303">若要取得用來連線至金鑰保存庫的權杖，IaaS VM 必須能連線至 Azure Active Directory 端點 \[login.microsoftonline.com\]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-303">To get a token to connect to your key vault, the IaaS VM must be able to connect to an Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="6d1ca-304">若要將加密金鑰寫入至您的金鑰保存庫，IaaS VM 必須能連接至金鑰保存庫端點。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-304">To write the encryption keys to your key vault, the IaaS VM must be able to connect to the key vault endpoint.</span></span>
  * <span data-ttu-id="6d1ca-305">IaaS VM 必須能連接至託管 Azure 擴充儲存機制的 Azure 儲存體端點，和託管 VHD 檔案的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-305">The IaaS VM must be able to connect to an Azure storage endpoint that hosts the Azure extension repository and an Azure storage account that hosts the VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="6d1ca-306">如果您的安全性原則會限制從 Azure VM 至網際網路的存取，您可以解析前述的 URI，並設定特定的規則以允許和這些 IP 的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-306">If your security policy limits access from Azure VMs to the Internet, you can resolve the preceding URI and configure a specific rule to allow outbound connectivity to the IPs.</span></span>
  >
  ><span data-ttu-id="6d1ca-307">設定與存取防火牆後的 Azure 金鑰保存庫 (英文) (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-307">To configure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="6d1ca-308">使用最新版的 Azure PowerShell SDK 版本來設定 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-308">Use the latest version of Azure PowerShell SDK version to configure Azure Disk Encryption.</span></span> <span data-ttu-id="6d1ca-309">下載最新版的 [Azure PowerShell 版本](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-309">Download the latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="6d1ca-310">[Azure PowerShell SDK 1.1.0 版](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016)不支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="6d1ca-311">如果您收到與使用 Azure PowerShell 1.1.0 相關的錯誤，請參閱[與 Azure PowerShell 1.1.0 相關的 Azure 磁碟加密錯誤](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-311">If you are receiving an error related to using Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related to Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="6d1ca-312">若要執行任何 Azure CLI 命令並使其與您的 Azure 訂用帳戶建立關聯，您必須先安裝 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-312">To run any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="6d1ca-313">若要安裝 Azure CLI 並使其與您的 Azure 訂用帳戶建立關聯，請參閱[如何安裝和設定 Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-313">To install Azure CLI and associate it with your Azure subscription, see [How to install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="6d1ca-314">若要使用適用於 Mac、Linux 和 Windows 的 Azure CLI 搭配 Azure Resource Manager，請參閱 [Resource Manager 模式中的 Azure CLI 命令](../virtual-machines/azure-cli-arm-commands.md)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-314">To use Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="6d1ca-315">在加密受控磁碟時，必要的先決條件是先擷取受控磁碟的快照集或先在 Azure 磁碟加密之外備份磁碟再啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-315">When encrypting a managed disk, it is mandatory prerequisite to take a snapshot of the managed disk or a backup of the disk outside of Azure Disk Encryption prior to enabling encryption.</span></span>  <span data-ttu-id="6d1ca-316">若未備妥備份，當加密期間發生任何未預期的失敗時，將可能會讓磁碟和 VM 變得無法存取又沒有復原選項。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-316">Without a backup in place, any unexpected failure during encryption may render the disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="6d1ca-317">Set-AzureRmVMDiskEncryptionExtension 目前不會備份受控磁碟，而且除非指定了 -skipVmBackup 參數，否則在針對受控磁碟使用時將會發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless the -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="6d1ca-318">除非您已在 Azure 磁碟加密之外建立備份，否則使用此參數並不安全。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-318">This parameter is unsafe to use unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="6d1ca-319">若指定了 -skipVmBackup 參數，此 Cmdlet 在執行加密之前將不會先備份受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-319">When the -skipVmBackup parameter is specified, the cmdlet will not make a backup of the managed disk prior to encryption.</span></span>  <span data-ttu-id="6d1ca-320">因此，我們才會認為必要的先決條件就是先備妥受控磁碟 VM 的備份，再啟用 Azure 磁碟加密，以防之後需要進行復原。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-320">For this reason, it is considered a mandatory prerequisite to make sure a backup of the managed disk VM is in place prior to enabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="6d1ca-321">除非您已在 Azure 磁碟加密之外建立快照集或備份，否則請永遠不要使用 -skipVmBackup 參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-321">The -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="6d1ca-322">Azure 磁碟加密解決方案對 Windows IaaS VM 使用 BitLocker 外部金鑰保護裝置。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-322">The Azure Disk Encryption solution uses the BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="6d1ca-323">對於加入網域的 VM，請勿推送任何會強制使用 TPM 保護裝置的群組原則。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="6d1ca-324">如需關於「在不含相容 TPM 的情形下允許使用 BitLocker」的群組原則相關資訊，請參閱 [BitLocker 群組原則參考文件](https://technet.microsoft.com/library/ee706521)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-324">For information about the group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="6d1ca-325">適用於具有自訂群組原則且已加入網域之虛擬機器上的 Bitlocker 原則必須包含下列設定：`Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` 當 Bitlocker 的自訂群組原則設定不相容時，Azure 磁碟加密將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-325">Bitlocker policy on domain joined virtual machines with custom group policy must include the following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="6d1ca-326">在沒有正確原則設定的電腦上，您可能必須套用新的原則、強制新的原則進行更新 (gpupdate.exe /force)，然後重新啟動。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-326">On machines that did not have the correct policy setting, applying the new policy, forcing the new policy to update (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="6d1ca-327">若要建立 Azure AD 應用程式、建立金鑰保存庫或設定現有的金鑰保存庫並啟用加密，請參閱 [Azure 磁碟加密的必要條件 PowerShell 指令碼](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-327">To create an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see the [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="6d1ca-328">若要使用 Azure CLI 設定磁碟加密必要條件，請參閱[此 Bash 指令碼](https://github.com/ejarvi/ade-cli-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-328">To configure disk-encryption prerequisites using the Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="6d1ca-329">若要使用 Azure 備份服務來備份和還原已加密的 VM，在透過 Azure 磁碟加密啟用加密時，請使用 Azure 磁碟加密金鑰組態來加密您的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-329">To use the Azure Backup service to back up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using the Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="6d1ca-330">備份服務只支援使用 KEK 組態加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-330">The Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="6d1ca-331">請參閱[如何使用 Azure 備份加密來備份與還原加密的虛擬機器](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption) (英文)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-331">See [How to back up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="6d1ca-332">在加密 Linux 作業系統磁碟區時請注意，您目前需要在加密程序結束時重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-332">When encrypting a Linux OS volume, note that a VM restart is currently required at the end of the process.</span></span> <span data-ttu-id="6d1ca-333">這可以透過入口網站、PowerShell 或 CLI 來完成。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-333">This can be done via the portal, powershell, or CLI.</span></span>   <span data-ttu-id="6d1ca-334">若要追蹤加密進度，請定期輪詢 Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus 所傳回的狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-334">To track the progress of encryption, periodically poll the status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="6d1ca-335">加密完成後，此命令所傳回的狀態訊息將會指出這一點。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-335">Once encryption is complete, the the status message returned by this command will indicate this.</span></span>  <span data-ttu-id="6d1ca-336">例如，「ProgressMessage：已成功加密作業系統磁碟，請重新啟動 VM」。此時即可重新啟動及使用 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot the VM"  At this point the VM can be restarted and used.</span></span>  

* <span data-ttu-id="6d1ca-337">適用於 Linux 的 Azure 磁碟加密會要求資料磁碟先在 Linux 中擁有已掛接的檔案系統，然後才會執行加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-337">Azure Disk Encryption for Linux requires data disks to have a mounted file system in Linux prior to encryption</span></span>

* <span data-ttu-id="6d1ca-338">適用於 Linux 的 Azure 磁碟加密不支援遞迴掛接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-338">Recursively mounted data disks are not supported by the Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="6d1ca-339">例如，如果目標系統已在 /foo/bar 掛接一個磁碟，又在 /foo/bar/baz 掛接另一個磁碟，則 /foo/bar/baz 的加密會成功，但 /foo/bar 的加密則會失敗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-339">For example, if the target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, the encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="6d1ca-340">只有符合上述必要條件的 Azure 資源庫支援的映像才會支援 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet the aforementioned prerequisites.</span></span> <span data-ttu-id="6d1ca-341">由於客戶自訂映像上可能存在自訂的資料分割配置和流程表現方式，因此系統不支援這些映像。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-341">Customer custom images are not supported due to custom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="6d1ca-342">此外，即使以資源庫映像為基礎的 VM 一開始符合必要條件，但如果該 VM 在建立之後做過修改，則也可能會變得不相容。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="6d1ca-343">為此，建議的 Linux VM 加密程序是從全新的資源庫映像來開始、加密 VM，然後再視需要於 VM 中新增自訂軟體或資料。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-343">For that reason, the suggested procedure for encrypting a Linux VM is to start from a clean gallery image, encrypt the VM, and then add custom software or data to the VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="6d1ca-344">只有使用 KEK 組態加密的 VM 支援備份和還原已加密的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with the KEK configuration.</span></span> <span data-ttu-id="6d1ca-345">未使用 KEK 加密的 VM 則不支援。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="6d1ca-346">KEK 是啟用 VM 的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-the-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="6d1ca-347">在 Azure Active Directory 中設定 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d1ca-347">Set up the Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="6d1ca-348">當您需要在 Azure 中執行中的 VM 上啟用加密時，Azure 磁碟加密會產生並將加密金鑰寫入金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-348">When you need encryption to be enabled on a running VM in Azure, Azure Disk Encryption generates and writes the encryption keys to your key vault.</span></span> <span data-ttu-id="6d1ca-349">在金鑰保存庫中管理加密金鑰需要 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="6d1ca-350">基於此目的，請建立 Azure AD 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="6d1ca-351">您可以在部落格文章 [Azure Key Vault - 逐步解說](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)的「取得應用程式的身分識別」一節中找到註冊應用程式的詳細步驟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-351">You can find detailed steps for registering an application in the “Get an Identity for the Application” section of the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="6d1ca-352">這篇文章也包含一些有關安裝及設定金鑰保存庫的實用範例。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="6d1ca-353">針對驗證目的，您可以使用用戶端密碼式驗證或用戶端憑證式 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="6d1ca-354">Azure AD 的用戶端密碼式驗證</span><span class="sxs-lookup"><span data-stu-id="6d1ca-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="6d1ca-355">下列各節可協助您設定 Azure AD 的用戶端密碼式驗證。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-355">The sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="6d1ca-356">使用 Azure PowerShell 來建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d1ca-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="6d1ca-357">使用下列 PowerShell Cmdlet 建立 Azure AD 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-357">Use the following PowerShell cmdlet to create an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="6d1ca-358">$azureAdApplication.ApplicationId 是 Azure AD ClientID，而 $aadClientSecret 是用戶端密碼，您稍後應該會用該資訊來啟用 Azure 磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-358">$azureAdApplication.ApplicationId is the Azure AD ClientID and $aadClientSecret is the client secret that you should use later to enable Azure Disk Encryption.</span></span> <span data-ttu-id="6d1ca-359">適當地保護 Azure AD 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-359">Safeguard the Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-the-azure-ad-client-id-and-secret-from-the-azure-classic-portal"></a><span data-ttu-id="6d1ca-360">從 Azure 傳統入口網站設定 Azure AD 用戶端識別碼和密碼</span><span class="sxs-lookup"><span data-stu-id="6d1ca-360">Setting up the Azure AD client ID and secret from the Azure classic portal</span></span>
<span data-ttu-id="6d1ca-361">您也可以使用 [Azure 傳統入口網站]( https://manage.windowsazure.com)設定您的 Azure AD 用戶端識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-361">You can also set up your Azure AD client ID and secret by using the [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="6d1ca-362">若要執行這項工作，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-362">To perform this task, do the following:</span></span>

1. <span data-ttu-id="6d1ca-363">按一下 [Active Directory] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-363">Click the **Active Directory** tab.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="6d1ca-365">按一下 [新增應用程式]，並輸入應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-365">Click **Add Application**, and then type the application name.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="6d1ca-367">按一下箭號按鈕，然後設定應用程式的屬性。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-367">Click the arrow button, and then configure the application properties.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="6d1ca-369">按一下左下角的核取記號來完成。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-369">Click the check mark in the lower left corner to finish.</span></span> <span data-ttu-id="6d1ca-370">應用程式組態頁面隨即出現，而 Azure AD 用戶端識別碼會顯示在頁面底部。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-370">The application configuration page appears, and the Azure AD client ID is displayed at the bottom of the page.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="6d1ca-372">按一下 [儲存] 按鈕來儲存 Azure AD 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-372">Save the Azure AD client secret by clicking the **Save** button.</span></span> <span data-ttu-id="6d1ca-373">請注意在金鑰文字方塊中的 Azure AD 用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-373">Note the Azure AD client secret in the keys text box.</span></span> <span data-ttu-id="6d1ca-374">適當地保護該密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-374">Safeguard it appropriately.</span></span>

 ![Azure 磁碟加密](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="6d1ca-376">在 Azure 傳統入口網站上不支援上述流程。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-376">The preceding flow is not supported on the Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="6d1ca-377">使用現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="6d1ca-377">Use an existing application</span></span>
<span data-ttu-id="6d1ca-378">若要執行下列命令，請取得並使用 [Azure AD PowerShell 模組](https://technet.microsoft.com/library/jj151815.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-378">To execute the following commands, obtain and use the [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-379">下列命令必須從新的 PowerShell 視窗執行。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-379">The following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="6d1ca-380">請勿使用 Azure PowerShell 或 Azure Resource Manager 視窗來執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-380">Do not use Azure PowerShell or the Azure Resource Manager window to execute the commands.</span></span> <span data-ttu-id="6d1ca-381">我們建議使用此方法是因為這些 Cmdlet 在 MSOnline 模組或 Azure AD PowerShell 中。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-381">We recommend this approach because these cmdlets are in the MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="6d1ca-382">Azure AD 的憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="6d1ca-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="6d1ca-383">Linux VM 目前不支援 Azure AD 憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="6d1ca-384">以下各節會說明如何設定 Azure AD 的憑證式驗證。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-384">The sections that follow show how to configure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="6d1ca-385">建立 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d1ca-385">Create an Azure AD application</span></span>
<span data-ttu-id="6d1ca-386">若要建立 Azure AD 應用程式，請執行下列 PowerShell Cmdlet︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-386">To create an Azure AD application, execute the following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-387">使用您的安全密碼來取代下列 `yourpassword` 字串，並保護密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-387">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="6d1ca-388">完成此步驟之後，請將 PFX 檔案上傳至您的金鑰保存庫，並啟用將該憑證部署到 VM 所需的存取原則。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-388">After you finish this step, upload a PFX file to your key vault and enable the access policy needed to deploy that certificate to a VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="6d1ca-389">使用現有的 Azure AD 應用程式</span><span class="sxs-lookup"><span data-stu-id="6d1ca-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="6d1ca-390">如果您要為現有應用程式設定憑證式驗證，請使用此處所示的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-390">If you are configuring certificate-based authentication for an existing application, use the PowerShell cmdlets shown here.</span></span> <span data-ttu-id="6d1ca-391">務必從新的 PowerShell 視窗執行它們。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-391">Be sure to execute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="6d1ca-392">完成此步驟之後，請將 PFX 檔案上傳至您的金鑰保存庫，並啟用將憑證部署到 VM 所需的存取原則。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-392">After you finish this step, upload a PFX file to your key vault and enable the access policy that's needed to deploy the certificate to a VM.</span></span>

##### <a name="upload-a-pfx-file-to-your-key-vault"></a><span data-ttu-id="6d1ca-393">將 PFX 檔案上傳至金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6d1ca-393">Upload a PFX file to your key vault</span></span>
<span data-ttu-id="6d1ca-394">如需此程序的詳細說明，請參閱[官方 Azure Key Vault 團隊部落格](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-394">For a detailed explanation of this process, see [The Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="6d1ca-395">不過，對於這項工作您只需要下列 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-395">However, the following PowerShell cmdlets are all you need for the task.</span></span> <span data-ttu-id="6d1ca-396">務必從 Azure PowerShell 主控台執行它們。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-396">Be sure to execute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-397">使用您的安全密碼來取代下列 `yourpassword` 字串，並保護密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-397">Replace the following `yourpassword` string with your secure password, and safeguard the password.</span></span>

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

##### <a name="deploy-a-certificate-in-your-key-vault-to-an-existing-vm"></a><span data-ttu-id="6d1ca-398">將金鑰保存庫中的憑證部署至現有 VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-398">Deploy a certificate in your key vault to an existing VM</span></span>
<span data-ttu-id="6d1ca-399">PFX 上傳完成之後，使用下列作業將金鑰保存庫中的憑證部署至現有 VM︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-399">After you finish uploading the PFX, deploy a certificate in the key vault to an existing VM with the following:</span></span>
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

#### <a name="set-up-the-key-vault-access-policy-for-the-azure-ad-application"></a><span data-ttu-id="6d1ca-400">設定 Azure AD 應用程式的金鑰保存庫存取原則</span><span class="sxs-lookup"><span data-stu-id="6d1ca-400">Set up the key vault access policy for the Azure AD application</span></span>
<span data-ttu-id="6d1ca-401">您的 Azure AD 應用程式需要權限，才能存取保存庫中的金鑰或密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-401">Your Azure AD application needs rights to access the keys or secrets in the vault.</span></span> <span data-ttu-id="6d1ca-402">使用 [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) Cmdlet 可授與應用程式權限，使用用戶端識別碼 (登錄應用程式時所產生) 做為 _–ServicePrincipalName_ 參數值。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-402">Use the [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet to grant permissions to the application, using the client ID (which was generated when the application was registered) as the _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="6d1ca-403">若要深入了解，請參閱部落格文章 [Azure Key Vault - 逐步解說](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-403">To learn more, see the blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="6d1ca-404">以下是如何透過 PowerShell 執行這項工作的範例：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-404">Here is an example of how to perform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="6d1ca-405">若要使用 Azure 磁碟加密，您必須對 Azure AD 用戶端應用程式設定下列存取原則：_WrapKey_ 和 _Set_ 權限。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-405">Azure Disk Encryption requires you to configure the following access policies to your Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="6d1ca-406">術語</span><span class="sxs-lookup"><span data-stu-id="6d1ca-406">Terminology</span></span>
<span data-ttu-id="6d1ca-407">若要了解此技術所使用的一些常用術語，請使用以下術語表：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-407">To understand some of the common terms used by this technology, use the following terminology table:</span></span>

| <span data-ttu-id="6d1ca-408">術語</span><span class="sxs-lookup"><span data-stu-id="6d1ca-408">Terminology</span></span> | <span data-ttu-id="6d1ca-409">定義</span><span class="sxs-lookup"><span data-stu-id="6d1ca-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d1ca-410">Azure AD</span></span> | <span data-ttu-id="6d1ca-411">Azure AD 是 [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="6d1ca-412">Azure AD 帳戶是從金鑰保存庫驗證、儲存和擷取密碼的必要條件。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="6d1ca-413">Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6d1ca-413">Azure Key Vault</span></span> | <span data-ttu-id="6d1ca-414">Key Vault 是密碼編譯金鑰管理服務，它是基於美國聯邦資訊處理標準 (FIPS) 驗證的硬體安全性模組，可協助您保護密碼編譯金鑰和敏感性密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="6d1ca-415">如需詳細資訊，請參閱 [Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="6d1ca-416">ARM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-416">ARM</span></span> | <span data-ttu-id="6d1ca-417">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d1ca-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="6d1ca-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="6d1ca-418">BitLocker</span></span> |<span data-ttu-id="6d1ca-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) 是一種業界認可的 Windows 磁碟區加密技術，用來在 Windows IaaS VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used to enable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="6d1ca-420">BEK</span><span class="sxs-lookup"><span data-stu-id="6d1ca-420">BEK</span></span> | <span data-ttu-id="6d1ca-421">BitLocker 加密金鑰可用來加密作業系統開機磁碟區和資料磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-421">BitLocker encryption keys are used to encrypt the OS boot volume and data volumes.</span></span> <span data-ttu-id="6d1ca-422">BitLocker 金鑰會在金鑰保存庫中以密碼形式保護。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-422">The BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="6d1ca-423">CLI</span><span class="sxs-lookup"><span data-stu-id="6d1ca-423">CLI</span></span> | <span data-ttu-id="6d1ca-424">請參閱 [Azure 命令列介面](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="6d1ca-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="6d1ca-425">DM-Crypt</span></span> |<span data-ttu-id="6d1ca-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) 是基於 Linux 的透明磁碟加密子系統，用來在 Linux IaaS VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is the Linux-based, transparent disk-encryption subsystem that's used to enable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="6d1ca-427">KEK</span><span class="sxs-lookup"><span data-stu-id="6d1ca-427">KEK</span></span> | <span data-ttu-id="6d1ca-428">金鑰加密金鑰是非對稱金鑰 (RSA 2048)，可用來保護或包裝密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-428">Key encryption key is the asymmetric key (RSA 2048) that you can use to protect or wrap the secret.</span></span> <span data-ttu-id="6d1ca-429">您可以提供硬體安全性模組 (HSM) 保護的金鑰或軟體保護的金鑰。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="6d1ca-430">如需詳細資訊，請參閱 [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) 文件。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="6d1ca-431">PS Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6d1ca-431">PS cmdlets</span></span> | <span data-ttu-id="6d1ca-432">請參閱 [Azure PowerShell Cmdlet](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="6d1ca-433">針對 Azure 磁碟加密安裝及設定您的金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6d1ca-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="6d1ca-434">Azure 磁碟加密會協助您保護金鑰保存庫中的磁碟加密金鑰和密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-434">Azure Disk Encryption helps safeguard the disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="6d1ca-435">若要設定 Azure 磁碟加密的金鑰保存庫，請完成下列各節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-435">To set up your key vault for Azure Disk Encryption, complete the steps in each of the following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="6d1ca-436">建立金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6d1ca-436">Create a key vault</span></span>
<span data-ttu-id="6d1ca-437">若要建立金鑰保存庫，請使用下列選項之一︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-437">To create a key vault, use one of the following options:</span></span>

* [<span data-ttu-id="6d1ca-438">"101-Key-Vault-Create" Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6d1ca-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="6d1ca-439">Azure PowerShell 金鑰保存庫 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6d1ca-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="6d1ca-440">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d1ca-440">Azure Resource Manager</span></span>
* <span data-ttu-id="6d1ca-441">如何[保護您的金鑰保存庫](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-441">How to [Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-442">如果您已為訂用帳戶設定了金鑰保存庫，請跳至下一節。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-442">If you have already set up a key vault for your subscription, skip to the next section.</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="6d1ca-444">設定金鑰加密金鑰 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="6d1ca-445">如果您想針對 BitLocker 加密金鑰使用 KEK 增加額外的安全性，請將 KEK 新增至您的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-445">If you want to use a KEK for an additional layer of security for the BitLocker encryption keys, add a KEK to your key vault.</span></span> <span data-ttu-id="6d1ca-446">使用 [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) Cmdlet 在金鑰保存庫中建立金鑰加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-446">Use the [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to create a key encryption key in the key vault.</span></span> <span data-ttu-id="6d1ca-447">您也可以從內部部署金鑰管理 HSM 匯入 KEK。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="6d1ca-448">如需詳細資訊，請參閱 [Key Vault 文件](https://azure.microsoft.com/documentation/services/key-vault/)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="6d1ca-449">您可以移至 Azure Resource Manager 或使用金鑰保存庫介面來新增 KEK。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-449">You can add the KEK by going to Azure Resource Manager or by using your key vault interface.</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="6d1ca-451">設定金鑰保存庫的權限</span><span class="sxs-lookup"><span data-stu-id="6d1ca-451">Set key vault permissions</span></span>
<span data-ttu-id="6d1ca-452">Azure 平台需要存取您金鑰保存庫中的加密金鑰或密碼，讓該資訊可供 VM 用來開機和解密磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-452">The Azure platform needs access to the encryption keys or secrets in your key vault to make them available to the VM for booting and decrypting the volumes.</span></span> <span data-ttu-id="6d1ca-453">若要授與權限給 Azure 平台，使用金鑰保存庫的 PowerShell Cmdlet 設定金鑰保存庫中的 **EnabledForDiskEncryption** 屬性：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-453">To grant permissions to the Azure platform, set the **EnabledForDiskEncryption** property in the key vault by using the key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="6d1ca-454">您也可以造訪 [Azure 資源 Explorer](https://resources.azure.com) 來設定 **EnabledForDiskEncryption** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-454">You can also set the **EnabledForDiskEncryption** property by visiting the [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="6d1ca-455">如之前所提及，您必須在金鑰保存庫上設定 **EnabledForDiskEncryption** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-455">As mentioned earlier, you must set the **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="6d1ca-456">否則，部署作業將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-456">Otherwise, the deployment will fail.</span></span>

<span data-ttu-id="6d1ca-457">您可以從金鑰保存庫介面設定 Azure AD 應用程式的存取原則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-457">You can set up access policies for your Azure AD application from the key vault interface, as shown here:</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="6d1ca-460">在 [進階存取原則] 索引標籤中，請確定您已為 Azure 磁碟加密啟用金鑰保存庫︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-460">On the **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure 金鑰保存庫](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="6d1ca-462">磁碟加密部署案例和使用者體驗</span><span class="sxs-lookup"><span data-stu-id="6d1ca-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="6d1ca-463">您可以啟用許多磁碟加密案例，步驟可能會因案例而有所不同。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-463">You can enable many disk-encryption scenarios, and the steps may vary according to the scenario.</span></span> <span data-ttu-id="6d1ca-464">下列各節涵蓋更詳細的案例。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-464">The following sections cover the scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-the-marketplace"></a><span data-ttu-id="6d1ca-465">在透過 Marketplace 所建立的新 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-465">Enable encryption on new IaaS VMs that are created from the Marketplace</span></span>
<span data-ttu-id="6d1ca-466">您可以使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)，透過 Azure 中的 Marketplace 在新 IaaS Windows VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-466">You can enable disk encryption on new IaaS Windows VM from the Marketplace in Azure by using the  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="6d1ca-467">在 Azure 快速入門範本上按一下 [部署至 Azure]，在 [參數] 刀鋒視窗中輸入加密組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-467">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="6d1ca-468">選取訂用帳戶、資源群組、資源群組位置、法律條款與合約，然後按一下 [建立] 以在新 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-468">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-469">此範本會建立使用 Windows Server 2012 資源庫映像的新加密 Windows VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-469">This template creates a new encrypted Windows VM that uses the Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="6d1ca-470">您可以使用此 [Resource Manager 範本](https://aka.ms/fde-rhel)，在具有 200 GB RAID-0 陣列的新 IaaS RedHat Linux 7.2 VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="6d1ca-471">在您部署範本之後，請確認 VM 加密狀態，方法是使用[在執行中的 Linux VM 上加密 OS 磁碟機](#encrypting-os-drive-on-a-running-linux-vm)中所述的 `Get-AzureRmVmDiskEncryptionStatus` Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-471">After you deploy the template, verify the VM encryption status by using the `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="6d1ca-472">當電腦傳回 _VMRestartPending_ 的狀態，重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-472">When the machine returns a status of _VMRestartPending_, restart the VM.</span></span>

<span data-ttu-id="6d1ca-473">針對透過 Marketplace 案例使用 Azure AD 用戶端識別碼的新 VM，以下資料表列出其 Resource Manager 範本參數︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-473">The following table lists the Resource Manager template parameters for new VMs from the Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="6d1ca-474">參數</span><span class="sxs-lookup"><span data-stu-id="6d1ca-474">Parameter</span></span> | <span data-ttu-id="6d1ca-475">說明</span><span class="sxs-lookup"><span data-stu-id="6d1ca-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-476">adminUserName</span></span> | <span data-ttu-id="6d1ca-477">虛擬機器的系統管理使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-477">Admin user name for the virtual machine.</span></span> |
| <span data-ttu-id="6d1ca-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="6d1ca-478">adminPassword</span></span> | <span data-ttu-id="6d1ca-479">虛擬機器的系統管理使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-479">Admin user password for the virtual machine.</span></span> |
| <span data-ttu-id="6d1ca-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-480">newStorageAccountName</span></span> | <span data-ttu-id="6d1ca-481">要儲存作業系統和資料 VHD 的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-481">Name of the storage account to store OS and data VHDs.</span></span> |
| <span data-ttu-id="6d1ca-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="6d1ca-482">vmSize</span></span> | <span data-ttu-id="6d1ca-483">VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-483">Size of the VM.</span></span> <span data-ttu-id="6d1ca-484">目前僅支援標準的 A、D 和 G 系列。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="6d1ca-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-485">virtualNetworkName</span></span> | <span data-ttu-id="6d1ca-486">VM NIC 應該隸屬的 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-486">Name of the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="6d1ca-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-487">subnetName</span></span> | <span data-ttu-id="6d1ca-488">VM NIC 應該隸屬的 VNet 中子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-488">Name of the subnet in the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="6d1ca-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="6d1ca-489">AADClientID</span></span> | <span data-ttu-id="6d1ca-490">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-490">Client ID of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="6d1ca-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="6d1ca-491">AADClientSecret</span></span> | <span data-ttu-id="6d1ca-492">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-492">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="6d1ca-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-493">keyVaultURL</span></span> | <span data-ttu-id="6d1ca-494">應上傳 BitLocker 金鑰的金鑰保存庫 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-494">URL of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="6d1ca-495">您可以使用 Cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI` 來取得它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-495">You can get it by using the cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="6d1ca-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="6d1ca-497">用來加密所產生 BitLocker 金鑰的金鑰加密金鑰 URL (選擇性)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-497">URL of the key encryption key that's used to encrypt the generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="6d1ca-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6d1ca-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="6d1ca-499">金鑰保存庫的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-499">Resource group of the key vault.</span></span> |
| <span data-ttu-id="6d1ca-500">vmName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-500">vmName</span></span> | <span data-ttu-id="6d1ca-501">要執行加密作業所在 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-501">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d1ca-502">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="6d1ca-503">您可以使用自己的 KEK，在金鑰保存庫中進一步保護資料加密金鑰 (複雜密碼)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-503">You can bring your own KEK to further safeguard the data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="6d1ca-504">在透過客戶加密 VHD 和加密金鑰所建立的新 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="6d1ca-505">在這個案例中，您可以使用 Resource Manager 範本、PowerShell Cmdlet 或 CLI 命令啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-505">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="6d1ca-506">下列各節將更加詳細地說明 Resource Manager 範本和 CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-506">The following sections explain in greater detail the Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="6d1ca-507">遵循下列其中一節的指示來準備可用於 Azure 的預先加密映像。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-507">Follow the instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="6d1ca-508">映像建立之後，您可以使用下一節的步驟來建立加密的 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-508">After the image is created, you can use the steps in the next section to create an encrypted Azure VM.</span></span>

* [<span data-ttu-id="6d1ca-509">準備已預先加密的 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="6d1ca-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="6d1ca-510">準備已預先加密的 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="6d1ca-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="6d1ca-511">使用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6d1ca-511">Using the Resource Manager template</span></span>
<span data-ttu-id="6d1ca-512">您可以使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm)在加密的 VHD 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-512">You can enable disk encryption on your encrypted VHD by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="6d1ca-513">在 Azure 快速入門範本上按一下 [部署至 Azure]，在 [參數] 刀鋒視窗中輸入加密組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-513">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="6d1ca-514">選取訂用帳戶、資源群組、資源群組位置、法律條款與合約，然後按一下 [建立] 以在新 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-514">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the new IaaS VM.</span></span>

<span data-ttu-id="6d1ca-515">以下資料表列出加密 VHD 的 Resource Manager 範本參數︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-515">The following table lists the Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="6d1ca-516">參數</span><span class="sxs-lookup"><span data-stu-id="6d1ca-516">Parameter</span></span> | <span data-ttu-id="6d1ca-517">說明</span><span class="sxs-lookup"><span data-stu-id="6d1ca-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-518">newStorageAccountName</span></span> | <span data-ttu-id="6d1ca-519">要儲存加密的作業系統 VHD 的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-519">Name of the storage account to store the encrypted OS VHD.</span></span> <span data-ttu-id="6d1ca-520">此儲存體帳戶應該已建立在與 VM 相同的資源群組和相同的位置中。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-520">This storage account should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="6d1ca-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="6d1ca-521">osVhdUri</span></span> | <span data-ttu-id="6d1ca-522">來自儲存體帳戶作業系統 VHD 的 URI。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-522">URI of the OS VHD from the storage account.</span></span> |
| <span data-ttu-id="6d1ca-523">osType</span><span class="sxs-lookup"><span data-stu-id="6d1ca-523">osType</span></span> | <span data-ttu-id="6d1ca-524">作業系統產品類型 (Windows/Linux)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="6d1ca-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-525">virtualNetworkName</span></span> | <span data-ttu-id="6d1ca-526">VM NIC 應該隸屬的 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-526">Name of the VNet that the VM NIC should belong to.</span></span> <span data-ttu-id="6d1ca-527">名稱應該已建立在與 VM 相同的資源群組和相同的位置中。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-527">The name should already have been created in the same resource group and same location as the VM.</span></span> |
| <span data-ttu-id="6d1ca-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-528">subnetName</span></span> | <span data-ttu-id="6d1ca-529">VM NIC 應該隸屬的 VNet 上子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-529">Name of the subnet on the VNet that the VM NIC should belong to.</span></span> |
| <span data-ttu-id="6d1ca-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="6d1ca-530">vmSize</span></span> | <span data-ttu-id="6d1ca-531">VM 的大小。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-531">Size of the VM.</span></span> <span data-ttu-id="6d1ca-532">目前僅支援標準的 A、D 和 G 系列。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="6d1ca-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="6d1ca-533">keyVaultResourceID</span></span> | <span data-ttu-id="6d1ca-534">在 Azure Resource Manager 中識別金鑰保存庫資源的 ResourceID。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-534">The ResourceID that identifies the key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="6d1ca-535">您可以使用 PowerShell Cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId` 來取得它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-535">You can get it by using the PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="6d1ca-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="6d1ca-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="6d1ca-537">在金鑰保存庫中所設定的磁碟加密金鑰的 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-537">URL of the disk-encryption key that's set up in the key vault.</span></span> |
| <span data-ttu-id="6d1ca-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="6d1ca-538">keyVaultKekUrl</span></span> | <span data-ttu-id="6d1ca-539">用來加密所產生磁碟加密金鑰的金鑰加密金鑰的 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-539">URL of the key encryption key for encrypting the generated disk-encryption key.</span></span> |
| <span data-ttu-id="6d1ca-540">vmName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-540">vmName</span></span> | <span data-ttu-id="6d1ca-541">IaaS VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-541">Name of the IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="6d1ca-542">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6d1ca-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="6d1ca-543">您可以使用 PowerShell Cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk) 在加密的 VHD 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-543">You can enable disk encryption on your encrypted VHD by using the PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="6d1ca-544">使用 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="6d1ca-544">Using CLI commands</span></span>
<span data-ttu-id="6d1ca-545">若要使用 CLI 命令啟用此案例的磁碟加密，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-545">To enable disk encryption for this scenario by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="6d1ca-546">設定金鑰保存庫的存取原則：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="6d1ca-547">設定 **EnabledForDiskEncryption** 旗標︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-547">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="6d1ca-548">設定權限給 Azure AD 應用程式，以將密碼寫入至您的金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-548">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="6d1ca-549">若要在現有或執行中的 VM 上啟用加密，請輸入︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-549">To enable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="6d1ca-550">取得加密狀態：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="6d1ca-551">若要從您加密的 VHD 啟用新 VM 上的加密，請使用以下參數搭配 `azure vm create` 命令：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-551">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="6d1ca-552">在 Azure 中現有或執行中的 IaaS Windows VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="6d1ca-553">在這個案例中，您可以使用 Resource Manager 範本、PowerShell Cmdlet 或 CLI 命令啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-553">In this scenario, you can enable encrypting by using the Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="6d1ca-554">下列各節將更加詳細地說明如何使用 Resource Manager 範本和 CLI 命令來啟用它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-554">The following sections explain in greater detail how to enable it by using the Resource Manager template and CLI commands.</span></span>

#### <a name="using-the-resource-manager-template"></a><span data-ttu-id="6d1ca-555">使用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6d1ca-555">Using the Resource Manager template</span></span>
<span data-ttu-id="6d1ca-556">您可以使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm)，在 Azure 中現有或執行中的 IaaS Windows VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="6d1ca-557">在 Azure 快速入門範本上按一下 [部署至 Azure]，在 [參數] 刀鋒視窗中輸入加密組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-557">On the Azure quick-start template, click **Deploy to Azure**, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="6d1ca-558">選取訂用帳戶、資源群組、資源群組位置、法律條款與合約，然後按一下 [建立] 以在現有或執行中的 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-558">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="6d1ca-559">針對使用 Azure AD 用戶端識別碼的現有或執行中 VM，以下資料表列出其 Resource Manager 範本參數︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-559">The following table lists the Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="6d1ca-560">參數</span><span class="sxs-lookup"><span data-stu-id="6d1ca-560">Parameter</span></span> | <span data-ttu-id="6d1ca-561">說明</span><span class="sxs-lookup"><span data-stu-id="6d1ca-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="6d1ca-562">AADClientID</span></span> | <span data-ttu-id="6d1ca-563">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-563">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="6d1ca-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="6d1ca-564">AADClientSecret</span></span> | <span data-ttu-id="6d1ca-565">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-565">Client secret of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="6d1ca-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-566">keyVaultName</span></span> | <span data-ttu-id="6d1ca-567">應上傳 BitLocker 金鑰的金鑰保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-567">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="6d1ca-568">您可以使用 Cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname` 來取得它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-568">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="6d1ca-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="6d1ca-570">用來加密所產生 BitLocker 金鑰的金鑰加密金鑰 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-570">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="6d1ca-571">如果您在 UseExistingKek 下拉式清單中選取 [nokek]，此參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-571">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="6d1ca-572">如果您在 UseExistingKek 下拉式清單中選取 [kek]，您必須輸入 _keyEncryptionKeyURL_ 值。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-572">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="6d1ca-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="6d1ca-573">volumeType</span></span> | <span data-ttu-id="6d1ca-574">執行加密作業所在磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-574">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="6d1ca-575">有效值為 _OS_、_Data_ 和 _All_。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="6d1ca-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="6d1ca-576">sequenceVersion</span></span> | <span data-ttu-id="6d1ca-577">BitLocker 作業的順序版本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-577">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="6d1ca-578">每當在相同的 VM 上執行磁碟加密作業時便遞增此版本號碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-578">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="6d1ca-579">vmName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-579">vmName</span></span> | <span data-ttu-id="6d1ca-580">要執行加密作業所在 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-580">Name of the VM that the encryption operation is to be performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d1ca-581">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="6d1ca-582">您可以使用自己的 KEK，在金鑰保存庫中進一步保護資料加密金鑰 (BitLocker 加密密碼)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-582">You can bring your own KEK to further safeguard the data encryption key (BitLocker encryption secret) in the key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="6d1ca-583">使用 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6d1ca-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="6d1ca-584">如需使用 PowerShell Cmdlet 以 Azure 磁碟加密來啟用加密的相關資訊，請參閱部落格文章[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="6d1ca-585">使用 CLI 命令</span><span class="sxs-lookup"><span data-stu-id="6d1ca-585">Using CLI commands</span></span>
<span data-ttu-id="6d1ca-586">若要在 Azure 中使用 CLI 命令來啟用現有或執行中 IaaS Windows VM 上的加密，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-586">To enable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do the following:</span></span>

1. <span data-ttu-id="6d1ca-587">若要設定金鑰保存庫的存取原則：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-587">To set access policies in the key vault:</span></span>
   * <span data-ttu-id="6d1ca-588">設定 **EnabledForDiskEncryption** 旗標︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-588">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="6d1ca-589">設定權限給 Azure AD 應用程式，以將密碼寫入至您的金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-589">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="6d1ca-590">若要在現有或執行中的 VM 上啟用加密︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-590">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="6d1ca-591">若要取得加密狀態：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-591">To get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="6d1ca-592">若要從您加密的 VHD 啟用新 VM 上的加密，請使用以下參數搭配 `azure vm create` 命令：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-592">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="6d1ca-593">在 Azure 中現有或執行中的 IaaS Linux VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="6d1ca-594">您可以使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm)，在 Azure 中現有或執行中的 IaaS Linux VM 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="6d1ca-595">在 Azure 快速入門範本上按一下 [部署至 Azure]，在 [參數] 刀鋒視窗中輸入加密組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-595">Click **Deploy to Azure** on the Azure quick-start template, enter the encryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="6d1ca-596">選取訂用帳戶、資源群組、資源群組位置、法律條款與合約，然後按一下 [建立] 以在現有或執行中的 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-596">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on the existing or running IaaS VM.</span></span>

<span data-ttu-id="6d1ca-597">針對使用 Azure AD 用戶端識別碼的現有或執行中 VM，以下資料表列出其 Resource Manager 範本參數︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-597">The following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="6d1ca-598">參數</span><span class="sxs-lookup"><span data-stu-id="6d1ca-598">Parameter</span></span> | <span data-ttu-id="6d1ca-599">說明</span><span class="sxs-lookup"><span data-stu-id="6d1ca-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="6d1ca-600">AADClientID</span></span> | <span data-ttu-id="6d1ca-601">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-601">Client ID of the Azure AD application that has permissions to write secrets to the key vault.</span></span> |
| <span data-ttu-id="6d1ca-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="6d1ca-602">AADClientSecret</span></span> | <span data-ttu-id="6d1ca-603">具有權限可將密碼寫入金鑰保存庫之 Azure AD 應用程式的用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-603">Client secret of the Azure AD application that has permissions to write secrets to your key vault.</span></span> |
| <span data-ttu-id="6d1ca-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-604">keyVaultName</span></span> | <span data-ttu-id="6d1ca-605">應上傳 BitLocker 金鑰的金鑰保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-605">Name of the key vault that the BitLocker key should be uploaded to.</span></span> <span data-ttu-id="6d1ca-606">您可以使用 Cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname` 來取得它。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-606">You can get it by using the cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="6d1ca-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="6d1ca-608">用來加密所產生 BitLocker 金鑰的金鑰加密金鑰 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-608">URL of the key encryption key that's used to encrypt the generated BitLocker key.</span></span> <span data-ttu-id="6d1ca-609">如果您在 UseExistingKek 下拉式清單中選取 [nokek]，此參數是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-609">This parameter is optional if you select **nokek** in the UseExistingKek drop-down list.</span></span> <span data-ttu-id="6d1ca-610">如果您在 UseExistingKek 下拉式清單中選取 [kek]，您必須輸入 _keyEncryptionKeyURL_ 值。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-610">If you select **kek** in the UseExistingKek drop-down list, you must enter the _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="6d1ca-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="6d1ca-611">volumeType</span></span> | <span data-ttu-id="6d1ca-612">執行加密作業所在磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-612">Type of volume that the encryption operation is performed on.</span></span> <span data-ttu-id="6d1ca-613">支援的有效值為 _OS_ 或 _All_ (適用於 RHEL 7.2、CentOS 7.2 和 Ubuntu 16.04)，和 _Data_ (適用於所有其他的散發套件)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="6d1ca-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="6d1ca-614">sequenceVersion</span></span> | <span data-ttu-id="6d1ca-615">BitLocker 作業的順序版本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-615">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="6d1ca-616">每當在相同的 VM 上執行磁碟加密作業時便遞增此版本號碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-616">Increment this version number every time a disk-encryption operation is performed on the same VM.</span></span> |
| <span data-ttu-id="6d1ca-617">vmName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-617">vmName</span></span> | <span data-ttu-id="6d1ca-618">要執行加密作業所在 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-618">Name of the VM that the encryption operation is to be performed on.</span></span> |
| <span data-ttu-id="6d1ca-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="6d1ca-619">passPhrase</span></span> | <span data-ttu-id="6d1ca-620">輸入強式複雜密碼做為資料加密金鑰。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-620">Type a strong passphrase as the data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="6d1ca-621">_KeyEncryptionKeyURL_ 是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="6d1ca-622">您可以使用自己的 KEK，在金鑰保存庫中進一步保護資料加密金鑰 (複雜密碼)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-622">You can bring your own KEK to further safeguard the data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="6d1ca-623">CLI 命令</span><span class="sxs-lookup"><span data-stu-id="6d1ca-623">CLI commands</span></span>
<span data-ttu-id="6d1ca-624">您可以安裝並使用 [CLI 命令](../cli-install-nodejs.md)在加密的 VHD 上啟用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-624">You can enable disk encryption on your encrypted VHD by installing and using the [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="6d1ca-625">若要在 Azure 中使用 CLI 命令來啟用現有或執行中 IaaS Linux VM 上的加密，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-625">To enable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do the following:</span></span>

1. <span data-ttu-id="6d1ca-626">設定金鑰保存庫的存取原則：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-626">Set access policies in the key vault:</span></span>

 * <span data-ttu-id="6d1ca-627">設定 **EnabledForDiskEncryption** 旗標︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-627">Set the **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="6d1ca-628">設定權限給 Azure AD 應用程式，以將密碼寫入至您的金鑰保存庫：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-628">Set permissions to Azure AD application to write secrets to your key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="6d1ca-629">若要在現有或執行中的 VM 上啟用加密︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-629">To enable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="6d1ca-630">取得加密狀態：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="6d1ca-631">若要從您加密的 VHD 啟用新 VM 上的加密，請使用以下參數搭配 `azure vm create` 命令：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-631">To enable encryption on a new VM from your encrypted VHD, use the following parameters with the `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-the-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="6d1ca-632">取得已加密 IaaS VM 的加密狀態</span><span class="sxs-lookup"><span data-stu-id="6d1ca-632">Get the encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="6d1ca-633">您可以使用 Azure Resource Manager、[PowerShell Cmdlet](/powershell/azure/overview) 或 CLI 命令取得加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-633">You can get the encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="6d1ca-634">下列章節將說明如何使用 Azure 傳統入口網站和 CLI 命令來取得加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-634">The following sections explain how to use the Azure classic portal and CLI commands to get the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="6d1ca-635">使用 Azure Resource Manager 取得已加密 Windows VM 的加密狀態</span><span class="sxs-lookup"><span data-stu-id="6d1ca-635">Get the encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="6d1ca-636">您可以從 Azure Resource Manager 取得 IaaS VM 的加密狀態，請執行以下步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-636">You can get the encryption status of the IaaS VM from Azure Resource Manager by doing the following:</span></span>

1. <span data-ttu-id="6d1ca-637">登入 [Azure 傳統入口網站](https://portal.azure.com/)，然後按一下左窗格中的 [虛擬機器] 以查看您訂用帳戶中虛擬機器的摘要檢視。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-637">Sign in to the [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in the left pane to see a summary view of the virtual machines in your subscription.</span></span> <span data-ttu-id="6d1ca-638">您可以從 [訂用帳戶] 下拉式清單中選取訂用帳戶名稱，以篩選虛擬機器檢視。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-638">You can filter the virtual machines view by selecting the subscription name in the **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="6d1ca-639">在 [虛擬機器] 頁面頂端，按一下 [資料行]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-639">At the top of the **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="6d1ca-640">從 [選擇資料行] 刀鋒視窗選取 [磁碟加密]，並按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-640">On the **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="6d1ca-641">您應該會看到磁碟加密資料行顯示出每個 VM 的加密狀態為_已啟用_或_未啟用_，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-641">You should see the disk-encryption column showing the encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in the following figure:</span></span>

 ![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-the-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-the-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="6d1ca-643">使用磁碟加密 PowerShell Cmdlet 取得已加密 (Windows/Linux) IaaS VM 的加密狀態</span><span class="sxs-lookup"><span data-stu-id="6d1ca-643">Get the encryption status of an encrypted (Windows/Linux) IaaS VM by using the disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="6d1ca-644">您可以透過磁碟加密 PowerShell Cmdlet `Get-AzureRmVMDiskEncryptionStatus` 來取得 IaaS VM 的加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-644">You can get the encryption status of the IaaS VM from the disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="6d1ca-645">若要取得 VM 的加密設定，請輸入以下資訊︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-645">To get the encryption settings for your VM, enter the following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="6d1ca-646">您可以檢查 _Get-AzureRmVMDiskEncryptionStatus_ 的輸出來取得加密金鑰 URL。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-646">You can inspect the output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

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

<span data-ttu-id="6d1ca-647">OSVolumeEncrypted 和 DataVolumesEncrypted 的設定值設定為 _Encrypted_，顯示這兩個磁碟區都是使用 Azure 磁碟加密來加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-647">The OSVolumeEncrypted and DataVolumesEncrypted settings values are set to _Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="6d1ca-648">如需使用 PowerShell Cmdlet 以 Azure 磁碟加密來啟用加密的相關資訊，請參閱部落格文章[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 1 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx)和[探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see the blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-649">在 Linux VM 上，`Get-AzureRmVMDiskEncryptionStatus` Cmdlet 報告加密狀態需要三至四分鐘。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-649">On Linux VMs, it takes three to four minutes for the `Get-AzureRmVMDiskEncryptionStatus` cmdlet to report the encryption status.</span></span>

#### <a name="get-the-encryption-status-of-the-iaas-vm-from-the-disk-encryption-cli-command"></a><span data-ttu-id="6d1ca-650">透過磁碟加密 CLI 命令取得 IaaS VM 的加密狀態</span><span class="sxs-lookup"><span data-stu-id="6d1ca-650">Get the encryption status of the IaaS VM from the disk-encryption CLI command</span></span>
<span data-ttu-id="6d1ca-651">您可以使用磁碟加密 CLI 命令 `azure vm show-disk-encryption-status` 取得 IaaS VM 的加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-651">You can get the encryption status of the IaaS VM by using the disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="6d1ca-652">若要取得 VM 的加密設定，請進入您的 Azure CLI 工作階段：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-652">To get the encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="6d1ca-653">在執行中 Windows IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="6d1ca-654">您可以透過 Azure 磁碟加密 Resource Manager 範本或 PowerShell Cmdlet，在執行中 Windows 或 Linux IaaS VM 上停用加密，並指定解密組態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-654">You can disable encryption on a running Windows or Linux IaaS VM via the Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify the decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="6d1ca-655">Windows VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-655">Windows VM</span></span>
<span data-ttu-id="6d1ca-656">停用加密步驟會在執行中 Windows IaaS VM 上停用 OS、資料磁碟區或兩者的加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-656">The disable-encryption step disables encryption of the OS, the data volume, or both on the running Windows IaaS VM.</span></span> <span data-ttu-id="6d1ca-657">您無法停用 OS 磁碟區並將資料磁碟區保持加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-657">You cannot disable the OS volume and leave the data volume encrypted.</span></span> <span data-ttu-id="6d1ca-658">執行停用加密步驟時，Azure 傳統部署模型會更新 VM 服務模型，且 Windows IaaS VM 會標示為已解密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-658">When the disable-encryption step is performed, the Azure classic deployment model updates the VM service model, and the Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="6d1ca-659">VM 的待用內容不會再加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-659">The contents of the VM are no longer encrypted at rest.</span></span> <span data-ttu-id="6d1ca-660">解密並不會刪除您的金鑰保存庫和加密金鑰資料 (Windows 系統的 BitLocker 加密金鑰或 Linux 的複雜密碼)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-660">The decryption does not delete your key vault and the encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="6d1ca-661">Linux VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-661">Linux VM</span></span>
<span data-ttu-id="6d1ca-662">停用加密步驟會在執行中 Linux IaaS VM 上停用資料磁碟區的加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-662">The disable-encryption step disables encryption of the data volume on the running Linux IaaS VM.</span></span> <span data-ttu-id="6d1ca-663">此步驟僅適用於 OS 磁碟機未加密的情況。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-663">This step only works if the OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-664">Linux VM 不允許在 OS 磁碟上停用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-664">Disabling encryption on the OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="6d1ca-665">在現有或執行中 IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="6d1ca-666">您可以使用 [Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm)，在執行中 Windows IaaS VM 上停用磁碟加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-666">You can disable disk encryption on running Windows IaaS VMs by using the [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="6d1ca-667">在 Azure 快速入門範本上按一下 [部署至 Azure]，在 [參數] 刀鋒視窗中輸入解密組態，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-667">On the Azure quick-start template, click **Deploy to Azure**, enter the decryption configuration on the **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="6d1ca-668">選取訂用帳戶、資源群組、資源群組位置、法律條款與合約，然後按一下 [建立] 以在新 IaaS VM 上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-668">Select the subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** to enable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="6d1ca-669">對於 Linux VM，您可以使用[在執行中的 Linux VM 上停用加密](https://aka.ms/decrypt-linuxvm)範本來停用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-669">For Linux VMs, you can disable encryption by using the [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="6d1ca-670">以下資料表列出可供在執行中 IaaS VM 上停用加密的 Resource Manager 範本參數︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-670">The following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="6d1ca-671">參數</span><span class="sxs-lookup"><span data-stu-id="6d1ca-671">Parameter</span></span> | <span data-ttu-id="6d1ca-672">說明</span><span class="sxs-lookup"><span data-stu-id="6d1ca-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6d1ca-673">vmName</span><span class="sxs-lookup"><span data-stu-id="6d1ca-673">vmName</span></span> | <span data-ttu-id="6d1ca-674">要執行加密作業所在 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-674">Name of the VM that the encryption operation is to be performed on.</span></span>
| <span data-ttu-id="6d1ca-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="6d1ca-675">volumeType</span></span> | <span data-ttu-id="6d1ca-676">執行解密作業所在磁碟區的類型。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="6d1ca-677">有效值為 _OS_、_Data_ 和 _All_。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="6d1ca-678">若未在 _Data_ 磁碟區上停用加密，則無法在執行中 Windows IaaS VM OS/開機磁碟區上停用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on the _Data_ volume.</span></span> <span data-ttu-id="6d1ca-679">也請注意 Linux VM 不允許在 OS 磁碟上停用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-679">Also note that disabling encryption on the OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="6d1ca-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="6d1ca-680">sequenceVersion</span></span> | <span data-ttu-id="6d1ca-681">BitLocker 作業的順序版本。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-681">Sequence version of the BitLocker operation.</span></span> <span data-ttu-id="6d1ca-682">每當在相同的 VM 上執行磁碟解密作業時便遞增此版本號碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-682">Increment this version number every time a disk decryption operation is performed on the same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="6d1ca-683">在現有或執行中 IaaS VM 上停用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="6d1ca-684">若要使用 PowerShell Cmdlet 在現有或執行中 IaaS VM 上停用加密，請參閱 [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-684">To disable encryption on an existing or running IaaS VM by using the PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="6d1ca-685">此 Cmdlet 同時支援 Windows 和 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="6d1ca-686">若要停用加密，它會在虛擬機器上安裝擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-686">To disable encryption, it installs an extension on the virtual machine.</span></span> <span data-ttu-id="6d1ca-687">如果未指定 _Name_ 參數，則會建立使用預設名稱 _AzureDiskEncryption for Windows VMs_ 的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-687">If the _Name_ parameter is not specified, an extension with the default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="6d1ca-688">在 Linux VM 上會使用 AzureDiskEncryptionForLinux 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-688">On Linux VMs, the AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="6d1ca-689">此 Cmdlet 會重新啟動虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-689">This cmdlet reboots the virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="6d1ca-690">在具有 Azure 受管理磁碟且預先加密的 IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="6d1ca-691">使用 Azure 受管理磁碟 ARM 範本，以使用位於以下位置的 ARM 範本從預先加密的 VHD 建立加密的 VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-691">Use the Azure Managed Disk ARM template to create a encrypted VM from a pre-encrypted VHD using the ARM template located at</span></span>   
<span data-ttu-id="6d1ca-692">[從預先加密的 VHD/儲存體 blob 建立新的已加密受管理磁碟] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="6d1ca-693">在具有 Azure 受管理磁碟的新 Linux IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="6d1ca-694">使用 Azure 受管理磁碟 ARM 範本，以使用位於以下位置的 ARM 範本建立新的已加密 Linux IaaS VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-694">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
<span data-ttu-id="6d1ca-695">[使用完整磁碟加密部署 RHEL 7.2] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="6d1ca-696">在具有 Azure 受管理磁碟的新 Windows IaaS VM 上啟用加密</span><span class="sxs-lookup"><span data-stu-id="6d1ca-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="6d1ca-697">使用 Azure 受管理磁碟 ARM 範本，以使用位於以下位置的 ARM 範本建立新的已加密 Linux IaaS VM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-697">Use the Azure Managed Disk ARM template to create a new encrypted Linux IaaS VM using the ARM template located at</span></span>   
 <span data-ttu-id="6d1ca-698">[從資源庫映像建立新的已加密 Windows IaaS 受管理磁碟 VM] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="6d1ca-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="6d1ca-699">您必須在啟用 Azure 磁碟加密之前，先在 Azure 磁碟加密之外對以受控磁碟為基礎的 VM 執行個體建立快照集和/或備份。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-699">It is mandatory to snapshot and/or backup a managed disk based VM instance outside of and prior to enabling Azure Disk Encryption.</span></span>  <span data-ttu-id="6d1ca-700">您可以從入口網站建立受控磁碟的快照集，也可以使用 Azure 備份來建立。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-700">A snapshot of the managed disk can be taken from the portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="6d1ca-701">擁有備份可確保在加密期間發生任何非預期的失敗時，能有復原選項可供選擇。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-701">Backups ensure that a recovery option is possible in the case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="6d1ca-702">在建立備份後，您就可以使用 Set-AzureRmVMDiskEncryptionExtension Cmdlet 並指定 -skipVmBackup 參數來加密受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-702">Once a backup is made, the Set-AzureRmVMDiskEncryptionExtension cmdlet can be used to encrypt managed disks by specifying the -skipVmBackup parameter.</span></span>  <span data-ttu-id="6d1ca-703">在建立好備份並指定了這個參數之前，對以受控磁碟為基礎的 VM 執行這個命令都將會失敗。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="6d1ca-704">現有已加密非高階 VM 的更新加密設定</span><span class="sxs-lookup"><span data-stu-id="6d1ca-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="6d1ca-705">針對執行中的 VM 使用現有 Azure 磁碟加密支援的介面 [PS Cmdlet、CLI 或 ARM 範本] 更新加密設定，如 AAD 用戶端識別碼/密碼、金鑰加密金鑰 [KEK]、Windows VM 適用的 BitLocker 加密金鑰，或 Linux VM 適用的複雜密碼等。僅支援非高階儲存體所支援 VM 的更新加密設定。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-705">Use the existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] to update the encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. The update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="6d1ca-706">不支援高階儲存體所支援 VM 的。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="6d1ca-707">附錄</span><span class="sxs-lookup"><span data-stu-id="6d1ca-707">Appendix</span></span>
### <a name="connect-to-your-subscription"></a><span data-ttu-id="6d1ca-708">連線至您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6d1ca-708">Connect to your subscription</span></span>
<span data-ttu-id="6d1ca-709">在繼續之前，請先參閱本文中＜必要條件＞一節。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-709">Before you proceed, review the *Prerequisites* section in this article.</span></span> <span data-ttu-id="6d1ca-710">確定已符合所有必要條件之後，請透過下列方式連接至您的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-710">After you ensure that all prerequisites have been met, connect to your subscription by doing the following:</span></span>

1. <span data-ttu-id="6d1ca-711">開始 Azure PowerShell 工作階段，並使用下列命令登入您的 Azure 帳戶：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-711">Start an Azure PowerShell session, and sign in to your Azure account with the following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="6d1ca-712">如果您有多個訂用帳戶，並想要指定要使用的其中一個，請輸入下列內容以查看您帳戶的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-712">If you have multiple subscriptions and want to specify one to use, type the following to see the subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="6d1ca-713">若要指定要使用的訂用帳戶，請輸入：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-713">To specify the subscription you want to use, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="6d1ca-714">若要確認訂用帳戶設定正確無誤，請輸入：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-714">To verify that the subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="6d1ca-715">若要確認已安裝 Azure 磁碟加密 Cmdlet，請輸入：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-715">To confirm the Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="6d1ca-716">下列的輸出可以確認 Azure 磁碟加密 PowerShell 的安裝：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-716">The following output confirms the Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="6d1ca-717">準備已預先加密的 Windows VHD</span><span class="sxs-lookup"><span data-stu-id="6d1ca-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="6d1ca-718">下列各節是準備預先加密的 Windows VHD 以在 Azure IaaS 中部署為加密的 VHD 的必要項目。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-718">The sections that follow are necessary to prepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="6d1ca-719">使用該資訊以在 Azure Site Recovery 或 Azure 上準備並啟動全新的 Windows VM (VHD)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-719">Use the information to prepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-to-allow-non-tpm-for-os-protection"></a><span data-ttu-id="6d1ca-720">更新群組原則以對作業系統保護允許非 TPM</span><span class="sxs-lookup"><span data-stu-id="6d1ca-720">Update group policy to allow non-TPM for OS protection</span></span>
<span data-ttu-id="6d1ca-721">設定 **BitLocker 磁碟機加密**的 BitLocker 群組原則設定，其位於此路徑**本機電腦原則** > **電腦設定** > **系統管理範本** > **Windows 元件**。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-721">Configure the BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="6d1ca-722">將這個設定變更為**作業系統磁碟機** > **啟動時需要其他驗證** > **在不含相容 TPM 的情形下允許使用 BitLocker**，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-722">Change this setting to **Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in the following figure:</span></span>

![Azure 中的 Microsoft Antimalware](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="6d1ca-724">安裝 BitLocker 功能元件</span><span class="sxs-lookup"><span data-stu-id="6d1ca-724">Install BitLocker feature components</span></span>
<span data-ttu-id="6d1ca-725">針對 Windows Server 2012 和更新版本，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-725">For Windows Server 2012 and later, use the following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="6d1ca-726">針對 Windows Server 2008 R2，請使用下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-726">For Windows Server 2008 R2, use the following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-the-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="6d1ca-727">使用 `bdehdcfg` 準備用於 BitLocker 的 OS 磁碟區</span><span class="sxs-lookup"><span data-stu-id="6d1ca-727">Prepare the OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="6d1ca-728">若要壓縮作業系統磁碟分割並為 BitLocker 準備電腦，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-728">To compress the OS partition and prepare the machine for BitLocker, execute the following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-the-os-volume-by-using-bitlocker"></a><span data-ttu-id="6d1ca-729">使用 BitLocker 保護作業系統磁碟區</span><span class="sxs-lookup"><span data-stu-id="6d1ca-729">Protect the OS volume by using BitLocker</span></span>
<span data-ttu-id="6d1ca-730">使用 [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) 命令，以使用外部的金鑰保護裝置在開機磁碟區上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-730">Use the [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command to enable encryption on the boot volume using an external key protector.</span></span> <span data-ttu-id="6d1ca-731">也將外部金鑰 (.bek 檔案) 放置於外部磁碟機或磁碟區。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-731">Also place the external key (.bek file) on the external drive or volume.</span></span> <span data-ttu-id="6d1ca-732">下次重新開機後，會在系統/開機磁碟區上啟用加密。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-732">Encryption is enabled on the system/boot volume after the next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="6d1ca-733">使用不同的資料/資源 VHD 來準備 VM，才能使用 BitLocker 取得外部金鑰。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-733">Prepare the VM with a separate data/resource VHD for getting the external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="6d1ca-734">在執行中的 Linux VM 上加密 OS 磁碟機</span><span class="sxs-lookup"><span data-stu-id="6d1ca-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="6d1ca-735">下列散發套件支援在執行中的 Linux VM 上加密 OS 磁碟機︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-735">Encryption of an OS drive on a running Linux VM is supported on the following distributions:</span></span>

* <span data-ttu-id="6d1ca-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="6d1ca-736">RHEL 7.2</span></span>
* <span data-ttu-id="6d1ca-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="6d1ca-737">CentOS 7.2</span></span>
* <span data-ttu-id="6d1ca-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6d1ca-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="6d1ca-739">OS 磁碟加密的必要條件</span><span class="sxs-lookup"><span data-stu-id="6d1ca-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="6d1ca-740">必須從 Azure Resource Manager 的Marketplace 映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-740">The VM must be created from the Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="6d1ca-741">具有至少 4 GB RAM 的 Azure VM (建議大小為 7 GB)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="6d1ca-742">(適用於 RHEL 和 CentOS) 停用 SELinux。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="6d1ca-743">若要停用 SELinux，請參閱「4.4.2.</span><span class="sxs-lookup"><span data-stu-id="6d1ca-743">To disable SELinux, see "4.4.2.</span></span> <span data-ttu-id="6d1ca-744">停用 SELinux」，其位於 VM 上的 [SELinux 使用者和系統管理員指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-744">Disabling SELinux" in the [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on the VM.</span></span>
* <span data-ttu-id="6d1ca-745">停用 SELinux 之後，至少重新啟動 VM 一次。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-745">After you disable SELinux, reboot the VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="6d1ca-746">步驟</span><span class="sxs-lookup"><span data-stu-id="6d1ca-746">Steps</span></span>
1. <span data-ttu-id="6d1ca-747">使用先前指定的其中一個散發套件來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-747">Create a VM by using one of the distributions specified previously.</span></span>

 <span data-ttu-id="6d1ca-748">若為 CentOS 7.2，支援透過特殊映像加密 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="6d1ca-749">若要使用此映像，請在建立 VM 時指定 "7.2n" 做為 SKU︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-749">To use this image, specify "7.2n" as the SKU when you create the VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="6d1ca-750">根據您的需求設定 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-750">Configure the VM according to your needs.</span></span> <span data-ttu-id="6d1ca-751">如果您要加密所有 (OS + 資料) 磁碟機，必須可從 /etc/fstab 指定和掛接資料磁碟機。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-751">If you are going to encrypt all the (OS + data) drives, the data drives need to be specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="6d1ca-752">使用 UUID=... 來指定 /etc/fstab 中的資料磁碟機，而不是指定區塊裝置名稱 (例如 /dev/sdb1)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-752">Use UUID=... to specify data drives in /etc/fstab instead of specifying the block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="6d1ca-753">加密期間，VM 上的磁碟機順序會變更。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-753">During encryption, the order of drives changes on the VM.</span></span> <span data-ttu-id="6d1ca-754">如果 VM 依賴特定的區塊裝置順序，則無法在加密後掛接裝置。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-754">If your VM relies on a specific order of block devices, it will fail to mount them after encryption.</span></span>

3. <span data-ttu-id="6d1ca-755">登出 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-755">Sign out of the SSH sessions.</span></span>

4. <span data-ttu-id="6d1ca-756">若要加密 OS，請在[啟用加密](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure)時將 volumeType 指定為 **All** 或 **OS**。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-756">To encrypt the OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="6d1ca-757">未以 `systemd` 服務的形式執行的所有使用者空間程序皆應使用 `SIGKILL` 來終止。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="6d1ca-758">重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-758">Reboot the VM.</span></span> <span data-ttu-id="6d1ca-759">當您在執行中的 VM 上啟用 OS 磁碟加密時，請規劃 VM 停機時間。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="6d1ca-760">使用[下一節](#monitoring-os-encryption-progress)的指示定期監視加密進度。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-760">Periodically monitor the progress of encryption by using the instructions in the [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="6d1ca-761">在 Get-AzureRmVmDiskEncryptionStatus 顯示「VMRestartPending」之後，請登入 VM 或使用入口網站、PowerShell 或 CLI 來重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in to it or by using the portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot the VM
    ```
<span data-ttu-id="6d1ca-762">重新開機之前，我們建議您儲存 VM 的[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of the VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="6d1ca-763">監視 OS 加密進度</span><span class="sxs-lookup"><span data-stu-id="6d1ca-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="6d1ca-764">有三種方式可監視 OS 加密進度：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="6d1ca-765">使用 `Get-AzureRmVmDiskEncryptionStatus` Cmdlet，並查看 ProgressMessage 欄位︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-765">Use the `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect the ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="6d1ca-766">VM 達到「OS disk encryption started」之後，需要在進階儲存體所支援的 VM 上耗費大約 40 至 50 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-766">After the VM reaches "OS disk encryption started," it takes about 40 to 50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="6d1ca-767">由於 WALinuxAgent 發生 [388 號問題](https://github.com/Azure/WALinuxAgent/issues/388)，某些散發套件的 `OsVolumeEncrypted` 和 `DataVolumesEncrypted` 會顯示為 `Unknown`。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="6d1ca-768">若使用 WALinuxAgent 2.1.5 和更新版本，就會自動修正此問題。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="6d1ca-769">如果您在輸出中看到 `Unknown`，可以使用 Azure 資源 Explorer 確認磁碟加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-769">If you see `Unknown` in the output, you can verify disk-encryption status by using the Azure Resource Explorer.</span></span>

 <span data-ttu-id="6d1ca-770">移至 [Azure 資源 Explorer](https://resources.azure.com/)，然後在左側選取面板中展開這個階層︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-770">Go to [Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in the selection panel on left:</span></span>

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

 <span data-ttu-id="6d1ca-771">在 InstanceView 中，向下捲動以查看磁碟機的加密狀態。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-771">In the InstanceView, scroll down to see the encryption status of your drives.</span></span>

 ![VM 執行個體檢視](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="6d1ca-773">查看[開機診斷](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="6d1ca-774">來自 ADE 擴充功能的訊息應該會在前面加上 `[AzureDiskEncryption]`。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-774">Messages from the ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="6d1ca-775">透過 SSH 登入 VM，並從下列位置取得擴充功能記錄檔：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-775">Sign in to the VM via SSH, and get the extension log from:</span></span>

    <span data-ttu-id="6d1ca-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="6d1ca-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="6d1ca-777">不建議在 OS 加密進行時登入 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-777">We recommend that you do not sign in to the VM while OS encryption is in progress.</span></span> <span data-ttu-id="6d1ca-778">其他兩個方法都失敗時，只複製記錄檔。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-778">Copy the logs only when the other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="6d1ca-779">準備已預先加密的 Linux VHD</span><span class="sxs-lookup"><span data-stu-id="6d1ca-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="6d1ca-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="6d1ca-780">Ubuntu 16</span></span>
<span data-ttu-id="6d1ca-781">在發佈安裝期間執行下列步驟以設定加密︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-781">Configure encryption during the distribution installation by doing the following:</span></span>

1. <span data-ttu-id="6d1ca-782">在分割磁碟時選取 [設定加密的磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-782">Select **Configure encrypted volumes** when you partition the disks.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="6d1ca-784">另外建立一個不得加密的開機磁碟機。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="6d1ca-785">加密根磁碟機。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-785">Encrypt your root drive.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="6d1ca-787">提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-787">Provide a passphrase.</span></span> <span data-ttu-id="6d1ca-788">這是您要上傳至金鑰保存庫的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-788">This is the passphrase that you upload to the key vault.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="6d1ca-790">完成分割。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-790">Finish partitioning.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="6d1ca-792">啟動 VM 時會要求輸入複雜密碼，請使用步驟 3 中提供的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-792">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="6d1ca-794">使用[這些指示](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/)準備要上傳到 Azure 的 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-794">Prepare the VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="6d1ca-795">還不要執行最後一個步驟 (解除佈建 VM)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-795">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="6d1ca-796">設定加密來與 Azure 搭配運作，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-796">Configure encryption to work with Azure by doing the following:</span></span>

1. <span data-ttu-id="6d1ca-797">在 /usr/local/sbin/azure_crypt_key.sh 下，使用以下指令碼的內容建立檔案。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with the content in the following script.</span></span> <span data-ttu-id="6d1ca-798">請注意 KeyFileName，因為它是 Azure 使用的複雜密碼檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-798">Pay attention to the KeyFileName, because it is the passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
        echo "FAILED to find suitable passphrase file ..." >&2
        echo -n "Try to enter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="6d1ca-799">在 */etc/crypttab* 中變更 crypt 設定。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-799">Change the crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="6d1ca-800">它看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="6d1ca-801">如果您正在 Windows 中編輯 *azure_crypt_key.sh* 並將它複製到 Linux，執行 `dos2unix /usr/local/sbin/azure_crypt_key.sh`。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it to Linux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="6d1ca-802">在指令碼中新增可執行檔權限︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-802">Add executable permissions to the script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="6d1ca-803">以加上程式碼行的方式編輯 /etc/initramfs-tools/modules：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="6d1ca-804">執行 `update-initramfs -u -k all` 來更新 initramfs，以讓 `keyscript` 生效。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-804">Run `update-initramfs -u -k all` to update the initramfs to make the `keyscript` take effect.</span></span>

7. <span data-ttu-id="6d1ca-805">現在您可以取消佈建 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-805">Now you can deprovision the VM.</span></span>

 ![Ubuntu 16.04 設定](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="6d1ca-807">繼續進行下一個步驟，並[將 VHD 上傳](#upload-encrypted-vhd-to-an-azure-storage-account)到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-807">Continue to the next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="6d1ca-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="6d1ca-808">openSUSE 13.2</span></span>
<span data-ttu-id="6d1ca-809">若要在發佈安裝期間設定加密，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-809">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="6d1ca-810">分割磁碟時，請選取 [加密磁碟區群組]，然後輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-810">When you partition the disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="6d1ca-811">這是您要上傳到金鑰保存庫的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-811">This is the password that you will upload to your key vault.</span></span>

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="6d1ca-813">使用您的密碼啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-813">Boot the VM using your password.</span></span>

 ![openSUSE 13.2 設定](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="6d1ca-815">請依照[準備 Azure 的 SLES 或 openSUSE 虛擬機器](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131)中的指示準備 VM 以上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-815">Prepare the VM for uploading to Azure by following the instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="6d1ca-816">還不要執行最後一個步驟 (解除佈建 VM)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-816">Do not run the last step (deprovisioning the VM) yet.</span></span>

<span data-ttu-id="6d1ca-817">若要設定加密來與 Azure 搭配運作，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-817">To configure encryption to work with Azure, do the following:</span></span>
1. <span data-ttu-id="6d1ca-818">編輯 /etc/dracut.conf 並新增下面這一行︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-818">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="6d1ca-819">註解化 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 檔案結尾的這幾行程式碼：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-819">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="6d1ca-820">在 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh 檔案開頭附加下面這一行：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-820">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="6d1ca-821">變更所有出現的：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="6d1ca-822">至：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="6d1ca-823">編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 並將它附加至「# Open LUKS device」：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it to “# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
5. <span data-ttu-id="6d1ca-824">執行 `/usr/sbin/dracut -f -v` 以更新 initrd。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-824">Run `/usr/sbin/dracut -f -v` to update the initrd.</span></span>

6. <span data-ttu-id="6d1ca-825">現在您可以取消佈建 VM，並[將 VHD 上傳](#upload-encrypted-vhd-to-an-azure-storage-account)到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-825">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="6d1ca-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6d1ca-826">CentOS 7</span></span>
<span data-ttu-id="6d1ca-827">若要在發佈安裝期間設定加密，請執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-827">To configure encryption during the distribution installation, do the following:</span></span>
1. <span data-ttu-id="6d1ca-828">在分割磁碟時選取 [加密資料]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="6d1ca-830">確定已為根分割選取 [加密]。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="6d1ca-832">提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-832">Provide a passphrase.</span></span> <span data-ttu-id="6d1ca-833">這是您要上傳到金鑰保存庫的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-833">This is the passphrase that you will upload to your key vault.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="6d1ca-835">啟動 VM 時會要求輸入複雜密碼，請使用步驟 3 中提供的複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-835">When you boot the VM and are asked for a passphrase, use the passphrase you provided in step 3.</span></span>

 ![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="6d1ca-837">請依照[準備 Azure 的 CentOS 式虛擬機器](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70)中的「CentOS 7.0+」指示準備 VM 以上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-837">Prepare the VM for uploading into Azure by using the "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="6d1ca-838">還不要執行最後一個步驟 (解除佈建 VM)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-838">Do not run the last step (deprovisioning the VM) yet.</span></span>

6. <span data-ttu-id="6d1ca-839">現在您可以取消佈建 VM，並[將 VHD 上傳](#upload-encrypted-vhd-to-an-azure-storage-account)到 Azure。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-839">Now you can deprovision the VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="6d1ca-840">若要設定加密來與 Azure 搭配運作，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-840">To configure encryption to work with Azure, do the following:</span></span>

1. <span data-ttu-id="6d1ca-841">編輯 /etc/dracut.conf 並新增下面這一行︰</span><span class="sxs-lookup"><span data-stu-id="6d1ca-841">Edit the /etc/dracut.conf, and add the following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="6d1ca-842">註解化 /usr/lib/dracut/modules.d/90crypt/module-setup.sh 檔案結尾的這幾行程式碼：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-842">Comment out these lines by the end of the file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
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

3. <span data-ttu-id="6d1ca-843">在 /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh 檔案開頭附加下面這一行：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-843">Append the following line at the beginning of the file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="6d1ca-844">變更所有出現的：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="6d1ca-845">to</span><span class="sxs-lookup"><span data-stu-id="6d1ca-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="6d1ca-846">編輯 /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh 並將此附加在「# Open LUKS device」之後：</span><span class="sxs-lookup"><span data-stu-id="6d1ca-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after the “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying to get the key from disks ..." >&2
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
5. <span data-ttu-id="6d1ca-847">執行「/usr/sbin/dracut -f -v」來更新 initrd。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-847">Run the “/usr/sbin/dracut -f -v” to update the initrd.</span></span>

![CentOS 7 設定](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-to-an-azure-storage-account"></a><span data-ttu-id="6d1ca-849">上傳加密的 VHD 至 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="6d1ca-849">Upload encrypted VHD to an Azure storage account</span></span>
<span data-ttu-id="6d1ca-850">啟用 BitLocker 加密或 DM-Crypt 加密之後，需要將本機加密的 VHD 上傳至儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-850">After BitLocker encryption or DM-Crypt encryption is enabled, the local encrypted VHD needs to be uploaded to your storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-the-disk-encryption-secret-for-the-pre-encrypted-vm-to-your-key-vault"></a><span data-ttu-id="6d1ca-851">上傳已預先加密 VM 的磁碟加密密碼至金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="6d1ca-851">Upload the disk-encryption secret for the pre-encrypted VM to your key vault</span></span>
<span data-ttu-id="6d1ca-852">先前取得的磁碟加密密碼必須上傳，做為金鑰保存庫中的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-852">The disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="6d1ca-853">金鑰保存庫必須為 Azure AD 用戶端啟用磁碟加密以及權限。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-853">The key vault needs to have disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="6d1ca-854">未使用 KEK 加密的磁碟加密密碼</span><span class="sxs-lookup"><span data-stu-id="6d1ca-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="6d1ca-855">若要在金鑰保存庫中設定密碼，請使用 [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-855">To set up the secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="6d1ca-856">如果您有 Windows 虛擬機器，bek 檔案會以 base64 字串編碼，然後使用 `Set-AzureKeyVaultSecret` Cmdlet 上傳至您的金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-856">If you have a Windows virtual machine, the bek file is encoded as a base64 string and then uploaded to your key vault using the `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="6d1ca-857">如果是 Linux，複雜密碼會以 base64 字串編碼，然後上傳至金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-857">For Linux, the passphrase is encoded as a base64 string and then uploaded to the key vault.</span></span> <span data-ttu-id="6d1ca-858">此外，請確定在金鑰保存庫中建立密碼時會設定下列標籤。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-858">In addition, make sure that the following tags are set when you create the secret in the key vault.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="6d1ca-859">在下一個步驟中使用 `$secretUrl`，以便[在不使用 KEK 的狀況下連接 OS 磁碟](#without-using-a-kek)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-859">Use the `$secretUrl` in the next step for [attaching the OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="6d1ca-860">使用 KEK 加密的磁碟加密密碼</span><span class="sxs-lookup"><span data-stu-id="6d1ca-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="6d1ca-861">將密碼上傳至金鑰保存庫之前，您可以選擇性地使用金鑰加密金鑰來加密密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-861">Before you upload the secret to the key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="6d1ca-862">使用包裝 [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) 先加密使用金鑰加密金鑰的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-862">Use the wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) to first encrypt the secret using the key encryption key.</span></span> <span data-ttu-id="6d1ca-863">這個包裝作業的輸出是 base64 URL 編碼的字串，您可以接著使用 [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) Cmdlet 將它上傳做為密碼。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-863">The output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using the [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is the passphrase that was provided for encryption during the distribution installation
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

<span data-ttu-id="6d1ca-864">在下一個步驟中使用 `$KeyEncryptionKey` 和 `$secretUrl`，以便[使用 KEK 連接 OS 磁碟](#using-a-kek)。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-864">Use `$KeyEncryptionKey` and `$secretUrl` in the next step for [attaching the OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="6d1ca-865">連接 OS 磁碟時，指定密碼的 URL</span><span class="sxs-lookup"><span data-stu-id="6d1ca-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="6d1ca-866">不使用 KEK</span><span class="sxs-lookup"><span data-stu-id="6d1ca-866">Without using a KEK</span></span>
<span data-ttu-id="6d1ca-867">當您在連接 OS 磁碟時，需要傳遞 `$secretUrl`。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-867">While you are attaching the OS disk, you need to pass `$secretUrl`.</span></span> <span data-ttu-id="6d1ca-868">URL 已在「未使用 KEK 加密的磁碟加密密碼」一節中產生。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-868">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="6d1ca-869">使用 KEK</span><span class="sxs-lookup"><span data-stu-id="6d1ca-869">Using a KEK</span></span>
<span data-ttu-id="6d1ca-870">連接 OS 磁碟時，傳遞 `$KeyEncryptionKey` 和 `$secretUrl`。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-870">When you attach the OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="6d1ca-871">URL 已在「未使用 KEK 加密的磁碟加密密碼」一節中產生。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-871">The URL was generated in the "Disk-encryption secret not encrypted with a KEK" section.</span></span>

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

## <a name="download-this-guide"></a><span data-ttu-id="6d1ca-872">下載此指南</span><span class="sxs-lookup"><span data-stu-id="6d1ca-872">Download this guide</span></span>
<span data-ttu-id="6d1ca-873">您可以從 [TechNet 資源庫](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)下載此指南。</span><span class="sxs-lookup"><span data-stu-id="6d1ca-873">You can download this guide from the [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="6d1ca-874">取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6d1ca-874">For more information</span></span>
[<span data-ttu-id="6d1ca-875">探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 1 部分</span><span class="sxs-lookup"><span data-stu-id="6d1ca-875">Explore Azure Disk Encryption with Azure PowerShell - Part 1</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[<span data-ttu-id="6d1ca-876">探索使用 Azure PowerShell 的 Azure 磁碟加密 - 第 2 部分</span><span class="sxs-lookup"><span data-stu-id="6d1ca-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
