---
title: "aaaTranslate 連結和 Url 的 Azure AD 應用程式 Proxy |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念。"
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
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a><span data-ttu-id="e694f-103">重新導向使用 Azure AD Application Proxy 發佈之應用程式的硬式編碼連結</span><span class="sxs-lookup"><span data-stu-id="e694f-103">Redirect hardcoded links for apps published with Azure AD Application Proxy</span></span>

<span data-ttu-id="e694f-104">Azure AD Application Proxy 可讓您在內部部署應用程式可用 toousers 遠端或在他們自己的裝置上。</span><span class="sxs-lookup"><span data-stu-id="e694f-104">Azure AD Application Proxy makes your on-premises apps available toousers who are remote or on their own devices.</span></span> <span data-ttu-id="e694f-105">不過，某些應用程式，所開發的內嵌在 hello HTML 中的本機連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-105">Some apps, however, were developed with local links embedded in hello HTML.</span></span> <span data-ttu-id="e694f-106">從遠端使用 hello 應用程式時，這些連結無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="e694f-106">These links don't work correctly when hello app is used remotely.</span></span> <span data-ttu-id="e694f-107">當您有幾個內部部署應用程式點 tooeach 其他時，您的使用者預期 hello 連結 tookeep 運作時不是在 hello 辦公室。</span><span class="sxs-lookup"><span data-stu-id="e694f-107">When you have several on-premises applications point tooeach other, your users expect hello links tookeep working when they're not at hello office.</span></span> 

<span data-ttu-id="e694f-108">hello 最佳方式 toomake 確定連結工作 hello 相同這兩個內部公司網路外 tooconfigure hello 外部 Url 的應用程式 toobe hello 相同其內部的 url。</span><span class="sxs-lookup"><span data-stu-id="e694f-108">hello best way toomake sure that links work hello same both inside and outside of your corporate network is tooconfigure hello external URLs of your apps toobe hello same as their internal URLs.</span></span> <span data-ttu-id="e694f-109">使用[自訂網域](active-directory-application-proxy-custom-domains.md)tooconfigure 您公司網域名稱，而不是 hello 預設應用程式 proxy 網域的外部 Url toohave。</span><span class="sxs-lookup"><span data-stu-id="e694f-109">Use [custom domains](active-directory-application-proxy-custom-domains.md) tooconfigure your external URLs toohave your corporate domain name instead of hello default application proxy domain.</span></span>

<span data-ttu-id="e694f-110">如果您的租用戶中，您無法使用自訂網域，hello 的應用程式 Proxy 連結轉譯 」 功能會保留您不論您的使用者工作的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-110">If you can't use custom domains in your tenant, then hello link translation feature of Application Proxy keeps your links working no matter where your users are.</span></span> <span data-ttu-id="e694f-111">當您指向直接 toointernal 端點或連接埠，您可以將對應的應用程式時這些內部 Url toohello 發行外部應用程式 Proxy Url。</span><span class="sxs-lookup"><span data-stu-id="e694f-111">When you have apps that point directly toointernal endpoints or ports, you can map these internal URLs toohello published external Application Proxy URLs.</span></span> <span data-ttu-id="e694f-112">若已啟用連結轉譯，應用程式 Proxy 會透過 HTML、CSS 搜尋，並選取已發佈內部連結的 JavaScript 標籤。</span><span class="sxs-lookup"><span data-stu-id="e694f-112">When link translation is enabled, and Application Proxy searches through HTML, CSS, and select JavaScript tags for published internal links.</span></span> <span data-ttu-id="e694f-113">然後 hello 應用程式 Proxy 服務會轉譯它們，以便讓您的使用者取得不受干擾的體驗。</span><span class="sxs-lookup"><span data-stu-id="e694f-113">Then hello Application Proxy service translates them so that your users get an uninterrupted experience.</span></span>

