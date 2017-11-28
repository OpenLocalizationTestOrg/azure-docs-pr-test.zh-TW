---
title: "如何在適用於 PostgreSQL 的 Azure 資料庫中還原伺服器 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站，在適用於 PostgreSQL 的 Azure 資料庫中還原伺服器。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="30f9d-103">如何使用 Azure 入口網站，在適用於 PostgreSQL 的 Azure 資料庫中備份和還原伺服器</span><span class="sxs-lookup"><span data-stu-id="30f9d-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="30f9d-104">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="30f9d-104">Backup happens Automatically</span></span>
<span data-ttu-id="30f9d-105">使用適用於 PostgreSQL 的 Azure 資料庫時，資料庫服務每隔 5 分鐘會自動備份一次服務。</span><span class="sxs-lookup"><span data-stu-id="30f9d-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="30f9d-106">使用基本層時，備份會保留 7 天，而使用標準層時會保留 35 天。</span><span class="sxs-lookup"><span data-stu-id="30f9d-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="30f9d-107">如需詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫服務層](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="30f9d-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="30f9d-108">透過這個自動備份功能，您可以將伺服器和其所有資料庫還原至新的伺服器，而且還原至更早的時間點。</span><span class="sxs-lookup"><span data-stu-id="30f9d-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="30f9d-109">在 Azure 入口網站中還原</span><span class="sxs-lookup"><span data-stu-id="30f9d-109">Restore in the Azure portal</span></span>
<span data-ttu-id="30f9d-110">適用於 PostgreSQL 的 Azure 資料庫可讓您將伺服器還原至過去的時間點，並還原至新的伺服器複本。</span><span class="sxs-lookup"><span data-stu-id="30f9d-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="30f9d-111">您可以使用這個新的伺服器復原資料。</span><span class="sxs-lookup"><span data-stu-id="30f9d-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="30f9d-112">比方說，如果今天中午不小心卸除資料表，您可以還原至中午之前的時刻，然後從該新的伺服器複本擷取遺漏的資料表和資料。</span><span class="sxs-lookup"><span data-stu-id="30f9d-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="30f9d-113">下列步驟會將範例伺服器還原至某個時間點︰</span><span class="sxs-lookup"><span data-stu-id="30f9d-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="30f9d-114">登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="30f9d-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="30f9d-115">找出您的「適用於 PostgreSQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="30f9d-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="30f9d-116">在 Azure 入口網站中，從左側功能表按一下 [所有資源]，然後輸入名稱搜尋現有的伺服器，例如 **mypgserver-20170401**。</span><span class="sxs-lookup"><span data-stu-id="30f9d-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="30f9d-117">按一下搜尋結果中列出的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="30f9d-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="30f9d-118">伺服器的 [概觀] 頁面隨即開啟，並提供可進一步設定的選項。</span><span class="sxs-lookup"><span data-stu-id="30f9d-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure 入口網站 - 搜尋找出您的伺服器](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="30f9d-120">在伺服器概觀刀鋒視窗頂端，按一下工具列上的 [還原]。</span><span class="sxs-lookup"><span data-stu-id="30f9d-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="30f9d-121">[還原] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="30f9d-121">The Restore blade opens.</span></span>

   ![適用於 PostgreSQL 的 Azure 資料庫 - 概觀 - 還原按鈕](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="30f9d-123">在 [還原] 表單中填入必要資訊︰</span><span class="sxs-lookup"><span data-stu-id="30f9d-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="30f9d-124">適用於 PostgreSQL 的 Azure 資料庫 - 還原資訊</span><span class="sxs-lookup"><span data-stu-id="30f9d-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="30f9d-125">**還原點**：選取在變更伺服器之前的時間點</span><span class="sxs-lookup"><span data-stu-id="30f9d-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="30f9d-126">**目標伺服器**︰提供要作為還原目的地的新伺服器名稱</span><span class="sxs-lookup"><span data-stu-id="30f9d-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="30f9d-127">**位置**︰您無法選取區域，預設是與來源伺服器相同的區域</span><span class="sxs-lookup"><span data-stu-id="30f9d-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="30f9d-128">**定價層**︰還原伺服器時，您無法變更此值。</span><span class="sxs-lookup"><span data-stu-id="30f9d-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="30f9d-129">它與來源伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="30f9d-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="30f9d-130">按一下 [確定] 將伺服器還原至某個時間點。</span><span class="sxs-lookup"><span data-stu-id="30f9d-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="30f9d-131">完成還原時，找出已建立的新伺服器，確認資料如預期般還原。</span><span class="sxs-lookup"><span data-stu-id="30f9d-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30f9d-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="30f9d-132">Next steps</span></span>
- [<span data-ttu-id="30f9d-133">「適用於 PostgreSQL 的 Azure 資料庫」的連線庫</span><span class="sxs-lookup"><span data-stu-id="30f9d-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
