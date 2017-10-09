---
title: "aaaServer Azure 資料庫中記錄檔取得 PostgreSQL |Microsoft 文件"
description: "在適用於 PostgreSQL 的 Azure 資料庫中產生查詢和錯誤記錄。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a><span data-ttu-id="b6449-103">適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="b6449-103">Server Logs in Azure Database for PostgreSQL</span></span> 
<span data-ttu-id="b6449-104">適用於 PostgreSQL 的 Azure 資料庫會產生查詢和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b6449-104">Azure Database for PostgreSQL generates query and error logs.</span></span> <span data-ttu-id="b6449-105">不過，不支援存取 tootransaction 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b6449-105">However, access tootransaction logs is not supported.</span></span> <span data-ttu-id="b6449-106">這些記錄檔可以是使用的 tooidentify、 疑難排解與修復組態錯誤和效能次佳。</span><span class="sxs-lookup"><span data-stu-id="b6449-106">These logs can be used tooidentify, troubleshoot, and repair configuration errors and sub-optimal performance.</span></span> <span data-ttu-id="b6449-107">如需詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html)。</span><span class="sxs-lookup"><span data-stu-id="b6449-107">For more information, see [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).</span></span>

## <a name="access-server-logs"></a><span data-ttu-id="b6449-108">存取伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="b6449-108">Access server logs</span></span>
<span data-ttu-id="b6449-109">您可以列出並下載 Azure PostgreSQL server 錯誤記錄檔使用 hello Azure 入口網站， [Azure CLI](howto-configure-server-logs-using-cli.md)和 Azure REST Api。</span><span class="sxs-lookup"><span data-stu-id="b6449-109">You can list and download Azure PostgreSQL server error logs using hello Azure Portal, [Azure CLI](howto-configure-server-logs-using-cli.md) and Azure REST APIs.</span></span>

