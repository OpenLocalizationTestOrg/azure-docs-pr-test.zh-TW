---
title: "aaaCreate 與使用 Azure App Service 環境的內部負載平衡器"
description: "有關如何 toocreate 和使用網際網路隔離的 Azure App Service 環境"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>建立及使用內部負載平衡器與 App Service Environment #

 Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。 有兩種方式 toodeploy App Service 環境 (ASE): 

- 使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。
- 與內部 IP 位址上 VIP，通常稱為 ILB ASE 因為 hello 內部端點的內部負載平衡器 (ILB)。 

本文章將示範如何 toocreate ILB ase。 如需 hello ASE 的概觀，請參閱[簡介 tooApp 服務環境][Intro]。 如何 toocreate 外部 ase 中，請參閱的 toolearn[建立外部 ASE][MakeExternalASE]。

## <a name="overview"></a>概觀 ##

您可以使用網際網路可存取端點或是您的 VNet 中的 IP 位址來部署 ASE。 tooset hello IP 位址 tooa VNet 位址，hello ASE 必須部署搭配 ILB 一起運作。 在部署 ASE 與 ILB 時，必須提供：

-   當您建立您的應用程式時，所使用的您自己的網域。
-   hello HTTPS 所用的憑證。
-   您的網域的 DNS 管理。

相對的，您可以執行以下動作：

-   安全地在 hello 雲端，您可以透過站對站或 Azure ExpressRoute VPN 存取主機內部網路應用程式。
-   主機的應用程式 hello 雲端中未列出的公用 DNS 伺服器。
-   建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式。

### <a name="disabled-functionality"></a>已停用的功能 ###

使用 ILB ASE 時，有一些動作您無法執行：

-   使用以 IP 為主的 SSL。
-   指派 IP 位址 toospecific 應用程式。
-   購買和使用憑證與透過 hello Azure 入口網站應用程式。 您可以直接透過「憑證授權單位」取得憑證並搭配您的應用程式使用。 您無法透過 hello Azure 入口網站來取得它們。

## <a name="create-an-ilb-ase"></a>建立 ILB ASE ##

toocreate ILB ase 中：

1. 在 hello Azure 入口網站，選取 **新增** > **Web + 行動** > **App Service 環境**。

2. 選取您的訂用帳戶。

3. 選取或建立資源群組。

4. 選取或建立 VNet。

5. 如果您選取現有的 VNet，您需要的子網路 toohold hello ASE toocreate。 請確定 tooset 子網路的大小夠大 tooaccommodate 未來成長的您 ASE。 建議的大小是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。 hello 最小的大小，您可以選取`/28`。 需要基礎結構之後，這個大小可能會縮放的 tooa 最大值為 11 的執行個體。

    * 在您的應用程式服務計劃超越 hello 的 100 個執行個體的預設最大值。

    * 調整至接近 100，但其中較多快速前端調整。

6. 選取 [虛擬網路/位置]  >  [虛擬網路設定]， 設定 hello **VIP 類型**太**內部**。

7. 輸入網域名稱。 此網域為 hello 用於此 ASE 中建立的應用程式。 有某些限制。 不能是：

    * net   

    * azurewebsites.net

    * p.azurewebsites.net

    * &lt;asename&gt;.p.azurewebsites.net

   hello 自訂網域名稱用於應用程式，供您 ASE hello 網域名稱不能重疊。 針對 ILB ase 中 hello 網域名稱與_contoso.com_，您無法使用您的應用程式，類似的自訂網域名稱：

    * www.contoso.com

    * abcd.def.contoso.com

    * abcd.contoso.com

   如果您知道您的應用程式的 hello 自訂網域名稱，選擇 不需要使用這些自訂網域名稱衝突的 ILB ASE hello 的網域。 在此範例中，您可以使用類似*contoso internal.com* hello 網域的 ASE 您因為不會衝突的自訂網域名稱結尾*。 contoso.com*。

