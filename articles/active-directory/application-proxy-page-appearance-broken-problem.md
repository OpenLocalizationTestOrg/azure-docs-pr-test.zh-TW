---
title: "應用程式 Proxy 應用程式的 aaaApplication 頁面不會正確顯示 |Microsoft 文件"
description: "Hello 網頁未正確顯示在 應用程式 Proxy 應用程式的指引您有與 Azure AD 整合"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="dd349-103">Application Proxy 應用程式的應用程式頁面未正確顯示</span><span class="sxs-lookup"><span data-stu-id="dd349-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="dd349-104">本文章協助 tootroubleshoot 與 Azure Active Directory 應用程式 Proxy 應用程式的問題時您瀏覽 toohello 頁面上，但在 hello 頁面上的項目看起來不正確。</span><span class="sxs-lookup"><span data-stu-id="dd349-104">This article help you tootroubleshoot issues with Azure Active Directory Application Proxy applications when you navigate toohello page, but something on hello page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="dd349-105">概觀</span><span class="sxs-lookup"><span data-stu-id="dd349-105">Overview</span></span>
<span data-ttu-id="dd349-106">當您發行應用程式 Proxy 應用程式時，只有在您的根目錄下的頁面存取 hello 應用程式時有可存取。</span><span class="sxs-lookup"><span data-stu-id="dd349-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing hello application.</span></span> <span data-ttu-id="dd349-107">如果沒有正確地顯示 hello 頁面，hello 根目錄內部 URL 用於 hello 應用程式可能會遺失一些頁面資源。</span><span class="sxs-lookup"><span data-stu-id="dd349-107">If hello page isn’t displaying correctly, hello root internal URL used for hello application may be missing some page resources.</span></span> <span data-ttu-id="dd349-108">tooresolve，請確定您已發行*所有*hello hello 頁面的資源做為您的應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="dd349-108">tooresolve, make sure you have published *all* hello resources for hello page as part of your application.</span></span>

<span data-ttu-id="dd349-109">您可以確認這是藉由開啟網路追蹤的 hello 問題 (例如 Fiddler 或 F12 工具 Internet Explorer/Edge)、 載入 hello 頁面上，並尋找 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="dd349-109">You can verify this is hello issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading hello page, and looking for 404 errors.</span></span> <span data-ttu-id="dd349-110">指出目前找不到，可能仍然需要 toobe 發行的 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="dd349-110">That indicates hello pages that currently cannot be found and may still need toobe published.</span></span>

<span data-ttu-id="dd349-111">此案例的範例，假設您已經發行費用應用程式使用的內部 URL <http://myapps/expenses>，但是 hello 應用程式會使用 hello 樣式表<http://myapps/style.css>。</span><span class="sxs-lookup"><span data-stu-id="dd349-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but hello app uses hello stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="dd349-112">在此情況下，hello 樣式表不在發行您的應用程式，因此載入 hello 費用應用程式擲回時嘗試 tooload style.css 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="dd349-112">In this case, hello stylesheet is not published in your application, so loading hello expenses app throw a 404 error while trying tooload style.css.</span></span> <span data-ttu-id="dd349-113">在此範例中，會解決 hello 問題發佈 hello 應用程式的內部 url <http://myapp/>改為。</span><span class="sxs-lookup"><span data-stu-id="dd349-113">In this example, hello problem would be resolved by publishing hello application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="dd349-114">發佈為一個應用程式時的問題</span><span class="sxs-lookup"><span data-stu-id="dd349-114">Problems with publishing as one application</span></span>

<span data-ttu-id="dd349-115">如果不可能 toopublish 中的所有資源都 hello 相同的應用程式，您需要 toopublish 多個應用程式，並啟用它們之間的連結。</span><span class="sxs-lookup"><span data-stu-id="dd349-115">If it is not possible toopublish all resources within hello same application, you need toopublish multiple applications and enable links between them.</span></span>

<span data-ttu-id="dd349-116">toodo 如此，我們建議使用 hello[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)方案。</span><span class="sxs-lookup"><span data-stu-id="dd349-116">toodo so, we recommend using hello [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="dd349-117">不過，此解決方案需要您的網域擁有 hello 憑證，您的應用程式可使用完整的網域名稱 (Fqdn)。</span><span class="sxs-lookup"><span data-stu-id="dd349-117">However, this solution requires that you own hello certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="dd349-118">如需其他選項，請參閱 hello[疑難排解中斷的連結文件](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1)。</span><span class="sxs-lookup"><span data-stu-id="dd349-118">For other options, see hello [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd349-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dd349-119">Next steps</span></span>
[<span data-ttu-id="dd349-120">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="dd349-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
