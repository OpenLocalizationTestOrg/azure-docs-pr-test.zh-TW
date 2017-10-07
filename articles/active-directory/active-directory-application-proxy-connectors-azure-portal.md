---
title: "aaaPublishing 不同網路與使用 Azure AD 應用程式 Proxy 連接器群組的位置上的應用程式 |Microsoft 文件"
description: "涵蓋如何 toocreate 和管理的 Azure AD 應用程式 Proxy 連接器群組。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>使用連接器群組在個別的網路和位置上發佈應用程式
> [!div class="op_single_selector"]
> * [Azure 入口網站](active-directory-application-proxy-connectors-azure-portal.md)
> * [Azure 傳統入口網站](active-directory-application-proxy-connectors.md)
>

客戶在越來越多的案例和應用程式中利用 Azure AD 的應用程式 Proxy。 因此我們啟用更多的拓撲使應用程式 Proxy 更具彈性。 如此您可以指定特定連接器 tooserve 特定應用程式，您可以建立應用程式 Proxy 連接器群組。 這項功能可讓您更多的控制和方式 toooptimize 您應用程式 Proxy 的部署。 

每個應用程式 Proxy 連接器會被指派 tooa 連接器群組。 所有 hello 屬於相同的連接器群組做為高可用性和負載平衡的個別單位 toohello 的連接器。 所有的連接器隸屬 tooa 連接器群組。 如果您未建立群組，則所有的連接器皆會在預設群組中。 您的系統管理員可以建立新的群組，並指派連接器 toothem hello Azure 入口網站中。 

所有應用程式會指派 tooa 連接器群組。 如果您不要建立群組，所有的應用程式會指派 tooa 預設群組。 但是，如果您組織成群組的連接器，您可以設定每個應用程式 toowork 與特定連接器群組。 在此情況下，只有該群組中的 hello 連接器服務收到要求時的 hello 應用程式。 如果您的應用程式裝載在不同的位置中，這是個很有用的功能。 您可以建立連接器群組的位置，以便應用程式一律會由實際關閉 toothem 的接點。

>[!TIP] 
>如果您有大規模的應用程式 Proxy 部署，則不會指派任何應用程式 toohello 預設連接器群組。 這樣一來，新的連接器沒有收到任何即時流量之前指派 tooan active 連接器群組。 這項設定也可讓您 tooput 連接器處於閒置模式將其移動後 toohello 預設群組，以便您可以執行維護，而不會影響您的使用者。

## <a name="prerequisites"></a>必要條件
toogroup 的連接器，您必須確定 toomake 您[安裝多個連接器](active-directory-application-proxy-enable.md)。 當您安裝新的連接器時，它也會自動加入 hello**預設**連接器群組。

