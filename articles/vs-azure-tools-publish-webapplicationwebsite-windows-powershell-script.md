---
title: "Publish-WebApplicationWebSite (Windows PowerShell 指令碼) | Microsoft Docs"
description: "了解如何將 Web 專案發佈至 Azure 網站。 此指令碼會在您的 Azure 訂用帳戶中建立所需的資源 (如果它們不存在)。"
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
ms.openlocfilehash: 07d21b7ce6cd8aee1cff704d316e7a2ca8c00437
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="cb05e-104">Publish-WebApplicationWebSite (Windows PowerShell 指令碼)</span><span class="sxs-lookup"><span data-stu-id="cb05e-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="cb05e-105">語法</span><span class="sxs-lookup"><span data-stu-id="cb05e-105">Syntax</span></span>
<span data-ttu-id="cb05e-106">將 Web 專案發佈至 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="cb05e-106">Publishes a web project to an Azure website.</span></span> <span data-ttu-id="cb05e-107">指令碼會在您的 Azure 訂用帳戶中建立所需的資源 (如果它們不存在)。</span><span class="sxs-lookup"><span data-stu-id="cb05e-107">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="cb05e-108">組態</span><span class="sxs-lookup"><span data-stu-id="cb05e-108">Configuration</span></span>
<span data-ttu-id="cb05e-109">描述部署詳細資訊的 JSON 組態檔路徑。</span><span class="sxs-lookup"><span data-stu-id="cb05e-109">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="cb05e-110">參數</span><span class="sxs-lookup"><span data-stu-id="cb05e-110">Parameter</span></span> | <span data-ttu-id="cb05e-111">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="cb05e-112">別名</span><span class="sxs-lookup"><span data-stu-id="cb05e-112">Aliases</span></span> |<span data-ttu-id="cb05e-113">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-113">none</span></span> |
| <span data-ttu-id="cb05e-114">必要？</span><span class="sxs-lookup"><span data-stu-id="cb05e-114">Required?</span></span> |<span data-ttu-id="cb05e-115">true</span><span class="sxs-lookup"><span data-stu-id="cb05e-115">true</span></span> |
| <span data-ttu-id="cb05e-116">位置</span><span class="sxs-lookup"><span data-stu-id="cb05e-116">Position</span></span> |<span data-ttu-id="cb05e-117">已命名</span><span class="sxs-lookup"><span data-stu-id="cb05e-117">named</span></span> |
| <span data-ttu-id="cb05e-118">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-118">Default value</span></span> |<span data-ttu-id="cb05e-119">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-119">none</span></span> |
| <span data-ttu-id="cb05e-120">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="cb05e-120">Accept pipeline input?</span></span> |<span data-ttu-id="cb05e-121">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-121">false</span></span> |
| <span data-ttu-id="cb05e-122">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="cb05e-122">Accept wildcard characters?</span></span> |<span data-ttu-id="cb05e-123">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="cb05e-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="cb05e-124">SubscriptionName</span></span>
<span data-ttu-id="cb05e-125">您要建立網站的 Azure 訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cb05e-125">The name of the Azure subscription that you want to create the website in.</span></span>

