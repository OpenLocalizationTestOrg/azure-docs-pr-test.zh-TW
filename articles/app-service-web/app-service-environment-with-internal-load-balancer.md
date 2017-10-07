---
title: "aaaCreating 和 App Service 環境中使用內部負載平衡器 |Microsoft 文件"
description: "搭配 ILB 建立及使用 ASE"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>搭配 App Service 環境使用內部負載平衡器

> [!NOTE] 
> 這篇文章是關於 hello App Service 環境 v1。 沒有 hello App Service 環境更容易 toouse 且功能更強大的基礎結構上執行較新版本。 有關 hello 新版本的詳細資訊以 hello 開頭的 toolearn[簡介 toohello App Service 環境](../app-service/app-service-environment/intro.md)。
>

hello 應用程式服務環境 (ASE) 功能是提供 hello 多租用戶戳記中不提供增強的組態功能的 Azure App Service 的高階服務選項。 hello ASE 功能基本上部署 Azure 應用程式服務在您的 Azure 虛擬 Network(VNet) hello。 應用程式服務環境的 hello 功能更深入瞭解提供的 toogain 讀取 hello[何謂 App Service 環境][ WhatisASE]文件。 如果您不知道的操作在 VNet 中的 hello 優點讀取 hello [Azure 虛擬網路常見問題集][virtualnetwork]。 

## <a name="overview"></a>概觀
ASE 可以使用網際網路可存取的端點或您 Vnet 中的 IP 位址加以部署。 In 順序 tooset hello IP 位址需要您具有內部的負載 Balancer(ILB) ASE toodeploy tooa VNet 位址。 當您的 ASE 是使用 ILB 設定時，您要提供：

* 您自己的網域或子網域。 toomake 它很容易，本文件假設子網域，但您可以設定兩種。 
* 使用 HTTPS 的 hello 憑證
* 您子網域的 DNS 管理。 

相對的，您可以執行以下動作：

* 裝載內部網路應用程式，例如企業營運應用程式，安全地在 hello 雲端您存取透過站台 tooSite 或 ExpressRoute 的 VPN
* 在公用 DNS 伺服器未列出 hello 雲端中的主機應用程式
* 建立與網際網路隔離，且您的前端 app 可以安全地與之整合的後端應用程式

#### <a name="disabled-functionality"></a>已停用的功能
當您使用 ILB ASE 時，有一些動作您無法執行。 這些動作包括︰

* 使用 IPSSL
* 指派的 IP 位址 toospecific 應用程式
* 購買並與透過 hello 入口網站應用程式使用的憑證。 您當然仍然可以取得直接與憑證授權單位的憑證，並使用您的應用程式，就不能透過 hello Azure 入口網站。

## <a name="creating-an-ilb-ase"></a>建立 ILB ASE
建立 ILB ASE 通常與建立 ASE 沒有太大差異。 如需建立 ase 中深入討論閱讀[如何 tooCreate App Service 環境][HowtoCreateASE]。 ILB ASE 是 hello 程序 toocreate hello 相同 ASE 建立期間建立 VNet，或選取現有的 VNet 之間。 toocreate ILB ase 中： 

