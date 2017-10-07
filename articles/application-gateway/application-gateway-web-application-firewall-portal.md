---
title: "aaaCreate 或更新 Azure 應用程式閘道與 web 應用程式防火牆 |Microsoft 文件"
description: "了解如何 toocreate 應用程式閘道使用的 web 應用程式防火牆 hello 入口網站"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b561a210-ed99-4ab4-be06-b49215e3255a
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: 68d140fef14499da654ea251d1208e6a800f55a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-web-application-firewall-by-using-hello-portal"></a>建立 web 應用程式防火牆使用 hello 入口網站應用程式閘道

> [!div class="op_single_selector"]
> * [Azure 入口網站](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure CLI](application-gateway-web-application-firewall-cli.md)

了解如何 toocreate web 應用程式防火牆啟用應用程式閘道。

hello web 應用程式中的防火牆 (WAF) Azure 應用程式閘道會從網頁型的常見攻擊，例如 SQL 資料隱碼、 跨網站指令碼的攻擊和工作階段倘若保護 web 應用程式。 Web 應用程式可防止許多 hello OWASP 前 10 個常見 web 弱點。

## <a name="scenarios"></a>案例

本文有兩個案例︰

在 hello 第一個案例中，您學會太[建立 web 應用程式防火牆應用程式閘道](#create-an-application-gateway-with-web-application-firewall)

在 hello 第二個案例中，您學會太[加入 web 應用程式防火牆 tooan 現有應用程式閘道](#add-web-application-firewall-to-an-existing-application-gateway)。

![案例範例][scenario]

> [!NOTE]
> 額外設定 hello 應用程式閘道，包括自訂健全狀況探查，hello 應用程式閘道設定之後，而不會在初始部署設定後端集區位址，以及其他規則。

## <a name="before-you-begin"></a>開始之前

「Azure 應用程式閘道」需要有自己的子網路。 當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。 一旦您部署應用程式閘道 tooa 子網路時，唯一的額外應用程式閘道就能 toobe 加入 toohello 子網路。

##<a name="add-web-application-firewall-to-an-existing-application-gateway"></a>加入 web 應用程式防火牆 tooan 現有應用程式閘道

這個範例會更新現有應用程式閘道 toosupport web 應用程式的防火牆防止模式中。

1. 在 [hello Azure 入口網站中**我的最愛**] 窗格中，按一下**所有資源**。 按一下 hello hello 中的現有應用程式閘道**所有資源**刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入 hello 名稱 hello**依名稱篩選...** 方塊 tooeasily 存取 hello DNS 區域。

   ![建立應用程式閘道][1]

1. 按一下**Web 應用程式防火牆**並更新 hello 應用程式閘道設定。 完成時，按一下 [儲存] 

    hello 設定 tooupdate 現有應用程式閘道 toosupport web 應用程式的防火牆是：

   | **設定** | **值** | **詳細資料**
   |---|---|---|
   |**升級 tooWAF 層**| 已檢查 | 這會設定 hello 應用程式閘道 toohello WAF 層 hello 層。|
   |**防火牆狀態**| 已啟用 | 此設定可讓 hello WAF hello 防火牆。|
   |**防火牆模式** | 預防 | 此設定可指定 Web 應用程式防火牆處理惡意流量的方式。 **偵測**模式只會記錄 hello 事件，其中**防止**模式 hello 事件記錄和停駐點 hello 惡意流量。|
   |**規則集**|3.0|此設定會決定 hello[核心規則集](application-gateway-web-application-firewall-overview.md#core-rule-sets)也就是使用的 tooprotect hello 後端集區成員。|
   |**設定已停用的規則**|視情況而異|tooprevent 可能誤判，此設定可讓您 toodisable 特定[規則與規則群組](application-gateway-crs-rulegroups-rules.md)。|

    >[!NOTE]
    > Hello SKU 升級現有的應用程式閘道 toohello WAF SKU，太調整大小變更**媒體**。 這可以在設定完成之後重新設定。

    ![顯示基本設定的刀鋒視窗][2-1]

    > [!NOTE]
    > 必須啟用 tooview web 應用程式防火牆記錄檔，診斷和 ApplicationGatewayFirewallLog 選取。 若要進行測試，可以選擇執行個體計數 1。 請務必 tooknow 任何執行個體計數在兩個執行個體未涵蓋 hello SLA，並因此不建議使用。 如果使用 Web 應用程式防火牆，便無法使用小型閘道。

## <a name="create-an-application-gateway-with-web-application-firewall"></a>使用 Web 應用程式防火牆來建立應用程式閘道

此案例將會：

* 建立含有兩個執行個體的中型 Web 應用程式防火牆應用程式閘道。
* 建立名為 AdatumAppGatewayVNET 且含有 10.0.0.0/16 保留 CIDR 區塊的虛擬網路。
* 建立名為 Appgatewaysubnet 且使用 10.0.0.0/28 做為其 CIDR 區塊的子網路。
* 為 SSL 卸載設定憑證。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。 如果您沒有帳戶，可以註冊[免費試用一個月](https://azure.microsoft.com/free)
1. 在 hello hello 入口網站的 我的最愛 窗格，按一下 **新增**
1. 在 hello**新增**刀鋒視窗中，按一下 **網路**。 在 hello**網路**刀鋒視窗中，按一下**應用程式閘道**hello 下列影像所示：
1. 瀏覽 toohello Azure 入口網站中，按一下**新增** > **網路** > **應用程式閘道**

    ![建立應用程式閘道][1]

1. 在 hello**基本概念**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:

   | **設定** | **值** | **詳細資料**
   |---|---|---|
   |**名稱**|AdatumAppGateway|hello hello 應用程式閘道名稱|
   |**層級**|WAF|可用的值為「標準」或 WAF。 請瀏覽[web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)toolearn 更多關於 WAF。|
   |**SKU 大小**|中型|當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。 當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。|
   |**執行個體計數**|2|高可用性的 hello 應用程式閘道的執行個體數目。 執行個體計數 1 應僅用於測試目的。|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello 應用程式閘道中。|
   |**資源群組**|**建立新項目：**AdatumAppGatewayRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

   ![顯示基本設定的刀鋒視窗][2-2]

1. 在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。 此步驟會開啟輸入 hello**選擇虛擬網路**刀鋒視窗。  按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。

   ![選擇虛擬網路][2]

1. 在 hello**刀鋒視窗中建立虛擬網路**輸入 hello 下列值，然後按一下 **確定**。 此步驟會關閉 hello**建立虛擬網路**和**選擇虛擬網路**刀鋒視窗。 如此即會填入 hello**子網路**欄位 hello**設定**刀鋒視窗的 選擇的 hello 子網路。

   |**設定** | **值** | **詳細資料** |
   |---|---|---|
   |**名稱**|AdatumAppGatewayVNET|Hello 應用程式閘道的名稱|
   |**位址空間**|10.0.0.0/16| 此值為 hello hello 虛擬網路的位址空間|
   |**子網路名稱**|AppGatewaySubnet|Hello 應用程式閘道 hello 子網路名稱|
   |**子網路位址範圍**|10.0.0.0/28 | 此子網路的後端集區成員 hello 虛擬網路中允許更多的其他子網路|

1. 在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇**公用**為 hello **IP 位址類型**

1. 在 hello**設定**刀鋒視窗底下**公用 IP 位址**，按一下 **選擇公用 IP 位址**，此步驟會開啟 hello**選擇公用 IP 位址**刀鋒視窗中，按一下 **建立新**。

   ![選擇公用 IP][3]

1. 在 hello**建立公用 IP 位址**刀鋒視窗中，接受 hello 預設值，然後按一下 **確定**。 此步驟會關閉 hello**選擇公用 IP 位址**刀鋒視窗，hello**建立公用 IP 位址**刀鋒視窗中，並填入**公用 IP 位址**hello 選擇公用 IP 位址。

1. 在 hello**設定**刀鋒視窗底下**接聽程式組態**，按一下  **HTTP**下**通訊協定**。 toouse **https**，都需要的憑證。 被需要 hello hello 憑證私密金鑰，因此必須提供 toobe hello 憑證的.pfx 匯出，而且 hello hello 檔案的密碼。

1. 設定 hello **WAF**特定設定。

   |**設定** | **值** | **詳細資料** |
   |---|---|---|
   |**防火牆狀態**| 已啟用| 此設定會開啟或關閉 WAF。|
   |**防火牆模式** | 預防| 此設定會決定 hello 動作 WAF 接替惡意流量。 如果選擇 **偵測** ，只會記錄流量。  如果選擇 [防止]，則會記錄並停止流量，且產生「403 未經授權」的回應。|


1. 檢閱 hello 摘要] 頁面上，按一下 [**確定**。  現在 hello 應用程式閘道會排入佇列，並建立。

1. 一旦建立 hello 應用程式閘道之後，瀏覽 tooit hello 應用程式閘道 hello toocontinue 入口網站組態中。

    ![應用程式閘道資源檢視][10]

下列步驟建立基本應用程式閘道與 hello 接聽程式、 後端集區、 後端 http 設定和規則的預設設定。 您可以修改這些設定 toosuit 部署成功 hello 佈建之後

> [!NOTE]
> 建立與 hello 基本 web 應用程式的防火牆設定的應用程式閘道設定成使用 CR 3.0 保護。

## <a name="next-steps"></a>後續步驟

接下來，您可以了解如何 tooconfigure hello 的自訂網域別名[公用 IP 位址](../dns/dns-custom-domain.md#public-ip-address)使用 Azure DNS 或其他的 DNS 提供者。

深入了解如何 tooconfigure 診斷記錄，toolog hello 或之事件的偵測到使用 web 應用程式防火牆阻止造訪[應用程式閘道診斷](application-gateway-diagnostics.md)

了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)

了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-portal.md)

<!--Image references-->
[1]: ./media/application-gateway-web-application-firewall-portal/figure1.png
[2]: ./media/application-gateway-web-application-firewall-portal/figure2.png
[2-1]: ./media/application-gateway-web-application-firewall-portal/figure2-1.png
[2-2]: ./media/application-gateway-web-application-firewall-portal/figure2-2.png
[3]: ./media/application-gateway-web-application-firewall-portal/figure3.png
[10]: ./media/application-gateway-web-application-firewall-portal/figure10.png
[scenario]: ./media/application-gateway-web-application-firewall-portal/scenario.png
