---
title: "aaaMap 現有的自訂 DNS 命名 tooAzure Web 應用程式 |Microsoft 文件"
description: "了解如何 tooadd 現有的自訂 DNS 網域名稱 （虛名網域） tooa web 應用程式、 行動裝置應用程式後端或在 Azure App Service API 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="51387-103">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="51387-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="51387-104">[Azure Web Apps](app-service-web-overview.md) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="51387-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="51387-105">本教學課程會示範如何 toomap 現有的自訂 DNS 命名 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51387-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="51387-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="51387-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51387-108">使用 CNAME 記錄來對應子網域 (例如，`www.contoso.com`)</span><span class="sxs-lookup"><span data-stu-id="51387-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="51387-109">使用 A 記錄來對應根網域 (例如，`contoso.com`)</span><span class="sxs-lookup"><span data-stu-id="51387-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="51387-110">使用 CNAME 記錄來對應萬用字元網域 (例如，`*.contoso.com`)</span><span class="sxs-lookup"><span data-stu-id="51387-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="51387-111">使用指令碼來自動對應網域</span><span class="sxs-lookup"><span data-stu-id="51387-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="51387-112">您可以使用**CNAME 記錄**或**記錄**toomap 自訂的 DNS 名稱 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="51387-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="51387-113">我們建議您對所有自訂 DNS 名稱使用 CNAME，但根網域除外 (例如 `contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="51387-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="51387-114">toomigrate 即時網站和其 DNS 網域名稱 tooApp 服務，請參閱[移轉作用中的 DNS 名稱 tooAzure App Service](app-service-custom-domain-name-migrate.md)。</span><span class="sxs-lookup"><span data-stu-id="51387-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51387-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="51387-115">Prerequisites</span></span>

<span data-ttu-id="51387-116">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="51387-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="51387-117">[建立 App Service 應用程式](/azure/app-service/)，或使用您針對另一個教學課程建立的應用程式。</span><span class="sxs-lookup"><span data-stu-id="51387-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="51387-118">購買網域名稱，並確定您的網域提供者 （例如 GoDaddy) 存取 toohello DNS 登錄。</span><span class="sxs-lookup"><span data-stu-id="51387-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="51387-119">例如，tooadd DNS 項目`contoso.com`和`www.contoso.com`，您必須是能夠 tooconfigure hello DNS 設定 hello`contoso.com`根網域。</span><span class="sxs-lookup"><span data-stu-id="51387-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="51387-120">如果您沒有現有的網域名稱，請考慮[購買網域使用 hello Azure 入口網站](custom-dns-web-site-buydomains-web-app.md)。</span><span class="sxs-lookup"><span data-stu-id="51387-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="51387-121">準備 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="51387-121">Prepare hello app</span></span>

