---
title: "aaaCreating hello Azure Marketplace 的虛擬機器映像 |Microsoft 文件"
description: "取得如何 toocreate 虛擬機器的映像 hello Azure Marketplace 供其他人 toopurchase 的詳細的指示。"
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
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="be4cb-103">指南 toocreate hello Azure Marketplace 的虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="be4cb-103">Guide toocreate a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="be4cb-104">這篇文章，**步驟 2**，會引導您完成準備 hello 虛擬硬碟 (Vhd) 會將部署 toohello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="be4cb-104">This article, **Step 2**, walks you through preparing hello virtual hard disks (VHDs) that you will deploy toohello Azure Marketplace.</span></span> <span data-ttu-id="be4cb-105">您的 Vhd 是您 SKU 的 hello foundation。</span><span class="sxs-lookup"><span data-stu-id="be4cb-105">Your VHDs are hello foundation of your SKU.</span></span> <span data-ttu-id="be4cb-106">您是否提供 Linux 或 Windows 為基礎的 SKU 有所不同 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="be4cb-106">hello process differs depending on whether you are providing a Linux-based or Windows-based SKU.</span></span> <span data-ttu-id="be4cb-107">本文將探討這兩種狀況。</span><span class="sxs-lookup"><span data-stu-id="be4cb-107">This article covers both scenarios.</span></span> <span data-ttu-id="be4cb-108">這個程序可與[帳戶建立和註冊][link-acct-creation]同步執行。</span><span class="sxs-lookup"><span data-stu-id="be4cb-108">This process can be performed in parallel with [Account creation and registration][link-acct-creation].</span></span>

## <a name="1-define-offers-and-skus"></a><span data-ttu-id="be4cb-109">1.定義供應項目和 SKU</span><span class="sxs-lookup"><span data-stu-id="be4cb-109">1. Define Offers and SKUs</span></span>
<span data-ttu-id="be4cb-110">在本節中，您將學會 toodefine hello 優惠和其相關聯的 Sku。</span><span class="sxs-lookup"><span data-stu-id="be4cb-110">In this section, you learn toodefine hello offers and their associated SKUs.</span></span>

<span data-ttu-id="be4cb-111">提供項目是其 Sku 的 「 父 」 tooall。</span><span class="sxs-lookup"><span data-stu-id="be4cb-111">An offer is a "parent" tooall of its SKUs.</span></span> <span data-ttu-id="be4cb-112">您可以擁有多個供應項目。</span><span class="sxs-lookup"><span data-stu-id="be4cb-112">You can have multiple offers.</span></span> <span data-ttu-id="be4cb-113">如何決定 toostructure 您提供項目是最多 tooyou。</span><span class="sxs-lookup"><span data-stu-id="be4cb-113">How you decide toostructure your offers is up tooyou.</span></span> <span data-ttu-id="be4cb-114">當 toostaging 推入的供應項目時，它是推入及所有其 Sku。</span><span class="sxs-lookup"><span data-stu-id="be4cb-114">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span> <span data-ttu-id="be4cb-115">請仔細評估 SKU 的識別項，因為它們會顯示在 hello URL:</span><span class="sxs-lookup"><span data-stu-id="be4cb-115">Carefully consider your SKU identifiers, because they will be visible in hello URL:</span></span>

* <span data-ttu-id="be4cb-116">Azure.com：http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span><span class="sxs-lookup"><span data-stu-id="be4cb-116">Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}</span></span>
* <span data-ttu-id="be4cb-117">Azure Preview 入口網站︰https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span><span class="sxs-lookup"><span data-stu-id="be4cb-117">Azure preview portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}</span></span>  

<span data-ttu-id="be4cb-118">SKU 不 hello 商業 VM 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-118">A SKU is hello commercial name for a VM image.</span></span> <span data-ttu-id="be4cb-119">VM 映像包含一個作業系統磁碟以及零或多個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-119">A VM image contains one operating system disk and zero or more data disks.</span></span> <span data-ttu-id="be4cb-120">它是基本上 hello 完成存放裝置設定檔的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="be4cb-120">It is essentially hello complete storage profile for a virtual machine.</span></span> <span data-ttu-id="be4cb-121">每個磁碟都需要一個 VHD。</span><span class="sxs-lookup"><span data-stu-id="be4cb-121">One VHD is needed per disk.</span></span> <span data-ttu-id="be4cb-122">即使是空白的資料磁碟需要建立 VHD toobe。</span><span class="sxs-lookup"><span data-stu-id="be4cb-122">Even blank data disks require a VHD toobe created.</span></span>

<span data-ttu-id="be4cb-123">不論您使用的作業系統，加入只 hello 最小數目的資料磁碟所需的 hello SKU。</span><span class="sxs-lookup"><span data-stu-id="be4cb-123">Regardless of which operating system you use, add only hello minimum number of data disks needed by hello SKU.</span></span> <span data-ttu-id="be4cb-124">客戶無法移除磁碟映像一起部署的 hello 次，但可以隨時加入磁碟期間或部署後可視需要。</span><span class="sxs-lookup"><span data-stu-id="be4cb-124">Customers cannot remove disks that are part of an image at hello time of deployment but can always add disks during or after deployment if they need them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be4cb-125">**請勿變更新映像版本中的磁碟計數。**</span><span class="sxs-lookup"><span data-stu-id="be4cb-125">**Do not change disk count in a new image version.**</span></span> <span data-ttu-id="be4cb-126">如果您必須重新設定 hello 映像中的資料磁碟，定義新的 SKU。</span><span class="sxs-lookup"><span data-stu-id="be4cb-126">If you must reconfigure Data disks in hello image, define a new SKU.</span></span> <span data-ttu-id="be4cb-127">發行新的映像版本，以不同的磁碟計數將會有中斷 hello 中的新映像版本的自動調整大小、 自動部署的解決方案，透過 ARM 範本和其他案例的情況下為基礎的新部署的 hello 可能性。</span><span class="sxs-lookup"><span data-stu-id="be4cb-127">Publishing a new image version with different disk counts will have hello potential of breaking new deployment based on hello new image version in cases of auto-scaling, automatic deployments of solutions through ARM templates and other scenarios.</span></span>
>
>

### <a name="11-add-an-offer"></a><span data-ttu-id="be4cb-128">1.1 加入供應項目</span><span class="sxs-lookup"><span data-stu-id="be4cb-128">1.1 Add an offer</span></span>
1. <span data-ttu-id="be4cb-129">登入 toohello[發佈入口網站][ link-pubportal]使用賣方帳戶。</span><span class="sxs-lookup"><span data-stu-id="be4cb-129">Sign in toohello [Publishing Portal][link-pubportal] by using your seller account.</span></span>
2. <span data-ttu-id="be4cb-130">選取 hello**虛擬機器**hello 發佈入口網站 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4cb-130">Select hello **Virtual Machines** tab of hello Publishing Portal.</span></span> <span data-ttu-id="be4cb-131">在 hello 提示項目欄位中，輸入您提供的名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-131">In hello prompted entry field, enter your offer name.</span></span> <span data-ttu-id="be4cb-132">hello 供應項目名稱通常是 hello 產品或服務計劃 toosell hello Azure Marketplace 中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-132">hello offer name is typically hello name of hello product or service that you plan toosell in hello Azure Marketplace.</span></span>
3. <span data-ttu-id="be4cb-133">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-133">Select **Create**.</span></span>

### <a name="12-define-a-sku"></a><span data-ttu-id="be4cb-134">1.2 定義 SKU</span><span class="sxs-lookup"><span data-stu-id="be4cb-134">1.2 Define a SKU</span></span>
<span data-ttu-id="be4cb-135">加入提供項目之後，您會需要 toodefine，並識別您的 Sku。</span><span class="sxs-lookup"><span data-stu-id="be4cb-135">After you have added an offer, you need toodefine and identify your SKUs.</span></span> <span data-ttu-id="be4cb-136">您可以有多個供應項目，每個供應項目在其下可以有多個 SKU。</span><span class="sxs-lookup"><span data-stu-id="be4cb-136">You can have multiple offers, and each offer can have multiple SKUs under it.</span></span> <span data-ttu-id="be4cb-137">當 toostaging 推入的供應項目時，它是推入及所有其 Sku。</span><span class="sxs-lookup"><span data-stu-id="be4cb-137">When an offer is pushed toostaging, it is pushed along with all of its SKUs.</span></span>

1. <span data-ttu-id="be4cb-138">**加入 SKU。**</span><span class="sxs-lookup"><span data-stu-id="be4cb-138">**Add a SKU.**</span></span> <span data-ttu-id="be4cb-139">hello SKU 需要 hello URL 中使用的識別項。</span><span class="sxs-lookup"><span data-stu-id="be4cb-139">hello SKU requires an identifier, which is used in hello URL.</span></span> <span data-ttu-id="be4cb-140">hello 識別碼中必須是唯一您的發行設定檔，但沒有與其他 「 發行者 」 的識別項衝突的風險。</span><span class="sxs-lookup"><span data-stu-id="be4cb-140">hello identifier must be unique within your publishing profile, but there is no risk of identifier collision with other publishers.</span></span>

   > [!NOTE]
   > <span data-ttu-id="be4cb-141">會顯示 hello Marketplace 中的 hello 優惠 URL 中的 hello 優惠和 SKU 識別碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-141">hello offer and SKU identifiers are displayed in hello offer URL in hello Marketplace.</span></span>
   >
   >