>[!NOTE]
><span data-ttu-id="e694f-114">hello 連結轉譯功能是讓租用戶，無論原因，無法使用的自訂網域 toohave hello 自己的應用程式的相同內部和外部 Url。</span><span class="sxs-lookup"><span data-stu-id="e694f-114">hello link translation feature is for tenants that, for whatever reason, can't use custom domains toohave hello same internal and external URLs for their apps.</span></span> <span data-ttu-id="e694f-115">在您啟用這項功能之前，請查看您是否適用 [Azure AD Application Proxy 中的自訂網域](active-directory-application-proxy-custom-domains.md)。</span><span class="sxs-lookup"><span data-stu-id="e694f-115">Before you enable this feature, see if [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) can work for you.</span></span>
>
><span data-ttu-id="e694f-116">或者，如果您需要與連結轉譯 tooconfigure hello 應用程式是 SharePoint，請參閱[設定適用於 SharePoint 2013 的備用存取對應](https://technet.microsoft.com/library/cc263208.aspx)的另一個方法 toomapping 連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-116">Or, if hello application you need tooconfigure with link translation is SharePoint, see [Configure alternate access mappings for SharePoint 2013](https://technet.microsoft.com/library/cc263208.aspx) for another approach toomapping links.</span></span>

## <a name="how-link-translation-works"></a><span data-ttu-id="e694f-117">連結轉譯的運作方式</span><span class="sxs-lookup"><span data-stu-id="e694f-117">How link translation works</span></span>

<span data-ttu-id="e694f-118">在驗證之後，當 hello proxy 伺服器傳遞 hello 應用程式資料 toohello 使用者應用程式 Proxy 掃描 hello 應用程式的硬式編碼的連結，然後將它們取代為其各自發行外部 Url。</span><span class="sxs-lookup"><span data-stu-id="e694f-118">After authentication, when hello proxy server passes hello application data toohello user, Application Proxy scans hello application for hardcoded links and replaces them with their respective, published external URLs.</span></span>

<span data-ttu-id="e694f-119">應用程式 Proxy 假設應用程式是以 UTF-8 編碼。</span><span class="sxs-lookup"><span data-stu-id="e694f-119">Application Proxy assumes that applications are encoded in UTF-8.</span></span> <span data-ttu-id="e694f-120">如果不是 hello 案例，hello 編碼類型中指定 http 回應標頭，例如`Content-Type:text/html;charset=utf-8`。</span><span class="sxs-lookup"><span data-stu-id="e694f-120">If that's not hello case, specify hello encoding type in an http response header, like `Content-Type:text/html;charset=utf-8`.</span></span>

### <a name="which-links-are-affected"></a><span data-ttu-id="e694f-121">哪些連結會受影響？</span><span class="sxs-lookup"><span data-stu-id="e694f-121">Which links are affected?</span></span>

<span data-ttu-id="e694f-122">hello 連結轉譯功能只會尋找 hello 主體的應用程式中的程式碼標記中的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-122">hello link translation feature only looks for links that are in code tags in hello body of an app.</span></span> <span data-ttu-id="e694f-123">Application Proxy 有個別功能可轉譯標頭中的 cookie 或 URL。</span><span class="sxs-lookup"><span data-stu-id="e694f-123">Application Proxy has a separate feature for translating cookies or URLs in headers.</span></span> 

<span data-ttu-id="e694f-124">內部部署應用程式中有兩種常見的內部連結類型：</span><span class="sxs-lookup"><span data-stu-id="e694f-124">There are two common types of internal links in on-premises applications:</span></span>

- <span data-ttu-id="e694f-125">**相對的內部連結**該點 tooa 共用類似的本機檔案結構中的資源`/claims/claims.html`。</span><span class="sxs-lookup"><span data-stu-id="e694f-125">**Relative internal links** that point tooa shared resource in a local file structure like `/claims/claims.html`.</span></span> <span data-ttu-id="e694f-126">這些連結會自動運作中應用程式，透過應用程式 Proxy 發佈，並繼續 toowork 不論連結轉譯。</span><span class="sxs-lookup"><span data-stu-id="e694f-126">These links automatically work in apps that are published through Application Proxy, and continue toowork with or without link translation.</span></span> 
- <span data-ttu-id="e694f-127">**硬式編碼內部連結**tooother 內部部署應用程式，例如`http://expenses`或發行檔案，像是`http://expenses/logo.jpg`。</span><span class="sxs-lookup"><span data-stu-id="e694f-127">**Hardcoded internal links** tooother on-premises apps like `http://expenses` or published files like `http://expenses/logo.jpg`.</span></span> <span data-ttu-id="e694f-128">hello 連結轉譯功能適用於內部連結硬式編碼，，而且會將其變更 toopoint toohello 外部 Url 的遠端使用者需要透過 toogo。</span><span class="sxs-lookup"><span data-stu-id="e694f-128">hello link translation feature works on hardcoded internal links, and changes them toopoint toohello external URLs that remote users need toogo through.</span></span>

### <a name="how-do-apps-link-tooeach-other"></a><span data-ttu-id="e694f-129">應用程式如何連結其他 tooeach？</span><span class="sxs-lookup"><span data-stu-id="e694f-129">How do apps link tooeach other?</span></span>

<span data-ttu-id="e694f-130">連結轉譯每個應用程式，啟用，所以您需要在 hello 個別應用程式層級的控制 hello 使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="e694f-130">Link translation is enabled for each application, so that you have control over hello user experience at hello per-app level.</span></span> <span data-ttu-id="e694f-131">開啟連結轉譯為應用程式時想要讓 hello 連結*從*該應用程式 toobe 轉譯，不是連結*至*該應用程式。</span><span class="sxs-lookup"><span data-stu-id="e694f-131">Turn on link translation for an app when you want hello links *from* that app toobe translated, not links *to* that app.</span></span> 

<span data-ttu-id="e694f-132">例如，假設您有三個透過所有連結 tooeach 其他的應用程式 Proxy 發行的應用程式： 效益、 費用和移動。</span><span class="sxs-lookup"><span data-stu-id="e694f-132">For example, suppose that you have three applications published through Application Proxy that all link tooeach other: Benefits, Expenses, and Travel.</span></span> <span data-ttu-id="e694f-133">第四個應用程式 (Feedback) 不是透過 Application Proxy 發佈。</span><span class="sxs-lookup"><span data-stu-id="e694f-133">There's a fourth app, Feedback, that isn't published through Application Proxy.</span></span>

<span data-ttu-id="e694f-134">當您啟用 hello 優點的應用程式的連結轉譯時，hello 連結 tooExpenses 和旅行重新導向的 toohello 外部 Url，針對這些應用程式，但由於沒有外部 URL hello 連結 tooFeedback 不重新導向。</span><span class="sxs-lookup"><span data-stu-id="e694f-134">When you enable link translation for hello Benefits app, hello links tooExpenses and Travel are redirected toohello external URLs for those apps, but hello link tooFeedback is not redirected because there is no external URL.</span></span> <span data-ttu-id="e694f-135">從費用及移動後 tooBenefits 沒有作用，因為尚未啟用連結轉譯這些兩個應用程式的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-135">Links from Expenses and Travel back tooBenefits don't work, because link translation has not been enabled for those two apps.</span></span>

![從啟用連結轉譯時的優點 tooother 應用程式的連結](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a><span data-ttu-id="e694f-137">哪些連結並未轉譯？</span><span class="sxs-lookup"><span data-stu-id="e694f-137">Which links aren't translated?</span></span>

<span data-ttu-id="e694f-138">某些連結 tooimprove 效能和安全性，無法轉譯：</span><span class="sxs-lookup"><span data-stu-id="e694f-138">tooimprove performance and security, some links aren't translated:</span></span>

- <span data-ttu-id="e694f-139">不在程式碼標籤內的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-139">Links not inside of code tags.</span></span> 
- <span data-ttu-id="e694f-140">不在 HTML、CSS 或 JavaScript 中的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-140">Links not in HTML, CSS, or JavaScript.</span></span> 
- <span data-ttu-id="e694f-141">從其他程式開啟的內部連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-141">Internal links opened from other programs.</span></span> <span data-ttu-id="e694f-142">不會轉譯透過電子郵件或立即訊息傳送的連結，或包含在其他文件中的連結。</span><span class="sxs-lookup"><span data-stu-id="e694f-142">Links sent through email or instant message, or included in other documents, won't be translated.</span></span> <span data-ttu-id="e694f-143">hello 使用者需要 tooknow toogo toohello 外部 URL。</span><span class="sxs-lookup"><span data-stu-id="e694f-143">hello users need tooknow toogo toohello external URL.</span></span>

<span data-ttu-id="e694f-144">如果您需要 toosupport 這些兩種情況下，使用 hello 相同內部和外部 Url，而不是連結轉譯。</span><span class="sxs-lookup"><span data-stu-id="e694f-144">If you need toosupport one of these two scenarios, use hello same internal and external URLs instead of link translation.</span></span>  

## <a name="enable-link-translation"></a><span data-ttu-id="e694f-145">啟用連結轉譯</span><span class="sxs-lookup"><span data-stu-id="e694f-145">Enable link translation</span></span>

<span data-ttu-id="e694f-146">開始使用連結轉譯很簡單，按一下按鈕即可：</span><span class="sxs-lookup"><span data-stu-id="e694f-146">Getting started with link translation is as easy as clicking a button:</span></span>

1. <span data-ttu-id="e694f-147">登入 toohello [Azure 入口網站](https://portal.azure.com)身為系統管理員。</span><span class="sxs-lookup"><span data-stu-id="e694f-147">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="e694f-148">跳過**Azure Active Directory** > **企業應用程式** > **所有應用程式**> 選取 hello 應用程式想 toomanage >**應用程式 proxy**。</span><span class="sxs-lookup"><span data-stu-id="e694f-148">Go too**Azure Active Directory** > **Enterprise applications** > **All applications** > select hello app you want toomanage > **Application proxy**.</span></span>
3. <span data-ttu-id="e694f-149">開啟**應用程式主體中的 轉譯 Url**太**是**。</span><span class="sxs-lookup"><span data-stu-id="e694f-149">Turn **Translate URLs in application body** too**Yes**.</span></span>

   ![應用程式主體中選取 [是] tootranslate Url](./media/application-proxy-link-translation/select_yes.png)<span data-ttu-id="e694f-151">.</span><span class="sxs-lookup"><span data-stu-id="e694f-151">.</span></span>
4. <span data-ttu-id="e694f-152">選取**儲存**tooapply 您的變更。</span><span class="sxs-lookup"><span data-stu-id="e694f-152">Select **Save** tooapply your changes.</span></span>

<span data-ttu-id="e694f-153">現在，當您的使用者存取此應用程式，hello proxy 會自動掃描已透過應用程式 Proxy 發佈在租用戶的內部 Url。</span><span class="sxs-lookup"><span data-stu-id="e694f-153">Now, when your users access this application, hello proxy will automatically scan for internal URLs that have been published through Application Proxy on your tenant.</span></span>

## <a name="send-feedback"></a><span data-ttu-id="e694f-154">傳送意見反應</span><span class="sxs-lookup"><span data-stu-id="e694f-154">Send feedback</span></span>

<span data-ttu-id="e694f-155">我們想要說明 toomake 這項功能工作的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="e694f-155">We want your help toomake this feature work for all your apps.</span></span> <span data-ttu-id="e694f-156">我們以 HTML 和 CSS，搜尋超過 30 的標記，並考慮哪些 JavaScript 案例 toosupport。</span><span class="sxs-lookup"><span data-stu-id="e694f-156">We search over 30 tags in HTML and CSS, and are considering which JavaScript cases toosupport.</span></span> <span data-ttu-id="e694f-157">如果您有不要翻譯的產生連結的範例，傳送程式碼片段太[應用程式 Proxy 的意見反應](mailto:aadapfeedback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="e694f-157">If you have an example of generated links that aren't being translated, send a code snippet too[Application Proxy Feedback](mailto:aadapfeedback@microsoft.com).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e694f-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e694f-158">Next steps</span></span>
<span data-ttu-id="e694f-159">[自訂網域搭配 Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) toohave hello 相同的內部和外部 URL</span><span class="sxs-lookup"><span data-stu-id="e694f-159">[Use custom domains with Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md) toohave hello same internal and external URL</span></span>

[<span data-ttu-id="e694f-160">設定 SharePoint 2013 的備用存取對應</span><span class="sxs-lookup"><span data-stu-id="e694f-160">Configure alternate access mappings for SharePoint 2013</span></span>](https://technet.microsoft.com/library/cc263208.aspx)
