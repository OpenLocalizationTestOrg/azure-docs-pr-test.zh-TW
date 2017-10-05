---
title: "在 Azure App Service 中設定自訂網域名稱 (GoDaddy)"
description: "了解如何搭配使用來自 GoDaddy 的網域名稱與 Azure Web Apps"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="7e0a0-103">在 Azure App Service 中設定自訂網域名稱 (直接向 GoDaddy 購買)</span><span class="sxs-lookup"><span data-stu-id="7e0a0-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="7e0a0-104">如果您已透過 Azure App Service Web Apps 購買網域，請參考 [購買 Web Apps 網域](custom-dns-web-site-buydomains-web-app.md)的最後一個步驟。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="7e0a0-105">本文提供搭配使用直接從 [GoDaddy](https://godaddy.com) 購買的自訂網域名稱與 [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) 的相關指示。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="7e0a0-106">了解 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="7e0a0-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="7e0a0-107">新增自訂網域的 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="7e0a0-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="7e0a0-108">若要將您的自訂網域與 App Service 中的 Web 應用程式產生關聯，您必須使用由 GoDaddy 所提供的工具，在 DNS 資料表中為您的自訂網域新增項目。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="7e0a0-109">在 GoDaddy.com 中，使用下列步驟來尋找 DNS 工具</span><span class="sxs-lookup"><span data-stu-id="7e0a0-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="7e0a0-110">在 GoDaddy.com 中登入您的帳戶，並依序選取 [我的帳戶]、[管理我的網域]。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="7e0a0-111">從下拉式功能表中選取要與 Azure Web 應用程式搭配使用的網域名稱，然後選取 [管理 DNS]。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![custom domain page for GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="7e0a0-113">在 [網域詳細資料] 頁面中，捲動至 [DNS 區域檔案] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="7e0a0-114">此區段可用來新增與修改網域名稱的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![DNS Zone File tab](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="7e0a0-116">選取 [新增記錄]  以新增現有記錄。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="7e0a0-117">若要**編輯**現有記錄，請選取該記錄旁的 [紙筆] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e0a0-118">新增記錄之前，請注意，GoDaddy 已為熱門子網域 (在編輯器中稱為**主機**) 建立 DNS 記錄，例如**電子郵件**、**檔案**、**郵件**及其他。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="7e0a0-119">如果您要使用的名稱已存在，請修改現有記錄，而非建立新記錄。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="7e0a0-120">新增記錄時，您必須先選取記錄類型。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-120">When adding a record, you must first select the record type.</span></span>
   
    ![選取記錄類型](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="7e0a0-122">接下來，您必須提供 [主機] \(自訂網域或子網域) 及其 [指向] 位置。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![新增區域記錄](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="7e0a0-124">新增 [A (主機) 記錄] 時，您必須將 [主機] 欄位設定為 **@** (這代表根網域名稱，例如 **contoso.com**)* (用於比對多個子網域的萬用字元)，或是您要使用的子網域 (例如 **www**)。您必須將 [指向] 欄位設定為 Azure Web 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="7e0a0-125">新增 [CNAME (別名) 記錄] 時，您必須將 [主機] 欄位設定為您要使用的子網域。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="7e0a0-126">例如 **www**。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-126">For example, **www**.</span></span> <span data-ttu-id="7e0a0-127">您必須將 [指向] 欄位設為 Azure Web 應用程式的 **.azurewebsites.net** 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="7e0a0-128">例如，**contoso.azurewebsites.net**。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="7e0a0-129">按一下 [加入另一個] 。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="7e0a0-130">選取 [TXT] 做為記錄類型，然後指定 **@** 的 [主機] 值和 **&lt;yourwebappname&gt;.azurewebsites.net** 的 [指向] 值。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7e0a0-131">Azure 會使用 TXT 記錄來驗證您擁有 A 記錄或第一筆 TXT 記錄所述的網域。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="7e0a0-132">一旦網域對應至 Azure 入口網站中的 Web 應用程式，即可移除此 TXT 記錄項目。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="7e0a0-133">當您完成新增或修改記錄時，請按一下 [完成]  以儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="7e0a0-134">在 Web 應用程式上啟用網域名稱</span><span class="sxs-lookup"><span data-stu-id="7e0a0-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="7e0a0-135">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7e0a0-136">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="7e0a0-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="7e0a0-137">變更的項目</span><span class="sxs-lookup"><span data-stu-id="7e0a0-137">What's changed</span></span>
* <span data-ttu-id="7e0a0-138">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="7e0a0-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

