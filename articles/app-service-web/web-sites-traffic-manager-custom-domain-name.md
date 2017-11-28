---
title: "aaaConfigure web 應用程式中使用流量管理員進行負載平衡的 Azure App Service 中的自訂網域名稱。"
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
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="a7369-103">在使用流量管理員的 Azure App Service 中設定 Web 應用程式的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="a7369-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="a7369-104">本文提供對 Azure App Service (使用流量管理員進行負載平衡的網站) 使用自訂網域名稱的一般指示。</span><span class="sxs-lookup"><span data-stu-id="a7369-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="a7369-105">了解 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="a7369-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="a7369-106">將 Web 應用程式設定為標準模式</span><span class="sxs-lookup"><span data-stu-id="a7369-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="a7369-107">新增自訂網域的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="a7369-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="a7369-108">如果您已購買通過 Azure App Service Web 應用程式網域則略過下列步驟，而且 toohello 最後一個步驟，請參閱[購買 Web 應用程式網域](custom-dns-web-site-buydomains-web-app.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="a7369-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="a7369-109">tooassociate 您使用 Azure App Service 中的 web 應用程式的自訂網域，您必須新增新的項目 hello DNS 資料表中的自訂網域使用 hello 網域註冊機構購買您的網域名稱，從所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="a7369-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="a7369-110">使用下列步驟 toolocate hello 並使用 hello DNS 工具。</span><span class="sxs-lookup"><span data-stu-id="a7369-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="a7369-111">登入 tooyour 帳戶在網域註冊機構，並尋找頁面，以管理 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="a7369-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="a7369-112">查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。</span><span class="sxs-lookup"><span data-stu-id="a7369-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="a7369-113">通常可以找到 toothis 頁面的連結可檢視您帳戶的資訊，和例如尋找連結**我的網域**。</span><span class="sxs-lookup"><span data-stu-id="a7369-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="a7369-114">一旦找到 hello 管理頁面的網域名稱，尋找可讓您 tooedit hello DNS 記錄的連結。</span><span class="sxs-lookup"><span data-stu-id="a7369-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="a7369-115">這可能會以 **Zone file****DNS Records** 或 **Advanced** 組態連結的形式列出。</span><span class="sxs-lookup"><span data-stu-id="a7369-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="a7369-116">hello 頁面最有可能已經建立，例如項目產生關聯的一些記錄 '**@**'或'\*' 與 '網域停車' 頁面。</span><span class="sxs-lookup"><span data-stu-id="a7369-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="a7369-117">它也可能包含常見子網域 (如 **www**) 的記錄。</span><span class="sxs-lookup"><span data-stu-id="a7369-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="a7369-118">hello 頁面會提到**CNAME 記錄**，或是提供下拉式清單 tooselect 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="a7369-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="a7369-119">它也可能提及其他記錄 (如 **A 記錄**和 **MX 記錄**)。</span><span class="sxs-lookup"><span data-stu-id="a7369-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="a7369-120">在部分情況下，會以其他名稱來稱呼 CNAME 記錄，如 **別名記錄**。</span><span class="sxs-lookup"><span data-stu-id="a7369-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="a7369-121">hello 頁面也可讓您太欄位**對應**從**主機名稱**或**網域名稱**tooanother 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="a7369-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="a7369-122">每個註冊機構的 hello 細節有所不同，一般來說您對應*從*自訂網域名稱 (例如**contoso.com**，)*至*hello Traffic Manager 網域名稱 (**contoso.trafficmanager.net**) 所用的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7369-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a7369-123">或者，如果記錄已在使用，而且需要 toopreemptively 繫結的應用程式 tooit，您可以建立額外的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="a7369-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="a7369-124">例如，繫結 toopreemptively **www.contoso.com** tooyour web 應用程式，建立 CNAME 記錄從**awverify.www**太**contoso.trafficmanager.net**。</span><span class="sxs-lookup"><span data-stu-id="a7369-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="a7369-125">然後，您可以加入"www.contoso.com"tooyour Web 應用程式而不需要變更 hello"www"CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="a7369-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="a7369-126">如需詳細資訊，請參閱[在自訂網域中建立 Web 應用程式的 DNS 記錄][CREATEDNS]。</span><span class="sxs-lookup"><span data-stu-id="a7369-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="a7369-127">當您完成後，在加入或修改在註冊機構的 DNS 記錄時，儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="a7369-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="a7369-128">啟用流量管理員</span><span class="sxs-lookup"><span data-stu-id="a7369-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="a7369-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7369-129">Next steps</span></span>
<span data-ttu-id="a7369-130">如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。</span><span class="sxs-lookup"><span data-stu-id="a7369-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
