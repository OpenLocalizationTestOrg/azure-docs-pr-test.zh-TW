---
title: "aaaConfigure 外部 Alwayson 可用性群組接聽程式 |Microsoft 文件"
description: "此教學課程會逐步引導您完成在外部可存取所使用的 Azure 中建立一律在可用性群組接聽程式的步驟 hello 公用虛擬 IP 位址的 hello 相關聯的雲端服務。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>設定 Azure 中 Always On 可用性群組的外部接聽程式
> [!div class="op_single_selector"]
> * [內部接聽程式](../classic/ps-sql-int-listener.md)
> * [外部接聽程式](../classic/ps-sql-ext-listener.md)
> 
> 

本主題說明如何 tooconfigure Alwayson 可用性群組的外部存取上的接聽程式 hello 網際網路。 這樣做的原因產生關聯 hello 雲端服務的**公用虛擬 IP (VIP)** hello 接聽程式的位址。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

您的可用性群組可包含的複本為僅限內部部署、僅限 Azure，或同時跨內部部署和 Azure 的混合式組態。 Azure 複本可以位於 hello 相同區域或跨多個區域，使用多個虛擬網路 (Vnet)。 下列的 hello 步驟假設您已經有[設定可用性群組](../classic/portal-sql-alwayson-availability-groups.md)，但尚未設定接聽程式。

## <a name="guidelines-and-limitations-for-external-listeners"></a>外部接聽程式的指導方針和限制
請注意下列有關在 Azure 中的 hello 可用性群組接聽程式的指導方針，當您部署使用 hello 雲端服務公用 VIP 位址的 hello:

* hello 可用性群組接聽程式都支援 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2。
* hello 用戶端應用程式必須位於另一個則包含您的可用性群組 Vm 的 hello 不同雲端服務。 Azure 會支援伺服器直接傳回用戶端和伺服器 hello 相同雲端服務。
* 根據預設，這篇文章中的 hello 步驟會顯示如何 tooconfigure 一個接聽程式 toouse hello 雲端服務的虛擬 IP (VIP) 位址。 不過，它可能 tooreserve 而建立多個雲端服務的 VIP 位址。 這可讓您在此與不同的 VIP 相關聯的每個的多個接聽程式的發行項 toocreate toouse hello 步驟。 如需有關如何 toocreate 多個 VIP 位址，請參閱詳細[每個雲端服務的多個 Vip](../../../load-balancer/load-balancer-multivip.md)。
* 如果您要建立混合式環境的接聽程式，hello 與內部網路必須有連線能力 toohello 在加法 toohello 公用網際網路以 hello Azure 虛擬網路的站台對站 VPN。 在 hello Azure 子網路，hello 可用性群組接聽程式連線到。 只有透過 hello 個別雲端服務的 hello 公用 IP 位址
* 不支援外部接聽程式在相同雲端的服務，您也可以使用的內部接聽程式的 hello toocreate hello 內部負載平衡 (ILB)。

## <a name="determine-hello-accessibility-of-hello-listener"></a>判斷 hello hello 接聽程式的協助工具
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

