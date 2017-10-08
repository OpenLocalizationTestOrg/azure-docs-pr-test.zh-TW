---
title: "aaaCreate Azure 堆疊開發套件的不同環境中的兩個虛擬網路之間的站對站 VPN 連線 |Microsoft 文件"
description: "雲端系統管理員會使用兩個單一節點 Azure 堆疊開發套件環境之間 toocreate 網站-站台 VPN 連線的逐步程序。"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: 74225a82efae7d9ca6dc08b45ff04c578fae785c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a>在不同 Azure Stack 開發套件環境中的兩個虛擬網路之間建立站對站 VPN 連線
## <a name="overview"></a>概觀
本文章將示範如何 toocreate 在兩個不同的 Azure 堆疊開發套件環境的兩個虛擬網路之間的站對站 VPN 連線。 當您設定 hello 連線時，您了解 Azure 堆疊中的 VPN 閘道的運作方式。

### <a name="connection-diagram"></a>連接圖表
hello 圖 hello 連線組態應該看起來像當您完成。

![站對站 VPN 連線組態](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a>開始之前
toocomplete hello 連接組態中，確定您已擁有 hello 下列項目，才能開始：

* 兩個伺服器都符合 hello Azure 堆疊開發套件的硬體需求，這會由 hello [Azure 堆疊部署必要條件](azure-stack-deploy.md)。 請確定該 hello hello 中出現的其他先決條件[文章](azure-stack-deploy.md)太履行。
* hello [Azure 堆疊開發套件](https://azure.microsoft.com/en-us/overview/azure-stack/try/)部署套件。

## <a name="deploy-hello-azure-stack-development-kit-environments"></a>部署 hello Azure 堆疊開發組件環境
toocomplete hello 連接組態中，您必須部署兩個 Azure 堆疊開發套件的環境。
> [!NOTE] 
> 您部署每個 Azure 堆疊開發套件，請遵循 hello[部署指示](azure-stack-run-powershell-script.md)。 在本文中，稱為 hello Azure 堆疊開發套件環境*POC1*和*POC2*。


## <a name="prepare-an-offer-on-poc1-and-poc2"></a>在 POC1 和 POC2 上準備供應項目
POC1 和 POC2 準備提供項目，可讓使用者可以訂閱 toohello 供應項目，並部署 hello 虛擬機器。 如需詳細資訊 toocreate 的供應項目，請參閱[讓虛擬機器可用 tooyour Azure 堆疊使用者](azure-stack-tutorial-tenant-vm.md)。

## <a name="review-and-complete-hello-network-configuration-table"></a>檢閱並完成 hello 網路組態資料表
hello 下表摘要說明這兩種 Azure 堆疊開發套件環境的 hello 網路組態。 使用 hello 資料表 tooadd hello 適合您網路的外部 BGPNAT 位址後面出現的 hello 程序。

**網路組態表**
|   |POC1|POC2|
|---------|---------|---------|
|虛擬網路名稱     |VNET-01|VNET-02 |
|虛擬網路位址空間 |10.0.10.0/23|10.0.20.0/23|
|子網路名稱     |Subnet-01|Subnet-02|
|子網路位址範圍|10.0.10.0/24 |10.0.20.0/24 |
|閘道器子網路     |10.0.11.0/24|10.0.21.0/24|
|外部 BGPNAT 位址     |         |         |

> [!NOTE]
> 在 hello 範例環境 hello 外部 BGPNAT IP 位址為 10.16.167.195 POC1，如和 POC2 的 10.16.169.131。 使用 hello 您 Azure 堆疊開發套件的主機，如下列程序 toodetermine hello 外部 BGPNAT IP 位址，然後將它們加入 toohello 先前網路組態資料表。


### <a name="get-hello-ip-address-of-hello-external-adapter-of-hello-nat-vm"></a>取得 hello hello hello NAT VM 的外部介面卡的 IP 位址
1. 登入 toohello Azure 堆疊實體機器 POC1。
2. 編輯下列 Powershell 程式碼 tooreplace hello 您的系統管理員密碼，然後再執行 hello POC 主機上的 hello 程式碼：

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. 新增 hello IP 位址 toohello 網路組態中表格的 hello 上一節。

4. 在 POC2 上重複執行此程序。

## <a name="create-hello-network-resources-in-poc1"></a>建立 hello POC1 中的網路資源
您現在建立 hello POC1 網路資源，您需要 tooset 註冊您的閘道。 hello 指示會告訴您如何使用 toocreate hello 資源 hello 使用者入口網站。 您也可以使用 PowerShell 的程式碼 toocreate hello 資源。

![工作流程，則使用的 toocreate 資源](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a>以租用戶身分登入
服務系統管理員可以登入為租用戶 tootest hello 計劃、 提供項目及可能會使用其租用戶的訂用帳戶。 如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。

### <a name="create-hello-virtual-network-and-vm-subnet"></a>建立 hello 虛擬網路和 VM 子網路
1. 使用租用戶帳戶 toosign toohello 使用者入口網站中。
2. 在 hello 使用者入口網站中，選取 **新增**。

    ![建立新的虛擬網路](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. 跳過**Marketplace**，然後選取**網路**。
4. 選取 [虛擬網路]。
5. 如**名稱**，**位址空間**，**子網路名稱**，和**子網路位址範圍**，稍早出現在使用 hello 值 hello 網路組態資料表。
6. 在**訂用帳戶**，會出現您稍早建立的 hello 訂用帳戶。
7. 針對 [資源群組]，您可以建立資源群組，或選取 [使用現有的] \(如果您已經有資源群組)。
8. 請確認 hello 預設位置。
9. 選取**Pin toodashboard**。
10. 選取 [ **建立**]。

### <a name="create-hello-gateway-subnet"></a>建立 hello 閘道子網路
1. Hello 儀表板中，開啟您稍早建立的 hello VNET 01 虛擬網路資源。
2. 在 hello**設定**刀鋒視窗中，選取**子網路**。
3. tooadd hello 虛擬網路，閘道子網路選取**閘道子網路**。
   
    ![新增閘道子網路](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. 根據預設，hello 子網路名稱設定太**GatewaySubnet**。
   閘道子網路相當特殊。 toofunction 正常運作，他們必須使用 hello *GatewaySubnet*名稱。
5. 在**位址範圍**，確認 hello 位址是**10.0.11.0/24**。
6. 選取**確定**toocreate hello 閘道子網路。

### <a name="create-hello-virtual-network-gateway"></a>建立 hello 虛擬網路閘道
1. 在 hello Azure 入口網站，選取 **新增**。 
2. 跳過**Marketplace**，然後選取**網路**。
3. 從網路資源的 hello 清單中選取**虛擬網路閘道**。
4. 在 [名稱] 中，輸入 **GW1**。
5. 選取 hello**虛擬網路**項目 toochoose 虛擬網路。
   選取**VNET 01**從 hello 清單。
6. 選取 hello**公用 IP 位址**功能表項目。 當 hello**選擇公用 IP 位址**刀鋒視窗隨即開啟，選取**建立新**。
7. 在 [名稱] 中輸入 **GW1-PiP**，然後選取 [確定]。
8.  針對 [VPN 類型]，預設會選取 [依路由]。
    保留 hello**路由式**VPN 類型。
9. 確認 [訂用帳戶] 和 [位置] 均正確無誤。 您可以釘選 hello 資源 toohello 儀表板。 選取 [ **建立**]。

### <a name="create-hello-local-network-gateway"></a>建立 hello 區域網路閘道
hello 實作*區域網路閘道*此 Azure 堆疊評估部署會比實際的 Azure 部署中有些許不同。

在 Azure 部署中，區域網路閘道代表內部 （在 hello 租用戶） 實體裝置，您在 Azure 中使用 tooconnect tooa 虛擬網路閘道。 此 Azure 堆疊評估部署時，在 hello 連接的兩端是虛擬網路閘道 ！

關於此方式 toothink 更普遍為，hello 區域網路閘道資源一律表示 hello 遠端閘道在 hello hello 連線的另一端。 Hello 方式 hello Azure 堆疊開發套件的設計，因為您需要 tooprovide hello IP 位址的 hello 外部網路介面卡上 hello 網路位址轉譯 (NAT) 的 hello VM 其他 Azure 堆疊開發套件為 hello hello 公用 IP 位址區域網路閘道。 然後，您會建立 NAT 對應上 hello NAT VM toomake 確定兩端都已正確連接。


### <a name="create-hello-local-network-gateway-resource"></a>建立 hello 區域網路閘道資源
1. 登入 toohello Azure 堆疊實體機器 POC1。
2. 在 hello 使用者入口網站中，選取 **新增**。
3. 跳過**Marketplace**，然後選取**網路**。
4. 從 hello 清單中的資源，選取 **區域網路閘道**。
5. 在 [名稱] 中，輸入 **POC2-GW**。
6. 在**IP 位址**，輸入 POC2 hello BGPNAT 外部位址。 此位址在稍早 hello 網路組態資料表。
7. 在**位址空間**，hello 的 hello 您稍後建立 POC2 VNET 位址空間，請輸入**10.0.20.0/23**。
8. 確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。

### <a name="create-hello-connection"></a>建立 hello 連線
1. 在 hello 使用者入口網站中，選取 **新增**。
2. 跳過**Marketplace**，然後選取**網路**。
3. 從 hello 清單中的資源，選取 **連接**。
4. 在 hello**基本概念**設定 刀鋒視窗，hello**連線類型**，選取**站對站 (IPSec)**。
5. 選取 hello**訂用帳戶**，**資源群組**，和**位置**，然後選取**確定**。
6. 在 hello**設定**刀鋒視窗中，選取**虛擬網路閘道**，然後選取**GW1**。
7. 選取 [區域網路閘道]，然後選取 [POC2-GW]。
8. 在 [連線名稱] 中，輸入 **POC1-POC2**。
9. 在 [共用金鑰 (PSK)] 中輸入 **12345**，然後選取 [確定]。
10. 在 hello**摘要**刀鋒視窗中，選取**確定**。

### <a name="create-a-vm"></a>建立 VM
toovalidate hello 必定會行經 hello VPN 連線的資料，您需要 hello 虛擬機器 toosend 和每個 Azure 堆疊開發套件中接收資料。 立即在 POC1 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。

1. 在 hello Azure 入口網站，選取 **新增**。
2. 跳過**Marketplace**，然後選取**計算**。
3. 在虛擬機器的映像的 hello 清單中選取 hello **Windows Server 2016 Eval Datacenter**映像。
4. 在 hello**基本概念**刀鋒視窗，請在**名稱**，輸入**VM01**。
5. 輸入有效的使用者名稱和密碼。 在建立後，您可以使用 toohello VM 中的這個帳戶 toosign。
6. 提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。
7. 在 hello**大小**刀鋒視窗中的，這個執行個體，請選取虛擬機器大小，然後選取**選取**。
8. 在 hello**設定**刀鋒視窗中，接受 hello 預設值。 請確定該 hello **VNET 01**已選取虛擬網路。 確認該 hello 子網路設定得**10.0.10.0/24**。 然後選取 [確定]。
9. 在 hello**摘要**刀鋒視窗中，檢閱 hello 設定，然後選取**確定**。



## <a name="create-hello-network-resources-in-poc2"></a>建立 hello POC2 中的網路資源

hello 下一個步驟是 POC2 toocreate hello 網路資源。 下列指示的 hello 顯示如何使用 toocreate hello 資源 hello 使用者入口網站。

### <a name="sign-in-as-a-tenant"></a>以租用戶身分登入
服務系統管理員可以登入為租用戶 tootest hello 計劃、 提供項目及可能會使用其租用戶的訂用帳戶。 如果您還沒有租用戶帳戶，請先[建立租用戶帳戶](azure-stack-add-new-user-aad.md)再登入。

### <a name="create-hello-virtual-network-and-vm-subnet"></a>建立 hello 虛擬網路和 VM 子網路

1. 使用租用戶帳戶來登入。
2. 在 hello 使用者入口網站中，選取 **新增**。
3. 跳過**Marketplace**，然後選取**網路**。
4. 選取 [虛擬網路]。
5. 使用 hello 資訊出現稍早在 hello 網路組態資料表 tooidentify hello 值 hello POC2**名稱**，**位址空間**，**子網路名稱**，和**子網路位址範圍**。
6. 在**訂用帳戶**，會出現您稍早建立的 hello 訂用帳戶。
7. 針對 [資源群組]，建立資源群組，或選取 [使用現有的] (如果您已經有資源群組)。
8. 確認 hello 預設**位置**。
9. 選取**Pin toodashboard**。
10. 選取 [ **建立**]。

### <a name="create-hello-gateway-subnet"></a>建立 hello 閘道子網路
1. 開啟您建立 hello 虛擬網路資源 (**VNET 02**) 從 hello 儀表板。
2. 在 hello**設定**刀鋒視窗中，選取**子網路**。
3. 選取**閘道子網路**tooadd hello 虛擬網路閘道子網路。
4. hello hello 子網路名稱設定得**GatewaySubnet**預設。
   閘道子網路是特殊的且必須是此特定名稱 toofunction 正確。
5. 在 hello**位址範圍**欄位中，請確認 hello 位址**10.0.21.0/24**。
6. 選取**確定**toocreate hello 閘道子網路。

### <a name="create-hello-virtual-network-gateway"></a>建立 hello 虛擬網路閘道
1. 在 hello Azure 入口網站，選取 **新增**。  
2. 跳過**Marketplace**，然後選取**網路**。
3. 從網路資源的 hello 清單中選取**虛擬網路閘道**。
4. 在 [名稱] 中，輸入 **GW2**。
5. toochoose 虛擬網路中，選取**虛擬網路**。 然後選取**VNET 02**從 hello 清單。
6. 選取 [公用 IP 位址]。 當 hello**選擇公用 IP 位址**刀鋒視窗隨即開啟，選取**建立新**。
7. 在 [名稱] 中輸入 **GW2-PiP**，然後選取 [確定]。
8. 針對 [VPN 類型]，預設會選取 [依路由]。
    保留 hello**路由式**VPN 類型。
9. 確認 [訂用帳戶] 和 [位置] 均正確無誤。 您可以釘選 hello 資源 toohello 儀表板。 選取 [ **建立**]。

### <a name="create-hello-local-network-gateway-resource"></a>建立 hello 區域網路閘道資源

1. 在 hello POC2 使用者入口網站中，選取 **新增**。 
4. 跳過**Marketplace**，然後選取**網路**。
5. 從 hello 清單中的資源，選取 **區域網路閘道**。
6. 在 [名稱] 中，輸入 **POC1-GW**。
7. 在**IP 位址**，輸入稍早在 hello 網路組態資料表中列出的 POC1 hello BGPNAT 外部位址。
8. 在**位址空間**，POC1，從輸入 hello **10.0.10.0/23**的位址空間**VNET 01**。
9. 確認您的 [訂用帳戶]、[資源群組] 和 [位置] 正確無誤，然後選取 [建立]。

## <a name="create-hello-connection"></a>建立 hello 連線
1. 在 hello 使用者入口網站中，選取 **新增**。 
2. 跳過**Marketplace**，然後選取**網路**。
3. 從 hello 清單中的資源，選取 **連接**。
4. 在 [hello**基本**設定] 刀鋒視窗，hello**連線類型**，選擇**站對站 (IPSec)**。
5. 選取 hello**訂用帳戶**，**資源群組**，和**位置**，然後選取**確定**。
6. 在 hello**設定**刀鋒視窗中，選取**虛擬網路閘道**，然後選取**GW2**。
7. 選取 [區域網路閘道]，然後選取 [POC1-GW]。
8. 在 [連線名稱] 中，輸入 **POC2-POC1**。
9. 在 [共用金鑰 (PSK)] 中，輸入 **12345**。 如果您選擇不同的值，請記得它*必須*符合 hello hello POC1 建立的共用金鑰的值。 選取 [確定] 。
10. 檢閱 hello**摘要**刀鋒視窗中，然後再選取**確定**。

## <a name="create-a-virtual-machine"></a>建立虛擬機器
請立即在 POC2 中建立虛擬機器，然後將它放在您虛擬網路的 VM 子網路上。

1. 在 hello Azure 入口網站，選取 **新增**。
2. 跳過**Marketplace**，然後選取**計算**。
3. 在虛擬機器的映像的 hello 清單中選取 hello **Windows Server 2016 Eval Datacenter**映像。
4. 在 hello**基本概念**刀鋒視窗中，針對**名稱**，輸入**VM02**。
5. 輸入有效的使用者名稱和密碼。 在建立後，您可以使用 toohello 虛擬機器中的這個帳戶 toosign。
6. 提供 [訂用帳戶]、[資源群組] 和 [位置]，然後選取 [確定]。
7. 在 hello**大小**刀鋒視窗中，選取虛擬機器大小會針對這個執行個體，然後**選取**。
8. 在 hello**設定**刀鋒視窗中，您可以接受 hello 預設值。 請確定該 hello **VNET 02**虛擬網路已選取，並確認該 hello 子網路設定得**10.0.20.0/24**。 選取 [確定] 。
9. 檢閱上 hello 的 hello 設定**摘要**刀鋒視窗中，然後再選取**確定**。

## <a name="configure-hello-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a>設定 hello NAT 虛擬機器上的閘道周遊每個 Azure 堆疊開發套件
因為 hello Azure 堆疊開發套件是獨立且從部署的 hello 實體主機的網路隔離，所以 hello*外部*VIP，都不會實際外部連接的 toois hello 閘道的網路。 相反地，隱藏 hello VIP 網路執行網路位址轉譯之路由器的後面。 

路由器是 Windows Server 虛擬機器，稱為*AzS bgpnat01*、 執行路由及遠端存取服務 (RRAS) 角色中的 hello Azure 堆疊開發套件基礎結構。 您必須設定 NAT hello AzS bgpnat01 虛擬機器 tooallow hello 站對站 VPN 連線 tooconnect 兩端上。 

tooconfigure hello VPN 連線，您必須建立對應 hello hello BGPNAT 虛擬機器 toohello VIP 的 hello 邊緣閘道集區上的外部介面的靜態 NAT 對應路由。 VPN 連線中的每個連接埠都必須要有一個靜態 NAT 對應路由。

> [!NOTE]
> 只有「Azure Stack 開發套件」環境才需要此組態。
> 
> 

### <a name="configure-hello-nat"></a>設定 NAT hello
> [!IMPORTANT]
> 您必須為兩個「Azure Stack 開發套件」環境都完成此程序。

1. 判斷 hello**內部 IP 位址**toouse hello 下列 PowerShell 指令碼中的。 開啟 hello 虛擬網路閘道 （GW1 和 GW2），然後在 hello**概觀**刀鋒視窗中的，儲存 hello hello 值**公用 IP 位址**供日後使用。
![內部 IP 位址](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)
2. 登入 toohello Azure 堆疊實體機器 POC1。
3. 複製並編輯 hello 下列 PowerShell 指令碼。 tooconfigure hello NAT 上每個 Azure 堆疊開發套件，在提升權限的 Windows PowerShell ISE 中執行 hello 指令碼。 Hello 的指令碼中加入值 toohello*外部 BGPNAT 位址*和*內部 IP 位址*預留位置：

   ```powershell
   # Designate hello external NAT address for hello ports that use hello IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping toomap hello external address toohello Gateway
   # Public IP Address toomap hello ISAKMP port 500 for PHASE 1 of hello IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish hello complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. 在 POC2 上重複執行此程序。

## <a name="test-hello-connection"></a>測試 hello 連接
現在，建立 hello 站對站連線時，您應該驗證，就可以透過它流動的流量。 toovalidate，登入 tooone hello 您在其中一個 Azure 堆疊開發套件的環境中建立的虛擬機器。 然後，ping hello 虛擬機器，您在建立 hello 其他環境。 

tooensure 您傳送嗨流量透過 hello 站對站連線，請確定您 ping hello hello hello 遠端子網路，不 hello VIP 上的虛擬機器的直接 IP (DIP) 位址。 在此尋找 hello DIP 位址的 toodo hello hello 連線的另一端。 儲存供稍後使用 hello 位址。

### <a name="sign-in-toohello-tenant-vm-in-poc1"></a>租用戶登入 toohello POC1 中的 VM
1. 登入 toohello Azure 堆疊實體機器 POC1，，然後使用租用戶帳戶 toosign toohello 使用者入口網站中。
2. 在 hello 左的導覽列中，選取 **計算**。
3. 在 [hello] 清單中的 Vm，尋找**VM01**您先前建立並加以選取。
4. 在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**，然後開啟 hello VM01.rdp 檔案。
   
     ![[連線] 按鈕](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. 使用建立 hello 虛擬機器時所設定的 hello 帳戶登入。
6. 開啟已提高權限的 [Windows PowerShell] 視窗。
7. 輸入 **ipconfig /all**。
8. Hello 輸出中尋找 hello **IPv4 位址**，然後儲存供稍後使用 hello 位址。 這是您將 ping 從 POC2 的 hello 位址。 在 hello 範例環境，位址是**10.0.10.4**，但您的環境中可能會不同。 它應該會落在 hello **10.0.10.0/24**您先前建立的子網路。
9. toocreate 允許 hello 虛擬機器 toorespond toopings，執行下列 PowerShell 命令的 hello 的防火牆規則：

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-toohello-tenant-vm-in-poc2"></a>租用戶登入 toohello POC2 中的 VM
1. 登入 toohello Azure 堆疊實體機器 POC2，，然後使用租用戶帳戶 toosign toohello 使用者入口網站中。
2. 在 hello 左的導覽列中，按一下 **計算**。
3. 從虛擬機器的 hello 清單，尋找**VM02**您先前建立並加以選取。
4. 在 hello 刀鋒視窗中的 hello 虛擬機器，按一下 **連接**。
5. 使用建立 hello 虛擬機器時所設定的 hello 帳戶登入。
6. 開啟已提高權限的 [Windows PowerShell] 視窗。
7. 輸入 **ipconfig /all**。
8. 您應該會看到落在 **10.0.20.0/24** 內的 IPv4 位址。 Hello 範例環境中，在 hello 位址是**10.0.20.4**，但您的地址可能會不同。
9. toocreate 允許 hello 虛擬機器 toorespond toopings，執行下列 PowerShell 命令的 hello 的防火牆規則：

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. 從 hello POC2 上的虛擬機器，ping hello 虛擬機器上 POC1，透過 hello 通道。 toodo，ping hello 您記錄從 VM01 的 DIP。
   在 hello 範例環境，這是**10.0.10.4**，但會確定您記下您的實驗室中的 tooping hello 地址。 您應該會看到類似下列的 hello 的結果：
   
    ![成功的 Ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. Hello 遠端虛擬機器的回覆指出測試成功 ！ 您可以關閉 hello 虛擬機器視窗。 tootest 您的連線，您可以嘗試其他種類的檔案複本的資料傳輸。

### <a name="viewing-data-transfer-statistics-through-hello-gateway-connection"></a>檢視資料傳輸的統計資料進行 hello 閘道連線
如果您想的 tooknow 多少資料通過站對站連線，這項資訊位於 hello**連接**刀鋒視窗。 這項測試也是另一個 hello 剛傳送的 ping 的 tooverify 實際上八月份 hello VPN 連線的方式。

1. 您已登入中 POC2 toohello 租用戶虛擬機器，而使用您的租用戶帳戶 toosign toothe 使用者入口網站中。
2. 跳過**所有資源**，然後選取 hello **POC2 POC1**連線。 [連線] 隨即顯示。
4. 在 hello**連接**刀鋒視窗，hello 的統計資料**中的資料**和**資料輸出**出現。 在下列螢幕擷取畫面的 hello，hello 大量的屬性會設定 tooadditional 檔案傳輸。 您應該會在該處看到一些非零的值。
   
    ![資料輸入和輸出](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
