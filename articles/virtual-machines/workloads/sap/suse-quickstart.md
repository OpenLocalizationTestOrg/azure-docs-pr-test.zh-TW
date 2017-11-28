---
title: "Microsoft Azure SUSE Linux Vm 上的 SAP NetWeaver aaaTesting |Microsoft 文件"
description: "在 Microsoft Azure SUSE Linux VM 上測試 SAP NetWeaver"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 645e358b-3ca1-4d3d-bf70-b0f287498d7a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: hermannd
ms.openlocfilehash: 0e3faab05417a1a15541e2b79aa7eddacda44611
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-sap-netweaver-on-microsoft-azure-suse-linux-vms"></a><span data-ttu-id="d5f4a-103">在 Microsoft Azure SUSE Linux VM 上執行 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="d5f4a-103">Running SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>
<span data-ttu-id="d5f4a-104">如果您在 Microsoft Azure SUSE Linux 虛擬機器 (Vm) 上執行的 SAP NetWeaver，本文將說明各種項目 tooconsider。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-104">This article describes various things tooconsider when you're running SAP NetWeaver on Microsoft Azure SUSE Linux virtual machines (VMs).</span></span> <span data-ttu-id="d5f4a-105">自 2016 年 5 月 19 日起，在 Azure 的 SUSE Linux VM 上已正式支援 SAP NetWeaver。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-105">As of May 19 2016 SAP NetWeaver is officially supported on SUSE Linux VMs on Azure.</span></span> <span data-ttu-id="d5f4a-106">如需有關 Linux 版本、SAP 核心版本等等的所有詳細資料，請參閱 SAP 附註 1928533＜Azure 上的 SAP 應用程式︰支援的產品和 Azure VM 類型＞。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-106">All details regarding Linux versions, SAP kernel versions and so on can be found in SAP Note 1928533 "SAP Applications on Azure: Supported Products and Azure VM types".</span></span>
<span data-ttu-id="d5f4a-107">如需 Linux VM 上 SAP 的進一步相關文件，請參閱︰[在 Linux 虛擬機器 (VM) 上使用 SAP](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-107">Further documentation about SAP on Linux VMs can be found here : [Using SAP on Linux virtual machines (VMs)](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d5f4a-108">hello 下列資訊應可協助您避免某些可能出現的錯誤。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-108">hello following information should help you avoid some potential pitfalls.</span></span>

## <a name="suse-images-on-azure-for-running-sap"></a><span data-ttu-id="d5f4a-109">Azure 上用來執行 SAP 的 SUSE 映像</span><span class="sxs-lookup"><span data-stu-id="d5f4a-109">SUSE images on Azure for running SAP</span></span>
<span data-ttu-id="d5f4a-110">若要在 Azure 上執行 SAP NetWeaver，請只使用 SUSE Linux Enterprise Server SLES 12 (SPx) - 另請參閱 SAP 附註 1928533。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-110">For running SAP NetWeaver on Azure, use only SUSE Linux Enterprise Server SLES 12 ( SPx ) - see also SAP note 1928533.</span></span> <span data-ttu-id="d5f4a-111">特殊的 SUSE 映像處於 hello Azure Marketplace (「 SLES 11 SP3 的 SAP CAL")，但這並不適用於一般使用方式。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-111">A special SUSE image is in hello Azure Marketplace ("SLES 11 SP3 for SAP CAL"), but this is not intended for general usage.</span></span> <span data-ttu-id="d5f4a-112">請勿使用此映像，因為它保留供 hello [SAP 雲端應用裝置程式庫](https://cal.sap.com/)方案。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-112">Do not use this image because it's reserved for hello [SAP Cloud Appliance Library](https://cal.sap.com/) solution.</span></span>  

