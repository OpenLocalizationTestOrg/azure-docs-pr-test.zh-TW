---
title: "建立 Azure Marketplace 的虛擬機器映像 | Microsoft Docs"
description: "如何建立 Azure Marketplace 的虛擬機器映像以讓其他人購買的詳細指示。"
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 046ce7af40301014746c6aef07d08d81ab4adcc2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="0beec-103">建立 Azure Marketplace 的虛擬機器映像的指南</span><span class="sxs-lookup"><span data-stu-id="0beec-103">Guide to create a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="0beec-104">本文的 **步驟 2**會逐步引導您準備您將部署到 Azure Marketplace 的虛擬硬碟 (VHD)。</span><span class="sxs-lookup"><span data-stu-id="0beec-104">This article, **Step 2**, walks you through preparing the virtual hard disks (VHDs) that you will deploy to the Azure Marketplace.</span></span> <span data-ttu-id="0beec-105">您的 VHD 是 SKU 的基礎。</span><span class="sxs-lookup"><span data-stu-id="0beec-105">Your VHDs are the foundation of your SKU.</span></span> <span data-ttu-id="0beec-106">這個程序會因為您是否提供以 Linux 或 Windows 為基礎的 SKU 而有所不同。</span><span class="sxs-lookup"><span data-stu-id="0beec-106">The process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="0beec-107">本文將探討這兩種狀況。</span><span class="sxs-lookup"><span data-stu-id="0beec-107">This article covers both scenarios.</span></span> <span data-ttu-id="0beec-108">這個程序可與[帳戶建立和註冊][link-acct-creation]同步執行。</span><span class="sxs-lookup"><span data-stu-id="0beec-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="0beec-109">1.定義供應項目和 SKU</span><span class="sxs-lookup"><span data-stu-id="0beec-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="0beec-110">在本節中，您會了解如何定義供應項目與其相關聯的 SKU。</span><span class="sxs-lookup"><span data-stu-id="0beec-110">In this section, you learn to define the offers and their associated SKUs.</span></span>

<span data-ttu-id="0beec-111">供應項目是其所有 SKU 的「上層」。</span><span class="sxs-lookup"><span data-stu-id="0beec-111">An offer is a "parent" to all of its SKUs.</span></span> <span data-ttu-id="0beec-112">您可以擁有多個供應項目。</span><span class="sxs-lookup"><span data-stu-id="0beec-112">You can have multiple offers.</span></span> <span data-ttu-id="0beec-113">您可以隨意決定供應項目的建構方式。</span><span class="sxs-lookup"><span data-stu-id="0beec-113">How you decide to structure your offers is up to you.</span></span> <span data-ttu-id="0beec-114">當供應項目進入預備環境，它的所有 SKU 也會一起進入。</span><span class="sxs-lookup"><span data-stu-id="0beec-114">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="0beec-115">細心考量您的 SKU 識別碼，因為這些識別碼會顯示於 URL 中：</span><span class="sxs-lookup"><span data-stu-id="0beec-115">Carefully consider your SKU identifiers, because they will be visible in the URL:</span></span>

* <span data-ttu-id="0beec-116">Azure.com：http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="0beec-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="0beec-117">Azure Preview 入口網站︰https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="0beec-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="0beec-118">SKU 是 VM 映像的商務名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-118">A SKU is the commercial name for a VM image.</span></span> <span data-ttu-id="0beec-119">VM 映像包含一個作業系統磁碟以及零或多個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0beec-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="0beec-120">它在本質上是虛擬機器的完整儲存體設定檔。</span><span class="sxs-lookup"><span data-stu-id="0beec-120">It is essentially the complete storage profile for a virtual machine.</span></span> <span data-ttu-id="0beec-121">每個磁碟都需要一個 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-121">One VHD is needed per disk.</span></span> <span data-ttu-id="0beec-122">即使空的資料磁碟也需要建立一個 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-122">Even blank data disks require a VHD to be created.</span></span>

