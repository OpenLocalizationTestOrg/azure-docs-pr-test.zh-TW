---
title: "使用 Azure Service Fabric CLI aaaManage Azure Service Fabric 應用程式"
description: "了解如何使用 Azure Service Fabric CLI toodeploy] 和 [移除應用程式，從 Azure Service Fabric 叢集"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>使用 Azure Service Fabric CLI 來管理 Azure Service Fabric 應用程式

深入了解如何 toocreate 和刪除 Azure Service Fabric 叢集中執行的應用程式。

## <a name="prerequisites"></a>必要條件

* 安裝 Service Fabric CLI。 然後選取 Service Fabric 叢集。 如需詳細資訊，請參閱[開始使用 Service Fabric CLI](service-fabric-cli.md)。

* 擁有 Service Fabric 應用程式封裝準備 toobe 部署。 如需有關如何 tooauthor 和封裝應用程式中，閱讀 hello [Service Fabric 應用程式模型](service-fabric-application-model.md)。

## <a name="overview"></a>概觀

toodeploy 新的應用程式，完成下列步驟：

1. 上傳應用程式封裝 toohello Service Fabric 映像存放區。
2. 佈建應用程式類型。
3. 指定和建立應用程式。
4. 指定和建立服務。

tooremove 現有的應用程式，完成下列步驟：

1. 刪除 hello 應用程式。
2. 解除佈建 hello 相關聯應用程式類型。
3. 刪除 hello 映像存放區的內容。

## <a name="deploy-a-new-application"></a>部署新應用程式

toodeploy 新的應用程式，完成下列工作的 hello:

### <a name="upload-a-new-application-package-toohello-image-store"></a>上傳新的應用程式封裝 toohello 映像存放區

建立應用程式之前，先上傳 hello 應用程式封裝 toohello Service Fabric 映像存放區。

例如，如果您的應用程式封裝在 hello`app_package_dir`目錄中，使用下列命令 tooupload hello 目錄的 hello:

```azurecli
sfctl application upload --path ~/app_package_dir
```

針對大型應用程式封裝，您可以指定 hello`--show-progress`選項 toodisplay hello hello 上傳進度。

### <a name="provision-hello-application-type"></a>佈建 hello 應用程式類型

Hello 上傳完成時，佈建 hello 應用程式。 tooprovision hello 應用程式，下列命令使用 hello:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

hello 值`application-type-build-path`hello hello 您上傳您的應用程式封裝的目錄名稱。

### <a name="create-an-application-from-an-application-type"></a>從應用程式類型建立應用程式

您佈建 hello 應用程式之後，請使用下列命令 tooname hello，並建立您的應用程式：

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`這是 hello 的 toouse hello 應用程式執行個體的名稱。 您可以從先前佈建的應用程式資訊清單取得額外的參數。

hello 應用程式名稱必須以 hello 前置詞開頭`fabric:/`。

### <a name="create-services-for-hello-new-application"></a>建立 hello 新應用程式的服務

建立應用程式之後，請從 hello 應用程式建立服務。 在下列範例的 hello，我們會建立新的無狀態服務從我們的應用程式。 您可以從應用程式建立的 hello 服務定義 hello 先前已佈建應用程式封裝中的服務資訊清單中。

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>確認應用程式部署和健康情況

tooverify 一切狀況良好，請使用下列健全狀況命令 hello:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

tooverify hello 服務狀況良好，請使用類似命令 tooretrieve hello 的健全狀況 hello 服務和應用程式：

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

狀況良好的服務和應用程式的 `Ok` 值是 `HealthState`。

## <a name="remove-an-existing-application"></a>移除現有的應用程式

tooremove 應用程式，完成下列工作的 hello:

### <a name="delete-hello-application"></a>刪除 hello 應用程式

toodelete hello 應用程式，下列命令使用 hello:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>解除佈建 hello 應用程式類型

刪除 hello 應用程式之後，您可以在解除如果不再需要佈建 hello 應用程式類型。 toounprovision hello 應用程式類型，下列命令使用 hello:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

hello 名稱和版本 hello 先前已佈建應用程式資訊清單中的，必須符合 hello 型別名稱和型別版本。

### <a name="delete-hello-application-package"></a>刪除 hello 應用程式套件

您必須已解除佈建 hello 應用程式類型之後，您可以刪除 hello 應用程式套件 hello 映像存放區如果不再需要。 刪除應用程式套件有助於回收磁碟空間。 

從 hello 映像存放區，下列命令使用 hello toodelete hello 應用程式封裝：

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`必須是 hello 您上傳您建立 hello 應用程式時的 hello 目錄名稱。

## <a name="upgrade-application"></a>升級應用程式

您可以建立您的應用程式之後, 重複 hello 同一組步驟 tooprovision 第二個版本的應用程式。 然後，Service Fabric 應用程式升級，您可以轉換 toorunning hello 第二個版本 hello 應用程式。 如需詳細資訊，請參閱 hello 文件上[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。

tooperform 升級時，第一個佈建 hello 下一版的 hello 應用程式使用與之前 hello 相同的命令：

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

我們建議然後 tooperform 受監視的自動升級時，執行下列命令的 hello 啟動 hello 升級：

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

升級會以指定的任何設定覆寫現有參數。 如有必要，應該傳遞應用程式參數做為引數 toohello 升級命令。 應用程式參數應該編碼為 JSON 物件。

tooretrieve 先前指定任何參數，您可以使用 hello`sfctl application info`命令。

當應用程式升級正在進行時，可以使用擷取 hello 狀態`sfctl application upgrade-status`命令。

最後，如果升級正在進行中，且需要 toobe 取消，您可以使用 hello `sfctl application upgrade-rollback` tooroll 回 hello 升級。

## <a name="next-steps"></a>後續步驟

* [Service Fabric CLI 基本概念](service-fabric-cli.md)
* [在 Linux 上開始使用 Service Fabric](service-fabric-get-started-linux.md)
* [Service Fabric 應用程式升級](service-fabric-application-upgrade.md)
