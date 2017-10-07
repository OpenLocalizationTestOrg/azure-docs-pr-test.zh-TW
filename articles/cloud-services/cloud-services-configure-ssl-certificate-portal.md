---
title: "雲端服務的 SSL aaaConfigure |Microsoft 文件"
description: "深入了解如何 toospecify HTTPS 端點，web 角色和如何 tooupload SSL 的憑證 toosecure 您的應用程式。 這些範例使用 hello Azure 入口網站。"
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
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
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

安全通訊端層 (SSL) 加密是最常用的 hello 方法保護資料傳送嗨跨網際網路。 一般工作的討論如何 toospecify HTTPS 端點，web 角色和如何 tooupload SSL 的憑證 toosecure 您的應用程式。

> [!NOTE]
> 在這項工作的 hello 程序適用於 tooAzure 雲端服務。應用程式服務，請參閱[這](../app-service-web/web-sites-configure-ssl-certificate.md)。
>

此工作使用生產部署。 Hello 本主題的結尾會提供有關使用預備環境部署。

如果尚未建立雲端服務，請先閱讀 [這裡](cloud-services-how-to-create-deploy-portal.md) 。

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

<a name="modify"> </a>

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

3. 在您的服務定義檔中加入**繫結**hello 內的項目**網站**> 一節。 這個項目會加入 HTTPS 繫結 toomap 端點 tooyour 網站：

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

   已完成所有 hello 必要的變更 toohello 服務定義檔。但是，您仍然需要 tooadd hello 憑證資訊與 hello 服務組態檔。
4. 在服務組態檔 (CSCFG) ServiceConfiguration.Cloud.cscfg 中，新增**憑證**值以取代您的憑證。 hello 下列程式碼範例提供詳細資料的 hello**憑證**區段中的，除了 hello 指紋值。

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

(這個範例會使用**sha1** hello 指紋演算法。 指定您的憑證指紋演算法的 hello 適當值。）

既然已經更新 hello 服務定義檔和服務組態檔，封裝上傳 tooAzure 部署。 如果您是使用 **cspack**，請確定未使用 **/generateConfigurationFile** 旗標，因為如此會將覆寫您剛插入的憑證資訊。

## <a name="step-3-upload-a-certificate"></a>步驟 3：上傳憑證
連接 toohello Azure 入口網站和...

1. 在 hello**所有資源**區段中的 hello 入口網站中，選取您的雲端服務。

    ![發佈您的雲端服務](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. 按一下 [憑證]。

    ![按一下 hello 憑證圖示](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. 按一下**上傳**hello 憑證區域的 hello 頂端。

    ![按一下 hello 上載功能表項目](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. 提供 hello**檔案**，**密碼**，然後按一下 **上傳**底部 hello hello 資料輸入區域。

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>步驟 4： 透過 HTTPS 連線 toohello 角色執行個體
您的部署會在 Azure 中已啟動並執行，您可以連線 tooit 使用 HTTPS。

1. 按一下 hello**網站 URL** tooopen hello web 瀏覽器。

   ![按一下 hello 網站 URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. 在網頁瀏覽器，修改 hello 連結 toouse **https**而不是**http**，，然後瀏覽 hello 頁面。

   > [!NOTE]
   > 如果您使用自我簽署的憑證，當您瀏覽 tooan HTTPS 端點，您可能會看到憑證錯誤 hello 瀏覽器中的 hello 自我簽署憑證與相關聯。 使用受信任的憑證授權單位所簽署的憑證來排除這個問題;hello 同時，您可以略過 hello 錯誤。 （另一個選項是 tooadd hello 自我簽署的憑證 toohello 使用者的受信任的憑證授權單位憑證存放區）。
   >
   >

   ![網站預覽](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > 如果您想 toouse SSL，而不是生產環境部署的預備環境部署，您必須先使用預備環境部署的 hello toodetermine hello URL。 一旦部署雲端服務，預備環境的 hello URL toohello 取決於 hello**部署 ID** GUID，格式如下：`https://deployment-id.cloudapp.net/`  
   >
   > 建立憑證與 hello 一般名稱 (CN) 等於 toohello GUID 為基礎的 URL (例如， **328187776e774ceda8fc57609d404462.cloudapp.net**)。 使用 hello 入口 tooadd hello 憑證 tooyour 分段雲端服務。 然後，將 hello 憑證資訊 tooyour CSDEF 和 CSCFG 檔案、 重新封裝您的應用程式，並更新您預備的部署 toouse hello 新封裝。
   >

## <a name="next-steps"></a>後續步驟
* [雲端服務的一般設定](cloud-services-how-to-configure-portal.md)。
* 了解如何太[部署雲端服務](cloud-services-how-to-create-deploy-portal.md)。
* 設定 [自訂網域名稱](cloud-services-custom-domain-name-portal.md)。
* [管理您的雲端服務](cloud-services-how-to-manage-portal.md)。
