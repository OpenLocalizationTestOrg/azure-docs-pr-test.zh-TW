---
title: "aaaDesired 狀態設定為 Azure 概觀 |Microsoft 文件"
description: "PowerShell 預期狀態設定為使用 hello Microsoft Azure 延伸模組處理常式的概觀。 包括必要條件、架構、Cmdlet..."
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="c674e-104">簡介 toohello Azure Desired State Configuration 延伸模組處理常式</span><span class="sxs-lookup"><span data-stu-id="c674e-104">Introduction toohello Azure Desired State Configuration extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="c674e-105">hello Azure VM 代理程式和相關聯的延伸模組是 hello Microsoft Azure 基礎結構服務的一部分。</span><span class="sxs-lookup"><span data-stu-id="c674e-105">hello Azure VM Agent and associated Extensions are part of hello Microsoft Azure Infrastructure Services.</span></span> <span data-ttu-id="c674e-106">VM 擴充功能是擴充 hello VM 功能及簡化各種 VM 管理操作的軟體元件。</span><span class="sxs-lookup"><span data-stu-id="c674e-106">VM Extensions are software components that extend hello VM functionality and simplify various VM management operations.</span></span> <span data-ttu-id="c674e-107">例如，hello VMAccess 擴充功能可以使用的 tooreset 系統管理員密碼或 hello 自訂指令碼延伸可以是使用的 tooexecute hello VM 上的指令碼。</span><span class="sxs-lookup"><span data-stu-id="c674e-107">For example, hello VMAccess extension can be used tooreset an administrator's password, or hello Custom Script extension can be used tooexecute a script on hello VM.</span></span>

<span data-ttu-id="c674e-108">本文介紹 hello PowerShell 預期狀態設定 (DSC) 的延伸模組的 Azure Vm 中當做 hello Azure PowerShell SDK 的一部分。</span><span class="sxs-lookup"><span data-stu-id="c674e-108">This article introduces hello PowerShell Desired State Configuration (DSC) Extension for Azure VMs as part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="c674e-109">您可以使用新的 cmdlet tooupload，並以 hello PowerShell DSC 擴充功能已啟用 Azure VM 上套用的 PowerShell DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="c674e-109">You can use new cmdlets tooupload and apply a PowerShell DSC configuration on an Azure VM enabled with hello PowerShell DSC extension.</span></span> <span data-ttu-id="c674e-110">PowerShell DSC tooenact hello hello PowerShell DSC 擴充功能呼叫收到 hello VM 上的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="c674e-110">hello PowerShell DSC extension calls into PowerShell DSC tooenact hello received DSC configuration on hello VM.</span></span> <span data-ttu-id="c674e-111">這項功能也會透過 hello Azure 入口網站提供的。</span><span class="sxs-lookup"><span data-stu-id="c674e-111">This functionality is also available through hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c674e-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="c674e-112">Prerequisites</span></span>
<span data-ttu-id="c674e-113">**本機電腦**toointeract 與 hello Azure VM 延伸模組，您需要 toouse 任一 hello Azure 入口網站或 hello Azure PowerShell SDK。</span><span class="sxs-lookup"><span data-stu-id="c674e-113">**Local machine** toointeract with hello Azure VM extension, you need toouse either hello Azure portal or hello Azure PowerShell SDK.</span></span> 

<span data-ttu-id="c674e-114">**客體代理程式**hello hello DSC 組態所設定的 Azure VM 需要 toobe Windows Management Framework (WMF) 4.0 或是 5.0 支援的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c674e-114">**Guest Agent** hello Azure VM that is configured by hello DSC configuration needs toobe an OS that supports either Windows Management Framework (WMF) 4.0 or 5.0.</span></span> <span data-ttu-id="c674e-115">hello 支援的 OS 版本的完整清單位於 hello [DSC 延伸模組版本歷程記錄](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/)。</span><span class="sxs-lookup"><span data-stu-id="c674e-115">hello full list of supported OS versions can be found at hello [DSC Extension Version History](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).</span></span>

## <a name="terms-and-concepts"></a><span data-ttu-id="c674e-116">詞彙和概念</span><span class="sxs-lookup"><span data-stu-id="c674e-116">Terms and concepts</span></span>
<span data-ttu-id="c674e-117">本指南會假設您熟悉下列概念的 hello:</span><span class="sxs-lookup"><span data-stu-id="c674e-117">This guide presumes familiarity with hello following concepts:</span></span>

