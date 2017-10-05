---
title: "將 Azure 雲端服務應用程式轉換成微服務 | Microsoft Docs"
description: "本指南會比較雲端服務的 Web 角色和背景工作角色以及 Service Fabric 的無狀態服務，以協助您從雲端服務移轉到 Service Fabric。"
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
ms.openlocfilehash: 4ab1f83e88b262b1752300b2786340d9abca8154
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-converting-web-and-worker-roles-to-service-fabric-stateless-services"></a><span data-ttu-id="3636b-103">將 Web 角色和背景工作角色轉換成 Service Fabric 無狀態服務的指南</span><span class="sxs-lookup"><span data-stu-id="3636b-103">Guide to converting Web and Worker Roles to Service Fabric stateless services</span></span>
<span data-ttu-id="3636b-104">本文說明如何將雲端服務的 Web 角色和背景工作角色移轉至 Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="3636b-104">This article describes how to migrate your Cloud Services Web and Worker Roles to Service Fabric stateless services.</span></span> <span data-ttu-id="3636b-105">對於整體架構會大致保持相同的應用程式來說，這是最簡單的雲端服務至 Service Fabric 移轉路徑。</span><span class="sxs-lookup"><span data-stu-id="3636b-105">This is the simplest migration path from Cloud Services to Service Fabric for applications whose overall architecture is going to stay roughly the same.</span></span>

## <a name="cloud-service-project-to-service-fabric-application-project"></a><span data-ttu-id="3636b-106">雲端服務專案到 Service Fabric 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="3636b-106">Cloud Service project to Service Fabric application project</span></span>
 <span data-ttu-id="3636b-107">雲端服務專案和 Service Fabric 應用程式專案結構類似，且兩者皆能代表應用程式的部署單位，也就是說，兩者各自會定義所部署來執行應用程式的完整封裝。</span><span class="sxs-lookup"><span data-stu-id="3636b-107">A Cloud Service project and a Service Fabric Application project have a similar structure and both represent the deployment unit for your application - that is, they each define the complete package that is deployed to run your application.</span></span> <span data-ttu-id="3636b-108">雲端服務專案包含一個或多個 Web 角色和背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="3636b-108">A Cloud Service project contains one or more Web or Worker Roles.</span></span> <span data-ttu-id="3636b-109">同樣地，Service Fabric 應用程式專案也包含一個或多個服務。</span><span class="sxs-lookup"><span data-stu-id="3636b-109">Similarly, a Service Fabric Application project contains one or more services.</span></span> 

<span data-ttu-id="3636b-110">兩者的差別在於，雲端服務專案會結合應用程式部署與 VM 部署，因此其中會包含 VM 組態設定，而 Service Fabric 應用程式專案則只會定義將要部署到 Service Fabric 叢集中一組現有 VM 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3636b-110">The difference is that the Cloud Service project couples the application deployment with a VM deployment and thus contains VM configuration settings in it, whereas the Service Fabric Application project only defines an application that will be deployed to a set of existing VMs in a Service Fabric cluster.</span></span> <span data-ttu-id="3636b-111">部署 Service Fabric 叢集時，可透過 Resource Manager 範本或 Azure 入口網站來進行部署，叢集本身只會部署一次，但可在此叢集中部署多個 Service Fabric 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3636b-111">The Service Fabric cluster itself is only deployed once, either through an Resource Manager template or through the Azure portal, and multiple Service Fabric applications can be deployed to it.</span></span>

![Service Fabric 和雲端服務專案的比較][3]

