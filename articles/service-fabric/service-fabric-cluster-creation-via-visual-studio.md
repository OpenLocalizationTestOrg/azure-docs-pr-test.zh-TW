---
title: "使用 Visual Studio 設定 Service Fabric 叢集 | Microsoft Docs"
description: "說明如何使用 Azure 資源群組專案在 Visual Studio 中建立的 Azure Resource Manager 範本設定 Service Fabric 叢集"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: c43145b96cdbdfaa7e1893e50d027321fe4c0510
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>使用 Visual Studio 設定 Service Fabric 叢集
本文說明如何使用 Visual Studio 和 Azure Resource Manager 範本設定 Azure Service Fabric 叢集。 我們將使用 Visual Studio Azure 資源群組專案來建立範本。 建立範本之後，可以從 Visual Studio 直接將範本部署至 Azure。 也可從指令碼或在連續整合 (CI) 功能中使用它。

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>使用 Azure 資源群組專案建立 Service Fabric 叢集範本
若要開始進行，請開啟 Visual Studio 並建立 Azure 資源群組專案 (可在 **Cloud** 資料夾下取得)：

![已選取 Azure 資源群組專案的 [新增專案] 對話方塊][1]

您可以為此專案建立新的 Visual Studio 方案，或將它加入至現有的方案。