<span data-ttu-id="c674e-118">組態 - DSC 組態文件。</span><span class="sxs-lookup"><span data-stu-id="c674e-118">Configuration - A DSC configuration document.</span></span> 

<span data-ttu-id="c674e-119">節點 - DSC 組態的目標。</span><span class="sxs-lookup"><span data-stu-id="c674e-119">Node - A target for a DSC configuration.</span></span> <span data-ttu-id="c674e-120">在本文件中，「 節點 」 一律指的是 tooan Azure VM。</span><span class="sxs-lookup"><span data-stu-id="c674e-120">In this document, "node" always refers tooan Azure VM.</span></span>

<span data-ttu-id="c674e-121">組態資料 - 包含組態之環境資料的 .psd1 檔案</span><span class="sxs-lookup"><span data-stu-id="c674e-121">Configuration Data - A .psd1 file containing environmental data for a configuration</span></span>

## <a name="architectural-overview"></a><span data-ttu-id="c674e-122">架構概觀</span><span class="sxs-lookup"><span data-stu-id="c674e-122">Architectural overview</span></span>
<span data-ttu-id="c674e-123">hello Azure DSC 延伸模組會使用 hello Azure VM 代理程式架構 toodeliver、 制定，及報告 Azure Vm 上執行的 DSC 設定。</span><span class="sxs-lookup"><span data-stu-id="c674e-123">hello Azure DSC extension uses hello Azure VM Agent framework toodeliver, enact, and report on DSC configurations running on Azure VMs.</span></span> <span data-ttu-id="c674e-124">hello DSC 延伸模組需要包含至少一個組態文件.zip 檔案，並提供一組參數透過 hello Azure PowerShell SDK 或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c674e-124">hello DSC extension expects a .zip file containing at least a configuration document, and a set of parameters provided either through hello Azure PowerShell SDK or through hello Azure portal.</span></span>

<span data-ttu-id="c674e-125">當第一次呼叫 hello 延伸 hello 時，它會執行安裝程序。</span><span class="sxs-lookup"><span data-stu-id="c674e-125">When hello extension is called for hello first time, it runs an installation process.</span></span> <span data-ttu-id="c674e-126">這個程序會使用下列邏輯 hello hello Windows Management Framework (WMF) 的版本：</span><span class="sxs-lookup"><span data-stu-id="c674e-126">This process installs a version of hello Windows Management Framework (WMF) using hello following logic:</span></span>

1. <span data-ttu-id="c674e-127">如果 hello Azure VM 的作業系統是 Windows Server 2016，會不採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="c674e-127">If hello Azure VM OS is Windows Server 2016, no action is taken.</span></span> <span data-ttu-id="c674e-128">Windows Server 2016 已安裝的 PowerShell hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="c674e-128">Windows Server 2016 already has hello latest version of PowerShell installed.</span></span>
2. <span data-ttu-id="c674e-129">如果 hello`wmfVersion`屬性已指定，該版的 hello WMF 已安裝，除非它是與 hello VM 之 OS 不相容。</span><span class="sxs-lookup"><span data-stu-id="c674e-129">If hello `wmfVersion` property is specified, that version of hello WMF is installed unless it is incompatible with hello VM's OS.</span></span>
3. <span data-ttu-id="c674e-130">如果沒有`wmfVersion`屬性已指定，hello 最適用 hello WMF 已安裝的版本。</span><span class="sxs-lookup"><span data-stu-id="c674e-130">If no `wmfVersion` property is specified, hello latest applicable version of hello WMF is installed.</span></span>