| <span data-ttu-id="cb05e-126">參數</span><span class="sxs-lookup"><span data-stu-id="cb05e-126">Parameter</span></span> | <span data-ttu-id="cb05e-127">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="cb05e-128">別名</span><span class="sxs-lookup"><span data-stu-id="cb05e-128">Aliases</span></span> |<span data-ttu-id="cb05e-129">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-129">none</span></span> |
| <span data-ttu-id="cb05e-130">必要？</span><span class="sxs-lookup"><span data-stu-id="cb05e-130">Required?</span></span> |<span data-ttu-id="cb05e-131">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-131">false</span></span> |
| <span data-ttu-id="cb05e-132">位置</span><span class="sxs-lookup"><span data-stu-id="cb05e-132">Position</span></span> |<span data-ttu-id="cb05e-133">已命名</span><span class="sxs-lookup"><span data-stu-id="cb05e-133">named</span></span> |
| <span data-ttu-id="cb05e-134">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-134">Default value</span></span> |<span data-ttu-id="cb05e-135">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-135">none</span></span> |
| <span data-ttu-id="cb05e-136">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="cb05e-136">Accept pipeline input?</span></span> |<span data-ttu-id="cb05e-137">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-137">false</span></span> |
| <span data-ttu-id="cb05e-138">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="cb05e-138">Accept wildcard characters?</span></span> |<span data-ttu-id="cb05e-139">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="cb05e-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="cb05e-140">WebDeployPackage</span></span>
<span data-ttu-id="cb05e-141">要發佈至網站的 Web 部署封裝路徑。</span><span class="sxs-lookup"><span data-stu-id="cb05e-141">The path to the web deployment package to publish to the website.</span></span> <span data-ttu-id="cb05e-142">您可以使用 Visual Studio 的 [發佈 Web] 精靈來建立此封裝。</span><span class="sxs-lookup"><span data-stu-id="cb05e-142">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="cb05e-143">如需詳細資訊，請參閱 [開始使用 Azure 雲端服務和 ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089)。</span><span class="sxs-lookup"><span data-stu-id="cb05e-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="cb05e-144">參數</span><span class="sxs-lookup"><span data-stu-id="cb05e-144">Parameter</span></span> | <span data-ttu-id="cb05e-145">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="cb05e-146">別名</span><span class="sxs-lookup"><span data-stu-id="cb05e-146">Aliases</span></span> |<span data-ttu-id="cb05e-147">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-147">none</span></span> |
| <span data-ttu-id="cb05e-148">必要？</span><span class="sxs-lookup"><span data-stu-id="cb05e-148">Required?</span></span> |<span data-ttu-id="cb05e-149">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-149">false</span></span> |
| <span data-ttu-id="cb05e-150">位置</span><span class="sxs-lookup"><span data-stu-id="cb05e-150">Position</span></span> |<span data-ttu-id="cb05e-151">已命名</span><span class="sxs-lookup"><span data-stu-id="cb05e-151">named</span></span> |
| <span data-ttu-id="cb05e-152">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-152">Default value</span></span> |<span data-ttu-id="cb05e-153">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-153">none</span></span> |
| <span data-ttu-id="cb05e-154">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="cb05e-154">Accept pipeline input?</span></span> |<span data-ttu-id="cb05e-155">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-155">false</span></span> |
| <span data-ttu-id="cb05e-156">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="cb05e-156">Accept wildcard characters?</span></span> |<span data-ttu-id="cb05e-157">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="cb05e-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="cb05e-158">DatabaseServerPassword</span></span>
<span data-ttu-id="cb05e-159">在 Azure 中 SQL Database 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="cb05e-159">The username and password for the SQL database in Azure.</span></span>

