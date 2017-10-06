---
title: "aaaHigh 可用性跨地理 AD FS 部署在 Azure 中使用 Azure Traffic Manager |Microsoft 文件"
description: "本文件中，您將學習如何 toodeploy AD FS 在 Azure 中的高可用性。"
keywords: "Ad fs 搭配 Azure 流量管理員] 中，使用 Azure Traffic Manager，地理、 多個資料中心、 地理資料中心、 多重地理資料中心，adfs 部署在 azure 中的 AD FS 部署 azure adfs、 azure adfs、 azure ad fs、 部署 adfs、 部署 ad fs，在 azure 中，adfs將 adfs 部署在 azure 中，在 azure、 adfs azure 簡介 tooAD FS、 Azure、 Azure iaas，ADFS 中的 AD FS 部署 AD FS 移動 adfs tooazure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>使用 Azure 流量管理員在 Azure 中部署高可用性跨地區 AD FS
[在 Azure 中的 AD FS 部署](active-directory-aadconnect-azure-adfs.md)提供逐步指南 toohow 為您可以針對您的組織在 Azure 中部署簡單的 AD FS 基礎結構。 本文章提供 hello 接下來的步驟 toocreate 地理跨部署在 Azure 中使用的 AD FS [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)。 Azure Traffic Manager 可幫您藉由建立地理位置模式高可用性和高效能為您的組織的 AD FS 基礎結構使用不同的可用 toosuit 需要從 hello 基礎結構的路由方式的範圍。

高可用性的跨地區 AD FS基礎結構能夠︰

* **消除單一失敗點：**容錯移轉功能的 Azure 流量管理員，可以達到高可用性的 AD FS 基礎結構即使其中一個 hello hello 地球的組件中的資料中心停機
* **更佳的效能：**您可以使用 hello 建議部署於此發行項 tooprovide 高效能 AD FS 基礎結構，可協助使用者驗證更快。 

