---
title: "在登入和存取面板頁面加上公司商標"
description: "了解如何將公司商標新增至 Azure 登入頁面和存取面板頁面"
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
ms.openlocfilehash: c558bd5f2b7fae91483cc2c6724c40442bb65045
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="add-company-branding-to-your-sign-in-and-access-panel-pages"></a><span data-ttu-id="6c764-103">在登入和存取面板頁面加上公司商標</span><span class="sxs-lookup"><span data-stu-id="6c764-103">Add company branding to your sign-in and Access Panel pages</span></span>
<span data-ttu-id="6c764-104">為了避免混淆，許多公司都想對其管理的所有網站和服務套用一致的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="6c764-104">To avoid confusion, many companies want to apply a consistent look and feel across all the websites and services they manage.</span></span> <span data-ttu-id="6c764-105">Azure Active Directory 提供這項功能，讓您利用公司標誌和自訂色彩配置來自訂下列網頁的外觀：</span><span class="sxs-lookup"><span data-stu-id="6c764-105">Azure Active Directory provides this capability by allowing you to customize the appearance of the following web pages with your company logo and custom color schemes:</span></span>

* <span data-ttu-id="6c764-106">**登入頁面** - 當您登入 Office 365 或其他使用 Azure AD 作為識別提供者的 Web 型應用程式時，便會出現此頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-106">**Sign-in page** - This is the page that appears when you sign in to Office 365 or other web-based applications that are using Azure AD as your identity provider.</span></span> <span data-ttu-id="6c764-107">在進行主領域探索期間或要輸入認證時，您就會與此頁面互動。</span><span class="sxs-lookup"><span data-stu-id="6c764-107">You interact with this page either during a Home Realm Discovery or to enter your credentials.</span></span> <span data-ttu-id="6c764-108">主領域探索可讓系統將同盟使用者重新導向至其內部部署 STS (例如 AD FS)。</span><span class="sxs-lookup"><span data-stu-id="6c764-108">The Home Realm Discovery allows the system to redirect federated users to their on-premises STS (such as AD FS).</span></span>
* <span data-ttu-id="6c764-109">**存取面板頁面** - 存取面板是網頁型入口網站，可讓您檢視並啟動 Azure AD 系統管理員已授與您存取權的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c764-109">**Access Panel page** - The Access Panel is a web-based portal that allows you to view and launch the cloud-based applications your Azure AD administrator has granted you access to.</span></span> <span data-ttu-id="6c764-110">若要存取「存取面板」，請使用下列 URL： [https://myapps.microsoft.com](https://myapps.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="6c764-110">To access the Access Panel, use the following URL: [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

<span data-ttu-id="6c764-111">本主題說明如何自訂登入頁面和存取面板頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-111">This topic explains how you can customize the sign-in page and the access panel page.</span></span>

