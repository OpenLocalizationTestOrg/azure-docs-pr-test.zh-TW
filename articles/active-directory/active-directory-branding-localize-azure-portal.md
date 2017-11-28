---
title: "aaaAdd 特定語言的公司品牌 tooyour 登入頁面在 hello Azure Active Directory |Microsoft 文件"
description: "了解如何 tooadd 語言特定公司品牌圖片和文字 tooan Azure 登入頁面"
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
ms.openlocfilehash: 1e33c31abc242e8455290beb1f03760be7b9ac42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-language-specific-company-branding-tooyour-sign-in-page-in-hello-azure-active-directory"></a><span data-ttu-id="b4ef0-103">將語言特定公司商標 tooyour 登入頁面 hello Azure Active Directory 中新增</span><span class="sxs-lookup"><span data-stu-id="b4ef0-103">Add language-specific company branding tooyour sign-in page in hello Azure Active Directory</span></span>
<span data-ttu-id="b4ef0-104">tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="b4ef0-105">Azure Active Directory 可讓您 toocustomize hello 外觀 hello 登入頁面與您的公司標誌自訂色彩配置，以提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="b4ef0-106">hello 登入頁面為 hello 頁面，會出現在您登入 tooOffice 365 或其他 web 應用程式使用 Azure AD 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="b4ef0-107">您互動此頁面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-107">You interact with this page tooenter your credentials.</span></span>

## <a name="customizing-hello-sign-in-page-for-another-language"></a><span data-ttu-id="b4ef0-108">自訂 hello 登入另一個語言的頁面</span><span class="sxs-lookup"><span data-stu-id="b4ef0-108">Customizing hello sign-in page for another language</span></span>
<span data-ttu-id="b4ef0-109">只有當您已經建立自訂的登入頁面中所述，您可以新增特定語言項目 tooyour 自訂登入頁面[新增公司品牌登入頁面 tooyour](active-directory-branding-custom-signon-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-109">You can add language-specific elements tooyour custom sign-in page only if you have already created a custom sign-in page as described in [Add company branding tooyour sign-in page](active-directory-branding-custom-signon-azure-portal.md).</span></span> <span data-ttu-id="b4ef0-110">您可以使用一組預設的可自訂元素，為每一目錄設定一個登入頁面。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-110">You can configure one sign-in page per directory with a default set of customizable elements.</span></span> <span data-ttu-id="b4ef0-111">設定頁面元素的 hello 預設集之後，您可以設定不同的地區設定的多個版本。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-111">After you’ve configured hello default set of page elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="b4ef0-112">您也可以混合使用並符合各種元素。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-112">You can also mix and match various elements.</span></span> <span data-ttu-id="b4ef0-113">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="b4ef0-113">For example, you could:</span></span>

* <span data-ttu-id="b4ef0-114">建立適用於所有文化特性的預設「登入頁面影像」  ，然後建立英文和法文的特定版本。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-114">Create a default **Sign-in page image** that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="b4ef0-115">當您設定您的瀏覽器 tooone 的這兩種語言時，會出現 hello 特定語言的映像，而 hello 預設圖例出現的所有其他語言。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-115">When you set your browsers tooone of these two languages, hello language-specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="b4ef0-116">為您的組織設定不同的標誌 (例如日文或希伯來文版本)。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-116">Configure different logos for your organization (for example, Japanese or Hebrew versions).</span></span>

<span data-ttu-id="b4ef0-117">我們建議您保留 hello 多語言變化低、 維護和效能考量。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-117">We recommend that you keep hello number of language variations low, for maintenance and performance reasons.</span></span>

<span data-ttu-id="b4ef0-118">**tooadd 公司商標 tooyour 目錄：**</span><span class="sxs-lookup"><span data-stu-id="b4ef0-118">**tooadd company branding tooyour directory:**</span></span>

1. <span data-ttu-id="b4ef0-119">登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-119">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="b4ef0-120">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-120">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="b4ef0-122">在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-122">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="b4ef0-123">在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**新增語言**命令。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-123">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![新增語言特定商標元素](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="b4ef0-125">修改您想 toocustomize 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-125">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="b4ef0-126">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-126">All elements are optional.</span></span>
6. <span data-ttu-id="b4ef0-127">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-127">Click **Save**.</span></span>

<span data-ttu-id="b4ef0-128">如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="b4ef0-128">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ef0-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4ef0-129">Next steps</span></span>
[<span data-ttu-id="b4ef0-130">新增公司品牌 tooyour 登入頁面</span><span class="sxs-lookup"><span data-stu-id="b4ef0-130">Add company branding tooyour sign-in page</span></span>](active-directory-branding-custom-signon-azure-portal.md)