## <a name="worker-role-to-stateless-service"></a><span data-ttu-id="3636b-113">背景工作角色至無狀態服務</span><span class="sxs-lookup"><span data-stu-id="3636b-113">Worker Role to stateless service</span></span>
<span data-ttu-id="3636b-114">從概念上來說，背景工作角色代表無狀態的工作負載，這表示是工作負載的每個執行個體都是相同的，隨時都可將要求路由傳送到任何執行個體。</span><span class="sxs-lookup"><span data-stu-id="3636b-114">Conceptually, a Worker Role represents a stateless workload, meaning every instance of the workload is identical and requests can be routed to any instance at any time.</span></span> <span data-ttu-id="3636b-115">每個執行個體應該不會記得先前的要求。</span><span class="sxs-lookup"><span data-stu-id="3636b-115">Each instance is not expected to remember the previous request.</span></span> <span data-ttu-id="3636b-116">工作負載的運作狀態是由外部狀態存放區 (例如 Azure 資料表儲存體或 Azure Document DB) 負責管理。</span><span class="sxs-lookup"><span data-stu-id="3636b-116">State that the workload operates on is managed by an external state store, such as Azure Table Storage or Azure Document DB.</span></span> <span data-ttu-id="3636b-117">在 Service Fabric 中，這類工作負載是以無狀態服務來代表。</span><span class="sxs-lookup"><span data-stu-id="3636b-117">In Service Fabric, this type of workload is represented by a Stateless Service.</span></span> <span data-ttu-id="3636b-118">只要將背景工作角色程式碼轉換成無狀態服務，就能以最簡單的方式將背景工作角色移轉到 Service Fabric。</span><span class="sxs-lookup"><span data-stu-id="3636b-118">The simplest approach to migrating a Worker Role to Service Fabric can be done by converting Worker Role code to a Stateless Service.</span></span>

![背景工作角色至無狀態服務][4]

## <a name="web-role-to-stateless-service"></a><span data-ttu-id="3636b-120">Web 角色至無狀態服務</span><span class="sxs-lookup"><span data-stu-id="3636b-120">Web Role to stateless service</span></span>
<span data-ttu-id="3636b-121">和背景工作角色類似，Web 角色也代表無狀態的工作負載，因此在概念上也能對應至 Service Fabric 無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="3636b-121">Similar to Worker Role, a Web Role also represents a stateless workload, and so conceptually it too can be mapped to a Service Fabric stateless service.</span></span> <span data-ttu-id="3636b-122">不過，和 Web 角色不同的是，Service Fabric 不支援 IIS。</span><span class="sxs-lookup"><span data-stu-id="3636b-122">However, unlike Web Roles, Service Fabric does not support IIS.</span></span> <span data-ttu-id="3636b-123">若要將 Web 應用程式從 Web 角色移轉至無狀態服務，必須先移動到可以自我裝載且不仰賴 IIS 或 System.Web (例如 ASP.NET Core 1) 的 Web 架構。</span><span class="sxs-lookup"><span data-stu-id="3636b-123">To migrate a web application from a Web Role to a stateless service requires first moving to a web framework that can be self-hosted and does not depend on IIS or System.Web, such as ASP.NET Core 1.</span></span>

| <span data-ttu-id="3636b-124">**應用程式**</span><span class="sxs-lookup"><span data-stu-id="3636b-124">**Application**</span></span> | <span data-ttu-id="3636b-125">**支援**</span><span class="sxs-lookup"><span data-stu-id="3636b-125">**Supported**</span></span> | <span data-ttu-id="3636b-126">**移轉路徑**</span><span class="sxs-lookup"><span data-stu-id="3636b-126">**Migration path**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3636b-127">ASP.NET Web Forms</span><span class="sxs-lookup"><span data-stu-id="3636b-127">ASP.NET Web Forms</span></span> |<span data-ttu-id="3636b-128">否</span><span class="sxs-lookup"><span data-stu-id="3636b-128">No</span></span> |<span data-ttu-id="3636b-129">轉換為 ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="3636b-129">Convert to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="3636b-130">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3636b-130">ASP.NET MVC</span></span> |<span data-ttu-id="3636b-131">移轉</span><span class="sxs-lookup"><span data-stu-id="3636b-131">With Migration</span></span> |<span data-ttu-id="3636b-132">升級至 ASP.NET Core 1 MVC</span><span class="sxs-lookup"><span data-stu-id="3636b-132">Upgrade to ASP.NET Core 1 MVC</span></span> |
| <span data-ttu-id="3636b-133">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="3636b-133">ASP.NET Web API</span></span> |<span data-ttu-id="3636b-134">移轉</span><span class="sxs-lookup"><span data-stu-id="3636b-134">With Migration</span></span> |<span data-ttu-id="3636b-135">使用自我裝載的伺服器或 ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="3636b-135">Use self-hosted server or ASP.NET Core 1</span></span> |
| <span data-ttu-id="3636b-136">ASP.NET Core 1</span><span class="sxs-lookup"><span data-stu-id="3636b-136">ASP.NET Core 1</span></span> |<span data-ttu-id="3636b-137">是</span><span class="sxs-lookup"><span data-stu-id="3636b-137">Yes</span></span> |<span data-ttu-id="3636b-138">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-138">N/A</span></span> |

