---
title: "使用 Azure CLI 2.0 來管理 Azure Service Fabric 應用程式"
description: "了解如何使用 Azure CLI 2.0 在 Azure Service Fabric 叢集中部署和移除應用程式。"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: 5728339236e3819b301e428f9d7a8add08f02b3e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-cli-20"></a><span data-ttu-id="5f394-103">使用 Azure CLI 2.0 來管理 Azure Service Fabric 應用程式</span><span class="sxs-lookup"><span data-stu-id="5f394-103">Manage an Azure Service Fabric application by using Azure CLI 2.0</span></span>

<span data-ttu-id="5f394-104">了解如何建立和刪除在 Azure Service Fabric 叢集中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f394-104">Learn how to create and delete applications that are running in an Azure Service Fabric cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f394-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="5f394-105">Prerequisites</span></span>

* <span data-ttu-id="5f394-106">安裝 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="5f394-106">Install Azure CLI 2.0.</span></span> <span data-ttu-id="5f394-107">然後選取 Service Fabric 叢集。</span><span class="sxs-lookup"><span data-stu-id="5f394-107">Then, select your Service Fabric cluster.</span></span> <span data-ttu-id="5f394-108">如需詳細資訊，請參閱[開始使用 Azure CLI 2.0](service-fabric-azure-cli-2-0.md)。</span><span class="sxs-lookup"><span data-stu-id="5f394-108">For more information, see [Get started with Azure CLI 2.0](service-fabric-azure-cli-2-0.md).</span></span>

* <span data-ttu-id="5f394-109">備妥 Service Fabric 應用程式封裝以供部署。</span><span class="sxs-lookup"><span data-stu-id="5f394-109">Have a Service Fabric application package ready to be deployed.</span></span> <span data-ttu-id="5f394-110">如需有關如何撰寫及封裝應用程式的詳細資訊，請參閱 [Service Fabric 應用程式模型](service-fabric-application-model.md)。</span><span class="sxs-lookup"><span data-stu-id="5f394-110">For more information about how to author and package an application, read about the [Service Fabric application model](service-fabric-application-model.md).</span></span>

## <a name="overview"></a><span data-ttu-id="5f394-111">概觀</span><span class="sxs-lookup"><span data-stu-id="5f394-111">Overview</span></span>

<span data-ttu-id="5f394-112">若要部署新應用程式，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f394-112">To deploy a new application, complete these steps:</span></span>

1. <span data-ttu-id="5f394-113">將應用程式封裝上傳到 Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="5f394-113">Upload an application package to the Service Fabric image store.</span></span>
2. <span data-ttu-id="5f394-114">佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="5f394-114">Provision an application type.</span></span>
3. <span data-ttu-id="5f394-115">指定和建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f394-115">Specify and create an application.</span></span>
4. <span data-ttu-id="5f394-116">指定和建立服務。</span><span class="sxs-lookup"><span data-stu-id="5f394-116">Specify and create services.</span></span>

<span data-ttu-id="5f394-117">若要移除現有的應用程式，請完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="5f394-117">To remove an existing application, complete these steps:</span></span>

1. <span data-ttu-id="5f394-118">刪除應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f394-118">Delete the application.</span></span>
2. <span data-ttu-id="5f394-119">將已關聯的應用程式類型解除佈建。</span><span class="sxs-lookup"><span data-stu-id="5f394-119">Unprovision the associated application type.</span></span>
3. <span data-ttu-id="5f394-120">刪除映像存放區內容。</span><span class="sxs-lookup"><span data-stu-id="5f394-120">Delete the image store content.</span></span>

## <a name="deploy-a-new-application"></a><span data-ttu-id="5f394-121">部署新應用程式</span><span class="sxs-lookup"><span data-stu-id="5f394-121">Deploy a new application</span></span>

<span data-ttu-id="5f394-122">若要部署新應用程式，請完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="5f394-122">To deploy a new application, complete the following tasks.</span></span>

### <a name="upload-a-new-application-package-to-the-image-store"></a><span data-ttu-id="5f394-123">將新應用程式套件上傳到映像存放區</span><span class="sxs-lookup"><span data-stu-id="5f394-123">Upload a new application package to the image store</span></span>

