---
title: "aaaUpgrade Azure Service Fabric 叢集 |Microsoft 文件"
description: "升級 hello Service Fabric 程式碼和/或執行 Service Fabric 叢集，包括設定叢集更新模式，升級憑證，新增應用程式連接埠，執行發行作業系統修補程式的組態，並以此類推。 執行 hello 升級時，您可以預期什麼？"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 15190ace-31ed-491f-a54b-b5ff61e718db
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/10/2017
ms.author: chackdan
ms.openlocfilehash: 94ac3833ec0810f79de06ecb50f254028fa90408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-an-azure-service-fabric-cluster"></a>升級 Azure Service Fabric 叢集
> [!div class="op_single_selector"]
> * [Azure 叢集](service-fabric-cluster-upgrade.md)
> * [獨立叢集](service-fabric-cluster-upgrade-windows-server.md)
> 
> 

對於任何現代的系統，可升級性的設計是產品金鑰 tooachieving 長期成功。 Azure Service Fabric 叢集是您所擁有，但部分由 Microsoft 管理的資源。 本文說明自動管理的部分以及您可以自行設定的部分。

## <a name="controlling-hello-fabric-version-that-runs-on-your-cluster"></a>控制在您的叢集執行的 hello fabric 版本
您可以設定叢集 tooreceive 自動架構升級為 Microsoft 發行，或者您可以選取您要叢集 toobe 支援的網狀架構版本。

您可以設定 hello"upgradeMode"hello 入口網站或使用資源管理員在建立 hello 時或稍後即時叢集上的叢集設定 

