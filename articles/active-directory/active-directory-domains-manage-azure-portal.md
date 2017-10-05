---
title: "管理 Azure Active Directory 中的自訂網域名稱 | Microsoft Docs"
description: "Azure Active Directory 中管理網域的管理概念和做法"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 402c1be07b8ee885ee5341128fb3f419611b924d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="14a31-103">管理 Azure Active Directory 中的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="14a31-104">網域名稱是許多目錄資源識別項的重要部分：它可能是使用者的使用者名稱或電子郵件地址的一部分、群組位址的一部分，也可能是應用程式的應用程式識別碼 URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="14a31-104">A domain name is an important part of the identifier for many directory resources: it is part of a user name or email address for a user, part of the address for a group, and can be part of the app ID URI for an application.</span></span> <span data-ttu-id="14a31-105">Azure Active Directory (Azure AD) 中的資源可包含已驗證為目錄 (其中含有資源) 所擁有的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by the directory that contains the resource.</span></span> <span data-ttu-id="14a31-106">只有全域管理員可以在 Azure AD 中執行網域管理工作。</span><span class="sxs-lookup"><span data-stu-id="14a31-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="14a31-107">設定 Azure AD 目錄的主要網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-107">Set the primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="14a31-108">建立目錄時，初始網域名稱 (例如 ‘contoso.onmicrosoft.com’) 同時也是主要網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-108">When your directory is created, the initial domain name, such as ‘contoso.onmicrosoft.com,’ is also the primary domain name.</span></span> <span data-ttu-id="14a31-109">當您建立新的使用者時，主要網域即為新使用者的預設網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-109">The primary domain is the default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="14a31-110">設定主要網域名稱可以簡化系統管理員在入口網站中建立新使用者的程序。</span><span class="sxs-lookup"><span data-stu-id="14a31-110">Setting a primary domain name streamlines the process for an administrator to create new users in the portal.</span></span> <span data-ttu-id="14a31-111">變更主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="14a31-111">To change the primary domain name:</span></span>

