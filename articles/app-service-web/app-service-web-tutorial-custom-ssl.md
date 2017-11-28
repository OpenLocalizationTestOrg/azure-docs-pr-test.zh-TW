---
title: "aaaBind 現有的自訂 SSL 憑證 tooAzure Web 應用程式 |Microsoft 文件"
description: "了解 tootoobind，自訂 SSL 憑證 tooyour web 應用程式、 行動裝置應用程式後端或在 Azure App Service API 應用程式。"
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
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="aca2f-103">繫結現有自訂 SSL 憑證 tooAzure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aca2f-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="aca2f-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="aca2f-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="aca2f-105">此教學課程會示範如何自訂 SSL toobind 您太購自受信任的憑證授權單位憑證[Azure Web Apps](app-service-web-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="aca2f-106">當您完成時，您會無法 tooaccess web 應用程式在您的自訂 DNS 網域的 hello HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="aca2f-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Web 應用程式與自訂 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="aca2f-108">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="aca2f-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aca2f-109">升級應用程式的定價層</span><span class="sxs-lookup"><span data-stu-id="aca2f-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="aca2f-110">繫結您自訂的 SSL 憑證 tooApp 服務</span><span class="sxs-lookup"><span data-stu-id="aca2f-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="aca2f-111">為應用程式強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="aca2f-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="aca2f-112">使用指令碼來自動繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="aca2f-113">如果您需要 tooget 自訂的 SSL 憑證，可以直接取得 hello Azure 入口網站中的其中一個，並將它繫結 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="aca2f-114">請遵循 hello [App Service 憑證教學課程](web-sites-purchase-ssl-web-site.md)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aca2f-115">必要條件</span><span class="sxs-lookup"><span data-stu-id="aca2f-115">Prerequisites</span></span>

<span data-ttu-id="aca2f-116">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="aca2f-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="aca2f-117">建立 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="aca2f-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="aca2f-118">對應的自訂 DNS 名稱 tooyour web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aca2f-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="aca2f-119">取得受信任憑證授權單位所核發的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="aca2f-120">SSL 憑證的需求</span><span class="sxs-lookup"><span data-stu-id="aca2f-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="aca2f-121">toouse App Service 中的憑證，hello 憑證必須符合下列需求的所有 hello:</span><span class="sxs-lookup"><span data-stu-id="aca2f-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="aca2f-122">由受信任的憑證授權單位簽署</span><span class="sxs-lookup"><span data-stu-id="aca2f-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="aca2f-123">以受密碼保護的 PFX 檔案形式匯出</span><span class="sxs-lookup"><span data-stu-id="aca2f-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="aca2f-124">包含長度至少為 2048 位元的私密金鑰</span><span class="sxs-lookup"><span data-stu-id="aca2f-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="aca2f-125">包含 hello 憑證鏈結中的所有中繼憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="aca2f-126">**橢圓曲線密碼編譯 (ECC) 憑證**可搭配 App Service 使用，但不在本文討論範圍內。</span><span class="sxs-lookup"><span data-stu-id="aca2f-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="aca2f-127">使用 hello 確切步驟 toocreate ECC 憑證上的憑證授權單位。</span><span class="sxs-lookup"><span data-stu-id="aca2f-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="aca2f-128">準備您的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aca2f-128">Prepare your web app</span></span>

<span data-ttu-id="aca2f-129">toobind 自訂 SSL 憑證 tooyour web 應用程式，您[App Service 方案](https://azure.microsoft.com/pricing/details/app-service/)必須在 hello**基本**，**標準**，或**Premium**層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="aca2f-130">在此步驟中，您確定，您的 web 應用程式在 hello 支援定價層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="aca2f-131">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="aca2f-131">Log in tooAzure</span></span>

<span data-ttu-id="aca2f-132">開啟 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="aca2f-133">瀏覽 tooyour web 應用程式</span><span class="sxs-lookup"><span data-stu-id="aca2f-133">Navigate tooyour web app</span></span>

<span data-ttu-id="aca2f-134">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="aca2f-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![選取 Web 應用程式](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="aca2f-136">您處於 hello 管理您的 web 應用程式 頁面。</span><span class="sxs-lookup"><span data-stu-id="aca2f-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="aca2f-137">核取 hello 定價層</span><span class="sxs-lookup"><span data-stu-id="aca2f-137">Check hello pricing tier</span></span>

<span data-ttu-id="aca2f-138">在 hello 左側瀏覽您的 web 應用程式頁面，捲動 toohello**設定**區段，然後選取**向上擴充 （應用程式服務方案）**。</span><span class="sxs-lookup"><span data-stu-id="aca2f-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![相應增加功能表](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="aca2f-140">請確定您的 web 應用程式不在 hello toomake**免費**或**共用**層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="aca2f-141">系統會以深藍色方塊醒目顯示 Web 應用程式目前的層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![檢查定價層](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="aca2f-143">不支援自訂 SSL hello**免費**或**共用**層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="aca2f-144">如果您需要 tooscale 總時，請遵循 hello 下一節中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="aca2f-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="aca2f-145">否則，請關閉 hello**選擇定價層**頁面上，並略過太[上傳和 SSL 憑證繫結](#upload)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="aca2f-146">相應增加您的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="aca2f-146">Scale up your App Service plan</span></span>

<span data-ttu-id="aca2f-147">選取其中一個 hello**基本**，**標準**，或**Premium**層。</span><span class="sxs-lookup"><span data-stu-id="aca2f-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="aca2f-148">按一下 [選取] 。</span><span class="sxs-lookup"><span data-stu-id="aca2f-148">Click **Select**.</span></span>

![選擇定價層](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="aca2f-150">當您看到下列通知 hello 時，hello 調整規模作業已完成。</span><span class="sxs-lookup"><span data-stu-id="aca2f-150">When you see hello following notification, hello scale operation is complete.</span></span>

![相應增加通知](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="aca2f-152">繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-152">Bind your SSL certificate</span></span>

<span data-ttu-id="aca2f-153">您已準備好 tooupload SSL 憑證 tooyour web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="aca2f-154">合併中繼憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-154">Merge intermediate certificates</span></span>

<span data-ttu-id="aca2f-155">如果您的憑證授權單位可提供您多個憑證 hello 憑證鏈結中，您需要為了 toomerge hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="aca2f-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="aca2f-156">toodo 這開啟每個憑證所收到的文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="aca2f-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="aca2f-157">建立 hello 合併憑證，請呼叫檔案_mergedcertificate.crt_。</span><span class="sxs-lookup"><span data-stu-id="aca2f-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="aca2f-158">在文字編輯器中，將複製到這個檔案的 hello 內容的每個憑證。</span><span class="sxs-lookup"><span data-stu-id="aca2f-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="aca2f-159">憑證的 hello 順序看起來應該像 hello 下列範本：</span><span class="sxs-lookup"><span data-stu-id="aca2f-159">hello order of your certificates should look like hello following template:</span></span>

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

### <a name="export-certificate-toopfx"></a><span data-ttu-id="aca2f-160">匯出憑證 tooPFX</span><span class="sxs-lookup"><span data-stu-id="aca2f-160">Export certificate tooPFX</span></span>

<span data-ttu-id="aca2f-161">使用 hello 私用金鑰來產生憑證要求匯出合併的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="aca2f-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="aca2f-162">如果您是使用 OpenSSL 產生憑證要求，則已建立私密金鑰檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="aca2f-163">tooexport 您憑證 tooPFX，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="aca2f-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="aca2f-164">Hello 預留位置取代_&lt;私用金鑰檔 >_和_&lt;合併憑證檔案 >_。</span><span class="sxs-lookup"><span data-stu-id="aca2f-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="aca2f-165">請在出現提示時定義一個匯出密碼。</span><span class="sxs-lookup"><span data-stu-id="aca2f-165">When prompted, define an export password.</span></span> <span data-ttu-id="aca2f-166">上傳您 SSL 憑證 tooApp 服務更新版本時，您將使用此密碼。</span><span class="sxs-lookup"><span data-stu-id="aca2f-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="aca2f-167">如果您使用 IIS 或_Certreq.exe_ toogenerate 您的憑證要求、 安裝 hello 憑證 tooyour 本機電腦，然後[匯出 hello 憑證 tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="aca2f-168">上傳 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-168">Upload your SSL certificate</span></span>

<span data-ttu-id="aca2f-169">tooupload SSL 憑證，請按一下**SSL 憑證**hello 左瀏覽 web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="aca2f-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="aca2f-170">按一下 [上傳憑證]。</span><span class="sxs-lookup"><span data-stu-id="aca2f-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="aca2f-171">在 [PFX 憑證檔案] 中，選取您的 PFX 檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="aca2f-172">在**憑證密碼**，匯出 hello PFX 檔案時，您所建立的型別 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="aca2f-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="aca2f-173">按一下 [上傳] 。</span><span class="sxs-lookup"><span data-stu-id="aca2f-173">Click **Upload**.</span></span>

![Upload certificate](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="aca2f-175">當應用程式服務完成上傳您的憑證時，它會出現在 hello **SSL 憑證**頁面。</span><span class="sxs-lookup"><span data-stu-id="aca2f-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificate uploaded](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="aca2f-177">繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-177">Bind your SSL certificate</span></span>

<span data-ttu-id="aca2f-178">在 hello **SSL 繫結**區段中，按一下**新增繫結**。</span><span class="sxs-lookup"><span data-stu-id="aca2f-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="aca2f-179">在 hello**新增 SSL 繫結**頁面上，使用 hello 下拉式清單 tooselect hello 網域名稱 toosecure 和 hello 憑證 toouse。</span><span class="sxs-lookup"><span data-stu-id="aca2f-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="aca2f-180">如果您已上傳您的憑證，但是看 hello 網域名稱在 hello **Hostname**下拉式清單中，請嘗試重新整理 hello 瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="aca2f-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="aca2f-181">在**SSL 類型**，選取是否 toouse **[伺服器名稱指示 (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** 或以 IP 為主的 SSL。</span><span class="sxs-lookup"><span data-stu-id="aca2f-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="aca2f-182">**以 SNI 為基礎的 SSL**：可能會新增多個以 SNI 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="aca2f-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="aca2f-183">此選項可讓多個 SSL 憑證 toosecure hello 上的多個網域相同的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="aca2f-184">大多數現代化的瀏覽器 (包括 Internet Explorer、Chrome、Firefox 和 Opera) 都支援 SNI (可在[伺服器名稱指示](http://wikipedia.org/wiki/Server_Name_Indication)找到更完整的瀏覽器支援資訊)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="aca2f-185">**以 IP 為基礎的 SSL**：可能只會新增一個以 IP 為基礎的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="aca2f-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="aca2f-186">此選項可讓只有一個 SSL 憑證 toosecure 專用的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="aca2f-187">toosecure 多個網域，您必須保護它們全部透過 hello 相同的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="aca2f-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="aca2f-188">這是以 SSL 繫結的 hello 傳統選項。</span><span class="sxs-lookup"><span data-stu-id="aca2f-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="aca2f-189">按一下 [新增繫結]。</span><span class="sxs-lookup"><span data-stu-id="aca2f-189">Click **Add Binding**.</span></span>

![繫結 SSL 憑證](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="aca2f-191">當應用程式服務完成上傳您的憑證時，它會出現在 hello **SSL 繫結**區段。</span><span class="sxs-lookup"><span data-stu-id="aca2f-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![憑證繫結 tooweb 應用程式](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="aca2f-193">將 IP SSL 的 A 記錄重新對應</span><span class="sxs-lookup"><span data-stu-id="aca2f-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="aca2f-194">如果您不在您 web 應用程式中使用 IP SSL，請略過太[測試您的自訂網域的 HTTPS](#test)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="aca2f-195">根據預設，web 應用程式會使用共用的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="aca2f-196">當您將以 IP 為基礎的 SSL 與憑證繫結時，App Service 會為 Web 應用程式建立新的專用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="aca2f-197">如果您已對應的記錄 tooyour web 應用程式，您的網域登錄以更新這個新的專用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="aca2f-198">Web 應用程式的**自訂網域**hello 新的專用 IP 位址更新頁面。</span><span class="sxs-lookup"><span data-stu-id="aca2f-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="aca2f-199">[複製此 IP 位址](app-service-web-tutorial-custom-domain.md#info)，然後[重新對應 hello 記錄](app-service-web-tutorial-custom-domain.md#map-an-a-record)toothis 新的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aca2f-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="aca2f-200">測試 HTTPS</span><span class="sxs-lookup"><span data-stu-id="aca2f-200">Test HTTPS</span></span>

<span data-ttu-id="aca2f-201">所有已離開 toodo 是 toomake 確定 HTTPS 適合您的自訂網域。</span><span class="sxs-lookup"><span data-stu-id="aca2f-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="aca2f-202">在不同的瀏覽器中瀏覽過`https://<your.custom.domain>`toosee，設定您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![入口網站瀏覽 tooAzure 應用程式](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="aca2f-204">如果您的 web 應用程式出現憑證驗證錯誤，您可能使用了自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="aca2f-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="aca2f-205">如果不是 hello 案例，您可能有遺漏的中繼憑證匯出您的憑證 toohello PFX 檔案時。</span><span class="sxs-lookup"><span data-stu-id="aca2f-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="aca2f-206">強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="aca2f-206">Enforce HTTPS</span></span>

<span data-ttu-id="aca2f-207">App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="aca2f-208">web 應用程式的 HTTPS tooenforce 定義重寫規則中 hello _web.config_ web 應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="aca2f-209">應用程式服務會使用這個檔案，不論 hello 語言架構 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="aca2f-210">有語言特定的要求重新導向。</span><span class="sxs-lookup"><span data-stu-id="aca2f-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="aca2f-211">ASP.NET MVC 可使用 hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx)篩選器，而不是在 hello 重寫規則_web.config_。</span><span class="sxs-lookup"><span data-stu-id="aca2f-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="aca2f-212">如果您是 .NET 開發人員，應該很熟悉這個檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="aca2f-213">它會在您方案的 hello 根目錄。</span><span class="sxs-lookup"><span data-stu-id="aca2f-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="aca2f-214">此外，如果您是使用 PHP、Node.js、Python 或 Java 進行開發，我們有可能會在 App Service 中代表您產生這個檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="aca2f-215">Tooyour web 應用程式的 FTP 端點連接在 hello 指示[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="aca2f-216">此檔案應該位於 _/home/site/wwwroot_。</span><span class="sxs-lookup"><span data-stu-id="aca2f-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="aca2f-217">如果沒有，請建立_web.config_以下列 XML 的 hello 這個資料夾中的檔案：</span><span class="sxs-lookup"><span data-stu-id="aca2f-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

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

<span data-ttu-id="aca2f-218">現有_web.config_檔案中，複製 hello 整個`<rule>`項目插入您_web.config_的`configuration/system.webServer/rewrite/rules`項目。</span><span class="sxs-lookup"><span data-stu-id="aca2f-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="aca2f-219">如果有其他`<rule>`中的項目您_web.config_，複製的位置 hello`<rule>`之前 hello 其他項目`<rule>`項目。</span><span class="sxs-lookup"><span data-stu-id="aca2f-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="aca2f-220">每當 hello 使用者提出 HTTP 要求 tooyour web 應用程式時，此規則就會傳回 HTTP 301 （永久重新導向） toohello HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="aca2f-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="aca2f-221">例如，它會重新導向從`http://contoso.com`太`https://contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="aca2f-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="aca2f-222">如需有關 hello IIS URL Rewrite 模組的詳細資訊，請參閱 hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite)文件。</span><span class="sxs-lookup"><span data-stu-id="aca2f-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="aca2f-223">強制 Linux 上的 Web Apps 使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="aca2f-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="aca2f-224">Linux 上的 App Service 不會強制使用 HTTPS，因此任何使用者仍可以使用 HTTP 存取您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aca2f-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="aca2f-225">web 應用程式的 HTTPS tooenforce 定義重寫規則中 hello _.htaccess_ web 應用程式的檔案。</span><span class="sxs-lookup"><span data-stu-id="aca2f-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="aca2f-226">Tooyour web 應用程式的 FTP 端點連接在 hello 指示[部署您使用 FTP/S 的應用程式服務的應用程式 tooAzure](app-service-deploy-ftp.md)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="aca2f-227">在_/home/site/wwwroot_，建立_.htaccess_檔案以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="aca2f-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="aca2f-228">每當 hello 使用者提出 HTTP 要求 tooyour web 應用程式時，此規則就會傳回 HTTP 301 （永久重新導向） toohello HTTPS 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="aca2f-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="aca2f-229">例如，它會重新導向從`http://contoso.com`太`https://contoso.com`。</span><span class="sxs-lookup"><span data-stu-id="aca2f-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="aca2f-230">使用指令碼進行自動化</span><span class="sxs-lookup"><span data-stu-id="aca2f-230">Automate with scripts</span></span>

<span data-ttu-id="aca2f-231">您可以自動化的 SSL 繫結的 web 應用程式與指令碼，使用 hello [Azure CLI](/cli/azure/install-azure-cli)或[Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="aca2f-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="aca2f-232">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aca2f-232">Azure CLI</span></span>

<span data-ttu-id="aca2f-233">hello 下列命令會將匯出的 PFX 檔案上傳，並取得 hello 指紋。</span><span class="sxs-lookup"><span data-stu-id="aca2f-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="aca2f-234">hello 下列命令會將使用 hello 指紋 hello 前一個命令從 sni SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="aca2f-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="aca2f-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="aca2f-235">Azure PowerShell</span></span>

<span data-ttu-id="aca2f-236">hello 下列命令將匯出的 PFX 檔案上傳並新增 sni SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="aca2f-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="aca2f-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aca2f-237">Next steps</span></span>

<span data-ttu-id="aca2f-238">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="aca2f-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aca2f-239">升級應用程式的定價層</span><span class="sxs-lookup"><span data-stu-id="aca2f-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="aca2f-240">繫結您自訂的 SSL 憑證 tooApp 服務</span><span class="sxs-lookup"><span data-stu-id="aca2f-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="aca2f-241">為應用程式強制使用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="aca2f-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="aca2f-242">使用指令碼來自動繫結 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="aca2f-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="aca2f-243">如何前進 toohello 下一個教學課程 toolearn toouse Azure 內容傳遞網路。</span><span class="sxs-lookup"><span data-stu-id="aca2f-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aca2f-244">將內容傳遞網路 (CDN) tooan Azure App Service</span><span class="sxs-lookup"><span data-stu-id="aca2f-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
