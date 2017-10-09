---
title: "在 OMS 解決方案 aaaAzure 自動化資源 |Microsoft 文件"
description: "OMS 中的解決方案通常會包含在 Azure 自動化 tooautomate 程序，例如收集及處理監視資料中的 runbook。  本文說明如何 tooinclude runbook 及其相關的資源，在方案中。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 5281462e-f480-4e5e-9c19-022f36dce76d
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 82a156f89bf77ce25e52e5e4596261ec07a24dae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-automation-resources-tooan-oms-management-solution-preview"></a><span data-ttu-id="dc852-104">新增 Azure 自動化資源 tooan OMS 管理解決方案 （預覽）</span><span class="sxs-lookup"><span data-stu-id="dc852-104">Adding Azure Automation resources tooan OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="dc852-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="dc852-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="dc852-106">如下所述的任何結構描述是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="dc852-106">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="dc852-107">[在 OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會包含在 Azure 自動化 tooautomate 程序，例如收集及處理監視資料中的 runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation tooautomate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="dc852-108">此外 toorunbooks，自動化帳戶包含資產，例如變數和支援 hello 方案中的 hello runbook 使用的排程。</span><span class="sxs-lookup"><span data-stu-id="dc852-108">In addition toorunbooks, Automation accounts includes assets such as variables and schedules that support hello runbooks used in hello solution.</span></span>  <span data-ttu-id="dc852-109">本文說明如何 tooinclude runbook 及其相關的資源，在方案中。</span><span class="sxs-lookup"><span data-stu-id="dc852-109">This article describes how tooinclude runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="dc852-110">hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="dc852-110">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="dc852-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc852-111">Prerequisites</span></span>
<span data-ttu-id="dc852-112">本文假設您已經熟悉 hello 下列資訊。</span><span class="sxs-lookup"><span data-stu-id="dc852-112">This article assumes that you're already familiar with hello following information.</span></span>

