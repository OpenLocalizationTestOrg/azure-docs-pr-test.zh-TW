---
title: "aaaConfigure 雲端服務中的自訂網域名稱 |Microsoft 文件"
description: "深入了解如何 tooexpose 您的 Azure 應用程式或資料上所設定的 DNS 設定自訂網域。"
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
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="90196-103">設定 Azure 雲端服務的自訂網域名稱</span><span class="sxs-lookup"><span data-stu-id="90196-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90196-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="90196-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="90196-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="90196-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="90196-106">當您建立雲端服務時，Azure 將其指派 tooa cloudapp.net 子網域。</span><span class="sxs-lookup"><span data-stu-id="90196-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="90196-107">例如，如果您的雲端服務名稱為"contoso"，您的使用者將會無法 tooaccess http://contoso.cloudapp.net 之類的 URL 上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="90196-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="90196-108">Azure 也會指派虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="90196-109">不過，您也可以在自己的網域名稱 (例如 contoso.com) 上公開您的應用程式。這篇文章說明如何 tooreserve 或設定自訂網域名稱的雲端服務 web 角色。</span><span class="sxs-lookup"><span data-stu-id="90196-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="90196-110">您已經了解什麼是 CNAME 和 A 記錄嗎？</span><span class="sxs-lookup"><span data-stu-id="90196-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="90196-111">[跳過 hello 說明](#add-a-cname-record-for-your-custom-domain)。</span><span class="sxs-lookup"><span data-stu-id="90196-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="90196-112">加快腳步！</span><span class="sxs-lookup"><span data-stu-id="90196-112">Get going faster!</span></span> <span data-ttu-id="90196-113">使用 hello Azure[引導式逐步解說](http://support.microsoft.com/kb/2990804)。</span><span class="sxs-lookup"><span data-stu-id="90196-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="90196-114">在彈指之間完成自訂網域名稱的關聯，以及與 Azure 雲端服務或 Azure 網站之間的通訊 (SSL) 保護。</span><span class="sxs-lookup"><span data-stu-id="90196-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="90196-115">在這項工作的 hello 程序適用於 tooAzure 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="90196-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="90196-116">如需應用程式服務的資訊，請參閱 [這裡](../app-service-web/web-sites-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="90196-117">如需儲存體帳戶的資訊，請參閱 [這裡](../storage/blobs/storage-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="90196-118">了解 CNAME 和 A 記錄</span><span class="sxs-lookup"><span data-stu-id="90196-118">Understand CNAME and A records</span></span>
<span data-ttu-id="90196-119">CNAME （或別名記錄） 和記錄同時 tooassociate 與特定伺服器的網域名稱可讓您 （或在此情況下，服務） 但是以不同的方式運作。</span><span class="sxs-lookup"><span data-stu-id="90196-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="90196-120">與 Azure 雲端服務，您應該先決定哪些 toouse 考慮使用 A 記錄時，也會產生一些特定的考量。</span><span class="sxs-lookup"><span data-stu-id="90196-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="90196-121">CNAME 或別名記錄</span><span class="sxs-lookup"><span data-stu-id="90196-121">CNAME or Alias record</span></span>
<span data-ttu-id="90196-122">CNAME 記錄對應*特定*網域，例如**contoso.com**或**www.contoso.com**，tooa 正式網域名稱。</span><span class="sxs-lookup"><span data-stu-id="90196-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="90196-123">在此情況下，hello 正式網域名稱為 hello **[myapp].cloudapp.net**網域名稱，您的 Azure 託管應用程式。</span><span class="sxs-lookup"><span data-stu-id="90196-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="90196-124">Hello CNAME 建立之後，建立一個別名 hello **[myapp].cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="90196-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="90196-125">hello 的 CNAME 項目將 toohello IP 位址，解析您**[myapp].cloudapp.net**自動服務，因此 hello hello 雲端服務 IP 位址變更時，如果您不需要 tootake 任何動作。</span><span class="sxs-lookup"><span data-stu-id="90196-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="90196-126">一些網域註冊機構只允許您 toomap 子網域時使用的 CNAME 記錄，例如 www.contoso.com，而不根名稱，例如 contoso.com。如需有關 CNAME 記錄的詳細資訊，請參閱您的註冊機構所提供的 hello 文件[hello 維基百科項目上的 CNAME 記錄](http://en.wikipedia.org/wiki/CNAME_record)，或使用 hello [IETF 網域名稱-實作和規格](http://tools.ietf.org/html/rfc1035)文件。</span><span class="sxs-lookup"><span data-stu-id="90196-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="90196-127">A 記錄</span><span class="sxs-lookup"><span data-stu-id="90196-127">A record</span></span>
<span data-ttu-id="90196-128">A 記錄將定義域對應，例如**contoso.com**或**www.contoso.com**，*或萬用字元網域*例如 **\*。 contoso.com**，tooan IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="90196-129">在 Azure 雲端服務的 hello 情況下，hello hello 服務的虛擬 IP。</span><span class="sxs-lookup"><span data-stu-id="90196-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="90196-130">因此 hello 的 A 記錄透過 CNAME 記錄的主要優點是，您可以擁有一個項目使用萬用字元，例如\* **。 contoso.com**，這會處理要求有多個子網域，例如**mail.contoso.com**， **login.contoso.com**，或**www.contso.com**。</span><span class="sxs-lookup"><span data-stu-id="90196-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="90196-131">由於 A 記錄對應 tooa 靜態 IP 位址，無法自動解決您的雲端服務的變更 toohello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="90196-132">使用您的雲端服務的 hello IP 位址被配置 hello 首次部署 tooan 空的插槽 （生產或預備環境。）如果您刪除 hello 插槽的 hello 部署，hello IP address 已釋放由 Azure 和任何未來的部署 toohello 位置提供新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="90196-133">為了方便起見，預備和生產部署或執行就地升級的現有部署之間交換時，會保存 hello IP 位址的指定的部署位置 （生產或預備環境）。</span><span class="sxs-lookup"><span data-stu-id="90196-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="90196-134">如需有關如何執行這些動作的詳細資訊，請參閱[toomanage 雲端服務的方式](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="90196-135">新增自訂網域的 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="90196-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="90196-136">toocreate CNAME 記錄，您必須新增新的項目 hello DNS 資料表中的自訂網域註冊機構所提供的 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="90196-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="90196-137">每個註冊機構有相似但稍微不同的方法指定 CNAME 記錄，但概念的 hello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="90196-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="90196-138">使用其中一個這些方法 toofind hello **。.cloudapp.net**指派 tooyour 雲端服務的網域名稱。</span><span class="sxs-lookup"><span data-stu-id="90196-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="90196-139">登入 toohello [Azure 傳統入口網站]，選取您的雲端服務，選取**儀表板**，然後尋找 hello**網站 URL** hello 中的項目**快速概覽** > 一節。</span><span class="sxs-lookup"><span data-stu-id="90196-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![快速概覽區段，顯示 hello 網站 URL][csurl]
     
       <span data-ttu-id="90196-141">**或**</span><span class="sxs-lookup"><span data-stu-id="90196-141">**OR**</span></span>  
   * <span data-ttu-id="90196-142">安裝和設定[Azure Powershell](/powershell/azure/overview)，，然後使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="90196-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="90196-143">儲存會建立一筆 CNAME 記錄時需要使用任一種方法，所傳回的 hello URL 中的 hello 網域名稱。</span><span class="sxs-lookup"><span data-stu-id="90196-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="90196-144">登入 tooyour DNS 註冊機構的網站，並移至 toohello 管理 DNS 的頁面。</span><span class="sxs-lookup"><span data-stu-id="90196-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="90196-145">查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。</span><span class="sxs-lookup"><span data-stu-id="90196-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="90196-146">現在找出可選取或輸入 CNAME 的地方。</span><span class="sxs-lookup"><span data-stu-id="90196-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="90196-147">您可能必須從下拉式清單，輸入或瀏覽 tooan 進階設定 頁面上，tooselect hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="90196-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="90196-148">您應該尋找 hello 文字**CNAME**，**別名**，或**子網域**。</span><span class="sxs-lookup"><span data-stu-id="90196-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="90196-149">您也必須提供 hello 網域或子網域別名 hello CNAME，例如**www**如果您想 toocreate 別名**www.customdomain.com**。如果您想 toocreate 別名 hello 根網域時，它可能被列為 hello '**@**' 註冊機構的 DNS 工具中的符號。</span><span class="sxs-lookup"><span data-stu-id="90196-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="90196-150">接著，您必須提供正式主機名稱，在此案例中為應用程式的 **cloudapp.net** 網域。</span><span class="sxs-lookup"><span data-stu-id="90196-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="90196-151">比方說，hello 下列 CNAME 記錄會轉送所有流量**www.contoso.com**太**contoso.cloudapp.net**，應用程式已部署的 hello 自訂網域名稱：</span><span class="sxs-lookup"><span data-stu-id="90196-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="90196-152">別名/主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="90196-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="90196-153">正式網域</span><span class="sxs-lookup"><span data-stu-id="90196-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="90196-154">www</span><span class="sxs-lookup"><span data-stu-id="90196-154">www</span></span> |<span data-ttu-id="90196-155">contoso.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="90196-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="90196-156">在訪客的**www.contoso.com** hello 轉送程序是不可見的 toothe 終端使用者，則不會看到 hello，則為 true 的主機 (contoso.cloudapp.net)。</span><span class="sxs-lookup"><span data-stu-id="90196-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="90196-157">hello 上述範例只適用於在 hello tootraffic **www**子網域。</span><span class="sxs-lookup"><span data-stu-id="90196-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="90196-158">因為 CNAME 記錄不能使用萬用字元，所以您必須為每一個網域/子網域建立一個 CNAME。</span><span class="sxs-lookup"><span data-stu-id="90196-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="90196-159">如果想 toodirect 流量從子網域，例如\*。 contoso.com、 tooyour.cloudapp.net 位址，您可以設定**URL 重新導向**或**向前 URL** DNS 設定中的項目或建立 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="90196-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="90196-160">新增自訂網域的 A 記錄</span><span class="sxs-lookup"><span data-stu-id="90196-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="90196-161">toocreate A 記錄，您必須先找到您的雲端服務的 hello 虛擬 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="90196-162">使用您的註冊機構所提供的 hello 工具，然後您的自訂網域的 hello DNS 資料表中加入新項目。</span><span class="sxs-lookup"><span data-stu-id="90196-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="90196-163">每個註冊機構具有相似但稍微不同的方法，指定 A 記錄，但概念的 hello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="90196-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="90196-164">使用下列方法 tooget hello 的雲端服務的 IP 位址的 hello 之一。</span><span class="sxs-lookup"><span data-stu-id="90196-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="90196-165">登入 toohello [Azure 傳統入口網站]，選取您的雲端服務，選取**儀表板**，然後尋找 hello**公用虛擬 IP (VIP) 位址**hello中的項目**快速概覽**> 一節。</span><span class="sxs-lookup"><span data-stu-id="90196-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![快速概覽區段，顯示 hello VIP][vip]
     
       <span data-ttu-id="90196-167">**或**</span><span class="sxs-lookup"><span data-stu-id="90196-167">**OR**</span></span>  
   * <span data-ttu-id="90196-168">安裝和設定[Azure Powershell](/powershell/azure/overview)，，然後使用 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="90196-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="90196-169">如果您有多個與您的雲端服務相關聯的端點，您會收到多行包含 hello IP 位址，但所有應該會顯示 hello 相同位址。</span><span class="sxs-lookup"><span data-stu-id="90196-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="90196-170">儲存 hello IP 位址，您將需要建立 A 記錄時。</span><span class="sxs-lookup"><span data-stu-id="90196-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="90196-171">登入 tooyour DNS 註冊機構的網站，並移至 toohello 管理 DNS 的頁面。</span><span class="sxs-lookup"><span data-stu-id="90196-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="90196-172">查詢的連結或 hello 網站的區域標示為**網域名稱**， **DNS**，或**名稱伺服器管理**。</span><span class="sxs-lookup"><span data-stu-id="90196-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="90196-173">現在找出可選取或輸入 A 記錄的地方。</span><span class="sxs-lookup"><span data-stu-id="90196-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="90196-174">您可能必須從下拉式清單，輸入或瀏覽 tooan 進階設定 頁面上，tooselect hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="90196-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="90196-175">選取或輸入 hello 網域或將使用此 A 記錄的子網域。</span><span class="sxs-lookup"><span data-stu-id="90196-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="90196-176">例如，選取**www**如果您想 toocreate 別名**www.customdomain.com**。如果您想要所有子網域 toocreate 萬用字元項目，請輸入 '__*__'。</span><span class="sxs-lookup"><span data-stu-id="90196-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="90196-177">這將會涵蓋所有子網域，例如 **mail.customdomain.com**、**login.customdomain.com** 和 **www.customdomain.com**。</span><span class="sxs-lookup"><span data-stu-id="90196-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="90196-178">如果您想 toocreate A 記錄 hello 根網域時，它可能被列為 hello '**@**' 註冊機構的 DNS 工具中的符號。</span><span class="sxs-lookup"><span data-stu-id="90196-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="90196-179">Hello 提供欄位中輸入您的雲端服務的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="90196-180">這樣會將關聯 hello 網域項目用於 hello 與您的雲端服務部署的 hello IP 位址的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="90196-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="90196-181">比方說，hello 下列記錄會轉送所有流量**contoso.com**太**137.135.70.239**，hello 已部署應用程式的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="90196-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="90196-182">主機名稱/子網域</span><span class="sxs-lookup"><span data-stu-id="90196-182">Host name/Subdomain</span></span> | <span data-ttu-id="90196-183">IP 位址</span><span class="sxs-lookup"><span data-stu-id="90196-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="90196-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="90196-184">137.135.70.239</span></span> |

<span data-ttu-id="90196-185">這個範例將示範如何建立 hello 根網域的 A 記錄。</span><span class="sxs-lookup"><span data-stu-id="90196-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="90196-186">如果您想 toocreate 萬用字元項目 toocover 所有子網域，您會輸入 '__*__' 為 hello 子網域。</span><span class="sxs-lookup"><span data-stu-id="90196-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="90196-187">依預設，Azure 中的 IP 位址是動態的。</span><span class="sxs-lookup"><span data-stu-id="90196-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="90196-188">您可能會想 toouse[保留的 IP 位址](../virtual-network/virtual-networks-reserved-public-ip.md)tooensure 不會變更您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="90196-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="90196-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90196-189">Next steps</span></span>
* [<span data-ttu-id="90196-190">如何 tooManage 雲端服務</span><span class="sxs-lookup"><span data-stu-id="90196-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="90196-191">如何 tooMap CDN 內容 tooa 自訂網域</span><span class="sxs-lookup"><span data-stu-id="90196-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="90196-192">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="90196-193">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="90196-194">設定 [SSL 憑證](cloud-services-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="90196-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[Azure 傳統入口網站]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
