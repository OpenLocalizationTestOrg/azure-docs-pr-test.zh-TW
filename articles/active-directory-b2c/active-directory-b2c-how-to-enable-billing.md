---
title: "aaaHow tooLink Azure 訂用帳戶 tooAzure AD B2C |Microsoft 文件"
description: "逐步指南 tooenable 計費的 Azure AD B2C 租用戶到 Azure 訂用帳戶。"
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
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a><span data-ttu-id="33e7c-103">連結使用費用 Azure 訂用帳戶 tooan Azure B2C 租用戶 toopay</span><span class="sxs-lookup"><span data-stu-id="33e7c-103">Linking an Azure Subscription tooan Azure B2C tenant toopay for usage charges</span></span>

<span data-ttu-id="33e7c-104">進行中的使用費用，適用於 Azure Active Directory B2C （或 Azure AD B2C） 會使用票據的 tooan Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-104">Ongoing usage charges for Azure Active Directory B2C (or Azure AD B2C) are billed tooan Azure Subscription.</span></span> <span data-ttu-id="33e7c-105">必須為 hello 租用戶系統管理員 tooexplicitly 連結 hello Azure AD B2C 租用戶 tooan 之後建立 hello B2C 租用戶本身的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-105">It is necessary for hello tenant administrator tooexplicitly link hello Azure AD B2C tenant tooan Azure subscription after creating hello B2C tenant itself.</span></span>  <span data-ttu-id="33e7c-106">此連結達成方式是建立 Azure AD"B2C 租用戶 「 hello 目標 Azure 訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="33e7c-106">This link is achieved by creating an Azure AD "B2C Tenant" resource in hello target Azure subscription.</span></span> <span data-ttu-id="33e7c-107">許多 B2C 租用戶可以是連結的 tooa 單一 Azure 訂用帳戶以及其他 Azure 資源 (例如，Vm，資料存放區，LogicApps)</span><span class="sxs-lookup"><span data-stu-id="33e7c-107">Many B2C tenants can be linked tooa single Azure subscription along with other Azure resources (for example, VMs, Data storage, LogicApps)</span></span>


