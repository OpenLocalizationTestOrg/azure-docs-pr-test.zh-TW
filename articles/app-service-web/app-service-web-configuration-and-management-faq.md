---
title: "Azure Web 應用程式的設定常見問題集 | Microsoft Docs"
description: "對於 Azure App Service 的 Web 應用程式功能的設定和管理問題，取得常見問題集的解答。"
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
ms.openlocfilehash: 8465454ac95150a5952039ff13733e90a5ca018d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a><span data-ttu-id="4e0c6-103">Azure 中 Web 應用程式的設定和管理常見問題集</span><span class="sxs-lookup"><span data-stu-id="4e0c6-103">Configuration and management FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="4e0c6-104">對於 [Azure App Service 的 Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)的設定和管理問題，本文章提供常見問題集 (FAQ) 的解答。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-104">This article has answers to frequently asked questions (FAQs) about configuration and management issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-to-move-app-service-resources"></a><span data-ttu-id="4e0c6-105">如果我想要移動 App Service 資源，有應該注意的限制嗎？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-105">Are there limitations I should be aware of if I want to move App Service resources?</span></span>

<span data-ttu-id="4e0c6-106">如果您打算將 App Service 資源移至新的資源群組或訂用帳戶，有一些要注意的限制。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-106">If you plan to move App Service resources to a new resource group or subscription, there are a few limitations to be aware of.</span></span> <span data-ttu-id="4e0c6-107">如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-107">For more information, see [App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).</span></span>

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a><span data-ttu-id="4e0c6-108">如何針對 Web 應用程式使用自訂網域名稱？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-108">How do I use a custom domain name for my web app?</span></span>

