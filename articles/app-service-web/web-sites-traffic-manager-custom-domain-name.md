---
title: "在使用流量管理員進行負載平衡的 Azure App Service 中設定 Web 應用程式的自訂網域名稱。"
description: "在包含負載平衡的流量管理員的 Azure App Service 中使用 Web 應用程式的自訂網域名稱。"
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 5f099201d9018a6f8577cb3daf127d09560fb94b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="abbab-103">在使用流量管理員的 Azure App Service 中設定 Web 應用程式的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="abbab-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="abbab-104">本文提供對 Azure App Service (使用流量管理員進行負載平衡的網站) 使用自訂網域名稱的一般指示。</span><span class="sxs-lookup"><span data-stu-id="abbab-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="abbab-105">了解 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="abbab-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="abbab-106">將 Web 應用程式設定為標準模式</span><span class="sxs-lookup"><span data-stu-id="abbab-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="abbab-107">新增自訂網域的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="abbab-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="abbab-108">如果您已透過 Azure App Service Web Apps 購買網域，請略過下列步驟，並參閱 [購買 Web Apps 網域](custom-dns-web-site-buydomains-web-app.md) 文章的最後一個步驟。</span><span class="sxs-lookup"><span data-stu-id="abbab-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="abbab-109">若要將您的自訂網域與 Azure App Service 的 Web 應用程式建立關聯，必須在 DNS 表格中為您的自訂網域新增項目，方法是使用您向其購買網域名稱之網域註冊機構所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="abbab-109">To associate your custom domain with a web app in Azure App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by the domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="abbab-110">使用下列步驟來尋找並使用 DNS 工具。</span><span class="sxs-lookup"><span data-stu-id="abbab-110">Use the following steps to locate and use the DNS tools.</span></span>

1. <span data-ttu-id="abbab-111">在網域註冊機構登入您的帳戶，並尋找用於管理 DNS 記錄的頁面。</span><span class="sxs-lookup"><span data-stu-id="abbab-111">Sign in to your account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="abbab-112">在網站中尋找標示為 **Domain Name**、**DNS** 或 **Name Server Management** 的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="abbab-112">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="abbab-113">通常該頁面的連結可透過檢視您的帳戶資訊，然後尋找 **我的網域**之類的連結來找到。</span><span class="sxs-lookup"><span data-stu-id="abbab-113">Often a link to this page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="abbab-114">一旦找到網域名稱的管理頁面，請尋找可讓您編輯 DNS 記錄的連結。</span><span class="sxs-lookup"><span data-stu-id="abbab-114">Once you have found the management page for your domain name, look for a link that allows you to edit the DNS records.</span></span> <span data-ttu-id="abbab-115">這可能會以 **Zone file****DNS Records** 或 **Advanced** 組態連結的形式列出。</span><span class="sxs-lookup"><span data-stu-id="abbab-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="abbab-116">頁面上可能已建立一些記錄，例如將 '**@**' 或 '\*' 與 'domain parking' (網域停放) 頁面建立關聯的項目。</span><span class="sxs-lookup"><span data-stu-id="abbab-116">The page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="abbab-117">它也可能包含常見子網域 (如 **www**) 的記錄。</span><span class="sxs-lookup"><span data-stu-id="abbab-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="abbab-118">頁面上會提及 **CNAME 記錄**，或提供選取記錄類型的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="abbab-118">The page will mention **CNAME records**, or provide a drop-down to select a record type.</span></span> <span data-ttu-id="abbab-119">它也可能提及其他記錄 (如 **A 記錄**和 **MX 記錄**)。</span><span class="sxs-lookup"><span data-stu-id="abbab-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="abbab-120">在部分情況下，會以其他名稱來稱呼 CNAME 記錄，如 **別名記錄**。</span><span class="sxs-lookup"><span data-stu-id="abbab-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="abbab-121">頁面上也會有可讓您將**主機名稱**或**網域名稱****對應**為其他網域名稱的欄位。</span><span class="sxs-lookup"><span data-stu-id="abbab-121">The page will also have fields that allow you to **map** from a **Host name** or **Domain name** to another domain name.</span></span>
3. <span data-ttu-id="abbab-122">由於每個註冊機構的特殊要求可能有所不同，一般來說，您會「從」自訂網域名稱 (例如 **contoso.com**) 對應「至」您 Web 應用程式使用的流量管理員網域名稱 (**contoso.trafficmanager.net**)。</span><span class="sxs-lookup"><span data-stu-id="abbab-122">While the specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* the Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="abbab-123">或者，如果記錄已在使用中，而您需要事先將您的應用程式繫結到該記錄，您可以建立其他的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="abbab-123">Alternatively, if a record is already in use and you need to preemptively bind your apps to it, you can create an additional CNAME record.</span></span> <span data-ttu-id="abbab-124">例如，若要事先將 **www.contoso.com** 繫結至 Web 應用程式，請建立從 **awverify.www** 至 **contoso.trafficmanager.net** 的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="abbab-124">For example, to preemptively bind **www.contoso.com** to your web app, create a CNAME record from **awverify.www** to **contoso.trafficmanager.net**.</span></span> <span data-ttu-id="abbab-125">然後，您可以將 "www.contoso.com" 新增至 Web 應用程式，而不必變更 "www" CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="abbab-125">You can then add "www.contoso.com" to your Web App without changing the "www" CNAME record.</span></span> <span data-ttu-id="abbab-126">如需詳細資訊，請參閱[在自訂網域中建立 Web 應用程式的 DNS 記錄][CREATEDNS]。</span><span class="sxs-lookup"><span data-stu-id="abbab-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="abbab-127">在註冊機構處將新增或修改 DNS 記錄的作業完成後，請儲存變更。</span><span class="sxs-lookup"><span data-stu-id="abbab-127">Once you have finished adding or modifying DNS records at your registrar, save the changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="abbab-128">啟用流量管理員</span><span class="sxs-lookup"><span data-stu-id="abbab-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="abbab-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="abbab-129">Next steps</span></span>
<span data-ttu-id="abbab-130">如需詳細資訊，請參閱 [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="abbab-130">For more information, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