<span data-ttu-id="c674e-131">Hello WMF 安裝需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="c674e-131">Installation of hello WMF requires a reboot.</span></span> <span data-ttu-id="c674e-132">重新開機後，hello 擴充功能下載 hello.zip 檔案中 hello 指定`modulesUrl`屬性。</span><span class="sxs-lookup"><span data-stu-id="c674e-132">After reboot, hello extension downloads hello .zip file specified in hello `modulesUrl` property.</span></span> <span data-ttu-id="c674e-133">如果這個位置是在 Azure blob 儲存體，SAS 權杖可以指定在 hello`sasToken`屬性 tooaccess hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="c674e-133">If this location is in Azure blob storage, a SAS token can be specified in hello `sasToken` property tooaccess hello file.</span></span> <span data-ttu-id="c674e-134">Hello.zip 會下載並解壓縮之後，hello 組態中定義的函式`configurationFunction`執行 toogenerate hello MOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="c674e-134">After hello .zip is downloaded and unpacked, hello configuration function defined in `configurationFunction` is run toogenerate hello MOF file.</span></span> <span data-ttu-id="c674e-135">然後執行 hello 延伸模組`Start-DscConfiguration -Force`在 hello 產生 MOF 檔案。</span><span class="sxs-lookup"><span data-stu-id="c674e-135">hello extension then runs `Start-DscConfiguration -Force` on hello generated MOF file.</span></span> <span data-ttu-id="c674e-136">hello 擴充功能會擷取輸出，並將它寫出 toohello Azure 狀態的通道。</span><span class="sxs-lookup"><span data-stu-id="c674e-136">hello extension captures output and writes it back out toohello Azure Status Channel.</span></span> <span data-ttu-id="c674e-137">從這個點上 hello DSC LCM 處理監視及修正像平常一樣。</span><span class="sxs-lookup"><span data-stu-id="c674e-137">From this point on, hello DSC LCM handles monitoring and correction as normal.</span></span> 

## <a name="powershell-cmdlets"></a><span data-ttu-id="c674e-138">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="c674e-138">PowerShell cmdlets</span></span>
<span data-ttu-id="c674e-139">PowerShell 指令程式可使用 Azure 資源管理員或 hello 傳統部署模型 toopackage、 發行和監視 DSC 延伸模組部署。</span><span class="sxs-lookup"><span data-stu-id="c674e-139">PowerShell cmdlets can be used with Azure Resource Manager or hello classic deployment model toopackage, publish, and monitor DSC extension deployments.</span></span> <span data-ttu-id="c674e-140">hello 列出下列 cmdlet hello 傳統部署模組，但是"Azure"取代"AzureRm"toouse hello Azure Resource Manager 模型。</span><span class="sxs-lookup"><span data-stu-id="c674e-140">hello following cmdlets listed are hello classic deployment modules, but "Azure" can be replaced with "AzureRm" toouse hello Azure Resource Manager model.</span></span> <span data-ttu-id="c674e-141">例如，`Publish-AzureVMDscConfiguration`使用 hello 傳統部署模型，其中`Publish-AzureRmVMDscConfiguration`使用 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="c674e-141">For example,  `Publish-AzureVMDscConfiguration` uses hello classic deployment model, where `Publish-AzureRmVMDscConfiguration` uses Azure Resource Manager.</span></span> 

<span data-ttu-id="c674e-142">`Publish-AzureVMDscConfiguration`接受在組態檔中、 掃描相依的 DSC 資源，然後建立包含 hello 組態和 DSC 資源所需的 tooenact hello 組態的.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="c674e-142">`Publish-AzureVMDscConfiguration` takes in a configuration file, scans it for dependent DSC resources, and creates a .zip file containing hello configuration and DSC resources needed tooenact hello configuration.</span></span> <span data-ttu-id="c674e-143">它也可以建立 hello 封裝使用本機 hello`-ConfigurationArchivePath`參數。</span><span class="sxs-lookup"><span data-stu-id="c674e-143">It can also create hello package locally using hello `-ConfigurationArchivePath` parameter.</span></span> <span data-ttu-id="c674e-144">否則，它會發行 hello.zip 檔案 tooAzure blob 儲存體，並保護其的安全與 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="c674e-144">Otherwise, it publishes hello .zip file tooAzure blob storage and secures it with a SAS token.</span></span>

<span data-ttu-id="c674e-145">此 cmdlet 建立 hello.zip 檔案根目錄 hello hello 保存資料夾有 hello.ps1 組態指令碼。</span><span class="sxs-lookup"><span data-stu-id="c674e-145">hello .zip file created by this cmdlet has hello .ps1 configuration script at hello root of hello archive folder.</span></span> <span data-ttu-id="c674e-146">資源擁有 hello 模組資料夾放在 hello 保存資料夾中。</span><span class="sxs-lookup"><span data-stu-id="c674e-146">Resources have hello module folder placed in hello archive folder.</span></span> 

