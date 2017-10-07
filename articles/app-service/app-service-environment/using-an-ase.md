---
title: "aaaUse Azure App Service 環境"
description: "如何發佈 toocreate，，和在 Azure App Service 環境調整應用程式"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>使用 App Service Environment #

## <a name="overview"></a>概觀 ##

Azure App Service Environment (ASE) 是 Azure App Service 到客戶之 Azure 虛擬網路中子網路的部署。 其中包括：

- **前端結束**: hello 前端是 HTTP/HTTPS 終止的 App Service 環境 (ASE) 中的位置。
- **工作者**: hello 背景工作可以裝載應用程式的 hello 資源。
- **資料庫**: hello 資料庫會保留定義 hello 環境的資訊。
- **儲存體**: hello 儲存體就是使用的 toohost hello 客戶發行應用程式。

> [!NOTE]
> App Service Environment 有兩個版本：ASEv1 和 ASEv2。 中 ASEv1，您必須管理 hello 資源，才能使用它們。 toolearn 如何 tooconfigure 和管理 ASEv1，請參閱[設定 App Service 環境 v1][ConfigureASEv1]。 hello 本文其餘部分著重於 ASEv2。
>
>

您可以使用適用於應用程式存取的外部 VIP 或內部 VIP，來部署 ASE (ASEv1 和 ASEv2)。 hello 與外部 VIP 的部署通常稱為外部 ase。 因為它會使用內部負載平衡器 (ILB)，會呼叫 hello ILB ASE hello 內部版本。 請參閱深入了解 hello ILB ASE toolearn[建立並使用 ILB ASE][MakeILBASE]。

## <a name="create-a-web-app-in-an-ase"></a>在 ASE 中建立 Web 應用程式 ##

toocreate 在 ase 中的 web 應用程式，您使用的 hello 相同的處理序，做為您建立時就一般來說，但有一些小差異。 當您建立新的 App Service 方案時：

- 而不是選擇的地理位置在哪一個 toodeploy 您的應用程式，您可以選擇 ase 中做為位置。
- 在 ASE 中建立的所有 App Service 方案必須在「隔離」定價層中。

如果您沒有 ase 中，您可以建立一個遵照中的 hello[建立 App Service 環境][MakeExternalASE]。

toocreate web 應用程式在 ase 中：

1. 選取 [新增] > [Web + 行動] > [Web 應用程式]。

2. 輸入 hello web 應用程式的名稱。 如果您已經在 ase 中選取的應用程式服務計劃，hello hello 應用程式的網域名稱會反映 hello ASE hello 網域名稱。

    ![選取 Web 應用程式名稱][1]

3. 選取一個訂用帳戶。

4. 輸入新的資源群組的名稱，或選取**使用現有**和從 hello 下拉式清單中選取一個。

5. 選取 ASE 中現有的 App Service 方案，或透過下列步驟建立一個新的方案：

    a. 選取 [新建]。

    b. 輸入您 App Service 方案的 hello 名稱。

    c. 選取您 ASE 中 hello**位置**下拉式清單。

    d. 選取 [隔離] 定價層。 選取 [選取] 。

    e. 選取 [確定] 。
    
    ![隔離定價層][2]

6. 選取 [ **建立**]。

## <a name="how-scale-works"></a>調整方式 ##

每個 App Service 應用程式都會在 App Service 方案中執行。 hello 容器模型是環境保存應用程式服務方案和應用程式服務方案保留應用程式。 當您調整應用程式時，您和調整其規模 hello 應用程式服務計劃因此縮放 hello hello 的所有應用程式相同的計劃。

在 ASEv2，當您調整 App Service 方案，也會自動加入 hello 所需的基礎結構。 沒有時間延遲 tooscale 作業時就會加入 hello 基礎結構。 ASEv1，hello 所需的基礎結構必須加入您才能建立或擴充您的應用程式服務方案。 

在 hello 多租用戶應用程式服務，縮放比例是立即通常因為資源集區是隨時可用 toosupport 它。 ASE 中沒有這類緩衝區，並在需要時配置資源。

在 ase 中，您可以調整 too100 執行個體。 這 100 個執行個體可以全都位於單一 App Service 方案中，或分散於多個 App Service 方案。

## <a name="ip-addresses"></a>IP 位址 ##

App Service 必須 hello 能力 tooallocate 專用的 IP 位址 tooan 應用程式。 這項功能可設定以 IP 為主的 SSL 之後, 中所述[繫結現有自訂 SSL 憑證 tooAzure web 應用程式][ConfigureSSL]。 但是，在 ASE 中，有一個明顯的例外。 您無法加入其他 IP 位址 toobe 用於 ILB ASE 以 IP 為主的 SSL。

在 ASEv1，您需要 tooallocate hello IP 位址做為資源才能使用它們。 ASEv2，在您使用它們從您的應用程式就像您一樣 hello 多租用戶應用程式服務中。 一定會有一個備用位址 ASEv2 中向上 too30 IP 位址。 每次您使用一個位址時，就會新增另一個位址，如此一律會有立即可供使用的位址。 需要的時間延遲是 tooallocate 另一個 IP 位址，不會新增 IP 位址快速連續。

## <a name="front-end-scaling"></a>前端調整大小 ##

在 ASEv2，當您擴充您的應用程式服務計劃，背景工作會自動加入 toosupport 它們。 每個 ASE 建立時都會包含兩個前端。 此外，hello 前端自動向外延展速率為每隔 15 的執行個體的一個前端應用程式服務方案中。 例如，如果您有 15 個執行個體，則會有三個前端。 如果縮放 too30 執行個體時，您會有四個最上層結束，以此類推。

