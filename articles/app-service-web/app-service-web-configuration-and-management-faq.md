---
title: "Azure web 應用程式的 aaaConfiguration 常見問題集 |Microsoft 文件"
description: "取得要求 hello Azure App Service Web 應用程式功能組態與管理問題的相關問題的答案 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a><span data-ttu-id="7f3de-103">Azure 中 Web 應用程式的設定和管理常見問題集</span><span class="sxs-lookup"><span data-stu-id="7f3de-103">Configuration and management FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="7f3de-104">這篇文章有解答 toofrequently 集 (Faq) 設定和管理問題的相關 hello [Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-104">This article has answers toofrequently asked questions (FAQs) about configuration and management issues for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a><span data-ttu-id="7f3de-105">有我應該了解如果想 toomove 應用程式服務資源的限制嗎？</span><span class="sxs-lookup"><span data-stu-id="7f3de-105">Are there limitations I should be aware of if I want toomove App Service resources?</span></span>

<span data-ttu-id="7f3de-106">如果您計劃 toomove App Service 資源 tooa 新資源群組或訂用帳戶，有一些限制 toobe 留意。</span><span class="sxs-lookup"><span data-stu-id="7f3de-106">If you plan toomove App Service resources tooa new resource group or subscription, there are a few limitations toobe aware of.</span></span> <span data-ttu-id="7f3de-107">如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-107">For more information, see [App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).</span></span>

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a><span data-ttu-id="7f3de-108">如何針對 Web 應用程式使用自訂網域名稱？</span><span class="sxs-lookup"><span data-stu-id="7f3de-108">How do I use a custom domain name for my web app?</span></span>

