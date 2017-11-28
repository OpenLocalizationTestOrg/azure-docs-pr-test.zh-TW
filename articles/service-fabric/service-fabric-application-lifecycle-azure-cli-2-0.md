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
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="439b2-103">使用 Azure CLI 2.0 來管理 Azure Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="439b2-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="439b2-104">深入了解如何 toocreate 和刪除 Azure Service Fabric 叢集中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b2-104">Learn how toocreate and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="439b2-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="439b2-105">Prerequisites</span></span>

* <span data-ttu-id="439b2-106">安裝 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="439b2-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="439b2-107">然後選取 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="439b2-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="439b2-108">如需詳細資訊，請參閱[開始使用 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)。</span><span class="sxs-lookup"><span data-stu-id="439b2-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="439b2-109">擁有 Service Fabric 應用程式封裝準備 toobe 部署。</span><span class="sxs-lookup"><span data-stu-id="439b2-109">Have a Service Fabric application package ready toobe deployed.</span></span> <span data-ttu-id="439b2-110">如需有關如何 tooauthor 和封裝應用程式中，閱讀 hello [Service Fabric 應用程式模型](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="439b2-110">For more information about how tooauthor and package an application, read about hello [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="439b2-111">概觀</span><span class="sxs-lookup"><span data-stu-id="439b2-111">Overview</span></span>

<span data-ttu-id="439b2-112">toodeploy 新的應用程式，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="439b2-112">toodeploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="439b2-113">上傳應用程式封裝 toohello Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="439b2-113">Upload an application package toohello Service Fabric image store.</span></span>
2. <span data-ttu-id="439b2-114">佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="439b2-114">Provision an application type.</span></span>
3. <span data-ttu-id="439b2-115">指定和建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b2-115">Specify and create an application.</span></span>
4. <span data-ttu-id="439b2-116">指定和建立服務。</span><span class="sxs-lookup"><span data-stu-id="439b2-116">Specify and create services.</span></span>

<span data-ttu-id="439b2-117">tooremove 現有的應用程式，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="439b2-117">tooremove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="439b2-118">刪除 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b2-118">Delete hello application.</span></span>
2. <span data-ttu-id="439b2-119">解除佈建 hello 相關聯應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="439b2-119">Unprovision hello associated application type.</span></span>
3. <span data-ttu-id="439b2-120">刪除 hello 映像存放區的內容。</span><span class="sxs-lookup"><span data-stu-id="439b2-120">Delete hello image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="439b2-121">部署新應用程式</span><span class="sxs-lookup"><span data-stu-id="439b2-121">Deploy a new application</span></span>

<span data-ttu-id="439b2-122">toodeploy 新的應用程式，完成下列工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="439b2-122">toodeploy a new application, complete hello following tasks.</span></span>

### <a name="upload-a-new-application-package-toohello-image-store"></a><span data-ttu-id="439b2-123">上傳新的應用程式封裝 toohello 映像存放區</span><span class="sxs-lookup"><span data-stu-id="439b2-123">Upload a new application package toohello image store</span></span>

<span data-ttu-id="439b2-124">建立應用程式之前，先上傳 hello 應用程式封裝 toohello Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="439b2-124">Before you create an application, upload hello application package toohello Service Fabric image store.</span></span> 

<span data-ttu-id="439b2-125">例如，如果您的應用程式封裝在 hello`app_package_dir`目錄中，使用下列命令 tooupload hello 目錄的 hello:</span><span class="sxs-lookup"><span data-stu-id="439b2-125">For example, if your application package is in hello `app_package_dir` directory, use hello following commands tooupload hello directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="439b2-126">針對大型應用程式封裝，您可以指定 hello`--show-progress`選項 toodisplay hello hello 上傳進度。</span><span class="sxs-lookup"><span data-stu-id="439b2-126">For large application packages, you can specify hello `--show-progress` option toodisplay hello progress of hello upload.</span></span>

### <a name="provision-hello-application-type"></a><span data-ttu-id="439b2-127">佈建 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="439b2-127">Provision hello application type</span></span>

<span data-ttu-id="439b2-128">Hello 上傳完成時，佈建 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b2-128">When hello upload is finished, provision hello application.</span></span> <span data-ttu-id="439b2-129">tooprovision hello 應用程式，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="439b2-129">tooprovision hello application, use hello following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="439b2-130">hello 值`application-type-build-path`hello hello 您上傳您的應用程式封裝的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="439b2-130">hello value for `application-type-build-path` is hello name of hello directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="439b2-131">從應用程式類型建立應用程式</span><span class="sxs-lookup"><span data-stu-id="439b2-131">Create an application from an application type</span></span>

<span data-ttu-id="439b2-132">您佈建 hello 應用程式之後，請使用下列命令 tooname hello，並建立您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="439b2-132">After you provision hello application, use hello following command tooname and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="439b2-133">`app-name`這是 hello 的 toouse hello 應用程式執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="439b2-133">`app-name` is hello name that you want toouse for hello application instance.</span></span> <span data-ttu-id="439b2-134">您可以從 hello 先前已佈建應用程式資訊清單，以取得額外的參數。</span><span class="sxs-lookup"><span data-stu-id="439b2-134">You can get additional parameters from hello previously provisioned application manifest.</span></span>

