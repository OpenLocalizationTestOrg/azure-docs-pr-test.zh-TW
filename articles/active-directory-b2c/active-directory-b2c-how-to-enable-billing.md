---
title: "如何將 Azure 訂用帳戶連結到 Azure AD B2C | Microsoft Docs"
description: "啟用 Azure 訂用帳戶內 Azure AD B2C 租用戶計費的逐步指南。"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 5b9955b2af7f20a79981315fa33a0eb5380a5465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="linking-an-azure-subscription-to-an-azure-b2c-tenant-to-pay-for-usage-charges"></a><span data-ttu-id="30cb3-103">將 Azure 訂用帳戶連結至 Azure B2C 租用戶以支付使用費用</span><span class="sxs-lookup"><span data-stu-id="30cb3-103">Linking an Azure Subscription to an Azure B2C tenant to pay for usage charges</span></span>

<span data-ttu-id="30cb3-104">Azure Active Directory B2C (或 Azure AD B2C) 的持續使用費用會計入 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed to an Azure Subscription.</span></span> <span data-ttu-id="30cb3-105">建立 B2C 租用戶本身之後，租用戶系統管理員必須明確地將 Azure AD B2C 租用戶連結至 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-105">It is necessary for the tenant administrator to explicitly link the Azure AD B2C tenant to an Azure subscription after creating the B2C tenant itself.</span></span>  <span data-ttu-id="30cb3-106">在目標 Azure 訂用帳戶中建立 Azure AD「B2C 租用戶」資源，即可達成此連結。</span><span class="sxs-lookup"><span data-stu-id="30cb3-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in the target Azure subscription.</span></span> <span data-ttu-id="30cb3-107">許多 B2C 租用戶可以連結至單一 Azure 訂用帳戶以及其他 Azure 資源 (例如，VM、資料儲存體、LogicApps)</span><span class="sxs-lookup"><span data-stu-id="30cb3-107">Many B2C tenants can be linked to a single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span></span>


