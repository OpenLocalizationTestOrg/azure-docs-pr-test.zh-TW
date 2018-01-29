---
title: "Azure Service Fabric 應用程式和服務描述 |Microsoft 文件"
description: "描述如何使用資訊清單來描述 Service Fabric 應用程式和服務。"
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
ms.date: 12/07/2017
ms.author: ryanwi
ms.openlocfilehash: 8e0cf78aef7e973188ce9581ec94f012f6ecde90
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="service-fabric-application-and-service-manifests"></a>Service Fabric 應用程式和服務資訊清單
本文說明 Service Fabric 應用程式和服務的方式定義和建立使用 ApplicationManifest.xml 和 ServiceManifest.xml 檔案版本。  這些資訊清單檔案的 XML 結構描述會記載在[ServiceFabricServiceModel.xsd 結構描述文件](service-fabric-service-model-schema.md)。

## <a name="describe-a-service-in-servicemanifestxml"></a>描述在 ServiceManifest.xml 的服務
服務資訊清單以宣告方式定義服務類型和版本。 它會指定如服務類型的服務中繼資料、健康狀態屬性、負載平衡度量、服務二進位檔和組態檔。  換句話說，它會描述組成服務封裝的程式碼、組態和資料封裝，以支援一或多個服務類型。 服務資訊清單可以包含多個程式碼、 組態和資料封裝，可獨立版本設定。 以下是 ASP.NET Core web 前端服務的服務資訊清單[投票範例應用程式](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="VotingWebPkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType. 
         This name must match the string used in RegisterServiceType call in Program.cs. -->
    <StatelessServiceType ServiceTypeName="VotingWebType" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>VotingWeb.exe</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an 
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="8080" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

**版本** 屬性為非結構化字串，不是由系統剖析。 版本屬性用於設定每個元件的版本以進行升級。

**ServiceTypes** 會宣告此資訊清單中 **CodePackages** 支援哪些服務類型。 當針對其中一種服務類型來具現化服務時，會藉由執行其進入點來啟動此資訊清單中宣告的所有程式碼封裝。 產生的處理程序預期在執行階段註冊支援的服務類型。 服務類型是在資訊清單層級而非程式碼套件層級宣告。 因此如果有多個程式碼封裝，每當系統尋找任何一個宣告的服務類型時，它們都會啟動。

**EntryPoint** 指定的可執行檔通常是長時間執行的服務主機。 **SetupEntryPoint** 是以與 Service Fabric 相同的認證執行的特殊權限進入點 (通常 *LocalSystem* 帳戶)，優先於任何其他進入點。  有個別設定的進入點，就不需要使用較高權限來長時間執行服務主機。 **EntryPoint** 指定的可執行檔是在 **SetupEntryPoint** 成功結束之後執行。 如果程序曾經終止或當機，則產生的程序會受到監視並重新啟動 (以 **SetupEntryPoint**再次開始)。  

使用 **SetupEntryPoint** 的一般案例，是當您在服務啟動之前執行可執行檔，或使用提高的權限來執行作業時。 例如︰

* 設定及初始化服務可執行檔需要的環境變數。 這不限於透過 Service Fabric 程式設計模型撰寫的執行檔。 例如，npm.exe 部署 node.js 應用程式，需要設定某些環境變數。
* 透過安裝安全性憑證設定存取控制。

如需有關如何設定 **SetupEntryPoint** 的詳細資訊，請參閱[設定服務安裝程式進入點的原則](service-fabric-application-runas-security.md)

**EnvironmentVariables** （不在上述範例中的設定） 提供設定此程式碼封裝的環境變數的清單。 環境變數會覆寫中`ApplicationManifest.xml`以不同的值提供不同服務執行個體。 

**DataPackage** （不在上述範例中的設定） 會宣告一個資料夾，名為**名稱**屬性包含任意的靜態資料，以供在執行階段程序。

**ConfigPackage** 宣告 **Name** 屬性所命名的資料夾，其中包含 *Settings.xml* 檔案。 設定檔案包含程序在執行階段讀回的使用者定義、成對的索引鍵/值設定等區段。 在升級期間，如果只有 **ConfigPackage** **版本**已變更，則不會重新啟動執行中程序。 相反地，回呼會通知程序組態設定已變更，因此它們可以動態方式重新載入。 以下是 *Settings.xml* 檔案的範例：

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

**資源**，例如端點使用的服務所要宣告/變更而不需要變更已編譯的程式碼。  服務資訊清單中指定的資源的存取權可以透過控制**SecurityGroup**應用程式資訊清單中。  當**端點**資源已定義服務資訊清單中，Service Fabric 會指派連接埠從保留的應用程式連接埠範圍時未明確指定連接埠。  深入了解[指定或覆寫 endpoint 資源](service-fabric-service-manifest-resources.md)。


<!--
For more information about other features supported by service manifests, refer to the following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application-in-applicationmanifestxml"></a>描述在 ApplicationManifest.xml 中的應用程式
應用程式資訊清單以宣告方式描述應用程式類型和版本。 它指定服務組成中繼資料，例如穩定的名稱、分割配置、執行個體計數/複寫因數、安全性/隔離原則、安置限制、組態覆寫和組成服務類型。 也說明要放置應用程式的負載平衡網域。

因此，應用程式資訊清單描述應用程式層級的元素，並參考用來組成應用程式類型的一個或多個服務資訊清單。 以下是應用程式資訊清單[投票範例應用程式](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart):

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VotingType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Parameters>
    <Parameter Name="VotingData_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingData_PartitionCount" DefaultValue="1" />
    <Parameter Name="VotingData_TargetReplicaSetSize" DefaultValue="3" />
    <Parameter Name="VotingWeb_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingDataPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="VotingWebPkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="VotingData">
      <StatefulService ServiceTypeName="VotingDataType" TargetReplicaSetSize="[VotingData_TargetReplicaSetSize]" MinReplicaSetSize="[VotingData_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[VotingData_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    <Service Name="VotingWeb" ServicePackageActivationMode="ExclusiveProcess">
      <StatelessService ServiceTypeName="VotingWebType" InstanceCount="[VotingWeb_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

如同服務資訊清單， **版本** 屬性為非結構化字串，不是由系統剖析。 版本屬性也用於設定每個元件的版本以進行升級。

**參數**定義整個應用程式資訊清單所使用的參數。 應用程式是 instatiated，和應用程式或服務組態設定可以覆寫時，就可以提供這些參數的值。  如果應用程式具現化期間將不會變更值，會使用預設參數值。 若要了解如何針對個別環境維護不同的應用程式和服務參數，請參閱 [管理多個環境的應用程式參數](service-fabric-manage-multiple-environment-app-configuration.md)

**ServiceManifestImport** 包含組成此應用程式類型之服務資訊清單的參考。 應用程式資訊清單可以包含多個服務資訊清單匯入、 每個獨立可以進行版本設定。 匯入的服務資訊清單會決定此應用程式類型中哪些服務類型有效。 在 ServiceManifestImport 內，您可覆寫 Settings.xml 中的組態值和 ServiceManifest.xml 檔案中的環境變數。 **原則**（在上述範例中未設定） 的端點繫結、 安全性和存取和封裝共用可以將已匯入的服務資訊清單上。  如需詳細資訊，請參閱[設定您的應用程式的安全性原則](service-fabric-application-runas-security.md)。

**DefaultServices** 宣告服務執行個體，該執行個體會在每次應用程式針對此應用程式類型具現化時建立。 預設服務只是為了方便起見，在建立之後，其行為在每個方面就像正常的服務。 它們會與應用程式執行個體中的其他任何服務一起升級，也可以一起移除。 應用程式資訊清單可以包含多個預設的服務。

**憑證**（不在上述範例中的設定） 會宣告用來的憑證[設定 HTTPS 端點](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service)或[加密應用程式資訊清單中的機密](service-fabric-application-secret-management.md)。

**原則**（不在上述範例中的設定） 描述記錄檔集合，[預設執行身分](service-fabric-application-runas-security.md)，[健全狀況](service-fabric-health-introduction.md#health-policies)，和[安全性存取](service-fabric-application-runas-security.md)在設定原則應用程式層級。

**主體**（在上述範例中未設定） 描述所需的安全性主體 （使用者或群組）[執行的服務和安全服務資源](service-fabric-application-runas-security.md)。  中所參考的主體**原則**區段。





<!--
For more information about other features supported by application manifests, refer to the following articles:

*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>後續步驟
- [封裝應用程式](service-fabric-package-apps.md)並讓它準備好進行部署。
- [部署和移除應用程式](service-fabric-deploy-remove-applications.md)。
- [設定參數和環境變數不同的應用程式執行個體](service-fabric-manage-multiple-environment-app-configuration.md)。
- [設定您的應用程式的安全性原則](service-fabric-application-runas-security.md)。
- [設定 HTTPS 端點](service-fabric-service-manifest-resources.md#example-specifying-an-https-endpoint-for-your-service)。
- [加密應用程式資訊清單中的機密](service-fabric-application-secret-management.md)

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png



