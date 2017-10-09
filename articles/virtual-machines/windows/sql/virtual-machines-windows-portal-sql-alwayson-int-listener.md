---
title: "Azure 虛擬機器中 SQL Server 可用性群組接聽程式 aaaCreate |Microsoft 文件"
description: "在 Azure 虛擬機器中建立 SQL Server 的 AlwaysOn 可用性群組接聽程式的逐步指示"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>在 Azure 中設定 Always On 可用性群組的負載平衡器
這篇文章說明如何 toocreate 負載平衡器，為 SQL Server Always On 可用性群組在 Azure 虛擬機器正在使用 Azure 資源管理員。 Hello SQL Server 執行個體位於 Azure 虛擬機器時，可用性群組需要負載平衡器。 hello 負載平衡器會儲存 hello hello 可用性群組接聽程式的 IP 位址。 如果可用性群組跨越多個區域，則每個區域都需要負載平衡器。

toocomplete 這個工作中，您需要的 toohave 正在使用資源管理員的 Azure 虛擬機器部署 SQL Server 可用性群組。 這兩個 SQL Server 虛擬機器必須屬於 toohello 相同可用性設定組。 您可以使用 hello [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)tooautomatically 建立 hello 可用性群組資源管理員 中。 此範本會自動為您建立內部負載平衡器。 

