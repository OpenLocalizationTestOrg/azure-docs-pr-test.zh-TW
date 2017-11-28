---
title: "解決現有 Azure AD Domain Services 受管理的網域的不相符目錄錯誤 | Microsoft Docs"
description: "了解並解決現有 Azure AD Domain Services 受管理的網域的不相符目錄錯誤"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 40eb75b7-827e-4d30-af6c-ca3c2af915c7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: 
ms.date: 07/06/2017
ms.author: maheshu
ms.openlocfilehash: ca9ff29f5f91b8d796a29706ab49a82e417d1ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-mismatched-directory-errors-for-existing-azure-ad-domain-services-managed-domains"></a><span data-ttu-id="66cba-103">解決現有 Azure AD Domain Services 受管理的網域的不相符目錄錯誤</span><span class="sxs-lookup"><span data-stu-id="66cba-103">Resolve mismatched directory errors for existing Azure AD Domain Services managed domains</span></span>
<span data-ttu-id="66cba-104">您有使用 Azure 傳統入口網站啟用的現有受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-104">You have an existing managed domain that was enabled using the Azure classic portal.</span></span> <span data-ttu-id="66cba-105">當您瀏覽至新的 Azure 入口網站並檢視受管理的網域時，您會看到下列錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="66cba-105">When you navigate to the new Azure portal and view the managed domain, you see the following error message:</span></span>

![不相符目錄錯誤](.\media\getting-started\mismatched-tenant-error.png)

<span data-ttu-id="66cba-107">在解決錯誤之前，您無法管理此受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-107">You cannot administer this managed domain until the error is resolved.</span></span>


## <a name="whats-causing-this-error"></a><span data-ttu-id="66cba-108">造成這個錯誤的原因是什麼？</span><span class="sxs-lookup"><span data-stu-id="66cba-108">What's causing this error?</span></span>
<span data-ttu-id="66cba-109">這個錯誤是在受管理的網域和在其中啟用的虛擬網路分別屬於兩個不同 Azure AD 租用戶時造成的。</span><span class="sxs-lookup"><span data-stu-id="66cba-109">This error is caused when your managed domain and the virtual network it is enabled in belong to two different Azure AD tenants.</span></span> <span data-ttu-id="66cba-110">例如，您有名為 'contoso.com' 的受管理的網域，它針對 Contoso 的 Azure AD 租用戶啟用。</span><span class="sxs-lookup"><span data-stu-id="66cba-110">For example, you have a managed domain called 'contoso.com' and it was enabled for Contoso's Azure AD tenant.</span></span> <span data-ttu-id="66cba-111">不過，在其中啟用受管理的網域的 Azure 虛擬網路屬於 Fabrikam - 不同的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="66cba-111">However, the Azure virtual network in which the managed domain was enabled belongs to Fabrikam - a different Azure AD tenant.</span></span>