<span data-ttu-id="5f394-124">建立應用程式之前，將應用程式封裝上傳到 Service Fabric 映像存放區。</span><span class="sxs-lookup"><span data-stu-id="5f394-124">Before you create an application, upload the application package to the Service Fabric image store.</span></span> 

<span data-ttu-id="5f394-125">例如，如果您的應用程式封裝在 `app_package_dir` 目錄中，使用下列命令上傳目錄：</span><span class="sxs-lookup"><span data-stu-id="5f394-125">For example, if your application package is in the `app_package_dir` directory, use the following commands to upload the directory:</span></span>

```azurecli
az sf application upload --path ~/app_package_dir
```

<span data-ttu-id="5f394-126">針對大型應用程式套件，您可以指定 `--show-progress` 選項以顯示上傳進度。</span><span class="sxs-lookup"><span data-stu-id="5f394-126">For large application packages, you can specify the `--show-progress` option to display the progress of the upload.</span></span>

### <a name="provision-the-application-type"></a><span data-ttu-id="5f394-127">佈建應用程式類型</span><span class="sxs-lookup"><span data-stu-id="5f394-127">Provision the application type</span></span>

<span data-ttu-id="5f394-128">上傳完成時，佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="5f394-128">When the upload is finished, provision the application.</span></span> <span data-ttu-id="5f394-129">若要佈建應用程式，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5f394-129">To provision the application, use the following command:</span></span>

```azurecli
az sf application provision --application-type-build-path app_package_dir
```

<span data-ttu-id="5f394-130">值 `application-type-build-path` 是您上傳應用程式封裝的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="5f394-130">The value for `application-type-build-path` is the name of the directory where you uploaded your application package.</span></span>

### <a name="create-an-application-from-an-application-type"></a><span data-ttu-id="5f394-131">從應用程式類型建立應用程式</span><span class="sxs-lookup"><span data-stu-id="5f394-131">Create an application from an application type</span></span>

<span data-ttu-id="5f394-132">佈建應用程式之後，使用下列命令為應用程式命名並建立應用程式：</span><span class="sxs-lookup"><span data-stu-id="5f394-132">After you provision the application, use the following command to name and create your application:</span></span>

```azurecli
az sf application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

<span data-ttu-id="5f394-133">`app-name` 是您想要用於應用程式執行個體的名稱。</span><span class="sxs-lookup"><span data-stu-id="5f394-133">`app-name` is the name that you want to use for the application instance.</span></span> <span data-ttu-id="5f394-134">您可以從先前佈建的應用程式資訊清單取得額外的參數。</span><span class="sxs-lookup"><span data-stu-id="5f394-134">You can get additional parameters from the previously provisioned application manifest.</span></span>

<span data-ttu-id="5f394-135">應用程式名稱必須以 `fabric:/` 前置詞作為開頭。</span><span class="sxs-lookup"><span data-stu-id="5f394-135">The application name must start with the prefix `fabric:/`.</span></span>

### <a name="create-services-for-the-new-application"></a><span data-ttu-id="5f394-136">為新的應用程式建立服務</span><span class="sxs-lookup"><span data-stu-id="5f394-136">Create services for the new application</span></span>

<span data-ttu-id="5f394-137">建立應用程式之後，從該應用程式建立服務。</span><span class="sxs-lookup"><span data-stu-id="5f394-137">After you have created an application, create services from the application.</span></span> <span data-ttu-id="5f394-138">在下列範例中，我們會從應用程式建立新的無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="5f394-138">In the following example, we create a new stateless service from our application.</span></span> <span data-ttu-id="5f394-139">先前佈建的應用程式封裝之中的服務資訊清單中會定義您可以從應用程式建立的服務。</span><span class="sxs-lookup"><span data-stu-id="5f394-139">The services that you can create from an application are defined in a service manifest in the previously provisioned application package.</span></span>

```azurecli
az sf service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a><span data-ttu-id="5f394-140">確認應用程式部署和健康情況</span><span class="sxs-lookup"><span data-stu-id="5f394-140">Verify application deployment and health</span></span>