1. 在 Azure 入口網站選取 hello**新增]-> [Web + 行動裝置版]-> [App Service 環境**
2. 選取您的訂用帳戶
3. 選取或建立資源群組
4. 選取或建立 VNet
5. 建立子網路 (如果選取 VNet)
6. 選取**虛擬的網路位置]-> [VNet 組態**和集 hello VIP 類型 tooInternal
7. 提供的子網域名稱 （這是用於此 ASE 中建立的應用程式的 hello 子網域）
8. 選取 [確定]，然後選取 [建立]

![][1]

Hello 虛擬網路 刀鋒視窗中沒有 VNet 組態選項。 這個選項可讓您在 [外部 VIP] 或 [內部 VIP] 之間選擇。 hello 預設值為外部。 如果您將它設定 tooExternal 您 ASE 會使用網際網路存取的 VIP。 如果您選取內部，您的 ASE 會使用您 VNet 內 IP 位址搭配 ILB 進行設定。 

選取內部之後, hello 能力 tooadd 多個 IP 位址的 tooyour ASE 已移除，改為您需要的 hello ASE tooprovide hello 子網域。 在以外部 VIP hello ase 中的 hello ASE 名稱用於 hello 子網域該 ASE 中建立的應用程式。 如果呼叫您 ASE ***contosotest***和該 ASE 中的應用程式呼叫***mytest***則 hello 子網域會是 hello 格式的***contosotest.p.azurewebsites.net***和hello 針對該應用程式的 URL 會是***mytest.contosotest.p.azurewebsites.net***。 如果您設定 hello VIP 類型 tooInternal，ASE 名稱不是 hello 子網域中的 hello ASE。 您可以明確地指定 hello 子網域。 如果您的子網域***contoso.corp.net***並進行應用程式，名為 ASE ***timereporting***然後 hello URL，該應用程式會針對***timereporting.contoso.corp.net***。

## <a name="apps-in-an-ilb-ase"></a>ILB ASE 中的 App
在 ILB ase 中建立應用程式是 hello 與通常在 ase 中建立應用程式相同。 

1. 在 Azure 入口網站選取 hello**新增]-> [Web + 行動裝置版]-> [Web**或**行動**或**API 應用程式**
2. 輸入 app 的名稱
3. 選取訂用帳戶
4. 選取或建立資源群組
5. 選取或建立 App Service 方案 (ASP)。 如果建立新的 ASP，然後選取您 ASE hello 位置和選取 hello 背景工作集區中建立您 ASP toobe 想。 當您建立 hello ASP 您選取您 ASE hello 位置和 hello 背景工作集區。 當您指定 hello 名稱，您會看到下的該 hello 子網域的 hello 應用程式的應用程式名稱取代 hello 子領域上您 ASE。 
6. 選取 [建立]。 您應該選取 hello **Pin toodashboard**核取方塊，如果您想 hello 應用程式 tooshow 儀表板上。 

![][2]

在 hello 應用程式名稱 hello 子網域名稱會取得您 ASE 更新的 tooreflect hello 子網域。 

## <a name="post-ilb-ase-creation-validation"></a>ILB ASE 建立後驗證
ILB ase 中有些許不同比 hello 非-ILB ASE。 如上所述需要 toomanage 自己的 DNS，而且您也可以 tooprovide 供 HTTPS 連線憑證。 

建立您 ASE 之後您會發現該 hello 子網域會顯示 hello 子網域，您指定，而且新的項目正在 hello**設定**功能表呼叫**ILB 憑證**。 hello ASE 會建立自我簽署憑證，使其更容易 tootest HTTPS。 hello 入口網站會告訴您針對 HTTPS 需要 tooprovide 您自己的憑證，但這是 toodrive toohave 亦會隨您的子網域的憑證。 

![][3]

如果您只嘗試項目，並不知道如何 toocreate 憑證，您可以使用 hello IIS MMC 主控台應用程式 toocreate 的自我簽署憑證。 一旦建立之後可以將它匯出為.pfx 檔案，並再將它上傳 hello ILB Certificate UI 中。 當您存取站台保護使用自我簽署憑證，您的瀏覽器會發出警告 hello 您要存取的網站，並不安全 toohello 無法 toovalidate hello 憑證到期。 如果您想 tooavoid 警告您將需要經過適當簽署的憑證符合您的子網域並具有已辨識您的瀏覽器的信任鏈結。

![][6]

如果您想 tootry hello 充滿您自己的憑證，並測試 HTTP 和 HTTPS 存取 tooyour ASE:

1. 建立 ASE 後移 tooASE UI **ASE-> 設定-> ILB 憑證**
2. 選取憑證 .pfx 檔案並提供密碼，來設定 ILB 憑證。 此步驟需要一些 tooprocess 時，且將顯示調整的作業正在進行中的 hello 訊息。
3. Hello ILB 位址取得您 ASE (**ASE]-> [屬性]-> [虛擬 IP 位址**)
4. 建立後，在 ASE 中建立 Web 應用程式 
5. 如果您還沒有該 VNET 中建立 VM (不在 hello 相同 hello ASE 或項目中斷與子網路)
6. 設定您子網域的 DNS。 您可以使用子網域中的萬用字元，在 DNS 中，或如果您想 toodo 一些簡單的測試中，編輯 hello 您 VM tooset web 應用程式名稱 tooVIP 的 IP 位址上的主機檔案。 如果您 ASE 有 hello 子網域名稱。 ilbase.com 和您所做 hello web 應用程式 mytestapp 使會位於 mytestapp.ilbase.com 然後在主機檔案中進行設定。 （在 Windows hello 主機檔案位於 C:\Windows\System32\drivers\etc\）
7. 該 VM 上使用瀏覽器並移 toohttp://mytestapp.ilbase.com （或任何 web 應用程式名稱會與您的子網域）
8. 該 VM 上使用瀏覽器，並移 toohttps://mytestapp.ilbase.com 如果使用自我簽署的憑證，您會有 tooaccept hello 缺乏安全性。 

hello 您 ILB 的 IP 位址會列為內容中 hello 虛擬 IP 位址

![][4]

## <a name="using-an-ilb-ase"></a>使用 ILB ASE
#### <a name="network-security-groups"></a>網路安全性群組
Hello 應用程式並不是可存取或甚至已知由您的應用程式的 ILB ASE 啟用網路隔離 hello 網際網路。 這非常適合用來裝載內部網路網站，例如企業營運應用程式。 如果您需要 toorestrict 存取，甚至進一步您仍然可以使用網路安全性 Groups(NSGs) toocontrol 存取在 hello 網路層級。 

如果您想 toouse Nsg toofurther 限制存取，則您需要確定未中斷 hello 通訊 toomake 該 hello ASE 需要順序 toooperate 中。 即使 hello HTTP/HTTPS 存取只能透過 hello ILB 使用 hello ASE hello ASE 仍取決於 hello VNet 外部資源。 何種網路存取權是的 toosee 仍然需要看 hello 文件中的 hello 資訊上[控制連入流量 tooan App Service 環境][ ControlInbound]和 hello 文件上的[網路透過 ExpressRoute 的 App Service 環境的組態詳細資料][ExpressRoute]。 

Azure toomanage 您 ASE 供的 tooconfigure Nsg 需要 tooknow hello IP 位址。 如果網際網路要求該 IP 位址也是從您 ASE hello 輸出 IP 位址。 針對您 ASE hello 輸出 IP 位址依然靜態您 ASE hello 存留期間。 如果您刪除並重建 ASE，您會收到新的 IP 位址。 此 IP 位址太移的 toofind**設定]-> [屬性**並尋找 hello**輸出的 IP 位址**。 

![][5]

#### <a name="general-ilb-ase-management"></a>一般 ILB ASE 管理
管理 ILB ase 中是主要 hello 與管理 ase 中通常相同。 您需要 tooscale 註冊您的背景工作集區 toohost 詳細的 ASP 執行個體，而且您前端伺服器的 HTTP/HTTPS 流量的增加 toohandle 量向上延展。 如需管理 ASE hello 組態的一般資訊，讀取 hello 文件上[設定 App Service 環境][ASEConfig]。 

hello 額外的管理項目是管理憑證和 DNS 管理。 您需要 tooobtain ILB ASE 建立之後用於 HTTPS hello 憑證上傳，並在到期之前取代它。 由於 Azure 擁有 hello 基底領域我們可以與外部 VIP ASEs 提供憑證。 由於 ILB ase 中所使用的 hello 子網域可以是任何項目，您必須 tooprovide 您自己的憑證的 HTTPS。 

#### <a name="dns-configuration"></a>DNS 組態
當使用外部 VIP hello DNS 由 Azure 管理。 在您 ASE 中建立任何應用程式會自動加入 tooAzure 即公用 DNS 的 DNS。 在 ILB ase 中您有 toomanage 自己的 DNS。 指定的子網域，像是 contoso.corp.net 您需要的 toocreate DNS A 記錄該點 tooyour ILB 位址：

    * 
    *.scm ftp 發佈 


## <a name="getting-started"></a>開始使用
所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。

tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp 服務環境][WhatisASE]

如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