<span data-ttu-id="c674e-147">`Set-AzureVMDscExtension`插入 hello 設定 hello PowerShell DSC 擴充功能所需的 VM 組態物件。</span><span class="sxs-lookup"><span data-stu-id="c674e-147">`Set-AzureVMDscExtension` injects hello settings needed by hello PowerShell DSC extension into a VM configuration object.</span></span> <span data-ttu-id="c674e-148">在 hello 傳統部署模型，hello VM 變更必須套用的 tooan Azure VM 與`Update-AzureVM`。</span><span class="sxs-lookup"><span data-stu-id="c674e-148">In hello classic deployment model, hello VM changes must be applied tooan Azure VM with `Update-AzureVM`.</span></span> 

<span data-ttu-id="c674e-149">`Get-AzureVMDscExtension`擷取特定 VM hello DSC 延伸模組狀態。</span><span class="sxs-lookup"><span data-stu-id="c674e-149">`Get-AzureVMDscExtension` retrieves hello DSC extension status of a particular VM.</span></span> 

<span data-ttu-id="c674e-150">`Get-AzureVMDscExtensionStatus`擷取 hello hello DSC 延伸模組處理常式所制定的 hello DSC 設定狀態。</span><span class="sxs-lookup"><span data-stu-id="c674e-150">`Get-AzureVMDscExtensionStatus` retrieves hello status of hello DSC configuration enacted by hello DSC extension handler.</span></span> <span data-ttu-id="c674e-151">此動作可在單一 VM 或一組 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="c674e-151">This action can be performed on a single VM, or group of VMs.</span></span>

<span data-ttu-id="c674e-152">`Remove-AzureVMDscExtension`移除指定的虛擬機器中的 hello 延伸模組處理常式。</span><span class="sxs-lookup"><span data-stu-id="c674e-152">`Remove-AzureVMDscExtension` removes hello extension handler from a given virtual machine.</span></span> <span data-ttu-id="c674e-153">此 cmdlet 會**不**移除 hello 設定、 解除安裝 WMF，hello 或變更 hello 虛擬機器上的 hello 套用設定。</span><span class="sxs-lookup"><span data-stu-id="c674e-153">This cmdlet does **not** remove hello configuration, uninstall hello WMF, or change hello applied settings on hello virtual machine.</span></span> <span data-ttu-id="c674e-154">它只會移除 hello 延伸模組處理常式。</span><span class="sxs-lookup"><span data-stu-id="c674e-154">It only removes hello extension handler.</span></span> 

<span data-ttu-id="c674e-155">**ASM 和 Azure Resource Manager Cmdlet 的主要差異**</span><span class="sxs-lookup"><span data-stu-id="c674e-155">**Key differences in ASM and Azure Resource Manager cmdlets**</span></span>

* <span data-ttu-id="c674e-156">Azure Resource Manager Cmdlet 是同步的。</span><span class="sxs-lookup"><span data-stu-id="c674e-156">Azure Resource Manager cmdlets are synchronous.</span></span> <span data-ttu-id="c674e-157">ASM Cmdlet 具備非同步性。</span><span class="sxs-lookup"><span data-stu-id="c674e-157">ASM cmdlets are asynchronous.</span></span>
* <span data-ttu-id="c674e-158">ResourceGroupName、VMName、ArchiveStorageAccountName、Version 及 Location 皆為 Azure Resource Manager 中的必要參數。</span><span class="sxs-lookup"><span data-stu-id="c674e-158">ResourceGroupName, VMName, ArchiveStorageAccountName, Version, and Location are all required parameters in Azure Resource Manager.</span></span>
* <span data-ttu-id="c674e-159">ArchiveResourceGroupName 是 Azure Resource Manager 的新選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="c674e-159">ArchiveResourceGroupName is a new optional parameter for Azure Resource Manager.</span></span> <span data-ttu-id="c674e-160">當您儲存體帳戶所屬 tooa 不同的資源群組的其中一個 hello 建立 hello 虛擬機器的位置時，您可以指定這個參數。</span><span class="sxs-lookup"><span data-stu-id="c674e-160">You can specify this parameter when your storage account belongs tooa different resource group than hello one where hello virtual machine is created.</span></span>
* <span data-ttu-id="c674e-161">ConfigurationArchive 在 Azure Resource Manager 中稱為 ArchiveBlobName</span><span class="sxs-lookup"><span data-stu-id="c674e-161">ConfigurationArchive is called ArchiveBlobName in Azure Resource Manager</span></span>
* <span data-ttu-id="c674e-162">ContainerName 在 Azure Resource Manager 中稱為 ArchiveContainerName</span><span class="sxs-lookup"><span data-stu-id="c674e-162">ContainerName is called ArchiveContainerName in Azure Resource Manager</span></span>
* <span data-ttu-id="c674e-163">StorageEndpointSuffix 在 Azure Resource Manager 中稱為 ArchiveStorageEndpointSuffix</span><span class="sxs-lookup"><span data-stu-id="c674e-163">StorageEndpointSuffix is called ArchiveStorageEndpointSuffix in Azure Resource Manager</span></span>
* <span data-ttu-id="c674e-164">已加入 tooAzure 自動更新 hello 延伸模組處理常式 toohello 最新版本與版本，並可供使用的資源管理員 tooenable hello AutoUpdate 交換器。</span><span class="sxs-lookup"><span data-stu-id="c674e-164">hello AutoUpdate switch has been added tooAzure Resource Manager tooenable automatic updating of hello extension handler toohello latest version as and when it is available.</span></span> <span data-ttu-id="c674e-165">請注意，這個參數會有 hello 潛在 toocause 重新開機的 hello hello WMF 發行新版本的 VM。</span><span class="sxs-lookup"><span data-stu-id="c674e-165">Note this parameter has hello potential toocause reboots on hello VM when a new version of hello WMF is released.</span></span> 

