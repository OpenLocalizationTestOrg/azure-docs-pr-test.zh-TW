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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a><span data-ttu-id="490b8-103">使用 Azure Service Fabric CLI 來管理 Azure Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-103">Manage an Azure Service Fabric application by using Azure Service Fabric CLI</span></span>

<span data-ttu-id="490b8-104">深入了解如何 toocreate 和刪除 Azure Service Fabric 叢集中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="490b8-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="490b8-105">Prerequisites</span></span>

* <span data-ttu-id="490b8-106">安裝 Service Fabric CLI。</span><span class="sxs-lookup"><span data-stu-id="490b8-106">Install Service Fabric CLI.</span></span> <span data-ttu-id="490b8-107">然後選取 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="490b8-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="490b8-108">如需詳細資訊，請參閱[開始使用 Service Fabric CLI](service-fabric-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="490b8-108">For more information, see [Get started with Service Fabric CLI](service-fabric-cli.md).</span></span>

* <span data-ttu-id="490b8-109">擁有 Service Fabric 應用程式封裝準備 toobe 部署。</span><span class="sxs-lookup"><span data-stu-id="490b8-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="490b8-110">如需有關如何 tooauthor 和封裝應用程式中，閱讀 hello [Service Fabric 應用程式模型](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="490b8-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="490b8-111">概觀</span><span class="sxs-lookup"><span data-stu-id="490b8-111">Overview</span></span>

<span data-ttu-id="490b8-112">toodeploy 新的應用程式，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="490b8-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="490b8-113">上傳應用程式封裝 toohello Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="490b8-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="490b8-114">佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="490b8-114">Provision an application type.</span></span>
3. <span data-ttu-id="490b8-115">指定和建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-115">Specify and create an application.</span></span>
4. <span data-ttu-id="490b8-116">指定和建立服務。</span><span class="sxs-lookup"><span data-stu-id="490b8-116">Specify and create services.</span></span>

<span data-ttu-id="490b8-117">tooremove 現有的應用程式，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="490b8-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="490b8-118">刪除 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-118">Delete hello application.</span></span>
2. <span data-ttu-id="490b8-119">解除佈建 hello 相關聯應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="490b8-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="490b8-120">刪除 hello 映像存放區的內容。</span><span class="sxs-lookup"><span data-stu-id="490b8-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="490b8-121">部署新應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-121">Deploy a new application</span></span>

<span data-ttu-id="490b8-122">toodeploy 新的應用程式，完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-122">toodeploy a new application, complete hello following tasks:</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="490b8-123">上傳新的應用程式封裝 toohello 映像存放區</span><span class="sxs-lookup"><span data-stu-id="490b8-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="490b8-124">建立應用程式之前，先上傳 hello 應用程式封裝 toohello Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="490b8-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span>

<span data-ttu-id="490b8-125">例如，如果您的應用程式封裝在 hello`app_package_dir`目錄中，使用下列命令 tooupload hello 目錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir
```

<span data-ttu-id="490b8-126">針對大型應用程式封裝，您可以指定 hello`--show-progress`選項 toodisplay hello hello 上傳進度。</span><span class="sxs-lookup"><span data-stu-id="490b8-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="490b8-127">佈建 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="490b8-127">Provision hello application type</span></span>

<span data-ttu-id="490b8-128">Hello 上傳完成時，佈建 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="490b8-129">tooprovision hello 應用程式，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="490b8-130">hello 值`application-type-build-path`hello hello 您上傳您的應用程式封裝的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="490b8-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="490b8-131">從應用程式類型建立應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-131">Create an application from an application type</span></span>

<span data-ttu-id="490b8-132">您佈建 hello 應用程式之後，請使用下列命令 tooname hello，並建立您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="490b8-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="490b8-133">`app-name`這是 hello 的 toouse hello 應用程式執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="490b8-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="490b8-134">您可以從先前佈建的應用程式資訊清單取得額外的參數。</span><span class="sxs-lookup"><span data-stu-id="490b8-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="490b8-135">hello 應用程式名稱必須以 hello 前置詞開頭`fabric:/`。</span><span class="sxs-lookup"><span data-stu-id="490b8-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="490b8-136">建立 hello 新應用程式的服務</span><span class="sxs-lookup"><span data-stu-id="490b8-136">Create services for hello new application</span></span>

<span data-ttu-id="490b8-137">建立應用程式之後，請從 hello 應用程式建立服務。</span><span class="sxs-lookup"><span data-stu-id="490b8-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="490b8-138">在下列範例的 hello，我們會建立新的無狀態服務從我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="490b8-139">您可以從應用程式建立的 hello 服務定義 hello 先前已佈建應用程式封裝中的服務資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="490b8-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="490b8-140">確認應用程式部署和健康情況</span><span class="sxs-lookup"><span data-stu-id="490b8-140">Verify application deployment and health</span></span>

<span data-ttu-id="490b8-141">tooverify 一切狀況良好，請使用下列健全狀況命令 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-141">tooverify everything is healthy, use hello following health commands:</span></span>

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

<span data-ttu-id="490b8-142">tooverify hello 服務狀況良好，請使用類似命令 tooretrieve hello 的健全狀況 hello 服務和應用程式：</span><span class="sxs-lookup"><span data-stu-id="490b8-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and the application:</span></span>

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

<span data-ttu-id="490b8-143">狀況良好的服務和應用程式的 `Ok` 值是 `HealthState`。</span><span class="sxs-lookup"><span data-stu-id="490b8-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="490b8-144">移除現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-144">Remove an existing application</span></span>

<span data-ttu-id="490b8-145">tooremove 應用程式，完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-145">tooremove an application, complete hello following tasks:</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="490b8-146">刪除 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-146">Delete hello application</span></span>

<span data-ttu-id="490b8-147">toodelete hello 應用程式，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-147">toodelete hello application, use hello following command:</span></span>

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="490b8-148">解除佈建 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="490b8-148">Unprovision hello application type</span></span>

<span data-ttu-id="490b8-149">刪除 hello 應用程式之後，您可以在解除如果不再需要佈建 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="490b8-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="490b8-150">toounprovision hello 應用程式類型，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="490b8-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="490b8-151">hello 名稱和版本 hello 先前已佈建應用程式資訊清單中的，必須符合 hello 型別名稱和型別版本。</span><span class="sxs-lookup"><span data-stu-id="490b8-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="490b8-152">刪除 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="490b8-152">Delete hello application package</span></span>

<span data-ttu-id="490b8-153">您必須已解除佈建 hello 應用程式類型之後，您可以刪除 hello 應用程式套件 hello 映像存放區如果不再需要。</span><span class="sxs-lookup"><span data-stu-id="490b8-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="490b8-154">刪除應用程式套件有助於回收磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="490b8-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="490b8-155">從 hello 映像存放區，下列命令使用 hello toodelete hello 應用程式封裝：</span><span class="sxs-lookup"><span data-stu-id="490b8-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
sfctl store delete --content-path app_package_dir
```