## <a name="log-retention"></a><span data-ttu-id="b6449-110">記錄保留</span><span class="sxs-lookup"><span data-stu-id="b6449-110">Log retention</span></span>
<span data-ttu-id="b6449-111">您可以設定使用的系統記錄檔的 hello 保留週期**記錄\_保留\_期間**與您的伺服器相關聯的參數。</span><span class="sxs-lookup"><span data-stu-id="b6449-111">You can set hello retention period for system logs using the **log\_retention\_period** parameter associated with your server.</span></span> <span data-ttu-id="b6449-112">這個參數的 hello 單位為的天 （需要 tooconfirm）。</span><span class="sxs-lookup"><span data-stu-id="b6449-112">hello unit for this parameter is days (need tooconfirm).</span></span> <span data-ttu-id="b6449-113">hello 預設值為 3 天。</span><span class="sxs-lookup"><span data-stu-id="b6449-113">hello default value is three days.</span></span> <span data-ttu-id="b6449-114">hello 最大值為 7 天。</span><span class="sxs-lookup"><span data-stu-id="b6449-114">hello maximum value is 7 days.</span></span> <span data-ttu-id="b6449-115">請注意您的伺服器必須具有足夠配置的儲存體 toocontain hello 保留記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b6449-115">Note that your server must have enough allocated storage toocontain hello retained log files.</span></span>
<span data-ttu-id="b6449-116">hello 記錄檔會旋轉每 1 小時] 或 [100 MB 的大小、 何者較早。</span><span class="sxs-lookup"><span data-stu-id="b6449-116">hello log files will rotate every 1 hour or 100MB size, whichever comes first.</span></span>

## <a name="configure-logging-for-azure-postgresql-server"></a><span data-ttu-id="b6449-117">設定 Azure PostgreSQL 伺服器的記錄</span><span class="sxs-lookup"><span data-stu-id="b6449-117">Configure logging for Azure PostgreSQL server</span></span>
<span data-ttu-id="b6449-118">您可以針對伺服器啟用查詢記錄和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="b6449-118">You can enable query logging and error logging for your server.</span></span> <span data-ttu-id="b6449-119">錯誤記錄可包含自動清空、連接和檢查點資訊。</span><span class="sxs-lookup"><span data-stu-id="b6449-119">Error logs can contain auto-vacuum, connection and checkpoints information.</span></span>

<span data-ttu-id="b6449-120">您可以藉由設定兩個伺服器參數來啟用 PostgreSQL DB 執行個體的查詢記錄︰log\_statement 和 log\_min\_duration\_statement。</span><span class="sxs-lookup"><span data-stu-id="b6449-120">You can enable query logging for your PostgreSQL DB instance by setting two server parameters: log\_statement and log\_min\_duration\_statement.</span></span>

<span data-ttu-id="b6449-121">hello**記錄\_陳述式**參數用於控制記錄哪一個 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b6449-121">hello **log\_statement** parameter controls which SQL statements are logged.</span></span> <span data-ttu-id="b6449-122">我們建議您將這個參數設定為太***所有***toolog 所有陳述式; hello 預設值是 none （需要 tooconfirm）。</span><span class="sxs-lookup"><span data-stu-id="b6449-122">We recommend setting this parameter too***all*** toolog all statements; hello default value is none (need tooconfirm).</span></span>

<span data-ttu-id="b6449-123">hello**記錄\_min\_持續時間\_陳述式**參數設定以毫秒為單位的記錄陳述式 toobe hello 限制。</span><span class="sxs-lookup"><span data-stu-id="b6449-123">hello **log\_min\_duration\_statement** parameter sets hello limit in milliseconds of a statement toobe logged.</span></span> <span data-ttu-id="b6449-124">記錄執行時間超過 hello 參數設定的所有 SQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="b6449-124">All SQL statements that run longer than hello parameter setting are logged.</span></span> <span data-ttu-id="b6449-125">這個參數 (需要 tooconfirm) 預設為停用和設定 toominus 1 (-1)。</span><span class="sxs-lookup"><span data-stu-id="b6449-125">This parameter is disabled and set toominus 1 (-1) by default (need tooconfirm).</span></span> <span data-ttu-id="b6449-126">啟用此參數，有助於追蹤應用程式中未最佳化的查詢。</span><span class="sxs-lookup"><span data-stu-id="b6449-126">Enabling this parameter can be helpful in tracking down unoptimized queries in your applications.</span></span>

<span data-ttu-id="b6449-127">hello**記錄\_min\_訊息**可讓您 toocontrol toohello server 記錄檔寫入的訊息層級。</span><span class="sxs-lookup"><span data-stu-id="b6449-127">hello **log\_min\_messages** allows you toocontrol which message levels are written toohello server log.</span></span> <span data-ttu-id="b6449-128">hello 預設為警告。</span><span class="sxs-lookup"><span data-stu-id="b6449-128">hello default is WARNING.</span></span> <span data-ttu-id="b6449-129">（需要 tooconfirm）</span><span class="sxs-lookup"><span data-stu-id="b6449-129">(need tooconfirm)</span></span>

<span data-ttu-id="b6449-130">如需有關這些設定的詳細資訊，請參閱[錯誤報告和記錄 (英文)](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) 文件。</span><span class="sxs-lookup"><span data-stu-id="b6449-130">For more information on these settings, see [Error Reporting and Logging](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html) documentation.</span></span> <span data-ttu-id="b6449-131">若要特別設定適用於 PostgreSQL 的 Azure 資料庫伺服器參數，請參閱[適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄](concepts-server-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="b6449-131">For particularly configuring Azure Database for PostgreSQL server parameters, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6449-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6449-132">Next steps</span></span>
- <span data-ttu-id="b6449-133">tooaccess 記錄使用 Azure CLI 命令列介面，請參閱 <<c0> [ 使用 Azure CLI 設定及存取伺服器記錄檔](howto-configure-server-logs-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b6449-133">tooaccess logs using Azure CLI command line interface, see [Configure and access server logs using Azure CLI](howto-configure-server-logs-using-cli.md)</span></span>
- <span data-ttu-id="b6449-134">如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b6449-134">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md).</span></span>