## <a name="azure-portal-functionality"></a><span data-ttu-id="c674e-166">Azure 入口網站功能</span><span class="sxs-lookup"><span data-stu-id="c674e-166">Azure portal functionality</span></span>
<span data-ttu-id="c674e-167">瀏覽 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="c674e-167">Browse tooa VM.</span></span> <span data-ttu-id="c674e-168">在 [設定] -> [一般] 底下，按一下 [擴充功能]。</span><span class="sxs-lookup"><span data-stu-id="c674e-168">Under Settings -> General click "Extensions."</span></span> <span data-ttu-id="c674e-169">系統會建立新窗格。</span><span class="sxs-lookup"><span data-stu-id="c674e-169">A new pane is created.</span></span> <span data-ttu-id="c674e-170">按一下 [加入]，然後選取 [PowerShell DSC]。</span><span class="sxs-lookup"><span data-stu-id="c674e-170">Click "Add" and select PowerShell DSC.</span></span>

<span data-ttu-id="c674e-171">hello 入口網站需要輸入。</span><span class="sxs-lookup"><span data-stu-id="c674e-171">hello portal needs input.</span></span>
<span data-ttu-id="c674e-172">**組態模組或指令碼**︰這是必要欄位。</span><span class="sxs-lookup"><span data-stu-id="c674e-172">**Configuration Modules or Script**: This field is mandatory.</span></span> <span data-ttu-id="c674e-173">需要.ps1 檔案包含設定指令碼或 hello.zip 內的模組資料夾中的所有依存資源與 hello 根目錄.ps1 設定指令碼的.zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="c674e-173">Requires a .ps1 file containing a configuration script, or a .zip file with a .ps1 configuration script at hello root, and all dependent resources in module folders within hello .zip.</span></span> <span data-ttu-id="c674e-174">它可以建立以 hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` hello Azure PowerShell SDK 中包含的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c674e-174">It can be created with hello `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` cmdlet included in hello Azure PowerShell SDK.</span></span> <span data-ttu-id="c674e-175">hello.zip 檔案上傳到您使用者的 blob 儲存體受到 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="c674e-175">hello .zip file is uploaded into your user blob storage secured by a SAS token.</span></span> 

<span data-ttu-id="c674e-176">**組態資料 PSD1 檔案**︰這是選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="c674e-176">**Configuration Data PSD1 File**: This field is optional.</span></span> <span data-ttu-id="c674e-177">如果您的組態需要.psd1 的組態資料檔，請使用此欄位 tooselect 它並將它上傳 tooyour 使用者 blob 儲存體，所以保護由 SAS 權杖。</span><span class="sxs-lookup"><span data-stu-id="c674e-177">If your configuration requires a configuration data file in .psd1, use this field tooselect it and upload it tooyour user blob storage, where it is secured by a SAS token.</span></span> 

<span data-ttu-id="c674e-178">**組態的模組完整名稱**：.ps1 檔案可以有多個組態函數。</span><span class="sxs-lookup"><span data-stu-id="c674e-178">**Module-Qualified Name of Configuration**: .ps1 files can have multiple configuration functions.</span></span> <span data-ttu-id="c674e-179">輸入 hello hello 設定.ps1 指令碼後面接著名稱 '\'和 hello hello 設定函式名稱。</span><span class="sxs-lookup"><span data-stu-id="c674e-179">Enter hello name of hello configuration .ps1 script followed by a  '\' and hello name of hello configuration function.</span></span> <span data-ttu-id="c674e-180">例如，如果.ps1 指令碼有 hello 名稱"configuration.ps1"hello 組態是"IisInstall 」，您會輸入：`configuration.ps1\IisInstall`</span><span class="sxs-lookup"><span data-stu-id="c674e-180">For example, if your .ps1 script has hello name "configuration.ps1", and hello configuration is "IisInstall", you would enter: `configuration.ps1\IisInstall`</span></span>

<span data-ttu-id="c674e-181">**組態引數**: hello 的設定函式會採用引數，如果在這裡 hello 格式輸入它們`argumentName1=value1,argumentName2=value2`。</span><span class="sxs-lookup"><span data-stu-id="c674e-181">**Configuration Arguments**: If hello configuration function takes arguments, enter them in here in hello format `argumentName1=value1,argumentName2=value2`.</span></span> <span data-ttu-id="c674e-182">請注意，此格式與透過 PowerShell Cmdlet 或 Resource Manager 範本接受組態引數的方式所採用的格式不同。</span><span class="sxs-lookup"><span data-stu-id="c674e-182">Note this format is a different format than how configuration arguments are accepted through PowerShell cmdlets or Resource Manager templates.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c674e-183">開始使用</span><span class="sxs-lookup"><span data-stu-id="c674e-183">Getting started</span></span>
<span data-ttu-id="c674e-184">hello Azure DSC 延伸模組會在 DSC 設定文件，並制定這些 Azure Vm 上。</span><span class="sxs-lookup"><span data-stu-id="c674e-184">hello Azure DSC extension takes in DSC configuration documents and enacts them on Azure VMs.</span></span> <span data-ttu-id="c674e-185">以下是簡單的組態範例。</span><span class="sxs-lookup"><span data-stu-id="c674e-185">A simple example of a configuration follows.</span></span> <span data-ttu-id="c674e-186">以 "IisInstall.ps1" 的名稱將它儲存在本機：</span><span class="sxs-lookup"><span data-stu-id="c674e-186">Save it locally as "IisInstall.ps1":</span></span>

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

<span data-ttu-id="c674e-187">hello hello 遵循步驟進行 hello IisInstall.ps1 指令碼指定的 VM、 執行 hello 組態，並回報狀態。</span><span class="sxs-lookup"><span data-stu-id="c674e-187">hello following steps place hello IisInstall.ps1 script on hello specified VM, execute hello configuration, and report back on status.</span></span>
###<a name="classic-model"></a><span data-ttu-id="c674e-188">傳統模型</span><span class="sxs-lookup"><span data-stu-id="c674e-188">Classic model</span></span>
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a><span data-ttu-id="c674e-189">Azure Resource Manager 模型</span><span class="sxs-lookup"><span data-stu-id="c674e-189">Azure Resource Manager model</span></span>

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a><span data-ttu-id="c674e-190">記錄</span><span class="sxs-lookup"><span data-stu-id="c674e-190">Logging</span></span>
<span data-ttu-id="c674e-191">記錄檔位於︰</span><span class="sxs-lookup"><span data-stu-id="c674e-191">Logs are placed in:</span></span>

<span data-ttu-id="c674e-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[版本號碼]</span><span class="sxs-lookup"><span data-stu-id="c674e-192">C:\WindowsAzure\Logs\Plugins\Microsoft.Powershell.DSC\[Version Number]</span></span>

## <a name="next-steps"></a><span data-ttu-id="c674e-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c674e-193">Next steps</span></span>
<span data-ttu-id="c674e-194">如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="c674e-194">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="c674e-195">檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c674e-195">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="c674e-196">toofind 額外的功能，您可以使用 PowerShell DSC[瀏覽 hello PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0)的多個 DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="c674e-196">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

<span data-ttu-id="c674e-197">如需將敏感性參數傳遞至設定的詳細資訊，請參閱[管理認證安全地與 hello DSC 延伸模組處理常式](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c674e-197">For details on passing sensitive parameters into configurations, see [Manage credentials securely with hello DSC extension handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

