---
title: "aaaPublish WebApplicationVM |Microsoft 文件"
description: "深入了解如何 toodeploy web 應用程式 tooa 虛擬機器。 如果不存在，此指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="e0957-104">Publish-WebApplicationVM (Windows PowerShell 指令碼)</span><span class="sxs-lookup"><span data-stu-id="e0957-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="e0957-105">部署 web 應用程式 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0957-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="e0957-106">若不存在，hello 指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e0957-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="e0957-107">組態</span><span class="sxs-lookup"><span data-stu-id="e0957-107">Configuration</span></span>
<span data-ttu-id="e0957-108">hello 路徑 toohello JSON 組態檔，描述 hello 部署的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e0957-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="e0957-109">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-109">Aliases</span></span> | <span data-ttu-id="e0957-110">無</span><span class="sxs-lookup"><span data-stu-id="e0957-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-111">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-111">Required?</span></span> |<span data-ttu-id="e0957-112">true</span><span class="sxs-lookup"><span data-stu-id="e0957-112">true</span></span> |
| <span data-ttu-id="e0957-113">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-113">Position</span></span> |<span data-ttu-id="e0957-114">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-114">named</span></span> |
| <span data-ttu-id="e0957-115">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-115">Default value</span></span> |<span data-ttu-id="e0957-116">無</span><span class="sxs-lookup"><span data-stu-id="e0957-116">none</span></span> |
| <span data-ttu-id="e0957-117">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-117">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-118">false</span><span class="sxs-lookup"><span data-stu-id="e0957-118">false</span></span> |
| <span data-ttu-id="e0957-119">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-119">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-120">false</span><span class="sxs-lookup"><span data-stu-id="e0957-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="e0957-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="e0957-121">SubscriptionName</span></span>
<span data-ttu-id="e0957-122">hello 名稱 hello 想 toocreate hello 虛擬機器的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e0957-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="e0957-123">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-123">Aliases</span></span> | <span data-ttu-id="e0957-124">無</span><span class="sxs-lookup"><span data-stu-id="e0957-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-125">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-125">Required?</span></span> |<span data-ttu-id="e0957-126">false</span><span class="sxs-lookup"><span data-stu-id="e0957-126">false</span></span> |
| <span data-ttu-id="e0957-127">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-127">Position</span></span> |<span data-ttu-id="e0957-128">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-128">named</span></span> |
| <span data-ttu-id="e0957-129">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-129">Default value</span></span> |<span data-ttu-id="e0957-130">在 hello 訂用帳戶檔案中使用 hello 第一個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e0957-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="e0957-131">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-131">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-132">false</span><span class="sxs-lookup"><span data-stu-id="e0957-132">false</span></span> |
| <span data-ttu-id="e0957-133">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-133">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-134">false</span><span class="sxs-lookup"><span data-stu-id="e0957-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="e0957-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="e0957-135">WebDeployPackage</span></span>
<span data-ttu-id="e0957-136">hello 路徑 toohello web 部署套件 toopublish toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0957-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="e0957-137">您可以使用 Visual Studio 中的 hello 發行網站精靈來建立此套件。</span><span class="sxs-lookup"><span data-stu-id="e0957-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="e0957-138">請參閱 [如何：在 Visual Studio 中建立 Web 部署封裝](https://msdn.microsoft.com/library/dd465323.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e0957-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="e0957-139">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-139">Aliases</span></span> | <span data-ttu-id="e0957-140">無</span><span class="sxs-lookup"><span data-stu-id="e0957-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-141">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-141">Required?</span></span> |<span data-ttu-id="e0957-142">false</span><span class="sxs-lookup"><span data-stu-id="e0957-142">false</span></span> |
| <span data-ttu-id="e0957-143">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-143">Position</span></span> |<span data-ttu-id="e0957-144">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-144">named</span></span> |
| <span data-ttu-id="e0957-145">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-145">Default value</span></span> |<span data-ttu-id="e0957-146">無</span><span class="sxs-lookup"><span data-stu-id="e0957-146">none</span></span> |
| <span data-ttu-id="e0957-147">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-147">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-148">false</span><span class="sxs-lookup"><span data-stu-id="e0957-148">false</span></span> |
| <span data-ttu-id="e0957-149">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-149">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-150">false</span><span class="sxs-lookup"><span data-stu-id="e0957-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="e0957-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="e0957-151">AllowUntrusted</span></span>
<span data-ttu-id="e0957-152">如果為 true，允許 hello 使用的不由受信任的根授權單位簽署的憑證。</span><span class="sxs-lookup"><span data-stu-id="e0957-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="e0957-153">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-153">Aliases</span></span> | <span data-ttu-id="e0957-154">無</span><span class="sxs-lookup"><span data-stu-id="e0957-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-155">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-155">Required?</span></span> |<span data-ttu-id="e0957-156">false</span><span class="sxs-lookup"><span data-stu-id="e0957-156">false</span></span> |
| <span data-ttu-id="e0957-157">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-157">Position</span></span> |<span data-ttu-id="e0957-158">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-158">named</span></span> |
| <span data-ttu-id="e0957-159">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-159">Default value</span></span> |<span data-ttu-id="e0957-160">false</span><span class="sxs-lookup"><span data-stu-id="e0957-160">false</span></span> |
| <span data-ttu-id="e0957-161">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-161">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-162">false</span><span class="sxs-lookup"><span data-stu-id="e0957-162">false</span></span> |
| <span data-ttu-id="e0957-163">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-163">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-164">false</span><span class="sxs-lookup"><span data-stu-id="e0957-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="e0957-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="e0957-165">VMPassword</span></span>
<span data-ttu-id="e0957-166">hello hello 虛擬機器帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="e0957-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="e0957-167">範例： VMPassword @{Name ="admin";密碼 ="password"}</span><span class="sxs-lookup"><span data-stu-id="e0957-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="e0957-168">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-168">Aliases</span></span> | <span data-ttu-id="e0957-169">無</span><span class="sxs-lookup"><span data-stu-id="e0957-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-170">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-170">Required?</span></span> |<span data-ttu-id="e0957-171">false</span><span class="sxs-lookup"><span data-stu-id="e0957-171">false</span></span> |
| <span data-ttu-id="e0957-172">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-172">Position</span></span> |<span data-ttu-id="e0957-173">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-173">named</span></span> |
| <span data-ttu-id="e0957-174">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-174">Default value</span></span> |<span data-ttu-id="e0957-175">無</span><span class="sxs-lookup"><span data-stu-id="e0957-175">none</span></span> |
| <span data-ttu-id="e0957-176">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-176">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-177">false</span><span class="sxs-lookup"><span data-stu-id="e0957-177">false</span></span> |
| <span data-ttu-id="e0957-178">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-178">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-179">false</span><span class="sxs-lookup"><span data-stu-id="e0957-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="e0957-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="e0957-180">DatabaseServerPassword</span></span>
<span data-ttu-id="e0957-181">在 Azure 中的 hello SQL database 的 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="e0957-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="e0957-182">範例： DatabaseServerPassword @{Name ="admin";密碼 ="password"}</span><span class="sxs-lookup"><span data-stu-id="e0957-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="e0957-183">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-183">Aliases</span></span> | <span data-ttu-id="e0957-184">無</span><span class="sxs-lookup"><span data-stu-id="e0957-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-185">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-185">Required?</span></span> |<span data-ttu-id="e0957-186">false</span><span class="sxs-lookup"><span data-stu-id="e0957-186">false</span></span> |
| <span data-ttu-id="e0957-187">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-187">Position</span></span> |<span data-ttu-id="e0957-188">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-188">named</span></span> |
| <span data-ttu-id="e0957-189">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-189">Default value</span></span> |<span data-ttu-id="e0957-190">無</span><span class="sxs-lookup"><span data-stu-id="e0957-190">none</span></span> |
| <span data-ttu-id="e0957-191">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-191">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-192">false</span><span class="sxs-lookup"><span data-stu-id="e0957-192">false</span></span> |
| <span data-ttu-id="e0957-193">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-193">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-194">false</span><span class="sxs-lookup"><span data-stu-id="e0957-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="e0957-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="e0957-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="e0957-196">如果為 true，列印訊息從 hello 指令碼 toohello 輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="e0957-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="e0957-197">別名</span><span class="sxs-lookup"><span data-stu-id="e0957-197">Aliases</span></span> | <span data-ttu-id="e0957-198">無</span><span class="sxs-lookup"><span data-stu-id="e0957-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="e0957-199">必要？</span><span class="sxs-lookup"><span data-stu-id="e0957-199">Required?</span></span> |<span data-ttu-id="e0957-200">false</span><span class="sxs-lookup"><span data-stu-id="e0957-200">false</span></span> |
| <span data-ttu-id="e0957-201">位置</span><span class="sxs-lookup"><span data-stu-id="e0957-201">Position</span></span> |<span data-ttu-id="e0957-202">已命名</span><span class="sxs-lookup"><span data-stu-id="e0957-202">named</span></span> |
| <span data-ttu-id="e0957-203">預設值</span><span class="sxs-lookup"><span data-stu-id="e0957-203">Default value</span></span> |<span data-ttu-id="e0957-204">false</span><span class="sxs-lookup"><span data-stu-id="e0957-204">false</span></span> |
| <span data-ttu-id="e0957-205">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="e0957-205">Accept pipeline input?</span></span> |<span data-ttu-id="e0957-206">false</span><span class="sxs-lookup"><span data-stu-id="e0957-206">false</span></span> |
| <span data-ttu-id="e0957-207">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="e0957-207">Accept wildcard characters?</span></span> |<span data-ttu-id="e0957-208">false</span><span class="sxs-lookup"><span data-stu-id="e0957-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="e0957-209">備註</span><span class="sxs-lookup"><span data-stu-id="e0957-209">Remarks</span></span>
<span data-ttu-id="e0957-210">如需如何 toouse hello 指令碼 toocreate 開發人員和測試環境，請參閱完整說明[使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](vs-azure-tools-publishing-using-powershell-scripts.md)。</span><span class="sxs-lookup"><span data-stu-id="e0957-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="e0957-211">hello JSON 組態檔指定部署 toobe hello 的細節。</span><span class="sxs-lookup"><span data-stu-id="e0957-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="e0957-212">其中包括建立 hello 專案，例如 hello、 同質群組、 VHD 映像的名稱和大小 hello 虛擬機器時指定的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="e0957-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="e0957-213">它也包括 hello hello 資料庫 tooprovision，hello 虛擬機器上的端點，如果有的話，，和 web 部署參數。</span><span class="sxs-lookup"><span data-stu-id="e0957-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="e0957-214">下列程式碼的 hello 顯示 JSON 組態檔範例：</span><span class="sxs-lookup"><span data-stu-id="e0957-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="e0957-215">您可以編輯 hello JSON 組態檔 toochange 要佈建。</span><span class="sxs-lookup"><span data-stu-id="e0957-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="e0957-216">虛擬機器和雲端服務是必要的但是 hello 資料庫區段為選擇性。</span><span class="sxs-lookup"><span data-stu-id="e0957-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

