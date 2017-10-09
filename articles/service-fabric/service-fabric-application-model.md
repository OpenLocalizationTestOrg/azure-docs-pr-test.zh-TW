---
title: "aaaAzure Service Fabric 應用程式模型 |Microsoft 文件"
description: "如何 toomodel 並描述應用程式和服務網狀架構中的服務。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>在 Service Fabric 中模型化應用程式
本文章提供 hello Azure Service Fabric 應用程式模型，以及如何 toodefine 應用程式和服務透過資訊清單檔案的總覽。

## <a name="understand-hello-application-model"></a>了解 hello 應用程式模型
應用程式是組成服務的集合，這些服務會執行特定函數。 服務會執行完整且獨立的函式，並且可獨立於其他服務啟動和執行。  服務是由程式碼、組態和資料所組成。 每一個服務程式碼 hello 可執行檔的二進位檔、 組態所組成，可在執行階段載入的服務設定和組成資料包含任意的靜態資料 toobe hello 服務所使用。 此階層應用程式模型中的每個元件都可以獨立建立版本和升級。

![hello Service Fabric 應用程式模型][appmodel-diagram]

應用程式類型是應用程式的分類，由服務類型的組合所組成。 服務類型是一項服務分類。 hello 分類可以有不同的設定與組態，但 hello 核心功能仍維持 hello 相同。 hello 服務執行個體是 hello 不同服務組態變化的 hello 相同服務類型。  

應用程式和服務的類別 (或「類型」) 是透過 XML 檔案 (應用程式資訊清單和服務資訊清單) 來說明。  hello 資訊清單是針對應用程式可以具現化 hello 叢集映像存放區中的 hello 範本。 hello hello ServiceManifest.xml 和 ApplicationManifest.xml 檔案的結構描述定義會隨 hello Service Fabric SDK 和工具太*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

hello 不同的應用程式執行個體的程式碼執行不同的處理序所裝載時，即使 hello 相同的 Service Fabric 節點。 此外，可以 hello 的每個應用程式執行個體的生命週期管理 （例如升級） 獨立。 hello 下列圖表顯示應用程式類型的服務型別，則會包含程式碼、 組態和資料封裝的組成方式。 toosimplify hello 圖表中，只有 hello 程式碼/config/資料封裝的`ServiceType4`都會顯示，但每個服務類型會包含部分或所有項目套件類型。

![Service Fabric 應用程式類型和服務類型][cluster-imagestore-apptypes]

兩個不同的資訊清單檔案是使用的 toodescribe 應用程式和服務： hello 服務資訊清單和應用程式資訊清單。 資訊清單會在 hello 下列各節中詳細說明。

可以有一或多個執行個體服務型別的 hello 叢集中使用中。 比方說，可設定狀態的服務執行個體或複本，獲得高可靠性位於 hello 叢集中不同節點上的複本之間複寫狀態。 複寫實質上提供 hello 服務 toobe 可用的複本，即使在叢集中的一個節點失敗。 A[分割服務](service-fabric-concepts-partitioning.md)進一步除以 hello 叢集的節點中其狀態 （和存取模式 toothat 狀態）。

hello 下列圖表顯示 hello 應用程式和服務執行個體、 資料分割和複本之間的關聯性。

![服務內的分割和複本][cluster-application-instances]

> [!TIP]
> 您可以檢視 hello 版面配置的應用程式中使用 http:// 在 hello Service Fabric 總管工具可用的叢集&lt;yourclusteraddress&gt;: 19080/總管。 如需詳細資訊，請參閱[使用 Service Fabric Explorer 視覺化叢集](service-fabric-visualizing-your-cluster.md)。
> 
> 

## <a name="describe-a-service"></a>描述服務
hello 服務資訊清單以宣告方式定義 hello 服務類型和版本。 它會指定如服務類型的服務中繼資料、健康狀態屬性、負載平衡度量、服務二進位檔和組態檔。  將另一種方式，描述構成服務封裝 toosupport hello 程式碼、 組態和資料封裝一或多個服務類型。 以下是簡單的範例服務資訊清單：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**版本**屬性為非結構化的字串，且無法剖析 hello 系統。 版本屬性是使用的 tooversion 升級每個元件。

**ServiceTypes** 會宣告此資訊清單中 **CodePackages** 支援哪些服務類型。 當針對其中一種服務類型來具現化服務時，會藉由執行其進入點來啟動此資訊清單中宣告的所有程式碼封裝。 hello 產生處理序在執行階段有預期的 tooregister hello 支援服務型別。 服務類型會宣告 hello 資訊清單的層級和非 hello 程式碼封裝層級。 因此當有多個程式碼封裝，其所有啟動的每當 hello 系統會尋找任何一種 hello 宣告的服務型別。

