---
title: "aaaAdd 公司品牌 tooyour 登入和存取面板頁面"
description: "了解如何 tooadd 公司品牌 toohello Azure 登入頁面和 hello 存取面板頁面"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: f74621b4-4ef0-4899-8c0e-0c20347a8c31
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/23/2017
ms.author: curtand
ms.openlocfilehash: b1c6442028393552bff3d380312c8cd1bfda5d31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-company-branding-tooyour-sign-in-and-access-panel-pages"></a><span data-ttu-id="2e54d-103">新增公司品牌 tooyour 登入和存取面板頁面</span><span class="sxs-lookup"><span data-stu-id="2e54d-103">Add company branding tooyour sign-in and Access Panel pages</span></span>
<span data-ttu-id="2e54d-104">tooavoid 混淆的可能性，許多公司都想 tooapply 一致的外觀及操作所有 hello 網站和他們管理的服務。</span><span class="sxs-lookup"><span data-stu-id="2e54d-104">tooavoid confusion, many companies want tooapply a consistent look and feel across all hello websites and services they manage.</span></span> <span data-ttu-id="2e54d-105">Azure Active Directory 可讓您遵循網頁與您的公司標誌自訂色彩配置的 hello toocustomize hello 外觀提供這項功能：</span><span class="sxs-lookup"><span data-stu-id="2e54d-105">Azure Active Directory provides this capability by allowing you toocustomize hello appearance of hello following web pages with your company logo and custom color schemes:</span></span>

* <span data-ttu-id="2e54d-106">**登入頁面**-這是出現在您登入 tooOffice 365 hello 頁面或其他 web 應用程式使用 Azure AD 作為身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="2e54d-106">**Sign-in page** - This is hello page that appears when you sign in tooOffice 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="2e54d-107">您與此頁面互動主領域探索或 tooenter 期間您的認證。</span><span class="sxs-lookup"><span data-stu-id="2e54d-107">You interact with this page either during a Home Realm Discovery or tooenter your credentials.</span></span> <span data-ttu-id="2e54d-108">hello 主領域探索可讓 hello 系統 tooredirect 同盟使用者 tootheir 內部部署 STS （例如 AD FS)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-108">hello Home Realm Discovery allows hello system tooredirect federated users tootheir on-premises STS (such as AD FS).</span></span>
* <span data-ttu-id="2e54d-109">**存取面板頁面**-hello 存取面板是網頁型入口網站，可讓您 tooview 及啟動 hello 雲端型應用程式您 Azure AD 管理員已授與您存取權。</span><span class="sxs-lookup"><span data-stu-id="2e54d-109">**Access Panel page** - hello Access Panel is a web-based portal that allows you tooview and launch hello cloud-based applications your Azure AD administrator has granted you access to.</span></span> <span data-ttu-id="2e54d-110">tooaccess hello 存取面板中，使用下列 URL 的 hello: [https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-110">tooaccess hello Access Panel, use hello following URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

<span data-ttu-id="2e54d-111">本主題說明如何自訂登入頁面 hello 和 hello 存取面板頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-111">This topic explains how you can customize hello sign-in page and hello access panel page.</span></span>

> [!NOTE]
> * <span data-ttu-id="2e54d-112">公司商標是只適用於您已升級 toohello Premium 或 Azure Active Directory Basic 版或 Office 365 使用者的功能。</span><span class="sxs-lookup"><span data-stu-id="2e54d-112">Company branding is a feature that is available only if you upgraded toohello Premium or Basic edition of Azure Active Directory, or are an Office 365 user.</span></span> <span data-ttu-id="2e54d-113">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-113">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>
> * <span data-ttu-id="2e54d-114">Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。</span><span class="sxs-lookup"><span data-stu-id="2e54d-114">Azure Active Directory Premium and Basic editions are available for customers in China using hello worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="2e54d-115">Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。</span><span class="sxs-lookup"><span data-stu-id="2e54d-115">Azure Active Directory Premium and Basic editions are not currently supported in hello Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="2e54d-116">如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-116">For more information, contact us at hello [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
>
>

## <a name="customizing-hello-sign-in-page"></a><span data-ttu-id="2e54d-117">自訂 hello 登入頁面</span><span class="sxs-lookup"><span data-stu-id="2e54d-117">Customizing hello sign-in page</span></span>
<span data-ttu-id="2e54d-118">一般而言，如果您需要瀏覽器為基礎的存取 tooyour 雲端應用程式和貴組織訂閱的服務，您可以使用 hello 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-118">Typically, if you need browser-based access tooyour cloud apps and services that your organization subscribes to, you use hello sign-in page.</span></span>

<span data-ttu-id="2e54d-119">如果您已套用變更 tooyour 登入頁面上，就可以在 hello 變更 tooappear tooan 小時。</span><span class="sxs-lookup"><span data-stu-id="2e54d-119">If you have applied changes tooyour sign-in page, it can take up tooan hour for hello changes tooappear.</span></span>

<span data-ttu-id="2e54d-120">只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-120">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="2e54d-121">當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-121">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="2e54d-122">在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。</span><span class="sxs-lookup"><span data-stu-id="2e54d-122">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="2e54d-123">您的網域名稱必須為 使用出現在 hello **Active Directory** > **目錄** > **網域**區段 hello Azure 傳統入口網站在您已設定的商標。</span><span class="sxs-lookup"><span data-stu-id="2e54d-123">Your domain name must appear as “Active” in hello **Active Directory** > **Directory** > **Domains** section of hello Azure classic portal where you have configured branding.</span></span>
> * <span data-ttu-id="2e54d-124">登入頁面品牌不會延續 toohello 消費者登入的 Microsoft 的頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-124">Sign-in page branding doesn’t carry over toohello consumer sign in page of Microsoft.</span></span> <span data-ttu-id="2e54d-125">如果您使用個人 Microsoft 帳戶登入，您可能會看到加上品牌的 Azure AD 所呈現的使用者磚清單，但您組織的品牌 hello 不會套用 toohello Microsoft 帳戶登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-125">If you sign in with a personal Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but hello branding of your organization does not apply toohello Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="2e54d-126">如果您的公司品牌、 色彩和其他可自訂的元素，此頁面上，您會想 tooshow，請參閱下列映像 toounderstand hello hello 兩種體驗差異 hello。</span><span class="sxs-lookup"><span data-stu-id="2e54d-126">If you want tooshow your company brand, colors and other customizable elements on this page, see hello following images toounderstand hello difference between hello two experiences.</span></span>

<span data-ttu-id="2e54d-127">下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之前**自訂：</span><span class="sxs-lookup"><span data-stu-id="2e54d-127">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面][1]