## <a name="entry-point-api-and-lifecycle"></a><span data-ttu-id="3636b-139">進入點 API 和生命週期</span><span class="sxs-lookup"><span data-stu-id="3636b-139">Entry point API and lifecycle</span></span>
<span data-ttu-id="3636b-140">背景工作角色和 Service Fabric 服務 API 提供類似的進入點：</span><span class="sxs-lookup"><span data-stu-id="3636b-140">Worker Role and Service Fabric service APIs offer similar entry points:</span></span> 

| <span data-ttu-id="3636b-141">**進入點**</span><span class="sxs-lookup"><span data-stu-id="3636b-141">**Entry Point**</span></span> | <span data-ttu-id="3636b-142">**背景工作角色**</span><span class="sxs-lookup"><span data-stu-id="3636b-142">**Worker Role**</span></span> | <span data-ttu-id="3636b-143">**Service Fabric 服務**</span><span class="sxs-lookup"><span data-stu-id="3636b-143">**Service Fabric service**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3636b-144">Processing</span><span class="sxs-lookup"><span data-stu-id="3636b-144">Processing</span></span> |`Run()` |`RunAsync()` |
| <span data-ttu-id="3636b-145">VM 啟動</span><span class="sxs-lookup"><span data-stu-id="3636b-145">VM start</span></span> |`OnStart()` |<span data-ttu-id="3636b-146">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-146">N/A</span></span> |
| <span data-ttu-id="3636b-147">VM 停止</span><span class="sxs-lookup"><span data-stu-id="3636b-147">VM stop</span></span> |`OnStop()` |<span data-ttu-id="3636b-148">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-148">N/A</span></span> |
| <span data-ttu-id="3636b-149">開啟接聽程式以接收用戶端要求</span><span class="sxs-lookup"><span data-stu-id="3636b-149">Open listener for client requests</span></span> |<span data-ttu-id="3636b-150">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-150">N/A</span></span> |<ul><li> <span data-ttu-id="3636b-151">`CreateServiceInstanceListener()` (針對無狀態)</span><span class="sxs-lookup"><span data-stu-id="3636b-151">`CreateServiceInstanceListener()` for stateless</span></span></li><li><span data-ttu-id="3636b-152">`CreateServiceReplicaListener()` (針對具狀態)</span><span class="sxs-lookup"><span data-stu-id="3636b-152">`CreateServiceReplicaListener()` for stateful</span></span></li></ul> |

### <a name="worker-role"></a><span data-ttu-id="3636b-153">背景工作角色</span><span class="sxs-lookup"><span data-stu-id="3636b-153">Worker Role</span></span>
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

### <a name="service-fabric-stateless-service"></a><span data-ttu-id="3636b-154">Service Fabric 無狀態服務</span><span class="sxs-lookup"><span data-stu-id="3636b-154">Service Fabric Stateless Service</span></span>
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

<span data-ttu-id="3636b-155">兩者都有可從中開始處理的主要「執行」覆寫。</span><span class="sxs-lookup"><span data-stu-id="3636b-155">Both have a primary "Run" override in which to begin processing.</span></span> <span data-ttu-id="3636b-156">Service Fabric 服務將 `Run`、`Start` 和 `Stop` 結合為單一進入點 `RunAsync`。</span><span class="sxs-lookup"><span data-stu-id="3636b-156">Service Fabric services  combine `Run`, `Start`, and `Stop` into a single entry point, `RunAsync`.</span></span> <span data-ttu-id="3636b-157">當 `RunAsync` 啟動時，服務應該會開始運作，而當 `RunAsync` 方法的 CancellationToken 收到信號時，則應該會停止運作。</span><span class="sxs-lookup"><span data-stu-id="3636b-157">Your service should begin working when `RunAsync` starts, and should stop working when the `RunAsync` method's CancellationToken is signaled.</span></span> 