<span data-ttu-id="439b2-135">hello 應用程式名稱必須以 hello 前置詞開頭`fabric:/`。</span><span class="sxs-lookup"><span data-stu-id="439b2-135">hello application name must start with hello prefix `fabric:/`.</span></span>

### <a name="create-services-for-hello-new-application"></a><span data-ttu-id="439b2-136">建立 hello 新應用程式的服務</span><span class="sxs-lookup"><span data-stu-id="439b2-136">Create services for hello new application</span></span>

<span data-ttu-id="439b2-137">建立應用程式之後，請從 hello 應用程式建立服務。</span><span class="sxs-lookup"><span data-stu-id="439b2-137">After you have created an application, create services from hello application.</span></span> <span data-ttu-id="439b2-138">在下列範例的 hello，我們會建立新的無狀態服務從我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="439b2-138">In hello following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="439b2-139">您可以從應用程式建立的 hello 服務定義 hello 先前已佈建應用程式封裝中的服務資訊清單中。</span><span class="sxs-lookup"><span data-stu-id="439b2-139">hello services that you can create from an application are defined in a service manifest in hello previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="439b2-140">確認應用程式部署和健康情況</span><span class="sxs-lookup"><span data-stu-id="439b2-140">Verify application deployment and health</span></span>

<span data-ttu-id="439b2-141">tooverify，應用程式及服務已成功部署，檢查列出 hello 應用程式和服務：</span><span class="sxs-lookup"><span data-stu-id="439b2-141">tooverify that an application and service were successfully deployed, check that hello application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="439b2-142">tooverify hello 服務狀況良好，請使用類似命令 tooretrieve hello 的健全狀況服務 hello 和 hello 應用程式：</span><span class="sxs-lookup"><span data-stu-id="439b2-142">tooverify that hello service is healthy, use similar commands tooretrieve hello health of both hello service and hello application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="439b2-143">狀況良好的服務和應用程式的 `Ok` 值是 `HealthState`。</span><span class="sxs-lookup"><span data-stu-id="439b2-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="439b2-144">移除現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="439b2-144">Remove an existing application</span></span>

<span data-ttu-id="439b2-145">tooremove 應用程式，完成下列工作的 hello。</span><span class="sxs-lookup"><span data-stu-id="439b2-145">tooremove an application, complete hello following tasks.</span></span>

### <a name="delete-hello-application"></a><span data-ttu-id="439b2-146">刪除 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="439b2-146">Delete hello application</span></span>

<span data-ttu-id="439b2-147">toodelete hello 應用程式，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="439b2-147">toodelete hello application, use hello following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a><span data-ttu-id="439b2-148">解除佈建 hello 應用程式類型</span><span class="sxs-lookup"><span data-stu-id="439b2-148">Unprovision hello application type</span></span>

<span data-ttu-id="439b2-149">刪除 hello 應用程式之後，您可以在解除如果不再需要佈建 hello 應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="439b2-149">After you delete hello application, you can unprovision hello application type if you no longer need it.</span></span> <span data-ttu-id="439b2-150">toounprovision hello 應用程式類型，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="439b2-150">toounprovision hello application type, use hello following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="439b2-151">hello 名稱和版本 hello 先前已佈建應用程式資訊清單中的，必須符合 hello 型別名稱和型別版本。</span><span class="sxs-lookup"><span data-stu-id="439b2-151">hello type name and type version must match hello name and version in hello previously provisioned application manifest.</span></span>

### <a name="delete-hello-application-package"></a><span data-ttu-id="439b2-152">刪除 hello 應用程式套件</span><span class="sxs-lookup"><span data-stu-id="439b2-152">Delete hello application package</span></span>

<span data-ttu-id="439b2-153">您必須已解除佈建 hello 應用程式類型之後，您可以刪除 hello 應用程式套件 hello 映像存放區如果不再需要。</span><span class="sxs-lookup"><span data-stu-id="439b2-153">After you have unprovisioned hello application type, you can delete hello application package from hello image store if you no longer need it.</span></span> <span data-ttu-id="439b2-154">刪除應用程式套件有助於回收磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="439b2-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="439b2-155">從 hello 映像存放區，下列命令使用 hello toodelete hello 應用程式封裝：</span><span class="sxs-lookup"><span data-stu-id="439b2-155">toodelete hello application package from hello image store, use hello following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="439b2-156">`content-path`必須是 hello 您上傳您建立 hello 應用程式時的 hello 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="439b2-156">`content-path` must be hello name of hello directory that you uploaded when you created hello application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="439b2-157">相關文章</span><span class="sxs-lookup"><span data-stu-id="439b2-157">Related articles</span></span>

* [<span data-ttu-id="439b2-158">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="439b2-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="439b2-159">開始使用 Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="439b2-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
