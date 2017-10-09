---
title: "應用程式閘道使用的 URL 路由規則-aaaCreate Azure CLI 2.0 |Microsoft 文件"
description: "本頁面提供的指示 toocreate、 設定 Azure 應用程式閘道使用的 URL 路由規則"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>以 Azure CLI 2.0 使用路徑型路由建立應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

路徑為基礎的路由 URL 可讓您 tooassociate 路由根據 hello 的 Http 要求的 URL 路徑。 它會檢查是否顯示 hello 應用程式閘道中的 hello URL 設定的路由 tooa 後端集區，並將傳送 hello 網路流量 toohello 定義後端集區。 URL 為基礎的路由的常見用法是不同的內容類型 toodifferent 後端伺服器集區的 tooload 平衡要求。

URL 為基礎的路由導入了新的規則類型 tooapplication 閘道。 應用程式閘道具有 2 種規則類型：基本和 PathBasedRouting。 基本規則類型提供循環配置資源 hello 後端服務集區時 PathBasedRouting 此外 tooround 環散佈，並選擇 hello 後端集區也會納入考量的 hello 要求 URL 的路徑模式。

## <a name="scenario"></a>案例

在下列範例的 hello，應用程式閘道為 contoso.com 的流量提供兩個後端伺服器集區： 預設的伺服器集區以及映像伺服器集區。

要求的 http://contoso.com/image * tooimage 伺服器集區 (imagesBackendPool) 路由傳送，hello 路徑模式不符，如果已選取預設伺服器集區 (appGatewayBackendPool)。

![URL 路由](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>登入 tooAzure

開啟 hello **Microsoft Azure 命令提示字元**，並登入。 

```azurecli
az login -u "username"
```

> [!NOTE]
> 您也可以使用`az login`不需要輸入 aka.ms/devicelogin 在程式碼的裝置登入的 hello 參數。

一旦您輸入 hello 前面範例中，將程式碼。 瀏覽 toohttps://aka.ms/devicelogin 瀏覽器 toocontinue hello 登入處理序。

![顯示裝置登入的 cmd][1]

在 hello 瀏覽器中，輸入您收到 hello 程式碼。 您已重新導向的 tooa 登入頁面。

![瀏覽器 tooenter 程式碼][2]

一旦輸入 hello 程式碼後您登入，關閉 hello 瀏覽器 toocontinue 與 hello 案例。

![已順利登入][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>新增路徑為基礎的規則 tooan 現有應用程式閘道

建立已定義路徑規則的應用程式閘道

### <a name="create-a-new-back-end-pool"></a>建立新的後端集區

設定應用程式閘道設定**imagesBackendPool** hello hello 後端集區中，負載平衡網路流量。 在此範例中，您可以設定不同的後端集區設定為 hello 新增後端集區。 每個後端集區都可以有它自己的後端集區設定。  後端 HTTP 設定使用規則 tooroute 流量 toohello 正確的後端集區成員。 這會決定 hello 通訊協定和連接埠傳送流量 toohello 後端集區成員時所使用。 Cookie 架構工作階段，也取決於 hello 後端 HTTP 設定。  Cookie 架構工作階段相似性啟用時，會傳送流量 toohello 相同的後端，為每個封包的先前要求。

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>建立新的前端連接埠

設定應用程式閘道 hello 前端連接埠。 hello 前端連接埠組態物件會使用接聽程式 toodefine 哪些連接埠 hello 應用程式閘道接聽 hello 接聽程式上的流量。

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>建立新的接聽程式

Hello 接聽程式設定。 此步驟會設定 hello hello 公用 IP 位址的接聽程式，以及使用 tooreceive 連入網路流量的連接埠。 hello 下列範例會使用前端 IP 組態之前設定的 hello、 前端連接埠組態和通訊協定 （http 或 https），並設定 hello 接聽程式。 在此範例中，hello 接聽 hello 公用 IP 位址上稍早建立的連接埠 82 tooHTTP 流量。

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>建立 hello Url 路徑對應

設定 URL 規則路徑 hello 後端集區。 此步驟會設定應用程式閘道 toodefine hello 對應 URL 路徑與哪一個後端集區指派 toohandle hello 連入流量之間所使用的 hello 相對路徑。

> [!IMPORTANT]
> 每個路徑開頭必須 / 和 hello 唯一地方"\*」 允許，則在 hello 結束。 有效範例包括 /xyz、/xyz* 或 /xyz/*。 hello fed toohello 路徑比對器的字串不包含任何文字 hello 之後第一次"？"或"#"，且這些字元不得使用。 

hello 下列範例會建立一個規則 」 映像 / / *"路徑路由流量 tooback 端"imagesBackendPool。 」 此規則可確保每一組 url 的流量路由的 toohello 後端。 比方說，http://adatum.com/images/figure1.jpg 會太"imagesBackendPool。 」 如果 hello 路徑不符合任何 hello 預先定義的路徑規則，hello 規則路徑對應設定也會設定預設的後端位址集區。 比方說，http://adatum.com/shoppingcart/test.html 會 toopool1，因為它定義為 hello 預設集區不相符的流量。

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>後續步驟

如果您想 toolearn 有關安全通訊端層 (SSL) 卸載時，請參閱[設定 SSL 卸載的應用程式閘道](application-gateway-ssl-cli.md)。


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
