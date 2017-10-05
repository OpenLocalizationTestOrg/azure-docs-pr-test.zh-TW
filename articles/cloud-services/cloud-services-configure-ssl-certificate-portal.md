---
title: "設定雲端服務的 SSL | Microsoft Docs"
description: "了解如何為 Web 角色指定 HTTPS 端點，以及如何上傳 SSL 憑證來保護應用程式的安全。 這些範例使用 Azure 入口網站。"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="ff0c6-104">在 Azure 設定應用程式的 SSL</span><span class="sxs-lookup"><span data-stu-id="ff0c6-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff0c6-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ff0c6-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="ff0c6-106">Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="ff0c6-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="ff0c6-107">安全通訊端層 (SSL) 加密是最常用來保護在網際網路上傳送之資料的方法。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="ff0c6-108">此常見工作會討論如何為 Web 角色指定 HTTPS 端點，以及如何上傳 SSL 憑證來保護應用程式的安全。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="ff0c6-109">此工作的程序適用於 Azure 雲端服務，若為應用程式服務，請參閱 [此處](../app-service-web/web-sites-configure-ssl-certificate.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="ff0c6-110">此工作使用生產部署。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-110">This task uses a production deployment.</span></span> <span data-ttu-id="ff0c6-111">本主題最後將提供關於如何使用預備部署的資訊。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="ff0c6-112">如果尚未建立雲端服務，請先閱讀 [這裡](cloud-services-how-to-create-deploy-portal.md) 。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="ff0c6-113">步驟 1：取得 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="ff0c6-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="ff0c6-114">若要設定應用程式的 SSL，首先您需要取得已由憑證授權單位 (CA) (專門核發憑證的受信任第三方) 簽署的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="ff0c6-115">如果您還沒有此類憑證，則必須向銷售 SSL 憑證的公司取得。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="ff0c6-116">憑證必須符合 Azure 中對於 SSL 憑證的下列要求：</span><span class="sxs-lookup"><span data-stu-id="ff0c6-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="ff0c6-117">憑證必須包含私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="ff0c6-118">憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換檔 (.pfx)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="ff0c6-119">憑證的主體名稱必須符合用來存取雲端服務的網域。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="ff0c6-120">您無法向憑證授權單位 (CA) 取得 cloudapp.net 網域的 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="ff0c6-121">您必須取得要在存取您的服務時使用的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="ff0c6-122">當您向 CA 要求憑證時，憑證的主體名稱必須符合用來存取應用程式的自訂網域名稱。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="ff0c6-123">例如，如果您的自訂網域名稱為 **contoso.com**，則您需向 CA 要求 ***.contoso.com** 或 **www.contoso.com** 憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="ff0c6-124">憑證至少必須以 2048 位元加密。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="ff0c6-125">基於測試目的，您可以 [建立](cloud-services-certs-create.md) 並使用自我簽署憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="ff0c6-126">自我簽署憑證不是由 CA 驗證，因此可以使用 cloudapp.net 網域做為網站 URL。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="ff0c6-127">例如，以下工作即使用自我簽署憑證，該憑證中使用的一般名稱 (CN) 為 **sslexample.cloudapp.net**。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="ff0c6-128">接下來，您必須在服務定義檔與服務組態檔中加入憑證的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="ff0c6-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="ff0c6-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="ff0c6-130">步驟 2：修改服務定義檔和組態檔</span><span class="sxs-lookup"><span data-stu-id="ff0c6-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="ff0c6-131">您的應用程式必須已設定為使用憑證，而且您必須新增 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="ff0c6-132">因此，您需要更新服務定義檔與服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="ff0c6-133">在開發環境中，開啟服務定義檔 (CSDEF)、在 [WebRole] 區段內新增 [Certificates] 區段，並新增下列憑證 (及中繼憑證) 相關資訊：</span><span class="sxs-lookup"><span data-stu-id="ff0c6-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="ff0c6-134">**Certificates** 區段定義憑證的名稱、位置，以及其所在的存放區名稱。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="ff0c6-135">權限 (`permisionLevel` 屬性) 可設為下列其中一個值：</span><span class="sxs-lookup"><span data-stu-id="ff0c6-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="ff0c6-136">權限值</span><span class="sxs-lookup"><span data-stu-id="ff0c6-136">Permission Value</span></span> | <span data-ttu-id="ff0c6-137">說明</span><span class="sxs-lookup"><span data-stu-id="ff0c6-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="ff0c6-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="ff0c6-138">limitedOrElevated</span></span> |<span data-ttu-id="ff0c6-139">**(預設值)** 所有角色處理序都可以存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="ff0c6-140">elevated</span><span class="sxs-lookup"><span data-stu-id="ff0c6-140">elevated</span></span> |<span data-ttu-id="ff0c6-141">只有較高權限的處理序可以存取私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="ff0c6-142">在服務定義檔中，於 **Endpoints** 區段內新增 **InputEndpoint** 元素，以啟用 HTTPS：</span><span class="sxs-lookup"><span data-stu-id="ff0c6-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="ff0c6-143">在服務定義檔中，於 **Sites** 區段內新增 **Binding** 元素。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="ff0c6-144">此項目會新增 HTTPS 繫結，以將端點對應至您的站台：</span><span class="sxs-lookup"><span data-stu-id="ff0c6-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="ff0c6-145">如此即已對服務定義檔完成所有必要變更，但是您仍然需要將憑證資訊新增至服務組態檔。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="ff0c6-146">在服務組態檔 (CSCFG) ServiceConfiguration.Cloud.cscfg 中，新增**憑證**值以取代您的憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="ff0c6-147">下列程式碼範例會提供 [憑證] 區段的詳細資料，指紋值除外。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="ff0c6-148">(本例針對指紋演算法使用 **sha1**。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="ff0c6-149">請指定適當的值作為憑證的指紋演算法。)</span><span class="sxs-lookup"><span data-stu-id="ff0c6-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="ff0c6-150">您已更新服務定義檔與服務組態檔，現在請封裝您的部署，以上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="ff0c6-151">如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="ff0c6-152">步驟 3：上傳憑證</span><span class="sxs-lookup"><span data-stu-id="ff0c6-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="ff0c6-153">連線到 Azure 入口網站並...</span><span class="sxs-lookup"><span data-stu-id="ff0c6-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="ff0c6-154">在入口網站的 [所有資源] 區段中，選取您的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![發佈您的雲端服務](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="ff0c6-156">按一下 [憑證]。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-156">Click **Certificates**.</span></span>

    ![按一下憑證圖示](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="ff0c6-158">按一下憑證區上方的 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-158">Click **Upload** at the top of the certificates area.</span></span>

    ![按一下 [上傳] 功能表項目](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="ff0c6-160">提供 [檔案]、[密碼]，然後按一下資料輸入區底部的 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="ff0c6-161">步驟 4：使用 HTTPS 來連線至角色執行個體</span><span class="sxs-lookup"><span data-stu-id="ff0c6-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="ff0c6-162">您的部署已在 Azure 啟動並執行，現在您可以使用 HTTPS 來與其連線。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="ff0c6-163">按一下 [網站 URL] 開啟網頁瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-163">Click the **Site URL** to open up the web browser.</span></span>

   ![按一下網站 URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="ff0c6-165">在網頁瀏覽器中，將連結修改為使用 **https** 而非 **http**，然後造訪網頁。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ff0c6-166">如果使用自我簽署憑證，則當您在瀏覽器中瀏覽至與該自我簽署憑證相關聯的 HTTPS 端點時，您會看見憑證錯誤。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="ff0c6-167">使用信任的憑證授權單位所簽署的憑證，則不會有此問題；因此，您可以忽略該錯誤。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="ff0c6-168">(另一個選項為新增自我簽署憑證至使用者的受信任憑證授權單位憑證存放區。)</span><span class="sxs-lookup"><span data-stu-id="ff0c6-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![網站預覽](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="ff0c6-170">若要對預備部署而不是對生產部署使用 SSL，首先您需要判定要在預備部署中使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="ff0c6-171">部署雲端服務之後，預備環境的 URL 即由**部署 ID** GUID 決定，格式如下：`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="ff0c6-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="ff0c6-172">建立一般名稱 (CN) 等於 GUID 型 URL (如 **328187776e774ceda8fc57609d404462.cloudapp.net**) 的憑證。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="ff0c6-173">使用入口網站將憑證新增至預備的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="ff0c6-174">接著，將憑證資訊新增至 CSDEF 和 CSCFG 檔案、重新封裝應用程式，然後更新預備的部署以使用新套件。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="ff0c6-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ff0c6-175">Next steps</span></span>
* <span data-ttu-id="ff0c6-176">[雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="ff0c6-177">了解如何 [部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="ff0c6-178">設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="ff0c6-179">[管理您的雲端服務](cloud-services-how-to-manage-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ff0c6-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
