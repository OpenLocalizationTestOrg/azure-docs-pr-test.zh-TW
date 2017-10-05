---
title: "Azure Service Fabric 應用程式部署 | Microsoft Docs"
description: "使用 FabricClient API 來部署和移除 Service Fabric 中的應用程式。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="6c1a4-103">使用 FabricClient 來部署和移除應用程式</span><span class="sxs-lookup"><span data-stu-id="6c1a4-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6c1a4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c1a4-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="6c1a4-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6c1a4-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="6c1a4-106">FabricClient API</span><span class="sxs-lookup"><span data-stu-id="6c1a4-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="6c1a4-107">[封裝應用程式類型][10]後，即可將它部署至 Azure Service Fabric 叢集中。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="6c1a4-108">部署涉及下列三個步驟：</span><span class="sxs-lookup"><span data-stu-id="6c1a4-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="6c1a4-109">將應用程式封裝上傳至映像存放區</span><span class="sxs-lookup"><span data-stu-id="6c1a4-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="6c1a4-110">註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="6c1a4-110">Register the application type</span></span>
3. <span data-ttu-id="6c1a4-111">建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-111">Create the application instance</span></span>

<span data-ttu-id="6c1a4-112">在應用程式中部署且個體開始在叢集中執行之後，您就可以刪除應用程式執行個體和其應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="6c1a4-113">從叢集完全移除應用程式需要執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="6c1a4-114">移除 (或刪除) 執行中的應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="6c1a4-115">取消註冊不再需要的應用程式類型</span><span class="sxs-lookup"><span data-stu-id="6c1a4-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="6c1a4-116">移除映像存放區中的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-116">Remove the application package from the image store</span></span>

