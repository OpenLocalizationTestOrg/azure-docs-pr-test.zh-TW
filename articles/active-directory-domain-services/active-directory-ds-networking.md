---
title: "Azure AD Domain Services︰網路指導方針 | Microsoft Docs"
description: "Azure Active Directory Domain Services 的網路考量"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Azure AD 網域服務的網路考量
## <a name="how-tooselect-an-azure-virtual-network"></a>如何 tooselect Azure 虛擬網路
hello 下列方針可協助您選取的虛擬網路 toouse 與 Azure AD 網域服務。

### <a name="type-of-azure-virtual-network"></a>Azure 虛擬網路類型
* 您可以啟用傳統 Azure 虛擬網路中的 Azure AD 網域服務。
* **使用 Azure Resource Manager 建立的虛擬網路無法啟用**Azure AD 網域服務。
* 您可以將資源管理員為基礎的虛擬網路 tooa 傳統虛擬網路連線 Azure AD 網域服務已啟用。 之後，您可以使用 Azure AD 網域服務中 hello 資源管理員為基礎的虛擬網路。 如需詳細資訊，請參閱 hello[網路連線](active-directory-ds-networking.md#network-connectivity)> 一節。
* **地區虛擬網路**： 如果您計劃 toouse 現有的虛擬網路，請確定它是區域虛擬網路。

  * 使用 hello 舊版同質群組機制的虛擬網路不能與 Azure AD 網域服務。
  * Azure AD 網域服務、 toouse[移轉繼承的虛擬網路 tooregional 虛擬網路](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)。

### <a name="azure-region-for-hello-virtual-network"></a>Hello 虛擬網路的 azure 地區
* 您的 Azure AD 網域服務受管理的網域部署在 hello 與 hello 選擇 tooenable hello 服務中的虛擬網路相同的 Azure 區域。
* 選取虛擬網路，其位於 Azure AD 網域服務支援的 Azure 區域中。
* 請參閱 hello[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)頁面 tooknow hello Azure AD 網域服務可用的 Azure 區域。

### <a name="requirements-for-hello-virtual-network"></a>Hello 虛擬網路需求
* **鄰近 tooyour Azure 工作負載**： 選取 hello 目前裝載/將裝載虛擬機器需要存取 tooAzure AD 網域服務的虛擬網路。
* **自訂/使-您-擁有 DNS 伺服器**： 請確認沒有任何自訂的 DNS 伺服器 hello 虛擬網路設定。
* **現有網域與 hello 相同的網域名稱**： 請確定您沒有現有的網域 hello 與該虛擬網路上可用的相同網域名稱。 比方說，假設您擁有 hello 選取的虛擬網路上呼叫 'contoso.com' 已存在的網域。 您嘗試 tooenable hello 與 Azure AD 網域服務受管理網域的更新版本中，相同的網域名稱 （亦即 'contoso.com'） 上的虛擬網路。 嘗試 tooenable Azure AD 網域服務時發生失敗。 此失敗是由於 tooname hello 網域名稱，該虛擬網路上的衝突。 在此情況下，您必須使用不同的名稱 tooset 註冊您 Azure AD 網域服務受管理的網域。 或者，可以解除佈建 hello 現有網域，然後繼續 tooenable Azure AD 網域服務。

> [!WARNING]
> Hello 服務啟用後，您無法移動網域服務 tooa 不同的虛擬網路。
>
>

## <a name="network-security-groups-and-subnet-design"></a>網路安全性群組與子網路設計
A[網路安全性群組 (NSG)](../virtual-network/virtual-networks-nsg.md)包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。 NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。 NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。 此外，流量 tooan 個別 VM 可能會限制進一步將 NSG 直接 toothat VM。

![建議的子網路設計](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>選擇子網路的最佳作法
* 部署 Azure AD 網域服務 tooa**分隔專用子網路**Azure 虛擬網路中。
* 不會套用 Nsg toohello 專用子網路的受管理的網域。 如果您必須先套用 Nsg toohello 專用子網路，請確定您**進行封鎖 hello 連接埠需要的 tooservice 及管理您的網域**。
* 不要過度限制 hello hello 專用子網路的受管理的網域內可用的 IP 位址數目。 這項限制防止 hello 服務兩個網域控制站可供受管理的網域。
* **請勿啟用 hello 閘道子網路中的 Azure AD 網域服務**的虛擬網路。

> [!WARNING]
> 當您建立關聯 NSG 與 Azure AD 網域服務中的子網路已啟用，您可能會中斷 Microsoft 的能力 tooservice 和管理 hello 網域。 此外，Azure AD 租用戶與受管理網域之間的同步處理已中斷。 **hello SLA 不適用的 toodeployments 其中 NSG 已套用該區塊的 Azure AD 網域服務更新與管理您的網域。**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Azure AD 網域服務所需的連接埠
hello 下列連接埠所需的 Azure AD 網域服務 tooservice 並維護受管理的網域。 請確定這些連接埠不會封鎖 hello 子網路已啟用受管理的網域。

| 連接埠號碼 | 目的 |
| --- | --- |
| 443 |與 Azure AD 租用戶同步處理 |
| 3389 |管理您的網域 |
| 5986 |管理您的網域 |
| 636 |安全 LDAP (LDAPS) 存取 tooyour 受管理的網域 |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>具有 Azure AD Domain Services 之虛擬網路的範例 NSG
下表中的 hello 說明範例 NSG，您可以設定虛擬網路與 Azure AD 網域服務受管理的網域。 此規則可讓您受管理的網域會保持修補、 更新和監視 Microsoft 以上面指定的連接埠 tooensure hello 的輸入的流量。 hello 預設 'DenyAll' 規則套用 tooall 其他輸入的流量的 hello 網際網路。

此外，hello NSG 也說明如何透過安全 LDAP 存取 toolock hello 網際網路。 如果您沒有透過啟用安全 LDAP 存取 tooyour 受管理的網域，hello 網際網路，略過此規則。 hello NSG 包含一組規則，允許對內的 LDAPS 存取透過 TCP 連接埠 636 只能從一組指定的 IP 位址。 hello NSG 規則 tooallow LDAPS 存取 hello 透過網際網路從指定的 IP 位址的優先順序高於 hello DenyAll NSG 規則。

![透過範例 NSG toosecure LDAPS 存取 hello 網際網路](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**更多資訊** - [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。


## <a name="network-connectivity"></a>網路連線
Azure AD 網域服務受管理網域只可在Azure 的單一傳統虛擬網路中啟用。 不支援使用 Azure Resource Manager 建立的虛擬網路。

### <a name="scenarios-for-connecting-azure-networks"></a>Azure 網路連線的案例
連接 Azure 虛擬網路 toouse hello 受管理的網域中任何 hello 下列部署案例：

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>使用 hello 管理多個 Azure 傳統虛擬網路中的網域
您可以連接其他傳統的 Azure 虛擬網路 toohello Azure 傳統的虛擬網路已啟用 Azure AD 網域服務。 此 VPN 連線可讓您 toouse hello 受管理的網域與您在其他虛擬網路中部署的工作負載。

![傳統的虛擬網路連線](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>使用資源管理員為基礎的虛擬網路中的 hello 受管理的網域
您可以連接的資源管理員為基礎的虛擬網路 toohello Azure 傳統的虛擬網路已啟用 Azure AD 網域服務。 此連線可讓您 toouse hello 受管理的網域擁有 hello 資源管理員為基礎的虛擬網路中部署您的工作負載。

![資源管理員 tooclassic 虛擬網路連線](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>網路連線選項
* **使用站對站 VPN 連線的 VNet 對 VNet 連線**： 連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting 虛擬網路 tooan 在內部部署站台位置。 這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。

    ![使用 VPN 閘道的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [詳細資訊 - 使用 VPN 閘道連接虛擬網路](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **VNet 對 VNet 連線使用虛擬網路對等互連**： 虛擬網路對等互連是一套機制 hello 中的兩個虛擬網路連接在一起，透過網路 hello Azure 中樞相同的區域。 所以，一旦 hello 兩個虛擬網路會顯示為一個供所有連接。 它們仍做為不同的資源進行管理，但這些虛擬網路中的虛擬機器可以使用私人 IP 位址彼此直接通訊。

    ![使用對等互連的虛擬網路連線](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [詳細資訊 - 虛擬網路對等互連](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>相關內容
* [Azure 虛擬網路對等互連](../virtual-network/virtual-network-peering-overview.md)
* [設定 VNet 對 VNet 連線以 hello 傳統部署模型](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Azure 網路安全性群組](../virtual-network/virtual-networks-nsg.md)
* [建立網路安全性群組](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
