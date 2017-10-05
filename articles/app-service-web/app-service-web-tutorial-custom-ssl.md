---
title: "將現有的自訂 SSL 憑證繫結至 Azure Web Apps | Microsoft Docs"
description: "了解如何將自訂 SSL 憑證繫結至 Azure App Service 中的 web 應用程式、行動裝置應用程式後端或 API 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="6093f-103">將現有的自訂 SSL 憑證繫結至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="6093f-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="6093f-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="6093f-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6093f-105">本教學課程會示範如何將您從受信任憑證授權單位購買的自訂 SSL 憑證繫結至 [Azure Web Apps](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6093f-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="6093f-106">當您完成時，將可以在自訂 DNS 網域的 HTTPS 端點存取 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Web 應用程式與自訂 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="6093f-108">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="6093f-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6093f-109">升級應用程式的定價層</span><span class="sxs-lookup"><span data-stu-id="6093f-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="6093f-110">將自訂 SSL 憑證繫結至 App Service</span><span class="sxs-lookup"><span data-stu-id="6093f-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="6093f-111">為應用程式強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6093f-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="6093f-112">使用指令碼來自動繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="6093f-113">如果您需要自訂 SSL 憑證，可以直接在 Azure 入口網站取得，並將它繫結至 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="6093f-114">遵循 [App Service 憑證教學課程](web-sites-purchase-ssl-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="6093f-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6093f-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="6093f-115">Prerequisites</span></span>

<span data-ttu-id="6093f-116">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="6093f-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="6093f-117">建立 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="6093f-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="6093f-118">將自訂 DNS 名稱對應至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6093f-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="6093f-119">取得受信任憑證授權單位所核發的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="6093f-120">SSL 憑證的需求</span><span class="sxs-lookup"><span data-stu-id="6093f-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="6093f-121">若要在 App Service 中使用憑證，憑證必須符合以下所有需求︰</span><span class="sxs-lookup"><span data-stu-id="6093f-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="6093f-122">由受信任的憑證授權單位簽署</span><span class="sxs-lookup"><span data-stu-id="6093f-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="6093f-123">以受密碼保護的 PFX 檔案形式匯出</span><span class="sxs-lookup"><span data-stu-id="6093f-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="6093f-124">包含長度至少為 2048 位元的私密金鑰</span><span class="sxs-lookup"><span data-stu-id="6093f-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="6093f-125">包含憑證鏈結中的所有中繼憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="6093f-126">**橢圓曲線密碼編譯 (ECC) 憑證**可搭配 App Service 使用，但不在本文討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="6093f-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="6093f-127">請洽詢您的憑證授權單位，了解建立 ECC 憑證的確切步驟。</span><span class="sxs-lookup"><span data-stu-id="6093f-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="6093f-128">準備您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6093f-128">Prepare your web app</span></span>

