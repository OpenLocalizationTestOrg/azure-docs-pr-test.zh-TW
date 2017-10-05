---
title: "在雲端服務中設定自訂網域名稱 | Microsoft Docs"
description: "了解如何藉由 DNS 設定，公開您的 Azure 應用程式或資料到自訂網域的網際網路上。  這些範例使用 Azure 入口網站。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 5783a246-a151-4fb1-b488-441bfb29ee44
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: cf43d86dddc3a68573e1ba1b09118c54f0b16bc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="833ef-104">設定 Azure 雲端服務的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="833ef-104">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="833ef-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="833ef-105">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="833ef-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="833ef-106">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="833ef-107">當您建立雲端服務時，Azure 會將它指派給 **cloudapp.net**的子網域。</span><span class="sxs-lookup"><span data-stu-id="833ef-107">When you create a Cloud Service, Azure assigns it to a subdomain of **cloudapp.net**.</span></span> <span data-ttu-id="833ef-108">例如，如果您的雲端服務的名稱為 "contoso"，您的使用者可以透過類似 http://contoso.cloudapp.net 的 URL 存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="833ef-108">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="833ef-109">Azure 也會指派虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-109">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="833ef-110">不過，您也可以在自己的網域名稱 (例如 **contoso.com**) 上公開您的應用程式。本文說明如何保留或設定雲端服務 Web 角色的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="833ef-110">However, you can also expose your application on your own domain name, such as **contoso.com**. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="833ef-111">您已經了解什麼是 CNAME 和 A 記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="833ef-111">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="833ef-112">[跳過說明](#add-a-cname-record-for-your-custom-domain)。</span><span class="sxs-lookup"><span data-stu-id="833ef-112">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="833ef-113">此工作的程序適用於 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="833ef-113">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="833ef-114">如需應用程式服務的資訊，請參閱 [這裡](../app-service-web/web-sites-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-114">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="833ef-115">如需儲存體帳戶的資訊，請參閱 [這裡](../storage/blobs/storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-115">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

<p/>

