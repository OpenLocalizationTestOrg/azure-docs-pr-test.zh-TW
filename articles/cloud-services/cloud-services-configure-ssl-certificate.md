---
title: "雲端服務 （傳統） aaaConfigure SSL |Microsoft 文件"
description: "深入了解如何 toospecify HTTPS 端點，web 角色和如何 tooupload SSL 的憑證 toosecure 您的應用程式。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="bcdca-103">在 Azure 設定應用程式的 SSL</span><span class="sxs-lookup"><span data-stu-id="bcdca-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bcdca-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bcdca-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="bcdca-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="bcdca-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="bcdca-106">安全通訊端層 (SSL) 加密是最常用的 hello 方法保護資料傳送嗨跨網際網路。</span><span class="sxs-lookup"><span data-stu-id="bcdca-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="bcdca-107">一般工作的討論如何 toospecify HTTPS 端點，web 角色和如何 tooupload SSL 的憑證 toosecure 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bcdca-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="bcdca-108">在這項工作的 hello 程序適用於 tooAzure 雲端服務。應用程式服務，請參閱[這](../app-service-web/web-sites-configure-ssl-certificate.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="bcdca-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="bcdca-109">此工作使用生產部署。</span><span class="sxs-lookup"><span data-stu-id="bcdca-109">This task uses a production deployment.</span></span> <span data-ttu-id="bcdca-110">Hello 本主題的結尾會提供有關使用預備環境部署。</span><span class="sxs-lookup"><span data-stu-id="bcdca-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="bcdca-111">如果尚未建立雲端服務，請先閱讀[這篇](cloud-services-how-to-create-deploy.md)文章。</span><span class="sxs-lookup"><span data-stu-id="bcdca-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="bcdca-112">步驟 1：取得 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="bcdca-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="bcdca-113">tooconfigure SSL 應用程式，您必須先 tooget 已簽署的憑證授權單位 (CA)，受信任的協力廠商簽發憑證，針對此用途的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="bcdca-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="bcdca-114">如果您還沒有其中一個，您會需要公司銷售的 SSL 憑證的其中一個 tooobtain。</span><span class="sxs-lookup"><span data-stu-id="bcdca-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="bcdca-115">hello 憑證必須符合下列需求的 SSL 憑證在 Azure 中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bcdca-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="bcdca-116">hello 憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcdca-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="bcdca-117">金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。</span><span class="sxs-lookup"><span data-stu-id="bcdca-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="bcdca-118">hello 憑證的主體名稱必須符合 hello 用網域 tooaccess hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bcdca-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="bcdca-119">您無法從 hello cloudapp.net 網域的憑證授權單位 (CA) 取得 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="bcdca-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="bcdca-120">您必須取得的自訂網域名稱 toouse 時存取您的服務。</span><span class="sxs-lookup"><span data-stu-id="bcdca-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="bcdca-121">當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱使用 tooaccess 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="bcdca-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="bcdca-122">例如，如果您的自訂網域名稱為 **contoso.com**，則您需向 CA 要求 ***.contoso.com** 或 **www.contoso.com** 憑證。</span><span class="sxs-lookup"><span data-stu-id="bcdca-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="bcdca-123">hello 憑證必須使用至少 2048年位元加密。</span><span class="sxs-lookup"><span data-stu-id="bcdca-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="bcdca-124">基於測試目的，您可以 [建立](cloud-services-certs-create.md) 並使用自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="bcdca-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="bcdca-125">自我簽署的憑證不會透過 CA 進行驗證，可使用和 hello cloudapp.net 網域 hello 網站 URL。</span><span class="sxs-lookup"><span data-stu-id="bcdca-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="bcdca-126">例如，hello 下列工作會使用自我簽署的憑證中的 hello hello 憑證中所使用的一般名稱 (CN) 是**sslexample.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="bcdca-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="bcdca-127">接下來，您必須在服務定義和服務組態檔中包含 hello 憑證的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="bcdca-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="bcdca-128">步驟 2： 修改 hello 服務定義檔和組態檔</span><span class="sxs-lookup"><span data-stu-id="bcdca-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="bcdca-129">您的應用程式必須設定的 toouse hello 憑證，而且必須加入 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="bcdca-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="bcdca-130">如此一來，hello 服務定義和服務組態檔必須更新 toobe。</span><span class="sxs-lookup"><span data-stu-id="bcdca-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="bcdca-131">在開發環境中，開啟 hello 服務定義檔 (CSDEF)，新增**憑證**區段內 hello **WebRole**區段，並包含下列資訊的 hello憑證 （和中繼憑證）：</span><span class="sxs-lookup"><span data-stu-id="bcdca-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="bcdca-132">hello**憑證**區段會定義 hello 我們憑證、 位置和 hello 名稱所在的 hello 存放區的名稱。</span><span class="sxs-lookup"><span data-stu-id="bcdca-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="bcdca-133">權限 (`permisionLevel`屬性) 可以是集合 tooone hello 的下列值：</span><span class="sxs-lookup"><span data-stu-id="bcdca-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="bcdca-134">權限值</span><span class="sxs-lookup"><span data-stu-id="bcdca-134">Permission Value</span></span> | <span data-ttu-id="bcdca-135">說明</span><span class="sxs-lookup"><span data-stu-id="bcdca-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="bcdca-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="bcdca-136">limitedOrElevated</span></span> |<span data-ttu-id="bcdca-137">**（預設值）**所有角色處理序可以都存取 hello 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcdca-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="bcdca-138">elevated</span><span class="sxs-lookup"><span data-stu-id="bcdca-138">elevated</span></span> |<span data-ttu-id="bcdca-139">只有在提升權限處理序可以存取 hello 私用金鑰。</span><span class="sxs-lookup"><span data-stu-id="bcdca-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="bcdca-140">在您的服務定義檔中加入**InputEndpoint** hello 內的項目**端點**區段 tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="bcdca-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443" 
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="bcdca-141">在您的服務定義檔中加入**繫結**hello 內的項目**網站**> 一節。</span><span class="sxs-lookup"><span data-stu-id="bcdca-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="bcdca-142">本節會加入 HTTPS 繫結 toomap 端點 tooyour 網站：</span><span class="sxs-lookup"><span data-stu-id="bcdca-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
    ```xml   
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="bcdca-143">已完成所有 hello 必要的變更 toohello 服務定義檔，但您仍然需要 tooadd hello 憑證資訊與 hello 服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="bcdca-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="bcdca-144">在服務組態檔 (CSCFG) 中，ServiceConfiguration.Cloud.cscfg 中加入**憑證**區段內 hello**角色**區段中，取代 hello 範例指紋值如下所示您的憑證：</span><span class="sxs-lookup"><span data-stu-id="bcdca-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
    ```xml   
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff" 
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc" 
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="bcdca-145">(上述範例會使用 hello **sha1** hello 指紋演算法。</span><span class="sxs-lookup"><span data-stu-id="bcdca-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="bcdca-146">指定您的憑證指紋演算法的 hello 適當值。）</span><span class="sxs-lookup"><span data-stu-id="bcdca-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="bcdca-147">既然已經更新 hello 服務定義檔和服務組態檔，封裝上傳 tooAzure 部署。</span><span class="sxs-lookup"><span data-stu-id="bcdca-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="bcdca-148">如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="bcdca-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="bcdca-149">步驟 3：上傳憑證</span><span class="sxs-lookup"><span data-stu-id="bcdca-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="bcdca-150">您的部署套件更新的 toouse hello 憑證，同時也已經加入 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="bcdca-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="bcdca-151">現在您可以上傳 hello 封裝和憑證 tooAzure 以 hello Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="bcdca-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="bcdca-152">登入 toohello [Azure 傳統入口網站][Azure classic portal]。</span><span class="sxs-lookup"><span data-stu-id="bcdca-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="bcdca-153">按一下**雲端服務**hello 左側導覽窗格中。</span><span class="sxs-lookup"><span data-stu-id="bcdca-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="bcdca-154">按一下想要的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bcdca-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="bcdca-155">按一下 hello**憑證** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bcdca-155">Click hello **Certificates** tab.</span></span>
   
    ![按一下 hello 憑證 索引標籤](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="bcdca-157">按一下 hello**上傳** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bcdca-157">Click hello **Upload** button.</span></span>
   
    ![上傳](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="bcdca-159">提供 hello**檔案**，**密碼**，然後按一下 **完成**(hello 核取記號)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="bcdca-160">步驟 4： 透過 HTTPS 連線 toohello 角色執行個體</span><span class="sxs-lookup"><span data-stu-id="bcdca-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="bcdca-161">您的部署會在 Azure 中已啟動並執行，您可以連線 tooit 使用 HTTPS。</span><span class="sxs-lookup"><span data-stu-id="bcdca-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="bcdca-162">在 hello Azure 傳統入口網站，選取您的部署，然後按一下 [hello] 下方的連結**網站 URL**。</span><span class="sxs-lookup"><span data-stu-id="bcdca-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![判定網站 URL][2]
2. <span data-ttu-id="bcdca-164">在網頁瀏覽器，修改 hello 連結 toouse **https**而不是**http**，，然後瀏覽 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="bcdca-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bcdca-165">如果您使用自我簽署的憑證，當您瀏覽 tooan HTTPS 端點，您可能會看到憑證錯誤 hello 瀏覽器中的 hello 自我簽署憑證與相關聯。</span><span class="sxs-lookup"><span data-stu-id="bcdca-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="bcdca-166">使用受信任的憑證授權單位所簽署的憑證來排除這個問題;hello 同時，您可以略過 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcdca-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="bcdca-167">（另一個選項是 tooadd hello 自我簽署的憑證 toohello 使用者的受信任的憑證授權單位憑證存放區）。</span><span class="sxs-lookup"><span data-stu-id="bcdca-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL 範例網站][3]

<span data-ttu-id="bcdca-169">如果您想 toouse SSL，而不是生產環境部署的預備環境部署，您必須先使用預備環境部署的 hello toodetermine hello URL。</span><span class="sxs-lookup"><span data-stu-id="bcdca-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="bcdca-170">部署雲端服務 toohello 預備環境，而不包括憑證或憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="bcdca-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="bcdca-171">一旦部署之後，您可以判斷 hello GUID 為基礎的 URL，列出的 hello Azure 傳統入口網站的**網站 URL**欄位。</span><span class="sxs-lookup"><span data-stu-id="bcdca-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="bcdca-172">建立憑證與 hello 一般名稱 (CN) 等於 toohello GUID 為基礎的 URL (例如， **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="bcdca-173">使用 hello Azure 傳統入口網站 tooadd hello 憑證 tooyour 分段雲端服務。</span><span class="sxs-lookup"><span data-stu-id="bcdca-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="bcdca-174">然後，將 hello 憑證資訊 tooyour CSDEF 和 CSCFG 檔案、 重新封裝您的應用程式，並更新您預備的部署 toouse hello 新封裝。</span><span class="sxs-lookup"><span data-stu-id="bcdca-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcdca-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcdca-175">Next steps</span></span>
* <span data-ttu-id="bcdca-176">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="bcdca-177">了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="bcdca-178">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="bcdca-179">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="bcdca-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
