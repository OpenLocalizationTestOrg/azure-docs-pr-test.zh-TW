---
title: "aaaCreate 外部的 Azure App Service 環境"
description: "說明如何 toocreate App Service 環境時建立的應用程式或獨立"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>建立外部 App Service 環境 #

Azure App Service Environment (ASE) 是將 Azure App Service 部署到客戶 Azure 虛擬網路 (VNet) 中子網路的一種部署。 有兩種方式 toodeploy App Service 環境 (ASE):

- 使用外部 IP 位址上的 VIP，通常稱為「外部 ASE」。
- 以內部 IP 位址上 hello VIP，通常稱為 ILB ASE 因為 hello 內部端點的內部負載平衡器 (ILB)。

本文章將示範如何 toocreate 外部 ase。 如需 hello ASE 的概觀，請參閱[簡介 toohello App Service 環境][Intro]。 如需有關如何 toocreate ILB ASE，請參閱詳細[建立並使用 ILB ASE][MakeILBASE]。

## <a name="before-you-create-your-ase"></a>建立 ASE 之前 ##

建立您 ASE 之後，您無法變更 hello 下列：

- 位置
- 訂用帳戶
- 資源群組
- 使用的 VNet
- 使用的子網路
- 子網路大小

> [!NOTE]
> 當您選擇的 VNet，並指定子網路時，請確定它是夠大 tooaccommodate 未來的成長。 我們建議使用包含 128 個位址的 `/25` 大小。
>

## <a name="three-ways-toocreate-an-ase"></a>三種方式 toocreate ase 中 ##

有三種方式 toocreate ase 中：

- **建立 App Service 方案時**。 這個方法會在一個步驟中建立 hello ASE 和 hello 應用程式服務方案。
- **作為獨立動作**。 這個方法會建立獨立 ASE，也就是任何項目的 ASE。 這個方法是更進階的程序 toocreate ase。 您使用它 toocreate ase 中搭配 ILB 一起運作。
- **從 Azure Resource Manager 範本**。 這個方法適用於進階使用者。 如需詳細資訊，請參閱[從範本建立 ASE][MakeASEfromTemplate]。

外部 ase 中都有公用 VIP，這表示所有 HTTP/HTTPS 流量 toohello 應用程式在 hello ASE 中的叫都用可存取網際網路的 IP 位址。 使用 ILB ase 中有 hello hello ASE 所使用的子網路的 IP 位址。 hello ILB ASE 中裝載的應用程式不會被公開直接 toohello 網際網路。

## <a name="create-an-ase-and-an-app-service-plan-together"></a>一起建立 ASE 和 App Service 方案 ##

hello 應用程式服務方案是應用程式的容器。 當您在 App Service 中建立應用程式時，要選擇或建立 App Service 方案。 hello 容器模型環境保存應用程式服務方案，而且應用程式服務方案保留應用程式。

toocreate ase 中建立 App Service 方案時：

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取**新增** > **Web + 行動** > **Web 應用程式**。

    ![建立 Web 應用程式][1]

2. 選取您的訂用帳戶。 hello 應用程式和 hello ASE 中建立 hello 相同訂用帳戶。

3. 選取或建立資源群組。 您可以使用資源群組來管理相關的一組 Azure 資源。 當您為應用程式建立角色型存取控制規則時，資源群組也十分實用。 如需詳細資訊，請參閱 hello [Azure 資源管理員概觀][ARMOverview]。

4. 選取 hello App Service 方案，然後選取**新建**。

    ![新增 App Service 方案][2]

5. 在 hello**位置**下拉式清單中，選取 hello 區域想 toocreate hello ASE。 如果您選取現有的 ASE，就不會建立新的 ASE。 hello 您選取的 ASE 中建立 hello 應用程式服務方案。 

6. 選取**定價層**，然後選擇其中一個 hello**隔離**定價 Sku。 如果您選擇**隔離** SKU 卡以及非 ASE 的位置，就會在該位置中建立新的 ASE。 toostart hello 程序 toocreate ase 中，選取**選取**。 hello**隔離**SKU 不只適用於搭配 ase。 您也無法在 ASE 中使用**隔離**以外的其他任何定價 SKU。

    ![定價層選取項目][3]

7. 輸入您 ASE hello 名稱。 在您的應用程式的 hello 可定址名稱中使用此名稱。 如果 hello ASE hello 名稱是_appsvcenvdemo_，hello 網域名稱是*。 appsvcenvdemo.p.azurewebsites.net*。 如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.appsvcenvdemo.p.azurewebsites.net。 您無法在 hello 名稱中使用空白字元。 如果您使用大寫字元，hello 網域名稱是 hello 總小寫版本名稱。

    ![新增 App Service 方案名稱][4]

8. 指定 Azure 虛擬網路詳細資料。 選取 [新建] 或 [選取現有]。 只有當您擁有 hello 所選資料區域中的 VNet 使用 hello 選項 tooselect 現有的 VNet。 如果您選取**新建**，輸入 hello VNet 的名稱。 會建立具有該名稱的 Resource Manager VNet。 它會使用 hello 位址空間`192.168.250.0/23`hello 所選資料區域中。 如果您選取 [選取現有]，您需要：

    a. 如果您有一個以上，請選取 hello VNet 位址區塊。

    b. 輸入新的子網路名稱。

    c. 選取 hello hello 子網路大小。 *請記住 tooselect 您 ASE 大小夠大 tooaccommodate 未來成長。* 建議是 `/25`，具有 128 個位址，而且可以處理最大大小的 ASE。 例如，不建議 `/28`，因為只有 16 個位址可供使用。 基礎結構會使用至少五個位址。 在 `/28` 子網路中，您會擁有 11 個執行個體的最大縮放比例。

    d. 選取 hello 子網路 IP 範圍。

