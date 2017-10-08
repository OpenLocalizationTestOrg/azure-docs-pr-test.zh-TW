---
title: "aaaCloud 服務角色組態 XPath 小祕技 |Microsoft 文件"
description: "hello 各種 XPath 設定，您可以使用在 hello 雲端服務角色組態 tooexpose 設定做為環境變數。"
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
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="a9854-103">利用 XPath 公開角色組態設定以做為環境變數</span><span class="sxs-lookup"><span data-stu-id="a9854-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="a9854-104">在 hello 雲端服務工作者或 web 角色服務定義檔中，您可以為環境變數來公開執行階段組態值。</span><span class="sxs-lookup"><span data-stu-id="a9854-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="a9854-105">支援下列 XPath 值 hello （其對應 tooAPI 值）。</span><span class="sxs-lookup"><span data-stu-id="a9854-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="a9854-106">下列 XPath 值也會提供透過 hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx)程式庫。</span><span class="sxs-lookup"><span data-stu-id="a9854-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="a9854-107">在模擬器中執行的應用程式</span><span class="sxs-lookup"><span data-stu-id="a9854-107">App running in emulator</span></span>
<span data-ttu-id="a9854-108">指出 hello 模擬器中執行該 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a9854-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="a9854-109">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-109">Type</span></span> | <span data-ttu-id="a9854-110">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-111">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-111">XPath</span></span> |<span data-ttu-id="a9854-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="a9854-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="a9854-113">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-113">Code</span></span> |<span data-ttu-id="a9854-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="a9854-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="a9854-115">部署 ID</span><span class="sxs-lookup"><span data-stu-id="a9854-115">Deployment ID</span></span>
<span data-ttu-id="a9854-116">擷取 hello hello 執行個體的部署識別碼。</span><span class="sxs-lookup"><span data-stu-id="a9854-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="a9854-117">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-117">Type</span></span> | <span data-ttu-id="a9854-118">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-119">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-119">XPath</span></span> |<span data-ttu-id="a9854-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="a9854-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="a9854-121">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-121">Code</span></span> |<span data-ttu-id="a9854-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="a9854-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="a9854-123">角色 ID</span><span class="sxs-lookup"><span data-stu-id="a9854-123">Role ID</span></span>
<span data-ttu-id="a9854-124">擷取 hello 目前角色執行個體的識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="a9854-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="a9854-125">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-125">Type</span></span> | <span data-ttu-id="a9854-126">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-127">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-127">XPath</span></span> |<span data-ttu-id="a9854-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="a9854-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="a9854-129">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-129">Code</span></span> |<span data-ttu-id="a9854-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="a9854-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="a9854-131">更新網站</span><span class="sxs-lookup"><span data-stu-id="a9854-131">Update domain</span></span>
<span data-ttu-id="a9854-132">擷取 hello hello 執行個體的更新網域。</span><span class="sxs-lookup"><span data-stu-id="a9854-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="a9854-133">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-133">Type</span></span> | <span data-ttu-id="a9854-134">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-135">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-135">XPath</span></span> |<span data-ttu-id="a9854-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="a9854-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="a9854-137">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-137">Code</span></span> |<span data-ttu-id="a9854-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="a9854-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="a9854-139">容錯網域</span><span class="sxs-lookup"><span data-stu-id="a9854-139">Fault domain</span></span>
<span data-ttu-id="a9854-140">擷取 hello hello 執行個體的容錯網域。</span><span class="sxs-lookup"><span data-stu-id="a9854-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="a9854-141">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-141">Type</span></span> | <span data-ttu-id="a9854-142">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-143">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-143">XPath</span></span> |<span data-ttu-id="a9854-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="a9854-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="a9854-145">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-145">Code</span></span> |<span data-ttu-id="a9854-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="a9854-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="a9854-147">角色名稱</span><span class="sxs-lookup"><span data-stu-id="a9854-147">Role name</span></span>
<span data-ttu-id="a9854-148">擷取 hello hello 執行個體的角色名稱。</span><span class="sxs-lookup"><span data-stu-id="a9854-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="a9854-149">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-149">Type</span></span> | <span data-ttu-id="a9854-150">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-151">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-151">XPath</span></span> |<span data-ttu-id="a9854-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="a9854-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="a9854-153">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-153">Code</span></span> |<span data-ttu-id="a9854-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="a9854-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="a9854-155">組態設定</span><span class="sxs-lookup"><span data-stu-id="a9854-155">Config setting</span></span>
<span data-ttu-id="a9854-156">Hello 擷取 hello 值會指定組態設定。</span><span class="sxs-lookup"><span data-stu-id="a9854-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="a9854-157">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-157">Type</span></span> | <span data-ttu-id="a9854-158">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-159">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-159">XPath</span></span> |<span data-ttu-id="a9854-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="a9854-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="a9854-161">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-161">Code</span></span> |<span data-ttu-id="a9854-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="a9854-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="a9854-163">本機儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="a9854-163">Local storage path</span></span>
<span data-ttu-id="a9854-164">擷取 hello hello 執行個體的本機儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="a9854-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="a9854-165">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-165">Type</span></span> | <span data-ttu-id="a9854-166">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-167">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-167">XPath</span></span> |<span data-ttu-id="a9854-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="a9854-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="a9854-169">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-169">Code</span></span> |<span data-ttu-id="a9854-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="a9854-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="a9854-171">本機儲存體大小</span><span class="sxs-lookup"><span data-stu-id="a9854-171">Local storage size</span></span>
<span data-ttu-id="a9854-172">擷取 hello hello hello 執行個體的本機儲存體大小。</span><span class="sxs-lookup"><span data-stu-id="a9854-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="a9854-173">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-173">Type</span></span> | <span data-ttu-id="a9854-174">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-175">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-175">XPath</span></span> |<span data-ttu-id="a9854-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="a9854-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="a9854-177">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-177">Code</span></span> |<span data-ttu-id="a9854-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="a9854-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="a9854-179">端點通訊協定</span><span class="sxs-lookup"><span data-stu-id="a9854-179">Endpoint protocol</span></span>
<span data-ttu-id="a9854-180">擷取 hello hello 執行個體的端點通訊協定。</span><span class="sxs-lookup"><span data-stu-id="a9854-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="a9854-181">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-181">Type</span></span> | <span data-ttu-id="a9854-182">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-183">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-183">XPath</span></span> |<span data-ttu-id="a9854-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="a9854-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="a9854-185">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-185">Code</span></span> |<span data-ttu-id="a9854-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="a9854-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="a9854-187">端點 IP</span><span class="sxs-lookup"><span data-stu-id="a9854-187">Endpoint IP</span></span>
<span data-ttu-id="a9854-188">取得 hello 指定端點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a9854-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="a9854-189">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-189">Type</span></span> | <span data-ttu-id="a9854-190">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-191">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-191">XPath</span></span> |<span data-ttu-id="a9854-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="a9854-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="a9854-193">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-193">Code</span></span> |<span data-ttu-id="a9854-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="a9854-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="a9854-195">端點連接埠</span><span class="sxs-lookup"><span data-stu-id="a9854-195">Endpoint port</span></span>
<span data-ttu-id="a9854-196">擷取 hello hello 執行個體的端點通訊埠。</span><span class="sxs-lookup"><span data-stu-id="a9854-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="a9854-197">類型</span><span class="sxs-lookup"><span data-stu-id="a9854-197">Type</span></span> | <span data-ttu-id="a9854-198">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="a9854-199">XPath</span><span class="sxs-lookup"><span data-stu-id="a9854-199">XPath</span></span> |<span data-ttu-id="a9854-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="a9854-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="a9854-201">代碼</span><span class="sxs-lookup"><span data-stu-id="a9854-201">Code</span></span> |<span data-ttu-id="a9854-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="a9854-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="a9854-203">範例</span><span class="sxs-lookup"><span data-stu-id="a9854-203">Example</span></span>
<span data-ttu-id="a9854-204">以下是使用名為的環境變數建立啟動工作的背景工作角色的範例`TestIsEmulated`設定 toohello [ @emulated xpath 值](#app-running-in-emulator)。</span><span class="sxs-lookup"><span data-stu-id="a9854-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="a9854-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a9854-205">Next steps</span></span>
<span data-ttu-id="a9854-206">深入了解 hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg)檔案。</span><span class="sxs-lookup"><span data-stu-id="a9854-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="a9854-207">建立 [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) 封裝。</span><span class="sxs-lookup"><span data-stu-id="a9854-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="a9854-208">為角色啟用 [遠端桌面](cloud-services-role-enable-remote-desktop.md) 。</span><span class="sxs-lookup"><span data-stu-id="a9854-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

