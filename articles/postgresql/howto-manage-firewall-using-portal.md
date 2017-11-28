---
title: "使用 Azure 入口網站建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則 | Microsoft Docs"
description: "使用 Azure 入口網站建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="7be8f-103">使用 Azure 入口網站建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7be8f-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="7be8f-104">伺服器等級防火牆規則可讓系統管理員從指定的 IP 位址或 IP 位址範圍，存取適用於 PostgreSQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="7be8f-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7be8f-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="7be8f-105">Prerequisites</span></span>
<span data-ttu-id="7be8f-106">若要逐步執行本作法指南，您需要︰</span><span class="sxs-lookup"><span data-stu-id="7be8f-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7be8f-107">[建立適用於 PostgreSQL 的 Azure 資料庫](quickstart-create-server-database-portal.md)伺服器</span><span class="sxs-lookup"><span data-stu-id="7be8f-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="7be8f-108">在 Azure 入口網站中建立伺服器層級的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7be8f-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="7be8f-109">在 [PostgreSQL 伺服器] 刀鋒視窗的 [設定] 標題下，按一下 [連線安全性]，開啟適用於 PostgreSQL 的 Azure 資料庫的 [連線安全性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7be8f-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="7be8f-111">按一下工具列上的 [新增我的 IP]。</span><span class="sxs-lookup"><span data-stu-id="7be8f-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="7be8f-112">這會使用 Azure 系統發現的電腦 IP 位址自動建立規則。</span><span class="sxs-lookup"><span data-stu-id="7be8f-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Azure 入口網站 - 按一下 [新增我的 IP]](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="7be8f-114">儲存設定之前，請確認您的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7be8f-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="7be8f-115">在某些情況下，Azure 入口網站觀察到的 IP 位址，不同於用來存取網際網路和 Azure 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7be8f-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="7be8f-116">因此，您可能需要變更起始 IP 和結束 IP，規則才會正常運作。</span><span class="sxs-lookup"><span data-stu-id="7be8f-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="7be8f-117">使用搜尋引擎或其他線上工具，檢查您自己的 IP 位址 (例如，使用 Bing 搜尋「我的 IP 位址是什麼」)。</span><span class="sxs-lookup"><span data-stu-id="7be8f-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![使用 Bing 搜尋「我的 IP 是什麼」](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="7be8f-119">新增其他位址範圍。</span><span class="sxs-lookup"><span data-stu-id="7be8f-119">Add additional address ranges.</span></span> <span data-ttu-id="7be8f-120">在「適用於 PostgreSQL 的 Azure 資料庫」防火牆的規則中，您可以指定單一 IP 位址，或位址範圍。</span><span class="sxs-lookup"><span data-stu-id="7be8f-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="7be8f-121">如果您想要將規則限制到單一 IP 位址，請在 [起始 IP] 和 [結束 IP] 欄位中輸入相同位址。</span><span class="sxs-lookup"><span data-stu-id="7be8f-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="7be8f-122">開放防火牆可讓系統管理員和使用者登入他們在 PostgreSQL 伺服器上具備有效認證的任何資料庫。</span><span class="sxs-lookup"><span data-stu-id="7be8f-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="7be8f-123">Azure 入口網站 - 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7be8f-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="7be8f-124">按一下工具列上的 [儲存]，儲存此伺服器等級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7be8f-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="7be8f-125">等待確認已成功更新防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7be8f-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Azure 入口網站 - 按一下 [儲存]](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="7be8f-127">透過 Azure 入口網站管理現有的伺服器層級防火牆規則</span><span class="sxs-lookup"><span data-stu-id="7be8f-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="7be8f-128">重複步驟來管理防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="7be8f-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="7be8f-129">若要新增目前的電腦，請按一下 [+新增我的 IP] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7be8f-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="7be8f-130">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7be8f-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="7be8f-131">若要新增其他 IP 位址，請輸入「規則名稱」、「起始 IP 位址」和「結束 IP 位址」。</span><span class="sxs-lookup"><span data-stu-id="7be8f-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="7be8f-132">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7be8f-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="7be8f-133">若要修改現有的規則，請按一下和修改規則中的任何欄位。</span><span class="sxs-lookup"><span data-stu-id="7be8f-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="7be8f-134">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7be8f-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="7be8f-135">若要刪除現有的規則，請按一下省略符號 [...]，然後按一下 [刪除] 移除規則。</span><span class="sxs-lookup"><span data-stu-id="7be8f-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="7be8f-136">按一下 [儲存]  儲存變更。</span><span class="sxs-lookup"><span data-stu-id="7be8f-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7be8f-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7be8f-137">Next steps</span></span>
- <span data-ttu-id="7be8f-138">同樣地，您可以透過指令碼[使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7be8f-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="7be8f-139">如需連線至「適用於 PostgreSQL 的 Azure 資料庫」伺服器的說明，請參閱[「適用於 PostgreSQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="7be8f-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
