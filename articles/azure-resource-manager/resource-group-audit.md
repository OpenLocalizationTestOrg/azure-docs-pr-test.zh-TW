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
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>檢視活動記錄在資源上的 tooaudit 動作
透過活動記錄檔，您可以判斷︰

* 您的訂用帳戶中的 hello 資源進行哪些作業
* （雖然後端服務所起始的作業不會傳回使用者為 hello 呼叫者），誰 hello 作業
* Hello 作業發生時
* hello hello 作業狀態
* 其他屬性，以幫助您 hello 值研究 hello 作業

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

您可以從 hello 入口網站、 PowerShell、 CLI Azure Insights REST API，透過 hello 活動記錄檔中擷取資訊或[Insights.NET 程式庫](https://www.nuget.org/packages/Microsoft.Azure.Insights/)。

## <a name="portal"></a>入口網站
1. tooview hello 活動記錄檔，透過 hello 入口網站中，選取**監視器**。
   
    ![檢視活動記錄檔](./media/resource-group-audit/select-monitor.png)

   或者，tooautomatically 篩選 hello 活動記錄檔以取得特定資源或資源群組中，選取**活動記錄檔**該資源刀鋒視窗。 請注意該 hello 活動記錄檔會自動篩選所選取的 hello 資源。
   
    ![依資源篩選](./media/resource-group-audit/filtered-by-resource.png)
2. 在 hello**活動記錄檔**刀鋒視窗中，您看到最近作業的摘要。
   
    ![顯示動作](./media/resource-group-audit/audit-summary.png)
3. 作業顯示，toorestrict hello 數目選取不同的條件。 比方說，hello 下列影像顯示 hello **Timespan**和**由事件初始化**欄位變更 tooview hello 的動作的特定使用者或應用程式 hello 過去一個月。 選取**套用**tooview hello 查詢結果。
   
    ![設定篩選選項](./media/resource-group-audit/set-filter.png)

4. 如果您稍後需要 toorun hello 查詢，請選取**儲存**並提供 hello 查詢名稱。
   
    ![儲存查詢](./media/resource-group-audit/save-query.png)
5. tooquickly 執行查詢，您可以選取其中一個 hello 內建查詢，例如部署失敗。

    ![選取查詢](./media/resource-group-audit/select-quick-query.png)

   hello 選取的查詢會自動設定所需的 hello 篩選值。

    ![檢視部署錯誤](./media/resource-group-audit/view-failed-deployment.png)   

6. 選取其中一個 hello 作業 toosee hello 事件的摘要。

    ![檢視作業](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. tooretrieve 記錄項目，執行 hello **Get AzureRmLog**命令。 您提供其他參數 toofilter hello 的項目清單。 如果您未指定開始和結束時間，則會傳回 hello 過去一小時內的項目。 例如，tooretrieve hello 操作的資源群組在 hello 過去一小時期間執行：

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    下列範例中的 hello 顯示 toouse hello 活動記錄 tooresearch 作業指定的時間期間採取的方式。 hello 開始和結束日期被指定日期格式。

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    或者，您可以使用日期函數 toospecify hello 日期範圍，例如 hello 過去 14 天。
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. 根據您指定 hello 開始時間、 hello 先前的命令可以傳回一長串的 hello 資源群組的作業。 您可以篩選 hello 結果以進行您所尋找的提供搜尋準則。 比方說，如果您嘗試的 tooresearch 如何停止 web 應用程式，您可以執行下列命令的 hello:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    並藉此了解停止動作是由 someone@contoso.com 所執行。 

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

3. 您可以查詢特定的使用者，即使對於已不存在的資源群組所採取的 hello 動作。

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. 您可以篩選失敗的作業。

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. 您可以專注於一個錯誤，藉由查看該項目 hello 狀態訊息。
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    它會傳回：
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>Azure CLI
* tooretrieve 記錄項目，執行 hello **azure 群組的記錄檔顯示**命令。

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>REST API
hello REST 作業，以使用 hello 活動記錄屬於 hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx)。 tooretrieve 活動記錄事件，請參閱[列出訂用帳戶中的 hello 管理事件](https://msdn.microsoft.com/library/azure/dn931934.aspx)。

## <a name="next-steps"></a>後續步驟
* Azure 活動記錄檔可以搭配 Power BI toogain 更深入了解您的訂用帳戶中的 hello 動作。 請參閱 [在 Power BI 和其他工具中檢視和分析 Azure 活動記錄檔](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)。
* 請參閱有關設定安全性原則 toolearn [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。
* toolearn 需 hello 命令檢視部署作業，請參閱[檢視部署作業](resource-manager-deployment-operations.md)。
* 如何 tooprevent 刪除資源，以針對所有使用者，請參閱的 toolearn[鎖定資源與 Azure 資源管理員](resource-group-lock-resources.md)。

