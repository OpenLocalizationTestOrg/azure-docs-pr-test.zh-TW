---
title: "將作用中的 DNS 名稱移轉至 Azure App Service | Microsoft Docs"
description: "了解如何在完全不停機的情況下，將已指派給即時網站的自訂 DNS 網域名稱移轉至 Azure App Service。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="ba42b-103">將作用中的 DNS 名稱移轉至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ba42b-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="ba42b-104">本文示範如何在完全不停機的情況下，將作用中的 DNS 名稱移轉至 [Azure App Service](../app-service/app-service-value-prop-what-is.md)。</span><span class="sxs-lookup"><span data-stu-id="ba42b-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="ba42b-105">當您將即時網站及其 DNS 網域名稱移轉至 App Service 時，該 DNS 名稱已對即時流量提供服務。</span><span class="sxs-lookup"><span data-stu-id="ba42b-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="ba42b-106">您可以先將作用中的 DNS 名稱繫結至 App Service 應用程式，以避免 DNS 解析在移轉期間發生停機。</span><span class="sxs-lookup"><span data-stu-id="ba42b-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="ba42b-107">如果您不擔心 DNS 解析發生停機，請參閱[將現有的自訂 DNS 名稱對應至 Azure Web Apps](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="ba42b-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba42b-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="ba42b-108">Prerequisites</span></span>

<span data-ttu-id="ba42b-109">若要完成本操作說明：</span><span class="sxs-lookup"><span data-stu-id="ba42b-109">To complete this how-to:</span></span>

- <span data-ttu-id="ba42b-110">[確定您的 App Service 應用程式不是位於免費層](app-service-web-tutorial-custom-domain.md#checkpricing)。</span><span class="sxs-lookup"><span data-stu-id="ba42b-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="ba42b-111">事先繫結網域名稱</span><span class="sxs-lookup"><span data-stu-id="ba42b-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="ba42b-112">當您事先繫結自訂網域時，要完成下列兩項之後才能對 DNS 記錄進行任何變更︰</span><span class="sxs-lookup"><span data-stu-id="ba42b-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="ba42b-113">確認網域擁有權</span><span class="sxs-lookup"><span data-stu-id="ba42b-113">Verify domain ownership</span></span>
- <span data-ttu-id="ba42b-114">為您的應用程式啟用網域名稱</span><span class="sxs-lookup"><span data-stu-id="ba42b-114">Enable the domain name for your app</span></span>

<span data-ttu-id="ba42b-115">當您最後將自訂 DNS 名稱從舊網站移轉至 App Service 應用程式時，DNS 解析不會發生停機。</span><span class="sxs-lookup"><span data-stu-id="ba42b-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="ba42b-116">建立網域驗證記錄</span><span class="sxs-lookup"><span data-stu-id="ba42b-116">Create domain verification record</span></span>

<span data-ttu-id="ba42b-117">若要確認網域擁有權，請新增 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba42b-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="ba42b-118">TXT 記錄會從 _awverify.&lt;子網域>_ 對應至 _&lt;應用程式名稱>.azurewebsites.net_。</span><span class="sxs-lookup"><span data-stu-id="ba42b-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="ba42b-119">您需要的 TXT 記錄取決於您要移轉的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba42b-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="ba42b-120">如需範例，請參閱下表 (`@` 通常代表根網域)：</span><span class="sxs-lookup"><span data-stu-id="ba42b-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="ba42b-121">DNS 記錄範例</span><span class="sxs-lookup"><span data-stu-id="ba42b-121">DNS record example</span></span> | <span data-ttu-id="ba42b-122">TXT 主機</span><span class="sxs-lookup"><span data-stu-id="ba42b-122">TXT Host</span></span> | <span data-ttu-id="ba42b-123">TXT 值</span><span class="sxs-lookup"><span data-stu-id="ba42b-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="ba42b-124">@ (根網域)</span><span class="sxs-lookup"><span data-stu-id="ba42b-124">@ (root)</span></span> | <span data-ttu-id="ba42b-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="ba42b-125">_awverify_</span></span> | <span data-ttu-id="ba42b-126">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ba42b-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ba42b-127">www (子網域)</span><span class="sxs-lookup"><span data-stu-id="ba42b-127">www (sub)</span></span> | <span data-ttu-id="ba42b-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="ba42b-128">_awverify.www_</span></span> | <span data-ttu-id="ba42b-129">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ba42b-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ba42b-130">\* (萬用字元)</span><span class="sxs-lookup"><span data-stu-id="ba42b-130">\* (wildcard)</span></span> | <span data-ttu-id="ba42b-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="ba42b-131">_awverify.\*_</span></span> | <span data-ttu-id="ba42b-132">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ba42b-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="ba42b-133">在您的 DNS 記錄頁面中，記下您要移轉之 DNS 名稱的記錄類型。</span><span class="sxs-lookup"><span data-stu-id="ba42b-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="ba42b-134">App Service 支援 CNAME 與 A 記錄之間的對應。</span><span class="sxs-lookup"><span data-stu-id="ba42b-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="ba42b-135">為您的應用程式啟用網域</span><span class="sxs-lookup"><span data-stu-id="ba42b-135">Enable the domain for your app</span></span>

<span data-ttu-id="ba42b-136">在 [Azure 入口網站](https://portal.azure.com)之應用程式頁面的左側導覽中，選取 [自訂網域]。</span><span class="sxs-lookup"><span data-stu-id="ba42b-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="ba42b-138">在 [自訂網域] 頁面中，選取 [新增主機名稱] 旁的 **+** 圖示。</span><span class="sxs-lookup"><span data-stu-id="ba42b-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="ba42b-140">鍵入您新增 TXT 記錄的完整網域名稱，例如 `www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="ba42b-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="ba42b-141">針對萬用字元網域 (例如 \*.contoso.com)，您可以使用符合萬用字元網域的任何 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="ba42b-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="ba42b-142">選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="ba42b-142">Select **Validate**.</span></span>

<span data-ttu-id="ba42b-143">[新增主機名稱] 按鈕會啟用。</span><span class="sxs-lookup"><span data-stu-id="ba42b-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="ba42b-144">確定將 [主機名稱記錄類型] 設定為您要移轉的 DNS 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="ba42b-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="ba42b-145">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="ba42b-145">Select **Add hostname**.</span></span>

![將 DNS 名稱新增至應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="ba42b-147">可能需要一些時間，新的主機名稱才會反映在應用程式的 [自訂網域] 分頁中。</span><span class="sxs-lookup"><span data-stu-id="ba42b-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="ba42b-148">嘗試重新整理瀏覽器以更新資料。</span><span class="sxs-lookup"><span data-stu-id="ba42b-148">Try refreshing the browser to update the data.</span></span>

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="ba42b-150">您的 DNS 名稱現已在您的 Azure 應用程式中啟用。</span><span class="sxs-lookup"><span data-stu-id="ba42b-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="ba42b-151">重新對應作用中的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="ba42b-151">Remap the active DNS name</span></span>

<span data-ttu-id="ba42b-152">唯一剩下的工作是重新對應作用中的 DNS 記錄，以指向 App Service。</span><span class="sxs-lookup"><span data-stu-id="ba42b-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="ba42b-153">目前，它仍指向舊網站。</span><span class="sxs-lookup"><span data-stu-id="ba42b-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="ba42b-154">複製應用程式的 IP 位址 (僅限 A 記錄)</span><span class="sxs-lookup"><span data-stu-id="ba42b-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="ba42b-155">如果您重新對應的是 CNAME 記錄，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="ba42b-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="ba42b-156">若要重新對應 A 記錄，您需要 App Service 應用程式的外部 IP 位址，如 [自訂網域] 頁面中所示。</span><span class="sxs-lookup"><span data-stu-id="ba42b-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="ba42b-157">選取右上角的 **X** 關閉 [新增主機名稱] 頁面。</span><span class="sxs-lookup"><span data-stu-id="ba42b-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="ba42b-158">在 [自訂網域] 頁面中，複製應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ba42b-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![入口網站瀏覽至 Azure 應用程式](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="ba42b-160">更新 DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="ba42b-160">Update the DNS record</span></span>

<span data-ttu-id="ba42b-161">回到您網域提供者的 DNS 記錄頁面，選取要重新對應的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ba42b-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="ba42b-162">在 `contoso.com` 根網域範例中，重新對應 A 或 CNAME 記錄，如下表中的範例所示：</span><span class="sxs-lookup"><span data-stu-id="ba42b-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="ba42b-163">FQDN 範例</span><span class="sxs-lookup"><span data-stu-id="ba42b-163">FQDN example</span></span> | <span data-ttu-id="ba42b-164">記錄類型</span><span class="sxs-lookup"><span data-stu-id="ba42b-164">Record type</span></span> | <span data-ttu-id="ba42b-165">Host</span><span class="sxs-lookup"><span data-stu-id="ba42b-165">Host</span></span> | <span data-ttu-id="ba42b-166">值</span><span class="sxs-lookup"><span data-stu-id="ba42b-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="ba42b-167">contoso.com (根網域)</span><span class="sxs-lookup"><span data-stu-id="ba42b-167">contoso.com (root)</span></span> | <span data-ttu-id="ba42b-168">具有使用 </span><span class="sxs-lookup"><span data-stu-id="ba42b-168">A</span></span> | `@` | <span data-ttu-id="ba42b-169">來自[複製應用程式的 IP 位址](#info)的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ba42b-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="ba42b-170">www.contoso.com (子網域)</span><span class="sxs-lookup"><span data-stu-id="ba42b-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="ba42b-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="ba42b-171">CNAME</span></span> | `www` | <span data-ttu-id="ba42b-172">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ba42b-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="ba42b-173">\*.contoso.com (萬用字元)</span><span class="sxs-lookup"><span data-stu-id="ba42b-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="ba42b-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="ba42b-174">CNAME</span></span> | _\*_ | <span data-ttu-id="ba42b-175">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="ba42b-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="ba42b-176">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="ba42b-176">Save your settings.</span></span>

<span data-ttu-id="ba42b-177">DNS 查詢應該會在 DNS 散佈發生後立即開始解析為 App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ba42b-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba42b-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba42b-178">Next steps</span></span>

<span data-ttu-id="ba42b-179">了解如何將自訂 SSL 憑證繫結至 App Service。</span><span class="sxs-lookup"><span data-stu-id="ba42b-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba42b-180">將現有的自訂 SSL 憑證繫結至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="ba42b-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
