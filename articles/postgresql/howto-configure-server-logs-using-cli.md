---
title: "使用 Azure CLI 設定和存取 PostgreSQL 的伺服器記錄 | Microsoft Docs"
description: "本文描述如何使用 Azure CLI 命令列，在適用於 PostgreSQL 的 Azure 資料庫中設定和存取伺服器記錄。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="f785a-103">使用 Azure CLI 設定和存取伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="f785a-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="f785a-104">您可以使用命令列介面 (Azure CLI) 來下載 PostgreSQL 伺服器錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="f785a-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="f785a-105">不過，不支援存取交易記錄。</span><span class="sxs-lookup"><span data-stu-id="f785a-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f785a-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="f785a-106">Prerequisites</span></span>
<span data-ttu-id="f785a-107">若要逐步執行本作法指南，您需要︰</span><span class="sxs-lookup"><span data-stu-id="f785a-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="f785a-108">[適用於 PostgreSQL 的 Azure 資料庫伺服器](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f785a-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="f785a-109">安裝 [Azure CLI 2.0](/cli/azure/install-azure-cli) 命令列公用程式，或在瀏覽器中使用 Azure Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="f785a-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="f785a-110">設定「適用於 PostgreSQL 的 Azure 資料庫」的記錄</span><span class="sxs-lookup"><span data-stu-id="f785a-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="f785a-111">您可以設定伺服器來存取查詢記錄和錯誤記錄。</span><span class="sxs-lookup"><span data-stu-id="f785a-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="f785a-112">錯誤記錄可包含自動清空、連線和檢查點資訊。</span><span class="sxs-lookup"><span data-stu-id="f785a-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="f785a-113">開啟記錄功能</span><span class="sxs-lookup"><span data-stu-id="f785a-113">Turn on logging</span></span>
2. <span data-ttu-id="f785a-114">更新 log\_statement 和 log\_min\_duration\_statement 來啟用查詢記錄</span><span class="sxs-lookup"><span data-stu-id="f785a-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="f785a-115">更新保留期限</span><span class="sxs-lookup"><span data-stu-id="f785a-115">Update retention period</span></span>

<span data-ttu-id="f785a-116">如需詳細資訊，請參閱[自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="f785a-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="f785a-117">列出適用於 PostgreSQL 伺服器的 Azure 資料庫之記錄</span><span class="sxs-lookup"><span data-stu-id="f785a-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="f785a-118">若要列出伺服器的可用記錄檔，請執行 [az postgres server-logs list](/cli/azure/postgres/server-logs#list) 命令。</span><span class="sxs-lookup"><span data-stu-id="f785a-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="f785a-119">您可以針對資源群組 **myresourcegroup** 下的伺服器 **mypgserver-20170401.postgres.database.azure.com**，列出伺服器的記錄檔，並輸出至名為 **log\_files\_list.txt** 的文字檔。</span><span class="sxs-lookup"><span data-stu-id="f785a-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="f785a-120">從伺服器將記錄下載至本機</span><span class="sxs-lookup"><span data-stu-id="f785a-120">Download logs locally from the server</span></span>
<span data-ttu-id="f785a-121">[az postgres server-logs download](/cli/azure/postgres/server-logs#download) 命令讓您可下載您伺服器適用的個別記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f785a-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="f785a-122">此範例會針對資源群組 **myresourcegroup** 下的伺服器 **mypgserver-20170401.postgres.database.azure.com**，將特定的記錄檔下載至您的本機環境。</span><span class="sxs-lookup"><span data-stu-id="f785a-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="f785a-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f785a-123">Next steps</span></span>
- <span data-ttu-id="f785a-124">若要深入了解伺服器記錄，請參閱[適用於 PostgreSQL 的 Azure 資料庫中的伺服器記錄](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="f785a-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="f785a-125">如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f785a-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
