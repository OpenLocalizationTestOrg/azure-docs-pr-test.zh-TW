---
title: "aaaHow tooCreate ILB ASE 使用 Azure 資源管理員範本 |Microsoft 文件"
description: "了解如何 toocreate 內部負載平衡器 ASE 使用 Azure Resource Manager 範本。"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>如何 tooCreate ILB ASE 使用 Azure 資源管理員範本

> [!NOTE] 
> 這篇文章是關於 hello App Service 環境 v1。 沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
>

## <a name="overview"></a>概觀
使用虛擬網路內部位址 (而不是公用 VIP) 可以建立 App Service 環境。  此內部位址是由稱為 hello 內部負載平衡器 (ILB) 的 Azure 元件提供。  ILB ase 中可以使用 hello Azure 入口網站來建立。  也可以透過 Azure Resource Manager 範本使用自動化建立。  這篇文章會逐步 hello 步驟和語法需要 toocreate ILB ase 中使用 Azure Resource Manager 範本。

自動建立 ILB ASE 涉及三個步驟︰

1. 使用內部負載平衡器位址，而不公用 VIP 的虛擬網路中建立第一個 hello 基底 ASE。  在此步驟中，指派 toohello ILB ASE 根網域名稱。
2. Hello 建立 ILB ASE 時，SSL 憑證上傳一次。  
3. hello 已上傳的 SSL 憑證明確指派 toohello ILB ASE 做為其 「 預設 」 的 SSL 憑證。  此 SSL 憑證將用於 SSL 流量 tooapps hello ILB ASE 上時使用一般根指派網域 toohello hello ASE (例如 https://someapp.mycustomrootcomain.com) 定址 hello 應用程式

## <a name="creating-hello-base-ilb-ase"></a>建立 hello 基底 ILB ASE
在 GitHub 上 ([這裡][quickstartilbasecreate]) 可以取得範例 Azure Resource Manager 範本及其相關聯的參數檔案。

大部分的 hello 參數在 hello *azuredeploy.parameters.json*檔案是常見的 toocreating 這兩個 ILB ASEs，以及 ASEs 繫結 tooa 公用 VIP。  out 參數的特殊附註，呼叫 hello 清單或是唯一的當建立 ILB ase 中：

* *interalLoadBalancingMode*： 在大部分情況下設定此 too3，這表示這兩個連接埠 80/443 上的 HTTP/HTTPS 流量，且 hello 控制項/資料通道連接埠接聽 hello ASE tooby hello FTP 服務，將繫結的 tooan ILB 配置虛擬網路內部位址。  如果設定此屬性會改為 too2，則只有 hello FTP 服務相關會繫結連接埠 （控制和資料通道） tooan ILB 位址，雖然 hello HTTP/HTTPS 流量將會保留在 hello 公用 VIP。
* *dns 尾碼*： 這個參數會定義將會指派 toohello ASE hello 預設根網域。  在 Azure App Service hello 公用種變化，hello 預設根網域的所有 web 應用程式是*.azurewebsites.net*。  不過由於 ILB ASE 內部 tooa 客戶虛擬網路，它不會使意義 toouse hello 公開服務的預設根網域。  相反地，ILB ASE 應具有適合在公司的內部虛擬網路內使用的預設根網域。  例如，假設性的 Contoso Corporation 可能會使用預設的根網域的*內部 contoso.com*預定的 tooonly 應用程式是可解析和 Contoso 虛擬網路中存取。 
* *ipSslAddressCount*： 這個參數會自動預設 tooa 中的數值 0 hello *azuredeploy.json*檔案，因為 ILB ASEs 只能有單一的 ILB 位址。  針對 ILB ase 中，任何明確的 IP SSL 位址，因此 hello ILB ase 中的 IP SSL 位址集區必須設定 toozero，否則將會發生佈建的錯誤。 

一次 hello *azuredeploy.parameters.json*為 ILB ase 中，ILB ASE，就可以建立使用下列 Powershell 程式碼片段的 hello hello 檔填入的。  變更 hello 檔案路徑 toomatch hello Azure 資源管理員範本檔案的位置在電腦。  另請記住 toosupply 您自己的值為 hello Azure Resource Manager 部署的名稱，資源群組名稱。

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Hello Azure Resource Manager 範本提交之後會需要幾小時的 hello ILB ASE toobe 建立。  Hello 建立完成之後，hello ILB ASE 會顯示在應用程式服務環境的 hello 訂用帳戶觸發 hello 部署的 hello 清單中的 hello 入口網站 UX。

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>上傳和設定 hello"Default"SSL 憑證
一次建立 ILB ASE hello，SSL 憑證應該是相關聯 hello ASE 當做建立 SSL 連線 tooapps hello 「 預設 」 SSL 憑證的使用。  繼續 hello 假設 Contoso Corporation 範例中，如果 hello ASE 的預設 DNS 尾碼是*內部 contoso.com*，然後連接太*https://some-random-app.internal-contoso.com*需要有效的 SSL 憑證 **.internal contoso.com*。 

有各種不同的方式 tooobtain 包括內部 Ca、 購買憑證從外部的簽發者，以及使用自我簽署的憑證的有效 SSL 憑證。  Hello hello SSL 憑證的來源，不論 hello 下列憑證的屬性皆需要 toobe 正確設定：

* *主旨*： 此屬性必須設定得 **.your 根網域-here.com*
* *主體替代名稱*： 此屬性必須包含 **.your 根網域-here.com*，和 **.scm.your-根-網域-here.com*。 hello 原因 hello 第二個項目是將成為使用 hello 表單的位址與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello *your-app-name.scm.your-root-domain-here.com*。

備妥有效的 SSL 憑證，還需要兩個額外的準備步驟。  hello SSL 憑證必須 toobe 轉換/儲存為.pfx 檔案。  請記住該 hello.pfx 檔案 tooinclude 所有中繼和根憑證，並且也需要 toobe 使用密碼保護。

然後 hello 結果的.pfx 檔案需要 toobe 轉換成 base64 字串因為將使用 Azure Resource Manager 範本上載 hello SSL 憑證。  Azure Resource Manager 範本是文字檔案，因為需要 toobe 讓它可以包含為 hello 範本的參數轉換成 base64 字串 hello.pfx 檔案。

下列的 hello Powershell 程式碼片段顯示產生的自我簽署的憑證的範例，匯出 hello 憑證為.pfx 檔案，將 hello.pfx 檔案轉換成 base64 編碼字串，然後儲存 hello base64 編碼字串 tooa 個別檔案。  hello Powershell 程式碼的 base64 編碼是改自 hello [Powershell 指令碼的部落格][examplebase64encoding]。

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

已成功產生 hello SSL 憑證，並轉換的 tooa base64 編碼字串，hello 範例如 GitHub 上的 Azure Resource Manager 範本[設定 hello 預設 SSL 憑證][ configuringDefaultSSLCertificate]可用。

hello 參數在 hello *azuredeploy.parameters.json*檔案如下所示：

* *appServiceEnvironmentName*: hello 的 hello ILB ASE 正在設定的名稱。
* *existingAseLocation*： 文字字串，包含 hello hello ILB ASE 部署所在的 Azure 區域。  例如 "South Central US"。
* *pfxBlobString*: hello based64 編碼 hello.pfx 檔案的字串表示。  使用 hello 稍早所示的程式碼片段，您會複製"exportedcert.pfx.b64 」 中所包含的 hello 字串並貼上做為 hello hello 值*pfxBlobString*屬性。
* *密碼*: hello 用密碼 toosecure hello.pfx 檔案。
* *certificateThumbprint*: hello 憑證的指紋。  如果您從 Powershell 擷取這個值 (例如*$certificate。憑證指紋*hello 從先前程式碼片段)，您可以使用與 hello 值-是。  但是如果您從 hello Windows 憑證對話方塊複製 hello 值，請記得 toostrip 出 hello 無關的空格。  hello *certificateThumbprint*看起來應該像這樣： AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*： 自己選擇的好記的字串識別項使用 tooidentity hello 憑證。  hello 名稱用於一部分 hello 唯一的 Azure 資源管理員識別碼 hello *Microsoft.Web/certificates*代表 hello SSL 憑證的實體。  hello 名稱**必須**結尾 hello 下列尾碼： \_yourASENameHere_InternalLoadBalancingASE。  為指標的 hello 憑證用於保護 ILB 啟用 ase 中 hello 入口網站會使用這個後置詞。

「azuredeploy.parameters.json」  的縮寫範例如下所示︰

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

一次 hello *azuredeploy.parameters.json*檔案已滿時，可以使用下列 Powershell 程式碼片段的 hello 設定 hello 預設 SSL 憑證。  變更 hello 檔案路徑 toomatch hello Azure 資源管理員範本檔案的位置在電腦。  另請記住 toosupply 您自己的值為 hello Azure Resource Manager 部署的名稱，資源群組名稱。

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Hello Azure Resource Manager 範本提交之後它需要大約 40 分鐘 ASE 前端 tooapply hello 變更每分鐘的時間。  例如，預設值使用兩個前端，可調整大小 ASE hello 範本需要一小時和 20 分鐘 toocomplete 周圍。  執行 hello 範本時 hello ASE 將不會無法 tooscaled。  

Hello 範本完成之後，可透過 HTTPS 存取 hello ILB ASE 上的應用程式並 hello 連線將會使用 hello 預設 SSL 憑證保護。  hello 預設 SSL 憑證將用於 hello ILB ASE 上的應用程式會解決使用 hello 應用程式名稱加上 hello 預設主機名稱的組合。  例如*https://mycustomapp.internal-contoso.com*會使用 hello 預設 SSL 憑證的 **.internal contoso.com*。

不過，如同 hello 公用多租用戶的服務上執行的應用程式，開發人員可以也設定個別的應用程式的自訂主機名稱，然後再設定個別的應用程式的唯一 SNI SSL 憑證繫結。  

## <a name="getting-started"></a>開始使用
tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)

所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