8. 選取 [確定]，然後選取 [建立]。

    ![ASE 建立][1]

在 hello**虛擬網路**刀鋒視窗中，有**虛擬網路組態**選項。 您可以使用 tooselect 外部 VIP 或 VIP 內部。 hello 預設值是**外部**。 如果您選取 [外部]，您的 ASE 會使用一個網際網路可存取的 VIP。 如果您選取 [內部]，您的 ASE 會使用您的 VNet 內 IP 位址搭配 ILB 進行設定。

選取後**內部**，hello 能力 tooadd 多個 IP 位址的 tooyour ASE 已移除。 相反地，您需要 hello ASE tooprovide hello 的網域。 在 ase 中與外部 VIP，hello hello ASE 在 hello 網域用於該 ASE 中建立的應用程式名稱。

如果您設定**VIP 類型**太**內部**，ASE 名稱不是 hello 網域中的 hello ASE。 您可以明確地指定 hello 網域。 如果您的網域是*contoso.corp.net*和您建立的應用程式，名為 ASE *timereporting*，該應用程式是 timereporting.contoso.corp.net hello URL。


## <a name="create-an-app-in-an-ilb-ase"></a>在 ILB ASE 中建立應用程式： ##

您在中 hello ILB ase 中建立的應用程式，您建立應用程式在 ase 中正常的方式相同。

1. 在 hello Azure 入口網站，選取 **新增** > **Web + 行動** > **Web**或**行動**或**API 應用程式**。

2. 輸入 hello hello 應用程式名稱。

3. 選取 hello 訂用帳戶。

4. 選取或建立資源群組。

5. 選取或建立 App Service 方案。 如果您想 toocreate 新的 App Service 方案，請選取您 ASE 做為 hello 位置。 選取您想要建立您的應用程式服務計劃 toobe hello 背景工作集區。 當您建立 hello 應用程式服務方案時，選取您 ASE hello 位置和 hello 背景工作集區。 當您指定 hello hello 應用程式名稱時，在您的應用程式名稱的 hello 定義域已取代 hello 網域您 ASE。

6. 選取 [ **建立**]。 如果您想 hello 應用程式 tooappear 儀表板上，選取**Pin toodashboard**核取方塊。

    ![App Service 方案建立][2]

    在下**應用程式名稱**，hello 網域名稱是您 ASE 更新的 tooreflect hello 網域。

## <a name="post-ilb-ase-creation-validation"></a>ILB ASE 建立後驗證 ##

ILB ase 中有些許不同比 hello 非-ILB ASE。 如先前所述，您需要 toomanage 自己的 DNS。 您也可以 tooprovide 供 HTTPS 連線憑證。

建立您 ASE 之後，hello 網域名稱會顯示您所指定的 hello 網域。 在 [設定] 功能表中會出現新的項目 [ILB 憑證]。 hello ASE 會建立未指定 hello ILB ASE 網域的憑證。 如果您使用 hello ASE 與該憑證時，您的瀏覽器會告訴您它無效。 此憑證可讓您更輕鬆 tootest HTTPS，但您需要 tooupload 自己是繫結的 tooyour ILB ASE 網域的憑證。 無論您的憑證是自我簽署或是從憑證授權單位取得，這個步驟都是必要的。

![ILB ASE 網域名稱][3]

您的 ILB ASE 需要有效的 SSL 憑證。 使用內部憑證授權單位、向外部簽發者購買憑證、或使用自我簽署的憑證。 Hello hello SSL 憑證的來源，不論 hello 下列憑證的屬性皆需要 toobe 正確設定：

* **主旨**: too*.your 根網域-這裡必須設定這個屬性。
* **Subject Alternative Name**︰此屬性必須同時包含 *.your-root-domain-here 和 *.scm.your-root-domain-here。 與每個應用程式關聯的 SCM/Kudu 站台的 SSL 連線 toohello 使用 hello 表單的位址*your-app-name.scm.your-root-domain-here*。

