---
title: "設計您第一個適用於 MySQL 資料庫的 Azure 資料庫 - Azure 入口網站 | Microsoft Docs"
description: "本教學課程說明如何使用「Azure 入口網站」來建立和管理「適用於 MySQL 的 Azure 資料庫」伺服器。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: c7b76cacbdc4e483353f64cc4e50c974867bb5b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="c6ced-103">設計您第一個適用於 MySQL 資料庫的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="c6ced-104">「適用於 MySQL 的 Azure 資料庫」是一個受管理的服務，可讓您在雲端執行、管理及調整高可用性 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6ced-104">Azure Database for MySQL is a managed service that enables you to run, manage, and scale highly available MySQL databases in the cloud.</span></span> <span data-ttu-id="c6ced-105">使用 Azure 入口網站，您可以輕鬆管理伺服器和設計資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6ced-105">Using the Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="c6ced-106">在本教學課程中，您將使用 Azure 入口網站來學習如何：</span><span class="sxs-lookup"><span data-stu-id="c6ced-106">In this tutorial, you use the Azure portal to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c6ced-107">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c6ced-108">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="c6ced-108">Configure the server firewall</span></span>
> * <span data-ttu-id="c6ced-109">使用 mysql 命令列工具來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-109">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="c6ced-110">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-110">Load sample data</span></span>
> * <span data-ttu-id="c6ced-111">查詢資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-111">Query data</span></span>
> * <span data-ttu-id="c6ced-112">更新資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-112">Update data</span></span>
> * <span data-ttu-id="c6ced-113">還原資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-113">Restore data</span></span>

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="c6ced-114">登入 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c6ced-114">Sign in to the Azure portal</span></span>
<span data-ttu-id="c6ced-115">開啟您的慣用網頁瀏覽器，然後瀏覽至 [Microsoft Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="c6ced-115">Open your favorite web browser, and visit the [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="c6ced-116">輸入您的認證來登入此入口網站。</span><span class="sxs-lookup"><span data-stu-id="c6ced-116">Enter your credentials to sign in to the portal.</span></span> <span data-ttu-id="c6ced-117">預設檢視是您的服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="c6ced-117">The default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="c6ced-118">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="c6ced-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="c6ced-119">建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。</span><span class="sxs-lookup"><span data-stu-id="c6ced-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="c6ced-120">伺服器會建立在 [Azure 資源群組](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)內。</span><span class="sxs-lookup"><span data-stu-id="c6ced-120">The server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="c6ced-121">瀏覽至 [資料庫] > [Azure Database for MySQL]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-121">Navigate to **Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="c6ced-122">如果您在 [資料庫] 類別底下找不到「MySQL 伺服器」，請按一下 [查看全部] 以顯示所有可用的資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="c6ced-122">If you cannot find MySQL Server under **Databases** category, click **See all** to show all available database services.</span></span> <span data-ttu-id="c6ced-123">您也可以在搜尋方塊中輸入 [Azure Database for MySQL] 以快速找到此服務。</span><span class="sxs-lookup"><span data-stu-id="c6ced-123">You can also type **Azure Database for MySQL** in the search box to quickly find the service.</span></span>
<span data-ttu-id="c6ced-124">![2-1 瀏覽至 MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="c6ced-124">![2-1 Navigate to MySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="c6ced-125">按一下 [Azure Database for MySQL] 圖格，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="c6ced-126">在我們的範例中，於「適用於 MySQL 的 Azure 資料庫」表單中填入下列資訊：</span><span class="sxs-lookup"><span data-stu-id="c6ced-126">In our example, fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="c6ced-127">**設定**</span><span class="sxs-lookup"><span data-stu-id="c6ced-127">**Setting**</span></span> | <span data-ttu-id="c6ced-128">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="c6ced-128">**Suggested value**</span></span> | <span data-ttu-id="c6ced-129">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="c6ced-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="c6ced-130">*伺服器名稱*</span><span class="sxs-lookup"><span data-stu-id="c6ced-130">*Server name*</span></span> | <span data-ttu-id="c6ced-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="c6ced-131">myserver4demo</span></span>  | <span data-ttu-id="c6ced-132">伺服器名稱必須是全域唯一的。</span><span class="sxs-lookup"><span data-stu-id="c6ced-132">Server name has to be globally unique.</span></span> |
| <span data-ttu-id="c6ced-133">*訂用帳戶*</span><span class="sxs-lookup"><span data-stu-id="c6ced-133">*Subscription*</span></span> | <span data-ttu-id="c6ced-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="c6ced-134">mysubscription</span></span> | <span data-ttu-id="c6ced-135">從下拉式清單中選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c6ced-135">Select your subscription from the drop-down.</span></span> |
| <span data-ttu-id="c6ced-136">*資源群組*</span><span class="sxs-lookup"><span data-stu-id="c6ced-136">*Resource group*</span></span> | <span data-ttu-id="c6ced-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="c6ced-137">myresourcegroup</span></span> | <span data-ttu-id="c6ced-138">建立資源群組或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c6ced-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="c6ced-139">*伺服器管理員登入*</span><span class="sxs-lookup"><span data-stu-id="c6ced-139">*Server admin login*</span></span> | <span data-ttu-id="c6ced-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="c6ced-140">myadmin</span></span> | <span data-ttu-id="c6ced-141">設定管理帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ced-141">Setup admin account name.</span></span> |
| <span data-ttu-id="c6ced-142">*密碼*</span><span class="sxs-lookup"><span data-stu-id="c6ced-142">*Password*</span></span> |  | <span data-ttu-id="c6ced-143">設定強式管理帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="c6ced-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="c6ced-144">*確認密碼*</span><span class="sxs-lookup"><span data-stu-id="c6ced-144">*Confirm password*</span></span> |  | <span data-ttu-id="c6ced-145">確認管理帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="c6ced-145">Confirm the admin account password.</span></span> |
| <bpt id="p1">*</bpt>Location<ept id="p1">*</ept> |  | <span data-ttu-id="c6ced-147">選取可用的區域。</span><span class="sxs-lookup"><span data-stu-id="c6ced-147">Select an available region.</span></span> |
| <span data-ttu-id="c6ced-148">*版本*</span><span class="sxs-lookup"><span data-stu-id="c6ced-148">*Version*</span></span> | <span data-ttu-id="c6ced-149">5.7</span><span class="sxs-lookup"><span data-stu-id="c6ced-149">5.7</span></span> | <span data-ttu-id="c6ced-150">選擇最新版本。</span><span class="sxs-lookup"><span data-stu-id="c6ced-150">Choose the latest version.</span></span> |
| <span data-ttu-id="c6ced-151">*設定效能*</span><span class="sxs-lookup"><span data-stu-id="c6ced-151">*Configure performance*</span></span> | <span data-ttu-id="c6ced-152">基本、50 個計算單位、50 GB</span><span class="sxs-lookup"><span data-stu-id="c6ced-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="c6ced-153">選擇 **[定價層]** 、 **[計算單位]** 、**[儲存體]** \(GB) ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="c6ced-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="c6ced-154">釘選到儀表板</span><span class="sxs-lookup"><span data-stu-id="c6ced-154">*Pin to Dashboard*</span></span> | <span data-ttu-id="c6ced-155">勾選</span><span class="sxs-lookup"><span data-stu-id="c6ced-155">Check</span></span> | <span data-ttu-id="c6ced-156">建議您核取此方塊，讓您在稍後能輕鬆地找到伺服器</span><span class="sxs-lookup"><span data-stu-id="c6ced-156">Recommended to check this box so you may find the server easily later on</span></span> |
<span data-ttu-id="c6ced-157">然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="c6ced-157">Then, click **Create**.</span></span> <span data-ttu-id="c6ced-158">在一兩分鐘內，新的「適用於 MySQL 的 Azure 資料庫」伺服器就會在雲端執行。</span><span class="sxs-lookup"><span data-stu-id="c6ced-158">In a minute or two, a new Azure Database for MySQL server is running in the cloud.</span></span> <span data-ttu-id="c6ced-159">您可以按一下工具列上的 [通知] 按鈕來監視部署程序。</span><span class="sxs-lookup"><span data-stu-id="c6ced-159">You can click **Notifications** button on the toolbar to monitor the deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="c6ced-160">設定防火牆</span><span class="sxs-lookup"><span data-stu-id="c6ced-160">Configure firewall</span></span>
<span data-ttu-id="c6ced-161">「適用於 MySQL 的 Azure 資料庫」會受到防火牆保護。</span><span class="sxs-lookup"><span data-stu-id="c6ced-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="c6ced-162">依預設，伺服器與其內部資料庫的所有連線皆會遭拒。</span><span class="sxs-lookup"><span data-stu-id="c6ced-162">By default, all connections to the server and the databases inside the server are rejected.</span></span> <span data-ttu-id="c6ced-163">第一次連線到 Azure Database for MySQL 之前，請設定防火牆來新增用戶端的公用網路 IP 位址 (或 IP 位址範圍)。</span><span class="sxs-lookup"><span data-stu-id="c6ced-163">Before connecting to Azure Database for MySQL for the first time, configure the firewall to add the client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="c6ced-164">按一下您新建立的伺服器，然後按一下 [連線安全性]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="c6ced-165">![3-1 連線安全性](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="c6ced-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="c6ced-166">您可以在這裡 [新增我的 IP]，或設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="c6ced-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="c6ced-167">請記得在建立規則後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-167">Remember to click **Save** after you have created the rules.</span></span>
<span data-ttu-id="c6ced-168">您現在可以使用 mysql 命令列工具或 MySQL Workbench GUI 工具來連線到伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6ced-168">You can now connect to the server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="c6ced-169">「適用於 MySQL 的 Azure 資料庫」伺服器會透過連接埠 3306 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c6ced-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="c6ced-170">如果您嘗試從公司網路內進行連線，您網路的防火牆可能不允許透過連接埠 3306 的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="c6ced-170">If you are trying to connect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="c6ced-171">若是如此，除非 IT 部門開啟連接埠 1433，否則您無法連線至 Azure MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6ced-171">If so, you cannot connect to Azure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c6ced-172">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="c6ced-172">Get connection information</span></span>
<span data-ttu-id="c6ced-173">請從 Azure 入口網站取得 Azure Database for MySQL 伺服器的完整 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-173">Get the fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from the Azure portal.</span></span> <span data-ttu-id="c6ced-174">您將使用 mysql 命令列工具搭配此完整伺服器名稱來連線到伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6ced-174">You use the fully qualified server name to connect to your server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="c6ced-175">在 [Azure 入口網站](https://portal.azure.com/)中，按一下左側功能表中的 [所有資源]，輸入名稱，然後搜尋您的 Azure Database for MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c6ced-175">In [Azure portal](https://portal.azure.com/), click **All resources** from the left-hand menu, type the name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="c6ced-176">選取伺服器名稱以檢視詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-176">Select the server name to view the details.</span></span>

2. <span data-ttu-id="c6ced-177">在 [設定] 標題之下，按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-177">Under the Settings heading, click **Properties**.</span></span> <span data-ttu-id="c6ced-178">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="c6ced-179">您可以按一下每個欄位旁邊的 [複製] 按鈕，以複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c6ced-179">You may click the copy button next to each field to copy to the clipboard.</span></span>
   <span data-ttu-id="c6ced-180">![4-2 伺服器屬性](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="c6ced-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="c6ced-181">在此範例中，伺服器名稱為 myserver4demo.mysql.database.azure.com，而伺服器管理員登入為 myadmin@myserver4demo。</span><span class="sxs-lookup"><span data-stu-id="c6ced-181">In this example, the server name is *myserver4demo.mysql.database.azure.com*, and the server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="c6ced-182">使用 mysql 來連線到伺服器</span><span class="sxs-lookup"><span data-stu-id="c6ced-182">Connect to the server using mysql</span></span>
<span data-ttu-id="c6ced-183">使用 [mysql 命令列工具](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)來建立對「適用於 MySQL 的 Azure 資料庫」伺服器的連線。</span><span class="sxs-lookup"><span data-stu-id="c6ced-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="c6ced-184">您可以從 Azure Cloud Shell 在瀏覽器中，或從自己的電腦使用本機安裝的 mysql 工具執行 mysql 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="c6ced-184">You can run the mysql command-line tool from the Azure Cloud Shell in the browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="c6ced-185">若要啟動 Azure Cloud Shell，請按一下本文中程式碼區塊的 `Try It` 按鈕，或請造訪 Azure 入口網站並按一下頂端右側工具列的 `>_` 圖示。</span><span class="sxs-lookup"><span data-stu-id="c6ced-185">To launch the Azure Cloud Shell, click the `Try It` button on a code block in this article, or visit the Azure portal and click the `>_` icon in the top right toolbar.</span></span> 

<span data-ttu-id="c6ced-186">輸入要連線的命令：</span><span class="sxs-lookup"><span data-stu-id="c6ced-186">Type the command to connect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="c6ced-187">建立空白資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-187">Create a blank database</span></span>
<span data-ttu-id="c6ced-188">連線到伺服器之後，請建立一個要搭配運作的空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6ced-188">Once you’re connected to the server, create a blank database to work with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="c6ced-189">在提示字元，執行下列命令以將連線切換到這個新建立的資料庫：</span><span class="sxs-lookup"><span data-stu-id="c6ced-189">At the prompt, run the following command to switch connection to this newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="c6ced-190">在資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="c6ced-190">Create tables in the database</span></span>
<span data-ttu-id="c6ced-191">既然您已知道如何連線到「適用於 MySQL 資料庫的 Azure 資料庫」，我們可以了解一下如何完成一些基本工作。</span><span class="sxs-lookup"><span data-stu-id="c6ced-191">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="c6ced-192">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="c6ced-193">我們將建立一個儲存清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="c6ced-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="c6ced-194">將資料載入到資料表</span><span class="sxs-lookup"><span data-stu-id="c6ced-194">Load data into the tables</span></span>
<span data-ttu-id="c6ced-195">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="c6ced-196">在開啟的命令提示字元視窗，執行下列查詢以插入幾列資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-196">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="c6ced-197">您現在已將兩列範例資料插入到先前建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="c6ced-197">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="c6ced-198">查詢並更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-198">Query and update the data in the tables</span></span>
<span data-ttu-id="c6ced-199">執行下列查詢，以從資料庫資料表中擷取資訊。</span><span class="sxs-lookup"><span data-stu-id="c6ced-199">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="c6ced-200">您也可以更新資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-200">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="c6ced-201">當您擷取資料時，資料列會相應地更新。</span><span class="sxs-lookup"><span data-stu-id="c6ced-201">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="c6ced-202">將資料庫還原至先前的時間點</span><span class="sxs-lookup"><span data-stu-id="c6ced-202">Restore a database to a previous point in time</span></span>
<span data-ttu-id="c6ced-203">假設您不小心刪除重要的資料庫資料表，而無法輕易地復原資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-203">Imagine you have accidentally deleted an important database table, and cannot recover the data easily.</span></span> <span data-ttu-id="c6ced-204">Azure Database for MySQL 可讓您將伺服器還原至某個時間點，並在新的伺服器中建立資料庫的複本。</span><span class="sxs-lookup"><span data-stu-id="c6ced-204">Azure Database for MySQL allows you to restore the server to a point in time, creating a copy of the databases into new server.</span></span> <span data-ttu-id="c6ced-205">您可以使用這個新的伺服器來復原已刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="c6ced-205">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="c6ced-206">下列步驟會將範例伺服器還原到新增資料表之前的時間點。</span><span class="sxs-lookup"><span data-stu-id="c6ced-206">The following steps restore the sample server to a point before the table was added.</span></span>

1. <span data-ttu-id="c6ced-207">在 Azure 入口網站中，找出您的 Azure Database for MySQL。</span><span class="sxs-lookup"><span data-stu-id="c6ced-207">In the Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="c6ced-208">在 [概觀] 頁面上，按一下工具列上的 [還原]。</span><span class="sxs-lookup"><span data-stu-id="c6ced-208">On the **Overview** page, click **Restore** on the toolbar.</span></span> <span data-ttu-id="c6ced-209">[還原] 頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="c6ced-209">The Restore page opens.</span></span>

   ![10-1 還原資料庫](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="c6ced-211">在 [還原] 表單中填入必要資訊。</span><span class="sxs-lookup"><span data-stu-id="c6ced-211">Fill out the **Restore** form with the required information.</span></span>
   
   ![10-2 還原表單](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="c6ced-213">**還原點**：在所列的時間範圍內，選取您想要還原的時間點。</span><span class="sxs-lookup"><span data-stu-id="c6ced-213">**Restore point**: Select a point-in-time that you want to restore to, within the timeframe listed.</span></span> <span data-ttu-id="c6ced-214">務必將您的當地時區轉換成 UTC。</span><span class="sxs-lookup"><span data-stu-id="c6ced-214">Make sure to convert your local timezone to UTC.</span></span>
   - <span data-ttu-id="c6ced-215">**還原到新伺服器**︰提供要作為還原目的地的新伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="c6ced-215">**Restore to new server**: Provide a new server name you want to restore to.</span></span>
   - <span data-ttu-id="c6ced-216">**位置**︰此區域與來源伺服器相同，無法加以變更。</span><span class="sxs-lookup"><span data-stu-id="c6ced-216">**Location**: The region is same as the source server, and cannot be changed.</span></span>
   - <span data-ttu-id="c6ced-217">**定價層**︰此定價層與來源伺服器相同，無法加以變更。</span><span class="sxs-lookup"><span data-stu-id="c6ced-217">**Pricing tier**: The pricing tier is the same as the source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="c6ced-218">按一下 [確定]，將伺服器[還原到資料表刪除之前的時間點](./howto-restore-server-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="c6ced-218">Click **OK** to restore the server to [restore to a point in time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="c6ced-219">還原伺服器可建立伺服器的新複本 (自您指定的時間點起)。</span><span class="sxs-lookup"><span data-stu-id="c6ced-219">Restoring a server creates a new copy of the server, as of the point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6ced-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c6ced-220">Next steps</span></span>
<span data-ttu-id="c6ced-221">在本教學課程中，您使用 Azure 入口網站來學習如何：</span><span class="sxs-lookup"><span data-stu-id="c6ced-221">In this tutorial, you use the Azure portal to learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c6ced-222">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="c6ced-223">設定伺服器防火牆</span><span class="sxs-lookup"><span data-stu-id="c6ced-223">Configure the server firewall</span></span>
> * <span data-ttu-id="c6ced-224">使用 mysql 命令列工具來建立資料庫</span><span class="sxs-lookup"><span data-stu-id="c6ced-224">Use mysql command-line tool to create a database</span></span>
> * <span data-ttu-id="c6ced-225">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-225">Load sample data</span></span>
> * <span data-ttu-id="c6ced-226">查詢資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-226">Query data</span></span>
> * <span data-ttu-id="c6ced-227">更新資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-227">Update data</span></span>
> * <span data-ttu-id="c6ced-228">還原資料</span><span class="sxs-lookup"><span data-stu-id="c6ced-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c6ced-229">如何將應用程式連線至 Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="c6ced-229">How to connect applications to Azure Database for MySQL</span></span>](./howto-connection-string.md)
