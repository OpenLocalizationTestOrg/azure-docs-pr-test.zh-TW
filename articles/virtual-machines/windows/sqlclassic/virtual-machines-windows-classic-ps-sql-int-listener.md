---
title: "Always On 可用性群組在 Azure 中的 ILB 接聽程式 aaaConfigure |Microsoft 文件"
description: "本教學課程使用 hello 傳統部署模型，以建立的資源，並且會使用內部負載平衡器的 Azure 中建立 Always On 可用性群組接聽程式。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>在 Azure 中設定 Always On 可用性群組的 ILB 接聽程式
> [!div class="op_single_selector"]
> * [內部接聽程式](../classic/ps-sql-int-listener.md)
> * [外部接聽程式](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>概觀

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../azure-resource-manager/resource-manager-deployment-model.md) 和傳統。 本文涵蓋 hello hello 傳統部署模型使用。 建議最新的部署使用 hello 資源管理員的模型。

tooconfigure Always On 可用性群組接聽程式在 hello 資源管理員模型中，請參閱[在 Azure 中設定 Alwayson 可用性群組的負載平衡器](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md)。

您的可用性群組可包含的複本為僅限內部部署或僅限 Azure，或同時跨內部部署和 Azure 的混合式組態。 Azure 複本可以位於 hello 相同區域或跨多個使用多個虛擬網路的區域。 hello 本文章中的程序假設您已經有[設定可用性群組](../classic/portal-sql-alwayson-availability-groups.md)但尚未設定接聽程式。

## <a name="guidelines-and-limitations-for-internal-listeners"></a>內部接聽程式指導方針和限制
hello 使用可用性群組接聽程式在 Azure 中使用內部負載平衡器 (ILB) 是主體 toohello 指導方針：

* hello 可用性群組接聽程式都支援 Windows Server 2008 R2、 Windows Server 2012 和 Windows Server 2012 R2。
* 只有設定其中一種內部的可用性群組接聽程式支援每個雲端服務，因為 hello 接聽程式是 toohello ILB，且沒有每個雲端服務只能有一個 ILB。 不過，很可能 toocreate 多個外部接聽程式。 如需詳細資訊，請參閱[在 Azure 中設定 Always On 可用性群組的外部接聽程式](../classic/ps-sql-ext-listener.md)。

## <a name="determine-hello-accessibility-of-hello-listener"></a>判斷 hello hello 接聽程式的協助工具
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