轉換/儲存為.pfx 檔案 hello SSL 憑證。 hello.pfx 檔案必須包含所有中繼和根憑證。 使用密碼保護其安全。

如果您想 toocreate 自我簽署憑證，您可以在這裡使用 hello PowerShell 命令。 ILB ASE 網域名稱，而不是要確定 toouse *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

下列 PowerShell 命令產生的 hello 憑證會標示瀏覽器，因為 hello 憑證不建立您的瀏覽器信任鏈結中的憑證授權單位。 tooget 的憑證，您的瀏覽器信任，採購它從您的瀏覽器信任鏈結中的商業憑證授權單位。 

![設定 ILB 憑證][4]

tooupload 您自己的憑證及測試存取：

1. 建立 hello ASE 之後，請移 toohello ASE UI。 選取 [ASE]  >  [設定]  >  [ILB 憑證]。

2. tooset hello ILB 憑證，請選取 hello 憑證.pfx 檔案，然後輸入 hello 密碼。 這個步驟需要一些時間 tooprocess。 會出現訊息指出上傳作業正在進行中。

3. 取得您 ASE hello ILB 位址。 選取 [ASE]  >  [屬性]  >  [虛擬 IP 位址]。

4. 建立 hello ASE 之後，請在您 ASE 中建立 web 應用程式。

5. 如果您在該 VNet 中還沒有 VM，則建立 VM。

    > [!NOTE] 
    > 不在此 VM 試 toocreate hello 相同子網路，如 hello ASE，因為它將會失敗，或是會造成問題。
    >
    >

6. 設定 hello DNS ASE 網域。 您可以在您的 DNS 中使用萬用字元搭配您的網域。 toodo 一些簡單的測試，請編輯您 VM tooset hello web 應用程式名稱 toohello VIP 的 IP 位址上 hello 主機檔案：

    a. 如果您 ASE 擁有 hello 網域名稱_。 ilbase.com_並建立名為 hello web 應用程式_mytestapp_，同時解決_mytestapp.ilbase.com_。然後，您設定_mytestapp.ilbase.com_ tooresolve toohello ILB 位址。 (在 Windows 中，hello 主機檔案位於 _C:\Windows\System32\drivers\etc\_。)

    b. tootest web 部署發行或存取 toohello 進階主控台中，建立的記錄_mytestapp.scm.ilbase.com_。

7. 在該 VM 上使用瀏覽器並移至 http://mytestapp.ilbase.com 。（或移的 toowhatever web 應用程式名稱會與您的網域）。

