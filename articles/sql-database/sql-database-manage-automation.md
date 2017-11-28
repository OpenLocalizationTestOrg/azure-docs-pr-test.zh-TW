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
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="b4c2d-103">使用 Azure 自動化管理 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="b4c2d-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="b4c2d-104">本指南將介紹 toohello Azure 自動化服務，而且您可以如何使用的 toosimplify 管理您的 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b4c2d-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="b4c2d-105">What is Azure Automation?</span></span>
<span data-ttu-id="b4c2d-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="b4c2d-107">使用 Azure 自動化，長時間執行、 手動、 容易發生錯誤，並經常重複的工作可以自動化的 tooincrease 可靠性、 效率與時間 toovalue 為您的組織。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b4c2d-108">Azure 自動化提供高度可靠、 高可用性的工作流程執行引擎隨著組織成長而擴充 toomeet 您的需求。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="b4c2d-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b4c2d-110">降低操作費用並釋出 IT / DevOps 人員 toofocus 移動您的雲端管理工作 toobe 商務價值的工作自動執行的 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="b4c2d-111">Azure 自動化為何有助於管理 Azure SQL 資料庫？</span><span class="sxs-lookup"><span data-stu-id="b4c2d-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="b4c2d-112">Azure SQL Database 可以管理 Azure 自動化中使用 hello [Azure SQL Database 的 PowerShell cmdlet](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/)位於 hello [Azure PowerShell 工具](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="b4c2d-113">Azure 自動化會有這些可用的 Azure SQL Database 的 PowerShell cmdlet hello 立即可用，讓您可以執行所有的 SQL DB hello 服務中管理工作。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="b4c2d-114">您也可以跨 Azure 服務和第 3 個合作對象系統配對這些 cmdlet 在 Azure 自動化中利用 hello 適用於其他 Azure 服務、 tooautomate 複雜工作的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b4c2d-115">Azure 自動化也有與 SQL 伺服器 hello 能力 toocommunicate 直接發出 SQL 命令，使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="b4c2d-116">hello [Azure 自動化 runbook 資源庫](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/)包含各種不同的產品團隊和社群 runbook tooget 啟動自動化管理的 Azure SQL 資料庫、 其他 Azure 服務和第 3 個合作對象系統。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="b4c2d-117">資源庫 Runbook 包括：</span><span class="sxs-lookup"><span data-stu-id="b4c2d-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="b4c2d-118">針對 SQL Server 資料庫執行 SQL 查詢 (英文)</span><span class="sxs-lookup"><span data-stu-id="b4c2d-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="b4c2d-119">依排程垂直調整 (向上或向下) Azure SQL Database (英文)</span><span class="sxs-lookup"><span data-stu-id="b4c2d-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="b4c2d-120">如果 SQL 資料表的資料庫到達其大小上則截斷該資料表 (英文)</span><span class="sxs-lookup"><span data-stu-id="b4c2d-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="b4c2d-121">如果 Azure SQL Database 高度片段化則索引其中的資料表 (英文)</span><span class="sxs-lookup"><span data-stu-id="b4c2d-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="b4c2d-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b4c2d-122">Next steps</span></span>
<span data-ttu-id="b4c2d-123">既然您已經學會 hello 的 Azure 自動化，而且可以如何使用的 toomanage Azure SQL database 的基本概念，請遵循這些連結 toolearn 深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="b4c2d-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="b4c2d-124">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="b4c2d-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="b4c2d-125">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="b4c2d-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="b4c2d-126">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="b4c2d-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="b4c2d-127">Azure 自動化： SQL 代理程式在 hello 雲端</span><span class="sxs-lookup"><span data-stu-id="b4c2d-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

