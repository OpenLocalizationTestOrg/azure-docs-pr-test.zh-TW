---
title: "在您的 Azure Active Directory aaaManaging 自訂網域名稱 |Microsoft 文件"
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
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="5777e-103">管理 Azure Active Directory 中的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="5777e-104">網域名稱是 hello 許多目錄資源的識別項很重要的一部分： 它屬於使用者時，為群組，請 hello 位址部分的使用者名稱或電子郵件地址，而且可以是應用程式的 hello 應用程式識別碼 URI 的一部分。</span><span class="sxs-lookup"><span data-stu-id="5777e-104">A domain name is an important part of hello identifier for many directory resources: it is part of a user name or email address for a user, part of hello address for a group, and can be part of hello app ID URI for an application.</span></span> <span data-ttu-id="5777e-105">Azure Active Directory (Azure AD) 中的資源可以包含已擁有 hello 目錄，其中包含 hello 資源驗證的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="5777e-106">只有全域管理員可以在 Azure AD 中執行網域管理工作。</span><span class="sxs-lookup"><span data-stu-id="5777e-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="5777e-107">設定您的 Azure AD 目錄的 hello 主要網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-107">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="5777e-108">建立您的目錄時，hello 初始網域名稱，例如 'contoso.onmicrosoft.com'，也是 hello 主要網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-108">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name.</span></span> <span data-ttu-id="5777e-109">hello 主要網域時建立新的使用者之新使用者的 hello 預設網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-109">hello primary domain is hello default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="5777e-110">設定主要網域名稱，來簡化管理員 toocreate 新使用者 hello 入口網站中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="5777e-110">Setting a primary domain name streamlines hello process for an administrator toocreate new users in hello portal.</span></span> <span data-ttu-id="5777e-111">toochange hello 主要網域名稱：</span><span class="sxs-lookup"><span data-stu-id="5777e-111">toochange hello primary domain name:</span></span>

1. <span data-ttu-id="5777e-112">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="5777e-112">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="5777e-113">選取**更多服務**，輸入**Azure Active Directory**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="5777e-113">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
   
   ![開啟使用者管理](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="5777e-115">在 hello***目錄名稱***刀鋒視窗中，選取**網域名稱**。</span><span class="sxs-lookup"><span data-stu-id="5777e-115">On hello ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="5777e-116">在 hello ***目錄名稱*-網域名稱**刀鋒視窗中，選取 hello 希望 toomake hello 主要網域名稱的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-116">On hello ***directory-name* - Domain names** blade, select hello domain name you would like toomake hello primary domain name.</span></span>
5. <span data-ttu-id="5777e-117">在 hello***網域名稱***刀鋒視窗 （也就是 hello 刀鋒視窗中開啟 hello 標題中具有新的網域名稱），選取 hello**設為主要**命令。</span><span class="sxs-lookup"><span data-stu-id="5777e-117">On hello ***domain name*** blade (that is, hello blade that opens that has your new domain name in hello title), select hello **Make primary** command.</span></span> <span data-ttu-id="5777e-118">出現提示時，請確認您的選擇。</span><span class="sxs-lookup"><span data-stu-id="5777e-118">Confirm your choice when prompted.</span></span>
   
   ![將網域名稱設為主要網域名稱](./media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="5777e-120">您可以變更目錄 toobe 的 hello 主要網域名稱不同盟任何驗證的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="5777e-120">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="5777e-121">變更 hello 主要網域為您的目錄不會變更任何現有使用者的 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-121">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="5777e-122">新增自訂網域名稱 tooyour Azure AD</span><span class="sxs-lookup"><span data-stu-id="5777e-122">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="5777e-123">您可以加總 too900 自訂網域名稱 tooeach Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="5777e-123">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="5777e-124">太 hello 程序[新增其他自訂網域名稱，](add-custom-domain.md) hello 相同的 hello 第一個自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-124">hello process too[add an additional custom domain name](add-custom-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="5777e-125">新增自訂網域的子網域</span><span class="sxs-lookup"><span data-stu-id="5777e-125">Add subdomains of a custom domain</span></span>
<span data-ttu-id="5777e-126">如果您想 tooadd 第三層網域名稱，例如 'europe.contoso.com' tooyour 目錄，您應該先 agregar y comprobar hello 第二層網域，例如 contoso.com。hello 子網域會自動由 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="5777e-126">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="5777e-127">hello 您剛才加入的子網域的 toosee 已經過驗證，重新整理 hello 頁面列出 hello 網域的 hello 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="5777e-127">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="5777e-128">如果您變更您的自訂網域名稱 hello DNS 註冊機構哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="5777e-128">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="5777e-129">如果您變更 hello DNS 註冊機構的自訂網域名稱時，您可以繼續 toouse 與 Azure AD 本身而不需要中斷以及其他設定工作的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-129">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="5777e-130">如果您使用自訂網域名稱搭配 Office 365、 Intune 或依賴 Azure AD 中的自訂網域名稱的其他服務，請參閱 toohello 文件，這些服務。</span><span class="sxs-lookup"><span data-stu-id="5777e-130">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="5777e-131">刪除自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-131">Delete a custom domain name</span></span>
<span data-ttu-id="5777e-132">如果您的組織不再使用該網域名稱，或如果您需要 toouse 網域名稱與另一個 Azure AD，您可以從您的 Azure AD 刪除自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-132">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="5777e-133">toodelete 自訂網域名稱，您必須先確定您的目錄中沒有任何資源依賴 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-133">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="5777e-134">如果有下列情況，即無法刪除目錄的網域名稱：</span><span class="sxs-lookup"><span data-stu-id="5777e-134">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="5777e-135">任何使用者具有使用者名稱、 電子郵件地址或包含 hello 網域名稱的 proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="5777e-135">Any user has a user name, email address, or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="5777e-136">任何群組具有電子郵件地址或包含 hello 網域名稱的 proxy 位址。</span><span class="sxs-lookup"><span data-stu-id="5777e-136">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="5777e-137">在您的 Azure AD 中的任何應用程式擁有的應用程式識別碼 URI，包括 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-137">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="5777e-138">您必須變更或刪除您的 Azure AD 目錄中的任何這類資源，才能刪除 hello 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="5777e-138">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="5777e-139">使用 PowerShell 或 Graph API toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-139">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="5777e-140">在 Azure Active Directory 中，大部分的網域名稱管理工作也都可以使用 Microsoft PowerShell 來完成，或使用 Azure AD 圖形 API 以程式設計方式來完成。</span><span class="sxs-lookup"><span data-stu-id="5777e-140">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="5777e-141">在 Azure AD 中使用 PowerShell toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-141">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="5777e-142">在 Azure AD 中使用 Graph API toomanage 網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-142">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="5777e-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5777e-143">Next steps</span></span>
* [<span data-ttu-id="5777e-144">新增自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="5777e-144">Add custom domain names</span></span>](add-custom-domain.md)

