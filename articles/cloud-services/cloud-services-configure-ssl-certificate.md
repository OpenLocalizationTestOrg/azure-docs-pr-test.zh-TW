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
# <a name="configuring-ssl-for-an-application-in-azure"></a>在 Azure 設定應用程式的 SSL
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-configure-ssl-certificate-portal.md)
> * [Azure 傳統入口網站](cloud-services-configure-ssl-certificate.md)
> 
> 

安全通訊端層 (SSL) 加密是最常用的 hello 方法保護資料傳送嗨跨網際網路。 一般工作的討論如何 toospecify HTTPS 端點，web 角色和如何 tooupload SSL 的憑證 toosecure 您的應用程式。

> [!NOTE]
> 在這項工作的 hello 程序適用於 tooAzure 雲端服務。應用程式服務，請參閱[這](../app-service-web/web-sites-configure-ssl-certificate.md)發行項。
> 
> 

此工作使用生產部署。 Hello 本主題的結尾會提供有關使用預備環境部署。

如果尚未建立雲端服務，請先閱讀[這篇](cloud-services-how-to-create-deploy.md)文章。

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>步驟 1：取得 SSL 憑證
tooconfigure SSL 應用程式，您必須先 tooget 已簽署的憑證授權單位 (CA)，受信任的協力廠商簽發憑證，針對此用途的 SSL 憑證。 如果您還沒有其中一個，您會需要公司銷售的 SSL 憑證的其中一個 tooobtain。

hello 憑證必須符合下列需求的 SSL 憑證在 Azure 中的 hello:

* hello 憑證必須包含私密金鑰。
* 金鑰交換，可匯出 tooa 個人資訊交換 (.pfx) 檔案，就必須建立 hello 憑證。
* hello 憑證的主體名稱必須符合 hello 用網域 tooaccess hello 雲端服務。 您無法從 hello cloudapp.net 網域的憑證授權單位 (CA) 取得 SSL 憑證。 您必須取得的自訂網域名稱 toouse 時存取您的服務。 當您從 CA 要求憑證時，hello 憑證的主體名稱必須符合 hello 自訂網域名稱使用 tooaccess 您的應用程式。 例如，如果您的自訂網域名稱為 **contoso.com**，則您需向 CA 要求 ***.contoso.com** 或 **www.contoso.com** 憑證。
* hello 憑證必須使用至少 2048年位元加密。

基於測試目的，您可以 [建立](cloud-services-certs-create.md) 並使用自我簽署憑證。 自我簽署的憑證不會透過 CA 進行驗證，可使用和 hello cloudapp.net 網域 hello 網站 URL。 例如，hello 下列工作會使用自我簽署的憑證中的 hello hello 憑證中所使用的一般名稱 (CN) 是**sslexample.cloudapp.net**。

接下來，您必須在服務定義和服務組態檔中包含 hello 憑證的相關資訊。

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>步驟 2： 修改 hello 服務定義檔和組態檔
您的應用程式必須設定的 toouse hello 憑證，而且必須加入 HTTPS 端點。 如此一來，hello 服務定義和服務組態檔必須更新 toobe。

1. 在開發環境中，開啟 hello 服務定義檔 (CSDEF)，新增**憑證**區段內 hello **WebRole**區段，並包含下列資訊的 hello憑證 （和中繼憑證）：
   
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
   
   hello**憑證**區段會定義 hello 我們憑證、 位置和 hello 名稱所在的 hello 存放區的名稱。
   
   權限 (`permisionLevel`屬性) 可以是集合 tooone hello 的下列值：
   
   | 權限值 | 說明 |
   | --- | --- |
   | limitedOrElevated |**（預設值）**所有角色處理序可以都存取 hello 私用金鑰。 |
   | elevated |只有在提升權限處理序可以存取 hello 私用金鑰。 |
2. 在您的服務定義檔中加入**InputEndpoint** hello 內的項目**端點**區段 tooenable HTTPS:
   
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

3. 在您的服務定義檔中加入**繫結**hello 內的項目**網站**> 一節。 本節會加入 HTTPS 繫結 toomap 端點 tooyour 網站：
   
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
   
   已完成所有 hello 必要的變更 toohello 服務定義檔，但您仍然需要 tooadd hello 憑證資訊與 hello 服務組態檔。
4. 在服務組態檔 (CSCFG) 中，ServiceConfiguration.Cloud.cscfg 中加入**憑證**區段內 hello**角色**區段中，取代 hello 範例指紋值如下所示您的憑證：
   
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

(上述範例會使用 hello **sha1** hello 指紋演算法。 指定您的憑證指紋演算法的 hello 適當值。）

既然已經更新 hello 服務定義檔和服務組態檔，封裝上傳 tooAzure 部署。 如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。

## <a name="step-3-upload-a-certificate"></a>步驟 3：上傳憑證
您的部署套件更新的 toouse hello 憑證，同時也已經加入 HTTPS 端點。 現在您可以上傳 hello 封裝和憑證 tooAzure 以 hello Azure 傳統入口網站。

1. 登入 toohello [Azure 傳統入口網站][Azure classic portal]。 
2. 按一下**雲端服務**hello 左側導覽窗格中。
3. 按一下想要的 hello 雲端服務。
4. 按一下 hello**憑證** 索引標籤。
   
    ![按一下 hello 憑證 索引標籤](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. 按一下 hello**上傳** 按鈕。
   
    ![上傳](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. 提供 hello**檔案**，**密碼**，然後按一下 **完成**(hello 核取記號)。

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>步驟 4： 透過 HTTPS 連線 toohello 角色執行個體
您的部署會在 Azure 中已啟動並執行，您可以連線 tooit 使用 HTTPS。

1. 在 hello Azure 傳統入口網站，選取您的部署，然後按一下 [hello] 下方的連結**網站 URL**。
   
   ![判定網站 URL][2]
2. 在網頁瀏覽器，修改 hello 連結 toouse **https**而不是**http**，，然後瀏覽 hello 頁面。
   
   > [!NOTE]
   > 如果您使用自我簽署的憑證，當您瀏覽 tooan HTTPS 端點，您可能會看到憑證錯誤 hello 瀏覽器中的 hello 自我簽署憑證與相關聯。 使用受信任的憑證授權單位所簽署的憑證來排除這個問題;hello 同時，您可以略過 hello 錯誤。 （另一個選項是 tooadd hello 自我簽署的憑證 toohello 使用者的受信任的憑證授權單位憑證存放區）。
   > 
   > 
   
   ![SSL 範例網站][3]

如果您想 toouse SSL，而不是生產環境部署的預備環境部署，您必須先使用預備環境部署的 hello toodetermine hello URL。 部署雲端服務 toohello 預備環境，而不包括憑證或憑證資訊。 一旦部署之後，您可以判斷 hello GUID 為基礎的 URL，列出的 hello Azure 傳統入口網站的**網站 URL**欄位。 建立憑證與 hello 一般名稱 (CN) 等於 toohello GUID 為基礎的 URL (例如， **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**)。 使用 hello Azure 傳統入口網站 tooadd hello 憑證 tooyour 分段雲端服務。 然後，將 hello 憑證資訊 tooyour CSDEF 和 CSCFG 檔案、 重新封裝您的應用程式，並更新您預備的部署 toouse hello 新封裝。

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure.md)。
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name.md)。
* [管理您的雲端服務](cloud-services-how-to-manage.md)。

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
