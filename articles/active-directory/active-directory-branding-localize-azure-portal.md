---
title: "在 Azure Active Directory 中將語言特定公司商標新增到登入頁面 | Microsoft Docs"
description: "了解如何將語言特定公司商標圖片和文字新增到 Azure 登入頁面"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a0310d6a-aaa7-4ea0-991d-6d3135b4382a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: e1fe8d855386ceec39edbc985538cdf32d78a13b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-language-specific-company-branding-to-your-sign-in-page-in-the-azure-active-directory"></a><span data-ttu-id="9fdb1-103">在 Azure Active Directory 中將語言特定公司商標新增到登入頁面</span><span class="sxs-lookup"><span data-stu-id="9fdb1-103">Add language-specific company branding to your sign-in page in the Azure Active Directory</span></span>
<span data-ttu-id="9fdb1-104">為了避免混淆，許多公司都想對其管理的所有網站和服務套用一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="9fdb1-105">Azure Active Directory 是透過讓您利用公司標誌和自訂色彩配置來自訂登入頁面外觀的方式，提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="9fdb1-106">登入頁面是當您登入 Office 365 或其他使用 Azure AD 作為識別提供者的 Web 型應用程式時，所顯示的頁面。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="9fdb1-107">您可以與此頁面互動來輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-107">You interact with this page to enter your credentials.</span></span>

## <a name="customizing-the-sign-in-page-for-another-language"></a><span data-ttu-id="9fdb1-108">自訂另一個語言的登入頁面</span><span class="sxs-lookup"><span data-stu-id="9fdb1-108">Customizing the sign-in page for another language</span></span>
<span data-ttu-id="9fdb1-109">只有當您已如 [將公司商標新增到登入頁面](active-directory-branding-custom-signon-azure-portal.md)所述建立自訂登入頁面時，您才可以將語言特定元素新增到自訂登入頁面。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-109">You can add language-specific elements to your custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding to your sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="9fdb1-110">您可以使用一組預設的可自訂元素，為每一目錄設定一個登入頁面。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="9fdb1-111">在您已設定一組預設的頁面元素之後，就可以設定不同地區設定的其他版本。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-111">After you’ve configured the default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="9fdb1-112">您也可以混合使用並符合各種元素。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-112">You can also mix and match various elements.</span></span> <span data-ttu-id="9fdb1-113">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="9fdb1-113">For example, you could:</span></span>

* <span data-ttu-id="9fdb1-114">建立適用於所有文化特性的預設「登入頁面影像」  ，然後建立英文和法文的特定版本。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="9fdb1-115">當您將瀏覽器設定為這兩種語言其中之一時，就會顯示語言特定影像，而針對其他所有語言則會顯示預設圖例。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-115">When you set your browsers to one of these two languages, the language-specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="9fdb1-116">為您的組織設定不同的標誌 (例如日文或希伯來文版本)。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="9fdb1-117">基於維護和效能考量，建議您不要使用太多語言變化。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-117">We recommend that you keep the number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="9fdb1-118">**將公司商標新增到您的目錄：**</span><span class="sxs-lookup"><span data-stu-id="9fdb1-118">**To add company branding to your directory:**</span></span>

1. <span data-ttu-id="9fdb1-119">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com) 。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-119">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9fdb1-120">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-120">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="9fdb1-122">在 [使用者和群組] 刀鋒視窗上，選取 [公司商標]。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-122">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="9fdb1-123">在 [使用者和群組 - 公司商標] 刀鋒視窗上，選取 [新增語言] 命令。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-123">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![新增語言特定商標元素](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="9fdb1-125">修改您想要自訂的元素。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-125">Modify the elements you want to customize.</span></span> <span data-ttu-id="9fdb1-126">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-126">All elements are optional.</span></span>
6. <span data-ttu-id="9fdb1-127">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-127">Click **Save**.</span></span>

<span data-ttu-id="9fdb1-128">您對登入頁面商標所做的任何變更可能最多需要一個小時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="9fdb1-128">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fdb1-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9fdb1-129">Next steps</span></span>
[<span data-ttu-id="9fdb1-130">將公司商標新增到您的登入頁面</span><span class="sxs-lookup"><span data-stu-id="9fdb1-130">Add company branding to your sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
