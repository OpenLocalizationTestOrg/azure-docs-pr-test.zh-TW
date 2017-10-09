---
title: "Azure PostgreSQL 資料庫中的 aaaConfigure hello 服務參數 |Microsoft 文件"
description: "本文說明如何 tooconfigure hello 服務在 Azure 資料庫使用於參數 PostgreSQL hello Azure CLI 命令列。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="246b5-103">使用 Azure CLI 自訂伺服器設定參數</span><span class="sxs-lookup"><span data-stu-id="246b5-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="246b5-104">您可以列出、 顯示及更新適用於使用命令列介面 (Azure CLI) hello Azure PostgreSQL 伺服器組態參數。</span><span class="sxs-lookup"><span data-stu-id="246b5-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="246b5-105">不過，只有一部分引擎設定會在伺服器層級公開而可供修改。</span><span class="sxs-lookup"><span data-stu-id="246b5-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="246b5-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="246b5-106">Prerequisites</span></span>
<span data-ttu-id="246b5-107">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="246b5-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="246b5-108">伺服器和資料庫 [建立適用於 PostgreSQL 的 Azure 資料庫](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="246b5-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="246b5-109">安裝[Azure CLI 2.0](/cli/azure/install-azure-cli)命令列公用程式或使用 hello Azure 雲端殼層 hello 瀏覽器中的。</span><span class="sxs-lookup"><span data-stu-id="246b5-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="246b5-110">列出適用於 PostgreSQL 伺服器之 Azure 資料庫的伺服器組態參數</span><span class="sxs-lookup"><span data-stu-id="246b5-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="246b5-111">toolist 中一部伺服器和其值，所有可修改的參數執行 hello [az postgres 伺服器組態清單](/cli/azure/postgres/server/configuration#list)命令。</span><span class="sxs-lookup"><span data-stu-id="246b5-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="246b5-112">您可以列出 hello 伺服器 hello 伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup**。</span><span class="sxs-lookup"><span data-stu-id="246b5-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="246b5-113">顯示伺服器設定參數的詳細資料</span><span class="sxs-lookup"><span data-stu-id="246b5-113">Show server configuration parameter details</span></span>
<span data-ttu-id="246b5-114">tooshow hello，執行的伺服器的特定組態參數的詳細資料[az postgres 伺服器組態顯示](/cli/azure/postgres/server/configuration#show)命令。</span><span class="sxs-lookup"><span data-stu-id="246b5-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="246b5-115">這個範例會顯示詳細資料的 hello**記錄\_min\_訊息**伺服器的伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**下資源群組**myresourcegroup。**</span><span class="sxs-lookup"><span data-stu-id="246b5-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="246b5-116">修改伺服器設定參數值</span><span class="sxs-lookup"><span data-stu-id="246b5-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="246b5-117">您也可以修改某些伺服器組態參數 hello 值，這會更新 hello PostgreSQL 伺服器引擎的 hello 基礎組態值。</span><span class="sxs-lookup"><span data-stu-id="246b5-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="246b5-118">tooupdate hello 組態使用 hello [az postgres 伺服器組態集](/cli/azure/postgres/server/configuration#set)命令。</span><span class="sxs-lookup"><span data-stu-id="246b5-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="246b5-119">tooupdate hello**記錄\_min\_訊息**伺服器的伺服器組態參數**mypgserver 20170401.postgres.database.azure.com**資源群組下**myresourcegroup。**</span><span class="sxs-lookup"><span data-stu-id="246b5-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="246b5-120">如果您想 tooreset hello 參數值的組態，您只需選擇出 hello 選擇性 tooleave`--value`參數和 hello 服務將會套用 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="246b5-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="246b5-121">在上述範例中，看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="246b5-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="246b5-122">這將會重設 hello**記錄\_min\_訊息**組態 toohello 預設值**警告**。</span><span class="sxs-lookup"><span data-stu-id="246b5-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="246b5-123">如需伺服器設定和允許值的進一步詳細資訊，請參閱有關[伺服器設定](https://www.postgresql.org/docs/9.6/static/runtime-config.html)的 PostgreSQL 文件。</span><span class="sxs-lookup"><span data-stu-id="246b5-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="246b5-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="246b5-124">Next steps</span></span>
- <span data-ttu-id="246b5-125">tooconfigure 及存取伺服器記錄檔，請參閱[Azure PostgreSQL 資料庫中的伺服器記錄檔](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="246b5-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
