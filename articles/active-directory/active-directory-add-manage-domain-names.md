---
title: "管理 Azure Active Directory 中的自訂網域名稱 | Microsoft Docs"
description: "管理概念和管理 Azure Active Directory 自訂網域的做法"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 5ae19bb370064de96cf466ca09b13d02563d65a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="94480-103">管理 Azure Active Directory 中的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="94480-104">網域名稱可以是許多目錄資源的重要識別碼，其屬於：</span><span class="sxs-lookup"><span data-stu-id="94480-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="94480-105">使用者的使用者名稱或電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="94480-105">A user name or email address for a user</span></span>
* <span data-ttu-id="94480-106">群組的位址</span><span class="sxs-lookup"><span data-stu-id="94480-106">The address for a group</span></span>
* <span data-ttu-id="94480-107">應用程式的應用程式識別碼 URI</span><span class="sxs-lookup"><span data-stu-id="94480-107">The app ID URI for an application</span></span>

<span data-ttu-id="94480-108">Azure Active Directory (Azure AD) 中的資源可包含已驗證為目錄 (其中含有資源) 所擁有的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified to be owned by the directory that contains the resource.</span></span> <span data-ttu-id="94480-109">只有全域管理員可以在 Azure AD 中執行網域管理工作。</span><span class="sxs-lookup"><span data-stu-id="94480-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94480-110">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="94480-110">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="94480-111">如需如何在 Azure AD 系統管理中心管理網域名稱的相關資訊，請參閱[在 Azure Active Directory 中管理自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="94480-111">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="94480-112">設定 Azure AD 目錄的主要網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-112">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="94480-113">在您建立目錄時，初始網域名稱也是目錄的主要網域名稱，例如 'contoso.onmicrosoft.com'。</span><span class="sxs-lookup"><span data-stu-id="94480-113">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name for your directory.</span></span> <span data-ttu-id="94480-114">當您在 [Azure 傳統入口網站](https://manage.windowsazure.com/)或其他入口網站 (例如 Office 365 管理入口網站) 建立新的使用者時，主要網域即為新使用者的預設網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-114">The primary domain is the default domain name for a new user when you create a new user in the [Azure classic portal](https://manage.windowsazure.com/), or other portals such as the Office 365 admin portal.</span></span> <span data-ttu-id="94480-115">這可以簡化系統管理員在入口網站中建立新使用者的程序。</span><span class="sxs-lookup"><span data-stu-id="94480-115">This streamlines the process for an administrator to create new users in the portal.</span></span>

<span data-ttu-id="94480-116">若要變更目錄的主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="94480-116">To change the primary domain name for your directory:</span></span>

1. <span data-ttu-id="94480-117">使用屬於 Azure AD目錄全域管理員的使用者帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="94480-117">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="94480-118">在左側的導覽列上選取 [Active Directory]  。</span><span class="sxs-lookup"><span data-stu-id="94480-118">Select **Active Directory** on the left navigation bar.</span></span>
3. <span data-ttu-id="94480-119">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="94480-119">Open your directory.</span></span>
4. <span data-ttu-id="94480-120">選取 [網域]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="94480-120">Select the **Domains** tab.</span></span>
5. <span data-ttu-id="94480-121">選取命令列上的 [變更主要網域]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="94480-121">Select the **Change primary** button on the command bar.</span></span>
6. <span data-ttu-id="94480-122">選取您想要設為目錄之新主要網域的網域。</span><span class="sxs-lookup"><span data-stu-id="94480-122">Select the domain that you want to be the new primary domain for your directory.</span></span>

<span data-ttu-id="94480-123">您可以將目錄的主要網域名稱變更為任何已驗證的非同盟自訂網域。</span><span class="sxs-lookup"><span data-stu-id="94480-123">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="94480-124">變更目錄的主要網域時，並不會變更任何現有使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-124">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="94480-125">新增 Azure AD 的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-125">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="94480-126">您可以為每個 Azure AD 目錄新增最多 900 個自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-126">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="94480-127">[新增其他自訂網域名稱](active-directory-add-domain.md) 的程序與新增第一個自訂網域名稱相同。</span><span class="sxs-lookup"><span data-stu-id="94480-127">The process to [add an additional custom domain name](active-directory-add-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="94480-128">新增自訂網域的子網域</span><span class="sxs-lookup"><span data-stu-id="94480-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="94480-129">如果您想要將第三層網域名稱新增至您的目錄，例如 'europe.contoso.com'，則應先新增並驗證第二層網域，例如 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="94480-129">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com.</span></span> <span data-ttu-id="94480-130">Azure AD 會自動驗證子網域。</span><span class="sxs-lookup"><span data-stu-id="94480-130">The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="94480-131">若要查看您剛才加入的子網域是否已通過驗證，請重新整理列出您目錄網域的瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="94480-131">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains in your directory.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="94480-132">如果您變更您的自訂網域名稱的 DNS 註冊機構，該怎麼辦</span><span class="sxs-lookup"><span data-stu-id="94480-132">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="94480-133">如果您變更自訂網域名稱的 DNS 註冊機構，仍可以繼續在 Azure AD 中使用自訂網域名稱而不會中斷，且不需要其他組態工作。</span><span class="sxs-lookup"><span data-stu-id="94480-133">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="94480-134">如果您的自訂網域名稱搭配使用 Office 365、Intune 或仰賴 Azure AD 自訂網域名稱的其他服務，則請參閱這些服務的文件。</span><span class="sxs-lookup"><span data-stu-id="94480-134">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="94480-135">刪除自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-135">Delete a custom domain name</span></span>
<span data-ttu-id="94480-136">如果貴組織不再使用該網域名稱，或如果您需要在另一個 Azure AD 中使用該網域名稱，您可以從您的 Azure AD 刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-136">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="94480-137">若要刪除自訂網域名稱，您必須先確定目錄中沒有任何資源仰賴該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-137">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="94480-138">如果有下列情況，即無法刪除目錄的網域名稱：</span><span class="sxs-lookup"><span data-stu-id="94480-138">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="94480-139">有任何使用者的使用者名稱、電子郵件地址或 Proxy 位址包含該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-139">Any user has a user name, email address, or proxy address that include the domain name.</span></span>
* <span data-ttu-id="94480-140">有任何群組的電子郵件地址或 Proxy 位址包含該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-140">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="94480-141">Azure AD 中任何應用程式的應用程式識別碼 URI 包括該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-141">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="94480-142">您必須變更或刪除 Azure AD 目錄中任何這類資源，才能刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="94480-142">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="94480-143">使用 PowerShell 或圖形 API 來管理網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-143">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="94480-144">在 Azure Active Directory 中，大部分的網域名稱管理工作也都可以使用 Microsoft PowerShell 來完成，或使用 Azure AD 圖形 API 以程式設計方式來完成。</span><span class="sxs-lookup"><span data-stu-id="94480-144">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="94480-145">使用 PowerShell 管理 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-145">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="94480-146">使用圖形 API 管理 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-146">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="94480-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94480-147">Next steps</span></span>
* [<span data-ttu-id="94480-148">了解 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-148">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="94480-149">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="94480-149">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