<span data-ttu-id="6c1a4-117">如果您在本機開發叢集上使用 [Visual Studio 部署和偵錯應用程式](service-fabric-publish-app-remote-cluster.md)，則先前所有步驟都會透過 PowerShell 指令碼自動處理。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="6c1a4-118">在應用程式專案的 [指令碼] 資料夾中可找到這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="6c1a4-119">本文提供該指令碼的背景資料，讓您可以在 Visual Studio 之外執行相同的作業。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="6c1a4-120">連接到叢集</span><span class="sxs-lookup"><span data-stu-id="6c1a4-120">Connect to the cluster</span></span>
<span data-ttu-id="6c1a4-121">執行本文中任何程式碼範例之前，請先建立 [FabricClient](/dotnet/api/system.fabric.fabricclient) 執行個體來連線到叢集。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="6c1a4-122">針對連線至本機開發叢集或遠端叢集，或是連線至使用 Azure Active Directory、X509 憑證或 Windows Active Directory 保護的叢集，如需相關的範例，請參閱[連線至安全的叢集](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis)。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="6c1a4-123">若要連線至本機開發叢集，請執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="6c1a4-124">上傳應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-124">Upload the application package</span></span>
<span data-ttu-id="6c1a4-125">假設您在 Visual Studio 中組建並封裝名為 *MyApplication* 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="6c1a4-126">根據預設，ApplicationManifest.xml 中列出的應用程式類型名稱會是 "MyApplicationType"。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="6c1a4-127">應用程式封裝 (其中包含必要的應用程式資訊清單、服務資訊清單和程式碼/組態/資料封裝) 位於 *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="6c1a4-128">上傳應用程式套件會將它放在內部 Service Fabric 元件可以存取的位置。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="6c1a4-129">Service Fabric 會在應用程式套件的註冊期間驗證應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="6c1a4-130">不過，如果您想要在本機確認應用程式套件 (亦即，在上傳前)，使用 [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="6c1a4-131">[Copy-ServiceFabricApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 會將應用程式套件上傳至叢集映像存放區。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="6c1a4-132">如果是大型的應用程式套件且/或具有許多檔案，您可以[將它壓縮](service-fabric-package-apps.md#compress-a-package)，並使用 PowerShell 將它複製到 ImageStore。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="6c1a4-133">壓縮會減少檔案大小和數目。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="6c1a4-134">請參閱[了解映像存放區連接字串](service-fabric-image-store-connection-string.md)，以取得有關映像存放區和映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="6c1a4-135">註冊應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-135">Register the application package</span></span>
<span data-ttu-id="6c1a4-136">註冊應用程式套件時，應用程式類型和應用程式資訊清單中宣告的版本可供使用。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="6c1a4-137">系統會讀取在上一個步驟上傳的套件，請確認套件、處理套件內容，然後將處理過的套件複製至內部系統位置。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="6c1a4-138">[ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 會註冊叢集中的應用程式類型，並使其可供部署。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="6c1a4-139">[GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API 會提供所有註冊成功之應用程式類型的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="6c1a4-140">您可以使用此 API 來判斷何時會完成註冊。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="6c1a4-141">建立應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-141">Create an application instance</span></span>
<span data-ttu-id="6c1a4-142">您可以使用 [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API，從任何已成功註冊的應用程式類型，將應用程式具現化。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="6c1a4-143">每個應用程式名稱的開頭必須為 "fabric:" 配置，而且必須是 (叢集內) 每個應用程式執行個體的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="6c1a4-144">如果已在目標應用程式類型的應用程式資訊清單中定義預設服務，也會一併建立這些服務。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="6c1a4-145">多個應用程式執行個體可以針對任何指定的已註冊應用程式類型版本來建立。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="6c1a4-146">每個應用程式執行個體將在隔離狀態下執行，包含本身的工作目錄和程序集。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="6c1a4-147">若要查看哪些具名的應用程式和服務正在叢集中執行，請執行 [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) 和 [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) API。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="6c1a4-148">建立服務執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-148">Create a service instance</span></span>
<span data-ttu-id="6c1a4-149">您可以使用 [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API，從服務類型將服務具現化。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="6c1a4-150">如果服務宣告為應用程式資訊清單中的預設服務，服務會在應用程式具現化時進行具現化。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="6c1a4-151">對已具現化的服務呼叫 [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API，會傳回 FabricException 類型的例外狀況，其中包含值為 FabricErrorCode.ServiceAlreadyExists 的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="6c1a4-152">移除服務執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-152">Remove a service instance</span></span>
<span data-ttu-id="6c1a4-153">當不再需要服務執行個體時，可以呼叫 [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API，將它從執行的應用程式執行個體中移除。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="6c1a4-154">此作業無法回復，且服務狀態無法復原。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="6c1a4-155">移除應用程式執行個體</span><span class="sxs-lookup"><span data-stu-id="6c1a4-155">Remove an application instance</span></span>
<span data-ttu-id="6c1a4-156">當不再需要應用程式執行個體時，您可以使用 [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API，依名稱將它永久移除。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="6c1a4-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) 會將屬於應用程式的所有服務自動移除，以及將所有服務狀態永久移除。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="6c1a4-158">此作業無法回復，且應用程式狀態無法復原。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="6c1a4-159">取消註冊應用程式類型</span><span class="sxs-lookup"><span data-stu-id="6c1a4-159">Unregister an application type</span></span>
<span data-ttu-id="6c1a4-160">不再需要特定版本的應用程式類型時，您應該使用 [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API 將該特定版本的應用程式類型取消註冊。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="6c1a4-161">取消註冊未使用的應用程式類型版本會釋放映像存放區已使用的儲存空間。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="6c1a4-162">只要沒有針對某個版本的應用程式類型進行具現化，且沒有擱置中的應用程式升級參考該版本的應用程式類型，便可取消註冊該版本的應用程式類型。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="6c1a4-163">從映像存放區移除應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-163">Remove an application package from the image store</span></span>
<span data-ttu-id="6c1a4-164">當不再需要應用程式套件時，您可以使用 [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API，從映像存放區將它刪除，以釋放系統資源。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6c1a4-165">疑難排解</span><span class="sxs-lookup"><span data-stu-id="6c1a4-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="6c1a4-166">Copy-ServiceFabricApplicationPackage 要求 ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="6c1a4-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="6c1a4-167">Service Fabric SDK 環境應已正確設定預設值。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="6c1a4-168">但若有需要，所有命令的 ImageStoreConnectionString都應符合 Service Fabric 叢集正在使用的值。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="6c1a4-169">您可以在使用 [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) 和 Get-ImageStoreConnectionStringFromClusterManifest 命令擷取的叢集資訊清單 ImageStoreConnectionString 中找到此值：</span><span class="sxs-lookup"><span data-stu-id="6c1a4-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="6c1a4-170">**Get ImageStoreConnectionStringFromClusterManifest** Cmdlet 是 Service Fabric SDK PowerShell 模組的一部分，可用來取得映像存放區連接字串。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="6c1a4-171">若要匯入 SDK 模組，請執行︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="6c1a4-172">會在叢集資訊清單中找到 ImageStoreConnectionString：</span><span class="sxs-lookup"><span data-stu-id="6c1a4-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="6c1a4-173">請參閱[了解映像存放區連接字串](service-fabric-image-store-connection-string.md)，以取得有關映像存放區和映像存放區連接字串的補充資訊。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="6c1a4-174">部署大型應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-174">Deploy large application package</span></span>
<span data-ttu-id="6c1a4-175">問題︰大型應用程式套件 (GB 的順序) 的 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API 逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="6c1a4-176">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-176">Try:</span></span>
- <span data-ttu-id="6c1a4-177">使用 `timeout` 參數指定 [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) 方法的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="6c1a4-178">此逾時預設為 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="6c1a4-179">檢查來源電腦與叢集之間的網路連線。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="6c1a4-180">如果連線速度變慢，請考慮使用更佳網路連線的電腦。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="6c1a4-181">如果用戶端電腦與叢集在不同的區域中，請考慮使用與叢集接近或相同區域中的用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="6c1a4-182">請檢查是否到達外部節流。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="6c1a4-183">例如，當映像存放區設定為使用 Azure 儲存體時，上傳可能受到節流控制。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="6c1a4-184">問題︰上傳套件順利完成，但 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="6c1a4-185">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-185">Try:</span></span>
- <span data-ttu-id="6c1a4-186">複製到映像存放區之前[壓縮封裝](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="6c1a4-187">壓縮會減少檔案的大小和數目，而後者則可減少資料傳輸量和 Service Fabric 必須執行的工作。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="6c1a4-188">上傳作業可能會變慢 (尤其是如果您包含壓縮時間)，但註冊和取消註冊應用程式類型會比較快。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="6c1a4-189">使用 `timeout` 參數為 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API 指定較大的逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="6c1a4-190">部署具有很多檔案的應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="6c1a4-190">Deploy application package with many files</span></span>
<span data-ttu-id="6c1a4-191">問題︰具有很多檔案的應用程式套件 (以千計的順序) [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) 的逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="6c1a4-192">請嘗試︰</span><span class="sxs-lookup"><span data-stu-id="6c1a4-192">Try:</span></span>
- <span data-ttu-id="6c1a4-193">複製到映像存放區之前[壓縮封裝](service-fabric-package-apps.md#compress-a-package)。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="6c1a4-194">壓縮會減少檔案的數目。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="6c1a4-195">使用 `timeout` 參數指定 [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) 的較大逾時。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="6c1a4-196">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="6c1a4-196">Code example</span></span>
<span data-ttu-id="6c1a4-197">下列範例會將應用程式套件複製到映像存放區、佈建應用程式類型、建立應用程式執行個體、建立服務執行個體、移除應用程式執行個體、取消佈建應用程式類型，以及將應用程式套件從映像存放區中刪除。</span><span class="sxs-lookup"><span data-stu-id="6c1a4-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="6c1a4-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c1a4-198">Next steps</span></span>
[<span data-ttu-id="6c1a4-199">Service Fabric 應用程式升級</span><span class="sxs-lookup"><span data-stu-id="6c1a4-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="6c1a4-200">Service Fabric 健康狀態簡介</span><span class="sxs-lookup"><span data-stu-id="6c1a4-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="6c1a4-201">診斷和疑難排解 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="6c1a4-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="6c1a4-202">在 Service Fabric 中模型化應用程式</span><span class="sxs-lookup"><span data-stu-id="6c1a4-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