- <span data-ttu-id="dc852-113">如何太[建立管理方案](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="dc852-113">How too[create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="dc852-114">hello 結構[方案檔](operations-management-suite-solutions-solution-file.md)。</span><span class="sxs-lookup"><span data-stu-id="dc852-114">hello structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="dc852-115">如何太[撰寫資源管理員範本](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="dc852-115">How too[author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="dc852-116">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="dc852-116">Automation account</span></span>
<span data-ttu-id="dc852-117">Azure 自動化中的所有資源都會包含在[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)中。</span><span class="sxs-lookup"><span data-stu-id="dc852-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="dc852-118">中所述[OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)hello 自動化帳戶不包含在 hello 管理解決方案，但必須先安裝 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="dc852-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello Automation account isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="dc852-119">如果它無法使用，hello 方案安裝將會失敗。</span><span class="sxs-lookup"><span data-stu-id="dc852-119">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="dc852-120">每個自動化資源 hello 名稱包括 hello 其自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-120">hello name of each Automation resource includes hello name of its Automation account.</span></span>  <span data-ttu-id="dc852-121">這是以 hello hello 方案**accountName**參數，如下列範例 runbook 資源的 hello 所示。</span><span class="sxs-lookup"><span data-stu-id="dc852-121">This is done in hello solution with hello **accountName** parameter as in hello following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="dc852-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="dc852-122">Runbooks</span></span>
<span data-ttu-id="dc852-123">您應該包含由 hello 方案檔中的 hello 方案使用，因此安裝 hello 方案時，他們所建立的任何 runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-123">You should include any runbooks used by hello solution in hello solution file so that they're created when hello solution is installed.</span></span>  <span data-ttu-id="dc852-124">您不能包含 hello 範本中的 hello runbook hello 主體，因此您應發佈 hello runbook tooa 公共場所位置存取它的任何使用者安裝方案。</span><span class="sxs-lookup"><span data-stu-id="dc852-124">You cannot contain hello body of hello runbook in hello template though, so you should publish hello runbook tooa public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="dc852-125">[Azure 自動化 runbook](../automation/automation-runbook-types.md)資源有一種**Microsoft.Automation/automationAccounts/runbooks**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have hello following structure.</span></span> <span data-ttu-id="dc852-126">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
        "type": "Microsoft.Automation/automationAccounts/runbooks",
        "apiVersion": "[variables('AutomationApiVersion')]",
        "dependsOn": [
        ],
        "location": "[parameters('regionId')]",
        "tags": { },
        "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
                "uri": "[variables('Runbook').Uri]",
                "version": [variables('Runbook').Version]"
            }
        }
    }


<span data-ttu-id="dc852-127">hello 下表描述的 runbook hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="dc852-127">hello properties for runbooks are described in hello following table.</span></span>

| <span data-ttu-id="dc852-128">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-128">Property</span></span> | <span data-ttu-id="dc852-129">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="dc852-130">runbookType</span></span> |<span data-ttu-id="dc852-131">指定 hello hello runbook 類型。</span><span class="sxs-lookup"><span data-stu-id="dc852-131">Specifies hello types of hello runbook.</span></span> <br><br> <span data-ttu-id="dc852-132">Script - PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="dc852-132">Script - PowerShell script</span></span> <br><span data-ttu-id="dc852-133">PowerShell - PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="dc852-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="dc852-134">GraphPowerShell - 圖形化 PowerShell 指令碼 Runbook</span><span class="sxs-lookup"><span data-stu-id="dc852-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="dc852-135">GraphPowerShellWorkflow - 圖形化 PowerShell 工作流程 Runbook</span><span class="sxs-lookup"><span data-stu-id="dc852-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="dc852-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="dc852-136">logProgress</span></span> |<span data-ttu-id="dc852-137">指定是否[進度記錄](../automation/automation-runbook-output-and-messages.md)應產生的 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="dc852-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="dc852-138">logVerbose</span></span> |<span data-ttu-id="dc852-139">指定是否[詳細資訊記錄](../automation/automation-runbook-output-and-messages.md)應產生的 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for hello runbook.</span></span> |
| <span data-ttu-id="dc852-140">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-140">description</span></span> |<span data-ttu-id="dc852-141">Hello runbook 的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="dc852-141">Optional description for hello runbook.</span></span> |
| <span data-ttu-id="dc852-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="dc852-142">publishContentLink</span></span> |<span data-ttu-id="dc852-143">指定 hello hello runbook 內容。</span><span class="sxs-lookup"><span data-stu-id="dc852-143">Specifies hello content of hello runbook.</span></span> <br><br><span data-ttu-id="dc852-144">uri 的 Uri toohello hello runbook 內容。</span><span class="sxs-lookup"><span data-stu-id="dc852-144">uri - Uri toohello content of hello runbook.</span></span>  <span data-ttu-id="dc852-145">這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc852-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="dc852-146">版本-您自己的追蹤的 hello runbook 的版本。</span><span class="sxs-lookup"><span data-stu-id="dc852-146">version - Version of hello runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="dc852-147">自動化作業</span><span class="sxs-lookup"><span data-stu-id="dc852-147">Automation jobs</span></span>
<span data-ttu-id="dc852-148">當您在 Azure 自動化中啟動 Runbook 時，此 Runbook 便會建立自動化作業。</span><span class="sxs-lookup"><span data-stu-id="dc852-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="dc852-149">您可以將自動化工作資源 tooyour 方案 tooautomatically 開始 runbook 安裝時，將 hello 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="dc852-149">You can add an automation job resource tooyour solution tooautomatically start a runbook when hello management solution is installed.</span></span>  <span data-ttu-id="dc852-150">這個方法是常用的 toostart runbook 所使用的 hello 解決方案的初始組態。</span><span class="sxs-lookup"><span data-stu-id="dc852-150">This method is typically used toostart runbooks that are used for initial configuration of hello solution.</span></span>  <span data-ttu-id="dc852-151">toostart runbook，以固定間隔建立[排程](#schedules)和[作業排程](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="dc852-151">toostart a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="dc852-152">工作資源的類型是**Microsoft.Automation/automationAccounts/jobs**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have hello following structure.</span></span>  <span data-ttu-id="dc852-153">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', parameters('Runbook').JobGuid)]",
      "type": "Microsoft.Automation/automationAccounts/jobs",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
      ],
      "tags": { },
      "properties": {
        "runbook": {
          "name": "[variables('Runbook').Name]"
        },
        "parameters": {
          "Parameter1": "[[variables('Runbook').Parameter1]",
          "Parameter2": "[[variables('Runbook').Parameter2]"
        }
      }
    }

<span data-ttu-id="dc852-154">自動化工作的 hello 屬性詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-154">hello properties for automation jobs are described in hello following table.</span></span>

| <span data-ttu-id="dc852-155">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-155">Property</span></span> | <span data-ttu-id="dc852-156">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-157">Runbook</span><span class="sxs-lookup"><span data-stu-id="dc852-157">runbook</span></span> |<span data-ttu-id="dc852-158">單一名稱同名的 hello runbook toostart hello 的實體。</span><span class="sxs-lookup"><span data-stu-id="dc852-158">Single name entity with hello name of hello runbook toostart.</span></span> |
| <span data-ttu-id="dc852-159">參數</span><span class="sxs-lookup"><span data-stu-id="dc852-159">parameters</span></span> |<span data-ttu-id="dc852-160">每個參數值 hello runbook 所需的實體。</span><span class="sxs-lookup"><span data-stu-id="dc852-160">Entity for each parameter value required by hello runbook.</span></span> |

