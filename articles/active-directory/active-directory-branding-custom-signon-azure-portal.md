---
title: "登入頁面 hello Azure Active Directory aaaCustomize |Microsoft 文件"
description: "深入了解如何 tooadd 公司品牌 toohello Azure 登入頁面"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 151521e3b9cbc6a438a589735058fbff78443cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="b02f4-103">新增公司品牌 tooyour 登入頁面 hello Azure Active Directory 中</span><span class="sxs-lookup"><span data-stu-id="b02f4-103">Add company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="b02f4-104">tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。</span><span class="sxs-lookup"><span data-stu-id="b02f4-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="b02f4-105">Azure Active Directory 可讓您 toocustomize hello 外觀 hello 登入頁面與您的公司標誌自訂色彩配置，以提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="b02f4-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="b02f4-106">hello 登入頁面為 hello 頁面，會出現在您登入 tooOffice 365 或其他 web 應用程式使用 Azure AD 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="b02f4-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="b02f4-107">您互動此頁面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="b02f4-107">You interact with this page tooenter your credentials.</span></span>

<span data-ttu-id="b02f4-108">如果您的公司品牌、 色彩和其他可自訂的元素，此頁面上，您會想 tooshow，請參閱下列映像 toounderstand hello hello 兩種體驗差異 hello。</span><span class="sxs-lookup"><span data-stu-id="b02f4-108">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="b02f4-109">下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之前**自訂：</span><span class="sxs-lookup"><span data-stu-id="b02f4-109">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="b02f4-111">下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之後**自訂：</span><span class="sxs-lookup"><span data-stu-id="b02f4-111">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="b02f4-113">自訂 hello 登入頁面</span><span class="sxs-lookup"><span data-stu-id="b02f4-113">Customizing hello sign-in page</span></span>
<span data-ttu-id="b02f4-114">一般而言，如果您需要瀏覽器為基礎的存取 tooyour 雲端應用程式和貴組織訂閱的服務，您可以使用 hello 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b02f4-114">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="b02f4-115">如果您已套用變更 tooyour 登入頁面上，就可以在 hello 變更 tooappear tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="b02f4-115">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="b02f4-116">只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b02f4-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="b02f4-117">當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b02f4-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="b02f4-118">在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。</span><span class="sxs-lookup"><span data-stu-id="b02f4-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="b02f4-119">您的網域名稱必須為 使用出現在 hello**網域**部分 hello Azure 入口網站中您已設定的商標。</span><span class="sxs-lookup"><span data-stu-id="b02f4-119">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="b02f4-120">如需詳細資訊，請參閱 [新增自訂網域名稱](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b02f4-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="b02f4-121">登入頁面品牌不會延續 toohello 消費者登入的 Microsoft 的頁面。</span><span class="sxs-lookup"><span data-stu-id="b02f4-121">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="b02f4-122">如果您使用 Microsoft 帳戶登入，您可能會看到加上品牌的 Azure AD 所呈現的使用者磚清單，但您組織的品牌 hello 不會套用 toohello Microsoft 帳戶登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b02f4-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="b02f4-123">在您登入頁面上，hello**讓我保持登**核取方塊可讓使用者 tooremain 時關閉並重新開啟瀏覽器登入。</span><span class="sxs-lookup"><span data-stu-id="b02f4-123">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span>

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="b02f4-125">它不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="b02f4-125">It does not effect session lifetime.</span></span> <span data-ttu-id="b02f4-126">您可以隱藏 hello hello Azure Active Directory 登入頁面上的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b02f4-126">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="b02f4-127">Hello 核取方塊會顯示是否取決 hello 設定**讓我保持登停用**。</span><span class="sxs-lookup"><span data-stu-id="b02f4-127">Whether hello checkbox is displayed depends on hello setting of **Keep me signed in disabled**.</span></span>

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="b02f4-129">toohide hello 核取方塊，設定此設定太**是**。</span><span class="sxs-lookup"><span data-stu-id="b02f4-129">toohide hello checkbox, configure this setting too**Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="b02f4-130">SharePoint Online 和 Office 2010 的某些功能而定的使用者可以 toocheck 此方塊。</span><span class="sxs-lookup"><span data-stu-id="b02f4-130">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="b02f4-131">如果您設定此設定 toohidden，您的使用者可能會看到 toosign 中其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="b02f4-131">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="b02f4-132">**tooadd 公司商標 tooyour 目錄：**</span><span class="sxs-lookup"><span data-stu-id="b02f4-132">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="b02f4-133">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b02f4-133">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="b02f4-134">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b02f4-134">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="b02f4-136">在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。</span><span class="sxs-lookup"><span data-stu-id="b02f4-136">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="b02f4-137">在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**編輯**命令。</span><span class="sxs-lookup"><span data-stu-id="b02f4-137">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="b02f4-139">修改您想 toocustomize 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="b02f4-139">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="b02f4-140">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="b02f4-140">All elements are optional.</span></span>
6. <span data-ttu-id="b02f4-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b02f4-141">Click **Save**.</span></span>

<span data-ttu-id="b02f4-142">如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="b02f4-142">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b02f4-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b02f4-143">Next steps</span></span>
[<span data-ttu-id="b02f4-144">新增語言特定公司商標</span><span class="sxs-lookup"><span data-stu-id="b02f4-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
