---
title: "aaaMigrate 作用中的 DNS 名稱 tooAzure 應用程式服務 |Microsoft 文件"
description: "了解如何自訂的 DNS 網域名稱已指派 tooa toomigrate 即時網站 tooAzure 應用程式服務不需任何停機。"
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
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="afceb-103">移轉作用中的 DNS 名稱 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="afceb-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="afceb-104">本文將告訴您如何 toomigrate 作用中的 DNS 名稱太[Azure App Service](../app-service/app-service-value-prop-what-is.md)完全不需要停機。</span><span class="sxs-lookup"><span data-stu-id="afceb-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="afceb-105">當您移轉即時網站和其 DNS 網域名稱 tooApp 服務時，該 DNS 名稱已提供服務的即時流量。</span><span class="sxs-lookup"><span data-stu-id="afceb-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="afceb-106">您可以事先繫結使用 DNS 名稱 tooyour hello App Service 應用程式，在 hello 移轉期間避免 DNS 解析中的停機時間。</span><span class="sxs-lookup"><span data-stu-id="afceb-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="afceb-107">如果您不擔心 DNS 解析中的停機時間，請參閱[對應現有自訂 DNS 名稱 tooAzure Web 應用程式](app-service-web-tutorial-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="afceb-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afceb-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="afceb-108">Prerequisites</span></span>

<span data-ttu-id="afceb-109">toocomplete 此使用方法：</span><span class="sxs-lookup"><span data-stu-id="afceb-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="afceb-110">[確定您的 App Service 應用程式不是位於免費層](app-service-web-tutorial-custom-domain.md#checkpricing)。</span><span class="sxs-lookup"><span data-stu-id="afceb-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="afceb-111">事先繫結 hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="afceb-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="afceb-112">當事先繫結的自訂網域時，您完成這兩個變更 DNS 記錄之前的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="afceb-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="afceb-113">確認網域擁有權</span><span class="sxs-lookup"><span data-stu-id="afceb-113">Verify domain ownership</span></span>
- <span data-ttu-id="afceb-114">啟用您的應用程式的 hello 網域名稱</span><span class="sxs-lookup"><span data-stu-id="afceb-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="afceb-115">當您最後會從舊網站 toohello hello App Service 應用程式移轉您自訂的 DNS 名稱時，DNS 解析中會有任何停機時間。</span><span class="sxs-lookup"><span data-stu-id="afceb-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="afceb-116">建立網域驗證記錄</span><span class="sxs-lookup"><span data-stu-id="afceb-116">Create domain verification record</span></span>

<span data-ttu-id="afceb-117">tooverify 網域擁有權，新增 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="afceb-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="afceb-118">從對應的 hello TXT 記錄_awverify。&lt;子網域 >_ too_&lt;應用程式名稱 >。 azurewebsites.net_。</span><span class="sxs-lookup"><span data-stu-id="afceb-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="afceb-119">hello TXT 記錄，您需要取決於 hello 想 toomigrate 的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="afceb-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="afceb-120">如需範例，請參閱下表中的 hello (`@`通常代表 hello 根網域):</span><span class="sxs-lookup"><span data-stu-id="afceb-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="afceb-121">DNS 記錄範例</span><span class="sxs-lookup"><span data-stu-id="afceb-121">DNS record example</span></span> | <span data-ttu-id="afceb-122">TXT 主機</span><span class="sxs-lookup"><span data-stu-id="afceb-122">TXT Host</span></span> | <span data-ttu-id="afceb-123">TXT 值</span><span class="sxs-lookup"><span data-stu-id="afceb-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="afceb-124">@ (根網域)</span><span class="sxs-lookup"><span data-stu-id="afceb-124">@ (root)</span></span> | <span data-ttu-id="afceb-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="afceb-125">_awverify_</span></span> | <span data-ttu-id="afceb-126">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="afceb-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="afceb-127">www (子網域)</span><span class="sxs-lookup"><span data-stu-id="afceb-127">www (sub)</span></span> | <span data-ttu-id="afceb-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="afceb-128">_awverify.www_</span></span> | <span data-ttu-id="afceb-129">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="afceb-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="afceb-130">\* (萬用字元)</span><span class="sxs-lookup"><span data-stu-id="afceb-130">\* (wildcard)</span></span> | <span data-ttu-id="afceb-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="afceb-131">_awverify.\*_</span></span> | <span data-ttu-id="afceb-132">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="afceb-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="afceb-133">在您 DNS 記錄 頁面中，記下 hello 記錄類型的 hello 想 toomigrate 的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="afceb-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="afceb-134">App Service 支援 CNAME 與 A 記錄之間的對應。</span><span class="sxs-lookup"><span data-stu-id="afceb-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="afceb-135">啟用您的應用程式的 hello 網域</span><span class="sxs-lookup"><span data-stu-id="afceb-135">Enable hello domain for your app</span></span>

<span data-ttu-id="afceb-136">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello hello 應用程式頁面的左導覽列中選取**自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="afceb-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="afceb-138">在 [hello**自訂網域**頁面上，選取 hello  **+** 圖示下一步] 太**新增主機名稱**。</span><span class="sxs-lookup"><span data-stu-id="afceb-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="afceb-140">型別 hello 完整的網域名稱新增 hello TXT 記錄，例如`www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="afceb-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="afceb-141">萬用字元網域 (像是\*。 contoso.com)，您可以使用任何符合 hello 萬用字元網域的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="afceb-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="afceb-142">選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="afceb-142">Select **Validate**.</span></span>

<span data-ttu-id="afceb-143">hello**新增 hostname**按鈕就會啟用。</span><span class="sxs-lookup"><span data-stu-id="afceb-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="afceb-144">請確定**主機名稱記錄類型**設定您想要 toomigrate toohello DNS 記錄類型。</span><span class="sxs-lookup"><span data-stu-id="afceb-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="afceb-145">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="afceb-145">Select **Add hostname**.</span></span>

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="afceb-147">它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="afceb-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="afceb-148">請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。</span><span class="sxs-lookup"><span data-stu-id="afceb-148">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="afceb-150">您的 DNS 名稱現已在您的 Azure 應用程式中啟用。</span><span class="sxs-lookup"><span data-stu-id="afceb-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="afceb-151">重新對應 hello 作用中的 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="afceb-151">Remap hello active DNS name</span></span>

<span data-ttu-id="afceb-152">hello 事左的 toodo 會重新對應您使用中的 DNS 記錄 toopoint tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="afceb-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="afceb-153">右現在，它仍然指向 tooyour 舊的站台。</span><span class="sxs-lookup"><span data-stu-id="afceb-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="afceb-154">複製 hello 應用程式的 IP 位址 （只記錄）</span><span class="sxs-lookup"><span data-stu-id="afceb-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="afceb-155">如果您重新對應的是 CNAME 記錄，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="afceb-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="afceb-156">tooremap A 記錄，您需要 hello App Service 應用程式的外部 IP 位址，如下所示 hello**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="afceb-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="afceb-157">關閉 hello**新增 hostname**頁面中的選取**X** hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="afceb-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="afceb-158">在 hello**自訂網域**頁面上，複製 hello 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="afceb-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="afceb-160">更新 hello DNS 記錄</span><span class="sxs-lookup"><span data-stu-id="afceb-160">Update hello DNS record</span></span>

<span data-ttu-id="afceb-161">在 hello 網域提供者的 DNS 記錄頁面上，選取 hello DNS 記錄 tooremap。</span><span class="sxs-lookup"><span data-stu-id="afceb-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="afceb-162">Hello`contoso.com`根網域的範例中，重新對應 hello A 或 CNAME 記錄，例如 hello 下表中的 hello 範例：</span><span class="sxs-lookup"><span data-stu-id="afceb-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="afceb-163">FQDN 範例</span><span class="sxs-lookup"><span data-stu-id="afceb-163">FQDN example</span></span> | <span data-ttu-id="afceb-164">記錄類型</span><span class="sxs-lookup"><span data-stu-id="afceb-164">Record type</span></span> | <span data-ttu-id="afceb-165">Host</span><span class="sxs-lookup"><span data-stu-id="afceb-165">Host</span></span> | <span data-ttu-id="afceb-166">值</span><span class="sxs-lookup"><span data-stu-id="afceb-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="afceb-167">contoso.com (根網域)</span><span class="sxs-lookup"><span data-stu-id="afceb-167">contoso.com (root)</span></span> | <span data-ttu-id="afceb-168">A</span><span class="sxs-lookup"><span data-stu-id="afceb-168">A</span></span> | `@` | <span data-ttu-id="afceb-169">從 IP 位址[複製 hello 應用程式的 IP 位址](#info)</span><span class="sxs-lookup"><span data-stu-id="afceb-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="afceb-170">www.contoso.com (子網域)</span><span class="sxs-lookup"><span data-stu-id="afceb-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="afceb-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="afceb-171">CNAME</span></span> | `www` | <span data-ttu-id="afceb-172">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="afceb-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="afceb-173">\*.contoso.com (萬用字元)</span><span class="sxs-lookup"><span data-stu-id="afceb-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="afceb-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="afceb-174">CNAME</span></span> | _\*_ | <span data-ttu-id="afceb-175">_&lt;應用程式名稱>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="afceb-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="afceb-176">儲存您的設定。</span><span class="sxs-lookup"><span data-stu-id="afceb-176">Save your settings.</span></span>

<span data-ttu-id="afceb-177">DNS 查詢應該只有在 DNS 傳播會發生之後，立即解決 tooyour App Service 應用程式會啟動。</span><span class="sxs-lookup"><span data-stu-id="afceb-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afceb-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afceb-178">Next steps</span></span>

<span data-ttu-id="afceb-179">了解如何 toobind 自訂 SSL 憑證 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="afceb-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="afceb-180">繫結現有自訂 SSL 憑證 tooAzure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="afceb-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
