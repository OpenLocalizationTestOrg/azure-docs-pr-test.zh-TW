---
title: "在 Azure 中的 Directory Federation Services aaaActive |Microsoft 文件"
description: "本文件中，您將學習如何 toodeploy AD FS 在 Azure 中的高可用性。"
keywords: "部署在 azure 中的 AD FS 部署 azure adfs、 azure adfs、 azure ad fs、 部署 adfs、 部署 ad fs，在 azure 中的 adfs、 部署在 azure 中的 adfs、 部署 AD FS 在 azure、 adfs azure、 簡介 tooAD FS、 Azure、 在 Azure 中，AD FS iaas，ADFS，移動 adfs tooazure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>在 Azure 中部署 Active Directory 同盟服務
AD FS 提供簡化、安全的身分識別同盟和 Web 單一登入 (SSO) 功能。 Azure AD 的同盟，或 O365 可讓的使用者 tooauthenticate 使用內部部署認證，並存取雲端中的所有資源。 如此一來，它變得很重要 toohave 高可用性的 AD FS 基礎結構 tooensure 存取 tooresources 這兩個內部部署和 hello 雲端中。 Azure 中部署 AD FS 可協助達到所需要的最小的投入時間的 hello 高可用性。
在 Azure 中部署 AD FS 有幾項優點，以下列出其中幾點︰

* **高可用性**-確定 hello Azure 可用性設定組的強大功能與高可用性的基礎結構。
* **輕鬆 tooScale** – 需要更多的效能？ 輕鬆地移轉在 Azure 中的幾個點擊 toomore 功能強大的機器
* **跨地理備援性**– 具有 Azure 地理備援您可以確保您的基礎結構是高可用性，跨 hello 球體
* **輕鬆 tooManage** – 高度簡化的管理選項，在 Azure 入口網站，管理您的基礎結構就非常簡單容易造成困擾 

## <a name="design-principles"></a>設計原則
![部署設計](./media/active-directory-aadconnect-azure-adfs/deployment.png)

hello 上圖顯示 hello 建議部署在 Azure AD FS 基礎結構的基本拓樸 toostart。 hello 背後的 hello 原則 hello 拓撲的各種元件如下：

* **DC/ADFS 伺服器**︰如果您的使用者人數少於 1,000 名，可以直接在網域控制站上安裝 AD FS 角色。 若不想讓任何 hello 網域控制站上的效能影響，或如果您有超過 1,000 個使用者，然後將部署在不同伺服器上的 AD FS。
* **WAP 伺服器**– 它是必要 toodeploy Web 應用程式 Proxy 伺服器，以便使用者可以連線到的 AD FS 時不 hello 公司網路也 hello。
* **DMZ**: hello Web 應用程式 Proxy 伺服器將會放置於 hello DMZ 和 hello 周邊網路與 hello 內部子網路之間允許只有 TCP/443 存取。
* **負載平衡器**: tooensure 的 AD FS 和 Web 應用程式 Proxy 伺服器的高可用性，建議使用 AD FS 伺服器和 Azure 負載平衡器的內部負載平衡器的 Web 應用程式 Proxy 伺服器。
* **可用性設定組**: tooprovide 備援 tooyour AD FS 部署，建議您分組類似的工作負載的可用性設定組中的兩個或多個虛擬機器。 這項組態可以確保在規劃或未規劃的維護事件發生期間，至少有一部虛擬機器可以使用。
* **儲存體帳戶**： 建議 toohave 兩個儲存體帳戶。 具有單一儲存體帳戶可能會導致 toocreation 的單一失敗點，而且可能會導致 hello 部署 toobecome hello 儲存體帳戶會關閉不太可能案例中無法使用。 兩個儲存體帳戶則有助於讓每條故障路線有一個相關聯的儲存體帳戶。
* **網路隔離**︰請將 Web 應用程式 Proxy 伺服器部署在不同的 DMZ 網路。 您可以將一個虛擬網路分割成兩個子網路，然後再部署隔離的子網路中的 hello Web 應用程式 Proxy 伺服器。 您只可以 hello 網路安全性設定群組的每個子網路，並允許 hello 兩個子網路所需的溝通。 下面會提供每種部署案例的其他詳細資料

