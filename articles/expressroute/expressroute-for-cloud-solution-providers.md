---
title: "aaaAzure 雲端方案提供者的 ExpressRoute |Microsoft 文件"
description: "本文提供的雲端服務提供者資訊該想 tooincorporate Azure 服務和 ExpressRoute 到其供應項目。"
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>適用於雲端解決方案提供者 (CSP) 的 ExpressRoute
Microsoft 提供超小數位數傳統的轉售商 」 和 「 散發者 (CSP) toobe 無法 toorapidly 佈建的新服務和解決方案的客戶不 hello 需要 tooinvest 開發這些新服務的服務。 tooallow hello 雲端方案提供者 (CSP) hello 能力 toodirectly 管理這些新的服務，Microsoft 提供的程式及 Api，可讓 hello CSP toomanage 代表客戶的 Microsoft Azure 資源。 其中一個資源是 ExpressRoute。 ExpressRoute 可讓 hello CSP tooconnect 現有客戶資源 tooAzure 服務。 ExpressRoute 是在 Azure 中的高速私用通訊連結 tooservices。 

ExpresRoute 被組成一組的高可用性，附加的 tooa 單一客戶的訂閱並不能共用的多個客戶的電路。 每個 expressroute 電路應該終止中不同的路由器 toomaintain hello 高可用性。

> [!NOTE]
> ExpressRoute 有頻寬和連接端點，這表示大型/複雜的實作需要單一客戶有多個 ExpressRoute 電路。
> 
> 

Microsoft Azure 提供越來越多的服務，您可以提供 tooyour 客戶。  toobest 充分利用這些服務都需要 hello 使用 ExpressRoute 連線 tooprovide 高速低延遲存取 toohello Microsoft Azure 環境。

## <a name="microsoft-azure-management"></a>Microsoft Azure 管理
Microsoft 提供的 Csp Api toomanage hello Azure 客戶訂用帳戶允許以程式設計方式與您自己的服務管理系統的整合。 [這裡](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx)可以找到支援的管理功能。

## <a name="microsoft-azure-resource-management"></a>Microsoft Azure 資源管理
Hello 合約您有與您的客戶將會決定如何將管理 hello 訂用帳戶。 hello CSP 才能直接管理 hello 建立和維護的資源或 hello 客戶可維持 hello Microsoft Azure 訂用帳戶的控制，並建立 hello Azure 資源，其所需。 如果您的客戶管理的資源在其 Microsoft Azure 訂用帳戶中的 hello 建立它們會使用兩個模型的其中一個:"連線-透過 「 模型或 「 直接-目標 」 模型。 Hello 下列各節將詳細說明這些模型。  