<span data-ttu-id="51387-122">toomap 自訂 DNS 名稱 tooa web 應用程式，hello web 應用程式的[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須付費的層 (**共用**，**基本**，**標準**，或**進階**)。</span><span class="sxs-lookup"><span data-stu-id="51387-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="51387-123">在此步驟中，您確定該 hello App Service 應用程式是在 hello 支援定價層。</span><span class="sxs-lookup"><span data-stu-id="51387-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="51387-124">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="51387-124">Sign in tooAzure</span></span>

<span data-ttu-id="51387-125">開啟 hello [Azure 入口網站](https://portal.azure.com)並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="51387-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="51387-126">瀏覽 toohello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="51387-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="51387-127">從 hello 左窗格中，選取**應用程式服務**，然後選取 hello hello 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="51387-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="51387-129">您會看到 hello hello App Service 應用程式管理頁面。</span><span class="sxs-lookup"><span data-stu-id="51387-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="51387-130">核取 hello 定價層</span><span class="sxs-lookup"><span data-stu-id="51387-130">Check hello pricing tier</span></span>

<span data-ttu-id="51387-131">在 hello 左瀏覽的 hello 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。</span><span class="sxs-lookup"><span data-stu-id="51387-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![相應增加功能表](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="51387-133">hello 應用程式目前的階層會以藍色框線反白顯示。</span><span class="sxs-lookup"><span data-stu-id="51387-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="51387-134">請確定該 hello 應用程式不在 hello toomake**免費**層。</span><span class="sxs-lookup"><span data-stu-id="51387-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="51387-135">不支援自訂 DNS hello**免費**層。</span><span class="sxs-lookup"><span data-stu-id="51387-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![檢查定價層](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="51387-137">如果 hello App Service 方案不**免費**，請關閉 hello**選擇定價層**頁面上，並略過太[CNAME 記錄對應](#cname)。</span><span class="sxs-lookup"><span data-stu-id="51387-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="51387-138">向上擴充 hello App Service 方案</span><span class="sxs-lookup"><span data-stu-id="51387-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="51387-139">選取任何 hello 非可用層 (**共用**，**基本**，**標準**，或**Premium**)。</span><span class="sxs-lookup"><span data-stu-id="51387-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="51387-140">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="51387-140">Click **Select**.</span></span>

![檢查定價層](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="51387-142">當您看到下列通知 hello 時，hello 調整規模作業已完成。</span><span class="sxs-lookup"><span data-stu-id="51387-142">When you see hello following notification, hello scale operation is complete.</span></span>

![擴充作業確認](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="51387-144">對應 CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="51387-144">Map a CNAME record</span></span>

<span data-ttu-id="51387-145">您可以在 hello 教學課程範例中，加入 hello 的 CNAME 記錄`www`子網域 (例如， `www.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="51387-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="51387-146">建立 hello CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="51387-146">Create hello CNAME record</span></span>

<span data-ttu-id="51387-147">新增子網域 toohello 應用程式的預設主機名稱的 CNAME 記錄 toomap (`<app_name>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="51387-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="51387-148">Hello`www.contoso.com`網域範例中，新增 CNAME 記錄對應 hello 名稱`www`太`<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="51387-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="51387-149">您新增 hello CNAME 之後，hello DNS 記錄 頁面看起來像下列範例中的 hello 中：</span><span class="sxs-lookup"><span data-stu-id="51387-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="51387-151">啟用在 Azure 中的 hello CNAME 記錄對應</span><span class="sxs-lookup"><span data-stu-id="51387-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="51387-152">在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="51387-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="51387-154">在 hello**自訂網域**頁面 hello 應用程式，加入 hello 完整自訂的 DNS 名稱 (`www.contoso.com`) toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="51387-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="51387-155">選取 hello  **+** 圖示下一步太**新增 hostname**。</span><span class="sxs-lookup"><span data-stu-id="51387-155">Select hello **+** icon next too**Add hostname**.</span></span>

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="51387-157">型別 hello 完整的網域名稱加入 CNAME 記錄，例如`www.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="51387-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="51387-158">選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="51387-158">Select **Validate**.</span></span>

<span data-ttu-id="51387-159">hello**新增 hostname**按鈕就會啟用。</span><span class="sxs-lookup"><span data-stu-id="51387-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="51387-160">請確定**主機名稱記錄類型**設定得**（www.example.com 或任何子網域） 的 CNAME**。</span><span class="sxs-lookup"><span data-stu-id="51387-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="51387-161">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="51387-161">Select **Add hostname**.</span></span>

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="51387-163">它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="51387-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="51387-164">請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。</span><span class="sxs-lookup"><span data-stu-id="51387-164">Try refreshing hello browser tooupdate hello data.</span></span>

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="51387-166">如果您錯過步驟或打錯字了某處更早版本，請參閱在 hello hello 頁面底部的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="51387-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![驗證錯誤](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="51387-168">對應 A 記錄</span><span class="sxs-lookup"><span data-stu-id="51387-168">Map an A record</span></span>

<span data-ttu-id="51387-169">您可以在 hello 教學課程範例中，加入 hello 根網域的 A 記錄 (例如， `contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="51387-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="51387-170">複製 hello 應用程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="51387-170">Copy hello app's IP address</span></span>

<span data-ttu-id="51387-171">toomap A 記錄，您需要 hello 應用程式的外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51387-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="51387-172">您可以在 hello 應用程式中找到這個 IP 位址**自訂網域**hello Azure 入口網站中的頁面。</span><span class="sxs-lookup"><span data-stu-id="51387-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="51387-173">在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="51387-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="51387-175">在 hello**自訂網域**頁面上，複製 hello 應用程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="51387-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="51387-177">建立 hello A 記錄</span><span class="sxs-lookup"><span data-stu-id="51387-177">Create hello A record</span></span>

<span data-ttu-id="51387-178">toomap A 記錄 tooan 應用程式，應用程式服務需要**兩個**DNS 記錄：</span><span class="sxs-lookup"><span data-stu-id="51387-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="51387-179">**A** toomap toohello 應用程式的 IP 位址記錄下來。</span><span class="sxs-lookup"><span data-stu-id="51387-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="51387-180">A **TXT**記錄 toomap toohello 應用程式的預設主機名稱`<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="51387-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="51387-181">應用程式服務會使用此記錄只有在設定時，tooverify 您擁有 hello 自訂網域。</span><span class="sxs-lookup"><span data-stu-id="51387-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="51387-182">驗證您的自訂網域並且在 App Service 中設定之後，您就可以刪除此 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="51387-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="51387-183">Hello`contoso.com`網域範例中，建立根據下表 toohello hello A 和 TXT 記錄 (`@`通常代表 hello 根網域)。</span><span class="sxs-lookup"><span data-stu-id="51387-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="51387-184">記錄類型</span><span class="sxs-lookup"><span data-stu-id="51387-184">Record type</span></span> | <span data-ttu-id="51387-185">Host</span><span class="sxs-lookup"><span data-stu-id="51387-185">Host</span></span> | <span data-ttu-id="51387-186">值</span><span class="sxs-lookup"><span data-stu-id="51387-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="51387-187">A</span><span class="sxs-lookup"><span data-stu-id="51387-187">A</span></span> | `@` | <span data-ttu-id="51387-188">從 IP 位址[複製 hello 應用程式的 IP 位址](#info)</span><span class="sxs-lookup"><span data-stu-id="51387-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="51387-189">TXT</span><span class="sxs-lookup"><span data-stu-id="51387-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="51387-190">當您加入 hello 記錄時，hello DNS 記錄 頁面看起來像 hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="51387-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![[DNS 記錄] 頁面](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="51387-192">啟用 hello 記錄中的對應 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="51387-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="51387-193">在 hello 應用程式**自訂網域**在 hello Azure 入口網站頁面上，新增 hello 完整自訂的 DNS 名稱 (例如， `contoso.com`) toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="51387-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="51387-194">選取 hello  **+** 圖示下一步太**新增 hostname**。</span><span class="sxs-lookup"><span data-stu-id="51387-194">Select hello **+** icon next too**Add hostname**.</span></span>

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="51387-196">型別 hello 完整的網域名稱設定 hello A 記錄，例如`contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="51387-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="51387-197">選取 [驗證]。</span><span class="sxs-lookup"><span data-stu-id="51387-197">Select **Validate**.</span></span>

<span data-ttu-id="51387-198">hello**新增 hostname**按鈕就會啟用。</span><span class="sxs-lookup"><span data-stu-id="51387-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="51387-199">請確定**主機名稱記錄類型**設定得**記錄 (example.com)**。</span><span class="sxs-lookup"><span data-stu-id="51387-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="51387-200">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="51387-200">Select **Add hostname**.</span></span>

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="51387-202">它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="51387-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="51387-203">請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。</span><span class="sxs-lookup"><span data-stu-id="51387-203">Try refreshing hello browser tooupdate hello data.</span></span>

![A 記錄已新增](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="51387-205">如果您錯過步驟或打錯字了某處更早版本，請參閱在 hello hello 頁面底部的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="51387-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![驗證錯誤](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="51387-207">對應萬用字元網域</span><span class="sxs-lookup"><span data-stu-id="51387-207">Map a wildcard domain</span></span>

<span data-ttu-id="51387-208">在 hello 教學課程範例中，您將對應[萬用字元 DNS 名稱](https://en.wikipedia.org/wiki/Wildcard_DNS_record)(例如， `*.contoso.com`) toohello App Service 應用程式藉由新增一筆 CNAME 記錄。</span><span class="sxs-lookup"><span data-stu-id="51387-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="51387-209">建立 hello CNAME 記錄</span><span class="sxs-lookup"><span data-stu-id="51387-209">Create hello CNAME record</span></span>

<span data-ttu-id="51387-210">新增萬用字元名稱 toohello 應用程式的預設主機名稱的 CNAME 記錄 toomap (`<app_name>.azurewebsites.net`)。</span><span class="sxs-lookup"><span data-stu-id="51387-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="51387-211">Hello`*.contoso.com`網域範例 hello CNAME 記錄會對應 hello 名稱`*`太`<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="51387-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="51387-212">當加入 hello CNAME 時，hello DNS 記錄 頁面看起來像 hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="51387-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="51387-214">啟用 hello 應用程式中的 hello CNAME 記錄對應</span><span class="sxs-lookup"><span data-stu-id="51387-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="51387-215">您現在可以新增任何符合 hello 萬用字元名稱 toohello 應用程式的子網域 (例如，`sub1.contoso.com`和`sub2.contoso.com`符合`*.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="51387-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="51387-216">在 hello 處於 hello Azure 入口網站的導覽 hello 應用程式頁面，選取 **自訂網域**。</span><span class="sxs-lookup"><span data-stu-id="51387-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![[自訂網域] 功能表](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="51387-218">選取 hello  **+** 圖示下一步太**新增 hostname**。</span><span class="sxs-lookup"><span data-stu-id="51387-218">Select hello **+** icon next too**Add hostname**.</span></span>

![新增主機名稱](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="51387-220">輸入符合 hello 萬用字元網域的完整的網域名稱 (例如， `sub1.contoso.com`)，然後選取**驗證**。</span><span class="sxs-lookup"><span data-stu-id="51387-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="51387-221">hello**新增 hostname**按鈕就會啟用。</span><span class="sxs-lookup"><span data-stu-id="51387-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="51387-222">請確定**主機名稱記錄類型**設定得**（www.example.com 或任何子網域） 的 CNAME 記錄**。</span><span class="sxs-lookup"><span data-stu-id="51387-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="51387-223">選取 [新增主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="51387-223">Select **Add hostname**.</span></span>

![新增 DNS 名稱 toohello 應用程式](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="51387-225">它可能需要一些時間 hello 反映在 hello 應用程式的新主機名稱 toobe**自訂網域**頁面。</span><span class="sxs-lookup"><span data-stu-id="51387-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="51387-226">請嘗試重新整理 hello 瀏覽器 tooupdate hello 資料。</span><span class="sxs-lookup"><span data-stu-id="51387-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="51387-227">選取 hello  **+** 圖示再次 tooadd 與 hello 萬用字元網域相符的另一個主機名稱。</span><span class="sxs-lookup"><span data-stu-id="51387-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="51387-228">例如，新增 `sub2.contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="51387-228">For example, add `sub2.contoso.com`.</span></span>

![CNAME 記錄已新增](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="51387-230">在瀏覽器中測試</span><span class="sxs-lookup"><span data-stu-id="51387-230">Test in browser</span></span>

<span data-ttu-id="51387-231">瀏覽 toohello 您先前設定的 DNS 名稱 (例如， `contoso.com`， `www.contoso.com`， `sub1.contoso.com`，和`sub2.contoso.com`)。</span><span class="sxs-lookup"><span data-stu-id="51387-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="51387-233">使用指令碼進行自動化</span><span class="sxs-lookup"><span data-stu-id="51387-233">Automate with scripts</span></span>

<span data-ttu-id="51387-234">您可以自動化的指令碼，自訂網域管理使用 hello [Azure CLI](/cli/azure/install-azure-cli)或[Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="51387-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="51387-235">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="51387-235">Azure CLI</span></span> 

<span data-ttu-id="51387-236">hello，下列命令會將已設定自訂 DNS 名稱 tooan App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51387-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="51387-237">如需詳細資訊，請參閱[對應自訂網域 tooa web 應用程式](scripts/app-service-cli-configure-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="51387-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="51387-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="51387-238">Azure PowerShell</span></span> 

<span data-ttu-id="51387-239">hello，下列命令會將已設定自訂 DNS 名稱 tooan App Service 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51387-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="51387-240">如需詳細資訊，請參閱[指派自訂網域 tooa web 應用程式](scripts/app-service-powershell-configure-custom-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="51387-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51387-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51387-241">Next steps</span></span>

<span data-ttu-id="51387-242">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="51387-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51387-243">使用 CNAME 記錄來對應子網域</span><span class="sxs-lookup"><span data-stu-id="51387-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="51387-244">使用 A 記錄來對應根網域</span><span class="sxs-lookup"><span data-stu-id="51387-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="51387-245">使用 CNAME 記錄來對應萬用字元網域</span><span class="sxs-lookup"><span data-stu-id="51387-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="51387-246">使用指令碼來自動對應網域</span><span class="sxs-lookup"><span data-stu-id="51387-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="51387-247">前進 toohello 下一個教學課程 toolearn toobind 自訂 SSL 憑證 tooa web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="51387-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51387-248">繫結現有自訂 SSL 憑證 tooAzure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="51387-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