## <a name="design-principles"></a>設計原則
![整體設計](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

hello 基本設計原則將會如下所示 hello 文件在 Azure 中的 AD FS 部署中的設計原則相同。 hello 上圖顯示 hello 基本部署 tooanother 地理區域的簡單的延伸。 以下是一些點 tooconsider 擴充部署 toonew 的地理區域時

* **虛擬網路：**您應該建立新的虛擬網路在 hello 地理區域中，您想 toodeploy 其他 AD FS 基礎結構。 在 hello 圖中您會見 Geo1 VNET 和 Geo2 VNET hello 在每個地理區域的兩個虛擬網路。
* **網域控制站和新的地理 VNET 中的 AD FS 伺服器：**建議 toodeploy hello 新的地理區域的網域控制站以便 hello AD FS 伺服器 hello 新區域中的沒有 toocontact 網域控制站在遠另一個離開網路 toocomplete 驗證，藉此改善 hello 效能。
* **儲存體帳戶︰** 儲存體帳戶會與某個區域相關聯。 因為您要部署新的地理區域中的機器，您必須 toocreate toobe hello 地區中使用新儲存體帳戶。  
* **網路安全性群組︰** 如同儲存體帳戶，在區域中建立的網路安全性群組不能用於另一個地理區域。 因此，您將需要 toocreate 新網路安全性群組類似 toothose hello 的第一個地理區域，INT 和周邊網路中 hello 新的地理區域的子網路。
* **公用 IP 位址的 DNS 標籤：** Azure Traffic Manager 可以參考 tooendpoints 只透過 DNS 標籤。 因此，您會需要的 toocreate hello 外部負載平衡器 ' 的公用 IP 位址的 DNS 標籤。
* **Azure 流量管理員：** Microsoft Azure Traffic Manager 可讓您 toocontrol hello 發佈的 hello 世界各地的不同資料中心內執行的使用者流量 tooyour 服務端點。 Azure Traffic Manager 可在 hello DNS 層級運作。 它會使用 DNS 回應 toodirect 使用者流量分散 tooglobally 端點。 用戶端，直接連接 toothose 端點。 使用不同的效能、 加權和優先權路由選項，您可以輕鬆選擇 hello 路由選項最適合貴組織的需求。 
* **V net tooV 網路連線之間兩個區域：**您不需要 toohave hello 虛擬網路之間的連線本身。 因為每個虛擬網路存取 toodomain 控制站，且具有 AD FS 和 WAP 伺服器本身，所以他們可以處理而不同的區域中的 hello 虛擬網路之間的任何連線。 

## <a name="steps-toointegrate-azure-traffic-manager"></a>步驟 toointegrate Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>在 [hello 新的地理區域部署 AD FS
遵循 hello 步驟和中的指導方針[在 Azure 中的 AD FS 部署](active-directory-aadconnect-azure-adfs.md)toodeploy hello hello 新的地理區域中的相同拓撲。

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Hello 網際網路對向 （公用） 的負載平衡器的公用 IP 位址的 DNS 標籤
如上面所述，hello Azure Traffic Manager 只能參考 tooDNS 標籤做為端點，因此是很重要的 toocreate hello 外部負載平衡器 ' 的公用 IP 位址的 DNS 標籤。 下列螢幕擷取畫面會顯示您可以設定 DNS 標籤 hello 公用 IP 位址的方式。 

![DNS 標籤](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>部署 Azure 流量管理員
請遵循以下 toocreate 流量管理員設定檔的 hello 步驟。 如需詳細資訊，您也可以使用參照太[管理 Azure Traffic Manager 設定檔](../traffic-manager/traffic-manager-manage-profiles.md)。

1. **建立流量管理員設定檔** ：為您的流量管理員設定檔提供一個唯一的名稱。 這個 hello 設定檔的名稱是 hello DNS 名稱的一部分，並做為 hello Traffic Manager 網域名稱標籤中的前置詞。 hello 名稱前置詞會針對您的流量管理員加入 too.trafficmanager.net toocreate DNS 標籤 /。 hello 以下螢幕擷取畫面顯示 hello 流量管理員 mysts 和產生 DNS 標籤都會是 mysts.trafficmanager.net 所設定的 DNS 首碼。 
   
    ![流量管理員設定檔建立](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **流量路由方法：** 流量管理員中有三個可用的路由選項：
   
   * 優先順序 
   * 效能
   * 加權
     
     **效能**hello 建議選項 tooachieve 高回應性的 AD FS 基礎結構。 不過，您可以選擇任何最適合您的部署需求的路由方式。 hello AD FS 功能不會受到選取 hello 路由選項。 如需詳細資訊，請參閱 [流量管理員流量路由方法](../traffic-manager/traffic-manager-routing-methods.md) 。 在 [hello 範例螢幕擷取畫面，您可以看到 hello**效能**選取方法。
3. **設定端點：**在 hello 流量管理員] 頁面上，按一下 [端點上，選取 [新增]。 這會開啟新增端點頁面類似 toohello 以下螢幕擷取畫面
   
   ![設定端點](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Hello 不同的輸入，請遵循下列指導方針 hello:
   
   **類型：**選取 Azure 端點，因為我們將會指向 tooan Azure 公用 IP 位址。
   
   **名稱：**建立您想 tooassociate 與 hello 端點的名稱。 這不 hello DNS 名稱，而且沒有任何關係 DNS 記錄。
   
   **目標資源類型：** hello value toothis 屬性選取公用 IP 位址。 
   
   **目標資源：**這會提供您選項 toochoose hello 不同的 DNS 標籤從您可以使用您的訂用帳戶底下。 選擇的 hello DNS 標示您要設定的對應 toohello 端點。
   
   新增您想讓 hello Azure Traffic Manager tooroute 流量每個地理區域的端點。
   如需詳細資訊和詳細的步驟 tooadd / traffic manager 中設定端點，請參閱太[新增、 停用、 啟用或刪除端點](../traffic-manager/traffic-manager-endpoints.md)
4. **設定探查：**在 hello 流量管理員] 頁面上，按一下 [上設定。 在 [hello 組態] 頁面上，您需要 toochange hello 監視器設定 tooprobe HTTP 連接埠 80 和相對路徑 /adfs/probe
   
    ![設定探查](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **請確認 hello hello 端點狀態 hello 組態完成之後在線上**。 如果所有端點都都 '降級' 狀態中，Azure Traffic Manager 會執行最佳嘗試 tooroute hello 流量假設 hello 診斷不正確，且所有端點都都都可以連線。
   > 
   > 
5. **DNS 記錄修改 Azure Traffic Manager:**同盟服務應 CNAME toohello Azure Traffic Manager DNS 名稱。 在中建立 CNAME hello 公用 DNS 記錄，讓實際人員正嘗試 tooreach hello 同盟服務到 hello Azure Traffic Manager。
   
    例如 toopoint hello 同盟服務 fs.fabidentity.com toohello 流量管理員] 中，您需要 tooupdate 遵循您 DNS 資源記錄 toobe hello:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>測試 hello 路由和 AD FS 登入
### <a name="routing-test"></a>路由測試
Hello 路由的基本測試將 tootry ping hello 同盟服務 DNS 名稱從每個地理區域中的機器。 根據 hello 選擇路由的方法，hello 端點實際偵測將會反映在 hello ping 顯示。 例如，如果您選取 hello 效能路由，然後最接近的 toohello hello 端點 hello 用戶端的區域中，將會達到。 以下是從兩個不同的區域用戶端電腦的兩個 ping hello 快照 EastAsia 區域中，一個在美國西部。 

![路由測試](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS 登入測試
最簡單方式 tootest hello AD FS 是使用 hello IdpInitiatedSignon.aspx 頁面。 中，它是必要的 tooenable 順序 toobe 無法 toodo hello IdpInitiatedSignOn hello AD FS 屬性上。 請遵循以下 tooverify 的 hello 步驟 AD FS 安裝

1. 執行 hello 以下 cmdlet hello AD FS 伺服器上，使用 PowerShell、 tooset 它 tooenabled。 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. 從任何外部電腦存取 https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. 您應該會看到 hello AD FS 網頁類似下面的：
   
    ![ADFS 測試 - 驗證挑戰](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    而成功登入時，它會提供您如下所示的成功訊息︰
   
    ![ADFS 測試 - 驗證](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>相關連結
* [Azure 中的基本 AD FS 部署](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure 流量管理員](../traffic-manager/traffic-manager-overview.md)
* [流量管理員流量路由方法](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>後續步驟
* [管理 Azure 流量管理員設定檔](../traffic-manager/traffic-manager-manage-profiles.md)
* [加入、停用、啟用或刪除端點](../traffic-manager/traffic-manager-endpoints.md) 