### <a name="connect-through-model"></a>Connect-Through 模型
![替代文字](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

在 hello 連接透過模型 hello CSP 會建立您的資料中心和客戶的 Azure 訂用帳戶之間的直接連接。 使用 ExpressRoute，您的網路連線與 Azure 建立 hello 直接連線。 然後您的客戶 tooyour 網路連線。 此案例需要該 hello 客戶通過 hello CSP 網路 tooaccess Azure 服務。 

如果您的客戶有未受其他 Azure 訂用帳戶 hello 您時，它們會使用公用網際網路或自己佈建 hello 非 CSP 訂用帳戶底下的私用連接 tooconnect toothose 服務的 hello。 

管理 Azure 服務的 csp，則會假設該 hello CSP 具有先前建立的客戶識別儲存的會再複寫到 Azure Active Directory 管理其 CSP 訂用帳戶透過 Administrate-On-Behalf-Of (AOBO)。 在此案例的重要驅動程式包含其中為特定的夥伴或服務提供者建立關聯性與 hello 客戶、 hello 客戶目前使用提供者服務，或者 hello 夥伴 desire tooprovide 裝載提供者的組合與 Azure 託管解決方案 tooprovide 彈性和地址客戶面臨的挑戰這無法滿足單獨的 CSP。 此模型如下 **圖**所說明。

![替代文字](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>連接 toomodel
![替代文字](./media/expressroute-for-cloud-solution-providers/connect-to.png)

在 hello 連接 toomodel，hello 服務提供者會建立其客戶的資料中心之間的直接連線，並 hello CSP 佈建 Azure 訂用帳戶使用 ExpressRoute hello 客戶 （客戶） 透過網路。

> [!NOTE]
> Expressroute hello 客戶會需要 toocreate 和維護 hello ExpressRoute 電路。  
> 
> 

此連線的案例需要該 hello 客戶直接透過客戶網路 tooaccess CSP 管理 Azure 訂用帳戶，就會使用連接的建立、 擁有且受 hello 客戶的全部或部分直接網路連線。 這些客戶會假設 hello 提供者目前沒有建立，客戶身分識別存放區，而且 hello 提供者會將其目前的身分識別存放區到 Azure Active Directory 複寫管理的協助 hello 客戶其透過 AOBO 訂用帳戶。 此案例中的重要驅動程式包含其中為特定的夥伴或服務提供者建立關聯性與 hello 客戶、 hello 客戶目前使用提供者服務，或者 hello 夥伴完全根據 desire tooprovide 服務沒有 hello 的 azure 託管的方案需要現有的提供者資料中心或基礎結構。

![替代文字](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

hello 這些兩個選項之間選擇根據客戶的需求，且您目前必須 tooprovide Azure 服務。 hello 詳細資料，這些模型和 hello 相關聯的角色型存取控制，網路功能，並涵蓋身分識別設計模式中 hello 下列連結查看詳細資料：

* **角色型存取控制 (RBAC)** – RBAC 是以 Azure Active Directory 為基礎。  如需 Azure RBAC 的詳細資訊，請參閱 [這裡](../active-directory/role-based-access-control-configure.md)。
* **網路**– 涵蓋 hello 各種主題的 Microsoft Azure 中的網路。
* **Azure Active Directory (AAD)** – AAD 提供 hello Microsoft Azure 和第 3 個合作對象 SaaS 應用程式的身分識別管理。 如需有關 Azure AD 的詳細資訊，請參閱 [這裡](https://azure.microsoft.com/documentation/services/active-directory/)。  

## <a name="network-speeds"></a>網路速度
ExpressRoute 支援從 50 Mb/s too10Gb/s 的網路速度。 這可讓客戶 toopurchase hello 其獨特的環境所需的網路頻寬量。

> [!NOTE]
> 視需要而不會中斷的通訊，您可以增加網路頻寬，但 tooreduce hello 網路速度需要破壞 hello 循環，再重新建立 hello 較低的網路速度。  
> 
> 

ExpressRoute 支援較佳的 hello 高速連線使用率 hello 連接的多個 Vnet tooa 單一 ExpressRoute 電路。 可以在 hello 所擁有的多個 Azure 訂閱之間共用單一 ExpressRoute 電路相同的客戶。

## <a name="configuring-expressroute"></a>設定 ExpressRoute
ExpressRoute 可以設定的 toosupport 三種類型的流量 ([路由網域](#ExpressRoute-routing-domains)) 透過單一的 ExpressRoute 電路。 此流量可以分成 Microsoft 對等、Azure 公用對等和私用對等。 您可以選擇一個或所有類型的單一 ExpressRoute 線路上傳送的流量 toobe 或多個 ExpressRoute 電路的 hello ExpressRoute 電路並隔離您的客戶所需的 hello 大小而定。 hello 安全性狀態，您的客戶可能不允許公用流量，以及透過私人流量 tootraverse hello 相同電路。

### <a name="connect-through-model"></a>Connect-Through 模型
在連接透過組態 hello 您是負責 hello 網路 underpinnings tooconnect 客戶資料中心資源 toohello 訂用帳戶裝載於 Azure 中的所有項目。 每個客戶的想 toouse Azure 功能會需要的自己 ExpressRoute 連線，將受 hello 您。 hello 您將使用 hello 相同方法 hello 客戶會使用 tooprocure hello ExpressRoute 電路。 hello，您將遵循相同的步驟所述 hello 文件中的 hello [ExpressRoute 工作流程](expressroute-workflows.md)循環佈建和循環狀態。 然後，您將設定 hello 邊界閘道通訊協定 (BGP) 路由 toocontrol hello 流量流入 hello 與內部網路與 Azure vNet 之間 hello。

### <a name="connect-toomodel"></a>連接 toomodel
在連接 tooconfiguration 客戶已經有現有的連接 tooAzure 或將會起始連線 toohello 網際網路服務提供者從您的客戶自己的資料中心連結 ExpressRoute 直接 tooAzure，而不是您的資料中心。 toobegin hello 佈建程序，您的客戶將步驟 hello 如上所述 hello 連接到模型中。 一旦建立 hello 電路客戶需要 tooconfigure hello 在內部部署路由器 toobe 無法 tooaccess 您的網路和 Azure Vnet。

您可以協助設定 hello 連線並設定 hello 路由 tooallow hello 資源中您資料中心 toocommunicate hello 用戶端中的資源資料中心，或裝載於 Azure 的 hello 資源。

## <a name="expressroute-routing-domains"></a>ExpressRoute 路由網域
ExpressRoute 提供三種路由網域︰公用、私用和 Microsoft 對等。 每個 hello 路由網域都設定了高可用性的主動-主動組態中的相同路由器。 如需 ExpressRoute 路由網域的詳細資訊，請參閱 [這裡](expressroute-circuit-peerings.md)。

您可以定義的自訂路由篩選 tooallow 只有 hello 路由您想要 tooallow 或需要。 如需詳細資訊或 toosee 如何 toomake 這些變更請參閱文件：[建立和修改使用 PowerShell 的 ExpressRoute 電路的路由](expressroute-howto-routing-classic.md)如需詳細資訊 路由篩選條件。

> [!NOTE]
> Microsoft 和公用互連連線但 hello 客戶或 CSP 所擁有的公用 IP 位址，而且必須遵守 tooall 定義規則。 如需詳細資訊，請參閱 hello [ExpressRoute 必要條件](expressroute-prerequisites.md)頁面。  
> 
> 

## <a name="routing"></a>路由
ExpressRoute 連線 toohello Azure 透過 hello Azure 虛擬網路閘道的網路。 網路閘道提供 Azure 虛擬網路的路由。

建立 Azure 虛擬網路時，也會建立預設路由表 hello vNet toodirect 流量從 hello hello vNet 子網路。 如果 hello 預設路由表並不足以執行自訂的 hello 方案 tooroute 傳出流量 toocustom 應用裝置可以建立路由，或者 tooblock 路由 toospecific 子網路或外部網路。

### <a name="default-routing"></a>預設路由
hello 預設路由表包含下列路由 hello:

* 子網路內的路由
* 子網路-到-子網路 hello 虛擬網路內
* toohello 網際網路
* 使用 VPN 閘道的虛擬網路對虛擬網路路由
* 使用 VPN 或 ExpressRoute 閘道的虛擬網路對內部部署網路路由

![替代文字](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>使用者定義的路由 (UDR)
使用者定義的路由讓 hello hello 從輸出流量控制指派子網路 tooother hello 虛擬網路中的子網路，或在其中一個 hello 其他預先定義的閘道 （ExpressRoute; 網際網路或 VPN）。 hello 預設系統路由表可以取代的使用者定義路由表，以自訂路由取代 hello 預設路由表。 使用使用者定義路由時，客戶可以建立特定路由 tooappliances，例如防火牆或入侵偵測應用程式，或封鎖存取 toospecific 子網路，從裝載 hello 使用者定義路由的 hello 子網路。 如需使用者定義的路由概觀，請參閱 [這裡](../virtual-network/virtual-networks-udr-overview.md)。 

## <a name="security"></a>安全性
根據哪一個模型正在使用中，連接 tooor 連接透過您的客戶定義其 vNet 中的 hello 安全性原則，或提供 toohello CSP toodefine tootheir Vnet hello 安全性原則需求。 可以定義下列安全性準則的 hello:

1. **客戶隔離**— hello Azure 平台提供客戶隔離客戶識別碼和 vNet 資訊儲存在安全資料庫中，也就是使用的 tooencapsulate GRE 通道中的每個客戶的流量。
2. **網路安全性群組 (NSG)**規則是用來定義允許流量進出的 Azure Vnet 中的 hello 子網路。 根據預設，hello NSG 包含封鎖規則 tooblock 流量從 hello 網際網路 toohello vNet 和允許規則的 vNet 內的流量。 如需網路安全性群組的詳細資訊，請參閱 [這裡](https://azure.microsoft.com/blog/network-security-groups/)。
3. **強制通道**— 這是網際網路繫結流量源自於 Azure toobe 被重新導向到內部部署資料中心上的 hello ExpressRoute 連線 toohello 選項 tooredirect。 如需強制通道的詳細資訊，請參閱 [這裡](expressroute-routing.md#advertising-default-routes)。  
4. **加密**— 即使 hello ExpressRoute 電路專用的 tooa 特定客戶，沒有 hello 網路提供者的 hello 可能性可能會違反服務等級，允許入侵者 tooexamine 封包流量。 tooaddress 潛在、 客戶或 CSP 可以透過加密流量 hello 藉由定義所有流量流入 hello 內部部署資源和 Azure 資源 （請參閱 「 選擇性通道模式 toohello IPSec 客戶 1 之間的 IPSec 通道模式原則的連線圖 5: ExpressRoute 安全性上述)。 hello 第二個選項是 hello 的 toouse hello 每個結束點 ExpressRoute 電路的防火牆應用裝置。 這將需要額外的第 3 個合作對象防火牆 Vm 設備/toobe 安裝這兩個 ends tooencrypt hello 流量透過 hello ExpressRoute 電路。

![替代文字](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>後續步驟
hello 雲端方案提供者服務會提供值 tooyour 客戶 hello 不需要成本基礎結構和能力購買，同時維持您所在位置為 hello 主要外包提供者的方式 tooincrease。 使用 Microsoft Azure 的緊密整合，即可完成 hello CSP API，可讓您的 Microsoft Azure 中現有的管理架構的 toointegrate 管理。  

可以在 hello 下列連結查看找到的其他資訊：

[Microsoft Cloud 解決方案提供者方案](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview)。  
[取得做為雲端方案提供者的準備 tootransact](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch)。  
[Microsoft Cloud 解決方案提供者資源](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources)。