<span data-ttu-id="490b8-156">`content-path`必須是 hello 您上傳您建立 hello 應用程式時的 hello 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="490b8-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="upgrade-application"></a><span data-ttu-id="490b8-157">升級應用程式</span><span class="sxs-lookup"><span data-stu-id="490b8-157">Upgrade application</span></span>

<span data-ttu-id="490b8-158">您可以建立您的應用程式之後, 重複 hello 同一組步驟 tooprovision 第二個版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-158">After creating your application, you can repeat hello same set of steps tooprovision a second version of your application.</span></span> <span data-ttu-id="490b8-159">然後，Service Fabric 應用程式升級，您可以轉換 toorunning hello 第二個版本 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="490b8-159">Then, with a Service Fabric application upgrade you can transition toorunning hello second version of hello application.</span></span> <span data-ttu-id="490b8-160">如需詳細資訊，請參閱 hello 文件上[Service Fabric 應用程式升級](service-fabric-application-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="490b8-160">For more information, see hello documentation on [Service Fabric application upgrades](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="490b8-161">tooperform 升級時，第一個佈建 hello 下一版的 hello 應用程式使用與之前 hello 相同的命令：</span><span class="sxs-lookup"><span data-stu-id="490b8-161">tooperform an upgrade, first provision hello next version of hello application using hello same commands as before:</span></span>

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

<span data-ttu-id="490b8-162">我們建議然後 tooperform 受監視的自動升級時，執行下列命令的 hello 啟動 hello 升級：</span><span class="sxs-lookup"><span data-stu-id="490b8-162">It is recommended then tooperform a monitored automatic upgrade, launch hello upgrade by running hello following command:</span></span>

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

<span data-ttu-id="490b8-163">升級會以指定的任何設定覆寫現有參數。</span><span class="sxs-lookup"><span data-stu-id="490b8-163">Upgrades override existing parameters with whatever set is specified.</span></span> <span data-ttu-id="490b8-164">如有必要，應該傳遞應用程式參數做為引數 toohello 升級命令。</span><span class="sxs-lookup"><span data-stu-id="490b8-164">Application parameters should be passed as arguments toohello upgrade command, if necessary.</span></span> <span data-ttu-id="490b8-165">應用程式參數應該編碼為 JSON 物件。</span><span class="sxs-lookup"><span data-stu-id="490b8-165">Application parameters should be encoded as a JSON object.</span></span>

<span data-ttu-id="490b8-166">tooretrieve 先前指定任何參數，您可以使用 hello`sfctl application info`命令。</span><span class="sxs-lookup"><span data-stu-id="490b8-166">tooretrieve any parameters previously specified, you can use hello `sfctl application info` command.</span></span>

<span data-ttu-id="490b8-167">當應用程式升級正在進行時，可以使用擷取 hello 狀態`sfctl application upgrade-status`命令。</span><span class="sxs-lookup"><span data-stu-id="490b8-167">When an application upgrade is in progress, hello status can be retrieved using the `sfctl application upgrade-status` command.</span></span>

<span data-ttu-id="490b8-168">最後，如果升級正在進行中，且需要 toobe 取消，您可以使用 hello `sfctl application upgrade-rollback` tooroll 回 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="490b8-168">Finally, if an upgrade is in progress and needs toobe canceled, you can use hello `sfctl application upgrade-rollback` tooroll back hello upgrade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="490b8-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="490b8-169">Next steps</span></span>

* [<span data-ttu-id="490b8-170">Service Fabric CLI 基本概念</span><span class="sxs-lookup"><span data-stu-id="490b8-170">Service Fabric CLI basics</span></span>](service-fabric-cli.md)
* [<span data-ttu-id="490b8-171">在 Linux 上開始使用 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="490b8-171">Getting started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="490b8-172">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="490b8-172">Launching a Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
