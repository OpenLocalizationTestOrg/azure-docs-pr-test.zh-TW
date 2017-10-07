---
title: "使用 Azure CLI 2.0 aaaManage Azure Service Fabric 應用程式"
description: "了解如何使用 Azure CLI 2.0 toodeploy] 和 [移除應用程式，從 Azure Service Fabric 叢集。"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ae1ba19513978b0f95ffb65d5f1f7a21ed5f2894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a>使用 Azure CLI 2.0 來管理 Azure Service Fabric 應用程式

深入了解如何 toocreate 和刪除 Azure Service Fabric 叢集中執行的應用程式。

## <a name="prerequisites"></a>必要條件

* 安裝 Azure CLI 2.0。 然後選取 Service Fabric 叢集。 如需詳細資訊，請參閱[開始使用 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)。

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

toodeploy 新的應用程式，完成下列工作的 hello。

### <a name="upload-a-new-application-package-toohello-image-store"></a>上傳新的應用程式封裝 toohello 映像存放區

建立應用程式之前，先上傳 hello 應用程式封裝 toohello Service Fabric 映像存放區。 

例如，如果您的應用程式封裝在 hello`app_package_dir`目錄中，使用下列命令 tooupload hello 目錄的 hello:

```azurecli
az sf application upload --path ~/app_package_dir
```

針對大型應用程式封裝，您可以指定 hello`--show-progress`選項 toodisplay hello hello 上傳進度。

### <a name="provision-hello-application-type"></a>佈建 hello 應用程式類型

Hello 上傳完成時，佈建 hello 應用程式。 tooprovision hello 應用程式，下列命令使用 hello:

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

hello 值`application-type-build-path`hello hello 您上傳您的應用程式封裝的目錄名稱。

### <a name="create-an-application-from-an-application-type"></a>從應用程式類型建立應用程式

您佈建 hello 應用程式之後，請使用下列命令 tooname hello，並建立您的應用程式：

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`這是 hello 的 toouse hello 應用程式執行個體的名稱。 您可以從 hello 先前已佈建應用程式資訊清單，以取得額外的參數。

hello 應用程式名稱必須以 hello 前置詞開頭`fabric:/`。

### <a name="create-services-for-hello-new-application"></a>建立 hello 新應用程式的服務

建立應用程式之後，請從 hello 應用程式建立服務。 在下列範例的 hello，我們會建立新的無狀態服務從我們的應用程式。 您可以從應用程式建立的 hello 服務定義 hello 先前已佈建應用程式封裝中的服務資訊清單中。

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>確認應用程式部署和健康情況

tooverify，應用程式及服務已成功部署，檢查列出 hello 應用程式和服務：

```azurecli
az sf application list
az sf service list --application-list TestApp
```

tooverify hello 服務狀況良好，請使用類似命令 tooretrieve hello 的健全狀況服務 hello 和 hello 應用程式：

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

狀況良好的服務和應用程式的 `Ok` 值是 `HealthState`。

## <a name="remove-an-existing-application"></a>移除現有的應用程式

tooremove 應用程式，完成下列工作的 hello。

### <a name="delete-hello-application"></a>刪除 hello 應用程式

toodelete hello 應用程式，下列命令使用 hello:

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>解除佈建 hello 應用程式類型

刪除 hello 應用程式之後，您可以在解除如果不再需要佈建 hello 應用程式類型。 toounprovision hello 應用程式類型，下列命令使用 hello:

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

hello 名稱和版本 hello 先前已佈建應用程式資訊清單中的，必須符合 hello 型別名稱和型別版本。

### <a name="delete-hello-application-package"></a>刪除 hello 應用程式套件

您必須已解除佈建 hello 應用程式類型之後，您可以刪除 hello 應用程式套件 hello 映像存放區如果不再需要。 刪除應用程式套件有助於回收磁碟空間。 

從 hello 映像存放區，下列命令使用 hello toodelete hello 應用程式封裝：

```azurecli
az sf application package-delete --content-path app_package_dir
```

`content-path`必須是 hello 您上傳您建立 hello 應用程式時的 hello 目錄名稱。

## <a name="related-articles"></a>相關文章

* [開始使用 Service Fabric 和 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [開始使用 Service Fabric XPlat CLI](service-fabric-azure-cli.md)