<span data-ttu-id="66cba-112">新的 Azure 入口網站 (特別是 Azure AD Domain Services 延擴充) 是建置在 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="66cba-112">The new Azure portal (and specifically the Azure AD Domain Services extension) is built on Azure Resource Manager.</span></span> <span data-ttu-id="66cba-113">在現代的 Azure Resource Manager 環境中，會強制執行特定限制，為資源提供更高的安全性和角色型存取控制 (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="66cba-113">In the modern Azure Resource Manager environment, certain restrictions are enforced to deliver greater security and for roles-based access control (RBAC) to resources.</span></span> <span data-ttu-id="66cba-114">為 Azure AD 租用戶啟用 Azure AD Domain Services 是敏感的作業，因為它會導致認證雜湊同步處理至受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-114">Enabling Azure AD Domain Services for an Azure AD tenant is a sensitive operation since it causes credential hashes to be synchronized to the managed domain.</span></span> <span data-ttu-id="66cba-115">這項作業需要您是目錄的租用戶管理員。</span><span class="sxs-lookup"><span data-stu-id="66cba-115">This operation requires you to be a tenant admin for the directory.</span></span> <span data-ttu-id="66cba-116">此外，您必須具有要在其中啟用受管理的網域之虛擬網路的系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="66cba-116">Additionally, you must have administrative privileges over the virtual network in which you enable the managed domain.</span></span> <span data-ttu-id="66cba-117">為了讓 RBAC 檢查能夠順利運作，受管理的網域和虛擬網路應該屬於相同 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="66cba-117">For the RBAC checks to work consistently, the managed domain and the virtual network should belong to the same Azure AD tenant.</span></span>

<span data-ttu-id="66cba-118">簡單來說，您無法在屬於另一個 Azure AD 租用戶 'fabrikam.com' 擁有之 Azure 訂用帳戶的虛擬網路中，針對 Azure AD 租用戶 'contoso.com' 啟用受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-118">In short, you cannot enable a managed domain for an Azure AD tenant 'contoso.com' in a virtual network belonging to an Azure subscription owned by another Azure AD tenant 'fabrikam.com'.</span></span> <span data-ttu-id="66cba-119">Azure 傳統入口網站未建置在資源管理員平台上，並且不會強制這類限制。</span><span class="sxs-lookup"><span data-stu-id="66cba-119">The Azure classic portal isn't built on top of the Resource Manager platform and does not enforce such restrictions.</span></span>

<span data-ttu-id="66cba-120">**有效設定**：在此案例中，Contoso 受管理的網域是針對 Contoso Azure AD 租用戶啟用。</span><span class="sxs-lookup"><span data-stu-id="66cba-120">**Valid configuration**: In this deployment scenario, the Contoso managed domain is enabled for the Contoso Azure AD tenant.</span></span> <span data-ttu-id="66cba-121">受管理的網域會在屬於 Contoso Azure AD 租用戶擁有之 Azure 訂用帳戶的虛擬網路中公開。</span><span class="sxs-lookup"><span data-stu-id="66cba-121">The managed domain is exposed in a virtual network belonging to an Azure subscription owned by the Contoso Azure AD tenant.</span></span> <span data-ttu-id="66cba-122">因此，受管理的網域以及虛擬網路屬於相同的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="66cba-122">Therefore, both the managed domain as well as the virtual network belong to the same Azure AD tenant.</span></span> <span data-ttu-id="66cba-123">此設定有效且完全受到支援。</span><span class="sxs-lookup"><span data-stu-id="66cba-123">This configuration is valid and fully supported.</span></span>

![有效租用戶設定](./media/getting-started/valid-tenant-config.png)

<span data-ttu-id="66cba-125">**不相符租用戶設定**：在此案例中，Contoso 受管理的網域是針對 Contoso Azure AD 租用戶啟用。</span><span class="sxs-lookup"><span data-stu-id="66cba-125">**Mismatched tenant configuration**: In this deployment scenario, the Contoso managed domain is enabled for the Contoso Azure AD tenant.</span></span> <span data-ttu-id="66cba-126">但是，受管理的網域會在屬於 Fabrikam Azure AD 租用戶擁有之 Azure 訂用帳戶的虛擬網路中公開。</span><span class="sxs-lookup"><span data-stu-id="66cba-126">However, the managed domain is exposed in a virtual network that belongs to an Azure subscription owned by the Fabrikam Azure AD tenant.</span></span> <span data-ttu-id="66cba-127">因此，受管理的網域和虛擬網路分別屬於兩個不同的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="66cba-127">Therefore, the managed domain and the virtual network belong to two different Azure AD tenants.</span></span> <span data-ttu-id="66cba-128">此設定是不相符租用戶設定，不受到支援。</span><span class="sxs-lookup"><span data-stu-id="66cba-128">This configuration is the mismatched tenant configuration and is not supported.</span></span> <span data-ttu-id="66cba-129">虛擬網路必須移至與受管理的網域相同的 Azure AD 租用戶 (也就是 Contoso)。</span><span class="sxs-lookup"><span data-stu-id="66cba-129">The virtual network must be moved to the same Azure AD tenant (that is, Contoso) as the managed domain.</span></span> <span data-ttu-id="66cba-130">如需詳細資訊，請參閱[解決方案](#resolution)一節。</span><span class="sxs-lookup"><span data-stu-id="66cba-130">See the [Resolution](#resolution) section for details.</span></span>

![不相符租用戶設定](./media/getting-started/mismatched-tenant-config.png)

<span data-ttu-id="66cba-132">因此，在受管理的網域和在其中啟用的虛擬網路分別屬於兩個不同 Azure AD 租用戶的案例中，您會看到這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="66cba-132">Therefore, in scenarios where the managed domain and the virtual network it is enabled in belong to two different Azure AD tenants you see this error.</span></span>

<span data-ttu-id="66cba-133">下列規則適用於資源管理員環境：</span><span class="sxs-lookup"><span data-stu-id="66cba-133">The following rules apply in the Resource Manager environment:</span></span>
- <span data-ttu-id="66cba-134">Azure AD 目錄有多個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="66cba-134">An Azure AD directory may have multiple Azure subscriptions.</span></span>
- <span data-ttu-id="66cba-135">Azure 訂用帳戶有多個資源，例如虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="66cba-135">An Azure subscription may have multiple resources such as virtual networks.</span></span>
- <span data-ttu-id="66cba-136">Azure AD 目錄已啟用單一 Azure AD Domain Services 受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-136">A single Azure AD Domain Services managed domain is enabled for an Azure AD directory.</span></span>
- <span data-ttu-id="66cba-137">Azure AD Domain Services 受管理的網域可以在屬於相同 Azure AD 租用戶內之任何 Azure 訂用帳戶的虛擬網路上啟用。</span><span class="sxs-lookup"><span data-stu-id="66cba-137">An Azure AD Domain Services managed domain can be enabled on a virtual network belonging to any of the Azure subscriptions within the same Azure AD tenant.</span></span>


## <a name="resolution"></a><span data-ttu-id="66cba-138">解決方案</span><span class="sxs-lookup"><span data-stu-id="66cba-138">Resolution</span></span>
<span data-ttu-id="66cba-139">您有兩個選項可以用來解決不相符目錄錯誤。</span><span class="sxs-lookup"><span data-stu-id="66cba-139">You have two options to resolve the mismatched directory error.</span></span> <span data-ttu-id="66cba-140">您可以：</span><span class="sxs-lookup"><span data-stu-id="66cba-140">You may:</span></span>

- <span data-ttu-id="66cba-141">按一下 [刪除] 按鈕，刪除現有的受管理的網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-141">Click the **Delete** button to delete the existing managed domain.</span></span> <span data-ttu-id="66cba-142">使用 [Azure 入口網站](https://portal.azure.com)重新建立，讓受管理的網域和可用的虛擬網路屬於 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="66cba-142">Re-create using the [Azure portal](https://portal.azure.com), so that the managed domain and virtual network it is available in belong to the Azure AD directory.</span></span> <span data-ttu-id="66cba-143">您必須重新加入新建立的受管理網域，先前的所有機器加入已刪除網域。</span><span class="sxs-lookup"><span data-stu-id="66cba-143">You must join afresh to the newly created managed domain, all machines previously joined to the deleted domain.</span></span>

- <span data-ttu-id="66cba-144">請連絡 Azure 支援中心，將包含虛擬網路的 Azure 訂用帳戶移至受管理的網域所屬的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="66cba-144">Contact Azure support to move the Azure subscription containing the virtual network to the Azure AD directory, to which your managed domain belongs.</span></span> <span data-ttu-id="66cba-145">按一下 [新增支援要求] 並且在支援要求的 [詳細資料] 區段中指定**不相符目錄**。</span><span class="sxs-lookup"><span data-stu-id="66cba-145">Click **New support request** and specify **mismatched directory** in the **Details** section of the support request.</span></span> <span data-ttu-id="66cba-146">包含錯誤訊息中提供的資訊作為支援要求的一部分。</span><span class="sxs-lookup"><span data-stu-id="66cba-146">Include the information provided in the error message as part of the support request.</span></span>


## <a name="related-content"></a><span data-ttu-id="66cba-147">相關內容</span><span class="sxs-lookup"><span data-stu-id="66cba-147">Related content</span></span>
* [<span data-ttu-id="66cba-148">Azure AD Domain Services - 入門指南</span><span class="sxs-lookup"><span data-stu-id="66cba-148">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="66cba-149">疑難排解指南 - Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="66cba-149">Troubleshooting guide - Azure AD Domain Services</span></span>](active-directory-ds-troubleshooting.md)
