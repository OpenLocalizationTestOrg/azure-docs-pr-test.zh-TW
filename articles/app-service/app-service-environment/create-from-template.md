---
title: "aaaCreate Azure App Service 環境使用資源管理員範本"
description: "說明如何使用資源管理員範本的外部或 ILB Azure App Service 環境 toocreate"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本立 ASE

## <a name="overview"></a>概觀
Azure App Service Environment (ASE) 可以使用網際網路可存取端點，或是 Azure 虛擬網路 (VNet) 中內部位址上的端點來建立。 使用內部端點建立時，該端點是由稱為內部負載平衡器 (ILB) 的 Azure 元件提供。 內部 IP 位址上 hello ASE 稱為 ILB ase。 hello ASE 與公用端點會呼叫外部 ase。 

Ase 中可以建立使用 hello Azure 入口網站或 Azure Resource Manager 範本。 本文逐步解說 hello 步驟和所需的資源管理員範本 toocreate 外部 ASE 或 ILB ASE 語法。 toolearn toocreate ASE hello Azure 入口網站中的看到如何[進行外部 ASE] [ MakeExternalASE]或[進行 ILB ASE][MakeILBASE]。

當您建立 ASE hello Azure 入口網站中時，您可以在相同的時間，或選擇到預先存在的 VNet toodeploy hello 建立 VNet。 從範本建立 ASE 時，必須具備下列項目： 

* Resource Manager VNet。
* 該 VNet 中的子網路。 我們建議的 ASE 子網路大小`/25`128 位址 tooaccomodate 未來成長使用。 建立 hello ASE 之後，您無法變更 hello 大小。
* 從您的 VNet hello 資源識別碼。 在虛擬網路內容 下，您可以從 hello Azure 入口網站取得這項資訊。
* 您想成 toodeploy 的 hello 訂用帳戶。
* 您想成 toodeploy hello 位置。

tooautomate ASE 建立：

1. 從範本建立 hello ASE。 如果是建立外部 ASE，完成此步驟就建立完成。 如果您建立 ILB ase 中，有幾個的多個項目 toodo。

2. 建立 ILB ASE 之後，會上傳與您的 ILB ASE 網域相符的 SSL 憑證。

