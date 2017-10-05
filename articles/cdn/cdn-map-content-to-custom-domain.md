---
title: "將 Azure CDN 內容對應至自訂網域 | Microsoft Docs"
description: "了解如何將 Azure CDN 內容對應至自訂網域。"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: cd6db44f7776859d1e6a893543cf0666182ca41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="map-azure-cdn-content-to-a-custom-domain"></a><span data-ttu-id="d10b7-103">將 Azure CDN 內容對應至自訂網域</span><span class="sxs-lookup"><span data-stu-id="d10b7-103">Map Azure CDN content to a custom domain</span></span>
<span data-ttu-id="d10b7-104">您可以將自訂網域對應至 CDN 端點，以在所快取內容的 URL 中使用您自己的網域名稱，而不是使用 azureedge.net 的子網域。</span><span class="sxs-lookup"><span data-stu-id="d10b7-104">You can map a custom domain to a CDN endpoint in order to use your own domain name in URLs to cached content rather than using a subdomain of azureedge.net.</span></span>

<span data-ttu-id="d10b7-105">有兩種方式可將您的自訂網域對應至 CDN 端點：</span><span class="sxs-lookup"><span data-stu-id="d10b7-105">There are two ways to map your custom domain to a CDN endpoint:</span></span>

1. <span data-ttu-id="d10b7-106">[向網域註冊機構建立 CNAME 記錄，並將您的自訂網域和子網域對應至 CDN 端點](#register-a-custom-domain-for-an-azure-cdn-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-106">[Create a CNAME record with your domain registrar and map your custom domain and subdomain to the CDN endpoint](#register-a-custom-domain-for-an-azure-cdn-endpoint).</span></span>
   
    <span data-ttu-id="d10b7-107">CNAME 記錄是將 `www.contosocdn.com` 或 `cdn.contoso.com` 等來源網域對應至目的地網域的 DNS 功能。</span><span class="sxs-lookup"><span data-stu-id="d10b7-107">A CNAME record is a DNS feature that maps a source domain, like `www.contosocdn.com` or `cdn.contoso.com`, to a destination domain.</span></span> <span data-ttu-id="d10b7-108">在這種情況下，來源網域是您的自訂網域和子網域 (像是 **www** 或 **cdn** 的子網域一律是必要項目)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-108">In this case, the source domain is your custom domain and subdomain (a subdomain, like **www** or **cdn** is always required).</span></span> <span data-ttu-id="d10b7-109">目的地網域是 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-109">The destination domain is your CDN endpoint.</span></span>  
   
    <span data-ttu-id="d10b7-110">然而，在將自訂網域對應至 CDN 端點的過程中，會由於您在 Azure 入口網站中註冊網域而導致網域短暫停擺。</span><span class="sxs-lookup"><span data-stu-id="d10b7-110">The process of mapping your custom domain to your CDN endpoint can, however, result in a brief period of downtime for the domain while you are registering the domain in the Azure  Portal.</span></span>
2. [<span data-ttu-id="d10b7-111">使用 **cdnverify** 加入中繼註冊步驟</span><span class="sxs-lookup"><span data-stu-id="d10b7-111">Add an intermediate registration step with **cdnverify**</span></span>](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    <span data-ttu-id="d10b7-112">如果自訂網域目前支援不得發生停機的服務等級協定 (SLA) 的應用程式，您可以使用 Azure **cdnverify** 子網域提供中繼註冊步驟，使用者就能在 DNS 對應發生時存取網域。</span><span class="sxs-lookup"><span data-stu-id="d10b7-112">If your custom domain is currently supporting an application with a service-level agreement (SLA) that requires that there be no downtime, then you can use the Azure **cdnverify** subdomain to provide an intermediate registration step so that users will be able to access your domain while the DNS mapping takes place.</span></span>  

<span data-ttu-id="d10b7-113">您使用上述其中一個程序註冊自訂網域之後，您會想要 [確認自訂子網域參照您的 CDN 端點](#verify-that-the-custom-subdomain-references-your-cdn-endpoint)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-113">After you register your custom domain using one of the above procedures, you will want to [verify that the custom subdomain references your CDN endpoint](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).</span></span>

> [!NOTE]
> <span data-ttu-id="d10b7-114">您必須向網域註冊機構建立 CNAME 記錄，以將網域對應至 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-114">You must create a CNAME record with your domain registrar to map your domain to the CDN endpoint.</span></span> <span data-ttu-id="d10b7-115">CNAME 記錄會對應至特定子網域 (例如 `www.contoso.com` 或 `cdn.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-115">CNAME records map specific subdomains such as `www.contoso.com` or `cdn.contoso.com`.</span></span> <span data-ttu-id="d10b7-116">CNAME 記錄無法對應至根網域 (例如 `contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-116">It is not possible to map a CNAME record to a root domain, such as `contoso.com`.</span></span>
> 
> <span data-ttu-id="d10b7-117">一個子網域只能與一個 CDN 端點產生關聯。</span><span class="sxs-lookup"><span data-stu-id="d10b7-117">A subdomain can only be associated with one CDN endpoint.</span></span> <span data-ttu-id="d10b7-118">您所建立的 CNAME 記錄會將所有定址至子網域的流量路由傳送至指定的端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-118">The CNAME record that you create will route all traffic addressed to the subdomain to the specified endpoint.</span></span>  <span data-ttu-id="d10b7-119">例如，如果您將 `www.contoso.com` 與您的 CDN 端點產生關聯，則無法將它與其他 Azure 端點產生關聯 (例如，儲存體帳戶端點或雲端服務端點)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-119">For example, if you associate `www.contoso.com` with your CDN endpoint, then you cannot associate it with other Azure endpoints, such as a storage account endpoint or a cloud service endpoint.</span></span> <span data-ttu-id="d10b7-120">不過，針對不同的服務端點，您可以使用來自相同網域的不同子網域。</span><span class="sxs-lookup"><span data-stu-id="d10b7-120">However, you can use different subdomains from the same domain for different service endpoints.</span></span> <span data-ttu-id="d10b7-121">您也可以將不同的子網域對應至相同的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-121">You can also map different subdomains to the same CDN endpoint.</span></span>
> 
> <span data-ttu-id="d10b7-122">若為**來自 Verizon 的 Azure CDN** (標準與進階) 端點，請注意，最多需要 **90 分鐘**的時間，才能將自訂網域變更傳播至 CDN 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-122">For **Azure CDN from Verizon** (Standard and Premium) endpoints, note that it takes up to **90 minutes** for custom domain changes to propagate to CDN edge nodes.</span></span>
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a><span data-ttu-id="d10b7-123">註冊 Azure CDN 端點的自訂網域</span><span class="sxs-lookup"><span data-stu-id="d10b7-123">Register a custom domain for an Azure CDN endpoint</span></span>
1. <span data-ttu-id="d10b7-124">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d10b7-125">依序按一下 [瀏覽] 和 [CDN 設定檔]，接著按一下包含要對應到自訂網域之端點的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="d10b7-125">Click **Browse**, then **CDN Profiles**, then the CDN profile with the endpoint you want to map to a custom domain.</span></span>  
3. <span data-ttu-id="d10b7-126">在 [CDN 設定檔]  刀鋒視窗中，按一下要與子網域產生關聯的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-126">In the **CDN Profile** blade, click the CDN endpoint with which you want to associate the subdomain.</span></span>
4. <span data-ttu-id="d10b7-127">在 [端點] 刀鋒視窗頂端，按一下 [新增自訂網域] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d10b7-127">At the top of the endpoint blade, click the **Add Custom Domain** button.</span></span>  <span data-ttu-id="d10b7-128">在 [新增自訂網域] 刀鋒視窗中，您會看到衍生自 CDN 端點的端點主機名稱，其可用來建立新的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-128">In the **Add a custom domain** blade, you'll see the endpoint host name, derived from your CDN endpoint, to use in creating a new CNAME record.</span></span> <span data-ttu-id="d10b7-129">主機名稱位址的格式會顯示為 **&lt;EndpointName>.azureedge.net**。</span><span class="sxs-lookup"><span data-stu-id="d10b7-129">The format of the host name address will appear as **&lt;EndpointName>.azureedge.net**.</span></span>  <span data-ttu-id="d10b7-130">您可以複製這個主機名稱，以用於建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-130">You can copy this host name to use in creating the CNAME record.</span></span>  
5. <span data-ttu-id="d10b7-131">瀏覽至您網域註冊機構的網站，並找出用於建立 DNS 記錄的區段。</span><span class="sxs-lookup"><span data-stu-id="d10b7-131">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="d10b7-132">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="d10b7-132">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
6. <span data-ttu-id="d10b7-133">尋找管理 CNAME 的區段。</span><span class="sxs-lookup"><span data-stu-id="d10b7-133">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="d10b7-134">您可能需要移至進階設定頁面，並尋找 CNAME、Alias 或 Subdomains 單字。</span><span class="sxs-lookup"><span data-stu-id="d10b7-134">You may have to go to an advanced settings page and look for the words CNAME, Alias, or Subdomains.</span></span>
7. <span data-ttu-id="d10b7-135">建立新的 CNAME 記錄，將您選擇的子網域 (例如 **www** 或 **cdn**) 對應到 [新增自訂網域] 刀鋒視窗中提供的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="d10b7-135">Create a new CNAME record that maps your chosen subdomain (for example, **www** or **cdn**) to the host name provided in the **Add a custom domain** blade.</span></span> 
8. <span data-ttu-id="d10b7-136">返回 [新增自訂網域]  刀鋒視窗，在對話方塊中輸入您的自訂網域 (包括子網域)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-136">Return to the **Add a custom domain** blade, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="d10b7-137">例如，以 `cdn.contoso.com` 或 `www.contoso.com` 格式輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d10b7-137">For example, enter the domain name in the format `www.contoso.com` or `cdn.contoso.com`.</span></span>   
   
   <span data-ttu-id="d10b7-138">Azure 會確認您所輸入的網域名稱存在 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-138">Azure will verify that the CNAME record exists for the domain name you have entered.</span></span> <span data-ttu-id="d10b7-139">如果 CNAME 正確，您的自訂網域就會驗證。</span><span class="sxs-lookup"><span data-stu-id="d10b7-139">If the CNAME is correct, your custom domain is validated.</span></span>  <span data-ttu-id="d10b7-140">然而，若為 **來自 Verizon 的 Azure CDN** (標準與進階) 端點，最多可能需要 90 分鐘的時間，自訂網域設定才能傳播至 CDN 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-140">For **Azure CDN from Verizon** (Standard and Premium) endpoints, it may take up to 90 minutes for custom domain settings to propagate to all CDN edge nodes, however.</span></span>  
   
   <span data-ttu-id="d10b7-141">請注意，在某些情況下，可能需要時間讓 CNAME 記錄傳播到網際網路上的名稱伺服器。</span><span class="sxs-lookup"><span data-stu-id="d10b7-141">Note that in some cases it can take time for the CNAME record to propagate to name servers on the Internet.</span></span> <span data-ttu-id="d10b7-142">如果未立即驗證您的網域，但您確信 CNAME 記錄正確，則請等待數分鐘的時間，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="d10b7-142">If your domain is not validated immediately, and you believe the CNAME record is correct, then wait a few minutes and try again.</span></span>

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain"></a><span data-ttu-id="d10b7-143">註冊使用中繼 cdnverify 子網域的 Azure CDN 端點的自訂網域</span><span class="sxs-lookup"><span data-stu-id="d10b7-143">Register a custom domain for an Azure CDN endpoint using the intermediary cdnverify subdomain</span></span>
1. <span data-ttu-id="d10b7-144">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-144">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d10b7-145">依序按一下 [瀏覽] 和 [CDN 設定檔]，接著按一下包含要對應到自訂網域之端點的 CDN 設定檔。</span><span class="sxs-lookup"><span data-stu-id="d10b7-145">Click **Browse**, then **CDN Profiles**, then the CDN profile with the endpoint you want to map to a custom domain.</span></span>  
3. <span data-ttu-id="d10b7-146">在 [CDN 設定檔]  刀鋒視窗中，按一下要與子網域產生關聯的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-146">In the **CDN Profile** blade, click the CDN endpoint with which you want to associate the subdomain.</span></span>
4. <span data-ttu-id="d10b7-147">在 [端點] 刀鋒視窗頂端，按一下 [新增自訂網域] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d10b7-147">At the top of the endpoint blade, click the **Add Custom Domain** button.</span></span>  <span data-ttu-id="d10b7-148">在 [新增自訂網域] 刀鋒視窗中，您會看到衍生自 CDN 端點的端點主機名稱，其可用來建立新的 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-148">In the **Add a custom domain** blade, you'll see the endpoint host name, derived from your CDN endpoint, to use in creating a new CNAME record.</span></span> <span data-ttu-id="d10b7-149">主機名稱位址的格式會顯示為 **&lt;EndpointName>.azureedge.net**。</span><span class="sxs-lookup"><span data-stu-id="d10b7-149">The format of the host name address will appear as **&lt;EndpointName>.azureedge.net**.</span></span>  <span data-ttu-id="d10b7-150">您可以複製這個主機名稱，以用於建立 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-150">You can copy this host name to use in creating the CNAME record.</span></span>
5. <span data-ttu-id="d10b7-151">瀏覽至您網域註冊機構的網站，並找出用於建立 DNS 記錄的區段。</span><span class="sxs-lookup"><span data-stu-id="d10b7-151">Navigate to your domain registrar's web site, and locate the section for creating DNS records.</span></span> <span data-ttu-id="d10b7-152">您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。</span><span class="sxs-lookup"><span data-stu-id="d10b7-152">You might find this in a section such as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
6. <span data-ttu-id="d10b7-153">尋找管理 CNAME 的區段。</span><span class="sxs-lookup"><span data-stu-id="d10b7-153">Find the section for managing CNAMEs.</span></span> <span data-ttu-id="d10b7-154">您可能需要移至進階設定頁面，並尋找 **CNAME**、**Alias** 或 **Subdomains** 單字。</span><span class="sxs-lookup"><span data-stu-id="d10b7-154">You may have to go to an advanced settings page and look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
7. <span data-ttu-id="d10b7-155">建立新的 CNAME 記錄，並提供包含 **cdnverify** 子網域的子網域別名。</span><span class="sxs-lookup"><span data-stu-id="d10b7-155">Create a new CNAME record, and provide a subdomain alias that includes the **cdnverify** subdomain.</span></span> <span data-ttu-id="d10b7-156">例如，您指定的子網域格式會是 **cdnverify.www** 或 **cdnverify.cdn**。</span><span class="sxs-lookup"><span data-stu-id="d10b7-156">For example, the subdomain that you specify will be in the format **cdnverify.www** or **cdnverify.cdn**.</span></span> <span data-ttu-id="d10b7-157">接著以格式 **cdnverify.&lt;EndpointName>.azureedge.net** 提供主機名稱，也就是您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-157">Then provide the host name, which is your CDN endpoint, in the format **cdnverify.&lt;EndpointName>.azureedge.net**.</span></span> <span data-ttu-id="d10b7-158">您的 DNS 對應看起來應該類似：`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`</span><span class="sxs-lookup"><span data-stu-id="d10b7-158">Your DNS mapping should look like: `cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`</span></span>  
8. <span data-ttu-id="d10b7-159">返回 [新增自訂網域]  刀鋒視窗，在對話方塊中輸入您的自訂網域 (包括子網域)。</span><span class="sxs-lookup"><span data-stu-id="d10b7-159">Return to the **Add a custom domain** blade, and enter your custom domain, including the subdomain, in the dialog box.</span></span> <span data-ttu-id="d10b7-160">例如，以 `cdn.contoso.com` 或 `www.contoso.com` 格式輸入網域名稱。</span><span class="sxs-lookup"><span data-stu-id="d10b7-160">For example, enter the domain name in the format `www.contoso.com` or `cdn.contoso.com`.</span></span> <span data-ttu-id="d10b7-161">請注意，在此步驟中，您不需要在子網域的前方加上 **cdnverify**。</span><span class="sxs-lookup"><span data-stu-id="d10b7-161">Note that in this step, you do not need to preface the subdomain with **cdnverify**.</span></span>  
   
    <span data-ttu-id="d10b7-162">Azure 會確認您所輸入的 cdnverify 網域名稱存在 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-162">Azure will verify that the CNAME record exists for the cdnverify domain name you have entered.</span></span>
9. <span data-ttu-id="d10b7-163">此時，自訂網域已通過 Azure 的驗證，不過前往網域的流量尚未路由傳送至 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-163">At this point, your custom domain has been verified by Azure, but traffic to your domain is not yet being routed to your CDN endpoint.</span></span> <span data-ttu-id="d10b7-164">當等候的時間足以讓自訂網域設定傳播至 CDN 邊緣節點 (90 分鐘用於**來自 Verizon 的 Azure CDN**，1-2 分鐘用於**來自 Akamai 的 Azure CDN**) 之後，返回 DNS 註冊機構的網站，並建立另一個 CNAME 記錄，將子網域對應至您的 CDN 端點。</span><span class="sxs-lookup"><span data-stu-id="d10b7-164">After waiting long enough to allow the custom domain settings to propagate to the CDN edge nodes (90 minutes for **Azure CDN from Verizon**, 1-2 minutes for **Azure CDN from Akamai**), return to your DNS registrar's web site and create another CNAME record that maps your subdomain to your CDN endpoint.</span></span> <span data-ttu-id="d10b7-165">例如，將子網域指定為 **www** 或 **cdn**，並將主機名稱指定為 **&lt;EndpointName>.azureedge.net**。</span><span class="sxs-lookup"><span data-stu-id="d10b7-165">For example, specify the subdomain as **www** or **cdn**, and the hostname as **&lt;EndpointName>.azureedge.net**.</span></span> <span data-ttu-id="d10b7-166">待這個步驟完成後，自訂網域的註冊作業也宣告完成。</span><span class="sxs-lookup"><span data-stu-id="d10b7-166">With this step, the registration of your custom domain is complete.</span></span>
10. <span data-ttu-id="d10b7-167">最後，您可以透過 **cdnverify**刪除您建立的 CNAME 記錄，因為只有在中繼步驟才需要此記錄。</span><span class="sxs-lookup"><span data-stu-id="d10b7-167">Finally, you can delete the CNAME record you created using **cdnverify**, as it was necessary only as an intermediary step.</span></span>  

## <a name="verify-that-the-custom-subdomain-references-your-cdn-endpoint"></a><span data-ttu-id="d10b7-168">確認自訂子網域參照您的 CDN 端點</span><span class="sxs-lookup"><span data-stu-id="d10b7-168">Verify that the custom subdomain references your CDN endpoint</span></span>
* <span data-ttu-id="d10b7-169">完成註冊您的自訂網域之後，即可使用自訂網域存取 CDN 端點所快取的內容。</span><span class="sxs-lookup"><span data-stu-id="d10b7-169">After you have completed the registration of your custom domain, you can access content that is cached at your CDN endpoint using the custom domain.</span></span>
  <span data-ttu-id="d10b7-170">請先確定您有端點上所快取的公用內容。</span><span class="sxs-lookup"><span data-stu-id="d10b7-170">First, ensure that you have public content that is cached at the endpoint.</span></span> <span data-ttu-id="d10b7-171">例如，如果您的 CDN 端點與儲存體帳戶相關聯，則 CDN 會快取公用 Blob 容器中的內容。</span><span class="sxs-lookup"><span data-stu-id="d10b7-171">For example, if your CDN endpoint is associated with a storage account, the CDN caches content in public blob containers.</span></span> <span data-ttu-id="d10b7-172">若要測試自訂網域，請確定您的容器設定為允許公用存取，而且它包含至少一個 Blob。</span><span class="sxs-lookup"><span data-stu-id="d10b7-172">To test the custom domain, ensure that your container is set to allow public access and that it contains at least one blob.</span></span>
* <span data-ttu-id="d10b7-173">在瀏覽器中，使用自訂網域瀏覽至 Blob 位址。</span><span class="sxs-lookup"><span data-stu-id="d10b7-173">In your browser, navigate to the address of the blob using the custom domain.</span></span> <span data-ttu-id="d10b7-174">例如，如果您的自訂網域是 `cdn.contoso.com`，快取 Blob 的 URL 會和下列 URL 類似：http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg</span><span class="sxs-lookup"><span data-stu-id="d10b7-174">For example, if your custom domain is `cdn.contoso.com`, the URL to a cached blob will be similar to the following URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg</span></span>

## <a name="see-also"></a><span data-ttu-id="d10b7-175">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d10b7-175">See Also</span></span>
[<span data-ttu-id="d10b7-176">如何啟用 Azure 內容傳遞網路 (CDN)</span><span class="sxs-lookup"><span data-stu-id="d10b7-176">How to Enable the Content Delivery Network (CDN)  for Azure</span></span>](cdn-create-new-endpoint.md)  
