---
title: "Azure Service Fabric Docker Compose 預覽"
description: "Azure Service Fabric 接受 Docker Compose 格式，可讓您更輕鬆地使用 Service Fabric 來協調現有容器。 這項支援目前只能預覽。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Azure Service Fabric 中 Docker Compose 的應用程式支援 (預覽)

Docker 使用 [docker-compose.yml](https://docs.docker.com/compose) 檔案定義多容器應用程式。 為了讓客戶能夠輕鬆地熟悉 Docker 以協調 Azure Service Fabric 上的現有容器，因此我們在平台中原生提供 Docker Compose 的預覽支援。 Service Fabric 可接受版本 3 以上的 `docker-compose.yml` 檔案。 

此支援目前只能預覽，因此僅支援 Compose 指示詞子集。 例如，不支援應用程式升級。 但是，您一律能夠移除與部署應用程式，而非升級。

若要使用此預覽，請透過 Azure 入口網站和對應的 SDK，以 Service Fabric 執行階段 5.7 版或更新版本建立您的叢集。 

> [!NOTE]
> 此功能目前只能預覽，尚未在生產環境中受到支援。

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>在 Service Fabric 上部署 Docker Compose 檔案

下列命令會建立一個 Service Fabric 應用程式 (在上述範例中名為 `fabric:/TestContainerApp`)，而監視及管理此應用程式的方式與任何其他 Service Fabric 應用程式一樣。 可使用指定的應用程式名稱查詢健康情況。

### <a name="use-powershell"></a>使用 PowerShell

透過在 PowerShell 中執行下列命令，從 docker-compose.yml 檔案建立 Service Fabric Compose 應用程式：

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName` 和 `RegistryPassword` 是指容器登錄使用者名稱與密碼。 您完成應用程式之後，可以使用下列命令檢查其狀態：

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

若要透過 PowerShell 刪除 Compose 應用程式，請使用下列命令：

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>使用 Azure Service Fabric CLI (sfctl)

或者，您也可以使用下列 Service Fabric CLI 命令：

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

您建立應用程式之後，可以使用下列命令檢查其狀態：

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

若要刪除該 Compose 應用程式，請使用下列命令：

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>支援的撰寫指示詞

此預覽支援 Compose 第 3 版格式的組態選項子集，包括下列基本項目：

* 服務 > 部署 > 複本
* 服務 > 部署 > 放置 > 條件約束
* 服務 > 部署 > 資源 > 限制
    * -cpu-shares
    * -memory
    * -memory-swap
* 服務 > 命令
* 服務 > 環境
* 服務 > 連接埠
* 服務 > 映像
* 服務 > 隔離 (僅適用於 Windows)
* 服務 > 記錄 > 驅動程式
* 服務 > 記錄 > 驅動程式 > 選項
* 磁碟區與部署 > 磁碟區

設定叢集，以便強制執行資源限制，如 [Service Fabric 資源管理](service-fabric-resource-governance.md) (英文) 中所述。 此預覽不支援所有其他的 Docker Compose 指示詞。

## <a name="servicednsname-computation"></a>ServiceDnsName 計算

如果在 Compose 檔案中指定的服務名稱是完整的網域名稱 (亦即包含點 [.])，則由 Service Fabric 註冊的 DNS 名稱為 `<ServiceName>` (包含點)。 如果不是，則應用程式名稱中的每個路徑線段會變成服務 DNS 名稱中的網域標籤，其中的第一個路徑線段會變成最上層的網域標籤。

例如，如果指定的應用程式名稱是 `fabric:/SampleApp/MyComposeApp`，則 `<ServiceName>.MyComposeApp.SampleApp` 會是註冊的 DNS 名稱。

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Compose (執行個體定義) 與 Service Fabric 應用程式模型 (類型定義) 之間的差異

docker-compose.yml 檔案描述一組可部署的容器，包括其屬性與組態。
例如，此檔案可包含環境變數與連接埠。 您也可以在 docker-compose.yml 檔案中指定放置條件約束、資源限制及 DNS 名稱等部署參數。

[Service Fabric 應用程式模型](service-fabric-application-model.md)使用服務類型與應用程式類型，其中您可以有許多相同類型的應用程式執行個體。 例如，可以讓每個客戶有一個應用程式執行個體。 這個以類型為基礎的模型支援同一個向執行階段註冊之應用程式的多個版本。

例如，客戶 A 可以有一個以類型 1.0 的 AppTypeA 具現化的應用程式，客戶 B 可以有另一個以相同類型與版本具現化的應用程式。 您在應用程式資訊清單中定義應用程式類型，並且在建立應用程式時指定應用程式名稱與部署參數。

雖然此模型提供彈性，但我們也正在規劃支援更簡單、以執行個體為基礎的部署類型，其中類型在資訊清單檔案中是隱含的。 在此模型中，每個應用程式會取得自己的獨立資訊清單。 我們正在透過新增對 docker-compose.yml (這是以執行個體為基礎的部署格式) 的支援來預覽此成果。

## <a name="next-steps"></a>後續步驟

* 參閱 [Service Fabric 應用程式模型](service-fabric-application-model.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)
