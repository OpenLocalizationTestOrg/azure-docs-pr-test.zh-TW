---
title: "適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄 | Microsoft Docs"
description: "在適用於 PostgreSQL 的 Azure 資料庫中產生查詢和錯誤記錄。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 10f6c490a4fdb4c70cb80b035eaebb9d2ad2e699
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a><span data-ttu-id="c9323-103">適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="c9323-103">Server Logs in Azure Database for PostgreSQL</span></span> 
<span data-ttu-id="c9323-104">適用於 PostgreSQL 的 Azure 資料庫會產生查詢和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="c9323-104">Azure Database for PostgreSQL generates query and error logs.</span></span> <span data-ttu-id="c9323-105">不過，不支援存取交易記錄。</span><span class="sxs-lookup"><span data-stu-id="c9323-105">However, access to transaction logs is not supported.</span></span> <span data-ttu-id="c9323-106">這些記錄可用來識別、疑難排解和修復設定錯誤和次佳效能。</span><span class="sxs-lookup"><span data-stu-id="c9323-106">These logs can be used to identify, troubleshoot, and repair configuration errors and sub-optimal performance.</span></span> <span data-ttu-id="c9323-107">如需詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html)。</span><span class="sxs-lookup"><span data-stu-id="c9323-107">For more information, see [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).</span></span>

## <a name="access-server-logs"></a><span data-ttu-id="c9323-108">存取伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="c9323-108">Access server logs</span></span>
<span data-ttu-id="c9323-109">您可以使用 Azure 入口網站、[Azure CLI](howto-configure-server-logs-using-cli.md) 和 Azure REST API，來列出和下載 Azure PostgreSQL 伺服器錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="c9323-109">You can list and download Azure PostgreSQL server error logs using the Azure Portal, [Azure CLI](howto-configure-server-logs-using-cli.md) and Azure REST APIs.</span></span>

## <a name="log-retention"></a><span data-ttu-id="c9323-110">記錄保留</span><span class="sxs-lookup"><span data-stu-id="c9323-110">Log retention</span></span>
<span data-ttu-id="c9323-111">您可以使用與您伺服器相關聯的 **log\_retention\_period** 參數，來設定系統記錄的保留期。</span><span class="sxs-lookup"><span data-stu-id="c9323-111">You can set the retention period for system logs using the **log\_retention\_period** parameter associated with your server.</span></span> <span data-ttu-id="c9323-112">此參數的單位為天 (需要確認)。</span><span class="sxs-lookup"><span data-stu-id="c9323-112">The unit for this parameter is days (need to confirm).</span></span> <span data-ttu-id="c9323-113">預設值為三天。</span><span class="sxs-lookup"><span data-stu-id="c9323-113">The default value is three days.</span></span> <span data-ttu-id="c9323-114">最大值為 7 天。</span><span class="sxs-lookup"><span data-stu-id="c9323-114">The maximum value is 7 days.</span></span> <span data-ttu-id="c9323-115">請注意，您的伺服器必須配置足夠的儲存體，才能包含保留的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c9323-115">Note that your server must have enough allocated storage to contain the retained log files.</span></span>
<span data-ttu-id="c9323-116">記錄檔每 1 小時或每 100 MB 的大小就會輪換 (端視何者先達到)。</span><span class="sxs-lookup"><span data-stu-id="c9323-116">The log files will rotate every 1 hour or 100MB size, whichever comes first.</span></span>

## <a name="configure-logging-for-azure-postgresql-server"></a><span data-ttu-id="c9323-117">設定 Azure PostgreSQL 伺服器的記錄</span><span class="sxs-lookup"><span data-stu-id="c9323-117">Configure logging for Azure PostgreSQL server</span></span>
<span data-ttu-id="c9323-118">您可以針對伺服器啟用查詢記錄和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="c9323-118">You can enable query logging and error logging for your server.</span></span> <span data-ttu-id="c9323-119">錯誤記錄可包含自動清空、連接和檢查點資訊。</span><span class="sxs-lookup"><span data-stu-id="c9323-119">Error logs can contain auto-vacuum, connection and checkpoints information.</span></span>

<span data-ttu-id="c9323-120">您可以藉由設定兩個伺服器參數來啟用 PostgreSQL DB 執行個體的查詢記錄︰log\_statement 和 log\_min\_duration\_statement。</span><span class="sxs-lookup"><span data-stu-id="c9323-120">You can enable query logging for your PostgreSQL DB instance by setting two server parameters: log\_statement and log\_min\_duration\_statement.</span></span>

<span data-ttu-id="c9323-121">**log\_statement** 參數控制要記錄哪些 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c9323-121">The **log\_statement** parameter controls which SQL statements are logged.</span></span> <span data-ttu-id="c9323-122">我們建議將此參數設為 ***all*** 以記錄所有陳述式；預設值為 none (需要確認)。</span><span class="sxs-lookup"><span data-stu-id="c9323-122">We recommend setting this parameter to ***all*** to log all statements; the default value is none (need to confirm).</span></span>

<span data-ttu-id="c9323-123">**log\_min\_duration\_statement** 參數會以毫秒為單位，設定要記錄之陳述式的限制。</span><span class="sxs-lookup"><span data-stu-id="c9323-123">The **log\_min\_duration\_statement** parameter sets the limit in milliseconds of a statement to be logged.</span></span> <span data-ttu-id="c9323-124">系統會記錄所有執行時間比此參數設定還長的 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="c9323-124">All SQL statements that run longer than the parameter setting are logged.</span></span> <span data-ttu-id="c9323-125">預設 (需要確認) 會停用此參數並設為負 1 (-1)。</span><span class="sxs-lookup"><span data-stu-id="c9323-125">This parameter is disabled and set to minus 1 (-1) by default (need to confirm).</span></span> <span data-ttu-id="c9323-126">啟用此參數，有助於追蹤應用程式中未最佳化的查詢。</span><span class="sxs-lookup"><span data-stu-id="c9323-126">Enabling this parameter can be helpful in tracking down unoptimized queries in your applications.</span></span>

<span data-ttu-id="c9323-127">**log\_min\_messages** 讓您能夠控制要將哪些訊息層級寫入伺服器記錄。</span><span class="sxs-lookup"><span data-stu-id="c9323-127">The **log\_min\_messages** allows you to control which message levels are written to the server log.</span></span> <span data-ttu-id="c9323-128">預設值為 WARNING。</span><span class="sxs-lookup"><span data-stu-id="c9323-128">The default is WARNING.</span></span> <span data-ttu-id="c9323-129">(需要確認)</span><span class="sxs-lookup"><span data-stu-id="c9323-129">(need to confirm)</span></span>

<span data-ttu-id="c9323-130">如需有關這些設定的詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) 文件。</span><span class="sxs-lookup"><span data-stu-id="c9323-130">For more information on these settings, see [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) documentation.</span></span> <span data-ttu-id="c9323-131">若要特別設定適用於 PostgreSQL 的 Azure 資料庫伺服器參數，請參閱[適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄](concepts-server-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="c9323-131">For particularly configuring Azure Database for PostgreSQL server parameters, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9323-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9323-132">Next steps</span></span>
- <span data-ttu-id="c9323-133">若要使用 Azure CLI 命令列介面存取記錄，請參閱[使用 Azure CLI 設定和存取伺服器記錄](howto-configure-server-logs-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c9323-133">To access logs using Azure CLI command line interface, see [Configure and access server logs using Azure CLI](howto-configure-server-logs-using-cli.md)</span></span>
- <span data-ttu-id="c9323-134">如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c9323-134">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md).</span></span>