---
title: "Azure Stack 虛擬機器簡介"
description: "了解 Azure Stack 虛擬機器"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: 68da653052d0e3dfd66d6b65958046e42cefce73
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-azure-stack-virtual-machines"></a><span data-ttu-id="df25a-103">Azure Stack 虛擬機器簡介</span><span class="sxs-lookup"><span data-stu-id="df25a-103">Introduction to Azure Stack virtual machines</span></span>

<span data-ttu-id="df25a-104">適用於：Azure Stack 整合系統和 Azure Stack 開發套件</span><span class="sxs-lookup"><span data-stu-id="df25a-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

## <a name="overview"></a><span data-ttu-id="df25a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="df25a-105">Overview</span></span>
<span data-ttu-id="df25a-106">Azure Stack 虛擬機器 (VM) 是 Azure Stack 提供的一種依需求、可調整的計算資源。</span><span class="sxs-lookup"><span data-stu-id="df25a-106">An Azure Stack Virtual Machine (VM) is one type of on-demand, scalable computing resource that Azure Stack offers.</span></span> <span data-ttu-id="df25a-107">一般而言，當您對於運算環境所需的控制權比其他選擇可提供的還要多時，則您會選擇 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-107">Typically, you choose a VM when you need more control over the computing environment than the other choices offer.</span></span> <span data-ttu-id="df25a-108">本文提供您在建立 VM 之前應該的事項、建立方式及管理方式的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="df25a-108">This article gives you information about what you should consider before you create a VM, how you create it, and how you manage it.</span></span>

<span data-ttu-id="df25a-109">Azure Stack VM 供虛擬化的彈性，您不需要管理個別的叢集或機器。</span><span class="sxs-lookup"><span data-stu-id="df25a-109">An Azure Stack VM gives you the flexibility of virtualization without the need to manage individual clusters or machines.</span></span> <span data-ttu-id="df25a-110">不過，您仍然需要執行工作來維護 VM，例如設定、修補和安裝在 VM 上執行的軟體。</span><span class="sxs-lookup"><span data-stu-id="df25a-110">However, you still need to maintain the VM by performing tasks, such as configuring, patching, and installing the software that runs on it.</span></span>

<span data-ttu-id="df25a-111">Azure Stack 虛擬機器有各種用途。</span><span class="sxs-lookup"><span data-stu-id="df25a-111">Azure Stack virtual machines can be used in various ways.</span></span> <span data-ttu-id="df25a-112">例如：</span><span class="sxs-lookup"><span data-stu-id="df25a-112">For example:</span></span>

* <span data-ttu-id="df25a-113">**開發和測試** – Azure Stack VM 提供快速又簡單的方法來建立電腦，讓電腦具備撰寫和測試應用程式所需的特定設定。</span><span class="sxs-lookup"><span data-stu-id="df25a-113">**Development and test** – Azure Stack VMs offer a quick and easy way to create a computer with a specific configuration required to code and test an application.</span></span>

* <span data-ttu-id="df25a-114">**雲端中的應用程式** – 因為對於應用程式的需求會變動，在 Azure Stack 中的 VM 上執行應用程式會較具經濟效益。</span><span class="sxs-lookup"><span data-stu-id="df25a-114">**Applications in the cloud** – Because demand for your application can fluctuate, it might make economic sense to run it on a VM in Azure Stack.</span></span> <span data-ttu-id="df25a-115">當您需要 VM 時便支付額外的 VM，而當您不需要時便關閉這些 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-115">You pay for extra VMs when you need them and shut them down when you don’t.</span></span>

* <span data-ttu-id="df25a-116">**擴充的資料中心** – Azure Stack 虛擬網路中的虛擬機器很容易連線至組織的網路或 Azure。</span><span class="sxs-lookup"><span data-stu-id="df25a-116">**Extended datacenter** – Virtual machines in an Azure Stack virtual network can easily be connected to your organization’s network or Azure.</span></span>

<span data-ttu-id="df25a-117">您的應用程式所使用的 VM 數目可以相應增加及相應放大為符合您需求的任何內容。</span><span class="sxs-lookup"><span data-stu-id="df25a-117">The number of VMs that your application uses can scale up and out to whatever is required to meet your needs.</span></span>

## <a name="what-do-i-need-to-think-about-before-creating-a-vm"></a><span data-ttu-id="df25a-118">我在建立 VM 之前需要先考慮什麼？</span><span class="sxs-lookup"><span data-stu-id="df25a-118">What do I need to think about before creating a VM?</span></span>

