---
title: "aaaManage 服務網狀架構中的多個環境 |Microsoft 文件"
description: "Service Fabric 應用程式可以執行的叢集大小介於一個機器 toothousands 的機器。 在某些情況下，您會想 tooconfigure 以不同的方式為這些不同環境的應用程式。 本文件涵蓋如何 toodefine 不同的應用程式參數，每個環境。"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>管理多個環境的應用程式參數
您可以從一個 toomany 千分位機器的任何位置使用，以建立 Azure Service Fabric 叢集。 應用程式二進位檔可以透過此各式各樣的環境，必須修改才能執行，而您通常想 tooconfigure hello 應用程式不同，根據您要部署至電腦的 hello 數目而定。

簡單來說，請考慮無狀態服務的 `InstanceCount` 。 當您在 Azure 中執行應用程式時，您通常會想 tooset 此參數 toohello 特殊值為"-1"。 此組態可確保您的服務 hello 叢集 （或 hello 節點類型，如果您已設定放置條件約束中的每個節點） 中的每個節點上執行。 不過，此設定不是適用於單一電腦叢集因為您不能有多個相同接聽 hello 的處理序在單一機器上的端點。 相反地，您通常設定`InstanceCount`太"1 的"。

## <a name="specifying-environment-specific-parameters"></a>指定環境特有的參數
hello 方案 toothis 組態問題是一組參數的預設服務和應用程式參數檔案，以填入這些參數的值指定的環境。 預設的服務和應用程式參數設定於 hello 應用程式，但服務資訊清單。 hello hello ServiceManifest.xml 和 ApplicationManifest.xml 檔案的結構描述定義會隨 hello Service Fabric SDK 和工具太*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>預設服務
Service Fabric 應用程式是由服務執行個體集合所組成。 在正在 toocreate 空白的應用程式可能然後動態地建立所有服務執行個體，大部分的應用程式會有一組時，應該一律建立 hello 應用程式具現化的核心服務。 這些是參考的 tooas 「 預設服務 」。 指定在 hello 應用程式資訊清單，其中含有包含方括號中的每個環境設定的預留位置：

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

每個具名參數的 hello 必須定義在 hello hello 應用程式資訊清單參數項目：

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

hello DefaultValue 屬性指定 hello 值 toobe hello 缺乏更特定參數用於指定的環境。

> [!NOTE]
> 並非所有的服務執行個體參數都適用於每個環境組態。 在 hello 上述範例中，hello LowKey，HighKey hello 服務資料分割配置的值必須明確定義 hello 服務的所有執行個體因為 hello 資料分割範圍是 hello 資料定義域而言不 hello 環境的函式。
> 
> 

### <a name="per-environment-service-configuration-settings"></a>每個環境的服務組態設定
hello [Service Fabric 應用程式模型](service-fabric-application-model.md)啟用 services tooinclude 設定封裝包含在執行階段可讀取的自訂金鑰-值組。 這些設定的 hello 值可以也來區別環境藉由指定`ConfigOverride`hello 應用程式資訊清單中。

假設您有下列 hello 的 hello Config\Settings.xml 檔案中設定的 hello`Stateful1`服務：

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
toooverride 對特定的應用程式環境，這個值建立`ConfigOverride`當您匯入 hello hello 應用程式資訊清單中的服務資訊清單。

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
接著可如上所示，依照環境設定此參數。 您可以藉由宣告它 hello 參數 hello 應用程式資訊清單區段中和在 hello 應用程式參數檔案中指定環境特定值。

> [!NOTE]
> 在服務組態設定的 hello 情況下，有三個位置的索引鍵的 hello 值可以設定的位置： hello 服務組態的封裝、 hello 應用程式資訊清單和 hello 應用程式參數檔案。 Service Fabric 會一律選擇 hello 應用程式參數檔案從第一次 （如果有指定），然後 hello 應用程式資訊清單，並最後 hello 組態封裝。
> 
> 

### <a name="setting-and-using-environment-variables"></a>設定及使用環境變數 
您可以指定和 hello ServiceManifest.xml 檔案中設定環境變數，然後覆寫這些每個執行個體為基礎的 hello ApplicationManifest.xml 檔案中。
hello 下面範例是兩個環境變數，設定一個值，並會覆寫其他 hello。 您可以使用應用程式參數 tooset 環境變數中的值 hello 相同方式，這些已用來設定覆寫。

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
hello ApplicationManifest.xml 中，參考 hello 程式碼封裝在 hello 與 hello ServiceManifest 中的 toooverride hello 環境變數`EnvironmentOverrides`項目。

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 建立名為服務執行個體的 hello 之後您可以從程式碼存取 hello 環境變數。 例如在 C# 中，您可以設定下列 hello

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Service Fabric 環境變數
Service Fabric 具有已針對每個服務執行個體設定的內建環境變數。 hello 的環境變數的完整清單是下面其中 hello 粗體會於 hello 是您將使用您的服務，在 hello 其他正在 Service Fabric 執行階段使用。 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[YourServiceName]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

hello 程式碼 belows 示範如何 toolist hello Service Fabric 環境變數
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
hello 以下是範例呼叫的應用程式類型的環境變數`GuestExe.Application`與服務類型呼叫`FrontEndService`在本機開發電腦上執行時。

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>應用程式參數檔案
hello Service Fabric 應用程式專案可以包含一或多個應用程式參數檔案。 每個定義 hello 特定參數的值 hello hello 應用程式資訊清單中所定義：

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
根據預設，新的應用程式有三個應用程式參數檔案，名稱分別是 Local.1Node.xml、Local.5Node.xml、Cloud.xml：

![方案總管中的應用程式參數檔案][app-parameters-solution-explorer]

toocreate 參數檔案，只要複製和貼上現有並為它提供新名稱。

## <a name="identifying-environment-specific-parameters-during-deployment"></a>在部署期間識別環境特有的參數
在部署階段，您會需要 toochoose hello 適當的參數檔案 tooapply 與您的應用程式。 您可以透過 Visual Studio 中的 hello 發行對話方塊，或透過 PowerShell。

### <a name="deploy-from-visual-studio"></a>從 Visual Studio 部署
當您在 Visual Studio 發行您的應用程式時，您可以選擇從 hello 參數可用檔案清單。

![在 hello 發行對話方塊中選擇參數檔案][publishdialog]

### <a name="deploy-from-powershell"></a>從 PowerShell 部署
hello `Deploy-FabricApplication.ps1` hello 應用程式專案範本中所包含的 PowerShell 指令碼接受做為參數的發行設定檔和 hello PublishProfile 包含參考 toohello 應用程式參數檔案。

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解一些 hello 核心概念，本主題中所討論，請參閱 「 hello [Service Fabric 的技術概觀](service-fabric-technical-overview.md)。 如需 Visual Studio 中其他可用的應用程式管理功能的相關資訊，請參閱 [在 Visual Studio 中管理 Service Fabric 應用程式](service-fabric-manage-application-in-visual-studio.md)。

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
