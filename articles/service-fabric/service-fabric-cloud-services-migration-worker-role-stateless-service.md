---
title: "Azure 雲端服務應用程式 toomicroservices aaaConvert |Microsoft 文件"
description: "本指南會比較雲端服務 Web 和背景工作角色和服務網狀架構無狀態服務 toohelp 從雲端服務 tooService 網狀架構的移轉。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a><span data-ttu-id="0b598-103">引導 tooconverting Web 和背景工作角色 tooService Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="0b598-103">Guide tooconverting Web and Worker Roles tooService Fabric stateless services</span></span>
<span data-ttu-id="0b598-104">本文說明如何 toomigrate 您雲端服務 Web 和背景工作角色 tooService Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="0b598-104">This article describes how toomigrate your Cloud Services Web and Worker Roles tooService Fabric stateless services.</span></span> <span data-ttu-id="0b598-105">這是應用程式的整體架構即將 toostay 大致 hello 相同 hello 簡單的移轉路徑從雲端服務 tooService 網狀架構。</span><span class="sxs-lookup"><span data-stu-id="0b598-105">This is hello simplest migration path from Cloud Services tooService Fabric for applications whose overall architecture is going toostay roughly hello same.</span></span>

## <a name="cloud-service-project-tooservice-fabric-application-project"></a><span data-ttu-id="0b598-106">雲端服務專案 tooService 網狀架構應用程式專案</span><span class="sxs-lookup"><span data-stu-id="0b598-106">Cloud Service project tooService Fabric application project</span></span>
 <span data-ttu-id="0b598-107">雲端服務專案和 Service Fabric 應用程式專案有類似的結構和兩個代表 hello 部署單位，您的應用程式-也就是說，它們每個會定義所部署的 toorun hello 完整封裝您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b598-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent hello deployment unit for your application - that is, they each define hello complete package that is deployed toorun your application.</span></span> <span data-ttu-id="0b598-108">雲端服務專案包含一個或多個 Web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="0b598-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="0b598-109">同樣地，Service Fabric 應用程式專案也包含一個或多個服務。</span><span class="sxs-lookup"><span data-stu-id="0b598-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="0b598-110">hello 的差異是 hello 雲端服務專案 couples hello 與 VM 部署的應用程式部署，因此會包含 VM 組態設定，而 hello Service Fabric 應用程式專案只會定義將部署的應用程式Service Fabric 叢集中的現有 Vm tooa 組。</span><span class="sxs-lookup"><span data-stu-id="0b598-110">hello difference is that hello Cloud Service project couples hello application deployment with a VM deployment and thus contains VM configuration settings in it, whereas hello Service Fabric Application project only defines an application that will be deployed tooa set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="0b598-111">一旦透過 Resource Manager 範本或透過 hello Azure 入口網站和應用程式可以是多個 Service Fabric 部署 tooit，只會部署 hello Service Fabric 叢集本身。</span><span class="sxs-lookup"><span data-stu-id="0b598-111">hello Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through hello Azure portal, and multiple Service Fabric applications can be deployed tooit.</span></span>

![Service Fabric 和雲端服務專案的比較][3]

## <a name="worker-role-toostateless-service"></a><span data-ttu-id="0b598-113">背景工作角色 toostateless 服務</span><span class="sxs-lookup"><span data-stu-id="0b598-113">Worker Role toostateless service</span></span>
<span data-ttu-id="0b598-114">就概念而言，背景工作角色代表無狀態工作負載，這表示是相同的 hello 工作負載的每個執行個體，並要求可以在任何時間是路由的 tooany 執行個體。</span><span class="sxs-lookup"><span data-stu-id="0b598-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of hello workload is identical and requests can be routed tooany instance at any time.</span></span> <span data-ttu-id="0b598-115">每個執行個體不是預期的 tooremember hello 前一個要求。</span><span class="sxs-lookup"><span data-stu-id="0b598-115">Each instance is not expected tooremember hello previous request.</span></span> <span data-ttu-id="0b598-116">狀態 hello 負載運作的外部狀態存放區，例如 Azure 資料表儲存體或 Azure 文件 DB 上管理。</span><span class="sxs-lookup"><span data-stu-id="0b598-116">State that hello workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="0b598-117">在 Service Fabric 中，這類工作負載是以無狀態服務來代表。</span><span class="sxs-lookup"><span data-stu-id="0b598-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="0b598-118">最簡單方法 toomigrating hello 背景工作角色 tooService 網狀架構都可以做到轉換背景工作角色程式碼 tooa 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="0b598-118">hello simplest approach toomigrating a Worker Role tooService Fabric can be done by converting Worker Role code tooa Stateless Service.</span></span>