<span data-ttu-id="2e54d-129">下列螢幕擷取畫面顯示和 hello Office 365 登入頁面在桌面的電腦上的範例 hello**之後**自訂：</span><span class="sxs-lookup"><span data-stu-id="2e54d-129">hello following screenshot shows and example for hello Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面][2]

<span data-ttu-id="2e54d-131">hello 下列螢幕擷取畫面顯示的範例登入頁面 hello Office 365 行動裝置上**之前**自訂：</span><span class="sxs-lookup"><span data-stu-id="2e54d-131">hello following screenshot shows an example of hello Office 365 sign-in page on a mobile device **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面][3]

<span data-ttu-id="2e54d-133">hello 下列螢幕擷取畫面顯示的範例登入頁面 hello Office 365 行動裝置上**之後**自訂：</span><span class="sxs-lookup"><span data-stu-id="2e54d-133">hello following screenshot shows an example of hello Office 365 sign-in page on a mobile device **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面][4]

<span data-ttu-id="2e54d-135">當您調整瀏覽器視窗時，hello 大型圖例，hello 像之前，顯示一個通常會裁剪 tooaccommodate 不同的螢幕外觀比例。</span><span class="sxs-lookup"><span data-stu-id="2e54d-135">When you resize a browser window, hello large Illustration, like hello one shown previously, is often cropped tooaccommodate different screen aspect ratios.</span></span> <span data-ttu-id="2e54d-136">這一點，您應該嘗試 tookeep hello 主要視覺元素 hello 圖中的，使其永遠顯示 hello 左上角 （右上由右至左語言）。</span><span class="sxs-lookup"><span data-stu-id="2e54d-136">With this in mind, you should try tookeep hello key visual elements in hello illustration so that they always appear in hello top-left corner (top-right for right-to-left languages).</span></span> <span data-ttu-id="2e54d-137">這是很重要，因為 hello 右下角出現朝上 / 左邊 hello 或從向 hello 上層 hello 底部調整大小通常就會發生。</span><span class="sxs-lookup"><span data-stu-id="2e54d-137">This is important because resizing typically occurs from hello bottom-right corner going towards hello top / left or from hello bottom towards hello top.</span></span>

<span data-ttu-id="2e54d-138">hello 下圖顯示剩餘的調整大小的 toohello hello 瀏覽器時，如何裁剪 hello 圖：</span><span class="sxs-lookup"><span data-stu-id="2e54d-138">hello following picture shows how hello illustration is cropped when hello browser is resized toohello left:</span></span>

![][6]

<span data-ttu-id="2e54d-139">以下是如何出現之後 hello 瀏覽器會調整大小接近 hello 上方：</span><span class="sxs-lookup"><span data-stu-id="2e54d-139">Here is how it appears after hello browser is resized toward hello top:</span></span>

![][7]

## <a name="what-elements-on-hello-page-can-i-customize"></a><span data-ttu-id="2e54d-140">可以自訂 hello 頁面上的哪些元素？</span><span class="sxs-lookup"><span data-stu-id="2e54d-140">What elements on hello page can I customize?</span></span>
<span data-ttu-id="2e54d-141">您可以自訂下列項目 hello 登入頁面上的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e54d-141">You can customize hello following elements on hello sign-in page:</span></span>

![][5]