本文著重於建立使用 ILB 的接聽程式。 如果您需要的公用或外部的接聽程式，請參閱這篇文章討論設定總 hello 版本[外部接聽程式](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>使用伺服器直接回傳建立負載平衡 VM 端點
您第一次建立 ILB，稍後執行本節中的 hello 指令碼。

為每部主控 Azure 複本的 VM 建立負載平衡端點。 如果您在多個地區複本，每個複本用於該區域檔案必須在相同雲端服務中的 hello hello 相同 Azure 虛擬網路。 建立跨越多個 Azure 區域的可用性群組複本需要設定多個虛擬網路。 如需跨虛擬網路連線設定的詳細資訊，請參閱[設定虛擬網路 toovirtual 網路連接性](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)。

1. 在 hello Azure 入口網站，移 tooeach VM 主控複本 tooview hello 詳細資料。

2. 按一下 hello**端點**每個 VM 索引標籤。

3. 請確認該 hello**名稱**和**公用連接埠**的 hello toouse 不存在於使用您想要的接聽程式端點。 在本節中的 hello 範例，hello 名稱是*MyEndpoint*，而 hello 通訊埠是*1433年*。

4. 在您的本機用戶端上下載並安裝最新的 hello [PowerShell 模組](https://azure.microsoft.com/downloads/)。

5. 啟動 Azure PowerShell。  
    開啟新的 PowerShell 工作階段，以 hello Azure 系統管理模組載入。

6. 執行 `Get-AzurePublishSettingsFile`。 這個指令程式會將您導向 tooa 瀏覽器 toodownload 發行設定檔案 tooa 本機目錄。 系統可能會提示您輸入 Azure 訂用帳戶的登入認證。

7. 執行下列 hello `Import-AzurePublishSettingsFile` hello hello 路徑的命令發行您所下載的設定檔：

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Hello 發行之後匯入設定檔，您可以管理您的 Azure 訂閱 hello PowerShell 工作階段中。

8. 針對 *ILB*，指派靜態 IP 位址。 藉由執行下列命令的 hello 檢查 hello 目前的虛擬網路設定：

        (Get-AzureVNetConfig).XMLConfiguration
9. 請注意 hello*子網路*hello 裝載 hello 複本 hello Vm 所在的子網路的名稱。 Hello 指令碼中的 hello $SubnetName 參數會使用此名稱。

10. 請注意 hello *VirtualNetworkSite*命名和 hello 啟動*AddressPrefix* hello 子網路，其中包含裝載 hello 複本 hello Vm。 尋找可用的 IP 位址，藉由傳遞兩個值 toohello`Test-AzureStaticVNetIP`命令，並藉由檢查 hello *AvailableAddresses*。 例如，如果 hello 虛擬網路稱為*MyVNet*開始的子網路位址範圍且*172.16.0.128*，hello 下列命令會列出可用的位址：

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. 選取其中一個 hello 可用的位址，並使用 hello $ILBStaticIP hello 下一個步驟中的 hello 指令碼參數中。

12. 複製下列 PowerShell 指令碼 tooa 文字編輯器的 hello，並設定您的環境的 hello 變數值 toosuit。 某些參數已提供預設值。  

    使用同質群組的現有部署無法新增 ILB。 如需有關 ILB 需求的詳細資訊，請參閱[內部負載平衡器概觀](../../../load-balancer/load-balancer-internal-overview.md)。

    此外，如果您的可用性群組跨越 Azure 地區，您必須執行 hello 指令碼一次每個資料中心 hello 雲端服務和位於該資料中心的節點。

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. 設定 hello 變數之後，複本 hello 編寫指令碼從 hello 文字編輯器 tooyour PowerShell 工作階段 toorun 它。 如果 hello 提示依然顯示 **>>** ，按下的 Enter 再次 toomake 確定 hello 指令碼開始執行。

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>必要時，請確認已安裝 KB2854082
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>開啟可用性群組節點中的 hello 防火牆連接埠
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>建立 hello 可用性群組接聽程式

兩個步驟建立 hello 可用性群組接聽程式。 首先，建立 hello 用戶端存取點叢集資源，並設定相依性。 第二，在 PowerShell 中設定 hello 叢集資源。

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>建立 hello 用戶端存取點並設定 hello 叢集相依性
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>在 PowerShell 中設定 hello 叢集資源
1. 對於 ILB，您必須使用 hello 的 hello 稍早建立的 ILB 的 IP 位址。 此 IP 位址在 PowerShell 中，使用下列指令碼的 hello tooobtain:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. 其中一個 hello Vm 上的作業系統 tooa 文字編輯器中，複製 hello PowerShell 指令碼，然後設定 hello 變數 toohello 您先前記下的值。

    適用於 Windows Server 2012 或更新版本，請使用下列指令碼的 hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Windows Server 2008 R2，使用下列指令碼的 hello:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. 設定 hello 的變數，開啟提升權限的 Windows PowerShell 視窗之後，貼上 hello 編寫指令碼從 hello 文字編輯器為您的 PowerShell 工作階段 toorun 它。 如果 hello 提示依然顯示 **>>** ，按 Enter 鍵一次 toomake 確定 hello 指令碼開始執行。

4. 重複上述步驟，為每個 VM 的 hello。  
    此指令碼以 hello hello 雲端服務 IP 位址設定 hello IP 位址資源，並設定其他參數，例如 hello 探查連接埠。 當 hello IP 位址資源處於線上時，它可以回應 toohello 輪詢從 hello 負載平衡的端點，您稍早建立的 hello 探查連接埠。

## <a name="bring-hello-listener-online"></a>使 hello 接聽程式連線
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>待處理項目
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>測試 hello 可用性群組接聽程式 (在 hello 相同虛擬網路)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>後續步驟
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