![背景工作角色 tooStateless 服務][4]

## <a name="web-role-toostateless-service"></a><span data-ttu-id="0b598-120">Web 角色 toostateless 服務</span><span class="sxs-lookup"><span data-stu-id="0b598-120">Web Role toostateless service</span></span>
<span data-ttu-id="0b598-121">類似 tooWorker 角色，Web 角色也代表無狀態工作負載，因此在概念上太可以對應的 tooa Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="0b598-121">Similar tooWorker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped tooa Service Fabric stateless service.</span></span> <span data-ttu-id="0b598-122">不過，和 Web 角色不同的是，Service Fabric 不支援 IIS。</span><span class="sxs-lookup"><span data-stu-id="0b598-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="0b598-123">toomigrate 從 Web 角色 tooa 無狀態服務的 web 應用程式需要第一個移動 tooa web 架構可以自我裝載，不需依賴 IIS 或 System.Web，例如 ASP.NET Core 1。</span><span class="sxs-lookup"><span data-stu-id="0b598-123">toomigrate a web application from a Web Role tooa stateless service requires first moving tooa web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="0b598-124">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="0b598-124">**Application**</span></span> | <span data-ttu-id="0b598-125">**支援**</span><span class="sxs-lookup"><span data-stu-id="0b598-125">**Supported**</span></span> | <span data-ttu-id="0b598-126">**移轉路徑**</span><span class="sxs-lookup"><span data-stu-id="0b598-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b598-127">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="0b598-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="0b598-128">否</span><span class="sxs-lookup"><span data-stu-id="0b598-128">No</span></span> |<span data-ttu-id="0b598-129">轉換 tooASP.NET 核心 1 MVC</span><span class="sxs-lookup"><span data-stu-id="0b598-129">Convert tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="0b598-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="0b598-130">ASP.NET MVC</span></span> |<span data-ttu-id="0b598-131">移轉</span><span class="sxs-lookup"><span data-stu-id="0b598-131">With Migration</span></span> |<span data-ttu-id="0b598-132">升級 tooASP.NET 核心 1 MVC</span><span class="sxs-lookup"><span data-stu-id="0b598-132">Upgrade tooASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="0b598-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="0b598-133">ASP.NET Web API</span></span> |<span data-ttu-id="0b598-134">移轉</span><span class="sxs-lookup"><span data-stu-id="0b598-134">With Migration</span></span> |<span data-ttu-id="0b598-135">使用自我裝載的伺服器或 ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="0b598-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="0b598-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="0b598-136">ASP.NET Core 1</span></span> |<span data-ttu-id="0b598-137">是</span><span class="sxs-lookup"><span data-stu-id="0b598-137">Yes</span></span> |<span data-ttu-id="0b598-138">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="0b598-139">進入點 API 和生命週期</span><span class="sxs-lookup"><span data-stu-id="0b598-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="0b598-140">背景工作角色和 Service Fabric 服務 API 提供類似的進入點：</span><span class="sxs-lookup"><span data-stu-id="0b598-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="0b598-141">**進入點**</span><span class="sxs-lookup"><span data-stu-id="0b598-141">**Entry Point**</span></span> | <span data-ttu-id="0b598-142">**背景工作角色**</span><span class="sxs-lookup"><span data-stu-id="0b598-142">**Worker Role**</span></span> | <span data-ttu-id="0b598-143">**Service Fabric 服務**</span><span class="sxs-lookup"><span data-stu-id="0b598-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b598-144">Processing</span><span class="sxs-lookup"><span data-stu-id="0b598-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="0b598-145">VM 啟動</span><span class="sxs-lookup"><span data-stu-id="0b598-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="0b598-146">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-146">N/A</span></span> |
| <span data-ttu-id="0b598-147">VM 停止</span><span class="sxs-lookup"><span data-stu-id="0b598-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="0b598-148">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-148">N/A</span></span> |
| <span data-ttu-id="0b598-149">開啟接聽程式以接收用戶端要求</span><span class="sxs-lookup"><span data-stu-id="0b598-149">Open listener for client requests</span></span> |<span data-ttu-id="0b598-150">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-150">N/A</span></span> |<ul><li> <span data-ttu-id="0b598-151">`CreateServiceInstanceListener()` (針對無狀態)</span><span class="sxs-lookup"><span data-stu-id="0b598-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="0b598-152">`CreateServiceReplicaListener()` (針對具狀態)</span><span class="sxs-lookup"><span data-stu-id="0b598-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="0b598-153">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="0b598-153">Worker Role</span></span>
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="0b598-154">Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="0b598-154">Service Fabric Stateless Service</span></span>
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

