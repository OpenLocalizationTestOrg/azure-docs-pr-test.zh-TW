---
title: "aaaConfigure Azure App Service (GoDaddy) 中的自訂網域名稱"
description: "了解 toouse 網域從 GoDaddy 使用 Azure Web 應用程式的名稱"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="09f64-103">在 Azure App Service 中設定自訂網域名稱 (直接向 GoDaddy 購買)</span><span class="sxs-lookup"><span data-stu-id="09f64-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="09f64-104">如果您已購買通過 Azure App Service Web 應用程式網域，則 toohello 最後一個步驟，請參閱[購買 Web 應用程式網域](custom-dns-web-site-buydomains-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="09f64-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="09f64-105">本文提供搭配使用直接從 [GoDaddy](https://godaddy.com) 購買的自訂網域名稱與 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="09f64-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="09f64-106">了解 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="09f64-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="09f64-107">新增自訂網域的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="09f64-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="09f64-108">tooassociate App Service 中的 web 應用程式與您的自訂網域，您必須新增新的項目 hello DNS 資料表中的自訂網域使用 GoDaddy 所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="09f64-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="09f64-109">使用 hello GoDaddy.com 依照步驟 toolocate hello DNS 工具</span><span class="sxs-lookup"><span data-stu-id="09f64-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="09f64-110">登入帳戶 tooyour GoDaddy.com，並選取**我的帳戶**然後**管理我的網域**。</span><span class="sxs-lookup"><span data-stu-id="09f64-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="09f64-111">您想 toouse Azure web 應用程式，並選取 hello 網域名稱的選取 hello 下拉式選單**管理 DNS**。</span><span class="sxs-lookup"><span data-stu-id="09f64-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![custom domain page for GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="09f64-113">從 hello**網域詳細資料**頁面上，捲動 toohello **DNS 區域檔案** 索引標籤。這是 hello 區段用於加入及修改您的網域名稱的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="09f64-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS Zone File tab](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="09f64-115">選取**新增記錄**tooadd 現有的記錄。</span><span class="sxs-lookup"><span data-stu-id="09f64-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="09f64-116">太**編輯**現有記錄、 選取 hello 畫筆及紙張圖示旁邊 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="09f64-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09f64-117">新增記錄之前，請注意，GoDaddy 已為熱門子網域 (在編輯器中稱為**主機**) 建立 DNS 記錄，例如**電子郵件**、**檔案**、**郵件**及其他。</span><span class="sxs-lookup"><span data-stu-id="09f64-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="09f64-118">如果您已經想 toouse hello 名稱存在，而不是建立一個新的 hello 現有記錄的修改。</span><span class="sxs-lookup"><span data-stu-id="09f64-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="09f64-119">當加入資料錄，您必須先選取 hello 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="09f64-119">When adding a record, you must first select hello record type.</span></span>
   
    ![選取記錄類型](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="09f64-121">接下來，您必須提供 hello**主機**(hello 自訂的網域或子網域) 和決定其**指向**。</span><span class="sxs-lookup"><span data-stu-id="09f64-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![新增區域記錄](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="09f64-123">加入時**（主機） 記錄**-您必須設定 hello**主機**欄位 tooeither  **@**  (這代表根網域名稱，例如**contoso.com**，) * （萬用字元比對多的子網域） 或您想 toouse hello 子網域 (例如， **www**。)您必須設定 hello**指向**欄位 toohello Azure web 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="09f64-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="09f64-124">加入時**CNAME （別名） 記錄**-您必須設定 hello**主機**apps toouse 欄位 toohello 子網域。</span><span class="sxs-lookup"><span data-stu-id="09f64-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="09f64-125">例如 **www**。</span><span class="sxs-lookup"><span data-stu-id="09f64-125">For example, **www**.</span></span> <span data-ttu-id="09f64-126">您必須設定 hello**指向**欄位 toohello **。 名稱是.azurewebsites.net** Azure web 應用程式的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="09f64-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="09f64-127">例如，**contoso.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="09f64-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="09f64-128">按一下 [加入另一個] 。</span><span class="sxs-lookup"><span data-stu-id="09f64-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="09f64-129">選取**TXT**和 hello 記錄類型，然後指定**主機**值 **@** 和**指向**值**&lt;yourwebappname&gt;。 名稱是.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="09f64-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09f64-130">Azure toovalidate 您擁有 hello 網域 hello 所記錄或 hello 第一個 TXT 記錄描述會使用這個 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="09f64-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="09f64-131">一旦 hello 網域已對應的 toohello hello Azure 入口網站中的 web 應用程式，就可以移除此 TXT 記錄項目。</span><span class="sxs-lookup"><span data-stu-id="09f64-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="09f64-132">當您完成新增或修改的記錄，按一下**完成**toosave 變更。</span><span class="sxs-lookup"><span data-stu-id="09f64-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="09f64-133">啟用 web 應用程式上的 hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="09f64-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="09f64-134">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="09f64-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="09f64-135">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="09f64-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="09f64-136">變更的項目</span><span class="sxs-lookup"><span data-stu-id="09f64-136">What's changed</span></span>
* <span data-ttu-id="09f64-137">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="09f64-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

