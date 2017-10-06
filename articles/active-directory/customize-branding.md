---
title: "登入頁面 hello Azure Active Directory aaaCustomize |Microsoft 文件"
description: "深入了解如何 tooadd 公司品牌 toohello Azure 登入頁面"
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
ms.openlocfilehash: 7a7ccdeef0764f6cf9e9e224acd4350983031fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-company-branding-tooyour-sign-in-page-in-azure-ad"></a><span data-ttu-id="2be82-103">快速入門： 新增公司品牌 tooyour 登入頁面，在 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="2be82-103">Quickstart: Add company branding tooyour sign-in page in Azure AD</span></span>
<span data-ttu-id="2be82-104">tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。</span><span class="sxs-lookup"><span data-stu-id="2be82-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="2be82-105">Azure Active Directory (Azure AD) 這項功能可讓您提供 toocustomize hello 外觀 hello 登入頁面與您的公司標誌自訂色彩配置。</span><span class="sxs-lookup"><span data-stu-id="2be82-105">Azure Active Directory (Azure AD) provides this capability by allowing you toocustomize hello appearance of hello sign-in page with your company logo and custom color schemes.</span></span> <span data-ttu-id="2be82-106">hello 登入頁面為 hello 頁面，會出現在您登入 tooOffice 365 或其他 web 應用程式使用 Azure AD 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="2be82-106">hello sign-in page is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="2be82-107">您互動此頁面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="2be82-107">You interact with this page tooenter your credentials.</span></span>

