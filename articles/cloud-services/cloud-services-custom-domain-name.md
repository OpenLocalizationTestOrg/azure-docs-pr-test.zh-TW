---
title: "在雲端服務中設定自訂網域名稱 | Microsoft Docs"
description: "了解如何設定 DNS 設定在自訂網域上公開 Azure 應用程式或資料。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 9f872fd5119042945356225a80331da18f3a6d99
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="1b498-103">設定 Azure 雲端服務的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="1b498-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b498-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1b498-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="1b498-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="1b498-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="1b498-106">當您建立雲端服務時，Azure 會將它指派給 cloudapp.net 的子網域。</span><span class="sxs-lookup"><span data-stu-id="1b498-106">When you create a Cloud Service, Azure assigns it to a subdomain of cloudapp.net.</span></span> <span data-ttu-id="1b498-107">例如，如果您的雲端服務的名稱為 "contoso"，您的使用者可以透過類似 http://contoso.cloudapp.net 的 URL 存取您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b498-107">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="1b498-108">Azure 也會指派虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="1b498-109">不過，您也可以在自己的網域名稱 (例如 contoso.com) 上公開您的應用程式。本文說明如何保留或設定雲端服務 Web 角色的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1b498-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="1b498-110">您已經了解什麼是 CNAME 和 A 記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="1b498-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="1b498-111">[跳過說明](#add-a-cname-record-for-your-custom-domain)。</span><span class="sxs-lookup"><span data-stu-id="1b498-111">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="1b498-112">加快腳步！</span><span class="sxs-lookup"><span data-stu-id="1b498-112">Get going faster!</span></span> <span data-ttu-id="1b498-113">使用 Azure [引導式逐步解說](http://support.microsoft.com/kb/2990804)。</span><span class="sxs-lookup"><span data-stu-id="1b498-113">Use the Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="1b498-114">在彈指之間完成自訂網域名稱的關聯，以及與 Azure 雲端服務或 Azure 網站之間的通訊 (SSL) 保護。</span><span class="sxs-lookup"><span data-stu-id="1b498-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="1b498-115">此工作的程序適用於 Azure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="1b498-115">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="1b498-116">如需應用程式服務的資訊，請參閱 [這裡](../app-service-web/web-sites-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="1b498-117">如需儲存體帳戶的資訊，請參閱 [這裡](../storage/blobs/storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="1b498-118">了解 CNAME 和 A 記錄</span><span class="sxs-lookup"><span data-stu-id="1b498-118">Understand CNAME and A records</span></span>
<span data-ttu-id="1b498-119">CNAME (或別名記錄) 和 A 記錄都可讓您將網域名稱和特定的伺服器 (在此案例中為服務) 產生關聯，但運作方式不同。</span><span class="sxs-lookup"><span data-stu-id="1b498-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="1b498-120">針對 Azure 雲端服務來使用 A 記錄時，在決定使用何者之前，還有一些事項應該考慮。</span><span class="sxs-lookup"><span data-stu-id="1b498-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="1b498-121">CNAME 或別名記錄</span><span class="sxs-lookup"><span data-stu-id="1b498-121">CNAME or Alias record</span></span>
<span data-ttu-id="1b498-122">CNAME 記錄將 *特定的* 網域 (例如 **contoso.com** or **www.contoso.com**) 對應到正式網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1b498-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="1b498-123">在此案例中，Canonical 網域名稱為 Azure 主控應用程式的 **[myapp].cloudapp.net** 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1b498-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="1b498-124">CNAME 建立之後還會建立 **[myapp].cloudapp.net**的別名。</span><span class="sxs-lookup"><span data-stu-id="1b498-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="1b498-125">CNAME 項目會自動解析成 **[myapp].cloudapp.net** 服務的 IP 位址，就算雲端服務的 IP 位址變更，您也不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="1b498-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="1b498-126">使用 CNAME 記錄時，某些網域註冊機構只允許您對應子網域 (如 www.contoso.com)，而不是根名稱 (如 contoso.com)。如需 CNAME 記錄的詳細資訊，請參閱註冊機構提供的文件、[維基百科 CNAME 記錄條目](http://en.wikipedia.org/wiki/CNAME_record)，或 [IETF 網域名稱 - 實作與規格](http://tools.ietf.org/html/rfc1035)文件。</span><span class="sxs-lookup"><span data-stu-id="1b498-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="1b498-127">A 記錄</span><span class="sxs-lookup"><span data-stu-id="1b498-127">A record</span></span>
<span data-ttu-id="1b498-128">A 記錄將網域 (例如 **contoso.com** 或 **www.contoso.com**) *或萬用字元網域* (例如 **\*.contoso.com**) 對應至 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="1b498-129">以 Azure 雲端服務而言，就是指服務的虛擬 IP。</span><span class="sxs-lookup"><span data-stu-id="1b498-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="1b498-130">相較於 CNAME 記錄，A 記錄的主要優點在於只需要有一個項目使用萬用字元，例如 \***.contoso.com**，即可處理多個子網域的要求，例如 **mail.contoso.com**、**login.contoso.com** 或 **www.contso.com**。</span><span class="sxs-lookup"><span data-stu-id="1b498-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="1b498-131">因為 A 記錄會對應至靜態 IP 位址，所以無法自動解析雲端服務 IP 位址的變更。</span><span class="sxs-lookup"><span data-stu-id="1b498-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="1b498-132">第一次將雲端服務部署到空的位置時 (生產或預備)，將會配置雲端服務所使用的 IP 位址。如果刪除此位置的部署，則 Azure 會釋放此 IP 位址，而未來再部署到此位置時，可能會給予新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="1b498-133">在預備和生產部署之間切換時，或就地升級現有的部署時，指定部署位置 (生產或預備) 的 IP 位址會保留下來，相當方便。</span><span class="sxs-lookup"><span data-stu-id="1b498-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="1b498-134">如需關於執行這些動作的詳細資訊，請參閱 [如何管理雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="1b498-135">新增自訂網域的 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="1b498-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="1b498-136">若要建立 CNAME 記錄，您必須使用註冊機構提供的工具，在 DNS 表格中為自訂網域新增項目。</span><span class="sxs-lookup"><span data-stu-id="1b498-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="1b498-137">各註冊機構指定 CNAME 記錄的方法都很類似，只是稍微不同，但概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="1b498-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="1b498-138">使用其中一種方法來尋找指派給雲端服務的 **.cloudapp.net** 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="1b498-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="1b498-139">登入 [Azure 傳統入口網站]，選取您的雲端服務，再選取 [儀表板]，然後在 [快速概覽] 區段中找出 [網站 URL] 項目。</span><span class="sxs-lookup"><span data-stu-id="1b498-139">Login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
     
       ![快速瀏覽區段，其中顯示網站 URL][csurl]
     
       <span data-ttu-id="1b498-141">**或**</span><span class="sxs-lookup"><span data-stu-id="1b498-141">**OR**</span></span>  
   * <span data-ttu-id="1b498-142">安裝並設定 [Azure Powershell](/powershell/azure/overview)，然後使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1b498-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="1b498-143">請將任一方法傳回的 URL 中所使用的網域名稱儲存下來，建立 CNAME 記錄時需要用到。</span><span class="sxs-lookup"><span data-stu-id="1b498-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="1b498-144">登入 DNS 註冊機構的網站，並移至 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="1b498-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="1b498-145">在網站中尋找標示為 **Domain Name**、**DNS** 或 **Name Server Management** 的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="1b498-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="1b498-146">現在找出可選取或輸入 CNAME 的地方。</span><span class="sxs-lookup"><span data-stu-id="1b498-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="1b498-147">您可能需要從下拉式清單中或移至進階設定頁面，才能選取記錄類型。</span><span class="sxs-lookup"><span data-stu-id="1b498-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="1b498-148">請尋找 **CNAME**、**Alias** 或 **Subdomains** 之類的字。</span><span class="sxs-lookup"><span data-stu-id="1b498-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="1b498-149">如果要建立 **www.customdomain.com** 的別名，您也必須為 CNAME 提供網域或子網域別名，例如 **www**。如果要建立根網域的別名，註冊機構的 DNS 工具中可能會以 '**@**' 符號列出此別名。</span><span class="sxs-lookup"><span data-stu-id="1b498-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="1b498-150">接著，您必須提供正式主機名稱，在此案例中為應用程式的 **cloudapp.net** 網域。</span><span class="sxs-lookup"><span data-stu-id="1b498-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="1b498-151">例如，下列 CNAME 記錄會將來自 **www.contoso.com** 的所有流量，轉送至 **contoso.cloudapp.net** (已部署之應用程式的自訂網域名稱)：</span><span class="sxs-lookup"><span data-stu-id="1b498-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="1b498-152">別名/主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="1b498-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="1b498-153">正式網域</span><span class="sxs-lookup"><span data-stu-id="1b498-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="1b498-154">www</span><span class="sxs-lookup"><span data-stu-id="1b498-154">www</span></span> |<span data-ttu-id="1b498-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="1b498-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="1b498-156">**www.contoso.com** 的訪客絕對看不到真正的主機 (contoso.cloudapp.net)，所以使用者不會察覺到轉送過程。</span><span class="sxs-lookup"><span data-stu-id="1b498-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="1b498-157">上述範例僅適用於 **www** 子網域的流量。</span><span class="sxs-lookup"><span data-stu-id="1b498-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="1b498-158">因為 CNAME 記錄不能使用萬用字元，所以您必須為每一個網域/子網域建立一個 CNAME。</span><span class="sxs-lookup"><span data-stu-id="1b498-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="1b498-159">如果要將來自子網域 (例如 \*.contoso.com) 的流量導向您的 cloudapp.net 位址，您可以在 DNS 設定中設定 [URL 重新導向] 或 [URL 轉送] 項目，或建立一筆 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="1b498-159">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="1b498-160">新增自訂網域的 A 記錄</span><span class="sxs-lookup"><span data-stu-id="1b498-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="1b498-161">若要建立 A 記錄，您必須先找出雲端服務的虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="1b498-162">然後，利用註冊機構提供的工具，在 DNS 表格中為自訂網域新增項目。</span><span class="sxs-lookup"><span data-stu-id="1b498-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="1b498-163">各註冊機構指定 A 記錄的方法都很類似，只是稍微不同，但概念都一樣。</span><span class="sxs-lookup"><span data-stu-id="1b498-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="1b498-164">使用下列其中一種方法取得雲端服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="1b498-165">登入 [Azure 傳統入口網站]，選取您的雲端服務，再選取 [儀表板]，然後在 [快速概覽] 區段中找出 [公用虛擬 IP (VIP) 位址] 項目。</span><span class="sxs-lookup"><span data-stu-id="1b498-165">login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Public Virtual IP (VIP) address** entry in the **quick glance** section.</span></span>
     
       ![快速瀏覽區段，其中顯示 VIP][vip]
     
       <span data-ttu-id="1b498-167">**或**</span><span class="sxs-lookup"><span data-stu-id="1b498-167">**OR**</span></span>  
   * <span data-ttu-id="1b498-168">安裝並設定 [Azure Powershell](/powershell/azure/overview)，然後使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="1b498-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="1b498-169">如果雲端服務有多個相關聯的端點，您會收到許多行 IP 位址，但全部都會顯示相同的位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing the IP address, but all should display the same address.</span></span>
     
     <span data-ttu-id="1b498-170">建立 A 記錄時需要用到此 IP 位址，請儲存下來。</span><span class="sxs-lookup"><span data-stu-id="1b498-170">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="1b498-171">登入 DNS 註冊機構的網站，並移至 DNS 管理頁面。</span><span class="sxs-lookup"><span data-stu-id="1b498-171">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="1b498-172">在網站中尋找標示為 **Domain Name**、**DNS** 或 **Name Server Management** 的連結或區域。</span><span class="sxs-lookup"><span data-stu-id="1b498-172">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="1b498-173">現在找出可選取或輸入 A 記錄的地方。</span><span class="sxs-lookup"><span data-stu-id="1b498-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="1b498-174">您可能需要從下拉式清單中或移至進階設定頁面，才能選取記錄類型。</span><span class="sxs-lookup"><span data-stu-id="1b498-174">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="1b498-175">選取或輸入將使用此 A 記錄的網域或子網域。</span><span class="sxs-lookup"><span data-stu-id="1b498-175">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="1b498-176">例如，若要建立 **www.customdomain.com** 的別名，請選取 **www**。如果要為所有子網域建立萬用字元項目，請輸入 '__*__'。</span><span class="sxs-lookup"><span data-stu-id="1b498-176">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="1b498-177">這將會涵蓋所有子網域，例如 **mail.customdomain.com**、**login.customdomain.com** 和 **www.customdomain.com**。</span><span class="sxs-lookup"><span data-stu-id="1b498-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="1b498-178">如果要建立根網域的 A 記錄，註冊機構的 DNS 工具中可能會以 '**@**' 符號列出此別名。</span><span class="sxs-lookup"><span data-stu-id="1b498-178">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="1b498-179">在提供的欄位中，輸入雲端服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1b498-179">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="1b498-180">這樣會將 A 記錄中使用的網域項目與雲端服務部署的 IP 位址產生關聯。</span><span class="sxs-lookup"><span data-stu-id="1b498-180">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="1b498-181">例如，下列 A 記錄會將來自 **contoso.com** 的所有流量轉送至 **137.135.70.239** (已部署之應用程式的 IP 位址)：</span><span class="sxs-lookup"><span data-stu-id="1b498-181">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="1b498-182">主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="1b498-182">Host name/Subdomain</span></span> | <span data-ttu-id="1b498-183">IP 位址</span><span class="sxs-lookup"><span data-stu-id="1b498-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="1b498-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="1b498-184">137.135.70.239</span></span> |

<span data-ttu-id="1b498-185">此範例示範建立根網域的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="1b498-185">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="1b498-186">如果想要建立萬用字元項目來涵蓋所有子網域，請輸入 '__*__' 做為子網域。</span><span class="sxs-lookup"><span data-stu-id="1b498-186">If you wish to create a wildcard entry to cover all subdomains, you would enter '__*__' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="1b498-187">依預設，Azure 中的 IP 位址是動態的。</span><span class="sxs-lookup"><span data-stu-id="1b498-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="1b498-188">您可能想要使用 [保留的 IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md) ，以確保您的 IP 位址不會變更。</span><span class="sxs-lookup"><span data-stu-id="1b498-188">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1b498-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b498-189">Next steps</span></span>
* [<span data-ttu-id="1b498-190">如何管理雲端服務</span><span class="sxs-lookup"><span data-stu-id="1b498-190">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="1b498-191">如何將 CDN 內容對應至自訂網域</span><span class="sxs-lookup"><span data-stu-id="1b498-191">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="1b498-192">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="1b498-193">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-193">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="1b498-194">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="1b498-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Azure 傳統入口網站]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