> [!IMPORTANT]
> <span data-ttu-id="30cb3-108">B2C 的最新使用計費和價格資訊位於下列網頁︰[Azure AD B2C 價格](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="30cb3-108">The latest information on usage billing and pricing for B2C is at the following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span></span>

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="30cb3-109">步驟 1 - 建立 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="30cb3-109">Step 1 - Create an Azure AD B2C Tenant</span></span>
<span data-ttu-id="30cb3-110">必須先完成 B2C 租用戶建立。</span><span class="sxs-lookup"><span data-stu-id="30cb3-110">B2C tenant creation must be completed first.</span></span> <span data-ttu-id="30cb3-111">如果您已經建立目標 B2C 租用戶，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="30cb3-111">Skip this step if you have already created your target B2C Tenant.</span></span> [<span data-ttu-id="30cb3-112">開始使用 Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="30cb3-112">Get started with Azure AD B2C</span></span>](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-the-azure-ad-tenant-that-shows-your-azure-subscription"></a><span data-ttu-id="30cb3-113">步驟 2 - 在 Azure AD 租用戶中開啟 Azure 入口網站，以顯示您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="30cb3-113">Step 2 - Open Azure portal in the Azure AD Tenant that shows your Azure subscription</span></span>
<span data-ttu-id="30cb3-114">瀏覽至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="30cb3-114">Navigate to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="30cb3-115">切換至 Azure AD 租用戶，以顯示您想要使用的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-115">Switch to the Azure AD Tenant that shows the Azure subscription you would like to use.</span></span> <span data-ttu-id="30cb3-116">此 Azure AD 租用戶與 B2C 租用戶不同。</span><span class="sxs-lookup"><span data-stu-id="30cb3-116">This Azure AD tenant is different from the B2C tenant.</span></span> <span data-ttu-id="30cb3-117">在 Azure 入口網站中，按一下儀表板右上角的帳戶名稱以選取 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-117">Within the Azure portal, click the account name on the upper right of the dashboard to select the Azure AD Tenant.</span></span> <span data-ttu-id="30cb3-118">需要有 Azure 訂用帳戶才能繼續執行。</span><span class="sxs-lookup"><span data-stu-id="30cb3-118">An Azure subscription is needed to proceed.</span></span> [<span data-ttu-id="30cb3-119">取得 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="30cb3-119">Get an Azure Subscription</span></span>](https://account.windowsazure.com/signup?showCatalog=True)

![切換至 Azure AD 租用戶](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a><span data-ttu-id="30cb3-121">步驟 3 - 在 Azure Marketplace 中建立 B2C 租用戶資源</span><span class="sxs-lookup"><span data-stu-id="30cb3-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span></span>
<span data-ttu-id="30cb3-122">按一下 [Marketplace] 圖示開啟 [Marketplace]，或選取儀表板的左上角的綠色 "+"。</span><span class="sxs-lookup"><span data-stu-id="30cb3-122">Open Marketplace by clicking the Marketplace icon, or selecting the green "+" in the upper left corner of the dashboard.</span></span>  <span data-ttu-id="30cb3-123">搜尋並選取 Azure Active Directory B2C。</span><span class="sxs-lookup"><span data-stu-id="30cb3-123">Search for and select Azure Active Directory B2C.</span></span> <span data-ttu-id="30cb3-124">選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="30cb3-124">Select Create.</span></span>

![選取 Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![搜尋 AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

<span data-ttu-id="30cb3-127">[Azure AD B2C 資源建立] 對話方塊包含下列參數︰</span><span class="sxs-lookup"><span data-stu-id="30cb3-127">The Azure AD B2C Resource create dialog covers the following parameters:</span></span>

1. <span data-ttu-id="30cb3-128">Azure AD B2C 租用戶 – 從下拉式清單選取 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from the dropdown.</span></span>  <span data-ttu-id="30cb3-129">只會顯示合格的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-129">Only eligible Azure AD B2C tenants show.</span></span>  <span data-ttu-id="30cb3-130">合格的 B2C 租用戶符合以下條件︰您是 B2C 租用戶的全域管理員，而且 B2C 租用戶目前並未與 Azure 訂用帳戶相關聯</span><span class="sxs-lookup"><span data-stu-id="30cb3-130">Eligible B2C tenants meet these conditions: You are the global administrator of the B2C tenant, and the B2C tenant is not currently associated to an Azure subscription</span></span>

2. <span data-ttu-id="30cb3-131">Azure AD B2C 資源名稱 - 已預先選，以符合 B2C 租用戶的網域名稱</span><span class="sxs-lookup"><span data-stu-id="30cb3-131">Azure AD B2C Resource name - is preselected to match the domain name of the B2C Tenant</span></span>

3. <span data-ttu-id="30cb3-132">訂用帳戶 - 您身為系統管理員或共同管理員的作用中 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="30cb3-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span></span>  <span data-ttu-id="30cb3-133">可以將多個 Azure AD B2C 租用戶新增至一個 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="30cb3-133">Multiple Azure AD B2C Tenants may be added to one Azure subscription</span></span>

4. <span data-ttu-id="30cb3-134">資源群組和資源群組位置 - 此構件可協助您安排多個 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="30cb3-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span></span>  <span data-ttu-id="30cb3-135">這個選項對於 B2C 租用戶位置、效能或計費狀態沒有任何影響</span><span class="sxs-lookup"><span data-stu-id="30cb3-135">This choice has no impact on your B2C tenant location, performance, or billing status</span></span>

5. <span data-ttu-id="30cb3-136">釘選到儀表板，即可輕鬆存取您的 B2C 租用戶帳單資訊和 B2C 租用戶設定![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span><span class="sxs-lookup"><span data-stu-id="30cb3-136">Pin to dashboard for easiest access to your B2C tenant billing information and the B2C tenant settings ![Create B2C Resource](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span></span>

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a><span data-ttu-id="30cb3-137">步驟 4 - 管理 B2C 租用戶資源 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="30cb3-137">Step 4 - Manage your B2C Tenant resources (optional)</span></span>
<span data-ttu-id="30cb3-138">部署完成後，新的「B2C 租用戶」資源便建立於目標資源群組和相關 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="30cb3-138">Once deployment is complete, a new "B2C Tenant" resource is created in the target resource group and related Azure subscription.</span></span>  <span data-ttu-id="30cb3-139">您應該會看到您其他的 Azure 資源旁邊新增「B2C 租用戶」類型的新資源。</span><span class="sxs-lookup"><span data-stu-id="30cb3-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span></span>

![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

<span data-ttu-id="30cb3-141">按一下 B2C 租用戶資源，您就能夠</span><span class="sxs-lookup"><span data-stu-id="30cb3-141">By clicking the B2C tenant resource, you are able to</span></span>
- <span data-ttu-id="30cb3-142">按一下訂用帳戶名稱，以檢閱帳單資訊。</span><span class="sxs-lookup"><span data-stu-id="30cb3-142">Click Subscription name to review billing information.</span></span> <span data-ttu-id="30cb3-143">請參閱「計費和使用量」。</span><span class="sxs-lookup"><span data-stu-id="30cb3-143">See Billing & Usage.</span></span>
- <span data-ttu-id="30cb3-144">按一下 [Azure AD B2C 設定]，以在 [B2C 租用戶設定] 刀鋒視窗中直接開啟新的瀏覽器索引標籤</span><span class="sxs-lookup"><span data-stu-id="30cb3-144">Click Azure AD B2C Settings to open a new browser tab directly in to your B2C tenant Settings blade</span></span>
- <span data-ttu-id="30cb3-145">提交支援要求</span><span class="sxs-lookup"><span data-stu-id="30cb3-145">Submit a support request</span></span>
- <span data-ttu-id="30cb3-146">將 B2C 租用戶資源移至另一個 Azure 訂用帳戶，或另一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="30cb3-146">Move your B2C tenant resource to another Azure Subscription, or to another Resource Group.</span></span>  <span data-ttu-id="30cb3-147">這個選項會變更哪一個 Azure 訂用帳戶會收到使用費用。</span><span class="sxs-lookup"><span data-stu-id="30cb3-147">This choice changes which Azure subscription receives usage charges.</span></span>

![B2C 資源設定](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a><span data-ttu-id="30cb3-149">已知問題</span><span class="sxs-lookup"><span data-stu-id="30cb3-149">Known Issues</span></span>
- <span data-ttu-id="30cb3-150">B2C 租用戶刪除。</span><span class="sxs-lookup"><span data-stu-id="30cb3-150">B2C Tenant deletion.</span></span> <span data-ttu-id="30cb3-151">如果在建立「B2C 租用戶」之後，將其刪除再以相同的網域名稱重新建立，請將「連結」資源也一併刪除再以相同的網域名稱重新建立。</span><span class="sxs-lookup"><span data-stu-id="30cb3-151">If a B2C Tenant is created, deleted, and re-created with the same domain name, please also delete and re-create the "Linking" resource with the same domain name.</span></span>  <span data-ttu-id="30cb3-152">您可以透過 Azure 入口網站，在訂用帳戶租用戶中的 [所有資源] 底下找到這個「連結」資源。</span><span class="sxs-lookup"><span data-stu-id="30cb3-152">You will find this "Linking" resource under "All resources" in the subscription tenant via the Azure portal.</span></span>
- <span data-ttu-id="30cb3-153">在區域資源位置自我強加的限制。</span><span class="sxs-lookup"><span data-stu-id="30cb3-153">Self-imposed restrictions on regional resource location.</span></span>  <span data-ttu-id="30cb3-154">在罕見的情況下，使用者可能針對建立 Azure 資源建立了區域限制。</span><span class="sxs-lookup"><span data-stu-id="30cb3-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span></span>  <span data-ttu-id="30cb3-155">此限制可能會導致無法在 Azure 訂用帳戶與「B2C 租用戶」之間建立「連結」。</span><span class="sxs-lookup"><span data-stu-id="30cb3-155">This restriction may prevent the creation of the Link between an Azure subscription and a B2C Tenant.</span></span> <span data-ttu-id="30cb3-156">若要減輕此問題的影響，請放寬這項限制。</span><span class="sxs-lookup"><span data-stu-id="30cb3-156">To mitigate, please relax this restriction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30cb3-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30cb3-157">Next steps</span></span>
<span data-ttu-id="30cb3-158">針對每個 B2C 租用戶完成這些步驟後，您的 Azure 訂用帳戶就會根據 Azure 直接或企業合約詳細資料計費。</span><span class="sxs-lookup"><span data-stu-id="30cb3-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span></span>
- <span data-ttu-id="30cb3-159">檢閱您選取的 Azure 訂用帳戶內的使用量和計費</span><span class="sxs-lookup"><span data-stu-id="30cb3-159">Review usage and billing within your selected Azure subscription</span></span>
- <span data-ttu-id="30cb3-160">使用[使用量報告 API](active-directory-b2c-reference-usage-reporting-api.md) 來檢閱詳細的每天使用量報告</span><span class="sxs-lookup"><span data-stu-id="30cb3-160">Review detailed day-by-day usage reports using the [Usage Reporting API](active-directory-b2c-reference-usage-reporting-api.md)</span></span>
