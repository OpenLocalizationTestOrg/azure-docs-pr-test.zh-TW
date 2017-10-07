---
title: "使用 API 管理快速入門 aaaAzure Service Fabric |Microsoft 文件"
description: "本指南也說明如何 tooquickly 開始使用 Azure API 管理和服務網狀架構。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a>Service Fabric 搭配 Azure API 管理快速入門

本指南也說明如何 tooset 以 Service Fabric 的 Azure API 管理及設定 Service Fabric 中的第一個應用程式開發介面作業 toosend 流量 tooback 後端服務。 toolearn 有關使用 Service Fabric 的 Azure API 管理案例的詳細資訊，請參閱 「 hello[概觀](service-fabric-api-management-overview.md)發行項。 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a>部署應用程式開發介面管理和服務網狀架構 tooAzure

toodeploy API 管理而共用的虛擬網路中的 Service Fabric 叢集 tooAzure hello 第一個步驟。 這可讓 Service Fabric 直接使用 API 管理 toocommunicate，讓它直接 tooany 後端服務在 Service Fabric 中可以執行服務探索、 服務分割解析，以及將流量。

### <a name="topology"></a>拓撲

本指南將部署的 hello 下列 API 管理和服務網狀架構中的子網路是拓樸 tooAzure hello 相同虛擬網路：

 ![圖片標題][sf-apim-topology-overview]

tooget 快速地開始，資源管理員範本可供每個部署步驟：

 - 網路拓撲：
    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]
 - Service Fabric 叢集：
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]
 - API 管理：
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

### <a name="sign-in-tooazure-and-select-your-subscription"></a>登入 tooAzure 並選取您的訂用帳戶

本指南使用 [Azure PowerShell][azure-powershell]。 當您啟動新的 PowerShell 工作階段時，登入 tooyour Azure 帳戶，並選取您的訂用帳戶，然後再執行 Azure 命令。
 
Azure 帳戶登入 tooyour 中：

```powershell
PS > Login-AzureRmAccount
```

選取您的訂用帳戶：

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a>建立資源群組

為您的部署建立新的新資源群組。 為其命名並提供位置。

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a>部署 hello 網路拓撲

hello 第一個步驟是 tooset 向上 hello 網路拓樸 toowhich API 管理，並將部署的 hello Service Fabric 叢集。 hello [network.json] [ network-arm] Resource Manager 範本會設定的 toocreate 虛擬網路 (VNET) 具有兩個的子網路和兩個網路安全性群組 (NSG) 群組。 

hello [network.parameters.json] [ network-parameters-arm]參數檔案包含 hello 名稱 hello 子網路和應用程式開發介面管理和服務網狀架構將會部署到的 Nsg。 本指南中，hello 參數值就不需要 toobe 變更。 使用這些值的 hello API 管理和服務網狀架構資源管理員範本，因此如果在修改這裡，您必須修改在據以 hello 其他資源管理員範本。 

 1. 下載下列資源管理員範本和參數檔 hello:

    - [network.json][network-arm]
    - [network.parameters.json][network-parameters-arm]

 2. 使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 hello 網路安裝程式的 hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a>部署 hello Service Fabric 叢集

一旦部署完成 hello 網路資源，hello 下一個步驟是 toodeploy Service Fabric 叢集 toohello VNET hello 子網路中，且 NSG 指定 hello Service Fabric 叢集。 本教學課程，hello 服務網狀架構資源管理員範本是預先設定的 toouse hello 名稱 hello VNET、 子網路，以及您 hello 上一個步驟中設定的 NSG。 

hello Service Fabric 叢集資源管理員範本是已設定的 toocreate 憑證安全性的安全叢集。 hello 憑證是針對您的叢集和 toomanage 使用者存取 tooyour Service Fabric 叢集使用的 toosecure 節點對節點通訊。 API 管理使用此憑證 tooaccess hello Service Fabric 命名服務的服務探索。

基於叢集安全性考量，此步驟需要您在 Key Vault 中有憑證。 如需有關使用 Key Vault 來設定安全叢集的詳細資訊，請參閱[這份關於使用 Resource Manager 在 Azure 中建立叢集的指南](service-fabric-cluster-creation-via-arm.md)