> [!NOTE]
> * <span data-ttu-id="2be82-108">公司商標 toohello Premium 或 Basic 版的 Azure AD 中，您升級時，才可以使用，或有 Office 365 授權。</span><span class="sxs-lookup"><span data-stu-id="2be82-108">Company branding is available only if you upgraded toohello Premium or Basic edition of Azure AD, or have an Office 365 license.</span></span> <span data-ttu-id="2be82-109">toolearn，如果您的授權類型的支援功能檢查 hello [Azure Active Directory 定價資訊頁面](https://azure.microsoft.com/pricing/details/active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="2be82-109">toolearn if a feature is supported by your license type, check hello [Azure Active Directory pricing information page](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>
> 
> * <span data-ttu-id="2be82-110">Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。</span><span class="sxs-lookup"><span data-stu-id="2be82-110">Azure Active Directory Premium and Basic editions are available for customers in China using hello worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="2be82-111">Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。</span><span class="sxs-lookup"><span data-stu-id="2be82-111">Azure Active Directory Premium and Basic editions are not currently supported in hello Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="2be82-112">如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="2be82-112">For more information, contact us at hello [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="2be82-113">自訂 hello 登入頁面</span><span class="sxs-lookup"><span data-stu-id="2be82-113">Customizing hello sign-in page</span></span>

<!--You can customize hello following elements on hello sign-in page: <attach image>-->

<span data-ttu-id="2be82-114">公司商標自訂會出現在 hello Azure AD 登入頁面上，當使用者存取租用戶特定 URL 這類[ *https://outlook.com/contoso.com*](https://outlook.com/contoso.com)。</span><span class="sxs-lookup"><span data-stu-id="2be82-114">Company branding customizations appear on hello Azure AD sign-in page when users access a tenant-specific URL such as [*https://outlook.com/contoso.com*](https://outlook.com/contoso.com).</span></span>

<span data-ttu-id="2be82-115">當使用者造訪泛型的 URL，例如 www.office.com 時，hello 登入頁面將不包含公司商標自訂項目，因為 hello 系統並不知道 hello 使用者是誰。</span><span class="sxs-lookup"><span data-stu-id="2be82-115">When users visit a generic URL such as www.office.com, hello sign-in page does not contain company branding customizations because hello system doesn’t know who hello user is.</span></span> <span data-ttu-id="2be82-116">使用者輸入其使用者識別碼或選取使用者圖格之後，就會顯示公司商標。</span><span class="sxs-lookup"><span data-stu-id="2be82-116">Company branding will show after users enter their user ID or select a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="2be82-117">您的網域名稱必須為 使用出現在 hello**網域**部分 hello Azure 入口網站中您已設定的商標。</span><span class="sxs-lookup"><span data-stu-id="2be82-117">Your domain name must appear as “Active" in hello **Domains** portion of hello Azure portal in which you have configured branding.</span></span> <span data-ttu-id="2be82-118">如需詳細資訊，請參閱[新增自訂網域名稱](add-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="2be82-118">For more information, see [Add a custom domain name](add-custom-domain.md).</span></span>
> * <span data-ttu-id="2be82-119">登入頁面品牌不會延續 toohello 登入頁面上的個人 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2be82-119">Sign-in page branding doesn’t carry over toohello sign-in page for personal Microsoft accounts.</span></span> <span data-ttu-id="2be82-120">如果訪客或員工使用個人 Microsoft 帳戶登入時，他們的登入頁面並不會反映您組織的品牌 hello。</span><span class="sxs-lookup"><span data-stu-id="2be82-120">If your employees or business guests sign in with a personal Microsoft account, their sign-in page does not reflect hello branding of your organization.</span></span>


### <a name="banner-logo"></a><span data-ttu-id="2be82-121">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="2be82-121">Banner logo</span></span> 

<span data-ttu-id="2be82-122">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-122">Description</span></span> | <span data-ttu-id="2be82-123">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-123">Constraints</span></span> | <span data-ttu-id="2be82-124">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-124">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-125">hello 橫幅標誌 顯示 hello 登入與 hello 存取面板頁面上。</span><span class="sxs-lookup"><span data-stu-id="2be82-125">hello banner logo is displayed on hello sign-in and hello Access panel pages.</span></span><br><span data-ttu-id="2be82-126">在 hello 登入頁面上，這會顯示 hello 使用者的組織是一旦決定後，通常之後輸入 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2be82-126">On hello sign-in page, this shows once hello user’s organization is determined, usually after hello username is entered.</span></span>  | <span data-ttu-id="2be82-127">透明 JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="2be82-127">Transparent JPG or PNG</span></span><br><span data-ttu-id="2be82-128">最大高度：36 像素</span><span class="sxs-lookup"><span data-stu-id="2be82-128">Max height: 36 px</span></span><br><span data-ttu-id="2be82-129">最大寬度：245 像素</span><span class="sxs-lookup"><span data-stu-id="2be82-129">Max width: 245 px</span></span> | <span data-ttu-id="2be82-130">在這裡使用您組織的標誌。</span><span class="sxs-lookup"><span data-stu-id="2be82-130">Use your organization’s logo here.</span></span><br><span data-ttu-id="2be82-131">使用透明的映像。</span><span class="sxs-lookup"><span data-stu-id="2be82-131">Use a transparent image.</span></span> <span data-ttu-id="2be82-132">請勿假設 hello 背景為白色。</span><span class="sxs-lookup"><span data-stu-id="2be82-132">Don’t assume that hello background will be white.</span></span><br><span data-ttu-id="2be82-133">不要在 hello 映像中新增您的標誌周圍填補，或您的標誌會尋找不當比例的小型。</span><span class="sxs-lookup"><span data-stu-id="2be82-133">Do not add padding around your logo in hello image or your logo will look disproportionately small.</span></span>

### <a name="username-hint"></a><span data-ttu-id="2be82-134">使用者名稱提示</span><span class="sxs-lookup"><span data-stu-id="2be82-134">Username hint</span></span>   
<span data-ttu-id="2be82-135">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-135">Description</span></span> | <span data-ttu-id="2be82-136">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-136">Constraints</span></span> | <span data-ttu-id="2be82-137">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-137">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-138">此自訂 hello 使用者名稱 欄位中的 hello 提示文字。</span><span class="sxs-lookup"><span data-stu-id="2be82-138">This customizes hello hint text in hello username field.</span></span> | <span data-ttu-id="2be82-139">向上 too64 字元的 Unicode 文字</span><span class="sxs-lookup"><span data-stu-id="2be82-139">Unicode text up too64 characters</span></span><br><span data-ttu-id="2be82-140">僅限純文字</span><span class="sxs-lookup"><span data-stu-id="2be82-140">Plain text only</span></span> | <span data-ttu-id="2be82-141">我們建議您不要設定此如果希望外部 tooyour 應用程式在您的組織 toosign guest 使用者。</span><span class="sxs-lookup"><span data-stu-id="2be82-141">We recommend that you do not set this if you expect guest users outside your organization toosign in tooyour app.</span></span>
            
### <a name="sign-in-page-text"></a><span data-ttu-id="2be82-142">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="2be82-142">Sign-in page text</span></span>   
<span data-ttu-id="2be82-143">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-143">Description</span></span> | <span data-ttu-id="2be82-144">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-144">Constraints</span></span> | <span data-ttu-id="2be82-145">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-145">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-146">這會出現在 hello hello 登入表單底部，而且可以使用的 toocommunicate 的其他資訊，例如 hello 電話號碼 tooyour 服務台或法律聲明。</span><span class="sxs-lookup"><span data-stu-id="2be82-146">This appears at hello bottom of hello sign-in form and can be used toocommunicate additional information such as hello phone number tooyour help desk, or a legal statement.</span></span> | <span data-ttu-id="2be82-147">向上 too256 字元的 Unicode 文字</span><span class="sxs-lookup"><span data-stu-id="2be82-147">Unicode text up too256 characters</span></span><br><span data-ttu-id="2be82-148">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="2be82-148">Plain text only (no links or HTML tags)</span></span> 

### <a name="sign-in-page-image"></a><span data-ttu-id="2be82-149">登入頁面映像</span><span class="sxs-lookup"><span data-stu-id="2be82-149">Sign-in page image</span></span>  
<span data-ttu-id="2be82-150">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-150">Description</span></span> | <span data-ttu-id="2be82-151">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-151">Constraints</span></span> | <span data-ttu-id="2be82-152">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-152">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-153">這會出現在 hello hello 登入頁面背景錨定的 toohello center hello 可檢視的空間，並將調整規模並且裁剪 toofill hello 瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="2be82-153">This appears in hello background of hello sign-in page, is anchored toohello center of hello viewable space, and will scale and crop toofill hello browser window.</span></span>  <br><span data-ttu-id="2be82-154">在手機這類螢幕狹窄的裝置上，不會顯示此映像。</span><span class="sxs-lookup"><span data-stu-id="2be82-154">On narrow screens such as mobile phones, this image is not shown.</span></span><br><span data-ttu-id="2be82-155">0.55 不透明的黑色遮罩會套用此映像透過我們的程式碼載入 hello 頁面時。</span><span class="sxs-lookup"><span data-stu-id="2be82-155">A black mask with 0.55 opacity will be applied over this image by our code when hello page is loaded.</span></span> | <span data-ttu-id="2be82-156">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="2be82-156">JPG or PNG</span></span><br><span data-ttu-id="2be82-157">映像尺寸：1920 x 1080 像素</span><span class="sxs-lookup"><span data-stu-id="2be82-157">Image dimensions: 1920x1080 px</span></span><br><span data-ttu-id="2be82-158">檔案大小：&gt; 300 KB</span><span class="sxs-lookup"><span data-stu-id="2be82-158">File size: &gt; 300 KB</span></span> | <br><span data-ttu-id="2be82-159">使用沒有強烈主題焦點的映像。</span><span class="sxs-lookup"><span data-stu-id="2be82-159">Use images where there isn't a strong subject focus.</span></span> <span data-ttu-id="2be82-160">表單登入的不透明 hello 停留 hello 中心，這個影像的周圍會出現，並可涵蓋 hello 映像，依據 hello hello 瀏覽器視窗大小的任何部分。</span><span class="sxs-lookup"><span data-stu-id="2be82-160">hello opaque sign-in form appears over hello center of this image and can cover any part of hello image depending on hello size of hello browser window.</span></span><br><span data-ttu-id="2be82-161">保留 hello 檔案大小越小越可能 tooensure 快速載入時間。</span><span class="sxs-lookup"><span data-stu-id="2be82-161">Keep hello file size as small as possible tooensure quick load times.</span></span> 

### <a name="background-color"></a><span data-ttu-id="2be82-162">背景色彩</span><span class="sxs-lookup"><span data-stu-id="2be82-162">Background Color</span></span>
<span data-ttu-id="2be82-163">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-163">Description</span></span> | <span data-ttu-id="2be82-164">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-164">Constraints</span></span> | <span data-ttu-id="2be82-165">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-165">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-166">此色彩會使用來取代 hello 低頻寬連線的背景影像。</span><span class="sxs-lookup"><span data-stu-id="2be82-166">This color is used in place of hello background image on low-bandwidth connections.</span></span> |   <span data-ttu-id="2be82-167">十六進位格式的 RGB 色彩 (範例：#FFFFFF</span><span class="sxs-lookup"><span data-stu-id="2be82-167">RGB color in hexadecimal (example: #FFFFFF</span></span> | <span data-ttu-id="2be82-168">我們建議使用 hello 主要色彩的 hello 橫幅標誌或您組織的色彩。</span><span class="sxs-lookup"><span data-stu-id="2be82-168">We suggest using hello primary color of hello banner logo or your organization color.</span></span>

### <a name="show-option-tooremain-signed-in"></a><span data-ttu-id="2be82-169">顯示選項 tooremain 登入</span><span class="sxs-lookup"><span data-stu-id="2be82-169">Show option tooremain signed in</span></span>
<span data-ttu-id="2be82-170">說明</span><span class="sxs-lookup"><span data-stu-id="2be82-170">Description</span></span> | <span data-ttu-id="2be82-171">條件約束</span><span class="sxs-lookup"><span data-stu-id="2be82-171">Constraints</span></span> | <span data-ttu-id="2be82-172">建議</span><span class="sxs-lookup"><span data-stu-id="2be82-172">Recommendations</span></span>
------- | ------- | ----------
<span data-ttu-id="2be82-173">Azure AD 登入提供 hello 使用者 hello 選項 tooremain 時關閉並重新開啟瀏覽器登入。</span><span class="sxs-lookup"><span data-stu-id="2be82-173">Azure AD sign in gives hello user hello option tooremain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="2be82-174">使用此 toohide 該選項。</span><span class="sxs-lookup"><span data-stu-id="2be82-174">Use this toohide that option.</span></span><br><span data-ttu-id="2be82-175">設定這太"No"toohide 此選項，從您的使用者。</span><span class="sxs-lookup"><span data-stu-id="2be82-175">Set this too“No” toohide this option from your users.</span></span> | &nbsp; | <span data-ttu-id="2be82-176">這不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="2be82-176">This does not affect session lifetime.</span></span><br><span data-ttu-id="2be82-177">SharePoint Online 和 Office 2010 的某些功能會相依於無法 toochoose tooremain 登入的使用者。</span><span class="sxs-lookup"><span data-stu-id="2be82-177">Some features of SharePoint Online and Office 2010 depend on users being able toochoose tooremain signed in.</span></span> <span data-ttu-id="2be82-178">如果您設定此 toobe 隱藏，使用者可能會看到 toosign 中其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="2be82-178">If you set this toobe hidden, your users may see additional and unexpected prompts toosign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="2be82-179">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2be82-179">All elements are optional.</span></span> <span data-ttu-id="2be82-180">例如，如果您不指定任何背景影像橫幅標誌，hello 登入頁面會顯示 hello 目的地站台 (例如，Office 365) 您的標誌和 hello 背景影像。</span><span class="sxs-lookup"><span data-stu-id="2be82-180">For example, if you specify a banner logo with no background image, hello sign-in page will show your logo and hello background image for hello destination site (for example, Office 365).</span></span>

## <a name="add-company-branding-tooyour-directory"></a><span data-ttu-id="2be82-181">新增公司品牌 tooyour 目錄</span><span class="sxs-lookup"><span data-stu-id="2be82-181">Add company branding tooyour directory</span></span>

1. <span data-ttu-id="2be82-182">登入太[hello Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2be82-182">Sign in too[hello Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2be82-183">選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="2be82-183">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-custom-signon-azure-portal/user-management.png)
3. <span data-ttu-id="2be82-185">在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。</span><span class="sxs-lookup"><span data-stu-id="2be82-185">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="2be82-186">在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**編輯**命令。</span><span class="sxs-lookup"><span data-stu-id="2be82-186">On hello **Users and groups - Company branding** blade, select hello **Edit** command.</span></span>

    ![編輯自訂商標](./media/active-directory-branding-custom-signon-azure-portal/edit-branding.png)
5. <span data-ttu-id="2be82-188">修改您想 toocustomize 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="2be82-188">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="2be82-189">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2be82-189">All elements are optional.</span></span>
6. <span data-ttu-id="2be82-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2be82-190">Click **Save**.</span></span>

<span data-ttu-id="2be82-191">如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="2be82-191">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="add-language-specific-company-branding-tooyour-directory"></a><span data-ttu-id="2be82-192">將語言特定公司商標 tooyour 目錄</span><span class="sxs-lookup"><span data-stu-id="2be82-192">Add language-specific company branding tooyour directory</span></span>

1. <span data-ttu-id="2be82-193">登入 toohello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2be82-193">Sign in toohello [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2be82-194">選取**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。</span><span class="sxs-lookup"><span data-stu-id="2be82-194">Select **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![開啟使用者管理](./media/active-directory-branding-localize-azure-portal/user-management.png)
3. <span data-ttu-id="2be82-196">在 hello**使用者和群組**刀鋒視窗中，選取**公司商標**。</span><span class="sxs-lookup"><span data-stu-id="2be82-196">On hello **Users and groups** blade, select **Company branding**.</span></span>
4. <span data-ttu-id="2be82-197">在 hello**使用者和群組-公司商標**刀鋒視窗中，選取 hello**新增語言**命令。</span><span class="sxs-lookup"><span data-stu-id="2be82-197">On hello **Users and groups - Company branding** blade, select hello **Add language** command.</span></span>

    ![新增語言特定商標元素](./media/active-directory-branding-localize-azure-portal/add-language.png)
5. <span data-ttu-id="2be82-199">修改您想 toocustomize 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="2be82-199">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="2be82-200">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2be82-200">All elements are optional.</span></span>
6. <span data-ttu-id="2be82-201">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2be82-201">Click **Save**.</span></span>

<span data-ttu-id="2be82-202">如您所做 toohello 登入頁面品牌 tooappear，它可能佔用 tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="2be82-202">It can take up tooan hour for any changes you made toohello sign-in page branding tooappear.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2be82-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2be82-203">Next steps</span></span>
<span data-ttu-id="2be82-204">本快速入門中，您學到如何 tooadd 公司商標 tooyour Azure AD 目錄。</span><span class="sxs-lookup"><span data-stu-id="2be82-204">In this quickstart, you’ve learned how tooadd company branding tooyour Azure AD directory.</span></span> 

<span data-ttu-id="2be82-205">您可以使用下列連結 tooconfigure 中公司商標 hello 從 Azure AD Azure 入口網站的 hello。</span><span class="sxs-lookup"><span data-stu-id="2be82-205">You can use hello following link tooconfigure your company branding in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2be82-206">設定公司商標</span><span class="sxs-lookup"><span data-stu-id="2be82-206">Configure company branding</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LoginTenantBrandingBlade) 