---
title: "aaaHow tooRestore MySQL 的 Azure 資料庫中的伺服器 |Microsoft 文件"
description: "本文說明如何 toorestore Azure Database 中的伺服器使用 MySQL hello Azure 入口網站。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="0a967-103">TooBackup 和還原 Azure 資料庫中的伺服器使用 MySQL hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0a967-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="0a967-104">備份會自動進行</span><span class="sxs-lookup"><span data-stu-id="0a967-104">Backup happens Automatically</span></span>
<span data-ttu-id="0a967-105">當使用 Azure 資料庫的 MySQL，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。</span><span class="sxs-lookup"><span data-stu-id="0a967-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="0a967-106">hello 備份時，可以使用 7 天內使用基本層次中，則為 35 天使用標準層時。</span><span class="sxs-lookup"><span data-stu-id="0a967-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="0a967-107">如需詳細資訊，請參閱[適用於 MySQL 的 Azure 資料庫服務層](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="0a967-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="0a967-108">使用這個自動備份功能您可能會到新伺服器 tooan 稍早的時間點還原 hello 伺服器及其所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="0a967-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="0a967-109">將還原的 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0a967-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="0a967-110">Azure 的 MySQL 資料庫可讓您 toorestore hello 伺服器回復 tooa 點的時間，並置於 tooa hello 伺服器新複本。</span><span class="sxs-lookup"><span data-stu-id="0a967-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="0a967-111">您可以使用這個新的伺服器 toorecover 您的資料。</span><span class="sxs-lookup"><span data-stu-id="0a967-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="0a967-112">比方說，如果資料表已意外卸除正午現在，您無法還原 toohello 正午之前的時間，擷取 hello 遺漏的資料表和資料從 hello 伺服器的新複本。</span><span class="sxs-lookup"><span data-stu-id="0a967-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="0a967-113">hello 下列的步驟還原 hello 範例伺服器 tooa 點時間：</span><span class="sxs-lookup"><span data-stu-id="0a967-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="0a967-114">登入 hello [Azure 入口網站](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="0a967-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="0a967-115">找出適用於 MySQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a967-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="0a967-116">Hello 左窗格中，選取**所有資源**，然後從 hello 清單中選取您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a967-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="0a967-117">在 hello hello 伺服器概觀刀鋒視窗頂端，按一下 **還原**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="0a967-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="0a967-118">hello 還原刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="0a967-118">hello Restore blade opens.</span></span>
<span data-ttu-id="0a967-119">![按一下 [還原] 按鈕](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="0a967-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="0a967-120">填寫 hello 還原表單 hello 所需的資訊：</span><span class="sxs-lookup"><span data-stu-id="0a967-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="0a967-121">**還原點 (UTC)**： 使用 hello 日期選擇器和時間選擇器，選取時間點 toorestore 至。</span><span class="sxs-lookup"><span data-stu-id="0a967-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="0a967-122">指定的 hello 時間是 UTC 格式，因此您可能需要 tooconvert hello 本地時間到 UTC。</span><span class="sxs-lookup"><span data-stu-id="0a967-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="0a967-123">**還原 toonew 伺服器**： 提供新的伺服器名稱 toorestore hello 現有伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a967-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="0a967-124">**位置**: hello 區域選擇自動填入 hello 來源伺服器的地區，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="0a967-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="0a967-125">**定價層**: hello 定價層選擇自動填入的 hello 相同定價層為 hello 來源伺服器，並無法在此進行變更。</span><span class="sxs-lookup"><span data-stu-id="0a967-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="0a967-126">![PITR 還原](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="0a967-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="0a967-127">按一下**確定**toorestore hello 伺服器 toorestore tooa 時間點。</span><span class="sxs-lookup"><span data-stu-id="0a967-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="0a967-128">Hello 還原完成後，找出已建立的資料庫已還原，如預期般 tooverify hello 的 hello 新伺服器。</span><span class="sxs-lookup"><span data-stu-id="0a967-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a967-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a967-129">Next steps</span></span>
- [<span data-ttu-id="0a967-130">適用於 MySQL 的 Azure 資料庫的連線庫</span><span class="sxs-lookup"><span data-stu-id="0a967-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)