<span data-ttu-id="dc852-161">hello 作業會包括 hello runbook 名稱和任何參數值 toobe 傳送 toohello runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-161">hello job includes hello runbook name and any parameter values toobe sent toohello runbook.</span></span>  <span data-ttu-id="dc852-162">hello 作業應該[相依於](operations-management-suite-solutions-solution-file.md#resources)hello 作業之前，必須建立 hello 自 hello runbook 啟動的 runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-162">hello job should [depend on](operations-management-suite-solutions-solution-file.md#resources) hello runbook that it's starting since hello runbook must be created before hello job.</span></span>  <span data-ttu-id="dc852-163">如果您有多個應該啟動的 Runbook，您可以藉由讓作業相依於其他任何應該先執行的作業，以定義這些 Runbook 的順序。</span><span class="sxs-lookup"><span data-stu-id="dc852-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="dc852-164">工作資源的 hello 名稱必須包含通常由參數指派的 GUID。</span><span class="sxs-lookup"><span data-stu-id="dc852-164">hello name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="dc852-165">[在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-solution-file.md#parameters)可讓您深入了解 GUID 參數。</span><span class="sxs-lookup"><span data-stu-id="dc852-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="dc852-166">憑證</span><span class="sxs-lookup"><span data-stu-id="dc852-166">Certificates</span></span>
<span data-ttu-id="dc852-167">[Azure 自動化憑證](../automation/automation-certificates.md)型別為**Microsoft.Automation/automationAccounts/certificates**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have hello following structure.</span></span> <span data-ttu-id="dc852-168">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
      "type": "Microsoft.Automation/automationAccounts/certificates",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "base64Value": "[variables('Certificate').Base64Value]",
        "thumbprint": "[variables('Certificate').Thumbprint]"
      }
    }



<span data-ttu-id="dc852-169">憑證資源的 hello 內容詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-169">hello properties for Certificates resources are described in hello following table.</span></span>

| <span data-ttu-id="dc852-170">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-170">Property</span></span> | <span data-ttu-id="dc852-171">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="dc852-172">base64Value</span></span> |<span data-ttu-id="dc852-173">Base 64 hello 憑證值。</span><span class="sxs-lookup"><span data-stu-id="dc852-173">Base 64 value for hello certificate.</span></span> |
| <span data-ttu-id="dc852-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="dc852-174">thumbprint</span></span> |<span data-ttu-id="dc852-175">Hello 憑證指模。</span><span class="sxs-lookup"><span data-stu-id="dc852-175">Thumbprint for hello certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="dc852-176">認證</span><span class="sxs-lookup"><span data-stu-id="dc852-176">Credentials</span></span>
<span data-ttu-id="dc852-177">[Azure 自動化認證](../automation/automation-credentials.md)型別為**Microsoft.Automation/automationAccounts/credentials**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have hello following structure.</span></span>  <span data-ttu-id="dc852-178">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
      "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
      "type": "Microsoft.Automation/automationAccounts/credentials",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "userName": "[parameters('credentialUsername')]",
        "password": "[parameters('credentialPassword')]"
      }
    }

<span data-ttu-id="dc852-179">認證資源的 hello 內容詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-179">hello properties for Credential resources are described in hello following table.</span></span>

| <span data-ttu-id="dc852-180">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-180">Property</span></span> | <span data-ttu-id="dc852-181">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-182">userName</span><span class="sxs-lookup"><span data-stu-id="dc852-182">userName</span></span> |<span data-ttu-id="dc852-183">Hello 認證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-183">User name for hello credential.</span></span> |
| <span data-ttu-id="dc852-184">password</span><span class="sxs-lookup"><span data-stu-id="dc852-184">password</span></span> |<span data-ttu-id="dc852-185">Hello 認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="dc852-185">Password for hello credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="dc852-186">排程</span><span class="sxs-lookup"><span data-stu-id="dc852-186">Schedules</span></span>
<span data-ttu-id="dc852-187">[Azure 自動化排程](../automation/automation-schedules.md)型別為**Microsoft.Automation/automationAccounts/schedules**而且具有下列結構的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have hello hello following structure.</span></span> <span data-ttu-id="dc852-188">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
      "type": "microsoft.automation/automationAccounts/schedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Schedule').Description]",
        "startTime": "[parameters('scheduleStartTime')]",
        "timeZone": "[parameters('scheduleTimeZone')]",
        "isEnabled": "[variables('Schedule').IsEnabled]",
        "interval": "[variables('Schedule').Interval]",
        "frequency": "[variables('Schedule').Frequency]"
      }
    }

