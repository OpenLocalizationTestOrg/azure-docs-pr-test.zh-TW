---
title: "使用 Azure 自動化 Azure SQL Database aaaManage |Microsoft 文件"
description: "深入了解如何 hello Azure 自動化服務可以使用的 toomanage 大規模的 Azure SQL 資料庫。"
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a>使用 Azure 自動化管理 Azure SQL 資料庫
本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理您的 Azure SQL database。

## <a name="what-is-azure-automation"></a>什麼是 Azure 自動化？
[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。 使用 Azure 自動化，長時間執行、 手動、 容易發生錯誤，並經常重複的工作可以自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織。

Azure 自動化提供高度可靠、 高可用性的工作流程執行引擎隨著組織成長而擴充 toomeet 您的需求。 在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。

降低操作費用並釋出 IT / DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Azure 自動化為何有助於管理 Azure SQL 資料庫？
Azure SQL Database 可以管理 Azure 自動化中使用 hello [Azure SQL Database 的 PowerShell cmdlet](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/)位於 hello [Azure PowerShell 工具](/powershell/azure/overview)。 Azure 自動化會有這些可用的 Azure SQL Database 的 PowerShell cmdlet hello 立即可用，讓您可以執行所有的 SQL DB hello 服務中管理工作。 您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。

Azure 自動化也有與 SQL 伺服器 hello 能力 toocommunicate 直接發出 SQL 命令，使用 PowerShell。

hello [Azure 自動化 runbook 資源庫](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/)包含各種不同的產品團隊和社群 runbook tooget 啟動自動化管理的 Azure SQL 資料庫、 其他 Azure 服務和第 3 個合作對象系統。 資源庫 Runbook 包括：

* [針對 SQL Server 資料庫執行 SQL 查詢 (英文)](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [依排程垂直調整 (向上或向下) Azure SQL Database (英文)](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [如果 SQL 資料表的資料庫到達其大小上則截斷該資料表 (英文)](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [如果 Azure SQL Database 高度片段化則索引其中的資料表 (英文)](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>後續步驟
既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure SQL database 的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。

* [Azure 自動化概觀](../automation/automation-intro.md)
* [我的第一個 Runbook](../automation/automation-first-runbook-graphical.md)
* [Azure 自動化的學習地圖](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Azure 自動化： SQL 代理程式在 hello 雲端](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

