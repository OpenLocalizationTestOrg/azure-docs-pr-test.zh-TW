---
title: "aaaCreate 及管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則 |Microsoft 文件"
description: "建立和管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="d4375-103">建立和管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d4375-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="d4375-104">伺服器層級防火牆規則可讓系統管理員 tooaccess Azure Database PostgreSQL 伺服器從指定的 IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="d4375-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d4375-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="d4375-105">Prerequisites</span></span>
<span data-ttu-id="d4375-106">透過這個方式 tooguide toostep，您需要：</span><span class="sxs-lookup"><span data-stu-id="d4375-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="d4375-107">[建立適用於 PostgreSQL 的 Azure 資料庫](quickstart-create-server-database-portal.md)伺服器</span><span class="sxs-lookup"><span data-stu-id="d4375-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="d4375-108">在 hello Azure 入口網站中建立伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d4375-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="d4375-109">在 hello PostgreSQL 伺服器刀鋒視窗中，設定下標題之下，按一下**連線安全性**tooopen hello 連線安全性刀鋒視窗中的 hello Azure PostgreSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="d4375-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d4375-111">按一下**加入我的 IP** hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="d4375-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="d4375-112">這將會自動建立規則，您的電腦，hello Azure 系統所了解 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4375-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Azure 入口網站 - 按一下 [新增我的 IP]](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="d4375-114">儲存 hello 組態之前，請確認您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4375-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="d4375-115">在某些情況下，Azure 入口網站所觀察到的 hello IP 位址與 hello 所使用的 IP 位址時存取 hello 網際網路和 Azure 的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d4375-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="d4375-116">因此，您可能需要 toochange hello 起始 IP 和結束 IP toomake hello 規則運作不如預期。</span><span class="sxs-lookup"><span data-stu-id="d4375-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="d4375-117">使用搜尋引擎或其他線上工具 toocheck 您自己的 IP 位址 （例如，Bing 搜尋 「 什麼是我的 IP 」）。</span><span class="sxs-lookup"><span data-stu-id="d4375-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![使用 Bing 搜尋「我的 IP 是什麼」](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="d4375-119">新增其他位址範圍。</span><span class="sxs-lookup"><span data-stu-id="d4375-119">Add additional address ranges.</span></span> <span data-ttu-id="d4375-120">在 hello hello Azure Database PostgreSQL 防火牆規則，您可以指定單一 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="d4375-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="d4375-121">如果您想 toolimit hello 規則 tooone 單一 IP 位址，相同的起始 IP 和結束 IP 位址 hello 欄位的型別 hello。</span><span class="sxs-lookup"><span data-stu-id="d4375-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="d4375-122">開啟 hello 防火牆可讓系統管理員和使用者 toologin tooany 資料庫上 hello PostgreSQL 伺服器 toowhich 它們具有有效的認證。</span><span class="sxs-lookup"><span data-stu-id="d4375-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="d4375-123">Azure 入口網站 - 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d4375-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="d4375-124">按一下**儲存**上 hello 工具列 toosave 此伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4375-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="d4375-125">等候 hello 確認 hello 更新 toohello 防火牆規則已順利完成。</span><span class="sxs-lookup"><span data-stu-id="d4375-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Azure 入口網站 - 按一下 [儲存]](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="d4375-127">管理現有的伺服器層級防火牆規則，透過 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d4375-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="d4375-128">重複 hello 步驟 toomanage hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d4375-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="d4375-129">tooadd hello 目前的電腦，按一下 [hello] 按鈕太 +**加入我的 IP**。</span><span class="sxs-lookup"><span data-stu-id="d4375-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="d4375-130">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d4375-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d4375-131">tooadd 額外的 IP 位址，輸入在 hello 規則名稱、 起始 IP 位址，與結束 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d4375-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="d4375-132">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d4375-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d4375-133">toomodify 現有的規則，按一下任一個 hello hello 規則中的欄位，並修改。</span><span class="sxs-lookup"><span data-stu-id="d4375-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="d4375-134">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d4375-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="d4375-135">toodelete 現有的規則，按一下 hello 省略符號 […]，然後按一下 [刪除移除 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="d4375-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="d4375-136">按一下**儲存**toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="d4375-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4375-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d4375-137">Next steps</span></span>
- <span data-ttu-id="d4375-138">同樣地，您可以編寫指令碼太[建立及管理 Azure 資料庫使用 Azure CLI PostgreSQL 防火牆規則](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d4375-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="d4375-139">連線 PostgreSQL 伺服器 tooan Azure 資料庫的說明，請參閱[PostgreSQL 的 Azure 資料庫的連接程式庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d4375-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