> [!NOTE]
> 如果在 Cloud 節點之下看不到 Azure 資源群組專案，表示尚未安裝 Azure SDK。 啟動 Web Platform Installer (如果尚未這麼做，請[立即安裝](http://www.microsoft.com/web/downloads/platform.aspx) )，然後搜尋 "Azure SDK for .NET" 並安裝與您的 Visual Studio 版本相容的版本。
> 
> 

按 [確定] 按鈕之後，Visual Studio 會要求您選取您想要建立的資源管理員範本：

![已選取 Service Fabric 叢集範本的 [選取 Azure 範本] 對話方塊][2]

選取 [Service Fabric 叢集] 範本，然後再按一次 [確定] 按鈕。 現在已建立專案與資源管理員範本。

## <a name="prepare-the-template-for-deployment"></a>準備範本以供部署
在部署範本以建立叢集之前，您必須提供必要的範本參數值。 這些參數值讀取自 `ServiceFabricCluster.parameters.json` 檔案，該檔案位於資源群組專案的 `Templates` 資料夾。 開啟該檔案並提供下列值：

| 參數名稱 | 說明 |
| --- | --- |
| adminUserName |Service Fabric 電腦 (節點) 的系統管理員帳戶名稱。 |
| certificateThumbprint |保護叢集安全的憑證指紋。 |
| sourceVaultResourceId |用來保護叢集的憑證儲存所在之金鑰保存庫的資源識別碼  。 |
| certificateUrlValue |叢集安全性憑證的 URL。 |

Visual Studio Service Fabric 資源管理員範本會建立一個受憑證保護的安全叢集。 此憑證是利用最後三個範本參數 (`certificateThumbprint`、`sourceVaultValue` 和 `certificateUrlValue`) 來識別，其必須存在於 **Azure 金鑰保存庫**中。 如需如何建立叢集安全性憑證的詳細資訊，請參閱 [Service Fabric 叢集安全性案例](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) 一文。

## <a name="optional-change-the-cluster-name"></a>選擇性︰變更叢集名稱
每個 Service Fabric 叢集都有一個名稱。 在 Azure 中建立網狀架構叢集時，叢集名稱會 (與 Azure 區域一起) 決定叢集的網域名稱系統 (DNS) 名稱。 例如，如果您將叢集命名為 `myBigCluster`，而且將裝載新叢集的資源群組位置 (Azure 區域) 是美國東部，則叢集的 DNS 名稱將是 `myBigCluster.eastus.cloudapp.azure.com`。

預設會自動產生叢集名稱，而且「叢集」前置詞後面會附加一個隨機的尾碼，使該名稱變成唯一的。 如此便可以很容易使用範本做為 **連續整合** (CI) 系統的一部分。 如果您想要為叢集使用特定名稱，一個對您有意義的名稱，請將 Resource Manager 範本檔案 (`ServiceFabricCluster.json`) 中 `clusterName` 變數值設定為您所選擇的名稱。 該名稱是該檔案中定義的第一個變數。

## <a name="optional-add-public-application-ports"></a>選擇性：新增公用應用程式連接埠
您也可能想變更叢集的公用應用程式連接埠再部署它。 根據預設，範本只會開啟兩個公用 TCP 連接埠 (80 和 8081)。 如果您的應用程式需要更多，請修改範本中的 Azure 負載平衡器定義。 此定義儲存在主要範本檔案 (`ServiceFabricCluster.json`) 中。 開啟該檔案，並搜尋 `loadBalancedAppPort`。 每個連接埠會與三個成品相關聯：

1. 範本參數：定義連接埠的 TCP 連接埠值：
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. 探查：定義 Azure 負載平衡器在容錯移轉到另一個節點之前，會嘗試使用特定 Service Fabric 節點的頻率和時間長度。 探查是負載平衡器資源的一部分。 以下是第一個預設應用程式連接埠的探查定義：
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. 將連接埠和探查繫結在一起的「負載平衡規則」  ，可在一組 Service Fabric 叢集節點上啟用負載平衡：
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   如果您打算部署至叢集的應用程式需要更多連接埠，您可以透過建立其他探查和負載平衡規則定義來新增連接埠。 如需如何透過 Resource Manager 範本使用 Azure Load Balancer 的詳細資訊，請參閱 [開始使用範本建立內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-template.md)。

## <a name="deploy-the-template-by-using-visual-studio"></a>使用 Visual Studio 部署範本
在`ServiceFabricCluster.param.dev.json` 中儲存所有必要的參數值後，您就可以部署範本和建立 Service Fabric 叢集。 以滑鼠右鍵按一下 Visual Studio [方案總管] 中的資源群組專案，然後選擇 [部署 | 新增部署...] 。 如有必要，Visual Studio 會顯示 [部署到資源群組] 對話方塊，要求您向 Azure 進行驗證：

![[部署到資源群組] 對話方塊][3]

此對話方塊可讓您選擇叢集的現有資源管理員資源群組，並提供給您建立新資源群組的選項。 通常對 Service Fabric 叢集使用個別的資源群組是很合理的。

按 [部署] 按鈕後，Visual Studio 就會提示您確認範本參數值。 按 [儲存]  按鈕。 有一個參數沒有持續的值：叢集的系統管理員帳戶密碼。 當 Visual Studio 提示您提供密碼值時，您必須這麼做。

> [!NOTE]
> 從 Azure SDK 2.9 開始，Visual Studio 支援在部署期間從 **Azure 金鑰保存庫**讀取密碼。 在 [範本參數] 對話方塊中，注意 `adminPassword` 參數文字方塊右邊有小的「金鑰」圖示。 這個圖示可讓您選取現有的金鑰保存庫密碼做為叢集的系統管理密碼。 務必先在金鑰保存庫的進階存取原則中啟用範本部署的 Azure Resource Manager 存取權。 
> 
> 

您可以在 Visual Studio 的 [輸出] 視窗中監視部署程序的進度。 一旦完成範本部署，即可使用您的新叢集！

> [!NOTE]
> 如果 PowerShell 未曾用來從您目前使用的電腦管理 Azure，則需要進行一些內部管理。
> 
> 1. 執行 [`Set-ExecutionPolicy`](https://technet.microsoft.com/library/hh849812.aspx) 命令以啟用 PowerShell 指令碼。 開發電腦通常可接受「不受限制」原則。
> 2. 決定是否允許從 Azure PowerShell 命令收集診斷資料，並且視需要執行 [`Enable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619303.aspx) 或 [`Disable-AzureRmDataCollection`](https://msdn.microsoft.com/library/mt619236.aspx)。 這可在範本部署期間避免不必要的提示。
> 
> 

如果有任何錯誤，請移至 [Azure 入口網站](https://portal.azure.com/) ，並開啟您要部署的目標資源群組。 按一下 [所有設定]，然後按一下設定刀鋒視窗上的 [部署]。 資源群組部署失敗會在通知中留下詳細的診斷資訊。

> [!NOTE]
> Service Fabric 叢集需要有一定數量的節點運作中，以維護可用性並維持狀態 - 稱為「維持仲裁」。 因此，除非您已先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)，否則關閉叢集中的所有電腦並不安全。
> 
> 

## <a name="next-steps"></a>後續步驟
* [了解如何使用 Azure 入口網站設定 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)
* [了解如何使用 Visual Studio 管理和部署 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
