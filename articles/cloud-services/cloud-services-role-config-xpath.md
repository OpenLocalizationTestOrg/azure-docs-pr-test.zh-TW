---
title: "雲端服務角色組態 XPath 功能提要 | Microsoft Docs"
description: "您可以在雲端服務角色組態中用來公開設定以做為環境變數的各種 XPath 設定。"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="1e65f-103">利用 XPath 公開角色組態設定以做為環境變數</span><span class="sxs-lookup"><span data-stu-id="1e65f-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="1e65f-104">在雲端服務背景工作角色或 Web 角色服務定義檔中，您可以公開執行階段組態值以做為環境變數。</span><span class="sxs-lookup"><span data-stu-id="1e65f-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="1e65f-105">支援下列 XPath 值 (其會對應至 API 值)。</span><span class="sxs-lookup"><span data-stu-id="1e65f-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="1e65f-106">這些 XPath 值也可以透過 [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) 程式庫來取得。</span><span class="sxs-lookup"><span data-stu-id="1e65f-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="1e65f-107">在模擬器中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="1e65f-107">App running in emulator</span></span>
<span data-ttu-id="1e65f-108">表示應用程式正在模擬器中執行。</span><span class="sxs-lookup"><span data-stu-id="1e65f-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="1e65f-109">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-109">Type</span></span> | <span data-ttu-id="1e65f-110">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-111">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-111">XPath</span></span> |<span data-ttu-id="1e65f-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="1e65f-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="1e65f-113">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-113">Code</span></span> |<span data-ttu-id="1e65f-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="1e65f-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="1e65f-115">部署 ID</span><span class="sxs-lookup"><span data-stu-id="1e65f-115">Deployment ID</span></span>
<span data-ttu-id="1e65f-116">擷取執行個體的部署 ID。</span><span class="sxs-lookup"><span data-stu-id="1e65f-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="1e65f-117">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-117">Type</span></span> | <span data-ttu-id="1e65f-118">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-119">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-119">XPath</span></span> |<span data-ttu-id="1e65f-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="1e65f-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="1e65f-121">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-121">Code</span></span> |<span data-ttu-id="1e65f-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="1e65f-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="1e65f-123">角色 ID</span><span class="sxs-lookup"><span data-stu-id="1e65f-123">Role ID</span></span>
<span data-ttu-id="1e65f-124">擷取執行個體目前的角色 ID。</span><span class="sxs-lookup"><span data-stu-id="1e65f-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="1e65f-125">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-125">Type</span></span> | <span data-ttu-id="1e65f-126">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-127">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-127">XPath</span></span> |<span data-ttu-id="1e65f-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="1e65f-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="1e65f-129">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-129">Code</span></span> |<span data-ttu-id="1e65f-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="1e65f-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="1e65f-131">更新網站</span><span class="sxs-lookup"><span data-stu-id="1e65f-131">Update domain</span></span>
<span data-ttu-id="1e65f-132">擷取執行個體的更新網域。</span><span class="sxs-lookup"><span data-stu-id="1e65f-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="1e65f-133">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-133">Type</span></span> | <span data-ttu-id="1e65f-134">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-135">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-135">XPath</span></span> |<span data-ttu-id="1e65f-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="1e65f-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="1e65f-137">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-137">Code</span></span> |<span data-ttu-id="1e65f-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="1e65f-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="1e65f-139">容錯網域</span><span class="sxs-lookup"><span data-stu-id="1e65f-139">Fault domain</span></span>
<span data-ttu-id="1e65f-140">擷取執行個體的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="1e65f-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="1e65f-141">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-141">Type</span></span> | <span data-ttu-id="1e65f-142">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-143">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-143">XPath</span></span> |<span data-ttu-id="1e65f-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="1e65f-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="1e65f-145">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-145">Code</span></span> |<span data-ttu-id="1e65f-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="1e65f-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="1e65f-147">角色名稱</span><span class="sxs-lookup"><span data-stu-id="1e65f-147">Role name</span></span>
<span data-ttu-id="1e65f-148">擷取執行個體的角色名稱。</span><span class="sxs-lookup"><span data-stu-id="1e65f-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="1e65f-149">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-149">Type</span></span> | <span data-ttu-id="1e65f-150">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-151">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-151">XPath</span></span> |<span data-ttu-id="1e65f-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="1e65f-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="1e65f-153">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-153">Code</span></span> |<span data-ttu-id="1e65f-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="1e65f-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="1e65f-155">組態設定</span><span class="sxs-lookup"><span data-stu-id="1e65f-155">Config setting</span></span>
<span data-ttu-id="1e65f-156">擷取指定之組態設定的值。</span><span class="sxs-lookup"><span data-stu-id="1e65f-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="1e65f-157">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-157">Type</span></span> | <span data-ttu-id="1e65f-158">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-159">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-159">XPath</span></span> |<span data-ttu-id="1e65f-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="1e65f-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="1e65f-161">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-161">Code</span></span> |<span data-ttu-id="1e65f-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="1e65f-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="1e65f-163">本機儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="1e65f-163">Local storage path</span></span>
<span data-ttu-id="1e65f-164">擷取執行個體的本機儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="1e65f-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="1e65f-165">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-165">Type</span></span> | <span data-ttu-id="1e65f-166">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-167">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-167">XPath</span></span> |<span data-ttu-id="1e65f-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="1e65f-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="1e65f-169">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-169">Code</span></span> |<span data-ttu-id="1e65f-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="1e65f-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="1e65f-171">本機儲存體大小</span><span class="sxs-lookup"><span data-stu-id="1e65f-171">Local storage size</span></span>
<span data-ttu-id="1e65f-172">擷取執行個體的本機儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="1e65f-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="1e65f-173">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-173">Type</span></span> | <span data-ttu-id="1e65f-174">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-175">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-175">XPath</span></span> |<span data-ttu-id="1e65f-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="1e65f-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="1e65f-177">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-177">Code</span></span> |<span data-ttu-id="1e65f-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="1e65f-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="1e65f-179">端點通訊協定</span><span class="sxs-lookup"><span data-stu-id="1e65f-179">Endpoint protocol</span></span>
<span data-ttu-id="1e65f-180">擷取執行個體的端點通訊協定。</span><span class="sxs-lookup"><span data-stu-id="1e65f-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="1e65f-181">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-181">Type</span></span> | <span data-ttu-id="1e65f-182">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-183">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-183">XPath</span></span> |<span data-ttu-id="1e65f-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="1e65f-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="1e65f-185">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-185">Code</span></span> |<span data-ttu-id="1e65f-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="1e65f-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="1e65f-187">端點 IP</span><span class="sxs-lookup"><span data-stu-id="1e65f-187">Endpoint IP</span></span>
<span data-ttu-id="1e65f-188">取得指定端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="1e65f-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="1e65f-189">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-189">Type</span></span> | <span data-ttu-id="1e65f-190">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-191">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-191">XPath</span></span> |<span data-ttu-id="1e65f-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="1e65f-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="1e65f-193">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-193">Code</span></span> |<span data-ttu-id="1e65f-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="1e65f-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="1e65f-195">端點連接埠</span><span class="sxs-lookup"><span data-stu-id="1e65f-195">Endpoint port</span></span>
<span data-ttu-id="1e65f-196">擷取執行個體的端點連接埠。</span><span class="sxs-lookup"><span data-stu-id="1e65f-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="1e65f-197">類型</span><span class="sxs-lookup"><span data-stu-id="1e65f-197">Type</span></span> | <span data-ttu-id="1e65f-198">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="1e65f-199">XPath</span><span class="sxs-lookup"><span data-stu-id="1e65f-199">XPath</span></span> |<span data-ttu-id="1e65f-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="1e65f-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="1e65f-201">代碼</span><span class="sxs-lookup"><span data-stu-id="1e65f-201">Code</span></span> |<span data-ttu-id="1e65f-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="1e65f-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="1e65f-203">範例</span><span class="sxs-lookup"><span data-stu-id="1e65f-203">Example</span></span>
<span data-ttu-id="1e65f-204">以下的背景工作角色範例會使用名為 `TestIsEmulated` 且設定為 [@emulated xpath 值](#app-running-in-emulator)的環境變數來建立啟動工作。</span><span class="sxs-lookup"><span data-stu-id="1e65f-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="1e65f-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1e65f-205">Next steps</span></span>
<span data-ttu-id="1e65f-206">深入了解 [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) 檔案。</span><span class="sxs-lookup"><span data-stu-id="1e65f-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="1e65f-207">建立 [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 封裝。</span><span class="sxs-lookup"><span data-stu-id="1e65f-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="1e65f-208">為角色啟用 [遠端桌面](cloud-services-role-enable-remote-desktop.md) 。</span><span class="sxs-lookup"><span data-stu-id="1e65f-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