| <span data-ttu-id="2e54d-142">頁面元素</span><span class="sxs-lookup"><span data-stu-id="2e54d-142">Page element</span></span> | <span data-ttu-id="2e54d-143">在 [hello] 頁面上的位置</span><span class="sxs-lookup"><span data-stu-id="2e54d-143">Location on hello page</span></span> |
|:--- | --- |
| <span data-ttu-id="2e54d-144">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="2e54d-144">Banner Logo</span></span> |<span data-ttu-id="2e54d-145">顯示 hello 的右上方 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-145">Shown at hello top-right of hello page.</span></span> <span data-ttu-id="2e54d-146">取代 hello 標誌 hello 目的地站台 （例如登入 toodisplays。</span><span class="sxs-lookup"><span data-stu-id="2e54d-146">Replaces hello logo hello destination site you are signing in toodisplays (For example.</span></span> <span data-ttu-id="2e54d-147">Office 365 或 Azure)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-147">Office 365 or Azure).</span></span> |
| <span data-ttu-id="2e54d-148">大型圖例/背景色彩</span><span class="sxs-lookup"><span data-stu-id="2e54d-148">Large Illustration / Background Color</span></span> |<span data-ttu-id="2e54d-149">顯示 hello hello 頁面左邊。</span><span class="sxs-lookup"><span data-stu-id="2e54d-149">Shown at hello left of hello page.</span></span> <span data-ttu-id="2e54d-150">會取代您要登入 toodisplays hello 映像 hello 目的地網站。</span><span class="sxs-lookup"><span data-stu-id="2e54d-150">Replaces hello image hello destination site you are signing in toodisplays.</span></span> <span data-ttu-id="2e54d-151">取代 hello 大型圖例在低頻寬連線或窄的畫面上，可能會顯示 hello 背景色彩。</span><span class="sxs-lookup"><span data-stu-id="2e54d-151">hello Background Color may be shown in place of hello Large Illustration on low bandwidth connections, or on narrow screens.</span></span> |
| <span data-ttu-id="2e54d-152">讓我保持登入</span><span class="sxs-lookup"><span data-stu-id="2e54d-152">Keep me signed-in</span></span> |<span data-ttu-id="2e54d-153">顯示在 hello 密碼文字方塊下方。</span><span class="sxs-lookup"><span data-stu-id="2e54d-153">Shown under hello Password textbox.</span></span> |
| <span data-ttu-id="2e54d-154">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-154">Sign-in Page Text</span></span> |<span data-ttu-id="2e54d-155">當您需要 tooconvey 很有幫助的資訊，再使用登入工作或學校帳戶時，上述 hello 頁尾。</span><span class="sxs-lookup"><span data-stu-id="2e54d-155">Shown above hello page footer when you need tooconvey helpful information before a sign-in with a work or school account.</span></span> <span data-ttu-id="2e54d-156">例如，您可能想 tooinclude hello 電話號碼 tooyour 服務台或法律聲明。</span><span class="sxs-lookup"><span data-stu-id="2e54d-156">For example, you may want tooinclude hello phone number tooyour help desk, or a legal statement.</span></span> |

> [!NOTE]
> <span data-ttu-id="2e54d-157">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2e54d-157">All elements are optional.</span></span> <span data-ttu-id="2e54d-158">比方說，如果您指定橫幅標誌 但沒有大型圖例，hello 登入頁面會顯示您的標誌和 hello 圖例中 hello 目的地站台 （也就是 hello Office 365 加州高速公路影像）。</span><span class="sxs-lookup"><span data-stu-id="2e54d-158">For example, if you specify a Banner Logo but no Large Illustration, hello sign-in page shows your logo and hello illustration for hello destination site (that is, hello Office 365 California highway image).</span></span>
>
>

<span data-ttu-id="2e54d-159">在您登入頁面上，hello**讓我保持登**核取方塊可讓使用者 tooremain 時關閉並重新開啟瀏覽器登入。</span><span class="sxs-lookup"><span data-stu-id="2e54d-159">On your sign-in page, hello **Keep me signed in** checkbox allows a user tooremain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="2e54d-160">它不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="2e54d-160">It does not effect session lifetime.</span></span> <span data-ttu-id="2e54d-161">您可以隱藏 hello hello Azure Active Directory 登入頁面上的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="2e54d-161">You can hide hello checkbox on hello Azure Active Directory sign-in page.</span></span>

<span data-ttu-id="2e54d-162">Hello 核取方塊會顯示是否取決 hello 設定**隱藏 KMSI**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-162">Whether hello checkbox is displayed depends on hello setting of **Hide KMSI**.</span></span>

![][9]

<span data-ttu-id="2e54d-163">toohide hello 核取方塊，設定此設定太**隱藏**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-163">toohide hello checkbox, configure this setting too**Hidden**.</span></span>

> [!NOTE]
> <span data-ttu-id="2e54d-164">SharePoint Online 和 Office 2010 的某些功能而定的使用者可以 toocheck 此方塊。</span><span class="sxs-lookup"><span data-stu-id="2e54d-164">Some features of SharePoint Online and Office 2010 depend on users being able toocheck this box.</span></span> <span data-ttu-id="2e54d-165">如果您設定此設定 toohidden，您的使用者可能會看到 toosign 中其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="2e54d-165">If you configure this setting toohidden, your users may see additional and unexpected prompts toosign-in.</span></span>
>
>

<span data-ttu-id="2e54d-166">您也可以將此頁面上的所有元素都翻成當地使用語。</span><span class="sxs-lookup"><span data-stu-id="2e54d-166">You can also localize all elements on this page.</span></span> <span data-ttu-id="2e54d-167">設定一組「預設」自訂元素之後，就可以設定不同地區設定的其他版本。</span><span class="sxs-lookup"><span data-stu-id="2e54d-167">Once you’ve configured a “default” set of customization elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="2e54d-168">您也可以混合使用並符合各種元素。</span><span class="sxs-lookup"><span data-stu-id="2e54d-168">You can also mix and match various elements.</span></span> <span data-ttu-id="2e54d-169">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="2e54d-169">For example, you can:</span></span>

