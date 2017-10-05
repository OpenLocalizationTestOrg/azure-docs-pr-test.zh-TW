---
title: "將 SSL 憑證新增至 Azure App Service 應用程式 | Microsoft Docs"
description: "了解如何將 SSL 憑證新增至您的 App Service 應用程式。"
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="357d6-103">購買並設定您的 Azure App Service 的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="357d6-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="357d6-104">在本教學課程中，您會購買 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** 的 SSL 憑證，安全地將它儲存在 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 中，並將它與自訂網域產生關聯，藉此保護 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="357d6-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="357d6-105">步驟 1 - 登入 Azure</span><span class="sxs-lookup"><span data-stu-id="357d6-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="357d6-106">登入 Azure 入口網站，網址是 http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="357d6-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="357d6-107">步驟 2 - 訂購 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="357d6-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="357d6-108">您可以在 **Azure 入口網站**中建立新的 [App Service 憑證](https://portal.azure.com/#create/Microsoft.SSL)，以訂購 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![建立憑證](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="357d6-110">輸入易記的 [名稱] 作為 SSL 憑證，並輸入 [網域名稱]</span><span class="sxs-lookup"><span data-stu-id="357d6-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-111">這是購買程序中其中一個最重要的部分。</span><span class="sxs-lookup"><span data-stu-id="357d6-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="357d6-112">請務必輸入您想要使用此憑證保護的正確主機名稱 (自訂網域)。</span><span class="sxs-lookup"><span data-stu-id="357d6-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="357d6-113">**請勿** 在主機名稱上附加 WWW。</span><span class="sxs-lookup"><span data-stu-id="357d6-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="357d6-114">選取 [訂用帳戶]、[資源群組] 和 [憑證 SKU]。</span><span class="sxs-lookup"><span data-stu-id="357d6-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="357d6-115">App Service 憑證只能由相同訂用帳戶中的其他應用程式服務使用。</span><span class="sxs-lookup"><span data-stu-id="357d6-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="357d6-116">步驟 3 - 將憑證儲存至 Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="357d6-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 是一項 Azure 服務，可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="357d6-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="357d6-118">完成 SSL 憑證購買程序之後，您必須開啟 [App Service 憑證](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders)的 [資源] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="357d6-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![插入準備在 KV 中儲存的影像](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="357d6-120">您會注意到憑證狀態是「暫止發行」，因為您必須先完成一些其他的步驟，才能開始使用此憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="357d6-121">按一下 [憑證屬性] 刀鋒視窗內的 [憑證設定]，然後按一下 [步驟 1：儲存]，將此憑證儲存至 Azure Key Vault。</span><span class="sxs-lookup"><span data-stu-id="357d6-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="357d6-122">從 [Key Vault 狀態] 刀鋒視窗中按一下 [Key Vault 存放庫]，選擇要儲存此憑證的現有 Key Vault，或者選擇 [建立新的 Key Vault]，在相同訂用帳戶和資源群組內建立新的 Key Vault。</span><span class="sxs-lookup"><span data-stu-id="357d6-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-123">Azure Key Vault 儲存此憑證會產生少許費用。</span><span class="sxs-lookup"><span data-stu-id="357d6-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="357d6-124">如需詳細資訊，請參閱 **[Azure Key Vault 定價詳細資料](https://azure.microsoft.com/pricing/details/key-vault/)**。</span><span class="sxs-lookup"><span data-stu-id="357d6-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="357d6-125">選取要儲存此憑證的 Key Vault 存放庫後，[儲存] 選項應顯示成功。</span><span class="sxs-lookup"><span data-stu-id="357d6-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![插入在 KV 中儲存成功的影像](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="357d6-127">步驟 4︰確認網域擁有權</span><span class="sxs-lookup"><span data-stu-id="357d6-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-128">App Service 憑證支援 3 種類型的網域驗證：網域、郵件和手動驗證。</span><span class="sxs-lookup"><span data-stu-id="357d6-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="357d6-129">[進階](#advanced)一節中會有詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="357d6-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="357d6-130">從您在步驟 3 使用的相同 [憑證設定] 刀鋒視窗，按一下 [步驟 2：驗證] 步驟。</span><span class="sxs-lookup"><span data-stu-id="357d6-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="357d6-131">**網域驗證**：**只有**在您**已經從 Azure App Service 購買自訂網域[時，這才是最方便的程序。](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="357d6-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="357d6-132">按一下 [驗證] 按鈕來完成這個步驟。</span><span class="sxs-lookup"><span data-stu-id="357d6-132">Click on **Verify** button to complete this step.</span></span>

![插入網域驗證的影像](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="357d6-134">按一下 [驗證] 之後，使用 [重新整理] 按鈕，直到 [驗證] 選項顯示成功為止。</span><span class="sxs-lookup"><span data-stu-id="357d6-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![插入在 KV 中驗證成功的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="357d6-136">步驟 5 - 將憑證指派給 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="357d6-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-137">在執行本節中的步驟之前，您必須先建立自訂網域名稱與應用程式的關聯。</span><span class="sxs-lookup"><span data-stu-id="357d6-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="357d6-138">如需詳細資訊，請參閱**[設定 Web 應用程式的自訂網域名稱。](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="357d6-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="357d6-139">在 **[Azure 入口網站](https://portal.azure.com/)**中，按一下頁面左側的 [App Service] 選項。</span><span class="sxs-lookup"><span data-stu-id="357d6-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="357d6-140">按一下您要指派此憑證的應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="357d6-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="357d6-141">在 [設定] 中，按一下 [SSL 憑證]。</span><span class="sxs-lookup"><span data-stu-id="357d6-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="357d6-142">按一下 [匯入 App Service 憑證] 並選取您剛購買的憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![插入匯入憑證的影像](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="357d6-144">在 [SSL 繫結] 區段中，按一下 [新增繫結]，然後使用下拉式清單選取要以 SSL 保護的網域名稱，以及要使用的憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="357d6-145">您也可以選擇使用**[伺服器名稱指示 (SNI) ](http://en.wikipedia.org/wiki/Server_Name_Indication)**還是 IP SSL。</span><span class="sxs-lookup"><span data-stu-id="357d6-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![插入 SSL 繫結的影像](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="357d6-147">按一下 [新增繫結]  ，儲存變更並啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="357d6-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="357d6-148">如果您已選取 [以 IP 為基礎的 SSL]，而且您的自訂網域是以 A 記錄設定，則必須執行下列額外步驟。</span><span class="sxs-lookup"><span data-stu-id="357d6-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="357d6-149">[進階](#Advanced)一節中會有詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="357d6-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="357d6-150">現在，您應該可以使用 `HTTPS://` 而非 `HTTP://` 造訪您的應用程式，確認已正確設定憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="357d6-151">步驟 6 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="357d6-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="357d6-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="357d6-152">Azure CLI</span></span>

<span data-ttu-id="357d6-153">[!code-azurecli[主要](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "將自訂 SSL 憑證繫結至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="357d6-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="357d6-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="357d6-154">PowerShell</span></span>

<span data-ttu-id="357d6-155">[!code-powershell[主要](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "將自訂 SSL 憑證繫結至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="357d6-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="357d6-156">進階</span><span class="sxs-lookup"><span data-stu-id="357d6-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="357d6-157">驗證網域擁有權</span><span class="sxs-lookup"><span data-stu-id="357d6-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="357d6-158">App Service 憑證另外支援 2 種類型的網域驗證：郵件和手動驗證。</span><span class="sxs-lookup"><span data-stu-id="357d6-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="357d6-159">郵件驗證</span><span class="sxs-lookup"><span data-stu-id="357d6-159">Mail Verification</span></span>

<span data-ttu-id="357d6-160">驗證電子郵件已傳送到與此自訂網域相關聯的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="357d6-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="357d6-161">若要完成電子郵件驗證步驟，請開啟電子郵件並按一下驗證連結。</span><span class="sxs-lookup"><span data-stu-id="357d6-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![插入電子郵件驗證的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="357d6-163">如果您需要重新傳送驗證電子郵件，按一下 [重新傳送電子郵件] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="357d6-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="357d6-164">手動驗證</span><span class="sxs-lookup"><span data-stu-id="357d6-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="357d6-165">HTML 網頁驗證 (僅適用於標準憑證 SKU)</span><span class="sxs-lookup"><span data-stu-id="357d6-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="357d6-166">建立名為 **"starfield.html"** 的 HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="357d6-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="357d6-167">此檔案的內容應該與網域驗證權杖的名稱完全相同。</span><span class="sxs-lookup"><span data-stu-id="357d6-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="357d6-168">(您可以從 [網域驗證狀態] 刀鋒視窗中複製權杖)</span><span class="sxs-lookup"><span data-stu-id="357d6-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="357d6-169">在主控您網域 `/.well-known/pki-validation/starfield.html` 的 Web 伺服器的根目錄上傳此檔案。</span><span class="sxs-lookup"><span data-stu-id="357d6-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="357d6-170">按一下 [重新整理]，在完成驗證之後更新憑證狀態。</span><span class="sxs-lookup"><span data-stu-id="357d6-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="357d6-171">驗證可能需要數分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="357d6-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="357d6-172">在終端機中使用 `curl -G http://<domain>/.well-known/pki-validation/starfield.html` 驗證回應應包含 `<verification-token>`。</span><span class="sxs-lookup"><span data-stu-id="357d6-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="357d6-173">DNS TXT 記錄驗證</span><span class="sxs-lookup"><span data-stu-id="357d6-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="357d6-174">使用 DNS 管理員，在具有與網域驗證權杖相同值的 `@` 子網域上建立 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="357d6-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="357d6-175">按一下 [重新整理]，在完成驗證之後更新憑證狀態。</span><span class="sxs-lookup"><span data-stu-id="357d6-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="357d6-176">您必須在值為 `<verification-token>` 的 `@.<domain>` 上建立 TXT 記錄。</span><span class="sxs-lookup"><span data-stu-id="357d6-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="357d6-177">將憑證指派給 App Service 應用程式</span><span class="sxs-lookup"><span data-stu-id="357d6-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="357d6-178">如果您已選取 [ **IP SSL** ]，而且您的自訂網域是以 A 記錄設定，則必須執行下列額外步驟：</span><span class="sxs-lookup"><span data-stu-id="357d6-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="357d6-179">設定 IP SSL 繫結之後，您的應用程式將會獲派專用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="357d6-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="357d6-180">您可以在應用程式設定下的 [自訂網域] 頁面上找到此 IP 位址，正好位於 [主機名稱] 區段上面。</span><span class="sxs-lookup"><span data-stu-id="357d6-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="357d6-181">它會列為 [外部 IP 位址]</span><span class="sxs-lookup"><span data-stu-id="357d6-181">It is listed as **External IP Address**</span></span>

![插入 IP SSL 的影像](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="357d6-183">請注意，此 IP 位址與先前用來設定網域 A 記錄的虛擬 IP 位址不同。</span><span class="sxs-lookup"><span data-stu-id="357d6-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="357d6-184">如果您設定成使用以 SNI 為基礎的 SSL，或未設定成使用 SSL，則不會列出此項目的位址。</span><span class="sxs-lookup"><span data-stu-id="357d6-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="357d6-185">使用網域名稱註冊機構所提供的工具，修改自訂網域名稱的 A 記錄，使其指向上一個步驟的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="357d6-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="357d6-186">重設金鑰和同步處理憑證</span><span class="sxs-lookup"><span data-stu-id="357d6-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="357d6-187">如果您需要重設憑證金鑰，請選取 [憑證屬性] 刀鋒視窗中的 [重設金鑰和同步處理] 選項。</span><span class="sxs-lookup"><span data-stu-id="357d6-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="357d6-188">按一下 [重設金鑰] 按鈕來啟動處理程序。</span><span class="sxs-lookup"><span data-stu-id="357d6-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="357d6-189">此程序需要 1 - 10 分鐘才能完成。</span><span class="sxs-lookup"><span data-stu-id="357d6-189">This process can take 1-10 minutes to complete.</span></span>

![插入重設 SSL 金鑰的影像](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="357d6-191">重設憑證的金鑰，會以憑證授權單位發行的新憑證變更憑證。</span><span class="sxs-lookup"><span data-stu-id="357d6-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="357d6-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="357d6-192">Next Steps</span></span>

* [<span data-ttu-id="357d6-193">新增內容傳遞網路</span><span class="sxs-lookup"><span data-stu-id="357d6-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)