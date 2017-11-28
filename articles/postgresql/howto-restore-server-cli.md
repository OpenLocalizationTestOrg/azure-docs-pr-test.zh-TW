---
title: "如何在 PostgreSQL 的 Azure 資料庫中備份與還原伺服器 | Microsoft Docs"
description: "了解如何使用 Azure CLI，在適用於 PostgreSQL 的 Azure 資料庫中備份和還原伺服器。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 871887e67d686a965a0648d2c6f0c72b3008db05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-the-azure-cli"></a><span data-ttu-id="bb108-103">如何使用 Azure CLI，在適用於 PostgreSQL 的 Azure 資料庫中備份和還原伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb108-103">How to back up and restore a server in Azure Database for PostgreSQL by using the Azure CLI</span></span>

<span data-ttu-id="bb108-104">使用 PostgreSQL 的 Azure 資料庫將伺服器資料庫還原到 7 至 35 天前的日期。</span><span class="sxs-lookup"><span data-stu-id="bb108-104">Use Azure Database for PostgreSQL to restore a server database to an earlier date that spans from 7 to 35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb108-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="bb108-105">Prerequisites</span></span>
<span data-ttu-id="bb108-106">若要完成本操作說明指南，您需要：</span><span class="sxs-lookup"><span data-stu-id="bb108-106">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="bb108-107">[「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bb108-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="bb108-108">如果您在本機安裝和使用 Azure CLI，本操作說明指南會要求您使用 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bb108-108">If you install and use the Azure CLI locally, this how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bb108-109">若要確認版本，請在 Azure CLI 命令提示字元中輸入 `az --version`。</span><span class="sxs-lookup"><span data-stu-id="bb108-109">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="bb108-110">若要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="bb108-110">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="bb108-111">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="bb108-111">Back up happens automatically</span></span>
<span data-ttu-id="bb108-112">當您使用 PostgreSQL 的 Azure 資料庫時，資料庫服務每隔 5 分鐘會自動備份一次服務。</span><span class="sxs-lookup"><span data-stu-id="bb108-112">When you use Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="bb108-113">基本層的備份保留 7 天。</span><span class="sxs-lookup"><span data-stu-id="bb108-113">For Basic Tier, the backups are available for 7 days.</span></span> <span data-ttu-id="bb108-114">標準層的備份保留 35 天。</span><span class="sxs-lookup"><span data-stu-id="bb108-114">For Standard Tier, the backups are available for 35 days.</span></span> <span data-ttu-id="bb108-115">如需詳細資訊，請參閱 [PostgreSQL 的 Azure 資料庫定價層](concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="bb108-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="bb108-116">透過這個自動備份功能，您可以將伺服器和其資料庫還原至某個較早的日期或時間點。</span><span class="sxs-lookup"><span data-stu-id="bb108-116">With this automatic backup feature, you can restore the server and its databases to an earlier date, or point in time.</span></span>

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a><span data-ttu-id="bb108-117">使用 Azure CLI 將資料庫還原到過去的時間點</span><span class="sxs-lookup"><span data-stu-id="bb108-117">Restore a database to a previous point in time by using the Azure CLI</span></span>
<span data-ttu-id="bb108-118">使用 PostgreSQL 的 Azure 資料庫將伺服器還原至過去的時間點。</span><span class="sxs-lookup"><span data-stu-id="bb108-118">Use Azure Database for PostgreSQL to restore the server to a previous point in time.</span></span> <span data-ttu-id="bb108-119">還原的資料會複製到新的伺服器，而現有的伺服器則保持原狀。</span><span class="sxs-lookup"><span data-stu-id="bb108-119">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="bb108-120">例如，如果資料表在今天中午意外卸除，您可以還原到中午之前的時間。</span><span class="sxs-lookup"><span data-stu-id="bb108-120">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="bb108-121">然後，您可從伺服器的還原複本擷取遺失的資料表和資料。</span><span class="sxs-lookup"><span data-stu-id="bb108-121">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="bb108-122">若要還原伺服器，請使用 Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) 命令。</span><span class="sxs-lookup"><span data-stu-id="bb108-122">To restore the server, use the Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="bb108-123">執行 restore 命令</span><span class="sxs-lookup"><span data-stu-id="bb108-123">Run the restore command</span></span>

<span data-ttu-id="bb108-124">若要還原伺服器，請在 Azure CLI 命令提示字元中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="bb108-124">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="bb108-125">`az postgres server restore` 命令需要下列參數：</span><span class="sxs-lookup"><span data-stu-id="bb108-125">The `az postgres server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="bb108-126">設定</span><span class="sxs-lookup"><span data-stu-id="bb108-126">Setting</span></span> | <span data-ttu-id="bb108-127">建議的值</span><span class="sxs-lookup"><span data-stu-id="bb108-127">Suggested value</span></span> | <span data-ttu-id="bb108-128">說明</span><span class="sxs-lookup"><span data-stu-id="bb108-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="bb108-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="bb108-129">resource-group</span></span> |  <span data-ttu-id="bb108-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bb108-130">myResourceGroup</span></span> |  <span data-ttu-id="bb108-131">來源伺服器所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bb108-131">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="bb108-132">名稱</span><span class="sxs-lookup"><span data-stu-id="bb108-132">name</span></span> | <span data-ttu-id="bb108-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="bb108-133">mypgserver-restored</span></span> | <span data-ttu-id="bb108-134">還原命令所建立之新伺服器的名稱。</span><span class="sxs-lookup"><span data-stu-id="bb108-134">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="bb108-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="bb108-135">restore-point-in-time</span></span> | <span data-ttu-id="bb108-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="bb108-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="bb108-137">選取要還原的時間點。</span><span class="sxs-lookup"><span data-stu-id="bb108-137">Select a point in time to restore to.</span></span> <span data-ttu-id="bb108-138">這個日期和時間必須在來源伺服器的備份保留期限內。</span><span class="sxs-lookup"><span data-stu-id="bb108-138">This date and time must be within the source server's back up retention period.</span></span> <span data-ttu-id="bb108-139">請使用 ISO8601 日期和時間格式。</span><span class="sxs-lookup"><span data-stu-id="bb108-139">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="bb108-140">例如，您可以使用自己的當地時區，例如 `2017-04-13T05:59:00-08:00`。</span><span class="sxs-lookup"><span data-stu-id="bb108-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="bb108-141">您也可以使用 UTC Zulu 格式，例如 `2017-04-13T13:59:00Z`。</span><span class="sxs-lookup"><span data-stu-id="bb108-141">You can also use the UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="bb108-142">source-server</span><span class="sxs-lookup"><span data-stu-id="bb108-142">source-server</span></span> | <span data-ttu-id="bb108-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="bb108-143">mypgserver-20170401</span></span> | <span data-ttu-id="bb108-144">要進行還原的來源伺服器之名稱或識別碼。</span><span class="sxs-lookup"><span data-stu-id="bb108-144">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="bb108-145">當您將伺服器還原到之前的時間點時，會建立新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb108-145">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="bb108-146">指定時間點的原始伺服器及其資料庫會複製到新的伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb108-146">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="bb108-147">已還原伺服器的位置與定價層值與原始伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="bb108-147">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="bb108-148">`az postgres server restore` 命令是同步的。</span><span class="sxs-lookup"><span data-stu-id="bb108-148">The `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="bb108-149">還原伺服器之後，您可以再次使用它以不同的時間點重複此程序。</span><span class="sxs-lookup"><span data-stu-id="bb108-149">After the server is restored, you can use it again to repeat the process for a different point in time.</span></span> 

<span data-ttu-id="bb108-150">完成還原程序後，找出新的伺服器，確認資料如預期般還原。</span><span class="sxs-lookup"><span data-stu-id="bb108-150">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb108-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb108-151">Next steps</span></span>
[<span data-ttu-id="bb108-152">「適用於 PostgreSQL 的 Azure 資料庫」的連線庫</span><span class="sxs-lookup"><span data-stu-id="bb108-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