<span data-ttu-id="df25a-119">當您在 Azure Stack 中建置應用程式基礎結構時，一定會面臨許多設計考量。</span><span class="sxs-lookup"><span data-stu-id="df25a-119">There are always a multitude of design considerations when you build out an application infrastructure in Azure Stack.</span></span> <span data-ttu-id="df25a-120">在您開始之前，仔細考量 VM 的這些層面很重要︰</span><span class="sxs-lookup"><span data-stu-id="df25a-120">These aspects of a VM are important to think about before you start:</span></span>

- <span data-ttu-id="df25a-121">應用程式資源的名稱</span><span class="sxs-lookup"><span data-stu-id="df25a-121">The names of your application resources</span></span>
- <span data-ttu-id="df25a-122">VM 的大小</span><span class="sxs-lookup"><span data-stu-id="df25a-122">The size of the VM</span></span>
- <span data-ttu-id="df25a-123">可建立的 VM 數目上限</span><span class="sxs-lookup"><span data-stu-id="df25a-123">The maximum number of VMs that can be created</span></span>
- <span data-ttu-id="df25a-124">VM 上執行的作業系統</span><span class="sxs-lookup"><span data-stu-id="df25a-124">The operating system that the VM runs</span></span>
- <span data-ttu-id="df25a-125">VM 啟動後的設定</span><span class="sxs-lookup"><span data-stu-id="df25a-125">The configuration of the VM after it starts</span></span> 
- <span data-ttu-id="df25a-126">VM 需要的相關資源</span><span class="sxs-lookup"><span data-stu-id="df25a-126">The related resources that the VM needs</span></span>

### <a name="naming"></a><span data-ttu-id="df25a-127">命名</span><span class="sxs-lookup"><span data-stu-id="df25a-127">Naming</span></span>

<span data-ttu-id="df25a-128">虛擬機器會被指派名稱，也具有作業系統中所設定的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="df25a-128">A virtual machine has a name assigned to it and it has a computer name configured as part of the operating system.</span></span> <span data-ttu-id="df25a-129">VM 的名稱最多可為 15 個字元。</span><span class="sxs-lookup"><span data-stu-id="df25a-129">The name of a VM can be up to 15 characters.</span></span>

<span data-ttu-id="df25a-130">如果您使用 Azure Stack 來建立作業系統磁碟，則電腦名稱和虛擬機器名稱相同。</span><span class="sxs-lookup"><span data-stu-id="df25a-130">If you use Azure Stack to create the operating system disk, the computer name and the virtual machine name are the same.</span></span> <span data-ttu-id="df25a-131">如果您上傳並使用您自己的映像 (該映像包含先前所設定的作業系統)，並用它來建立虛擬機器，則名稱可能會不同。</span><span class="sxs-lookup"><span data-stu-id="df25a-131">If you upload and use your own image that contains a previously configured operating system and use it to create a virtual machine, the names may be different.</span></span> <span data-ttu-id="df25a-132">當您上傳自己的映像檔時，作業系統中的電腦名稱和虛擬機器名稱最好相同。</span><span class="sxs-lookup"><span data-stu-id="df25a-132">When you upload your own image file, make the computer name in the operating system and the virtual machine name the same as a best practice.</span></span>

### <a name="vm-size"></a><span data-ttu-id="df25a-133">VM 大小</span><span class="sxs-lookup"><span data-stu-id="df25a-133">VM size</span></span>

<span data-ttu-id="df25a-134">您使用的 VM 大小取決於您要執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="df25a-134">The size of the VM that you use is determined by the workload that you want to run.</span></span> <span data-ttu-id="df25a-135">您所選的大小會決定例如處理電源、記憶體和儲存體容量等因素。</span><span class="sxs-lookup"><span data-stu-id="df25a-135">The size that you choose then determines factors such as processing power, memory, and storage capacity.</span></span> <span data-ttu-id="df25a-136">Azure Stack 提供各種不同的大小來支援許多用途。</span><span class="sxs-lookup"><span data-stu-id="df25a-136">Azure Stack offers a wide variety of sizes to support many types of uses.</span></span>

### <a name="vm-limits"></a><span data-ttu-id="df25a-137">VM 限制</span><span class="sxs-lookup"><span data-stu-id="df25a-137">VM limits</span></span>

<span data-ttu-id="df25a-138">訂用帳戶設有預設配額限制，可能會影響如何部署專案的許多 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-138">Your subscription has default quota limits in place that can impact the deployment of many VMs for your project.</span></span> <span data-ttu-id="df25a-139">每一訂用帳戶目前的限制是每一區域 20 個 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-139">The current limit on a per subscription basis is 20 VMs per region.</span></span>