<span data-ttu-id="3636b-158">背景工作角色和 Service Fabric 服務的生命週期與存留期之間有幾個主要差異：</span><span class="sxs-lookup"><span data-stu-id="3636b-158">There are several key differences between the lifecycle and lifetime of Worker Roles and Service Fabric services:</span></span>

* <span data-ttu-id="3636b-159">**生命週期：** 最大的差異是背景工作角色是 VM，因此其生命週期繫結至 VM，且包含 VM 啟動和停止時的事件。</span><span class="sxs-lookup"><span data-stu-id="3636b-159">**Lifecycle:** The biggest difference is that a Worker Role is a VM and so its lifecycle is tied to the VM, which includes events for when the VM starts and stops.</span></span> <span data-ttu-id="3636b-160">Service Fabric 服務的生命週期則和 VM 的生命週期不同，因此不包含主機 VM 或機器啟動和停止時的事件，因為它們彼此不相關。</span><span class="sxs-lookup"><span data-stu-id="3636b-160">A Service Fabric service has a lifecycle that is separate from the VM lifecycle, so it does not include events for when the host VM or machine starts and stop, as they are not related.</span></span>
* <span data-ttu-id="3636b-161">**存留期：**背景工作角色執行個體會在 `Run` 方法結束時回收。</span><span class="sxs-lookup"><span data-stu-id="3636b-161">**Lifetime:** A Worker Role instance will recycle if the `Run` method exits.</span></span> <span data-ttu-id="3636b-162">不過，Service Fabric 服務中的 `RunAsync` 方法可以執行到完成為止，且服務執行個體會維持啟動狀態。</span><span class="sxs-lookup"><span data-stu-id="3636b-162">The `RunAsync` method in a Service Fabric service however can run to completion and the service instance will stay up.</span></span> 

<span data-ttu-id="3636b-163">Service Fabric 為接聽用戶端要求的服務提供選擇性的通訊設定進入點。</span><span class="sxs-lookup"><span data-stu-id="3636b-163">Service Fabric provides an optional communication setup entry point for services that listen for client requests.</span></span> <span data-ttu-id="3636b-164">RunAsync 和通訊進入點都是 Service Fabric 服務中的選擇性覆寫 (服務可選擇只接聽用戶端要求或只執行處理迴圈，或兩者都選擇)，這就是 RunAsync 方法不必重新啟動服務執行個體就可以結束的原因，因為它可以繼續接聽用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="3636b-164">Both the RunAsync and communication entry point are optional overrides in Service Fabric services - your service may choose to only listen to client requests, or only run a processing loop, or both - which is why the RunAsync method is allowed to exit without restarting the service instance, because it may continue to listen for client requests.</span></span>

## <a name="application-api-and-environment"></a><span data-ttu-id="3636b-165">應用程式 API 和環境</span><span class="sxs-lookup"><span data-stu-id="3636b-165">Application API and environment</span></span>
<span data-ttu-id="3636b-166">雲端服務環境 API 提供目前 VM 執行個體的資訊和功能，以及關於其他 VM 角色執行個體的資訊。</span><span class="sxs-lookup"><span data-stu-id="3636b-166">The Cloud Services environment API provides information and functionality for the current VM instance as well as information about other VM role instances.</span></span> <span data-ttu-id="3636b-167">Service Fabric 則提供其執行階段的相關資訊，以及關於服務目前執行所在之節點的某些資訊。</span><span class="sxs-lookup"><span data-stu-id="3636b-167">Service Fabric provides information related to its runtime and some information about the node a service is currently running on.</span></span> 

