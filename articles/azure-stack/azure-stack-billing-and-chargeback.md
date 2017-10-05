---
title: "Azure Stack 中的客戶帳務與退款 | Microsoft Docs"
description: "了解如何從 Azure Stack 擷取資源使用量資訊。"
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: fd2db137948490707a2f4799535062aeef4509e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="usage-and-billing-in-azure-stack"></a>Azure Stack 中的使用量與計費

使用量代表使用者取用的資源數量。 Azure Stack 會收集每個使用者的使用量資訊，並使用該資訊向使用者收費。 此文章說明如何針對資源使用量向 Azure Stack 使用者收費，以及如何存取帳單資訊以進行分析、退款等作業。

Azure Stack 包含針對所有資源收集並彙總使用量資料的基礎架構。 您可以使用帳單配接器存取此資料，並將資料匯出到帳單系統，或將資料匯出到像 Microsoft Power BI 這樣的商務智慧工具。 匯出之後，此帳單資訊就會用於分析，或傳送到退款系統。

![將 Azure Stack 連接至帳單應用程式之帳單配接器的概念模型](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a>我可以找到哪些使用量資訊，以及如何尋找？

Azure Stack 資源提供者 (例如計算、儲存體及網路) 會以每小時為間隔，針對每個訂用帳戶產生使用量資料。 使用量資料包含和所使用資源有關的資訊，例如資源名稱、計量名稱、計量識別碼、已使用數量等等。若要深入了解計量識別碼資源，請參閱[使用情況 API 常見問題集](azure-stack-usage-related-faq.md)文章。 

收集到使用量資料之後，就會將資料[回報給 Azure](azure-stack-usage-reporting.md)，以產生可透過 Azure 計費入口網站檢視的帳單。 Azure 計費入口網站只會顯示可收費資源的使用量資料。 除了可收費資源之外，Azure Stack 可擷取更廣泛資源的使用量資料，您可以透過 REST API 或 PowerShell，在 Azure Stack 環境中存取那些資料。 Azure Stack 雲端系統管理員可以擷取所有使用者訂用帳戶的使用量資料，而使用者則只能取得他們自己的使用量詳細資料。

## <a name="retrieve-usage-information"></a>擷取使用量資訊

若要產生使用量資料，您應該有正在執行並使用系統的資源。 如果不確定您是否有任何資源正在 Azure Stack Marketplace 中執行，請部署虛擬機器 (VM)，並檢查 VM 監控刀鋒視窗以確定它正在執行。 請使用下列 PowerShell Cmdlet 檢視使用量資料：

1. [安裝適用於 Azure Stack 的 PowerShell](azure-stack-powershell-install.md)
2. * [設定 Azure Stack 使用者](azure-stack-powershell-configure-user.md)或 [Azure Stack 操作員](azure-stack-powershell-configure-admin.md) 的 PowerShell 環境 
3. 若要擷取使用量資料，請使用 [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell Cmdlet：
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   如果有使用量資料，就會傳回資料，如以下螢幕擷取畫面所示： 
   
   ![使用量彙總](media/azure-stack-billing-and-chargeback/image2.png)
   
   PowerShell 針對每個呼叫傳回 1,000 行使用量。 您可以使用連續參數擷取超過 1,000 行

## <a name="next-steps"></a>後續步驟

[向 Azure 回報 Azure Stack 使用量資料](azure-stack-usage-reporting.md)

[提供者資源使用情況 API](azure-stack-provider-resource-api.md)

[租用戶資源使用情況 API](azure-stack-tenant-resource-usage-api.md)

[使用量相關常見問題集](azure-stack-usage-related-faq.md)

