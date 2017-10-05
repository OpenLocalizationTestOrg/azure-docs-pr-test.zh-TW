---
title: "使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則 | Microsoft Docs"
description: "使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="69c37-103">使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="69c37-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="69c37-104">伺服器等級防火牆規則可讓系統管理員從指定的 IP 位址或 IP 位址範圍，存取適用於 MySQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="69c37-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="69c37-105">在 Azure 入口網站中建立伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="69c37-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="69c37-106">在 [MySQL 伺服器] 刀鋒視窗的 [設定] 標題下，按一下 [連線安全性]，開啟「適用於 MySQL 的 Azure 資料庫」的 [連線安全性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="69c37-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="69c37-108">在工具列上按一下 [新增我的 IP]，可使用 Azure 系統發現的電腦 IP 位址建立規則。</span><span class="sxs-lookup"><span data-stu-id="69c37-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Azure 入口網站 - 按一下 [新增我的 IP]](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="69c37-110">儲存設定之前，請確認您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="69c37-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="69c37-111">在某些情況下，Azure 入口網站觀察到的 IP 位址，不同於用來存取網際網路和 Azure 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="69c37-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="69c37-112">因此，您可能需要變更起始 IP 和結束 IP，規則才會正常運作。</span><span class="sxs-lookup"><span data-stu-id="69c37-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="69c37-113">使用搜尋引擎或其他線上工具，檢查您自己的 IP 位址 (例如，搜尋「我的 IP 位址是什麼」)。</span><span class="sxs-lookup"><span data-stu-id="69c37-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![使用 Bing 搜尋「我的 IP 位址是什麼」](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="69c37-115">新增其他位址範圍。</span><span class="sxs-lookup"><span data-stu-id="69c37-115">Add additional address ranges.</span></span> <span data-ttu-id="69c37-116">在「適用於 MySQL 的 Azure 資料庫」防火牆的規則中，您可以指定單一 IP 位址，或位址範圍。</span><span class="sxs-lookup"><span data-stu-id="69c37-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="69c37-117">如果您想要將規則限制到單一 IP 位址，請在 [起始 IP] 和 [結束 IP] 欄位中輸入相同位址。</span><span class="sxs-lookup"><span data-stu-id="69c37-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="69c37-118">開放防火牆可讓系統管理員和使用者存取他們在 MySQL 伺服器上具備有效認證的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="69c37-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="69c37-119">Azure 入口網站 - 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="69c37-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="69c37-120">按一下工具列上的 [儲存]，儲存此伺服器等級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="69c37-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="69c37-121">等待確認已成功更新防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="69c37-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Azure 入口網站 - 按一下 [儲存]](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="69c37-123">透過 Azure 入口網站管理現有的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="69c37-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="69c37-124">重複步驟來管理防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="69c37-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="69c37-125">若要新增目前的電腦，請按一下 [+新增我的 IP]。</span><span class="sxs-lookup"><span data-stu-id="69c37-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="69c37-126">若要新增其他 IP 位址，請輸入 [規則名稱]、[起始 IP 位址] 和 [結束 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="69c37-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="69c37-127">若要修改現有的規則，請按一下和修改規則中的任何欄位。</span><span class="sxs-lookup"><span data-stu-id="69c37-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="69c37-128">若要刪除現有的規則，請按一下省略符號 [...]，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="69c37-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="69c37-129">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="69c37-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69c37-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69c37-130">Next steps</span></span>
- <span data-ttu-id="69c37-131">如需連線至「適用於 MySQL 的 Azure 資料庫」伺服器的說明，請參閱[「適用於 MySQL 的 Azure 資料庫」的連線庫](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="69c37-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