> [!NOTE]
> * <span data-ttu-id="6c764-112">公司商標是您升級至 Premium 或 Basic 版本的 Azure Active Directory 後，或是 Office 365 使用者時才能使用的功能。</span><span class="sxs-lookup"><span data-stu-id="6c764-112">Company branding is a feature that is available only if you upgraded to the Premium or Basic edition of Azure Active Directory, or are an Office 365 user.</span></span> <span data-ttu-id="6c764-113">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="6c764-113">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>
> * <span data-ttu-id="6c764-114">Azure Active Directory Premium 和 Basic 版本適用於使用全球 Azure Active Directory 執行個體的中國客戶。</span><span class="sxs-lookup"><span data-stu-id="6c764-114">Azure Active Directory Premium and Basic editions are available for customers in China using the worldwide instance of Azure Active Directory.</span></span> <span data-ttu-id="6c764-115">由 21Vianet 在中國提供的 Microsoft Azure 服務目前不支援 Azure Active Directory Premium 和 Basic 版本。</span><span class="sxs-lookup"><span data-stu-id="6c764-115">Azure Active Directory Premium and Basic editions are not currently supported in the Microsoft Azure service operated by 21Vianet in China.</span></span> <span data-ttu-id="6c764-116">如需詳細資訊，請透過 [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="6c764-116">For more information, contact us at the [Azure Active Directory Forum](https://feedback.azure.com/forums/169401-azure-active-directory/).</span></span>
>
>

## <a name="customizing-the-sign-in-page"></a><span data-ttu-id="6c764-117">自訂登入頁面</span><span class="sxs-lookup"><span data-stu-id="6c764-117">Customizing the sign-in page</span></span>
<span data-ttu-id="6c764-118">一般而言，如果您需要透過瀏覽器存取貴組織訂閱的雲端應用程式和服務，您可使用登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-118">Typically, if you need browser-based access to your cloud apps and services that your organization subscribes to, you use the sign-in page.</span></span>

<span data-ttu-id="6c764-119">如果您已對登入頁面套用變更，最多需要一小時變更才會出現。</span><span class="sxs-lookup"><span data-stu-id="6c764-119">If you have applied changes to your sign-in page, it can take up to an hour for the changes to appear.</span></span>

<span data-ttu-id="6c764-120">只有當您使用租用戶特定 URL (例如 https://outlook.com/**contoso**.com 或 https://mail.**contoso**.com) 來造訪服務時，才會顯示加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-120">A branded sign-in page only appears when you visit a service with a tenant-specific URL such as https://outlook.com/**contoso**.com, or https://mail.**contoso**.com.</span></span>

<span data-ttu-id="6c764-121">當您造訪具有非租用戶特定 URL (例如 https://mail.office365.com) 的服務，就會看到未加上商標的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-121">When you visit a service with non-tenant specific URLs (e.g.: https://mail.office365.com), a non-branded sign-in page appears.</span></span> <span data-ttu-id="6c764-122">在此情況下，只要您一輸入使用者識別碼或是選取使用者磚，就會顯示您的商標。</span><span class="sxs-lookup"><span data-stu-id="6c764-122">in this case, your branding appears once you have entered your user ID or you have selected a user tile.</span></span>

> [!NOTE]
> * <span data-ttu-id="6c764-123">在已設定商標之 Azure 傳統入口網站的 [Active Directory]  >  [目錄]  >  [網域] 區段中，您的網域名稱必須為 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="6c764-123">Your domain name must appear as “Active” in the **Active Directory** > **Directory** > **Domains** section of the Azure classic portal where you have configured branding.</span></span>
> * <span data-ttu-id="6c764-124">登入頁面商標不會延續到 Microsoft 的消費者登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-124">Sign-in page branding doesn’t carry over to the consumer sign in page of Microsoft.</span></span> <span data-ttu-id="6c764-125">如果您使用個人 Microsoft 帳戶進行登入，可能會看到 Azure AD 所呈現並加上商標的使用者圖格清單，但是您組織的商標不會套用到 Microsoft 帳戶登入頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-125">If you sign in with a personal Microsoft account, you may see a branded list of user tiles rendered by Azure AD, but the branding of your organization does not apply to the Microsoft account sign-in page.</span></span>
>
>

<span data-ttu-id="6c764-126">如果您想要在此頁面上顯示您的公司商標、色彩和其他可自訂的元素，請參閱下列影像以了解這兩種做法的差異。</span><span class="sxs-lookup"><span data-stu-id="6c764-126">If you want to show your company brand, colors and other customizable elements on this page, see the following images to understand the difference between the two experiences.</span></span>

<span data-ttu-id="6c764-127">下列螢幕擷取畫面顯示桌上型電腦上 Office 365 登入頁面的自訂「前」  範例︰</span><span class="sxs-lookup"><span data-stu-id="6c764-127">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面][1]

<span data-ttu-id="6c764-129">下列螢幕擷取畫面顯示桌上型電腦上 Office 365 登入頁面的自訂「後」  範例︰</span><span class="sxs-lookup"><span data-stu-id="6c764-129">The following screenshot shows and example for the Office 365 sign-in page on a desktop computer **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面][2]

<span data-ttu-id="6c764-131">下列螢幕擷取畫面顯示自訂 **前** 在行動裝置上的 Office 365 登入頁面範例︰</span><span class="sxs-lookup"><span data-stu-id="6c764-131">The following screenshot shows an example of the Office 365 sign-in page on a mobile device **before** a customization:</span></span>

![自訂前的 Office 365 登入頁面][3]

<span data-ttu-id="6c764-133">下列螢幕擷取畫面顯示自訂 **後** 在行動裝置上的 Office 365 登入頁面範例︰</span><span class="sxs-lookup"><span data-stu-id="6c764-133">The following screenshot shows an example of the Office 365 sign-in page on a mobile device **after** a customization:</span></span>

![自訂後的 Office 365 登入頁面][4]

<span data-ttu-id="6c764-135">當您調整瀏覽器視窗大小時，大型圖例 (例如先前所示的圖例) 通常會裁剪成符合不同的螢幕外觀比例。</span><span class="sxs-lookup"><span data-stu-id="6c764-135">When you resize a browser window, the large Illustration, like the one shown previously, is often cropped to accommodate different screen aspect ratios.</span></span> <span data-ttu-id="6c764-136">請記住，您應該嘗試保持圖例中的主要視覺元素，讓它們永遠顯示在左上角 (從右至左的語言，則顯示在右上角)。</span><span class="sxs-lookup"><span data-stu-id="6c764-136">With this in mind, you should try to keep the key visual elements in the illustration so that they always appear in the top-left corner (top-right for right-to-left languages).</span></span> <span data-ttu-id="6c764-137">這十分重要，因為調整大小通常會從右下角往上/往左，或從下方往上方。</span><span class="sxs-lookup"><span data-stu-id="6c764-137">This is important because resizing typically occurs from the bottom-right corner going towards the top / left or from the bottom towards the top.</span></span>

<span data-ttu-id="6c764-138">下圖顯示將瀏覽器調整到左方時如何裁剪圖例：</span><span class="sxs-lookup"><span data-stu-id="6c764-138">The following picture shows how the illustration is cropped when the browser is resized to the left:</span></span>

![][6]

<span data-ttu-id="6c764-139">以下是將瀏覽器調整到上方之後，如何顯示圖例：</span><span class="sxs-lookup"><span data-stu-id="6c764-139">Here is how it appears after the browser is resized toward the top:</span></span>

![][7]

## <a name="what-elements-on-the-page-can-i-customize"></a><span data-ttu-id="6c764-140">我們可以自訂頁面上的哪些元素？</span><span class="sxs-lookup"><span data-stu-id="6c764-140">What elements on the page can I customize?</span></span>
<span data-ttu-id="6c764-141">您可以自訂登入頁面上的下列元素：</span><span class="sxs-lookup"><span data-stu-id="6c764-141">You can customize the following elements on the sign-in page:</span></span>

![][5]

| <span data-ttu-id="6c764-142">頁面元素</span><span class="sxs-lookup"><span data-stu-id="6c764-142">Page element</span></span> | <span data-ttu-id="6c764-143">頁面上的位置</span><span class="sxs-lookup"><span data-stu-id="6c764-143">Location on the page</span></span> |
|:--- | --- |
| <span data-ttu-id="6c764-144">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="6c764-144">Banner Logo</span></span> |<span data-ttu-id="6c764-145">顯示於頁面的右上方。</span><span class="sxs-lookup"><span data-stu-id="6c764-145">Shown at the top-right of the page.</span></span> <span data-ttu-id="6c764-146">取代您所登入之目的地網站要顯示的標誌 (例如 </span><span class="sxs-lookup"><span data-stu-id="6c764-146">Replaces the logo the destination site you are signing in to displays (For example.</span></span> <span data-ttu-id="6c764-147">Office 365 或 Azure)。</span><span class="sxs-lookup"><span data-stu-id="6c764-147">Office 365 or Azure).</span></span> |
| <span data-ttu-id="6c764-148">大型圖例/背景色彩</span><span class="sxs-lookup"><span data-stu-id="6c764-148">Large Illustration / Background Color</span></span> |<span data-ttu-id="6c764-149">顯示於頁面的左方。</span><span class="sxs-lookup"><span data-stu-id="6c764-149">Shown at the left of the page.</span></span> <span data-ttu-id="6c764-150">取代您所登入之目的地網站要顯示的影像。</span><span class="sxs-lookup"><span data-stu-id="6c764-150">Replaces the image the destination site you are signing in to displays.</span></span> <span data-ttu-id="6c764-151">可能會顯示「背景色彩」，來替代低頻寬連線或窄畫面上的「大型圖例」。</span><span class="sxs-lookup"><span data-stu-id="6c764-151">The Background Color may be shown in place of the Large Illustration on low bandwidth connections, or on narrow screens.</span></span> |
| <span data-ttu-id="6c764-152">讓我保持登入</span><span class="sxs-lookup"><span data-stu-id="6c764-152">Keep me signed-in</span></span> |<span data-ttu-id="6c764-153">顯示在 [密碼] 文字方塊之下。</span><span class="sxs-lookup"><span data-stu-id="6c764-153">Shown under the Password textbox.</span></span> |
| <span data-ttu-id="6c764-154">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="6c764-154">Sign-in Page Text</span></span> |<span data-ttu-id="6c764-155">在使用工作或學校帳戶登入之前需要傳達有用資訊時，會顯示於頁尾上方。</span><span class="sxs-lookup"><span data-stu-id="6c764-155">Shown above the page footer when you need to convey helpful information before a sign-in with a work or school account.</span></span> <span data-ttu-id="6c764-156">例如，您可能想要包括支援人員的電話號碼或法律聲明。</span><span class="sxs-lookup"><span data-stu-id="6c764-156">For example, you may want to include the phone number to your help desk, or a legal statement.</span></span> |

> [!NOTE]
> <span data-ttu-id="6c764-157">所有元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="6c764-157">All elements are optional.</span></span> <span data-ttu-id="6c764-158">例如，如果您指定 [橫幅標誌]，但未指定 [大型圖例]，則登入頁面會顯示您的標誌以及目的地網站的圖例 (即 Office 365 加州高速公路影像)。</span><span class="sxs-lookup"><span data-stu-id="6c764-158">For example, if you specify a Banner Logo but no Large Illustration, the sign-in page shows your logo and the illustration for the destination site (that is, the Office 365 California highway image).</span></span>
>
>

<span data-ttu-id="6c764-159">登入頁面上的 [讓我保持登入] 核取方塊，可讓使用者在關閉並重新開啟其瀏覽器時保持登入狀態。</span><span class="sxs-lookup"><span data-stu-id="6c764-159">On your sign-in page, the **Keep me signed in** checkbox allows a user to remain signed in when they close and re-open their browser.</span></span> <span data-ttu-id="6c764-160">它不會影響工作階段存留期。</span><span class="sxs-lookup"><span data-stu-id="6c764-160">It does not effect session lifetime.</span></span> <span data-ttu-id="6c764-161">您可以在 Azure Active Directory 登入頁面上隱藏此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="6c764-161">You can hide the checkbox on the Azure Active Directory sign-in page.</span></span>

<span data-ttu-id="6c764-162">核取方塊顯示與否取決於 [隱藏 KMSI] 的設定。</span><span class="sxs-lookup"><span data-stu-id="6c764-162">Whether the checkbox is displayed depends on the setting of **Hide KMSI**.</span></span>

![][9]

<span data-ttu-id="6c764-163">若要隱藏此核取方塊，請將此設定設為 [隱藏]。</span><span class="sxs-lookup"><span data-stu-id="6c764-163">To hide the checkbox, configure this setting to **Hidden**.</span></span>

> [!NOTE]
> <span data-ttu-id="6c764-164">SharePoint Online 和 Office 2010 的某些功能取決於能夠核取此方塊的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c764-164">Some features of SharePoint Online and Office 2010 depend on users being able to check this box.</span></span> <span data-ttu-id="6c764-165">如果您將此設定設為隱藏，使用者可能會在登入時看見其他和非預期的提示。</span><span class="sxs-lookup"><span data-stu-id="6c764-165">If you configure this setting to hidden, your users may see additional and unexpected prompts to sign-in.</span></span>
>
>

<span data-ttu-id="6c764-166">您也可以將此頁面上的所有元素都翻成當地使用語。</span><span class="sxs-lookup"><span data-stu-id="6c764-166">You can also localize all elements on this page.</span></span> <span data-ttu-id="6c764-167">設定一組「預設」自訂元素之後，就可以設定不同地區設定的其他版本。</span><span class="sxs-lookup"><span data-stu-id="6c764-167">Once you’ve configured a “default” set of customization elements, you can configure more versions for different locales.</span></span> <span data-ttu-id="6c764-168">您也可以混合使用並符合各種元素。</span><span class="sxs-lookup"><span data-stu-id="6c764-168">You can also mix and match various elements.</span></span> <span data-ttu-id="6c764-169">例如，您可以：</span><span class="sxs-lookup"><span data-stu-id="6c764-169">For example, you can:</span></span>

* <span data-ttu-id="6c764-170">建立適用於所有文化的「預設」大型圖例，然後建立英文和法文的特定版本。</span><span class="sxs-lookup"><span data-stu-id="6c764-170">Create a “default” Large Illustration that works for all cultures, then create specific versions for English and French.</span></span> <span data-ttu-id="6c764-171">當您將瀏覽器設定為這兩種語言之一時，會出現特定的影像，至於其他所有語言則會出現預設圖例。</span><span class="sxs-lookup"><span data-stu-id="6c764-171">When you set your browsers to one of these two languages, the specific image appears, while the default illustration appears for all other languages.</span></span>
* <span data-ttu-id="6c764-172">為您的組織設定不同的標誌 (例如日文或希伯來文版本)。</span><span class="sxs-lookup"><span data-stu-id="6c764-172">Configure different logos for your organization (e.g. Japanese or Hebrew versions).</span></span>

## <a name="access-panel-page-customization"></a><span data-ttu-id="6c764-173">存取面板頁面自訂</span><span class="sxs-lookup"><span data-stu-id="6c764-173">Access panel page customization</span></span>
<span data-ttu-id="6c764-174">[存取面板] 頁面基本上是入口網站頁面，可供快速存取系統管理員已授與您存取權的雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c764-174">The Access Panel page is essentially a portal page for quick access to the cloud apps you have been granted access to by your administrator.</span></span> <span data-ttu-id="6c764-175">在此頁面上，您的應用程式會顯示為可點選的應用程式圖格。</span><span class="sxs-lookup"><span data-stu-id="6c764-175">On this page, your apps appear as clickable application tiles.</span></span>

<span data-ttu-id="6c764-176">下列螢幕擷取畫面顯示自訂後的存取面板頁面範例：</span><span class="sxs-lookup"><span data-stu-id="6c764-176">The following screenshot shows an example of an access panel page after customization.</span></span>

![][8]

## <a name="configure-your-directory-with-company-branding"></a><span data-ttu-id="6c764-177">使用公司商標來設定目錄</span><span class="sxs-lookup"><span data-stu-id="6c764-177">Configure your directory with company branding</span></span>
<span data-ttu-id="6c764-178">您可以針對 Azure 傳統入口網站中的每個目錄，設定一組預設的可自訂元素。</span><span class="sxs-lookup"><span data-stu-id="6c764-178">You can configure one default set of customizable elements per directory in the Azure classic portal.</span></span> <span data-ttu-id="6c764-179">儲存預設值之後，系統管理員可以針對不同的語言/地區設定新增每個元素的當地語系化版本。</span><span class="sxs-lookup"><span data-stu-id="6c764-179">After the defaults have been saved, an administrator can add localized versions of each element, for different languages / locales.</span></span> <span data-ttu-id="6c764-180">所有可自訂元素都是選用的。</span><span class="sxs-lookup"><span data-stu-id="6c764-180">All customizable elements are optional.</span></span>

<span data-ttu-id="6c764-181">例如，如果您設定預設 [橫幅標誌]，但未設定 [大型圖例]，則登入頁面會將您的標誌顯示在右上角。</span><span class="sxs-lookup"><span data-stu-id="6c764-181">For example, if you configure a default Banner Logo but no Large Illustration, the sign-in page displays your logo in the upper-right corner.</span></span> <span data-ttu-id="6c764-182">不過，會顯示網站的預設圖例。</span><span class="sxs-lookup"><span data-stu-id="6c764-182">However the default illustration of the site is displayed.</span></span>

<span data-ttu-id="6c764-183">假設有下列組態︰</span><span class="sxs-lookup"><span data-stu-id="6c764-183">Imagine the following configuration:</span></span>

* <span data-ttu-id="6c764-184">預設的橫幅標誌和英文登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="6c764-184">A default Banner Logo and Sign-In Page Text in English</span></span>
* <span data-ttu-id="6c764-185">語言特定的德文登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="6c764-185">A language-specific sign in Page Text for German</span></span>

<span data-ttu-id="6c764-186">如果您的語言喜好設定是德文，您會得到預設的橫幅標誌但為德文文字。</span><span class="sxs-lookup"><span data-stu-id="6c764-186">If your language preference is German, you get the default Banner Logo but the German text.</span></span>

<span data-ttu-id="6c764-187">技術上，雖然您可以針對 Azure AD 所支援的每種語言設定不同的一組，但是基於維護和效能考量，建議您保持低變化數目。</span><span class="sxs-lookup"><span data-stu-id="6c764-187">While you could technically configure a different set for each language supported by Azure AD, we recommend that you keep the number of variations low, for maintenance and performance reasons.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c764-188">Yammer 不會顯示 Azure AD 品牌化登入頁面，直到使用者登入之後。</span><span class="sxs-lookup"><span data-stu-id="6c764-188">Yammer does not show the Azure AD branded sign-in page until after the user signs in.</span></span> <span data-ttu-id="6c764-189">使用者會先看到一般 Office 365 登入頁面，然後再看到該頁面之後的品牌化頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-189">The user sees the generic Office 365 sign-in page first, and then the branded page after that.</span></span>   
 
 
<span data-ttu-id="6c764-190">**若要將公司商標新增至您的目錄，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c764-190">**To add company branding to your directory, perform the following steps:**</span></span>

1. <span data-ttu-id="6c764-191">以想要自訂之目錄的管理員身分，登入 [Azure 傳統入口網站](https://manage.windowsazure.com) 。</span><span class="sxs-lookup"><span data-stu-id="6c764-191">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="6c764-192">選取您想要自訂的目錄。</span><span class="sxs-lookup"><span data-stu-id="6c764-192">Select the directory you want to customize.</span></span>
3. <span data-ttu-id="6c764-193">在頂端的工具列中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-193">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="6c764-194">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-194">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="6c764-195">修改您想要自訂的元素。</span><span class="sxs-lookup"><span data-stu-id="6c764-195">Modify the elements you want to customize.</span></span> <span data-ttu-id="6c764-196">所有欄位都是選用的。</span><span class="sxs-lookup"><span data-stu-id="6c764-196">All fields are optional.</span></span>
6. <span data-ttu-id="6c764-197">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-197">Click **Save**.</span></span>

<span data-ttu-id="6c764-198">您對登入頁面商標進行的新變更最多需要一個小時才會出現。</span><span class="sxs-lookup"><span data-stu-id="6c764-198">It can take up to an hour for new change you made to the sign-in page branding to appear.</span></span>

<span data-ttu-id="6c764-199">**若要新增語言特定公司商標，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c764-199">**To add language-specific company branding, perform the following steps:**</span></span>

1. <span data-ttu-id="6c764-200">以想要自訂之目錄的管理員身分，登入 [Azure 傳統入口網站](https://manage.windowsazure.com) 。</span><span class="sxs-lookup"><span data-stu-id="6c764-200">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="6c764-201">選取您想要自訂的目錄。</span><span class="sxs-lookup"><span data-stu-id="6c764-201">Select the directory you want to customize.</span></span>
<span data-ttu-id="6c764-202">fs3。</span><span class="sxs-lookup"><span data-stu-id="6c764-202">fs3.</span></span> <span data-ttu-id="6c764-203">在頂端的工具列中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-203">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="6c764-204">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-204">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="6c764-205">按一下 [新增特定語言的商標] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-205">Click **Add branding for a specific language**.</span></span>
6. <span data-ttu-id="6c764-206">選取您要自訂標誌的語言，然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-206">Select the language you want to customize the logo for, and then click **Next**.</span></span>
7. <span data-ttu-id="6c764-207">僅編輯您想要設定語言特定覆寫的元素。</span><span class="sxs-lookup"><span data-stu-id="6c764-207">Edit only the elements for which you want to configure language-specific overrides.</span></span> <span data-ttu-id="6c764-208">所有欄位都是選用的。</span><span class="sxs-lookup"><span data-stu-id="6c764-208">All fields are optional.</span></span> <span data-ttu-id="6c764-209">如果欄位空白，則會改為顯示自訂預設值 (或者，如果未設定自訂預設值，則為 Microsoft 預設值)。</span><span class="sxs-lookup"><span data-stu-id="6c764-209">If a field is left blank, then the custom default value is displayed instead (or the Microsoft default if a custom default is not configured).</span></span>
8. <span data-ttu-id="6c764-210">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-210">Click **Save**.</span></span>

<span data-ttu-id="6c764-211">**若要從您的目錄中移除公司商標，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c764-211">**To remove company branding from your directory, perform the following steps:**</span></span>

1. <span data-ttu-id="6c764-212">以想要自訂之目錄的管理員身分，登入 [Azure 傳統入口網站](https://manage.windowsazure.com) 。</span><span class="sxs-lookup"><span data-stu-id="6c764-212">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator of the directory you want to customize.</span></span>
2. <span data-ttu-id="6c764-213">選取您想要自訂的目錄。</span><span class="sxs-lookup"><span data-stu-id="6c764-213">Select the directory you want to customize.</span></span>
3. <span data-ttu-id="6c764-214">在頂端的工具列中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-214">In the toolbar on the top, click **Configure**.</span></span>
4. <span data-ttu-id="6c764-215">按一下 [自訂商標] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-215">Click **Customize Branding**.</span></span>
5. <span data-ttu-id="6c764-216">在 [自訂商標] 頁面上，選取 [編輯現有商標設定]  ，然後移至下一頁。</span><span class="sxs-lookup"><span data-stu-id="6c764-216">On the Customize Branding page, select **Edit Existing Branding Settings** and then go to the next page.</span></span>
6. <span data-ttu-id="6c764-217">根據您想要移除的元素，執行下列一或多項動作：</span><span class="sxs-lookup"><span data-stu-id="6c764-217">Depending on which elements you want to remove, do one or more of the following:</span></span>

    <span data-ttu-id="6c764-218">a.</span><span class="sxs-lookup"><span data-stu-id="6c764-218">a.</span></span> <span data-ttu-id="6c764-219">在 [橫幅標誌] 之下，選取 [移除上傳的標誌]。</span><span class="sxs-lookup"><span data-stu-id="6c764-219">Under **Banner Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="6c764-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c764-220">b.</span></span> <span data-ttu-id="6c764-221">在 [圖格標誌] 之下，選取 [移除上傳的標誌]。</span><span class="sxs-lookup"><span data-stu-id="6c764-221">Under **Tile Logo**, select **Remove uploaded logo**.</span></span>

    <span data-ttu-id="6c764-222">c.</span><span class="sxs-lookup"><span data-stu-id="6c764-222">c.</span></span> <span data-ttu-id="6c764-223">移除所有文字方塊中的文字。</span><span class="sxs-lookup"><span data-stu-id="6c764-223">Remove the text from all textboxes.</span></span>

    <span data-ttu-id="6c764-224">d.</span><span class="sxs-lookup"><span data-stu-id="6c764-224">d.</span></span> <span data-ttu-id="6c764-225">按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="6c764-225">Click **Next**.</span></span>

    <span data-ttu-id="6c764-226">e.</span><span class="sxs-lookup"><span data-stu-id="6c764-226">e.</span></span> <span data-ttu-id="6c764-227">移除所有文字方塊中的文字。</span><span class="sxs-lookup"><span data-stu-id="6c764-227">Remove the text from all textboxes.</span></span>
7. <span data-ttu-id="6c764-228">按一下 [儲存]  移除元素。</span><span class="sxs-lookup"><span data-stu-id="6c764-228">Click **Save** to remove the elements.</span></span>
8. <span data-ttu-id="6c764-229">如有必要，請再按一下 [自訂商標]  ，並針對需要移除的所有語言特定商標重複這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6c764-229">If necessary, click **Customize Branding** again and repeat these steps for all language-specific branding that needs to be removed.</span></span>
    <span data-ttu-id="6c764-230">按一下 [自訂商標] 並看到未設定現有設定的 [自訂預設商標] 表單時，已移除所有商標設定。</span><span class="sxs-lookup"><span data-stu-id="6c764-230">All branding settings have been removed when you click **Customize Branding** and see the **Customize Default Branding** form with no existing settings configured.</span></span>

## <a name="testing-and-examples"></a><span data-ttu-id="6c764-231">測試和範例</span><span class="sxs-lookup"><span data-stu-id="6c764-231">Testing and examples</span></span>
<span data-ttu-id="6c764-232">建議您先使用測試租用戶進行試驗，再於生產環境中進行變更。</span><span class="sxs-lookup"><span data-stu-id="6c764-232">We recommend that you experiment with a test tenant before making changes in your production environment.</span></span>

<span data-ttu-id="6c764-233">**若要確認商標是否已套用︰**</span><span class="sxs-lookup"><span data-stu-id="6c764-233">**To verify whether your branding has been applied:**</span></span>

1. <span data-ttu-id="6c764-234">開啟 InPrivate 或 Incognito 瀏覽器工作階段。</span><span class="sxs-lookup"><span data-stu-id="6c764-234">Open an InPrivate or Incognito browser session.</span></span>
2. <span data-ttu-id="6c764-235">瀏覽 https://outlook.com/contoso.com，並將 contoso.com 取代為您自訂的網域。</span><span class="sxs-lookup"><span data-stu-id="6c764-235">Visit https://outlook.com/contoso.com, replacing contoso.com with the domain you’ve customized.</span></span>

<span data-ttu-id="6c764-236">這也適用於類似 contoso.onmicrosoft.com 的網域。</span><span class="sxs-lookup"><span data-stu-id="6c764-236">This also works with domains that look like contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="6c764-237">為了協助您建立有效自訂集，我們已自訂下列兩個虛構的登入頁面：</span><span class="sxs-lookup"><span data-stu-id="6c764-237">To help you create effective customization sets, we have customized the following two fictitious sign-in pages:</span></span>

* [<span data-ttu-id="6c764-238">http://aka.ms/aaddemo001</span><span class="sxs-lookup"><span data-stu-id="6c764-238">http://aka.ms/aaddemo001</span></span>](http://aka.ms/aaddemo001)
* [<span data-ttu-id="6c764-239">http://aka.ms/aaddemo002</span><span class="sxs-lookup"><span data-stu-id="6c764-239">http://aka.ms/aaddemo002</span></span>](http://aka.ms/aaddemo002)

<span data-ttu-id="6c764-240">若要測試語言特定設定，您需要將網頁瀏覽器中的預設語言喜好設定修改為已在自訂中所設定的語言。</span><span class="sxs-lookup"><span data-stu-id="6c764-240">To test the language-specific settings, you need to modify the default language preferences in your web browser to a language you have set in your customization.</span></span> <span data-ttu-id="6c764-241">在 Internet Explorer 中，您可在 [網際網路選項]  功能表中進行此設定。</span><span class="sxs-lookup"><span data-stu-id="6c764-241">In Internet Explorer, you configure this in the **Internet Options** menu.</span></span>

## <a name="customizable-elements"></a><span data-ttu-id="6c764-242">可自訂元素</span><span class="sxs-lookup"><span data-stu-id="6c764-242">Customizable elements</span></span>
<span data-ttu-id="6c764-243">Azure AD 中的部分可自訂元素有多個使用案例。</span><span class="sxs-lookup"><span data-stu-id="6c764-243">Some customizable elements in Azure AD have multiple use cases.</span></span> <span data-ttu-id="6c764-244">您可以在每個目錄設定一次公司標誌並同時用於 [登入] 頁面和 [存取面板] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6c764-244">You can configure company logos once per directory and is used on both, the sign-in and Access Panel pages.</span></span> <span data-ttu-id="6c764-245">有些可自訂元素為登入頁面所特有。</span><span class="sxs-lookup"><span data-stu-id="6c764-245">Some customizable elements are specific only to the sign-in page.</span></span> <span data-ttu-id="6c764-246">下表提供不同可自訂元素的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6c764-246">The following table provides details for the different customizable elements.</span></span>

| <span data-ttu-id="6c764-247">名稱</span><span class="sxs-lookup"><span data-stu-id="6c764-247">Name</span></span> | <span data-ttu-id="6c764-248">說明</span><span class="sxs-lookup"><span data-stu-id="6c764-248">Description</span></span> | <span data-ttu-id="6c764-249">條件約束</span><span class="sxs-lookup"><span data-stu-id="6c764-249">Constraints</span></span> | <span data-ttu-id="6c764-250">建議</span><span class="sxs-lookup"><span data-stu-id="6c764-250">Recommendations</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6c764-251">橫幅標誌</span><span class="sxs-lookup"><span data-stu-id="6c764-251">Banner Logo</span></span> |<span data-ttu-id="6c764-252">[橫幅標誌] 會顯示在 [登入] 頁面和 [存取面板] 上。</span><span class="sxs-lookup"><span data-stu-id="6c764-252">The Banner Logo is displayed on the sign-in page and the Access panel.</span></span> |<p><span data-ttu-id="6c764-253">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="6c764-253">JPG or PNG</span></span></p><p><span data-ttu-id="6c764-254">60x280 像素</span><span class="sxs-lookup"><span data-stu-id="6c764-254">60x280 pixels</span></span></p><p><span data-ttu-id="6c764-255">10 KB</span><span class="sxs-lookup"><span data-stu-id="6c764-255">10 KB</span></span></p> |<p><span data-ttu-id="6c764-256">使用您組織的完整標誌 (包含形符和商標)</span><span class="sxs-lookup"><span data-stu-id="6c764-256">Use your organization’s full logo (including pictogram and logotype)</span></span></p><p><span data-ttu-id="6c764-257">保持低於 30 個像素，避免行動裝置上出現捲軸</span><span class="sxs-lookup"><span data-stu-id="6c764-257">Keep it under 30 pixels high to avoid introducing scrollbars on mobile devices</span></span></p><p><span data-ttu-id="6c764-258">保持低於 4 KB</span><span class="sxs-lookup"><span data-stu-id="6c764-258">Keep it under 4 KB</span></span></p><p><span data-ttu-id="6c764-259">使用透明 PNG (不認為登入頁面一律具有白色背景)</span><span class="sxs-lookup"><span data-stu-id="6c764-259">Use a transparent PNG (don’t assume that the sign-in page always has a white background)</span></span></p> |
| <span data-ttu-id="6c764-260">磚標誌</span><span class="sxs-lookup"><span data-stu-id="6c764-260">Tile Logo</span></span> |<span data-ttu-id="6c764-261">(目前未用於 [登入] 頁面中) 未來，這段文字可能用來取代不同體驗位置中的泛用「工作或學校帳戶」pictogram。</span><span class="sxs-lookup"><span data-stu-id="6c764-261">(currently not used in the sign-in page) In the future, this text may be used to replace the generic “work or school account” pictogram in different places of the experience.</span></span> |<p><span data-ttu-id="6c764-262">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="6c764-262">JPG or PNG</span></span></p><p><span data-ttu-id="6c764-263">120x120 像素</span><span class="sxs-lookup"><span data-stu-id="6c764-263">120x120 pixels</span></span></p><p><span data-ttu-id="6c764-264">10 KB</span><span class="sxs-lookup"><span data-stu-id="6c764-264">10 KB</span></span></p> |<p><span data-ttu-id="6c764-265">保持簡單 (無小型文字)，因為此影像大小可能會調整為 50%</span><span class="sxs-lookup"><span data-stu-id="6c764-265">Keep it simple (no small text), as this image may be resized to 50%</span></span> |
| </p> | | | |
| <span data-ttu-id="6c764-266">登入頁面使用者名稱標籤</span><span class="sxs-lookup"><span data-stu-id="6c764-266">Sign-in Page User Name Label</span></span> |<span data-ttu-id="6c764-267">(目前未用於 [登入] 頁面中) 未來，這段文字可能用來取代不同體驗位置中的泛用「工作或學校帳戶」字串。</span><span class="sxs-lookup"><span data-stu-id="6c764-267">(currently not used in the sign-in page) In the future, this text may be used to replace the generic “work or school account” string in different places of the experience.</span></span> <span data-ttu-id="6c764-268">您可以將它設定為「Contoso 帳戶」或「Contoso 識別碼」這類項目。</span><span class="sxs-lookup"><span data-stu-id="6c764-268">You can set it to something like “Contoso account” or “Contoso ID.”</span></span> |<p><span data-ttu-id="6c764-269">Unicode 文字，最多 50 個字元</span><span class="sxs-lookup"><span data-stu-id="6c764-269">Unicode text, up to 50 characters</span></span></p><p><span data-ttu-id="6c764-270">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="6c764-270">Plain text only (no links or HTML tags)</span></span></p> |<p><span data-ttu-id="6c764-271">保持簡短和簡單</span><span class="sxs-lookup"><span data-stu-id="6c764-271">Keep it short and simple</span></span></p><p><span data-ttu-id="6c764-272">詢問使用者通常如何參照您提供給他們的工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c764-272">Ask your users how they usually refer to the work or school account you provide them with.</span></span></p> |
| <span data-ttu-id="6c764-273">登入頁面文字</span><span class="sxs-lookup"><span data-stu-id="6c764-273">Sign-in Page Text</span></span> |<span data-ttu-id="6c764-274">此「重複使用」文字會出現在 [登入] 頁面表單下方，並且可以用來傳達其他指示或可在何處取得說明和支援。</span><span class="sxs-lookup"><span data-stu-id="6c764-274">This “boilerplate” text appears below the sign-in page form and can be used to communicate additional instructions, or where to get help and support.</span></span> |<p><span data-ttu-id="6c764-275">Unicode 文字，最多 256 個字元</span><span class="sxs-lookup"><span data-stu-id="6c764-275">Unicode text, up to 256 characters</span></span></p><p><span data-ttu-id="6c764-276">僅純文字 (沒有連結或 HTML 標記)</span><span class="sxs-lookup"><span data-stu-id="6c764-276">Plain text only (no links or HTML tags)</span></span></p> |<span data-ttu-id="6c764-277">保持低於 250 個字元 (約 3 行文字)</span><span class="sxs-lookup"><span data-stu-id="6c764-277">Keep it under 250 characters (approximately 3 lines of text)</span></span> |
| <span data-ttu-id="6c764-278">登入頁面圖例</span><span class="sxs-lookup"><span data-stu-id="6c764-278">Sign-in Page Illustration</span></span> |<span data-ttu-id="6c764-279">圖例是顯示在 [登入] 頁面表單左邊之 [登入] 頁面中的大型影像。</span><span class="sxs-lookup"><span data-stu-id="6c764-279">The illustration is a large image that is displayed on the sign-in page to the left of the sign-in page form.</span></span> |<p><span data-ttu-id="6c764-280">JPG 或 PNG</span><span class="sxs-lookup"><span data-stu-id="6c764-280">JPG or PNG</span></span></p><p><span data-ttu-id="6c764-281">1420x1200</span><span class="sxs-lookup"><span data-stu-id="6c764-281">1420x1200</span></span></p><p><span data-ttu-id="6c764-282">500 KB</span><span class="sxs-lookup"><span data-stu-id="6c764-282">500 KB</span></span></p> |<p><span data-ttu-id="6c764-283">1420x1200 像素</span><span class="sxs-lookup"><span data-stu-id="6c764-283">1420x1200 pixels</span></span></p><p><span data-ttu-id="6c764-284">重要事項：保持越小越好，最好低於 200 KB。</span><span class="sxs-lookup"><span data-stu-id="6c764-284">Important: Keep it as small as possible, ideally under 200 KB.</span></span> <span data-ttu-id="6c764-285">如果此影像太大，則會在未快取影像時影響 [登入] 頁面的效能</span><span class="sxs-lookup"><span data-stu-id="6c764-285">If this image is too large, the performance of the Sign-in page is impacted when the image isn’t cached</span></span></p><p><span data-ttu-id="6c764-286">此影像通常會進行剪裁，以符合不同的螢幕外觀比例。</span><span class="sxs-lookup"><span data-stu-id="6c764-286">This image is often cropped, to accommodate different screen ratios.</span></span> <span data-ttu-id="6c764-287">將主要視覺元素保持在左上角 (RTL 語言，則顯示在右上角)，因為隨著瀏覽器視窗的縮小，調整大小會從右下角往左上方。</span><span class="sxs-lookup"><span data-stu-id="6c764-287">Keep the primary visual elements in the top left corner (top right for RTL languages), because resizing occurs from the bottom/right corner, going towards the top / left, as the browser window shrinks.</span></span></p> |
| <span data-ttu-id="6c764-288">登入頁面背景色彩</span><span class="sxs-lookup"><span data-stu-id="6c764-288">Sign-in Page Background Color</span></span> |<span data-ttu-id="6c764-289">登入頁面背景色彩用於 [登入] 頁面表單左方的區域。</span><span class="sxs-lookup"><span data-stu-id="6c764-289">The sign-in page background color is used in the area to the left of the sign-in page form.</span></span> |<span data-ttu-id="6c764-290">必須是十六進位格式的 RGB 色彩 (範例: #FFFFFF)</span><span class="sxs-lookup"><span data-stu-id="6c764-290">Must be an RGB color in hexadecimal form (example: #FFFFFF)</span></span> |<p><span data-ttu-id="6c764-291">可能會顯示背景色彩，來替代低頻寬連線上的大型圖例</span><span class="sxs-lookup"><span data-stu-id="6c764-291">The background color may be shown in place of the large Illustration on low-bandwidth connections</span></span></p><p><span data-ttu-id="6c764-292">我們建議挑選橫幅標誌的主要色彩</span><span class="sxs-lookup"><span data-stu-id="6c764-292">We suggest picking the primary color of the Banner Logo</span></span></p> |

## <a name="next-steps"></a><span data-ttu-id="6c764-293">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c764-293">Next steps</span></span>
* [<span data-ttu-id="6c764-294">開始使用 Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="6c764-294">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="6c764-295">檢視存取和使用情況報告</span><span class="sxs-lookup"><span data-stu-id="6c764-295">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)

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
