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
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="67c2b-103">您的 Service Fabric 應用程式和後續步驟</span><span class="sxs-lookup"><span data-stu-id="67c2b-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="67c2b-104">您的 Azure Service Fabric 應用程式已經建立。</span><span class="sxs-lookup"><span data-stu-id="67c2b-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="67c2b-105">本文說明 hello 結構的一些可能的後續步驟和您的專案。</span><span class="sxs-lookup"><span data-stu-id="67c2b-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="67c2b-106">您的應用程式</span><span class="sxs-lookup"><span data-stu-id="67c2b-106">Your application</span></span>
<span data-ttu-id="67c2b-107">每個新應用程式都包含一個應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="67c2b-107">Every new application includes an application project.</span></span> <span data-ttu-id="67c2b-108">可能有一或兩個其他專案中的，視選擇服務 hello 類型而定。</span><span class="sxs-lookup"><span data-stu-id="67c2b-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="67c2b-109">hello 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="67c2b-109">hello application project</span></span>
<span data-ttu-id="67c2b-110">hello 應用程式專案所組成：</span><span class="sxs-lookup"><span data-stu-id="67c2b-110">hello application project consists of:</span></span>

* <span data-ttu-id="67c2b-111">一組構成應用程式的參考 toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="67c2b-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="67c2b-112">三個發行，您可以使用 toomaintain 喜好設定，使用不同的環境-例如喜好設定相關的 tooa 叢集端點，以及是否 tooperform 升級部署預設的設定檔 （1 節點本機、 5 節點本機和雲端）。</span><span class="sxs-lookup"><span data-stu-id="67c2b-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="67c2b-113">三個應用程式參數檔案 （同上），您可以使用 toomaintain 環境特定應用程式設定，例如服務的資料分割 toocreate 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="67c2b-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="67c2b-114">部署指令碼，您可以使用 toodeploy 應用程式從 hello 命令列，或做為自動化的連續整合及部署管線的一部分。</span><span class="sxs-lookup"><span data-stu-id="67c2b-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="67c2b-115">hello 應用程式資訊清單，其中描述 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="67c2b-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="67c2b-116">您可以在 hello ApplicationPackageRoot 資料夾下找到 hello 資訊清單。</span><span class="sxs-lookup"><span data-stu-id="67c2b-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="67c2b-117">無狀態服務</span><span class="sxs-lookup"><span data-stu-id="67c2b-117">Stateless service</span></span>
<span data-ttu-id="67c2b-118">當您新增新的無狀態服務時，Visual Studio 會加入包含類型，從繼承而來的服務專案 tooyour 解決方案`StatelessService`。</span><span class="sxs-lookup"><span data-stu-id="67c2b-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="67c2b-119">hello 服務遞增計數器中的區域變數。</span><span class="sxs-lookup"><span data-stu-id="67c2b-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="67c2b-120">具狀態服務</span><span class="sxs-lookup"><span data-stu-id="67c2b-120">Stateful service</span></span>
<span data-ttu-id="67c2b-121">當您新增新的可設定狀態服務時，Visual Studio 會加入包含類型，從繼承而來的服務專案 tooyour 解決方案`StatefulService`。</span><span class="sxs-lookup"><span data-stu-id="67c2b-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="67c2b-122">hello 服務遞增計數器中的其`RunAsync`方法和存放區中的 hello 結果`ReliableDictionary`。</span><span class="sxs-lookup"><span data-stu-id="67c2b-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="67c2b-123">動作項目服務</span><span class="sxs-lookup"><span data-stu-id="67c2b-123">Actor service</span></span>
<span data-ttu-id="67c2b-124">當您新增新的可靠動作項目時，Visual Studio 會加入兩個專案 tooyour 方案： 執行者專案和介面的專案。</span><span class="sxs-lookup"><span data-stu-id="67c2b-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="67c2b-125">hello 執行者專案提供方法來設定和取得 hello 計數器的值可靠地保存在 hello 動作項目的狀態。</span><span class="sxs-lookup"><span data-stu-id="67c2b-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="67c2b-126">hello 介面專案提供介面的其他服務可以使用 tooinvoke hello 動作項目。</span><span class="sxs-lookup"><span data-stu-id="67c2b-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="67c2b-127">無狀態 Web API</span><span class="sxs-lookup"><span data-stu-id="67c2b-127">Stateless Web API</span></span>
<span data-ttu-id="67c2b-128">hello 無狀態 Web API 專案提供基本 web 服務，您可以使用 tooopen tooexternal 用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="67c2b-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="67c2b-129">如需 hello 專案的結構化的詳細資訊，請參閱[與 OWIN 自我主控的服務網狀架構 Web API 服務](service-fabric-reliable-services-communication-webapi.md)。</span><span class="sxs-lookup"><span data-stu-id="67c2b-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="67c2b-130">ASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="67c2b-130">ASP.NET core</span></span>
<span data-ttu-id="67c2b-131">hello Service Fabric SDK 提供的相同設定的 ASP.NET Core 範本可供獨立 ASP.NET Core 專案的 hello： 空的[Web API][aspnet-webapi]，和[Web 應用程式][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="67c2b-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="67c2b-132">客體可執行檔和客體容器</span><span class="sxs-lookup"><span data-stu-id="67c2b-132">Guest executables and guest containers</span></span>

<span data-ttu-id="67c2b-133">服務網狀架構 'guest' 是不以 hello 平台的程式設計模型所建立的服務。</span><span class="sxs-lookup"><span data-stu-id="67c2b-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="67c2b-134">您可以將封裝 hello 二進位檔的來賓是[hello 應用程式封裝中直接](service-fabric-deploy-existing-app.md)或[容器映像透過](service-fabric-deploy-container.md)。</span><span class="sxs-lookup"><span data-stu-id="67c2b-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="67c2b-135">在這兩種情況下，Visual Studio 會建立 hello hello 中的必要成品**ApplicationPackageRoot** hello 應用程式專案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="67c2b-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="67c2b-136">Visual Studio 不會建立新的服務專案，因為 hello 代碼已經存在其他位置。</span><span class="sxs-lookup"><span data-stu-id="67c2b-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="67c2b-137">如果您想要的 toomanage 對來賓專案一起 hello Service Fabric 應用程式專案，您可以將它們加入 toohello 相同的 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="67c2b-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67c2b-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67c2b-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="67c2b-139">建立 Azure 叢集</span><span class="sxs-lookup"><span data-stu-id="67c2b-139">Create an Azure cluster</span></span>
<span data-ttu-id="67c2b-140">hello Service Fabric SDK 提供開發和測試的本機叢集。</span><span class="sxs-lookup"><span data-stu-id="67c2b-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="67c2b-141">toocreate 叢集，以在 Azure 中，請參閱[從 hello Azure 入口網站設定 Service Fabric 叢集][create-cluster-in-portal]。</span><span class="sxs-lookup"><span data-stu-id="67c2b-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="67c2b-142">發行應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="67c2b-142">Publish your application tooAzure</span></span>
<span data-ttu-id="67c2b-143">您可以發佈您的應用程式，直接從 Visual Studio tooan Azure 的叢集。</span><span class="sxs-lookup"><span data-stu-id="67c2b-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="67c2b-144">toolearn 作法，請參閱[發行應用程式 tooAzure][publish-app-to-azure]。</span><span class="sxs-lookup"><span data-stu-id="67c2b-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="67c2b-145">使用 Service Fabric 總管 toovisualize 您的叢集</span><span class="sxs-lookup"><span data-stu-id="67c2b-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="67c2b-146">Service Fabric 總管提供簡單的方式 toovisualize 您的叢集，包括部署的應用程式和實體配置。</span><span class="sxs-lookup"><span data-stu-id="67c2b-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="67c2b-147">詳細資訊，請參閱 toolearn[視覺化您的叢集，利用 Service Fabric 總管][visualize-with-sfx]。</span><span class="sxs-lookup"><span data-stu-id="67c2b-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="67c2b-148">進行服務版本設定和升級</span><span class="sxs-lookup"><span data-stu-id="67c2b-148">Version and upgrade your services</span></span>
<span data-ttu-id="67c2b-149">Service Fabric 可讓您為應用程式中的獨立服務進行獨立的版本設定和升級。</span><span class="sxs-lookup"><span data-stu-id="67c2b-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="67c2b-150">詳細資訊，請參閱 toolearn[版本控制和升級您的服務][app-upgrade-tutorial]。</span><span class="sxs-lookup"><span data-stu-id="67c2b-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="67c2b-151">使用 Visual Studio Team Services 設定持續整合</span><span class="sxs-lookup"><span data-stu-id="67c2b-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="67c2b-152">toolearn 如何設定連續整合程序 Service Fabric 應用程式，請參閱[設定與 Visual Studio Team Services 的連續整合][ci-with-vso]。</span><span class="sxs-lookup"><span data-stu-id="67c2b-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