* <span data-ttu-id="2e54d-170">建立適用於所有文化的「預設」大型圖例，然後建立英文和法文的特定版本。</span><span class="sxs-lookup"><span data-stu-id="2e54d-170">Create a “default” Large Illustration that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="2e54d-171">當您設定您的瀏覽器 tooone 的這兩種語言時，會出現 hello 特定映像，而 hello 預設圖例出現的所有其他語言。</span><span class="sxs-lookup"><span data-stu-id="2e54d-171">When you set your browsers tooone of these two languages, hello specific image appears, while hello default illustration appears for all other languages.</span></span>
* <span data-ttu-id="2e54d-172">為您的組織設定不同的標誌 (例如日文或希伯來文版本)。</span><span class="sxs-lookup"><span data-stu-id="2e54d-172">Configure different logos for your organization (e.g. Japanese or Hebrew versions).</span></span>

## <a name="access-panel-page-customization"></a><span data-ttu-id="2e54d-173">存取面板頁面自訂</span><span class="sxs-lookup"><span data-stu-id="2e54d-173">Access panel page customization</span></span>
<span data-ttu-id="2e54d-174">hello 存取面板 頁面是您已授與的快速存取 toohello 雲端應用程式存取 tooby 您的系統管理員基本上入口網站頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-174">hello Access Panel page is essentially a portal page for quick access toohello cloud apps you have been granted access tooby your administrator.</span></span> <span data-ttu-id="2e54d-175">在此頁面上，您的應用程式會顯示為可點選的應用程式圖格。</span><span class="sxs-lookup"><span data-stu-id="2e54d-175">On this page, your apps appear as clickable application tiles.</span></span>

<span data-ttu-id="2e54d-176">下列螢幕擷取畫面的 hello 自訂後，顯示存取面板頁面的範例。</span><span class="sxs-lookup"><span data-stu-id="2e54d-176">hello following screenshot shows an example of an access panel page after customization.</span></span>

![][8]

## <a name="configure-your-directory-with-company-branding"></a><span data-ttu-id="2e54d-177">使用公司商標來設定目錄</span><span class="sxs-lookup"><span data-stu-id="2e54d-177">Configure your directory with company branding</span></span>
<span data-ttu-id="2e54d-178">您可以在 hello Azure 傳統入口網站中設定一個預設集的每個目錄的自訂項目。</span><span class="sxs-lookup"><span data-stu-id="2e54d-178">You can configure one default set of customizable elements per directory in hello Azure classic portal.</span></span> <span data-ttu-id="2e54d-179">已儲存 hello 預設值之後，系統管理員可以新增每個項目，針對不同語言的當地語系化的版本 / 地區設定。</span><span class="sxs-lookup"><span data-stu-id="2e54d-179">After hello defaults have been saved, an administrator can add localized versions of each element, for different languages / locales.</span></span> <span data-ttu-id="2e54d-180">所有可自訂元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2e54d-180">All customizable elements are optional.</span></span>

<span data-ttu-id="2e54d-181">例如，如果您設定預設 橫幅標誌，但沒有大型圖例，hello 登入頁面會顯示您的標誌 hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="2e54d-181">For example, if you configure a default Banner Logo but no Large Illustration, hello sign-in page displays your logo in hello upper-right corner.</span></span> <span data-ttu-id="2e54d-182">不過，系統會顯示 hello hello 站台的預設圖例。</span><span class="sxs-lookup"><span data-stu-id="2e54d-182">However hello default illustration of hello site is displayed.</span></span>

<span data-ttu-id="2e54d-183">假設有下列組態的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e54d-183">Imagine hello following configuration:</span></span>

* <span data-ttu-id="2e54d-184">預設的橫幅標誌和英文登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-184">A default Banner Logo and Sign-In Page Text in English</span></span>
* <span data-ttu-id="2e54d-185">語言特定的德文登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-185">A language-specific sign in Page Text for German</span></span>

<span data-ttu-id="2e54d-186">如果您的語言喜好設定為德文，您會取得 hello 預設橫幅標誌 但 hello 德文的文字。</span><span class="sxs-lookup"><span data-stu-id="2e54d-186">If your language preference is German, you get hello default Banner Logo but hello German text.</span></span>

<span data-ttu-id="2e54d-187">雖然技術上來說，您可以設定一組不同的 Azure AD 支援每種語言，我們建議您保留 hello 多變化低、 維護和效能考量。</span><span class="sxs-lookup"><span data-stu-id="2e54d-187">While you could technically configure a different set for each language supported by Azure AD, we recommend that you keep hello number of variations low, for maintenance and performance reasons.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e54d-188">Yammer 並不會顯示 hello 使用者登入之後，Azure AD 品牌登入頁面之前的 hello。</span><span class="sxs-lookup"><span data-stu-id="2e54d-188">Yammer does not show hello Azure AD branded sign-in page until after hello user signs in.</span></span> <span data-ttu-id="2e54d-189">hello 使用者會看到第一次，hello 泛用 Office 365 登入頁面和 hello 然後品牌頁面之後。</span><span class="sxs-lookup"><span data-stu-id="2e54d-189">hello user sees hello generic Office 365 sign-in page first, and then hello branded page after that.</span></span>   
 
 
<span data-ttu-id="2e54d-190">**tooadd 公司商標 tooyour 目錄中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2e54d-190">**tooadd company branding tooyour directory, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e54d-191">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="2e54d-191">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator of hello directory you want toocustomize.</span></span>
2. <span data-ttu-id="2e54d-192">選取您想要 toocustomize hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2e54d-192">Select hello directory you want toocustomize.</span></span>
3. <span data-ttu-id="2e54d-193">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-193">In hello toolbar on hello top, click **Configure**.</span></span>
4. <span data-ttu-id="2e54d-194">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-194">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="2e54d-195">修改您想 toocustomize 的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="2e54d-195">Modify hello elements you want toocustomize.</span></span> <span data-ttu-id="2e54d-196">所有欄位都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2e54d-196">All fields are optional.</span></span>
6. <span data-ttu-id="2e54d-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-197">Click **Save**.</span></span>

