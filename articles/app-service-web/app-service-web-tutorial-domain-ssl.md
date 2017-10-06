---
title: "aaaAdd 自訂網域和 SSL tooan Azure web 應用程式 |Microsoft 文件"
description: "了解如何 tooprepare Azure web 應用程式 toogo 生產藉由新增公司商標。 對應 hello 自訂網域名稱 （虛名網域） tooyour web 應用程式，並保護其安全的自訂 SSL 憑證。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>新增自訂網域及 SSL tooan Azure web 應用程式

本教學課程會示範如何 tooquickly 對應自訂網域名稱 tooyour Azure web 應用程式，並使用 自訂的 SSL 憑證保護安全性。 

## <a name="before-you-begin"></a>開始之前

執行此範例之前，安裝 hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)在本機。

您也需要系統管理存取權 toohello DNS 設定 頁面，為個別網域提供者。 例如，tooadd `www.contoso.com`，您需要 toobe 無法 tooconfigure DNS 項目`contoso.com`。

最後，您必須是有效的。PFX 檔案_和_其密碼，為您想 tooupload hello SSL 憑證並繫結。 此 SSL 憑證應該是您想要設定的 toosecure hello 自訂網域名稱。 在上述範例中的 hello，保護您的 SSL 憑證應該`www.contoso.com`。 

## <a name="step-1---create-an-azure-web-app"></a>步驟 1 - 建立 Azure Web 應用程式

### <a name="log-in-tooazure"></a>登入 tooAzure

