---
title: "aaaAdd SSL 憑證 tooyour Azure App Service 應用程式 |Microsoft 文件"
description: "了解如何 tooadd SSL 憑證 tooyour App Service 應用程式。"
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
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="69cd8-103">購買並設定您的 Azure App Service 的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="69cd8-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="69cd8-104">在本教學課程中，您會購買 **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)** 的 SSL 憑證，安全地將它儲存在 [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 中，並將它與自訂網域產生關聯，藉此保護 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="69cd8-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="69cd8-105">步驟 1-tooAzure 中的記錄檔</span><span class="sxs-lookup"><span data-stu-id="69cd8-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="69cd8-106">登入 toohello http://portal.azure.com 在 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="69cd8-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="69cd8-107">步驟 2 - 訂購 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="69cd8-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="69cd8-108">您可以訂購 SSL 憑證來建立新[應用程式的服務憑證](https://portal.azure.com/#create/Microsoft.SSL)在 hello **Azure 入口網站**。</span><span class="sxs-lookup"><span data-stu-id="69cd8-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![建立憑證](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="69cd8-110">輸入好記**名稱**SSL 憑證，然後輸入 hello**網域名稱**</span><span class="sxs-lookup"><span data-stu-id="69cd8-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-111">這是一個 hello hello 採購程序的最重要的部分。</span><span class="sxs-lookup"><span data-stu-id="69cd8-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="69cd8-112">請確定 tooenter 更正您想要與此憑證 tooprotect 的主機名稱 （自訂的網域）。</span><span class="sxs-lookup"><span data-stu-id="69cd8-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="69cd8-113">**不這麼做**附加 hello 與 WWW 的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="69cd8-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="69cd8-114">選取 [訂用帳戶]、[資源群組] 和 [憑證 SKU]。</span><span class="sxs-lookup"><span data-stu-id="69cd8-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="69cd8-115">App Service 憑證只可供其他應用程式內的服務 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="69cd8-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="69cd8-116">步驟 3-hello 憑證儲存在 Azure 金鑰保存庫</span><span class="sxs-lookup"><span data-stu-id="69cd8-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) 是一項 Azure 服務，可協助保護雲端應用程式和服務所使用的密碼編譯金鑰和祕密。</span><span class="sxs-lookup"><span data-stu-id="69cd8-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="69cd8-118">Hello SSL 憑證購買完成之後，您需要 tooopen [App Service 憑證](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders)資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="69cd8-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![插入 KV toostore 準備的映像](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="69cd8-120">您會注意到憑證的狀態是**「 暫止發行"**還有幾個步驟之前，您可以開始使用此憑證需要 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="69cd8-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="69cd8-121">按一下**憑證設定**內部憑證屬性刀鋒視窗，然後按一下 **步驟 1： 儲存區**toostore Azure 金鑰保存庫中的這個憑證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="69cd8-122">從**金鑰保存庫狀態**刀鋒視窗中，按一下 **金鑰保存庫儲存機制**toochoose 現有的金鑰保存庫 toostore 此憑證**或建立新金鑰保存庫**toocreate 新的金鑰保存庫在相同的訂用帳戶和資源群組內。</span><span class="sxs-lookup"><span data-stu-id="69cd8-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-123">Azure Key Vault 儲存此憑證會產生少許費用。</span><span class="sxs-lookup"><span data-stu-id="69cd8-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="69cd8-124">如需詳細資訊，請參閱 **[Azure Key Vault 定價詳細資料](https://azure.microsoft.com/pricing/details/key-vault/)**。</span><span class="sxs-lookup"><span data-stu-id="69cd8-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="69cd8-125">一旦您選取 hello 金鑰保存庫儲存機制 toostore 此憑證，hello**存放區**選項應該會顯示成功。</span><span class="sxs-lookup"><span data-stu-id="69cd8-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![插入在 KV 中儲存成功的影像](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="69cd8-127">步驟 4-確認 hello 網域擁有權</span><span class="sxs-lookup"><span data-stu-id="69cd8-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-128">App Service 憑證支援 3 種類型的網域驗證：網域、郵件和手動驗證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="69cd8-129">這些說明，請參閱詳細資料請參閱 hello[進階區段](#advanced)。</span><span class="sxs-lookup"><span data-stu-id="69cd8-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="69cd8-130">從 hello 相同**憑證設定**您在步驟 3 中使用刀鋒視窗中，按一下**步驟 2： 確認**。</span><span class="sxs-lookup"><span data-stu-id="69cd8-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="69cd8-131">**網域驗證**這是 hello 最方便的程序**只当**您尚未**[購買 Azure App Service 從您的自訂網域。](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="69cd8-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="69cd8-132">按一下**確認**按鈕 toocomplete 此步驟。</span><span class="sxs-lookup"><span data-stu-id="69cd8-132">Click on **Verify** button toocomplete this step.</span></span>

![插入網域驗證的影像](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="69cd8-134">按一下後**確認**，使用 hello**重新整理**按鈕，直到 hello**確認**選項應該會顯示成功。</span><span class="sxs-lookup"><span data-stu-id="69cd8-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![插入在 KV 中驗證成功的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="69cd8-136">步驟 5： 指定憑證 tooApp 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="69cd8-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-137">在執行本節中的 hello 步驟之前, 您必須有關聯的自訂網域名稱與您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="69cd8-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="69cd8-138">如需詳細資訊，請參閱**[設定 Web 應用程式的自訂網域名稱。](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="69cd8-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="69cd8-139">在 hello  **[Azure 入口網站](https://portal.azure.com/)**，按一下 hello **App Service** hello 左側的 hello 頁面的選項。</span><span class="sxs-lookup"><span data-stu-id="69cd8-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="69cd8-140">按一下 hello 名稱的應用程式 toowhich 想 tooassign 此憑證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="69cd8-141">在 hello**設定**，按一下  **SSL 憑證**。</span><span class="sxs-lookup"><span data-stu-id="69cd8-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="69cd8-142">按一下**匯入應用程式的服務憑證**和選取 hello 您購買的憑證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![插入匯入憑證的影像](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="69cd8-144">在 hello **ssl 繫結**區段按一下**新增繫結**，和使用 SSL，使用 hello 下拉式清單 tooselect hello 網域名稱 toosecure hello 憑證 toouse。</span><span class="sxs-lookup"><span data-stu-id="69cd8-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="69cd8-145">您也可以選取是否 toouse **[伺服器名稱指示 (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** 或 IP 為主的 SSL。</span><span class="sxs-lookup"><span data-stu-id="69cd8-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![插入 SSL 繫結的影像](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="69cd8-147">按一下**新增繫結**toosave hello 變更並啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="69cd8-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="69cd8-148">如果您選取**IP 為主的 SSL**和您的自訂網域已設定使用 A 記錄，您必須執行下列額外步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="69cd8-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="69cd8-149">這些說明，請參閱詳細資料請參閱 hello[進階區段](#Advanced)。</span><span class="sxs-lookup"><span data-stu-id="69cd8-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="69cd8-150">此時，您應該能夠 toovisit 您的應用程式使用`HTTPS://`而不是`HTTP://`hello 憑證的 tooverify 已正確設定。</span><span class="sxs-lookup"><span data-stu-id="69cd8-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="69cd8-151">步驟 6 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="69cd8-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="69cd8-152">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69cd8-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="69cd8-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69cd8-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="69cd8-154">進階</span><span class="sxs-lookup"><span data-stu-id="69cd8-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="69cd8-155">驗證網域擁有權</span><span class="sxs-lookup"><span data-stu-id="69cd8-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="69cd8-156">App Service 憑證另外支援 2 種類型的網域驗證：郵件和手動驗證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="69cd8-157">郵件驗證</span><span class="sxs-lookup"><span data-stu-id="69cd8-157">Mail Verification</span></span>

<span data-ttu-id="69cd8-158">驗證電子郵件已經傳送的 toohello 與此自訂網域的電子郵件地址相關聯。</span><span class="sxs-lookup"><span data-stu-id="69cd8-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="69cd8-159">toocomplete hello 電子郵件驗證步驟中，開啟 hello 電子郵件，然後按一下 hello 驗證連結。</span><span class="sxs-lookup"><span data-stu-id="69cd8-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![插入電子郵件驗證的影像](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="69cd8-161">如果您需要 tooresend hello 驗證電子郵件，請按一下 hello**重新傳送電子郵件** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="69cd8-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="69cd8-162">手動驗證</span><span class="sxs-lookup"><span data-stu-id="69cd8-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69cd8-163">HTML 網頁驗證 (僅適用於標準憑證 SKU)</span><span class="sxs-lookup"><span data-stu-id="69cd8-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="69cd8-164">建立名為 **"starfield.html"** 的 HTML 檔案</span><span class="sxs-lookup"><span data-stu-id="69cd8-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="69cd8-165">內容的這個檔案應該 hello 的 hello 網域驗證語彙基元的確切名稱。</span><span class="sxs-lookup"><span data-stu-id="69cd8-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="69cd8-166">（您可以複製 hello 語彙基元 hello 網域驗證狀態刀鋒視窗）</span><span class="sxs-lookup"><span data-stu-id="69cd8-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="69cd8-167">上傳這個檔案位於 hello hello web 伺服器裝載您的網域根目錄`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="69cd8-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="69cd8-168">按一下**重新整理**tooupdate hello 憑證狀態完成驗證之後。</span><span class="sxs-lookup"><span data-stu-id="69cd8-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="69cd8-169">可能需要幾分鐘，讓驗證 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="69cd8-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="69cd8-170">確認終端機利用`curl -G http://<domain>/.well-known/pki-validation/starfield.html`hello 回應應包含 hello `<verification-token>`。</span><span class="sxs-lookup"><span data-stu-id="69cd8-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="69cd8-171">DNS TXT 記錄驗證</span><span class="sxs-lookup"><span data-stu-id="69cd8-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="69cd8-172">使用 DNS 管理員中，建立 TXT 記錄上 hello`@`子網域與值相等 toohello 網域驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="69cd8-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="69cd8-173">按一下**[重新整理]** tooupdate hello 完成驗證後的憑證狀態。</span><span class="sxs-lookup"><span data-stu-id="69cd8-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="69cd8-174">您需要 toocreate TXT 記錄上`@.<domain>`值`<verification-token>`。</span><span class="sxs-lookup"><span data-stu-id="69cd8-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="69cd8-175">指派憑證 tooApp 服務應用程式</span><span class="sxs-lookup"><span data-stu-id="69cd8-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="69cd8-176">如果您選取**IP 為主的 SSL**和您的自訂網域已設定使用 A 記錄，您必須執行下列額外步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="69cd8-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="69cd8-177">設定之後 IP 為根據的 SSL 繫結，會指派 tooyour 應用程式的專用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="69cd8-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="69cd8-178">您可以找到這個 IP 位址上 hello**自訂網域**頁面的 設定應用程式，上面 hello 下**Hostname** > 一節。</span><span class="sxs-lookup"><span data-stu-id="69cd8-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="69cd8-179">它會列為 [外部 IP 位址]</span><span class="sxs-lookup"><span data-stu-id="69cd8-179">It is listed as **External IP Address**</span></span>

![插入 IP SSL 的影像](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="69cd8-181">請注意，此 IP 位址與 hello 虛擬 IP 位址用於先前 tooconfigure hello A 記錄您的網域不同。</span><span class="sxs-lookup"><span data-stu-id="69cd8-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="69cd8-182">如果您已設定的 toouse SNI 為根據的 SSL，或不設定 toouse SSL，沒有位址會列示為此項目。</span><span class="sxs-lookup"><span data-stu-id="69cd8-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="69cd8-183">使用您網域名稱註冊機構所提供的 hello 工具，來修改 hello 您的自訂網域名稱 toopoint toohello 的 IP 位址從 hello 上一個步驟的記錄。</span><span class="sxs-lookup"><span data-stu-id="69cd8-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="69cd8-184">重設金鑰，並將同步 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="69cd8-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="69cd8-185">如果您需要 tooRekey 您的憑證，選取**重設金鑰，並將同步**選項**憑證內容**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="69cd8-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="69cd8-186">按一下**重設金鑰**按鈕 tooinitiate hello 程序。</span><span class="sxs-lookup"><span data-stu-id="69cd8-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="69cd8-187">此程序可能需要 1-10 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="69cd8-187">This process can take 1-10 minutes toocomplete.</span></span>

![插入重設 SSL 金鑰的影像](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="69cd8-189">重設您的憑證的金鑰復原 hello 與 hello 憑證授權單位發行新憑證的憑證。</span><span class="sxs-lookup"><span data-stu-id="69cd8-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69cd8-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69cd8-190">Next Steps</span></span>

* [<span data-ttu-id="69cd8-191">新增內容傳遞網路</span><span class="sxs-lookup"><span data-stu-id="69cd8-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)