| <span data-ttu-id="3636b-168">**環境工作**</span><span class="sxs-lookup"><span data-stu-id="3636b-168">**Environment Task**</span></span> | <span data-ttu-id="3636b-169">**雲端服務**</span><span class="sxs-lookup"><span data-stu-id="3636b-169">**Cloud Services**</span></span> | <span data-ttu-id="3636b-170">**Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="3636b-170">**Service Fabric**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3636b-171">組態設定和變更通知</span><span class="sxs-lookup"><span data-stu-id="3636b-171">Configuration Settings and change notification</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="3636b-172">本機儲存體</span><span class="sxs-lookup"><span data-stu-id="3636b-172">Local Storage</span></span> |`RoleEnvironment` |`CodePackageActivationContext` |
| <span data-ttu-id="3636b-173">端點資訊</span><span class="sxs-lookup"><span data-stu-id="3636b-173">Endpoint Information</span></span> |`RoleInstance` <ul><li><span data-ttu-id="3636b-174">目前的執行個體︰`RoleEnvironment.CurrentRoleInstance`</span><span class="sxs-lookup"><span data-stu-id="3636b-174">Current instance: `RoleEnvironment.CurrentRoleInstance`</span></span></li><li><span data-ttu-id="3636b-175">其他角色和執行個體︰`RoleEnvironment.Roles`</span><span class="sxs-lookup"><span data-stu-id="3636b-175">Other roles and instance: `RoleEnvironment.Roles`</span></span></li> |<ul><li><span data-ttu-id="3636b-176">`NodeContext` (針對目前的節點位址)</span><span class="sxs-lookup"><span data-stu-id="3636b-176">`NodeContext` for current Node address</span></span></li><li><span data-ttu-id="3636b-177">`FabricClient` 和 `ServicePartitionResolver` (針對服務端點探索)</span><span class="sxs-lookup"><span data-stu-id="3636b-177">`FabricClient` and `ServicePartitionResolver` for service endpoint discovery</span></span></li> |
| <span data-ttu-id="3636b-178">環境模擬</span><span class="sxs-lookup"><span data-stu-id="3636b-178">Environment Emulation</span></span> |`RoleEnvironment.IsEmulated` |<span data-ttu-id="3636b-179">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-179">N/A</span></span> |
| <span data-ttu-id="3636b-180">同時變更事件</span><span class="sxs-lookup"><span data-stu-id="3636b-180">Simultaneous change event</span></span> |`RoleEnvironment` |<span data-ttu-id="3636b-181">N/A</span><span class="sxs-lookup"><span data-stu-id="3636b-181">N/A</span></span> |

## <a name="configuration-settings"></a><span data-ttu-id="3636b-182">組態設定</span><span class="sxs-lookup"><span data-stu-id="3636b-182">Configuration settings</span></span>
<span data-ttu-id="3636b-183">雲端服務中的組態設定已針對 VM 角色設定，並套用至該 VM 角色的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="3636b-183">Configuration settings in Cloud Services are set for a VM role and apply to all instances of that VM role.</span></span> <span data-ttu-id="3636b-184">這些設定是 ServiceConfiguration.*.cscfg 檔案中所設定的索引鍵/值組，並可直接透過 RoleEnvironment 進行存取。</span><span class="sxs-lookup"><span data-stu-id="3636b-184">These settings are key-value pairs set in ServiceConfiguration.*.cscfg files and can be accessed directly through RoleEnvironment.</span></span> <span data-ttu-id="3636b-185">在 Service Fabric 中，設定會個別套用至每個服務和每個應用程式，而不是套用至 VM，因為 VM 可以裝載多個服務和應用程式。</span><span class="sxs-lookup"><span data-stu-id="3636b-185">In Service Fabric, settings apply individually to each service and to each application, rather than to a VM, because a VM can host multiple services and applications.</span></span> <span data-ttu-id="3636b-186">服務包含三個封裝：</span><span class="sxs-lookup"><span data-stu-id="3636b-186">A service is composed of three packages:</span></span>

