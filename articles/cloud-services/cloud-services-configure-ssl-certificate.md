---
title: "設定雲端服務的 SSL (傳統) | Microsoft Docs"
description: "了解如何為 Web 角色指定 HTTPS 端點，以及如何上傳 SSL 憑證來保護應用程式的安全。"
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="03841-103">在 Azure 設定應用程式的 SSL</span><span class="sxs-lookup"><span data-stu-id="03841-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03841-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="03841-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="03841-105">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="03841-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="03841-106">安全通訊端層 (SSL) 加密是最常用來保護在網際網路上傳送之資料的方法。</span><span class="sxs-lookup"><span data-stu-id="03841-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="03841-107">此常見工作會討論如何為 Web 角色指定 HTTPS 端點，以及如何上傳 SSL 憑證來保護應用程式的安全。</span><span class="sxs-lookup"><span data-stu-id="03841-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="03841-108">此工作的程序適用於 Azure 雲端服務，若為應用程式服務，請參閱[這篇](../app-service-web/web-sites-configure-ssl-certificate.md)文章。</span><span class="sxs-lookup"><span data-stu-id="03841-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="03841-109">此工作使用生產部署。</span><span class="sxs-lookup"><span data-stu-id="03841-109">This task uses a production deployment.</span></span> <span data-ttu-id="03841-110">本主題最後將提供關於如何使用預備部署的資訊。</span><span class="sxs-lookup"><span data-stu-id="03841-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="03841-111">如果尚未建立雲端服務，請先閱讀[這篇](cloud-services-how-to-create-deploy.md)文章。</span><span class="sxs-lookup"><span data-stu-id="03841-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="03841-112">步驟 1：取得 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="03841-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="03841-113">若要設定應用程式的 SSL，首先您需要取得已由憑證授權單位 (CA) (專門核發憑證的受信任第三方) 簽署的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="03841-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="03841-114">如果您還沒有此類憑證，則必須向銷售 SSL 憑證的公司取得。</span><span class="sxs-lookup"><span data-stu-id="03841-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="03841-115">憑證必須符合 Azure 中對於 SSL 憑證的下列要求：</span><span class="sxs-lookup"><span data-stu-id="03841-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="03841-116">憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="03841-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="03841-117">憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換檔 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="03841-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="03841-118">憑證的主體名稱必須符合用來存取雲端服務的網域。</span><span class="sxs-lookup"><span data-stu-id="03841-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="03841-119">您無法向憑證授權單位 (CA) 取得 cloudapp.net 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="03841-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="03841-120">您必須取得要在存取您的服務時使用的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="03841-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="03841-121">當您向 CA 要求憑證時，憑證的主體名稱必須符合用來存取應用程式的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="03841-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="03841-122">例如，如果您的自訂網域名稱為 **contoso.com**，則您需向 CA 要求 ***.contoso.com** 或 **www.contoso.com** 憑證。</span><span class="sxs-lookup"><span data-stu-id="03841-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="03841-123">憑證至少必須以 2048 位元加密。</span><span class="sxs-lookup"><span data-stu-id="03841-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="03841-124">基於測試目的，您可以 [建立](cloud-services-certs-create.md) 並使用自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="03841-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="03841-125">自我簽署憑證不是由 CA 驗證，因此可以使用 cloudapp.net 網域做為網站 URL。</span><span class="sxs-lookup"><span data-stu-id="03841-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="03841-126">例如，以下工作即使用自我簽署憑證，該憑證中使用的一般名稱 (CN) 為 **sslexample.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="03841-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="03841-127">接下來，您必須在服務定義檔與服務組態檔中加入憑證的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="03841-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="03841-128">步驟 2：修改服務定義檔和組態檔</span><span class="sxs-lookup"><span data-stu-id="03841-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="03841-129">您的應用程式必須已設定為使用憑證，而且您必須新增 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="03841-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="03841-130">因此，您需要更新服務定義檔與服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="03841-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="03841-131">在開發環境中，開啟服務定義檔 (CSDEF)、在 [WebRole] 區段內新增 [Certificates] 區段，並新增下列憑證 (及中繼憑證) 相關資訊：</span><span class="sxs-lookup"><span data-stu-id="03841-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="03841-132">**Certificates** 區段定義憑證的名稱、位置，以及其所在的存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="03841-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="03841-133">權限 (`permisionLevel` 屬性) 可設為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="03841-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="03841-134">權限值</span><span class="sxs-lookup"><span data-stu-id="03841-134">Permission Value</span></span> | <span data-ttu-id="03841-135">說明</span><span class="sxs-lookup"><span data-stu-id="03841-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="03841-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="03841-136">limitedOrElevated</span></span> |<span data-ttu-id="03841-137">**(預設值)** 所有角色處理序都可以存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="03841-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="03841-138">elevated</span><span class="sxs-lookup"><span data-stu-id="03841-138">elevated</span></span> |<span data-ttu-id="03841-139">只有較高權限的處理序可以存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="03841-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="03841-140">在服務定義檔中，於 **Endpoints** 區段內新增 **InputEndpoint** 元素，以啟用 HTTPS：</span><span class="sxs-lookup"><span data-stu-id="03841-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="03841-141">在服務定義檔中，於 **Sites** 區段內新增 **Binding** 元素。</span><span class="sxs-lookup"><span data-stu-id="03841-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="03841-142">此區段會新增 HTTPS 繫結，以將端點對應至您的站台：</span><span class="sxs-lookup"><span data-stu-id="03841-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="03841-143">如此即已對服務定義檔完成所有必要變更，但是您仍然需要將憑證資訊新增至服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="03841-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="03841-144">在服務組態檔 (CSCFG) (ServiceConfiguration.Cloud.cscfg) 中，於 **Role** 區段內新增 **Certificates** 區段，以將下面顯示的範例指紋值取代為憑證的指紋值：</span><span class="sxs-lookup"><span data-stu-id="03841-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="03841-145">(上述範例針對指紋演算法的部分使用 **sha1**。</span><span class="sxs-lookup"><span data-stu-id="03841-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="03841-146">請指定適當的值作為憑證的指紋演算法。)</span><span class="sxs-lookup"><span data-stu-id="03841-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="03841-147">您已更新服務定義檔與服務組態檔，現在請封裝您的部署，以上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="03841-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="03841-148">如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="03841-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="03841-149">步驟 3：上傳憑證</span><span class="sxs-lookup"><span data-stu-id="03841-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="03841-150">您的部署套件已更新為使用該憑證，而且您已新增 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="03841-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="03841-151">現在您可以利用 Azure 傳統入口網站將套件和憑證上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="03841-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="03841-152">登入 [Azure 傳統入口網站][Azure classic portal]。</span><span class="sxs-lookup"><span data-stu-id="03841-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="03841-153">按一下左邊瀏覽窗格的 [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="03841-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="03841-154">按一下所需的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="03841-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="03841-155">按一下 [憑證] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="03841-155">Click the **Certificates** tab.</span></span>
   
    ![按一下 [憑證] 索引標籤](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="03841-157">按一下 [上傳]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="03841-157">Click the **Upload** button.</span></span>
   
    ![上傳](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="03841-159">提供 **[檔案]** 、**[密碼]** ，然後按一下 **[完成]**  \(核取記號)。</span><span class="sxs-lookup"><span data-stu-id="03841-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="03841-160">步驟 4：使用 HTTPS 來連線至角色執行個體</span><span class="sxs-lookup"><span data-stu-id="03841-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="03841-161">您的部署已在 Azure 啟動並執行，現在您可以使用 HTTPS 來與其連線。</span><span class="sxs-lookup"><span data-stu-id="03841-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="03841-162">在 Azure 傳統入口網站中，選取您的部署，然後按一下 [網站 URL] 下的連結。</span><span class="sxs-lookup"><span data-stu-id="03841-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![判定網站 URL][2]
2. <span data-ttu-id="03841-164">在網頁瀏覽器中，將連結修改為使用 **https** 而非 **http**，然後造訪網頁。</span><span class="sxs-lookup"><span data-stu-id="03841-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="03841-165">如果使用自我簽署憑證，則當您在瀏覽器中瀏覽至與該自我簽署憑證相關聯的 HTTPS 端點時，您會看見憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="03841-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="03841-166">使用信任的憑證授權單位所簽署的憑證，則不會有此問題；因此，您可以忽略該錯誤。</span><span class="sxs-lookup"><span data-stu-id="03841-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="03841-167">(另一個選項為新增自我簽署憑證至使用者的受信任憑證授權單位憑證存放區。)</span><span class="sxs-lookup"><span data-stu-id="03841-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![SSL 範例網站][3]

<span data-ttu-id="03841-169">若要對預備部署而不是對生產部署使用 SSL，首先您需要判定要在預備部署中使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="03841-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="03841-170">請將您的雲端服務部署至預備環境，但不包括憑證或任何憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="03841-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="03841-171">一旦部署好，您就可以判定 GUID 型 URL (這會列在 Azure 傳統入口網站的 [網站 URL] 欄位中)。</span><span class="sxs-lookup"><span data-stu-id="03841-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="03841-172">建立一般名稱 (CN) 等於 GUID 型 URL (如 **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**) 的憑證。</span><span class="sxs-lookup"><span data-stu-id="03841-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="03841-173">使用 Azure 傳統入口網站將憑證新增至預備的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="03841-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="03841-174">接著，將憑證資訊新增至 CSDEF 和 CSCFG 檔案、重新封裝應用程式，然後更新預備的部署以使用新套件。</span><span class="sxs-lookup"><span data-stu-id="03841-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03841-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="03841-175">Next steps</span></span>
* <span data-ttu-id="03841-176">[雲端服務的一般設定](cloud-services-how-to-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="03841-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="03841-177">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="03841-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="03841-178">設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。</span><span class="sxs-lookup"><span data-stu-id="03841-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="03841-179">[管理您的雲端服務](cloud-services-how-to-manage.md)。</span><span class="sxs-lookup"><span data-stu-id="03841-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