這個前端數目應該足以適用於大部分情況。 但是，您也可用更快的速率相應放大。 您可以變更為每五個執行個體的一個前端低 tooas hello 比率。 沒有變更 hello 比例收取費用。 如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。

前端資源是 hello ASE hello HTTP/HTTPS 端點。 Hello 預設前端組態，每個前端記憶體使用量持續約為 60%。 客戶工作負載不會在前端上執行。 hello 前端與尊重 tooscale 的關鍵因素是 hello CPU 驅動主要是由 HTTPS 流量。

## <a name="app-access"></a>應用程式存取 ##

在外部 ase 中，建立應用程式時所使用的 hello 網域與不同 hello 多租用戶應用程式服務的。 它包括 hello ASE hello 名稱。 如需有關如何 toocreate 外部 ase 中，請參閱[建立 App Service 環境][MakeExternalASE]。 hello 網域名稱，在外部 ase 中看起來像*。&lt;asename&gt;。 p.azurewebsites.net*。 例如，如果您 ASE 名為_外部 ase_和裝載應用程式呼叫_contoso_該 ASE 中，在您連線到它在 hello 下列 Url:

- contoso.external-ase.p.azurewebsites.net
- contoso.scm.external-ase.p.azurewebsites.net

hello URL contoso.scm.external ase.p.azurewebsites.net 使用的 tooaccess hello Kudu 主控台或使用 web 應用程式部署發行。 Hello Kudu 主控台上的資訊，請參閱[Azure App Service 的 Kudu 主控台][Kudu]。 hello Kudu 主控台可讓您 web UI 的偵錯、 上傳檔案、 編輯檔案，以及執行更多。

在 ILB ase 中，您會在部署期間判斷 hello 網域。 如需有關如何 toocreate ILB ASE，請參閱[建立並使用 ILB ASE][MakeILBASE]。 如果您指定 hello 網域名稱_ilb ase.info_，hello 應用程式，ASE 應用程式建立期間可以使用該網域。 Hello 應用程式名為_contoso_，hello url:

- contoso.ilb-ase.info
- contoso.scm.ilb-ase.info

## <a name="publishing"></a>發佈 ##

如同 hello 多租用戶應用程式服務，在 ase 中您可以將發行使用：

- Web 部署。
- FTP。
- 持續整合。
- 拖放在 hello Kudu 主控台。
- IDE，例如 Visual Studio、Eclipse 或 IntelliJ IDEA。

與外部 ase 中，這些行為的發行選項 hello 相同。 如需詳細資訊，請參閱[在 Azure App Service 中部署][AppDeploy]。 

hello 與發行的主要差異是尊重 tooan ILB ASE。 ILB ase 中，與 hello 發行端點則是只能透過 hello ILB 所有可用項目。 hello ILB 會位於 hello 虛擬網路中的 hello ASE 子網路中的私人 IP。 如果您沒有網路存取 toohello ILB，您無法發行該 ASE 上的任何應用程式。 如中所述[建立並使用 ILB ASE][MakeILBASE]，hello 應用程式需要 tooconfigure DNS hello 系統中。 其中包含 hello SCM 端點。 如果未正確定義它們，就無法發佈。 您的 Ide 也需要 toohave 網路存取 toohello ILB 順序 toopublish 中的直接 tooit。

以網際網路為基礎 CI 系統，例如 GitHub 和 Visual Studio Team Services，不使用 ILB ASE 因為 hello 發行端點不是可存取網際網路。 相反地，您需要 toouse 使用提取模型，例如 Dropbox 的 CI 系統。

hello ILB ASE 中的應用程式的發行端點會使用 ILB ASE 建立與該 hello hello 網域。 您可以在 hello 應用程式發行設定檔和 hello 應用程式的入口網站的刀鋒視窗中看到它 (在**概觀** > **Essentials**同時也位於**屬性**)。 

## <a name="pricing"></a>價格 ##

定價 SKU 呼叫 hello**隔離**建立 ASEv2 只能搭配使用。 所有裝載於 ASEv2 的應用程式服務計劃已 hello 定價 SKU 的隔離。 隔離的 App Service 方案費率會因區域而有所不同。 

此外 toohello 價格為您的應用程式服務計劃，ASE 本身一般速率。 hello 一般速率不會變更您 ASE hello 大小及支付 hello ASE 基礎結構在調整率 1 其他預設值的前端每隔 15 的 App Service 方案執行個體。  

如果 hello 預設小數位數率 1 前端每隔 15 的 App Service 方案執行個體不是速度不夠快，您可以調整 hello 比率前端加入或是 hello hello 前端的大小。  當您調整 hello 比例或大小時，您需支付不會加入預設的 hello 前端核心。  

例如，如果您調整 hello 小數位數的比率 too10，前端會加入每 10 個執行個體的 App Service 方案中。 hello 一般費用涵蓋一個前端每隔 15 的執行個體的小數位數速率。 小數位數的比率較 10，您需支付費用 hello 第三個前端加入 hello 10 App Service 方案執行個體。 您無須 toopay，當您到達 15 的執行個體，因為它已自動加入。

如果您已調整的 hello 前端 too2 核心 hello 大小，但不是會調整 hello 比率則您需支付 hello 額外的核心。  2 前端，所以即使 hello 自動調整臨界值以下您願意支付額外的 2 核心如果增加 hello 大小 too2 核心前端建立 ase。

如需詳細資訊，請參閱 [Azure App Service 價格][Pricing]。

## <a name="delete-an-ase"></a>刪除 ASE ##

toodelete ase 中： 

1. 使用**刪除**頂端的 hello hello **App Service 環境**刀鋒視窗。 

2. 輸入您想 toodelete 您 ASE tooconfirm hello 名稱它。 當您刪除 ase 中時，會刪除所有的 hello 內容以及。 

    ![ASE 刪除][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