## <a name="steps-toodeploy-ad-fs-in-azure"></a>步驟 toodeploy 在 Azure 中的 AD FS
此章節大綱 hello 指南 toodeploy hello 以下所述的 hello 步驟所述在 Azure 中的 AD FS 基礎結構。

### <a name="1-deploying-hello-network"></a>1.部署的 hello 網路
如上所述，您可以在單一虛擬網路中建立兩個子網路，或是建立兩個完全不同的虛擬網路 (VNet)。 本文內容著重於部署單一虛擬網路，再將它分成兩個子網路。 這是目前比較簡單的方式，因為兩個個別的 Vnet 需要 VNet tooVNet 閘道進行通訊。

**1.1 建立虛擬網路**

![建立虛擬網路](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Hello Azure 入口網站，在選取的虛擬網路，而且您可以部署 hello 虛擬網路和立即以只要按一下的一個子網路。 INT 子網路也有定義，而且可供立即 Vm toobe 加入。
hello 下一個步驟是 tooadd 另一個子網路 toohello 網路，也就是 hello 周邊網路的子網路。 toocreate hello 周邊網路的子網路，只需

* 選取新建立的 hello 網路
* 在 hello 內容中，選取 子網路
* 在 hello 子網路 面板中，按一下 hello 加入按鈕
* 提供 hello 子網路名稱和位址空間資訊 toocreate hello 子網路

![子網路](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![子網路 DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2.建立 hello 網路安全性群組**

網路安全性群組 (NSG) 包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。 NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。 NSG 與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。
基於本指南的 hello 目的，我們將建立兩個 Nsg： 分別指派給內部網路以及周邊網路。 其各自的標籤為 NSG_INT 和 NSG_DMZ。

![建立 NSG](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

NSG 建立的 hello 之後, 會有 0 輸入和 0 輸出規則。 一旦 hello 角色 hello 個別伺服器上的安裝且正常運作，然後 hello 輸入和輸出規則才能進行相應的 toohello 所需的安全性層級。

![初始化 NSG](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

建立 hello Nsg 之後，建立與子網路關聯 NSG_INT INT 和 NSG_DMZ 與周邊網路的子網路。 下面提供了範例螢幕擷取畫面︰

![NSG 設定](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* 按一下 子網路的子網路 tooopen hello 面板上
* 選取以 hello NSG hello 子網路 tooassociate 

完成設定後，子網路的 hello 面板看起來應該像下面：

![NSG 之後的子網路](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3.建立 tooon 內部部署連線**

我們需要連接 tooon 內部部署的順序 toodeploy hello 網域控制站 (DC) 在 azure 中。 Azure 提供各種連線選項 tooconnect 您在內部部署基礎結構 tooyour Azure 基礎結構。

* 點對站
* 虛擬網路站對站
* ExpressRoute

建議 toouse ExpressRoute。 ExpressRoute 可讓您在 Azure 資料中心和內部部署或共置環境中的基礎結構之間建立私人連接。 ExpressRoute 連線不會經過 hello 公用網際網路。 它們提供更多的可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。
雖然建議 toouse ExpressRoute，您可以選擇最適合貴組織的任何連線方法。 深入了解 ExpressRoute 和 hello toolearn 各種連線選項，使用 ExpressRoute，讀取[ExpressRoute 技術概觀](https://aka.ms/Azure/ExpressRoute)。

### <a name="2-create-storage-accounts"></a>2.建立儲存體帳戶
順序 toomaintain 高可用性和避免依賴單一儲存體帳戶，您可以建立兩個儲存體帳戶。 每個可用性設定組中的 hello 機器分成兩個群組，然後指派每個群組個別的儲存體帳戶。

![建立儲存體帳戶](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3.建立可用性設定組
針對每個角色 （DC/AD FS 和 WAP），建立可用性設定組包含 2 機器每個在 hello 最小。 這有助於讓每個角色達到更高的可用性。 建立 hello 可用性設定組，而是在 hello 下列重要 toodecide:

* **故障網域**： 中的虛擬機器 hello 相同容錯網域共用相同電源和實體網路交換器 hello。 建議最少準備 2 個容錯網域。 hello 預設值為 3，您可以讓它保持原狀針對此部署的 hello 用途
* **更新網域**： 屬於的 toohello 更新期間一起重新相同更新網域的機器。 您想 toohave 最小值為 2 的更新網域。 hello 預設值為 5，您可以讓它保持原狀針對此部署的 hello 用途

![可用性集合](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

建立 hello 下列可用性設定組

| 可用性設定組 | 角色 | 容錯網域 | 更新網域 |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4.部署虛擬機器
hello 下一個步驟是 toodeploy 會裝載基礎結構中的 hello 不同角色的虛擬機器。 每個可用性設定組中建議至少要有兩部機器。 建立 hello 基本部署的四個虛擬機器。

| 機器 | 角色 | 子網路 | 可用性設定組 | 儲存體帳戶 | IP 位址 |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |靜態 |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |靜態 |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |靜態 |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |靜態 |

您可能已注意到我們還未指定 NSG。 這是因為 azure 可讓您使用 NSG hello 子網路層級。 然後，您可以使用個別的 NSG 相關聯是 hello 子網路，否則 hello NIC 物件 hello 控制機器網路流量。 如需詳細資訊，請閱讀 [什麼是網路安全性群組 (NSG)](https://aka.ms/Azure/NSG)。
如果您要管理 hello DNS，建議使用靜態 IP 位址。 您可以使用 Azure DNS，並改為在 hello 網域的 DNS 記錄，請參閱其 Azure Fqdn toohello 新機器。
虛擬機器窗格看起來應該像下面 hello 部署完成之後：

![虛擬機器已部署](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5.設定 hello 網域控制站 / AD FS 伺服器
 在訂單 tooauthenticate 任何內送要求，AD FS 需要 toocontact hello 網域控制站。 toosave hello 昂貴的路線，從 Azure tooon 內部部署 DC 驗證，建議 toodeploy hello Azure 中的網域控制站的複本。 在訂單 tooattain 高可用性，建議您 toocreate 至少 2 的網域控制站的可用性設定組。

| 網域控制站 | 角色 | 儲存體帳戶 |
|:---:|:---:|:---:|
| contosodc1 |複本 |contososac1 |
| contosodc2 |複本 |contososac2 |

* 將 hello 兩部伺服器升級為複本網域控制站與 DNS
* 設定 hello AD FS 伺服器安裝使用 hello 伺服器管理員的 hello AD FS 角色。

### <a name="6-deploying-internal-load-balancer-ilb"></a>6.部署內部負載平衡器 (ILB)
**6.1.建立 hello ILB**

toodeploy ILB，在 hello Azure 入口網站並按一下選取的負載平衡器加 （+）。

> [!NOTE]
> 如果您沒有看到**負載平衡器**程式功能表中，按一下**瀏覽**hello 在左下方的 hello 入口網站和捲動，直到您看到**負載平衡器**。  然後按一下 hello 黃色星號 tooadd 它 tooyour 功能表。 現在選取 hello 新增負載平衡器圖示 tooopen hello 面板 toobegin 組態的 hello 負載平衡器。
> 
> 

![瀏覽負載平衡器](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **名稱**： 授與任何適合的名稱 toohello 負載平衡器
* **配置**： 因為此負載平衡器將會放在 hello AD FS 伺服器前面，而是內部網路連線，請選取 「 內部 」
* **虛擬網路**： 選擇您要在其中部署 AD FS 的 hello 虛擬網路
* **子網路**： 選擇這裡 hello 內部的子網路
* **IP 位址指派**：靜態

![內部負載平衡器](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

按一下 之後建立和部署 hello ILB，您應該會看到它的負載平衡器的 hello 清單中：

![ILB 之後的負載平衡器](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

下一個步驟是 tooconfigure hello 後端集區和 hello 後端探查。

**6.2.設定 ILB 後端集區**

選取新建立的 ILB hello 負載平衡器面板中的 hello。 它會開啟 hello 設定面板。 

1. 選取從 hello 設定面板的後端集區
2. Hello 中加入 後端集區面板，請按一下 新增虛擬機器
3. 此時您會看到一個面板供您選擇可用性設定組
4. 選擇 AD FS hello 可用性設定組

![設定 ILB 後端集區](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3.設定探查**

在 hello ILB 設定面板中，選取 探查。

1. 按一下 [新增]
2. 提供探查的詳細資料 a. **名稱**︰探查名稱 b. **通訊協定**：TCP c. **連接埠**：443 (HTTPS) d. **間隔**: 5 （預設值）-這是 ILB 將在其中探查 hello 後端集區 e 中的 hello 機器 hello 間隔。 **狀況不良閾值限制**: 2 （預設 val ue） – 這是連續探查失敗之後 ILB 會宣告機器 hello 後端集區無回應，並會停止傳送流量 tooit hello 臨界值。

![設定 ILB 探查](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4.建立負載平衡規則**

順序 tooeffectively 平衡 hello 流量應負載平衡規則與設定 hello ILB。 在訂單 toocreate 負載平衡規則 

1. 選取負載平衡規則和 hello hello ILB 設定面板
2. 按一下 加入在 hello 負載平衡規則面板
3. Hello 新增負載平衡規則面板。 **名稱**： 提供 hello 規則 b 的名稱。 **通訊協定**︰選取 [TCP] c. **連接埠**：443 d. **後端連接埠**：443 e. **後端集區**： 選取您建立 hello AD FS 叢集舊版 f 的 hello 集區。 **探查**： 稍早建立的 AD FS 伺服器選取 hello 探查

![設定 ILB 平衡規則](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5.更新 ILB 的 DNS**

請 tooyour DNS 伺服器，並建立 hello ILB CNAME。 hello CNAME 應 hello federation service 與 hello 指向 hello ILB toohello IP 位址的 IP 位址。 如果 hello ILB DIP 位址是 10.3.0.8，且已安裝的 hello 同盟服務的範例為 fs.contoso.com，然後建立指向 too10.3.0.8 fs.contoso.com 的 CNAME。
這會確保所有 fs.contoso.com 最後會在 hello ILB 有關的通訊，而且也適當地路由都傳送。

### <a name="7-configuring-hello-web-application-proxy-server"></a>7.設定 hello Web Application Proxy 伺服器
**7.1.設定 hello Web 應用程式 Proxy 伺服器 tooreach AD FS 伺服器**

中的 Web 應用程式 Proxy 伺服器後方 hello ILB 能夠 tooreach hello AD FS 伺服器的順序 tooensure，建立 hello ILB 的 hello %systemroot%\system32\drivers\etc\hosts 中的記錄。 請注意，hello 辨別的名稱 (DN) 應該 hello federation service 名稱，例如 fs.contoso.com。而且 hello IP 項目應該 hello ILB 的 IP 位址 (10.3.0.8 hello 範例所示)。

**7.2.安裝 hello Web 應用程式 Proxy 角色**

確定的 Web 應用程式 Proxy 伺服器後方 ILB 能夠 tooreach hello AD FS 伺服器之後，您接下來可以安裝 hello Web 應用程式 Proxy 伺服器。 Web 應用程式 Proxy 伺服器不是聯結的 toohello 網域。 Hello Web 應用程式 Proxy 角色安裝 hello 兩個 Web 應用程式 Proxy 伺服器上，選取 hello 遠端存取角色。 hello 伺服器管理員 會引導您 toocomplete hello WAP 安裝。
如需有關如何閱讀 toodeploy WAP，[安裝及設定 Web Application Proxy 伺服器 hello](https://technet.microsoft.com/library/dn383662.aspx)。

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.部署 hello 網際網路對向的 (Public) 負載平衡器
**8.1.建立網際網路對向 (公用) 負載平衡器**

在 hello Azure 入口網站，選取負載平衡器，然後按一下新增。 在 [hello 建立負載平衡器] 面板中，輸入下列資訊的 hello

1. **名稱**: hello 負載平衡器的名稱
2. **配置**︰公用 – 此選項會告知 Azure，此負載平衡器需要公用位址。
3. **IP 位址**︰建立新的 IP 位址 (動態)

![網際網路對向負載平衡器](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

部署之後，hello 負載平衡器會出現在 hello 負載平衡器清單。

![負載平衡器清單](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2.指派 DNS 標籤 toohello 公用 IP**

按一下新建立的 hello hello 負載平衡器組態的 hello 面板上的面板 toobring 在負載平衡器項目。 請遵循以下步驟 tooconfigure hello DNS 標籤 hello 公用 ip:

1. 按一下 hello 公用 IP 位址。 這會開啟 hello 公用 ip 的 hello 面板和它的設定
2. 按一下 [組態]
3. 提供 DNS 標籤。 這會成為 hello 公用 DNS 標籤，您可以從任何地方，例如 contosofs.westus.cloudapp.azure.com 存取。您可以新增項目在 hello 外部 DNS hello 同盟服務 （例如 fs.contoso.com) 解析 toohello DNS 標籤 hello 外部負載平衡器 (contosofs.westus.cloudapp.azure.com)。

![設定網際網路對向負載平衡器](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![設定網際網路對向負載平衡器 (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3.設定網際網路對向 (公用) 負載平衡器的後端集區** 

相同的步驟與建立 hello 內部負載平衡器，遵循 hello hello 可用性為網際網路對向的 (Public) 負載平衡器的 tooconfigure hello 後端集區設定 hello WAP 伺服器。 例如，contosowapset。

![設定網際網路對向負載平衡器的後端集區](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4.設定探查**

請遵循相同步驟如所示設定 hello 內部負載平衡器 tooconfigure hello 探查 WAP 伺服器 hello 後端集區的 hello。

![設定網際網路對向負載平衡器的探查](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5.建立負載平衡規則**

請遵循相同的步驟 ILB tooconfigure hello 負載平衡規則為 TCP 443 hello。

![設定網際網路對向負載平衡器的平衡規則](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9.保護 hello 網路
**9.1.保護 hello 內部子網路**

整體來說，您需要下列規則 tooefficiently 保護您的內部子網路 （依 hello 順序如下所示） 的 hello

| 規則 | 說明 | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |允許從 DMZ hello HTTPS 通訊 |輸入 |
| DenyInternetOutbound |沒有存取 toointernet |輸出 |

![INT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[註解]: <> (![INT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [註解]: <> (![INT 存取規則 (輸出)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2.保護 hello 周邊網路子網路**

| 規則 | 說明 | Flow |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |從網際網路 toohello DMZ 允許 HTTPS |輸入 |
| DenyInternetOutbound |HTTPS toointernet 以外的項目遭到封鎖 |輸出 |

![EXT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[註解]: <> (![EXT 存取規則 (輸入)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [註解]: <> (![EXT 存取規則 (輸出)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> 如果需要用戶端使用者憑證驗證 (使用 X509 使用者憑證的 clientTLS 驗證)，則 AD FS 需要啟用 TCP 連接埠 49443 以供輸入存取。
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10.測試 hello AD FS 登入
hello 最簡單方式是的 tootest AD FS 會使用 hello IdpInitiatedSignon.aspx 頁面。 中，它是必要的 tooenable 順序 toobe 無法 toodo hello IdpInitiatedSignOn hello AD FS 屬性上。 請遵循以下 tooverify 的 hello 步驟 AD FS 安裝

1. 執行 hello 以下 cmdlet hello AD FS 伺服器上，使用 PowerShell、 tooset 它 tooenabled。
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. 從任何外部電腦存取 https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. 您應該會看到 hello AD FS 網頁類似下面的：

![測試登入網頁](./media/active-directory-aadconnect-azure-adfs/test1.png)

成功登入時，它會提供您如下所示的成功訊息︰

![測試成功](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>在 Azure 中部署 AD FS 的範本
hello 範本部署 6 電腦安裝程式，2 個網域控制站，AD FS 和 WAP。

[Azure 部署範本中的 AD FS](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

您可以使用現有的虛擬網路，或在部署此範本時建立新的 VNET。 以下列出各種不同的參數可用來自訂 hello 部署 hello hello 部署程序中的 hello 參數的使用方式描述 hello。 

| 參數 | 說明 |
|:--- |:--- |
| 位置 |hello 區域 toodeploy hello 資源到例如美東。 |
| StorageAccountType |hello 建立儲存體帳戶的 hello 型別 |
| VirtualNetworkUsage |指出將建立新的虛擬網路，或使用現有的虛擬網路 |
| virtualNetworkName |hello 虛擬網路 tooCreate，強制在現有或新的虛擬網路使用方式的 hello 名稱 |
| VirtualNetworkResourceGroupName |指定 hello hello hello 現有的虛擬網路所在的資源群組名稱。 當使用現有的虛擬網路，這會變成必要的參數以便 hello 部署可以尋找 hello 識別碼 hello 現有的虛擬網路 |
| VirtualNetworkAddressRange |hello 位址範圍的 hello 新的 VNET，如果建立新的虛擬網路的必要項 |
| InternalSubnetName |hello hello 內部子網路名稱，強制在兩個虛擬網路使用方式選項 （新的或現有的） |
| InternalSubnetAddressRange |hello hello 內部子網路，其中包含 hello 網域控制站和 ADFS 伺服器，強制性，如果建立新的虛擬網路的位址範圍。 |
| DMZSubnetAddressRange |hello hello 周邊網路的子網路，其中包含 hello Windows 應用程式 proxy 伺服器，當建立新的虛擬網路的位址範圍。 |
| DMZSubnetName |hello hello 內部子網路名稱，強制在兩個虛擬網路使用方式選項 （新的或現有的）。 |
| ADDC01NICIPAddress |hello 內部 IP 位址的 hello 第一個網域控制站，此 IP 位址將會以靜態方式指派 toohello DC，且必須是 hello 內部子網路內的有效 ip 位址 |
| ADDC02NICIPAddress |hello 內部 IP 位址的 hello 第二個網域控制站，此 IP 位址將會以靜態方式指派 toohello DC，且必須是 hello 內部子網路內的有效 ip 位址 |
| ADFS01NICIPAddress |hello 內部 IP 位址第一部 ADFS 伺服器 hello，此 IP 位址將會以靜態方式指派 toohello ADFS 伺服器，而且必須 hello 內部子網路內的有效 ip 位址 |
| ADFS02NICIPAddress |hello 內部 IP 位址的第二個 ADFS 伺服器 hello，此 IP 位址將會以靜態方式指派 toohello ADFS 伺服器，而且必須 hello 內部子網路內的有效 ip 位址 |
| WAP01NICIPAddress |hello 內部 IP 位址第一部 WAP 伺服器 hello，此 IP 位址將會以靜態方式指派 toohello WAP 伺服器，而且必須 hello 周邊網路子網路內的有效 ip 位址 |
| WAP02NICIPAddress |hello 內部 IP 位址的第二個 WAP 伺服器 hello，此 IP 位址將會以靜態方式指派 toohello WAP 伺服器也必須是有效的 ip 位址 hello 周邊網路子網路內 |
| ADFSLoadBalancerPrivateIPAddress |hello ADFS 的 hello 內部 IP 位址的負載平衡器，此 IP 位址將會以靜態方式指派 toohello 負載平衡器，且必須是 hello 內部子網路內的有效 ip 位址 |
| ADDCVMNamePrefix |網域控制站的虛擬機器名稱前置詞 |
| ADFSVMNamePrefix |ADFS 伺服器的虛擬機器名稱前置詞 |
| WAPVMNamePrefix |WAP 伺服器的虛擬機器名稱前置詞 |
| ADDCVMSize |hello 的 hello 網域控制站的 vm 大小 |
| ADFSVMSize |hello ADFS 伺服器 hello vm 大小 |
| WAPVMSize |hello 的 hello WAP 伺服器的 vm 大小 |
| AdminUserName |hello 名稱 hello hello 虛擬機器的本機系統管理員 |
| AdminPassword |hello hello 虛擬機器的 hello 本機系統管理員帳戶密碼 |

## <a name="additional-resources"></a>其他資源
* [可用性設定組](https://aka.ms/Azure/Availability) 
* [Azure 負載平衡器](https://aka.ms/Azure/ILB)
* [內部負載平衡器](https://aka.ms/Azure/ILB/Internal)
* [網際網路對向負載平衡器](https://aka.ms/Azure/ILB/Internet)
* [儲存體帳戶](https://aka.ms/Azure/Storage)
* [Azure 虛擬網路](https://aka.ms/Azure/VNet)
* [AD FS 和 Web 應用程式 Proxy 連結](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>後續步驟
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
* [使用 Azure AD Connect 設定和管理 AD FS](active-directory-aadconnectfed-whatis.md)
* [使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