### <a name="operating-system-disks-and-images"></a><span data-ttu-id="df25a-140">作業系統磁碟和映像</span><span class="sxs-lookup"><span data-stu-id="df25a-140">Operating system disks and images</span></span>

<span data-ttu-id="df25a-141">虛擬機器是使用虛擬硬碟 (VHD) 來儲存其作業系統 (OS) 和資料。</span><span class="sxs-lookup"><span data-stu-id="df25a-141">Virtual machines use virtual hard disks (VHDs) to store their operating system (OS) and data.</span></span> <span data-ttu-id="df25a-142">VHD 也能夠使用於您可以選擇用來安裝 OS 的映像。</span><span class="sxs-lookup"><span data-stu-id="df25a-142">VHDs are also used for the images you can choose from to install an OS.</span></span>
<span data-ttu-id="df25a-143">Azure Stack 提供一個市集，適用於各種版本和類型的作業系統。</span><span class="sxs-lookup"><span data-stu-id="df25a-143">Azure Stack provides a marketplace to use with various versions and types of operating systems.</span></span> <span data-ttu-id="df25a-144">Marketplace 映像是依映像發行者、優惠、SKU 和版本 (版本通常會指定為最新版本) 來識別。</span><span class="sxs-lookup"><span data-stu-id="df25a-144">Marketplace images are identified by image publisher, offer, sku, and version (typically version is specified as latest).</span></span>

<span data-ttu-id="df25a-145">下表顯示一些方法讓您找到映像的資訊：</span><span class="sxs-lookup"><span data-stu-id="df25a-145">The following table shows some ways that you can find the information for an image:</span></span>