## <a name="create-connector-groups"></a>建立連接器群組
使用這些步驟 toocreate 您想要的多個連接器群組。 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
1. 選取 [Azure Active Directory]  >  [企業應用程式]  >  [應用程式 Proxy]。
2. 選取 [新增連接器群組]。 hello 新連接器群組刀鋒視窗隨即出現。

   ![選取新的連接器群組](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. 指定新的連接器群組的名稱，然後使用 hello 下拉功能表 tooselect 連接器屬於此群組中。
4. 選取 [ **儲存**]。

## <a name="assign-applications-tooyour-connector-groups"></a>指派應用程式 tooyour 連接器群組
已透過應用程式 Proxy 發佈的每個應用程式均按照這些步驟處理。 當您第一次發行，或在需要時，您可以使用這些步驟 toochange hello 分派，您可以指派應用程式 tooa 連接器群組。   

1. 從 hello 管理儀表板為您的目錄，選取**企業應用程式** > **所有應用程式**> hello 想 tooassign tooa 連接器群組的應用程式 > **應用程式 Proxy**。
2. 使用 hello**連接器群組**想 hello toouse 應用程式的下拉式清單中功能表 tooselect hello 群組。
3. 選取**儲存**tooapply hello 變更。

## <a name="use-cases-for-connector-groups"></a>連接器群組的使用案例 

連接器群組可用於多種不同狀況，包括：

### <a name="sites-with-multiple-interconnected-datacenters"></a>具有多個互連資料中心的網站

許多組織都有數個彼此連接的資料中心。 在此情況下，您想讓 tookeep 盡流量 hello 資料中心內儘可能因為跨資料中心的連結是高度耗費資源而變慢。 您可以部署中每個資料中心 tooserve 只有 hello 應用程式位於 hello 資料中心內的連接器。 這種方式跨資料中心連結降到最低，並提供完全透明的經驗 tooyour 使用者。

### <a name="applications-installed-on-isolated-networks"></a>安裝在隔離網路上的應用程式

應用程式可以裝載於不屬於 hello 主要公司網路的網路。 您可以使用連接器群組 tooinstall 專用連接器隔離的網路 tooalso 隔離的應用程式 toohello 網路上。 當協力廠商為您的組織維護特定應用程式時，就會發生這種情形。 

連接器群組可讓您 tooinstall 專用的網路發佈只有特定應用程式，以更輕鬆的連接器和更安全的 toooutsource 應用程式管理 toothird 廠商所提供。

### <a name="applications-installed-on-iaas"></a>IaaS 上已安裝應用程式 

對於應用程式安裝在 IaaS 雲端存取，連接器群組提供常見服務 toosecure hello 存取 tooall hello 應用程式。 連接器群組不在您的公司網路上建立其他相依性或片段 hello 應用程式體驗。 連接器可安裝在每個雲端資料中心，而且只為該網路中的應用程式提供服務。 您可以安裝數個連接器 tooachieve 高可用性。

取得做為範例的組織有數個虛擬機器連線 tootheir 自己主控的 IaaS 虛擬網路。 tooallow 員工 toouse 這些應用程式，這些私人網路會使用站對站 VPN 連線的 toohello 公司網路。 針對位於內部部署的員工，這會提供良好的體驗。 但是，它可能不適合用來遠端員工，因為它需要額外的內部部署基礎結構 tooroute 存取，您可以看到在 hello 圖中：

![AzureAD Iaas 網路](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
與 Azure AD 應用程式 Proxy 連接器群組，您可以啟用一般服務 toosecure hello 存取 tooall 應用程式，而不需要在您的公司網路上建立其他相依性：

![AzureAD Iaas 多雲端廠商](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>多樹系 – 每個樹系不同的連接器群組

大部分已部署應用程式 Proxy 的客戶會執行 Kerberos 限制委派 (KCD) 來使用單一登入 (SSO) 功能。 tooachieve 這 hello 連接器的電腦需要 toobe 聯結的 tooa 網域，可以委派 hello 朝 hello 應用程式的使用者。 KCD 支援跨樹系功能。 但對於擁有不同的多樹系環境且它們之間沒有信任的公司來說，單一連接器無法用於所有的樹系。 

在此情況下，每個樹系，可部署特定連接器，且已發行的 tooserve 組 tooserve 應用程式只 hello 該特定樹系的使用者。 每個連接器群組代表不同的樹系。 雖然 hello 租用戶和大部分的 hello 體驗有統一適用於所有樹系中，使用者可以指派 tootheir 樹系的應用程式使用 Azure AD 群組。
 
### <a name="disaster-recovery-sites"></a>災害復原網站

您可以根據您站台的實作方式，使用災害復原 (DR) 網站採用兩種不同的方法︰

* 如果您的 DR 網站內建於主動 / 主動模式，其中與 hello 主要站台完全相同而且 hello 相同網路和 AD 設定，您可以在 hello hello DR 網站上建立 hello 連接器相同 hello 主要站台連接器群組。 這樣可以為您的 Azure AD toodetect 容錯移轉。
* 如果您的 DR 網站是分開 hello 主要站台，您可以在 hello DR 網站中，建立不同的連接器群組 1） 必須備份應用程式或 2） 手動將視轉向至 hello 現有應用程式 toohello DR 連接器群組。
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>從單一租用戶為多家公司提供服務

有許多不同的方式 tooimplement 單一服務提供者會將部署和維護 Azure AD 的模型相關的多個公司的服務。 連接器群組可協助 hello 系統管理員隔離 hello 連接器和應用程式分成不同的群組。 其中一個方法，這是適用於小型公司，是 toohave 單一雖然 hello 不同公司都有自己的網域名稱和網路的 Azure AD 租用戶。 M&A 案例和情況也是如此，其中單一 IT 部門會針對規範或企業原因為幾家公司提供服務。 

## <a name="sample-configurations"></a>範例組態

您可以實作，一些範例包括 hello 下列連接器群組。
 
### <a name="default-configuration--no-use-for-connector-groups"></a>預設組態 – 不使用連接器群組

如果您不使用連接器群組，您的組態會看起來像這樣︰

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
這個組態就對小型部署和測試就已足夠。 如果您的組織具有平面網路拓撲，則它也會正常運作。
 
### <a name="default-configuration-and-an-isolated-network"></a>預設組態和隔離的網路

此組態是 hello 預設值，這在沒有執行例如 IaaS 虛擬網路隔離網路中的特定應用程式的演進而來： 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>建議的組態 – 幾個特定的群組和預設的閒置群組

hello 建議組態的大型且複雜的組織為群組，不做任何應用程式，使用閒置或新安裝的連接器是 toohave hello 預設連接器群組。 所有應用程式會使用自訂的連接器群組來提供服務。 這可讓所有 hello 複雜度 hello 上面所述的案例。

Hello 下列範例中，在 hello 公司會有兩個資料中心，A 和 B，以提供每個站台的兩個連接器。 每個網站都有不同的應用程式在其上執行。 

![AzureAD 沒有連接器群組](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>後續步驟

* [了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)
* [啟用單一登入](application-proxy-sso-overview.md)