* <span data-ttu-id="3636b-187">**程式碼：** 包含服務的可執行檔、二進位檔、DLL 和服務需要執行的任何其他檔案。</span><span class="sxs-lookup"><span data-stu-id="3636b-187">**Code:** contains the service executables, binaries, DLLs, and any other files a service needs to run.</span></span>
* <span data-ttu-id="3636b-188">**組態：** 服務的所有組態檔和設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-188">**Config:** all configuration files and settings for a service.</span></span>
* <span data-ttu-id="3636b-189">**資料：** 與服務相關聯的靜態資料檔案。</span><span class="sxs-lookup"><span data-stu-id="3636b-189">**Data:** static data files associated with the service.</span></span>

<span data-ttu-id="3636b-190">這些封裝每一個都可以獨立設定版本和升級。</span><span class="sxs-lookup"><span data-stu-id="3636b-190">Each of these packages can be independently versioned and upgraded.</span></span> <span data-ttu-id="3636b-191">和雲端服務類似，組態封裝可以透過 API 以程式設計方式存取，並有提供事件來通知服務其組態封裝已變更。</span><span class="sxs-lookup"><span data-stu-id="3636b-191">Similar to Cloud Services, a config package can be accessed programmatically through an API and events are available to notify the service of a config package change.</span></span> <span data-ttu-id="3636b-192">Settings.xml 檔案可用於索引鍵/值組的組態和程式設計存取，類似於 App.config 檔案的應用程式設定區段。</span><span class="sxs-lookup"><span data-stu-id="3636b-192">A Settings.xml file can be used for key-value configuration and programmatic access similar to the app settings section of an App.config file.</span></span> <span data-ttu-id="3636b-193">不過，和雲端服務不同的是，Service Fabric 組態封裝可以包含任何格式的任何組態檔，無論是 XML、JSON、YAML 或自訂的二進位格式。</span><span class="sxs-lookup"><span data-stu-id="3636b-193">However, unlike Cloud Services, a Service Fabric config package can contain any configuration files in any format, whether it's XML, JSON, YAML, or a custom binary format.</span></span> 

### <a name="accessing-configuration"></a><span data-ttu-id="3636b-194">存取組態</span><span class="sxs-lookup"><span data-stu-id="3636b-194">Accessing configuration</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="3636b-195">雲端服務</span><span class="sxs-lookup"><span data-stu-id="3636b-195">Cloud Services</span></span>
<span data-ttu-id="3636b-196">透過 `RoleEnvironment`即可存取 ServiceConfiguration.*.cscfg 中的組態設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-196">Configuration settings from ServiceConfiguration.*.cscfg can be accessed through `RoleEnvironment`.</span></span> <span data-ttu-id="3636b-197">這些設定可全域提供給相同雲端服務部署中的所有角色執行個體使用。</span><span class="sxs-lookup"><span data-stu-id="3636b-197">These settings are globally available to all role instances in the same Cloud Service deployment.</span></span>

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a><span data-ttu-id="3636b-198">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3636b-198">Service Fabric</span></span>
<span data-ttu-id="3636b-199">每個服務都有自己的個別組態封裝。</span><span class="sxs-lookup"><span data-stu-id="3636b-199">Each service has its own individual configuration package.</span></span> <span data-ttu-id="3636b-200">可供叢集中所有應用程式存取的全域組態設定沒有內建機制。</span><span class="sxs-lookup"><span data-stu-id="3636b-200">There is no built-in mechanism for global configuration settings accessible by all applications in a cluster.</span></span> <span data-ttu-id="3636b-201">使用組態封裝內的 Service Fabric 特殊組態檔 Settings.xml 時，Settings.xml 中的值可以在應用程式層級覆寫，實現應用程式層級的組態設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-201">When using Service Fabric's special Settings.xml configuration file within a configuration package, values in Settings.xml can be overwritten at the application level, making application-level configuration settings possible.</span></span>

<span data-ttu-id="3636b-202">透過服務的 `CodePackageActivationContext`即可在每個服務執行個體內存取組態設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-202">Configuration settings are accesses within each service instance through the service's `CodePackageActivationContext`.</span></span>

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

