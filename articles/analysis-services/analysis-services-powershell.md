---
title: "使用 PowerShell 的 Azure Analysis Services aaaManage |Microsoft 文件"
description: "使用 PowerShell 的 Azure Analysis Services 管理。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>使用 PowerShell 管理 Azure Analysis Services

本文說明的 PowerShell cmdlet 使用 tooperform Azure Analysis Services 伺服器和資料庫管理工作。 

伺服器管理工作，例如建立或刪除伺服器、 暫停或繼續伺服器作業，或變更 hello 服務層級 （層級） 會使用 Azure 資源管理員 (AzureRM) cmdlet。 管理資料庫，例如加入或移除角色成員、 處理或資料分割使用的 cmdlet 中包含的其他工作 hello 相同 SQL Server Analysis Services 的 SqlServer 模組。

## <a name="permissions"></a>權限
大部分的 PowerShell 工作需要您所管理的 hello Analysis Services 伺服器上具有管理員權限。 排定的 PowerShell 工作都是自動的作業。 hello Analysis Services 伺服器上，執行 hello 排程器的 hello 帳戶必須具有系統管理員權限。 

伺服器作業使用 AzureRm cmdlet，為您的帳戶或執行排程器的 hello 帳戶也必須屬於 toohello 擁有者角色中的 hello 資源[所有存取控制 (RBAC)](../active-directory/role-based-access-control-what-is.md)。 

## <a name="server-operations"></a>伺服器作業 
Azure Analysis Services 指令程式會包含在 hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)元件的模組。 tooinstall AzureRM cmdlet 模組，請參閱[Azure 資源管理員 cmdlet](/powershell/azure/overview) hello PowerShell 資源庫中。

|Cmdlet|說明| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|匯出記錄 toofile。| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|取得伺服器執行個體的詳細資料。|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|建立伺服器執行個體。|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|移除伺服器執行個體。|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|暫停伺服器執行個體。| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|繼續伺服器執行個體。|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|修改伺服器執行個體。|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|測試 hello 存在伺服器執行個體。| 

## <a name="database-operations"></a>資料庫作業

Azure Analysis Services 資料庫作業使用 hello 相同[SqlServer](https://www.powershellgallery.com/packages/SqlServer) SQL Server Analysis Services 的模組。 不過，Azure Analysis Services 並不支援所有的 Cmdlet。 

hello SqlServer 模組提供特定工作的資料庫管理指令程式以及 hello 一般用途 Invoke-ascmd 指令程式可接受表格式模型指令碼語言 」 (TMSL) 查詢或指令碼。 hello hello SqlServer 模組中的下列指令程式支援 Azure Analysis Services。

  
|Cmdlet|說明|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|加入成員 tooa 資料庫角色。| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|備份 Analysis Services 資料庫。|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|從資料庫角色移除成員。|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|執行 TMSL 指令碼。|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|處理資料庫。|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|處理資料分割。| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|處理資料表。|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|合併資料分割。|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|還原 Analysis Services 資料庫。| 
  

## <a name="related-information"></a>相關資訊

* [下載 SQL Server PowerShell 模組](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [下載 SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [PowerShell 資源庫中的 SqlServer 模組](https://www.powershellgallery.com/packages/SqlServer)    
* [相容性層級 1200 和更高層級的表格式模型程式設計](https://msdn.microsoft.com/library/mt712541.aspx)
