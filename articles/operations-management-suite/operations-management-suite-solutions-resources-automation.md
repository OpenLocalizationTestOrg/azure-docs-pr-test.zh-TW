---
title: "OMS 解決方案中的 Azure 自動化資源 | Microsoft Docs"
description: "OMS 中的解決方案通常會在 Azure 自動化中包含 Runbook，以便自動執行一些程序，例如收集及處理監視資料。  本文說明如何在解決方案中包含 Runbook 與其相關資源。"
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
ms.openlocfilehash: c1909183a33ed03d8165671cff25cc8b83b77733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="adding-azure-automation-resources-to-an-oms-management-solution-preview"></a><span data-ttu-id="42de8-104">將 Azure 自動化資源新增至 OMS 管理解決方案 (預覽)</span><span class="sxs-lookup"><span data-stu-id="42de8-104">Adding Azure Automation resources to an OMS management solution (Preview)</span></span>
> [!NOTE]
> <span data-ttu-id="42de8-105">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="42de8-105">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="42de8-106">以下所述的任何結構描述可能會有所變更。</span><span class="sxs-lookup"><span data-stu-id="42de8-106">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="42de8-107">[OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會在 Azure 自動化中包含 Runbook，以便自動執行一些程序，例如收集及處理監視資料。</span><span class="sxs-lookup"><span data-stu-id="42de8-107">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include runbooks in Azure Automation to automate processes such as collecting and processing monitoring data.</span></span>  <span data-ttu-id="42de8-108">除了 Runbook，自動化帳戶還包含一些資產，例如支援解決方案中所用 Runbook 的變數和排程。</span><span class="sxs-lookup"><span data-stu-id="42de8-108">In addition to runbooks, Automation accounts includes assets such as variables and schedules that support the runbooks used in the solution.</span></span>  <span data-ttu-id="42de8-109">本文說明如何在解決方案中包含 Runbook 與其相關資源。</span><span class="sxs-lookup"><span data-stu-id="42de8-109">This article describes how to include runbooks and their related resources in a solution.</span></span>

> [!NOTE]
> <span data-ttu-id="42de8-110">本文中的範例使用管理解決方案所必要或通用的參數和變數，如[在 Operations Management Suite (OMS) 中建立管理解決方案](operations-management-suite-solutions-creating.md)所述。</span><span class="sxs-lookup"><span data-stu-id="42de8-110">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="42de8-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="42de8-111">Prerequisites</span></span>
<span data-ttu-id="42de8-112">本文假設您已熟悉下列資訊。</span><span class="sxs-lookup"><span data-stu-id="42de8-112">This article assumes that you're already familiar with the following information.</span></span>

- <span data-ttu-id="42de8-113">如何[建立管理解決方案](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="42de8-113">How to [create a management solution](operations-management-suite-solutions-creating.md).</span></span>
- <span data-ttu-id="42de8-114">[解決方案檔](operations-management-suite-solutions-solution-file.md)的結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-114">The structure of a [solution file](operations-management-suite-solutions-solution-file.md).</span></span>
- <span data-ttu-id="42de8-115">如何[製作 Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="42de8-115">How to [author Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>

## <a name="automation-account"></a><span data-ttu-id="42de8-116">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="42de8-116">Automation account</span></span>
<span data-ttu-id="42de8-117">Azure 自動化中的所有資源都會包含在[自動化帳戶](../automation/automation-security-overview.md#automation-account-overview)中。</span><span class="sxs-lookup"><span data-stu-id="42de8-117">All resources in Azure Automation are contained in an [Automation account](../automation/automation-security-overview.md#automation-account-overview).</span></span>  <span data-ttu-id="42de8-118">如 [OMS 工作區和自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)所述，自動化帳戶不包含在管理解決方案中，但是在安裝解決方案前就必須存在。</span><span class="sxs-lookup"><span data-stu-id="42de8-118">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the Automation account isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="42de8-119">如果無法使用，則解決方案會安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="42de8-119">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="42de8-120">每個自動化資源的名稱皆包含其自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-120">The name of each Automation resource includes the name of its Automation account.</span></span>  <span data-ttu-id="42de8-121">這可在具有 **accountName** 參數的解決方案中完成，如下列 Runbook 資源範例所示。</span><span class="sxs-lookup"><span data-stu-id="42de8-121">This is done in the solution with the **accountName** parameter as in the following example of a runbook resource.</span></span>

    "name": "[concat(parameters('accountName'), '/MyRunbook'))]"


## <a name="runbooks"></a><span data-ttu-id="42de8-122">Runbook</span><span class="sxs-lookup"><span data-stu-id="42de8-122">Runbooks</span></span>
<span data-ttu-id="42de8-123">您應該在解決方案檔中包含解決方案所使用的任何 Runbook，以便系統會在安裝解決方案時建立這些 Runbook。</span><span class="sxs-lookup"><span data-stu-id="42de8-123">You should include any runbooks used by the solution in the solution file so that they're created when the solution is installed.</span></span>  <span data-ttu-id="42de8-124">但您不能在範本中包含 Runbook 的主體，因此，您應該將 Runbook 發佈到公用位置，以供安裝了解決方案的使用者存取。</span><span class="sxs-lookup"><span data-stu-id="42de8-124">You cannot contain the body of the runbook in the template though, so you should publish the runbook to a public location where it can be accessed by any user installing your solution.</span></span>

<span data-ttu-id="42de8-125">[Azure 自動化 Runbook](../automation/automation-runbook-types.md) 資源的類型為 **Microsoft.Automation/automationAccounts/runbooks**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-125">[Azure Automation runbook](../automation/automation-runbook-types.md) resources have a type of **Microsoft.Automation/automationAccounts/runbooks** and have the following structure.</span></span> <span data-ttu-id="42de8-126">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-126">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="42de8-127">下表會說明 Runbook 的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-127">The properties for runbooks are described in the following table.</span></span>

| <span data-ttu-id="42de8-128">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-128">Property</span></span> | <span data-ttu-id="42de8-129">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-130">runbookType</span><span class="sxs-lookup"><span data-stu-id="42de8-130">runbookType</span></span> |<span data-ttu-id="42de8-131">指定 Runbook 的類型。</span><span class="sxs-lookup"><span data-stu-id="42de8-131">Specifies the types of the runbook.</span></span> <br><br> <span data-ttu-id="42de8-132">Script - PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="42de8-132">Script - PowerShell script</span></span> <br><span data-ttu-id="42de8-133">PowerShell - PowerShell 工作流程</span><span class="sxs-lookup"><span data-stu-id="42de8-133">PowerShell - PowerShell workflow</span></span> <br> <span data-ttu-id="42de8-134">GraphPowerShell - 圖形化 PowerShell 指令碼 Runbook</span><span class="sxs-lookup"><span data-stu-id="42de8-134">GraphPowerShell - Graphical PowerShell script runbook</span></span> <br> <span data-ttu-id="42de8-135">GraphPowerShellWorkflow - 圖形化 PowerShell 工作流程 Runbook</span><span class="sxs-lookup"><span data-stu-id="42de8-135">GraphPowerShellWorkflow - Graphical PowerShell workflow runbook</span></span> |
| <span data-ttu-id="42de8-136">logProgress</span><span class="sxs-lookup"><span data-stu-id="42de8-136">logProgress</span></span> |<span data-ttu-id="42de8-137">指定是否應針對 Runbook 產生[進度記錄](../automation/automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="42de8-137">Specifies whether [progress records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="42de8-138">logVerbose</span><span class="sxs-lookup"><span data-stu-id="42de8-138">logVerbose</span></span> |<span data-ttu-id="42de8-139">指定是否應針對 Runbook 產生[詳細資訊記錄](../automation/automation-runbook-output-and-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="42de8-139">Specifies whether [verbose records](../automation/automation-runbook-output-and-messages.md) should be generated for the runbook.</span></span> |
| <span data-ttu-id="42de8-140">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-140">description</span></span> |<span data-ttu-id="42de8-141">Runbook 的選擇性說明。</span><span class="sxs-lookup"><span data-stu-id="42de8-141">Optional description for the runbook.</span></span> |
| <span data-ttu-id="42de8-142">publishContentLink</span><span class="sxs-lookup"><span data-stu-id="42de8-142">publishContentLink</span></span> |<span data-ttu-id="42de8-143">指定 Runbook 的內容。</span><span class="sxs-lookup"><span data-stu-id="42de8-143">Specifies the content of the runbook.</span></span> <br><br><span data-ttu-id="42de8-144">uri - 指定 Runbook 的內容 Uri。</span><span class="sxs-lookup"><span data-stu-id="42de8-144">uri - Uri to the content of the runbook.</span></span>  <span data-ttu-id="42de8-145">這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="42de8-145">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="42de8-146">版本 - 您自己追蹤的 Runbook 版本。</span><span class="sxs-lookup"><span data-stu-id="42de8-146">version - Version of the runbook for your own tracking.</span></span> |


## <a name="automation-jobs"></a><span data-ttu-id="42de8-147">自動化作業</span><span class="sxs-lookup"><span data-stu-id="42de8-147">Automation jobs</span></span>
<span data-ttu-id="42de8-148">當您在 Azure 自動化中啟動 Runbook 時，此 Runbook 便會建立自動化作業。</span><span class="sxs-lookup"><span data-stu-id="42de8-148">When you start a runbook in Azure Automation, it creates an automation job.</span></span>  <span data-ttu-id="42de8-149">您可以在解決方案中新增自動化作業資源，以在安裝管理解決方案時自動啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="42de8-149">You can add an automation job resource to your solution to automatically start a runbook when the management solution is installed.</span></span>  <span data-ttu-id="42de8-150">這個方法通常會用來啟動可對解決方案進行初始設定的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="42de8-150">This method is typically used to start runbooks that are used for initial configuration of the solution.</span></span>  <span data-ttu-id="42de8-151">若要定期啟動 Runbook，請建立[排程](#schedules)和[作業排程](#job-schedules)</span><span class="sxs-lookup"><span data-stu-id="42de8-151">To start a runbook at regular intervals, create a [schedule](#schedules) and a [job schedule](#job-schedules)</span></span>

<span data-ttu-id="42de8-152">作業資源的類型為 **Microsoft.Automation/automationAccounts/jobs**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-152">Job resources have a type of **Microsoft.Automation/automationAccounts/jobs** and have the following structure.</span></span>  <span data-ttu-id="42de8-153">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-153">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="42de8-154">下表會說明自動化作業的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-154">The properties for automation jobs are described in the following table.</span></span>

| <span data-ttu-id="42de8-155">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-155">Property</span></span> | <span data-ttu-id="42de8-156">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-156">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-157">Runbook</span><span class="sxs-lookup"><span data-stu-id="42de8-157">runbook</span></span> |<span data-ttu-id="42de8-158">具有要啟動之 Runbook 名稱的單一名稱實體。</span><span class="sxs-lookup"><span data-stu-id="42de8-158">Single name entity with the name of the runbook to start.</span></span> |
| <span data-ttu-id="42de8-159">參數</span><span class="sxs-lookup"><span data-stu-id="42de8-159">parameters</span></span> |<span data-ttu-id="42de8-160">Runbook 所需之每個參數值的實體。</span><span class="sxs-lookup"><span data-stu-id="42de8-160">Entity for each parameter value required by the runbook.</span></span> |

<span data-ttu-id="42de8-161">作業包含 Runbook 名稱和任何要傳送至 Runbook 的參數值。</span><span class="sxs-lookup"><span data-stu-id="42de8-161">The job includes the runbook name and any parameter values to be sent to the runbook.</span></span>  <span data-ttu-id="42de8-162">作業應該[相依於](operations-management-suite-solutions-solution-file.md#resources)正在啟動的 Runbook，因為 Runbook 必須建立於作業之前。</span><span class="sxs-lookup"><span data-stu-id="42de8-162">The job should [depend on](operations-management-suite-solutions-solution-file.md#resources) the runbook that it's starting since the runbook must be created before the job.</span></span>  <span data-ttu-id="42de8-163">如果您有多個應該啟動的 Runbook，您可以藉由讓作業相依於其他任何應該先執行的作業，以定義這些 Runbook 的順序。</span><span class="sxs-lookup"><span data-stu-id="42de8-163">If you have multiple runbooks that should be started you can define their order by having a job depend on any other jobs that should be run first.</span></span>

<span data-ttu-id="42de8-164">作業資源的名稱必須包含通常由參數所指派的 GUID。</span><span class="sxs-lookup"><span data-stu-id="42de8-164">The name of a job resource must contain a GUID which is typically assigned by a parameter.</span></span>  <span data-ttu-id="42de8-165">[在 Operations Management Suite (OMS) 中建立解決方案](operations-management-suite-solutions-solution-file.md#parameters)可讓您深入了解 GUID 參數。</span><span class="sxs-lookup"><span data-stu-id="42de8-165">You can read more about GUID parameters in [Creating solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-solution-file.md#parameters).</span></span>  


## <a name="certificates"></a><span data-ttu-id="42de8-166">憑證</span><span class="sxs-lookup"><span data-stu-id="42de8-166">Certificates</span></span>
<span data-ttu-id="42de8-167">[Azure 自動化憑證](../automation/automation-certificates.md)的類型為 **Microsoft.Automation/automationAccounts/certificates**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-167">[Azure Automation certificates](../automation/automation-certificates.md) have a type of **Microsoft.Automation/automationAccounts/certificates** and have the following structure.</span></span> <span data-ttu-id="42de8-168">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-168">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="42de8-169">下表會說明憑證資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-169">The properties for Certificates resources are described in the following table.</span></span>

| <span data-ttu-id="42de8-170">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-170">Property</span></span> | <span data-ttu-id="42de8-171">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-171">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-172">base64Value</span><span class="sxs-lookup"><span data-stu-id="42de8-172">base64Value</span></span> |<span data-ttu-id="42de8-173">憑證的 Base 64 值。</span><span class="sxs-lookup"><span data-stu-id="42de8-173">Base 64 value for the certificate.</span></span> |
| <span data-ttu-id="42de8-174">thumbprint</span><span class="sxs-lookup"><span data-stu-id="42de8-174">thumbprint</span></span> |<span data-ttu-id="42de8-175">憑證的指紋。</span><span class="sxs-lookup"><span data-stu-id="42de8-175">Thumbprint for the certificate.</span></span> |



## <a name="credentials"></a><span data-ttu-id="42de8-176">認證</span><span class="sxs-lookup"><span data-stu-id="42de8-176">Credentials</span></span>
<span data-ttu-id="42de8-177">[Azure 自動化認證](../automation/automation-credentials.md)的類型為 **Microsoft.Automation/automationAccounts/credentials**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-177">[Azure Automation credentials](../automation/automation-credentials.md) have a type of **Microsoft.Automation/automationAccounts/credentials** and have the following structure.</span></span>  <span data-ttu-id="42de8-178">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-178">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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

<span data-ttu-id="42de8-179">下表會說明認證資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-179">The properties for Credential resources are described in the following table.</span></span>

| <span data-ttu-id="42de8-180">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-180">Property</span></span> | <span data-ttu-id="42de8-181">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-182">userName</span><span class="sxs-lookup"><span data-stu-id="42de8-182">userName</span></span> |<span data-ttu-id="42de8-183">認證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-183">User name for the credential.</span></span> |
| <span data-ttu-id="42de8-184">password</span><span class="sxs-lookup"><span data-stu-id="42de8-184">password</span></span> |<span data-ttu-id="42de8-185">認證的密碼。</span><span class="sxs-lookup"><span data-stu-id="42de8-185">Password for the credential.</span></span> |


## <a name="schedules"></a><span data-ttu-id="42de8-186">排程</span><span class="sxs-lookup"><span data-stu-id="42de8-186">Schedules</span></span>
<span data-ttu-id="42de8-187">[Azure 自動化排程](../automation/automation-schedules.md)的類型為 **Microsoft.Automation/automationAccounts/schedules**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-187">[Azure Automation schedules](../automation/automation-schedules.md) have a type of **Microsoft.Automation/automationAccounts/schedules** and have the the following structure.</span></span> <span data-ttu-id="42de8-188">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-188">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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

<span data-ttu-id="42de8-189">下表會說明排程資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-189">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="42de8-190">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-190">Property</span></span> | <span data-ttu-id="42de8-191">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-191">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-192">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-192">description</span></span> |<span data-ttu-id="42de8-193">排程的選擇性說明。</span><span class="sxs-lookup"><span data-stu-id="42de8-193">Optional description for the schedule.</span></span> |
| <span data-ttu-id="42de8-194">startTime</span><span class="sxs-lookup"><span data-stu-id="42de8-194">startTime</span></span> |<span data-ttu-id="42de8-195">將排程的開始時間指定為 DateTime 物件。</span><span class="sxs-lookup"><span data-stu-id="42de8-195">Specifies the start time of a schedule as a DateTime object.</span></span> <span data-ttu-id="42de8-196">如果可以轉換成有效的 DateTime，即可提供字串。</span><span class="sxs-lookup"><span data-stu-id="42de8-196">A string can be provided if it can be converted to a valid DateTime.</span></span> |
| <span data-ttu-id="42de8-197">isEnabled</span><span class="sxs-lookup"><span data-stu-id="42de8-197">isEnabled</span></span> |<span data-ttu-id="42de8-198">指定是否啟用排程。</span><span class="sxs-lookup"><span data-stu-id="42de8-198">Specifies whether the schedule is enabled.</span></span> |
| <span data-ttu-id="42de8-199">interval</span><span class="sxs-lookup"><span data-stu-id="42de8-199">interval</span></span> |<span data-ttu-id="42de8-200">排程的間隔類型。</span><span class="sxs-lookup"><span data-stu-id="42de8-200">The type of interval for the schedule.</span></span><br><br><span data-ttu-id="42de8-201">day</span><span class="sxs-lookup"><span data-stu-id="42de8-201">day</span></span><br><span data-ttu-id="42de8-202">hour</span><span class="sxs-lookup"><span data-stu-id="42de8-202">hour</span></span> |
| <span data-ttu-id="42de8-203">frequency</span><span class="sxs-lookup"><span data-stu-id="42de8-203">frequency</span></span> |<span data-ttu-id="42de8-204">應觸發排程的頻率 (以天數或時數為單位)。</span><span class="sxs-lookup"><span data-stu-id="42de8-204">Frequency that the schedule should fire in number of days or hours.</span></span> |

<span data-ttu-id="42de8-205">排程的開始時間值必須大於目前的時間。</span><span class="sxs-lookup"><span data-stu-id="42de8-205">Schedules must have a start time with a value greater than the current time.</span></span>  <span data-ttu-id="42de8-206">您無法知道解決方案會在何時安裝，因此不能以變數來提供此值。</span><span class="sxs-lookup"><span data-stu-id="42de8-206">You cannot provide this value with a variable since you would have no way of knowing when it's going to be installed.</span></span>

<span data-ttu-id="42de8-207">在解決方案中使用排程資源時，請使用下列兩種策略的其中一種。</span><span class="sxs-lookup"><span data-stu-id="42de8-207">Use one of the following two strategies when using schedule resources in a solution.</span></span>

- <span data-ttu-id="42de8-208">使用參數來提供排程的開始時間。</span><span class="sxs-lookup"><span data-stu-id="42de8-208">Use a parameter for the start time of the schedule.</span></span>  <span data-ttu-id="42de8-209">這會提示使用者在他們安裝解決方案時提供值。</span><span class="sxs-lookup"><span data-stu-id="42de8-209">This will prompt the user to provide a value when they install the solution.</span></span>  <span data-ttu-id="42de8-210">如果您有多個排程，您可以對它們使用單一參數值。</span><span class="sxs-lookup"><span data-stu-id="42de8-210">If you have multiple schedules, you could use a single parameter value for more than one of them.</span></span>
- <span data-ttu-id="42de8-211">使用會在安裝解決方案時啟動的 Runbook 來建立排程。</span><span class="sxs-lookup"><span data-stu-id="42de8-211">Create the schedules using a runbook that starts when the solution is installed.</span></span>  <span data-ttu-id="42de8-212">這可讓使用者不必指定時間，但您不能在解決方案中包含排程，以便在移除解決方案時將該排程移除。</span><span class="sxs-lookup"><span data-stu-id="42de8-212">This removes the requirement of the user to specify a time, but you can't contain the schedule in your solution so it will be removed when the solution is removed.</span></span>


### <a name="job-schedules"></a><span data-ttu-id="42de8-213">作業排程</span><span class="sxs-lookup"><span data-stu-id="42de8-213">Job schedules</span></span>
<span data-ttu-id="42de8-214">作業排程資源會連結 Runbook 與排程。</span><span class="sxs-lookup"><span data-stu-id="42de8-214">Job schedule resources link a runbook with a schedule.</span></span>  <span data-ttu-id="42de8-215">作業排程資源的類型為 **Microsoft.Automation/automationAccounts/jobSchedules**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-215">They have a type of **Microsoft.Automation/automationAccounts/jobSchedules** and have the the following structure.</span></span>  <span data-ttu-id="42de8-216">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-216">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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


<span data-ttu-id="42de8-217">下表會說明作業排程的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-217">The properties for job schedules are described in the following table.</span></span>

| <span data-ttu-id="42de8-218">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-218">Property</span></span> | <span data-ttu-id="42de8-219">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-219">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-220">排程名稱</span><span class="sxs-lookup"><span data-stu-id="42de8-220">schedule name</span></span> |<span data-ttu-id="42de8-221">包含排程名稱的單一**名稱**實體。</span><span class="sxs-lookup"><span data-stu-id="42de8-221">Single **name** entity with the name of the schedule.</span></span> |
| <span data-ttu-id="42de8-222">Runbook 名稱</span><span class="sxs-lookup"><span data-stu-id="42de8-222">runbook name</span></span>  |<span data-ttu-id="42de8-223">包含 Runbook 名稱的單一**名稱**實體。</span><span class="sxs-lookup"><span data-stu-id="42de8-223">Single **name** entity with the name of the runbook.</span></span>  |



## <a name="variables"></a><span data-ttu-id="42de8-224">變數</span><span class="sxs-lookup"><span data-stu-id="42de8-224">Variables</span></span>
<span data-ttu-id="42de8-225">[Azure 自動化變數](../automation/automation-variables.md)的類型為 **Microsoft.Automation/automationAccounts/variables**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-225">[Azure Automation variables](../automation/automation-variables.md) have a type of **Microsoft.Automation/automationAccounts/variables** and have the following structure.</span></span>  <span data-ttu-id="42de8-226">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-226">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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

<span data-ttu-id="42de8-227">下表會說明變數資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-227">The properties for variable resources are described in the following table.</span></span>

| <span data-ttu-id="42de8-228">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-228">Property</span></span> | <span data-ttu-id="42de8-229">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-229">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-230">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-230">description</span></span> | <span data-ttu-id="42de8-231">變數的選擇性說明。</span><span class="sxs-lookup"><span data-stu-id="42de8-231">Optional description for the variable.</span></span> |
| <span data-ttu-id="42de8-232">isEncrypted</span><span class="sxs-lookup"><span data-stu-id="42de8-232">isEncrypted</span></span> | <span data-ttu-id="42de8-233">指定是否應加密變數。</span><span class="sxs-lookup"><span data-stu-id="42de8-233">Specifies whether the variable should be encrypted.</span></span> |
| <span data-ttu-id="42de8-234">類型</span><span class="sxs-lookup"><span data-stu-id="42de8-234">type</span></span> | <span data-ttu-id="42de8-235">這個屬性目前沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="42de8-235">This property currently has no effect.</span></span>  <span data-ttu-id="42de8-236">變數的資料類型將由初始值所決定。</span><span class="sxs-lookup"><span data-stu-id="42de8-236">The data type of the variable will be determined by the initial value.</span></span> |
| <span data-ttu-id="42de8-237">value</span><span class="sxs-lookup"><span data-stu-id="42de8-237">value</span></span> | <span data-ttu-id="42de8-238">變數的值。</span><span class="sxs-lookup"><span data-stu-id="42de8-238">Value for the variable.</span></span> |

> [!NOTE]
> <span data-ttu-id="42de8-239">**type** 屬性目前不會影響所建立的變數。</span><span class="sxs-lookup"><span data-stu-id="42de8-239">The **type** property currently has no effect on the variable being created.</span></span>  <span data-ttu-id="42de8-240">變數的資料類型將由 value 所決定。</span><span class="sxs-lookup"><span data-stu-id="42de8-240">The data type for the variable will be determined by the value.</span></span>  

<span data-ttu-id="42de8-241">如果您設定變數的初始值，則必須將它設定為正確的資料類型。</span><span class="sxs-lookup"><span data-stu-id="42de8-241">If you set the initial value for the variable, it must be configured as the correct data type.</span></span>  <span data-ttu-id="42de8-242">下表提供允許的不同資料類型和其語法。</span><span class="sxs-lookup"><span data-stu-id="42de8-242">The following table provides the different data types allowable and their syntax.</span></span>  <span data-ttu-id="42de8-243">請注意，JSON 中的值應該一律要用引號括住，並以括號括住任何特殊字元。</span><span class="sxs-lookup"><span data-stu-id="42de8-243">Note that values in JSON are expected to always be enclosed in quotes with any special characters within the quotes.</span></span>  <span data-ttu-id="42de8-244">例如，以括住字串的引號指定字串值 (使用逸出字元 (\\))，並以一組引號指定數值。</span><span class="sxs-lookup"><span data-stu-id="42de8-244">For example, a string value would be specified by quotes around the string (using the escape character (\\)) while a numeric value would be specified with one set of quotes.</span></span>

| <span data-ttu-id="42de8-245">資料類型</span><span class="sxs-lookup"><span data-stu-id="42de8-245">Data type</span></span> | <span data-ttu-id="42de8-246">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-246">Description</span></span> | <span data-ttu-id="42de8-247">範例</span><span class="sxs-lookup"><span data-stu-id="42de8-247">Example</span></span> | <span data-ttu-id="42de8-248">解析成</span><span class="sxs-lookup"><span data-stu-id="42de8-248">Resolves to</span></span> |
|:--|:--|:--|:--|
| <span data-ttu-id="42de8-249">字串</span><span class="sxs-lookup"><span data-stu-id="42de8-249">string</span></span>   | <span data-ttu-id="42de8-250">以雙引號括住值。</span><span class="sxs-lookup"><span data-stu-id="42de8-250">Enclose value in double quotes.</span></span>  | <span data-ttu-id="42de8-251">"\"Hello world\""</span><span class="sxs-lookup"><span data-stu-id="42de8-251">"\"Hello world\""</span></span> | <span data-ttu-id="42de8-252">"Hello world"</span><span class="sxs-lookup"><span data-stu-id="42de8-252">"Hello world"</span></span> |
| <span data-ttu-id="42de8-253">numeric</span><span class="sxs-lookup"><span data-stu-id="42de8-253">numeric</span></span>  | <span data-ttu-id="42de8-254">以單引號括住數值。</span><span class="sxs-lookup"><span data-stu-id="42de8-254">Numeric value with single quotes.</span></span>| <span data-ttu-id="42de8-255">"64"</span><span class="sxs-lookup"><span data-stu-id="42de8-255">"64"</span></span> | <span data-ttu-id="42de8-256">64</span><span class="sxs-lookup"><span data-stu-id="42de8-256">64</span></span> |
| <span data-ttu-id="42de8-257">布林值</span><span class="sxs-lookup"><span data-stu-id="42de8-257">boolean</span></span>  | <span data-ttu-id="42de8-258">以引號括住 **true** 或 **false**。</span><span class="sxs-lookup"><span data-stu-id="42de8-258">**true** or **false** in quotes.</span></span>  <span data-ttu-id="42de8-259">請注意，此值必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="42de8-259">Note that this value must be lowercase.</span></span> | <span data-ttu-id="42de8-260">"true"</span><span class="sxs-lookup"><span data-stu-id="42de8-260">"true"</span></span> | <span data-ttu-id="42de8-261">true</span><span class="sxs-lookup"><span data-stu-id="42de8-261">true</span></span> |
| <span data-ttu-id="42de8-262">datetime</span><span class="sxs-lookup"><span data-stu-id="42de8-262">datetime</span></span> | <span data-ttu-id="42de8-263">序列化的日期值。</span><span class="sxs-lookup"><span data-stu-id="42de8-263">Serialized date value.</span></span><br><span data-ttu-id="42de8-264">您可以在 PowerShell 中使用 ConvertTo-Json Cmdlet，以針對特定日期產生這個值。</span><span class="sxs-lookup"><span data-stu-id="42de8-264">You can use the ConvertTo-Json cmdlet in PowerShell to generate this value for a particular date.</span></span><br><span data-ttu-id="42de8-265">範例：get-date "5/24/2017 13:14:57" \\</span><span class="sxs-lookup"><span data-stu-id="42de8-265">Example: get-date "5/24/2017 13:14:57" \\</span></span>| <span data-ttu-id="42de8-266">ConvertTo-Json</span><span class="sxs-lookup"><span data-stu-id="42de8-266">ConvertTo-Json</span></span> | <span data-ttu-id="42de8-267">"\\/Date(1495656897378)\\/"</span><span class="sxs-lookup"><span data-stu-id="42de8-267">"\\/Date(1495656897378)\\/"</span></span> | <span data-ttu-id="42de8-268">2017-05-24 13:14:57</span><span class="sxs-lookup"><span data-stu-id="42de8-268">2017-05-24 13:14:57</span></span> |

## <a name="modules"></a><span data-ttu-id="42de8-269">模組</span><span class="sxs-lookup"><span data-stu-id="42de8-269">Modules</span></span>
<span data-ttu-id="42de8-270">您的管理解決方案不需定義您的 Runbook 所用的[全域模組](../automation/automation-integration-modules.md)，因為您永遠可以在自動化帳戶中使用這些模組。</span><span class="sxs-lookup"><span data-stu-id="42de8-270">Your management solution does not need to define [global modules](../automation/automation-integration-modules.md) used by your runbooks because they will always be available in your Automation account.</span></span>  <span data-ttu-id="42de8-271">對於 Runbook 所使用的其他任何模組，您不需要包含其資源。</span><span class="sxs-lookup"><span data-stu-id="42de8-271">You do need to include a resource for any other module used by your runbooks.</span></span>

<span data-ttu-id="42de8-272">[整合模組](../automation/automation-integration-modules.md)的類型為 **Microsoft.Automation/automationAccounts/modules**，且具有下列結構。</span><span class="sxs-lookup"><span data-stu-id="42de8-272">[Integration modules](../automation/automation-integration-modules.md) have a type of **Microsoft.Automation/automationAccounts/modules** and have the following structure.</span></span>  <span data-ttu-id="42de8-273">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="42de8-273">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span>

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


<span data-ttu-id="42de8-274">下表會說明模組資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="42de8-274">The properties for module resources are described in the following table.</span></span>

| <span data-ttu-id="42de8-275">屬性</span><span class="sxs-lookup"><span data-stu-id="42de8-275">Property</span></span> | <span data-ttu-id="42de8-276">說明</span><span class="sxs-lookup"><span data-stu-id="42de8-276">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="42de8-277">contentLink</span><span class="sxs-lookup"><span data-stu-id="42de8-277">contentLink</span></span> |<span data-ttu-id="42de8-278">指定模組的內容。</span><span class="sxs-lookup"><span data-stu-id="42de8-278">Specifies the content of the module.</span></span> <br><br><span data-ttu-id="42de8-279">uri - 模組內容的 Uri。</span><span class="sxs-lookup"><span data-stu-id="42de8-279">uri - Uri to the content of the module.</span></span>  <span data-ttu-id="42de8-280">這會是 PowerShell 和 Script Runbook 的 .ps1 檔案，以及 Graph Runbook 的已匯出圖形化 Runbook 檔案。</span><span class="sxs-lookup"><span data-stu-id="42de8-280">This will be a .ps1 file for PowerShell and Script runbooks, and an exported graphical runbook file for a Graph runbook.</span></span>  <br> <span data-ttu-id="42de8-281">版本 - 自有追蹤的模組版本。</span><span class="sxs-lookup"><span data-stu-id="42de8-281">version - Version of the module for your own tracking.</span></span> |

<span data-ttu-id="42de8-282">Runbook 應該相依於模組資源，以確保模組資源會比 Runbook 還早建立。</span><span class="sxs-lookup"><span data-stu-id="42de8-282">The runbook should depend on the module resource to ensure that it's created before the runbook.</span></span>

### <a name="updating-modules"></a><span data-ttu-id="42de8-283">更新模組</span><span class="sxs-lookup"><span data-stu-id="42de8-283">Updating modules</span></span>
<span data-ttu-id="42de8-284">如果您更新的管理解決方案包含使用排程的 Runbook，而且新版的解決方案具有該 Runbook 所用的新模組，則 Runbook 可能會使用舊版的模組。</span><span class="sxs-lookup"><span data-stu-id="42de8-284">If you update a management solution that includes a runbook that uses a schedule, and the new version of your solution has a new module used by that runbook, then the runbook may use the old version of the module.</span></span>  <span data-ttu-id="42de8-285">您應該在您的解決方案中納入下列 Runbook，並建立一項作業，以在任何其他 Runbook 之前執行這些 Runbook。</span><span class="sxs-lookup"><span data-stu-id="42de8-285">You should include the following runbooks in your solution and create a job to run them before any other runbooks.</span></span>  <span data-ttu-id="42de8-286">這可確保在載入 Runbook 之前，會視需要更新任何模組。</span><span class="sxs-lookup"><span data-stu-id="42de8-286">This will ensure that any modules are updated as required before the runbooks are loaded.</span></span>

* <span data-ttu-id="42de8-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) 可確保您解決方案中 Runbook 使用的所有模組都是最新版本。</span><span class="sxs-lookup"><span data-stu-id="42de8-287">[Update-ModulesinAutomationToLatestVersion](https://www.powershellgallery.com/packages/Update-ModulesInAutomationToLatestVersion/1.03/DisplayScript) will ensure that all of the modules used by runbooks in your solution are the latest version.</span></span>  
* <span data-ttu-id="42de8-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) 可重新註冊所有的排程資源，以確保已連結到這些資源的 Runbook 使用最新模組。</span><span class="sxs-lookup"><span data-stu-id="42de8-288">[ReRegisterAutomationSchedule-MS-Mgmt](https://www.powershellgallery.com/packages/ReRegisterAutomationSchedule-MS-Mgmt/1.0/DisplayScript) will reregister all of the schedule resources to ensure that the runbooks linked to them with use the latest modules.</span></span>




## <a name="sample"></a><span data-ttu-id="42de8-289">範例</span><span class="sxs-lookup"><span data-stu-id="42de8-289">Sample</span></span>
<span data-ttu-id="42de8-290">以下是解決方案的範例，其中包含下列資源：</span><span class="sxs-lookup"><span data-stu-id="42de8-290">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="42de8-291">Runbook。</span><span class="sxs-lookup"><span data-stu-id="42de8-291">Runbook.</span></span>  <span data-ttu-id="42de8-292">這是儲存在公用 GitHub 儲存機制的 Runbook 範例。</span><span class="sxs-lookup"><span data-stu-id="42de8-292">This is a sample runbook stored in a public GitHub repository.</span></span>
- <span data-ttu-id="42de8-293">在安裝解決方案時會啟動 Runbook 的自動化作業。</span><span class="sxs-lookup"><span data-stu-id="42de8-293">Automation job that starts the runbook when the solution is installed.</span></span>
- <span data-ttu-id="42de8-294">用來定期啟動 Runbook 的排程和作業排程。</span><span class="sxs-lookup"><span data-stu-id="42de8-294">Schedule and job schedule to start the runbook at regular intervals.</span></span>
- <span data-ttu-id="42de8-295">憑證。</span><span class="sxs-lookup"><span data-stu-id="42de8-295">Certificate.</span></span>
- <span data-ttu-id="42de8-296">認證。</span><span class="sxs-lookup"><span data-stu-id="42de8-296">Credential.</span></span>
- <span data-ttu-id="42de8-297">變數。</span><span class="sxs-lookup"><span data-stu-id="42de8-297">Variable.</span></span>
- <span data-ttu-id="42de8-298">模組。</span><span class="sxs-lookup"><span data-stu-id="42de8-298">Module.</span></span>  <span data-ttu-id="42de8-299">這個 [OMSIngestionAPI 模組](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5)可用來將資料寫入 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="42de8-299">This is the [OMSIngestionAPI module](https://www.powershellgallery.com/packages/OMSIngestionAPI/1.5) for writing data to Log Analytics.</span></span> 

<span data-ttu-id="42de8-300">此範例會使用[標準的解決方案參數](operations-management-suite-solutions-solution-file.md#parameters)變數，相對於資源定義中的硬式編碼值，這類變數常用於解決方案中。</span><span class="sxs-lookup"><span data-stu-id="42de8-300">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>


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
            "description": "GUID for the schedule link to runbook.",
            "control": "guid"
          }
        },
        "runbookJobGuid": {
          "type": "string",
          "metadata": {
            "description": "GUID for the runbook job.",
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




## <a name="next-steps"></a><span data-ttu-id="42de8-301">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42de8-301">Next steps</span></span>
* <span data-ttu-id="42de8-302">[將檢視新增至您的解決方案](operations-management-suite-solutions-resources-views.md)，以將所收集的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="42de8-302">[Add a view to your solution](operations-management-suite-solutions-resources-views.md) to visualize collected data.</span></span>