1. <span data-ttu-id="14a31-112">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="14a31-112">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="14a31-113">選取 [更多服務]，在文字方塊中輸入 **Azure Active Directory**，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="14a31-113">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="14a31-115">在 [directory-name] 刀鋒視窗上，選取 [網域名稱]。</span><span class="sxs-lookup"><span data-stu-id="14a31-115">On the ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="14a31-116">在 [*directory-name* - 網域名稱] 刀鋒視窗上，選取您想要設為主要網域名稱的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-116">On the ***directory-name* - Domain names** blade, select the domain name you would like to make the primary domain name.</span></span>
5. <span data-ttu-id="14a31-117">在 [網域名稱] 刀鋒視窗 (也就是所開啟且標題中含有新網域名稱的刀鋒視窗) 上，選取 [設為主要] 命令。</span><span class="sxs-lookup"><span data-stu-id="14a31-117">On the ***domain name*** blade (that is, the blade that opens that has your new domain name in the title), select the **Make primary** command.</span></span> <span data-ttu-id="14a31-118">出現提示時，請確認您的選擇。</span><span class="sxs-lookup"><span data-stu-id="14a31-118">Confirm your choice when prompted.</span></span>
   
   ![將網域名稱設為主要網域名稱](./media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="14a31-120">您可以將目錄的主要網域名稱變更為任何已驗證的非同盟自訂網域。</span><span class="sxs-lookup"><span data-stu-id="14a31-120">You can change the primary domain name for your directory to be any verified custom domain that is not federated.</span></span> <span data-ttu-id="14a31-121">變更目錄的主要網域時，並不會變更任何現有使用者的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-121">Changing the primary domain for your directory will not change the user names for any existing users.</span></span>

## <a name="add-custom-domain-names-to-your-azure-ad"></a><span data-ttu-id="14a31-122">新增 Azure AD 的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-122">Add custom domain names to your Azure AD</span></span>
<span data-ttu-id="14a31-123">您可以為每個 Azure AD 目錄新增最多 900 個自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-123">You can add up to 900 custom domain names to each Azure AD directory.</span></span> <span data-ttu-id="14a31-124">[新增其他自訂網域名稱](add-custom-domain.md) 的程序與新增第一個自訂網域名稱相同。</span><span class="sxs-lookup"><span data-stu-id="14a31-124">The process to [add an additional custom domain name](add-custom-domain.md) is the same for the first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="14a31-125">新增自訂網域的子網域</span><span class="sxs-lookup"><span data-stu-id="14a31-125">Add subdomains of a custom domain</span></span>
<span data-ttu-id="14a31-126">如果您想要將第三層網域名稱新增至您的目錄，例如 'europe.contoso.com'，則應先新增並驗證第二層網域，例如 contoso.com。Azure AD 會自動驗證子網域。</span><span class="sxs-lookup"><span data-stu-id="14a31-126">If you want to add a third-level domain name such as ‘europe.contoso.com’ to your directory, you should first add and verify the second-level domain, such as contoso.com. The subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="14a31-127">若要查看您剛才新增的子網域是否已通過驗證，請重新整理列出網域的瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="14a31-127">To see that the subdomain that you just added has been verified, refresh the page in the browser that lists the domains.</span></span>

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="14a31-128">如果您變更您的自訂網域名稱的 DNS 註冊機構，該怎麼辦</span><span class="sxs-lookup"><span data-stu-id="14a31-128">What to do if you change the DNS registrar for your custom domain name</span></span>
<span data-ttu-id="14a31-129">如果您變更自訂網域名稱的 DNS 註冊機構，仍可以繼續在 Azure AD 中使用自訂網域名稱而不會中斷，且不需要其他組態工作。</span><span class="sxs-lookup"><span data-stu-id="14a31-129">If you change the DNS registrar for your custom domain name, you can continue to use your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="14a31-130">如果您的自訂網域名稱搭配使用 Office 365、Intune 或仰賴 Azure AD 自訂網域名稱的其他服務，則請參閱這些服務的文件。</span><span class="sxs-lookup"><span data-stu-id="14a31-130">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer to the documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="14a31-131">刪除自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-131">Delete a custom domain name</span></span>
<span data-ttu-id="14a31-132">如果貴組織不再使用該網域名稱，或如果您需要在另一個 Azure AD 中使用該網域名稱，您可以從您的 Azure AD 刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-132">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need to use that domain name with another Azure AD.</span></span>

<span data-ttu-id="14a31-133">若要刪除自訂網域名稱，您必須先確定目錄中沒有任何資源仰賴該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-133">To delete a custom domain name, you must first ensure that no resources in your directory rely on the domain name.</span></span> <span data-ttu-id="14a31-134">如果有下列情況，即無法刪除目錄的網域名稱：</span><span class="sxs-lookup"><span data-stu-id="14a31-134">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="14a31-135">有任何使用者的使用者名稱、電子郵件地址或 Proxy 位址包含該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-135">Any user has a user name, email address, or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="14a31-136">有任何群組的電子郵件地址或 Proxy 位址包含該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-136">Any group has an email address or proxy address that includes the domain name.</span></span>
* <span data-ttu-id="14a31-137">Azure AD 中任何應用程式的應用程式識別碼 URI 包括該網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-137">Any application in your Azure AD has an app ID URI that includes the domain name.</span></span>

<span data-ttu-id="14a31-138">您必須變更或刪除 Azure AD 目錄中任何這類資源，才能刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="14a31-138">You must change or delete any such resource in your Azure AD directory before you can delete the custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a><span data-ttu-id="14a31-139">使用 PowerShell 或圖形 API 來管理網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-139">Use PowerShell or Graph API to manage domain names</span></span>
<span data-ttu-id="14a31-140">在 Azure Active Directory 中，大部分的網域名稱管理工作也都可以使用 Microsoft PowerShell 來完成，或使用 Azure AD 圖形 API 以程式設計方式來完成。</span><span class="sxs-lookup"><span data-stu-id="14a31-140">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="14a31-141">使用 PowerShell 管理 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-141">Using PowerShell to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="14a31-142">使用圖形 API 管理 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-142">Using Graph API to manage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="14a31-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14a31-143">Next steps</span></span>
* [<span data-ttu-id="14a31-144">新增自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="14a31-144">Add custom domain names</span></span>](add-custom-domain.md)

