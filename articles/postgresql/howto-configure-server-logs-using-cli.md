---
title: "使用 Azure CLI PostgreSQL 的 aaaConfigure 及存取伺服器記錄檔 |Microsoft 文件"
description: "本文說明如何 tooconfigure 及存取 hello 伺服器記錄檔中 Azure Database PostgreSQL 使用 Azure CLI 命令列。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="2d59f-103">使用 Azure CLI 設定和存取伺服器記錄</span><span class="sxs-lookup"><span data-stu-id="2d59f-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="2d59f-104">您可以下載 hello PostgreSQL server 錯誤記錄檔使用 hello 命令列介面 (Azure CLI)。</span><span class="sxs-lookup"><span data-stu-id="2d59f-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="2d59f-105">不過，不支援存取 tootransaction 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d59f-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d59f-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="2d59f-106">Prerequisites</span></span>
<span data-ttu-id="2d59f-107">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="2d59f-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="2d59f-108">[適用於 PostgreSQL 的 Azure 資料庫伺服器](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2d59f-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="2d59f-109">安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="2d59f-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="2d59f-110">設定「適用於 PostgreSQL 的 Azure 資料庫」的記錄</span><span class="sxs-lookup"><span data-stu-id="2d59f-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="2d59f-111">您可以設定 hello 伺服器 tooaccess 查詢記錄檔和錯誤記錄檔。</span><span class="sxs-lookup"><span data-stu-id="2d59f-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="2d59f-112">錯誤記錄可包含自動清空、連線和檢查點資訊。</span><span class="sxs-lookup"><span data-stu-id="2d59f-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="2d59f-113">開啟記錄功能</span><span class="sxs-lookup"><span data-stu-id="2d59f-113">Turn on logging</span></span>
2. <span data-ttu-id="2d59f-114">更新記錄\_陳述式和記錄\_min\_持續時間\_陳述式 tooenable 查詢記錄</span><span class="sxs-lookup"><span data-stu-id="2d59f-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="2d59f-115">更新保留期限</span><span class="sxs-lookup"><span data-stu-id="2d59f-115">Update retention period</span></span>

<span data-ttu-id="2d59f-116">如需詳細資訊，請參閱[自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="2d59f-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="2d59f-117">列出適用於 PostgreSQL 伺服器的 Azure 資料庫之記錄</span><span class="sxs-lookup"><span data-stu-id="2d59f-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="2d59f-118">toolist hello 可用的記錄檔以取得您的伺服器上執行 hello [az postgres 伺服器記錄檔清單](/cli/azure/postgres/server-logs#list)命令。</span><span class="sxs-lookup"><span data-stu-id="2d59f-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="2d59f-119">您可以列出 hello 記錄檔以取得伺服器**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup**，指示它 tooa 文字和名為檔案**記錄\_檔案\_list.txt。**</span><span class="sxs-lookup"><span data-stu-id="2d59f-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="2d59f-120">從 hello 伺服器在本機下載記錄檔</span><span class="sxs-lookup"><span data-stu-id="2d59f-120">Download logs locally from hello server</span></span>
<span data-ttu-id="2d59f-121">hello [az postgres 伺服器記錄檔下載](/cli/azure/postgres/server-logs#download)命令可讓您 toodownload 個別記錄檔，為您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2d59f-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="2d59f-122">此範例中下載 hello hello 伺服器的特定記錄檔**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup** tooyour 本機環境。</span><span class="sxs-lookup"><span data-stu-id="2d59f-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="2d59f-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2d59f-123">Next steps</span></span>
- <span data-ttu-id="2d59f-124">toolearn 進一步了解伺服器記錄檔，請參閱[Azure PostgreSQL 資料庫中的伺服器記錄檔](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="2d59f-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="2d59f-125">如需伺服器參數的詳細資訊，請參閱[使用 Azure CLI 自訂伺服器設定參數](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="2d59f-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
