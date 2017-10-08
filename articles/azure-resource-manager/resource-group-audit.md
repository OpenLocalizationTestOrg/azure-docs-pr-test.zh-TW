---
title: "aaaView Azure 活動記錄 toomonitor 資源 |Microsoft 文件"
description: "使用 hello 活動記錄檔 tooreview 使用者動作和錯誤。 顯示 Azure 入口網站 PowerShell、Azure CLI 和 REST。"
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
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="f8bc7-104">檢視活動記錄在資源上的 tooaudit 動作</span><span class="sxs-lookup"><span data-stu-id="f8bc7-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="f8bc7-105">透過活動記錄檔，您可以判斷︰</span><span class="sxs-lookup"><span data-stu-id="f8bc7-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="f8bc7-106">您的訂用帳戶中的 hello 資源進行哪些作業</span><span class="sxs-lookup"><span data-stu-id="f8bc7-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="f8bc7-107">（雖然後端服務所起始的作業不會傳回使用者為 hello 呼叫者），誰 hello 作業</span><span class="sxs-lookup"><span data-stu-id="f8bc7-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="f8bc7-108">Hello 作業發生時</span><span class="sxs-lookup"><span data-stu-id="f8bc7-108">when hello operation occurred</span></span>
* <span data-ttu-id="f8bc7-109">hello hello 作業狀態</span><span class="sxs-lookup"><span data-stu-id="f8bc7-109">hello status of hello operation</span></span>
* <span data-ttu-id="f8bc7-110">其他屬性，以幫助您 hello 值研究 hello 作業</span><span class="sxs-lookup"><span data-stu-id="f8bc7-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="f8bc7-111">您可以從 hello 入口網站、 PowerShell、 CLI Azure Insights REST API，透過 hello 活動記錄檔中擷取資訊或[Insights.NET 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Insights/)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="f8bc7-112">入口網站</span><span class="sxs-lookup"><span data-stu-id="f8bc7-112">Portal</span></span>
1. <span data-ttu-id="f8bc7-113">tooview hello 活動記錄檔，透過 hello 入口網站中，選取**監視器**。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![檢視活動記錄檔](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="f8bc7-115">或者，tooautomatically 篩選 hello 活動記錄檔以取得特定資源或資源群組中，選取**活動記錄檔**該資源刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="f8bc7-116">請注意該 hello 活動記錄檔會自動篩選所選取的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![依資源篩選](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="f8bc7-118">在 hello**活動記錄檔**刀鋒視窗中，您看到最近作業的摘要。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![顯示動作](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="f8bc7-120">作業顯示，toorestrict hello 數目選取不同的條件。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="f8bc7-121">比方說，hello 下列影像顯示 hello **Timespan**和**由事件初始化**欄位變更 tooview hello 的動作的特定使用者或應用程式 hello 過去一個月。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="f8bc7-122">選取**套用**tooview hello 查詢結果。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![設定篩選選項](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="f8bc7-124">如果您稍後需要 toorun hello 查詢，請選取**儲存**並提供 hello 查詢名稱。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![儲存查詢](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="f8bc7-126">tooquickly 執行查詢，您可以選取其中一個 hello 內建查詢，例如部署失敗。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![選取查詢](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="f8bc7-128">hello 選取的查詢會自動設定所需的 hello 篩選值。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-128">hello selected query automatically sets hello required filter values.</span></span>

    ![檢視部署錯誤](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="f8bc7-130">選取其中一個 hello 作業 toosee hello 事件的摘要。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![檢視作業](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="f8bc7-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8bc7-132">PowerShell</span></span>
1. <span data-ttu-id="f8bc7-133">tooretrieve 記錄項目，執行 hello **Get AzureRmLog**命令。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="f8bc7-134">您提供其他參數 toofilter hello 的項目清單。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="f8bc7-135">如果您未指定開始和結束時間，則會傳回 hello 過去一小時內的項目。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="f8bc7-136">例如，tooretrieve hello 操作的資源群組在 hello 過去一小時期間執行：</span><span class="sxs-lookup"><span data-stu-id="f8bc7-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="f8bc7-137">下列範例中的 hello 顯示 toouse hello 活動記錄 tooresearch 作業指定的時間期間採取的方式。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="f8bc7-138">hello 開始和結束日期被指定日期格式。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="f8bc7-139">或者，您可以使用日期函數 toospecify hello 日期範圍，例如 hello 過去 14 天。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="f8bc7-140">根據您指定 hello 開始時間、 hello 先前的命令可以傳回一長串的 hello 資源群組的作業。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="f8bc7-141">您可以篩選 hello 結果以進行您所尋找的提供搜尋準則。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="f8bc7-142">比方說，如果您嘗試的 tooresearch 如何停止 web 應用程式，您可以執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f8bc7-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="f8bc7-143">並藉此了解停止動作是由 someone@contoso.com 所執行。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="f8bc7-144">您可以查詢特定的使用者，即使對於已不存在的資源群組所採取的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="f8bc7-145">您可以篩選失敗的作業。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="f8bc7-146">您可以專注於一個錯誤，藉由查看該項目 hello 狀態訊息。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="f8bc7-147">它會傳回：</span><span class="sxs-lookup"><span data-stu-id="f8bc7-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="f8bc7-148">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f8bc7-148">Azure CLI</span></span>
* <span data-ttu-id="f8bc7-149">tooretrieve 記錄項目，執行 hello **azure 群組的記錄檔顯示**命令。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="f8bc7-150">REST API</span><span class="sxs-lookup"><span data-stu-id="f8bc7-150">REST API</span></span>
<span data-ttu-id="f8bc7-151">hello REST 作業，以使用 hello 活動記錄屬於 hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="f8bc7-152">tooretrieve 活動記錄事件，請參閱[列出訂用帳戶中的 hello 管理事件](https://msdn.microsoft.com/library/azure/dn931934.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8bc7-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8bc7-153">Next steps</span></span>
* <span data-ttu-id="f8bc7-154">Azure 活動記錄檔可以搭配 Power BI toogain 更深入了解您的訂用帳戶中的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="f8bc7-155">請參閱 [在 Power BI 和其他工具中檢視和分析 Azure 活動記錄檔](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="f8bc7-156">請參閱有關設定安全性原則 toolearn [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="f8bc7-157">toolearn 需 hello 命令檢視部署作業，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="f8bc7-158">如何 tooprevent 刪除資源，以針對所有使用者，請參閱的 toolearn[鎖定資源與 Azure 資源管理員](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="f8bc7-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

