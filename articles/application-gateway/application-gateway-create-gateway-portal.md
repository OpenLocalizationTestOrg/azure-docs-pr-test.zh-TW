---
title: "aaaCreate 應用程式閘道的 Azure 入口網站 |Microsoft 文件"
description: "了解如何使用應用程式閘道 toocreate hello 入口網站"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 54dffe95-d802-4f86-9e2e-293f49bd1e06
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 24c1d5701eae372cd233162ceb58dea36a3b6a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-hello-portal"></a>建立與 hello 入口網站應用程式閘道

[應用程式閘道](application-gateway-introduction.md)是專用的虛擬設備，會以服務形式提供應用程式傳遞控制器 (ADC)，為您的應用程式提供各種第 7 層負載平衡功能。 這篇文章帶領您完成 hello 步驟 toocreate 利用 hello Azure 入口網站，做為後端成員加入現有的伺服器應用程式閘道。

## <a name="log-in-tooazure"></a>登入 tooAzure

登入 toohello 在 Azure 入口網站[http://portal.azure.com](http://portal.azure.com)

## <a name="create-application-gateway"></a>建立應用程式閘道

toocreate 應用程式閘道，完成 hello 遵循的步驟。 應用程式閘道需要有自己的子網路。 當建立虛擬網路，請確定您保留足夠的位址空間 toohave 多個子網路。 Hello 應用程式閘道部署的 tooa 子網路之後，只是其他應用程式閘道可以加入 tooit。

1. 在 hello hello 入口網站的 我的最愛 窗格，按一下 **新增**
1. 在 hello**新增**刀鋒視窗中，按一下 **網路**。 在 hello**網路**刀鋒視窗中，按一下**應用程式閘道**hello 下列影像所示：

    ![建立應用程式閘道][1]

1. 在 hello**基本概念**刀鋒視窗中，輸入 hello 下列值，然後按一下 **確定**:

   | **設定** | **值** | **詳細資料**|
   |---|---|---|
   |**名稱**|AdatumAppGateway|hello hello 應用程式閘道名稱|
   |**層級**|標準|可用的值為「標準」或 WAF。 請瀏覽[web 應用程式防火牆](application-gateway-web-application-firewall-overview.md)toolearn 更多關於 WAF。|
   |**SKU 大小**|中型|當選擇「標準」層級時，選項為 [小型]、[中型] 和 [大型]。 當選擇 WAF 層級時，選項只有 [中型] 和 [大型]。|
   |**執行個體計數**|2|高可用性的 hello 應用程式閘道的執行個體數目。 執行個體計數 1 應僅用於測試目的。|
   |**訂用帳戶**|[您的訂用帳戶]|選取的訂用帳戶 toocreate hello 應用程式閘道中。|
   |**資源群組**|**建立新項目：**AdatumAppGatewayRG|建立資源群組。 hello 資源群組名稱必須是唯一 hello 您選取的訂用帳戶內。 深入了解資源群組，請閱讀 hello toolearn[資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#resource-groups)概觀文件。|
   |**位置**|美國西部||

1. 在 hello**設定**刀鋒視窗中出現在下方**虛擬網路**，按一下 **選擇虛擬網路**。 hello**選擇虛擬網路**刀鋒視窗隨即開啟。  按一下**建立新**tooopen hello**建立虛擬網路**刀鋒視窗。

   ![選擇虛擬網路][2]

1. 在 hello**刀鋒視窗中建立虛擬網路**輸入 hello 下列值，然後按一下 **確定**。 hello**建立虛擬網路**和**選擇虛擬網路**關閉刀鋒視窗。 此步驟中會填入 hello**子網路**欄位 hello**設定**刀鋒視窗的 選擇的 hello 子網路。

   | **設定** | **值** | **詳細資料**|
   |---|---|---|
   |**名稱**|AdatumAppGatewayVNET|Hello 應用程式閘道的名稱|
   |**位址空間**|10.0.0.0/16|這是 hello hello 虛擬網路的位址空間|
   |**子網路名稱**|AppGatewaySubnet|Hello 應用程式閘道 hello 子網路名稱|
   |**子網路位址範圍**|10.0.0.0/28|此子網路的後端集區成員 hello 虛擬網路中允許更多的其他子網路|

1. 在 hello**設定**刀鋒視窗底下**前端 IP 組態**，選擇**公用**為 hello **IP 位址類型**

1. 在 hello**設定**刀鋒視窗底下**公用 IP 位址**按一下**選擇公用 IP 位址**，hello**選擇公用 IP 位址**刀鋒視窗中開啟按一下 **建立新**。

   ![選擇公用 IP][3]

1. 在 hello**建立公用 IP 位址**刀鋒視窗中，接受 hello 預設值，然後按一下 **確定**。 hello 刀鋒視窗會關閉，並於其中填入 hello**公用 IP 位址**hello 選擇公用 IP 位址。

1. 在 hello**設定**刀鋒視窗底下**接聽程式組態**，按一下  **HTTP**下**通訊協定**。 輸入 hello hello 連接埠 toouse**連接埠**欄位。

2. 按一下**確定**上 hello**設定**toocontinue 刀鋒視窗。

1. 檢閱上 hello 的 hello 設定**摘要**刀鋒視窗，然後按一下**確定**toostart 建立 hello 應用程式閘道。 建立應用程式閘道是長時間執行的工作，並採用時間 toocomplete。

## <a name="add-servers-toobackend-pools"></a>新增伺服器 toobackend 集區

一旦您建立 hello 應用程式閘道時，裝載 hello 應用程式 toobe 負載平衡的 hello 系統仍然需要 toobe 加入的 toohello 應用程式閘道。 hello IP 位址、 FQDN 或 Nic 的這些伺服器會加入 toohello 後端位址集區。

### <a name="ip-address-or-fqdn"></a>IP 位址或 FQDN

1. Hello，hello Azure 入口網站中建立的應用程式閘道與**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **AdatumAppGateway**中的應用程式閘道 hello 所有資源刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**AdatumAppGateway**在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello 應用程式閘道。

1. 會顯示您所建立的 hello 應用程式閘道。 按一下**後端集區**，並選取目前後端集區 hello **appGatewayBackendPool**，hello **appGatewayBackendPool**刀鋒視窗隨即開啟。

   ![應用程式閘道後端集區][4]

1. 按一下**加入目標**tooadd IP 位址的 FQDN 值。 選擇**IP 位址或 FQDN**為 hello**類型**hello 欄位中輸入您的 IP 位址或 FQDN。 針對其他的後端集區成員重複這個步驟。 完成時，按一下 [儲存]。

### <a name="virtual-machine-and-nic"></a>虛擬機器和 NIC

您也可以將虛擬機器 NIC 新增為後端集區成員。 唯一的虛擬機器內 hello 與 hello 應用程式閘道相同虛擬網路都是透過 hello 下拉式清單。

1. Hello，hello Azure 入口網站中建立的應用程式閘道與**我的最愛**] 窗格中，按一下 [**所有資源**。 按一下 hello **AdatumAppGateway**中的應用程式閘道 hello 所有資源刀鋒視窗。 如果您已選取的 hello 訂用帳戶有多項資源，您可以輸入**AdatumAppGateway**在 hello**依名稱篩選...** 方塊 tooeasily 存取 hello 應用程式閘道。

1. 會顯示您所建立的 hello 應用程式閘道。 按一下**後端集區**，並選取目前後端集區 hello **appGatewayBackendPool**，hello **appGatewayBackendPool**刀鋒視窗隨即開啟。

   ![應用程式閘道後端集區][5]

1. 按一下**加入目標**tooadd IP 位址的 FQDN 值。 選擇**虛擬機器**為 hello**類型**選取 hello 虛擬機器和 NIC toouse。 完成時，按一下 [儲存]

   > [!NOTE]
   > 唯一的虛擬機器中 hello 相同虛擬網路，如 hello 下拉式方塊中的 hello 應用程式閘道可用。

## <a name="clean-up-resources"></a>清除資源

當不再需要請刪除 hello 資源群組、 應用程式閘道和所有相關的資源。 因此，從 hello 應用程式閘道刀鋒視窗，然後按一下 選取 hello 資源群組的 toodo**刪除**。

## <a name="next-steps"></a>後續步驟

在此案例中，您可以部署應用程式閘道，並加入伺服器 toohello 後端。 hello 下一個步驟是修改設定，並在 hello 閘道的調整規則的 tooconfigure hello 應用程式閘道。 瀏覽下列發行項的 hello，您可以找到下列步驟：

了解如何 toocreate 自訂健全狀況探查造訪[建立自訂的健全狀況探查](application-gateway-create-probe-portal.md)

了解如何 tooconfigure SSL 卸載且採用 hello 昂貴 SSL 解密關閉您的 web 伺服器造訪[設定 SSL 卸載](application-gateway-ssl-portal.md)

深入了解如何 tooprotect 應用程式與[Web 應用程式防火牆](application-gateway-webapplicationfirewall-overview.md)應用程式閘道的功能。

<!--Image references-->
[1]: ./media/application-gateway-create-gateway-portal/figure1.png
[2]: ./media/application-gateway-create-gateway-portal/figure2.png
[3]: ./media/application-gateway-create-gateway-portal/figure3.png
[4]: ./media/application-gateway-create-gateway-portal/figure4.png
[5]: ./media/application-gateway-create-gateway-portal/figure5.png
[scenario]: ./media/application-gateway-create-gateway-portal/scenario.png