### <a name="configuration-update-events"></a><span data-ttu-id="3636b-203">組態更新事件</span><span class="sxs-lookup"><span data-stu-id="3636b-203">Configuration update events</span></span>
#### <a name="cloud-services"></a><span data-ttu-id="3636b-204">雲端服務</span><span class="sxs-lookup"><span data-stu-id="3636b-204">Cloud Services</span></span>
<span data-ttu-id="3636b-205">當環境發生變更 (例如組態變更) 時，就會使用 `RoleEnvironment.Changed` 事件來通知所有角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="3636b-205">The `RoleEnvironment.Changed` event is used to notify all role instances when a change occurs in the environment, such as a configuration change.</span></span> <span data-ttu-id="3636b-206">使用此事件可取用組態更新，卻又不會回收角色執行個體或重新啟動背景工作角色處理序。</span><span class="sxs-lookup"><span data-stu-id="3636b-206">This is used to consume configuration updates without recycling role instances or restarting a worker process.</span></span>

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get the list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a><span data-ttu-id="3636b-207">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3636b-207">Service Fabric</span></span>
<span data-ttu-id="3636b-208">服務中的三個封裝類型 (程式碼、組態和資料) 每個都有可在封裝已更新、新增或移除時通知服務執行個體的事件。</span><span class="sxs-lookup"><span data-stu-id="3636b-208">Each of the three package types in a service - Code, Config, and Data - have events that notify a service instance when a package is updated, added, or removed.</span></span> <span data-ttu-id="3636b-209">服務可以包含多個各類型的封裝。</span><span class="sxs-lookup"><span data-stu-id="3636b-209">A service can contain multiple packages of each type.</span></span> <span data-ttu-id="3636b-210">例如，服務可以有多個組態封裝，每個都個別設定版本並可升級。</span><span class="sxs-lookup"><span data-stu-id="3636b-210">For example, a service may have multiple config packages, each individually versioned and upgradeable.</span></span> 

<span data-ttu-id="3636b-211">這些事件可供取用服務封裝中的變更而不必重新啟動服務執行個體。</span><span class="sxs-lookup"><span data-stu-id="3636b-211">These events are available to consume changes in service packages without restarting the service instance.</span></span>

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a><span data-ttu-id="3636b-212">啟動工作</span><span class="sxs-lookup"><span data-stu-id="3636b-212">Startup tasks</span></span>
<span data-ttu-id="3636b-213">啟動工作是應用程式啟動前所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="3636b-213">Startup tasks are actions that are taken before an application starts.</span></span> <span data-ttu-id="3636b-214">啟動工作通常用來以提高的權限執行安裝指令碼。</span><span class="sxs-lookup"><span data-stu-id="3636b-214">A startup task is typically used to run setup scripts using elevated privileges.</span></span> <span data-ttu-id="3636b-215">雲端服務和 Service Fabric 皆支援啟動工作。</span><span class="sxs-lookup"><span data-stu-id="3636b-215">Both Cloud Services and Service Fabric support start-up tasks.</span></span> <span data-ttu-id="3636b-216">兩者的主要差異是，雲端服務中的啟動工作繫結至 VM，因為它是角色執行個體的一部分，而 Service Fabric 中的啟動工作則繫結至服務，而不會繫結至任何特定 VM。</span><span class="sxs-lookup"><span data-stu-id="3636b-216">The main difference is that in Cloud Services, a startup task is tied to a VM because it is part of a role instance, whereas in Service Fabric a startup task is tied to a service, which is not tied to any particular VM.</span></span>