| <span data-ttu-id="cb05e-160">參數</span><span class="sxs-lookup"><span data-stu-id="cb05e-160">Parameter</span></span> | <span data-ttu-id="cb05e-161">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="cb05e-162">別名</span><span class="sxs-lookup"><span data-stu-id="cb05e-162">Aliases</span></span> |<span data-ttu-id="cb05e-163">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-163">none</span></span> |
| <span data-ttu-id="cb05e-164">必要？</span><span class="sxs-lookup"><span data-stu-id="cb05e-164">Required?</span></span> |<span data-ttu-id="cb05e-165">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-165">false</span></span> |
| <span data-ttu-id="cb05e-166">位置</span><span class="sxs-lookup"><span data-stu-id="cb05e-166">Position</span></span> |<span data-ttu-id="cb05e-167">已命名</span><span class="sxs-lookup"><span data-stu-id="cb05e-167">named</span></span> |
| <span data-ttu-id="cb05e-168">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-168">Default value</span></span> |<span data-ttu-id="cb05e-169">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-169">none</span></span> |
| <span data-ttu-id="cb05e-170">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="cb05e-170">Accept pipeline input?</span></span> |<span data-ttu-id="cb05e-171">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-171">false</span></span> |
| <span data-ttu-id="cb05e-172">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="cb05e-172">Accept wildcard characters?</span></span> |<span data-ttu-id="cb05e-173">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="cb05e-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="cb05e-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="cb05e-175">如果為 true，將訊息從指令碼列印至輸出資料流。</span><span class="sxs-lookup"><span data-stu-id="cb05e-175">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="cb05e-176">參數</span><span class="sxs-lookup"><span data-stu-id="cb05e-176">Parameter</span></span> | <span data-ttu-id="cb05e-177">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="cb05e-178">別名</span><span class="sxs-lookup"><span data-stu-id="cb05e-178">Aliases</span></span> |<span data-ttu-id="cb05e-179">無</span><span class="sxs-lookup"><span data-stu-id="cb05e-179">none</span></span> |
| <span data-ttu-id="cb05e-180">必要？</span><span class="sxs-lookup"><span data-stu-id="cb05e-180">Required?</span></span> |<span data-ttu-id="cb05e-181">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-181">false</span></span> |
| <span data-ttu-id="cb05e-182">位置</span><span class="sxs-lookup"><span data-stu-id="cb05e-182">Position</span></span> |<span data-ttu-id="cb05e-183">已命名</span><span class="sxs-lookup"><span data-stu-id="cb05e-183">named</span></span> |
| <span data-ttu-id="cb05e-184">預設值</span><span class="sxs-lookup"><span data-stu-id="cb05e-184">Default value</span></span> |<span data-ttu-id="cb05e-185">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-185">false</span></span> |
| <span data-ttu-id="cb05e-186">接受管線輸入？</span><span class="sxs-lookup"><span data-stu-id="cb05e-186">Accept pipeline input?</span></span> |<span data-ttu-id="cb05e-187">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-187">false</span></span> |
| <span data-ttu-id="cb05e-188">接受萬用字元？</span><span class="sxs-lookup"><span data-stu-id="cb05e-188">Accept wildcard characters?</span></span> |<span data-ttu-id="cb05e-189">false</span><span class="sxs-lookup"><span data-stu-id="cb05e-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="cb05e-190">備註</span><span class="sxs-lookup"><span data-stu-id="cb05e-190">Remarks</span></span>
<span data-ttu-id="cb05e-191">如需如何使用指令碼來建立開發和測試環境的完整說明，請參閱 [使用 Windows PowerShell 指令碼來發佈至開發和測試環境](vs-azure-tools-publishing-using-powershell-scripts.md)。</span><span class="sxs-lookup"><span data-stu-id="cb05e-191">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="cb05e-192">JSON 組態檔會指定待部署項目的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="cb05e-192">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="cb05e-193">它會包含您在建立專案時所指定的資訊，例如網站的名稱和使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cb05e-193">It includes the information that you specified when you created the project, such as the name and username for the website.</span></span> <span data-ttu-id="cb05e-194">它還包含要佈建的資料庫 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="cb05e-194">It also includes the database to provision, if any.</span></span> <span data-ttu-id="cb05e-195">下列程式碼片段將顯示一個 JSON 組態檔範例：</span><span class="sxs-lookup"><span data-stu-id="cb05e-195">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="cb05e-196">您可以編輯 JSON 組態檔來變更部署項目。</span><span class="sxs-lookup"><span data-stu-id="cb05e-196">You can edit the JSON configuration file to change what is deployed.</span></span> <span data-ttu-id="cb05e-197">[網站] 區段是必要項目，但 [資料庫] 區段是選用項目。</span><span class="sxs-lookup"><span data-stu-id="cb05e-197">A webSite section is required, but the database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb05e-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cb05e-198">Next steps</span></span>
<span data-ttu-id="cb05e-199">如需詳細資訊，請參閱 [Publish-WebApplicationVM (Windows PowerShell 指令碼)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="cb05e-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

