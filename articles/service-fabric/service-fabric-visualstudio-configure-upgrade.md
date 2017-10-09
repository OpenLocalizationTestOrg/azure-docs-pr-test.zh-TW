---
title: "Service Fabric 應用程式的 aaaConfigure hello 升級 |Microsoft 文件"
description: "了解如何 tooconfigure hello 升級 Service Fabric 應用程式使用 Microsoft Visual Studio 的設定。"
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a>Service Fabric 應用程式的 hello 升級 Visual Studio 中設定
Visual Studio tools for Azure Service Fabric 提供升級支援發行 toolocal 或遠端叢集。 有三種情況，您想在其中 tooupgrade 您應用程式 tooa 較新版本而不是取代 hello 應用程式在測試和偵錯期間：

* 應用程式資料 hello 升級期間將不會遺失。
* 可用性維持高的所以將不會有任何服務中斷，hello 在升級期間，是否有足夠的服務執行個體分散到升級網域。
* 在應用程式進行升級時，可以對該應用程式進行測試。

## <a name="parameters-needed-tooupgrade"></a>需要 tooupgrade 參數。
您可以選擇的部署類型有兩種：一般或升級。 標準的部署會清除任何先前的部署資訊和 hello 叢集上的資料，同時升級部署會保留它。 當您升級 Visual Studio 中的 Service Fabric 應用程式時，您需要 tooprovide 應用程式升級參數和健全狀況檢查原則。 說明參數的應用程式升級控制項 hello 升級，而健康情況檢查原則可讓您判斷 hello 升級是否成功。 如需詳細資訊，請參閱 [Service Fabric 應用程式升級：升級參數](service-fabric-application-upgrade-parameters.md) 。

有三種升級模式：Monitored、UnmonitoredAuto 及 UnmonitoredManual。

* 監視升級會自動執行 hello 升級應用程式健全狀況檢查。
* UnmonitoredAuto 升級自動化 hello 升級，但略過 hello 應用程式健全狀況檢查。
* 當您進行 UnmonitoredManual 升級時，您需要 toomanually 升級每個升級網域。

每一種升級模式都需要一組不同的參數。 請參閱[應用程式升級參數](service-fabric-application-upgrade-parameters.md)toolearn 更多關於 hello 可用的升級選項。

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a>在 Visual Studio 中升級 Service Fabric 應用程式
如果您使用 hello Visual Studio Service Fabric 工具 tooupgrade Service Fabric 應用程式，您可以指定發佈程序 toobe 升級，而不是標準的部署方式是檢查 hello **hello 應用程式升級**檢查方塊。

### <a name="tooconfigure-hello-upgrade-parameters"></a>tooconfigure hello 升級參數
1. 按一下 hello**設定**按鈕下一步 toohello 核取方塊。 hello**編輯升級參數** 對話方塊隨即出現。 hello**編輯升級參數**對話方塊支援 hello 監視、 UnmonitoredAuto 和 UnmonitoredManual 升級模式。
2. 選取您想 toouse，然後填寫 hello 參數方格 hello 升級模式。

    每個參數都有預設值。 hello 選擇性參數*DefaultServiceTypeHealthPolicy*接受輸入雜湊資料表。 以下是範例的 hello 雜湊資料表輸入格式*DefaultServiceTypeHealthPolicy*:

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    *ServiceTypeHealthPolicyMap*在 hello 會採用雜湊資料表輸入另一個選擇性參數是下列格式：

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    以下是一個真實範例：

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. 如果您選取 UnmonitoredManual 升級模式，您必須手動啟動 PowerShell 主控台 toocontinue 並完成 hello 升級程序。 請參閱太[Service Fabric 應用程式升級： 進階主題](service-fabric-application-upgrade-advanced.md)toolearn 如何手動升級運作方式。

## <a name="upgrade-an-application-by-using-powershell"></a>使用 PowerShell 升級應用程式
您可以使用 PowerShell cmdlet tooupgrade Service Fabric 應用程式。 如需詳細資訊，請參閱 [Service Fabric 應用程式升級教學課程](service-fabric-application-upgrade-tutorial.md)和 [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx)。

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a>Hello 應用程式資訊清單檔中指定的健全狀況檢查原則
Service Fabric 應用程式中的每個服務可以有其本身的健全狀況原則參數，覆寫 hello 預設值。 您可以提供這些 hello 應用程式資訊清單檔中的參數值。

hello 下列範例顯示如何 tooapply 唯一的健全狀況檢查 hello 應用程式資訊清單中的每個服務的原則。

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a>後續步驟
如需有關部署應用程式的詳細資訊，請參閱 [在 Azure Service Fabric 中部署現有的應用程式](service-fabric-deploy-existing-app.md)。