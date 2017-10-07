---
title: "aaaUsing Elasticsearch 做為 Service Fabric 應用程式追蹤存放區 |Microsoft 文件"
description: "說明 Service Fabric 應用程式可以如何使用 Elasticsearch 和 Kibana toostore、 索引和搜尋應用程式追蹤 （記錄檔）"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>把 Elasticsearch 當做 Service Fabric 應用程式追蹤存放區來使用
## <a name="introduction"></a>簡介
本文將說明 [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) 應用程式如何使用 **Elasticsearch** 和 **Kibana** 來儲存、檢索和搜尋應用程式追蹤。 [Elasticsarch](https://www.elastic.co/guide/index.html) 是開放原始碼、分散式和可調整的即時搜尋和分析引擎，很適合執行這項工作。 它可以安裝在 Microsoft Azure 中執行的 Windows 和 Linux 虛擬機器上。 Elasticsearch 可有效率地處理使用 **Windows 事件追蹤 (ETW)** 之類的技術所產生的「結構化」追蹤。

ETW 會使用 Service Fabric 執行階段 toosource 診斷資訊 （追蹤）。 它是 hello 建議 Service Fabric 應用程式 toosource 方法其診斷資訊，太。 使用相同的機制可讓執行階段提供，且應用程式所提供的追蹤和疑難排解更加容易讓之間的相互關聯的 hello。 在 Visual Studio 中的 Service Fabric 專案範本包含記錄的應用程式開發介面 (根據 hello.NET **EventSource**類別)，預設會發出 ETW 追蹤。 如需使用 ETW 的 Service Fabric 應用程式追蹤的一般概觀，請參閱 [監視和診斷本機開發設定中的服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)。

Hello 追蹤 tooshow 向上 Elasticsearch 中，它們需要 toobe 擷取的即時 hello Service Fabric 叢集節點 （在 hello 應用程式正在執行） 並傳送 tooan Elasticsearch 端點。 追蹤擷取有兩個主要選項：

* **同處理序追蹤擷取**  
  hello 應用程式或更精確地說，服務處理程序，負責傳送嗨診斷資料 toohello 追蹤存放區 (Elasticsearch)。
* **跨處理序追蹤擷取**  
  獨立的代理程式會擷取從 hello 服務處理程序或處理程序的追蹤，然後將它們傳送 toohello 追蹤存放區。

以下，我們將描述如何註冊在 Azure 上、 Elasticsearch tooset 討論 hello 專業人員和優缺點比較兩個擷取選項，並說明如何 tooconfigure Service Fabric 服務 toosend 資料 tooElasticsearch。

## <a name="set-up-elasticsearch-on-azure"></a>在 Azure 上設定 Elasticsearch
hello hello Elasticsearch 服務在 Azure 上的最直接的方式 tooset 是透過[ **Azure 資源管理員範本**](../azure-resource-manager/resource-group-overview.md)。 Azure 快速入門範本儲存機制提供完整的 [Elasticsearch 快速入門 Azure 資源管理員範本](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) 。 這個範本會針對縮放單位使用不同的儲存體帳戶 (節點群組)。 它也可以佈建具有不同組態和連接各種數量的資料磁碟的個別用戶端與伺服器節點。

在此，我們使用另一個範本，呼叫**ES MultiNode**從 hello [Azure 診斷工具儲存機制](https://github.com/Azure/azure-diagnostics-tools)。 此範本是更容易 toouse，而且它會建立 HTTP 基本驗證所保護的 Elasticsearch 叢集。 在繼續之前，請從 GitHub tooyour 電腦下載 hello 儲存機制 （由複製 hello 儲存機制或下載 zip 檔案）。 hello ES MultiNode 範本位於 hello 與 hello 資料夾中相同的名稱。

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>準備電腦 toorun Elasticsearch 安裝指令碼
hello 最簡單的方式 toouse hello ES MultiNode 範本都是透過提供的 Azure PowerShell 指令碼，呼叫`CreateElasticSearchCluster`。 toouse 此指令碼，您需要 tooinstall PowerShell 模組和一個工具，稱為**openssl**。 hello 後者是從遠端建立 SSH 金鑰，它可以是使用的 tooadminister Elasticsearch 叢集所需。

`CreateElasticSearchCluster`指令碼被設計的易用性 hello ES MultiNode 範本，從 Windows 電腦。 它是在非 Windows 的電腦，可能 toouse hello 範本，但這種情況下已超出本文 hello 範圍。

1. 如果您尚未安裝它們，請安裝 [**Azure PowerShell 模組**](http://aka.ms/webpi-azps)。 出現提示時，請按一下 [執行]，然後按一下 [安裝]。 需要 Azure PowerShell 1.3 或更新版本。
2. hello **openssl**工具隨附於的 hello 分佈[ **Git for Windows**](http://www.git-scm.com/downloads)。 如果您尚未安裝，請立即安裝 [Git for Windows](http://www.git-scm.com/downloads) 。 （hello 預設安裝選項是 [確定]）。
3. 假設 Git 已安裝但不是包含在 hello 系統路徑中，開啟 Microsoft Azure PowerShell 視窗，然後執行下列命令的 hello:
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    取代 hello `<Git installation folder>` hello Git 位置，在您的電腦; 上 hello 預設值是**"C:\Program Files\Git"**。 請注意在 hello 開頭 hello 第一個路徑的 hello 分號字元。
4. 確認您已登入 tooAzure (透過[ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet)，您已選取 hello 訂用帳戶，應該使用 toocreate 彈性的搜尋叢集。 您可以使用 `Get-AzureRmContext` 和 `Get-AzureRmSubscription` Cmdlet，確認選取的是正確的訂用帳戶。
5. 如果您尚未這樣做，請變更 hello 目前目錄 toohello ES MultiNode 資料夾。

### <a name="run-hello-createelasticsearchcluster-script"></a>執行 hello CreateElasticSearchCluster 指令碼
執行 hello 指令碼之前，請開啟 hello`azuredeploy-parameters.json`檔案，並確認或提供 hello 指令碼參數的值。 提供下列參數的 hello:

| 參數名稱 | 說明 |
| --- | --- |
| dnsNameForLoadBalancerIP |hello 是使用的 toocreate hello 公開可見的 DNS 名稱 hello 彈性的搜尋叢集 （藉由附加 hello Azure 地區網域 toohello 提供名稱） 的名稱。 例如，如果此參數值是"myBigCluster"hello 選擇 Azure 地區為美國西部，hello 叢集 hello 產生 DNS 名稱會是 myBigCluster.westus.cloudapp.azure.com。 <br /><br />此名稱也可做為許多成品 hello 彈性的搜尋叢集中，例如資料節點名稱與相關聯的根名稱。 |
| adminUsername |hello hello 系統管理員帳戶名稱管理 hello 彈性的搜尋叢集 （自動產生對應的 SSH 金鑰）。 |
| dataNodeCount |hello hello 彈性的搜尋叢集中的節點數目。 hello hello 指令碼的目前版本不會區分資料與查詢節點。所有的節點會播放這兩個角色。 預設值 too3 節點。 |
| dataDiskSize |hello 的大小 （以 gb 為單位） 的資料磁碟配置的每個資料節點。 每個節點會接收 4 個資料磁碟，以獨佔方式專用 tooElastic 搜尋服務。 |
| region |hello 應該位於 hello 彈性的搜尋叢集的 Azure 區域名稱。 |
| esUserName |hello hello 為使用者的使用者名稱設定 toohave 存取 tooES 叢集 （主旨 tooHTTP 基本驗證）。 hello 密碼不是參數檔案的一部分，必須提供何時`CreateElasticSearchCluster`指令碼會叫用。 |
| vmSizeDataNodes |hello 彈性的搜尋叢集節點的 Azure 虛擬機器大小。 預設值 tooStandard_D2。 |

現在您已準備好 toorun hello 指令碼。 發出下列命令的 hello:

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

其中 

| 指令碼參數名稱 | 說明 |
| --- | --- |
| `<es-group-name>` |hello hello Azure 資源群組的名稱將會包含所有的彈性的搜尋叢集資源。 |
| `<azure-region>` |hello hello Azure hello 彈性的搜尋叢集建立所在的區域名稱。 |
| `<es-password>` |hello hello 彈性的搜尋使用者密碼。 |

> [!NOTE]
> 如果您從 hello 測試 AzureResourceGroup cmdlet 取得 NullReferenceException，忘記 toolog tooAzure 上的 (`Add-AzureRmAccount`)。
> 
> 

如果您收到執行 hello 指令碼錯誤，且您判斷 hello 錯誤因錯誤的範本參數值，請更正 hello 參數檔案，然後再次執行 hello 指令碼，以不同的資源群組名稱。 您也可以重複使用 hello 相同資源群組名稱，而且有 hello 清除 hello 舊的指令碼，藉由新增 hello`-RemoveExistingResourceGroup`參數 toohello 指令碼引動過程。

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>執行 hello CreateElasticSearchCluster 指令碼的結果
執行 hello 之後`CreateElasticSearchCluster`指令碼，將建立下列主要成品的 hello。 此範例中，我們假設您使用的是 「 myBigCluster"做為 hello hello 值`dnsNameForLoadBalancerIP`參數與您用來建立 hello 叢集該 hello 地區為美國西部。

| 構件 | 名稱、位置及備註 |
| --- | --- |
| 用於遠端系統管理的 SSH 金鑰 |myBigCluster.key 檔 （在已執行哪些 hello CreateElasticSearchCluster 的 hello 目錄）。 <br /><br />此金鑰檔，可以是使用的 tooconnect toohello 管理節點及 （透過 hello 管理節點） toodata hello 叢集中的節點。 |
| 管理節點 |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />專用的 VM 的遠端 Elasticsearch 叢集系統管理-hello 只有一個，可讓外部 SSH 連線。 在 hello 相同的虛擬網路，為所有的 hello Elasticsearch 叢集節點，但未執行任何 Elasticsearch 服務上執行。 |
| 資料節點 |myBigCluster1 … myBigCluster*N* <br /><br />執行 Elasticsearch 和 Kibana 服務的資料節點。 您可以連接透過 SSH tooeach 節點，但只能透過 hello 管理節點。 |
| Elasticsearch 叢集 |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />hello hello Elasticsearch 叢集 （請注意 hello /es 尾碼） 的主要端點。 受到基本 HTTP 驗證 （hello 認證 hello 指定 esUserName/esPassword hello ES MultiNode 範本參數）。 hello 叢集也有基本的叢集管理 hello head 外掛程式安裝 (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head)。 |
| Kibana 服務 |http://myBigCluster.westus.cloudapp.azure.com <br /><br />hello Kibana 服務設定 tooshow 資料中，從建立 Elasticsearch 叢集 hello。 受到 hello hello 與相同的驗證認證叢集本身。 |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>同處理序與跨處理序追蹤擷取
在 hello 的簡介，我們曾提及收集診斷資料的兩個基本的方式： 同處理序和跨處理序。 各有優缺點。

Hello 的優點**同處理序追蹤擷取**包括：

1. *輕鬆設定及部署*
   
   * 診斷資料收集的 hello 組態只是 hello 應用程式組態的一部分。 它是簡單 tooalways 保持其 「 同步 」 以 hello 其餘部分的 hello 應用程式。
   * 輕鬆就可達成個別應用程式或個別服務的組態。
   * 跨處理序追蹤擷取通常需要不同的部署和 hello 診斷代理程式的設定，這是額外的管理工作和錯誤的潛在來源。 hello 特定代理程式的技術通常可讓每個虛擬機器 （節點） 的 hello 代理程式只有一個執行個體。 這表示該組態的所有應用程式之間共用的 hello 診斷組態的 hello 集合，該節點上執行的服務。
2. *彈性*
   
   * hello 應用程式可以傳送 hello 資料每當需要 toogo，只要用戶端程式庫支援 hello 目標資料儲存系統。 可以依需要加入新的來源。
   * 可以實作複雜的擷取、篩選和資料彙總規則。
   * 跨處理序追蹤擷取通常受限於 hello 代理程式支援的 hello 資料接收器。 有些代理程式是可擴充的。
3. *存取 toointernal 應用程式資料和內容*
   
   * hello hello 應用程式/服務處理序內執行的診斷子系統可以輕鬆地擴大 hello 與內容資訊的追蹤。
   * 在 hello 跨處理序的方法，hello 資料必須傳送 tooan 代理程式，透過某種處理序間通訊機制，例如 Windows 事件追蹤。 此機制可能會造成額外的限制。

Hello 的優點**跨處理序追蹤擷取**包括：

1. *hello 能力 toomonitor hello 應用程式並收集損毀傾印*
   
   * 同處理序追蹤擷取可能會失敗，如果失敗 toostart hello 應用程式，或當機。 獨立代理程式有更好的機會可擷取重要的疑難排解資訊。<br /><br />
2. *成熟度、穩健性和已證實的效能*
   
   * 平台供應商 （例如 Microsoft Azure 診斷代理程式） 所開發的代理程式已主旨 toorigorous 測試和戰鬥強化。
   * 使用同處理序擷取的追蹤，必須小心 tooensure hello 活動的應用程式處理序從傳送診斷資料不會不干擾 hello 應用程式的主要工作或引入計時或效能問題。 獨立執行的代理程式是較不容易出錯的 toothese 問題，特別設計的 toolimit 它 hello 系統上的影響。

它也可能 toocombine 這兩種方法而獲益。 事實上，它可能 hello 對於許多應用程式的最佳解決方案。

在此，我們使用 hello **Microsoft.Diagnostic.Listeners 文件庫**和 hello 同處理序追蹤擷取 toosend 從 Service Fabric 應用程式 tooan Elasticsearch 叢集中的資料。

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>使用 hello 接聽程式文件庫 toosend 診斷資料 tooElasticsearch
hello Microsoft.Diagnostic.Listeners 程式庫是 PartyCluster 範例 Service Fabric 應用程式的一部分。 toouse 它：

1. 下載[hello PartyCluster 範例](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster)從 GitHub。
2. Hello Microsoft.Diagnostics.Listeners 和 Microsoft.Diagnostics.Listeners.Fabric 專案 （整個資料夾） 從 hello PartyCluster 範例目錄 toohello 方案資料夾複製了應該 toosend hello 資料 tooElasticsearch hello 應用程式.
3. 開啟 hello 目標方案，以滑鼠右鍵按一下 hello 方案總管] 中的 hello 方案節點，然後選擇 [**加入現有專案**。 新增 hello Microsoft.Diagnostics.Listeners 專案 toohello 方案。 重複 hello 相同 hello Microsoft.Diagnostics.Listeners.Fabric 專案。
4. 將專案參考加入您的服務專案 toohello 兩個已加入專案。 （應該 toosend 資料 tooElasticsearch 每個服務應參考 Microsoft.Diagnostics.EventListeners 和 Microsoft.Diagnostics.EventListeners.Fabric。）
   
    ![專案參考 tooMicrosoft.Diagnostics.EventListeners 和 Microsoft.Diagnostics.EventListeners.Fabric 文件庫][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Service Fabric 公開上市版本和 Microsoft.Diagnostics.Tracing Nuget 封裝
以 Service Fabric 公開上市版本 (2.0.135，2016 年 3 月 31 日發行) 建置的應用程式會以 **.NET Framework 4.5.2**為目標。 這個版本是 hello hello Azure 支援在 hello 階段 hello GA 版本的.NET Framework 最高版本。 不幸的是，這個版本的 hello framework 缺少某些 EventListener Api 該 hello Microsoft.Diagnostics.Listeners 需要程式庫。 EventSource （form hello 基礎網狀架構應用程式中的記錄 Api hello 元件） 和 EventListener 會緊密結合的因為每個使用 hello Microsoft.Diagnostics.Listeners 程式庫的專案必須使用替代的實作EventSource。 這個實作由 hello **Microsoft.Diagnostics.Tracing Nuget 封裝**、 由 Microsoft 所撰寫。 hello 封裝是包含在 hello 架構，所以變更任何程式碼不不需要參考命名空間變更以外的 EventSource 完全與舊版相容。

toostart 使用 hello Microsoft.Diagnostics.Tracing 實作 hello EventSource 類別，請遵循下列步驟，針對每個需要 toosend 資料 tooElasticsearch 的服務專案：

1. Hello 服務專案上按一下滑鼠右鍵，然後選擇 **管理 Nuget 封裝**。
2. 切換 toohello nuget.org 封裝來源 （如果尚未選取），並搜尋"**Microsoft.Diagnostics.Tracing**"。
3. 安裝 hello`Microsoft.Diagnostics.Tracing.EventSource`封裝 （和其相依性）。
4. 開啟 hello **ServiceEventSource.cs**或**ActorEventSource.cs**服務專案中的檔案，並將 hello`using System.Diagnostics.Tracing`指示詞在 hello 與 hello 檔案頂端`using Microsoft.Diagnostics.Tracing`指示詞。

這些步驟不是必要的一次 hello **.NET Framework 4.6** Microsoft Azure 支援。

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Elasticsearch 接聽程式具現化和組態
hello 傳送診斷資料 tooElasticsearch 的最後一個步驟是 toocreate 的執行個體`ElasticSearchListener`並設定 Elasticsearch 連線資料。 hello 接聽程式會自動擷取所有透過 hello 服務專案中定義的 EventSource 類別所引發的事件。 它需要 toobe hello hello 服務存留期間保持運作以便 hello 最佳放置的 toocreate 處於 hello 服務初始化程式碼。 以下是無狀態服務的 hello 初始化程式碼無法樣子 hello 必要變更後 (新增項目開頭的註解中指出`****`):

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Elasticsearch 連線資料都應該放在不同的區段 hello 服務組態檔中 (**PackageRoot\Config\Settings.xml**)。 hello hello 區段名稱必須對應傳遞 toohello toohello 值`FabricConfigurationProvider`建構函式，例如：

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
hello 值`serviceUri`，`userName`和`password`參數 toohello Elasticsearch 叢集端點位址、 Elasticsearch 使用者名稱和密碼，分別對應。 `indexNamePrefix`是 hello Elasticsearch 索引; 前置詞hello Microsoft.Diagnostics.Listeners 程式庫會每天建立新的索引，其資料。

### <a name="verification"></a>驗證
就這麼簡單！ 現在，每次執行 hello 服務時，它會開始傳送嗨組態中指定的追蹤 toohello Elasticsearch 服務。 您可以驗證，請開啟 hello Kibana UI hello 目標 Elasticsearch 執行個體相關聯。 在本例中，hello 網址是 http://myBigCluster.westus.cloudapp.azure.com/。 選擇 hello 名稱前置詞索引的核取`ElasticSearchListener`確實已建立並填入資料執行個體。

![顯示 PartyCluster 應用程式事件的 Kibana][2]

## <a name="next-steps"></a>後續步驟
* [深入了解診斷和監視 Service Fabric 服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
