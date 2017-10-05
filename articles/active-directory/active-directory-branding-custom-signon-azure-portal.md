---
title: "在 Azure Active Directory 中自訂登入頁面 | Microsoft Docs"
description: "了解如何將公司商標新增到 Azure 登入頁面"
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
ms.openlocfilehash: 27590c018ea55e9793246c7a4cab10f934ea502b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="36a8b-103">在 Azure Active Directory 中將公司商標新增至登入頁面</span><span class="sxs-lookup"><span data-stu-id="36a8b-103">Add company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="36a8b-104">為了避免混淆，許多公司都想對其管理的所有網站和服務套用一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="36a8b-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="36a8b-105">Azure Active Directory 是透過讓您利用公司標誌和自訂色彩配置來自訂登入頁面外觀的方式，提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="36a8b-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="36a8b-106">登入頁面是當您登入 Office 365 或其他使用 Azure AD 作為識別提供者的 Web 型應用程式時，所顯示的頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="36a8b-107">您可以與此頁面互動來輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="36a8b-107">You interact with this page to enter your credentials.</span></span>

<span data-ttu-id="36a8b-108">如果您想要在此頁面上顯示您的公司商標、色彩和其他可自訂的元素，請參閱下列影像以了解這兩種做法的差異。</span><span class="sxs-lookup"><span data-stu-id="36a8b-108">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="36a8b-109">下列螢幕擷取畫面顯示桌上型電腦上 Office 365 登入頁面的自訂「前」  範例︰</span><span class="sxs-lookup"><span data-stu-id="36a8b-109">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-before-customization.png)

<span data-ttu-id="36a8b-111">下列螢幕擷取畫面顯示桌上型電腦上 Office 365 登入頁面的自訂「後」  範例︰</span><span class="sxs-lookup"><span data-stu-id="36a8b-111">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面](./media/active-directory-branding-custom-signon-azure-portal/sign-in-page-after-customization.png)

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="36a8b-113">自訂登入頁面</span><span class="sxs-lookup"><span data-stu-id="36a8b-113">Customizing the sign-in page</span></span>
<span data-ttu-id="36a8b-114">一般而言，如果您需要透過瀏覽器存取貴組織訂閱的雲端應用程式和服務，您可使用登入頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-114">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="36a8b-115">如果您已對登入頁面套用變更，最多需要一小時變更才會出現。</span><span class="sxs-lookup"><span data-stu-id="36a8b-115">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="36a8b-116">只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-116">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="36a8b-117">當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-117">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="36a8b-118">在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。</span><span class="sxs-lookup"><span data-stu-id="36a8b-118">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="36a8b-119">在您已設定商標之 Azure 入口網站的 [網域]  部分，您的網域名稱必須顯示為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="36a8b-119">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="36a8b-120">如需詳細資訊，請參閱 [新增自訂網域名稱](active-directory-domains-add-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="36a8b-120">For more information, see [Add custom domain names](active-directory-domains-add-azure-portal.md).</span></span>
> * <span data-ttu-id="36a8b-121">登入頁面商標不會延續到 Microsoft 的消費者登入頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-121">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="36a8b-122">如果您使用 Microsoft 帳戶進行登入，您可能會看到 Azure AD 所呈現且已加上商標的使用者磚清單，但是您組織的商標不會套用到 Microsoft 帳戶登入頁面。</span><span class="sxs-lookup"><span data-stu-id="36a8b-122">If you sign in with a Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="36a8b-123">登入頁面上的 [讓我保持登入] 核取方塊，可讓使用者在關閉並重新開啟其瀏覽器時保持登入狀態。</span><span class="sxs-lookup"><span data-stu-id="36a8b-123">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span>

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/01.png)

<span data-ttu-id="36a8b-125">它不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="36a8b-125">It does not effect session lifetime.</span></span> <span data-ttu-id="36a8b-126">您可以在 Azure Active Directory 登入頁面上隱藏此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="36a8b-126">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>
<span data-ttu-id="36a8b-127">是否會顯示核取方塊取決於 [已停用 [讓我保持登入]] 的設定。</span><span class="sxs-lookup"><span data-stu-id="36a8b-127">Whether the checkbox is displayed depends on the setting of **Keep me signed in disabled**.</span></span>

   ![讓我保持登入](./media/active-directory-branding-custom-signon-azure-portal/02.png)

<span data-ttu-id="36a8b-129">若要隱藏此核取方塊，請將此設定設為 [是]。</span><span class="sxs-lookup"><span data-stu-id="36a8b-129">To hide the checkbox, configure this setting to **Yes**.</span></span>

> [!NOTE]
> <span data-ttu-id="36a8b-130">SharePoint Online 和 Office 2010 的某些功能取決於能夠核取此方塊的使用者。</span><span class="sxs-lookup"><span data-stu-id="36a8b-130">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="36a8b-131">如果您將此設定設為隱藏，使用者可能會在登入時看見其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="36a8b-131">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="36a8b-132">**將公司商標新增到您的目錄：**</span><span class="sxs-lookup"><span data-stu-id="36a8b-132">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="36a8b-133">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="36a8b-133">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="36a8b-134">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="36a8b-134">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="36a8b-136">在 [使用者和群組] 刀鋒視窗上，選取 [公司商標]。</span><span class="sxs-lookup"><span data-stu-id="36a8b-136">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="36a8b-137">在 [使用者和群組 - 公司商標] 刀鋒視窗上，選取 [編輯] 命令。</span><span class="sxs-lookup"><span data-stu-id="36a8b-137">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="36a8b-139">修改您想要自訂的元素。</span><span class="sxs-lookup"><span data-stu-id="36a8b-139">Modify the elements you want to customize.</span></span> <span data-ttu-id="36a8b-140">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="36a8b-140">All elements are optional.</span></span>
6. <span data-ttu-id="36a8b-141">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="36a8b-141">Click **Save**.</span></span>

<span data-ttu-id="36a8b-142">您對登入頁面商標所做的任何變更可能最多需要一個小時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="36a8b-142">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36a8b-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="36a8b-143">Next steps</span></span>
[<span data-ttu-id="36a8b-144">新增語言特定公司商標</span><span class="sxs-lookup"><span data-stu-id="36a8b-144">Add language-specific company branding</span></span>](active-directory-branding-localize-azure-portal.md)