我們正在進行 toouse hello Azure CLI 2.0 終端機視窗 toocreate hello 資源中的需要 toohost 我們在 Azure 中的 Node.js 應用程式。  登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>建立資源群組   
建立資源群組以 hello [az 群組建立](/cli/azure/group#create)。 Azure 資源群組是在其中部署與管理 Azure 資源 (如 Web 應用程式、資料庫和儲存體帳戶) 的邏輯容器。 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee 何種可能的值，您可以使用`---location`，使用 hello `az appservice list-locations` Azure CLI 命令。

## <a name="create-an-app-service-plan"></a>建立應用程式服務方案

建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

hello 下列範例會建立名為 App Service 方案`myAppServicePlan`使用 hello**基本**定價層。

az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1

Hello 應用程式服務方案建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>建立 Web 應用程式

已建立 App Service 方案，建立 web 應用程式內 hello`myAppServicePlan`應用程式服務方案。 您正在裝載的空間 toodeploy 您的程式碼，以及為您提供 URL tooview hello hello web 應用程式提供部署應用程式。 使用 hello [az 應用程式 web 建立](/cli/azure/appservice/web#create)命令 toocreate hello web 應用程式。 

在下方的 hello 命令，請取代您自己的唯一應用程式名稱，您會看到 hello`<app_name>`預留位置。 這個唯一名稱會用做為 hello hello hello web 應用程式的預設網域名稱的一部分，因此 hello 名稱需要 toobe 唯一跨 Azure 中的所有應用程式。 公開 tooyour 使用者之前，您稍後可以對應任何自訂 DNS 項目 toohello web 應用程式。 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

從 JSON 輸出 hello`defaultHostName`顯示 web 應用程式的預設網域名稱。 在瀏覽器中瀏覽 toothis 位址。

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>步驟 2 - 設定 DNS 對應

在此步驟中，您必須加入的對應自訂網域 tooyour web 應用程式的預設網域名稱，從`<app_name>.azurewebsites.net`。 一般而言，您可以在網域提供者的網站中執行此步驟。 每個網域註冊機構的網站稍有不同，請查閱您的提供者文件。 不過，以下有幾個一般方針。 

### <a name="navigate-tootoodns-management-page"></a>瀏覽 tootooDNS 管理頁面

首先，登入 tooyour 網域註冊機構的網站。  

然後，尋找 hello 頁面管理 DNS 記錄。 尋找連結或標示為 hello 網站的區域**網域名稱**， **DNS**，或**名稱伺服器管理**。 通常，您可以找到 hello 連結，檢視您的帳戶資訊，例如尋找連結**我的網域**。

找到此頁面之後，尋找可讓您新增或編輯 DNS 記錄的連結。 這可能是 [區域檔案]、[DNS 記錄] 連結，或 [進階設定] 連結。

### <a name="create-a-cname-record"></a>建立 CNAME 記錄

新增對應 hello 所需的子網域名稱 tooyour web 應用程式的預設網域名稱的 CNAME 記錄 (`<app_name>.azurewebsites.net`，其中`<app_name>`是您的應用程式的唯一名稱)。

Hello`www.contoso.com`範例中，建立 CNAME 對應 hello `www` hostname 太`<app_name>.azurewebsites.net`。

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>步驟 3-設定 web 應用程式上的 hello 自訂網域

當您完成設定 hello 主機名稱的對應網域提供者的網站中時，您已準備好 tooconfigure hello 自訂網域 web 應用程式上。 使用 hello [az appservice web 設定主機名稱加入](/cli/azure/appservice/web/config/hostname#add)命令 tooadd 這項設定。 

在下方的 hello 命令，請取代`<app_name>`與您的唯一應用程式名稱 < your_custom_domain > hello 完整格式的自訂網域名稱 (例如`www.contoso.com`)。 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

hello 自訂網域，現在是完全對應的 tooyour web 應用程式。 在瀏覽器中瀏覽 toohello 自訂網域名稱。 例如：

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>步驟 4-繫結的自訂 SSL 憑證 tooyour web 應用程式

現在您已經有 Azure web 應用程式，您想要 hello 瀏覽器的網址列中的 hello 網域名稱。 不過，如果您瀏覽 toohello`https://<your_custom_domain>`現在，您會收到憑證錯誤。 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

發生此錯誤是因為 Web 應用程式尚無符合自訂網域名稱的 SSL 憑證繫結。 不過，您無法取得錯誤如果您瀏覽過`https://<app_name>.azurewebsites.net`。 這是因為您的應用程式，以及所有的 Azure App Service 應用程式，使用 hello SSL 憑證保護 hello`*.azurewebsites.net`預設萬用字元網域。 

在您的自訂網域名稱來排序 tooaccess 您 web 應用程式，您需要 toobind hello SSL 憑證 toohello web 應用程式的自訂網域。 您將在此步驟中這樣做。 

### <a name="upload-hello-ssl-certificate"></a>上傳 hello SSL 憑證

Hello tooyour web 應用程式的自訂網域的 SSL 憑證上傳使用 hello [az appservice web 設定 ssl 上傳](/cli/azure/appservice/web/config/ssl#upload)命令。

在下方的 hello 命令，請取代`<app_name>`具有唯一的應用程式名稱`<path_to_ptx_file>`與 hello 路徑 tooyour。PFX 檔案和`<password>`與憑證的密碼。 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

上傳 hello 憑證時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

從 JSON 輸出 hello`thumbprint`顯示您上傳的憑證指紋。 將複製的值供 hello 下一個步驟。

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>繫結 hello 上傳 SSL 憑證 toohello web 應用程式

您的 web 應用程式現在具有您想，hello 自訂網域名稱，而且也有保護該自訂網域的 SSL 憑證。 hello 事左的 toodo 是 toobind hello 上傳的憑證 toohello web 應用程式。 您可以使用 hello [az appservice web 設定 ssl 繫結](/cli/azure/appservice/web/config/ssl#bind)命令。

在下方的 hello 命令，請取代`<app_name>`具有唯一的應用程式名稱和`<thumbprint-from-previous-output>`hello 您從 hello 前一個命令取得的憑證指紋。 

az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI

Hello 憑證繫結的 tooyour web 應用程式時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }

在瀏覽器中瀏覽 tooHTTPS 端點的自訂網域名稱。 例如：

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>其他資源

[購買自訂網域名稱並在 Azure App Service 中設定](custom-dns-web-site-buydomains-web-app.md)
[購買並設定 Azure App Service 的 SSL 憑證](web-sites-purchase-ssl-web-site.md)
