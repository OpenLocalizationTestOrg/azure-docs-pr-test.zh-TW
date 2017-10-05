---
title: "轉譯連結和 URL Azure AD Application Proxy | Microsoft Docs"
description: "涵蓋 Azure AD 應用程式 Proxy 連接器的基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 57218346d236b376d2227e0ffaea6c6dd5ebe855
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a><span data-ttu-id="b8d27-103">重新導向使用 Azure AD Application Proxy 發佈之應用程式的硬式編碼連結</span><span class="sxs-lookup"><span data-stu-id="b8d27-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span></span>

<span data-ttu-id="b8d27-104">Azure AD Application Proxy 讓您的內部部署應用程式可供遠端使用者使用，或讓使用者在其自己的裝置上使用。</span><span class="sxs-lookup"><span data-stu-id="b8d27-104">Azure AD Application Proxy makes your on-premises apps available to users who are remote or on their own devices.</span></span> <span data-ttu-id="b8d27-105">不過，有些應用程式是以 HTML 中內嵌的本機連結進行開發。</span><span class="sxs-lookup"><span data-stu-id="b8d27-105">Some apps, however, were developed with local links embedded in the HTML.</span></span> <span data-ttu-id="b8d27-106">從遠端使用應用程式時，這些連結無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="b8d27-106">These links don't work correctly when the app is used remotely.</span></span> <span data-ttu-id="b8d27-107">當您有數個指向彼此的內部部署應用程式時，使用者預期當他們不在辦公室時，連結可持續運作。</span><span class="sxs-lookup"><span data-stu-id="b8d27-107">When you have several on-premises applications point to each other, your users expect the links to keep working when they're not at the office.</span></span> 

<span data-ttu-id="b8d27-108">若要確定連結在公司網路內部和外部的運作方式相同，最佳方法就是將您應用程式的外部 URL 設定為與其內部 URL 相同。</span><span class="sxs-lookup"><span data-stu-id="b8d27-108">The best way to make sure that links work the same both inside and outside of your corporate network is to configure the external URLs of your apps to be the same as their internal URLs.</span></span> <span data-ttu-id="b8d27-109">使用[自訂網域](active-directory-application-proxy-custom-domains.md)，將您的外部 URL 設定為包含公司網域名稱，而不是預設的應用程式 Proxy 網域。</span><span class="sxs-lookup"><span data-stu-id="b8d27-109">Use [custom domains](active-directory-application-proxy-custom-domains.md) to configure your external URLs to have your corporate domain name instead of the default application proxy domain.</span></span>

<span data-ttu-id="b8d27-110">如果您無法在租用戶中使用自訂網域，應用程式 Proxy 的連結轉譯功能會讓您的連結保持運作 (不論您的使用者身在何處)。</span><span class="sxs-lookup"><span data-stu-id="b8d27-110">If you can't use custom domains in your tenant, then the link translation feature of Application Proxy keeps your links working no matter where your users are.</span></span> <span data-ttu-id="b8d27-111">當您有直接指向內部端點或連接埠的應用程式時，您可以將這些內部 URL 對應至已發佈的外部 Application Proxy URL。</span><span class="sxs-lookup"><span data-stu-id="b8d27-111">When you have apps that point directly to internal endpoints or ports, you can map these internal URLs to the published external Application Proxy URLs.</span></span> <span data-ttu-id="b8d27-112">若已啟用連結轉譯，應用程式 Proxy 會透過 HTML、CSS 搜尋，並選取已發佈內部連結的 JavaScript 標籤。</span><span class="sxs-lookup"><span data-stu-id="b8d27-112">When link translation is enabled, and Application Proxy searches through HTML, CSS, and select JavaScript tags for published internal links.</span></span> <span data-ttu-id="b8d27-113">然後應用程式 Proxy 會將它們轉譯，以便使用者獲得不受干擾的體驗。</span><span class="sxs-lookup"><span data-stu-id="b8d27-113">Then the Application Proxy service translates them so that your users get an uninterrupted experience.</span></span>