> [!NOTE]
> 您可以在用於叢集存取的加法 toohello 憑證加入 Azure Active Directory 驗證。 Azure Active Directory hello 建議方式 toomanage 使用者存取 tooyour Service Fabric 叢集，但不是需要 toocomplete 本教學課程。 不論是叢集的節點對節點安全性，還是「Azure API 管理」驗證，都需要憑證，後者目前不支援向 Service Fabric 後端的 Azure Active Directory 進行驗證。

 1. 下載下列資源管理員範本和參數檔 hello:
 
    - [cluster.json][cluster-arm]
    - [cluster.parameters.json][cluster-parameters-arm]

 2. 填寫在 hello hello 空參數`cluster.parameters.json`檔案的部署，包括 hello[金鑰保存庫資訊](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault)叢集憑證。

 3. 使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 toocreate hello Service Fabric 叢集 hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a>部署 API 管理

最後，部署在 hello 子網路和指定的 API 管理 NSG 中的 API 管理 toohello VNET。 您無須 toowait 的 hello Service Fabric 叢集部署 toofinish 之前部署 API 管理。 

本教學課程，hello API 管理 Resource Manager 範本是預先設定的 toouse hello 名稱 hello VNET、 子網路，以及您 hello 上一個步驟中設定的 NSG。 

 1. 下載下列資源管理員範本和參數檔 hello:
 
    - [apim.json][apim-arm]
    - [apim.parameters.json][apim-parameters-arm]

 2. 填寫在 hello hello 空參數`apim.parameters.json`為您的部署。

 3. 使用下列 PowerShell 命令 toodeploy hello 資源管理員範本和參數檔案 API 管理的 hello:

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a>設定 API 管理

部署完您的「API 管理」與 Service Fabric 叢集之後，您可以在「API 管理」中設定 Service Fabric 後端。 這可讓您 toocreate 傳送流量 tooyour Service Fabric 叢集的後端服務原則。

### <a name="api-management-security"></a>API 管理安全性

tooconfigure hello Service Fabric 後端中，您必須先 tooconfigure API 管理安全性設定。 tooconfigure 安全性設定，請移 tooyour API 管理服務在 hello Azure 入口網站中。

#### <a name="enable-hello-api-management-rest-api"></a>啟用 hello API 管理 REST API

hello API 管理 REST API 是目前唯一的方式 tooconfigure hello 後端服務。 hello 第一個步驟為 tooenable hello API 管理 REST API，並保護其安全。

 1. 在 hello API 管理服務中，選取 **管理 API-PREVIEW**下**安全性**。
 2. 檢查 hello**啟用 API 管理 REST API**核取方塊。
 3. 請注意 hello 管理 API URL-這是我們會使用向上 hello Service Fabric 後端的更新版本 tooset hello URL
 4. 產生**存取權杖**藉由選取到期日和索引鍵，然後按一下 hello**產生**朝 hello hello 頁面底部的按鈕。
 5. 複製 hello**存取權杖**並將它儲存-我們會使用它在 hello 下列步驟。 請注意這點不同於 hello 主要金鑰和次要金鑰。

#### <a name="upload-a-service-fabric-client-certificate"></a>上傳 Service Fabric 用戶端憑證

API 管理必須與您的 Service Fabric 叢集服務探索使用具有存取 tooyour 叢集的用戶端憑證驗證。 為了簡單起見，這個教學課程使用 hello 相同的憑證建立其預設值可以是使用的 tooaccess hello Service Fabric 叢集時，指定您的叢集。

 1. 在 hello API 管理服務中，選取 **用戶端憑證-PREVIEW**下**安全性**。
 2. 按一下 hello **+ 加**按鈕
 2. 選取 hello 私密金鑰檔 (.pfx) 的 hello 叢集指定憑證，則建立 Service Fabric 叢集時，為它命名，並提供 hello 私密金鑰密碼。

> [!NOTE]
> 本教學課程使用相同憑證的 hello 的用戶端驗證和叢集節點的安全性。 如果您有一個設定的 tooaccess Service Fabric 叢集，您可以使用不同的用戶端憑證。

### <a name="configure-hello-backend"></a>設定 hello 後端

API 管理的安全性設定，您可以設定 hello Service Fabric 後端。 Service Fabric 範例 hello Service Fabric 叢集是 hello 後端，而不是特定的 Service Fabric 服務。 這允許一項服務比單一原則 tooroute toomore hello 叢集中。

這個步驟需要 hello 您先前產生的存取權杖，並 hello 您上傳 tooAPI 管理 hello 上一個步驟中的您叢集的憑證指紋。

