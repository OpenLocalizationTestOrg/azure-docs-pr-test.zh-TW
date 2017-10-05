---
title: "Application Proxy 應用程式的應用程式頁面未正確顯示 | Microsoft Docs"
description: "當頁面在已與 Azure AD 整合的 Application Proxy 應用程式中未正確顯示時的指引"
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
ms.openlocfilehash: cac4c333e59ef9a0f28a2f93a7afee22eeafd54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a><span data-ttu-id="9212a-103">Application Proxy 應用程式的應用程式頁面未正確顯示</span><span class="sxs-lookup"><span data-stu-id="9212a-103">Application page does not display correctly for an Application Proxy application</span></span>

<span data-ttu-id="9212a-104">這篇文章可在您瀏覽至應用程式頁面，但該頁面有些內容未正確顯示時，協助您為 Azure Active Directory Application Proxy 應用程式的問題疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9212a-104">This article help you to troubleshoot issues with Azure Active Directory Application Proxy applications when you navigate to the page, but something on the page doesn't look correct.</span></span>

## <a name="overview"></a><span data-ttu-id="9212a-105">概觀</span><span class="sxs-lookup"><span data-stu-id="9212a-105">Overview</span></span>
<span data-ttu-id="9212a-106">當您發佈 Application Proxy 應用程式時，在存取該應用程式時只有您根目錄下的頁面才可供存取。</span><span class="sxs-lookup"><span data-stu-id="9212a-106">When you publish an Application Proxy app, only pages under your root are accessible when accessing the application.</span></span> <span data-ttu-id="9212a-107">如果頁面未正確顯示，則用於該應用程式的根目錄內部 URL 可能遺漏某些頁面資源。</span><span class="sxs-lookup"><span data-stu-id="9212a-107">If the page isn’t displaying correctly, the root internal URL used for the application may be missing some page resources.</span></span> <span data-ttu-id="9212a-108">若要解決此問題，請確定您已發佈該頁面的*所有*資源做為您應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="9212a-108">To resolve, make sure you have published *all* the resources for the page as part of your application.</span></span>

<span data-ttu-id="9212a-109">您可以開啟網路追蹤程式 (例如 Fiddler，或 Internet Explorer/Edge 中的 F12 工具)，載入頁面，然後尋找 404 錯誤，來驗證這就是問題。</span><span class="sxs-lookup"><span data-stu-id="9212a-109">You can verify this is the issue by opening your network tracker (such as Fiddler, or F12 tools in Internet Explorer/Edge), loading the page, and looking for 404 errors.</span></span> <span data-ttu-id="9212a-110">此錯誤表示該頁面目前找不到，且可能仍然需要發佈。</span><span class="sxs-lookup"><span data-stu-id="9212a-110">That indicates the pages that currently cannot be found and may still need to be published.</span></span>

<span data-ttu-id="9212a-111">以此案例為例，假設您已使用 <http://myapps/expenses> 的內部 URL 發佈一個費用應用程式，但該應用程式使用樣式表 <http://myapps/style.css>。</span><span class="sxs-lookup"><span data-stu-id="9212a-111">As an example of this case, assume you have published an expenses application using an internal URL of <http://myapps/expenses>, but the app uses the stylesheet <http://myapps/style.css>.</span></span> <span data-ttu-id="9212a-112">在此狀況下，該樣式表未在您的應用程式中發佈，因此若載入費用應用程式，則會在嘗試載入 style.css 時擲回 404 錯誤。</span><span class="sxs-lookup"><span data-stu-id="9212a-112">In this case, the stylesheet is not published in your application, so loading the expenses app throw a 404 error while trying to load style.css.</span></span> <span data-ttu-id="9212a-113">在此範例中，改用 <http://myapp/> 的內部 URL 發佈應用程式，就能解決問題。</span><span class="sxs-lookup"><span data-stu-id="9212a-113">In this example, the problem would be resolved by publishing the application with an internal URL of <http://myapp/> instead.</span></span>

## <a name="problems-with-publishing-as-one-application"></a><span data-ttu-id="9212a-114">發佈為一個應用程式時的問題</span><span class="sxs-lookup"><span data-stu-id="9212a-114">Problems with publishing as one application</span></span>

<span data-ttu-id="9212a-115">如果無法在同一個應用程式內發佈所有的資源，您必須發佈多個應用程式，並啟用之間的連結。</span><span class="sxs-lookup"><span data-stu-id="9212a-115">If it is not possible to publish all resources within the same application, you need to publish multiple applications and enable links between them.</span></span>

<span data-ttu-id="9212a-116">若要這樣做，我們建議使用[自訂網域](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)解決方案。</span><span class="sxs-lookup"><span data-stu-id="9212a-116">To do so, we recommend using the [custom domains](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solution.</span></span> <span data-ttu-id="9212a-117">不過，此解決方案需要您擁有您網域的憑證，且您的應用程式使用完整的網域名稱 (FQDN)。</span><span class="sxs-lookup"><span data-stu-id="9212a-117">However, this solution requires that you own the certificate for your domain and your applications use fully qualified domain names (FQDNs).</span></span> <span data-ttu-id="9212a-118">如需其他選項，請參閱[為連結中斷的文件疑難排解](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1)。</span><span class="sxs-lookup"><span data-stu-id="9212a-118">For other options, see the [troubleshoot broken links documentation](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9212a-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9212a-119">Next steps</span></span>
[<span data-ttu-id="9212a-120">使用 Azure AD 應用程式 Proxy 發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="9212a-120">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