<span data-ttu-id="dc852-189">排程資源的 hello 內容詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-189">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="dc852-190">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-190">Property</span></span> | <span data-ttu-id="dc852-191">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-192">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-192">description</span></span> |<span data-ttu-id="dc852-193">Hello 排程的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="dc852-193">Optional description for hello schedule.</span></span> |
| <span data-ttu-id="dc852-194">startTime</span><span class="sxs-lookup"><span data-stu-id="dc852-194">startTime</span></span> |<span data-ttu-id="dc852-195">排程 hello 開始時間指定為 DateTime 物件。</span><span class="sxs-lookup"><span data-stu-id="dc852-195">Specifies hello start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="dc852-196">如果可以轉換的 tooa 可提供字串有效的日期時間。</span><span class="sxs-lookup"><span data-stu-id="dc852-196">A string can be provided if it can be converted tooa valid DateTime.</span></span> |
| <span data-ttu-id="dc852-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="dc852-197">isEnabled</span></span> |<span data-ttu-id="dc852-198">指定是否啟用 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="dc852-198">Specifies whether hello schedule is enabled.</span></span> |
| <span data-ttu-id="dc852-199">interval</span><span class="sxs-lookup"><span data-stu-id="dc852-199">interval</span></span> |<span data-ttu-id="dc852-200">hello hello 排程的間隔類型。</span><span class="sxs-lookup"><span data-stu-id="dc852-200">hello type of interval for hello schedule.</span></span><br><br><span data-ttu-id="dc852-201">day</span><span class="sxs-lookup"><span data-stu-id="dc852-201">day</span></span><br><span data-ttu-id="dc852-202">hour</span><span class="sxs-lookup"><span data-stu-id="dc852-202">hour</span></span> |
| <span data-ttu-id="dc852-203">frequency</span><span class="sxs-lookup"><span data-stu-id="dc852-203">frequency</span></span> |<span data-ttu-id="dc852-204">Hello 排程的頻率應該引發天數或小時。</span><span class="sxs-lookup"><span data-stu-id="dc852-204">Frequency that hello schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="dc852-205">排程必須具有開始時間大於 hello 的值與目前的時間。</span><span class="sxs-lookup"><span data-stu-id="dc852-205">Schedules must have a start time with a value greater than hello current time.</span></span>  <span data-ttu-id="dc852-206">因為您會有無從得知進行 toobe 安裝時，您無法提供此值的變數。</span><span class="sxs-lookup"><span data-stu-id="dc852-206">You cannot provide this value with a variable since you would have no way of knowing when it's going toobe installed.</span></span>

<span data-ttu-id="dc852-207">使用其中一個方案中使用排程的資源時，下列兩種策略的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-207">Use one of hello following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="dc852-208">使用參數進行 hello hello 排程開始時間。</span><span class="sxs-lookup"><span data-stu-id="dc852-208">Use a parameter for hello start time of hello schedule.</span></span>  <span data-ttu-id="dc852-209">在安裝 hello 方案時，這會提示 hello 使用者 tooprovide 值。</span><span class="sxs-lookup"><span data-stu-id="dc852-209">This will prompt hello user tooprovide a value when they install hello solution.</span></span>  <span data-ttu-id="dc852-210">如果您有多個排程，您可以對它們使用單一參數值。</span><span class="sxs-lookup"><span data-stu-id="dc852-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="dc852-211">建立 hello 排程使用 runbook 啟動時安裝 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="dc852-211">Create hello schedules using a runbook that starts when hello solution is installed.</span></span>  <span data-ttu-id="dc852-212">這會移除 hello 需求的時間，但是您不能包含 hello 使用者 toospecify hello 排程，因此移除 hello 方案時將會移除您方案中的。</span><span class="sxs-lookup"><span data-stu-id="dc852-212">This removes hello requirement of hello user toospecify a time, but you can't contain hello schedule in your solution so it will be removed when hello solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="dc852-213">作業排程</span><span class="sxs-lookup"><span data-stu-id="dc852-213">Job schedules</span></span>
<span data-ttu-id="dc852-214">作業排程資源會連結 Runbook 與排程。</span><span class="sxs-lookup"><span data-stu-id="dc852-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="dc852-215">它們有一種**Microsoft.Automation/automationAccounts/jobSchedules**而且具有下列結構的 hello hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have hello hello following structure.</span></span>  <span data-ttu-id="dc852-216">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
      "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
      "type": "microsoft.automation/automationAccounts/jobSchedules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "location": "[parameters('regionId')]",
      "dependsOn": [
        "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
        "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
      ],
      "tags": {
      },
      "properties": {
        "schedule": {
          "name": "[variables('Schedule').Name]"
        },
        "runbook": {
          "name": "[variables('Runbook').Name]"
        }
      }
    }


<span data-ttu-id="dc852-217">作業排程的 hello 屬性詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-217">hello properties for job schedules are described in hello following table.</span></span>

| <span data-ttu-id="dc852-218">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-218">Property</span></span> | <span data-ttu-id="dc852-219">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-220">排程名稱</span><span class="sxs-lookup"><span data-stu-id="dc852-220">schedule name</span></span> |<span data-ttu-id="dc852-221">單一**名稱**實體與 hello hello 排程名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-221">Single **name** entity with hello name of hello schedule.</span></span> |
| <span data-ttu-id="dc852-222">Runbook 名稱</span><span class="sxs-lookup"><span data-stu-id="dc852-222">runbook name</span></span>  |<span data-ttu-id="dc852-223">單一**名稱**實體與 hello hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-223">Single **name** entity with hello name of hello runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="dc852-224">變數</span><span class="sxs-lookup"><span data-stu-id="dc852-224">Variables</span></span>
<span data-ttu-id="dc852-225">[Azure 自動化變數](../automation/automation-variables.md)型別為**Microsoft.Automation/automationAccounts/variables**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have hello following structure.</span></span>  <span data-ttu-id="dc852-226">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
      "type": "microsoft.automation/automationAccounts/variables",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "tags": { },
      "dependsOn": [
      ],
      "properties": {
        "description": "[variables('Variable').Description]",
        "isEncrypted": "[variables('Variable').Encrypted]",
        "type": "[variables('Variable').Type]",
        "value": "[variables('Variable').Value]"
      }
    }