<span data-ttu-id="d5f4a-113">針對 Azure 上的所有新測試和安裝，您應該使用 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-113">You should use Azure Resource Manager for all new tests and installations on Azure.</span></span> <span data-ttu-id="d5f4a-114">toolook SUSE SLES 映像及使用 Azure PowerShell 或 hello Azure 命令列介面 (CLI)，下列命令使用 hello 的版本。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-114">toolook for SUSE SLES images and versions by using Azure PowerShell or hello Azure command-line interface (CLI), use hello following commands.</span></span> <span data-ttu-id="d5f4a-115">然後，您可以使用 hello 輸出，例如 toodefine hello 中作業系統映像部署新的 SUSE Linux VM 的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-115">You can then use hello output, for example, toodefine hello OS image in a JSON template for deploying a new SUSE Linux VM.</span></span>
<span data-ttu-id="d5f4a-116">下列 PowerShell 命令適用於 Azure Powershell 版本 1.0.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-116">These PowerShell commands are valid for Azure PowerShell version 1.0.1 and later.</span></span>

<span data-ttu-id="d5f4a-117">建議您使用時仍有可能 toouse hello 標準 SLES 映像為 SAP 安裝 toomake 使用 hello 新 SLES，也就是可用的 SAP 映像現在 hello Azure 上影像的影像圖庫。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-117">While it's still possible toouse hello standard SLES images for SAP installations it's recommended toomake use of hello new SLES for SAP images which are available now on hello Azure image gallery.</span></span> <span data-ttu-id="d5f4a-118">可以找到這些映像的詳細資訊，在 hello 對應[Azure Marketplace 頁面]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP )或 hello [SUSE 常見問題集相關網頁適用於 SAP 的 SLES]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ )。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-118">More information about these images can be found on hello corresponding [Azure Marketplace page]( https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SUSE.SLES-SAP ) or hello [SUSE FAQ web page about SLES for SAP]( https://www.suse.com/products/sles-for-sap/frequently-asked-questions/ ).</span></span>


* <span data-ttu-id="d5f4a-119">尋找現有的發佈者，包括 SUSE：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-119">Look for existing publishers, including SUSE:</span></span>
  
   ```
   PS  : Get-AzureRmVMImagePublisher -Location "West Europe"  | where-object { $_.publishername -like "*US*"  }
   CLI : azure vm image list-publishers westeurope | grep "US"
   ```
* <span data-ttu-id="d5f4a-120">從 SUSE 尋找現有的供應項目：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-120">Look for existing offerings from SUSE:</span></span>
  
   ```
   PS  : Get-AzureRmVMImageOffer -Location "West Europe" -Publisher "SUSE"
   CLI : azure vm image list-offers westeurope SUSE
   ```
* <span data-ttu-id="d5f4a-121">尋找 SUSE SLES 供應項目：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-121">Look for SUSE SLES offerings:</span></span>
  
   ```
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES"
   PS  : Get-AzureRmVMImageSku -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP"
   CLI : azure vm image list-skus westeurope SUSE SLES
   CLI : azure vm image list-skus westeurope SUSE SLES-SAP
   ```
* <span data-ttu-id="d5f4a-122">尋找 SLES SKU 的特定版本：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-122">Look for a specific version of a SLES SKU:</span></span>
  
   ```
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES" -skus "12-SP2"
   PS  : Get-AzureRmVMImage -Location "West Europe" -Publisher "SUSE" -Offer "SLES-SAP" -skus "12-SP2"
   CLI : azure vm image list westeurope SUSE SLES 12-SP2
   CLI : azure vm image list westeurope SUSE SLES-SAP 12-SP2
   ```

## <a name="installing-walinuxagent-in-a-suse-vm"></a><span data-ttu-id="d5f4a-123">在 SUSE VM 中安裝 WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="d5f4a-123">Installing WALinuxAgent in a SUSE VM</span></span>
<span data-ttu-id="d5f4a-124">呼叫 WALinuxAgent hello 代理程式是在 hello Azure Marketplace 中的 hello SLES 映像的一部分。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-124">hello agent called WALinuxAgent is part of hello SLES images in hello Azure Marketplace.</span></span> <span data-ttu-id="d5f4a-125">如需手動安裝 (例如從內部部署上傳 SLES OS 虛擬磁碟 (VHD)) 的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-125">For information about installing it manually (for example, when uploading a SLES OS virtual hard disk (VHD) from on-premises), see:</span></span>

* [<span data-ttu-id="d5f4a-126">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="d5f4a-126">OpenSUSE</span></span>](http://software.opensuse.org/package/WALinuxAgent)
* [<span data-ttu-id="d5f4a-127">Azure</span><span class="sxs-lookup"><span data-stu-id="d5f4a-127">Azure</span></span>](../../linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d5f4a-128">SUSE</span><span class="sxs-lookup"><span data-stu-id="d5f4a-128">SUSE</span></span>](https://www.suse.com/communities/blog/suse-linux-enterprise-server-configuration-for-windows-azure/)

## <a name="sap-enhanced-monitoring"></a><span data-ttu-id="d5f4a-129">SAP「增強型監視」</span><span class="sxs-lookup"><span data-stu-id="d5f4a-129">SAP "enhanced monitoring"</span></span>
<span data-ttu-id="d5f4a-130">SAP 「 增強監視 」 是必要的先決條件 toorun SAP on Azure。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-130">SAP "enhanced monitoring" is a mandatory prerequisite toorun SAP on Azure.</span></span> <span data-ttu-id="d5f4a-131">請查看 SAP 附註 2191498＜Linux 搭配 Azure 上的 SAP：增強型監視＞中的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-131">Please check details in SAP note 2191498 "SAP on Linux with Azure: Enhanced Monitoring".</span></span>

## <a name="attaching-azure-data-disks-tooan-azure-linux-vm"></a><span data-ttu-id="d5f4a-132">附加的 Azure 資料磁碟 tooan Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="d5f4a-132">Attaching Azure data disks tooan Azure Linux VM</span></span>
<span data-ttu-id="d5f4a-133">使用 hello 裝置識別碼，您應該永遠不會掛接 Azure 資料磁碟 tooan Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="d5f4a-133">You should never mount Azure data disks tooan Azure Linux VM by using hello device ID.</span></span> <span data-ttu-id="d5f4a-134">請改用 hello 通用唯一識別碼 (UUID)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-134">Instead, use hello universally unique identifier (UUID).</span></span> <span data-ttu-id="d5f4a-135">當您使用圖形化工具 toomount Azure 資料磁碟，例如，請格外小心。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-135">Be careful when you use graphical tools toomount Azure data disks, for example.</span></span> <span data-ttu-id="d5f4a-136">請仔細檢查 hello /etc/fstab 中的項目。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-136">Double-check hello entries in /etc/fstab.</span></span>

<span data-ttu-id="d5f4a-137">hello 裝置識別碼 hello 問題是，它可能會變更，然後 hello Azure VM 可能會停止回應 hello 開機程序。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-137">hello issue with hello device ID is that it might change, and then hello Azure VM might hang in hello boot process.</span></span> <span data-ttu-id="d5f4a-138">toomitigate hello 問題，您可以在 /etc/fstab 中新增 hello nofail 參數。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-138">toomitigate hello issue, you could add hello nofail parameter in /etc/fstab.</span></span> <span data-ttu-id="d5f4a-139">但是，請謹慎使用 nofail，因此應用程式可能會使用 hello 掛接點，做為前，以防外部的 Azure 資料磁碟未掛接 hello 開機期間，可能會寫入 hello 根檔案系統。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-139">But, be careful with nofail because applications might use hello mount point as before, and might write into hello root file system in case an external Azure data disk wasn't mounted during hello boot.</span></span>

<span data-ttu-id="d5f4a-140">hello 唯一的例外狀況 toomounting 透過 UUID 附加為疑難排解 hello 之後 > 一節中所述的用途，作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-140">hello only exception toomounting via UUID is attaching an OS disk for troubleshooting purposes, as described in hello following section.</span></span>

## <a name="troubleshooting-a-suse-vm-that-isnt-accessible-anymore"></a><span data-ttu-id="d5f4a-141">針對無法再存取的 SUSE VM 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d5f4a-141">Troubleshooting a SUSE VM that isn't accessible anymore</span></span>
<span data-ttu-id="d5f4a-142">可能會有其中 SUSE VM 在 Azure 上停止回應 hello 開機程序 （例如，具有與掛接的磁碟相關的錯誤） 的情況。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-142">There might be situations where a SUSE VM on Azure hangs in hello boot process (for example, with an error related to mounting disks).</span></span> <span data-ttu-id="d5f4a-143">您可以使用 Azure 虛擬機器 v2 hello Azure 入口網站中的 hello 開機診斷功能來確認此問題。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-143">You can verify this issue by using hello boot diagnostics feature for Azure Virtual Machines v2 in hello Azure portal.</span></span> <span data-ttu-id="d5f4a-144">如需詳細資訊，請參閱 [開機診斷](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-144">For more information, see [Boot diagnostics](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span>

<span data-ttu-id="d5f4a-145">其中一種方式 toosolve hello 問題是從 hello tooattach hello OS 磁碟損毀 VM tooanother SUSE VM 在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-145">One way toosolve hello problem is tooattach hello OS disk from hello damaged VM tooanother SUSE VM on Azure.</span></span> <span data-ttu-id="d5f4a-146">Hello 下一節中所述，然後進行適當的變更，例如編輯 /etc/fstab 或移除網路 udev 規則。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-146">Then make appropriate changes like editing /etc/fstab or removing network udev rules, as described in hello next section.</span></span>

<span data-ttu-id="d5f4a-147">還有一個很重要的事 tooconsider。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-147">There is one important thing tooconsider.</span></span> <span data-ttu-id="d5f4a-148">部署數個 SUSE Vm 從相同的 Azure Marketplace 映像 (例如，SLES 11 SP4) 會導致的 hello hello OS 磁碟 tooalways hello 由裝載 UUID 相同。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-148">Deploying several SUSE VMs from hello same Azure Marketplace image (for example, SLES 11 SP4) causes hello OS disk tooalways be mounted by hello same UUID.</span></span> <span data-ttu-id="d5f4a-149">因此，使用 hello UUID tooattach 從不同的 VM 部署使用相同的 Azure Marketplace 映像會導致兩個相同的 Uuid hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-149">Therefore, using hello UUID tooattach an OS disk from a different VM that was deployed by using hello same Azure Marketplace image will result in two identical UUIDs.</span></span> <span data-ttu-id="d5f4a-150">這會造成問題，可能表示 hello 適用於疑難排解的 VM 實際上會從附加的 hello 開機，及損毀的作業系統磁碟，而不是 hello 原始。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-150">This causes problems and could mean that hello VM meant for troubleshooting will in fact boot from hello attached and damaged OS disk instead of hello original one.</span></span>

<span data-ttu-id="d5f4a-151">有兩種方式 tooavoid 這樣：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-151">There are two ways tooavoid this:</span></span>

* <span data-ttu-id="d5f4a-152">使用不同的 Azure Marketplace 映像的 hello 疑難排解 VM (例如，SLES 11 SPx 而不是 SLES 12)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-152">Use a different Azure Marketplace image for hello troubleshooting VM (for example, SLES 11 SPx instead of SLES 12 ).</span></span>
* <span data-ttu-id="d5f4a-153">從另一個 VM 不附加的損毀的 hello OS 磁碟使用 UUID-使用其他項目。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-153">Don't attach hello damaged OS disk from another VM by using UUID--use something else.</span></span>

## <a name="uploading-a-suse-vm-from-on-premises-tooazure"></a><span data-ttu-id="d5f4a-154">上傳 SUSE VM 從內部部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d5f4a-154">Uploading a SUSE VM from on-premises tooAzure</span></span>
<span data-ttu-id="d5f4a-155">如需 hello 步驟 tooupload SUSE VM 從內部部署 tooAzure 的說明，請參閱[SLES 或 openSUSE 虛擬機器做好 Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-155">For a description of hello steps tooupload a SUSE VM from on-premises tooAzure, see [Prepare a SLES or openSUSE virtual machine for Azure](../../linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d5f4a-156">如果您想的 tooupload hello 端 （例如，tookeep 現有 SAP 安裝，以及 hello 主機名稱） 步驟沒有 hello 解除佈建 VM，請檢查下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d5f4a-156">If you want tooupload a VM without hello deprovision step at hello end (for example, tookeep an existing SAP installation, as well as hello host name), check hello following items:</span></span>

* <span data-ttu-id="d5f4a-157">請確定該 hello OS 磁碟掛接使用 UUID 和不 hello 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-157">Make sure that hello OS disk is mounted by using UUID and not hello device ID.</span></span> <span data-ttu-id="d5f4a-158">變更只是在 /etc/fstab tooUUID 是不夠的 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-158">Changing tooUUID just in /etc/fstab is not enough for hello OS disk.</span></span> <span data-ttu-id="d5f4a-159">此外，別忘了 tooadapt hello 開機載入器透過 YaST 或藉由編輯 /boot/grub/menu.lst。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-159">Also, don't forget tooadapt hello boot loader through YaST or by editing /boot/grub/menu.lst.</span></span>
* <span data-ttu-id="d5f4a-160">如果您使用 hello VHDX 格式的 hello SUSE 作業系統磁碟，並將它轉換為上傳 tooAzure tooVHD，很可能是該 hello 網路裝置，將變更 eth0 tooeth1。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-160">If you use hello VHDX format for hello SUSE OS disk and convert it tooVHD for uploading tooAzure, it's very likely that hello network device will change from eth0 tooeth1.</span></span> <span data-ttu-id="d5f4a-161">中所述，tooavoid 問題時要在 Azure 上啟動更新版本中，變更後 tooeth0[修正 eth0 中的複製 SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-161">tooavoid issues when you're booting on Azure later, change back tooeth0 as described in [Fixing eth0 in cloned SLES 11 VMware](https://dartron.wordpress.com/2013/09/27/fixing-eth1-in-cloned-sles-11-vmware/).</span></span>

<span data-ttu-id="d5f4a-162">Toowhat 的此外 hello 文章所述，我們建議您移除這個：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-162">In addition toowhat's described in hello article, we recommend that you remove this:</span></span>

   <span data-ttu-id="d5f4a-163">/lib/udev/rules.d/75-persistent-net-generator.rules</span><span class="sxs-lookup"><span data-stu-id="d5f4a-163">/lib/udev/rules.d/75-persistent-net-generator.rules</span></span>

<span data-ttu-id="d5f4a-164">您也可以安裝 hello Azure Linux 代理程式 (waagent) toohelp 您避免潛在的問題，只要不是多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-164">You can also install hello Azure Linux Agent (waagent) toohelp you avoid potential issues, as long as there are not multiple NICs.</span></span>

## <a name="deploying-a-suse-vm-on-azure"></a><span data-ttu-id="d5f4a-165">在 Azure 上部署 SUSE VM</span><span class="sxs-lookup"><span data-stu-id="d5f4a-165">Deploying a SUSE VM on Azure</span></span>
<span data-ttu-id="d5f4a-166">您應該使用 hello 新的 Azure Resource Manager 模型中的 JSON 範本檔案來建立新的 SUSE Vm。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-166">You should create new SUSE VMs by using JSON template files in hello new Azure Resource Manager model.</span></span> <span data-ttu-id="d5f4a-167">Hello JSON 範本檔案建立之後，您可以使用下列替代 tooPowerShell 為 CLI 命令的 hello 部署 hello VM:</span><span class="sxs-lookup"><span data-stu-id="d5f4a-167">After hello JSON template file is created, you can deploy hello VM by using hello following CLI command as an alternative tooPowerShell:</span></span>

   ```
   azure group deployment create "<deployment name>" -g "<resource group name>" --template-file "<../../filename.json>"

   ```
<span data-ttu-id="d5f4a-168">如需有關 JSON 範本檔案的更多詳細資料，請參閱[編寫 Azure Resource Manager 範本](../../../resource-group-authoring-templates.md)和 [Azure 快速入門範本](https://azure.microsoft.com/documentation/templates/)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-168">For more details about JSON template files, see [Authoring Azure Resource Manager templates](../../../resource-group-authoring-templates.md) and [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span>

<span data-ttu-id="d5f4a-169">如需 CLI 和 Azure 資源管理員的詳細資訊，請參閱[使用 hello for Mac、 Linux 及 Windows Azure 資源管理員使用 Azure CLI](../../../xplat-cli-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-169">For more details about CLI and Azure Resource Manager, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../../../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="sap-license-and-hardware-key"></a><span data-ttu-id="d5f4a-170">SAP 授權與硬體金鑰</span><span class="sxs-lookup"><span data-stu-id="d5f4a-170">SAP license and hardware key</span></span>
<span data-ttu-id="d5f4a-171">官方 SAP Azure 認證 hello，新的機制已導入了的 toocalculate hello SAP 硬體金鑰用於 hello SAP 授權。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-171">For hello official SAP-Azure certification, a new mechanism was introduced toocalculate hello SAP hardware key that's used for hello SAP license.</span></span> <span data-ttu-id="d5f4a-172">hello SAP 核心必須調整 toobe toomake 的用法。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-172">hello SAP kernel had toobe adapted toomake use of this.</span></span> <span data-ttu-id="d5f4a-173">Linux 先前的 SAP 核心版本不包括此程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-173">Former SAP kernel versions for Linux did not include this code change.</span></span> <span data-ttu-id="d5f4a-174">因此，在某些情況下 (例如，Azure VM 調整大小)、 變更 hello SAP 硬體金鑰與 hello SAP 授權已不再有效。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-174">Therefore, in certain situations (for example, Azure VM resizing), hello SAP hardware key changed and hello SAP license was no longer be valid.</span></span> <span data-ttu-id="d5f4a-175">在最新 SAP Linux 核心 hello 可解決此問題。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-175">This is solved in hello latest SAP Linux kernels.</span></span> <span data-ttu-id="d5f4a-176">如需詳細資料，請查看 SAP 附註 1928533。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-176">For details please check SAP note 1928533.</span></span>

## <a name="suse-sapconf-package--tuned-adm"></a><span data-ttu-id="d5f4a-177">SUSE sapconf 封裝 / tuned-adm</span><span class="sxs-lookup"><span data-stu-id="d5f4a-177">SUSE sapconf package / tuned-adm</span></span>
<span data-ttu-id="d5f4a-178">SUSE 提供稱為 "sapconf" 的封裝，這組封裝負責管理一組 SAP 特定設定。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-178">SUSE provides a package called "sapconf" that manages a set of SAP-specific settings.</span></span> <span data-ttu-id="d5f4a-179">如詳細什麼此封裝，以及如何 tooinstall 並使用它，請參閱[使用 sapconf tooprepare SUSE Linux Enterprise Server toorun SAP 系統](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/)和[何謂 sapconf 或如何 tooprepare SUSE Linux Enterprise用於執行 SAP 系統的伺服器嗎？](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).</span><span class="sxs-lookup"><span data-stu-id="d5f4a-179">For more details about what this package does, and how tooinstall and use it, see [Using sapconf tooprepare a SUSE Linux Enterprise Server toorun SAP systems](https://www.suse.com/communities/blog/using-sapconf-to-prepare-suse-linux-enterprise-server-to-run-sap-systems/) and [What is sapconf or how tooprepare a SUSE Linux Enterprise Server for running SAP systems?](http://scn.sap.com/community/linux/blog/2014/03/31/what-is-sapconf-or-how-to-prepare-a-suse-linux-enterprise-server-for-running-sap-systems).</span></span>

<span data-ttu-id="d5f4a-180">在 hello 同時有這項新工具取代 sapconf-微調.adm</span><span class="sxs-lookup"><span data-stu-id="d5f4a-180">In hello meantime there is a new tool which replaces sapconf - tuned-adm.</span></span> <span data-ttu-id="d5f4a-181">其中一個可以找到下列 hello 下方的兩個連結此工具的更多詳細。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-181">One can find more details about this tool following hello two links below.</span></span>

<span data-ttu-id="d5f4a-182">您可以在 [這裡](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html)</span><span class="sxs-lookup"><span data-stu-id="d5f4a-182">SLES documentation about tuned-adm profile sap-hana can be found [here](https://www.suse.com/documentation/sles-for-sap-12/book_s4s/data/sec_s4s_configure_sapconf.html)</span></span> 

<span data-ttu-id="d5f4a-183">您可以在第 6.2 章中的 [這裡](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) ，找到如何利用 tuned-adm 針對 SAP 工作負載微調系統</span><span class="sxs-lookup"><span data-stu-id="d5f4a-183">Tuning Systems for SAP Workloads with tuned-adm - can be found [here](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/book_s4s/book_s4s.pdf) in chapter 6.2</span></span>

## <a name="nfs-share-in-distributed-sap-installations"></a><span data-ttu-id="d5f4a-184">分散式 SAP 安裝中的 NFS 共用</span><span class="sxs-lookup"><span data-stu-id="d5f4a-184">NFS share in distributed SAP installations</span></span>
<span data-ttu-id="d5f4a-185">如果您擁有分散式的安裝中-例如，您想要 tooinstall hello 資料庫並 hello SAP 應用程式伺服器在不同的 Vm--您可以共用 hello /sapmnt 目錄透過網路檔案系統 (NFS)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-185">If you have a distributed installation--for example, where you want tooinstall hello database and hello SAP application servers in separate VMs--you can share hello /sapmnt directory via Network File System (NFS).</span></span> <span data-ttu-id="d5f4a-186">如果您建立 NFS 共用的 /sapmnt hello 之後，您就會發生問題 hello 安裝步驟，請檢查 toosee 如果"no_root_squash"hello 共用設定。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-186">If you have problems with hello installation steps after you create hello NFS share for /sapmnt, check toosee if "no_root_squash" is set for hello share.</span></span>

## <a name="logical-volumes"></a><span data-ttu-id="d5f4a-187">邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="d5f4a-187">Logical volumes</span></span>
<span data-ttu-id="d5f4a-188">在過去的 hello 視其中一個大型的邏輯磁碟區跨多個 Azure 資料磁碟 （例如，適用於 hello SAP 資料庫），被建議 toouse mdadm lvm 未完全在 Azure 上尚未驗證。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-188">In hello past if one needed a large logical volume across multiple Azure data disks (for example, for hello SAP database), it was recommended toouse mdadm as lvm wasn't fully validated yet on Azure.</span></span> <span data-ttu-id="d5f4a-189">如何使用 mdadm，在 Azure 上的 Linux RAID 向上 tooset 參閱的 toolearn[設定軟體 RAID on Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-189">toolearn how tooset up Linux RAID on Azure by using mdadm, see [Configure software RAID on Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="d5f4a-190">在同時從 2016 年的開頭開始 hello 也 lvm 完全支援在 Azure 上，可用來當做替代 toomdadm。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-190">In hello meantime as of beginning of May 2016 also lvm is fully supported on Azure and can be used as an alternative toomdadm.</span></span> <span data-ttu-id="d5f4a-191">如需有關 Azure 上 lvm 的其他資訊，請參閱[在 Azure 中的 Linux VM 上設定 LVM](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-191">For additional information regarding lvm on Azure see [Configure LVM on a Linux VM in Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="azure-suse-repository"></a><span data-ttu-id="d5f4a-192">Azure SUSE 儲存機制</span><span class="sxs-lookup"><span data-stu-id="d5f4a-192">Azure SUSE repository</span></span>
<span data-ttu-id="d5f4a-193">如果您有存取 toohello 標準 Azure SUSE 儲存機制的問題，您可以使用簡單的命令 tooreset 它。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-193">If you have an issue with access toohello standard Azure SUSE repository, you can use a simple command tooreset it.</span></span> <span data-ttu-id="d5f4a-194">如果您的 Azure 區域，然後複製 hello 映像 tooa 不同區域想 toodeploy 建立私用的作業系統映像，可能會發生這個狀況根據此私用的作業系統映像的新 Vm。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-194">This might happen if you create a private OS image in an Azure region and then copy hello image tooa different region where you want toodeploy new VMs that are based on this private OS image.</span></span> <span data-ttu-id="d5f4a-195">只要執行下列命令 hello VM 內的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5f4a-195">Just run hello following command inside hello VM:</span></span>

   ```
   service guestregister restart
   ```

## <a name="gnome-desktop"></a><span data-ttu-id="d5f4a-196">Gnome 桌面</span><span class="sxs-lookup"><span data-stu-id="d5f4a-196">Gnome desktop</span></span>
<span data-ttu-id="d5f4a-197">如果您想 toouse hello Gnome 桌面 tooinstall 完整的 SAP 示範系統包括 SAP GUI，在單一 VM-內部瀏覽器，然後 SAP 管理主控台--使用此提示 tooinstall 它 hello Azure SLES 影像：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-197">If you want toouse hello Gnome desktop tooinstall a complete SAP demo system inside a single VM--including a SAP GUI, browser, and SAP management console--use this hint tooinstall it on hello Azure SLES images:</span></span>

   <span data-ttu-id="d5f4a-198">SLES 11：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-198">For SLES 11:</span></span>

   ```
   zypper in -t pattern gnome
   ```

   <span data-ttu-id="d5f4a-199">SLES 12：</span><span class="sxs-lookup"><span data-stu-id="d5f4a-199">For SLES 12:</span></span>

   ```
   zypper in -t pattern gnome-basic
   ```

## <a name="sap-support-for-oracle-on-linux-in-hello-cloud"></a><span data-ttu-id="d5f4a-200">Oracle Linux hello 雲端上的 SAP 支援</span><span class="sxs-lookup"><span data-stu-id="d5f4a-200">SAP support for Oracle on Linux in hello cloud</span></span>
<span data-ttu-id="d5f4a-201">在虛擬環境中，Oracle 對 Linux 的支援有所限制。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-201">There is a support restriction from Oracle on Linux in virtualized environments.</span></span> <span data-ttu-id="d5f4a-202">雖然這不是 Azure 特定主題，是重要的 toounderstand。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-202">Although this is not an Azure-specific topic, it's important toounderstand.</span></span> <span data-ttu-id="d5f4a-203">SAP 不支援 SUSE 上的 Oracle 或類似 Azure 之公用雲端中的 Red Hat。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-203">SAP does not support Oracle on SUSE or Red Hat in a public cloud like Azure.</span></span> <span data-ttu-id="d5f4a-204">toodiscuss 本主題中，請直接連絡 Oracle。</span><span class="sxs-lookup"><span data-stu-id="d5f4a-204">toodiscuss this topic, contact Oracle directly.</span></span>