>[!NOTE]
><span data-ttu-id="b8d27-114">連結轉譯功能適用於無法使用自訂網域 (不論何種原因) 讓其應用程式具有相同內部和外部 URL 的租用戶。</span><span class="sxs-lookup"><span data-stu-id="b8d27-114">The link translation feature is for tenants that, for whatever reason, can't use custom domains to have the same internal and external URLs for their apps.</span></span> <span data-ttu-id="b8d27-115">在您啟用這項功能之前，請查看您是否適用 [Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="b8d27-115">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) can work for you.</span></span>
>
><span data-ttu-id="b8d27-116">或者，如果您需要透過連結轉譯設定的應用程式為 SharePoint，請參閱[設定 SharePoint 2013 的備用存取對應](https://technet.microsoft.com/library/cc263208.aspx)以取得對應連結的另一種方法。</span><span class="sxs-lookup"><span data-stu-id="b8d27-116">Or, if the application you need to configure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach to mapping links.</span></span>

## <a name="how-link-translation-works"></a><span data-ttu-id="b8d27-117">連結轉譯的運作方式</span><span class="sxs-lookup"><span data-stu-id="b8d27-117">How link translation works</span></span>

<span data-ttu-id="b8d27-118">驗證之後，當 Proxy 伺服器將應用程式資料傳遞給使用者時，Application Proxy 會掃描應用程式中的硬式編碼連結，然後以其各自發佈的外部 URL 加以取代。</span><span class="sxs-lookup"><span data-stu-id="b8d27-118">After authentication, when the proxy server passes the application data to the user, Application Proxy scans the application for hardcoded links and replaces them with their respective, published external URLs.</span></span>

<span data-ttu-id="b8d27-119">應用程式 Proxy 假設應用程式是以 UTF-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="b8d27-119">Application Proxy assumes that applications are encoded in UTF-8.</span></span> <span data-ttu-id="b8d27-120">如果事實並非如此，請在 http 回應標頭中指定編碼類型，例如 `Content-Type:text/html;charset=utf-8`。</span><span class="sxs-lookup"><span data-stu-id="b8d27-120">If that's not the case, specify the encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span></span>

### <a name="which-links-are-affected"></a><span data-ttu-id="b8d27-121">哪些連結會受影響？</span><span class="sxs-lookup"><span data-stu-id="b8d27-121">Which links are affected?</span></span>

<span data-ttu-id="b8d27-122">連結轉譯功能只會尋找位於應用程式主體的程式碼標籤中的連結。</span><span class="sxs-lookup"><span data-stu-id="b8d27-122">The link translation feature only looks for links that are in code tags in the body of an app.</span></span> <span data-ttu-id="b8d27-123">Application Proxy 有個別功能可轉譯標頭中的 cookie 或 URL。</span><span class="sxs-lookup"><span data-stu-id="b8d27-123">Application Proxy has a separate feature for translating cookies or URLs in headers.</span></span> 

<span data-ttu-id="b8d27-124">內部部署應用程式中有兩種常見的內部連結類型：</span><span class="sxs-lookup"><span data-stu-id="b8d27-124">There are two common types of internal links in on-premises applications:</span></span>

- <span data-ttu-id="b8d27-125">**相對內部連結**，其指向本機檔案結構中的共用資源，例如 `/claims/claims.html`。</span><span class="sxs-lookup"><span data-stu-id="b8d27-125">**Relative internal links** that point to a shared resource in a local file structure like `/claims/claims.html`.</span></span> <span data-ttu-id="b8d27-126">這些連結會自動在透過應用程式 Proxy 發佈的應用程式中運作，並且持續運作 (不論是否啟用連結轉譯)。</span><span class="sxs-lookup"><span data-stu-id="b8d27-126">These links automatically work in apps that are published through Application Proxy, and continue to work with or without link translation.</span></span> 
- <span data-ttu-id="b8d27-127">其他內部部署應用程式 (例如 `http://expenses`) 或已發佈檔案 (例如 `http://expenses/logo.jpg`) 的**硬式編碼內部連結**。</span><span class="sxs-lookup"><span data-stu-id="b8d27-127">**Hardcoded internal links** to other on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span></span> <span data-ttu-id="b8d27-128">連結轉譯功能適用於硬式編碼內部連結，並可將這些連結變更為指向遠端使用者必須通過的外部 URL。</span><span class="sxs-lookup"><span data-stu-id="b8d27-128">The link translation feature works on hardcoded internal links, and changes them to point to the external URLs that remote users need to go through.</span></span>

### <a name="how-do-apps-link-to-each-other"></a><span data-ttu-id="b8d27-129">應用程式如何彼此連結？</span><span class="sxs-lookup"><span data-stu-id="b8d27-129">How do apps link to each other?</span></span>

<span data-ttu-id="b8d27-130">每個應用程式都已啟用連結轉譯，以便您控制每個應用程式層級的使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="b8d27-130">Link translation is enabled for each application, so that you have control over the user experience at the per-app level.</span></span> <span data-ttu-id="b8d27-131">當您想要轉譯「來自」該應用程式的連結 (而非「連到」該應用程式的連結) 時，請開啟應用程式的連結轉譯。</span><span class="sxs-lookup"><span data-stu-id="b8d27-131">Turn on link translation for an app when you want the links *from* that app to be translated, not links *to* that app.</span></span> 

<span data-ttu-id="b8d27-132">例如，假設您有三個透過 Application Proxy 發佈且彼此連結的應用程式：Benefits、Expenses 和 Travel。</span><span class="sxs-lookup"><span data-stu-id="b8d27-132">For example, suppose that you have three applications published through Application Proxy that all link to each other: Benefits, Expenses, and Travel.</span></span> <span data-ttu-id="b8d27-133">第四個應用程式 (Feedback) 不是透過 Application Proxy 發佈。</span><span class="sxs-lookup"><span data-stu-id="b8d27-133">There's a fourth app, Feedback, that isn't published through Application Proxy.</span></span>

<span data-ttu-id="b8d27-134">當您啟用 Benefits 應用程式的連結轉譯時，Expenses 和 Travel 的連結會重新導向至這些應用程式的外部 URL，但 Feedback 的連結因為沒有外部 URL 而不會重新導向。</span><span class="sxs-lookup"><span data-stu-id="b8d27-134">When you enable link translation for the Benefits app, the links to Expenses and Travel are redirected to the external URLs for those apps, but the link to Feedback is not redirected because there is no external URL.</span></span> <span data-ttu-id="b8d27-135">從 Expenses 和 Travel 回到 Benefits 的連結沒有作用，因為這兩個應用程式尚未啟用連結轉譯功能。</span><span class="sxs-lookup"><span data-stu-id="b8d27-135">Links from Expenses and Travel back to Benefits don't work, because link translation has not been enabled for those two apps.</span></span>

![已啟用連結轉譯時從 Benefits 到其他應用程式的連結](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a><span data-ttu-id="b8d27-137">哪些連結並未轉譯？</span><span class="sxs-lookup"><span data-stu-id="b8d27-137">Which links aren't translated?</span></span>

<span data-ttu-id="b8d27-138">為了改善效能和安全性，並未轉譯有些連結：</span><span class="sxs-lookup"><span data-stu-id="b8d27-138">To improve performance and security, some links aren't translated:</span></span>

- <span data-ttu-id="b8d27-139">不在程式碼標籤內的連結。</span><span class="sxs-lookup"><span data-stu-id="b8d27-139">Links not inside of code tags.</span></span> 
- <span data-ttu-id="b8d27-140">不在 HTML、CSS 或 JavaScript 中的連結。</span><span class="sxs-lookup"><span data-stu-id="b8d27-140">Links not in HTML, CSS, or JavaScript.</span></span> 
- <span data-ttu-id="b8d27-141">從其他程式開啟的內部連結。</span><span class="sxs-lookup"><span data-stu-id="b8d27-141">Internal links opened from other programs.</span></span> <span data-ttu-id="b8d27-142">不會轉譯透過電子郵件或立即訊息傳送的連結，或包含在其他文件中的連結。</span><span class="sxs-lookup"><span data-stu-id="b8d27-142">Links sent through email or instant message, or included in other documents, won't be translated.</span></span> <span data-ttu-id="b8d27-143">使用者必須知道要移至外部 URL。</span><span class="sxs-lookup"><span data-stu-id="b8d27-143">The users need to know to go to the external URL.</span></span>

<span data-ttu-id="b8d27-144">如果您必須支援下列其中一種情況，請使用相同的內部和外部 URL，而不需進行連結轉譯。</span><span class="sxs-lookup"><span data-stu-id="b8d27-144">If you need to support one of these two scenarios, use the same internal and external URLs instead of link translation.</span></span>  

## <a name="enable-link-translation"></a><span data-ttu-id="b8d27-145">啟用連結轉譯</span><span class="sxs-lookup"><span data-stu-id="b8d27-145">Enable link translation</span></span>

<span data-ttu-id="b8d27-146">開始使用連結轉譯很簡單，按一下按鈕即可：</span><span class="sxs-lookup"><span data-stu-id="b8d27-146">Getting started with link translation is as easy as clicking a button:</span></span>

1. <span data-ttu-id="b8d27-147">以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b8d27-147">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="b8d27-148">移至 [Azure Active Directory] > [企業應用程式] > [所有應用程式] > 選取您要管理的應用程式 > [Application Proxy]。</span><span class="sxs-lookup"><span data-stu-id="b8d27-148">Go to **Azure Active Directory** > **Enterprise applications** > **All applications** > select the app you want to manage > **Application proxy**.</span></span>
3. <span data-ttu-id="b8d27-149">將 [轉譯應用程式主體中的 URL] 切換為 [是]。</span><span class="sxs-lookup"><span data-stu-id="b8d27-149">Turn **Translate URLs in application body** to **Yes**.</span></span>

   ![選取 [是] 可轉譯應用程式主體中的 URL](./media/application-proxy-link-translation/select_yes.png)<span data-ttu-id="b8d27-151">。</span><span class="sxs-lookup"><span data-stu-id="b8d27-151">.</span></span>
4. <span data-ttu-id="b8d27-152">選取 [儲存] 以套用變更。</span><span class="sxs-lookup"><span data-stu-id="b8d27-152">Select **Save** to apply your changes.</span></span>

<span data-ttu-id="b8d27-153">現在，當您的使用者存取此應用程式時，Proxy 會自動掃描已透過您租用戶上的 Application Proxy 發佈的內部 URL。</span><span class="sxs-lookup"><span data-stu-id="b8d27-153">Now, when your users access this application, the proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span></span>

## <a name="send-feedback"></a><span data-ttu-id="b8d27-154">傳送意見反應</span><span class="sxs-lookup"><span data-stu-id="b8d27-154">Send feedback</span></span>

<span data-ttu-id="b8d27-155">我們需要您的協助，讓這項功能可用於您所有的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b8d27-155">We want your help to make this feature work for all your apps.</span></span> <span data-ttu-id="b8d27-156">我們搜尋 HTML 和 CSS 中超過 30 個標籤，並考慮要支援哪些 JavaScript 案例。</span><span class="sxs-lookup"><span data-stu-id="b8d27-156">We search over 30 tags in HTML and CSS, and are considering which JavaScript cases to support.</span></span> <span data-ttu-id="b8d27-157">如果您有不在轉譯中的已產生連結範例，請將程式碼片段傳送至 [Application Proxy 意見反應](mailto:aadapfeedback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="b8d27-157">If you have an example of generated links that aren't being translated, send a code snippet to [Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b8d27-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8d27-158">Next steps</span></span>
<span data-ttu-id="b8d27-159">[使用自訂網域搭配 Azure AD 應用程式 Proxy](active-directory-application-proxy-custom-domains.md) 以具有相同的內部和外部 URL</span><span class="sxs-lookup"><span data-stu-id="b8d27-159">[Use custom domains with Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) to have the same internal and external URL</span></span>

[<span data-ttu-id="b8d27-160">設定 SharePoint 2013 的備用存取對應</span><span class="sxs-lookup"><span data-stu-id="b8d27-160">Configure alternate access mappings for SharePoint 2013</span></span>](https://technet.microsoft.com/library/cc263208.aspx)