> [!NOTE]
> 如果您使用不同的用戶端憑證 hello 上一個步驟中的 API 管理，您需要 hello 指紋 hello 用戶端憑證在此步驟中加入 toohello 叢集憑證指紋。

傳送 hello 遵循 HTTP PUT 要求 toohello 您先前記下啟用 hello API 管理 REST API tooconfigure hello Service Fabric 後端服務時的 API 管理 API URL。 您應該會看到`HTTP 201 Created`hello 命令執行成功的回應。 如需有關每個欄位的詳細資訊，請參閱 hello API 管理[後端應用程式開發介面參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)。

HTTP 命令和 URL：
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

要求標頭：
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

要求本文：
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

hello **url**這裡參數就是完整的服務名稱是在叢集中的所有要求的服務路由 tooby 預設，如果後端原則中不指定任何服務名稱。 您可能使用假的服務名稱，例如"fabric: / 假/服務 」 如果您不想 toohave 後援服務。

請參閱 toohello API 管理[後端應用程式開發介面參考文件](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend)如需有關每個欄位。

#### <a name="example"></a>範例

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a>部署 Service Fabric 後端服務

有 hello Service Fabric 設定為後端 tooAPI 管理之後，您可以編寫後端原則，您將流量傳送 tooyour Service Fabric 服務的 api。 但首先您必須在 Service Fabric tooaccept 要求中執行的服務。

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a>建立具有 HTTP 端點的 Service Fabric 服務

此教學課程中，我們將建立基本無狀態 ASP.NET Core 可靠的服務使用 hello 預設 Web API 專案範本。 這會為您的服務建立一個 HTTP 端點，而您將會透過「Azure API 管理」來公開此服務：

```
/api/values
```

請從[為您的 ASP.NET Core 開發設定開發環境](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core)開始著手。

設定完開發環境之後，請以「系統管理員」身分啟動 Visual Studio，然後建立 ASP.NET Core 服務：

 1. 在 Visual Studio 中，選取 [檔案] -> [新增專案]。
 2. 選取雲端下的 hello Service Fabric 應用程式範本並將其命名**"ApiApplication"**。
 3. 選取 hello ASP.NET Core 服務範本和名稱 hello 專案**"WebApiService"**。
 4. 選取 Web 應用程式開發介面 ASP.NET Core 1.1 hello 專案範本。
 5. Hello 專案建立之後，開啟`PackageRoot\ServiceManifest.xml`並移除 hello `Port` hello 端點資源的組態屬性：
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    這可讓 Service Fabric toospecify hello 應用程式連接埠的範圍，我們透過 hello 網路安全性小組在 hello 叢集資源管理員範本中，開啟允許流量 tooflow tooit 從 API 管理中的動態連接埠。
 
 6. 按 f5 鍵，在 Visual Studio tooverify hello web API 中的是在本機使用。 

    開啟 Service Fabric 總管，並向下切入 tooa hello ASP.NET Core service toosee hello 基底位址 hello 服務正在接聽的特定執行個體。 新增`/api/values`toohello 基底地址，並在瀏覽器中開啟它。 這樣會叫用 hello hello Web API 範本中的 hello ValuesController 上的 Get 方法。 它會傳回 hello hello 範本，包含兩個字串的 JSON 陣列所提供的預設回應：

    ```json
    ["value1", "value2"]`
    ```

    這是您將會公開透過 API 管理 Azure 中的 hello 端點。

 7. 最後，部署在 Azure 中的 hello 應用程式 tooyour 叢集。 [使用 Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box)，以滑鼠右鍵按一下 hello 應用程式專案，然後選取**發行**。 提供您的叢集端點 (例如， `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello 應用程式 tooyour Service Fabric 叢集在 Azure 中。

一個名為 `fabric:/ApiApplication/WebApiService` 的 ASP.NET Core 無狀態服務現在應該正在 Azure 中的 Service Fabric 叢集內執行。

## <a name="create-an-api-operation"></a>建立 API 作業

