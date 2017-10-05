---
title: "在 Azure Active Directory 中自訂登入頁面 | Microsoft Docs"
description: "了解如何將公司商標新增到 Azure 登入頁面"
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: bddf2542eecce8bdeccda6053203bf2c2ba0ffb2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="quickstart-add-company-branding-to-your-sign-in-page-in-azure-ad"></a><span data-ttu-id="d0c60-103">快速入門：在 Azure AD 中將公司商標新增至登入頁面</span><span class="sxs-lookup"><span data-stu-id="d0c60-103">Quickstart: Add company branding to your sign-in page in Azure AD</span></span>
<span data-ttu-id="d0c60-104">為了避免混淆，許多公司都想對其管理的所有網站和服務套用一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="d0c60-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="d0c60-105">Azure Active Directory (Azure AD) 是透過讓您利用公司標誌和自訂色彩配置來自訂登入頁面外觀的方式，提供這項功能。</span><span class="sxs-lookup"><span data-stu-id="d0c60-105">Azure Active Directory (Azure AD) provides this capability by allowing you to customize the appearance of the sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="d0c60-106">登入頁面是當您登入 Office 365 或其他使用 Azure AD 作為識別提供者的 Web 型應用程式時，所顯示的頁面。</span><span class="sxs-lookup"><span data-stu-id="d0c60-106">The sign-in page is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="d0c60-107">您可以與此頁面互動來輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="d0c60-107">You interact with this page to enter your credentials.</span></span>