<span data-ttu-id="2e54d-198">它最多可能需要新的變更 tooan 小時您製作 toohello 登入頁面，商標 tooappear。</span><span class="sxs-lookup"><span data-stu-id="2e54d-198">It can take up tooan hour for new change you made toohello sign-in page branding tooappear.</span></span>

<span data-ttu-id="2e54d-199">**tooadd 特定語言的公司品牌，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2e54d-199">**tooadd language-specific company branding, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e54d-200">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="2e54d-200">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator of hello directory you want toocustomize.</span></span>
2. <span data-ttu-id="2e54d-201">選取您想要 toocustomize hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2e54d-201">Select hello directory you want toocustomize.</span></span>
<span data-ttu-id="2e54d-202">fs3。</span><span class="sxs-lookup"><span data-stu-id="2e54d-202">fs3.</span></span> <span data-ttu-id="2e54d-203">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-203">In hello toolbar on hello top, click **Configure**.</span></span>
4. <span data-ttu-id="2e54d-204">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-204">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="2e54d-205">按一下 [新增特定語言的商標] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-205">Click **Add branding for a specific language**.</span></span>
6. <span data-ttu-id="2e54d-206">選取您想 toocustomize hello 標誌，然後再按一下 hello 語言**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-206">Select hello language you want toocustomize hello logo for, and then click **Next**.</span></span>
7. <span data-ttu-id="2e54d-207">編輯您要為其 tooconfigure 特定語言覆寫只 hello 元素。</span><span class="sxs-lookup"><span data-stu-id="2e54d-207">Edit only hello elements for which you want tooconfigure language-specific overrides.</span></span> <span data-ttu-id="2e54d-208">所有欄位都是選用的。</span><span class="sxs-lookup"><span data-stu-id="2e54d-208">All fields are optional.</span></span> <span data-ttu-id="2e54d-209">如果欄位保留空白，然後 hello 自訂的預設值改為顯示 （或 hello Microsoft 預設值，如果未設定自訂的預設值）。</span><span class="sxs-lookup"><span data-stu-id="2e54d-209">If a field is left blank, then hello custom default value is displayed instead (or hello Microsoft default if a custom default is not configured).</span></span>
8. <span data-ttu-id="2e54d-210">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-210">Click **Save**.</span></span>

<span data-ttu-id="2e54d-211">**tooremove 公司品牌從您的目錄中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2e54d-211">**tooremove company branding from your directory, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e54d-212">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)想 toocustomize hello 目錄的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="2e54d-212">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an administrator of hello directory you want toocustomize.</span></span>
2. <span data-ttu-id="2e54d-213">選取您想要 toocustomize hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2e54d-213">Select hello directory you want toocustomize.</span></span>
3. <span data-ttu-id="2e54d-214">在 hello hello 上方的工具列中按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="2e54d-214">In hello toolbar on hello top, click **Configure**.</span></span>
4. <span data-ttu-id="2e54d-215">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-215">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="2e54d-216">在 hello 自訂品牌 頁面上，選取 **編輯現有品牌設定**並前往 toohello 下一個頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-216">On hello Customize Branding page, select **Edit Existing Branding Settings** and then go toohello next page.</span></span>
6. <span data-ttu-id="2e54d-217">根據哪一個項目要 tooremove，執行下列一或多個 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="2e54d-217">Depending on which elements you want tooremove, do one or more of hello following:</span></span>

    <span data-ttu-id="2e54d-218">a.</span><span class="sxs-lookup"><span data-stu-id="2e54d-218">a.</span></span> <span data-ttu-id="2e54d-219">在 [橫幅標誌] 之下，選取 [移除上傳的標誌]。</span><span class="sxs-lookup"><span data-stu-id="2e54d-219">Under **Banner Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="2e54d-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="2e54d-220">b.</span></span> <span data-ttu-id="2e54d-221">在 [圖格標誌] 之下，選取 [移除上傳的標誌]。</span><span class="sxs-lookup"><span data-stu-id="2e54d-221">Under **Tile Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="2e54d-222">c.</span><span class="sxs-lookup"><span data-stu-id="2e54d-222">c.</span></span> <span data-ttu-id="2e54d-223">移除所有的文字方塊中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="2e54d-223">Remove hello text from all textboxes.</span></span>

    <span data-ttu-id="2e54d-224">d.</span><span class="sxs-lookup"><span data-stu-id="2e54d-224">d.</span></span> <span data-ttu-id="2e54d-225">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="2e54d-225">Click **Next**.</span></span>

    <span data-ttu-id="2e54d-226">e.</span><span class="sxs-lookup"><span data-stu-id="2e54d-226">e.</span></span> <span data-ttu-id="2e54d-227">移除所有的文字方塊中的 hello 文字。</span><span class="sxs-lookup"><span data-stu-id="2e54d-227">Remove hello text from all textboxes.</span></span>
