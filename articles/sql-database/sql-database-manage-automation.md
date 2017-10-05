---
title: "使用 Azure 自動化管理 Azure SQL 資料庫 | Microsoft Docs"
description: "了解如何使用 Azure 自動化服務大規模地管理 Azure SQL 資料庫。"
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
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="c47de-103">使用 Azure 自動化管理 Azure SQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="c47de-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="c47de-104">本指南將為您介紹 Azure 自動化服務，以及如何使用它來簡化您的 Azure SQL 資料庫管理。</span><span class="sxs-lookup"><span data-stu-id="c47de-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="c47de-105">什麼是 Azure 自動化？</span><span class="sxs-lookup"><span data-stu-id="c47de-105">What is Azure Automation?</span></span>
<span data-ttu-id="c47de-106">[Azure 自動化](https://azure.microsoft.com/services/automation/) 是一項 Azure 服務，可經由程序自動化簡化雲端管理。</span><span class="sxs-lookup"><span data-stu-id="c47de-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="c47de-107">透過 Azure 自動化，長時間執行、手動、容易發生錯誤和經常重複的工作都可以自動化，以提高可靠性、效率，並為您的組織縮短創造價值時程。</span><span class="sxs-lookup"><span data-stu-id="c47de-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="c47de-108">Azure 自動化提供非常可靠且高度可用的工作流程執行引擎，可隨著組織的成長根據您的需求進行調整。</span><span class="sxs-lookup"><span data-stu-id="c47de-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="c47de-109">在 Azure 自動化中，程序可透過手動方式、經由協力廠商系統，或依照排程的間隔啟動，讓工作精準地在需要時執行。</span><span class="sxs-lookup"><span data-stu-id="c47de-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="c47de-110">將您的雲端管理工作交由「Azure 自動化」自動執行，以降低營運負擔並釋出 IT/開發維運人力，使其專注於能夠為企業創造價值的工作上。</span><span class="sxs-lookup"><span data-stu-id="c47de-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="c47de-111">Azure 自動化為何有助於管理 Azure SQL 資料庫？</span><span class="sxs-lookup"><span data-stu-id="c47de-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="c47de-112">Azure SQL 資料庫可透過 [Azure PowerShell 工具](/powershell/azure/overview)中提供的 [Azure SQL Database PowerShell Cmdlet](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/)，在 Azure 自動化中受到管理。</span><span class="sxs-lookup"><span data-stu-id="c47de-112">Azure SQL Database can be managed in Azure Automation by using the [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in the [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="c47de-113">Azure 自動化的這些 Azure SQL 資料庫 PowerShell Cmdlet 都是內建的，以便您在服務內執行所有的 SQL 資料庫管理工作。</span><span class="sxs-lookup"><span data-stu-id="c47de-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of the box, so that you can perform all of your SQL DB management tasks within the service.</span></span> <span data-ttu-id="c47de-114">您也可以將 Azure 自動化中的這些 Cmdlet 與其他 Azure 服務的 Cmdlet 搭配，以透過 Azure 服務和協力廠商系統自動執行複雜的工作。</span><span class="sxs-lookup"><span data-stu-id="c47de-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="c47de-115">Azure 自動化也可直接與 SQL 伺服器通訊，只要使用 PowerShell 發出 SQL 命令即可。</span><span class="sxs-lookup"><span data-stu-id="c47de-115">Azure Automation also has the ability to communicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="c47de-116">[Azure 自動化 Runbook 資源庫](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) 含有多種產品團隊和社群 Runbook，可供您開始針對 Azure SQL Database、其他 Azure 服務及協力廠商系統進行自動化管理。</span><span class="sxs-lookup"><span data-stu-id="c47de-116">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="c47de-117">資源庫 Runbook 包括：</span><span class="sxs-lookup"><span data-stu-id="c47de-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="c47de-118">針對 SQL Server 資料庫執行 SQL 查詢 (英文)</span><span class="sxs-lookup"><span data-stu-id="c47de-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="c47de-119">依排程垂直調整 (向上或向下) Azure SQL Database (英文)</span><span class="sxs-lookup"><span data-stu-id="c47de-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="c47de-120">如果 SQL 資料表的資料庫到達其大小上則截斷該資料表 (英文)</span><span class="sxs-lookup"><span data-stu-id="c47de-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="c47de-121">如果 Azure SQL Database 高度片段化則索引其中的資料表 (英文)</span><span class="sxs-lookup"><span data-stu-id="c47de-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="c47de-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c47de-122">Next steps</span></span>
<span data-ttu-id="c47de-123">了解 Azure 自動化的基本概念以及如何用它來管理 Azure SQL 資料庫之後，請參考下列連結，以深入了解 Azure 自動化。</span><span class="sxs-lookup"><span data-stu-id="c47de-123">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure SQL databases, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="c47de-124">Azure 自動化概觀</span><span class="sxs-lookup"><span data-stu-id="c47de-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="c47de-125">我的第一個 Runbook</span><span class="sxs-lookup"><span data-stu-id="c47de-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="c47de-126">Azure 自動化的學習地圖</span><span class="sxs-lookup"><span data-stu-id="c47de-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="c47de-127">Azure Automation: Your SQL Agent in the Cloud (Azure 自動化：雲端中的 SQL 代理程式)</span><span class="sxs-lookup"><span data-stu-id="c47de-127">Azure Automation: Your SQL Agent in the Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