本文著重於建立使用 **外部負載平衡**的接聽程式。 如果您想要的接聽程式是私用 tooyour 虛擬網路，請參閱提供的步驟設定這篇文章 hello 版本[搭配 ILB 一起運作的接聽程式](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>使用伺服器直接回傳建立負載平衡 VM 端點
外部負載平衡使用 hello 虛擬 hello 公用虛擬 IP 位址的 hello 裝載 Vm 的雲端服務。 因此您不需要 toocreate 或 hello 負載平衡器設定在此情況下。

您必須為每個主控 Azure 複本的 VM 建立負載平衡端點。 如果您在多個地區複本，每個複本用於該區域檔案必須在相同雲端服務中的 hello hello 相同的 VNet。 建立跨越多個 Azure 區域的可用性群組複本需要設定多個 VNet。 如需有關設定跨 VNet 連線的詳細資訊，請參閱[設定 VNet tooVNet 連線](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。

1. 在 hello Azure 入口網站，瀏覽 tooeach VM 裝載的複本和檢視 hello 詳細資料。
2. 按一下 hello**端點**hello Vm 的每個索引標籤。
3. 請確認該 hello**名稱**和**公用連接埠**您想要的 hello 接聽程式端點 toouse 已不在使用。 Hello 下列範例中，在 hello 名稱是"MyEndpoint"而 hello 通訊埠是"1433"。
4. 在您的本機用戶端上下載並安裝[hello 最新的 PowerShell 模組](https://azure.microsoft.com/downloads/)。
5. 啟動 **Azure PowerShell**。 新的 PowerShell 工作階段隨即開啟與 hello Azure 系統管理模組載入。
6. 執行 **Get-AzurePublishSettingsFile**。 這個指令程式會將您導向 tooa 瀏覽器 toodownload 發行設定檔案 tooa 本機目錄。 系統可能會提示您輸入 Azure 訂用帳戶的登入認證。
7. 執行 hello **Import-azurepublishsettingsfile** hello hello 路徑的命令發行您所下載的設定檔：
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Hello 發行設定檔匯入，您可以管理您的 Azure 訂閱 hello PowerShell 工作階段中。
    
1. 將以下 hello PowerShell 指令碼複製到文字編輯器，並設定 hello 變數值 toosuit 環境 （某些參數已提供預設值）。 請注意，是否您的可用性群組跨越 Azure 地區，您必須執行 hello 指令碼一次每個資料中心 hello 雲端服務和位於該資料中心的節點。
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. 一旦您已經設定 hello 變數，複製 hello 編寫指令碼從 hello 文字編輯器為您的 Azure PowerShell 工作階段 toorun 它。 如果 hello 提示依然顯示 >>，輸入的 ENTER 再次 toomake 確定 hello 指令碼開始執行。

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>必要時，請確認已安裝 KB2854082
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>開啟可用性群組節點中的 hello 防火牆連接埠
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>建立 hello 可用性群組接聽程式

兩個步驟建立 hello 可用性群組接聽程式。 首先，建立 hello 用戶端存取點叢集資源，並設定相依性。 其次，使用 PowerShell 設定 hello 叢集資源。

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>建立 hello 用戶端存取點並設定 hello 叢集相依性
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>在 PowerShell 中設定 hello 叢集資源
1. 外部負載平衡，您必須取得 hello 公用虛擬 IP 位址的 hello 雲端服務，其中包含您的複本。 登入 hello Azure 入口網站。 瀏覽 toohello 包含您的可用性群組 VM 的雲端服務。 開啟 hello**儀表板**檢視。
2. 請注意下方顯示 hello 位址**公用虛擬 IP (VIP) 位址**。 如果您的解決方案跨越多個 VNet，請針對包含主控複本之 VM 的每個雲端服務重複此步驟。
3. 其中一個 hello Vm 上 hello 以下 PowerShell 指令碼複製到文字編輯器並設定 hello 變數 toohello 您先前記下的值。
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. 之後設定 hello 變數，開啟提升權限的 Windows PowerShell 視窗，然後複製 hello 文字編輯器中的 hello 指令碼並貼到您的 Azure PowerShell 工作階段 toorun 它。 如果 hello 提示依然顯示 >>，輸入的 ENTER 再次 toomake 確定 hello 指令碼開始執行。
5. 在每個 VM 上重複此步驟。 此指令碼與 hello hello 雲端服務 IP 位址設定 hello IP 位址資源，並且設定類似 hello 探查連接埠其他參數。 當 hello IP 位址資源處於線上時，它可以回應 toohello 輪詢 hello 從稍早在本教學課程中建立的 hello 負載平衡端點的探查連接埠。

## <a name="bring-hello-listener-online"></a>使 hello 接聽程式連線
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>待處理項目
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>測試 hello 可用性群組接聽程式 (在 hello 相同 VNet)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>測試 hello 可用性群組接聽程式 (透過 hello 網際網路)
在順序從外部 hello 虛擬網路的 tooaccess hello 接聽程式，您必須使用外部/公用負載平衡 （如本主題所述） 而不 ILB，也就是只在 hello 內存取相同的 VNet。 在 hello 連接字串中，您可以指定 hello 雲端服務名稱。 例如，如果您擁有 hello 名稱的雲端服務*mycloudservice*，hello sqlcmd 陳述式將如下所示：

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

與 hello 上述範例中，不同的是 SQL 驗證必須使用，因為 hello 呼叫端無法使用 windows 驗證透過 hello 網際網路。 如需詳細資訊，請參閱 [Azure VM 中的 Always On 可用性群組：用戶端連線能力情況](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx)。 使用 SQL 驗證時，請確定您建立 hello 兩個複本上的相同登入。 如需疑難排解與可用性群組的登入的詳細資訊，請參閱[toomap 登入或使用包含 SQL 資料庫使用者 tooconnect tooother 複本和對應 tooavailability 資料庫](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx)。

如果 hello Alwayson 複本位於不同子網路中，用戶端必須指定**MultisubnetFailover = True** hello 連接字串中。 這會導致平行連接嘗試 tooreplicas hello 不同子網路中。 請注意，此情況包含跨區域的 Always On 可用性群組部署。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

