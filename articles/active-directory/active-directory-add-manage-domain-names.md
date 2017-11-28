---
title: "在您的 Azure Active Directory aaaManaging 自訂網域名稱 |Microsoft 文件"
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
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="3a13c-103">管理 Azure Active Directory 中的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="3a13c-104">網域名稱可以是許多目錄資源的重要識別碼，其屬於：</span><span class="sxs-lookup"><span data-stu-id="3a13c-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="3a13c-105">使用者的使用者名稱或電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="3a13c-105">A user name or email address for a user</span></span>
* <span data-ttu-id="3a13c-106">hello 位址群組</span><span class="sxs-lookup"><span data-stu-id="3a13c-106">hello address for a group</span></span>
* <span data-ttu-id="3a13c-107">hello 應用程式識別碼 URI 的應用程式</span><span class="sxs-lookup"><span data-stu-id="3a13c-107">hello app ID URI for an application</span></span>

<span data-ttu-id="3a13c-108">Azure Active Directory (Azure AD) 中的資源可以包含已驗證 toobe 所擁有 hello 目錄，其中包含 hello 資源的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="3a13c-109">只有全域管理員可以在 Azure AD 中執行網域管理工作。</span><span class="sxs-lookup"><span data-stu-id="3a13c-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a13c-110">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="3a13c-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="3a13c-111">如何 toomanage 您的網域名稱在 hello Azure AD 系統管理中心，請參閱[管理您的 Azure Active Directory 中的自訂網域名稱](active-directory-domains-manage-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3a13c-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="3a13c-112">設定您的 Azure AD 目錄的 hello 主要網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="3a13c-113">建立您的目錄時，hello 初始網域名稱，例如 'contoso.onmicrosoft.com'，也是 hello 主要網域名稱，為您的目錄。</span><span class="sxs-lookup"><span data-stu-id="3a13c-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="3a13c-114">hello 主要網域是 hello 預設網域名稱用於新的使用者，當您建立新的使用者在 hello [Azure 傳統入口網站](https://manage.windowsazure.com/)，或其他入口網站，例如 hello Office 365 系統管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="3a13c-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="3a13c-115">這可簡化系統管理員 toocreate 新的使用者在 hello 入口網站中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="3a13c-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="3a13c-116">您的目錄的 toochange hello 主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="3a13c-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="3a13c-117">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com/)的 Azure AD 目錄的全域系統管理員的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a13c-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="3a13c-118">選取**Active Directory** hello 左側的導覽列上。</span><span class="sxs-lookup"><span data-stu-id="3a13c-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="3a13c-119">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="3a13c-119">Open your directory.</span></span>
4. <span data-ttu-id="3a13c-120">選取 hello**網域** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3a13c-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="3a13c-121">選取 hello**變更主要**hello 命令列上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="3a13c-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="3a13c-122">選取您想 toobe hello 新的主要網域，為您的目錄 hello 網域。</span><span class="sxs-lookup"><span data-stu-id="3a13c-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="3a13c-123">您可以變更目錄 toobe 的 hello 主要網域名稱不同盟任何驗證的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="3a13c-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="3a13c-124">變更 hello 主要網域為您的目錄不會變更任何現有使用者的 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="3a13c-125">新增自訂網域名稱 tooyour Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a13c-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="3a13c-126">您可以加總 too900 自訂網域名稱 tooeach Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="3a13c-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="3a13c-127">太 hello 程序[新增其他自訂網域名稱，](active-directory-add-domain.md) hello 相同的 hello 第一個自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="3a13c-128">新增自訂網域的子網域</span><span class="sxs-lookup"><span data-stu-id="3a13c-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="3a13c-129">如果您想 tooadd 第三層網域名稱，例如 'europe.contoso.com' tooyour 目錄，您應該先 agregar y comprobar hello 第二層網域，例如 contoso.com。hello 子網域會自動由 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="3a13c-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="3a13c-130">hello 您剛才加入的子網域的 toosee 已經過驗證，重新整理 hello 頁面，列出您的目錄中的 hello 網域的 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="3a13c-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="3a13c-131">如果您變更您的自訂網域名稱 hello DNS 註冊機構哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="3a13c-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="3a13c-132">如果您變更 hello DNS 註冊機構的自訂網域名稱時，您可以繼續 toouse 與 Azure AD 本身而不需要中斷以及其他設定工作的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="3a13c-133">如果您使用自訂網域名稱搭配 Office 365、 Intune 或依賴 Azure AD 中的自訂網域名稱的其他服務，請參閱 toohello 文件，這些服務。</span><span class="sxs-lookup"><span data-stu-id="3a13c-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="3a13c-134">刪除自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-134">Delete a custom domain name</span></span>
<span data-ttu-id="3a13c-135">如果您的組織不再使用該網域名稱，或如果您需要 toouse 網域名稱與另一個 Azure AD，您可以從您的 Azure AD 刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="3a13c-136">toodelete 自訂網域名稱，您必須先確定您的目錄中沒有任何資源依賴 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="3a13c-137">如果有下列情況，即無法刪除目錄的網域名稱：</span><span class="sxs-lookup"><span data-stu-id="3a13c-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="3a13c-138">任何使用者具有使用者名稱、 電子郵件地址或包含 hello 網域名稱的 proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="3a13c-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="3a13c-139">任何群組具有電子郵件地址或包含 hello 網域名稱的 proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="3a13c-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="3a13c-140">在您的 Azure AD 中的任何應用程式擁有的應用程式識別碼 URI，包括 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="3a13c-141">您必須變更或刪除您的 Azure AD 目錄中的任何這類資源，才能刪除 hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="3a13c-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="3a13c-142">使用 PowerShell 或 Graph API toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="3a13c-143">在 Azure Active Directory 中，大部分的網域名稱管理工作也都可以使用 Microsoft PowerShell 來完成，或使用 Azure AD 圖形 API 以程式設計方式來完成。</span><span class="sxs-lookup"><span data-stu-id="3a13c-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="3a13c-144">在 Azure AD 中使用 PowerShell toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="3a13c-145">在 Azure AD 中使用 Graph API toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="3a13c-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3a13c-146">Next steps</span></span>
* [<span data-ttu-id="3a13c-147">了解 Azure AD 中的網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="3a13c-148">管理自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="3a13c-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