3. hello 已上傳的 SSL 憑證指派 toohello ILB ASE 做為其 「 預設 」 的 SSL 憑證。  此憑證用於 SSL 流量 tooapps hello ILB ASE 上，使用 hello 一般根網域的指派的 toohello ASE (例如，https://someapp.mycustomrootcomain.com) 時。


## <a name="create-hello-ase"></a>建立 hello ASE
在 GitHub 上的[範例][quickstartasev2create]中有可建立 ASE 的 Resource Manager 範本及其相關聯的參數檔案。

如果您想 toomake ILB ase 中，使用這些資源管理員範本[範例][quickstartilbasecreate]。 它們，符合 toothat 使用案例。 大部分的 hello 參數在 hello *azuredeploy.parameters.json*檔案是常見 toohello 建立 ILB ASEs 和外部 ASEs。 hello 表呼叫參數的特殊附註，或獨有的當您建立 ILB ase 中：

* *interalLoadBalancingMode*： 在大部分情況下，設定此 too3，這表示這兩個連接埠 80/443 上的 HTTP/HTTPS 流量，及 hello 控制項/資料通道連接埠上 hello ASE tooby hello FTP 服務該通訊埠，您將繫結的 tooan ILB 配置的虛擬網路內部位址。 如果這個屬性設定 too2，只有 hello FTP 服務的相關連接埠 （控制和資料通道） 是繫結的 tooan ILB 位址。 hello HTTP/HTTPS 流量會保留在 hello 公用 VIP。
* *dns 尾碼*： 這個參數會定義會指派的 toohello ASE hello 預設根網域。 在 Azure App Service hello 公用種變化，hello 預設根網域的所有 web 應用程式是*.azurewebsites.net*。 由於 ILB ASE 內部 tooa 客戶虛擬網路，就沒有任何意義 toouse hello 公開服務的預設根網域。 相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。 例如，Contoso Corporation 可能會使用預設的根網域的*內部 contoso.com*針對預定的 toobe 解析與只能在 Contoso 虛擬網路中存取應用程式。 
* *ipSslAddressCount*： 這個參數會自動預設為 tooa 中的數值 0 hello *azuredeploy.json*檔案，因為 ILB ASEs 只能有單一的 ILB 位址。 ILB ASE 沒有明確的 IP-SSL 位址。 因此，hello ILB ase 中的 IP SSL 位址集區必須設定 toozero。 否則，就會發生佈建錯誤。 

之後 hello *azuredeploy.parameters.json*檔案填滿，請建立 hello ASE 利用 hello PowerShell 程式碼片段。 變更 hello 檔案路徑 toomatch hello 資源管理員範本檔案位置在電腦上。 請記住 toosupply 您自己的值為 hello 資源管理員部署名稱和 hello 資源群組名稱：

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

它會建立 hello ASE toobe 一小時。 然後 hello ASE 顯示 hello ASEs 觸發 hello 部署的 hello 訂閱 hello 清單中的入口網站中。

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>上傳和設定 hello 「 預設 」 的 SSL 憑證
會使用的 tooestablish SSL 連線 tooapps hello 「 預設 」 SSL 憑證，必須是與 hello ASE 相關聯的 SSL 憑證。 如果 hello ASE 的預設 DNS 尾碼是*內部 contoso.com*，連線 toohttps://some-random-app.internal-contoso.com 需要有效的 SSL 憑證 **.internal contoso.com*. 

使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證，取得有效的 SSL 憑證。 不論 hello 來源 hello SSL 憑證，必須適當設定下列憑證屬性的 hello:

* **主旨**： 此屬性必須設定得 **.your 根網域-here.com*。
* **Subject Alternative Name**此屬性必須同時包含 *.your-root-domain-here.com 和 *.scm.your-root-domain-here.com。與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello 使用 hello 表單的位址*your-app-name.scm.your-root-domain-here.com*。

備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。 轉換/儲存為.pfx 檔案 hello SSL 憑證。 請記住該 hello.pfx 檔案必須包含所有中繼和根憑證。 使用密碼保護其安全。

toobe 轉換成 base64 字串 hello 的 SSL 憑證上傳使用資源管理員範本，因為需要 hello.pfx 檔案。 因為資源管理員範本檔案是文字檔，hello.pfx 檔必須轉換成 base64 字串。 如此一來，它可以包含為 hello 範本的參數。

使用下列 PowerShell 程式碼片段的 hello:

* 產生自我簽署憑證。
* Hello 憑證匯出為.pfx 檔案。
* 轉換為 base64 編碼的字串中的 hello.pfx 檔案。
* 儲存 hello base64 編碼字串 tooa 個別檔案。 

此為 base64 編碼的 PowerShell 程式碼是來自 hello [PowerShell 指令碼的部落格][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Hello SSL 憑證已成功產生，並轉換 tooa base64 編碼字串之後，使用 hello 範例 Resource Manager 範本[設定 hello 預設 SSL 憑證][ quickstartconfiguressl] GitHub 上。 

hello 參數在 hello *azuredeploy.parameters.json*檔案如下：

* *appServiceEnvironmentName*: hello 的 hello ILB ASE 正在設定的名稱。
* *existingAseLocation*： 文字字串，包含 hello hello ILB ASE 部署所在的 Azure 區域。  例如："South Central US (美國中南部)"。
* *pfxBlobString*: hello based64 編碼的字串表示法的 hello.pfx 檔案。 使用 hello 稍早所示的程式碼片段，並將複製 hello"exportedcert.pfx.b64 」 中所包含的字串。 中貼上做為 hello hello 值*pfxBlobString*屬性。
* *密碼*: hello 用密碼 toosecure hello.pfx 檔案。
* *certificateThumbprint*: hello 憑證的指紋。 如果您從 PowerShell 擷取這個值 (例如， *$certificate。憑證指紋*hello 從先前程式碼片段)，您可以使用 hello 值。 如果您從 Windows 憑證對話方塊 hello 複製 hello 值，請記得 toostrip 出 hello 無關的空格。 hello *certificateThumbprint*應看起來像 AF3143EB61D43F6727842115BB7F17BBCECAECAE。
* *certificateName*： 自己選擇的好記的字串識別項使用 tooidentity hello 憑證。 hello 名稱用於一部分 hello 唯一的資源管理員識別碼 hello *Microsoft.Web/certificates*代表 hello SSL 憑證的實體。 hello 名稱*必須*結尾 hello 下列尾碼： \_yourASENameHere_InternalLoadBalancingASE。 hello Azure 入口網站會使用這個後置詞，如 hello 憑證指標是使用的 toosecure ILB 啟用 ase。

以下是 azuredeploy.parameters.json  的縮簡範例︰

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

之後 hello *azuredeploy.parameters.json*檔案填滿、 使用 hello PowerShell 程式碼片段設定 hello 預設 SSL 憑證。 變更 hello 檔案路徑 toomatch hello 資源管理員範本檔案的位置在電腦。 請記住 toosupply 您自己的值為 hello 資源管理員部署名稱和 hello 資源群組名稱：

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

花大約 40 分鐘每項 ASE 前端 tooapply hello 變更。 例如，對於預設大小的 ASE 使用兩個前端，hello 範本所花費一小時和 20 分鐘 toocomplete 周圍。 當執行 hello 範本時，無法擴充 hello ASE。  

Hello 範本完成之後，可以透過 HTTPS 存取 hello ILB ASE 上的應用程式。 hello 連線使用 hello 預設 SSL 憑證來進行保護。 hello ILB ASE 上的應用程式會使用 hello 應用程式名稱加上 hello 預設主機名稱的組合來進行定址時，會使用 hello 預設 SSL 憑證。 例如，https://mycustomapp.internal-contoso.com 使用 hello 預設 SSL 憑證的 **.internal contoso.com*。

不過，如同 hello 的多租用戶公用服務執行的應用程式，開發人員可以設定個別的應用程式的自訂主機名稱。 他們也可以為個別的應用程式設定唯一 SNI SSL 憑證繫結。

## <a name="app-service-environment-v1"></a>App Service 環境 v1 ##
App Service Environment 有兩個版本：ASEv1 和 ASEv2。 hello 上述資訊為基礎 ASEv2。 此區段會顯示 hello ASEv2 ASEv1 之間的差異。

ASEv1，在您的所有資源 hello 手動管理。 含有 hello 前端、 背景工作，與用於 IP SSL 的 IP 位址。 您可以調整您的應用程式服務計劃之前，您必須向外延展 hello 背景工作集區的 toohost 它。

ASEv1 使用與 ASEv2 不同的定價模式。 在 ASEv1 中，要支付每個配置的核心， 包括用於前端或未裝載任何工作負載之背景工作角色的核心。 ASEv1，在 ase 中的 hello 預設最大標尺大小會是 55 主機總計。 包括背景工作角色與前端。 一個利用 tooASEv1 是它可以部署在傳統的虛擬網路和資源管理員的虛擬網路中。 toolearn 深入了解 ASEv1，請參閱[App Service 環境 v1 簡介][ASEv1Intro]。

toocreate ASEv1 使用資源管理員範本，請參閱[使用資源管理員範本建立 ILB ASE v1][ILBASEv1Template]。


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
