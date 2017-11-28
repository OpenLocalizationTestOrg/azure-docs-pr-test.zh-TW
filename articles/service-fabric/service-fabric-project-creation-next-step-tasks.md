---
title: "Service Fabric 專案建立後續步驟 |Microsoft Docs"
description: "本文包含一組用於 Service Fabric 的核心開發工作連結"
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
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="061ef-103">您的 Service Fabric 應用程式和後續步驟</span><span class="sxs-lookup"><span data-stu-id="061ef-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="061ef-104">您的 Azure Service Fabric 應用程式已經建立。</span><span class="sxs-lookup"><span data-stu-id="061ef-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="061ef-105">本文說明您專案的建立方式和一些潛在後續步驟。</span><span class="sxs-lookup"><span data-stu-id="061ef-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="061ef-106">您的應用程式</span><span class="sxs-lookup"><span data-stu-id="061ef-106">Your application</span></span>
<span data-ttu-id="061ef-107">每個新應用程式都包含一個應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="061ef-107">Every new application includes an application project.</span></span> <span data-ttu-id="061ef-108">視所選擇的服務類型而定，可能會有一個或兩個額外的專案。</span><span class="sxs-lookup"><span data-stu-id="061ef-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="061ef-109">應用程式專案</span><span class="sxs-lookup"><span data-stu-id="061ef-109">The application project</span></span>
<span data-ttu-id="061ef-110">應用程式專案包含：</span><span class="sxs-lookup"><span data-stu-id="061ef-110">The application project consists of:</span></span>

* <span data-ttu-id="061ef-111">一組對構成應用程式之服務的參考。</span><span class="sxs-lookup"><span data-stu-id="061ef-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="061ef-112">三個發行設定檔 (1-Node Local、5-Node Local、Cloud)，可用來維護喜好設定，以搭配不同的環境使用，例如叢集端點的相關喜好設定，以及是否預設要執行升級部署。</span><span class="sxs-lookup"><span data-stu-id="061ef-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="061ef-113">三個應用程式參數檔案 (同上)，可用來維護環境特定應用程式組態，例如為服務建立之分割區的數目。</span><span class="sxs-lookup"><span data-stu-id="061ef-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="061ef-114">部署指令碼，可用來從命令列部署您的應用程式，或透過自動化連續整合和部署管線中部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="061ef-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="061ef-115">應用程式資訊清單，描述應用程式。</span><span class="sxs-lookup"><span data-stu-id="061ef-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="061ef-116">您可以在 ApplicationPackageRoot 資料夾下方找到資訊清單。</span><span class="sxs-lookup"><span data-stu-id="061ef-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="061ef-117">無狀態服務</span><span class="sxs-lookup"><span data-stu-id="061ef-117">Stateless service</span></span>
<span data-ttu-id="061ef-118">當您加入一個新的無狀態服務時，Visual Studio 會將一個服務專案 (包含來自 `StatelessService`的類型) 加入至您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="061ef-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="061ef-119">此服務會使計數器中的區域變數遞增。</span><span class="sxs-lookup"><span data-stu-id="061ef-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="061ef-120">具狀態服務</span><span class="sxs-lookup"><span data-stu-id="061ef-120">Stateful service</span></span>
<span data-ttu-id="061ef-121">當您加入一個新的具狀態服務時，Visual Studio 會將一個服務專案 (包含來自 `StatefulService`的類型) 加入至您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="061ef-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="061ef-122">此服務會將 `RunAsync` 方法中的計數器遞增，並將結果儲存在 `ReliableDictionary` 中。</span><span class="sxs-lookup"><span data-stu-id="061ef-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="061ef-123">動作項目服務</span><span class="sxs-lookup"><span data-stu-id="061ef-123">Actor service</span></span>
<span data-ttu-id="061ef-124">當您加入一個新的 Reliable Actor 時，Visual Studio 會將兩個專案加入至您的解決方案：動作項目專案和介面專案。</span><span class="sxs-lookup"><span data-stu-id="061ef-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="061ef-125">動作項目專案提供了一些方法，以便設定和取得動作項目的狀態中可靠地保存的計數器值。</span><span class="sxs-lookup"><span data-stu-id="061ef-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="061ef-126">介面專案提供了其他服務可用來叫用動作項目的介面。</span><span class="sxs-lookup"><span data-stu-id="061ef-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="061ef-127">無狀態 Web API</span><span class="sxs-lookup"><span data-stu-id="061ef-127">Stateless Web API</span></span>
<span data-ttu-id="061ef-128">無狀態 Web API 專案會提供基本一項 Web 服務，您可用來對外部用戶端開放您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="061ef-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="061ef-129">如需有關如何建構專案的詳細資訊，請參閱 [Service Fabric Web API 服務與 OWIN 自我裝載](service-fabric-reliable-services-communication-webapi.md)。</span><span class="sxs-lookup"><span data-stu-id="061ef-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="061ef-130">ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="061ef-130">ASP.NET core</span></span>
<span data-ttu-id="061ef-131">Service Fabric SDK 提供 ASP.NET Core 範本的相同集合，適用於獨立 ASP.NET Core 專案︰空的、[Web API][aspnet-webapi] 和 [Web 應用程式][aspnet-webapp]。</span><span class="sxs-lookup"><span data-stu-id="061ef-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="061ef-132">客體可執行檔和客體容器</span><span class="sxs-lookup"><span data-stu-id="061ef-132">Guest executables and guest containers</span></span>