9. 選取**建立**toocreate hello ASE。 Hello App Service 方案及 hello 應用程式，也會建立此程序。 hello ASE、 應用程式服務方案和應用程式是全部都是在 hello 相同訂用帳戶和也在 hello 相同資源群組。 如果您 ASE 需要針對個別資源群組，或需要 ILB ase 中，遵循 hello 步驟 toocreate ase 中單獨使用。

## <a name="create-an-ase-by-itself"></a>由 ASE 本身建立 ##

如果您建立 ASE 獨立，它就不會包含任何項目。 空白 ase 中仍會產生 hello 基礎結構的每月費用。 請遵循這些步驟 toocreate ase 中搭配 ILB 一起運作或 toocreate ase 中在它自己的資源群組。 建立您 ASE 之後，您可以使用 hello 一般程序中建立應用程式。 選取您新 ASE 做為 hello 位置。

1. 搜尋 hello Azure Marketplace 中的**App Service 環境**，或選取**新增** > **Web 行動** > **應用程式服務環境**。 

2. 輸入您 ASE hello 名稱。 這個名稱會用於建立 hello ASE 中的 hello 應用程式。 如果 hello 名稱*mynewdemoase*，hello 子網域名稱是*。 mynewdemoase.p.azurewebsites.net*。 如果您建立名為 mytestapp 的應用程式，則可定址於 mytestapp.mynewdemoase.p.azurewebsites.net。 您無法在 hello 名稱中使用空白字元。 如果您使用大寫字元，hello 網域名稱是 hello 總小寫版本 hello 名稱。 如果您是使用 ILB，ASE 名稱就不會用於您的子網域中，但是會在 ASE 建立期間明確指定。

    ![ASE 命名][5]

3. 選取您的訂用帳戶。 此訂用帳戶也是 hello hello ASE 中的所有應用程式使用的其中一個。 您無法將 ASE 放在另一個訂用帳戶中的 VNet。

4. 選取或指定新的資源群組。 hello 同一個用於您的 VNet 時，必須要用於您 ASE hello 資源群組。 如果您選取現有的 VNet，針對您 ASE hello 資源群組的選擇是更新的 tooreflect 的 VNet。 *您可以建立 ase 中是不同於 hello VNet 資源群組，如果您使用資源管理員範本的資源群組。* toocreate ase 中的從範本，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。

    ![資源群組選取項目][6]

5. 選取您的 VNet 和位置。 您可以建立新的 VNet 或選取現有的 VNet： 

    * 如果您選取新的 VNet，就可以指定名稱和位置。 hello 新的 VNet 有 hello 位址範圍 192.168.250.0/23 和名為 default 的子網路。 hello 子網路定義為 192.168.250.0/24。 您只能選取 Resource Manager VNet。 hello **VIP 類型**的選擇會決定是否從可以直接存取您 ASE hello 網際網路 （外部） 或如果它使用 ILB。 toolearn 進一步了解這些選項，請參閱[建立並使用 App Service 環境的內部負載平衡器][MakeILBASE]。 

      * 如果您選取**外部**hello **VIP 類型**，您可以選取多少外部 IP 位址 hello 系統會透過 IP SSL 的用途。 
    
      * 如果您選取**內部**hello **VIP 類型**，您必須指定您 ASE 使用 hello 網域。 您可以將 ASE 部署到使用公用或私人位址範圍的 VNet。 toouse 公用位址範圍的 VNet，您必須事先 toocreate hello VNet。 
    
    * 如果您選取現有的 VNet，請建立 hello ASE 時建立新的子網路。 *您無法在 hello 入口網站中使用的預先建立的子網路。如果您是使用 Resource Manager 範本，則可以使用現有的子網路建立 ASE。* toocreate ase 中的從範本，請參閱[從範本建立 App Service 環境][MakeASEfromTemplate]。

## <a name="app-service-environment-v1"></a>App Service 環境 v1 ##

您仍然可以建立 hello 第一個版本的 App Service 環境 (ASEv1) 執行個體。 處理時，搜尋 hello Marketplace 的 toostart 如**App Service 環境 v1**。 您可以建立 hello ASE 中 hello 建立 hello 獨立 ASE 相同方式。 完成後，您的 ASEv1 會有兩個「前端」和兩個「背景工作角色」。 與 ASEv1，您必須管理 hello 前端和背景工作。 當您建立 App Service 方案時，它們不會自動新增。 hello 前端做為 hello HTTP/HTTPS 端點，並且將流量傳送 toohello 背景工作。 hello 工作者是 hello 角色裝載您的應用程式。 建立您 ASE 之後，您可以調整 hello 前端和背景工作數量。 

toolearn 深入了解 ASEv1，請參閱[簡介 toohello App Service 環境 v1][ASEv1Intro]。 如需有關調整的詳細資訊，管理及監視 ASEv1，請參閱[如何 tooconfigure App Service 環境][ConfigureASEv1]。

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



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