8. 在該 VM 上使用瀏覽器並移至 https://mytestapp.ilbase.com 。如果您使用自我簽署的憑證，請接受 hello 缺乏安全性。

    hello 對於您 ILB 的 IP 位址會列示在下**IP 位址**。 這份清單也會有 hello hello 外部 VIP、 輸入的管理流量使用的 IP 位址。

    ![ILB IP 位址][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web 工作，函式和 hello ILB ASE

ILB ASE 支援函式和 web 工作，但 hello 入口 toowork 它們，您必須擁有網路存取 toohello SCM 站台。  這表示您的瀏覽器必須處於或連接 toohello 虛擬網路的主機上。  

當您使用 ILB ASE Azure 函式時，您可能會收到錯誤訊息表示 「 我們無法函式現在能夠 tooretrieve。 請稍後再試。」 Hello 函式 UI 會透過 HTTPS 運用 hello SCM 站台和 hello 根憑證不在 hello 瀏覽器信任鏈結，就會發生這個錯誤。 Web 工作具有類似的問題。 tooavoid 這個問題，您可以執行 hello 下列其中一項：

- 新增 hello 憑證 tooyour 受信任的憑證存放區。 這會解除封鎖 Edge 及 Internet Explorer。
- 使用 Chrome 第一次移 toohello SCM 站台、 接受 hello 受信任的憑證並前往 toohello 入口網站。
- 使用瀏覽器信任鏈結中的商業憑證。  這是 hello 最佳選項。  

## <a name="dns-configuration"></a>DNS 組態 ##

當您使用外部 VIP 時，hello DNS 是由 Azure 中管理。 在您 ASE 中建立任何應用程式會自動加入 tooAzure DNS，這是公用的 DNS。 在 ILB ASE 中，您必須管理您自己的 DNS。 針對指定的網域，例如_contoso.net_，您需要的 toocreate DNS A 記錄在 DNS 中針對該點 tooyour ILB 位址：

- *.contoso.net
- *.scm.contoso.net

如果 ILB ASE 網域來進行多項功能，此 ASE 之外，您可能需要 toomanage DNS 以每個應用程式名稱為基礎。 這個方法很困難，因為時，您需要 tooadd 每個新的應用程式名稱在您的 DNS 中建立它。 基於這個理由，建議使用專用網域。

## <a name="publish-with-an-ilb-ase"></a>使用 ILB ASE 發佈 ##

每一個建立的應用程式，都有兩個端點。 在 ILB ASE 中，您有 &lt;app name>.&lt;ILB ASE Domain> 和 &lt;app name>.scm.&lt;ILB ASE Domain>。 

hello SCM 網站名稱會採用您 toohello Kudu 主控台中，稱為 hello**進階入口網站**內 hello Azure 入口網站。 hello Kudu 主控台可讓您檢視環境變數中，瀏覽 hello 磁碟，請使用主控台，以及執行更多。 如需詳細資訊，請參閱 [Azure App Service 的 Kudu 主控台][Kudu]。 

在 hello 多租用戶應用程式服務和外部 ase 中，沒有單一登入 Azure 入口網站的 hello 與 hello Kudu 主控台之間的功能。 Hello ILB ASE，不過，您需要 toouse 發行的憑證 toosign hello Kudu 主控台。

以網際網路為基礎 CI 系統，例如 GitHub 和 Visual Studio Team Services，不使用 ILB ASE 因為 hello 發行端點無法存取網際網路。 相反地，您需要 toouse 使用提取模型，例如 Dropbox 的 CI 系統。

hello ILB ASE 中的應用程式的發行端點會使用 ILB ASE 建立與該 hello hello 網域。 此網域會出現在 hello 應用程式發行設定檔和 hello 應用程式的入口網站的刀鋒視窗 (**概觀** > **Essentials**以及**屬性**)。 如果您有與 hello 子網域 ILB ASE *contoso.net*和應用程式命名*mytest*，使用*mytest.contoso.net* ftp 和*mytest.scm.contoso.net*用於 web 部署。

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>將 ILB ASE 與 WAF 裝置耦合 ##

Azure App Service 提供許多保護 hello 系統的安全性措施。 它們也可以協助 toodetermine 是否已遭竊取應用程式。 hello 最佳保護 web 應用程式是 toocouple 裝載平台，Azure 應用程式服務，例如 web 應用程式防火牆 (WAF)。 因為 hello ILB ASE 的網路隔離的應用程式端點，所以很適合這樣的使用。

深入了解如何 tooconfigure 程式的 ILB ASE WAF 裝置，請參閱 toolearn[使用 App Service 環境設定 web 應用程式防火牆][ASEWAF]。 本文將說明如何 toouse Barracuda 虛擬應用裝置與您 ASE。 另一個選項是 toouse Azure 應用程式閘道。 應用程式閘道會使用任何應用程式放在它後面的 hello OWASP 核心規則 toosecure。 如需應用程式閘道的詳細資訊，請參閱[簡介 toohello Azure web 應用程式防火牆][AppGW]。

## <a name="get-started"></a>開始使用 ##

中都提供所有發行項和 ASEs 的方式-tooinstructions [App Service 環境的讀我檔案][ASEReadme]。

* tooget 入門 ASEs，請參閱[簡介 tooApp 服務環境][Intro]。
* 如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/)。
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
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