> [!IMPORTANT]
> <span data-ttu-id="33e7c-108">hello 使用量計費和 B2C 位於 hello 遵循頁面上的定價的最新資訊： [Azure AD B2C 定價](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span><span class="sxs-lookup"><span data-stu-id="33e7c-108">hello latest information on usage billing and pricing for B2C is at hello following page: [Azure AD B2C Pricing](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)</span></span>

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="33e7c-109">步驟 1 - 建立 Azure AD B2C 租用戶</span><span class="sxs-lookup"><span data-stu-id="33e7c-109">Step 1 - Create an Azure AD B2C Tenant</span></span>
<span data-ttu-id="33e7c-110">必須先完成 B2C 租用戶建立。</span><span class="sxs-lookup"><span data-stu-id="33e7c-110">B2C tenant creation must be completed first.</span></span> <span data-ttu-id="33e7c-111">如果您已經建立目標 B2C 租用戶，請略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="33e7c-111">Skip this step if you have already created your target B2C Tenant.</span></span> [<span data-ttu-id="33e7c-112">開始使用 Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="33e7c-112">Get started with Azure AD B2C</span></span>](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a><span data-ttu-id="33e7c-113">步驟 2-hello 顯示您的 Azure 訂用帳戶的 Azure AD 租用戶中開啟 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="33e7c-113">Step 2 - Open Azure portal in hello Azure AD Tenant that shows your Azure subscription</span></span>
<span data-ttu-id="33e7c-114">瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="33e7c-114">Navigate toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="33e7c-115">切換 toohello 顯示 hello 希望 toouse 的 Azure 訂用帳戶的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-115">Switch toohello Azure AD Tenant that shows hello Azure subscription you would like toouse.</span></span> <span data-ttu-id="33e7c-116">此 Azure AD 租用戶與不同 hello B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-116">This Azure AD tenant is different from hello B2C tenant.</span></span> <span data-ttu-id="33e7c-117">在 hello Azure 入口網站，按一下 hello 上 hello 右上方的 hello 儀表板 tooselect hello Azure AD 租用戶的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="33e7c-117">Within hello Azure portal, click hello account name on hello upper right of hello dashboard tooselect hello Azure AD Tenant.</span></span> <span data-ttu-id="33e7c-118">Azure 訂用帳戶是必要的 tooproceed。</span><span class="sxs-lookup"><span data-stu-id="33e7c-118">An Azure subscription is needed tooproceed.</span></span> [<span data-ttu-id="33e7c-119">取得 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33e7c-119">Get an Azure Subscription</span></span>](https://account.windowsazure.com/signup?showCatalog=True)

![切換 tooyour Azure AD 租用戶](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a><span data-ttu-id="33e7c-121">步驟 3 - 在 Azure Marketplace 中建立 B2C 租用戶資源</span><span class="sxs-lookup"><span data-stu-id="33e7c-121">Step 3 - Create a B2C Tenant resource in Azure Marketplace</span></span>
<span data-ttu-id="33e7c-122">開啟 Marketplace 按一下 hello Marketplace 圖示，或選取 hello 綠色"+"hello 左上角的 hello 儀表板。</span><span class="sxs-lookup"><span data-stu-id="33e7c-122">Open Marketplace by clicking hello Marketplace icon, or selecting hello green "+" in hello upper left corner of hello dashboard.</span></span>  <span data-ttu-id="33e7c-123">搜尋並選取 Azure Active Directory B2C。</span><span class="sxs-lookup"><span data-stu-id="33e7c-123">Search for and select Azure Active Directory B2C.</span></span> <span data-ttu-id="33e7c-124">選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="33e7c-124">Select Create.</span></span>

![選取 Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![搜尋 AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

<span data-ttu-id="33e7c-127">hello Azure AD B2C 資源建立對話方塊涵蓋 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="33e7c-127">hello Azure AD B2C Resource create dialog covers hello following parameters:</span></span>

1. <span data-ttu-id="33e7c-128">Azure AD B2C 租用戶 – 從 hello 下拉式清單中選取 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-128">Azure AD B2C Tenant – Select an Azure AD B2C Tenant from hello dropdown.</span></span>  <span data-ttu-id="33e7c-129">只會顯示合格的 Azure AD B2C 租用戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-129">Only eligible Azure AD B2C tenants show.</span></span>  <span data-ttu-id="33e7c-130">合格 B2C 租用戶符合這些條件： 您是 hello hello B2C 租用戶的全域系統管理員和 hello B2C 租用戶不是目前相關聯的 tooan Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33e7c-130">Eligible B2C tenants meet these conditions: You are hello global administrator of hello B2C tenant, and hello B2C tenant is not currently associated tooan Azure subscription</span></span>

2. <span data-ttu-id="33e7c-131">Azure AD B2C 資源名稱-是 hello 的 B2C 租用戶的預先選取的 toomatch hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="33e7c-131">Azure AD B2C Resource name - is preselected toomatch hello domain name of hello B2C Tenant</span></span>

3. <span data-ttu-id="33e7c-132">訂用帳戶 - 您身為系統管理員或共同管理員的作用中 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-132">Subscription - An active Azure subscription in which you are an administrator or a co-administrator.</span></span>  <span data-ttu-id="33e7c-133">多個 Azure AD B2C 租用戶加入 tooone Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="33e7c-133">Multiple Azure AD B2C Tenants may be added tooone Azure subscription</span></span>

4. <span data-ttu-id="33e7c-134">資源群組和資源群組位置 - 此構件可協助您安排多個 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="33e7c-134">Resource Group and Resource Group location - This artifact helps you organize multiple Azure resources.</span></span>  <span data-ttu-id="33e7c-135">這個選項對於 B2C 租用戶位置、效能或計費狀態沒有任何影響</span><span class="sxs-lookup"><span data-stu-id="33e7c-135">This choice has no impact on your B2C tenant location, performance, or billing status</span></span>

5. <span data-ttu-id="33e7c-136">釘選最簡單的存取 tooyour B2C 租用戶，帳單資訊和 hello B2C 租用戶設定 toodashboard![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span><span class="sxs-lookup"><span data-stu-id="33e7c-136">Pin toodashboard for easiest access tooyour B2C tenant billing information and hello B2C tenant settings ![Create B2C Resource](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)</span></span>

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a><span data-ttu-id="33e7c-137">步驟 4 - 管理 B2C 租用戶資源 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="33e7c-137">Step 4 - Manage your B2C Tenant resources (optional)</span></span>
<span data-ttu-id="33e7c-138">當部署完成之後，新的 「 B2C 租用戶 「 資源 hello 目標資源群組中所建立，以及相關 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="33e7c-138">Once deployment is complete, a new "B2C Tenant" resource is created in hello target resource group and related Azure subscription.</span></span>  <span data-ttu-id="33e7c-139">您應該會看到您其他的 Azure 資源旁邊新增「B2C 租用戶」類型的新資源。</span><span class="sxs-lookup"><span data-stu-id="33e7c-139">You should see a new resource of type "B2C Tenant" added alongside your other Azure resources.</span></span>

![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

<span data-ttu-id="33e7c-141">藉由按一下 hello B2C 租用戶資源，您就能夠</span><span class="sxs-lookup"><span data-stu-id="33e7c-141">By clicking hello B2C tenant resource, you are able to</span></span>
- <span data-ttu-id="33e7c-142">按一下訂用帳戶名稱 tooreview 帳單資訊。</span><span class="sxs-lookup"><span data-stu-id="33e7c-142">Click Subscription name tooreview billing information.</span></span> <span data-ttu-id="33e7c-143">請參閱「計費和使用量」。</span><span class="sxs-lookup"><span data-stu-id="33e7c-143">See Billing & Usage.</span></span>
- <span data-ttu-id="33e7c-144">按一下 [Azure AD B2C 設定 tooopen 直接 tooyour B2C 租用戶設定] 刀鋒視窗中新的瀏覽器索引標籤</span><span class="sxs-lookup"><span data-stu-id="33e7c-144">Click Azure AD B2C Settings tooopen a new browser tab directly in tooyour B2C tenant Settings blade</span></span>
- <span data-ttu-id="33e7c-145">提交支援要求</span><span class="sxs-lookup"><span data-stu-id="33e7c-145">Submit a support request</span></span>
- <span data-ttu-id="33e7c-146">移動您 B2C 租用戶資源 tooanother Azure 訂用帳戶或 tooanother 資源群組。</span><span class="sxs-lookup"><span data-stu-id="33e7c-146">Move your B2C tenant resource tooanother Azure Subscription, or tooanother Resource Group.</span></span>  <span data-ttu-id="33e7c-147">這個選項會變更哪一個 Azure 訂用帳戶會收到使用費用。</span><span class="sxs-lookup"><span data-stu-id="33e7c-147">This choice changes which Azure subscription receives usage charges.</span></span>

![B2C 資源設定](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a><span data-ttu-id="33e7c-149">已知問題</span><span class="sxs-lookup"><span data-stu-id="33e7c-149">Known Issues</span></span>
- <span data-ttu-id="33e7c-150">B2C 租用戶刪除。</span><span class="sxs-lookup"><span data-stu-id="33e7c-150">B2C Tenant deletion.</span></span> <span data-ttu-id="33e7c-151">建立 B2C 租用戶時，如果刪除，並重新建立與 hello 相同的網域名稱，請也刪除並重新建立以 hello hello 「 連結 」 資源相同的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="33e7c-151">If a B2C Tenant is created, deleted, and re-created with hello same domain name, please also delete and re-create hello "Linking" resource with hello same domain name.</span></span>  <span data-ttu-id="33e7c-152">您會發現這在 hello 訂用帳戶的租用戶透過 hello Azure 入口網站中 「 連結 」 [資源] 下所有資源。</span><span class="sxs-lookup"><span data-stu-id="33e7c-152">You will find this "Linking" resource under "All resources" in hello subscription tenant via hello Azure portal.</span></span>
- <span data-ttu-id="33e7c-153">在區域資源位置自我強加的限制。</span><span class="sxs-lookup"><span data-stu-id="33e7c-153">Self-imposed restrictions on regional resource location.</span></span>  <span data-ttu-id="33e7c-154">在罕見的情況下，使用者可能針對建立 Azure 資源建立了區域限制。</span><span class="sxs-lookup"><span data-stu-id="33e7c-154">In rare cases, a user may have established a regional restriction for Azure resource creation.</span></span>  <span data-ttu-id="33e7c-155">這項限制可能會導致 hello 建立 hello 連結 Azure 訂用帳戶和 B2C 租用戶之間。</span><span class="sxs-lookup"><span data-stu-id="33e7c-155">This restriction may prevent hello creation of hello Link between an Azure subscription and a B2C Tenant.</span></span> <span data-ttu-id="33e7c-156">toomitigate，請放寬這項限制。</span><span class="sxs-lookup"><span data-stu-id="33e7c-156">toomitigate, please relax this restriction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33e7c-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33e7c-157">Next steps</span></span>
<span data-ttu-id="33e7c-158">針對每個 B2C 租用戶完成這些步驟後，您的 Azure 訂用帳戶就會根據 Azure 直接或企業合約詳細資料計費。</span><span class="sxs-lookup"><span data-stu-id="33e7c-158">Once these steps are complete for each of your B2C tenants, your Azure subscription is billed in accordance with your Azure Direct or Enterprise Agreement details.</span></span>
- <span data-ttu-id="33e7c-159">檢閱您選取的 Azure 訂用帳戶內的使用量和計費</span><span class="sxs-lookup"><span data-stu-id="33e7c-159">Review usage and billing within your selected Azure subscription</span></span>
- <span data-ttu-id="33e7c-160">檢閱詳細的每一天使用量報告使用 hello[使用量報告 API](active-directory-b2c-reference-usage-reporting-api.md)</span><span class="sxs-lookup"><span data-stu-id="33e7c-160">Review detailed day-by-day usage reports using hello [Usage Reporting API](active-directory-b2c-reference-usage-reporting-api.md)</span></span>