> [!NOTE]
> * <span data-ttu-id="d0c60-108">公司商標僅在您升級至「進階」或「基本」版本的 Azure AD 後，或擁有 Office 365 授權時才能使用。</span><span class="sxs-lookup"><span data-stu-id="d0c60-108">Company branding is available only if you upgraded to the Premium or Basic edition of Azure AD, or have an Office 365 license.</span></span> <span data-ttu-id="d0c60-109">若要了解您的授權類型是否支援某功能，請查看 [Azure Active Directory 價格資訊頁面](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="d0c60-109">To learn if a feature is supported by your license type, check the [Azure Active Directory pricing information page](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>
> 
> * <span data-ttu-id="d0c60-110">Azure Active Directory Premium 和 Basic 版本適用於使用全球 Azure Active Directory 執行個體的中國客戶。</span><span class="sxs-lookup"><span data-stu-id="d0c60-110">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="d0c60-111">由 21Vianet 在中國提供的 Microsoft Azure 服務目前不支援 Azure Active Directory Premium 和 Basic 版本。</span><span class="sxs-lookup"><span data-stu-id="d0c60-111">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="d0c60-112">如需詳細資訊，請透過 [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="d0c60-112">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="d0c60-113">自訂登入頁面</span><span class="sxs-lookup"><span data-stu-id="d0c60-113">Customizing the sign-in page</span></span>

<!--You can customize the following elements on the sign-in page: <attach image>-->

<span data-ttu-id="d0c60-114">當使用者存取租用戶特定 URL (例如 [*https://outlook.com/contoso.com*](https://outlook.com/contoso.com)) 時，公司商標自訂會出現在 Azure AD 登入頁面上。</span><span class="sxs-lookup"><span data-stu-id="d0c60-114">Company branding customizations appear on the Azure AD sign-in page when users access a tenant-specific URL such as [*https://outlook.com/contoso.com*](https://outlook.com/contoso.com).</span></span>

<span data-ttu-id="d0c60-115">當使用者造訪一般 URL (例如 www.office.com) 時，因為系統不知道使用者是誰，登入頁面不包含公司商標自訂。</span><span class="sxs-lookup"><span data-stu-id="d0c60-115">When users visit a generic URL such as www.office.com, the sign-in page does not contain company branding customizations because the system doesn’t know who the user is.</span></span> <span data-ttu-id="d0c60-116">使用者輸入其使用者識別碼或選取使用者圖格之後，就會顯示公司商標。</span><span class="sxs-lookup"><span data-stu-id="d0c60-116">Company branding will show after users enter their user ID or select a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="d0c60-117">在您已設定商標之 Azure 入口網站的 [網域]  部分，您的網域名稱必須顯示為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="d0c60-117">Your domain name must appear as “Active" in the **Domains** portion of the Azure portal in which you have configured branding.</span></span> <span data-ttu-id="d0c60-118">如需詳細資訊，請參閱[新增自訂網域名稱](add-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="d0c60-118">For more information, see [Add a custom domain name](add-custom-domain.md).</span></span>
> * <span data-ttu-id="d0c60-119">登入頁面商標不會延續到個人 Microsoft 帳戶的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="d0c60-119">Sign-in page branding doesn’t carry over to the sign-in page for personal Microsoft accounts.</span></span> <span data-ttu-id="d0c60-120">如果您的員工或商務來賓使用個人 Microsoft 帳戶登入，其登入頁面不會反映貴組織的商標。</span><span class="sxs-lookup"><span data-stu-id="d0c60-120">If your employees or business guests sign in with a personal Microsoft account, their sign-in page does not reflect the branding of your organization.</span></span>


### <a name="banner-logo"></a><span data-ttu-id="d0c60-121">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="d0c60-121">Banner logo</span></span> 

<span data-ttu-id="d0c60-122">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-122">Description</span></span> | <span data-ttu-id="d0c60-123">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-123">Constraints</span></span> | <span data-ttu-id="d0c60-124">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-124">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-125">橫幅標誌會顯示在 [登入] 和 [存取面板] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="d0c60-125">The banner logo is displayed on the sign-in and the Access panel pages.</span></span><br><span data-ttu-id="d0c60-126">在 [登入] 頁面上，標誌在使用者組織確定後才會顯示，這通常是在使用者名稱輸入後。</span><span class="sxs-lookup"><span data-stu-id="d0c60-126">On the sign-in page, this shows once the user’s organization is determined, usually after the username is entered.</span></span>  | <span data-ttu-id="d0c60-127">透明 JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="d0c60-127">Transparent JPG or PNG</span></span><br><span data-ttu-id="d0c60-128">最大高度：36 像素</span><span class="sxs-lookup"><span data-stu-id="d0c60-128">Max height: 36 px</span></span><br><span data-ttu-id="d0c60-129">最大寬度：245 像素</span><span class="sxs-lookup"><span data-stu-id="d0c60-129">Max width: 245 px</span></span> | <span data-ttu-id="d0c60-130">在這裡使用您組織的標誌。</span><span class="sxs-lookup"><span data-stu-id="d0c60-130">Use your organization’s logo here.</span></span><br><span data-ttu-id="d0c60-131">使用透明的映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-131">Use a transparent image.</span></span> <span data-ttu-id="d0c60-132">請勿假設背景為白色。</span><span class="sxs-lookup"><span data-stu-id="d0c60-132">Don’t assume that the background will be white.</span></span><br><span data-ttu-id="d0c60-133">請勿在映像中的標誌周圍加上邊框間距，否則您的標誌會看起來不成比例。</span><span class="sxs-lookup"><span data-stu-id="d0c60-133">Do not add padding around your logo in the image or your logo will look disproportionately small.</span></span>

### <a name="username-hint"></a><span data-ttu-id="d0c60-134">使用者名稱提示</span><span class="sxs-lookup"><span data-stu-id="d0c60-134">Username hint</span></span>   
<span data-ttu-id="d0c60-135">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-135">Description</span></span> | <span data-ttu-id="d0c60-136">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-136">Constraints</span></span> | <span data-ttu-id="d0c60-137">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-137">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-138">這可自訂使用者名稱欄位中的提示文字。</span><span class="sxs-lookup"><span data-stu-id="d0c60-138">This customizes the hint text in the username field.</span></span> | <span data-ttu-id="d0c60-139">Unicode 文字最多 64 個字元</span><span class="sxs-lookup"><span data-stu-id="d0c60-139">Unicode text up to 64 characters</span></span><br><span data-ttu-id="d0c60-140">僅限純文字</span><span class="sxs-lookup"><span data-stu-id="d0c60-140">Plain text only</span></span> | <span data-ttu-id="d0c60-141">如果您希望貴組織以外的來賓使用者登入您的應用程式，建議您不要設定此項目。</span><span class="sxs-lookup"><span data-stu-id="d0c60-141">We recommend that you do not set this if you expect guest users outside your organization to sign in to your app.</span></span>
            
### <a name="sign-in-page-text"></a><span data-ttu-id="d0c60-142">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="d0c60-142">Sign-in page text</span></span>   
<span data-ttu-id="d0c60-143">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-143">Description</span></span> | <span data-ttu-id="d0c60-144">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-144">Constraints</span></span> | <span data-ttu-id="d0c60-145">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-145">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-146">這會出現在登入表單底部，可用來提供其他資訊 (例如技術支援中心的電話號碼)，或顯示法律聲明。</span><span class="sxs-lookup"><span data-stu-id="d0c60-146">This appears at the bottom of the sign-in form and can be used to communicate additional information such as the phone number to your help desk, or a legal statement.</span></span> | <span data-ttu-id="d0c60-147">Unicode 文字最多 256 個字元</span><span class="sxs-lookup"><span data-stu-id="d0c60-147">Unicode text up to 256 characters</span></span><br><span data-ttu-id="d0c60-148">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="d0c60-148">Plain text only (no links or HTML tags)</span></span>   

### <a name="sign-in-page-image"></a><span data-ttu-id="d0c60-149">登入頁面映像</span><span class="sxs-lookup"><span data-stu-id="d0c60-149">Sign-in page image</span></span>  
<span data-ttu-id="d0c60-150">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-150">Description</span></span> | <span data-ttu-id="d0c60-151">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-151">Constraints</span></span> | <span data-ttu-id="d0c60-152">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-152">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-153">這會出現在登入頁面的背景，錨定至可檢視空間的中心，並且會調整並裁切以填滿瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="d0c60-153">This appears in the background of the sign-in page, is anchored to the center of the viewable space, and will scale and crop to fill the browser window.</span></span>    <br><span data-ttu-id="d0c60-154">在手機這類螢幕狹窄的裝置上，不會顯示此映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-154">On narrow screens such as mobile phones, this image is not shown.</span></span><br><span data-ttu-id="d0c60-155">載入頁面時，會根據我們的程式碼套用 0.55 不透明度的黑色遮罩至此映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-155">A black mask with 0.55 opacity will be applied over this image by our code when the page is loaded.</span></span> | <span data-ttu-id="d0c60-156">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="d0c60-156">JPG or PNG</span></span><br><span data-ttu-id="d0c60-157">映像尺寸：1920 x 1080 像素</span><span class="sxs-lookup"><span data-stu-id="d0c60-157">Image dimensions: 1920x1080 px</span></span><br><span data-ttu-id="d0c60-158">檔案大小：&gt; 300 KB</span><span class="sxs-lookup"><span data-stu-id="d0c60-158">File size: &gt; 300 KB</span></span> | <br><span data-ttu-id="d0c60-159">使用沒有強烈主題焦點的映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-159">Use images where there isn't a strong subject focus.</span></span> <span data-ttu-id="d0c60-160">不透明的登入表單隨即出現在映像中央，並且可根據瀏覽器視窗的大小來覆蓋映像的任何部分。</span><span class="sxs-lookup"><span data-stu-id="d0c60-160">The opaque sign-in form appears over the center of this image and can cover any part of the image depending on the size of the browser window.</span></span><br><span data-ttu-id="d0c60-161">檔案大小保持越小越好，以確保快速載入時間。</span><span class="sxs-lookup"><span data-stu-id="d0c60-161">Keep the file size as small as possible to ensure quick load times.</span></span> 

### <a name="background-color"></a><span data-ttu-id="d0c60-162">背景色彩</span><span class="sxs-lookup"><span data-stu-id="d0c60-162">Background Color</span></span>
<span data-ttu-id="d0c60-163">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-163">Description</span></span> | <span data-ttu-id="d0c60-164">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-164">Constraints</span></span> | <span data-ttu-id="d0c60-165">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-165">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-166">在低頻寬連線時，此顏色會用來取代背景映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-166">This color is used in place of the background image on low-bandwidth connections.</span></span> | <span data-ttu-id="d0c60-167">十六進位格式的 RGB 色彩 (範例：#FFFFFF</span><span class="sxs-lookup"><span data-stu-id="d0c60-167">RGB color in hexadecimal (example: #FFFFFF</span></span> | <span data-ttu-id="d0c60-168">建議使用橫幅標誌的主要顏色或貴組織的代表顏色。</span><span class="sxs-lookup"><span data-stu-id="d0c60-168">We suggest using the primary color of the banner logo or your organization color.</span></span>

### <a name="show-option-to-remain-signed-in"></a><span data-ttu-id="d0c60-169">顯示保持登入的選項</span><span class="sxs-lookup"><span data-stu-id="d0c60-169">Show option to remain signed in</span></span>
<span data-ttu-id="d0c60-170">說明</span><span class="sxs-lookup"><span data-stu-id="d0c60-170">Description</span></span> | <span data-ttu-id="d0c60-171">條件約束</span><span class="sxs-lookup"><span data-stu-id="d0c60-171">Constraints</span></span> | <span data-ttu-id="d0c60-172">建議</span><span class="sxs-lookup"><span data-stu-id="d0c60-172">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="d0c60-173">Azure AD 登入可讓使用者選擇在關閉並重新開啟其瀏覽器時保持登入。</span><span class="sxs-lookup"><span data-stu-id="d0c60-173">Azure AD sign in gives the user the option to remain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="d0c60-174">使用此項目來隱藏該選項。</span><span class="sxs-lookup"><span data-stu-id="d0c60-174">Use this to hide that option.</span></span><br><span data-ttu-id="d0c60-175">將此設為 [否]，以向您的使用者隱藏此選項。</span><span class="sxs-lookup"><span data-stu-id="d0c60-175">Set this to “No” to hide this option from your users.</span></span> | &nbsp; | <span data-ttu-id="d0c60-176">這不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="d0c60-176">This does not affect session lifetime.</span></span><br><span data-ttu-id="d0c60-177">SharePoint Online 和 Office 2010 的某些功能取決於能夠選擇此選項以保持登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="d0c60-177">Some features of SharePoint Online and Office 2010 depend on users being able to choose to remain signed in.</span></span> <span data-ttu-id="d0c60-178">如果您將此設為隱藏，使用者可能會在登入時看見其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="d0c60-178">If you set this to be hidden, your users may see additional and unexpected prompts to sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="d0c60-179">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="d0c60-179">All elements are optional.</span></span> <span data-ttu-id="d0c60-180">例如，如果您指定的橫幅標誌沒有任何背景映像，登入頁面會針對目的地網站 (例如，Office 365) 顯示您的標誌和背景映像。</span><span class="sxs-lookup"><span data-stu-id="d0c60-180">For example, if you specify a banner logo with no background image, the sign-in page will show your logo and the background image for the destination site (for example, Office 365).</span></span>

## <a name="add-company-branding-to-your-directory"></a><span data-ttu-id="d0c60-181">將公司商標新增到您的目錄</span><span class="sxs-lookup"><span data-stu-id="d0c60-181">Add company branding to your directory</span></span>

1. <span data-ttu-id="d0c60-182">使用具備目錄全域管理員身分的帳戶來登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d0c60-182">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d0c60-183">選取 [更多服務]，在文字方塊中輸入「使用者和群組」，然後選取 **Enter**。</span><span class="sxs-lookup"><span data-stu-id="d0c60-183">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="d0c60-185">在 [使用者和群組] 刀鋒視窗上，選取 [公司商標]。</span><span class="sxs-lookup"><span data-stu-id="d0c60-185">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="d0c60-186">在 [使用者和群組 - 公司商標] 刀鋒視窗上，選取 [編輯] 命令。</span><span class="sxs-lookup"><span data-stu-id="d0c60-186">On the **Users and groups - Company branding** blade, select the **Edit** command.</span></span>

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="d0c60-188">修改您想要自訂的元素。</span><span class="sxs-lookup"><span data-stu-id="d0c60-188">Modify the elements you want to customize.</span></span> <span data-ttu-id="d0c60-189">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="d0c60-189">All elements are optional.</span></span>
6. <span data-ttu-id="d0c60-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d0c60-190">Click **Save**.</span></span>

<span data-ttu-id="d0c60-191">您對登入頁面商標所做的任何變更可能最多需要一個小時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="d0c60-191">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="add-language-specific-company-branding-to-your-directory"></a><span data-ttu-id="d0c60-192">將特定語言公司商標新增到您的目錄</span><span class="sxs-lookup"><span data-stu-id="d0c60-192">Add language-specific company branding to your directory</span></span>

1. <span data-ttu-id="d0c60-193">使用具備目錄全域管理員身分的帳戶來登入 [Azure AD 管理中心](https://aad.portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d0c60-193">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="d0c60-194">在文字方塊中選取 [使用者和群組]，然後選取 [Enter]。</span><span class="sxs-lookup"><span data-stu-id="d0c60-194">Select **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="d0c60-196">在 [使用者和群組] 刀鋒視窗上，選取 [公司商標]。</span><span class="sxs-lookup"><span data-stu-id="d0c60-196">On the **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="d0c60-197">在 [使用者和群組 - 公司商標] 刀鋒視窗上，選取 [新增語言] 命令。</span><span class="sxs-lookup"><span data-stu-id="d0c60-197">On the **Users and groups - Company branding** blade, select the **Add language** command.</span></span>

    ![新增語言特定商標元素](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="d0c60-199">修改您想要自訂的元素。</span><span class="sxs-lookup"><span data-stu-id="d0c60-199">Modify the elements you want to customize.</span></span> <span data-ttu-id="d0c60-200">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="d0c60-200">All elements are optional.</span></span>
6. <span data-ttu-id="d0c60-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d0c60-201">Click **Save**.</span></span>

<span data-ttu-id="d0c60-202">您對登入頁面商標所做的任何變更可能最多需要一個小時才會顯示。</span><span class="sxs-lookup"><span data-stu-id="d0c60-202">It can take up to an hour for any changes you made to the sign-in page branding to appear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0c60-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d0c60-203">Next steps</span></span>
<span data-ttu-id="d0c60-204">本快速入門中，您會了解如何將公司商標新增到您的 Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="d0c60-204">In this quickstart, you’ve learned how to add company branding to your Azure AD directory.</span></span> 

<span data-ttu-id="d0c60-205">您可以從 Azure 入口網站使用下列連結在 Azure AD 中設定公司商標。</span><span class="sxs-lookup"><span data-stu-id="d0c60-205">You can use the following link to configure your company branding in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d0c60-206">設定公司商標</span><span class="sxs-lookup"><span data-stu-id="d0c60-206">Configure company branding</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 