<span data-ttu-id="0b598-155">兩者都有主要的 [執行] 覆寫 toobegin 處理。</span><span class="sxs-lookup"><span data-stu-id="0b598-155">Both have a primary "Run" override in which toobegin processing.</span></span> <span data-ttu-id="0b598-156">Service Fabric 服務將 `Run`、`Start` 和 `Stop` 結合為單一進入點 `RunAsync`。</span><span class="sxs-lookup"><span data-stu-id="0b598-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="0b598-157">您的服務應該開始運作`RunAsync`正常啟動，且應該停止運作時 hello`RunAsync`方法的 CancellationToken 發出信號。</span><span class="sxs-lookup"><span data-stu-id="0b598-157">Your service should begin working when `RunAsync` starts, and should stop working when hello `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="0b598-158">有幾項 hello 生命週期和背景工作角色和服務網狀架構服務的存留期之間的主要差異：</span><span class="sxs-lookup"><span data-stu-id="0b598-158">There are several key differences between hello lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="0b598-159">**生命週期：** hello 最大的差異是背景工作角色是 VM，因此其生命週期是繫結的 toohello VM，包括何時 hello VM 啟動和停止事件。</span><span class="sxs-lookup"><span data-stu-id="0b598-159">**Lifecycle:** hello biggest difference is that a Worker Role is a VM and so its lifecycle is tied toohello VM, which includes events for when hello VM starts and stops.</span></span> <span data-ttu-id="0b598-160">Service Fabric 服務具有是分開 hello VM 生命週期，所以它不包含事件的 VM 或電腦啟動和停止，hello 的主控件時，因為它們不相關的生命週期。</span><span class="sxs-lookup"><span data-stu-id="0b598-160">A Service Fabric service has a lifecycle that is separate from hello VM lifecycle, so it does not include events for when hello host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="0b598-161">**存留期：**的背景工作角色執行個體就會回收如果 hello`Run`方法即會結束。</span><span class="sxs-lookup"><span data-stu-id="0b598-161">**Lifetime:** A Worker Role instance will recycle if hello `Run` method exits.</span></span> <span data-ttu-id="0b598-162">hello `RunAsync` Service Fabric 服務中的方法不過可以執行 toocompletion 而且 hello 服務執行個體將保持註冊。</span><span class="sxs-lookup"><span data-stu-id="0b598-162">hello `RunAsync` method in a Service Fabric service however can run toocompletion and hello service instance will stay up.</span></span> 

<span data-ttu-id="0b598-163">Service Fabric 為接聽用戶端要求的服務提供選擇性的通訊設定進入點。</span><span class="sxs-lookup"><span data-stu-id="0b598-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="0b598-164">Hello RunAsync 和通訊的進入點是在 Service Fabric 服務-服務可能會選擇 tooonly 接聽 tooclient 要求，或只處理迴圈，及 / 或執行-這就是為什麼 hello RunAsync 方法允許 tooexit 不含選擇性覆寫重新啟動 hello 服務執行個體，因為它可能會繼續 toolisten 用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="0b598-164">Both hello RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose tooonly listen tooclient requests, or only run a processing loop, or both - which is why hello RunAsync method is allowed tooexit without restarting hello service instance, because it may continue toolisten for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="0b598-165">應用程式 API 和環境</span><span class="sxs-lookup"><span data-stu-id="0b598-165">Application API and environment</span></span>
<span data-ttu-id="0b598-166">hello 雲端服務環境 API 提供的資訊和 hello 目前 VM 執行個體，以及其他 VM 角色執行個體的相關資訊的功能。</span><span class="sxs-lookup"><span data-stu-id="0b598-166">hello Cloud Services environment API provides information and functionality for hello current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="0b598-167">Service Fabric 提供 tooits 執行階段相關的資訊，以及目前在執行某些 hello 節點服務的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0b598-167">Service Fabric provides information related tooits runtime and some information about hello node a service is currently running on.</span></span> 

