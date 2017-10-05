---
title: "如何在適用於 MySQL 的 Azure 資料庫中還原伺服器 | Microsoft Docs"
description: "本文說明如何使用 Azure 入口網站，在適用於 MySQL 的 Azure 資料庫中還原伺服器。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="925ed-103">如何使用 Azure 入口網站，在適用於 MySQL 的 Azure 資料庫中備份和還原伺服器</span><span class="sxs-lookup"><span data-stu-id="925ed-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="925ed-104">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="925ed-104">Backup happens Automatically</span></span>
<span data-ttu-id="925ed-105">使用適用於 MySQL 的 Azure 資料庫時，資料庫服務每隔 5 分鐘會自動備份一次服務。</span><span class="sxs-lookup"><span data-stu-id="925ed-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="925ed-106">使用基本層時，備份會保留 7 天，而使用標準層時會保留 35 天。</span><span class="sxs-lookup"><span data-stu-id="925ed-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="925ed-107">如需詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫服務層](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="925ed-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="925ed-108">透過這個自動備份功能，您可以將伺服器和其所有資料庫還原至新的伺服器，而且還原至更早的時間點。</span><span class="sxs-lookup"><span data-stu-id="925ed-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="925ed-109">在 Azure 入口網站中還原</span><span class="sxs-lookup"><span data-stu-id="925ed-109">Restore in the Azure portal</span></span>
<span data-ttu-id="925ed-110">適用於 MySQL 的 Azure 資料庫可讓您將伺服器還原至過去的時間點，並還原至新的伺服器複本。</span><span class="sxs-lookup"><span data-stu-id="925ed-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="925ed-111">您可以使用這個新的伺服器復原資料。</span><span class="sxs-lookup"><span data-stu-id="925ed-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="925ed-112">比方說，如果今天中午不小心卸除資料表，您可以還原至中午之前的時刻，然後從該新的伺服器複本擷取遺漏的資料表和資料。</span><span class="sxs-lookup"><span data-stu-id="925ed-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="925ed-113">下列步驟會將範例伺服器還原至某個時間點︰</span><span class="sxs-lookup"><span data-stu-id="925ed-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="925ed-114">登入 [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="925ed-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="925ed-115">找出適用於 MySQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="925ed-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="925ed-116">在左窗格中，選取 [所有資源]，然後從清單中選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="925ed-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="925ed-117">在伺服器概觀刀鋒視窗頂端，按一下工具列上的 [還原]。</span><span class="sxs-lookup"><span data-stu-id="925ed-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="925ed-118">[還原] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="925ed-118">The Restore blade opens.</span></span>
<span data-ttu-id="925ed-119">![按一下 [還原] 按鈕](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="925ed-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="925ed-120">在 [還原] 表單中填入必要資訊︰</span><span class="sxs-lookup"><span data-stu-id="925ed-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="925ed-121">**還原點 (UTC)**︰使用日期選擇器和時間選擇器，選取要還原的時間點。</span><span class="sxs-lookup"><span data-stu-id="925ed-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="925ed-122">指定的時間是 UTC 格式，因此您可能需要將本地時間轉換成 UTC。</span><span class="sxs-lookup"><span data-stu-id="925ed-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="925ed-123">**還原至新伺服器**︰提供新的伺服器名稱作為還原現有伺服器的目的地。</span><span class="sxs-lookup"><span data-stu-id="925ed-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="925ed-124">**位置**︰區域選擇會自動填入來源伺服器區域，無法變更。</span><span class="sxs-lookup"><span data-stu-id="925ed-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="925ed-125">**定價層**︰定價層選擇會自動填入與來源伺服器相同的定價層，在這裡無法變更。</span><span class="sxs-lookup"><span data-stu-id="925ed-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="925ed-126">![PITR 還原](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="925ed-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="925ed-127">按一下 [確定] 將伺服器還原至某個時間點。</span><span class="sxs-lookup"><span data-stu-id="925ed-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="925ed-128">還原完成之後，找出已建立的新伺服器，確認資料庫如預期般還原。</span><span class="sxs-lookup"><span data-stu-id="925ed-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="925ed-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="925ed-129">Next steps</span></span>
- [<span data-ttu-id="925ed-130">適用於 MySQL 的 Azure 資料庫的連線庫</span><span class="sxs-lookup"><span data-stu-id="925ed-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)