7. <span data-ttu-id="2e54d-228">按一下**儲存**tooremove hello 項目。</span><span class="sxs-lookup"><span data-stu-id="2e54d-228">Click **Save** tooremove hello elements.</span></span>
8. <span data-ttu-id="2e54d-229">如果有必要，請按一下**自訂品牌**再次並移除所有特定語言品牌需要 toobe 重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2e54d-229">If necessary, click **Customize Branding** again and repeat these steps for all language-specific branding that needs toobe removed.</span></span>
    <span data-ttu-id="2e54d-230">當您按一下 已移除所有的品牌設定**自訂品牌**並查看 hello**自訂預設品牌**表單沒有現有的設定。</span><span class="sxs-lookup"><span data-stu-id="2e54d-230">All branding settings have been removed when you click **Customize Branding** and see hello **Customize Default Branding** form with no existing settings configured.</span></span>

## <a name="testing-and-examples"></a><span data-ttu-id="2e54d-231">測試和範例</span><span class="sxs-lookup"><span data-stu-id="2e54d-231">Testing and examples</span></span>
<span data-ttu-id="2e54d-232">建議您先使用測試租用戶進行試驗，再於生產環境中進行變更。</span><span class="sxs-lookup"><span data-stu-id="2e54d-232">We recommend that you experiment with a test tenant before making changes in your production environment.</span></span>

<span data-ttu-id="2e54d-233">**tooverify 是否您的品牌已套用：**</span><span class="sxs-lookup"><span data-stu-id="2e54d-233">**tooverify whether your branding has been applied:**</span></span>

1. <span data-ttu-id="2e54d-234">開啟 InPrivate 或 Incognito 瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="2e54d-234">Open an InPrivate or Incognito browser session.</span></span>
2. <span data-ttu-id="2e54d-235">請瀏覽 https://outlook.com/contoso.com，以您自訂的 hello 網域取代 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="2e54d-235">Visit https://outlook.com/contoso.com, replacing contoso.com with hello domain you’ve customized.</span></span>

<span data-ttu-id="2e54d-236">這也適用於類似 contoso.onmicrosoft.com 的網域。</span><span class="sxs-lookup"><span data-stu-id="2e54d-236">This also works with domains that look like contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="2e54d-237">toohelp 建立有效的自訂集，我們已自訂下列兩個虛構登入頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="2e54d-237">toohelp you create effective customization sets, we have customized hello following two fictitious sign-in pages:</span></span>