現在我們準備 toocreate API 管理中的作業與該外部用戶端使用 toocommunicate hello hello Service Fabric 叢集中執行的 ASP.NET Core 無狀態服務。

 1. 登入 toohello Azure 入口網站，並瀏覽 tooyour API 管理服務部署。
 2. 在 hello API 管理服務刀鋒視窗中，選取  **Api-預覽**
 3. 加入新的應用程式開發介面，請按一下 hello**空白應用程式開發介面**方塊，並填寫 [hello] 對話方塊：

     - **Web 服務 URL**：就 Service Fabric 後端而言，並不使用此 URL 值。 您可以在這裡輸入任何值。 針對本教學課程，請使用：`http://servicefabric`。
     - **名稱**：為您的 API 提供任何名稱。 針對本教學課程，請使用 `Service Fabric App`。
     - **URL 配置**：選取 [HTTP]、[HTTPS] 或 [both]。 針對本教學課程，請使用 `both`。
     - **API URL 尾碼**：為 API 提供一個尾碼。 針對本教學課程，請使用 `myapp`。
 
 4. 一旦建立 hello API 時，按一下  **+ 加入作業**tooadd 前端的 API 作業。 填寫 hello 值：
    
     - **URL**： 選取`GET`和 hello API 提供的 URL 路徑。 針對本教學課程，請使用 `/api/values`。
     
       根據預設，hello URL 指定路徑這裡 hello URL 路徑傳送 toohello 後端服務的網狀架構服務。 如果您使用 hello 相同 URL 路徑以下服務所使用，在此情況下`/api/values`，然後 hello 作業適用於不需要進一步修改。 您也可以指定 URL 路徑不同於您的後端服務的網狀架構服務所使用的 hello URL 路徑在此情況下您也會需要 toospecify 路徑重寫作業原則中更新版本。
     - **顯示名稱**： 提供 hello 應用程式開發介面的任何名稱。 針對本教學課程，請使用 `Values`。

## <a name="configure-a-backend-policy"></a>設定後端原則

hello 後端原則結合的所有項目。 這是您在其中設定 hello 後端 Service Fabric 服務 toowhich 要求會路由傳送。 您可以套用此原則 tooany API 作業。 hello [Service Fabric 的後端設定](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)提供 hello 下列要求會路由控制項： 
 - 藉由指定的 Service Fabric 服務執行個體名稱，可能是硬式編碼服務執行個體選取範圍 (比方說， `"fabric:/myapp/myservice"`) 或產生自 hello HTTP 要求 (例如， `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`)。
 - 分割區解析：方法是使用任何 Service Fabric 資料分割配置來產生分割區索引鍵。
 - 無狀態服務的複本選取。
 - 解決方式重試重新解決服務的位置，然後重新傳送要求 toospecify hello 條件可讓您的條件。

此教學課程中，建立路由要求直接 toohello 先前部署的 ASP.NET Core 無狀態服務的後端原則：

 1. 選取和編輯 hello**輸入原則**hello`Values`按一下 hello [編輯] 圖示，然後再選取作業**程式碼檢視**。
 2. 在 [hello 原則程式碼編輯器] 中，加入`set-backend-service`原則底下輸入原則，如下所示，並按一下 hello**儲存**按鈕：
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

一組完整的 Service Fabric 後端原則屬性，請參閱 toohello [API 管理後端文件](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)

### <a name="add-hello-api-tooa-product"></a>新增 hello API tooa 產品。 

您可以呼叫 hello API 之前，它必須加入您將可以授與存取 toousers tooa 產品。 

 1. 在 hello API 管理服務中，選取 **產品-PREVIEW**。
 2. 「API 管理」預設會提供兩種產品：[入門] 和 [無限制]。 選取 hello 無限制的產品。
 3. 選取 API。
 4. 按一下 hello **+ 加** 按鈕。
 5. 選取 hello `Service Fabric App` API hello 前述步驟中建立，並按一下 hello**選取** 按鈕。

### <a name="test-it"></a>進行測試

您現在可以嘗試透過 API 管理服務網狀架構中傳送要求 tooyour 後端服務，直接從 hello Azure 入口網站。

 1. 在 hello API 管理服務中，選取  **API-PREVIEW**。
 2. 在 [hello `Service Fabric App` hello 先前步驟中，在您建立的應用程式開發介面選取 hello**測試**] 索引標籤。
 3. 按一下 hello**傳送**按鈕 toosend 測試要求 toohello 後端服務。

## <a name="next-steps"></a>後續步驟

此時，您應該已在 Service Fabric 與「API 管理」做好基本設定。

此教學課程會使用您得以快速設定，您 Service Fabric 叢集 tooget 基本憑證為基礎的使用者驗證。 建議您使用 [Azure Active Directory 驗證](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication)，以針對 Service Fabric 叢集提供更進階的使用者驗證。 

下一步[建立並設定進階的產品設定在 Azure API 管理](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules)tooprepare 應用程式的真實世界的流量。

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