<span data-ttu-id="dc852-227">hello 下表描述 hello 變數資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="dc852-227">hello properties for variable resources are described in hello following table.</span></span>

| <span data-ttu-id="dc852-228">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-228">Property</span></span> | <span data-ttu-id="dc852-229">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-230">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-230">description</span></span> | <span data-ttu-id="dc852-231">Hello 變數的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="dc852-231">Optional description for hello variable.</span></span> |
| <span data-ttu-id="dc852-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="dc852-232">isEncrypted</span></span> | <span data-ttu-id="dc852-233">指定是否應該加密 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="dc852-233">Specifies whether hello variable should be encrypted.</span></span> |
| <span data-ttu-id="dc852-234">類型</span><span class="sxs-lookup"><span data-stu-id="dc852-234">type</span></span> | <span data-ttu-id="dc852-235">這個屬性目前沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="dc852-235">This property currently has no effect.</span></span>  <span data-ttu-id="dc852-236">hello hello 變數資料類型將決定由 hello 初始值。</span><span class="sxs-lookup"><span data-stu-id="dc852-236">hello data type of hello variable will be determined by hello initial value.</span></span> |
| <span data-ttu-id="dc852-237">value</span><span class="sxs-lookup"><span data-stu-id="dc852-237">value</span></span> | <span data-ttu-id="dc852-238">Hello 變數的值。</span><span class="sxs-lookup"><span data-stu-id="dc852-238">Value for hello variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="dc852-239">hello**類型** 內容目前沒有正在建立 hello 變數上的沒有作用。</span><span class="sxs-lookup"><span data-stu-id="dc852-239">hello **type** property currently has no effect on hello variable being created.</span></span>  <span data-ttu-id="dc852-240">hello hello 變數的資料類型將決定 hello 值。</span><span class="sxs-lookup"><span data-stu-id="dc852-240">hello data type for hello variable will be determined by hello value.</span></span>  