**SetupEntryPoint**是以 hello 相同認證為 Service Fabric 執行特殊權限的進入點 (通常 hello *LocalSystem*帳戶) 之前的任何其他的進入點。 hello 可執行檔所指定**EntryPoint**通常是 hello 長時間執行的服務主機。 hello 存在的個別安裝進入點可避免使用較高權限 toorun hello 服務主機很長的時間。 hello 可執行檔所指定**EntryPoint**執行**SetupEntryPoint**成功結束。 如果曾 hello 程序會結束，或當機，監視及重新啟動 hello 產生處理序 (開頭為再次**SetupEntryPoint**)。  

使用的典型案例**SetupEntryPoint**是當您執行可執行檔 hello 服務啟動前或執行的作業，以提高權限。 例如：

* 設定及初始化 hello 服務可執行檔需要的環境變數。 這不是透過 hello Service Fabric 程式設計模型撰寫有限的 tooonly 可執行檔。 例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。
* 透過安裝安全性憑證設定存取控制。

如需有關如何 tooconfigure hello **SetupEntryPoint**看到[設定服務安裝程式的進入點的 hello 原則](service-fabric-application-runas-security.md)

**EnvironmentVariables** 提供針對此程式碼封裝設定的環境變數清單。 Environmentment 變數會覆寫在 hello `ApplicationManifest.xml` tooprovide 不同服務執行個體的值不同。 

**DataPackage**宣告資料夾，名為 hello**名稱**屬性包含任意的靜態資料 toobe hello 程序所耗用在執行階段。

**Settings.xml**宣告資料夾，名為 hello**名稱**屬性包含*Settings.xml*檔案。 hello 設定檔包含 hello 處理序讀取回執行階段的使用者定義的索引鍵-值組設定的區段。 在升級期間，如果僅 hello **Settings.xml** **版本**已變更，則不會重新啟動 hello 執行程序。 相反地，回呼會通知組態設定已變更，因此它們可以重新載入以動態方式的 hello 程序。 以下是 *Settings.xml* 檔案的範例：

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> 服務資訊清單可以包含多個程式碼、組態和資料封裝。 每個皆可獨立建立版本。
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>描述應用程式
hello 應用程式資訊清單以宣告方式描述 hello 應用程式類型和版本。 它指定服務組成中繼資料，例如穩定的名稱、分割配置、執行個體計數/複寫因數、安全性/隔離原則、安置限制、組態覆寫和組成服務類型。 hello 應用程式所放置的 hello 負載平衡的網域也將描述。

因此，應用程式資訊清單描述 hello 應用程式層級的項目，並參照一個或多個服務資訊清單 toocompose 應用程式類型。 以下是簡單的範例應用程式資訊清單：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

喜歡服務資訊清單、**版本**屬性為非結構化的字串，且不會剖析 hello 系統。 版本屬性也會使用的 tooversion 升級每個元件。

**ServiceManifestImport**包含參考 tooservice 資訊清單構成此應用程式類型。 匯入的服務資訊清單會決定此應用程式類型中哪些服務類型有效。 Hello ServiceManifestImport，在您覆寫 ServiceManifest.xml 檔案中的 Settings.xml 和環境變數中的組態值。 


**DefaultServices** 宣告服務執行個體，該執行個體會在每次應用程式針對此應用程式類型具現化時建立。 預設服務只是為了方便起見，在建立之後，其行為在每個方面就像正常的服務。 它們會連同任何其他服務升級 hello 應用程式執行個體中，會一併移除。

> [!NOTE]
> 應用程式資訊清單可以包含多個服務資訊清單匯入和預設服務。 每個服務資訊清單匯入都可以獨立建立版本。
> 
> 

如何 toomaintain 不同的應用程式和服務參數，針對個別的環境，請參閱的 toolearn[管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)。

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>後續步驟
[封裝應用程式](service-fabric-package-apps.md)並使其準備 toodeploy。

[部署和移除應用程式][ 10]描述如何 toouse PowerShell toomanage 應用程式執行個體。

[管理應用程式參數的多個環境][ 11]描述如何 tooconfigure 參數和環境變數不同的應用程式執行個體。

[設定您的應用程式的安全性原則][ 12]描述 toorun 下安全性原則 toorestrict 存取服務的方式。

[應用程式主控模型][13]說明已部署之服務的複本 (或執行個體) 與服務主機處理序之間的關聯性。

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