| <span data-ttu-id="3636b-217">雲端服務</span><span class="sxs-lookup"><span data-stu-id="3636b-217">Cloud Services</span></span> | <span data-ttu-id="3636b-218">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3636b-218">Service Fabric</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3636b-219">組態位置</span><span class="sxs-lookup"><span data-stu-id="3636b-219">Configuration location</span></span> |<span data-ttu-id="3636b-220">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="3636b-220">ServiceDefinition.csdef</span></span> |
| <span data-ttu-id="3636b-221">權限</span><span class="sxs-lookup"><span data-stu-id="3636b-221">Privileges</span></span> |<span data-ttu-id="3636b-222">「有限」或「提高」</span><span class="sxs-lookup"><span data-stu-id="3636b-222">"limited" or "elevated"</span></span> |
| <span data-ttu-id="3636b-223">排序</span><span class="sxs-lookup"><span data-stu-id="3636b-223">Sequencing</span></span> |<span data-ttu-id="3636b-224">「簡單」、「背景」、「前景」</span><span class="sxs-lookup"><span data-stu-id="3636b-224">"simple", "background", "foreground"</span></span> |

### <a name="cloud-services"></a><span data-ttu-id="3636b-225">雲端服務</span><span class="sxs-lookup"><span data-stu-id="3636b-225">Cloud Services</span></span>
<span data-ttu-id="3636b-226">雲端服務中的啟動進入點是在 ServiceDefinition.csdef 中針對每個角色進行設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-226">In Cloud Services a startup entry point is configured per role in ServiceDefinition.csdef.</span></span> 

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

### <a name="service-fabric"></a><span data-ttu-id="3636b-227">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3636b-227">Service Fabric</span></span>
<span data-ttu-id="3636b-228">Service Fabric 中的啟動進入點是在 ServiceManifest.xml 中針對每個服務進行設定。</span><span class="sxs-lookup"><span data-stu-id="3636b-228">In Service Fabric a startup entry point is configured per service in ServiceManifest.xml:</span></span>

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

## <a name="a-note-about-development-environment"></a><span data-ttu-id="3636b-229">開發環境的注意事項</span><span class="sxs-lookup"><span data-stu-id="3636b-229">A note about development environment</span></span>
<span data-ttu-id="3636b-230">雲端服務和 Service Fabric 都會使用專案範本來與 Visual Studio 整合，並支援偵錯、設定以及部署到本機和 Azure。</span><span class="sxs-lookup"><span data-stu-id="3636b-230">Both Cloud Services and Service Fabric are integrated with Visual Studio with project templates and support for debugging, configuring, and deploying both locally and to Azure.</span></span> <span data-ttu-id="3636b-231">雲端服務和 Service Fabric 也都提供本機開發執行階段環境。</span><span class="sxs-lookup"><span data-stu-id="3636b-231">Both Cloud Services and Service Fabric also provide a local development runtime environment.</span></span> <span data-ttu-id="3636b-232">兩者的差異在於，雲端服務的開發執行階段會模擬其執行所在的 Azure 環境，但 Service Fabric 不會使用模擬器，而是使用完整的 Service Fabric 執行階段。</span><span class="sxs-lookup"><span data-stu-id="3636b-232">The difference is that while the Cloud Service development runtime emulates the Azure environment on which it runs, Service Fabric does not use an emulator - it uses the complete Service Fabric runtime.</span></span> <span data-ttu-id="3636b-233">您在本機開發機器執行的 Service Fabric 環境和在生產階段時執行的是相同的環境。</span><span class="sxs-lookup"><span data-stu-id="3636b-233">The Service Fabric environment you run on your local development machine is the same environment that runs in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3636b-234">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3636b-234">Next steps</span></span>
<span data-ttu-id="3636b-235">請深入了解 Service Fabric Reliable Services 以及雲端服務與 Service Fabric 應用程式架構之間的基本差異，以了解如何利用 Service Fabric 的整組功能。</span><span class="sxs-lookup"><span data-stu-id="3636b-235">Read more about Service Fabric Reliable Services and the fundamental differences between Cloud Services and Service Fabric application architecture to understand how to take advantage of the full set of Service Fabric features.</span></span>

* [<span data-ttu-id="3636b-236">開始使用 Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3636b-236">Getting started with Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="3636b-237">雲端服務和 Service Fabric 之間差異的概念指南</span><span class="sxs-lookup"><span data-stu-id="3636b-237">Conceptual guide to the differences between Cloud Services and Service Fabric</span></span>](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