<span data-ttu-id="7f3de-109">如需搭配使用的自訂網域名稱與您的 Azure web 應用程式，答案 toocommon 問題，請參閱我們七個分鐘的影片[新增自訂網域名稱](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-109">For answers toocommon questions about using a custom domain name with your Azure web app, see our seven-minute video [Add a custom domain name](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name).</span></span> <span data-ttu-id="7f3de-110">hello 視訊提供逐步解說，如何 tooadd 自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7f3de-110">hello video offers a walkthrough of how tooadd a custom domain name.</span></span> <span data-ttu-id="7f3de-111">它會描述如何 toouse 自己的 URL，而不是 hello *。 使用您的 App Service web 應用程式的名稱是.azurewebsites.net URL。</span><span class="sxs-lookup"><span data-stu-id="7f3de-111">It describes how toouse your own URL instead of hello *.azurewebsites.net URL with your App Service web app.</span></span> <span data-ttu-id="7f3de-112">您也可以看到的詳細逐步解說[如何 toomap 自訂網域名稱](web-sites-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-112">You also can see a detailed walkthrough of [how toomap a custom domain name](web-sites-custom-domain-name.md).</span></span>


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a><span data-ttu-id="7f3de-113">如何為 Web 應用程式購買新的自訂網域？</span><span class="sxs-lookup"><span data-stu-id="7f3de-113">How do I purchase a new custom domain for my web app?</span></span>

<span data-ttu-id="7f3de-114">如何 toopurchase 及設定自訂網域，以您的 App Service web 應用程式，請參閱的 toolearn[購買並設定應用程式服務中的自訂網域名稱](custom-dns-web-site-buydomains-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-114">toolearn how toopurchase and set up a custom domain for your App Service web app, see [Buy and configure a custom domain name in App Service](custom-dns-web-site-buydomains-web-app.md).</span></span>


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a><span data-ttu-id="7f3de-115">如何上傳及設定 Web 應用程式的現有 SSL 憑證？</span><span class="sxs-lookup"><span data-stu-id="7f3de-115">How do I upload and configure an existing SSL certificate for my web app?</span></span>

<span data-ttu-id="7f3de-116">如何 tooupload 及設定現有的自訂 SSL 憑證，請參閱的 toolearn[繫結現有自訂 SSL 憑證 tooan Azure web 應用程式](app-service-web-tutorial-custom-ssl.md#upload)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-116">toolearn how tooupload and set up an existing custom SSL certificate, see [Bind an existing custom SSL certificate tooan Azure web app](app-service-web-tutorial-custom-ssl.md#upload).</span></span>


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a><span data-ttu-id="7f3de-117">如何購買 Web 應用程式的新 SSL 憑證並且在 Azure 中設定？</span><span class="sxs-lookup"><span data-stu-id="7f3de-117">How do I purchase and configure a new SSL certificate in Azure for my web app?</span></span>

<span data-ttu-id="7f3de-118">如何 toopurchase 及設定 SSL 憑證的 App Service web 應用程式，請參閱的 toolearn[新增 App Service 應用程式的 SSL 憑證 tooyour](web-sites-purchase-ssl-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-118">toolearn how toopurchase and set up an SSL certificate for your App Service web app, see [Add an SSL certificate tooyour App Service app](web-sites-purchase-ssl-web-site.md).</span></span>


## <a name="how-do-i-move-application-insights-resources"></a><span data-ttu-id="7f3de-119">如何移動 Application Insights 資源？</span><span class="sxs-lookup"><span data-stu-id="7f3de-119">How do I move Application Insights resources?</span></span>

<span data-ttu-id="7f3de-120">目前，Azure Application Insights 並不支援 hello 移動作業。</span><span class="sxs-lookup"><span data-stu-id="7f3de-120">Currently, Azure Application Insights doesn't support hello move operation.</span></span> <span data-ttu-id="7f3de-121">如果您的原始資源群組包含 Application Insights 資源，則您無法移動該資源。</span><span class="sxs-lookup"><span data-stu-id="7f3de-121">If your original resource group includes an Application Insights resource, you cannot move that resource.</span></span> <span data-ttu-id="7f3de-122">如果您包含 hello Application Insights 資源，當您嘗試 toomove App Service 應用程式時，整個 hello 移動操作失敗。</span><span class="sxs-lookup"><span data-stu-id="7f3de-122">If you include hello Application Insights resource when you try toomove an App Service app, hello entire move operation fails.</span></span> <span data-ttu-id="7f3de-123">不過，Application Insights 和 hello 應用程式服務計劃不需要在 toobe hello 與 hello 應用程式 toofunction 的 hello 應用程式的相同資源群組正確。</span><span class="sxs-lookup"><span data-stu-id="7f3de-123">However, Application Insights and hello App Service plan do not need toobe in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="7f3de-124">如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-124">For more information, see [App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).</span></span>

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a><span data-ttu-id="7f3de-125">可以在哪裡尋找指引檢查清單及深入了解資源移動作業？</span><span class="sxs-lookup"><span data-stu-id="7f3de-125">Where can I find a guidance checklist and learn more about resource move operations?</span></span>

<span data-ttu-id="7f3de-126">[應用程式服務限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)示範如何 toomove 資源 tooeither 新的訂用帳戶或 tooa 新資源群組中 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7f3de-126">[App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) shows you how toomove resources tooeither a new subscription or tooa new resource group in hello same subscription.</span></span> <span data-ttu-id="7f3de-127">您可以取得 hello 資源移動檢查清單的相關資訊，了解哪些服務支援 hello 移動作業，以及深入了解應用程式服務限制與其他主題。</span><span class="sxs-lookup"><span data-stu-id="7f3de-127">You can get information about hello resource move checklist, learn which services support hello move operation, and learn more about App Service limitations and other topics.</span></span>

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a><span data-ttu-id="7f3de-128">如何在我的 web 應用程式設定 hello 伺服器時區？</span><span class="sxs-lookup"><span data-stu-id="7f3de-128">How do I set hello server time zone for my web app?</span></span>

<span data-ttu-id="7f3de-129">tooset hello 伺服器時區 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="7f3de-129">tooset hello server time zone for your web app:</span></span>

1. <span data-ttu-id="7f3de-130">在 hello 您應用程式服務的訂閱，在 Azure 入口網站移 toohello**應用程式設定**功能表。</span><span class="sxs-lookup"><span data-stu-id="7f3de-130">In hello Azure portal, in your App Service subscription, go toohello **Application settings** menu.</span></span>
2. <span data-ttu-id="7f3de-131">在 [應用程式設定] 底下，新增以下設定：</span><span class="sxs-lookup"><span data-stu-id="7f3de-131">Under **App settings**, add this setting:</span></span>
    * <span data-ttu-id="7f3de-132">索引鍵 = WEBSITE_TIME_ZONE</span><span class="sxs-lookup"><span data-stu-id="7f3de-132">Key = WEBSITE_TIME_ZONE</span></span>
    * <span data-ttu-id="7f3de-133">值 =*您想要的 hello 時區*</span><span class="sxs-lookup"><span data-stu-id="7f3de-133">Value = *hello time zone you want*</span></span>
3. <span data-ttu-id="7f3de-134">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="7f3de-134">Select **Save**.</span></span>

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a><span data-ttu-id="7f3de-135">為什麼我的持續 WebJobs 有時候會失敗？</span><span class="sxs-lookup"><span data-stu-id="7f3de-135">Why do my continuous WebJobs sometimes fail?</span></span>

<span data-ttu-id="7f3de-136">根據預設，Web 應用程式如果閒置一段時間，就會卸載。</span><span class="sxs-lookup"><span data-stu-id="7f3de-136">By default, web apps are unloaded if they are idle for a set period of time.</span></span> <span data-ttu-id="7f3de-137">這可讓 hello 系統節省資源。</span><span class="sxs-lookup"><span data-stu-id="7f3de-137">This lets hello system conserve resources.</span></span> <span data-ttu-id="7f3de-138">在基本和標準計畫中，您可以開啟 hello **Always On**設定 tookeep hello web 應用程式載入所有 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="7f3de-138">In Basic and Standard plans, you can turn on hello **Always On** setting tookeep hello web app loaded all hello time.</span></span> <span data-ttu-id="7f3de-139">如果您的 web 應用程式執行連續 web 工作，您應該開啟**Always On**，或 hello WebJobs 可能無法可靠地執行。</span><span class="sxs-lookup"><span data-stu-id="7f3de-139">If your web app runs continuous WebJobs, you should turn on **Always On**, or hello WebJobs might not run reliably.</span></span> <span data-ttu-id="7f3de-140">如需詳細資訊，請參閱[建立持續執行 WebJob](web-sites-create-web-jobs.md#CreateContinuous)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-140">For more information, see [Create a continuously running WebJob](web-sites-create-web-jobs.md#CreateContinuous).</span></span>

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a><span data-ttu-id="7f3de-141">如何在我的 web 應用程式取得 hello 輸出的 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="7f3de-141">How do I get hello outbound IP address for my web app?</span></span>

<span data-ttu-id="7f3de-142">tooget hello 的 web 應用程式傳出的 IP 位址的清單：</span><span class="sxs-lookup"><span data-stu-id="7f3de-142">tooget hello list of outbound IP addresses for your web app:</span></span>

1. <span data-ttu-id="7f3de-143">在 [hello Azure 入口網站，在您 web 應用程式] 刀鋒視窗中，移 toohello**屬性**功能表。</span><span class="sxs-lookup"><span data-stu-id="7f3de-143">In hello Azure portal, on your web app blade, go toohello **Properties** menu.</span></span>
2. <span data-ttu-id="7f3de-144">搜尋**輸出 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="7f3de-144">Search for **outbound ip addresses**.</span></span>

<span data-ttu-id="7f3de-145">hello 輸出的 IP 位址清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7f3de-145">hello list of outbound IP addresses appears.</span></span>

<span data-ttu-id="7f3de-146">如果您的網站裝載在 App Service 環境 powerapps，toolearn 如何 tooget 輸出的 IP 位址，請參閱[傳出的網路位址](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-146">If your website is hosted in App Service Environment for PowerApps, toolearn how tooget your outbound IP address, see [Outbound network addresses](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).</span></span>

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a><span data-ttu-id="7f3de-147">如何為 Web 應用程式取得保留或專用輸入 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="7f3de-147">How do I get a reserved or dedicated inbound IP address for my web app?</span></span>

<span data-ttu-id="7f3de-148">傳入呼叫時進行 tooyour Azure 應用程式網站的專用或保留 IP 位址的 tooset 安裝並設定以 IP 為主的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="7f3de-148">tooset up a dedicated or reserved IP address for inbound calls made tooyour Azure app website, install and configure an IP-based SSL certificate.</span></span>

<span data-ttu-id="7f3de-149">請注意該 toouse 專用或進行傳入呼叫時的保留的 IP 位址，您的應用程式服務方案必須在基本或更高版本的服務方案中。</span><span class="sxs-lookup"><span data-stu-id="7f3de-149">Note that toouse a dedicated or reserved IP address for inbound calls, your App Service plan must be in a Basic or higher service plan.</span></span>

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a><span data-ttu-id="7f3de-150">例如，對於網站裝載其他地方可以匯出外部 Azure 中，我 App Service 憑證 toouse 嗎？</span><span class="sxs-lookup"><span data-stu-id="7f3de-150">Can I export my App Service certificate toouse outside Azure, such as for a website hosted elsewhere?</span></span> 

<span data-ttu-id="7f3de-151">App Service 憑證被視為 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="7f3de-151">App Service certificates are considered Azure resources.</span></span> <span data-ttu-id="7f3de-152">它們不是預期的 toouse 超出您的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="7f3de-152">They are not intended toouse outside your Azure services.</span></span> <span data-ttu-id="7f3de-153">您無法將它們匯出 toouse Azure 外部。</span><span class="sxs-lookup"><span data-stu-id="7f3de-153">You cannot export them toouse outside Azure.</span></span> <span data-ttu-id="7f3de-154">如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-154">For more information, see [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).</span></span>

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a><span data-ttu-id="7f3de-155">我可以匯出我與其他 Azure 雲端服務的應用程式服務憑證 toouse 嗎？</span><span class="sxs-lookup"><span data-stu-id="7f3de-155">Can I export my App Service certificate toouse with other Azure cloud services?</span></span>

<span data-ttu-id="7f3de-156">hello 入口網站提供部署的 App Service 憑證，透過 Azure 金鑰保存庫 tooApp 服務應用程式第一級的體驗。</span><span class="sxs-lookup"><span data-stu-id="7f3de-156">hello portal provides a first-class experience for deploying an App Service certificate through Azure Key Vault tooApp Service apps.</span></span> <span data-ttu-id="7f3de-157">不過，我們已經收到來自客戶 toouse 要求外 hello 應用程式服務的平台，這些憑證，例如使用 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7f3de-157">However, we have been receiving requests from customers toouse these certificates outside hello App Service platform, for example, with Azure Virtual Machines.</span></span> <span data-ttu-id="7f3de-158">toolearn 如何 toocreate 應用程式服務的本機複本 PFX 憑證讓您可以使用 hello 憑證與其他 Azure 資源，請參閱[建立本機應用程式服務憑證 PFX 複本](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-158">toolearn how toocreate a local PFX copy of your App Service certificate so you can use hello certificate with other Azure resources, see [Create a local PFX copy of an App Service certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span></span>

<span data-ttu-id="7f3de-159">如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-159">For more information, see [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).</span></span>


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a><span data-ttu-id="7f3de-160">為什麼當我嘗試 tooback 設定我的 web 應用程式時看到 「 部分成功 」 的 hello 訊息？</span><span class="sxs-lookup"><span data-stu-id="7f3de-160">Why do I see hello message "Partially Succeeded" when I try tooback up my web app?</span></span>

<span data-ttu-id="7f3de-161">備份失敗的常見原因是，某些檔案正在使用中的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f3de-161">A common cause of backup failure is that some files are in use by hello application.</span></span> <span data-ttu-id="7f3de-162">您執行 hello 備份使用中的檔案都會被鎖定。</span><span class="sxs-lookup"><span data-stu-id="7f3de-162">Files that are in use are locked while you perform hello backup.</span></span> <span data-ttu-id="7f3de-163">這樣會避免這些檔案進行備份，因此可能導致「部分成功」狀態。</span><span class="sxs-lookup"><span data-stu-id="7f3de-163">This prevents these files from being backed up and might result in a "Partially Succeeded" status.</span></span> <span data-ttu-id="7f3de-164">您可以有可能避免發生此 hello 備份程序從排除的檔案。</span><span class="sxs-lookup"><span data-stu-id="7f3de-164">You can potentially prevent this from occurring by excluding files from hello backup process.</span></span> <span data-ttu-id="7f3de-165">您可以選擇 tooback 向上僅需要什麼。</span><span class="sxs-lookup"><span data-stu-id="7f3de-165">You can choose tooback up only what is needed.</span></span> <span data-ttu-id="7f3de-166">如需詳細資訊，請參閱[備份只 hello 的重要部分您 Azure web 應用程式的站台](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-166">For more information, see [Backup just hello important parts of your site with Azure web apps](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).</span></span>

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a><span data-ttu-id="7f3de-167">如何移除從 hello HTTP 回應的標頭？</span><span class="sxs-lookup"><span data-stu-id="7f3de-167">How do I remove a header from hello HTTP response?</span></span>

<span data-ttu-id="7f3de-168">從 HTTP 回應 hello tooremove hello 標頭會更新網站的 web.config 檔。</span><span class="sxs-lookup"><span data-stu-id="7f3de-168">tooremove hello headers from hello HTTP response, update your site’s web.config file.</span></span> <span data-ttu-id="7f3de-169">如需詳細資訊，請參閱[在 Azure 網站上移除標準伺服器標題](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-169">For more information, see [Remove standard server headers on your Azure websites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).</span></span>

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a><span data-ttu-id="7f3de-170">App Service 是否符合 PCI 標準 3.0 和 3.1 的規範？</span><span class="sxs-lookup"><span data-stu-id="7f3de-170">Is App Service compliant with PCI Standard 3.0 and 3.1?</span></span>

<span data-ttu-id="7f3de-171">目前，hello Azure App Service Web 應用程式功能是符合 PCI 資料安全標準 (DSS) 版本 3.0 層級 1。</span><span class="sxs-lookup"><span data-stu-id="7f3de-171">Currently, hello Web Apps feature of Azure App Service is in compliance with PCI Data Security Standard (DSS) version 3.0 Level 1.</span></span> <span data-ttu-id="7f3de-172">PCI DSS 3.1 版在我們的藍圖中。</span><span class="sxs-lookup"><span data-stu-id="7f3de-172">PCI DSS version 3.1 is on our roadmap.</span></span> <span data-ttu-id="7f3de-173">規劃已在進行中的採用 hello 最新標準的方式會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="7f3de-173">Planning is already underway for how adoption of hello latest standard will proceed.</span></span>

<span data-ttu-id="7f3de-174">PCI DSS 3.1 版憑證需要停用傳輸層安全性 (TLS) 1.0。</span><span class="sxs-lookup"><span data-stu-id="7f3de-174">PCI DSS version 3.1 certification requires disabling Transport Layer Security (TLS) 1.0.</span></span> <span data-ttu-id="7f3de-175">目前，停用 TLS 1.0 不是大部分 App Service 方案的選項。</span><span class="sxs-lookup"><span data-stu-id="7f3de-175">Currently, disabling TLS 1.0 is not an option for most App Service plans.</span></span> <span data-ttu-id="7f3de-176">不過，如果您使用 App Service 環境，或不願意 toomigrate 您工作負載 tooApp 服務環境，您可以取得更好的控制，您的環境。</span><span class="sxs-lookup"><span data-stu-id="7f3de-176">However, If you use App Service Environment or are willing toomigrate your workload tooApp Service Environment, you can get greater control of your environment.</span></span> <span data-ttu-id="7f3de-177">這牽涉到藉由連絡 Azure 支援人員來停用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="7f3de-177">This involves disabling TLS 1.0 by contacting Azure Support.</span></span> <span data-ttu-id="7f3de-178">在靠近未來 hello，我們計劃 toomake 這些設定可存取 toousers。</span><span class="sxs-lookup"><span data-stu-id="7f3de-178">In hello near future, we plan toomake these settings accessible toousers.</span></span>

<span data-ttu-id="7f3de-179">如需詳細資訊，請參閱 [Microsoft Azure App Service Web 應用程式符合 PCI 標準 3.0 和 3.1 的規範](https://support.microsoft.com/help/3124528)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-179">For more information, see [Microsoft Azure App Service web app compliance with PCI Standard 3.0 and 3.1](https://support.microsoft.com/help/3124528).</span></span>

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a><span data-ttu-id="7f3de-180">如何使用 hello 預備環境和部署位置？</span><span class="sxs-lookup"><span data-stu-id="7f3de-180">How do I use hello staging environment and deployment slots?</span></span>

<span data-ttu-id="7f3de-181">在標準和高階應用程式服務計劃，當您部署您的 web 應用程式 tooApp 服務，您可以部署 tooa 不同的部署位置，而不是 toohello 預設生產位置。</span><span class="sxs-lookup"><span data-stu-id="7f3de-181">In Standard and Premium App Service plans, when you deploy your web app tooApp Service, you can deploy tooa separate deployment slot instead of toohello default production slot.</span></span> <span data-ttu-id="7f3de-182">部署位置是具有專屬主機名稱的即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f3de-182">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="7f3de-183">Web 應用程式的內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="7f3de-183">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span>

<span data-ttu-id="7f3de-184">如需有關使用部署位置的詳細資訊，請參閱[在 App Service 中設定預備環境](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-184">For more information about using deployment slots, see [Set up a staging environment in App Service](web-sites-staged-publishing.md).</span></span>

## <a name="how-do-i-access-and-review-webjob-logs"></a><span data-ttu-id="7f3de-185">如何存取及檢閱 WebJob 記錄？</span><span class="sxs-lookup"><span data-stu-id="7f3de-185">How do I access and review WebJob logs?</span></span>

<span data-ttu-id="7f3de-186">tooreview WebJob 記錄檔：</span><span class="sxs-lookup"><span data-stu-id="7f3de-186">tooreview WebJob logs:</span></span>

1. <span data-ttu-id="7f3de-187">登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-187">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="7f3de-188">選取 hello WebJob。</span><span class="sxs-lookup"><span data-stu-id="7f3de-188">Select hello WebJob.</span></span>
3. <span data-ttu-id="7f3de-189">選取 hello**切換輸出** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f3de-189">Select hello **Toggle Output** button.</span></span>
4. <span data-ttu-id="7f3de-190">toodownload hello 輸出檔中，選取 hello**下載**連結。</span><span class="sxs-lookup"><span data-stu-id="7f3de-190">toodownload hello output file, select hello **Download** link.</span></span>
5. <span data-ttu-id="7f3de-191">針對個別的執行，選取 [個別叫用]。</span><span class="sxs-lookup"><span data-stu-id="7f3de-191">For individual runs, select **Individual Invoke**.</span></span>
6. <span data-ttu-id="7f3de-192">選取 hello**切換輸出** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f3de-192">Select hello **Toggle Output** button.</span></span>
7. <span data-ttu-id="7f3de-193">選取 hello 下載連結。</span><span class="sxs-lookup"><span data-stu-id="7f3de-193">Select hello download link.</span></span>

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a><span data-ttu-id="7f3de-194">我試著使用 SQL Server toouse 混合式連線。</span><span class="sxs-lookup"><span data-stu-id="7f3de-194">I'm trying toouse Hybrid Connections with SQL Server.</span></span> <span data-ttu-id="7f3de-195">為什麼看 hello 訊息 「 System.OverflowException： 數學運算導致溢位 」？</span><span class="sxs-lookup"><span data-stu-id="7f3de-195">Why do I see hello message "System.OverflowException: Arithmetic operation resulted in an overflow"?</span></span>

<span data-ttu-id="7f3de-196">如果您使用混合式連線 tooaccess SQL Server 時，於 2016 年 10 的 Microsoft.NET 更新可能會導致連線 toofail。</span><span class="sxs-lookup"><span data-stu-id="7f3de-196">If you use Hybrid Connections tooaccess SQL Server, a Microsoft .NET update on May 10, 2016, might cause connections toofail.</span></span> <span data-ttu-id="7f3de-197">您可能會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="7f3de-197">You might see this message:</span></span>

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a><span data-ttu-id="7f3de-198">解決方案</span><span class="sxs-lookup"><span data-stu-id="7f3de-198">Resolution</span></span>

<span data-ttu-id="7f3de-199">我們正在 tooupdate 混合式連線管理員 toofix 此問題。</span><span class="sxs-lookup"><span data-stu-id="7f3de-199">We are working tooupdate Hybrid Connection Manager toofix this issue.</span></span> <span data-ttu-id="7f3de-200">如需因應措施，請參閱[SQL Server 的混合式連線錯誤：System.OverflowException：數學運算導致溢位](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-200">For workarounds, see [Hybrid Connections error with SQL Server: System.OverflowException: Arithmetic operation resulted in an overflow](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).</span></span>

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a><span data-ttu-id="7f3de-201">如何新增或編輯 URL 重寫規則？</span><span class="sxs-lookup"><span data-stu-id="7f3de-201">How do I add or edit a URL rewrite rule?</span></span>

<span data-ttu-id="7f3de-202">tooadd 或編輯 URL 重寫規則：</span><span class="sxs-lookup"><span data-stu-id="7f3de-202">tooadd or edit a URL rewrite rule:</span></span>

1. <span data-ttu-id="7f3de-203">設定網際網路資訊服務 (IIS) 管理員，以便連接 tooyour App Service web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f3de-203">Set up Internet Information Services (IIS) Manager so that it connects tooyour App Service web app.</span></span> <span data-ttu-id="7f3de-204">如何 tooconnect IIS 管理員 tooApp 服務，請參閱的 toolearn[使用 IIS 管理員的 Azure 網站的遠端管理](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-204">toolearn how tooconnect IIS Manager tooApp Service, see [Remote administration of Azure websites by using IIS Manager](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).</span></span>
2. <span data-ttu-id="7f3de-205">在 IIS 管理員中，新增或編輯 URL 重寫規則。</span><span class="sxs-lookup"><span data-stu-id="7f3de-205">In IIS Manager, add or edit a URL rewrite rule.</span></span> <span data-ttu-id="7f3de-206">toolearn 如何 tooadd] 或 [編輯 URL 重寫規則，請參閱[建立重寫規則的 hello URL rewrite 模組](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-206">toolearn how tooadd or edit a URL rewrite rule, see [Create rewrite rules for hello URL rewrite module](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).</span></span>

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a><span data-ttu-id="7f3de-207">我要如何控制輸入的流量 tooApp 服務？</span><span class="sxs-lookup"><span data-stu-id="7f3de-207">How do I control inbound traffic tooApp Service?</span></span>

<span data-ttu-id="7f3de-208">在 hello 網站層級，您有兩個選項來控制輸入的流量 tooApp 服務：</span><span class="sxs-lookup"><span data-stu-id="7f3de-208">At hello site level, you have two options for controlling inbound traffic tooApp Service:</span></span>

* <span data-ttu-id="7f3de-209">開啟動態 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="7f3de-209">Turn on dynamic IP restrictions.</span></span> <span data-ttu-id="7f3de-210">如何 tooturn 上動態 IP 限制，請參閱的 toolearn [Azure 網站的 IP 及網域限制](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-210">toolearn how tooturn on dynamic IP restrictions, see [IP and domain restrictions for Azure websites](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).</span></span>
* <span data-ttu-id="7f3de-211">開啟模組安全性。</span><span class="sxs-lookup"><span data-stu-id="7f3de-211">Turn on Module Security.</span></span> <span data-ttu-id="7f3de-212">如何 tooturn 模組的安全性，請參閱的 toolearn [ModSecurity web 應用程式防火牆在 Azure 網站上的](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-212">toolearn how tooturn on Module Security, see [ModSecurity web application firewall on Azure websites](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).</span></span>

<span data-ttu-id="7f3de-213">如果您使用 App Service Environment，您可以使用 [Barracuda 防火牆](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-213">If you use App Service Environment, you can use [Barracuda firewall](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).</span></span>

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a><span data-ttu-id="7f3de-214">如何封鎖 App Service Web 應用程式中的連接埠？</span><span class="sxs-lookup"><span data-stu-id="7f3de-214">How do I block ports in an App Service web app?</span></span>

<span data-ttu-id="7f3de-215">在 hello 應用程式服務共用的租用戶環境，則不是特定連接埠可能 tooblock 由於 hello 本質之故 hello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7f3de-215">In hello App Service shared tenant environment, it is not possible tooblock specific ports because of hello nature of hello infrastructure.</span></span> <span data-ttu-id="7f3de-216">TCP 連接埠 4016、4018 和 4020 也可能已經針對 Visual Studio 遠端偵錯而開啟。</span><span class="sxs-lookup"><span data-stu-id="7f3de-216">TCP ports 4016, 4018, and 4020 also might be open for Visual Studio remote debugging.</span></span>

<span data-ttu-id="7f3de-217">在 App Service Environment 中，您對於輸入與輸出流量有完整控制權。</span><span class="sxs-lookup"><span data-stu-id="7f3de-217">In App Service Environment, you have full control over inbound  and outbound traffic.</span></span> <span data-ttu-id="7f3de-218">您可以使用網路安全性群組 toorestrict 或封鎖特定連接埠。</span><span class="sxs-lookup"><span data-stu-id="7f3de-218">You can use Network Security Groups toorestrict or block specific ports.</span></span> <span data-ttu-id="7f3de-219">如需 App Service Environment 的詳細資訊，請參閱[App Service Environment 簡介](https://azure.microsoft.com/blog/introducing-app-service-environment/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-219">For more information about App Service Environment, see [Introducing App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/).</span></span>

## <a name="how-do-i-capture-an-f12-trace"></a><span data-ttu-id="7f3de-220">如何擷取 F12 追蹤？</span><span class="sxs-lookup"><span data-stu-id="7f3de-220">How do I capture an F12 trace?</span></span>

<span data-ttu-id="7f3de-221">您有兩個選項可以用來擷取 F12 追蹤：</span><span class="sxs-lookup"><span data-stu-id="7f3de-221">You have two options for capturing an F12 trace:</span></span>

* <span data-ttu-id="7f3de-222">F12 HTTP 追蹤</span><span class="sxs-lookup"><span data-stu-id="7f3de-222">F12 HTTP trace</span></span>
* <span data-ttu-id="7f3de-223">F12 主控台輸出</span><span class="sxs-lookup"><span data-stu-id="7f3de-223">F12 console output</span></span>

### <a name="f12-http-trace"></a><span data-ttu-id="7f3de-224">F12 HTTP 追蹤</span><span class="sxs-lookup"><span data-stu-id="7f3de-224">F12 HTTP trace</span></span>

1. <span data-ttu-id="7f3de-225">在 Internet Explorer 中，移 tooyour 網站。</span><span class="sxs-lookup"><span data-stu-id="7f3de-225">In Internet Explorer, go tooyour website.</span></span> <span data-ttu-id="7f3de-226">您沒有 hello 接下來的步驟之前，它會在重要 toosign。</span><span class="sxs-lookup"><span data-stu-id="7f3de-226">It's important toosign in before you do hello next steps.</span></span> <span data-ttu-id="7f3de-227">否則，hello F12 追蹤會擷取敏感性登入資料。</span><span class="sxs-lookup"><span data-stu-id="7f3de-227">Otherwise, hello F12 trace captures sensitive sign-in data.</span></span>
2. <span data-ttu-id="7f3de-228">按下 F12。</span><span class="sxs-lookup"><span data-stu-id="7f3de-228">Press F12.</span></span>
3. <span data-ttu-id="7f3de-229">請確認該 hello**網路** 索引標籤，並選取然後選取 hello 綠色**播放** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f3de-229">Verify that hello **Network** tab is selected, and then select hello green **Play** button.</span></span>
4. <span data-ttu-id="7f3de-230">請勿 hello 重現 hello 問題的步驟。</span><span class="sxs-lookup"><span data-stu-id="7f3de-230">Do hello steps that reproduce hello issue.</span></span>
5. <span data-ttu-id="7f3de-231">選取 hello 紅色**停止** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7f3de-231">Select hello red **Stop** button.</span></span>
6. <span data-ttu-id="7f3de-232">選取 hello**儲存**按鈕 （磁片圖示），並將 hello HAR 檔案儲存 （在 Internet Explorer 和邊緣）*或*hello HAR 檔案，以滑鼠右鍵按一下，然後選取**內容另存為 HAR** (在 Chrome 中)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-232">Select hello **Save** button (disk icon), and save hello HAR file (in Internet Explorer and Edge) *or* right-click hello HAR file, and then select **Save as HAR with content** (in Chrome).</span></span>

### <a name="f12-console-output"></a><span data-ttu-id="7f3de-233">F12 主控台輸出</span><span class="sxs-lookup"><span data-stu-id="7f3de-233">F12 console output</span></span>

1. <span data-ttu-id="7f3de-234">選取 hello**主控台** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7f3de-234">Select hello **Console** tab.</span></span>
2. <span data-ttu-id="7f3de-235">每個索引標籤，其中包含零個以上的項目，選取 [hello] 索引標籤 (**錯誤**，**警告**，或**資訊**)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-235">For each tab that contains more than zero items, select hello tab (**Error**, **Warning**, or **Information**).</span></span> <span data-ttu-id="7f3de-236">如果沒有選取 hello 索引標籤，hello 索引標籤的圖示是灰色或黑色移開 hello 資料指標時。</span><span class="sxs-lookup"><span data-stu-id="7f3de-236">If hello tab isn’t selected, hello tab icon is gray or black when you move hello cursor away from it.</span></span>
3. <span data-ttu-id="7f3de-237">Hello 訊息區域中的 hello 窗格中，以滑鼠右鍵按一下，然後選取**複製所有**。</span><span class="sxs-lookup"><span data-stu-id="7f3de-237">Right-click in hello message area of hello pane, and then select **Copy all**.</span></span>
4. <span data-ttu-id="7f3de-238">貼上 hello 文字在檔案中，複製並儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f3de-238">Paste hello copied text in a file, and then save hello file.</span></span>

<span data-ttu-id="7f3de-239">tooview HAR 檔案，您可以使用 hello [HAR 檢視器](http://www.softwareishard.com/har/viewer/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-239">tooview an HAR file, you can use hello [HAR viewer](http://www.softwareishard.com/har/viewer/).</span></span>

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a><span data-ttu-id="7f3de-240">為什麼我收到錯誤當我嘗試 tooconnect App Service web 應用程式 tooa 虛擬網路，連線的 tooExpressRoute？</span><span class="sxs-lookup"><span data-stu-id="7f3de-240">Why do I get an error when I try tooconnect an App Service web app tooa virtual network that is connected tooExpressRoute?</span></span>

<span data-ttu-id="7f3de-241">如果您嘗試 tooconnect Azure web 應用程式 tooa 連線虛擬網路已 tooAzure ExpressRoute，它會失敗。</span><span class="sxs-lookup"><span data-stu-id="7f3de-241">If you try tooconnect an Azure web app tooa virtual network that's connected tooAzure ExpressRoute, it fails.</span></span> <span data-ttu-id="7f3de-242">hello 會出現下列訊息: 「 閘道 」 不 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="7f3de-242">hello following message appears: "Gateway is not a VPN gateway."</span></span>

<span data-ttu-id="7f3de-243">目前，您不能有點對站 VPN 連線 tooa 虛擬網路，連線的 tooExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="7f3de-243">Currently, you cannot have point-to-site VPN connections tooa virtual network that is connected tooExpressRoute.</span></span> <span data-ttu-id="7f3de-244">點對站 VPN 和 ExpressRoute 不能共存在 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7f3de-244">A point-to-site VPN and ExpressRoute cannot coexist for hello same virtual network.</span></span> <span data-ttu-id="7f3de-245">如需詳細資訊，請參閱 [ExpressRoute 和站對站 VPN 連線限制](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-245">For more information, see [ExpressRoute and site-to-site VPN connections limits and limitations](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).</span></span>

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a><span data-ttu-id="7f3de-246">如何連接 App Service web 應用程式 tooa 虛擬網路，靜態的路由 （以原則為基礎） 閘道？</span><span class="sxs-lookup"><span data-stu-id="7f3de-246">How do I connect an App Service web app tooa virtual network that has a static routing (policy-based) gateway?</span></span>

<span data-ttu-id="7f3de-247">目前不支援連接 App Service web 應用程式 tooa 虛擬網路，靜態的路由 （以原則為基礎） 閘道。</span><span class="sxs-lookup"><span data-stu-id="7f3de-247">Currently, connecting an App Service web app tooa virtual network that has a static routing (policy-based) gateway is not supported.</span></span> <span data-ttu-id="7f3de-248">如果您的目標虛擬網路已經存在，您必須先啟用，動態路由閘道，才能連接的 tooan 應用程式的點對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="7f3de-248">If your target virtual network already exists, it must have point-to-site VPN enabled, with a dynamic routing gateway, before it can be connected tooan app.</span></span> <span data-ttu-id="7f3de-249">如果您的閘道設定 toostatic 路由，您無法啟用點對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="7f3de-249">If your gateway is set toostatic routing, you cannot enable a point-to-site VPN.</span></span> 

<span data-ttu-id="7f3de-250">如需詳細資訊，請參閱[將應用程式與 Azure 虛擬網路整合](web-sites-integrate-with-vnet.md#getting-started)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-250">For more information, see [Integrate an app with an Azure virtual network](web-sites-integrate-with-vnet.md#getting-started).</span></span>

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a><span data-ttu-id="7f3de-251">為什麼我就算有 2 個可用的背景工作角色，卻還是只能在 App Service Environment 中建立一個 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="7f3de-251">In my App Service Environment, why can I create only one App Service plan, even though I have two workers available?</span></span>

<span data-ttu-id="7f3de-252">tooprovide 容錯功能，App Service 環境需要每個背景工作集區需要至少一個額外的計算資源。</span><span class="sxs-lookup"><span data-stu-id="7f3de-252">tooprovide fault tolerance, App Service Environment requires that each worker pool needs at least one additional compute resource.</span></span> <span data-ttu-id="7f3de-253">hello 額外的計算資源不能指定工作負載。</span><span class="sxs-lookup"><span data-stu-id="7f3de-253">hello additional compute resource cannot be assigned a workload.</span></span>

<span data-ttu-id="7f3de-254">如需詳細資訊，請參閱[如何 toocreate App Service 環境](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-254">For more information, see [How toocreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a><span data-ttu-id="7f3de-255">為什麼當我嘗試 toocreate App Service 環境看到逾時？</span><span class="sxs-lookup"><span data-stu-id="7f3de-255">Why do I see timeouts when I try toocreate an App Service Environment?</span></span>

<span data-ttu-id="7f3de-256">有時候，建立 App Service Environment 會失敗。</span><span class="sxs-lookup"><span data-stu-id="7f3de-256">Sometimes, creating an App Service Environment fails.</span></span> <span data-ttu-id="7f3de-257">在此情況下，您會看到下列錯誤 hello 活動記錄檔中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7f3de-257">In that case, you see hello following error in hello Activity logs:</span></span>
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

<span data-ttu-id="7f3de-258">tooresolve，請確定無 hello 下列條件成立：</span><span class="sxs-lookup"><span data-stu-id="7f3de-258">tooresolve this, make sure that none of hello following conditions are true:</span></span>
* <span data-ttu-id="7f3de-259">hello 子網路為太小。</span><span class="sxs-lookup"><span data-stu-id="7f3de-259">hello subnet is too small.</span></span>
* <span data-ttu-id="7f3de-260">hello 子網路不是空的。</span><span class="sxs-lookup"><span data-stu-id="7f3de-260">hello subnet is not empty.</span></span>
* <span data-ttu-id="7f3de-261">ExpressRoute 防止 App Service 環境的 hello 網路連線需求。</span><span class="sxs-lookup"><span data-stu-id="7f3de-261">ExpressRoute prevents hello network connectivity requirements of an App Service Environment.</span></span>
* <span data-ttu-id="7f3de-262">不正確的網路安全性群組可防止您的 App Service 環境的 hello 網路連線需求。</span><span class="sxs-lookup"><span data-stu-id="7f3de-262">A bad Network Security Group prevents hello network connectivity requirements of an App Service Environment.</span></span>
* <span data-ttu-id="7f3de-263">強制通道已開啟。</span><span class="sxs-lookup"><span data-stu-id="7f3de-263">Forced tunneling is turned on.</span></span>

<span data-ttu-id="7f3de-264">如需詳細資訊，請參閱[部署 (建立) 新的 Azure App Service Environment 時最常遇到的問題](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-264">For more information, see [Frequent issues when deploying (creating) a new Azure App Service Environment](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).</span></span>

## <a name="why-cant-i-delete-my-app-service-plan"></a><span data-ttu-id="7f3de-265">為什麼我無法刪除 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="7f3de-265">Why can't I delete my App Service plan?</span></span>

<span data-ttu-id="7f3de-266">如果任何 App Service 應用程式與 hello 應用程式服務方案相關聯，您無法刪除 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="7f3de-266">You can't delete an App Service plan if any App Service apps are associated with hello App Service plan.</span></span> <span data-ttu-id="7f3de-267">刪除 App Service 方案之前，請從 hello 應用程式服務方案中移除所有相關聯的應用程式服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="7f3de-267">Before you delete an App Service plan, remove all associated App Service apps from hello App Service plan.</span></span>

## <a name="how-do-i-schedule-a-webjob"></a><span data-ttu-id="7f3de-268">如何排程 WebJob？</span><span class="sxs-lookup"><span data-stu-id="7f3de-268">How do I schedule a WebJob?</span></span>

<span data-ttu-id="7f3de-269">您可以使用 Cron 運算式建立已排程 WebJob：</span><span class="sxs-lookup"><span data-stu-id="7f3de-269">You can create a scheduled WebJob by using Cron expressions:</span></span>

1. <span data-ttu-id="7f3de-270">建立 settings.job 檔案。</span><span class="sxs-lookup"><span data-stu-id="7f3de-270">Create a settings.job file.</span></span>
2. <span data-ttu-id="7f3de-271">在此 JSON 檔案中，使用 Cron 運算式以包含排程屬性：</span><span class="sxs-lookup"><span data-stu-id="7f3de-271">In this JSON file, include a schedule property by using a Cron expression:</span></span> 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

<span data-ttu-id="7f3de-272">如需已排程 WebJobs 的詳細資訊，請參閱[使用 Cron 運算式來建立已排程 WebJob](web-sites-create-web-jobs.md#CreateScheduledCRON)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-272">For more information about scheduled WebJobs, see [Create a scheduled WebJob by using a Cron expression](web-sites-create-web-jobs.md#CreateScheduledCRON).</span></span>

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a><span data-ttu-id="7f3de-273">如何執行 App Service 應用程式的滲透測試？</span><span class="sxs-lookup"><span data-stu-id="7f3de-273">How do I perform penetration testing for my App Service app?</span></span>

<span data-ttu-id="7f3de-274">tooperform 滲透測試[提交要求](https://security-forms.azure.com/penetration-testing/terms)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-274">tooperform penetration testing, [submit a request](https://security-forms.azure.com/penetration-testing/terms).</span></span>

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a><span data-ttu-id="7f3de-275">如何針對使用流量管理員的 App Service Web 應用程式設定自訂網域名稱？</span><span class="sxs-lookup"><span data-stu-id="7f3de-275">How do I configure a custom domain name for an App Service web app that uses Traffic Manager?</span></span>

<span data-ttu-id="7f3de-276">如何 toouse 自訂網域名稱與 App Service 應用程式使用 Azure Traffic Manager 負載平衡，請參閱的 toolearn[流量管理員設定 Azure web 應用程式的自訂網域名稱](web-sites-traffic-manager-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-276">toolearn how toouse a custom domain name with an App Service app that uses Azure Traffic Manager for load balancing, see [Configure a custom domain name for an Azure web app with Traffic Manager](web-sites-traffic-manager-custom-domain-name.md).</span></span>

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a><span data-ttu-id="7f3de-277">我的 App Service 憑證標示為詐騙。</span><span class="sxs-lookup"><span data-stu-id="7f3de-277">My App Service certificate is flagged for fraud.</span></span> <span data-ttu-id="7f3de-278">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="7f3de-278">How do I resolve this?</span></span>

<span data-ttu-id="7f3de-279">App Service 憑證購買 hello 網域驗證，您可能會看到下列訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="7f3de-279">During hello domain verification of an App Service certificate purchase, you might see hello following message:</span></span>

<span data-ttu-id="7f3de-280">「您的憑證已標示為可能詐騙。</span><span class="sxs-lookup"><span data-stu-id="7f3de-280">“Your certificate has been flagged for possible fraud.</span></span> <span data-ttu-id="7f3de-281">hello 要求目前正在進行檢閱。</span><span class="sxs-lookup"><span data-stu-id="7f3de-281">hello request is currently under review.</span></span> <span data-ttu-id="7f3de-282">如果 hello 憑證不會使用 24 小時內，請連絡 Azure 支援。 」</span><span class="sxs-lookup"><span data-stu-id="7f3de-282">If hello certificate does not become usable within 24 hours, please contact Azure Support.”</span></span>

<span data-ttu-id="7f3de-283">Hello 訊息表示，如這個詐騙驗證程序可能佔用 too24 小時 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7f3de-283">As hello message indicates, this fraud verification process might take up too24 hours toocomplete.</span></span> <span data-ttu-id="7f3de-284">在此期間，您將會繼續 toosee hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="7f3de-284">During this time, you'll continue toosee hello message.</span></span>

<span data-ttu-id="7f3de-285">如果您的應用程式服務的憑證在 24 小時後，此訊息將繼續 tooshow，請執行下列 PowerShell 指令碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="7f3de-285">If your App Service certificate continues tooshow this message after 24 hours, please run hello following PowerShell script.</span></span> <span data-ttu-id="7f3de-286">hello 指令碼連絡人 hello[憑證提供者](https://www.godaddy.com/)直接 tooresolve hello 問題。</span><span class="sxs-lookup"><span data-stu-id="7f3de-286">hello script contacts hello [certificate provider](https://www.godaddy.com/) directly tooresolve hello issue.</span></span>

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a><span data-ttu-id="7f3de-287">驗證和授權如何在 App Service 中運作？</span><span class="sxs-lookup"><span data-stu-id="7f3de-287">How do authentication and authorization work in App Service?</span></span>

<span data-ttu-id="7f3de-288">如需 App Service 中驗證和授權的詳細文件，請參閱 [App Service 安全性](../app-service/app-service-security-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-288">For detailed documentation for authentication and authorization in App Service, see [App Service security](../app-service/app-service-security-readme.md).</span></span> <span data-ttu-id="7f3de-289">hello 文件也具有資訊有關設定應用程式服務 toouse 各種識別提供者登入：</span><span class="sxs-lookup"><span data-stu-id="7f3de-289">hello documentation also has information about setting up App Service toouse various identify provider sign-ins:</span></span>
* [<span data-ttu-id="7f3de-290">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f3de-290">Azure Active Directory</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [<span data-ttu-id="7f3de-291">Facebook</span><span class="sxs-lookup"><span data-stu-id="7f3de-291">Facebook</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [<span data-ttu-id="7f3de-292">Google</span><span class="sxs-lookup"><span data-stu-id="7f3de-292">Google</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [<span data-ttu-id="7f3de-293">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="7f3de-293">Microsoft Account</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [<span data-ttu-id="7f3de-294">Twitter</span><span class="sxs-lookup"><span data-stu-id="7f3de-294">Twitter</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a><span data-ttu-id="7f3de-295">如何導向 hello 預設 *。 azurewebsites.net 網域 toomy Azure web 應用程式的自訂網域？</span><span class="sxs-lookup"><span data-stu-id="7f3de-295">How do I redirect hello default *.azurewebsites.net domain toomy Azure web app's custom domain?</span></span>

<span data-ttu-id="7f3de-296">當您建立新的網站透過 Web 應用程式在 Azure 中，預設值*sitename*。 azurewebsites.net 網域 tooyour 站台指派。</span><span class="sxs-lookup"><span data-stu-id="7f3de-296">When you create a new website by using Web Apps in Azure, a default *sitename*.azurewebsites.net domain is assigned tooyour site.</span></span> <span data-ttu-id="7f3de-297">如果您新增自訂主機名稱 tooyour 站台並不希望您的預設使用者 toobe 無法 tooaccess *。 azurewebsites.net 網域中，您可以重新導向 hello 預設 URL。</span><span class="sxs-lookup"><span data-stu-id="7f3de-297">If you add a custom host name tooyour site and don’t want users toobe able tooaccess your default *.azurewebsites.net domain, you can redirect hello default URL.</span></span> <span data-ttu-id="7f3de-298">toolearn 如何 tooredirect 所有流量從您的網站預設網域 tooyour 的自訂網域，請參閱[重新導向 hello 預設網域 tooyour 自訂網域在 Azure web 應用程式](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-298">toolearn how tooredirect all traffic from your website's default domain tooyour custom domain, see [Redirect hello default domain tooyour custom domain in Azure web apps](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).</span></span>

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a><span data-ttu-id="7f3de-299">如何判斷安裝在 App Service 中的是哪一個版本的 .NET？</span><span class="sxs-lookup"><span data-stu-id="7f3de-299">How do I determine which version of .NET version is installed in App Service?</span></span>

<span data-ttu-id="7f3de-300">hello 最快方式 toofind hello 新版的 Microsoft.NET 應用程式服務中安裝是使用 hello Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="7f3de-300">hello quickest way toofind hello version of Microsoft .NET that's installed in App Service is by using hello Kudu console.</span></span> <span data-ttu-id="7f3de-301">您可以從 hello 入口網站或使用 App Service 應用程式的 hello URL 來存取 hello Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="7f3de-301">You can access hello Kudu console from hello portal or by using hello URL of your App Service app.</span></span> <span data-ttu-id="7f3de-302">如需詳細指示，請參閱[判斷 hello 安裝應用程式服務中的.NET 版本](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-302">For detailed instructions, see [Determine hello installed .NET version in App Service](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).</span></span>

## <a name="why-isnt-autoscale-working-as-expected"></a><span data-ttu-id="7f3de-303">為什麼自動調整無法如預期般運作？</span><span class="sxs-lookup"><span data-stu-id="7f3de-303">Why isn't Autoscale working as expected?</span></span>

<span data-ttu-id="7f3de-304">如果 Azure 自動調整規模尚未在調整或擴充 hello web 應用程式執行個體，如您所預期，您可能執行的情況中，我們刻意選擇不 tooscale tooavoid 無限迴圈因為太"出現 flapping 的現象。 」</span><span class="sxs-lookup"><span data-stu-id="7f3de-304">If Azure Autoscale hasn't scaled in or scaled out hello web app instance as you expected, you might be running into a scenario in which we intentionally choose not tooscale tooavoid an infinite loop due too"flapping."</span></span> <span data-ttu-id="7f3de-305">當 hello 向外延展和小數位數的臨界值之間沒有足夠的邊界時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="7f3de-305">This usually happens when there isn't an adequate margin between hello scale-out and scale-in thresholds.</span></span> <span data-ttu-id="7f3de-306">如何 tooavoid"出現 flapping 的現象"和 tooread 有關其他自動調整規模的最佳作法，請參閱的 toolearn[自動調整規模的最佳作法](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-306">toolearn how tooavoid "flapping" and tooread about other Autoscale best practices, see [Autoscale best practices](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).</span></span>

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a><span data-ttu-id="7f3de-307">為什麼自動調整有時候只會部分調整？</span><span class="sxs-lookup"><span data-stu-id="7f3de-307">Why does Autoscale sometimes scale only partially?</span></span>

<span data-ttu-id="7f3de-308">當計量超出預先設定的界限時，會觸發自動調整。</span><span class="sxs-lookup"><span data-stu-id="7f3de-308">Autoscale is triggered when metrics exceed preconfigured boundaries.</span></span> <span data-ttu-id="7f3de-309">有時候，您可能會注意到 hello 容量只有部分填滿您所預期的比較的 toowhat。</span><span class="sxs-lookup"><span data-stu-id="7f3de-309">Sometimes, you might notice that hello capacity is only partially filled compared toowhat you expected.</span></span> <span data-ttu-id="7f3de-310">無法使用您想要的執行個體的 hello 數目時，也可能會發生。</span><span class="sxs-lookup"><span data-stu-id="7f3de-310">This might occur when hello number of instances you want are not available.</span></span> <span data-ttu-id="7f3de-311">在該案例中，自動調整部分填滿入 hello 可用執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="7f3de-311">In that scenario, Autoscale partially fills in with hello available number of instances.</span></span> <span data-ttu-id="7f3de-312">自動調整規模則會執行 hello 重新平衡邏輯 tooget 更多容量。</span><span class="sxs-lookup"><span data-stu-id="7f3de-312">Autoscale then runs hello rebalance logic tooget more capacity.</span></span> <span data-ttu-id="7f3de-313">它會配置 hello 剩餘的執行個體。</span><span class="sxs-lookup"><span data-stu-id="7f3de-313">It allocates hello remaining instances.</span></span> <span data-ttu-id="7f3de-314">請注意，這可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="7f3de-314">Note that this might take a few minutes.</span></span>

<span data-ttu-id="7f3de-315">如果您沒有看到預期 hello 的執行個體數幾分鐘後，它可能是因為 hello 部分填滿 hello 界限內足夠 toobring hello 度量。</span><span class="sxs-lookup"><span data-stu-id="7f3de-315">If you don't see hello expected number of instances after a few minutes, it might be because hello partial refill was enough toobring hello metrics within hello boundaries.</span></span> <span data-ttu-id="7f3de-316">或者，您也可以自動調整規模可能會有比例縮小，因為它已達到 hello 下限標準。</span><span class="sxs-lookup"><span data-stu-id="7f3de-316">Or, Autoscale might have scaled down because it reached hello lower metrics boundary.</span></span>

<span data-ttu-id="7f3de-317">如果這些條件都不適用，而且 hello 問題持續發生，請提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="7f3de-317">If none of these conditions apply and hello problem persists, submit a support request.</span></span>

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a><span data-ttu-id="7f3de-318">如何針對內容開啟 HTTP 壓縮？</span><span class="sxs-lookup"><span data-stu-id="7f3de-318">How do I turn on HTTP compression for my content?</span></span>

<span data-ttu-id="7f3de-319">對於靜態和動態的內容類型，壓縮 tooturn 加入下列程式碼 toohello 應用程式層級的 web.config 檔的 hello:</span><span class="sxs-lookup"><span data-stu-id="7f3de-319">tooturn on compression both for static and dynamic content types, add hello following code toohello application-level web.config file:</span></span>

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

<span data-ttu-id="7f3de-320">您也可以指定 hello 特定動態和靜態的 MIME 類型的 toocompress。</span><span class="sxs-lookup"><span data-stu-id="7f3de-320">You also can specify hello specific dynamic and static MIME types that you want toocompress.</span></span> <span data-ttu-id="7f3de-321">如需詳細資訊，請參閱我們回應 tooa 論壇中的問題[httpCompression 設定簡單的 Azure 網站上](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-321">For more information, see our response tooa forum question in [httpCompression settings on a simple Azure website](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).</span></span>

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a><span data-ttu-id="7f3de-322">如何將從內部部署環境 tooApp 服務移轉？</span><span class="sxs-lookup"><span data-stu-id="7f3de-322">How do I migrate from an on-premises environment tooApp Service?</span></span>

<span data-ttu-id="7f3de-323">從 Windows 和 Linux web 伺服器 tooApp 服務 toomigrate 站台，您可以使用 Azure 應用程式服務移轉小幫手。</span><span class="sxs-lookup"><span data-stu-id="7f3de-323">toomigrate sites from Windows and Linux web servers tooApp Service, you can use Azure App Service Migration Assistant.</span></span> <span data-ttu-id="7f3de-324">hello 移轉工具中如有需要 Azure 中建立 web 應用程式和資料庫，並接著將發佈 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="7f3de-324">hello migration tool creates web apps and databases in Azure as needed, and then publishes hello content.</span></span> <span data-ttu-id="7f3de-325">如需詳細資訊，請參閱 [Azure App Service 移轉小幫手](https://www.movemetothecloud.net/)。</span><span class="sxs-lookup"><span data-stu-id="7f3de-325">For more information, see [Azure App Service Migration Assistant](https://www.movemetothecloud.net/).</span></span>
