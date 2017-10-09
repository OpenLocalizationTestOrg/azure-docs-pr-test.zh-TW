---
title: "aaaAzure 服務網狀架構 Docker 撰寫預覽"
description: "Azure Service Fabric 接受 Docker Compose 格式 toomake 它更容易使用 Service Fabric tooorchestrate 現有容器。 這項支援目前只能預覽。"
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
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Azure Service Fabric 中 Docker Compose 的應用程式支援 (預覽)

Docker 使用 hello [docker compose.yml](https://docs.docker.com/compose)定義多個容器應用程式的檔案。 toomake 它熟悉 Docker tooorchestrate 現有容器應用程式在 Azure Service Fabric 的客戶輕鬆，我們要加入的 Docker Compose 的預覽支援原生 hello 平台。 Service Fabric 可接受版本 3 以上的 `docker-compose.yml` 檔案。 

此支援目前只能預覽，因此僅支援 Compose 指示詞子集。 例如，不支援應用程式升級。 但是，您一律能夠移除與部署應用程式，而非升級。

此預覽 toouse，5.7 或更高的 hello Service Fabric 執行階段透過 hello hello 對應 SDK 以及 Azure 入口網站，建立您的叢集與版本。 

> [!NOTE]
> 此功能目前只能預覽，尚未在生產環境中受到支援。

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>在 Service Fabric 上部署 Docker Compose 檔案

hello 下列命令會建立 Service Fabric 應用程式 (名為`fabric:/TestContainerApp`hello 前面範例中)，您可以監視並管理任何其他的 Service Fabric 應用程式一樣。 您可以使用健康狀態查詢的 hello 指定的應用程式名稱。

### <a name="use-powershell"></a>使用 PowerShell

建立 Service Fabric 撰寫的應用程式從 docker compose.yml 檔案，藉由執行下列命令在 PowerShell 中的 hello:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`和`RegistryPassword`toohello 容器登錄使用者名稱和密碼，請參閱。 Hello 應用程式完成之後，您可以使用下列命令的 hello 檢查其狀態：

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete hello 撰寫應用程式，透過 PowerShell，請使用下列命令的 hello:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>使用 Azure Service Fabric CLI (sfctl)

或者，您可以使用下列服務網狀架構 CLI 命令的 hello:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

在您建立 hello 應用程式後，您可以使用下列命令的 hello 檢查其狀態：

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

toodelete hello 撰寫應用程式，請使用下列命令的 hello:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>支援的撰寫指示詞

本預覽版支援從 hello 撰寫第 3 版格式，包括下列基本類型的 hello hello 組態選項的子集：

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

中所述，設定強制執行資源限制的 hello 叢集[Service Fabric 資源控管](service-fabric-resource-governance.md)。 此預覽不支援所有其他的 Docker Compose 指示詞。

## <a name="servicednsname-computation"></a>ServiceDnsName 計算

如果您在撰寫檔案中指定的 hello 服務名稱是完整的網域名稱 （也就是它包含點 [.]），註冊 Service Fabric hello DNS 名稱是`<ServiceName>`（包括 hello 點）。 否則，每個路徑區段 hello 應用程式名稱會成為網域中的標籤與 hello 成為 hello 最上層網域標籤第一個路徑區段，hello 服務 DNS 名稱。

例如，如果 hello 指定應用程式名稱是`fabric:/SampleApp/MyComposeApp`，`<ServiceName>.MyComposeApp.SampleApp`會 hello 已註冊的 DNS 名稱。

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Compose (執行個體定義) 與 Service Fabric 應用程式模型 (類型定義) 之間的差異

docker-compose.yml 檔案描述一組可部署的容器，包括其屬性與組態。
例如，hello 檔案可以包含環境變數和連接埠。 您也可以在 hello docker compose.yml 檔案中指定部署參數，例如安置限制、 資源限制，以及 DNS 名稱。

hello [Service Fabric 應用程式模型](service-fabric-application-model.md)使用服務類型和應用程式類型，您可以在其中有許多應用程式執行個體的 hello 相同的型別。 例如，可以讓每個客戶有一個應用程式執行個體。 此類型為基礎的模型支援多個版本的 hello 已向 hello 執行階段的相同應用程式類型。

例如，客戶 A 」 可以有型別 1.0 AppTypeA，使用具現化的應用程式和客戶 B 」 可以有另一個應用程式使用 hello 具現化相同的類型和版本。 您定義 hello 應用程式類型在 hello 應用程式資訊清單，並建立 hello 應用程式時，指定 hello 應用程式名稱和部署參數。

雖然這種模型提供的彈性，我們也計劃 toosupport 更簡單、 執行個體為基礎的部署模型類型的隱含從 hello 資訊清單檔案。 在此模型中，每個應用程式會取得自己的獨立資訊清單。 我們正在透過新增對 docker-compose.yml (這是以執行個體為基礎的部署格式) 的支援來預覽此成果。

## <a name="next-steps"></a>後續步驟

* Hello 上讀取[Service Fabric 應用程式模型](service-fabric-application-model.md)
* [開始使用 Service Fabric CLI](service-fabric-cli.md)