<span data-ttu-id="dc852-241">如果您設定 hello 初始 hello 變數值，它必須設定為 hello 正確的資料類型。</span><span class="sxs-lookup"><span data-stu-id="dc852-241">If you set hello initial value for hello variable, it must be configured as hello correct data type.</span></span>  <span data-ttu-id="dc852-242">hello 下表提供可允許的 hello 不同的資料類型，以及其語法。</span><span class="sxs-lookup"><span data-stu-id="dc852-242">hello following table provides hello different data types allowable and their syntax.</span></span>  <span data-ttu-id="dc852-243">請注意，在 JSON 中的值是預期的 tooalways 括以引號括住含有 hello 括在引號內的任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="dc852-243">Note that values in JSON are expected tooalways be enclosed in quotes with any special characters within hello quotes.</span></span>  <span data-ttu-id="dc852-244">例如，字串值會指定以引號括住 hello 字串 (使用 hello 逸出字元 (\\)) 時可以使用引號括住的一組指定的數字的值。</span><span class="sxs-lookup"><span data-stu-id="dc852-244">For example, a string value would be specified by quotes around hello string (using hello escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="dc852-245">資料類型</span><span class="sxs-lookup"><span data-stu-id="dc852-245">Data type</span></span> | <span data-ttu-id="dc852-246">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-246">Description</span></span> | <span data-ttu-id="dc852-247">範例</span><span class="sxs-lookup"><span data-stu-id="dc852-247">Example</span></span> | <span data-ttu-id="dc852-248">太解析</span><span class="sxs-lookup"><span data-stu-id="dc852-248">Resolves too</span></span>|
|:--|:--|:--|:--|
| <span data-ttu-id="dc852-249">字串</span><span class="sxs-lookup"><span data-stu-id="dc852-249">string</span></span>   | <span data-ttu-id="dc852-250">以雙引號括住值。</span><span class="sxs-lookup"><span data-stu-id="dc852-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="dc852-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="dc852-251">"\"Hello world\""</span></span> | <span data-ttu-id="dc852-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="dc852-252">"Hello world"</span></span> |
| <span data-ttu-id="dc852-253">numeric</span><span class="sxs-lookup"><span data-stu-id="dc852-253">numeric</span></span>  | <span data-ttu-id="dc852-254">以單引號括住數值。</span><span class="sxs-lookup"><span data-stu-id="dc852-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="dc852-255">"64"</span><span class="sxs-lookup"><span data-stu-id="dc852-255">"64"</span></span> | <span data-ttu-id="dc852-256">64</span><span class="sxs-lookup"><span data-stu-id="dc852-256">64</span></span> |
| <span data-ttu-id="dc852-257">布林值</span><span class="sxs-lookup"><span data-stu-id="dc852-257">boolean</span></span>  | <span data-ttu-id="dc852-258">以引號括住 **true** 或 **false**。</span><span class="sxs-lookup"><span data-stu-id="dc852-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="dc852-259">請注意，此值必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="dc852-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="dc852-260">"true"</span><span class="sxs-lookup"><span data-stu-id="dc852-260">"true"</span></span> | <span data-ttu-id="dc852-261">true</span><span class="sxs-lookup"><span data-stu-id="dc852-261">true</span></span> |
| <span data-ttu-id="dc852-262">datetime</span><span class="sxs-lookup"><span data-stu-id="dc852-262">datetime</span></span> | <span data-ttu-id="dc852-263">序列化的日期值。</span><span class="sxs-lookup"><span data-stu-id="dc852-263">Serialized date value.</span></span><br><span data-ttu-id="dc852-264">您可以使用 PowerShell toogenerate 中的 hello Convertto-json cmdlet 此值，在特定日期。</span><span class="sxs-lookup"><span data-stu-id="dc852-264">You can use hello ConvertTo-Json cmdlet in PowerShell toogenerate this value for a particular date.</span></span><br><span data-ttu-id="dc852-265">範例：get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="dc852-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="dc852-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="dc852-266">ConvertTo-Json</span></span> | <span data-ttu-id="dc852-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="dc852-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="dc852-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="dc852-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="dc852-269">模組</span><span class="sxs-lookup"><span data-stu-id="dc852-269">Modules</span></span>
<span data-ttu-id="dc852-270">您的管理解決方案不需要 toodefine[全域模組](../automation/automation-integration-modules.md)使用您的 runbook，因為它們永遠都可以在您的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="dc852-270">Your management solution does not need toodefine [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="dc852-271">您將 runbook 所使用的任何其他模組需要 tooinclude 資源。</span><span class="sxs-lookup"><span data-stu-id="dc852-271">You do need tooinclude a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="dc852-272">[整合模組](../automation/automation-integration-modules.md)型別為**Microsoft.Automation/automationAccounts/modules**而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have hello following structure.</span></span>  <span data-ttu-id="dc852-273">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="dc852-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span>

    {
      "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
      "type": "Microsoft.Automation/automationAccounts/modules",
      "apiVersion": "[variables('AutomationApiVersion')]",
      "dependsOn": [
      ],
      "properties": {
        "contentLink": {
          "uri": "[variables('Module').Uri]"
        }
      }
    }


<span data-ttu-id="dc852-274">模組資源的 hello 內容詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc852-274">hello properties for module resources are described in hello following table.</span></span>

| <span data-ttu-id="dc852-275">屬性</span><span class="sxs-lookup"><span data-stu-id="dc852-275">Property</span></span> | <span data-ttu-id="dc852-276">說明</span><span class="sxs-lookup"><span data-stu-id="dc852-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="dc852-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="dc852-277">contentLink</span></span> |<span data-ttu-id="dc852-278">指定 hello hello 模組內容。</span><span class="sxs-lookup"><span data-stu-id="dc852-278">Specifies hello content of hello module.</span></span> <br><br><span data-ttu-id="dc852-279">uri 的 Uri toohello hello 模組內容。</span><span class="sxs-lookup"><span data-stu-id="dc852-279">uri - Uri toohello content of hello module.</span></span>  <span data-ttu-id="dc852-280">這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc852-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="dc852-281">版本-您自己的追蹤的 hello 模組版本。</span><span class="sxs-lookup"><span data-stu-id="dc852-281">version - Version of hello module for your own tracking.</span></span> |

<span data-ttu-id="dc852-282">一旦建立 hello runbook 之前的 hello 模組資源 tooensure 需要具備 hello runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-282">hello runbook should depend on hello module resource tooensure that it's created before hello runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="dc852-283">更新模組</span><span class="sxs-lookup"><span data-stu-id="dc852-283">Updating modules</span></span>
<span data-ttu-id="dc852-284">如果您更新的管理解決方案，包括 runbook 所使用的排程，而且 hello 新版本，您的方案有使用該 runbook 的新模組，hello runbook 可能會使用 hello 模組 hello 舊版本。</span><span class="sxs-lookup"><span data-stu-id="dc852-284">If you update a management solution that includes a runbook that uses a schedule, and hello new version of your solution has a new module used by that runbook, then hello runbook may use hello old version of hello module.</span></span>  <span data-ttu-id="dc852-285">您應該包含 hello 遵循您的方案中的 runbook，並建立工作 toorun 它們之前的任何其他 runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-285">You should include hello following runbooks in your solution and create a job toorun them before any other runbooks.</span></span>  <span data-ttu-id="dc852-286">這可確保任何模組，會更新為所需的 hello runbook 會載入。</span><span class="sxs-lookup"><span data-stu-id="dc852-286">This will ensure that any modules are updated as required before hello runbooks are loaded.</span></span>

* <span data-ttu-id="dc852-287">[更新 ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript)可確保所有的方案中的 runbook 所使用的 hello 模組都 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="dc852-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of hello modules used by runbooks in your solution are hello latest version.</span></span>  
* <span data-ttu-id="dc852-288">[個 MS ReRegisterAutomationSchedule 管理](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript)重新註冊所有 hello 排程資源 tooensure hello runbook 連結 toothem 與使用 hello 最新的模組。</span><span class="sxs-lookup"><span data-stu-id="dc852-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of hello schedule resources tooensure that hello runbooks linked toothem with use hello latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="dc852-289">範例</span><span class="sxs-lookup"><span data-stu-id="dc852-289">Sample</span></span>
<span data-ttu-id="dc852-290">以下是方案的範例，包括所包含的 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="dc852-290">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="dc852-291">Runbook。</span><span class="sxs-lookup"><span data-stu-id="dc852-291">Runbook.</span></span>  <span data-ttu-id="dc852-292">這是儲存在公用 GitHub 儲存機制的 Runbook 範例。</span><span class="sxs-lookup"><span data-stu-id="dc852-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="dc852-293">啟動時安裝 hello 解決方案的 hello runbook 的自動化作業。</span><span class="sxs-lookup"><span data-stu-id="dc852-293">Automation job that starts hello runbook when hello solution is installed.</span></span>
- <span data-ttu-id="dc852-294">排程與工作排程 toostart hello runbook 的固定間隔。</span><span class="sxs-lookup"><span data-stu-id="dc852-294">Schedule and job schedule toostart hello runbook at regular intervals.</span></span>
- <span data-ttu-id="dc852-295">憑證。</span><span class="sxs-lookup"><span data-stu-id="dc852-295">Certificate.</span></span>
- <span data-ttu-id="dc852-296">認證。</span><span class="sxs-lookup"><span data-stu-id="dc852-296">Credential.</span></span>
- <span data-ttu-id="dc852-297">變數。</span><span class="sxs-lookup"><span data-stu-id="dc852-297">Variable.</span></span>
- <span data-ttu-id="dc852-298">模組。</span><span class="sxs-lookup"><span data-stu-id="dc852-298">Module.</span></span>  <span data-ttu-id="dc852-299">這是 hello [OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)撰寫資料 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="dc852-299">This is hello [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data tooLog Analytics.</span></span> 

<span data-ttu-id="dc852-300">hello 範例會使用[標準方案參數](operations-management-suite-solutions-solution-file.md#parameters)通常做為方案中使用變數相對於 toohardcoding hello 資源定義中的值。</span><span class="sxs-lookup"><span data-stu-id="dc852-300">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>


    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "workspaceName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Log Analytics workspace."
          }
        },
        "accountName": {
          "type": "string",
          "metadata": {
            "Description": "Name of Automation account."
          }
        },
        "workspaceregionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Log Analytics workspace."
          }
        },
        "regionId": {
          "type": "string",
          "metadata": {
            "Description": "Region of Automation account."
          }
        },
        "pricingTier": {
          "type": "string",
          "metadata": {
            "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account."
          }
        },
        "certificateBase64Value": {
          "type": "string",
          "metadata": {
            "Description": "Base 64 value for certificate."
          }
        },
        "certificateThumbprint": {
          "type": "securestring",
          "metadata": {
            "Description": "Thumbprint for certificate."
          }
        },
        "credentialUsername": {
          "type": "string",
          "metadata": {
            "Description": "Username for credential."
          }
        },
        "credentialPassword": {
          "type": "securestring",
          "metadata": {
            "Description": "Password for credential."
          }
        },
        "scheduleStartTime": {
          "type": "string",
          "metadata": {
            "Description": "Start time for shedule."
          }
        },
        "scheduleTimeZone": {
          "type": "string",
          "metadata": {
            "Description": "Time zone for schedule."
          }
        },
        "scheduleLinkGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello schedule link toorunbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for hello runbook job.",
            "control": "guid"
          }
        }
      },
      "variables": {
        "SolutionName": "MySolution",
        "SolutionVersion": "1.0",
        "SolutionPublisher": "Contoso",
        "ProductName": "SampleSolution",
    
        "LogAnalyticsApiVersion": "2015-11-01-preview",
        "AutomationApiVersion": "2015-10-31",
    
        "Runbook": {
          "Name": "MyRunbook",
          "Description": "Sample runbook",
          "Type": "PowerShell",
          "Uri": "https://raw.githubusercontent.com/user/myrepo/master/samples/MyRunbook.ps1",
          "JobGuid": "[parameters('runbookJobGuid')]"
        },
    
        "Certificate": {
          "Name": "MyCertificate",
          "Base64Value": "[parameters('certificateBase64Value')]",
          "Thumbprint": "[parameters('certificateThumbprint')]"
        },
    
        "Credential": {
          "Name": "MyCredential",
          "UserName": "[parameters('credentialUsername')]",
          "Password": "[parameters('credentialPassword')]"
        },
    
        "Schedule": {
          "Name": "MySchedule",
          "Description": "Sample schedule",
          "IsEnabled": "true",
          "Interval": "1",
          "Frequency": "hour",
          "StartTime": "[parameters('scheduleStartTime')]",
          "TimeZone": "[parameters('scheduleTimeZone')]",
          "LinkGuid": "[parameters('scheduleLinkGuid')]"
        },
    
        "Variable": {
          "Name": "MyVariable",
          "Description": "Sample variable",
          "Encrypted": 0,
          "Type": "string",
          "Value": "'This is my string value.'"
        },
    
        "Module": {
          "Name": "OMSIngestionAPI",
          "Uri": "https://devopsgallerystorage.blob.core.windows.net/packages/omsingestionapi.1.3.0.nupkg"
        }
      },
      "resources": [
        {
          "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
          "location": "[parameters('workspaceRegionId')]",
          "tags": { },
          "type": "Microsoft.OperationsManagement/solutions",
          "apiVersion": "[variables('LogAnalyticsApiVersion')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
            "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
            "referencedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/modules/', parameters('accountName'), variables('Module').Name)]"
            ],
            "containedResources": [
              "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobs/', parameters('accountName'), variables('Runbook').JobGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/certificates/', parameters('accountName'), variables('Certificate').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/credentials/', parameters('accountName'), variables('Credential').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]",
              "[resourceId('Microsoft.Automation/automationAccounts/jobSchedules/', parameters('accountName'), variables('Schedule').LinkGuid)]",
              "[resourceId('Microsoft.Automation/automationAccounts/variables/', parameters('accountName'), variables('Variable').Name)]"
            ]
          },
          "plan": {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
            "Version": "[variables('SolutionVersion')]",
            "product": "[variables('ProductName')]",
            "publisher": "[variables('SolutionPublisher')]",
            "promotionCode": ""
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').Name)]",
          "type": "Microsoft.Automation/automationAccounts/runbooks",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "location": "[parameters('regionId')]",
          "tags": { },
          "properties": {
            "runbookType": "[variables('Runbook').Type]",
            "logProgress": "true",
            "logVerbose": "true",
            "description": "[variables('Runbook').Description]",
            "publishContentLink": {
              "uri": "[variables('Runbook').Uri]",
              "version": "1.0.0.0"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Runbook').JobGuid)]",
          "type": "Microsoft.Automation/automationAccounts/jobs",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[concat('Microsoft.Automation/automationAccounts/', parameters('accountName'), '/runbooks/', variables('Runbook').Name)]"
          ],
          "tags": { },
          "properties": {
            "runbook": {
              "name": "[variables('Runbook').Name]"
            },
            "parameters": {
              "targetSubscriptionId": "[subscription().subscriptionId]",
              "resourcegroup": "[resourceGroup().name]",
              "automationaccount": "[parameters('accountName')]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Certificate').Name)]",
          "type": "Microsoft.Automation/automationAccounts/certificates",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "Base64Value": "[variables('Certificate').Base64Value]",
            "Thumbprint": "[variables('Certificate').Thumbprint]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Credential').Name)]",
          "type": "Microsoft.Automation/automationAccounts/credentials",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "userName": "[variables('Credential').UserName]",
            "password": "[variables('Credential').Password]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').Name)]",
          "type": "microsoft.automation/automationAccounts/schedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Schedule').Description]",
            "startTime": "[variables('Schedule').StartTime]",
            "timeZone": "[variables('Schedule').TimeZone]",
            "isEnabled": "[variables('Schedule').IsEnabled]",
            "interval": "[variables('Schedule').Interval]",
            "frequency": "[variables('Schedule').Frequency]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Schedule').LinkGuid)]",
          "type": "microsoft.automation/automationAccounts/jobSchedules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "location": "[parameters('regionId')]",
          "dependsOn": [
            "[resourceId('Microsoft.Automation/automationAccounts/runbooks/', parameters('accountName'), variables('Runbook').Name)]",
            "[resourceId('Microsoft.Automation/automationAccounts/schedules/', parameters('accountName'), variables('Schedule').Name)]"
          ],
          "tags": {
          },
          "properties": {
            "schedule": {
              "name": "[variables('Schedule').Name]"
            },
            "runbook": {
              "name": "[variables('Runbook').Name]"
            }
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Variable').Name)]",
          "type": "microsoft.automation/automationAccounts/variables",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "tags": { },
          "dependsOn": [
          ],
          "properties": {
            "description": "[variables('Variable').Description]",
            "isEncrypted": "[variables('Variable').Encrypted]",
            "type": "[variables('Variable').Type]",
            "value": "[variables('Variable').Value]"
          }
        },
        {
          "name": "[concat(parameters('accountName'), '/', variables('Module').Name)]",
          "type": "Microsoft.Automation/automationAccounts/modules",
          "apiVersion": "[variables('AutomationApiVersion')]",
          "dependsOn": [
          ],
          "properties": {
            "contentLink": {
              "uri": "[variables('Module').Uri]"
            }
          }
        }
    
      ],
      "outputs": { }
    }




## <a name="next-steps"></a><span data-ttu-id="dc852-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc852-301">Next steps</span></span>
* <span data-ttu-id="dc852-302">[將檢視 tooyour 方案](operations-management-suite-solutions-resources-views.md)toovisualize 收集資料。</span><span class="sxs-lookup"><span data-stu-id="dc852-302">[Add a view tooyour solution](operations-management-suite-solutions-resources-views.md) toovisualize collected data.</span></span>
