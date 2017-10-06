---
title: "如何的 aaaOverview toocreate 及部署方案 toohello Marketplace |Microsoft 文件"
description: "了解 hello 步驟需要的 toobecome 核准的 Microsoft 開發人員，建立及部署虛擬機器映像、 範本、 資料服務或在 hello Azure Marketplace 中的開發人員服務"
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
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a><span data-ttu-id="938e3-103">發佈和管理在 hello Azure Marketplace 提供項目</span><span class="sxs-lookup"><span data-stu-id="938e3-103">Publish and manage an offer in hello Azure Marketplace</span></span>
<span data-ttu-id="938e3-104">這篇文章會提供 toohelp 開發人員建立、 部署和管理他們 hello Azure Marketplace 中列出的其他 Azure 客戶和合作夥伴 toopurchase 和使用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="938e3-104">This article is provided toohelp developers create, deploy, and manage their solutions listed in hello Azure Marketplace for other Azure customers and partners toopurchase and use.</span></span>

## <a name="marketplace-publishing"></a><span data-ttu-id="938e3-105">Marketplace 發佈</span><span class="sxs-lookup"><span data-stu-id="938e3-105">Marketplace publishing</span></span>
<span data-ttu-id="938e3-106">為 Azure 的 「 發行者 」，您可以發佈和銷售您的創新方案或服務 tooother 開發人員，Isv 和 IT 專業人員在 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="938e3-106">As an Azure publisher, you can distribute and sell your innovative solution or service tooother developers, ISVs, and IT professionals in hello Marketplace.</span></span> <span data-ttu-id="938e3-107">透過 hello Marketplace，您可以連線到客戶希望 tooquickly 開發雲端應用程式與行動方案。</span><span class="sxs-lookup"><span data-stu-id="938e3-107">Through hello Marketplace, you can reach customers who want tooquickly develop their cloud-based applications and mobile solutions.</span></span> <span data-ttu-id="938e3-108">如果您的方案的目標商務使用者，您可能想 tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace。</span><span class="sxs-lookup"><span data-stu-id="938e3-108">If your solution targets business users, you might want tooconsider hello [AppSource](http://appsource.microsoft.com) marketplace.</span></span>


## <a name="supported-types-of-solutions"></a><span data-ttu-id="938e3-109">支援的解決方案類型</span><span class="sxs-lookup"><span data-stu-id="938e3-109">Supported types of solutions</span></span>
<span data-ttu-id="938e3-110">因為 「 發行者 」 是 toodefine 貴公司提供哪些類型的方案，您會想 toodo hello 第一件事。</span><span class="sxs-lookup"><span data-stu-id="938e3-110">hello first thing you want toodo as a publisher is toodefine what kind of solution your company is offering.</span></span> <span data-ttu-id="938e3-111">hello Marketplace 支援下列類型的優惠的 hello:</span><span class="sxs-lookup"><span data-stu-id="938e3-111">hello Marketplace supports hello following types of offers:</span></span>

|<span data-ttu-id="938e3-112">解決方案類型</span><span class="sxs-lookup"><span data-stu-id="938e3-112">Solution type</span></span>|<span data-ttu-id="938e3-113">虛擬機器</span><span class="sxs-lookup"><span data-stu-id="938e3-113">Virtual machine</span></span>|<span data-ttu-id="938e3-114">解決方案範本</span><span class="sxs-lookup"><span data-stu-id="938e3-114">Solution template</span></span>|
|---|---|---|
|<span data-ttu-id="938e3-115">**定義**</span><span class="sxs-lookup"><span data-stu-id="938e3-115">**Definition**</span></span>|<span data-ttu-id="938e3-116">預先配置的映像，包含完整安裝的作業系統以及一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="938e3-116">Preconfigured images with a fully installed operating system and one or more applications.</span></span> <span data-ttu-id="938e3-117">虛擬機器映像提供 hello 資訊必要 toocreate，並部署 hello Azure 虛擬機器服務中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="938e3-117">A virtual machine image provides hello information necessary toocreate and deploy virtual machines in hello Azure Virtual Machines service.</span></span>|<span data-ttu-id="938e3-118">可參考一或多個獨特 Azure 服務 (包含由其他賣家發佈的服務) 的資料結構。</span><span class="sxs-lookup"><span data-stu-id="938e3-118">A data structure that can reference one or more distinct Azure services, including services published by other sellers.</span></span> <span data-ttu-id="938e3-119">Azure 的訂閱者可以使用它 toodeploy 以單一、 協調的方式中一或多個供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-119">Azure subscribers can use it toodeploy one or more offerings in a single, coordinated manner.</span></span>|
|<span data-ttu-id="938e3-120">**範例**</span><span class="sxs-lookup"><span data-stu-id="938e3-120">**Example**</span></span>|<span data-ttu-id="938e3-121">身為 Azure 發行者，您已建立並驗證帶有創新資料庫服務的 VM。</span><span class="sxs-lookup"><span data-stu-id="938e3-121">As an Azure publisher, you've created and validated a VM with an innovative database service.</span></span> <span data-ttu-id="938e3-122">其他 Azure 訂戶想 tooprocure，並將此 VM 部署至雲端服務環境。</span><span class="sxs-lookup"><span data-stu-id="938e3-122">Other Azure subscribers want tooprocure and deploy this VM into their cloud service environments.</span></span>|<span data-ttu-id="938e3-123">為 Azure 的 「 發行者 」，您已配套一的組服務從整個 Azure，可讓您快速 toodeploy 與負載平衡、 增強式的安全性、 高可用性的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="938e3-123">As an Azure publisher, you've bundled a set of services from across Azure that make it quick toodeploy cloud services with load balancing, enhanced security, and high availability.</span></span> <span data-ttu-id="938e3-124">其他 Azure 訂戶可以獲得符合其目標的 hello 解決方案範本，以節省時間。</span><span class="sxs-lookup"><span data-stu-id="938e3-124">Other Azure subscribers can save time by procuring hello solution template that meets their objective.</span></span> <span data-ttu-id="938e3-125">在沒有 toomanually 找出、 採購、 部署和設定 hello 相同或類似的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="938e3-125">They don't have toomanually locate, procure, deploy, and configure hello same or similar Azure services.</span></span>|

> [!NOTE]
> <span data-ttu-id="938e3-126">某些步驟之間會共用 hello 不同類型解決方案，因此有些則解決方案的相異 toohello 個別的型別。</span><span class="sxs-lookup"><span data-stu-id="938e3-126">Some steps are shared between hello different types of solutions, and others are distinct toohello respective type of solution.</span></span> <span data-ttu-id="938e3-127">本文章提供簡短的概觀的 hello 步驟需 toocomplete 的任何類型的解決方案。</span><span class="sxs-lookup"><span data-stu-id="938e3-127">This article provides a short overview of hello steps you need toocomplete for any type of solution.</span></span>

## <a name="publish-a-solution"></a><span data-ttu-id="938e3-128">發佈解決方案</span><span class="sxs-lookup"><span data-stu-id="938e3-128">Publish a solution</span></span>
![提名、註冊、發佈](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a><span data-ttu-id="938e3-130">提名您的解決方案以供預先核准</span><span class="sxs-lookup"><span data-stu-id="938e3-130">Nominate your solution for pre-approval</span></span>
<span data-ttu-id="938e3-131">虛擬機器 toopublish[方案](https://createopportunity.azurewebsites.net)toohello Marketplace，完成 Microsoft Azure 認證的 hello**方案提名表單**。</span><span class="sxs-lookup"><span data-stu-id="938e3-131">toopublish a virtual machine [solution](https://createopportunity.azurewebsites.net) toohello Marketplace, complete hello Microsoft Azure Certified **Solution Nomination Form**.</span></span>

>[!NOTE]
> <span data-ttu-id="938e3-132">如果您正在使用協力廠商客戶經理或 DX 夥伴管理員，要求他們 toonominate hello Azure 認證計劃您的方案。</span><span class="sxs-lookup"><span data-stu-id="938e3-132">If you are working with a Partner Account Manager or a DX Partner Manager, ask them toonominate your solution for hello Azure Certified program.</span></span> <span data-ttu-id="938e3-133">您也可以移 toohello [Microsoft Azure 認證](http://createopportunity.azurewebsites.net)網頁和填寫 hello 應用程式表單。</span><span class="sxs-lookup"><span data-stu-id="938e3-133">You can also go toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) webpage and fill out hello application form.</span></span> <span data-ttu-id="938e3-134">輸入 hello 夥伴客戶經理或 DX 夥伴管理員的電子郵件中 hello **Microsoft 發起人連絡人**方塊。</span><span class="sxs-lookup"><span data-stu-id="938e3-134">Enter hello email of your Partner Account Manager or DX Partner Manager in hello **Microsoft Sponsor Contact** box.</span></span>

<span data-ttu-id="938e3-135">如果符合在 hello hello 適用性準則[Azure Marketplace 參與原則](http://go.microsoft.com/fwlink/?LinkID=526833)和您的應用程式獲得核准後，我們開始使用您 tooonboard 您方案 toohello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="938e3-135">If you meet hello eligibility criteria in hello [Azure Marketplace participation policies](http://go.microsoft.com/fwlink/?LinkID=526833) and your application is approved, we start working with you tooonboard your solution toohello Marketplace.</span></span>

### <a name="register-your-account-as-a-microsoft-seller"></a><span data-ttu-id="938e3-136">將您的帳戶註冊為 Microsoft 賣方</span><span class="sxs-lookup"><span data-stu-id="938e3-136">Register your account as a Microsoft seller</span></span>
<span data-ttu-id="938e3-137">將您的 Microsoft 帳戶註冊為 [Microsoft 開發人員帳戶](marketplace-publishing-accounts-creation-registration.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-137">Register your Microsoft account as a [Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md).</span></span>

### <a name="publish-your-solution"></a><span data-ttu-id="938e3-138">發佈您的解決方案</span><span class="sxs-lookup"><span data-stu-id="938e3-138">Publish your solution</span></span>
<span data-ttu-id="938e3-139">toopublish 方案 toohello 服務商場，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="938e3-139">toopublish a solution toohello Marketplace, follow these steps:</span></span>
1. <span data-ttu-id="938e3-140">符合 hello 非技術性的需求。</span><span class="sxs-lookup"><span data-stu-id="938e3-140">Fulfill hello nontechnical requirements.</span></span>

    <span data-ttu-id="938e3-141">a.</span><span class="sxs-lookup"><span data-stu-id="938e3-141">a.</span></span> <span data-ttu-id="938e3-142">滿足 hello[非技術性的必要條件](marketplace-publishing-pre-requisites.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-142">Fulfill hello [nontechnical prerequisites](marketplace-publishing-pre-requisites.md).</span></span>

    <span data-ttu-id="938e3-143">b.</span><span class="sxs-lookup"><span data-stu-id="938e3-143">b.</span></span> <span data-ttu-id="938e3-144">滿足 hello [VM 技術必要條件](marketplace-publishing-vm-image-creation-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-144">Fulfill hello [VM technical prerequisites](marketplace-publishing-vm-image-creation-prerequisites.md).</span></span>

    <span data-ttu-id="938e3-145">c.</span><span class="sxs-lookup"><span data-stu-id="938e3-145">c.</span></span> <span data-ttu-id="938e3-146">滿足 hello[方案範本技術必要條件](marketplace-publishing-solution-template-creation-prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-146">Fulfill hello [solution template technical prerequisites](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span>

2. <span data-ttu-id="938e3-147">建立您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-147">Create your offer.</span></span>

    <span data-ttu-id="938e3-148">a.</span><span class="sxs-lookup"><span data-stu-id="938e3-148">a.</span></span> <span data-ttu-id="938e3-149">建立[虛擬機器](marketplace-publishing-vm-image-creation.md)供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-149">Create a [virtual machine](marketplace-publishing-vm-image-creation.md) offer.</span></span>

    <span data-ttu-id="938e3-150">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="938e3-150">b.</span></span> <span data-ttu-id="938e3-151">建立[解決方案範本](marketplace-publishing-solution-template-creation.md)供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-151">Create a [solution template](marketplace-publishing-solution-template-creation.md) offer.</span></span>

3. <span data-ttu-id="938e3-152">建立您的供應項目[行銷內容](marketplace-publishing-push-to-staging.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-152">Create your offer [marketing content](marketplace-publishing-push-to-staging.md).</span></span>

4. <span data-ttu-id="938e3-153">在預備環境中測試您的供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-153">Test your offer in staging.</span></span>

    <span data-ttu-id="938e3-154">a.</span><span class="sxs-lookup"><span data-stu-id="938e3-154">a.</span></span> <span data-ttu-id="938e3-155">在[預備環境](marketplace-publishing-vm-image-test-in-staging.md)中測試您的 VM 供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-155">Test your VM offer in [staging](marketplace-publishing-vm-image-test-in-staging.md).</span></span>

    <span data-ttu-id="938e3-156">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="938e3-156">b.</span></span> <span data-ttu-id="938e3-157">在[預備環境](marketplace-publishing-solution-template-test-in-staging.md)中測試您的解決方案範本供應項目。</span><span class="sxs-lookup"><span data-stu-id="938e3-157">Test your solution template offer in [staging](marketplace-publishing-solution-template-test-in-staging.md).</span></span>

5. <span data-ttu-id="938e3-158">部署您的優惠 toohello [Marketplace](marketplace-publishing-push-to-production.md)。</span><span class="sxs-lookup"><span data-stu-id="938e3-158">Deploy your offer toohello [Marketplace](marketplace-publishing-push-to-production.md).</span></span>


### <a name="create-and-manage-a-virtual-machine-image"></a><span data-ttu-id="938e3-159">建立和管理虛擬機器映像</span><span class="sxs-lookup"><span data-stu-id="938e3-159">Create and manage a virtual machine image</span></span>
<span data-ttu-id="938e3-160">使用這些資源來建立和管理 VM 映像︰</span><span class="sxs-lookup"><span data-stu-id="938e3-160">Create and manage a VM image by using these resources:</span></span>
* <span data-ttu-id="938e3-161">建立[內部部署](marketplace-publishing-vm-image-creation-on-premise.md) VM 映像。</span><span class="sxs-lookup"><span data-stu-id="938e3-161">Create a VM image [on-premises](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>
* <span data-ttu-id="938e3-162">建立虛擬機器執行[hello Azure 入口網站中的 Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="938e3-162">Create a virtual machine running [Windows in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="938e3-163">建立虛擬機器執行[hello Azure 入口網站中的 Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="938e3-163">Create a virtual machine running [Linux in hello Azure portal](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="938e3-164">針對 [VHD 建立](marketplace-publishing-vm-image-creation-troubleshooting.md)常見問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="938e3-164">Troubleshoot common issues encountered during [VHD creation](marketplace-publishing-vm-image-creation-troubleshooting.md).</span></span>

## <a name="manage-your-solution"></a><span data-ttu-id="938e3-165">管理您的解決方案</span><span class="sxs-lookup"><span data-stu-id="938e3-165">Manage your solution</span></span>
<span data-ttu-id="938e3-166">管理您的解決方案，協助從 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="938e3-166">Manage your solution with help from hello following resources:</span></span>
* [<span data-ttu-id="938e3-167">虛擬機器的讀取 hello 後製指南提供</span><span class="sxs-lookup"><span data-stu-id="938e3-167">Read hello post-production guide for virtual machine offers</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="938e3-168">更新優惠或 SKU 的 hello 非技術性的詳細資料</span><span class="sxs-lookup"><span data-stu-id="938e3-168">Update hello nontechnical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [<span data-ttu-id="938e3-169">更新優惠或 SKU 的 hello 技術的詳細資料</span><span class="sxs-lookup"><span data-stu-id="938e3-169">Update hello technical details of an offer or a SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [<span data-ttu-id="938e3-170">在已列出的供應項目下新增 SKU</span><span class="sxs-lookup"><span data-stu-id="938e3-170">Add a new SKU under a listed offer</span></span>](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [<span data-ttu-id="938e3-171">變更所列的 SKU hello 資料磁碟計數</span><span class="sxs-lookup"><span data-stu-id="938e3-171">Change hello data disk count for a listed SKU</span></span>](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [<span data-ttu-id="938e3-172">列出的優惠刪除 hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="938e3-172">Delete a listed offer from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md)
* [<span data-ttu-id="938e3-173">從 hello Marketplace 刪除列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="938e3-173">Delete a listed SKU from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="938e3-174">從 hello Marketplace 刪除 hello 目前版本列出的 SKU</span><span class="sxs-lookup"><span data-stu-id="938e3-174">Delete hello current version of a listed SKU from hello Marketplace</span></span>](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [<span data-ttu-id="938e3-175">還原 hello 列出價格 tooproduction 值</span><span class="sxs-lookup"><span data-stu-id="938e3-175">Revert hello listing price tooproduction values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [<span data-ttu-id="938e3-176">還原 hello 計費模型 tooproduction 值</span><span class="sxs-lookup"><span data-stu-id="938e3-176">Revert hello billing model tooproduction values</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [<span data-ttu-id="938e3-177">還原列出的 SKU toohello 生產環境值 hello 可見性設定</span><span class="sxs-lookup"><span data-stu-id="938e3-177">Revert hello visibility setting of a listed SKU toohello production value</span></span>](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [<span data-ttu-id="938e3-178">變更雲端解決方案提供者轉售商獎勵</span><span class="sxs-lookup"><span data-stu-id="938e3-178">Change your Cloud Solution Provider reseller incentive</span></span>](marketplace-publishing-csp-incentive.md)
* [<span data-ttu-id="938e3-179">了解付款報告</span><span class="sxs-lookup"><span data-stu-id="938e3-179">Understand your payout reporting</span></span>](marketplace-publishing-report-payout.md)
* [<span data-ttu-id="938e3-180">以發佈者身分取得支援</span><span class="sxs-lookup"><span data-stu-id="938e3-180">Get support as a publisher</span></span>](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a><span data-ttu-id="938e3-181">其他資源</span><span class="sxs-lookup"><span data-stu-id="938e3-181">Additional resources</span></span>
[<span data-ttu-id="938e3-182">設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="938e3-182">Set up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)