| <span data-ttu-id="0b598-168">**環境工作**</span><span class="sxs-lookup"><span data-stu-id="0b598-168">**Environment Task**</span></span> | <span data-ttu-id="0b598-169">**雲端服務**</span><span class="sxs-lookup"><span data-stu-id="0b598-169">**Cloud Services**</span></span> | <span data-ttu-id="0b598-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="0b598-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b598-171">組態設定和變更通知</span><span class="sxs-lookup"><span data-stu-id="0b598-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="0b598-172">本機儲存體</span><span class="sxs-lookup"><span data-stu-id="0b598-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="0b598-173">端點資訊</span><span class="sxs-lookup"><span data-stu-id="0b598-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="0b598-174">目前的執行個體︰`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="0b598-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="0b598-175">其他角色和執行個體︰`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="0b598-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="0b598-176">`NodeContext` (針對目前的節點位址)</span><span class="sxs-lookup"><span data-stu-id="0b598-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="0b598-177">`FabricClient` 和 `ServicePartitionResolver` (針對服務端點探索)</span><span class="sxs-lookup"><span data-stu-id="0b598-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="0b598-178">環境模擬</span><span class="sxs-lookup"><span data-stu-id="0b598-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="0b598-179">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-179">N/A</span></span> |
| <span data-ttu-id="0b598-180">同時變更事件</span><span class="sxs-lookup"><span data-stu-id="0b598-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="0b598-181">N/A</span><span class="sxs-lookup"><span data-stu-id="0b598-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="0b598-182">組態設定</span><span class="sxs-lookup"><span data-stu-id="0b598-182">Configuration settings</span></span>
<span data-ttu-id="0b598-183">雲端服務中的組態設定會設定的 VM 角色，並套用 tooall 該 VM 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="0b598-183">Configuration settings in Cloud Services are set for a VM role and apply tooall instances of that VM role.</span></span> <span data-ttu-id="0b598-184">這些設定是 ServiceConfiguration.*.cscfg 檔案中所設定的索引鍵/值組，並可直接透過 RoleEnvironment 進行存取。</span><span class="sxs-lookup"><span data-stu-id="0b598-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="0b598-185">在 Service Fabric 設定適用於個別 tooeach 服務和 tooeach 應用程式，而不是 tooa VM，因為 VM 可以裝載多個服務和應用程式。</span><span class="sxs-lookup"><span data-stu-id="0b598-185">In Service Fabric, settings apply individually tooeach service and tooeach application, rather than tooa VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="0b598-186">服務包含三個封裝：</span><span class="sxs-lookup"><span data-stu-id="0b598-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="0b598-187">**程式碼：** hello 服務可執行檔、 二進位檔、 Dll 以及任何其他檔案包含服務需要 toorun。</span><span class="sxs-lookup"><span data-stu-id="0b598-187">**Code:** contains hello service executables, binaries, DLLs, and any other files a service needs toorun.</span></span>
* <span data-ttu-id="0b598-188">**組態：** 服務的所有組態檔和設定。</span><span class="sxs-lookup"><span data-stu-id="0b598-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="0b598-189">**資料：** hello 服務相關聯的靜態資料檔案。</span><span class="sxs-lookup"><span data-stu-id="0b598-189">**Data:** static data files associated with hello service.</span></span>