<span data-ttu-id="4e0c6-109">如需將自訂網域名稱與 Azure Web 應用程式搭配使用的常見問題解答，請參閱我們的七分鐘影片：[新增自訂網域名稱](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-109">For answers to common questions about using a custom domain name with your Azure web app, see our seven-minute video [Add a custom domain name](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name).</span></span> <span data-ttu-id="4e0c6-110">影片提供如何新增自訂網域名稱的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-110">The video offers a walkthrough of how to add a custom domain name.</span></span> <span data-ttu-id="4e0c6-111">說明如何搭配使用自己的 URL (而不是 *.azurewebsites.net URL) 與 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-111">It describes how to use your own URL instead of the *.azurewebsites.net URL with your App Service web app.</span></span> <span data-ttu-id="4e0c6-112">您也可以參閱[如何對應自訂網域名稱](web-sites-custom-domain-name.md)的詳細逐步解說。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-112">You also can see a detailed walkthrough of [how to map a custom domain name](web-sites-custom-domain-name.md).</span></span>


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a><span data-ttu-id="4e0c6-113">如何為 Web 應用程式購買新的自訂網域？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-113">How do I purchase a new custom domain for my web app?</span></span>

<span data-ttu-id="4e0c6-114">若要深入了解如何購買並設定 App Service Web 應用程式的自訂網域，請參閱[購買自訂網域名稱並且在 App Service 中設定](custom-dns-web-site-buydomains-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-114">To learn how to purchase and set up a custom domain for your App Service web app, see [Buy and configure a custom domain name in App Service](custom-dns-web-site-buydomains-web-app.md).</span></span>


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a><span data-ttu-id="4e0c6-115">如何上傳及設定 Web 應用程式的現有 SSL 憑證？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-115">How do I upload and configure an existing SSL certificate for my web app?</span></span>

<span data-ttu-id="4e0c6-116">若要深入了解如何上傳及設定現有的自訂 SSL 憑證，請參閱[將現有的自訂 SSL 憑證繫結至 Azure Web 應用程式](app-service-web-tutorial-custom-ssl.md#upload)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-116">To learn how to upload and set up an existing custom SSL certificate, see [Bind an existing custom SSL certificate to an Azure web app](app-service-web-tutorial-custom-ssl.md#upload).</span></span>


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a><span data-ttu-id="4e0c6-117">如何購買 Web 應用程式的新 SSL 憑證並且在 Azure 中設定？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-117">How do I purchase and configure a new SSL certificate in Azure for my web app?</span></span>

<span data-ttu-id="4e0c6-118">若要深入了解如何購買及設定 App Service Web 應用程式的 SSL 憑證，請參閱[將 SSL 憑證新增至您的 App Service 應用程式](web-sites-purchase-ssl-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-118">To learn how to purchase and set up an SSL certificate for your App Service web app, see [Add an SSL certificate to your App Service app](web-sites-purchase-ssl-web-site.md).</span></span>


## <a name="how-do-i-move-application-insights-resources"></a><span data-ttu-id="4e0c6-119">如何移動 Application Insights 資源？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-119">How do I move Application Insights resources?</span></span>

<span data-ttu-id="4e0c6-120">目前，Azure Application Insights 並不支援移動作業。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-120">Currently, Azure Application Insights doesn't support the move operation.</span></span> <span data-ttu-id="4e0c6-121">如果您的原始資源群組包含 Application Insights 資源，則您無法移動該資源。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-121">If your original resource group includes an Application Insights resource, you cannot move that resource.</span></span> <span data-ttu-id="4e0c6-122">如果您在嘗試移動 App Service 應用程式時包含 Application Insights 資源，則整個移動作業會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-122">If you include the Application Insights resource when you try to move an App Service app, the entire move operation fails.</span></span> <span data-ttu-id="4e0c6-123">不過，Application Insights 和 App Service 方案不需要位於與應用程式相同的資源群組，應用程式就能正確運作。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-123">However, Application Insights and the App Service plan do not need to be in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="4e0c6-124">如需詳細資訊，請參閱 [App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-124">For more information, see [App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).</span></span>

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a><span data-ttu-id="4e0c6-125">可以在哪裡尋找指引檢查清單及深入了解資源移動作業？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-125">Where can I find a guidance checklist and learn more about resource move operations?</span></span>

<span data-ttu-id="4e0c6-126">[App Service 限制](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations)說明如何將資源移至新的訂用帳戶或相同訂用帳戶中新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-126">[App Service limitations](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) shows you how to move resources to either a new subscription or to a new resource group in the same subscription.</span></span> <span data-ttu-id="4e0c6-127">您可以取得資源移動檢查清單的相關資訊、深入了解哪些服務支援移動作業，以及深入了解 App Service 限制與其他主題。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-127">You can get information about the resource move checklist, learn which services support the move operation, and learn more about App Service limitations and other topics.</span></span>

## <a name="how-do-i-set-the-server-time-zone-for-my-web-app"></a><span data-ttu-id="4e0c6-128">如何設定 Web 應用程式的伺服器時區？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-128">How do I set the server time zone for my web app?</span></span>

<span data-ttu-id="4e0c6-129">若要設定 Web 應用程式的伺服器時區：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-129">To set the server time zone for your web app:</span></span>

1. <span data-ttu-id="4e0c6-130">在 Azure 入口網站的 App Service 訂用帳戶中，移至 [應用程式設定] 功能表。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-130">In the Azure portal, in your App Service subscription, go to the **Application settings** menu.</span></span>
2. <span data-ttu-id="4e0c6-131">在 [應用程式設定] 底下，新增以下設定：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-131">Under **App settings**, add this setting:</span></span>
    * <span data-ttu-id="4e0c6-132">索引鍵 = WEBSITE_TIME_ZONE</span><span class="sxs-lookup"><span data-stu-id="4e0c6-132">Key = WEBSITE_TIME_ZONE</span></span>
    * <span data-ttu-id="4e0c6-133">值 = 您想要的時區</span><span class="sxs-lookup"><span data-stu-id="4e0c6-133">Value = *The time zone you want*</span></span>
3. <span data-ttu-id="4e0c6-134">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-134">Select **Save**.</span></span>

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a><span data-ttu-id="4e0c6-135">為什麼我的持續 WebJobs 有時候會失敗？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-135">Why do my continuous WebJobs sometimes fail?</span></span>

<span data-ttu-id="4e0c6-136">根據預設，Web 應用程式如果閒置一段時間，就會卸載。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-136">By default, web apps are unloaded if they are idle for a set period of time.</span></span> <span data-ttu-id="4e0c6-137">此舉有助於系統保留資源。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-137">This lets the system conserve resources.</span></span> <span data-ttu-id="4e0c6-138">在「基本」和「標準」方案中，您可以開啟 [永遠開啟] 設定，讓 Web 應用程式隨時保持載入。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-138">In Basic and Standard plans, you can turn on the **Always On** setting to keep the web app loaded all the time.</span></span> <span data-ttu-id="4e0c6-139">如果您的 Web 應用程式會執行持續的 WebJobs，就應該開啟 [永遠開啟]，否則 WebJobs 可能無法可靠地執行。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-139">If your web app runs continuous WebJobs, you should turn on **Always On**, or the WebJobs might not run reliably.</span></span> <span data-ttu-id="4e0c6-140">如需詳細資訊，請參閱[建立持續執行 WebJob](web-sites-create-web-jobs.md#CreateContinuous)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-140">For more information, see [Create a continuously running WebJob](web-sites-create-web-jobs.md#CreateContinuous).</span></span>

## <a name="how-do-i-get-the-outbound-ip-address-for-my-web-app"></a><span data-ttu-id="4e0c6-141">如何取得 Web 應用程式的輸出 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-141">How do I get the outbound IP address for my web app?</span></span>

<span data-ttu-id="4e0c6-142">若要取得 Web 應用程式的輸出 IP 位址清單：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-142">To get the list of outbound IP addresses for your web app:</span></span>

1. <span data-ttu-id="4e0c6-143">在 Azure 入口網站的 Web 應用程式刀鋒視窗中，移至 [屬性] 功能表。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-143">In the Azure portal, on your web app blade, go to the **Properties** menu.</span></span>
2. <span data-ttu-id="4e0c6-144">搜尋**輸出 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-144">Search for **outbound ip addresses**.</span></span>

<span data-ttu-id="4e0c6-145">輸出 IP 位址清單隨即出現。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-145">The list of outbound IP addresses appears.</span></span>

<span data-ttu-id="4e0c6-146">如果您的網站裝載在 App Service Environment for PowerApps，若要深入了解如何取得輸出 IP 位址，請參閱[輸出網路位址](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-146">If your website is hosted in App Service Environment for PowerApps, to learn how to get your outbound IP address, see [Outbound network addresses](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).</span></span>

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a><span data-ttu-id="4e0c6-147">如何為 Web 應用程式取得保留或專用輸入 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-147">How do I get a reserved or dedicated inbound IP address for my web app?</span></span>

<span data-ttu-id="4e0c6-148">若要針對向 Azure 應用程式網站進行的輸入呼叫設定專用或保留 IP 位址，請安裝及設定以 IP 為主的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-148">To set up a dedicated or reserved IP address for inbound calls made to your Azure app website, install and configure an IP-based SSL certificate.</span></span>

<span data-ttu-id="4e0c6-149">請注意，若要針對輸入呼叫使用專用或保留 IP 位址，您的 App Service 方案必須是「基本」或更高版本的服務方案。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-149">Note that to use a dedicated or reserved IP address for inbound calls, your App Service plan must be in a Basic or higher service plan.</span></span>

## <a name="can-i-export-my-app-service-certificate-to-use-outside-azure-such-as-for-a-website-hosted-elsewhere"></a><span data-ttu-id="4e0c6-150">是否可以將 App Service 憑證匯出以在 Azure 外部使用，例如在其他位置裝載的網站？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-150">Can I export my App Service certificate to use outside Azure, such as for a website hosted elsewhere?</span></span> 

<span data-ttu-id="4e0c6-151">App Service 憑證被視為 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-151">App Service certificates are considered Azure resources.</span></span> <span data-ttu-id="4e0c6-152">它們並不適合在 Azure 服務外部使用。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-152">They are not intended to use outside your Azure services.</span></span> <span data-ttu-id="4e0c6-153">您無法將它們匯出以在 Azure 外部使用。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-153">You cannot export them to use outside Azure.</span></span> <span data-ttu-id="4e0c6-154">如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-154">For more information, see [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).</span></span>

## <a name="can-i-export-my-app-service-certificate-to-use-with-other-azure-cloud-services"></a><span data-ttu-id="4e0c6-155">是否可以匯出我的 App Service 憑證以與其他 Azure 雲端服務搭配使用？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-155">Can I export my App Service certificate to use with other Azure cloud services?</span></span>

<span data-ttu-id="4e0c6-156">入口網站提供透過 Azure Key Vault 將 App Service 憑證部署至 App Service 應用程式的頂級體驗。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-156">The portal provides a first-class experience for deploying an App Service certificate through Azure Key Vault to App Service apps.</span></span> <span data-ttu-id="4e0c6-157">不過，我們已經收到客戶的要求，想要在 App Service 平台外部使用這些憑證，例如，使用 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-157">However, we have been receiving requests from customers to use these certificates outside the App Service platform, for example, with Azure Virtual Machines.</span></span> <span data-ttu-id="4e0c6-158">若要深入了解如何建立 App Service 憑證的本機 PFX 複本，以便與其他 Azure 資源搭配使用憑證，請參閱[建立 App Service 憑證的本機 PFX 複本](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-158">To learn how to create a local PFX copy of your App Service certificate so you can use the certificate with other Azure resources, see [Create a local PFX copy of an App Service certificate](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).</span></span>

<span data-ttu-id="4e0c6-159">如需詳細資訊，請參閱 [App Service 憑證和自訂網域的常見問題集](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-159">For more information, see [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).</span></span>


## <a name="why-do-i-see-the-message-partially-succeeded-when-i-try-to-back-up-my-web-app"></a><span data-ttu-id="4e0c6-160">為什麼當我嘗試備份 Web 應用程式時看到「部分成功」訊息？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-160">Why do I see the message "Partially Succeeded" when I try to back up my web app?</span></span>

<span data-ttu-id="4e0c6-161">備份失敗的常見原因是某些檔案正在由應用程式使用中。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-161">A common cause of backup failure is that some files are in use by the application.</span></span> <span data-ttu-id="4e0c6-162">您在執行備份時，使用中的檔案會遭到鎖定。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-162">Files that are in use are locked while you perform the backup.</span></span> <span data-ttu-id="4e0c6-163">這樣會避免這些檔案進行備份，因此可能導致「部分成功」狀態。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-163">This prevents these files from being backed up and might result in a "Partially Succeeded" status.</span></span> <span data-ttu-id="4e0c6-164">您也許可以藉由從備份程序排除此檔案來防止這個情形發生。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-164">You can potentially prevent this from occurring by excluding files from the backup process.</span></span> <span data-ttu-id="4e0c6-165">您可以選擇僅備份需要的項目。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-165">You can choose to back up only what is needed.</span></span> <span data-ttu-id="4e0c6-166">如需詳細資訊，請參閱[僅備份網站與 Azure Web 應用程式的重要部分](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-166">For more information, see [Backup just the important parts of your site with Azure web apps](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).</span></span>

## <a name="how-do-i-remove-a-header-from-the-http-response"></a><span data-ttu-id="4e0c6-167">如何從 HTTP 回應移除標題？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-167">How do I remove a header from the HTTP response?</span></span>

<span data-ttu-id="4e0c6-168">若要從 HTTP 回應移除標題，請更新網站的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-168">To remove the headers from the HTTP response, update your site’s web.config file.</span></span> <span data-ttu-id="4e0c6-169">如需詳細資訊，請參閱[在 Azure 網站上移除標準伺服器標題](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-169">For more information, see [Remove standard server headers on your Azure websites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).</span></span>

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a><span data-ttu-id="4e0c6-170">App Service 是否符合 PCI 標準 3.0 和 3.1 的規範？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-170">Is App Service compliant with PCI Standard 3.0 and 3.1?</span></span>

<span data-ttu-id="4e0c6-171">目前，Azure App Service 的 Web 應用程式功能符合 PCI 資料安全標準 (DSS) 版本 3.0 層級 1 的規範。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-171">Currently, the Web Apps feature of Azure App Service is in compliance with PCI Data Security Standard (DSS) version 3.0 Level 1.</span></span> <span data-ttu-id="4e0c6-172">PCI DSS 3.1 版在我們的藍圖中。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-172">PCI DSS version 3.1 is on our roadmap.</span></span> <span data-ttu-id="4e0c6-173">如何持續採用最新標準的規劃已在進行中。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-173">Planning is already underway for how adoption of the latest standard will proceed.</span></span>

<span data-ttu-id="4e0c6-174">PCI DSS 3.1 版憑證需要停用傳輸層安全性 (TLS) 1.0。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-174">PCI DSS version 3.1 certification requires disabling Transport Layer Security (TLS) 1.0.</span></span> <span data-ttu-id="4e0c6-175">目前，停用 TLS 1.0 不是大部分 App Service 方案的選項。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-175">Currently, disabling TLS 1.0 is not an option for most App Service plans.</span></span> <span data-ttu-id="4e0c6-176">不過，如果您使用 App Service Environment，或願意將您的工作負載移轉至 App Service Environment，您可以掌握對環境更好的控制。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-176">However, If you use App Service Environment or are willing to migrate your workload to App Service Environment, you can get greater control of your environment.</span></span> <span data-ttu-id="4e0c6-177">這牽涉到藉由連絡 Azure 支援人員來停用 TLS 1.0。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-177">This involves disabling TLS 1.0 by contacting Azure Support.</span></span> <span data-ttu-id="4e0c6-178">在不久的將來，我們計劃讓使用者能夠存取這些設定。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-178">In the near future, we plan to make these settings accessible to users.</span></span>

<span data-ttu-id="4e0c6-179">如需詳細資訊，請參閱 [Microsoft Azure App Service Web 應用程式符合 PCI 標準 3.0 和 3.1 的規範](https://support.microsoft.com/help/3124528)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-179">For more information, see [Microsoft Azure App Service web app compliance with PCI Standard 3.0 and 3.1](https://support.microsoft.com/help/3124528).</span></span>

## <a name="how-do-i-use-the-staging-environment-and-deployment-slots"></a><span data-ttu-id="4e0c6-180">如何使用預備環境和部署位置？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-180">How do I use the staging environment and deployment slots?</span></span>

<span data-ttu-id="4e0c6-181">在 [標準] 或 [進階] App Service 方案中，當您將 Web 應用程式部署至 App Service 時，可以部署到個別的部署位置，而不是預設的生產位置。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-181">In Standard and Premium App Service plans, when you deploy your web app to App Service, you can deploy to a separate deployment slot instead of to the default production slot.</span></span> <span data-ttu-id="4e0c6-182">部署位置是具有專屬主機名稱的即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-182">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="4e0c6-183">兩個部署位置 (包括生產位置) 之間的 Web 應用程式內容與設定項目可以互相交換。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-183">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span>

<span data-ttu-id="4e0c6-184">如需有關使用部署位置的詳細資訊，請參閱[在 App Service 中設定預備環境](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-184">For more information about using deployment slots, see [Set up a staging environment in App Service](web-sites-staged-publishing.md).</span></span>

## <a name="how-do-i-access-and-review-webjob-logs"></a><span data-ttu-id="4e0c6-185">如何存取及檢閱 WebJob 記錄？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-185">How do I access and review WebJob logs?</span></span>

<span data-ttu-id="4e0c6-186">若要檢閱 WebJob 記錄：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-186">To review WebJob logs:</span></span>

1. <span data-ttu-id="4e0c6-187">登入 [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-187">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="4e0c6-188">選取 WebJob。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-188">Select the WebJob.</span></span>
3. <span data-ttu-id="4e0c6-189">選取 [切換輸出] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-189">Select the **Toggle Output** button.</span></span>
4. <span data-ttu-id="4e0c6-190">若要下載輸出檔案，請選取 [下載] 連結。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-190">To download the output file, select the **Download** link.</span></span>
5. <span data-ttu-id="4e0c6-191">針對個別的執行，選取 [個別叫用]。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-191">For individual runs, select **Individual Invoke**.</span></span>
6. <span data-ttu-id="4e0c6-192">選取 [切換輸出] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-192">Select the **Toggle Output** button.</span></span>
7. <span data-ttu-id="4e0c6-193">選取下載連結。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-193">Select the download link.</span></span>

## <a name="im-trying-to-use-hybrid-connections-with-sql-server-why-do-i-see-the-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a><span data-ttu-id="4e0c6-194">我正在嘗試使用混合式連線與 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-194">I'm trying to use Hybrid Connections with SQL Server.</span></span> <span data-ttu-id="4e0c6-195">為什麼會看到「System.OverflowException：	數學運算導致溢位」訊息？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-195">Why do I see the message "System.OverflowException: Arithmetic operation resulted in an overflow"?</span></span>

<span data-ttu-id="4e0c6-196">如果您使用混合式連線來存取 SQL Server (2016 年 5 月 10 日的 Microsoft.NET 更新)，可能會導致連線失敗。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-196">If you use Hybrid Connections to access SQL Server, a Microsoft .NET update on May 10, 2016, might cause connections to fail.</span></span> <span data-ttu-id="4e0c6-197">您可能會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-197">You might see this message:</span></span>

```
Exception: System.Data.Entity.Core.EntityException: The underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a><span data-ttu-id="4e0c6-198">解決方案</span><span class="sxs-lookup"><span data-stu-id="4e0c6-198">Resolution</span></span>

<span data-ttu-id="4e0c6-199">我們正在更新混合式連線管理員，以修正此問題。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-199">We are working to update Hybrid Connection Manager to fix this issue.</span></span> <span data-ttu-id="4e0c6-200">如需因應措施，請參閱[SQL Server 的混合式連線錯誤：System.OverflowException：數學運算導致溢位](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-200">For workarounds, see [Hybrid Connections error with SQL Server: System.OverflowException: Arithmetic operation resulted in an overflow](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).</span></span>

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a><span data-ttu-id="4e0c6-201">如何新增或編輯 URL 重寫規則？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-201">How do I add or edit a URL rewrite rule?</span></span>

<span data-ttu-id="4e0c6-202">若要新增或編輯 URL 重寫規則：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-202">To add or edit a URL rewrite rule:</span></span>

1. <span data-ttu-id="4e0c6-203">設定網際網路資訊服務 (IIS) 管理員，以便連線到您的 App Service Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-203">Set up Internet Information Services (IIS) Manager so that it connects to your App Service web app.</span></span> <span data-ttu-id="4e0c6-204">若要了解如何將 IIS 管理員連線到 App Service，請參閱[使用 IIS 管理員進行 Azure 網站的遠端管理](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-204">To learn how to connect IIS Manager to App Service, see [Remote administration of Azure websites by using IIS Manager](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).</span></span>
2. <span data-ttu-id="4e0c6-205">在 IIS 管理員中，新增或編輯 URL 重寫規則。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-205">In IIS Manager, add or edit a URL rewrite rule.</span></span> <span data-ttu-id="4e0c6-206">若要了解如何新增或編輯 URL 重寫規則，請參閱[建立 URL 重寫模組的重寫規則](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-206">To learn how to add or edit a URL rewrite rule, see [Create rewrite rules for the URL rewrite module](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).</span></span>

## <a name="how-do-i-control-inbound-traffic-to-app-service"></a><span data-ttu-id="4e0c6-207">如何控制 App Service 的輸入流量？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-207">How do I control inbound traffic to App Service?</span></span>

<span data-ttu-id="4e0c6-208">在網站層級中，您有兩個選項可以用來控制 App Service 的輸入流量：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-208">At the site level, you have two options for controlling inbound traffic to App Service:</span></span>

* <span data-ttu-id="4e0c6-209">開啟動態 IP 限制。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-209">Turn on dynamic IP restrictions.</span></span> <span data-ttu-id="4e0c6-210">若要深入了解如何開啟動態 IP 限制，請參閱 [Azure 網站的 IP 和網域限制](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-210">To learn how to turn on dynamic IP restrictions, see [IP and domain restrictions for Azure websites](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).</span></span>
* <span data-ttu-id="4e0c6-211">開啟模組安全性。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-211">Turn on Module Security.</span></span> <span data-ttu-id="4e0c6-212">若要了解如何開啟模組安全性，請參閱 [Azure 網站上的 ModSecurity Web 應用程式防火牆](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-212">To learn how to turn on Module Security, see [ModSecurity web application firewall on Azure websites](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).</span></span>

<span data-ttu-id="4e0c6-213">如果您使用 App Service Environment，您可以使用 [Barracuda 防火牆](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-213">If you use App Service Environment, you can use [Barracuda firewall](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).</span></span>

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a><span data-ttu-id="4e0c6-214">如何封鎖 App Service Web 應用程式中的連接埠？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-214">How do I block ports in an App Service web app?</span></span>

<span data-ttu-id="4e0c6-215">在 App Service 共用租用戶環境中，因為基礎結構的本質，所以無法封鎖特定連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-215">In the App Service shared tenant environment, it is not possible to block specific ports because of the nature of the infrastructure.</span></span> <span data-ttu-id="4e0c6-216">TCP 連接埠 4016、4018 和 4020 也可能已經針對 Visual Studio 遠端偵錯而開啟。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-216">TCP ports 4016, 4018, and 4020 also might be open for Visual Studio remote debugging.</span></span>

<span data-ttu-id="4e0c6-217">在 App Service Environment 中，您對於輸入與輸出流量有完整控制權。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-217">In App Service Environment, you have full control over inbound  and outbound traffic.</span></span> <span data-ttu-id="4e0c6-218">您可以使用網路安全性群組來限制或封鎖特定連接埠。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-218">You can use Network Security Groups to restrict or block specific ports.</span></span> <span data-ttu-id="4e0c6-219">如需 App Service Environment 的詳細資訊，請參閱[App Service Environment 簡介](https://azure.microsoft.com/blog/introducing-app-service-environment/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-219">For more information about App Service Environment, see [Introducing App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/).</span></span>

## <a name="how-do-i-capture-an-f12-trace"></a><span data-ttu-id="4e0c6-220">如何擷取 F12 追蹤？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-220">How do I capture an F12 trace?</span></span>

<span data-ttu-id="4e0c6-221">您有兩個選項可以用來擷取 F12 追蹤：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-221">You have two options for capturing an F12 trace:</span></span>

* <span data-ttu-id="4e0c6-222">F12 HTTP 追蹤</span><span class="sxs-lookup"><span data-stu-id="4e0c6-222">F12 HTTP trace</span></span>
* <span data-ttu-id="4e0c6-223">F12 主控台輸出</span><span class="sxs-lookup"><span data-stu-id="4e0c6-223">F12 console output</span></span>

### <a name="f12-http-trace"></a><span data-ttu-id="4e0c6-224">F12 HTTP 追蹤</span><span class="sxs-lookup"><span data-stu-id="4e0c6-224">F12 HTTP trace</span></span>

1. <span data-ttu-id="4e0c6-225">在 Internet Explorer 中，移至您的網站。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-225">In Internet Explorer, go to your website.</span></span> <span data-ttu-id="4e0c6-226">請務必在執行下一個步驟之前登入。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-226">It's important to sign in before you do the next steps.</span></span> <span data-ttu-id="4e0c6-227">否則，F12 追蹤會擷取敏感性登入資料。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-227">Otherwise, the F12 trace captures sensitive sign-in data.</span></span>
2. <span data-ttu-id="4e0c6-228">按下 F12。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-228">Press F12.</span></span>
3. <span data-ttu-id="4e0c6-229">確認 [網路] 索引標籤已選取，然後選取綠色 [播放] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-229">Verify that the **Network** tab is selected, and then select the green **Play** button.</span></span>
4. <span data-ttu-id="4e0c6-230">執行重現問題的步驟。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-230">Do the steps that reproduce the issue.</span></span>
5. <span data-ttu-id="4e0c6-231">選取紅色 [停止] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-231">Select the red **Stop** button.</span></span>
6. <span data-ttu-id="4e0c6-232">選取 [儲存]按鈕 (磁片圖示)，並儲存 HAR 檔案 (在 Internet Explorer 和 Edge 中) 或者以滑鼠右鍵按一下 HAR 檔案，然後選取 [內容另存為 HAR] \(在 Chrome 中)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-232">Select the **Save** button (disk icon), and save the HAR file (in Internet Explorer and Edge) *or* right-click the HAR file, and then select **Save as HAR with content** (in Chrome).</span></span>

### <a name="f12-console-output"></a><span data-ttu-id="4e0c6-233">F12 主控台輸出</span><span class="sxs-lookup"><span data-stu-id="4e0c6-233">F12 console output</span></span>

1. <span data-ttu-id="4e0c6-234">選取 [主控台] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-234">Select the **Console** tab.</span></span>
2. <span data-ttu-id="4e0c6-235">對於包含零個以上項目的每個索引標籤，選取索引標籤 (**錯誤**、**警告**或**資訊**)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-235">For each tab that contains more than zero items, select the tab (**Error**, **Warning**, or **Information**).</span></span> <span data-ttu-id="4e0c6-236">如果沒有選取索引標籤，當您將資料指標移開該索引標籤時，索引標籤圖示是灰色或黑色。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-236">If the tab isn’t selected, the tab icon is gray or black when you move the cursor away from it.</span></span>
3. <span data-ttu-id="4e0c6-237">以滑鼠右鍵按一下窗格的訊息區域，然後選取 [全部複製]。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-237">Right-click in the message area of the pane, and then select **Copy all**.</span></span>
4. <span data-ttu-id="4e0c6-238">在檔案中貼上複製的文字，然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-238">Paste the copied text in a file, and then save the file.</span></span>

<span data-ttu-id="4e0c6-239">若要檢視 HAR 檔案，您可以使用 [HAR 檢視器](http://www.softwareishard.com/har/viewer/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-239">To view an HAR file, you can use the [HAR viewer](http://www.softwareishard.com/har/viewer/).</span></span>

## <a name="why-do-i-get-an-error-when-i-try-to-connect-an-app-service-web-app-to-a-virtual-network-that-is-connected-to-expressroute"></a><span data-ttu-id="4e0c6-240">為什麼當我嘗試將 App Service Web 應用程式連線到虛擬網路 (已連線到 ExpressRoute) 時遇到錯誤？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-240">Why do I get an error when I try to connect an App Service web app to a virtual network that is connected to ExpressRoute?</span></span>

<span data-ttu-id="4e0c6-241">如果您嘗試將 Azure Web 應用程式連線到已連線至 Azure ExpressRoute 的虛擬網路，就會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-241">If you try to connect an Azure web app to a virtual network that's connected to Azure ExpressRoute, it fails.</span></span> <span data-ttu-id="4e0c6-242">會出現下列訊息：「閘道不是 VPN 閘道」。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-242">The following message appears: "Gateway is not a VPN gateway."</span></span>

<span data-ttu-id="4e0c6-243">目前，您對於已連線至 ExpressRoute 的虛擬網路不能使用點對站 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-243">Currently, you cannot have point-to-site VPN connections to a virtual network that is connected to ExpressRoute.</span></span> <span data-ttu-id="4e0c6-244">點對站 VPN 和 ExpressRoute 不能並存在相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-244">A point-to-site VPN and ExpressRoute cannot coexist for the same virtual network.</span></span> <span data-ttu-id="4e0c6-245">如需詳細資訊，請參閱 [ExpressRoute 和站對站 VPN 連線限制](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-245">For more information, see [ExpressRoute and site-to-site VPN connections limits and limitations](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).</span></span>

## <a name="how-do-i-connect-an-app-service-web-app-to-a-virtual-network-that-has-a-static-routing-policy-based-gateway"></a><span data-ttu-id="4e0c6-246">如何將 App Service Web 應用程式連線至具有靜態路由 (以原則為基礎) 閘道的虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-246">How do I connect an App Service web app to a virtual network that has a static routing (policy-based) gateway?</span></span>

<span data-ttu-id="4e0c6-247">目前，不支援將 App Service Web 應用程式連線至具有靜態路由 (以原則為基礎) 閘道的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-247">Currently, connecting an App Service web app to a virtual network that has a static routing (policy-based) gateway is not supported.</span></span> <span data-ttu-id="4e0c6-248">如果目標虛擬網路已存在，您必須先以動態路由閘道器啟用其點對站 VPN，才能使該虛擬網路與應用程式連線。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-248">If your target virtual network already exists, it must have point-to-site VPN enabled, with a dynamic routing gateway, before it can be connected to an app.</span></span> <span data-ttu-id="4e0c6-249">如果您的閘道設定為靜態路由，您無法啟用點對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-249">If your gateway is set to static routing, you cannot enable a point-to-site VPN.</span></span> 

<span data-ttu-id="4e0c6-250">如需詳細資訊，請參閱[將應用程式與 Azure 虛擬網路整合](web-sites-integrate-with-vnet.md#getting-started)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-250">For more information, see [Integrate an app with an Azure virtual network](web-sites-integrate-with-vnet.md#getting-started).</span></span>

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a><span data-ttu-id="4e0c6-251">為什麼我就算有 2 個可用的背景工作角色，卻還是只能在 App Service Environment 中建立一個 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-251">In my App Service Environment, why can I create only one App Service plan, even though I have two workers available?</span></span>

<span data-ttu-id="4e0c6-252">為了提供容錯功能，App Service Environment 要求每個背景工作角色集區需要至少一個額外的計算資源。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-252">To provide fault tolerance, App Service Environment requires that each worker pool needs at least one additional compute resource.</span></span> <span data-ttu-id="4e0c6-253">不能對額外的計算資源指派工作負載。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-253">The additional compute resource cannot be assigned a workload.</span></span>

<span data-ttu-id="4e0c6-254">如需詳細資訊，請參閱[如何建立 App Service Environment](app-service-web-how-to-create-an-app-service-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-254">For more information, see [How to create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

## <a name="why-do-i-see-timeouts-when-i-try-to-create-an-app-service-environment"></a><span data-ttu-id="4e0c6-255">為什麼當我嘗試建立 App Service Environment 時看到逾時？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-255">Why do I see timeouts when I try to create an App Service Environment?</span></span>

<span data-ttu-id="4e0c6-256">有時候，建立 App Service Environment 會失敗。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-256">Sometimes, creating an App Service Environment fails.</span></span> <span data-ttu-id="4e0c6-257">在此情況下，您會在活動記錄中看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-257">In that case, you see the following error in the Activity logs:</span></span>
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"The resource provision operation did not complete within the allowed timeout period.”}}
```

<span data-ttu-id="4e0c6-258">若要解決此問題，請確定下列條件均不成立：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-258">To resolve this, make sure that none of the following conditions are true:</span></span>
* <span data-ttu-id="4e0c6-259">子網路太小。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-259">The subnet is too small.</span></span>
* <span data-ttu-id="4e0c6-260">子網路並非空白。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-260">The subnet is not empty.</span></span>
* <span data-ttu-id="4e0c6-261">ExpressRoute 阻止 App Service Environment 的網路連線需求。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-261">ExpressRoute prevents the network connectivity requirements of an App Service Environment.</span></span>
* <span data-ttu-id="4e0c6-262">不正確的網路安全性群組會阻止 App Service Environment 的網路連線需求。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-262">A bad Network Security Group prevents the network connectivity requirements of an App Service Environment.</span></span>
* <span data-ttu-id="4e0c6-263">強制通道已開啟。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-263">Forced tunneling is turned on.</span></span>

<span data-ttu-id="4e0c6-264">如需詳細資訊，請參閱[部署 (建立) 新的 Azure App Service Environment 時最常遇到的問題](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-264">For more information, see [Frequent issues when deploying (creating) a new Azure App Service Environment](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).</span></span>

## <a name="why-cant-i-delete-my-app-service-plan"></a><span data-ttu-id="4e0c6-265">為什麼我無法刪除 App Service 方案？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-265">Why can't I delete my App Service plan?</span></span>

<span data-ttu-id="4e0c6-266">如果任何 App Service 應用程式與 App Service 方案相關聯，您就無法刪除 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-266">You can't delete an App Service plan if any App Service apps are associated with the App Service plan.</span></span> <span data-ttu-id="4e0c6-267">刪除 App Service 方案之前，請從 App Service 方案中移除所有相關聯的 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-267">Before you delete an App Service plan, remove all associated App Service apps from the App Service plan.</span></span>

## <a name="how-do-i-schedule-a-webjob"></a><span data-ttu-id="4e0c6-268">如何排程 WebJob？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-268">How do I schedule a WebJob?</span></span>

<span data-ttu-id="4e0c6-269">您可以使用 Cron 運算式建立已排程 WebJob：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-269">You can create a scheduled WebJob by using Cron expressions:</span></span>

1. <span data-ttu-id="4e0c6-270">建立 settings.job 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-270">Create a settings.job file.</span></span>
2. <span data-ttu-id="4e0c6-271">在此 JSON 檔案中，使用 Cron 運算式以包含排程屬性：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-271">In this JSON file, include a schedule property by using a Cron expression:</span></span> 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of the week}" }
    ```

<span data-ttu-id="4e0c6-272">如需已排程 WebJobs 的詳細資訊，請參閱[使用 Cron 運算式來建立已排程 WebJob](web-sites-create-web-jobs.md#CreateScheduledCRON)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-272">For more information about scheduled WebJobs, see [Create a scheduled WebJob by using a Cron expression](web-sites-create-web-jobs.md#CreateScheduledCRON).</span></span>

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a><span data-ttu-id="4e0c6-273">如何執行 App Service 應用程式的滲透測試？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-273">How do I perform penetration testing for my App Service app?</span></span>

<span data-ttu-id="4e0c6-274">若要執行滲透測試，請[提交要求](https://security-forms.azure.com/penetration-testing/terms)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-274">To perform penetration testing, [submit a request](https://security-forms.azure.com/penetration-testing/terms).</span></span>

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a><span data-ttu-id="4e0c6-275">如何針對使用流量管理員的 App Service Web 應用程式設定自訂網域名稱？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-275">How do I configure a custom domain name for an App Service web app that uses Traffic Manager?</span></span>

<span data-ttu-id="4e0c6-276">若要深入了解如何搭配使用自訂網域名稱與 App Service 應用程式 (使用 Azure 流量管理員)，以進行負載平衡，請參閱[設定具有流量管理員之 Azure Web 應用程式的自訂網域名稱](web-sites-traffic-manager-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-276">To learn how to use a custom domain name with an App Service app that uses Azure Traffic Manager for load balancing, see [Configure a custom domain name for an Azure web app with Traffic Manager](web-sites-traffic-manager-custom-domain-name.md).</span></span>

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a><span data-ttu-id="4e0c6-277">我的 App Service 憑證標示為詐騙。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-277">My App Service certificate is flagged for fraud.</span></span> <span data-ttu-id="4e0c6-278">如何解決這個問題？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-278">How do I resolve this?</span></span>

<span data-ttu-id="4e0c6-279">在 App Service 憑證購買的網域驗證期間，您可能會看到下列訊息：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-279">During the domain verification of an App Service certificate purchase, you might see the following message:</span></span>

<span data-ttu-id="4e0c6-280">「您的憑證已標示為可能詐騙。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-280">“Your certificate has been flagged for possible fraud.</span></span> <span data-ttu-id="4e0c6-281">要求目前正在進行檢閱。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-281">The request is currently under review.</span></span> <span data-ttu-id="4e0c6-282">如果憑證在 24 小時內無法成為可使用，請連絡 Azure 支援」。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-282">If the certificate does not become usable within 24 hours, please contact Azure Support.”</span></span>

<span data-ttu-id="4e0c6-283">此訊息表示，這個詐騙驗證程序可能需要 24 小時才能完成。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-283">As the message indicates, this fraud verification process might take up to 24 hours to complete.</span></span> <span data-ttu-id="4e0c6-284">在此期間，您將會持續看到訊息。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-284">During this time, you'll continue to see the message.</span></span>

<span data-ttu-id="4e0c6-285">如果您的 App Service 憑證在 24 小時後持續顯示此訊息，請執行下列 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-285">If your App Service certificate continues to show this message after 24 hours, please run the following PowerShell script.</span></span> <span data-ttu-id="4e0c6-286">指令碼會直接連絡[憑證提供者](https://www.godaddy.com/)以解決此問題。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-286">The script contacts the [certificate provider](https://www.godaddy.com/) directly to resolve the issue.</span></span>

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a><span data-ttu-id="4e0c6-287">驗證和授權如何在 App Service 中運作？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-287">How do authentication and authorization work in App Service?</span></span>

<span data-ttu-id="4e0c6-288">如需 App Service 中驗證和授權的詳細文件，請參閱 [App Service 安全性](../app-service/app-service-security-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-288">For detailed documentation for authentication and authorization in App Service, see [App Service security](../app-service/app-service-security-readme.md).</span></span> <span data-ttu-id="4e0c6-289">文件也有設定 App Service 以使用各種身分識別提供者登入的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-289">The documentation also has information about setting up App Service to use various identify provider sign-ins:</span></span>
* [<span data-ttu-id="4e0c6-290">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4e0c6-290">Azure Active Directory</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [<span data-ttu-id="4e0c6-291">Facebook</span><span class="sxs-lookup"><span data-stu-id="4e0c6-291">Facebook</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [<span data-ttu-id="4e0c6-292">Google</span><span class="sxs-lookup"><span data-stu-id="4e0c6-292">Google</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [<span data-ttu-id="4e0c6-293">Microsoft 帳戶</span><span class="sxs-lookup"><span data-stu-id="4e0c6-293">Microsoft Account</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [<span data-ttu-id="4e0c6-294">Twitter</span><span class="sxs-lookup"><span data-stu-id="4e0c6-294">Twitter</span></span>](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-the-default-azurewebsitesnet-domain-to-my-azure-web-apps-custom-domain"></a><span data-ttu-id="4e0c6-295">如何將預設 *.azurewebsites.net 網域重新導向至我的 Azure Web 應用程式的自訂網域？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-295">How do I redirect the default *.azurewebsites.net domain to my Azure web app's custom domain?</span></span>

<span data-ttu-id="4e0c6-296">當您使用 Azure 中的 Web 應用程式建立新網站時，預設 sitename.azurewebsites.net 網域會指派至您的網站。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-296">When you create a new website by using Web Apps in Azure, a default *sitename*.azurewebsites.net domain is assigned to your site.</span></span> <span data-ttu-id="4e0c6-297">如果您將自訂主機名稱新增至您的網站，且不想讓使用者能夠存取您的預設 *.azurewebsites.net 網域，您可以重新導向預設 URL。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-297">If you add a custom host name to your site and don’t want users to be able to access your default *.azurewebsites.net domain, you can redirect the default URL.</span></span> <span data-ttu-id="4e0c6-298">若要深入了解如何將網站預設網域的所有流量重新導向至自訂網域，請參閱[將預設網域重新導向至 Azure Web 應用程式中的自訂網域](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-298">To learn how to redirect all traffic from your website's default domain to your custom domain, see [Redirect the default domain to your custom domain in Azure web apps](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).</span></span>

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a><span data-ttu-id="4e0c6-299">如何判斷安裝在 App Service 中的是哪一個版本的 .NET？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-299">How do I determine which version of .NET version is installed in App Service?</span></span>

<span data-ttu-id="4e0c6-300">尋找 App Service 中已安裝之 Microsoft.NET 版本的最快方式是使用 Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-300">The quickest way to find the version of Microsoft .NET that's installed in App Service is by using the Kudu console.</span></span> <span data-ttu-id="4e0c6-301">您可以從入口網站或使用 App Service 應用程式的 URL 來存取 Kudu 主控台。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-301">You can access the Kudu console from the portal or by using the URL of your App Service app.</span></span> <span data-ttu-id="4e0c6-302">如需詳細指示，請參閱[判斷 App Service 中安裝的 .NET 版本](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-302">For detailed instructions, see [Determine the installed .NET version in App Service](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).</span></span>

## <a name="why-isnt-autoscale-working-as-expected"></a><span data-ttu-id="4e0c6-303">為什麼自動調整無法如預期般運作？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-303">Why isn't Autoscale working as expected?</span></span>

<span data-ttu-id="4e0c6-304">如果 Azure 自動調整尚未如您預期地相應縮小或相應放大 Web 應用程式執行個體，您可能會進入我們故意選擇不調整以避免因為「flapping」而造成無限迴圈的案例。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-304">If Azure Autoscale hasn't scaled in or scaled out the web app instance as you expected, you might be running into a scenario in which we intentionally choose not to scale to avoid an infinite loop due to "flapping."</span></span> <span data-ttu-id="4e0c6-305">當相應放大或相應縮小閾值之間沒有足夠邊界時，就會發生這種情形。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-305">This usually happens when there isn't an adequate margin between the scale-out and scale-in thresholds.</span></span> <span data-ttu-id="4e0c6-306">若要深入了解如何避免「flapping」以及了解其他自動調整最佳做法，請參閱[自動調整最佳做法](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-306">To learn how to avoid "flapping" and to read about other Autoscale best practices, see [Autoscale best practices](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).</span></span>

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a><span data-ttu-id="4e0c6-307">為什麼自動調整有時候只會部分調整？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-307">Why does Autoscale sometimes scale only partially?</span></span>

<span data-ttu-id="4e0c6-308">當計量超出預先設定的界限時，會觸發自動調整。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-308">Autoscale is triggered when metrics exceed preconfigured boundaries.</span></span> <span data-ttu-id="4e0c6-309">有時候，您可能會注意到，相較於您的預期，容量只有部分填滿。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-309">Sometimes, you might notice that the capacity is only partially filled compared to what you expected.</span></span> <span data-ttu-id="4e0c6-310">無法使用您想要的執行個體數目時，也可能會發生這個情形。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-310">This might occur when the number of instances you want are not available.</span></span> <span data-ttu-id="4e0c6-311">在該案例中，自動調整會部分填滿可用的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-311">In that scenario, Autoscale partially fills in with the available number of instances.</span></span> <span data-ttu-id="4e0c6-312">然後自動調整會執行重新平衡邏輯，以取得更多容量。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-312">Autoscale then runs the rebalance logic to get more capacity.</span></span> <span data-ttu-id="4e0c6-313">它會配置剩餘的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-313">It allocates the remaining instances.</span></span> <span data-ttu-id="4e0c6-314">請注意，這可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-314">Note that this might take a few minutes.</span></span>

<span data-ttu-id="4e0c6-315">如果您在幾分鐘之後沒有看到預期的執行個體數目，可能是因為部分填滿已足以攜帶界限內的計量。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-315">If you don't see the expected number of instances after a few minutes, it might be because the partial refill was enough to bring the metrics within the boundaries.</span></span> <span data-ttu-id="4e0c6-316">或者，自動調整可能已經相應減少，因為它已達到計量下限。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-316">Or, Autoscale might have scaled down because it reached the lower metrics boundary.</span></span>

<span data-ttu-id="4e0c6-317">如果這些條件都不適用，而且問題持續發生，請提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-317">If none of these conditions apply and the problem persists, submit a support request.</span></span>

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a><span data-ttu-id="4e0c6-318">如何針對內容開啟 HTTP 壓縮？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-318">How do I turn on HTTP compression for my content?</span></span>

<span data-ttu-id="4e0c6-319">若要同時對靜態和動態內容類型開啟壓縮，請將下列程式碼新增至應用程式層級的 web.config 檔案：</span><span class="sxs-lookup"><span data-stu-id="4e0c6-319">To turn on compression both for static and dynamic content types, add the following code to the application-level web.config file:</span></span>

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

<span data-ttu-id="4e0c6-320">您也可以指定您想要壓縮的特定動態和靜態 MIME 類型。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-320">You also can specify the specific dynamic and static MIME types that you want to compress.</span></span> <span data-ttu-id="4e0c6-321">如需詳細資訊，請參閱[簡單 Azure 網站上的 httpCompression 設定](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview)中，我們對於論壇問題的回應。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-321">For more information, see our response to a forum question in [httpCompression settings on a simple Azure website](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).</span></span>

## <a name="how-do-i-migrate-from-an-on-premises-environment-to-app-service"></a><span data-ttu-id="4e0c6-322">如何從內部部署環境移轉至 App Service？</span><span class="sxs-lookup"><span data-stu-id="4e0c6-322">How do I migrate from an on-premises environment to App Service?</span></span>

<span data-ttu-id="4e0c6-323">若要將網站從 Windows 和 Linux 網頁伺服器移轉至 App Service，您可以使用 Azure App Service 移轉小幫手。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-323">To migrate sites from Windows and Linux web servers to App Service, you can use Azure App Service Migration Assistant.</span></span> <span data-ttu-id="4e0c6-324">移轉工具會視需要在 Azure 中建立 Web 應用程式和資料庫，然後發佈內容。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-324">The migration tool creates web apps and databases in Azure as needed, and then publishes the content.</span></span> <span data-ttu-id="4e0c6-325">如需詳細資訊，請參閱 [Azure App Service 移轉小幫手](https://www.movemetothecloud.net/)。</span><span class="sxs-lookup"><span data-stu-id="4e0c6-325">For more information, see [Azure App Service Migration Assistant](https://www.movemetothecloud.net/).</span></span>
