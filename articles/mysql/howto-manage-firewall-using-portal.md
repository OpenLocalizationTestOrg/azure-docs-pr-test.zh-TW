---
title: "aaaCreate 和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則 |Microsoft 文件"
description: "建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="a0021-103">建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0021-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="a0021-104">伺服器層級防火牆規則可讓系統管理員 tooaccess Azure 資料庫的 MySQL 伺服器從指定的 IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a0021-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="a0021-105">在 hello Azure 入口網站中建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0021-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="a0021-106">Hello MySQL 伺服器 刀鋒視窗，設定下標題之下，按一下**連線安全性**tooopen hello 連線安全性刀鋒視窗中的 hello Azure MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a0021-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="a0021-108">按一下**加入我的 IP**上 hello 工具列 toocreate hello IP 位址的電腦，因為看得見 hello Azure 系統的規則。</span><span class="sxs-lookup"><span data-stu-id="a0021-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Azure 入口網站 - 按一下 [新增我的 IP]](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="a0021-110">儲存 hello 組態之前，請確認您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a0021-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="a0021-111">在某些情況下，Azure 入口網站所觀察到的 hello IP 位址與 hello 所使用的 IP 位址時存取 hello 網際網路和 Azure 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0021-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="a0021-112">因此，您可能需要 toochange hello 起始 IP 和結束 IP toomake hello 規則運作不如預期。</span><span class="sxs-lookup"><span data-stu-id="a0021-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="a0021-113">使用搜尋引擎或其他線上工具 toocheck 您自己的 IP 位址 （例如，搜尋 「 什麼是我的 IP 位址 」）。</span><span class="sxs-lookup"><span data-stu-id="a0021-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![使用 Bing 搜尋「我的 IP 位址是什麼」](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="a0021-115">新增其他位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a0021-115">Add additional address ranges.</span></span> <span data-ttu-id="a0021-116">在 hello hello Azure 資料庫的 MySQL 防火牆規則，您可以指定單一 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a0021-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="a0021-117">如果您想 toolimit hello 規則 tooone 單一 IP 位址，相同的起始 IP 和結束 IP 位址 hello 欄位的型別 hello。</span><span class="sxs-lookup"><span data-stu-id="a0021-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="a0021-118">開啟 hello 防火牆可讓系統管理員和使用者 tooaccess hello MySQL server toowhich 它們具有有效的認證上任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="a0021-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="a0021-119">Azure 入口網站 - 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0021-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="a0021-120">按一下**儲存**上 hello 工具列 toosave 此伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0021-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="a0021-121">等候 hello 確認 hello 更新 toohello 防火牆規則已順利完成。</span><span class="sxs-lookup"><span data-stu-id="a0021-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Azure 入口網站 - 按一下 [儲存]](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="a0021-123">管理現有的伺服器層級防火牆規則，透過 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a0021-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="a0021-124">重複 hello 步驟 toomanage hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0021-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="a0021-125">tooadd hello 目前的電腦，按一下**+ 加入我的 IP**。</span><span class="sxs-lookup"><span data-stu-id="a0021-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="a0021-126">tooadd 額外的 IP 位址，在 hello**規則名稱**，**起始 IP**，和**結束 IP**。</span><span class="sxs-lookup"><span data-stu-id="a0021-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="a0021-127">toomodify 現有的規則，按一下任一個 hello hello 規則中的欄位，並修改。</span><span class="sxs-lookup"><span data-stu-id="a0021-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="a0021-128">toodelete 現有規則，按一下 hello 省略符號 […]，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="a0021-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="a0021-129">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="a0021-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0021-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0021-130">Next steps</span></span>
- <span data-ttu-id="a0021-131">在連接 tooan Azure 資料庫的 MySQL 伺服器的說明，請參閱[MySQL 的 Azure 資料庫的連接程式庫](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="a0021-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
