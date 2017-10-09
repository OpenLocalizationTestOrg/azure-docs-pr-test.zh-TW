---
title: "使用 Visual Studio Service Fabric 叢集 aaaSetting |Microsoft 文件"
description: "描述如何 tooset 註冊 Service Fabric 叢集所使用的 Azure 資源群組專案在 Visual Studio 中所建立的 Azure Resource Manager 範本"
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
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>使用 Visual Studio 設定 Service Fabric 叢集
本文說明如何使用 Visual Studio 和 Azure Resource Manager 範本 tooset 向上 Azure Service Fabric 叢集。 我們將使用 Visual Studio Azure 資源群組專案 toocreate hello 範本。 建立 hello 範本之後，它可以部署直接從 Visual Studio tooAzure。 也可從指令碼或在連續整合 (CI) 功能中使用它。

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>使用 Azure 資源群組專案建立 Service Fabric 叢集範本
tooget 啟動中，開啟 Visual Studio 並建立 Azure 資源群組專案 (即在 hello**雲端**資料夾):

![已選取 Azure 資源群組專案的 [新增專案] 對話方塊][1]

您可以建立新的 Visual Studio 方案，此專案，或將它加入 tooan 現有的方案。

> [!NOTE]
> 如果看不到 hello Azure 資源群組專案 hello 雲端 節點下的，表示您沒有 hello 已安裝 Azure SDK。 啟動 Web Platform Installer ([立即安裝](http://www.microsoft.com/web/downloads/platform.aspx)如果您還沒有)，然後搜尋 < Azure SDK for.NET 中，並安裝 hello 版本與您的 Visual Studio 版本相容。
> 
> 

點擊 hello [確定] 按鈕之後，Visual Studio 會詢問您想 toocreate tooselect hello Resource Manager 範本：

![已選取 Service Fabric 叢集範本的 [選取 Azure 範本] 對話方塊][2]

再次選取 hello Service Fabric 叢集範本和叫用的 hello [確定] 按鈕。 hello 專案和 hello Resource Manager 範本現在已建立。

## <a name="prepare-hello-template-for-deployment"></a>準備部署的 hello 範本
Hello 範本是已部署的 toocreate hello 叢集之前，您必須提供所需的 hello 範本參數的值。 這些參數值從 hello 讀取`ServiceFabricCluster.parameters.json`檔案，位於 hello `Templates` hello 資源群組專案的資料夾。 開啟 hello 檔案，並提供下列值的 hello:

| 參數名稱 | 說明 |
| --- | --- |
| adminUserName |hello hello 系統管理員帳戶名稱的 Service Fabric 機器 （節點）。 |
| certificateThumbprint |hello，可保護 hello 叢集 hello 憑證的指紋。 |
| sourceVaultResourceId |hello*資源識別碼*hello 金鑰保存庫，可保護 hello 叢集 hello 憑證的儲存位置。 |
| certificateUrlValue |hello hello 叢集安全性憑證 URL。 |

hello Visual Studio 服務網狀架構資源管理員範本會建立安全的叢集所保護的憑證。 此憑證由 hello 最後三個樣板參數 (`certificateThumbprint`， `sourceVaultValue`，和`certificateUrlValue`)，且必須存在於**Azure 金鑰保存庫**。 如需有關如何 toocreate hello 叢集安全性憑證的詳細資訊，請參閱[Service Fabric 叢集安全性案例](service-fabric-cluster-security.md#x509-certificates-and-service-fabric)發行項。

## <a name="optional-change-hello-cluster-name"></a>選擇性： 變更 hello 叢集名稱
每個 Service Fabric 叢集都有一個名稱。 在 Azure 中建立網狀架構叢集時，叢集名稱會決定 （搭配 hello Azure 地區) hello hello 叢集的網域名稱系統 (DNS) 名稱。 例如，如果您將檔案命名您的叢集`myBigCluster`，和將裝載 hello 新叢集的 hello 資源群組的 hello 位置 （Azure 地區） 是美國東部、 hello hello 叢集 DNS 名稱會是`myBigCluster.eastus.cloudapp.azure.com`。

根據預設 hello 叢集名稱是自動產生，而且後面會附加隨機尾碼 tooa 「 叢集 」 前置詞。 這使得您可以非常輕易 toouse hello 範本的一部分**連續整合**(CI) 系統。 如果您想 toouse 之特定名稱的叢集，一個是有意義的 tooyou 設定 hello hello 值`clusterName`hello 資源管理員範本檔案中的變數 (`ServiceFabricCluster.json`) tooyour 選擇的名稱。 它是定義在該檔案中的 hello 第一個變數。

## <a name="optional-add-public-application-ports"></a>選擇性：新增公用應用程式連接埠
您也可以 toochange hello 公用應用程式連接埠 hello 叢集部署之前。 根據預設，只有兩個公用 TCP 連接埠 （80 和 8081） 會開啟 hello 範本。 如果您需要多個應用程式，可以修改 hello 範本中的 hello Azure 負載平衡器定義。 hello 定義會儲存在 hello 主要範本檔案 (`ServiceFabricCluster.json`)。 開啟該檔案，並搜尋 `loadBalancedAppPort`。 每個連接埠會與三個成品相關聯：

1. 定義 hello hello 連接埠的 TCP 連接埠值的範本變數：
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. A*探查*定義頻率和時間的 hello Azure 負載平衡器會嘗試透過其中一個 tooanother toouse 特定 Service Fabric 節點失敗之前。 hello 探查是 hello 資源負載平衡器的一部分。 以下是第一個預設應用程式連接埠 hello hello 探查定義：
   
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
3. A*負載平衡規則*，結合 hello 連接埠和 hello 探查，啟用負載平衡的一組 Service Fabric 叢集節點：
   
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
   如果您計劃 toodeploy toohello 叢集 hello 應用程式需要更多連接埠，您可以將它們加入建立額外的探查和負載平衡規則定義。 如需有關如何 toowork 與 Azure 負載平衡器透過資源管理員範本，請參閱[開始建立使用範本的內部負載平衡器](../load-balancer/load-balancer-get-started-ilb-arm-template.md)。

## <a name="deploy-hello-template-by-using-visual-studio"></a>使用 Visual Studio 部署 hello 範本
儲存之後所有 hello 中的必要的參數值`ServiceFabricCluster.param.dev.json`檔案中，您已準備好 toodeploy hello 範本，並建立 Service Fabric 叢集。 Visual Studio 方案總管] 中的 hello 資源群組專案上按一下滑鼠右鍵，然後選擇 [**部署 |新增部署...**.如果有必要，Visual Studio 會顯示 hello**部署 tooResource 群組**對話方塊，詢問您 tooauthenticate tooAzure:

![部署 tooResource 群組對話方塊][3]

hello 對話方塊可讓您選擇 hello 叢集和新 hello 選項 toocreate 提供現有的資源管理員資源群組。 它通常使意義 toouse Service Fabric 叢集的個別資源群組。

點擊 hello 部署按鈕之後，Visual Studio 會提示您 tooconfirm hello 範本參數的值。 叫用的 hello**儲存** 按鈕。 一個參數並沒有持續的值： hello hello 叢集的系統管理帳戶密碼。 Visual Studio 會提示您輸入其中一個時，您會需要 tooprovide 密碼值。

> [!NOTE]
> 從 Azure SDK 2.9 開始，Visual Studio 支援在部署期間從 **Azure 金鑰保存庫**讀取密碼。 在 [hello 範本參數] 對話方塊，請注意該 hello`adminPassword`參數文字方塊右 hello 上具有少許的 「 金鑰 」 圖示。 此圖示可讓您現有的金鑰保存庫密碼 tooselect 當做 hello hello 叢集系統管理密碼。 您只需要確定 toofirst 啟用 hello 進階存取原則中的金鑰保存庫的範本部署的 Azure 資源管理員存取權。 
> 
> 

您可以監視 hello hello Visual Studio 輸出視窗中的 hello 部署程序的進度。 Hello 範本部署完成後，您的新叢集將會是準備 toouse ！

> [!NOTE]
> 如果 PowerShell 永遠不會使用從您目前使用的 hello 機器 tooadminister Azure，您需要 toodo 極小的內部管理。
> 
> 1. 啟用 PowerShell 指令碼執行 hello [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx)命令。 開發電腦通常可接受「不受限制」原則。
> 2. 決定是否從 Azure PowerShell 命令，然後執行 tooallow 診斷資料收集[ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx)或[ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx)視。 這可在範本部署期間避免不必要的提示。
> 
> 

如果有任何錯誤，請移至 toohello [Azure 入口網站](https://portal.azure.com/)與您部署到開啟的 hello 資源群組。 按一下**所有設定**，然後按一下 [**部署**hello 設定] 刀鋒視窗上。 資源群組部署失敗會在通知中留下詳細的診斷資訊。

> [!NOTE]
> Service Fabric 叢集需要 toomaintain 可用性節點 toobe 數目和保留狀態-參照 tooas 「 維持仲裁 」。 因此，它不是向 hello 機器 hello 叢集中的所有安全 tooshut 除非您先執行[狀態的完整備份](service-fabric-reliable-services-backup-restore.md)。
> 
> 

## <a name="next-steps"></a>後續步驟
* [深入了解設定使用 hello Azure 入口網站的 Service Fabric 叢集](service-fabric-cluster-creation-via-portal.md)
* [深入了解如何 toomanage 及部署 Service Fabric 應用程式使用 Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