* [<span data-ttu-id="2e54d-238">http://aka.ms/aaddemo001</span><span class="sxs-lookup"><span data-stu-id="2e54d-238">http://aka.ms/aaddemo001</span></span>](http://aka.ms/aaddemo001)
* [<span data-ttu-id="2e54d-239">http://aka.ms/aaddemo002</span><span class="sxs-lookup"><span data-stu-id="2e54d-239">http://aka.ms/aaddemo002</span></span>](http://aka.ms/aaddemo002)

<span data-ttu-id="2e54d-240">tootest hello 語言專屬的設定，您會需要 toomodify hello 預設語言喜好設定設定您的自訂您的 web 瀏覽器 tooa 語言。</span><span class="sxs-lookup"><span data-stu-id="2e54d-240">tootest hello language-specific settings, you need toomodify hello default language preferences in your web browser tooa language you have set in your customization.</span></span> <span data-ttu-id="2e54d-241">在 Internet Explorer 中，您會設定這在 hello**網際網路選項**功能表。</span><span class="sxs-lookup"><span data-stu-id="2e54d-241">In Internet Explorer, you configure this in hello **Internet Options** menu.</span></span>

## <a name="customizable-elements"></a><span data-ttu-id="2e54d-242">可自訂元素</span><span class="sxs-lookup"><span data-stu-id="2e54d-242">Customizable elements</span></span>
<span data-ttu-id="2e54d-243">Azure AD 中的部分可自訂元素有多個使用案例。</span><span class="sxs-lookup"><span data-stu-id="2e54d-243">Some customizable elements in Azure AD have multiple use cases.</span></span> <span data-ttu-id="2e54d-244">您可以設定目錄每一次公司標誌，並且適用於兩者，hello 登入和存取面板 頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-244">You can configure company logos once per directory and is used on both, hello sign-in and Access Panel pages.</span></span> <span data-ttu-id="2e54d-245">有些可自訂的元素是特定唯一 toohello 登入頁面。</span><span class="sxs-lookup"><span data-stu-id="2e54d-245">Some customizable elements are specific only toohello sign-in page.</span></span> <span data-ttu-id="2e54d-246">hello 下表提供詳細資料 hello 可自訂的不同元素。</span><span class="sxs-lookup"><span data-stu-id="2e54d-246">hello following table provides details for hello different customizable elements.</span></span>

| <span data-ttu-id="2e54d-247">名稱</span><span class="sxs-lookup"><span data-stu-id="2e54d-247">Name</span></span> | <span data-ttu-id="2e54d-248">說明</span><span class="sxs-lookup"><span data-stu-id="2e54d-248">Description</span></span> | <span data-ttu-id="2e54d-249">條件約束</span><span class="sxs-lookup"><span data-stu-id="2e54d-249">Constraints</span></span> | <span data-ttu-id="2e54d-250">建議</span><span class="sxs-lookup"><span data-stu-id="2e54d-250">Recommendations</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2e54d-251">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="2e54d-251">Banner Logo</span></span> |<span data-ttu-id="2e54d-252">hello 橫幅標誌會顯示 hello 登入頁面和 hello 存取面板上。</span><span class="sxs-lookup"><span data-stu-id="2e54d-252">hello Banner Logo is displayed on hello sign-in page and hello Access panel.</span></span> |<p><span data-ttu-id="2e54d-253">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="2e54d-253">JPG or PNG</span></span></p><p><span data-ttu-id="2e54d-254">60x280 像素</span><span class="sxs-lookup"><span data-stu-id="2e54d-254">60x280 pixels</span></span></p><p><span data-ttu-id="2e54d-255">10 KB</span><span class="sxs-lookup"><span data-stu-id="2e54d-255">10 KB</span></span></p> |<p><span data-ttu-id="2e54d-256">使用您組織的完整標誌 (包含形符和商標)</span><span class="sxs-lookup"><span data-stu-id="2e54d-256">Use your organization’s full logo (including pictogram and logotype)</span></span></p><p><span data-ttu-id="2e54d-257">將它保留在 30 像素高 tooavoid 引入行動裝置上的捲軸</span><span class="sxs-lookup"><span data-stu-id="2e54d-257">Keep it under 30 pixels high tooavoid introducing scrollbars on mobile devices</span></span></p><p><span data-ttu-id="2e54d-258">保持低於 4 KB</span><span class="sxs-lookup"><span data-stu-id="2e54d-258">Keep it under 4 KB</span></span></p><p><span data-ttu-id="2e54d-259">使用透明 PNG （不要認為該 hello 登入頁面一律擁有白色背景）</span><span class="sxs-lookup"><span data-stu-id="2e54d-259">Use a transparent PNG (don’t assume that hello sign-in page always has a white background)</span></span></p> |
| <span data-ttu-id="2e54d-260">磚標誌</span><span class="sxs-lookup"><span data-stu-id="2e54d-260">Tile Logo</span></span> |<span data-ttu-id="2e54d-261">（目前未用於 hello 登入頁面）在未來的 hello，此文字可能會使用的 tooreplace hello 泛用 「 公司或學校帳戶 」 形符 hello 體驗的不同位置中。</span><span class="sxs-lookup"><span data-stu-id="2e54d-261">(currently not used in hello sign-in page) In hello future, this text may be used tooreplace hello generic “work or school account” pictogram in different places of hello experience.</span></span> |<p><span data-ttu-id="2e54d-262">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="2e54d-262">JPG or PNG</span></span></p><p><span data-ttu-id="2e54d-263">120x120 像素</span><span class="sxs-lookup"><span data-stu-id="2e54d-263">120x120 pixels</span></span></p><p><span data-ttu-id="2e54d-264">10 KB</span><span class="sxs-lookup"><span data-stu-id="2e54d-264">10 KB</span></span></p> |<p><span data-ttu-id="2e54d-265">使其保持簡單 （沒有小型文字），因為此映像可能會調整大小的 too50%</span><span class="sxs-lookup"><span data-stu-id="2e54d-265">Keep it simple (no small text), as this image may be resized too50%</span></span> |
| </p> | | | |
| <span data-ttu-id="2e54d-266">登入頁面使用者名稱標籤</span><span class="sxs-lookup"><span data-stu-id="2e54d-266">Sign-in Page User Name Label</span></span> |<span data-ttu-id="2e54d-267">（目前未用於 hello 登入頁面）在未來的 hello，此文字可能會使用的 tooreplace hello hello 體驗的不同位置中的泛用 「 公司或學校帳戶 」 字串。</span><span class="sxs-lookup"><span data-stu-id="2e54d-267">(currently not used in hello sign-in page) In hello future, this text may be used tooreplace hello generic “work or school account” string in different places of hello experience.</span></span> <span data-ttu-id="2e54d-268">您可以將它設定 toosomething，例如"Contoso account"或"Contoso id。 」</span><span class="sxs-lookup"><span data-stu-id="2e54d-268">You can set it toosomething like “Contoso account” or “Contoso ID.”</span></span> |<p><span data-ttu-id="2e54d-269">向上 too50 字元的 Unicode 文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-269">Unicode text, up too50 characters</span></span></p><p><span data-ttu-id="2e54d-270">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="2e54d-270">Plain text only (no links or HTML tags)</span></span></p> |<p><span data-ttu-id="2e54d-271">保持簡短和簡單</span><span class="sxs-lookup"><span data-stu-id="2e54d-271">Keep it short and simple</span></span></p><p><span data-ttu-id="2e54d-272">詢問使用者如何它們通常是指 toohello 工作或學校帳戶您提供的。</span><span class="sxs-lookup"><span data-stu-id="2e54d-272">Ask your users how they usually refer toohello work or school account you provide them with.</span></span></p> |
| <span data-ttu-id="2e54d-273">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-273">Sign-in Page Text</span></span> |<span data-ttu-id="2e54d-274">此 「 重複使用 」 文字 hello 登入頁面表單下方會出現，並使用的 toocommunicate 其他指示，或可在 tooget 說明及支援。</span><span class="sxs-lookup"><span data-stu-id="2e54d-274">This “boilerplate” text appears below hello sign-in page form and can be used toocommunicate additional instructions, or where tooget help and support.</span></span> |<p><span data-ttu-id="2e54d-275">向上 too256 字元的 Unicode 文字</span><span class="sxs-lookup"><span data-stu-id="2e54d-275">Unicode text, up too256 characters</span></span></p><p><span data-ttu-id="2e54d-276">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="2e54d-276">Plain text only (no links or HTML tags)</span></span></p> |<span data-ttu-id="2e54d-277">保持低於 250 個字元 (約 3 行文字)</span><span class="sxs-lookup"><span data-stu-id="2e54d-277">Keep it under 250 characters (approximately 3 lines of text)</span></span> |
| <span data-ttu-id="2e54d-278">登入頁面圖例</span><span class="sxs-lookup"><span data-stu-id="2e54d-278">Sign-in Page Illustration</span></span> |<span data-ttu-id="2e54d-279">hello 圖是顯示在 hello 登入頁面 toohello hello 登入頁面表單左邊的大型映像。</span><span class="sxs-lookup"><span data-stu-id="2e54d-279">hello illustration is a large image that is displayed on hello sign-in page toohello left of hello sign-in page form.</span></span> |<p><span data-ttu-id="2e54d-280">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="2e54d-280">JPG or PNG</span></span></p><p><span data-ttu-id="2e54d-281">1420x1200</span><span class="sxs-lookup"><span data-stu-id="2e54d-281">1420x1200</span></span></p><p><span data-ttu-id="2e54d-282">500 KB</span><span class="sxs-lookup"><span data-stu-id="2e54d-282">500 KB</span></span></p> |<p><span data-ttu-id="2e54d-283">1420x1200 像素</span><span class="sxs-lookup"><span data-stu-id="2e54d-283">1420x1200 pixels</span></span></p><p><span data-ttu-id="2e54d-284">重要事項：保持越小越好，最好低於 200 KB。</span><span class="sxs-lookup"><span data-stu-id="2e54d-284">Important: Keep it as small as possible, ideally under 200 KB.</span></span> <span data-ttu-id="2e54d-285">Hello 映像不快取時，如果此影像太大，會影響 hello 效能的 hello 登入頁面</span><span class="sxs-lookup"><span data-stu-id="2e54d-285">If this image is too large, hello performance of hello Sign-in page is impacted when hello image isn’t cached</span></span></p><p><span data-ttu-id="2e54d-286">這是通常裁剪影像，tooaccommodate 不同外觀比例。</span><span class="sxs-lookup"><span data-stu-id="2e54d-286">This image is often cropped, tooaccommodate different screen ratios.</span></span> <span data-ttu-id="2e54d-287">Hello 主要視覺元素保持 hello 左上角 （右上方對 RTL 語言），因為從 hello 右下角，hello 瀏覽器視窗縮小至 hello 上 / 左邊，調整大小時發生。</span><span class="sxs-lookup"><span data-stu-id="2e54d-287">Keep hello primary visual elements in hello top left corner (top right for RTL languages), because resizing occurs from hello bottom/right corner, going towards hello top / left, as hello browser window shrinks.</span></span></p> |
| <span data-ttu-id="2e54d-288">登入頁面背景色彩</span><span class="sxs-lookup"><span data-stu-id="2e54d-288">Sign-in Page Background Color</span></span> |<span data-ttu-id="2e54d-289">在 hello 區域 toohello hello 登入頁面表單左邊用於 hello 登入頁面背景色彩。</span><span class="sxs-lookup"><span data-stu-id="2e54d-289">hello sign-in page background color is used in hello area toohello left of hello sign-in page form.</span></span> |<span data-ttu-id="2e54d-290">必須是十六進位格式的 RGB 色彩 (範例: #FFFFFF)</span><span class="sxs-lookup"><span data-stu-id="2e54d-290">Must be an RGB color in hexadecimal form (example: #FFFFFF)</span></span> |<p><span data-ttu-id="2e54d-291">hello 背景色彩可能會顯示以 hello 取代在低頻寬連接上的大型圖例</span><span class="sxs-lookup"><span data-stu-id="2e54d-291">hello background color may be shown in place of hello large Illustration on low-bandwidth connections</span></span></p><p><span data-ttu-id="2e54d-292">我們建議挑選橫幅標誌 hello hello 主要色彩</span><span class="sxs-lookup"><span data-stu-id="2e54d-292">We suggest picking hello primary color of hello Banner Logo</span></span></p> |

## <a name="next-steps"></a><span data-ttu-id="2e54d-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2e54d-293">Next steps</span></span>
* [<span data-ttu-id="2e54d-294">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="2e54d-294">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="2e54d-295">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="2e54d-295">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)

<!--Image references-->
[1]: ./media/active-directory-add-company-branding/SignInPage_beforecustomization.png
[2]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization.png
[3]: ./media/active-directory-add-company-branding/SignInPage_mobile_beforecustomization.png
[4]: ./media/active-directory-add-company-branding/SignInPage_mobile_aftercustomization.png
[5]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_elements.png
[6]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedleft.png
[7]: ./media/active-directory-add-company-branding/SignInPage_aftercustomization_croppedtop.png
[8]: ./media/active-directory-add-company-branding/APBranding.png
[9]: ./media/active-directory-add-company-branding/hidekmsi.png