<span data-ttu-id="061ef-133">Service Fabric「客體」這個服務並非由平台的程式設計模型所建立。</span><span class="sxs-lookup"><span data-stu-id="061ef-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="061ef-134">您可以[直接在應用程式套件中](service-fabric-deploy-existing-app.md)或[透過容器映像](service-fabric-deploy-container.md)，將客體的二進位檔案進行封裝。</span><span class="sxs-lookup"><span data-stu-id="061ef-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="061ef-135">在這兩種情況下，Visual Studio 會在應用程式專案的 **ApplicationPackageRoot** 資料夾中建立必要的成品。</span><span class="sxs-lookup"><span data-stu-id="061ef-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="061ef-136">Visual Studio 不會建立新的服務專案，因為程式碼已經存在於其他地方。</span><span class="sxs-lookup"><span data-stu-id="061ef-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="061ef-137">如果您想要同時管理客體專案與 Service Fabric 應用程式專案，您可以將它們新增至相同的 Visual Studio 解決方案。</span><span class="sxs-lookup"><span data-stu-id="061ef-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="061ef-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="061ef-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="061ef-139">建立 Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="061ef-139">Create an Azure cluster</span></span>
<span data-ttu-id="061ef-140">Service Fabric SDK 提供一個用於開發和測試的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="061ef-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="061ef-141">若要在 Azure 中建立叢集，請參閱[從 Azure 入口網站設定 Service Fabric 叢集][create-cluster-in-portal]。</span><span class="sxs-lookup"><span data-stu-id="061ef-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="061ef-142">將應用程式發行至 Azure</span><span class="sxs-lookup"><span data-stu-id="061ef-142">Publish your application to Azure</span></span>
<span data-ttu-id="061ef-143">您可以直接從 Visual Studio 將應用程式發行至 Azure 叢集。</span><span class="sxs-lookup"><span data-stu-id="061ef-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="061ef-144">若要瞭解做法，請參閱[將應用程式發佈至 Azure][publish-app-to-azure]。</span><span class="sxs-lookup"><span data-stu-id="061ef-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="061ef-145">使用 Service Fabric 總管將叢集視覺化</span><span class="sxs-lookup"><span data-stu-id="061ef-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="061ef-146">「Service Fabric 總管」提供一個將叢集 (包括已部署的應用程式和實體配置) 視覺化的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="061ef-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="061ef-147">若要深入了解，請參閱[使用 Service Fabric Explorer 將叢集視覺化][visualize-with-sfx]。</span><span class="sxs-lookup"><span data-stu-id="061ef-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="061ef-148">進行服務版本設定和升級</span><span class="sxs-lookup"><span data-stu-id="061ef-148">Version and upgrade your services</span></span>
<span data-ttu-id="061ef-149">Service Fabric 可讓您為應用程式中的獨立服務進行獨立的版本設定和升級。</span><span class="sxs-lookup"><span data-stu-id="061ef-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="061ef-150">若要深入了解，請參閱[進行服務版本設定和升級][app-upgrade-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="061ef-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="061ef-151">使用 Visual Studio Team Services 設定持續整合</span><span class="sxs-lookup"><span data-stu-id="061ef-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="061ef-152">若要深入了解如何為 Service Fabric 應用程式設定持續整合程序，請參閱[使用 Visual Studio Team Services 設定持續整合][ci-with-vso]。</span><span class="sxs-lookup"><span data-stu-id="061ef-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