> [!NOTE]
> 請確定 tookeep 您永遠執行支援的網狀架構版本的叢集。 如下，當我們宣佈 hello 發行新版的 service fabric hello 舊版標示為的支援即將結束後的 60 天內從該日期的最小值。 hello hello 新版本上經過宣布[hello 服務網狀架構小組部落格上](https://blogs.msdn.microsoft.com/azureservicefabric/)。 hello 新版本，就可用 toochoose。 
> 
> 

14 天先前 toohello 到期的 hello 發行您的叢集正在執行，就會產生健全狀況事件，以您的叢集到警告健全狀況狀態。 您升級 tooa 支援的 fabric 版本之前，hello 叢集會維持在警告狀態。

### <a name="setting-hello-upgrade-mode-via-portal"></a>透過入口網站設定 hello 升級模式
當您建立 hello 叢集時，您可以設定 hello 叢集 tooautomatic 或手動。

![Create_Manualmode][Create_Manualmode]

您可以設定 hello 叢集 tooautomatic 或手動在即時的叢集上，使用 hello 管理體驗。 

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-portal"></a>升級 tooa tooManual 模式透過入口網站設定的叢集上的新版本。
tooupgrade tooa 新版本，您只需要 toodo 是從 hello 下拉式清單中選取 hello 可用版本和儲存。 hello Fabric 升級取得自動開始。 hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。

如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 更多有關此文件 tooread 捲動 tooset 這些自訂的健全狀況原則。 

一旦您修正導致 hello 復原 hello 問題，您需要 tooinitiate hello 升級同樣地，由下列 hello 與之前相同的步驟。

![Manage_Automaticmode][Manage_Automaticmode]

### <a name="setting-hello-upgrade-mode-via-a-resource-manager-template"></a>設定資源管理員範本透過 hello 升級模式
加入 hello"upgradeMode 」 組態 toohello Microsoft.ServiceFabric/clusters 資源定義和組 hello"clusterCodeVersion"tooone hello 的支援如下所示的網狀架構版本，然後再部署 hello 範本。 hello"upgradeMode"有效值為 「 手動 」 或 「 自動 」

![ARMUpgradeMode][ARMUpgradeMode]

#### <a name="upgrading-tooa-new-version-on-a-cluster-that-is-set-toomanual-mode-via-a-resource-manager-template"></a>升級 tooa 設定資源管理員範本透過 tooManual 模式在叢集上的新版本。
Hello 叢集處於手動模式中，tooupgrade tooa 新版本時變更 hello"clusterCodeVersion"tooa 支援的版本，並將其部署。 hello hello 範本部署的 hello Fabric 升級已盡力而為取得開始自動。 hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。

如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 更多有關此文件 tooread 捲動 tooset 這些自訂的健全狀況原則。 

一旦您修正導致 hello 復原 hello 問題，您需要 tooinitiate hello 升級同樣地，由下列 hello 與之前相同的步驟。

### <a name="get-list-of-all-available-version-for-all-environments-for-a-given-subscription"></a>針對給定的訂用帳戶取得所有環境的所有可用版本清單
執行 hello 下列命令，以及您應該取得輸出類似 toothis。

“supportExpiryUtc” 會告訴您給定的版本即將到期或已過期。 hello 最新版本沒有有效的日期-它的值為"9999-12-31T23:59:59.9999999"，這就表示未尚未設定 hello 到期日。

```REST
GET https://<endpoint>/subscriptions/{{subscriptionId}}/providers/Microsoft.ServiceFabric/locations/{{location}}/clusterVersions?api-version=2016-09-01

Example: https://management.azure.com/subscriptions/1857f442-3bce-4b96-ad95-627f76437a67/providers/Microsoft.ServiceFabric/locations/eastus/clusterVersions?api-version=2016-09-01

Output:
{
                  "value": [
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/5.0.1427.9490",
                      "name": "5.0.1427.9490",
                      "type": "Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.0.1427.9490",
                        "supportExpiryUtc": "2016-11-26T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.0.1427.9490",
                      "name": "5.1.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "5.1.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Windows"
                      }
                    },
                    {
                      "id": "subscriptions/35349203-a0b3-405e-8a23-9f1450984307/providers/Microsoft.ServiceFabric/environments/Windows/clusterVersions/4.4.1427.9490",
                      "name": "4.4.1427.9490",
                      "type": " Microsoft.ServiceFabric/environments/clusterVersions",
                      "properties": {
                        "codeVersion": "4.4.1427.9490",
                        "supportExpiryUtc": "9999-12-31T23:59:59.9999999",
                        "environment": "Linux"
                      }
                    }
                  ]
                }


```

## <a name="fabric-upgrade-behavior-when-hello-cluster-upgrade-mode-is-automatic"></a>為 [自動] 時 hello 叢集升級模式的 fabric 升級行為
Microsoft 維護 hello 網狀架構程式碼和執行於 Azure 的叢集中的組態。 我們對可視需要執行受監視的自動升級 toohello 軟體。 升級的項目可能是程式碼、組態或兩者。 toomake 確定您的應用程式有任何影響或因為 toothese 升級的影響降到最低，我們會執行 hello 升級在 hello 下列階段：

### <a name="phase-1-an-upgrade-is-performed-by-using-all-cluster-health-policies"></a>階段 1：使用所有叢集健康狀態原則執行升級
在此階段，hello 升級繼續執行一個升級網域一次，並執行 hello 叢集中的 hello 應用程式繼續 toorun 完全不需要停機。 hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 必須遵守 tooduring hello 升級。

如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 然後以電子郵件傳送 toohello hello 訂用帳戶擁有者。 hello 電子郵件會包含下列資訊的 hello:

* 我們必須 tooroll 回叢集升級的通知。
* 建議的修復動作 (如果有的話)。
* hello 天數 (n) 我們執行階段 2 之前。

我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。 Hello 之後已傳送 hello 日期 hello 電子郵件中的 n 天，我們繼續 tooPhase 2。

如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。 在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。 執行成功不會有任何電子郵件確認。 這是傳送您太多的電子郵件-收到電子郵件應該視為例外狀況 toonormal tooavoid。 我們預期大部分的 hello 叢集升級 toosucceed 而不會影響您應用程式的可用性。

### <a name="phase-2-an-upgrade-is-performed-by-using-default-health-policies-only"></a>階段 2：僅使用預設健康狀態原則執行升級
在這個階段中的 hello 健全狀況原則是設定的方式，已在 hello 開頭 hello 升級狀況良好的應用程式的 hello 數目會維持相同的 hello hello 升級程序的持續時間的 hello。 階段 1，如同 hello 階段 2 升級繼續執行一個升級網域一次，並執行 hello 叢集中的 hello 應用程式繼續 toorun 完全不需要停機。 hello 叢集健全狀況原則 （節點健全狀況和 hello 所有 hello hello 叢集中執行的應用程式的健全狀況的組合） 會遵守 toofor hello hello 升級期間。

如果 hello 叢集健全狀況原則實際上不符合，會回復 hello 升級。 然後以電子郵件傳送 toohello hello 訂用帳戶擁有者。 hello 電子郵件會包含下列資訊的 hello:

* 我們必須 tooroll 回叢集升級的通知。
* 建議的修復動作 (如果有的話)。
* hello 天數直到我們執行階段 3 (n)。

我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。 在 n 天到達的前幾天會傳送提醒電子郵件。 Hello 之後已傳送 hello 日期 hello 電子郵件中的 n 天，我們繼續 tooPhase 3。 我們傳送給您在階段 2 中的 hello 電子郵件必須謹慎地加以，必須採取修復動作。

如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。 在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。 執行成功不會有任何電子郵件確認。

### <a name="phase-3-an-upgrade-is-performed-by-using-aggressive-health-policies"></a>階段 3：使用積極的叢集健康狀態原則執行升級
在這個階段中的這些健全狀況原則會導向到 hello 升級完成，而不是 hello hello 應用程式的健全狀況。 很少叢集升級會最後會變成這個階段。 如果您的叢集取得 toothis 階段，會有很好的機會，您的應用程式會變為狀況不良 （或） 失去可用性。

類似 toohello 其他兩個階段階段 3 升級一次前進一個升級網域。

如果不符合 hello 叢集健全狀況原則，會回復 hello 升級。 我們嘗試 tooexecute hello 相同升級幾次，以防任何升級的基礎結構原因而失敗。 在這之後，已釘選 hello 叢集，使它不會再接收支援和 （或） 升級。

這項資訊的電子郵件會傳送 toohello 訂用帳戶擁有者，以及 hello 修復動作。 我們不會任何叢集 tooget 進入階段 3 已失敗時的狀態。

如果符合 hello 叢集健全狀況原則，hello 升級會被視為成功，並標示為完成。 在這個階段中，這可能會在 hello 初始升級或任何 hello 升級重播。 執行成功不會有任何電子郵件確認。

## <a name="cluster-configurations-that-you-control"></a>您控制的叢集組態
此外 toohello 能力 tooset hello 叢集升級模式，以下是您可以變更即時叢集的 hello 組態。

### <a name="certificates"></a>憑證
您可以加入新檔案或輕鬆地刪除 hello 叢集和用戶端透過 hello 入口網站的憑證。 請參閱太[如需詳細指示這份文件](service-fabric-cluster-security-update-certs-azure.md)

![如果螢幕擷取畫面顯示 hello Azure 入口網站中的憑證指紋。][CertificateUpgrade]

### <a name="application-ports"></a>應用程式連接埠
您可以藉由變更 hello 與 hello 節點類型相關聯的負載平衡器資源屬性來變更應用程式連接埠。 您可以使用 hello 入口網站，或您可以直接使用資源管理員 PowerShell。

tooopen 新的連接埠節點型別中所有 Vm 上 hello 遵循：

1. 加入新的探查 toohello 適當負載平衡器。
   
    如果您使用 hello 入口網站部署您的叢集，hello 負載平衡器名為"LB-name 的 hello 資源群組 NodeTypename"，其中每個節點類型。 因為 hello 負載平衡器名稱是唯一的只有在資源群組內，最好是如果您的特定資源群組下搜尋它們。
   
    ![螢幕擷取畫面顯示新增探查 tooa 的負載平衡器 hello 入口網站中。][AddingProbes]
2. 加入新的規則 toohello 負載平衡器。
   
    加入新的規則 toohello 相同負載平衡器使用您建立 hello 上一個步驟中的 hello 探查。
   
    ![Hello 入口網站中加入新的規則 tooa 負載平衡器。][AddingLBRules]

### <a name="placement-properties"></a>放置屬性
針對每個 hello 節點型別，您可以新增您想 toouse 要在應用程式中的自訂放置屬性。 NodeType 是您可使用而不需明確新增的預設屬性。

> [!NOTE]
> 如需 hello 使用位置條件約束，節點屬性的詳細資訊和如何 toodefine 它們，請參閱 toohello > 一節 「 放置條件約束和節點屬性 」，在 hello Service Fabric 叢集資源管理員文件中的有關[描述您的叢集](service-fabric-cluster-resource-manager-cluster-description.md).
> 
> 

### <a name="capacity-metrics"></a>容量度量
針對每個 hello 節點型別，您可以加入您在應用程式 tooreport 負載想 toouse 自訂容量計量。 Hello 使用容量度量 tooreport 負載的詳細資訊，請參閱有關 toohello Service Fabric 叢集資源管理員的文件[描述叢集](service-fabric-cluster-resource-manager-cluster-description.md)和[度量和負載](service-fabric-cluster-resource-manager-metrics.md)。

### <a name="fabric-upgrade-settings---health-polices"></a>Fabric 升級設 - 健全狀況原則
您可以為網狀架構升級指定自訂的健全狀況原則。 如果您已經設定叢集 tooAutomatic fabric 升級，這些原則會取得套用的 toohello 階段 1 的 hello 網狀架構自動升級。
如果您已將您手動網狀架構的叢集升級，則這些原則會套用每次您選取觸發 hello 系統 tookick 關閉 hello fabric 升級在叢集中的新版本。 如果您不會覆寫 hello 原則，則會使用 hello 預設值。

您可以指定 hello 自訂健全狀況原則，或選取進階升級設定 hello 檢閱 hello hello 「 網狀架構升級 」 刀鋒視窗中，在目前的設定。 檢閱 hello 如何下列圖片。 

![管理自訂的健康狀態原則][HealthPolices]

### <a name="customize-fabric-settings-for-your-cluster"></a>自訂叢集的 Fabric 設定
請參閱太[服務網狀架構叢集網狀架構設定](service-fabric-cluster-fabric-settings.md)功能以及自訂它們。

### <a name="os-patches-on-hello-vms-that-make-up-hello-cluster"></a>Hello hello 叢集所組成的 Vm 上的 OS 修補程式
參照太[修補程式的協調流程的應用程式](service-fabric-patch-orchestration-application.md)的可部署於您叢集 tooinstall 修補程式，從 Windows Update 以協調的方式，保留 hello world hello 服務可用。 

### <a name="os-upgrades-on-hello-vms-that-make-up-hello-cluster"></a>在 hello hello 叢集所組成的 Vm 上的作業系統升級
如果您必須升級 hello hello 的 hello 叢集的虛擬機器上的作業系統映像，您必須進行一個 VM 一次。 您要負責這項升級，因為目前沒有將這項升級自動化。

## <a name="next-steps"></a>後續步驟
* 深入了解如何 toocustomize 某些 hello[服務網狀架構叢集網狀架構設定](service-fabric-cluster-fabric-settings.md)
* 了解如何太[叢集及相應放大](service-fabric-cluster-scale-up-down.md)
* 了解 [應用程式升級](service-fabric-application-upgrade.md)

<!--Image references-->
[CertificateUpgrade]: ./media/service-fabric-cluster-upgrade/CertificateUpgrade2.png
[AddingProbes]: ./media/service-fabric-cluster-upgrade/addingProbes2.PNG
[AddingLBRules]: ./media/service-fabric-cluster-upgrade/addingLBRules.png
[HealthPolices]: ./media/service-fabric-cluster-upgrade/Manage_AutomodeWadvSettings.PNG
[ARMUpgradeMode]: ./media/service-fabric-cluster-upgrade/ARMUpgradeMode.PNG
[Create_Manualmode]: ./media/service-fabric-cluster-upgrade/Create_Manualmode.PNG
[Manage_Automaticmode]: ./media/service-fabric-cluster-upgrade/Manage_Automaticmode.PNG