> [!TIP]
> <span data-ttu-id="833ef-116">快速完成啟用 -- 使用全新的 Azure [引導式逐步解說](http://support.microsoft.com/kb/2990804)！</span><span class="sxs-lookup"><span data-stu-id="833ef-116">Get going faster--use the NEW Azure [guided walkthrough](http://support.microsoft.com/kb/2990804)!</span></span>  <span data-ttu-id="833ef-117">在彈指之間完成自訂網域名稱的關聯，以及與 Azure 雲端服務或 Azure 網站之間的通訊 (SSL) 保護。</span><span class="sxs-lookup"><span data-stu-id="833ef-117">It makes associating a custom domain name AND securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="833ef-118">了解 CNAME 和 A 記錄</span><span class="sxs-lookup"><span data-stu-id="833ef-118">Understand CNAME and A records</span></span>
<span data-ttu-id="833ef-119">CNAME (或別名記錄) 和 A 記錄都可讓您將網域名稱和特定的伺服器 (在此案例中為服務) 產生關聯，但運作方式不同。</span><span class="sxs-lookup"><span data-stu-id="833ef-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="833ef-120">針對 Azure 雲端服務來使用 A 記錄時，在決定使用何者之前，還有一些事項應該考慮。</span><span class="sxs-lookup"><span data-stu-id="833ef-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="833ef-121">CNAME 或別名記錄</span><span class="sxs-lookup"><span data-stu-id="833ef-121">CNAME or Alias record</span></span>
<span data-ttu-id="833ef-122">CNAME 記錄將 *特定的* 網域 (例如 **contoso.com** or **www.contoso.com**) 對應到正式網域名稱。</span><span class="sxs-lookup"><span data-stu-id="833ef-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="833ef-123">在此案例中，Canonical 網域名稱為 Azure 主控應用程式的 **[myapp].cloudapp.net** 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="833ef-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="833ef-124">CNAME 建立之後還會建立 **[myapp].cloudapp.net**的別名。</span><span class="sxs-lookup"><span data-stu-id="833ef-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="833ef-125">CNAME 項目會自動解析成 **[myapp].cloudapp.net** 服務的 IP 位址，就算雲端服務的 IP 位址變更，您也不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="833ef-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="833ef-126">使用 CNAME 記錄時，某些網域註冊機構只允許您對應子網域 (如 www.contoso.com)，而不是根名稱 (如 contoso.com)。如需 CNAME 記錄的詳細資訊，請參閱註冊機構提供的文件、[維基百科 CNAME 記錄條目](http://en.wikipedia.org/wiki/CNAME_record)，或 [IETF 網域名稱 - 實作與規格](http://tools.ietf.org/html/rfc1035)文件。</span><span class="sxs-lookup"><span data-stu-id="833ef-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="833ef-127">A 記錄</span><span class="sxs-lookup"><span data-stu-id="833ef-127">A record</span></span>
<span data-ttu-id="833ef-128">A 記錄將網域 (例如 **contoso.com** 或 **www.contoso.com**) 或萬用字元網域 (例如 **\*.contoso.com**) 對應至 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-128">An *A* record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="833ef-129">以 Azure 雲端服務而言，就是指服務的虛擬 IP。</span><span class="sxs-lookup"><span data-stu-id="833ef-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="833ef-130">相較於 CNAME 記錄，A 記錄的主要優點在於只需要有一個項目使用萬用字元，例如 \***.contoso.com**，即可處理多個子網域的要求，例如 **mail.contoso.com**、**login.contoso.com** 或 **www.contso.com**。</span><span class="sxs-lookup"><span data-stu-id="833ef-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="833ef-131">因為 A 記錄會對應至靜態 IP 位址，所以無法自動解析雲端服務 IP 位址的變更。</span><span class="sxs-lookup"><span data-stu-id="833ef-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="833ef-132">第一次將雲端服務部署到空的位置時 (生產或預備)，將會配置雲端服務所使用的 IP 位址。如果刪除此位置的部署，則 Azure 會釋放此 IP 位址，而未來再部署到此位置時，可能會給予新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="833ef-133">在預備和生產部署之間切換時，或就地升級現有的部署時，指定部署位置 (生產或預備) 的 IP 位址會保留下來，相當方便。</span><span class="sxs-lookup"><span data-stu-id="833ef-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="833ef-134">如需關於執行這些動作的詳細資訊，請參閱 [如何管理雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="833ef-135">新增自訂網域的 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="833ef-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="833ef-136">若要建立 CNAME 記錄，您必須使用註冊機構提供的工具，在 DNS 表格中為自訂網域新增項目。</span><span class="sxs-lookup"><span data-stu-id="833ef-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="833ef-137">各註冊機構指定 CNAME 記錄的方法都很類似，只是稍微不同，但概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="833ef-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="833ef-138">使用其中一種方法來尋找指派給雲端服務的 **.cloudapp.net** 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="833ef-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="833ef-139">登入 [Azure 入口網站]，選取您的雲端服務，查看 [基本功能] 區段，然後尋找 [網站 URL] 項目。</span><span class="sxs-lookup"><span data-stu-id="833ef-139">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Site URL** entry.</span></span>
     
       ![快速瀏覽區段，其中顯示網站 URL][csurl]
     
       <span data-ttu-id="833ef-141">**或**</span><span class="sxs-lookup"><span data-stu-id="833ef-141">**OR**</span></span>
   * <span data-ttu-id="833ef-142">安裝並設定 [Azure Powershell](/powershell/azure/overview)，然後使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="833ef-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="833ef-143">請將任一方法傳回的 URL 中所使用的網域名稱儲存下來，建立 CNAME 記錄時需要用到。</span><span class="sxs-lookup"><span data-stu-id="833ef-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="833ef-144">登入 DNS 註冊機構的網站，並移至 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="833ef-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="833ef-145">在網站中尋找標示為 **Domain Name**、**DNS** 或 **Name Server Management** 的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="833ef-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="833ef-146">現在找出可選取或輸入 CNAME 的地方。</span><span class="sxs-lookup"><span data-stu-id="833ef-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="833ef-147">您可能需要從下拉式清單中或移至進階設定頁面，才能選取記錄類型。</span><span class="sxs-lookup"><span data-stu-id="833ef-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="833ef-148">請尋找 **CNAME**、**Alias** 或 **Subdomains** 之類的字。</span><span class="sxs-lookup"><span data-stu-id="833ef-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="833ef-149">如果要建立 **www.customdomain.com** 的別名，您也必須為 CNAME 提供網域或子網域別名，例如 **www**。如果要建立根網域的別名，註冊機構的 DNS 工具中可能會以 '**@**' 符號列出此別名。</span><span class="sxs-lookup"><span data-stu-id="833ef-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="833ef-150">接著，您必須提供正式主機名稱，在此案例中為應用程式的 **cloudapp.net** 網域。</span><span class="sxs-lookup"><span data-stu-id="833ef-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="833ef-151">例如，下列 CNAME 記錄會將來自 **www.contoso.com** 的所有流量，轉送至 **contoso.cloudapp.net** (已部署之應用程式的自訂網域名稱)：</span><span class="sxs-lookup"><span data-stu-id="833ef-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="833ef-152">別名/主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="833ef-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="833ef-153">正式網域</span><span class="sxs-lookup"><span data-stu-id="833ef-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="833ef-154">www</span><span class="sxs-lookup"><span data-stu-id="833ef-154">www</span></span> |<span data-ttu-id="833ef-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="833ef-155">contoso.cloudapp.net</span></span> |

> [!NOTE]
> <span data-ttu-id="833ef-156">**www.contoso.com** 的訪客絕對看不到真正的主機 (contoso.cloudapp.net)，所以使用者不會察覺到轉送過程。</span><span class="sxs-lookup"><span data-stu-id="833ef-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>
> 
> <span data-ttu-id="833ef-157">上述範例僅適用於 **www** 子網域的流量。</span><span class="sxs-lookup"><span data-stu-id="833ef-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="833ef-158">因為 CNAME 記錄不能使用萬用字元，所以您必須為每一個網域/子網域建立一個 CNAME。</span><span class="sxs-lookup"><span data-stu-id="833ef-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="833ef-159">如果要將來自子網域 (例如 *.contoso.com) 的流量導向您的 cloudapp.net 位址，您可以在 DNS 設定中設定 [URL 重新導向] 或 [URL 轉送] 項目，或建立 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="833ef-159">If you want to direct  traffic from subdomains, such as *.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="833ef-160">新增自訂網域的 A 記錄</span><span class="sxs-lookup"><span data-stu-id="833ef-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="833ef-161">若要建立 A 記錄，您必須先找出雲端服務的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="833ef-162">然後，利用註冊機構提供的工具，在 DNS 表格中為自訂網域新增項目。</span><span class="sxs-lookup"><span data-stu-id="833ef-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="833ef-163">各註冊機構指定 A 記錄的方法都很類似，只是稍微不同，但概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="833ef-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="833ef-164">使用下列其中一種方法取得雲端服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="833ef-165">登入 [Azure 入口網站]，選取您的雲端服務，查看 [基本功能] 區段，然後尋找 [公用 IP 位址] 項目。</span><span class="sxs-lookup"><span data-stu-id="833ef-165">Login to the [Azure portal], select your cloud service, look at the **Essentials** section and then find the **Public IP addresses** entry.</span></span>
     
       ![快速瀏覽區段，其中顯示 VIP][vip]
     
       <span data-ttu-id="833ef-167">**或**</span><span class="sxs-lookup"><span data-stu-id="833ef-167">**OR**</span></span>
   * <span data-ttu-id="833ef-168">安裝並設定 [Azure Powershell](/powershell/azure/overview)，然後使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="833ef-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="833ef-169">建立 A 記錄時需要用到此 IP 位址，請儲存下來。</span><span class="sxs-lookup"><span data-stu-id="833ef-169">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="833ef-170">登入 DNS 註冊機構的網站，並移至 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="833ef-170">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="833ef-171">在網站中尋找標示為 **Domain Name**、**DNS** 或 **Name Server Management** 的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="833ef-171">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="833ef-172">現在找出可選取或輸入 A 記錄的地方。</span><span class="sxs-lookup"><span data-stu-id="833ef-172">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="833ef-173">您可能需要從下拉式清單中或移至進階設定頁面，才能選取記錄類型。</span><span class="sxs-lookup"><span data-stu-id="833ef-173">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="833ef-174">選取或輸入將使用此 A 記錄的網域或子網域。</span><span class="sxs-lookup"><span data-stu-id="833ef-174">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="833ef-175">例如，若要建立 **www.customdomain.com** 的別名，請選取 **www**。如果要為所有子網域建立萬用字元項目，請輸入 '*****'。</span><span class="sxs-lookup"><span data-stu-id="833ef-175">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '*****'.</span></span> <span data-ttu-id="833ef-176">這將會涵蓋所有子網域，例如 **mail.customdomain.com**、**login.customdomain.com** 和 **www.customdomain.com**。</span><span class="sxs-lookup"><span data-stu-id="833ef-176">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="833ef-177">如果要建立根網域的 A 記錄，註冊機構的 DNS 工具中可能會以 '**@**' 符號列出此別名。</span><span class="sxs-lookup"><span data-stu-id="833ef-177">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="833ef-178">在提供的欄位中，輸入雲端服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="833ef-178">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="833ef-179">這樣會將 A 記錄中使用的網域項目與雲端服務部署的 IP 位址產生關聯。</span><span class="sxs-lookup"><span data-stu-id="833ef-179">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="833ef-180">例如，下列 A 記錄會將來自 **contoso.com** 的所有流量轉送至 **137.135.70.239** (已部署之應用程式的 IP 位址)：</span><span class="sxs-lookup"><span data-stu-id="833ef-180">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="833ef-181">主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="833ef-181">Host name/Subdomain</span></span> | <span data-ttu-id="833ef-182">IP 位址</span><span class="sxs-lookup"><span data-stu-id="833ef-182">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="833ef-183">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="833ef-183">137.135.70.239</span></span> |

<span data-ttu-id="833ef-184">此範例示範建立根網域的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="833ef-184">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="833ef-185">如果想要建立萬用字元項目來涵蓋所有子網域，請輸入 '*****' 做為子網域。</span><span class="sxs-lookup"><span data-stu-id="833ef-185">If you wish to create a wildcard entry to cover all subdomains, you would enter '*****' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="833ef-186">依預設，Azure 中的 IP 位址是動態的。</span><span class="sxs-lookup"><span data-stu-id="833ef-186">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="833ef-187">您可能想要使用 [保留的 IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md) ，以確保您的 IP 位址不會變更。</span><span class="sxs-lookup"><span data-stu-id="833ef-187">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="833ef-188">後續步驟</span><span class="sxs-lookup"><span data-stu-id="833ef-188">Next steps</span></span>
* [<span data-ttu-id="833ef-189">如何管理雲端服務</span><span class="sxs-lookup"><span data-stu-id="833ef-189">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="833ef-190">如何將 CDN 內容對應至自訂網域</span><span class="sxs-lookup"><span data-stu-id="833ef-190">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="833ef-191">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-191">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="833ef-192">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-192">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="833ef-193">設定 [SSL 憑證](cloud-services-configure-ssl-certificate-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="833ef-193">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: cloud-services-how-to-manage-portal.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure 入口網站]: https://portal.azure.com
[vip]: ./media/cloud-services-custom-domain-name-portal/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name-portal/csurl.png