<span data-ttu-id="6093f-129">若要將自訂 SSL 憑證繫結至您的 web 應用程式，您的 [App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須為**基本**、**標準**或**進階**層。</span><span class="sxs-lookup"><span data-stu-id="6093f-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="6093f-130">在此步驟中，您要確定 Web 應用程式在支援的定價層。</span><span class="sxs-lookup"><span data-stu-id="6093f-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="6093f-131">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="6093f-131">Log in to Azure</span></span>

<span data-ttu-id="6093f-132">開啟 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6093f-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="6093f-133">瀏覽至您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6093f-133">Navigate to your web app</span></span>

<span data-ttu-id="6093f-134">按一下左側功能表中的 [應用程式服務]，然後按一下 Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="6093f-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![選取 Web 應用程式](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="6093f-136">您已經位於 Web 應用程式的管理頁面。</span><span class="sxs-lookup"><span data-stu-id="6093f-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="6093f-137">檢查定價層</span><span class="sxs-lookup"><span data-stu-id="6093f-137">Check the pricing tier</span></span>

<span data-ttu-id="6093f-138">在 Web 應用程式頁面的左側導覽中，捲動到 [設定] 區段，然後選取 [相應增加 (App Service 方案)]。</span><span class="sxs-lookup"><span data-stu-id="6093f-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![相應增加功能表](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="6093f-140">請檢查以確定您的 web 應用程式不在**免費**或**共用** 層中。</span><span class="sxs-lookup"><span data-stu-id="6093f-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="6093f-141">系統會以深藍色方塊醒目顯示 Web 應用程式目前的層。</span><span class="sxs-lookup"><span data-stu-id="6093f-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![檢查定價層](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="6093f-143">**免費**和**共用**層中不支援自訂 SSL。</span><span class="sxs-lookup"><span data-stu-id="6093f-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="6093f-144">如果您需要相應增加，請遵循下一節中的步驟來進行。</span><span class="sxs-lookup"><span data-stu-id="6093f-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="6093f-145">否則，請關閉 [選擇定價層] 頁面，然後跳至[上傳並繫結 SSL 憑證](#upload)。</span><span class="sxs-lookup"><span data-stu-id="6093f-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="6093f-146">相應增加您的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="6093f-146">Scale up your App Service plan</span></span>

<span data-ttu-id="6093f-147">選取**基本****標準**或**高階**層的其中一個。</span><span class="sxs-lookup"><span data-stu-id="6093f-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="6093f-148">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="6093f-148">Click **Select**.</span></span>

![選擇定價層](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="6093f-150">當您看見下列通知時，表示擴充作業已完成。</span><span class="sxs-lookup"><span data-stu-id="6093f-150">When you see the following notification, the scale operation is complete.</span></span>

![相應增加通知](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="6093f-152">繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-152">Bind your SSL certificate</span></span>

<span data-ttu-id="6093f-153">您已準備好將 SSL 憑證上傳至您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="6093f-154">合併中繼憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-154">Merge intermediate certificates</span></span>

<span data-ttu-id="6093f-155">如果憑證授權單位在憑證鏈結中提供多個憑證，您需要依序合併憑證。</span><span class="sxs-lookup"><span data-stu-id="6093f-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="6093f-156">若要這樣做，請在文字編輯器中開啟您收到的每個憑證。</span><span class="sxs-lookup"><span data-stu-id="6093f-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="6093f-157">為合併的憑證建立一個檔案，並取名為 _mergedcertificate.crt_。</span><span class="sxs-lookup"><span data-stu-id="6093f-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="6093f-158">在文字編輯器中，將每個憑證的內容複製到這個檔案中。</span><span class="sxs-lookup"><span data-stu-id="6093f-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="6093f-159">憑證的順序看起來應類似以下範本：</span><span class="sxs-lookup"><span data-stu-id="6093f-159">The order of your certificates should look like the following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="6093f-160">將憑證匯出為 PFX</span><span class="sxs-lookup"><span data-stu-id="6093f-160">Export certificate to PFX</span></span>

<span data-ttu-id="6093f-161">使用與憑證要求共同產生的私密金鑰，將您合併的 SSL 憑證匯出。</span><span class="sxs-lookup"><span data-stu-id="6093f-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="6093f-162">如果您是使用 OpenSSL 產生憑證要求，則已建立私密金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="6093f-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="6093f-163">若要將您的憑證匯出為 PFX，請執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="6093f-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="6093f-164">取代預留位置 _&lt;private-key-file>_ 和 _&lt;merged-certificate-file>_。</span><span class="sxs-lookup"><span data-stu-id="6093f-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="6093f-165">請在出現提示時定義一個匯出密碼。</span><span class="sxs-lookup"><span data-stu-id="6093f-165">When prompted, define an export password.</span></span> <span data-ttu-id="6093f-166">您之後將 SSL 憑證上傳至 App Service 時，將會用到這組密碼。</span><span class="sxs-lookup"><span data-stu-id="6093f-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="6093f-167">如果您使用 IIS 或 _Certreq.exe_ 產生憑證要求，請將憑證安裝至本機電腦，然後[將憑證匯出為 PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="6093f-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="6093f-168">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-168">Upload your SSL certificate</span></span>

<span data-ttu-id="6093f-169">若要上傳 SSL 憑證，請按一下 Web 應用程式左側導覽列中的 [SSL 憑證]。</span><span class="sxs-lookup"><span data-stu-id="6093f-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="6093f-170">按一下 [上傳憑證]。</span><span class="sxs-lookup"><span data-stu-id="6093f-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="6093f-171">在 [PFX 憑證檔案] 中，選取您的 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="6093f-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="6093f-172">在 [憑證密碼] 中，輸入您將 PFX 檔案匯出時所建立的密碼。</span><span class="sxs-lookup"><span data-stu-id="6093f-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="6093f-173">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="6093f-173">Click **Upload**.</span></span>

![Upload certificate](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="6093f-175">當 App Service 完成上傳您的憑證時，它會出現在 [SSL 憑證] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6093f-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificate uploaded](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="6093f-177">繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-177">Bind your SSL certificate</span></span>

<span data-ttu-id="6093f-178">在 [SSL 繫結] 區段中，按一下 [新增繫結]。</span><span class="sxs-lookup"><span data-stu-id="6093f-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="6093f-179">在 [新增 SSL 繫結] 頁面中，使用下拉式清單選取要保護的網域名稱，以及要使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="6093f-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="6093f-180">如果您已經上傳憑證，但 [主機名稱] 下拉式清單中沒有顯示網域名稱，請嘗試重新整理瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="6093f-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="6093f-181">在 **SSL 類型**中，選擇使用**[伺服器名稱指示 (SNI) ](http://en.wikipedia.org/wiki/Server_Name_Indication)**還是以 IP 為基礎的 SSL。</span><span class="sxs-lookup"><span data-stu-id="6093f-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="6093f-182">**以 SNI 為基礎的 SSL**：可能會新增多個以 SNI 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="6093f-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="6093f-183">此選項可允許多個 SSL 憑證保護同一個 IP 位址上的多個網域。</span><span class="sxs-lookup"><span data-stu-id="6093f-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="6093f-184">大多數現代化的瀏覽器 (包括 Internet Explorer、Chrome、Firefox 和 Opera) 都支援 SNI (可在[伺服器名稱指示](http://wikipedia.org/wiki/Server_Name_Indication)找到更完整的瀏覽器支援資訊)。</span><span class="sxs-lookup"><span data-stu-id="6093f-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="6093f-185">**以 IP 為基礎的 SSL**：可能只會新增一個以 IP 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="6093f-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="6093f-186">此選項只允許一個 SSL 憑證保護專用的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6093f-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="6093f-187">若要保護多個網域，您必須全部使用相同的 SSL 憑證來保護它們。</span><span class="sxs-lookup"><span data-stu-id="6093f-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="6093f-188">這是 SSL 繫結的傳統選項。</span><span class="sxs-lookup"><span data-stu-id="6093f-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="6093f-189">按一下 [新增繫結]。</span><span class="sxs-lookup"><span data-stu-id="6093f-189">Click **Add Binding**.</span></span>

![繫結 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="6093f-191">當 App Service 完成上傳您的憑證時，它會出現在 [SSL 繫結] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6093f-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![繫結至 web 應用程式的憑證](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="6093f-193">將 IP SSL 的 A 記錄重新對應</span><span class="sxs-lookup"><span data-stu-id="6093f-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="6093f-194">如果您不使用 web 應用程式中以 IP 為基礎的 SSL，請跳至[測試自訂網域的 HTTPS](#test)。</span><span class="sxs-lookup"><span data-stu-id="6093f-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="6093f-195">根據預設，web 應用程式會使用共用的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6093f-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="6093f-196">當您將以 IP 為基礎的 SSL 與憑證繫結時，App Service 會為 Web 應用程式建立新的專用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6093f-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="6093f-197">如果您已將 A 記錄對應至 web 應用程式，請使用這個新的專用 IP 位址來更新您的網域登錄。</span><span class="sxs-lookup"><span data-stu-id="6093f-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="6093f-198">已將 Web 應用程式的**自訂網域**頁面更新為新的專用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6093f-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="6093f-199">[複製此 IP 位址](app-service-web-tutorial-custom-domain.md#info)，然後[將 A 記錄重新對應](app-service-web-tutorial-custom-domain.md#map-an-a-record)到這個新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6093f-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="6093f-200">測試 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6093f-200">Test HTTPS</span></span>

<span data-ttu-id="6093f-201">現在只剩下確定 HTTPS 是否能用在您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="6093f-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="6093f-202">在各種瀏覽器中，瀏覽至 `https://<your.custom.domain>` 以查看它是否能提供您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![入口網站瀏覽至 Azure 應用程式](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="6093f-204">如果您的 web 應用程式出現憑證驗證錯誤，您可能使用了自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="6093f-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="6093f-205">如果不是，在您將憑證匯出為 PFX 檔案時，可能遺漏了中繼憑證。</span><span class="sxs-lookup"><span data-stu-id="6093f-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="6093f-206">強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6093f-206">Enforce HTTPS</span></span>

<span data-ttu-id="6093f-207">App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="6093f-208">若要強制 Web 應用程式使用 HTTPS，請在 Web 應用程式的 _web.config_ 檔案中定義重寫規則。</span><span class="sxs-lookup"><span data-stu-id="6093f-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="6093f-209">無論 Web 應用程式語言架構為何，App Service 應用程式都會使用這個檔案。</span><span class="sxs-lookup"><span data-stu-id="6093f-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="6093f-210">有語言特定的要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="6093f-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="6093f-211">ASP.NET MVC 可使用 [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) 篩選，而非 _web.config_ 中的重寫規則。</span><span class="sxs-lookup"><span data-stu-id="6093f-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="6093f-212">如果您是 .NET 開發人員，應該很熟悉這個檔案。</span><span class="sxs-lookup"><span data-stu-id="6093f-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="6093f-213">它會在您解決方案的根目錄。</span><span class="sxs-lookup"><span data-stu-id="6093f-213">It is in the root of your solution.</span></span>

<span data-ttu-id="6093f-214">此外，如果您是使用 PHP、Node.js、Python 或 Java 進行開發，我們有可能會在 App Service 中代表您產生這個檔案。</span><span class="sxs-lookup"><span data-stu-id="6093f-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="6093f-215">遵循[使用 FTP/S 將應用程式部署至 Azure App Service](app-service-deploy-ftp.md) 中的指示，連線到 Web 應用程式的 FTP 端點。</span><span class="sxs-lookup"><span data-stu-id="6093f-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="6093f-216">此檔案應該位於 _/home/site/wwwroot_。</span><span class="sxs-lookup"><span data-stu-id="6093f-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="6093f-217">如果沒有，請在此資料夾中建立一個 _web.config_ 檔案，並包含下列 XML：</span><span class="sxs-lookup"><span data-stu-id="6093f-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="6093f-218">對於現有的 _web.config_ 檔案，請將整個 `<rule>` 元素複製到 _web.config_ 的 `configuration/system.webServer/rewrite/rules` 元素中。</span><span class="sxs-lookup"><span data-stu-id="6093f-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="6093f-219">如果您的 _web.config_ 中有其他 `<rule>` 元素，請將複製的 `<rule>` 元素放在其他 `<rule>` 元素之前。</span><span class="sxs-lookup"><span data-stu-id="6093f-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="6093f-220">每當使用者向 web 應用程式要求 HTTP 時，此規則就會將 HTTP 301 (永久重新導向) 傳回 HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6093f-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="6093f-221">例如，它會從 `http://contoso.com` 重新導向至 `https://contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="6093f-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="6093f-222">如需 IIS URL Rewrite 模組的詳細資訊，請參閱 [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) \(英文\) 文件。</span><span class="sxs-lookup"><span data-stu-id="6093f-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="6093f-223">強制 Linux 上的 Web Apps 使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6093f-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="6093f-224">Linux 上的 App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6093f-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="6093f-225">若要強制 Web 應用程式使用 HTTPS，請在 Web 應用程式的 _.htaccess_ 檔案中定義重寫規則。</span><span class="sxs-lookup"><span data-stu-id="6093f-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="6093f-226">遵循[使用 FTP/S 將應用程式部署至 Azure App Service](app-service-deploy-ftp.md) 中的指示，連線到 Web 應用程式的 FTP 端點。</span><span class="sxs-lookup"><span data-stu-id="6093f-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="6093f-227">在 _/home/site/wwwroot_ 中，建立一個包含以下程式碼的 _.htaccess_ 檔案：</span><span class="sxs-lookup"><span data-stu-id="6093f-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="6093f-228">每當使用者向 web 應用程式要求 HTTP 時，此規則就會將 HTTP 301 (永久重新導向) 傳回 HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="6093f-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="6093f-229">例如，它會從 `http://contoso.com` 重新導向至 `https://contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="6093f-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="6093f-230">使用指令碼進行自動化</span><span class="sxs-lookup"><span data-stu-id="6093f-230">Automate with scripts</span></span>

<span data-ttu-id="6093f-231">您可以使用 [Azure CLI](/cli/azure/install-azure-cli) 或 [Azure PowerShell](/powershell/azure/overview)，透過指令碼將 web 應用程式的 SSL 繫結自動化。</span><span class="sxs-lookup"><span data-stu-id="6093f-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="6093f-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6093f-232">Azure CLI</span></span>

<span data-ttu-id="6093f-233">下列命令會將匯出的 PFX 檔案上傳，並取得憑證指紋。</span><span class="sxs-lookup"><span data-stu-id="6093f-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="6093f-234">下列命令會使用上述命令的指紋來新增以 SNI 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="6093f-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="6093f-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6093f-235">Azure PowerShell</span></span>

<span data-ttu-id="6093f-236">下列命令會將匯出的 PFX 檔案上傳，並新增以 SNI 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="6093f-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="6093f-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6093f-237">Next steps</span></span>

<span data-ttu-id="6093f-238">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="6093f-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6093f-239">升級應用程式的定價層</span><span class="sxs-lookup"><span data-stu-id="6093f-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="6093f-240">將自訂 SSL 憑證繫結至 App Service</span><span class="sxs-lookup"><span data-stu-id="6093f-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="6093f-241">為應用程式強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="6093f-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="6093f-242">使用指令碼來自動繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6093f-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="6093f-243">前進至下一個教學課程，以了解如何使用 Azure 內容傳遞網路。</span><span class="sxs-lookup"><span data-stu-id="6093f-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6093f-244">將內容傳遞網路 (CDN) 新增至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6093f-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