如果您想要的話，也可以 [手動設定可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。

本文會要求您已經設定可用性群組。  

相關主題包括：

* [在 Azure VM (GUI) 中設定 Always On 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [使用 Azure Resource Manager 和 PowerShell 來設定 VNet 對 VNet 連線](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

藉由查核透過這份文件，來建立，並在 hello Azure 入口網站中設定負載平衡器。 Hello 程序完成之後，您會設定 hello 叢集 toouse hello IP 位址從 hello hello 可用性群組接聽程式的負載平衡器。

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>建立及設定 hello Azure 入口網站中的 hello 負載平衡器
在這個部分 hello 工作中，請勿 hello 遵循：

1. 在 hello Azure 入口網站，建立 hello 負載平衡器並設定 hello IP 位址。
2. 設定 hello 後端集區。
3. 建立 hello 探查。 
4. 設定 hello 負載平衡規則。

> [!NOTE]
> 如果在多個資源群組和地區 hello SQL Server 執行個體，執行每個步驟兩次，一次每個資源群組中。
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>步驟 1： 建立 hello 負載平衡器並設定 hello IP 位址
首先，建立 hello 負載平衡器。 

1. 在 hello Azure 入口網站，開啟 hello 資源群組含有 hello SQL Server 虛擬機器。 

2. 在 hello 資源群組中，按一下 **新增**。

3. 搜尋**負載平衡器**，然後在 hello 搜尋結果中，選取**負載平衡器**，這由發佈**Microsoft**。

4. 在 hello**負載平衡器**刀鋒視窗中，按一下 **建立**。

5. 在 hello**建立負載平衡器**對話方塊方塊中，hello 負載平衡器設定，如下所示：

   | 設定 | 值 |
   | --- | --- |
   | **名稱** |文字名稱，代表 hello 負載平衡器。 例如 **sqlLB**。 |
   | **類型** |**內部**： 大部分的實作會使用內部負載平衡器，可讓應用程式內 hello 相同虛擬網路 tooconnect toohello 可用性群組。  </br> **外部**： 允許應用程式 tooconnect toohello 透過公用網際網路連線的可用性群組。 |
   | **虛擬網路** |選取 hello hello SQL Server 則會在中的虛擬網路。 |
   | **子網路** |選取 hello SQL Server 執行個體位在的 hello 子網路。 |
   | **IP 位址指派** |**靜態** |
   | **私人 IP 位址** |指定可用的 IP 位址從 hello 子網路。 當您建立 hello 叢集上的接聽程式時，請使用此 IP 位址。 在 PowerShell 指令碼，在本文中稍後使用這個位址 hello`$ILBIP`變數。 |
   | **訂用帳戶** |如果您有多個訂用帳戶，此欄位才會出現。 選取您想要與此資源 tooassociate hello 訂用帳戶。 它通常是 hello 相同訂用帳戶的 hello 可用性群組的所有都 hello 資源。 |
   | **資源群組** |選取 hello 資源群組中的 hello SQL Server 執行個體。 |
   | **位置** |選取 hello Azure hello SQL Server 執行個體位在的位置。 |

6. 按一下 [建立] 。 

Azure 會建立 hello 負載平衡器。 hello 負載平衡器所屬 tooa 特定網路、 子網路、 資源群組和位置。 Azure 完成 hello 工作之後，請確認在 Azure 中的 hello 負載平衡器設定。 

### <a name="step-2-configure-hello-back-end-pool"></a>步驟 2： 設定 hello 後端集區
Azure 會呼叫 hello 後端位址集區*後端集區*。 在此情況下，hello 後端集區是 hello 兩個 SQL Server 執行個體可用性群組中的 hello 位址。 

1. 在資源群組中，按一下您所建立的 hello 負載平衡器。 

2. 在 [設定] 上，按一下 [後端集區]。

3. 在**後端集區**，按一下 **新增**toocreate 的後端位址集區。 

4. 在**新增後端集區**下**名稱**，輸入 hello 後端集區的名稱。

5. 在 [虛擬機器] 之下，按一下 [新增虛擬機器]。 

6. 在下**選擇虛擬機器**，按一下 **選擇可用性設定組**，然後指定 hello 可用性設定組 hello SQL Server 虛擬機器屬於。

7. 您已選擇 hello 可用性設定組之後，請按一下**選擇 hello 虛擬機器**，選取 hello 兩部虛擬機器的主控件 hello hello 可用性群組中的 SQL Server 執行個體，然後按一下**選取**. 

8. 按一下**確定**tooclose hello 刀鋒視窗的**選擇虛擬機器**，和**新增後端集區**。 

Azure 會更新 hello hello 後端位址集區設定。 您的可用性設定組現在有包含兩個 SQL Server 執行個體的集區。

### <a name="step-3-create-a-probe"></a>步驟 3：建立探查
hello 探查定義 Azure 如何驗證哪些 hello SQL Server 執行個體目前擁有 hello 可用性群組接聽程式。 Azure 探查 hello 服務根據 hello 建立 hello 探查時，您所定義的連接埠上的 IP 位址。

1. 在 hello 負載平衡器**設定**刀鋒視窗中，按一下 **健全狀況探查**。 

2. 在 hello**健全狀況探查**刀鋒視窗中，按一下 **新增**。

3. Hello 上設定 hello 探查**新增探查**刀鋒視窗。 使用下列值 tooconfigure hello 探查的 hello:

   | 設定 | 值 |
   | --- | --- |
   | **名稱** |代表 hello 探查文字名稱。 例如 **SQLAlwaysOnEndPointProbe**。 |
   | **通訊協定** |**TCP** |
   | **連接埠** |您可以使用任何可用的連接埠。 例如 *59999*。 |
   | **間隔** |*5* |
   | **狀況不良臨界值** |*2* |

4.  按一下 [確定] 。 

> [!NOTE]
> 請確定您指定的 hello 通訊埠的兩個 SQL Server 執行個體的 hello 防火牆上開啟。 兩個執行個體需要 hello 您使用的 TCP 連接埠的輸入的規則。 如需詳細資訊，請參閱[新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx)。 
> 
> 

Azure 會建立 hello 探查，然後再使用它 tootest 哪一個 SQL Server 執行個體具有 hello hello 可用性群組接聽程式。

### <a name="step-4-set-hello-load-balancing-rules"></a>步驟 4： 設定 hello 負載平衡規則
hello 負載平衡規則設定 hello 負載平衡器將流量 toohello SQL Server 執行個體的路由。 此負載平衡器，您會啟用伺服器直接回傳，因為只有其中一個 hello 兩個 SQL Server 執行個體擁有 hello 可用性群組接聽程式資源一次。

1. 在 hello 負載平衡器**設定**刀鋒視窗中，按一下 **負載平衡規則**。 

2. 在 hello**負載平衡規則**刀鋒視窗中，按一下 **新增**。

3. 在 hello**新增負載平衡規則**刀鋒視窗中，設定 hello 負載平衡規則。 使用下列設定的 hello: 

   | 設定 | 值 |
   | --- | --- |
   | **名稱** |文字名稱，代表 hello 負載平衡規則。 例如 **SQLAlwaysOnEndPointListener**。 |
   | **通訊協定** |**TCP** |
   | **連接埠** |*1433* |
   | **後端連接埠** |*1433*.系統會忽略此值，因為此規則使用 [浮動 IP (伺服器直接回傳)]。 |
   | **探查** |此負載平衡器使用您所建立的 hello 探查 hello 名稱。 |
   | **工作階段持續性** |**None** |
   | **閒置逾時 (分鐘)** |*4* |
   | **浮動 IP (伺服器直接回傳)** |**已啟用** |

   > [!NOTE]
   > 您可能必須關閉 hello 刀鋒視窗 tooview tooscroll hello 的所有設定。
   > 

4. 按一下 [確定] 。 
5. Azure 會設定 hello 負載平衡規則。 現在 hello 負載平衡器設定的 tooroute 流量 toohello SQL Server 執行個體裝載 hello hello 可用性群組接聽程式。 

此時，hello 資源群組已連接 tooboth SQL Server 電腦的負載平衡器。 hello 負載平衡器也包含 hello SQL Server Always On 可用性群組接聽程式，IP 位址，讓電腦可以回應 toorequests hello 可用性群組。

> [!NOTE]
> 如果您的 SQL Server 執行個體中兩個不同的區域，請重複 hello hello 步驟其他區域。 每個區域都需要負載平衡器。 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>設定 hello 叢集 toouse hello 負載平衡器 IP 位址
hello 下一個步驟是在 hello 叢集 tooconfigure hello 接聽程式，並讓 hello 接聽程式連線。 請勿 hello 遵循： 

1. Hello 容錯移轉叢集上建立 hello 可用性群組接聽程式。 

2. 顯示 hello 接聽程式連線。

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>步驟 5: Hello 容錯移轉叢集上建立 hello 可用性群組接聽程式
在此步驟中，您可以手動建立容錯移轉叢集管理員和 SQL Server Management Studio 中的 hello 可用性群組接聽程式。

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>確認 hello hello 接聽程式組態

如果正確設定 hello 叢集資源和相依性，您應該在 SQL Server Management Studio 無法 tooview hello 接聽程式。 tooset hello 接聽程式通訊埠，請勿遵循 hello:

1. 啟動 SQL Server Management Studio，然後連接 toohello 主要複本。

2. 跳過**AlwaysOn 高可用性** > **可用性群組** > **可用性群組接聽程式**。  
    您現在應該會看到您在建立容錯移轉叢集管理員 中的 hello 接聽程式名稱。 

3. Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。

4. 在 hello**連接埠**方塊中，使用 hello $EndpointPort 您稍早所指定 hello hello 可用性群組接聽程式的連接埠號碼 （1433年是 hello 預設值），然後按一下 **[確定]**。

現在，您在以 Resource Manager 模式執行的 Azure 虛擬機器中，已有一個可用性群組。 

## <a name="test-hello-connection-toohello-listener"></a>測試 hello 連接 toohello 接聽程式
藉由 hello 下列測試 hello 連接：

1. RDP tooa SQL Server 執行個體處於 hello 相同虛擬網路，但不會無法自己 hello 複本。 此伺服器可以 hello hello 叢集中的其他 SQL Server 執行個體。

2. 使用**sqlcmd**公用程式 tootest hello 連線。 例如，下列指令碼的 hello 建立**sqlcmd**透過 hello 接聽程式使用 Windows 驗證連接 toohello 主要複本：
   
        sqlcmd -S <listenerName> -E

hello SQLCMD 連線自動連接到裝載主要複本的 hello toohello SQL Server 執行個體。 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>建立其他可用性群組的 IP 位址

每個可用性群組都會使用個別的接聽程式。 每個接聽程式有其自己的 IP 位址。 使用 hello 相同額外的接聽程式的負載平衡器 toohold hello IP 位址。 建立可用性群組之後，新增 hello IP 位址 toohello 負載平衡器，然後再設定 hello 接聽程式。

tooadd IP 位址 tooa 負載平衡器以 hello Azure 入口網站，請勿 hello 遵循：

1. 在 hello Azure 入口網站，開啟包含 hello 負載平衡器的 hello 資源群組，然後按一下 hello 負載平衡器。 

2. 在 設定 下按一下 前端 IP 集區，然後按一下新增。 

3. 在下**新增前端 IP 位址**，指派 hello 前端的名稱。 

4. 請確認該 hello**虛擬網路**和 hello**子網路**hello 與 hello SQL Server 執行個體相同。

5. Hello hello 接聽程式的 IP 位址設定。 
   
   >[!TIP]
   >您可以設定 hello IP 位址 toostatic，然後輸入 hello 子網路中的目前未使用的位址。 或者，您可以設定 hello IP 位址 toodynamic，並儲存 hello 前端 IP 集區。 當您這樣做時，hello Azure 入口網站會自動指派的可用 IP 位址 toohello 集區。 然後，您可以重新開啟 hello 前端 IP 集區，並變更 hello 分派 toostatic。 

6. 儲存 hello hello 接聽程式的 IP 位址。 

7. 使用下列設定的 hello 新增健全狀況探查：

   |設定 |值
   |:-----|:----
   |**名稱** |名稱 tooidentify hello 探查。
   |**通訊協定** |TCP
   |**連接埠** |未使用的 TCP 通訊埠，其必須可在所有虛擬機器上使用。 不能用於其他用途。 沒有兩個接聽程式可以使用 hello 相同探查連接埠。 
   |**間隔** |嘗試 hello 探查之間的時間量。 使用 hello 預設 (5)。
   |**狀況不良臨界值** |hello 應該會失敗，虛擬機器會被視為狀況不良之前的連續臨界值數目。

8. 按一下**確定**toosave hello 探查。 

9. 建立負載平衡規則。 按一下 負載平衡規則，然後按一下新增。

10. 設定 hello 新負載平衡規則使用 hello 下列設定：

   |設定 |值
   |:-----|:----
   |**名稱** |名稱 tooidentify hello 負載平衡規則。 
   |**前端 IP 位址** |選取您建立 hello IP 位址。 
   |**通訊協定** |TCP
   |**連接埠** |使用 hello hello SQL Server 執行個體正在使用的通訊埠。 預設的執行個體會使用連接埠 1433，除非您有進行變更。 
   |**後端連接埠** |相同的值做為使用 hello**連接埠**。
   |**後端集區** |hello 包含 hello hello SQL Server 執行個體的虛擬機器的集區。 
   |**健康狀態探查** |選擇您所建立的 hello 探查。
   |**工作階段持續性** |None
   |**閒置逾時 (分鐘)** |預設值 (4)
   |**浮動 IP (伺服器直接回傳)** | 已啟用

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>設定 hello 可用性群組 toouse hello 新 IP 位址

toofinish 設定 hello 叢集中，遵循您所做的 hello 第一個可用性群組的重複 hello 步驟。 也就是設定 hello[叢集 toouse hello 新 IP 位址](#configure-the-cluster-to-use-the-load-balancer-ip-address)。 

加入 hello 接聽程式的 IP 位址之後，請透過 hello 下列方式設定 hello 其他可用性群組： 

1. 請確認為 hello 新 IP 位址的 hello 探查連接埠已開啟兩部 SQL Server 虛擬機器上。 

2. [在 [叢集管理員] 中，加入 hello 用戶端存取點](#addcap)。

3. [設定 hello 可用性群組的 hello IP 資源](#congroup)。

   >[!IMPORTANT]
   >當您建立 hello IP 位址時，使用您加入 toohello 負載平衡器的 hello IP 位址。  

4. [讓 hello SQL Server 可用性群組資源相依於 hello 用戶端存取點](#dependencyGroup)。

5. [使 hello 用戶端存取點依存於 hello IP 位址資源](#listname)。
 
6. [在 PowerShell 中設定 hello 叢集參數](#setparam)。

設定 hello 可用性群組 toouse hello 新的 IP 位址之後，設定 hello 連接 toohello 接聽程式。 

## <a name="next-steps"></a>後續步驟

- [在不同區域中的 Azure 虛擬機器上設定 SQL Server Always On 可用性群組](virtual-machines-windows-portal-sql-availability-group-dr.md)
