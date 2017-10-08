---
title: "aaaCloud 服務角色組態 XPath 小祕技 |Microsoft 文件"
description: "hello 各種 XPath 設定，您可以使用在 hello 雲端服務角色組態 tooexpose 設定做為環境變數。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>利用 XPath 公開角色組態設定以做為環境變數
在 hello 雲端服務工作者或 web 角色服務定義檔中，您可以為環境變數來公開執行階段組態值。 支援下列 XPath 值 hello （其對應 tooAPI 值）。

下列 XPath 值也會提供透過 hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx)程式庫。 

## <a name="app-running-in-emulator"></a>在模擬器中執行的應用程式
指出 hello 模擬器中執行該 hello 應用程式。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| 代碼 |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>部署 ID
擷取 hello hello 執行個體的部署識別碼。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| 代碼 |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>角色 ID
擷取 hello 目前角色執行個體的識別碼 hello。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| 代碼 |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a>更新網站
擷取 hello hello 執行個體的更新網域。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| 代碼 |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>容錯網域
擷取 hello hello 執行個體的容錯網域。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| 代碼 |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>角色名稱
擷取 hello hello 執行個體的角色名稱。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| 代碼 |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>組態設定
Hello 擷取 hello 值會指定組態設定。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| 代碼 |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>本機儲存體路徑
擷取 hello hello 執行個體的本機儲存體路徑。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| 代碼 |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>本機儲存體大小
擷取 hello hello hello 執行個體的本機儲存體大小。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| 代碼 |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>端點通訊協定
擷取 hello hello 執行個體的端點通訊協定。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| 代碼 |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>端點 IP
取得 hello 指定端點的 IP 位址。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| 代碼 |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>端點連接埠
擷取 hello hello 執行個體的端點通訊埠。

| 類型 | 範例 |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| 代碼 |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>範例
以下是使用名為的環境變數建立啟動工作的背景工作角色的範例`TestIsEmulated`設定 toohello [ @emulated xpath 值](#app-running-in-emulator)。 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>後續步驟
深入了解 hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg)檔案。

建立 [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 封裝。

為角色啟用 [遠端桌面](cloud-services-role-enable-remote-desktop.md) 。