2. <span data-ttu-id="be4cb-142">**為 SKU 加入摘要描述。**</span><span class="sxs-lookup"><span data-stu-id="be4cb-142">**Add a summary description for your SKU.**</span></span> <span data-ttu-id="be4cb-143">摘要描述都是可見的 toocustomers，因此您應該讓它們可輕鬆地讀取。</span><span class="sxs-lookup"><span data-stu-id="be4cb-143">Summary descriptions are visible toocustomers, so you should make them easily readable.</span></span> <span data-ttu-id="be4cb-144">這項資訊不需要 toobe 鎖定直到 hello 「 推入 tooStaging 」 階段。</span><span class="sxs-lookup"><span data-stu-id="be4cb-144">This information does not need toobe locked until hello "Push tooStaging" phase.</span></span> <span data-ttu-id="be4cb-145">之前，您是免費 tooedit 它。</span><span class="sxs-lookup"><span data-stu-id="be4cb-145">Until then, you are free tooedit it.</span></span>
3. <span data-ttu-id="be4cb-146">如果您使用 Windows 架構的 Sku，請遵循 hello 建議的連結 tooacquire hello 核准的 Windows Server 版本。</span><span class="sxs-lookup"><span data-stu-id="be4cb-146">If you are using Windows-based SKUs, follow hello suggested links tooacquire hello approved versions of Windows Server.</span></span>

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a><span data-ttu-id="be4cb-147">2.建立與 Azure 相容的 VHD (以 Linux 為基礎)</span><span class="sxs-lookup"><span data-stu-id="be4cb-147">2. Create an Azure-compatible VHD (Linux-based)</span></span>
<span data-ttu-id="be4cb-148">本節著重於建立以 Linux 為基礎的 VM 映像的 hello Azure Marketplace 的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="be4cb-148">This section focuses on best practices for creating a Linux-based VM image for hello Azure Marketplace.</span></span> <span data-ttu-id="be4cb-149">逐步解說中，請參閱下列文件的 toohello:[建立及上傳的虛擬硬碟包含 hello Linux 作業系統](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="be4cb-149">For a step-by-step walkthrough, refer toohello following documentation: [Creating and Uploading a Virtual Hard Disk that Contains hello Linux Operating System](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a><span data-ttu-id="be4cb-150">3.建立與 Azure 相容的 VHD (以 Windows 為基礎)</span><span class="sxs-lookup"><span data-stu-id="be4cb-150">3. Create an Azure-compatible VHD (Windows-based)</span></span>
<span data-ttu-id="be4cb-151">本節著重於 hello 步驟 toocreate 根據 Windows Server hello Azure Marketplace 的 SKU。</span><span class="sxs-lookup"><span data-stu-id="be4cb-151">This section focuses on hello steps toocreate a SKU based on Windows Server for hello Azure Marketplace.</span></span>

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a><span data-ttu-id="be4cb-152">3.1 請確定您使用 hello 更正基底 Vhd</span><span class="sxs-lookup"><span data-stu-id="be4cb-152">3.1 Ensure that you are using hello correct base VHDs</span></span>
<span data-ttu-id="be4cb-153">hello 作業系統 VHD 為 VM 映像必須使用 Azure 核准基底映像包含 Windows Server 或 SQL Server 為基礎。</span><span class="sxs-lookup"><span data-stu-id="be4cb-153">hello operating system VHD for your VM image must be based on an Azure-approved base image that contains Windows Server or SQL Server.</span></span>

<span data-ttu-id="be4cb-154">toobegin，從下列映像，位於 hello hello 建立 VM [Microsoft Azure 入口網站][link-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="be4cb-154">toobegin, create a VM from one of hello following images, located at hello [Microsoft Azure portal][link-azure-portal]:</span></span>

* <span data-ttu-id="be4cb-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2]、[2012 Datacenter][link-datactr-2012]、[2008 R2 SP1][link-datactr-2008-r2])</span><span class="sxs-lookup"><span data-stu-id="be4cb-155">Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])</span></span>
* <span data-ttu-id="be4cb-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent]、[Standard][link-sql-2014-std]、[Web][link-sql-2014-web])</span><span class="sxs-lookup"><span data-stu-id="be4cb-156">SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])</span></span>
* <span data-ttu-id="be4cb-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent]、[Standard][link-sql-2012-std]、[Web][link-sql-2012-web])</span><span class="sxs-lookup"><span data-stu-id="be4cb-157">SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])</span></span>

<span data-ttu-id="be4cb-158">也可以在 hello SKU 頁面下方的 hello 發佈入口網站中找到這些連結。</span><span class="sxs-lookup"><span data-stu-id="be4cb-158">These links can also be found in hello Publishing Portal under hello SKU page.</span></span>

> [!TIP]
> <span data-ttu-id="be4cb-159">如果您使用 hello 目前的 Azure 入口網站或 PowerShell，會核准已於 2014 年 9 月 8 日發行及更新版本的 Windows Server 映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-159">If you are using hello current Azure portal or PowerShell, Windows Server images published on September 8, 2014 and later are approved.</span></span>
>
>

### <a name="32-create-your-windows-based-vm"></a><span data-ttu-id="be4cb-160">3.2 建立您的 Windows 型 VM</span><span class="sxs-lookup"><span data-stu-id="be4cb-160">3.2 Create your Windows-based VM</span></span>
<span data-ttu-id="be4cb-161">從 hello Microsoft Azure 入口網站，您可以建立您只需要幾個簡單步驟中的核准基底映像為基礎的 VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-161">From hello Microsoft Azure portal, you can create your VM based on an approved base image in just a few simple steps.</span></span> <span data-ttu-id="be4cb-162">hello 下面是 hello 程序的概觀：</span><span class="sxs-lookup"><span data-stu-id="be4cb-162">hello following is an overview of hello process:</span></span>

1. <span data-ttu-id="be4cb-163">從 hello 基底映像 頁面上，選取**建立虛擬機器**toobe 導向 toohello 新[Microsoft Azure 入口網站][link-azure-portal]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-163">From hello base image page, select **Create Virtual Machine** toobe directed toohello new [Microsoft Azure portal][link-azure-portal].</span></span>

    ![繪圖][img-acom-1]
2. <span data-ttu-id="be4cb-165">登入 toohello 入口網站以 hello Microsoft 帳戶和 hello 想 toouse 的 Azure 訂用帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-165">Sign in toohello portal with hello Microsoft account and password for hello Azure subscription you want toouse.</span></span>
3. <span data-ttu-id="be4cb-166">使用您已選取 hello 基底映像，請遵循 hello 提示 toocreate VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-166">Follow hello prompts toocreate a VM by using hello base image you have selected.</span></span> <span data-ttu-id="be4cb-167">您的主機名稱 （hello 電腦名稱）、 （系統管理員身分註冊），使用者名稱和密碼需要 tooprovide hello VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-167">You need tooprovide a host name (name of hello computer), user name (registered as an administrator), and password for hello VM.</span></span>

    ![繪圖][img-portal-vm-create]
4. <span data-ttu-id="be4cb-169">選取 hello VM toodeploy hello 大小：</span><span class="sxs-lookup"><span data-stu-id="be4cb-169">Select hello size of hello VM toodeploy:</span></span>

    <span data-ttu-id="be4cb-170">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-170">a.</span></span>    <span data-ttu-id="be4cb-171">如果您計劃 toodevelop hello VHD 在內部，hello 大小並不重要。</span><span class="sxs-lookup"><span data-stu-id="be4cb-171">If you plan toodevelop hello VHD on-premises, hello size does not matter.</span></span> <span data-ttu-id="be4cb-172">請考慮使用 hello 其中較小的 Vm。</span><span class="sxs-lookup"><span data-stu-id="be4cb-172">Consider using one of hello smaller VMs.</span></span>

    <span data-ttu-id="be4cb-173">b.</span><span class="sxs-lookup"><span data-stu-id="be4cb-173">b.</span></span>    <span data-ttu-id="be4cb-174">如果您計劃 Azure 中的 toodevelop hello 映像，請考慮使用其中一種 hello 建議 hello 選映像的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="be4cb-174">If you plan toodevelop hello image in Azure, consider using one of hello recommended VM sizes for hello selected image.</span></span>

    <span data-ttu-id="be4cb-175">c.</span><span class="sxs-lookup"><span data-stu-id="be4cb-175">c.</span></span>    <span data-ttu-id="be4cb-176">如需定價資訊，請參閱 toohello**建議定價層**hello 入口網站上顯示的選取器。</span><span class="sxs-lookup"><span data-stu-id="be4cb-176">For pricing information, refer toohello **Recommended pricing tiers** selector displayed on hello portal.</span></span> <span data-ttu-id="be4cb-177">它會提供 hello hello 發行者所提供的三種建議的大小。</span><span class="sxs-lookup"><span data-stu-id="be4cb-177">It will provide hello three recommended sizes provided by hello publisher.</span></span> <span data-ttu-id="be4cb-178">（在此情況下，hello 發行者是 Microsoft）。</span><span class="sxs-lookup"><span data-stu-id="be4cb-178">(In this case, hello publisher is Microsoft.)</span></span>

    ![繪圖][img-portal-vm-size]
5. <span data-ttu-id="be4cb-180">設定屬性：</span><span class="sxs-lookup"><span data-stu-id="be4cb-180">Set properties:</span></span>

    <span data-ttu-id="be4cb-181">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-181">a.</span></span>    <span data-ttu-id="be4cb-182">針對快速部署，您可以保留 hello hello 屬性底下的預設值**選擇性組態**和**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-182">For quick deployment, you can leave hello default values for hello properties under **Optional Configuration** and **Resource Group**.</span></span>

    <span data-ttu-id="be4cb-183">b.</span><span class="sxs-lookup"><span data-stu-id="be4cb-183">b.</span></span>    <span data-ttu-id="be4cb-184">在下**儲存體帳戶**，您可以選擇性地選取 VHD 儲存在作業系統的 hello hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="be4cb-184">Under **Storage Account**, you can optionally select hello storage account in which hello operating system VHD will be stored.</span></span>

    <span data-ttu-id="be4cb-185">c.</span><span class="sxs-lookup"><span data-stu-id="be4cb-185">c.</span></span>    <span data-ttu-id="be4cb-186">在下**資源群組**，您可以選擇性地選取 hello 中哪些 tooplace hello VM 的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="be4cb-186">Under **Resource Group**, you can optionally select hello logical group in which tooplace hello VM.</span></span>
6. <span data-ttu-id="be4cb-187">選取 hello**位置**部署：</span><span class="sxs-lookup"><span data-stu-id="be4cb-187">Select hello **Location** for deployment:</span></span>

    <span data-ttu-id="be4cb-188">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-188">a.</span></span>    <span data-ttu-id="be4cb-189">如果您計劃 toodevelop hello VHD 在內部部署，因為您稍後將上傳 hello 映像 tooAzure，並不重要 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="be4cb-189">If you plan toodevelop hello VHD on-premises, hello location does not matter because you will upload hello image tooAzure later.</span></span>

    <span data-ttu-id="be4cb-190">b.</span><span class="sxs-lookup"><span data-stu-id="be4cb-190">b.</span></span>    <span data-ttu-id="be4cb-191">如果您計劃 Azure 中的 toodevelop hello 映像，請考慮使用其中一種從 hello 開頭的 hello 美國為基礎的 Microsoft Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="be4cb-191">If you plan toodevelop hello image in Azure, consider using one of hello US-based Microsoft Azure regions from hello beginning.</span></span> <span data-ttu-id="be4cb-192">這可加速 hello VHD 複製程序，Microsoft 會代替您執行，當您送出您的映像的憑證。</span><span class="sxs-lookup"><span data-stu-id="be4cb-192">This speeds up hello VHD copying process that Microsoft performs on your behalf when you submit your image for certification.</span></span>

    ![繪圖][img-portal-vm-location]
7. <span data-ttu-id="be4cb-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="be4cb-194">Click **Create**.</span></span> <span data-ttu-id="be4cb-195">hello VM 啟動 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="be4cb-195">hello VM starts toodeploy.</span></span> <span data-ttu-id="be4cb-196">分鐘內，您可以成功部署，而且您 sku 就可以開始 toocreate hello 映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-196">Within minutes, you will have a successful deployment and can begin toocreate hello image for your SKU.</span></span>

### <a name="33-develop-your-vhd-in-hello-cloud"></a><span data-ttu-id="be4cb-197">3.3 開發您的 VHD hello 雲端中</span><span class="sxs-lookup"><span data-stu-id="be4cb-197">3.3 Develop your VHD in hello cloud</span></span>
<span data-ttu-id="be4cb-198">我們強烈建議您在使用遠端桌面通訊協定 (RDP) 來開發您 hello 雲端中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="be4cb-198">We strongly recommend that you develop your VHD in hello cloud by using Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="be4cb-199">您可以連接 tooRDP 與佈建期間指定 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-199">You connect tooRDP with hello user name and password specified during provisioning.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be4cb-200">如果您開發 VHD 內部部署 (不建議)，請參閱 [建立虛擬機器映像內部部署](marketplace-publishing-vm-image-creation-on-premise.md)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-200">If you develop your VHD on-premises (which is not recommended), see [Creating a virtual machine image on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span> <span data-ttu-id="be4cb-201">下載您的 VHD 不需要，如果您正在開發 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="be4cb-201">Downloading your VHD is not necessary if you are developing in hello cloud.</span></span>
>
>

<span data-ttu-id="be4cb-202">**透過使用 hello 的 RDP 連線[Microsoft Azure 入口網站][link-azure-portal]**</span><span class="sxs-lookup"><span data-stu-id="be4cb-202">**Connect via RDP using hello [Microsoft Azure portal][link-azure-portal]**</span></span>

1. <span data-ttu-id="be4cb-203">選取 [瀏覽] > [VM]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-203">Select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="be4cb-204">hello 虛擬機器刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-204">hello Virtual machines blade opens.</span></span> <span data-ttu-id="be4cb-205">請確定該 hello 想與 tooconnect 的 VM 正在執行，然後再從已部署的 Vm hello 清單中選取。</span><span class="sxs-lookup"><span data-stu-id="be4cb-205">Ensure that hello VM that you want tooconnect with is running, and then select it from hello list of deployed VMs.</span></span>
3. <span data-ttu-id="be4cb-206">描述 hello 刀鋒視窗中開啟選取的 VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-206">A blade opens that describes hello selected VM.</span></span> <span data-ttu-id="be4cb-207">在 hello 頂端，按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-207">At hello top, click **Connect**.</span></span>
4. <span data-ttu-id="be4cb-208">您會提示的 tooenter hello 使用者名稱和您在佈建期間指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-208">You are prompted tooenter hello user name and password that you specified during provisioning.</span></span>

<span data-ttu-id="be4cb-209">**使用 PowerShell，透過 RDP 連接**</span><span class="sxs-lookup"><span data-stu-id="be4cb-209">**Connect via RDP using PowerShell**</span></span>

<span data-ttu-id="be4cb-210">toodownload 遠端桌面檔案 tooa 本機電腦，使用 hello [Get-azureremotedesktopfile cmdlet][link-technet-2]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-210">toodownload a remote desktop file tooa local machine, use hello [Get-AzureRemoteDesktopFile cmdlet][link-technet-2].</span></span> <span data-ttu-id="be4cb-211">在順序 toouse 這個指令程式，您需要 tooknow hello hello 服務名稱和 hello VM 的名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-211">In order toouse this cmdlet, you need tooknow hello name of hello service and name of hello VM.</span></span> <span data-ttu-id="be4cb-212">如果您從 hello 建立 hello VM [Microsoft Azure 入口網站][link-azure-portal]，您可以找到此資訊在 VM 屬性：</span><span class="sxs-lookup"><span data-stu-id="be4cb-212">If you created hello VM from hello [Microsoft Azure portal][link-azure-portal], you can find this information under VM properties:</span></span>

1. <span data-ttu-id="be4cb-213">在 hello Microsoft Azure 入口網站中，選取 **瀏覽** > **Vm**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-213">In hello Microsoft Azure portal, select **Browse** > **VMs**.</span></span>
2. <span data-ttu-id="be4cb-214">hello 虛擬機器刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-214">hello Virtual machines blade opens.</span></span> <span data-ttu-id="be4cb-215">選取 hello 您部署的 VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-215">Select hello VM that you deployed.</span></span>
3. <span data-ttu-id="be4cb-216">描述 hello 刀鋒視窗中開啟選取的 VM。</span><span class="sxs-lookup"><span data-stu-id="be4cb-216">A blade opens that describes hello selected VM.</span></span>
4. <span data-ttu-id="be4cb-217">按一下 [內容] 。</span><span class="sxs-lookup"><span data-stu-id="be4cb-217">Click **Properties**.</span></span>
5. <span data-ttu-id="be4cb-218">hello hello 網域名稱的第一個部分是 hello 服務名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-218">hello first portion of hello domain name is hello service name.</span></span> <span data-ttu-id="be4cb-219">hello 主機名稱是 hello VM 名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-219">hello host name is hello VM name.</span></span>

    ![繪圖][img-portal-vm-rdp]
6. <span data-ttu-id="be4cb-221">如下所示為 hello cmdlet toodownload hello RDP 檔案建立 hello VM toohello 系統管理員的本機桌面。</span><span class="sxs-lookup"><span data-stu-id="be4cb-221">hello cmdlet toodownload hello RDP file for hello created VM toohello administrator's local desktop is as follows.</span></span>

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

<span data-ttu-id="be4cb-222">RDP 的詳細資訊可以在 hello 文章中找到 MSDN 上[透過 RDP 或 SSH 連接 tooan Azure VM](http://msdn.microsoft.com/library/azure/dn535788.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-222">More information about RDP can be found on MSDN in hello article [Connect tooan Azure VM with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).</span></span>

<span data-ttu-id="be4cb-223">**設定 VM 並建立您的 SKU**</span><span class="sxs-lookup"><span data-stu-id="be4cb-223">**Configure a VM and create your SKU**</span></span>

<span data-ttu-id="be4cb-224">下載 VHD hello 作業系統之後, 使用 HyperV 並設定建立您的 SKU VM toobegin。</span><span class="sxs-lookup"><span data-stu-id="be4cb-224">After hello operating system VHD is downloaded, use Hyper­V and configure a VM toobegin creating your SKU.</span></span> <span data-ttu-id="be4cb-225">詳細的步驟，請參閱下列 TechNet 連結 hello:[安裝 HyperV 和設定 VM](http://technet.microsoft.com/library/hh846766.aspx)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-225">Detailed steps can be found at hello following TechNet link: [Install Hyper­V and Configure a VM](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="34-choose-hello-correct-vhd-size"></a><span data-ttu-id="be4cb-226">3.4 選擇 hello 正確的 VHD 大小</span><span class="sxs-lookup"><span data-stu-id="be4cb-226">3.4 Choose hello correct VHD size</span></span>
<span data-ttu-id="be4cb-227">hello Windows 作業系統 VHD VM 映像中應該建立為 128 GB 的固定格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="be4cb-227">hello Windows operating system VHD in your VM image should be created as a 128-GB fixed-format VHD.</span></span>  

<span data-ttu-id="be4cb-228">如果 hello 實體大小小於 128 GB，hello VHD 應該為疏鬆。</span><span class="sxs-lookup"><span data-stu-id="be4cb-228">If hello physical size is less than 128 GB, hello VHD should be sparse.</span></span> <span data-ttu-id="be4cb-229">hello 基底 Windows 和 SQL Server 提供的映像已經符合這些需求，因此不會變更的 hello VHD 取得 hello 格式或 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="be4cb-229">hello base Windows and SQL Server images provided already meet these requirements, so do not change hello format or hello size of hello VHD obtained.</span></span>  

<span data-ttu-id="be4cb-230">資料磁碟的大小可高達 1 TB。</span><span class="sxs-lookup"><span data-stu-id="be4cb-230">Data disks can be as large as 1 TB.</span></span> <span data-ttu-id="be4cb-231">決定時 hello 磁碟大小，請記住，客戶無法調整大小 Vhd 映像內部署的 hello 次。</span><span class="sxs-lookup"><span data-stu-id="be4cb-231">When deciding on hello disk size, remember that customers cannot resize VHDs within an image at hello time of deployment.</span></span> <span data-ttu-id="be4cb-232">資料磁碟 VHD 應建立為固定格式 VHD。</span><span class="sxs-lookup"><span data-stu-id="be4cb-232">Data disk VHDs should be created as a fixed-format VHD.</span></span> <span data-ttu-id="be4cb-233">也可以是疏鬆 VHD。</span><span class="sxs-lookup"><span data-stu-id="be4cb-233">They should also be sparse.</span></span> <span data-ttu-id="be4cb-234">資料磁碟可以空白或包含資料。</span><span class="sxs-lookup"><span data-stu-id="be4cb-234">Data disks can be empty or contain data.</span></span>

### <a name="35-install-hello-latest-windows-patches"></a><span data-ttu-id="be4cb-235">3.5 安裝 hello 最新 Windows 修補程式</span><span class="sxs-lookup"><span data-stu-id="be4cb-235">3.5 Install hello latest Windows patches</span></span>
<span data-ttu-id="be4cb-236">hello 基底映像包含最新修補程式 hello 向上 tootheir 發行日期。</span><span class="sxs-lookup"><span data-stu-id="be4cb-236">hello base images contain hello latest patches up tootheir published date.</span></span> <span data-ttu-id="be4cb-237">之前發行 hello 作業系統已建立的 VHD，請確定已經執行的 Windows Update 以及所有 hello 最新重大，和已安裝重要的安全性更新。</span><span class="sxs-lookup"><span data-stu-id="be4cb-237">Before publishing hello operating system VHD you have created, ensure that Windows Update has been run and that all hello latest Critical and Important security updates have been installed.</span></span>

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a><span data-ttu-id="be4cb-238">3.6 必要時執行其他設定並排程工作</span><span class="sxs-lookup"><span data-stu-id="be4cb-238">3.6 Perform additional configuration and schedule tasks as necessary</span></span>
<span data-ttu-id="be4cb-239">如果需要進行其他設定，請考慮使用排定的工作後，在執行啟動 toomake 在任何最後的變更 toohello VM 已部署：</span><span class="sxs-lookup"><span data-stu-id="be4cb-239">If additional configuration is needed, consider using a scheduled task that runs at startup toomake any final changes toohello VM after it has been deployed:</span></span>

* <span data-ttu-id="be4cb-240">它是最佳的作法 toohave hello 工作本身成功執行後刪除。</span><span class="sxs-lookup"><span data-stu-id="be4cb-240">It is a best practice toohave hello task delete itself upon successful execution.</span></span>
* <span data-ttu-id="be4cb-241">沒有設定應依賴 C 或 D 磁碟機以外的磁碟機，因為它們永遠會保證 tooexist hello 只有兩個磁碟機。</span><span class="sxs-lookup"><span data-stu-id="be4cb-241">No configuration should rely on drives other than drives C or D, because these are hello only two drives that are always guaranteed tooexist.</span></span> <span data-ttu-id="be4cb-242">磁碟機 C 是 hello 作業系統磁碟，以及磁碟機 D 是 hello 暫存本機磁碟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-242">Drive C is hello operating system disk, and drive D is hello temporary local disk.</span></span>

### <a name="37-generalize-hello-image"></a><span data-ttu-id="be4cb-243">3.7 hello 映像一般化</span><span class="sxs-lookup"><span data-stu-id="be4cb-243">3.7 Generalize hello image</span></span>
<span data-ttu-id="be4cb-244">Hello Azure Marketplace 中的所有映像必須是可重複使用，以一般方式。</span><span class="sxs-lookup"><span data-stu-id="be4cb-244">All images in hello Azure Marketplace must be reusable in a generic fashion.</span></span> <span data-ttu-id="be4cb-245">換句話說，必須先一般化 hello 作業系統 VHD:</span><span class="sxs-lookup"><span data-stu-id="be4cb-245">In other words, hello operating system VHD must be generalized:</span></span>

* <span data-ttu-id="be4cb-246">適用於 Windows、 hello 映像應該是 「 已執行 sysprep，"，而且沒有組態應該不支援 hello **sysprep**命令。</span><span class="sxs-lookup"><span data-stu-id="be4cb-246">For Windows, hello image should be "sysprepped," and no configurations should be done that do not support hello **sysprep** command.</span></span>
* <span data-ttu-id="be4cb-247">您可以執行下列命令從 hello 目錄 windir%\System32\Sysprep hello。</span><span class="sxs-lookup"><span data-stu-id="be4cb-247">You can run hello following command from hello directory %windir%\System32\Sysprep.</span></span>

        sysprep.exe /generalize /oobe /shutdown

  <span data-ttu-id="be4cb-248">Toosysprep hello 作業系統如何在下列 MSDN 文章 hello 的步驟中提供的指引：[建立並上傳 Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-248">Guidance on how toosysprep hello operating system is provided in Step of hello following MSDN article: [Create and upload a Windows Server VHD tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="4-deploy-a-vm-from-your-vhds"></a><span data-ttu-id="be4cb-249">4.從您的 VHD 部署 VM</span><span class="sxs-lookup"><span data-stu-id="be4cb-249">4. Deploy a VM from your VHDs</span></span>
<span data-ttu-id="be4cb-250">您已上傳您的 Vhd （hello 一般化作業系統 VHD 和零個或多個資料磁碟 Vhd） 之後 tooan Azure 儲存體帳戶，您可以註冊他們的使用者 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-250">After you have uploaded your VHDs (hello generalized operating system VHD and zero or more data disk VHDs) tooan Azure storage account, you can register them as a user VM image.</span></span> <span data-ttu-id="be4cb-251">您可以接著測試該映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-251">Then you can test that image.</span></span> <span data-ttu-id="be4cb-252">注意，因為您的作業系統 VHD 經過一般化後，您無法直接部署 hello VM 提供 hello VHD URL。</span><span class="sxs-lookup"><span data-stu-id="be4cb-252">Note that because your operating system VHD is generalized, you cannot directly deploy hello VM by providing hello VHD URL.</span></span>

<span data-ttu-id="be4cb-253">toolearn 更多關於 VM 映像，檢閱 hello 下列部落格文章：</span><span class="sxs-lookup"><span data-stu-id="be4cb-253">toolearn more about VM images, review hello following blog posts:</span></span>

* [<span data-ttu-id="be4cb-254">VM 映像</span><span class="sxs-lookup"><span data-stu-id="be4cb-254">VM Image</span></span>](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [<span data-ttu-id="be4cb-255">VM 映像 PowerShell 如何</span><span class="sxs-lookup"><span data-stu-id="be4cb-255">VM Image PowerShell How To</span></span>](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [<span data-ttu-id="be4cb-256">關於 Azure 中的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="be4cb-256">About VM images in Azure</span></span>](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a><span data-ttu-id="be4cb-257">Hello 必要工具、 PowerShell 和 Azure CLI 設定</span><span class="sxs-lookup"><span data-stu-id="be4cb-257">Set up hello necessary tools, PowerShell and Azure CLI</span></span>
* [<span data-ttu-id="be4cb-258">如何 toosetup PowerShell</span><span class="sxs-lookup"><span data-stu-id="be4cb-258">How toosetup PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="be4cb-259">如何 toosetup Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be4cb-259">How toosetup Azure CLI</span></span>](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a><span data-ttu-id="be4cb-260">4.1 建立使用者 VM 映像</span><span class="sxs-lookup"><span data-stu-id="be4cb-260">4.1 Create a user VM image</span></span>
#### <a name="capture-vm"></a><span data-ttu-id="be4cb-261">擷取 VM</span><span class="sxs-lookup"><span data-stu-id="be4cb-261">Capture VM</span></span>
<span data-ttu-id="be4cb-262">請閱讀下面提供的指引擷取 hello VM 使用 API/PowerShell Azure CLI 的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="be4cb-262">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="be4cb-263">API</span><span class="sxs-lookup"><span data-stu-id="be4cb-263">API</span></span>](https://msdn.microsoft.com/library/mt163560.aspx)
* [<span data-ttu-id="be4cb-264">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be4cb-264">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="be4cb-265">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be4cb-265">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a><span data-ttu-id="be4cb-266">一般化映像</span><span class="sxs-lookup"><span data-stu-id="be4cb-266">Generalize Image</span></span>
<span data-ttu-id="be4cb-267">請閱讀下面提供的指引擷取 hello VM 使用 API/PowerShell Azure CLI 的 hello 連結。</span><span class="sxs-lookup"><span data-stu-id="be4cb-267">Please read hello links given below for guidance on capturing hello VM using API/PowerShell/Azure CLI.</span></span>

* [<span data-ttu-id="be4cb-268">API</span><span class="sxs-lookup"><span data-stu-id="be4cb-268">API</span></span>](https://msdn.microsoft.com/library/mt269439.aspx)
* [<span data-ttu-id="be4cb-269">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be4cb-269">PowerShell</span></span>](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="be4cb-270">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be4cb-270">Azure CLI</span></span>](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a><span data-ttu-id="be4cb-271">4.2 從使用者 VM 映像部署 VM</span><span class="sxs-lookup"><span data-stu-id="be4cb-271">4.2 Deploy a VM from a user VM image</span></span>
<span data-ttu-id="be4cb-272">toodeploy 將 VM 從使用者 VM 映像，您可以使用目前的 hello [Azure 入口網站](https://manage.windowsazure.com)或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="be4cb-272">toodeploy a VM from a user VM image, you can use hello current [Azure portal](https://manage.windowsazure.com) or PowerShell.</span></span>

<span data-ttu-id="be4cb-273">**從 hello 目前的 Azure 入口網站部署 VM**</span><span class="sxs-lookup"><span data-stu-id="be4cb-273">**Deploy a VM from hello current Azure portal**</span></span>

1. <span data-ttu-id="be4cb-274">跳過**新增** > **計算** > **虛擬機器** > **從組件庫**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-274">Go too**New** > **Compute** > **Virtual machine** > **From gallery**.</span></span>

    ![繪圖][img-manage-vm-new]
2. <span data-ttu-id="be4cb-276">跳過**我的映像**，，然後選取會 hello VM 映像從哪些 toodeploy VM:</span><span class="sxs-lookup"><span data-stu-id="be4cb-276">Go too**My images**, and then select hello VM image from which toodeploy a VM:</span></span>

   1. <span data-ttu-id="be4cb-277">請特別注意 toowhich 映像選取，因為 hello**我的映像**檢視會列出作業系統映像和 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-277">Pay close attention toowhich image you select, because hello **My images** view lists both operating system images and VM images.</span></span>
   2. <span data-ttu-id="be4cb-278">查看 hello 磁碟數目，有助於判斷您部署的映像類型，因為 hello 多數的 VM 映像具有多個磁碟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-278">Looking at hello number of disks can help determine what type of image you are deploying, because hello majority of VM images have more than one disk.</span></span> <span data-ttu-id="be4cb-279">但是，所以仍有可能 toohave 只有一個單一的作業系統磁碟，就必須使用的 VM 映像**的磁碟數目**設定 too1。</span><span class="sxs-lookup"><span data-stu-id="be4cb-279">However, it is still possible toohave a VM image with only a single operating system disk, which would then have **Number of disks** set too1.</span></span>

      ![繪圖][img-manage-vm-select]
3. <span data-ttu-id="be4cb-281">遵循 hello VM 建立精靈，並指定 hello VM 名稱、 VM 大小、 位置、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-281">Follow hello VM creation wizard and specify hello VM name, VM size, location, user name, and password.</span></span>

<span data-ttu-id="be4cb-282">**從 PowerShell 部署 VM**</span><span class="sxs-lookup"><span data-stu-id="be4cb-282">**Deploy a VM from PowerShell**</span></span>

<span data-ttu-id="be4cb-283">toodeploy hello 從大型 VM 一般化剛才建立的 VM 映像，您可以使用下列 cmdlet 的 hello。</span><span class="sxs-lookup"><span data-stu-id="be4cb-283">toodeploy a large VM from hello generalized VM image just created, you can use hello following cmdlets.</span></span>

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> <span data-ttu-id="be4cb-284">如需其他協助，請參閱 [針對 VHD 建立常見問題進行疑難排解]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-284">Please refer [Troubleshooting common issues encountered during VHD creation] for additional assistance.</span></span>
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a><span data-ttu-id="be4cb-285">5.取得 VM 映像的認證</span><span class="sxs-lookup"><span data-stu-id="be4cb-285">5. Obtain certification for your VM image</span></span>
<span data-ttu-id="be4cb-286">hello VM 映像的準備 hello Azure Marketplace 中的下一個步驟是的 toohave 其認證。</span><span class="sxs-lookup"><span data-stu-id="be4cb-286">hello next step in preparing your VM image for hello Azure Marketplace is toohave it certified.</span></span>

<span data-ttu-id="be4cb-287">此程序包括執行特殊的憑證 」 工具上, 傳 hello 驗證結果 toohello Azure Vhd 所在的容器、 加入提供項目、 定義您 SKU 和送出您的 VM 映像的憑證。</span><span class="sxs-lookup"><span data-stu-id="be4cb-287">This process includes running a special certification tool, uploading hello verification results toohello Azure container where your VHDs reside, adding an offer, defining your SKU, and submitting your VM image for certification.</span></span>

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a><span data-ttu-id="be4cb-288">5.1 下載並執行的 Azure 認證的 hello 憑證測試工具</span><span class="sxs-lookup"><span data-stu-id="be4cb-288">5.1 Download and run hello Certification Test Tool for Azure Certified</span></span>
<span data-ttu-id="be4cb-289">hello 憑證工具在執行中的 VM，佈建使用者的 VM 映像上執行，hello VM 映像的 tooensure 與 Microsoft Azure 相容。</span><span class="sxs-lookup"><span data-stu-id="be4cb-289">hello certification tool runs on a running VM, provisioned from your user VM image, tooensure that hello VM image is compatible with Microsoft Azure.</span></span> <span data-ttu-id="be4cb-290">它會確認 hello 指引和需求的相關準備您的 VHD 符合。</span><span class="sxs-lookup"><span data-stu-id="be4cb-290">It will verify that hello guidance and requirements about preparing your VHD have been met.</span></span> <span data-ttu-id="be4cb-291">hello 工具 hello 輸出是相容性報告，應在 hello 發佈入口網站時提出要求的憑證上傳。</span><span class="sxs-lookup"><span data-stu-id="be4cb-291">hello output of hello tool is a compatibility report, which should be uploaded on hello Publishing Portal while requesting certification.</span></span>

<span data-ttu-id="be4cb-292">hello 憑證 」 工具可以搭配 Windows 和 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="be4cb-292">hello certification tool can be used with both Windows and Linux VMs.</span></span> <span data-ttu-id="be4cb-293">它會連接透過 PowerShell tooWindows 為基礎的 Vm，並連接透過 SSH.Net tooLinux Vm:</span><span class="sxs-lookup"><span data-stu-id="be4cb-293">It connects tooWindows-based VMs via PowerShell and connects tooLinux VMs via SSH.Net:</span></span>

1. <span data-ttu-id="be4cb-294">首先，下載 hello 憑證 」 工具在 hello [Microsoft 下載網站][link-msft-download]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-294">First, download hello certification tool at hello [Microsoft download site][link-msft-download].</span></span>
2. <span data-ttu-id="be4cb-295">開啟 hello 憑證 」 工具，然後再按一下 [hello**啟動新的測試**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="be4cb-295">Open hello certification tool, and then click hello **Start New Test** button.</span></span>
3. <span data-ttu-id="be4cb-296">從 hello**測試資訊**畫面上，輸入 hello 測試回合的名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-296">From hello **Test Information** screen, enter a name for hello test run.</span></span>
4. <span data-ttu-id="be4cb-297">選擇您的 VM 位於 Linux 或 Windows。</span><span class="sxs-lookup"><span data-stu-id="be4cb-297">Choose whether your VM is on Linux or Windows.</span></span> <span data-ttu-id="be4cb-298">根據選擇的方法，請選取 hello 後續的選項。</span><span class="sxs-lookup"><span data-stu-id="be4cb-298">Depending on which you choose, select hello subsequent options.</span></span>

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a><span data-ttu-id="be4cb-299">**連接 hello 憑證工具 tooa Linux VM 映像**</span><span class="sxs-lookup"><span data-stu-id="be4cb-299">**Connect hello certification tool tooa Linux VM image**</span></span>
1. <span data-ttu-id="be4cb-300">選取 hello SSH 驗證模式： 密碼或金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="be4cb-300">Select hello SSH authentication mode: password or key file.</span></span>
2. <span data-ttu-id="be4cb-301">如果使用密碼型驗證，請輸入 hello 網域名稱系統 (DNS) 名稱、 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-301">If using password-­based authentication, enter hello Domain Name System (DNS) name, user name, and password.</span></span>
3. <span data-ttu-id="be4cb-302">如果使用金鑰檔的驗證，請輸入 hello DNS 名稱、 使用者名稱和私用金鑰的位置。</span><span class="sxs-lookup"><span data-stu-id="be4cb-302">If using key file authentication, enter hello DNS name, user name, and private key location.</span></span>

   ![Linux VM 映像的密碼驗證][img-cert-vm-pswd-lnx]

   ![Linux VM 映像的金鑰檔案驗證][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a><span data-ttu-id="be4cb-305">**連接 hello 憑證工具 tooa windows VM 映像**</span><span class="sxs-lookup"><span data-stu-id="be4cb-305">**Connect hello certification tool tooa Windows-based VM image**</span></span>
1. <span data-ttu-id="be4cb-306">輸入完整的 hello VM DNS 名稱 (例如，MyVMName.Cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-306">Enter hello fully qualified VM DNS name (for example, MyVMName.Cloudapp.net).</span></span>
2. <span data-ttu-id="be4cb-307">輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-307">Enter hello user name and password.</span></span>

   ![Windows VM 映像的密碼驗證][img-cert-vm-pswd-win]

<span data-ttu-id="be4cb-309">您已選取正確的 hello 選項為 Linux 或 windows VM 映像之後，請選取**測試連接**tooensure SSH.Net 或 PowerShell 具有有效的連接，基於測試目的。</span><span class="sxs-lookup"><span data-stu-id="be4cb-309">After you have selected hello correct options for your Linux or Windows-based VM image, select **Test Connection** tooensure that SSH.Net or PowerShell has a valid connection for testing purposes.</span></span> <span data-ttu-id="be4cb-310">建立連接之後，請選取**下一步**toostart hello 測試。</span><span class="sxs-lookup"><span data-stu-id="be4cb-310">After a connection is established, select **Next** toostart hello test.</span></span>

<span data-ttu-id="be4cb-311">Hello 測試完成時，您會收到 hello 結果 （成功/失敗/警告） 的每個測試項目。</span><span class="sxs-lookup"><span data-stu-id="be4cb-311">When hello test is complete, you will receive hello results (Pass/Fail/Warning) for each test element.</span></span>

![Linux VM 映像的測試案例][img-cert-vm-test-lnx]

![Windows VM 映像的測試案例][img-cert-vm-test-win]

<span data-ttu-id="be4cb-314">如果任何 hello 測試失敗，未經過認證您的映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-314">If any of hello tests fail, your image will not be certified.</span></span> <span data-ttu-id="be4cb-315">如果發生這種情況，請檢閱 hello 需求，並進行任何必要的變更。</span><span class="sxs-lookup"><span data-stu-id="be4cb-315">If this occurs, review hello requirements and make any necessary changes.</span></span>

<span data-ttu-id="be4cb-316">Hello 自動化測試之後，系統會詢問 tooprovide 其他輸入您的 VM 映像，透過問卷螢幕上。</span><span class="sxs-lookup"><span data-stu-id="be4cb-316">After hello automated test, you are asked tooprovide additional input on your VM image via a questionnaire screen.</span></span>  <span data-ttu-id="be4cb-317">完成 hello 問題，然後選取 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-317">Complete hello questions, and then select **Next**.</span></span>

![認證工具問卷][img-cert-vm-questionnaire]

![認證工具問卷][img-cert-vm-questionnaire-2]

<span data-ttu-id="be4cb-320">Hello 問卷完成之後，您可以提供其他資訊，例如 hello Linux VM 映像的 SSH 存取資訊以及說明任何失敗的評估。</span><span class="sxs-lookup"><span data-stu-id="be4cb-320">After you have completed hello questionnaire, you can provide additional information such as SSH access information for hello Linux VM image and an explanation for any failed assessments.</span></span> <span data-ttu-id="be4cb-321">您可以下載 hello 測試結果中和記錄檔 hello 執行測試案例加入 tooyour 答案 toohello 問卷。</span><span class="sxs-lookup"><span data-stu-id="be4cb-321">You can download hello test results and log files for hello executed test cases in addition tooyour answers toohello questionnaire.</span></span> <span data-ttu-id="be4cb-322">將 hello 結果儲存在 hello 相同的容器，為您的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="be4cb-322">Save hello results in hello same container as your VHDs.</span></span>

![儲存認證測試結果][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a><span data-ttu-id="be4cb-324">5.2 會取得您的 VM 映像中的 hello 共用的存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="be4cb-324">5.2 Get hello shared access signature URI for your VM images</span></span>
<span data-ttu-id="be4cb-325">在發行程序 hello，您可以指定 hello 統一資源識別元 (Uri) 會導致 tooeach 的 hello 您已建立您的 sku 的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="be4cb-325">During hello publishing process, you specify hello uniform resource identifiers (URIs) that lead tooeach of hello VHDs you have created for your SKU.</span></span> <span data-ttu-id="be4cb-326">Microsoft hello 憑證程序期間需要存取 toothese Vhd。</span><span class="sxs-lookup"><span data-stu-id="be4cb-326">Microsoft needs access toothese VHDs during hello certification process.</span></span> <span data-ttu-id="be4cb-327">因此，您必須針對每個 VHD toocreate 共用的存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-327">Therefore, you need toocreate a shared access signature URI for each VHD.</span></span> <span data-ttu-id="be4cb-328">這是應該進入的 URI hello**映像**hello 發佈入口網站中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4cb-328">This is hello URI that should be entered in the **Images** tab in hello Publishing Portal.</span></span>

<span data-ttu-id="be4cb-329">hello 共用的存取簽章建立 URI 應該遵守 toohello 下列需求：</span><span class="sxs-lookup"><span data-stu-id="be4cb-329">hello shared access signature URI created should adhere toohello following requirements:</span></span>

* <span data-ttu-id="be4cb-330">為 VHD 產生共用存取簽章 URI 時，必須有足夠的列出和讀取權限。</span><span class="sxs-lookup"><span data-stu-id="be4cb-330">When generating shared access signature URIs for your VHDs, List and Read­ permissions are sufficient.</span></span> <span data-ttu-id="be4cb-331">不提供寫入或刪除存取權。</span><span class="sxs-lookup"><span data-stu-id="be4cb-331">Do not provide Write or Delete access.</span></span>
* <span data-ttu-id="be4cb-332">建立 hello 共用的存取簽章 URI 時 hello 持續時間的存取應該至少三 （3） 中的週。</span><span class="sxs-lookup"><span data-stu-id="be4cb-332">hello duration for access should be a minimum of three (3) weeks from when hello shared access signature URI is created.</span></span>
* <span data-ttu-id="be4cb-333">UTC 時間，hello 目前日期之前的選取 hello 天 toosafeguard。</span><span class="sxs-lookup"><span data-stu-id="be4cb-333">toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="be4cb-334">例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。</span><span class="sxs-lookup"><span data-stu-id="be4cb-334">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

<span data-ttu-id="be4cb-335">可以是 SAS URL 中產生多個方式 tooshare VHD Azure marketplace。</span><span class="sxs-lookup"><span data-stu-id="be4cb-335">SAS URL can be generated in multiple ways tooshare your VHD for Azure Marketplace.</span></span>
<span data-ttu-id="be4cb-336">下列是 hello 3 建議使用的工具：</span><span class="sxs-lookup"><span data-stu-id="be4cb-336">Following are hello 3 recommended tools:</span></span>

1.  <span data-ttu-id="be4cb-337">Azure 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="be4cb-337">Azure Storage Explorer</span></span>
2.  <span data-ttu-id="be4cb-338">Microsoft 儲存體總管</span><span class="sxs-lookup"><span data-stu-id="be4cb-338">Microsoft Storage Explorer</span></span>
3.  <span data-ttu-id="be4cb-339">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="be4cb-339">Azure CLI</span></span>

<span data-ttu-id="be4cb-340">**Azure 儲存體總管 (建議 Windows 使用者採用)**</span><span class="sxs-lookup"><span data-stu-id="be4cb-340">**Azure Storage Explorer (Recommended for Windows Users)**</span></span>

<span data-ttu-id="be4cb-341">下面是使用 Azure 儲存體總管來產生 SAS URL 的 hello 步驟</span><span class="sxs-lookup"><span data-stu-id="be4cb-341">Following are hello steps for generating SAS URL by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="be4cb-342">從 CodePlex 下載 [Azure 儲存體總管 6 預覽 3](https://azurestorageexplorer.codeplex.com/)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-342">Download [Azure Storage Explorer 6 Preview 3](https://azurestorageexplorer.codeplex.com/) from CodePlex.</span></span> <span data-ttu-id="be4cb-343">跳過[Azure 儲存體總管 6 預覽](https://azurestorageexplorer.codeplex.com/)按一下**「 下載 」**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-343">Go too[Azure Storage Explorer 6 Preview](https://azurestorageexplorer.codeplex.com/) and click **"Downloads"**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. <span data-ttu-id="be4cb-345">下載 [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668)，解壓縮之後安裝。</span><span class="sxs-lookup"><span data-stu-id="be4cb-345">Download [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) and install after unzipping it.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. <span data-ttu-id="be4cb-347">安裝之後，開啟 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be4cb-347">After it is installed, open hello application.</span></span>
4. <span data-ttu-id="be4cb-348">按一下 [加入帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="be4cb-348">Click **Add Account**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. <span data-ttu-id="be4cb-350">指定 hello 儲存體帳戶名稱、 儲存體帳戶金鑰，以及儲存體端點網域。</span><span class="sxs-lookup"><span data-stu-id="be4cb-350">Specify hello storage account name, storage account key, and storage endpoints domain.</span></span> <span data-ttu-id="be4cb-351">這是您 Azure 訂用帳戶中的 hello 儲存體帳戶，您已保留您的 VHD 在 Azure 入口網站上。</span><span class="sxs-lookup"><span data-stu-id="be4cb-351">This is hello storage account in your Azure subscription where you have kept your VHD on Azure portal.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. <span data-ttu-id="be4cb-353">一旦連線 Azure 儲存體總管 tooyour 特定儲存體帳戶，就會開始的顯示所有 hello 包含 hello 儲存體帳戶內。</span><span class="sxs-lookup"><span data-stu-id="be4cb-353">Once Azure Storage Explorer is connected tooyour specific storage account, it will start showing all of hello contains within hello storage account.</span></span> <span data-ttu-id="be4cb-354">選取您複製 hello 作業系統磁碟的 VHD 檔案 （也資料磁碟如果它們適用於您的案例） 的 hello 容器。</span><span class="sxs-lookup"><span data-stu-id="be4cb-354">Select hello container where you copied hello operating system disk VHD file (also data disks if they are applicable for your scenario).</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. <span data-ttu-id="be4cb-356">選取後 hello blob 容器，Azure 儲存體總管啟動 hello 容器內的顯示 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="be4cb-356">After selecting hello blob container, Azure Storage Explorer starts showing hello files within hello container.</span></span> <span data-ttu-id="be4cb-357">選取需要 toobe 送出的 hello 映像檔案 (.vhd)。</span><span class="sxs-lookup"><span data-stu-id="be4cb-357">Select hello image file (.vhd) that needs toobe submitted.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  <span data-ttu-id="be4cb-359">選取之後 hello.vhd 檔案 hello 容器中，按一下 hello**安全性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4cb-359">After selecting hello .vhd file in hello container, click hello **Security** tab.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  <span data-ttu-id="be4cb-361">在 hello **Blob 容器安全性**對話方塊中，保留 hello 的預設值在 hello**存取層級**索引標籤，然後再按一下**共用存取簽章** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4cb-361">In hello **Blob Container Security** dialog box, leave hello defaults on hello **Access Level** tab, and then click **Shared Access Signatures** tab.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. <span data-ttu-id="be4cb-363">請遵循下列 toogenerate hello.vhd 映像的共用的存取簽章 URI 的 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="be4cb-363">Follow hello steps below toogenerate a shared access signature URI for hello .vhd image:</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    <span data-ttu-id="be4cb-365">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-365">a.</span></span> <span data-ttu-id="be4cb-366">**從允許的存取：** toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。</span><span class="sxs-lookup"><span data-stu-id="be4cb-366">**Access permitted from:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="be4cb-367">例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。</span><span class="sxs-lookup"><span data-stu-id="be4cb-367">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="be4cb-368">b.</span><span class="sxs-lookup"><span data-stu-id="be4cb-368">b.</span></span> <span data-ttu-id="be4cb-369">**若要允許存取：**選取 hello 之後至少 3 週的日期**從允許存取**日期。</span><span class="sxs-lookup"><span data-stu-id="be4cb-369">**Access permitted to:** Select a date that is at least 3 weeks after hello **Access permitted from** date.</span></span>

    <span data-ttu-id="be4cb-370">c.</span><span class="sxs-lookup"><span data-stu-id="be4cb-370">c.</span></span> <span data-ttu-id="be4cb-371">**允許的動作：**選取 hello**清單**和**讀取**權限。</span><span class="sxs-lookup"><span data-stu-id="be4cb-371">**Actions permitted:** Select hello **List** and **Read** permissions.</span></span>

    <span data-ttu-id="be4cb-372">d.</span><span class="sxs-lookup"><span data-stu-id="be4cb-372">d.</span></span> <span data-ttu-id="be4cb-373">如果您已正確，選取.vhd 檔案，則您的檔案會出現在**Blob 名稱 tooaccess**與擴充功能的.vhd。</span><span class="sxs-lookup"><span data-stu-id="be4cb-373">If you have selected your .vhd file correctly, then your file appears in **Blob name tooaccess** with extension .vhd.</span></span>

    <span data-ttu-id="be4cb-374">e.</span><span class="sxs-lookup"><span data-stu-id="be4cb-374">e.</span></span> <span data-ttu-id="be4cb-375">按一下 [產生簽章]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-375">Click **Generate Signature**.</span></span>

    <span data-ttu-id="be4cb-376">f.</span><span class="sxs-lookup"><span data-stu-id="be4cb-376">f.</span></span> <span data-ttu-id="be4cb-377">在**產生共用存取簽章 URI 這個容器的**，hello 遵循以反白顯示上方的核取：</span><span class="sxs-lookup"><span data-stu-id="be4cb-377">In **Generated Shared Access Signature URI of this container**, check for hello following as highlighted above:</span></span>

       - <span data-ttu-id="be4cb-378">請確定您的映像檔案名稱和**".vhd"** hello URI 中。</span><span class="sxs-lookup"><span data-stu-id="be4cb-378">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
       - <span data-ttu-id="be4cb-379">結尾 hello hello 簽章，請確定**"= rl"**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-379">At hello end of hello signature, make sure that **"=rl"** appears.</span></span> <span data-ttu-id="be4cb-380">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="be4cb-380">This demonstrates that Read and List access was provided successfully.</span></span>
       - <span data-ttu-id="be4cb-381">Hello 簽章的中間，請確定**"sr-iov = c 」**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-381">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="be4cb-382">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="be4cb-382">This demonstrates that you have container level access</span></span>

11. <span data-ttu-id="be4cb-383">hello 的 tooensure 產生共用存取簽章 URI 如何運作，請按一下**瀏覽器中的測試**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-383">tooensure that hello generated shared access signature URI works, click **Test in Browser**.</span></span> <span data-ttu-id="be4cb-384">它應該開始 hello 下載程序。</span><span class="sxs-lookup"><span data-stu-id="be4cb-384">It should start hello download process.</span></span>

12. <span data-ttu-id="be4cb-385">將複製 hello 共用的存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-385">Copy hello shared access signature URI.</span></span> <span data-ttu-id="be4cb-386">這是將 URI toopaste hello 到 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="be4cb-386">This is hello URI toopaste into hello Publishing Portal.</span></span>

13. <span data-ttu-id="be4cb-387">針對每個 VHD hello SKU 中重複步驟 6-10。</span><span class="sxs-lookup"><span data-stu-id="be4cb-387">Repeat steps 6-10 for each VHD in hello SKU.</span></span>

<span data-ttu-id="be4cb-388">**Microsoft Azure 儲存體總管 (Windows/MAC/Linux)**</span><span class="sxs-lookup"><span data-stu-id="be4cb-388">**Microsoft Azure Storage Explorer (Windows/MAC/Linux)**</span></span>

<span data-ttu-id="be4cb-389">下面是使用 Microsoft Azure 儲存體總管來產生 SAS URL 的 hello 步驟</span><span class="sxs-lookup"><span data-stu-id="be4cb-389">Following are hello steps for generating SAS URL by using Microsoft Azure Storage Explorer</span></span>

1.  <span data-ttu-id="be4cb-390">從 [http://storageexplorer.com/](http://storageexplorer.com/) 網站下載 Microsoft Azure 儲存體總管。</span><span class="sxs-lookup"><span data-stu-id="be4cb-390">Download Microsoft Azure Storage Explorer form [http://storageexplorer.com/](http://storageexplorer.com/) website.</span></span> <span data-ttu-id="be4cb-391">跳過[Microsoft Azure 儲存體總管](http://storageexplorer.com/releasenotes.html)按一下**"下載 for Windows"**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-391">Go too[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) and click **“Download for Windows”**.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  <span data-ttu-id="be4cb-393">安裝之後，開啟 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="be4cb-393">After it is installed, open hello application.</span></span>

3.  <span data-ttu-id="be4cb-394">按一下 [加入帳戶] 。</span><span class="sxs-lookup"><span data-stu-id="be4cb-394">Click **Add Account**.</span></span>

4.  <span data-ttu-id="be4cb-395">登入 tooyour 帳戶來設定 Microsoft Azure 儲存體總管 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="be4cb-395">Configure Microsoft Azure Storage Explorer tooyour subscription by sign in tooyour account</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  <span data-ttu-id="be4cb-397">移 toostorage 帳戶，然後選取 hello 容器</span><span class="sxs-lookup"><span data-stu-id="be4cb-397">Go toostorage account and select hello Container</span></span>

6.  <span data-ttu-id="be4cb-398">選取 [取得共用存取簽章...]</span><span class="sxs-lookup"><span data-stu-id="be4cb-398">Select **“Get Share Access Signature..”**</span></span> <span data-ttu-id="be4cb-399">使用滑鼠右鍵按一下的 hello**容器**</span><span class="sxs-lookup"><span data-stu-id="be4cb-399">by using Right Click of hello **container**</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  <span data-ttu-id="be4cb-401">根據下列指示，更新 [開始時間]、[到期時間] 和 [權限]</span><span class="sxs-lookup"><span data-stu-id="be4cb-401">Update Start time, Expiry time and Permissions as per following</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    <span data-ttu-id="be4cb-403">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-403">a.</span></span>  <span data-ttu-id="be4cb-404">**開始時間：** toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。</span><span class="sxs-lookup"><span data-stu-id="be4cb-404">**Start Time:** toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="be4cb-405">例如，如果 hello 目前日期為 2014 年 10 月 6 日，選取時間 2014 年 10 月 5 日。</span><span class="sxs-lookup"><span data-stu-id="be4cb-405">For example, if hello current date is October 6, 2014, select 10/5/2014.</span></span>

    <span data-ttu-id="be4cb-406">b.</span><span class="sxs-lookup"><span data-stu-id="be4cb-406">b.</span></span>  <span data-ttu-id="be4cb-407">**到期時間：**選取 hello 之後至少 3 週的日期**開始時間**日期。</span><span class="sxs-lookup"><span data-stu-id="be4cb-407">**Expiry Time:** Select a date that is at least 3 weeks after hello **Start Time** date.</span></span>

    <span data-ttu-id="be4cb-408">c.</span><span class="sxs-lookup"><span data-stu-id="be4cb-408">c.</span></span>  <span data-ttu-id="be4cb-409">**權限：**選取 hello**清單**和**讀取**權限</span><span class="sxs-lookup"><span data-stu-id="be4cb-409">**Permissions:** Select hello **List** and **Read** permissions</span></span>

8.  <span data-ttu-id="be4cb-410">複製容器共用存取簽章 URI</span><span class="sxs-lookup"><span data-stu-id="be4cb-410">Copy Container shared access signature URI</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    <span data-ttu-id="be4cb-412">產生的 SAS URL 是用於容器層級，現在我們需要在它 tooadd VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-412">Generated SAS URL is for container Level and now we need tooadd VHD name in it.</span></span>

    <span data-ttu-id="be4cb-413">容器層級 SAS URL 的格式︰`https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="be4cb-413">Format of Container Level SAS URL: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="be4cb-414">SAS URL 中，如下所示的 hello 容器名稱後面插入 VHD 的名稱`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="be4cb-414">Insert VHD name after hello container name in SAS URL as below `https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    <span data-ttu-id="be4cb-415">範例：</span><span class="sxs-lookup"><span data-stu-id="be4cb-415">Example:</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    <span data-ttu-id="be4cb-417">TestRGVM201631920152.vhd 為 hello VHD 名稱，然後將 VHD SAS URL`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span><span class="sxs-lookup"><span data-stu-id="be4cb-417">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be `https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`</span></span>

    - <span data-ttu-id="be4cb-418">請確定您的映像檔案名稱和**".vhd"** hello URI 中。</span><span class="sxs-lookup"><span data-stu-id="be4cb-418">Make sure that your image file name and **".vhd"** are in hello URI.</span></span>
    - <span data-ttu-id="be4cb-419">Hello 簽章的中間，請確定**"sp = rl"**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-419">In middle of hello signature, make sure that **"sp=rl"** appears.</span></span> <span data-ttu-id="be4cb-420">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="be4cb-420">This demonstrates that Read and List access was provided successfully.</span></span>
    - <span data-ttu-id="be4cb-421">Hello 簽章的中間，請確定**"sr-iov = c 」**隨即出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-421">In middle of hello signature, make sure that **"sr=c"** appears.</span></span> <span data-ttu-id="be4cb-422">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="be4cb-422">This demonstrates that you have container level access</span></span>

9.  <span data-ttu-id="be4cb-423">tooensure 的 hello 產生共用的存取簽章 URI 是有效的在瀏覽器測試它。</span><span class="sxs-lookup"><span data-stu-id="be4cb-423">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="be4cb-424">它應該啟動 hello 下載程序</span><span class="sxs-lookup"><span data-stu-id="be4cb-424">It should start hello download process</span></span>

10. <span data-ttu-id="be4cb-425">將複製 hello 共用的存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-425">Copy hello shared access signature URI.</span></span> <span data-ttu-id="be4cb-426">這是將 URI toopaste hello 到 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="be4cb-426">This is hello URI toopaste into hello Publishing Portal.</span></span>

11. <span data-ttu-id="be4cb-427">針對每個 VHD hello SKU 中重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-427">Repeat these steps for each VHD in hello SKU.</span></span>

<span data-ttu-id="be4cb-428">**Azure CLI (建議用於非 Windows 和持續整合)**</span><span class="sxs-lookup"><span data-stu-id="be4cb-428">**Azure CLI (Recommended for Non-Windows & Continuous Integration)**</span></span>

<span data-ttu-id="be4cb-429">下面是使用 Azure CLI 來產生 SAS URL 的 hello 步驟</span><span class="sxs-lookup"><span data-stu-id="be4cb-429">Following are hello steps for generating SAS URL by using Azure CLI</span></span>

1.  <span data-ttu-id="be4cb-430">從[這裡](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/)下載 Microsoft Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-430">Download Microsoft Azure CLI from [here](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/).</span></span> <span data-ttu-id="be4cb-431">您也可以找到適用於 **[Windows](http://aka.ms/webpi-azure-cli)** 和 **[MAC OS](http://aka.ms/mac-azure-cli)** 的不同連結。</span><span class="sxs-lookup"><span data-stu-id="be4cb-431">You can also find different links for **[Windows](http://aka.ms/webpi-azure-cli)** and **[MAC OS](http://aka.ms/mac-azure-cli)**.</span></span>

2.  <span data-ttu-id="be4cb-432">下載之後，請安裝</span><span class="sxs-lookup"><span data-stu-id="be4cb-432">Once it is downloaded, please install</span></span>

3.  <span data-ttu-id="be4cb-433">使用下列程式碼建立 PowerShell 檔案，並將它儲存在本機</span><span class="sxs-lookup"><span data-stu-id="be4cb-433">Create a PowerShell file with following code and save it in local</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    <span data-ttu-id="be4cb-434">更新下列 hello 中上方的參數</span><span class="sxs-lookup"><span data-stu-id="be4cb-434">Update hello following parameters in above</span></span>

    <span data-ttu-id="be4cb-435">a.</span><span class="sxs-lookup"><span data-stu-id="be4cb-435">a.</span></span> <span data-ttu-id="be4cb-436">**`<StorageAccountName>`**：提供您的儲存體帳戶名稱</span><span class="sxs-lookup"><span data-stu-id="be4cb-436">**`<StorageAccountName>`**: Give your storage account name</span></span>

    <span data-ttu-id="be4cb-437">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="be4cb-437">b.</span></span> <span data-ttu-id="be4cb-438">**`<Storage Account Key>`**：提供您的儲存體帳戶金鑰</span><span class="sxs-lookup"><span data-stu-id="be4cb-438">**`<Storage Account Key>`**: Give your storage account key</span></span>

    <span data-ttu-id="be4cb-439">c.</span><span class="sxs-lookup"><span data-stu-id="be4cb-439">c.</span></span> <span data-ttu-id="be4cb-440">**`<Permission Start Date>`**: toosafeguard UTC 時間，hello 目前日期前的選取 hello 一天。</span><span class="sxs-lookup"><span data-stu-id="be4cb-440">**`<Permission Start Date>`**: toosafeguard for UTC time, select hello day before hello current date.</span></span> <span data-ttu-id="be4cb-441">比方說，如果 hello 目前日期為 2016 年 10 月 26 日，則值應該是 2016 年 10 月 25</span><span class="sxs-lookup"><span data-stu-id="be4cb-441">For example, if hello current date is October 26, 2016, then value should be 10/25/2016</span></span>

    <span data-ttu-id="be4cb-442">d.</span><span class="sxs-lookup"><span data-stu-id="be4cb-442">d.</span></span> <span data-ttu-id="be4cb-443">**`<Permission End Date>`**： 選取的日期，之後 hello 至少 3 週**開始日期**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-443">**`<Permission End Date>`**: Select a date that is at least 3 weeks after hello **Start Date**.</span></span> <span data-ttu-id="be4cb-444">所以值應該為 **11/02/2016**。</span><span class="sxs-lookup"><span data-stu-id="be4cb-444">Then value should be **11/02/2016**.</span></span>

    <span data-ttu-id="be4cb-445">以下是 hello 範例程式碼之後更新適當的參數</span><span class="sxs-lookup"><span data-stu-id="be4cb-445">Following is hello example code after updating proper parameters</span></span>

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  <span data-ttu-id="be4cb-446">使用「以系統管理員身分執行」模式下開啟 Powershell 編輯器，並在步驟 #3 中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="be4cb-446">Open Powershell editor with “Run as Administrator” mode and open file in step #3.</span></span>

5.  <span data-ttu-id="be4cb-447">執行的 hello 指令碼，它會提供您 hello 容器層級存取 SAS URL</span><span class="sxs-lookup"><span data-stu-id="be4cb-447">Run hello script and it will provide you hello SAS URL for container level access</span></span>

    <span data-ttu-id="be4cb-448">下列將會是 hello SAS 簽章和複製 hello 反白顯示組件，[記事本] 中的 hello 輸出</span><span class="sxs-lookup"><span data-stu-id="be4cb-448">Following will be hello output of hello SAS Signature and copy hello highlighted part in a notepad</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  <span data-ttu-id="be4cb-450">現在，您會看到容器層級 SAS URL，您需要在它 tooadd VHD 名稱。</span><span class="sxs-lookup"><span data-stu-id="be4cb-450">Now you will get container level SAS URL and you need tooadd VHD name in it.</span></span>

    <span data-ttu-id="be4cb-451">容器等級 SAS URL #</span><span class="sxs-lookup"><span data-stu-id="be4cb-451">Container level SAS URL #</span></span>

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  <span data-ttu-id="be4cb-452">SAS URL 中的 hello 容器名稱後面插入 VHD 的名稱，如下所示`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span><span class="sxs-lookup"><span data-stu-id="be4cb-452">Insert VHD name after hello container name in SAS URL as shown below `https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`</span></span>

    <span data-ttu-id="be4cb-453">範例：</span><span class="sxs-lookup"><span data-stu-id="be4cb-453">Example:</span></span>

    <span data-ttu-id="be4cb-454">TestRGVM201631920152.vhd 為 hello VHD 名稱，然後將 VHD SAS URL</span><span class="sxs-lookup"><span data-stu-id="be4cb-454">TestRGVM201631920152.vhd is hello VHD Name then VHD SAS URL will be</span></span>

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - <span data-ttu-id="be4cb-455">請確定您的映像檔案名稱和".vhd"位於 hello URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-455">Make sure that your image file name and ".vhd" are in hello URI.</span></span>
    -   <span data-ttu-id="be4cb-456">Hello 簽章的中間，請確定 「 sp = rl 」 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-456">In middle of hello signature, make sure that "sp=rl" appears.</span></span> <span data-ttu-id="be4cb-457">這表明已成功提供 [讀取] 和 [列出] 存取權。</span><span class="sxs-lookup"><span data-stu-id="be4cb-457">This demonstrates that Read and List access was provided successfully.</span></span>
    -   <span data-ttu-id="be4cb-458">Hello 簽章的中間，請確定 「 sr-iov = c"會出現。</span><span class="sxs-lookup"><span data-stu-id="be4cb-458">In middle of hello signature, make sure that "sr=c" appears.</span></span> <span data-ttu-id="be4cb-459">這示範您具有容器層級存取</span><span class="sxs-lookup"><span data-stu-id="be4cb-459">This demonstrates that you have container level access</span></span>

8.  <span data-ttu-id="be4cb-460">tooensure 的 hello 產生共用的存取簽章 URI 是有效的在瀏覽器測試它。</span><span class="sxs-lookup"><span data-stu-id="be4cb-460">tooensure that hello generated shared access signature URI works, test it in browser.</span></span> <span data-ttu-id="be4cb-461">它應該啟動 hello 下載程序</span><span class="sxs-lookup"><span data-stu-id="be4cb-461">It should start hello download process</span></span>

9.  <span data-ttu-id="be4cb-462">將複製 hello 共用的存取簽章 URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-462">Copy hello shared access signature URI.</span></span> <span data-ttu-id="be4cb-463">這是將 URI toopaste hello 到 hello 發佈入口網站。</span><span class="sxs-lookup"><span data-stu-id="be4cb-463">This is hello URI toopaste into hello Publishing Portal.</span></span>

10. <span data-ttu-id="be4cb-464">針對每個 VHD hello SKU 中重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="be4cb-464">Repeat these steps for each VHD in hello SKU.</span></span>


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a><span data-ttu-id="be4cb-465">5.3 提供 hello VM 映像的相關資訊，並要求 hello 發佈入口網站中的憑證</span><span class="sxs-lookup"><span data-stu-id="be4cb-465">5.3 Provide information about hello VM image and request certification in hello Publishing Portal</span></span>
<span data-ttu-id="be4cb-466">您已建立您的優惠和 SKU 之後，您應該輸入 hello 與該 SKU 相關聯的映像詳細資料：</span><span class="sxs-lookup"><span data-stu-id="be4cb-466">After you have created your offer and SKU, you should enter hello image details associated with that SKU:</span></span>

1. <span data-ttu-id="be4cb-467">移 toohello[發佈入口網站][link-pubportal]，然後使用賣方帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="be4cb-467">Go toohello [Publishing Portal][link-pubportal], and then sign in with your seller account.</span></span>
2. <span data-ttu-id="be4cb-468">選取 hello **VM 映像** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="be4cb-468">Select hello **VM images** tab.</span></span>
3. <span data-ttu-id="be4cb-469">列在 hello hello 頁面頂端的 hello 識別碼實際上是 hello 供應項目識別碼和 hello SKU 識別碼。</span><span class="sxs-lookup"><span data-stu-id="be4cb-469">hello identifier listed at hello top of hello page is actually hello offer identifier and not hello SKU identifier.</span></span>
4. <span data-ttu-id="be4cb-470">填寫 [hello] 下的 hello 屬性**Sku** > 一節。</span><span class="sxs-lookup"><span data-stu-id="be4cb-470">Fill out hello properties under hello **SKUs** section.</span></span>
5. <span data-ttu-id="be4cb-471">在下**作業系統系列**，按一下 hello 與 hello 作業系統 VHD 相關聯的作業系統類型。</span><span class="sxs-lookup"><span data-stu-id="be4cb-471">Under **Operating system family**, click hello operating system type associated with hello operating system VHD.</span></span>
6. <span data-ttu-id="be4cb-472">在 hello**作業系統**方塊中，描述 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="be4cb-472">In hello **Operating system** box, describe hello operating system.</span></span> <span data-ttu-id="be4cb-473">請考慮使用作業系統系列、類型、版本和更新等格式。</span><span class="sxs-lookup"><span data-stu-id="be4cb-473">Consider a format such as operating system family, type, version, and updates.</span></span> <span data-ttu-id="be4cb-474">其中一個範例為 "Windows Server Datacenter 2014 R2"。</span><span class="sxs-lookup"><span data-stu-id="be4cb-474">An example is "Windows Server Datacenter 2014 R2."</span></span>
7. <span data-ttu-id="be4cb-475">選取 toosix 建議虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="be4cb-475">Select up toosix recommended virtual machine sizes.</span></span> <span data-ttu-id="be4cb-476">這些是決定 toopurchase 並部署您的映像時，取得顯示的 toohello 客戶 hello Azure 入口網站中的 hello 定價層刀鋒視窗中的建議。</span><span class="sxs-lookup"><span data-stu-id="be4cb-476">These are recommendations that get displayed toohello customer in hello Pricing tier blade in hello Azure Portal when they decide toopurchase and deploy your image.</span></span> <span data-ttu-id="be4cb-477">**這些只是建議。hello 客戶都可以 tooselect 映像中指定任何可容納 hello 磁碟的 VM 大小。**</span><span class="sxs-lookup"><span data-stu-id="be4cb-477">**These are only recommendations. hello customer is able tooselect any VM size that accommodates hello disks specified in your image.**</span></span>
8. <span data-ttu-id="be4cb-478">輸入 hello 的版本。</span><span class="sxs-lookup"><span data-stu-id="be4cb-478">Enter hello version.</span></span> <span data-ttu-id="be4cb-479">hello 版本 欄位會封裝的語意版本 tooidentify hello 產品和它的更新：</span><span class="sxs-lookup"><span data-stu-id="be4cb-479">hello version field encapsulates a semantic version tooidentify hello product and its updates:</span></span>
   * <span data-ttu-id="be4cb-480">版本應為 hello 表單 X.Y.Z，X、 Y 和 Z 都是整數。</span><span class="sxs-lookup"><span data-stu-id="be4cb-480">Versions should be of hello form X.Y.Z, where X, Y, and Z are integers.</span></span>
   * <span data-ttu-id="be4cb-481">不同 SKU 中的映像可以有不同的主要和次要版本。</span><span class="sxs-lookup"><span data-stu-id="be4cb-481">Images in different SKUs can have different major and minor versions.</span></span>
   * <span data-ttu-id="be4cb-482">SKU 中的版本只應該增加 hello 修補程式的版本 (從 X.Y.Z Z) 的累加變更。</span><span class="sxs-lookup"><span data-stu-id="be4cb-482">Versions within a SKU should only be incremental changes, which increase hello patch version (Z from X.Y.Z).</span></span>
9. <span data-ttu-id="be4cb-483">在 hello **OS VHD URL**方塊中，輸入 hello 共用的存取簽章建立 hello 作業系統 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-483">In hello **OS VHD URL** box, enter hello shared access signature URI created for hello operating system VHD.</span></span>
10. <span data-ttu-id="be4cb-484">如果有與此 SKU 相關聯的資料磁碟，請選取 hello 邏輯單元編號 (LUN) toowhich 您想要部署時裝載此資料磁碟 toobe。</span><span class="sxs-lookup"><span data-stu-id="be4cb-484">If there are data disks associated with this SKU, select hello logical unit number (LUN) toowhich you would like this data disk toobe mounted upon deployment.</span></span>
11. <span data-ttu-id="be4cb-485">在 hello **LUN X VHD URL**方塊中，輸入 hello 共用的存取簽章建立 hello 第一個資料 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="be4cb-485">In hello **LUN X VHD URL** box, enter hello shared access signature URI created for hello first data VHD.</span></span>

    ![繪圖](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a><span data-ttu-id="be4cb-487">常見的 SAS URL 問題和修正</span><span class="sxs-lookup"><span data-stu-id="be4cb-487">Common SAS URL issues & fixes</span></span>

|<span data-ttu-id="be4cb-488">問題</span><span class="sxs-lookup"><span data-stu-id="be4cb-488">Issue</span></span>|<span data-ttu-id="be4cb-489">失敗訊息</span><span class="sxs-lookup"><span data-stu-id="be4cb-489">Failure Message</span></span>|<span data-ttu-id="be4cb-490">修正</span><span class="sxs-lookup"><span data-stu-id="be4cb-490">Fix</span></span>|<span data-ttu-id="be4cb-491">文件連結</span><span class="sxs-lookup"><span data-stu-id="be4cb-491">Documentation Link</span></span>|
|---|---|---|---|
|<span data-ttu-id="be4cb-492">複製映像失敗 - 在 SAS url 中找不到 "?"</span><span class="sxs-lookup"><span data-stu-id="be4cb-492">Failure in copying images - "?" is not found in SAS url</span></span>|<span data-ttu-id="be4cb-493">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-493">Failure: Copying Images.</span></span> <span data-ttu-id="be4cb-494">您不能 toodownload blob 使用提供的 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="be4cb-494">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="be4cb-495">建議您更新 hello SAS Url 使用工具</span><span class="sxs-lookup"><span data-stu-id="be4cb-495">Update hello SAS Url using recommended tools</span></span>|[<span data-ttu-id="be4cb-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="be4cb-496">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="be4cb-497">映像複製失敗 - SAS url 中未設定 “st” 和 “se” 參數</span><span class="sxs-lookup"><span data-stu-id="be4cb-497">Failure in copying images - “st” and “se” parameters not in SAS url</span></span>|<span data-ttu-id="be4cb-498">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-498">Failure: Copying Images.</span></span> <span data-ttu-id="be4cb-499">您不能 toodownload blob 使用提供的 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="be4cb-499">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="be4cb-500">更新 hello SAS Url 與它的開始和結束日期</span><span class="sxs-lookup"><span data-stu-id="be4cb-500">Update hello SAS Url with Start and End dates on it</span></span>|[<span data-ttu-id="be4cb-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="be4cb-501">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="be4cb-502">複製映像失敗 - SAS url 中沒有 “sp=rl”</span><span class="sxs-lookup"><span data-stu-id="be4cb-502">Failure in copying images - “sp=rl” not in SAS url</span></span>|<span data-ttu-id="be4cb-503">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-503">Failure: Copying Images.</span></span> <span data-ttu-id="be4cb-504">您不能 toodownload blob 使用所提供的 SAS Uri</span><span class="sxs-lookup"><span data-stu-id="be4cb-504">Not able toodownload blob using provided SAS Uri</span></span>|<span data-ttu-id="be4cb-505">更新 hello SAS Url 設定為 「 讀取 」 和 「 清單的權限</span><span class="sxs-lookup"><span data-stu-id="be4cb-505">Update hello SAS Url with permissions set as “Read” & “List</span></span>|[<span data-ttu-id="be4cb-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="be4cb-506">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="be4cb-507">複製映像失敗 - SAS url 中的 vhd 名稱含有空格</span><span class="sxs-lookup"><span data-stu-id="be4cb-507">Failure in copying images - SAS url have white spaces in vhd name</span></span>|<span data-ttu-id="be4cb-508">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-508">Failure: Copying Images.</span></span> <span data-ttu-id="be4cb-509">您不能 toodownload blob 使用提供的 SAS Uri。</span><span class="sxs-lookup"><span data-stu-id="be4cb-509">Not able toodownload blob using provided SAS Uri.</span></span>|<span data-ttu-id="be4cb-510">更新不含空格的 hello SAS Url</span><span class="sxs-lookup"><span data-stu-id="be4cb-510">Update hello SAS Url without white spaces</span></span>|[<span data-ttu-id="be4cb-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="be4cb-511">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|<span data-ttu-id="be4cb-512">複製映像失敗 – SAS Url 授權錯誤的</span><span class="sxs-lookup"><span data-stu-id="be4cb-512">Failure in copying images – SAS Url Authorization error</span></span>|<span data-ttu-id="be4cb-513">失敗︰複製映像。</span><span class="sxs-lookup"><span data-stu-id="be4cb-513">Failure: Copying Images.</span></span> <span data-ttu-id="be4cb-514">您不能 toodownload blob 到期 tooauthorization 錯誤</span><span class="sxs-lookup"><span data-stu-id="be4cb-514">Not able toodownload blob due tooauthorization error</span></span>|<span data-ttu-id="be4cb-515">重新產生 hello SAS Url</span><span class="sxs-lookup"><span data-stu-id="be4cb-515">Regenerate hello SAS Url</span></span>|[<span data-ttu-id="be4cb-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span><span class="sxs-lookup"><span data-stu-id="be4cb-516">https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/</span></span>](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a><span data-ttu-id="be4cb-517">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be4cb-517">Next step</span></span>
<span data-ttu-id="be4cb-518">您完成 hello SKU 詳細資料之後，您可以移動轉寄 toohello [Azure Marketplace 行銷內容指南][link-pushstaging]。</span><span class="sxs-lookup"><span data-stu-id="be4cb-518">After you are done with hello SKU details, you can move forward toohello [Azure Marketplace marketing content guide][link-pushstaging].</span></span> <span data-ttu-id="be4cb-519">您可以在該步驟 hello 發行程序中，提供 hello 太行銷內容、 價格和其他資訊的必要之前**步驟 3： 在預備環境中測試您的 VM 提供**、 部署之前測試各種案例，使用案例hello 公用可視性的優惠 toohello Azure Marketplace 並購買。</span><span class="sxs-lookup"><span data-stu-id="be4cb-519">In that step of hello publishing process, you provide hello marketing content, pricing, and other information necessary prior too**Step 3: Testing your VM offer in staging**, where you test various use-case scenarios before deploying hello offer toohello Azure Marketplace for public visibility and purchase.</span></span>  

## <a name="see-also"></a><span data-ttu-id="be4cb-520">另請參閱</span><span class="sxs-lookup"><span data-stu-id="be4cb-520">See also</span></span>
* [<span data-ttu-id="be4cb-521">快速入門： 如何 toopublish 優惠 toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="be4cb-521">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

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
