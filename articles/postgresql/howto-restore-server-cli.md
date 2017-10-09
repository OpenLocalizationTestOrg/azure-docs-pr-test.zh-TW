---
title: "如何 tooback 及 PostgreSQL 還原 Azure 資料庫中的伺服器 |Microsoft 文件"
description: "了解如何向上 tooback 和還原 Azure 資料庫中的伺服器為 PostgreSQL 使用 hello Azure CLI。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="db609-103">向上 tooback 和還原 Azure 資料庫中的伺服器為 PostgreSQL 使用 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="db609-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="db609-104">使用 PostgreSQL toorestore 伺服器資料庫 tooan 較早的日期，從 7 too35 天跨越 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="db609-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db609-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="db609-105">Prerequisites</span></span>
<span data-ttu-id="db609-106">toocomplete 此如何 tooguide，您需要：</span><span class="sxs-lookup"><span data-stu-id="db609-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="db609-107">[「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="db609-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="db609-108">如果您安裝並在本機使用 Azure CLI hello，此方式 tooguide 會要求您使用 Azure CLI 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="db609-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="db609-109">tooconfirm hello 版本，在 hello Azure CLI 命令提示字元中輸入`az --version`。</span><span class="sxs-lookup"><span data-stu-id="db609-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="db609-110">tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="db609-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="db609-111">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="db609-111">Back up happens automatically</span></span>
<span data-ttu-id="db609-112">當您使用 Azure 資料庫進行 PostgreSQL 時，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="db609-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="db609-113">基本層，hello 備份皆可為 7 天。</span><span class="sxs-lookup"><span data-stu-id="db609-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="db609-114">標準層，hello 備份皆可為 35 天。</span><span class="sxs-lookup"><span data-stu-id="db609-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="db609-115">如需詳細資訊，請參閱 [PostgreSQL 的 Azure 資料庫定價層](concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="db609-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="db609-116">使用這個自動備份功能，您可以還原 hello 伺服器和其資料庫 tooan 早的日期或時間點。</span><span class="sxs-lookup"><span data-stu-id="db609-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="db609-117">還原資料庫 tooa 前一個點的時間，使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="db609-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="db609-118">使用 Azure 資料庫 PostgreSQL toorestore hello 伺服器 tooa 先前時間點。</span><span class="sxs-lookup"><span data-stu-id="db609-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="db609-119">hello 還原資料複製的 tooa 新的伺服器，以及 hello 現有的伺服器保持原狀。</span><span class="sxs-lookup"><span data-stu-id="db609-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="db609-120">例如，如果卸除資料表時不小心正午今天，您可以還原 toohello 正午之前的時間。</span><span class="sxs-lookup"><span data-stu-id="db609-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="db609-121">然後，您可以擷取遺失的資料表與資料，從還原的 hello 份 hello 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="db609-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="db609-122">toorestore hello 伺服器，使用 hello Azure CLI [az postgres 伺服器還原](/cli/azure/postgres/server#restore)命令。</span><span class="sxs-lookup"><span data-stu-id="db609-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="db609-123">執行 hello restore 命令</span><span class="sxs-lookup"><span data-stu-id="db609-123">Run hello restore command</span></span>

<span data-ttu-id="db609-124">toorestore hello 伺服器 hello Azure CLI 命令提示字元，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="db609-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="db609-125">hello`az postgres server restore`命令需要 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="db609-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="db609-126">設定</span><span class="sxs-lookup"><span data-stu-id="db609-126">Setting</span></span> | <span data-ttu-id="db609-127">建議的值</span><span class="sxs-lookup"><span data-stu-id="db609-127">Suggested value</span></span> | <span data-ttu-id="db609-128">說明</span><span class="sxs-lookup"><span data-stu-id="db609-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="db609-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="db609-129">resource-group</span></span> |  <span data-ttu-id="db609-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="db609-130">myResourceGroup</span></span> |  <span data-ttu-id="db609-131">Hello 來源伺服器所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="db609-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="db609-132">名稱</span><span class="sxs-lookup"><span data-stu-id="db609-132">name</span></span> | <span data-ttu-id="db609-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="db609-133">mypgserver-restored</span></span> | <span data-ttu-id="db609-134">hello hello hello restore 命令所建立的新伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="db609-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="db609-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="db609-135">restore-point-in-time</span></span> | <span data-ttu-id="db609-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="db609-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="db609-137">在時間 toorestore 至選取的點。</span><span class="sxs-lookup"><span data-stu-id="db609-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="db609-138">這個日期和時間必須在 hello 來源伺服器的備份保留期限內。</span><span class="sxs-lookup"><span data-stu-id="db609-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="db609-139">使用 hello ISO8601 日期和時間格式。</span><span class="sxs-lookup"><span data-stu-id="db609-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="db609-140">例如，您可以使用自己的當地時區，例如 `2017-04-13T05:59:00-08:00`。</span><span class="sxs-lookup"><span data-stu-id="db609-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="db609-141">您也可以使用 UTC Zulu 格式，例如 hello `2017-04-13T13:59:00Z`。</span><span class="sxs-lookup"><span data-stu-id="db609-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="db609-142">source-server</span><span class="sxs-lookup"><span data-stu-id="db609-142">source-server</span></span> | <span data-ttu-id="db609-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="db609-143">mypgserver-20170401</span></span> | <span data-ttu-id="db609-144">hello 名稱或識別碼 hello 來源伺服器 toorestore 從。</span><span class="sxs-lookup"><span data-stu-id="db609-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="db609-145">當您還原伺服器 tooan 早的時間點，建立新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="db609-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="db609-146">hello 原始伺服器和資料庫 hello 從指定的時間點複製的 toohello 新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="db609-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="db609-147">hello 位置] 和 [定價層的值為 hello 還原伺服器保持 hello 相同為 hello 原始伺服器。</span><span class="sxs-lookup"><span data-stu-id="db609-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="db609-148">hello`az postgres server restore`是同步的命令。</span><span class="sxs-lookup"><span data-stu-id="db609-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="db609-149">還原 hello 伺服器之後，您可以使用它再次 toorepeat hello 程序的不同點的時間。</span><span class="sxs-lookup"><span data-stu-id="db609-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="db609-150">Hello 之後還原程序完成，找出 hello 新伺服器，並確認 hello 資料還原如預期般。</span><span class="sxs-lookup"><span data-stu-id="db609-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db609-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db609-151">Next steps</span></span>
[<span data-ttu-id="db609-152">「適用於 PostgreSQL 的 Azure 資料庫」的連線庫</span><span class="sxs-lookup"><span data-stu-id="db609-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