<span data-ttu-id="0b598-190">這些封裝每一個都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="0b598-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="0b598-191">類似 tooCloud 服務，設定封裝可以透過程式設計方式存取的 api，有可用的 toonotify hello 服務組態的封裝變更的事件。</span><span class="sxs-lookup"><span data-stu-id="0b598-191">Similar tooCloud Services, a config package can be accessed programmatically through an API and events are available toonotify hello service of a config package change.</span></span> <span data-ttu-id="0b598-192">Settings.xml 檔案可以用於索引鍵-值組態和以程式設計方式存取類似 toohello 應用程式設定區段的 App.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="0b598-192">A Settings.xml file can be used for key-value configuration and programmatic access similar toohello app settings section of an App.config file.</span></span> <span data-ttu-id="0b598-193">不過，和雲端服務不同的是，Service Fabric 組態封裝可以包含任何格式的任何組態檔，無論是 XML、JSON、YAML 或自訂的二進位格式。</span><span class="sxs-lookup"><span data-stu-id="0b598-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="0b598-194">存取組態</span><span class="sxs-lookup"><span data-stu-id="0b598-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="0b598-195">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0b598-195">Cloud Services</span></span>
<span data-ttu-id="0b598-196">透過 `RoleEnvironment`即可存取 ServiceConfiguration.*.cscfg 中的組態設定。</span><span class="sxs-lookup"><span data-stu-id="0b598-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="0b598-197">這些設定會全域可用 tooall hello 中的角色執行個體相同的雲端服務部署。</span><span class="sxs-lookup"><span data-stu-id="0b598-197">These settings are globally available tooall role instances in hello same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="0b598-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0b598-198">Service Fabric</span></span>
<span data-ttu-id="0b598-199">每個服務都有自己的個別組態封裝。</span><span class="sxs-lookup"><span data-stu-id="0b598-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="0b598-200">可供叢集中所有應用程式存取的全域組態設定沒有內建機制。</span><span class="sxs-lookup"><span data-stu-id="0b598-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="0b598-201">使用 Service Fabric 特殊 Settings.xml 組態檔內組態封裝時，可以是 hello 應用程式層級，讓應用程式層級的組態設定可以覆寫 Settings.xml 中的值。</span><span class="sxs-lookup"><span data-stu-id="0b598-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at hello application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="0b598-202">組態設定是透過 hello 服務每個服務執行個體內存取`CodePackageActivationContext`。</span><span class="sxs-lookup"><span data-stu-id="0b598-202">Configuration settings are accesses within each service instance through hello service's `CodePackageActivationContext`.</span></span>

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a><span data-ttu-id="0b598-203">組態更新事件</span><span class="sxs-lookup"><span data-stu-id="0b598-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="0b598-204">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0b598-204">Cloud Services</span></span>
<span data-ttu-id="0b598-205">hello`RoleEnvironment.Changed`事件就會使用的 toonotify 所有角色執行個體變更時，就會都發生在 hello 環境中，例如組態變更。</span><span class="sxs-lookup"><span data-stu-id="0b598-205">hello `RoleEnvironment.Changed` event is used toonotify all role instances when a change occurs in hello environment, such as a configuration change.</span></span> <span data-ttu-id="0b598-206">這是使用的 tooconsume 組態更新，而不需要回收角色執行個體，或重新啟動背景工作處理序。</span><span class="sxs-lookup"><span data-stu-id="0b598-206">This is used tooconsume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="0b598-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0b598-207">Service Fabric</span></span>
<span data-ttu-id="0b598-208">Hello 三種封裝類型服務的程式碼、 組態中和資料層中有更新、 加入或移除封裝時，通知的服務執行個體的事件。</span><span class="sxs-lookup"><span data-stu-id="0b598-208">Each of hello three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="0b598-209">服務可以包含多個各類型的封裝。</span><span class="sxs-lookup"><span data-stu-id="0b598-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="0b598-210">例如，服務可以有多個組態封裝，每個都個別設定版本並可升級。</span><span class="sxs-lookup"><span data-stu-id="0b598-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="0b598-211">這些事件是在不需要重新啟動 hello 服務執行個體的服務封裝中的可用 tooconsume 變更。</span><span class="sxs-lookup"><span data-stu-id="0b598-211">These events are available tooconsume changes in service packages without restarting hello service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="0b598-212">啟動工作</span><span class="sxs-lookup"><span data-stu-id="0b598-212">Startup tasks</span></span>
<span data-ttu-id="0b598-213">啟動工作是應用程式啟動前所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="0b598-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="0b598-214">啟動工作是常用的 toorun 安裝指令碼，使用提高的權限。</span><span class="sxs-lookup"><span data-stu-id="0b598-214">A startup task is typically used toorun setup scripts using elevated privileges.</span></span> <span data-ttu-id="0b598-215">雲端服務和 Service Fabric 皆支援啟動工作。</span><span class="sxs-lookup"><span data-stu-id="0b598-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="0b598-216">hello 主要差異在於，在雲端服務、 啟動工作是繫結的 tooa VM 因為它是一部分的角色執行個體，而服務網狀架構中的啟動工作是繫結的 tooa 服務，不是繫結的 tooany 特定 VM。</span><span class="sxs-lookup"><span data-stu-id="0b598-216">hello main difference is that in Cloud Services, a startup task is tied tooa VM because it is part of a role instance, whereas in Service Fabric a startup task is tied tooa service, which is not tied tooany particular VM.</span></span>

