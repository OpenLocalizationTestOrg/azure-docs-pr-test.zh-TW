---
title: "概述如何建立及部署優惠至 Marketplace | Microsoft Docs"
description: "了解在 Azure Marketplace 中成為核准的 Microsoft 開發人員，以及建立及部署虛擬機器映像、範本、資料服務或開發人員服務所需的步驟"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: 8fbf201343f6710d2781a4b56ae54833ed4c06cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="publish-and-manage-an-offer-in-the-azure-marketplace"></a><span data-ttu-id="2d6f1-103">在 Azure Marketplace 中發佈和管理供應項目</span><span class="sxs-lookup"><span data-stu-id="2d6f1-103">Publish and manage an offer in the Azure Marketplace</span></span>
<span data-ttu-id="2d6f1-104">此文章可協助開發人員建立解決方案、部署並管理他們在 Azure Marketplace 中列出的解決方案，讓其他 Azure 客戶與合作夥伴可進行購買及使用。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-104">This article is provided to help developers create, deploy, and manage their solutions listed in the Azure Marketplace for other Azure customers and partners to purchase and use.</span></span>

## <a name="marketplace-publishing"></a><span data-ttu-id="2d6f1-105">Marketplace 發佈</span><span class="sxs-lookup"><span data-stu-id="2d6f1-105">Marketplace publishing</span></span>
<span data-ttu-id="2d6f1-106">身為 Azure 發行者，您可以將創新的解決方案或服務散發和販售給 Marketplace 中的其他開發人員、ISV 和 IT 專業人員。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-106">As an Azure publisher, you can distribute and sell your innovative solution or service to other developers, ISVs, and IT professionals in the Marketplace.</span></span> <span data-ttu-id="2d6f1-107">透過 Marketplace，您可以接觸到想要快速開發其雲端型應用程式和行動解決方案的客戶。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-107">Through the Marketplace, you can reach customers who want to quickly develop their cloud-based applications and mobile solutions.</span></span> <span data-ttu-id="2d6f1-108">如果您的解決方案是以商務使用者為目標，則您可能要考慮 [AppSource](http://appsource.microsoft.com) Marketplace。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-108">If your solution targets business users, you might want to consider the [AppSource](http://appsource.microsoft.com) marketplace.</span></span>


## <a name="supported-types-of-solutions"></a><span data-ttu-id="2d6f1-109">支援的解決方案類型</span><span class="sxs-lookup"><span data-stu-id="2d6f1-109">Supported types of solutions</span></span>
<span data-ttu-id="2d6f1-110">首先，您需要以發行者的身分，定義您的公司提供的解決方案類型。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-110">The first thing you want to do as a publisher is to define what kind of solution your company is offering.</span></span> <span data-ttu-id="2d6f1-111">Marketplace 支援下列幾種供應項目：</span><span class="sxs-lookup"><span data-stu-id="2d6f1-111">The Marketplace supports the following types of offers:</span></span>

|<span data-ttu-id="2d6f1-112">解決方案類型</span><span class="sxs-lookup"><span data-stu-id="2d6f1-112">Solution type</span></span>|<span data-ttu-id="2d6f1-113">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2d6f1-113">Virtual machine</span></span>|<span data-ttu-id="2d6f1-114">解決方案範本</span><span class="sxs-lookup"><span data-stu-id="2d6f1-114">Solution template</span></span>|
|---|---|---|
|<span data-ttu-id="2d6f1-115">**定義**</span><span class="sxs-lookup"><span data-stu-id="2d6f1-115">**Definition**</span></span>|<span data-ttu-id="2d6f1-116">預先配置的映像，包含完整安裝的作業系統以及一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-116">Preconfigured images with a fully installed operating system and one or more applications.</span></span> <span data-ttu-id="2d6f1-117">虛擬機器映像提供在 Azure 虛擬機器服務中建立及部署虛擬機器所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-117">A virtual machine image provides the information necessary to create and deploy virtual machines in the Azure Virtual Machines service.</span></span>|<span data-ttu-id="2d6f1-118">可參考一或多個獨特 Azure 服務 (包含由其他賣家發佈的服務) 的資料結構。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-118">A data structure that can reference one or more distinct Azure services, including services published by other sellers.</span></span> <span data-ttu-id="2d6f1-119">Azure 訂戶能使用此結構，以單一、協調的方式部署一或多個供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-119">Azure subscribers can use it to deploy one or more offerings in a single, coordinated manner.</span></span>|
|<span data-ttu-id="2d6f1-120">**範例**</span><span class="sxs-lookup"><span data-stu-id="2d6f1-120">**Example**</span></span>|<span data-ttu-id="2d6f1-121">身為 Azure 發行者，您已建立並驗證帶有創新資料庫服務的 VM。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-121">As an Azure publisher, you've created and validated a VM with an innovative database service.</span></span> <span data-ttu-id="2d6f1-122">其他 Azure 訂戶願意購買此 VM 並部署至其雲端服務環境。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-122">Other Azure subscribers want to procure and deploy this VM into their cloud service environments.</span></span>|<span data-ttu-id="2d6f1-123">身為 Azure 發行者，您組合了 Azure 的幾項服務，以便快速部署負載平衡、強化安全性且高可用性的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-123">As an Azure publisher, you've bundled a set of services from across Azure that make it quick to deploy cloud services with load balancing, enhanced security, and high availability.</span></span> <span data-ttu-id="2d6f1-124">其他 Azure 訂戶可藉由取得符合其目標的解決方案範本來節省時間。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-124">Other Azure subscribers can save time by procuring the solution template that meets their objective.</span></span> <span data-ttu-id="2d6f1-125">他們不必手動尋找、取得、部署及設定相同或類似的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-125">They don't have to manually locate, procure, deploy, and configure the same or similar Azure services.</span></span>|

> [!NOTE]
> <span data-ttu-id="2d6f1-126">有些步驟會在不同類型的解決方案間共用，但有些步驟則因解決方案類型而有所不同。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-126">Some steps are shared between the different types of solutions, and others are distinct to the respective type of solution.</span></span> <span data-ttu-id="2d6f1-127">本文提供簡短的概觀，讓您了解每種類型的解決方案必須完成哪些步驟。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-127">This article provides a short overview of the steps you need to complete for any type of solution.</span></span>

## <a name="publish-a-solution"></a><span data-ttu-id="2d6f1-128">發佈解決方案</span><span class="sxs-lookup"><span data-stu-id="2d6f1-128">Publish a solution</span></span>
![提名、註冊、發佈](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a><span data-ttu-id="2d6f1-130">提名您的解決方案以供預先核准</span><span class="sxs-lookup"><span data-stu-id="2d6f1-130">Nominate your solution for pre-approval</span></span>
<span data-ttu-id="2d6f1-131">若要在 Marketplace 中發佈虛擬機器[解決方案](https://createopportunity.azurewebsites.net)，請填妥 Microsoft Azure 認證**解決方案提名表單**。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-131">To publish a virtual machine [solution](https://createopportunity.azurewebsites.net) to the Marketplace, complete the Microsoft Azure Certified **Solution Nomination Form**.</span></span>

>[!NOTE]
> <span data-ttu-id="2d6f1-132">如果您與合作夥伴帳戶管理員或 DX 合作夥伴管理員合作，請要求他們提名讓您的解決方案能夠加入 Azure 認證計劃。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-132">If you are working with a Partner Account Manager or a DX Partner Manager, ask them to nominate your solution for the Azure Certified program.</span></span> <span data-ttu-id="2d6f1-133">您也可以移至 [Microsoft Azure 認證](http://createopportunity.azurewebsites.net)網頁，然後填妥申請表單。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-133">You can also go to the [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) webpage and fill out the application form.</span></span> <span data-ttu-id="2d6f1-134">在 [Microsoft 贊助者連絡人] 方塊中輸入您的夥伴客戶經理或 DX 夥伴經理的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-134">Enter the email of your Partner Account Manager or DX Partner Manager in the **Microsoft Sponsor Contact** box.</span></span>

<span data-ttu-id="2d6f1-135">如果您符合 [Azure Marketplace 參與原則](http://go.microsoft.com/fwlink/?LinkID=526833)的資格條件，且您的應用程式獲得核准，我們就會開始與您合作將您的解決方案上架到 Marketplace。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-135">If you meet the eligibility criteria in the [Azure Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833) and your application is approved, we start working with you to onboard your solution to the Marketplace.</span></span>

### <a name="register-your-account-as-a-microsoft-seller"></a><span data-ttu-id="2d6f1-136">將您的帳戶註冊為 Microsoft 賣方</span><span class="sxs-lookup"><span data-stu-id="2d6f1-136">Register your account as a Microsoft seller</span></span>
<span data-ttu-id="2d6f1-137">將您的 Microsoft 帳戶註冊為 [Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-137">Register your Microsoft account as a [Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md).</span></span>

### <a name="publish-your-solution"></a><span data-ttu-id="2d6f1-138">發佈您的解決方案</span><span class="sxs-lookup"><span data-stu-id="2d6f1-138">Publish your solution</span></span>
<span data-ttu-id="2d6f1-139">若要在 Marketplace 中發佈解決方案，請遵循下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="2d6f1-139">To publish a solution to the Marketplace, follow these steps:</span></span>
1. <span data-ttu-id="2d6f1-140">滿足非技術性需求。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-140">Fulfill the nontechnical requirements.</span></span>

    <span data-ttu-id="2d6f1-141">a.</span><span class="sxs-lookup"><span data-stu-id="2d6f1-141">a.</span></span> <span data-ttu-id="2d6f1-142">滿足[非技術性必要條件](marketplace-publishing-pre-requisites.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-142">Fulfill the [nontechnical prerequisites](marketplace-publishing-pre-requisites.md).</span></span>

    <span data-ttu-id="2d6f1-143">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-143">b.</span></span> <span data-ttu-id="2d6f1-144">滿足 [VM 技術性必要條件](marketplace-publishing-vm-image-creation-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-144">Fulfill the [VM technical prerequisites](marketplace-publishing-vm-image-creation-prerequisites.md).</span></span>

    <span data-ttu-id="2d6f1-145">c.</span><span class="sxs-lookup"><span data-stu-id="2d6f1-145">c.</span></span> <span data-ttu-id="2d6f1-146">滿足[解決方案範本技術性必要條件](marketplace-publishing-solution-template-creation-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-146">Fulfill the [solution template technical prerequisites](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span>

2. <span data-ttu-id="2d6f1-147">建立您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-147">Create your offer.</span></span>

    <span data-ttu-id="2d6f1-148">a.</span><span class="sxs-lookup"><span data-stu-id="2d6f1-148">a.</span></span> <span data-ttu-id="2d6f1-149">建立[虛擬機器](marketplace-publishing-vm-image-creation.md)供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-149">Create a [virtual machine](marketplace-publishing-vm-image-creation.md) offer.</span></span>

    <span data-ttu-id="2d6f1-150">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-150">b.</span></span> <span data-ttu-id="2d6f1-151">建立[解決方案範本](marketplace-publishing-solution-template-creation.md)供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-151">Create a [solution template](marketplace-publishing-solution-template-creation.md) offer.</span></span>

3. <span data-ttu-id="2d6f1-152">建立您的供應項目[行銷內容](marketplace-publishing-push-to-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-152">Create your offer [marketing content](marketplace-publishing-push-to-staging.md).</span></span>

4. <span data-ttu-id="2d6f1-153">在預備環境中測試您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-153">Test your offer in staging.</span></span>

    <span data-ttu-id="2d6f1-154">a.</span><span class="sxs-lookup"><span data-stu-id="2d6f1-154">a.</span></span> <span data-ttu-id="2d6f1-155">在[預備環境](marketplace-publishing-vm-image-test-in-staging.md)中測試您的 VM 供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-155">Test your VM offer in [staging](marketplace-publishing-vm-image-test-in-staging.md).</span></span>

    <span data-ttu-id="2d6f1-156">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-156">b.</span></span> <span data-ttu-id="2d6f1-157">在[預備環境](marketplace-publishing-solution-template-test-in-staging.md)中測試您的解決方案範本供應項目。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-157">Test your solution template offer in [staging](marketplace-publishing-solution-template-test-in-staging.md).</span></span>

5. <span data-ttu-id="2d6f1-158">將您的供應項目部署至 [Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-158">Deploy your offer to the [Marketplace](marketplace-publishing-push-to-production.md).</span></span>


### <a name="create-and-manage-a-virtual-machine-image"></a><span data-ttu-id="2d6f1-159">建立和管理虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="2d6f1-159">Create and manage a virtual machine image</span></span>
<span data-ttu-id="2d6f1-160">使用這些資源來建立和管理 VM 映像︰</span><span class="sxs-lookup"><span data-stu-id="2d6f1-160">Create and manage a VM image by using these resources:</span></span>
* <span data-ttu-id="2d6f1-161">建立[內部部署](marketplace-publishing-vm-image-creation-on-premise.md) VM 映像。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-161">Create a VM image [on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>
* <span data-ttu-id="2d6f1-162">在 [Azure 入口網站](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中建立執行 Windows 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-162">Create a virtual machine running [Windows in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2d6f1-163">在 [Azure 入口網站](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中建立執行 Linux 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-163">Create a virtual machine running [Linux in the Azure portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="2d6f1-164">針對 [VHD 建立](marketplace-publishing-vm-image-creation-troubleshooting.md)常見問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="2d6f1-164">Troubleshoot common issues encountered during [VHD creation](marketplace-publishing-vm-image-creation-troubleshooting.md).</span></span>

## <a name="manage-your-solution"></a><span data-ttu-id="2d6f1-165">管理您的解決方案</span><span class="sxs-lookup"><span data-stu-id="2d6f1-165">Manage your solution</span></span>
<span data-ttu-id="2d6f1-166">透過下列資源的協助來管理您的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="2d6f1-166">Manage your solution with help from the following resources:</span></span>
* [<span data-ttu-id="2d6f1-167">閱讀虛擬機器供應項目的後期製作指南</span><span class="sxs-lookup"><span data-stu-id="2d6f1-167">Read the post-production guide for virtual machine offers</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="2d6f1-168">更新供應項目或 SKU 的非技術性詳細資料</span><span class="sxs-lookup"><span data-stu-id="2d6f1-168">Update the nontechnical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [<span data-ttu-id="2d6f1-169">更新供應項目或 SKU 的技術性詳細資料</span><span class="sxs-lookup"><span data-stu-id="2d6f1-169">Update the technical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [<span data-ttu-id="2d6f1-170">在已列出的供應項目下新增 SKU</span><span class="sxs-lookup"><span data-stu-id="2d6f1-170">Add a new SKU under a listed offer</span></span>](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [<span data-ttu-id="2d6f1-171">變更已列出 SKU 的資料磁碟計數</span><span class="sxs-lookup"><span data-stu-id="2d6f1-171">Change the data disk count for a listed SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [<span data-ttu-id="2d6f1-172">從 Marketplace 刪除已列出的供應項目</span><span class="sxs-lookup"><span data-stu-id="2d6f1-172">Delete a listed offer from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="2d6f1-173">從 Marketplace 刪除已列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="2d6f1-173">Delete a listed SKU from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="2d6f1-174">從 Marketplace 刪除已列出 SKU 的目前版本</span><span class="sxs-lookup"><span data-stu-id="2d6f1-174">Delete the current version of a listed SKU from the Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="2d6f1-175">將列出價格還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="2d6f1-175">Revert the listing price to production values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [<span data-ttu-id="2d6f1-176">將計費模式還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="2d6f1-176">Revert the billing model to production values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [<span data-ttu-id="2d6f1-177">將已列出的 SKU 的可見性設定還原成生產環境值</span><span class="sxs-lookup"><span data-stu-id="2d6f1-177">Revert the visibility setting of a listed SKU to the production value</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [<span data-ttu-id="2d6f1-178">變更雲端解決方案提供者轉售商獎勵</span><span class="sxs-lookup"><span data-stu-id="2d6f1-178">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="2d6f1-179">了解付款報告</span><span class="sxs-lookup"><span data-stu-id="2d6f1-179">Understand your payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="2d6f1-180">以發佈者身分取得支援</span><span class="sxs-lookup"><span data-stu-id="2d6f1-180">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a><span data-ttu-id="2d6f1-181">其他資源</span><span class="sxs-lookup"><span data-stu-id="2d6f1-181">Additional resources</span></span>
[<span data-ttu-id="2d6f1-182">設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2d6f1-182">Set up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)
