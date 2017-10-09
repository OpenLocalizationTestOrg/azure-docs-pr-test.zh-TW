---
title: "aaaPublish WebApplicationWebSite （Windows PowerShell 指令碼） |Microsoft 文件"
description: "了解如何 toopublish web 專案 tooan Azure 網站。 如果不存在，此指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="314bc-104">Publish-WebApplicationWebSite (Windows PowerShell 指令碼)</span><span class="sxs-lookup"><span data-stu-id="314bc-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="314bc-105">語法</span><span class="sxs-lookup"><span data-stu-id="314bc-105">Syntax</span></span>
<span data-ttu-id="314bc-106">發行的 web 專案 tooan Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="314bc-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="314bc-107">若不存在，hello 指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="314bc-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="314bc-108">組態</span><span class="sxs-lookup"><span data-stu-id="314bc-108">Configuration</span></span>
<span data-ttu-id="314bc-109">hello 路徑 toohello JSON 組態檔，描述 hello 部署的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="314bc-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="314bc-110">參數</span><span class="sxs-lookup"><span data-stu-id="314bc-110">Parameter</span></span> | <span data-ttu-id="314bc-111">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="314bc-112">別名</span><span class="sxs-lookup"><span data-stu-id="314bc-112">Aliases</span></span> |<span data-ttu-id="314bc-113">無</span><span class="sxs-lookup"><span data-stu-id="314bc-113">none</span></span> |
| <span data-ttu-id="314bc-114">必要？</span><span class="sxs-lookup"><span data-stu-id="314bc-114">Required?</span></span> |<span data-ttu-id="314bc-115">true</span><span class="sxs-lookup"><span data-stu-id="314bc-115">true</span></span> |
| <span data-ttu-id="314bc-116">位置</span><span class="sxs-lookup"><span data-stu-id="314bc-116">Position</span></span> |<span data-ttu-id="314bc-117">已命名</span><span class="sxs-lookup"><span data-stu-id="314bc-117">named</span></span> |
| <span data-ttu-id="314bc-118">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-118">Default value</span></span> |<span data-ttu-id="314bc-119">無</span><span class="sxs-lookup"><span data-stu-id="314bc-119">none</span></span> |
| <span data-ttu-id="314bc-120">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="314bc-120">Accept pipeline input?</span></span> |<span data-ttu-id="314bc-121">false</span><span class="sxs-lookup"><span data-stu-id="314bc-121">false</span></span> |
| <span data-ttu-id="314bc-122">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="314bc-122">Accept wildcard characters?</span></span> |<span data-ttu-id="314bc-123">false</span><span class="sxs-lookup"><span data-stu-id="314bc-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="314bc-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="314bc-124">SubscriptionName</span></span>
<span data-ttu-id="314bc-125">hello hello 想 toocreate hello 網站中的 Azure 訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="314bc-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="314bc-126">參數</span><span class="sxs-lookup"><span data-stu-id="314bc-126">Parameter</span></span> | <span data-ttu-id="314bc-127">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="314bc-128">別名</span><span class="sxs-lookup"><span data-stu-id="314bc-128">Aliases</span></span> |<span data-ttu-id="314bc-129">無</span><span class="sxs-lookup"><span data-stu-id="314bc-129">none</span></span> |
| <span data-ttu-id="314bc-130">必要？</span><span class="sxs-lookup"><span data-stu-id="314bc-130">Required?</span></span> |<span data-ttu-id="314bc-131">false</span><span class="sxs-lookup"><span data-stu-id="314bc-131">false</span></span> |
| <span data-ttu-id="314bc-132">位置</span><span class="sxs-lookup"><span data-stu-id="314bc-132">Position</span></span> |<span data-ttu-id="314bc-133">已命名</span><span class="sxs-lookup"><span data-stu-id="314bc-133">named</span></span> |
| <span data-ttu-id="314bc-134">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-134">Default value</span></span> |<span data-ttu-id="314bc-135">無</span><span class="sxs-lookup"><span data-stu-id="314bc-135">none</span></span> |
| <span data-ttu-id="314bc-136">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="314bc-136">Accept pipeline input?</span></span> |<span data-ttu-id="314bc-137">false</span><span class="sxs-lookup"><span data-stu-id="314bc-137">false</span></span> |
| <span data-ttu-id="314bc-138">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="314bc-138">Accept wildcard characters?</span></span> |<span data-ttu-id="314bc-139">false</span><span class="sxs-lookup"><span data-stu-id="314bc-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="314bc-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="314bc-140">WebDeployPackage</span></span>
<span data-ttu-id="314bc-141">hello 路徑 toohello web 部署套件 toopublish toohello 網站。</span><span class="sxs-lookup"><span data-stu-id="314bc-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="314bc-142">您可以使用 Visual Studio 中的 hello 發行網站精靈來建立此套件。</span><span class="sxs-lookup"><span data-stu-id="314bc-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="314bc-143">如需詳細資訊，請參閱 [開始使用 Azure 雲端服務和 ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089)。</span><span class="sxs-lookup"><span data-stu-id="314bc-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="314bc-144">參數</span><span class="sxs-lookup"><span data-stu-id="314bc-144">Parameter</span></span> | <span data-ttu-id="314bc-145">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="314bc-146">別名</span><span class="sxs-lookup"><span data-stu-id="314bc-146">Aliases</span></span> |<span data-ttu-id="314bc-147">無</span><span class="sxs-lookup"><span data-stu-id="314bc-147">none</span></span> |
| <span data-ttu-id="314bc-148">必要？</span><span class="sxs-lookup"><span data-stu-id="314bc-148">Required?</span></span> |<span data-ttu-id="314bc-149">false</span><span class="sxs-lookup"><span data-stu-id="314bc-149">false</span></span> |
| <span data-ttu-id="314bc-150">位置</span><span class="sxs-lookup"><span data-stu-id="314bc-150">Position</span></span> |<span data-ttu-id="314bc-151">已命名</span><span class="sxs-lookup"><span data-stu-id="314bc-151">named</span></span> |
| <span data-ttu-id="314bc-152">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-152">Default value</span></span> |<span data-ttu-id="314bc-153">無</span><span class="sxs-lookup"><span data-stu-id="314bc-153">none</span></span> |
| <span data-ttu-id="314bc-154">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="314bc-154">Accept pipeline input?</span></span> |<span data-ttu-id="314bc-155">false</span><span class="sxs-lookup"><span data-stu-id="314bc-155">false</span></span> |
| <span data-ttu-id="314bc-156">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="314bc-156">Accept wildcard characters?</span></span> |<span data-ttu-id="314bc-157">false</span><span class="sxs-lookup"><span data-stu-id="314bc-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="314bc-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="314bc-158">DatabaseServerPassword</span></span>
<span data-ttu-id="314bc-159">hello 使用者名稱和密碼 hello Azure 中的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="314bc-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="314bc-160">參數</span><span class="sxs-lookup"><span data-stu-id="314bc-160">Parameter</span></span> | <span data-ttu-id="314bc-161">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="314bc-162">別名</span><span class="sxs-lookup"><span data-stu-id="314bc-162">Aliases</span></span> |<span data-ttu-id="314bc-163">無</span><span class="sxs-lookup"><span data-stu-id="314bc-163">none</span></span> |
| <span data-ttu-id="314bc-164">必要？</span><span class="sxs-lookup"><span data-stu-id="314bc-164">Required?</span></span> |<span data-ttu-id="314bc-165">false</span><span class="sxs-lookup"><span data-stu-id="314bc-165">false</span></span> |
| <span data-ttu-id="314bc-166">位置</span><span class="sxs-lookup"><span data-stu-id="314bc-166">Position</span></span> |<span data-ttu-id="314bc-167">已命名</span><span class="sxs-lookup"><span data-stu-id="314bc-167">named</span></span> |
| <span data-ttu-id="314bc-168">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-168">Default value</span></span> |<span data-ttu-id="314bc-169">無</span><span class="sxs-lookup"><span data-stu-id="314bc-169">none</span></span> |
| <span data-ttu-id="314bc-170">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="314bc-170">Accept pipeline input?</span></span> |<span data-ttu-id="314bc-171">false</span><span class="sxs-lookup"><span data-stu-id="314bc-171">false</span></span> |
| <span data-ttu-id="314bc-172">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="314bc-172">Accept wildcard characters?</span></span> |<span data-ttu-id="314bc-173">false</span><span class="sxs-lookup"><span data-stu-id="314bc-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="314bc-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="314bc-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="314bc-175">如果為 true，列印訊息從 hello 指令碼 toohello 輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="314bc-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="314bc-176">參數</span><span class="sxs-lookup"><span data-stu-id="314bc-176">Parameter</span></span> | <span data-ttu-id="314bc-177">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="314bc-178">別名</span><span class="sxs-lookup"><span data-stu-id="314bc-178">Aliases</span></span> |<span data-ttu-id="314bc-179">無</span><span class="sxs-lookup"><span data-stu-id="314bc-179">none</span></span> |
| <span data-ttu-id="314bc-180">必要？</span><span class="sxs-lookup"><span data-stu-id="314bc-180">Required?</span></span> |<span data-ttu-id="314bc-181">false</span><span class="sxs-lookup"><span data-stu-id="314bc-181">false</span></span> |
| <span data-ttu-id="314bc-182">位置</span><span class="sxs-lookup"><span data-stu-id="314bc-182">Position</span></span> |<span data-ttu-id="314bc-183">已命名</span><span class="sxs-lookup"><span data-stu-id="314bc-183">named</span></span> |
| <span data-ttu-id="314bc-184">預設值</span><span class="sxs-lookup"><span data-stu-id="314bc-184">Default value</span></span> |<span data-ttu-id="314bc-185">false</span><span class="sxs-lookup"><span data-stu-id="314bc-185">false</span></span> |
| <span data-ttu-id="314bc-186">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="314bc-186">Accept pipeline input?</span></span> |<span data-ttu-id="314bc-187">false</span><span class="sxs-lookup"><span data-stu-id="314bc-187">false</span></span> |
| <span data-ttu-id="314bc-188">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="314bc-188">Accept wildcard characters?</span></span> |<span data-ttu-id="314bc-189">false</span><span class="sxs-lookup"><span data-stu-id="314bc-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="314bc-190">備註</span><span class="sxs-lookup"><span data-stu-id="314bc-190">Remarks</span></span>
<span data-ttu-id="314bc-191">如需如何 toouse hello 指令碼 toocreate 開發人員和測試環境，請參閱完整說明[使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](vs-azure-tools-publishing-using-powershell-scripts.md)。</span><span class="sxs-lookup"><span data-stu-id="314bc-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="314bc-192">hello JSON 組態檔指定部署 toobe hello 的細節。</span><span class="sxs-lookup"><span data-stu-id="314bc-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="314bc-193">其中包括建立 hello 專案，例如 hello 名稱和 hello 網站的使用者名稱時指定的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="314bc-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="314bc-194">它也包含 hello 資料庫 tooprovision，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="314bc-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="314bc-195">下列程式碼的 hello 顯示 JSON 組態檔範例：</span><span class="sxs-lookup"><span data-stu-id="314bc-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="314bc-196">您可以編輯 hello JSON 組態檔 toochange 部署的內容。</span><span class="sxs-lookup"><span data-stu-id="314bc-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="314bc-197">網站區段為必要項，但 hello 資料庫區段為選擇性。</span><span class="sxs-lookup"><span data-stu-id="314bc-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="314bc-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="314bc-198">Next steps</span></span>
<span data-ttu-id="314bc-199">如需詳細資訊，請參閱 [Publish-WebApplicationVM (Windows PowerShell 指令碼)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="314bc-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

