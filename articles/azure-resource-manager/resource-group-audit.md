---
title: "檢視 Azure 活動記錄以監視資源 | Microsoft Docs"
description: "使用活動記錄檢閱使用者動作和錯誤。 顯示 Azure 入口網站 PowerShell、Azure CLI 和 REST。"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="1cedf-104">檢視活動記錄以稽核對資源的動作</span><span class="sxs-lookup"><span data-stu-id="1cedf-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="1cedf-105">透過活動記錄檔，您可以判斷︰</span><span class="sxs-lookup"><span data-stu-id="1cedf-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="1cedf-106">訂用帳戶的資源在進行哪些作業</span><span class="sxs-lookup"><span data-stu-id="1cedf-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="1cedf-107">誰起始作業 (雖然由後端服務起始的作業不會傳回使用者做為呼叫端)</span><span class="sxs-lookup"><span data-stu-id="1cedf-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="1cedf-108">作業進行的時間</span><span class="sxs-lookup"><span data-stu-id="1cedf-108">when the operation occurred</span></span>
* <span data-ttu-id="1cedf-109">作業的狀態</span><span class="sxs-lookup"><span data-stu-id="1cedf-109">the status of the operation</span></span>
* <span data-ttu-id="1cedf-110">其他可能協助您研究作業的屬性值</span><span class="sxs-lookup"><span data-stu-id="1cedf-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="1cedf-111">您可以透過入口網站、PowerShell、Azure CLI、Insights REST API 或 [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/)擷取活動記錄檔中的資訊。</span><span class="sxs-lookup"><span data-stu-id="1cedf-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="1cedf-112">入口網站</span><span class="sxs-lookup"><span data-stu-id="1cedf-112">Portal</span></span>
1. <span data-ttu-id="1cedf-113">若要透過入口網站檢視活動記錄，請選取 [監視]。</span><span class="sxs-lookup"><span data-stu-id="1cedf-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![檢視活動記錄檔](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="1cedf-115">或者，若要自動篩選特定資源或資源群組的活動記錄檔，請從該資源刀鋒視窗中選取 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="1cedf-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="1cedf-116">請注意，選取的資源會自動篩選活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1cedf-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![依資源篩選](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="1cedf-118">在 [活動記錄] 刀鋒視窗中，您會看到最近作業的摘要。</span><span class="sxs-lookup"><span data-stu-id="1cedf-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![顯示動作](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="1cedf-120">若要限制顯示的作業數目，可以選取不同的條件。</span><span class="sxs-lookup"><span data-stu-id="1cedf-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="1cedf-121">例如，下圖顯示變更 [時間範圍] 和 [事件起始者] 欄位，以檢視特定使用者或應用程式在上個月所採取的動作。</span><span class="sxs-lookup"><span data-stu-id="1cedf-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="1cedf-122">選取 [套用]  以檢視查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="1cedf-122">Select **Apply** to view the results of your query.</span></span>
   
    ![設定篩選選項](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="1cedf-124">如果您稍後需要再執行查詢，請選取 [儲存]  並給查詢一個名稱。</span><span class="sxs-lookup"><span data-stu-id="1cedf-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![儲存查詢](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="1cedf-126">若要快速執行查詢，可以選取其中一個內建的查詢，例如失敗的部署。</span><span class="sxs-lookup"><span data-stu-id="1cedf-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![選取查詢](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="1cedf-128">選取的查詢會自動設定必要的篩選值。</span><span class="sxs-lookup"><span data-stu-id="1cedf-128">The selected query automatically sets the required filter values.</span></span>

    ![檢視部署錯誤](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="1cedf-130">選取其中一項作業以查看事件的摘要。</span><span class="sxs-lookup"><span data-stu-id="1cedf-130">Select one of the operations to see a summary of the event.</span></span>

    ![檢視作業](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="1cedf-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cedf-132">PowerShell</span></span>
1. <span data-ttu-id="1cedf-133">若要擷取記錄檔項目，請執行 **Get-AzureRmLog** 命令。</span><span class="sxs-lookup"><span data-stu-id="1cedf-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="1cedf-134">您可提供額外的參數來篩選項目清單。</span><span class="sxs-lookup"><span data-stu-id="1cedf-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="1cedf-135">如果未指定開始和結束時間，則會傳回最後一個小時的項目。</span><span class="sxs-lookup"><span data-stu-id="1cedf-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="1cedf-136">例如，若要在過去一小時執行期間擷取資源群組的作業：</span><span class="sxs-lookup"><span data-stu-id="1cedf-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="1cedf-137">下列範例示範如何使用活動記錄來研究指定期間所採取的作業。</span><span class="sxs-lookup"><span data-stu-id="1cedf-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="1cedf-138">以日期格式指定開始和結束日期。</span><span class="sxs-lookup"><span data-stu-id="1cedf-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="1cedf-139">或者，您可以使用日期函數來指定日期範圍，例如過去 14 天。</span><span class="sxs-lookup"><span data-stu-id="1cedf-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="1cedf-140">視您指定的開始時間而定，先前的命令可以傳回該資源群組的一長串作業。</span><span class="sxs-lookup"><span data-stu-id="1cedf-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="1cedf-141">您可以提供搜尋準則，以篩選您所尋找的結果。</span><span class="sxs-lookup"><span data-stu-id="1cedf-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="1cedf-142">例如，假如您想研究 Web 應用程式停止執行的方式，可以執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="1cedf-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="1cedf-143">並藉此了解停止動作是由 someone@contoso.com 所執行。</span><span class="sxs-lookup"><span data-stu-id="1cedf-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="1cedf-144">您可以查閱由特定使用者採取的動作，即使是針對已不存在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1cedf-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="1cedf-145">您可以篩選失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="1cedf-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="1cedf-146">您可以查看該項目的狀態訊息，專注於一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="1cedf-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="1cedf-147">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="1cedf-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="1cedf-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1cedf-148">Azure CLI</span></span>
* <span data-ttu-id="1cedf-149">若要擷取記錄檔項目，您可執行 **azure group log show** 命令。</span><span class="sxs-lookup"><span data-stu-id="1cedf-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="1cedf-150">REST API</span><span class="sxs-lookup"><span data-stu-id="1cedf-150">REST API</span></span>
<span data-ttu-id="1cedf-151">可用來處理活動記錄檔的 REST 作業屬於 [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)的一部分。</span><span class="sxs-lookup"><span data-stu-id="1cedf-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="1cedf-152">若要擷取活動記錄檔事件，請參閱 [列出訂用帳戶中的管理事件](https://msdn.microsoft.com/library/azure/dn931934.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1cedf-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cedf-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1cedf-153">Next steps</span></span>
* <span data-ttu-id="1cedf-154">Azure 活動記錄檔可以搭配 Power BI 用來更深入了解訂用帳戶中的動作。</span><span class="sxs-lookup"><span data-stu-id="1cedf-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="1cedf-155">請參閱 [在 Power BI 和其他工具中檢視和分析 Azure 活動記錄檔](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)。</span><span class="sxs-lookup"><span data-stu-id="1cedf-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="1cedf-156">如要了解如何設定安全性原則，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="1cedf-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="1cedf-157">若要深入了解檢視部署作業的命令，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="1cedf-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="1cedf-158">若要了解如何防止刪除所有使用者的資源，請參閱 [使用 Azure Resource Manager 鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="1cedf-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