<span data-ttu-id="0beec-123">無論您使用哪一種作業系統，您只能加入 SKU 所需的最少數目資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0beec-123">Regardless of which operating system you use, add only the minimum number of data disks needed by the SKU.</span></span> <span data-ttu-id="0beec-124">客戶無法在部署時移除屬於映像一部分的磁碟，但是可隨時在必要時於部署期間或之後加入磁碟。</span><span class="sxs-lookup"><span data-stu-id="0beec-124">Customers cannot remove disks that are part of an image at the time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0beec-125">**請勿變更新映像版本中的磁碟計數。**</span><span class="sxs-lookup"><span data-stu-id="0beec-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="0beec-126">如果您必須重新設定映像中的資料磁碟，請定義新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="0beec-126">If you must reconfigure Data disks in the image, define a new SKU.</span></span> <span data-ttu-id="0beec-127">對於自動調整大小、透過 ARM 範本自動部署解決方案和其他案例來說，發行磁碟計數相異的新映像版本有可能會毀損以新映像版本為基礎的新部署。</span><span class="sxs-lookup"><span data-stu-id="0beec-127">Publishing a new image version with different disk counts will have the potential of breaking new deployment based on the new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="0beec-128">1.1 加入供應項目</span><span class="sxs-lookup"><span data-stu-id="0beec-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="0beec-129">使用您的賣方帳戶登入[發佈入口網站][link-pubportal]。</span><span class="sxs-lookup"><span data-stu-id="0beec-129">Sign in to the [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="0beec-130">選取發佈入口網站的 [虛擬機器]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0beec-130">Select the **Virtual Machines** tab of the Publishing Portal.</span></span> <span data-ttu-id="0beec-131">在提示的輸入欄位中輸入您的供應項目名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-131">In the prompted entry field, enter your offer name.</span></span> <span data-ttu-id="0beec-132">供應項目名稱通常是您計劃在 Azure Marketplace 中銷售的產品或服務的名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-132">The offer name is typically the name of the product or service that you plan to sell in the Azure Marketplace.</span></span>
3. <span data-ttu-id="0beec-133">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="0beec-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="0beec-134">1.2 定義 SKU</span><span class="sxs-lookup"><span data-stu-id="0beec-134">1.2 Define a SKU</span></span>
<span data-ttu-id="0beec-135">在您加入供應項目之後，您必須定義及識別您的 SKU。</span><span class="sxs-lookup"><span data-stu-id="0beec-135">After you have added an offer, you need to define and identify your SKUs.</span></span> <span data-ttu-id="0beec-136">您可以有多個供應項目，每個供應項目在其下可以有多個 SKU。</span><span class="sxs-lookup"><span data-stu-id="0beec-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="0beec-137">當供應項目進入預備環境，它的所有 SKU 也會一起進入。</span><span class="sxs-lookup"><span data-stu-id="0beec-137">When an offer is pushed to staging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="0beec-138">**加入 SKU。**</span><span class="sxs-lookup"><span data-stu-id="0beec-138">**Add a SKU.**</span></span> <span data-ttu-id="0beec-139">SKU 必須具備用於 URL 中的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-139">The SKU requires an identifier, which is used in the URL.</span></span> <span data-ttu-id="0beec-140">此識別碼必須是發行設定檔中的唯一識別碼，但是若與其他發行者發生識別碼衝突，並不會有任何風險。</span><span class="sxs-lookup"><span data-stu-id="0beec-140">The identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0beec-141">供應項目和 SKU 識別項會顯示在 Marketplace 中的供應項目 URL。</span><span class="sxs-lookup"><span data-stu-id="0beec-141">The offer and SKU identifiers are displayed in the offer URL in the Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="0beec-142">**為 SKU 加入摘要描述。**</span><span class="sxs-lookup"><span data-stu-id="0beec-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="0beec-143">客戶可以看見摘要說明，所以您應讓說明可容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="0beec-143">Summary descriptions are visible to customers, so you should make them easily readable.</span></span> <span data-ttu-id="0beec-144">此資訊在「進入預備環境」階段之前都不需要鎖定。</span><span class="sxs-lookup"><span data-stu-id="0beec-144">This information does not need to be locked until the "Push to Staging" phase.</span></span> <span data-ttu-id="0beec-145">在那之前，您都可以任意編輯。</span><span class="sxs-lookup"><span data-stu-id="0beec-145">Until then, you are free to edit it.</span></span>
3. <span data-ttu-id="0beec-146">如果您正在使用以 Windows 為基礎的 SKU，請遵循建議的連結，要求使用核准的 Windows Server 版本。</span><span class="sxs-lookup"><span data-stu-id="0beec-146">If you are using Windows-based SKUs, follow the suggested links to acquire the approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="0beec-147">2.建立與 Azure 相容的 VHD (以 Linux 為基礎)</span><span class="sxs-lookup"><span data-stu-id="0beec-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="0beec-148">本節的焦點在於為 Azure Marketplace 建立以 Linux 為基礎的 VM 映像所採行的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0beec-148">This section focuses on best practices for creating a Linux-based VM image for the Azure Marketplace.</span></span> <span data-ttu-id="0beec-149">若需逐步解說，請參考下列文件：[建立與上傳包含 Linux 作業系統的虛擬硬碟](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0beec-149">For a step-by-step walkthrough, refer to the following documentation: [Creating and Uploading a Virtual Hard Disk that Contains the Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="0beec-150">3.建立與 Azure 相容的 VHD (以 Windows 為基礎)</span><span class="sxs-lookup"><span data-stu-id="0beec-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="0beec-151">本節的焦點在於為 Azure Marketplace 建立以 Windows Server 為基礎的 SKU 所採行的步驟。</span><span class="sxs-lookup"><span data-stu-id="0beec-151">This section focuses on the steps to create a SKU based on Windows Server for the Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-the-correct-base-vhds"></a><span data-ttu-id="0beec-152">3.1 確認您使用的是正確的基底 VHD</span><span class="sxs-lookup"><span data-stu-id="0beec-152">3.1 Ensure that you are using the correct base VHDs</span></span>
<span data-ttu-id="0beec-153">VM 映像的作業系統 VHD 必須以獲得 Azure 核准的基底映像為基礎，包含 Windows Server 或 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="0beec-153">The operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="0beec-154">若要開始，請從下列其中一個映像建立 VM，位於 [Microsoft Azure 入口網站][link-azure-portal]：</span><span class="sxs-lookup"><span data-stu-id="0beec-154">To begin, create a VM from one of the following images, located at the [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="0beec-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2]、[2012 Datacenter][link-datactr-2012]、[2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="0beec-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="0beec-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent]、[Standard][link-sql-2014-std]、[Web][link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="0beec-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="0beec-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent]、[Standard][link-sql-2012-std]、[Web][link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="0beec-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="0beec-158">這些連結也可以在 SKU 頁面下的發佈入口網站中找到。</span><span class="sxs-lookup"><span data-stu-id="0beec-158">These links can also be found in the Publishing Portal under the SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="0beec-159">如果您使用的是最新的 Azure 入口網站或 PowerShell，2014 年 9 月 8 日之後發行的 Windows Server 映像都會獲得核准。</span><span class="sxs-lookup"><span data-stu-id="0beec-159">If you are using the current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="0beec-160">3.2 建立您的 Windows 型 VM</span><span class="sxs-lookup"><span data-stu-id="0beec-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="0beec-161">從 Microsoft Azure 入口網站，您可以利用幾個簡單的步驟，根據核准的基底映像建立您的 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-161">From the Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="0beec-162">下列內容是程序概觀：</span><span class="sxs-lookup"><span data-stu-id="0beec-162">The following is an overview of the process:</span></span>

1. <span data-ttu-id="0beec-163">從基底映像頁面，選取 [建立虛擬機器] 以導向新的 [Microsoft Azure 入口網站][link-azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="0beec-163">From the base image page, select **Create Virtual Machine** to be directed to the new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![繪圖][img-acom-1]
2. <span data-ttu-id="0beec-165">利用您想使用的 Azure 訂用帳戶之 Microsoft 帳戶和密碼登入入口網站。</span><span class="sxs-lookup"><span data-stu-id="0beec-165">Sign in to the portal with the Microsoft account and password for the Azure subscription you want to use.</span></span>
3. <span data-ttu-id="0beec-166">遵循提示以使用您已選取的基底映像建立 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-166">Follow the prompts to create a VM by using the base image you have selected.</span></span> <span data-ttu-id="0beec-167">您必須提供主機名稱 (電腦的名稱)、使用者名稱 (以系統管理員身分註冊) 和 VM 的密碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-167">You need to provide a host name (name of the computer), user name (registered as an administrator), and password for the VM.</span></span>

    ![繪圖][img-portal-vm-create]
4. <span data-ttu-id="0beec-169">選取要部署之 VM 的大小：</span><span class="sxs-lookup"><span data-stu-id="0beec-169">Select the size of the VM to deploy:</span></span>

    <span data-ttu-id="0beec-170">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-170">a.</span></span>    <span data-ttu-id="0beec-171">如果您打算開發 VHD 內部部署，大小不會造成影響。</span><span class="sxs-lookup"><span data-stu-id="0beec-171">If you plan to develop the VHD on-premises, the size does not matter.</span></span> <span data-ttu-id="0beec-172">請考慮使用其中一個較小的 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-172">Consider using one of the smaller VMs.</span></span>

    <span data-ttu-id="0beec-173">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-173">b.</span></span>    <span data-ttu-id="0beec-174">如果您打算在 Azure 中開發映像，請考慮使用其中一個建議的 VM 大小做為選取的映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-174">If you plan to develop the image in Azure, consider using one of the recommended VM sizes for the selected image.</span></span>

    <span data-ttu-id="0beec-175">c.</span><span class="sxs-lookup"><span data-stu-id="0beec-175">c.</span></span>    <span data-ttu-id="0beec-176">關於價格資訊，請參閱入口網站上所顯示的**建議定價層**選取器。</span><span class="sxs-lookup"><span data-stu-id="0beec-176">For pricing information, refer to the **Recommended pricing tiers** selector displayed on the portal.</span></span> <span data-ttu-id="0beec-177">(在這個案例中，發行者為 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="0beec-177">It will provide the three recommended sizes provided by the publisher.</span></span> <span data-ttu-id="0beec-178">)</span><span class="sxs-lookup"><span data-stu-id="0beec-178">(In this case, the publisher is Microsoft.)</span></span>

    ![繪圖][img-portal-vm-size]
5. <span data-ttu-id="0beec-180">設定屬性：</span><span class="sxs-lookup"><span data-stu-id="0beec-180">Set properties:</span></span>

    <span data-ttu-id="0beec-181">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-181">a.</span></span>    <span data-ttu-id="0beec-182">若要快速部署，您可以保留 [選用設定] 與 [資源群組] 下的預設值。</span><span class="sxs-lookup"><span data-stu-id="0beec-182">For quick deployment, you can leave the default values for the properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="0beec-183">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-183">b.</span></span>    <span data-ttu-id="0beec-184">在 [儲存體帳戶] 之下，您可以視情況選取要儲存作業系統 VHD 的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0beec-184">Under **Storage Account**, you can optionally select the storage account in which the operating system VHD will be stored.</span></span>

    <span data-ttu-id="0beec-185">c.</span><span class="sxs-lookup"><span data-stu-id="0beec-185">c.</span></span>    <span data-ttu-id="0beec-186">在 [資源群組] 之下，您可以視情況選取要放置 VM 的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="0beec-186">Under **Resource Group**, you can optionally select the logical group in which to place the VM.</span></span>
6. <span data-ttu-id="0beec-187">選取部署的 [位置]  ：</span><span class="sxs-lookup"><span data-stu-id="0beec-187">Select the **Location** for deployment:</span></span>

    <span data-ttu-id="0beec-188">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-188">a.</span></span>    <span data-ttu-id="0beec-189">如果您打算開發 VHD 內部部署，位置不會造成影響，因為您稍後會將映像上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="0beec-189">If you plan to develop the VHD on-premises, the location does not matter because you will upload the image to Azure later.</span></span>

    <span data-ttu-id="0beec-190">b.</span><span class="sxs-lookup"><span data-stu-id="0beec-190">b.</span></span>    <span data-ttu-id="0beec-191">如果您打算在 Azure 中開發映像，請考慮從一開始就使用其中一個位於美國的 Microsoft Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="0beec-191">If you plan to develop the image in Azure, consider using one of the US-based Microsoft Azure regions from the beginning.</span></span> <span data-ttu-id="0beec-192">這樣可以在您提交映像以進行認證時，加速 Microsoft 代表您執行的 VHD 複製程序。</span><span class="sxs-lookup"><span data-stu-id="0beec-192">This speeds up the VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![繪圖][img-portal-vm-location]
7. <span data-ttu-id="0beec-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-194">Click **Create**.</span></span> <span data-ttu-id="0beec-195">開始部署 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-195">The VM starts to deploy.</span></span> <span data-ttu-id="0beec-196">在數分鐘內，您將成功完成部署，並且可以開始為您的 SKU 建立映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-196">Within minutes, you will have a successful deployment and can begin to create the image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-the-cloud"></a><span data-ttu-id="0beec-197">3.3 在雲端開發您的 VHD</span><span class="sxs-lookup"><span data-stu-id="0beec-197">3.3 Develop your VHD in the cloud</span></span>
<span data-ttu-id="0beec-198">強烈建議您在使用遠端桌面通訊協定 (RDP)，在雲端開發您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-198">We strongly recommend that you develop your VHD in the cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="0beec-199">您會利用在佈建期間指定的使用者名稱和密碼連接到 RDP。</span><span class="sxs-lookup"><span data-stu-id="0beec-199">You connect to RDP with the user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0beec-200">如果您開發 VHD 內部部署 (不建議)，請參閱 [建立虛擬機器映像內部部署](marketplace-publishing-vm-image-creation-on-premise.md)。</span><span class="sxs-lookup"><span data-stu-id="0beec-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="0beec-201">如果您在雲端中開發，就不必下載您的 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-201">Downloading your VHD is not necessary if you are developing in the cloud.</span></span>
>
>

<span data-ttu-id="0beec-202">**使用 [Microsoft Azure 入口網站][link-azure-portal]，透過 RDP 進行連接**</span><span class="sxs-lookup"><span data-stu-id="0beec-202">**Connect via RDP using the [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="0beec-203">選取 [瀏覽] > [VM]。</span><span class="sxs-lookup"><span data-stu-id="0beec-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="0beec-204">[虛擬機器] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0beec-204">The Virtual machines blade opens.</span></span> <span data-ttu-id="0beec-205">確認您要連接的 VM 正在運作，然後從已部署的 VM 清單中選取該 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-205">Ensure that the VM that you want to connect with is running, and then select it from the list of deployed VMs.</span></span>
3. <span data-ttu-id="0beec-206">描述選取之 VM 的刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0beec-206">A blade opens that describes the selected VM.</span></span> <span data-ttu-id="0beec-207">在頂端，按一下 [連接] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-207">At the top, click **Connect**.</span></span>
4. <span data-ttu-id="0beec-208">系統會提示您輸入在佈建期間指定的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-208">You are prompted to enter the user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="0beec-209">**使用 PowerShell，透過 RDP 連接**</span><span class="sxs-lookup"><span data-stu-id="0beec-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="0beec-210">若要將遠端桌面檔案下載至本機電腦，請使用 [Get-AzureRemoteDesktopFile Cmdlet][link-technet-2]。</span><span class="sxs-lookup"><span data-stu-id="0beec-210">To download a remote desktop file to a local machine, use the [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="0beec-211">為了使用這個 Cmdlet，您必須知道服務名稱和 VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-211">In order to use this cmdlet, you need to know the name of the service and name of the VM.</span></span> <span data-ttu-id="0beec-212">如果您已從 [Microsoft Azure 入口網站][link-azure-portal]建立 VM，您可以在 VM 屬性下找到此資訊：</span><span class="sxs-lookup"><span data-stu-id="0beec-212">If you created the VM from the [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="0beec-213">在 Microsoft Azure 入口網站中，選取 [瀏覽] > [VM]。</span><span class="sxs-lookup"><span data-stu-id="0beec-213">In the Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="0beec-214">[虛擬機器] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0beec-214">The Virtual machines blade opens.</span></span> <span data-ttu-id="0beec-215">選取您部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-215">Select the VM that you deployed.</span></span>
3. <span data-ttu-id="0beec-216">描述選取之 VM 的刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0beec-216">A blade opens that describes the selected VM.</span></span>
4. <span data-ttu-id="0beec-217">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-217">Click **Properties**.</span></span>
5. <span data-ttu-id="0beec-218">網域名稱的第一個部份是服務名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-218">The first portion of the domain name is the service name.</span></span> <span data-ttu-id="0beec-219">主機名稱是 VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-219">The host name is the VM name.</span></span>

    ![繪圖][img-portal-vm-rdp]
6. <span data-ttu-id="0beec-221">要將已建立之 VM 的 RDP 檔案下載至系統管理員的本機桌面之 Cmdlet 如下所示。</span><span class="sxs-lookup"><span data-stu-id="0beec-221">The cmdlet to download the RDP file for the created VM to the administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="0beec-222">在 MSDN 的文章＜ [透過 RDP 或 SSH 連接至 Azure VM](http://msdn.microsoft.com/library/azure/dn535788.aspx)＞中可找到 RDP 的相關詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0beec-222">More information about RDP can be found on MSDN in the article [Connect to an Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="0beec-223">**設定 VM 並建立您的 SKU**</span><span class="sxs-lookup"><span data-stu-id="0beec-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="0beec-224">下載作業系統 VHD 之後，請使用 Hyper-V 並將 VM 設定為開始建立您的 SKU。</span><span class="sxs-lookup"><span data-stu-id="0beec-224">After the operating system VHD is downloaded, use Hyper­V and configure a VM to begin creating your SKU.</span></span> <span data-ttu-id="0beec-225">詳細步驟可在下列 TechNet 連結中找到： [安裝 Hyper-V 和設定 VM](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0beec-225">Detailed steps can be found at the following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-the-correct-vhd-size"></a><span data-ttu-id="0beec-226">3.4 選擇正確的 VHD 大小</span><span class="sxs-lookup"><span data-stu-id="0beec-226">3.4 Choose the correct VHD size</span></span>
<span data-ttu-id="0beec-227">您 VM 映像中的 Windows 作業系統 VHD 應建立為 128 GB 固定格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-227">The Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="0beec-228">如果實體大小小於 128 GB，此 VHD 應為疏鬆 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-228">If the physical size is less than 128 GB, the VHD should be sparse.</span></span> <span data-ttu-id="0beec-229">所提供的基底 Windows 和 SQL Server 映像皆符合這些需求；所以請勿變更所取得之 VHD 的格式或大小。</span><span class="sxs-lookup"><span data-stu-id="0beec-229">The base Windows and SQL Server images provided already meet these requirements, so do not change the format or the size of the VHD obtained.</span></span>  

<span data-ttu-id="0beec-230">資料磁碟的大小可高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="0beec-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="0beec-231">決定磁碟大小時，請記得客戶無法於部署時在映像中調整 VHD 大小。</span><span class="sxs-lookup"><span data-stu-id="0beec-231">When deciding on the disk size, remember that customers cannot resize VHDs within an image at the time of deployment.</span></span> <span data-ttu-id="0beec-232">資料磁碟 VHD 應建立為固定格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="0beec-233">也可以是疏鬆 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-233">They should also be sparse.</span></span> <span data-ttu-id="0beec-234">資料磁碟可以空白或包含資料。</span><span class="sxs-lookup"><span data-stu-id="0beec-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-the-latest-windows-patches"></a><span data-ttu-id="0beec-235">3.5 安裝最新的 Windows 補充程式</span><span class="sxs-lookup"><span data-stu-id="0beec-235">3.5 Install the latest Windows patches</span></span>
<span data-ttu-id="0beec-236">基底映像包含至其發佈日期為止的最新補充程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-236">The base images contain the latest patches up to their published date.</span></span> <span data-ttu-id="0beec-237">在您發行您已建立的作業系統 VHD 之前，請確認 Windows Update 已執行，且已安裝最新的「關鍵」和「重要」安全性更新。</span><span class="sxs-lookup"><span data-stu-id="0beec-237">Before publishing the operating system VHD you have created, ensure that Windows Update has been run and that all the latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="0beec-238">3.6 必要時執行其他設定並排程工作</span><span class="sxs-lookup"><span data-stu-id="0beec-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="0beec-239">如果需要進行其他設定，請在部署 VM 後，考慮使用在啟動時執行的已排程工作，進行最終的 VM 變更：</span><span class="sxs-lookup"><span data-stu-id="0beec-239">If additional configuration is needed, consider using a scheduled task that runs at startup to make any final changes to the VM after it has been deployed:</span></span>

* <span data-ttu-id="0beec-240">讓工作在成功執行時將自己刪除是最佳作法。</span><span class="sxs-lookup"><span data-stu-id="0beec-240">It is a best practice to have the task delete itself upon successful execution.</span></span>
* <span data-ttu-id="0beec-241">所有設定都應該依靠磁碟機 C 或 D，因為它們是唯二保證隨時都存在的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="0beec-241">No configuration should rely on drives other than drives C or D, because these are the only two drives that are always guaranteed to exist.</span></span> <span data-ttu-id="0beec-242">磁碟機 C 是作業系統磁碟，而磁碟機 D 是暫存本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="0beec-242">Drive C is the operating system disk, and drive D is the temporary local disk.</span></span>

### <a name="37-generalize-the-image"></a><span data-ttu-id="0beec-243">3.7 一般化映像</span><span class="sxs-lookup"><span data-stu-id="0beec-243">3.7 Generalize the image</span></span>
<span data-ttu-id="0beec-244">Azure Marketplace 中的所有映像通常都必須能夠重複使用。</span><span class="sxs-lookup"><span data-stu-id="0beec-244">All images in the Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="0beec-245">也就是說，作業系統 VHD 必須一般化：</span><span class="sxs-lookup"><span data-stu-id="0beec-245">In other words, the operating system VHD must be generalized:</span></span>

* <span data-ttu-id="0beec-246">對 Windows 而言，此映像應該是 "sysprepped"，而且所有設定都應該在支援 **sysprep** 命令的狀態下進行。</span><span class="sxs-lookup"><span data-stu-id="0beec-246">For Windows, the image should be "sysprepped," and no configurations should be done that do not support the **sysprep** command.</span></span>
* <span data-ttu-id="0beec-247">您可以從目錄 %windir%\System32\Sysprep 執行以下命令。</span><span class="sxs-lookup"><span data-stu-id="0beec-247">You can run the following command from the directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="0beec-248">下列 MSDN 文章的「步驟」提供如何 sysprep 作業系統的指導：[建立 Windows Server VHD 並將其上傳至 Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0beec-248">Guidance on how to sysprep the operating system is provided in Step of the following MSDN article: [Create and upload a Windows Server VHD to Azure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="0beec-249">4.從您的 VHD 部署 VM</span><span class="sxs-lookup"><span data-stu-id="0beec-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="0beec-250">在您將 VHD (一般化作業系統 VHD 和零或更多個資料磁碟 VHD) 上傳至 Azure 儲存體帳戶之後，您就可以將它們註冊為使用者 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-250">After you have uploaded your VHDs (the generalized operating system VHD and zero or more data disk VHDs) to an Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="0beec-251">您可以接著測試該映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-251">Then you can test that image.</span></span> <span data-ttu-id="0beec-252">請注意，因為您的作業系統 VHD 已一般化，所以您無法藉由提供 VHD URL 來直接部署 VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-252">Note that because your operating system VHD is generalized, you cannot directly deploy the VM by providing the VHD URL.</span></span>

<span data-ttu-id="0beec-253">若要深入了解 VM 映像，請檢閱下列部落格文章：</span><span class="sxs-lookup"><span data-stu-id="0beec-253">To learn more about VM images, review the following blog posts:</span></span>

* [<span data-ttu-id="0beec-254">VM 映像</span><span class="sxs-lookup"><span data-stu-id="0beec-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="0beec-255">VM 映像 PowerShell 如何</span><span class="sxs-lookup"><span data-stu-id="0beec-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="0beec-256">關於 Azure 中的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="0beec-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-the-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="0beec-257">設定必要的工具 (PowerShell 和 Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="0beec-257">Set up the necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="0beec-258">如何設定 PowerShell</span><span class="sxs-lookup"><span data-stu-id="0beec-258">How to setup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="0beec-259">如何設定 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0beec-259">How to setup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="0beec-260">4.1 建立使用者 VM 映像</span><span class="sxs-lookup"><span data-stu-id="0beec-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="0beec-261">擷取 VM</span><span class="sxs-lookup"><span data-stu-id="0beec-261">Capture VM</span></span>
<span data-ttu-id="0beec-262">如需使用 API/PowerShell/Azure CLI 擷取 VM 的相關指引，請閱讀下面指定的連結。</span><span class="sxs-lookup"><span data-stu-id="0beec-262">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="0beec-263">API</span><span class="sxs-lookup"><span data-stu-id="0beec-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="0beec-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0beec-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0beec-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0beec-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="0beec-266">一般化映像</span><span class="sxs-lookup"><span data-stu-id="0beec-266">Generalize Image</span></span>
<span data-ttu-id="0beec-267">如需使用 API/PowerShell/Azure CLI 擷取 VM 的相關指引，請閱讀下面指定的連結。</span><span class="sxs-lookup"><span data-stu-id="0beec-267">Please read the links given below for guidance on capturing the VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="0beec-268">API</span><span class="sxs-lookup"><span data-stu-id="0beec-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="0beec-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0beec-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="0beec-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0beec-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="0beec-271">4.2 從使用者 VM 映像部署 VM</span><span class="sxs-lookup"><span data-stu-id="0beec-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="0beec-272">若要從使用者 VM 映像部署 VM，您可以使用最新的 [Azure 入口網站](https://manage.windowsazure.com) 或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0beec-272">To deploy a VM from a user VM image, you can use the current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="0beec-273">**從最新的 Azure 入口網站部署 VM**</span><span class="sxs-lookup"><span data-stu-id="0beec-273">**Deploy a VM from the current Azure portal**</span></span>

1. <span data-ttu-id="0beec-274">移至 [新增] > [計算] > [虛擬機器] > [從資源庫]。</span><span class="sxs-lookup"><span data-stu-id="0beec-274">Go to **New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![繪圖][img-manage-vm-new]
2. <span data-ttu-id="0beec-276">移至 [我的映像] ，然後選取要從其中部署 VM 的 VM 映像：</span><span class="sxs-lookup"><span data-stu-id="0beec-276">Go to **My images**, and then select the VM image from which to deploy a VM:</span></span>

   1. <span data-ttu-id="0beec-277">密切注意您選取的映像，因為 [我的映像]  檢視會同時列出作業系統映像和 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-277">Pay close attention to which image you select, because the **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="0beec-278">查看磁碟數目有助於判斷您正在部署的映像類型，因為大部分的 VM 映像都具有一個以上的磁碟。</span><span class="sxs-lookup"><span data-stu-id="0beec-278">Looking at the number of disks can help determine what type of image you are deploying, because the majority of VM images have more than one disk.</span></span> <span data-ttu-id="0beec-279">然而，VM 映像還是可能只有一個作業系統磁碟，然後會將 [磁碟數目]  設定為 1。</span><span class="sxs-lookup"><span data-stu-id="0beec-279">However, it is still possible to have a VM image with only a single operating system disk, which would then have **Number of disks** set to 1.</span></span>

      ![繪圖][img-manage-vm-select]
3. <span data-ttu-id="0beec-281">遵循 VM 建立精靈，並指定 VM 名稱、VM 大小、位置、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-281">Follow the VM creation wizard and specify the VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="0beec-282">**從 PowerShell 部署 VM**</span><span class="sxs-lookup"><span data-stu-id="0beec-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="0beec-283">若要從剛才建立的一般化 VM 映像部署大型 VM，您可使用下列 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0beec-283">To deploy a large VM from the generalized VM image just created, you can use the following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="0beec-284">如需其他協助，請參閱 [針對 VHD 建立常見問題進行疑難排解]。</span><span class="sxs-lookup"><span data-stu-id="0beec-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="0beec-285">5.取得 VM 映像的認證</span><span class="sxs-lookup"><span data-stu-id="0beec-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="0beec-286">為您的 VM 映像做好進入 Azure Marketplace 之準備的下一個步驟是為它取得認證。</span><span class="sxs-lookup"><span data-stu-id="0beec-286">The next step in preparing your VM image for the Azure Marketplace is to have it certified.</span></span>

<span data-ttu-id="0beec-287">這個程序包含執行特殊的認證工具、將認證結果上傳至您的 VHD 所在的 Azure 容器、加入供應項目、定義您的 SKU、以及提交您的 VM 映像以取得認證。</span><span class="sxs-lookup"><span data-stu-id="0beec-287">This process includes running a special certification tool, uploading the verification results to the Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-the-certification-test-tool-for-azure-certified"></a><span data-ttu-id="0beec-288">5.1 下載並執行適用於 Azure 認證的認證測試工具</span><span class="sxs-lookup"><span data-stu-id="0beec-288">5.1 Download and run the Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="0beec-289">此認證工具會在運作中的 VM (從您的使用者 VM 映像佈建) 上執行，以確保 VM 映像與 Microsoft Azure 相容。</span><span class="sxs-lookup"><span data-stu-id="0beec-289">The certification tool runs on a running VM, provisioned from your user VM image, to ensure that the VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="0beec-290">它將驗證是否已符合為 VHD 做準備的指導和需求。</span><span class="sxs-lookup"><span data-stu-id="0beec-290">It will verify that the guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="0beec-291">工具的輸出是相容性報告，應該在要求憑證時於發佈入口網站上傳。</span><span class="sxs-lookup"><span data-stu-id="0beec-291">The output of the tool is a compatibility report, which should be uploaded on the Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="0beec-292">認證工具可使用於 Windows 和 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="0beec-292">The certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="0beec-293">它會透過 PowerShell 連接至 Windows 型 VM，並透過 SSH.Net 連接至 Linux VM：</span><span class="sxs-lookup"><span data-stu-id="0beec-293">It connects to Windows-based VMs via PowerShell and connects to Linux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="0beec-294">首先，請在 [Microsoft 下載網站][link-msft-download]下載認證工具。</span><span class="sxs-lookup"><span data-stu-id="0beec-294">First, download the certification tool at the [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="0beec-295">開啟認證工具，然後按一下 [啟動新測試]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0beec-295">Open the certification tool, and then click the **Start New Test** button.</span></span>
3. <span data-ttu-id="0beec-296">從 [測試資訊]  畫面，輸入執行測試的名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-296">From the **Test Information** screen, enter a name for the test run.</span></span>
4. <span data-ttu-id="0beec-297">選擇您的 VM 位於 Linux 或 Windows。</span><span class="sxs-lookup"><span data-stu-id="0beec-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="0beec-298">根據您的選擇，選取後續選項。</span><span class="sxs-lookup"><span data-stu-id="0beec-298">Depending on which you choose, select the subsequent options.</span></span>

### <a name="connect-the-certification-tool-to-a-linux-vm-image"></a><span data-ttu-id="0beec-299">**將認證工具連接到 Linux VM 映像**</span><span class="sxs-lookup"><span data-stu-id="0beec-299">**Connect the certification tool to a Linux VM image**</span></span>
1. <span data-ttu-id="0beec-300">選取 SSH 驗證模式：密碼或金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="0beec-300">Select the SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="0beec-301">如果使用以密碼為基礎的驗證，請輸入網域名稱系統 (DNS) 名稱、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-301">If using password-­based authentication, enter the Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="0beec-302">如果使用金鑰檔案驗證，請輸入 DNS 名稱、使用者名稱和私密金鑰位置。</span><span class="sxs-lookup"><span data-stu-id="0beec-302">If using key file authentication, enter the DNS name, user name, and private key location.</span></span>

   ![Linux VM 映像的密碼驗證][img-cert-vm-pswd-lnx]

   ![Linux VM 映像的金鑰檔案驗證][img-cert-vm-key-lnx]

### <a name="connect-the-certification-tool-to-a-windows-based-vm-image"></a><span data-ttu-id="0beec-305">**將認證工具連接到 Windows 型 VM 映像**</span><span class="sxs-lookup"><span data-stu-id="0beec-305">**Connect the certification tool to a Windows-based VM image**</span></span>
1. <span data-ttu-id="0beec-306">輸入完整 VM DNS 名稱 (例如 MyVMName.Cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="0beec-306">Enter the fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="0beec-307">輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-307">Enter the user name and password.</span></span>

   ![Windows VM 映像的密碼驗證][img-cert-vm-pswd-win]

<span data-ttu-id="0beec-309">在您選取了 Linux 型或 Windows 型 VM 映像的正確選項之後，請選取 [測試連接]  以確認 SSH.Net 或 PowerShell 是否具有有效的連接以供測試用途。</span><span class="sxs-lookup"><span data-stu-id="0beec-309">After you have selected the correct options for your Linux or Windows-based VM image, select **Test Connection** to ensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="0beec-310">建立連接之後，選取 [下一步]  啟動測試。</span><span class="sxs-lookup"><span data-stu-id="0beec-310">After a connection is established, select **Next** to start the test.</span></span>

<span data-ttu-id="0beec-311">測試完成時，您將收到每個測試項目的結果 (通過/失敗/警告)。</span><span class="sxs-lookup"><span data-stu-id="0beec-311">When the test is complete, you will receive the results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM 映像的測試案例][img-cert-vm-test-lnx]

![Windows VM 映像的測試案例][img-cert-vm-test-win]

<span data-ttu-id="0beec-314">如果任何測試失敗，您的映像就不會獲得認證。</span><span class="sxs-lookup"><span data-stu-id="0beec-314">If any of the tests fail, your image will not be certified.</span></span> <span data-ttu-id="0beec-315">如果發生這種情況，請檢閱需求並進行任何必要的變更。</span><span class="sxs-lookup"><span data-stu-id="0beec-315">If this occurs, review the requirements and make any necessary changes.</span></span>

<span data-ttu-id="0beec-316">在自動化測試之後，系統會要求您透過問卷螢幕提供您的 VM 映像的額外輸入。</span><span class="sxs-lookup"><span data-stu-id="0beec-316">After the automated test, you are asked to provide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="0beec-317">完成問題，然後選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-317">Complete the questions, and then select **Next**.</span></span>

![認證工具問卷][img-cert-vm-questionnaire]

![認證工具問卷][img-cert-vm-questionnaire-2]

<span data-ttu-id="0beec-320">在您完成問卷調查之後，您可以提供其他資訊，例如 Linux VM 映像的 SSH 存取資訊以及失敗評估的說明。</span><span class="sxs-lookup"><span data-stu-id="0beec-320">After you have completed the questionnaire, you can provide additional information such as SSH access information for the Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="0beec-321">除了問卷調查的答案以外，您可以下載已執行測試案例的測試結果和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0beec-321">You can download the test results and log files for the executed test cases in addition to your answers to the questionnaire.</span></span> <span data-ttu-id="0beec-322">將結果儲存在與您的 VHD 相同的容器中。</span><span class="sxs-lookup"><span data-stu-id="0beec-322">Save the results in the same container as your VHDs.</span></span>

![儲存認證測試結果][img-cert-vm-results]

### <a name="52-get-the-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="0beec-324">5.2 取得 VM 映像的共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="0beec-324">5.2 Get the shared access signature URI for your VM images</span></span>
<span data-ttu-id="0beec-325">在發行期間，您會指定統一資源識別項 (URI)，這些 URI 會指向您為 SKU 所建立的每個 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-325">During the publishing process, you specify the uniform resource identifiers (URIs) that lead to each of the VHDs you have created for your SKU.</span></span> <span data-ttu-id="0beec-326">Microsoft 需要在認證程序期間存取這些 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-326">Microsoft needs access to these VHDs during the certification process.</span></span> <span data-ttu-id="0beec-327">因此，您必須建立每個 VHD 的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-327">Therefore, you need to create a shared access signature URI for each VHD.</span></span> <span data-ttu-id="0beec-328">此為要在發佈入口網站的 [映像]  標籤中輸入的 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-328">This is the URI that should be entered in the **Images** tab in the Publishing Portal.</span></span>

<span data-ttu-id="0beec-329">建立的共用存取簽章 URI 應符合下列需求：</span><span class="sxs-lookup"><span data-stu-id="0beec-329">The shared access signature URI created should adhere to the following requirements:</span></span>

* <span data-ttu-id="0beec-330">為 VHD 產生共用存取簽章 URI 時，必須有足夠的列出和讀取權限。</span><span class="sxs-lookup"><span data-stu-id="0beec-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="0beec-331">不提供寫入或刪除存取權。</span><span class="sxs-lookup"><span data-stu-id="0beec-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="0beec-332">存取期間應為建立共用存取簽章 URI 起至少三個 (3) 星期。</span><span class="sxs-lookup"><span data-stu-id="0beec-332">The duration for access should be a minimum of three (3) weeks from when the shared access signature URI is created.</span></span>
* <span data-ttu-id="0beec-333">為了確保使用 UTC 時間，請選取目前日期之前的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-333">To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="0beec-334">例如，如果目前日期為 2014 年 10 月 6 日，則選取 10/5/2014。</span><span class="sxs-lookup"><span data-stu-id="0beec-334">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="0beec-335">有多種方式可產生 SAS URL，以便將您的 VHD 分享到 Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="0beec-335">SAS URL can be generated in multiple ways to share your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="0beec-336">以下是 3 個建議的工具︰</span><span class="sxs-lookup"><span data-stu-id="0beec-336">Following are the 3 recommended tools:</span></span>

1.  <span data-ttu-id="0beec-337">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="0beec-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="0beec-338">Microsoft 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="0beec-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="0beec-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0beec-339">Azure CLI</span></span>

<span data-ttu-id="0beec-340">**Azure 儲存體總管 (建議 Windows 使用者採用)**</span><span class="sxs-lookup"><span data-stu-id="0beec-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="0beec-341">以下是關於使用 Azure 儲存體總管產生 SAS URL 的步驟</span><span class="sxs-lookup"><span data-stu-id="0beec-341">Following are the steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="0beec-342">從 CodePlex 下載 [Azure 儲存體總管 6 預覽 3](https://azurestorageexplorer.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="0beec-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="0beec-343">移至 [Azure 儲存體總管 6 預覽](https://azurestorageexplorer.codeplex.com/)，然後按 [下載]。</span><span class="sxs-lookup"><span data-stu-id="0beec-343">Go to [Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="0beec-345">下載 [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)，解壓縮之後安裝。</span><span class="sxs-lookup"><span data-stu-id="0beec-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="0beec-347">安裝之後，請開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-347">After it is installed, open the application.</span></span>
4. <span data-ttu-id="0beec-348">按一下 [加入帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-348">Click **Add Account**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="0beec-350">指定儲存體帳戶名稱、儲存體帳戶金鑰和儲存體端點網域。</span><span class="sxs-lookup"><span data-stu-id="0beec-350">Specify the storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="0beec-351">這是您的 Azure 訂用帳戶中的儲存體帳戶，其中保存您在 Azure 入口網站上的 VHD。</span><span class="sxs-lookup"><span data-stu-id="0beec-351">This is the storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="0beec-353">Azure 儲存體總管連接至特定的儲存體帳戶之後，就會開始顯示所有儲存體帳戶內的容器。</span><span class="sxs-lookup"><span data-stu-id="0beec-353">Once Azure Storage Explorer is connected to your specific storage account, it will start showing all of the contains within the storage account.</span></span> <span data-ttu-id="0beec-354">選取您已複製作業系統磁碟 VHD 檔案 (如果適用於您的案例，同時也複製資料磁碟) 所在的容器。</span><span class="sxs-lookup"><span data-stu-id="0beec-354">Select the container where you copied the operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="0beec-356">選取 Blob 容器之後，Azure 儲存體總管會開始顯示容器內的檔案。</span><span class="sxs-lookup"><span data-stu-id="0beec-356">After selecting the blob container, Azure Storage Explorer starts showing the files within the container.</span></span> <span data-ttu-id="0beec-357">選取需要提交的影像檔案 (.vhd)。</span><span class="sxs-lookup"><span data-stu-id="0beec-357">Select the image file (.vhd) that needs to be submitted.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="0beec-359">選取容器中的 .vhd 檔案之後，按一下 [安全性]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0beec-359">After selecting the .vhd file in the container, click the **Security** tab.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="0beec-361">在 [Blob 容器安全性] 對話方塊中，保留 [存取層級] 索引標籤上的預設值，然後按一下 [共用存取簽章] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0beec-361">In the **Blob Container Security** dialog box, leave the defaults on the **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="0beec-363">遵循下列步驟來產生 .vhd 映像的共用存取簽章 URI：</span><span class="sxs-lookup"><span data-stu-id="0beec-363">Follow the steps below to generate a shared access signature URI for the .vhd image:</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="0beec-365">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-365">a.</span></span> <span data-ttu-id="0beec-366">**允許存取開始日期**：為了確保使用 UTC 時間，請選取目前日期之前的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-366">**Access permitted from:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="0beec-367">例如，如果目前日期為 2014 年 10 月 6 日，則選取 10/5/2014。</span><span class="sxs-lookup"><span data-stu-id="0beec-367">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="0beec-368">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-368">b.</span></span> <span data-ttu-id="0beec-369">**允許存取結束日期**：選取至少在 [允許存取開始日期] 之後 3 個星期的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-369">**Access permitted to:** Select a date that is at least 3 weeks after the **Access permitted from** date.</span></span>

    <span data-ttu-id="0beec-370">c.</span><span class="sxs-lookup"><span data-stu-id="0beec-370">c.</span></span> <span data-ttu-id="0beec-371">**允許動作**：選取 [列出] 和 [讀取] 權限。</span><span class="sxs-lookup"><span data-stu-id="0beec-371">**Actions permitted:** Select the **List** and **Read** permissions.</span></span>

    <span data-ttu-id="0beec-372">d.</span><span class="sxs-lookup"><span data-stu-id="0beec-372">d.</span></span> <span data-ttu-id="0beec-373">如果您已正確選取 .vhd 檔案，則您的檔案會出現在 [要存取的 Blob 名稱] 中且副檔名為 .vhd。</span><span class="sxs-lookup"><span data-stu-id="0beec-373">If you have selected your .vhd file correctly, then your file appears in **Blob name to access** with extension .vhd.</span></span>

    <span data-ttu-id="0beec-374">e.</span><span class="sxs-lookup"><span data-stu-id="0beec-374">e.</span></span> <span data-ttu-id="0beec-375">按一下 [產生簽章]。</span><span class="sxs-lookup"><span data-stu-id="0beec-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="0beec-376">f.</span><span class="sxs-lookup"><span data-stu-id="0beec-376">f.</span></span> <span data-ttu-id="0beec-377">在 [此容器產生的共用存取簽章 URI] 中，在下列項目中檢查上方反白顯示的項目：</span><span class="sxs-lookup"><span data-stu-id="0beec-377">In **Generated Shared Access Signature URI of this container**, check for the following as highlighted above:</span></span>

       - <span data-ttu-id="0beec-378">確定您的映像檔案名稱和 **".vhd"** 位於 URI 中。</span><span class="sxs-lookup"><span data-stu-id="0beec-378">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
       - <span data-ttu-id="0beec-379">確定 **"= rl"** 出現在簽章的結尾。</span><span class="sxs-lookup"><span data-stu-id="0beec-379">At the end of the signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="0beec-380">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="0beec-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="0beec-381">確定 **"sr=c"** 出現在簽章的中間。</span><span class="sxs-lookup"><span data-stu-id="0beec-381">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="0beec-382">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="0beec-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="0beec-383">若要確認產生的共用存取簽章 URI 有效，請按一下 [在瀏覽器中測試]。</span><span class="sxs-lookup"><span data-stu-id="0beec-383">To ensure that the generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="0beec-384">應該會啟動下載程序。</span><span class="sxs-lookup"><span data-stu-id="0beec-384">It should start the download process.</span></span>

12. <span data-ttu-id="0beec-385">複製共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-385">Copy the shared access signature URI.</span></span> <span data-ttu-id="0beec-386">此為要貼入發佈入口網站的 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-386">This is the URI to paste into the Publishing Portal.</span></span>

13. <span data-ttu-id="0beec-387">針對 SKU 中的每個 VHD 重複步驟 6-10。</span><span class="sxs-lookup"><span data-stu-id="0beec-387">Repeat steps 6-10 for each VHD in the SKU.</span></span>

<span data-ttu-id="0beec-388">**Microsoft Azure 儲存體總管 (Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="0beec-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="0beec-389">以下是關於使用 Microsoft Azure 儲存體總管產生 SAS URL 的步驟</span><span class="sxs-lookup"><span data-stu-id="0beec-389">Following are the steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="0beec-390">從 [http://storageexplorer.com/](http://storageexplorer.com/) 網站下載 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="0beec-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="0beec-391">移至 [Microsoft Azure 儲存體總管](http://storageexplorer.com/releasenotes.html)，然後按 [下載 Windows 版]。</span><span class="sxs-lookup"><span data-stu-id="0beec-391">Go to [Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="0beec-393">安裝之後，請開啟應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-393">After it is installed, open the application.</span></span>

3.  <span data-ttu-id="0beec-394">按一下 [加入帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="0beec-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="0beec-395">登入帳戶將 Microsoft Azure 儲存體總管設定給您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0beec-395">Configure Microsoft Azure Storage Explorer to your subscription by sign in to your account</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="0beec-397">移至儲存體帳戶，選取 [容器]</span><span class="sxs-lookup"><span data-stu-id="0beec-397">Go to storage account and select the Container</span></span>

6.  <span data-ttu-id="0beec-398">選取 [取得共用存取簽章...]</span><span class="sxs-lookup"><span data-stu-id="0beec-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="0beec-399">\(以滑鼠右鍵按一下 [容器])</span><span class="sxs-lookup"><span data-stu-id="0beec-399">by using Right Click of the **container**</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="0beec-401">根據下列指示，更新 [開始時間]、[到期時間] 和 [權限]</span><span class="sxs-lookup"><span data-stu-id="0beec-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="0beec-403">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-403">a.</span></span>  <span data-ttu-id="0beec-404">**開始時間：**為了確保使用 UTC 時間，請選取目前日期之前的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-404">**Start Time:** To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="0beec-405">例如，如果目前日期為 2014 年 10 月 6 日，則選取 10/5/2014。</span><span class="sxs-lookup"><span data-stu-id="0beec-405">For example, if the current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="0beec-406">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-406">b.</span></span>  <span data-ttu-id="0beec-407">**到期時間︰**選取至少在 [開始時間] 日期之後 3 個星期的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-407">**Expiry Time:** Select a date that is at least 3 weeks after the **Start Time** date.</span></span>

    <span data-ttu-id="0beec-408">c.</span><span class="sxs-lookup"><span data-stu-id="0beec-408">c.</span></span>  <span data-ttu-id="0beec-409">**權限：**：選取 [列出] 和 [讀取] 權限</span><span class="sxs-lookup"><span data-stu-id="0beec-409">**Permissions:** Select the **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="0beec-410">複製容器共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="0beec-410">Copy Container shared access signature URI</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="0beec-412">產生的 SAS URL 是容器層級，我們現在需要在其中新增 VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-412">Generated SAS URL is for container Level and now we need to add VHD name in it.</span></span>

    <span data-ttu-id="0beec-413">容器層級 SAS URL 的格式︰`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="0beec-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="0beec-414">在 SAS URL 中的容器名稱之後插入 VHD 名稱，如下所示 `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="0beec-414">Insert VHD name after the container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="0beec-415">範例：</span><span class="sxs-lookup"><span data-stu-id="0beec-415">Example:</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="0beec-417">TestRGVM201631920152.vhd 是 VHD 的名稱，所以 VHD SAS URL 會是 `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="0beec-417">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="0beec-418">確定您的映像檔案名稱和 **".vhd"** 位於 URI 中。</span><span class="sxs-lookup"><span data-stu-id="0beec-418">Make sure that your image file name and **".vhd"** are in the URI.</span></span>
    - <span data-ttu-id="0beec-419">確定 **"sp=rl"** 出現在簽章的中間。</span><span class="sxs-lookup"><span data-stu-id="0beec-419">In middle of the signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="0beec-420">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="0beec-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="0beec-421">確定 **"sr=c"** 出現在簽章的中間。</span><span class="sxs-lookup"><span data-stu-id="0beec-421">In middle of the signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="0beec-422">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="0beec-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="0beec-423">若要確認產生的共用存取簽章 URI 有效，請在瀏覽器中測試。</span><span class="sxs-lookup"><span data-stu-id="0beec-423">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="0beec-424">應該會啟動下載程序</span><span class="sxs-lookup"><span data-stu-id="0beec-424">It should start the download process</span></span>

10. <span data-ttu-id="0beec-425">複製共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-425">Copy the shared access signature URI.</span></span> <span data-ttu-id="0beec-426">此為要貼入發佈入口網站的 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-426">This is the URI to paste into the Publishing Portal.</span></span>

11. <span data-ttu-id="0beec-427">為 SKU 中的每個 VHD 重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="0beec-427">Repeat these steps for each VHD in the SKU.</span></span>

<span data-ttu-id="0beec-428">**Azure CLI (建議用於非 Windows 和持續整合)**</span><span class="sxs-lookup"><span data-stu-id="0beec-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="0beec-429">以下是關於使用 Azure CLI 產生 SAS URL 的步驟</span><span class="sxs-lookup"><span data-stu-id="0beec-429">Following are the steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="0beec-430">從[這裡](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)下載 Microsoft Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="0beec-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="0beec-431">您也可以找到適用於 **[Windows](http://aka.ms/webpi-azure-cli)** 和 **[MAC OS](http://aka.ms/mac-azure-cli)** 的不同連結。</span><span class="sxs-lookup"><span data-stu-id="0beec-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="0beec-432">下載之後，請安裝</span><span class="sxs-lookup"><span data-stu-id="0beec-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="0beec-433">使用下列程式碼建立 PowerShell 檔案，並將它儲存在本機</span><span class="sxs-lookup"><span data-stu-id="0beec-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="0beec-434">在上面的程式碼中，更新下列參數</span><span class="sxs-lookup"><span data-stu-id="0beec-434">Update the following parameters in above</span></span>

    <span data-ttu-id="0beec-435">a.</span><span class="sxs-lookup"><span data-stu-id="0beec-435">a.</span></span> <span data-ttu-id="0beec-436">**`<StorageAccountName>`**：提供您的儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="0beec-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="0beec-437">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="0beec-437">b.</span></span> <span data-ttu-id="0beec-438">**`<Storage Account Key>`**：提供您的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="0beec-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="0beec-439">c.</span><span class="sxs-lookup"><span data-stu-id="0beec-439">c.</span></span> <span data-ttu-id="0beec-440">**`<Permission Start Date>`**：為了確保使用 UTC 時間，請選取目前日期之前的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-440">**`<Permission Start Date>`**: To safeguard for UTC time, select the day before the current date.</span></span> <span data-ttu-id="0beec-441">例如，如果目前日期為 2016 年 10 月 26 日，則值應該為 10/25/2016</span><span class="sxs-lookup"><span data-stu-id="0beec-441">For example, if the current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="0beec-442">d.</span><span class="sxs-lookup"><span data-stu-id="0beec-442">d.</span></span> <span data-ttu-id="0beec-443">**`<Permission End Date>`**：選取至少在 [開始日期] 之後 3 個星期的日期。</span><span class="sxs-lookup"><span data-stu-id="0beec-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after the **Start Date**.</span></span> <span data-ttu-id="0beec-444">所以值應該為 **11/02/2016**。</span><span class="sxs-lookup"><span data-stu-id="0beec-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="0beec-445">以下是更新適當參數之後的範例程式碼</span><span class="sxs-lookup"><span data-stu-id="0beec-445">Following is the example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="0beec-446">使用「以系統管理員身分執行」模式下開啟 Powershell 編輯器，並在步驟 #3 中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="0beec-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="0beec-447">執行指令碼，它會提供容器層級存取的 SAS URL 給您</span><span class="sxs-lookup"><span data-stu-id="0beec-447">Run the script and it will provide you the SAS URL for container level access</span></span>

    <span data-ttu-id="0beec-448">以下是 SAS 簽章的輸出，請將醒目提示的部分複製到記事本</span><span class="sxs-lookup"><span data-stu-id="0beec-448">Following will be the output of the SAS Signature and copy the highlighted part in a notepad</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="0beec-450">現在您會取得容器層級 SAS URL，您需要在其中新增 VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="0beec-450">Now you will get container level SAS URL and you need to add VHD name in it.</span></span>

    <span data-ttu-id="0beec-451">容器等級 SAS URL #</span><span class="sxs-lookup"><span data-stu-id="0beec-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="0beec-452">在 SAS URL 中的容器名稱之後插入 VHD 名稱，如下所示 `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="0beec-452">Insert VHD name after the container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="0beec-453">範例：</span><span class="sxs-lookup"><span data-stu-id="0beec-453">Example:</span></span>

    <span data-ttu-id="0beec-454">TestRGVM201631920152.vhd 是 VHD 的名稱，所以 VHD SAS URL 會是</span><span class="sxs-lookup"><span data-stu-id="0beec-454">TestRGVM201631920152.vhd is the VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="0beec-455">確定您的映像檔案名稱和 ".vhd" 位於 URI 中。</span><span class="sxs-lookup"><span data-stu-id="0beec-455">Make sure that your image file name and ".vhd" are in the URI.</span></span>
    -   <span data-ttu-id="0beec-456">確定 "sp=rl" 出現在簽章的中間。</span><span class="sxs-lookup"><span data-stu-id="0beec-456">In middle of the signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="0beec-457">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="0beec-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="0beec-458">確定 "sr=c" 出現在簽章的中間。</span><span class="sxs-lookup"><span data-stu-id="0beec-458">In middle of the signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="0beec-459">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="0beec-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="0beec-460">若要確認產生的共用存取簽章 URI 有效，請在瀏覽器中測試。</span><span class="sxs-lookup"><span data-stu-id="0beec-460">To ensure that the generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="0beec-461">應該會啟動下載程序</span><span class="sxs-lookup"><span data-stu-id="0beec-461">It should start the download process</span></span>

9.  <span data-ttu-id="0beec-462">複製共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-462">Copy the shared access signature URI.</span></span> <span data-ttu-id="0beec-463">此為要貼入發佈入口網站的 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-463">This is the URI to paste into the Publishing Portal.</span></span>

10. <span data-ttu-id="0beec-464">為 SKU 中的每個 VHD 重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="0beec-464">Repeat these steps for each VHD in the SKU.</span></span>


### <a name="53-provide-information-about-the-vm-image-and-request-certification-in-the-publishing-portal"></a><span data-ttu-id="0beec-465">5.3 在發佈入口網站中提供 VM 映像和要求認證的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0beec-465">5.3 Provide information about the VM image and request certification in the Publishing Portal</span></span>
<span data-ttu-id="0beec-466">在您已建立供應項目和 SKU 之後，您應該輸入和該 SKU 相關聯的映像詳細資料：</span><span class="sxs-lookup"><span data-stu-id="0beec-466">After you have created your offer and SKU, you should enter the image details associated with that SKU:</span></span>

1. <span data-ttu-id="0beec-467">移至[發佈入口網站][link-pubportal]，然後以您的賣方帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="0beec-467">Go to the [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="0beec-468">選取 [VM 映像]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0beec-468">Select the **VM images** tab.</span></span>
3. <span data-ttu-id="0beec-469">列在頁面頂端的識別碼其實是供應項目識別碼，而不是 SKU 識別碼。</span><span class="sxs-lookup"><span data-stu-id="0beec-469">The identifier listed at the top of the page is actually the offer identifier and not the SKU identifier.</span></span>
4. <span data-ttu-id="0beec-470">在 [SKU]  區段中填入屬性。</span><span class="sxs-lookup"><span data-stu-id="0beec-470">Fill out the properties under the **SKUs** section.</span></span>
5. <span data-ttu-id="0beec-471">在 [作業系統系列] 下，選取與作業系統 VHD 相關聯的作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="0beec-471">Under **Operating system family**, click the operating system type associated with the operating system VHD.</span></span>
6. <span data-ttu-id="0beec-472">在 [作業系統]  方塊中，描述作業系統。</span><span class="sxs-lookup"><span data-stu-id="0beec-472">In the **Operating system** box, describe the operating system.</span></span> <span data-ttu-id="0beec-473">請考慮使用作業系統系列、類型、版本和更新等格式。</span><span class="sxs-lookup"><span data-stu-id="0beec-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="0beec-474">其中一個範例為 "Windows Server Datacenter 2014 R2"。</span><span class="sxs-lookup"><span data-stu-id="0beec-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="0beec-475">最多選取六個建議的虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="0beec-475">Select up to six recommended virtual machine sizes.</span></span> <span data-ttu-id="0beec-476">當客戶決定購買與部署您的映像時，這些大小是在 Azure 入口網站的 [定價層] 刀鋒視窗中對其顯示的建議大小。</span><span class="sxs-lookup"><span data-stu-id="0beec-476">These are recommendations that get displayed to the customer in the Pricing tier blade in the Azure Portal when they decide to purchase and deploy your image.</span></span> <span data-ttu-id="0beec-477">**這些只是建議大小。客戶可以選取任何可容納您映像中指定之磁碟的 VM 大小。**</span><span class="sxs-lookup"><span data-stu-id="0beec-477">**These are only recommendations. The customer is able to select any VM size that accommodates the disks specified in your image.**</span></span>
8. <span data-ttu-id="0beec-478">輸入版本。</span><span class="sxs-lookup"><span data-stu-id="0beec-478">Enter the version.</span></span> <span data-ttu-id="0beec-479">[版本] 欄位會封裝語意版本來識別產品及其更新：</span><span class="sxs-lookup"><span data-stu-id="0beec-479">The version field encapsulates a semantic version to identify the product and its updates:</span></span>
   * <span data-ttu-id="0beec-480">版本格式應該是 X.Y.Z，其中 X、Y 和 Z 是整數。</span><span class="sxs-lookup"><span data-stu-id="0beec-480">Versions should be of the form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="0beec-481">不同 SKU 中的映像可以有不同的主要和次要版本。</span><span class="sxs-lookup"><span data-stu-id="0beec-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="0beec-482">SKU 中的版本應該是累加變更，增加修補程式版本 (X.Y.Z 中的 Z)。</span><span class="sxs-lookup"><span data-stu-id="0beec-482">Versions within a SKU should only be incremental changes, which increase the patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="0beec-483">在 [OS VHD URL]  方塊中輸入為作業系統 VHD 建立的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-483">In the **OS VHD URL** box, enter the shared access signature URI created for the operating system VHD.</span></span>
10. <span data-ttu-id="0beec-484">如果有和這個 SKU 相關聯的資料磁碟，請選取您希望在部署時於其中裝載這個資料磁碟的邏輯單元編號 (LUN)。</span><span class="sxs-lookup"><span data-stu-id="0beec-484">If there are data disks associated with this SKU, select the logical unit number (LUN) to which you would like this data disk to be mounted upon deployment.</span></span>
11. <span data-ttu-id="0beec-485">在 [LUN X VHD URL]  方塊中輸入為第一個資料 VHD 建立的共用存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="0beec-485">In the **LUN X VHD URL** box, enter the shared access signature URI created for the first data VHD.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="0beec-487">常見的 SAS URL 問題和修正</span><span class="sxs-lookup"><span data-stu-id="0beec-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="0beec-488">問題</span><span class="sxs-lookup"><span data-stu-id="0beec-488">Issue</span></span>|<span data-ttu-id="0beec-489">失敗訊息</span><span class="sxs-lookup"><span data-stu-id="0beec-489">Failure Message</span></span>|<span data-ttu-id="0beec-490">修正</span><span class="sxs-lookup"><span data-stu-id="0beec-490">Fix</span></span>|<span data-ttu-id="0beec-491">文件連結</span><span class="sxs-lookup"><span data-stu-id="0beec-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="0beec-492">複製映像失敗 - 在 SAS url 中找不到 "?"</span><span class="sxs-lookup"><span data-stu-id="0beec-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="0beec-493">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-493">Failure: Copying Images.</span></span> <span data-ttu-id="0beec-494">無法使用提供的 SAS Uri 下載 blob。</span><span class="sxs-lookup"><span data-stu-id="0beec-494">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="0beec-495">使用建議的工具更新 SAS Url</span><span class="sxs-lookup"><span data-stu-id="0beec-495">Update the SAS Url using recommended tools</span></span>|[<span data-ttu-id="0beec-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="0beec-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="0beec-497">映像複製失敗 - SAS url 中未設定 “st” 和 “se” 參數</span><span class="sxs-lookup"><span data-stu-id="0beec-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="0beec-498">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-498">Failure: Copying Images.</span></span> <span data-ttu-id="0beec-499">無法使用提供的 SAS Uri 下載 blob。</span><span class="sxs-lookup"><span data-stu-id="0beec-499">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="0beec-500">更新 SAS Url，必須包含開始和結束日期</span><span class="sxs-lookup"><span data-stu-id="0beec-500">Update the SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="0beec-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="0beec-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="0beec-502">複製映像失敗 - SAS url 中沒有 “sp=rl”</span><span class="sxs-lookup"><span data-stu-id="0beec-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="0beec-503">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-503">Failure: Copying Images.</span></span> <span data-ttu-id="0beec-504">無法使用提供的 SAS Uri 下載 blob</span><span class="sxs-lookup"><span data-stu-id="0beec-504">Not able to download blob using provided SAS Uri</span></span>|<span data-ttu-id="0beec-505">更新 SAS Url，將權限設定為「讀取」和「列出」</span><span class="sxs-lookup"><span data-stu-id="0beec-505">Update the SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="0beec-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="0beec-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="0beec-507">複製映像失敗 - SAS url 中的 vhd 名稱含有空格</span><span class="sxs-lookup"><span data-stu-id="0beec-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="0beec-508">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-508">Failure: Copying Images.</span></span> <span data-ttu-id="0beec-509">無法使用提供的 SAS Uri 下載 blob。</span><span class="sxs-lookup"><span data-stu-id="0beec-509">Not able to download blob using provided SAS Uri.</span></span>|<span data-ttu-id="0beec-510">更新 SAS Url，不能含有空格</span><span class="sxs-lookup"><span data-stu-id="0beec-510">Update the SAS Url without white spaces</span></span>|[<span data-ttu-id="0beec-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="0beec-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="0beec-512">複製映像失敗 – SAS Url 授權錯誤的</span><span class="sxs-lookup"><span data-stu-id="0beec-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="0beec-513">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="0beec-513">Failure: Copying Images.</span></span> <span data-ttu-id="0beec-514">因為發生授權錯誤，無法下載 blob</span><span class="sxs-lookup"><span data-stu-id="0beec-514">Not able to download blob due to authorization error</span></span>|<span data-ttu-id="0beec-515">重新產生 SAS Url</span><span class="sxs-lookup"><span data-stu-id="0beec-515">Regenerate the SAS Url</span></span>|[<span data-ttu-id="0beec-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="0beec-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="0beec-517">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0beec-517">Next step</span></span>
<span data-ttu-id="0beec-518">完成 SKU 詳細資料之後，您可以移至 [Azure Marketplace 行銷內容指南][link-pushstaging]。</span><span class="sxs-lookup"><span data-stu-id="0beec-518">After you are done with the SKU details, you can move forward to the [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="0beec-519">在發佈程序的該步驟中，您會在 **步驟 3：在預備環境中測試您的 VM 供應項目**之前提供行銷內容、價格和其他必要資訊，而您會在該步驟中測試各種使用案例，然後再將供應項目部署到 Azure Marketplace 以供公開查看和購買。</span><span class="sxs-lookup"><span data-stu-id="0beec-519">In that step of the publishing process, you provide the marketing content, pricing, and other information necessary prior to **Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying the offer to the Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="0beec-520">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0beec-520">See also</span></span>
* [<span data-ttu-id="0beec-521">使用者入門：如何將供應項目發佈至 Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="0beec-521">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/
