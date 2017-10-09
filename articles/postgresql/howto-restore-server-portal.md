---
title: "如何 tooRestore Azure PostgreSQL 資料庫中的伺服器 |Microsoft 文件"
description: "本文說明如何 toorestore Azure Database 中的伺服器使用 PostgreSQL hello Azure 入口網站。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="0cb27-103">TooBackup 和還原 Azure 資料庫中的伺服器使用 PostgreSQL hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0cb27-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="0cb27-104">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="0cb27-104">Backup happens Automatically</span></span>
<span data-ttu-id="0cb27-105">當使用 Azure 資料庫的 PostgreSQL，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="0cb27-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="0cb27-106">hello 備份時，可以使用 7 天內使用基本層次中，則為 35 天使用標準層時。</span><span class="sxs-lookup"><span data-stu-id="0cb27-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="0cb27-107">如需詳細資訊，請參閱[適用於 PostgreSQL 的 Azure 資料庫服務層](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="0cb27-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="0cb27-108">使用這個自動備份功能您可能會到新伺服器 tooan 稍早的時間點還原 hello 伺服器及其所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="0cb27-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="0cb27-109">將還原的 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0cb27-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="0cb27-110">Azure PostgreSQL 資料庫可讓您 toorestore hello 伺服器回復 tooa 點的時間，並置於 tooa hello 伺服器新複本。</span><span class="sxs-lookup"><span data-stu-id="0cb27-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="0cb27-111">您可以使用這個新的伺服器 toorecover 您的資料。</span><span class="sxs-lookup"><span data-stu-id="0cb27-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="0cb27-112">比方說，如果資料表已意外卸除正午現在，您無法還原 toohello 正午之前的時間，擷取 hello 遺漏的資料表和資料從 hello 伺服器的新複本。</span><span class="sxs-lookup"><span data-stu-id="0cb27-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="0cb27-113">hello 下列的步驟還原 hello 範例伺服器 tooa 點時間：</span><span class="sxs-lookup"><span data-stu-id="0cb27-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="0cb27-114">登入 hello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="0cb27-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="0cb27-115">找出您的「適用於 PostgreSQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="0cb27-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="0cb27-116">在 hello Azure 入口網站，按一下**所有資源**從 hello 左側功能表，然後輸入 hello 名稱，例如**mypgserver 20170401**，toosearch 您現有的伺服器。</span><span class="sxs-lookup"><span data-stu-id="0cb27-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="0cb27-117">按一下 hello hello 搜尋結果中所列的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="0cb27-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="0cb27-118">hello**概觀**頁面會針對您的伺服器會開啟，並提供進一步組態的選項。</span><span class="sxs-lookup"><span data-stu-id="0cb27-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Azure 入口網站-搜尋 toolocate 您的伺服器](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="0cb27-120">在 hello hello 伺服器概觀刀鋒視窗頂端，按一下 **還原**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="0cb27-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="0cb27-121">hello 還原刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0cb27-121">hello Restore blade opens.</span></span>

   ![適用於 PostgreSQL 的 Azure 資料庫 - 概觀 - 還原按鈕](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="0cb27-123">填寫 hello 還原表單 hello 所需的資訊：</span><span class="sxs-lookup"><span data-stu-id="0cb27-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="0cb27-124">適用於 PostgreSQL 的 Azure 資料庫 - 還原資訊</span><span class="sxs-lookup"><span data-stu-id="0cb27-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="0cb27-125">**還原點**： 選取在時間點所發生之前 hello 伺服器已變更</span><span class="sxs-lookup"><span data-stu-id="0cb27-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="0cb27-126">**目標伺服器**： 提供新的伺服器名稱，您想要 toorestore</span><span class="sxs-lookup"><span data-stu-id="0cb27-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="0cb27-127">**位置**： 您無法選取 hello 區域，依預設它是與 hello 來源伺服器相同</span><span class="sxs-lookup"><span data-stu-id="0cb27-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="0cb27-128">**定價層**︰還原伺服器時，您無法變更此值。</span><span class="sxs-lookup"><span data-stu-id="0cb27-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="0cb27-129">它是與 hello 來源伺服器相同。</span><span class="sxs-lookup"><span data-stu-id="0cb27-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="0cb27-130">按一下**確定**toorestore hello 伺服器 toorestore tooa 時間點。</span><span class="sxs-lookup"><span data-stu-id="0cb27-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="0cb27-131">一旦 hello 還原完成時，找出 hello 建立 tooverify hello 如預期般，已還原資料的新伺服器。</span><span class="sxs-lookup"><span data-stu-id="0cb27-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cb27-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cb27-132">Next steps</span></span>
- [<span data-ttu-id="0cb27-133">「適用於 PostgreSQL 的 Azure 資料庫」的連線庫</span><span class="sxs-lookup"><span data-stu-id="0cb27-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
