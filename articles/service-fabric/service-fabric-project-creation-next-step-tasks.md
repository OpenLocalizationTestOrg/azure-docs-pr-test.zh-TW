---
title: "aaaService 網狀架構專案建立後續步驟 |Microsoft 文件"
description: "本文章包含連結 tooa 組的核心開發工作適用於 Service Fabric"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>您的 Service Fabric 應用程式和後續步驟
您的 Azure Service Fabric 應用程式已經建立。 本文說明 hello 結構的一些可能的後續步驟和您的專案。

## <a name="your-application"></a>您的應用程式
每個新應用程式都包含一個應用程式專案。 可能有一或兩個其他專案中的，視選擇服務 hello 類型而定。

### <a name="hello-application-project"></a>hello 應用程式專案
hello 應用程式專案所組成：

* 一組構成應用程式的參考 toohello 服務。
* 三個發行，您可以使用 toomaintain 喜好設定，使用不同的環境-例如喜好設定相關的 tooa 叢集端點，以及是否 tooperform 升級部署預設的設定檔 （1 節點本機、 5 節點本機和雲端）。
* 三個應用程式參數檔案 （同上），您可以使用 toomaintain 環境特定應用程式設定，例如服務的資料分割 toocreate 的 hello 數目。
* 部署指令碼，您可以使用 toodeploy 應用程式從 hello 命令列，或做為自動化的連續整合及部署管線的一部分。
* hello 應用程式資訊清單，其中描述 hello 應用程式。 您可以在 hello ApplicationPackageRoot 資料夾下找到 hello 資訊清單。

### <a name="stateless-service"></a>無狀態服務
當您新增新的無狀態服務時，Visual Studio 會加入包含類型，從繼承而來的服務專案 tooyour 解決方案`StatelessService`。 hello 服務遞增計數器中的區域變數。

### <a name="stateful-service"></a>具狀態服務
當您新增新的可設定狀態服務時，Visual Studio 會加入包含類型，從繼承而來的服務專案 tooyour 解決方案`StatefulService`。 hello 服務遞增計數器中的其`RunAsync`方法和存放區中的 hello 結果`ReliableDictionary`。

### <a name="actor-service"></a>動作項目服務
當您新增新的可靠動作項目時，Visual Studio 會加入兩個專案 tooyour 方案： 執行者專案和介面的專案。

hello 執行者專案提供方法來設定和取得 hello 計數器的值可靠地保存在 hello 動作項目的狀態。 hello 介面專案提供介面的其他服務可以使用 tooinvoke hello 動作項目。

### <a name="stateless-web-api"></a>無狀態 Web API
hello 無狀態 Web API 專案提供基本 web 服務，您可以使用 tooopen tooexternal 用戶端應用程式。 如需 hello 專案的結構化的詳細資訊，請參閱[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)。


### <a name="aspnet-core"></a>ASP.NET 核心
hello Service Fabric SDK 提供的相同設定的 ASP.NET Core 範本可供獨立 ASP.NET Core 專案的 hello： 空的[Web API][aspnet-webapi]，和[Web 應用程式][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>客體可執行檔和客體容器

服務網狀架構 'guest' 是不以 hello 平台的程式設計模型所建立的服務。 您可以將封裝 hello 二進位檔的來賓是[hello 應用程式封裝中直接](service-fabric-deploy-existing-app.md)或[容器映像透過](service-fabric-deploy-container.md)。 在這兩種情況下，Visual Studio 會建立 hello hello 中的必要成品**ApplicationPackageRoot** hello 應用程式專案的資料夾。 Visual Studio 不會建立新的服務專案，因為 hello 代碼已經存在其他位置。 如果您想要的 toomanage 對來賓專案一起 hello Service Fabric 應用程式專案，您可以將它們加入 toohello 相同的 Visual Studio 方案。

## <a name="next-steps"></a>後續步驟
### <a name="create-an-azure-cluster"></a>建立 Azure 叢集
hello Service Fabric SDK 提供開發和測試的本機叢集。 toocreate 叢集，以在 Azure 中，請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集][create-cluster-in-portal]。

### <a name="publish-your-application-tooazure"></a>發行應用程式 tooAzure
您可以發佈您的應用程式，直接從 Visual Studio tooan Azure 的叢集。 toolearn 作法，請參閱[發行應用程式 tooAzure][publish-app-to-azure]。

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>使用 Service Fabric 總管 toovisualize 您的叢集
Service Fabric 總管提供簡單的方式 toovisualize 您的叢集，包括部署的應用程式和實體配置。 詳細資訊，請參閱 toolearn[視覺化您的叢集，利用 Service Fabric 總管][visualize-with-sfx]。

### <a name="version-and-upgrade-your-services"></a>進行服務版本設定和升級
Service Fabric 可讓您為應用程式中的獨立服務進行獨立的版本設定和升級。 詳細資訊，請參閱 toolearn[版本控制和升級您的服務][app-upgrade-tutorial]。

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>使用 Visual Studio Team Services 設定持續整合
toolearn 如何設定連續整合程序 Service Fabric 應用程式，請參閱[設定與 Visual Studio Team Services 的連續整合][ci-with-vso]。

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