| <span data-ttu-id="0b598-217">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0b598-217">Cloud Services</span></span> | <span data-ttu-id="0b598-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0b598-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b598-219">組態位置</span><span class="sxs-lookup"><span data-stu-id="0b598-219">Configuration location</span></span> |<span data-ttu-id="0b598-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="0b598-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="0b598-221">權限</span><span class="sxs-lookup"><span data-stu-id="0b598-221">Privileges</span></span> |<span data-ttu-id="0b598-222">「有限」或「提高」</span><span class="sxs-lookup"><span data-stu-id="0b598-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="0b598-223">排序</span><span class="sxs-lookup"><span data-stu-id="0b598-223">Sequencing</span></span> |<span data-ttu-id="0b598-224">「簡單」、「背景」、「前景」</span><span class="sxs-lookup"><span data-stu-id="0b598-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="0b598-225">雲端服務</span><span class="sxs-lookup"><span data-stu-id="0b598-225">Cloud Services</span></span>
<span data-ttu-id="0b598-226">雲端服務中的啟動進入點是在 ServiceDefinition.csdef 中針對每個角色進行設定。</span><span class="sxs-lookup"><span data-stu-id="0b598-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a><span data-ttu-id="0b598-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0b598-227">Service Fabric</span></span>
<span data-ttu-id="0b598-228">Service Fabric 中的啟動進入點是在 ServiceManifest.xml 中針對每個服務進行設定。</span><span class="sxs-lookup"><span data-stu-id="0b598-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a><span data-ttu-id="0b598-229">開發環境的注意事項</span><span class="sxs-lookup"><span data-stu-id="0b598-229">A note about development environment</span></span>
<span data-ttu-id="0b598-230">雲端服務和服務網狀架構會使用 Visual Studio 與整合專案範本，以及支援偵錯、 設定及部署在本機和 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0b598-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and tooAzure.</span></span> <span data-ttu-id="0b598-231">雲端服務和 Service Fabric 也都提供本機開發執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="0b598-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="0b598-232">hello 的差異在於 hello 雲端服務的開發執行階段會模擬 hello 於所執行的 Azure 環境中，Service Fabric 不會使用模擬器-它會使用 hello 完成 Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="0b598-232">hello difference is that while hello Cloud Service development runtime emulates hello Azure environment on which it runs, Service Fabric does not use an emulator - it uses hello complete Service Fabric runtime.</span></span> <span data-ttu-id="0b598-233">hello Service Fabric 本機開發電腦執行的環境是 hello 在生產環境中執行的相同環境。</span><span class="sxs-lookup"><span data-stu-id="0b598-233">hello Service Fabric environment you run on your local development machine is hello same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b598-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b598-234">Next steps</span></span>
<span data-ttu-id="0b598-235">深入了解有關服務網狀架構可靠的服務和 hello 雲端服務和 Service Fabric 應用程式架構 toounderstand tootake 利用完整的 hello 的 Service Fabric 功能的設定方式之間的基本差異。</span><span class="sxs-lookup"><span data-stu-id="0b598-235">Read more about Service Fabric Reliable Services and hello fundamental differences between Cloud Services and Service Fabric application architecture toounderstand how tootake advantage of hello full set of Service Fabric features.</span></span>

* [<span data-ttu-id="0b598-236">開始使用 Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0b598-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="0b598-237">雲端服務和服務網狀架構之間的概念指南 toohello 差異</span><span class="sxs-lookup"><span data-stu-id="0b598-237">Conceptual guide toohello differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