|<span data-ttu-id="df25a-146">方法</span><span class="sxs-lookup"><span data-stu-id="df25a-146">Method</span></span>|<span data-ttu-id="df25a-147">說明</span><span class="sxs-lookup"><span data-stu-id="df25a-147">Description</span></span>|
|---------|---------|
|<span data-ttu-id="df25a-148">Azure Stack 入口網站</span><span class="sxs-lookup"><span data-stu-id="df25a-148">Azure Stack portal</span></span>|<span data-ttu-id="df25a-149">當您選取要使用的影像時，會自動為您指定值。</span><span class="sxs-lookup"><span data-stu-id="df25a-149">The values are automatically specified for you when you select an image to use.</span></span>|
|<span data-ttu-id="df25a-150">Azure Stack PowerShell</span><span class="sxs-lookup"><span data-stu-id="df25a-150">Azure Stack PowerShell</span></span>|`Get-AzureRMVMImagePublisher -Location "location"`<br>`Get-AzureRMVMImageOffer -Location "location" -Publisher "publisherName"`<br>`Get-AzureRMVMImageSku -Location "location" -Publisher "publisherName" -Offer "offerName"`|
|<span data-ttu-id="df25a-151">REST API</span><span class="sxs-lookup"><span data-stu-id="df25a-151">REST APIs</span></span>     |[<span data-ttu-id="df25a-152">列出映像發行者</span><span class="sxs-lookup"><span data-stu-id="df25a-152">List image publishers</span></span>](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<br>[<span data-ttu-id="df25a-153">列出映像優惠</span><span class="sxs-lookup"><span data-stu-id="df25a-153">List image offers</span></span>](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<br>[<span data-ttu-id="df25a-154">列出映像 SKU</span><span class="sxs-lookup"><span data-stu-id="df25a-154">List image SKUs</span></span>](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus)|

<span data-ttu-id="df25a-155">您可以選擇上傳並使用自己的映像。</span><span class="sxs-lookup"><span data-stu-id="df25a-155">You can choose to upload and use your own image.</span></span> <span data-ttu-id="df25a-156">如果這樣做，則不會使用發行者名稱、供應項目和 SKU。</span><span class="sxs-lookup"><span data-stu-id="df25a-156">If you do, the publisher name, offer, and sku aren’t used.</span></span>

### <a name="extensions"></a><span data-ttu-id="df25a-157">擴充功能</span><span class="sxs-lookup"><span data-stu-id="df25a-157">Extensions</span></span>

<span data-ttu-id="df25a-158">VM 擴充可透過部署後設定及自動化工作，讓您的 VM 有更多功能。</span><span class="sxs-lookup"><span data-stu-id="df25a-158">VM extensions give your VM additional capabilities through post deployment configuration and automated tasks.</span></span>
<span data-ttu-id="df25a-159">可以使用擴充功能來完成這些常見工作︰</span><span class="sxs-lookup"><span data-stu-id="df25a-159">These common tasks can be accomplished using extensions:</span></span>

* <span data-ttu-id="df25a-160">執行自訂指令碼 –「自訂指令碼擴充」可在佈建 VM 時執行您的指令碼，以協助您在 VM 上設定工作負載。</span><span class="sxs-lookup"><span data-stu-id="df25a-160">Run custom scripts – The Custom Script Extension helps you configure workloads on the VM by running your script when the VM is provisioned.</span></span>
* <span data-ttu-id="df25a-161">部署和管理設定 –「PowerShell 期望狀態設定 (DSC) 擴充」可協助您在 VM 上設定 DSC 來管理設定和環境。</span><span class="sxs-lookup"><span data-stu-id="df25a-161">Deploy and manage configurations – The PowerShell Desired State Configuration (DSC) Extension helps you set up DSC on a VM to manage configurations and environments.</span></span>
* <span data-ttu-id="df25a-162">收集診斷資料 –「Azure 診斷擴充」可協助您設定 VM 來收集診斷資料，用來監視應用程式的健康情況。</span><span class="sxs-lookup"><span data-stu-id="df25a-162">Collect diagnostics data – The Azure Diagnostics Extension helps you configure the VM to collect diagnostics data that can be used to monitor the health of your application.</span></span>

### <a name="related-resources"></a><span data-ttu-id="df25a-163">相關資源</span><span class="sxs-lookup"><span data-stu-id="df25a-163">Related resources</span></span>

<span data-ttu-id="df25a-164">下表中的資源由 VM 使用，在建立 VM 時必須存在或已建立。</span><span class="sxs-lookup"><span data-stu-id="df25a-164">The resources in the following table are used by the VM and need to exist or be created when the VM is created.</span></span>


|<span data-ttu-id="df25a-165">資源</span><span class="sxs-lookup"><span data-stu-id="df25a-165">Resource</span></span>|<span data-ttu-id="df25a-166">必要</span><span class="sxs-lookup"><span data-stu-id="df25a-166">Required</span></span>|<span data-ttu-id="df25a-167">說明</span><span class="sxs-lookup"><span data-stu-id="df25a-167">Description</span></span>|
|---------|---------|---------|
|<span data-ttu-id="df25a-168">資源群組</span><span class="sxs-lookup"><span data-stu-id="df25a-168">Resource group</span></span>|<span data-ttu-id="df25a-169">是</span><span class="sxs-lookup"><span data-stu-id="df25a-169">Yes</span></span>|<span data-ttu-id="df25a-170">VM 必須包含在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="df25a-170">The VM must be contained in a resource group.</span></span>|
|<span data-ttu-id="df25a-171">儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="df25a-171">Storage account</span></span>|<span data-ttu-id="df25a-172">是</span><span class="sxs-lookup"><span data-stu-id="df25a-172">Yes</span></span>|<span data-ttu-id="df25a-173">VM 需要儲存體帳戶儲存其虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="df25a-173">The VM needs the storage account to store its virtual hard disks.</span></span>|
|<span data-ttu-id="df25a-174">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="df25a-174">Virtual network</span></span>|<span data-ttu-id="df25a-175">是</span><span class="sxs-lookup"><span data-stu-id="df25a-175">Yes</span></span>|<span data-ttu-id="df25a-176">VM 必須是虛擬網路的成員。</span><span class="sxs-lookup"><span data-stu-id="df25a-176">The VM must be a member of a virtual network.</span></span>|
|<span data-ttu-id="df25a-177">公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="df25a-177">Public IP address</span></span>|<span data-ttu-id="df25a-178">否</span><span class="sxs-lookup"><span data-stu-id="df25a-178">No</span></span>|<span data-ttu-id="df25a-179">可以有公用 IP 位址指派給 VM，以從遠端存取它。</span><span class="sxs-lookup"><span data-stu-id="df25a-179">The VM can have a public IP address assigned to it to remotely access it.</span></span>|
|<span data-ttu-id="df25a-180">網路介面</span><span class="sxs-lookup"><span data-stu-id="df25a-180">Network interface</span></span>|<span data-ttu-id="df25a-181">是</span><span class="sxs-lookup"><span data-stu-id="df25a-181">Yes</span></span>|<span data-ttu-id="df25a-182">VM 需要網路介面以在網路中進行通訊。</span><span class="sxs-lookup"><span data-stu-id="df25a-182">The VM needs the network interface to communicate in the network.</span></span>|
|<span data-ttu-id="df25a-183">資料磁碟</span><span class="sxs-lookup"><span data-stu-id="df25a-183">Data disks</span></span>|<span data-ttu-id="df25a-184">否</span><span class="sxs-lookup"><span data-stu-id="df25a-184">No</span></span>|<span data-ttu-id="df25a-185">VM 可以包含資料磁碟來擴充儲存體功能。</span><span class="sxs-lookup"><span data-stu-id="df25a-185">The VM can include data disks to expand storage capabilities.</span></span>|

## <a name="how-do-i-create-my-first-vm"></a><span data-ttu-id="df25a-186">如何建立第一個 VM？</span><span class="sxs-lookup"><span data-stu-id="df25a-186">How do I create my first VM?</span></span>

<span data-ttu-id="df25a-187">建立 VM 有多種選擇。</span><span class="sxs-lookup"><span data-stu-id="df25a-187">You have several choices to create a VM.</span></span> <span data-ttu-id="df25a-188">您的選擇取決於您的環境。</span><span class="sxs-lookup"><span data-stu-id="df25a-188">Your choice depends on your environment.</span></span>
<span data-ttu-id="df25a-189">下表提供資訊來協助您開始建立 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-189">The following table provides information to get you started creating your VM.</span></span>


|<span data-ttu-id="df25a-190">方法</span><span class="sxs-lookup"><span data-stu-id="df25a-190">Method</span></span>|<span data-ttu-id="df25a-191">文章</span><span class="sxs-lookup"><span data-stu-id="df25a-191">Article</span></span>|
|---------|---------|
|<span data-ttu-id="df25a-192">Azure Stack 入口網站</span><span class="sxs-lookup"><span data-stu-id="df25a-192">Azure Stack portal</span></span>|<span data-ttu-id="df25a-193">使用 Azure Stack 入口網站建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-193">Create a Windows virtual machine with the Azure Stack portal</span></span><br>[<span data-ttu-id="df25a-194">使用 Azure Stack 入口網站建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-194">Create a Linux virtual machine using the Azure Stack portal</span></span>](azure-stack-quick-linux-portal.md)|
|<span data-ttu-id="df25a-195">範本</span><span class="sxs-lookup"><span data-stu-id="df25a-195">Templates</span></span>|<span data-ttu-id="df25a-196">Azure Stack 快速入門範本位於：</span><span class="sxs-lookup"><span data-stu-id="df25a-196">Azure Stack Quickstart templates are located at:</span></span><br> [<span data-ttu-id="df25a-197">https://github.com/Azure/AzureStack-QuickStart-Templates</span><span class="sxs-lookup"><span data-stu-id="df25a-197">https://github.com/Azure/AzureStack-QuickStart-Templates</span></span>](https://github.com/Azure/AzureStack-QuickStart-Templates)|
|<span data-ttu-id="df25a-198">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df25a-198">PowerShell</span></span>|[<span data-ttu-id="df25a-199">在 Azure Stack 中使用 PowerShell 建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-199">Create a Windows virtual machine by using PowerShell in Azure Stack</span></span>](azure-stack-quick-create-vm-windows-powershell.md)<br>[<span data-ttu-id="df25a-200">在 Azure Stack 中使用 PowerShell 建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-200">Create a Linux virtual machine by using PowerShell in Azure Stack</span></span>](azure-stack-quick-create-vm-linux-powershell.md)|
|<span data-ttu-id="df25a-201">CLI</span><span class="sxs-lookup"><span data-stu-id="df25a-201">CLI</span></span>|[<span data-ttu-id="df25a-202">在 Azure Stack 中使用 CLI 建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-202">Create a Windows virtual machine by using CLI in Azure Stack</span></span>](azure-stack-quick-create-vm-windows-cli.md)<br>[<span data-ttu-id="df25a-203">在 Azure Stack 中使用 CLI 建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="df25a-203">Create a Linux virtual machine by using CLI in Azure Stack</span></span>](azure-stack-quick-create-vm-linux-cli.md)|

## <a name="how-do-i-manage-the-vm-that-i-created"></a><span data-ttu-id="df25a-204">如何管理我所建立的 VM？</span><span class="sxs-lookup"><span data-stu-id="df25a-204">How do I manage the VM that I created?</span></span>

<span data-ttu-id="df25a-205">可以使用以瀏覽器為基礎的入口網站、支援指令碼處理的命令列工具，或直接透過 API 管理 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-205">VMs can be managed using a browser-based portal, command-line tools with support for scripting, or directly through APIs.</span></span> <span data-ttu-id="df25a-206">您可能會執行的一些一般管理工作為取得 VM 的相關資訊、登入 VM、管理可用性，以及進行備份。</span><span class="sxs-lookup"><span data-stu-id="df25a-206">Some typical management tasks that you might perform are getting information about a VM, logging on to a VM, managing availability, and making backups.</span></span>

### <a name="get-information-about-a-vm"></a><span data-ttu-id="df25a-207">取得 VM 的相關資訊</span><span class="sxs-lookup"><span data-stu-id="df25a-207">Get information about a VM</span></span>

<span data-ttu-id="df25a-208">下表顯示一些方法讓您取得 VM 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="df25a-208">The following table shows you some of the ways you can get information about a VM.</span></span>


|<span data-ttu-id="df25a-209">方法</span><span class="sxs-lookup"><span data-stu-id="df25a-209">Method</span></span>|<span data-ttu-id="df25a-210">說明</span><span class="sxs-lookup"><span data-stu-id="df25a-210">Description</span></span>|
|---------|---------|
|<span data-ttu-id="df25a-211">Azure Stack 入口網站</span><span class="sxs-lookup"><span data-stu-id="df25a-211">Azure Stack portal</span></span>|<span data-ttu-id="df25a-212">在 [中樞] 功能表中，按一下 [虛擬機器]，然後從清單中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-212">On the hub menu, click Virtual Machines and then select the VM from the list.</span></span> <span data-ttu-id="df25a-213">在 VM 的頁面上，您可以存取概觀資訊、設定值及監視計量。</span><span class="sxs-lookup"><span data-stu-id="df25a-213">On the page for the VM, you have access to overview information, setting values, and monitoring metrics.</span></span>|
|<span data-ttu-id="df25a-214">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df25a-214">Azure PowerShell</span></span>|<span data-ttu-id="df25a-215">在 Azure 和 Azure Stack 中，管理 VM 的方法很相似。</span><span class="sxs-lookup"><span data-stu-id="df25a-215">Managing VMs is similar in Azure and Azure Stack.</span></span> <span data-ttu-id="df25a-216">如需有關使用 PowerShell 的詳細資訊，請參閱下列 Azure 主題：</span><span class="sxs-lookup"><span data-stu-id="df25a-216">For more information about using PowerShell, see the following Azure topic:</span></span><br>[<span data-ttu-id="df25a-217">使用 Azure PowerShell 模組建立和管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="df25a-217">Create and Manage Windows VMs with the Azure PowerShell module</span></span>](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/tutorial-manage-vm#understand-vm-sizes)|
|<span data-ttu-id="df25a-218">用戶端 SDK</span><span class="sxs-lookup"><span data-stu-id="df25a-218">Client SDKs</span></span>|<span data-ttu-id="df25a-219">在 Azure 和 Azure Stack 中，使用 C# 來管理 VM 的方法很相似。</span><span class="sxs-lookup"><span data-stu-id="df25a-219">Using C# to manage VMs is similar in Azure and Azure Stack.</span></span> <span data-ttu-id="df25a-220">如需詳細資訊，請參閱下列 Azure 主題：</span><span class="sxs-lookup"><span data-stu-id="df25a-220">For more information, see the following Azure topic:</span></span><br>[<span data-ttu-id="df25a-221">在 Azure 中使用 C# 建立和管理 Windows VM</span><span class="sxs-lookup"><span data-stu-id="df25a-221">Create and manage Windows VMs in Azure using C#</span></span>](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/csharp)|

### <a name="connect-to-the-vm"></a><span data-ttu-id="df25a-222">連接至 VM</span><span class="sxs-lookup"><span data-stu-id="df25a-222">Connect to the VM</span></span>

<span data-ttu-id="df25a-223">在 Azure Stack 入口網站中，您可以使用 [連線] 按鈕來連線至 VM。</span><span class="sxs-lookup"><span data-stu-id="df25a-223">You can use the **Connect** button in the Azure Stack portal to connect to your VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df25a-224">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df25a-224">Next steps</span></span>
* [<span data-ttu-id="df25a-225">Azure Stack 中虛擬機器的考量</span><span class="sxs-lookup"><span data-stu-id="df25a-225">Considerations for Virtual Machines in Azure Stack</span></span>](azure-stack-vm-considerations.md)