<span data-ttu-id="5f394-141">若要確認應用程式和服務是否部署成功，請檢查是否有列出該應用程式和服務：</span><span class="sxs-lookup"><span data-stu-id="5f394-141">To verify that an application and service were successfully deployed, check that the application and service are listed:</span></span>

```azurecli
az sf application list
az sf service list --application-list TestApp
```

<span data-ttu-id="5f394-142">若要確認服務是否狀況良好，請使用類似的命令來取出服務和應用程式的健康情況：</span><span class="sxs-lookup"><span data-stu-id="5f394-142">To verify that the service is healthy, use similar commands to retrieve the health of both the service and the application:</span></span>

```azurecli
az sf application health --application-id TestApp
az sf service health --service-id TestApp/TestSvc
```

<span data-ttu-id="5f394-143">狀況良好的服務和應用程式的 `Ok` 值是 `HealthState`。</span><span class="sxs-lookup"><span data-stu-id="5f394-143">Healthy services and applications have a `HealthState` value of `Ok`.</span></span>

## <a name="remove-an-existing-application"></a><span data-ttu-id="5f394-144">移除現有的應用程式</span><span class="sxs-lookup"><span data-stu-id="5f394-144">Remove an existing application</span></span>

<span data-ttu-id="5f394-145">若要移除應用程式，請完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="5f394-145">To remove an application, complete the following tasks.</span></span>

### <a name="delete-the-application"></a><span data-ttu-id="5f394-146">刪除應用程式</span><span class="sxs-lookup"><span data-stu-id="5f394-146">Delete the application</span></span>

<span data-ttu-id="5f394-147">若要刪除應用程式，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5f394-147">To delete the application, use the following command:</span></span>

```azurecli
az sf application delete --application-id TestEdApp
```

### <a name="unprovision-the-application-type"></a><span data-ttu-id="5f394-148">將應用程式類型解除佈建</span><span class="sxs-lookup"><span data-stu-id="5f394-148">Unprovision the application type</span></span>

<span data-ttu-id="5f394-149">刪除應用程式之後，如果不再需要應用程式，可以解除佈建應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="5f394-149">After you delete the application, you can unprovision the application type if you no longer need it.</span></span> <span data-ttu-id="5f394-150">若要解除佈建應用程式類型，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5f394-150">To unprovision the application type, use the following command:</span></span>

```azurecli
az sf application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

<span data-ttu-id="5f394-151">類型名稱和類型版本必須與先前佈建的應用程式資訊清單中的名稱和版本相符。</span><span class="sxs-lookup"><span data-stu-id="5f394-151">The type name and type version must match the name and version in the previously provisioned application manifest.</span></span>

### <a name="delete-the-application-package"></a><span data-ttu-id="5f394-152">刪除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="5f394-152">Delete the application package</span></span>

<span data-ttu-id="5f394-153">解除佈建應用程式類型之後，如果不再需要應用程式封裝，可以從映像存放區中刪除應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="5f394-153">After you have unprovisioned the application type, you can delete the application package from the image store if you no longer need it.</span></span> <span data-ttu-id="5f394-154">刪除應用程式套件有助於回收磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="5f394-154">Deleting application packages helps reclaim disk space.</span></span> 

<span data-ttu-id="5f394-155">若要從映像存放區中刪除應用程式封裝，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5f394-155">To delete the application package from the image store, use the following command:</span></span>

```azurecli
az sf application package-delete --content-path app_package_dir
```

<span data-ttu-id="5f394-156">`content-path` 必須是您建立應用程式時上傳的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="5f394-156">`content-path` must be the name of the directory that you uploaded when you created the application.</span></span>

## <a name="related-articles"></a><span data-ttu-id="5f394-157">相關文章</span><span class="sxs-lookup"><span data-stu-id="5f394-157">Related articles</span></span>

* [<span data-ttu-id="5f394-158">開始使用 Service Fabric 和 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f394-158">Get started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="5f394-159">開始使用 Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="5f394-159">Get started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
