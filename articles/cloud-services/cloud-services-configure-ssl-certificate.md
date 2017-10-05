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
# <a name="configuring-ssl-for-an-application-in-azure"></a>在 Azure 設定應用程式的 SSL
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-configure-ssl-certificate-portal.md)
> * [Azure 傳統入口網站](cloud-services-configure-ssl-certificate.md)
> 
> 

安全通訊端層 (SSL) 加密是最常用來保護在網際網路上傳送之資料的方法。 此常見工作會討論如何為 Web 角色指定 HTTPS 端點，以及如何上傳 SSL 憑證來保護應用程式的安全。

> [!NOTE]
> 此工作的程序適用於 Azure 雲端服務，若為應用程式服務，請參閱[這篇](../app-service-web/web-sites-configure-ssl-certificate.md)文章。
> 
> 

此工作使用生產部署。 本主題最後將提供關於如何使用預備部署的資訊。

如果尚未建立雲端服務，請先閱讀[這篇](cloud-services-how-to-create-deploy.md)文章。

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>步驟 1：取得 SSL 憑證
若要設定應用程式的 SSL，首先您需要取得已由憑證授權單位 (CA) (專門核發憑證的受信任第三方) 簽署的 SSL 憑證。 如果您還沒有此類憑證，則必須向銷售 SSL 憑證的公司取得。

憑證必須符合 Azure 中對於 SSL 憑證的下列要求：

* 憑證必須包含私密金鑰。
* 憑證必須是為了進行金鑰交換而建立，且可匯出成個人資訊交換檔 (.pfx)。
* 憑證的主體名稱必須符合用來存取雲端服務的網域。 您無法向憑證授權單位 (CA) 取得 cloudapp.net 網域的 SSL 憑證。 您必須取得要在存取您的服務時使用的自訂網域名稱。 當您向 CA 要求憑證時，憑證的主體名稱必須符合用來存取應用程式的自訂網域名稱。 例如，如果您的自訂網域名稱為 **contoso.com**，則您需向 CA 要求 ***.contoso.com** 或 **www.contoso.com** 憑證。
* 憑證至少必須以 2048 位元加密。

基於測試目的，您可以 [建立](cloud-services-certs-create.md) 並使用自我簽署憑證。 自我簽署憑證不是由 CA 驗證，因此可以使用 cloudapp.net 網域做為網站 URL。 例如，以下工作即使用自我簽署憑證，該憑證中使用的一般名稱 (CN) 為 **sslexample.cloudapp.net**。

接下來，您必須在服務定義檔與服務組態檔中加入憑證的相關資訊。

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a>步驟 2：修改服務定義檔和組態檔
您的應用程式必須已設定為使用憑證，而且您必須新增 HTTPS 端點。 因此，您需要更新服務定義檔與服務組態檔。

1. 在開發環境中，開啟服務定義檔 (CSDEF)、在 [WebRole] 區段內新增 [Certificates] 區段，並新增下列憑證 (及中繼憑證) 相關資訊：
   
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
   
   **Certificates** 區段定義憑證的名稱、位置，以及其所在的存放區名稱。
   
   權限 (`permisionLevel` 屬性) 可設為下列其中一個值：
   
   | 權限值 | 說明 |
   | --- | --- |
   | limitedOrElevated |**(預設值)** 所有角色處理序都可以存取私密金鑰。 |
   | elevated |只有較高權限的處理序可以存取私密金鑰。 |
2. 在服務定義檔中，於 **Endpoints** 區段內新增 **InputEndpoint** 元素，以啟用 HTTPS：
   
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

3. 在服務定義檔中，於 **Sites** 區段內新增 **Binding** 元素。 此區段會新增 HTTPS 繫結，以將端點對應至您的站台：
   
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
   
   如此即已對服務定義檔完成所有必要變更，但是您仍然需要將憑證資訊新增至服務組態檔。
4. 在服務組態檔 (CSCFG) (ServiceConfiguration.Cloud.cscfg) 中，於 **Role** 區段內新增 **Certificates** 區段，以將下面顯示的範例指紋值取代為憑證的指紋值：
   
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

(上述範例針對指紋演算法的部分使用 **sha1**。 請指定適當的值作為憑證的指紋演算法。)

您已更新服務定義檔與服務組態檔，現在請封裝您的部署，以上傳至 Azure。 如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。

## <a name="step-3-upload-a-certificate"></a>步驟 3：上傳憑證
您的部署套件已更新為使用該憑證，而且您已新增 HTTPS 端點。 現在您可以利用 Azure 傳統入口網站將套件和憑證上傳至 Azure。

1. 登入 [Azure 傳統入口網站][Azure classic portal]。 
2. 按一下左邊瀏覽窗格的 [雲端服務]。
3. 按一下所需的雲端服務。
4. 按一下 [憑證] 索引標籤。
   
    ![按一下 [憑證] 索引標籤](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. 按一下 [上傳]  按鈕。
   
    ![上傳](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. 提供 **[檔案]** 、**[密碼]** ，然後按一下 **[完成]**  \(核取記號)。

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a>步驟 4：使用 HTTPS 來連線至角色執行個體
您的部署已在 Azure 啟動並執行，現在您可以使用 HTTPS 來與其連線。

1. 在 Azure 傳統入口網站中，選取您的部署，然後按一下 [網站 URL] 下的連結。
   
   ![判定網站 URL][2]
2. 在網頁瀏覽器中，將連結修改為使用 **https** 而非 **http**，然後造訪網頁。
   
   > [!NOTE]
   > 如果使用自我簽署憑證，則當您在瀏覽器中瀏覽至與該自我簽署憑證相關聯的 HTTPS 端點時，您會看見憑證錯誤。 使用信任的憑證授權單位所簽署的憑證，則不會有此問題；因此，您可以忽略該錯誤。 (另一個選項為新增自我簽署憑證至使用者的受信任憑證授權單位憑證存放區。)
   > 
   > 
   
   ![SSL 範例網站][3]

若要對預備部署而不是對生產部署使用 SSL，首先您需要判定要在預備部署中使用的 URL。 請將您的雲端服務部署至預備環境，但不包括憑證或任何憑證資訊。 一旦部署好，您就可以判定 GUID 型 URL (這會列在 Azure 傳統入口網站的 [網站 URL] 欄位中)。 建立一般名稱 (CN) 等於 GUID 型 URL (如 **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**) 的憑證。 使用 Azure 傳統入口網站將憑證新增至預備的雲端服務。 接著，將憑證資訊新增至 CSDEF 和 CSCFG 檔案、重新封裝應用程式，然後更新預備的部署以使用新套件。

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure.md)。
* 了解如何 [部署雲端服務](cloud-services-how-to-create-deploy.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* [管理您的雲端服務](cloud-services-how-to-manage.md)。

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
