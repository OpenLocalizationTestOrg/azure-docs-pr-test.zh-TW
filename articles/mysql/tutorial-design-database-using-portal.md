---
title: "第一個 Azure 資料庫的 MySQL 資料庫-Azure 入口網站的 aaaDesign |Microsoft 文件"
description: "本教學課程說明如何 toocreate 和管理 MySQL 伺服器的 Azure 資料庫，以及使用 Azure 入口網站的資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="dfe85-103">設計您第一個適用於 MySQL 資料庫的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="dfe85-104">Azure MySQL 資料庫是受管理的服務，可讓您 toorun、 管理及調整 hello 雲端中的高可用性 MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfe85-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="dfe85-105">使用 hello Azure 入口網站，可以輕鬆地管理您的伺服器及設計資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfe85-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="dfe85-106">在此教學課程中，您可以使用 hello Azure 入口網站 toolearn 如何以：</span><span class="sxs-lookup"><span data-stu-id="dfe85-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dfe85-107">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="dfe85-108">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="dfe85-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="dfe85-109">使用 mysql 命令列工具 toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="dfe85-110">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-110">Load sample data</span></span>
> * <span data-ttu-id="dfe85-111">查詢資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-111">Query data</span></span>
> * <span data-ttu-id="dfe85-112">更新資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-112">Update data</span></span>
> * <span data-ttu-id="dfe85-113">還原資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="dfe85-114">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dfe85-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="dfe85-115">開啟我的最愛網頁瀏覽器，並造訪 hello [Microsoft Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="dfe85-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="dfe85-116">輸入認證 toosign toohello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="dfe85-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="dfe85-117">hello 預設檢視是服務儀表板。</span><span class="sxs-lookup"><span data-stu-id="dfe85-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="dfe85-118">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="dfe85-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="dfe85-119">建立的「適用於 MySQL 的 Azure 資料庫」伺服器會有一組已定義的[計算和儲存體](./concepts-compute-unit-and-storage.md)資源。</span><span class="sxs-lookup"><span data-stu-id="dfe85-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="dfe85-120">hello 伺服器內建立[Azure 資源群組](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)。</span><span class="sxs-lookup"><span data-stu-id="dfe85-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="dfe85-121">瀏覽過**資料庫** > **Azure 資料庫的 MySQL**。</span><span class="sxs-lookup"><span data-stu-id="dfe85-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="dfe85-122">如果找不到 MySQL Server 底下**資料庫**分類中，按一下 **查看所有**tooshow 所有可用的資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="dfe85-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="dfe85-123">您也可以輸入**Azure 資料庫的 MySQL**在 hello 搜尋方塊 tooquickly 尋找 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="dfe85-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="dfe85-124">![2-1 瀏覽 tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="dfe85-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="dfe85-125">按一下 Azure Database for MySQL 圖格，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="dfe85-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="dfe85-126">在本例中，填寫 hello Azure 資料庫的 MySQL 表單以 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="dfe85-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="dfe85-127">**設定**</span><span class="sxs-lookup"><span data-stu-id="dfe85-127">**Setting**</span></span> | <span data-ttu-id="dfe85-128">**建議的值**</span><span class="sxs-lookup"><span data-stu-id="dfe85-128">**Suggested value**</span></span> | <span data-ttu-id="dfe85-129">**欄位描述**</span><span class="sxs-lookup"><span data-stu-id="dfe85-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="dfe85-130">*伺服器名稱*</span><span class="sxs-lookup"><span data-stu-id="dfe85-130">*Server name*</span></span> | <span data-ttu-id="dfe85-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="dfe85-131">myserver4demo</span></span>  | <span data-ttu-id="dfe85-132">伺服器名稱的全域唯一 toobe。</span><span class="sxs-lookup"><span data-stu-id="dfe85-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="dfe85-133">*訂用帳戶*</span><span class="sxs-lookup"><span data-stu-id="dfe85-133">*Subscription*</span></span> | <span data-ttu-id="dfe85-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="dfe85-134">mysubscription</span></span> | <span data-ttu-id="dfe85-135">從 hello 下拉式清單中選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="dfe85-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="dfe85-136">*資源群組*</span><span class="sxs-lookup"><span data-stu-id="dfe85-136">*Resource group*</span></span> | <span data-ttu-id="dfe85-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="dfe85-137">myresourcegroup</span></span> | <span data-ttu-id="dfe85-138">建立資源群組或使用現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dfe85-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="dfe85-139">*伺服器管理員登入*</span><span class="sxs-lookup"><span data-stu-id="dfe85-139">*Server admin login*</span></span> | <span data-ttu-id="dfe85-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="dfe85-140">myadmin</span></span> | <span data-ttu-id="dfe85-141">設定管理帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="dfe85-141">Setup admin account name.</span></span> |
| <span data-ttu-id="dfe85-142">*密碼*</span><span class="sxs-lookup"><span data-stu-id="dfe85-142">*Password*</span></span> |  | <span data-ttu-id="dfe85-143">設定強式管理帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="dfe85-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="dfe85-144">*確認密碼*</span><span class="sxs-lookup"><span data-stu-id="dfe85-144">*Confirm password*</span></span> |  | <span data-ttu-id="dfe85-145">確認 hello 管理帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="dfe85-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="dfe85-146">*位置*</span><span class="sxs-lookup"><span data-stu-id="dfe85-146">*Location*</span></span> |  | <span data-ttu-id="dfe85-147">選取可用的區域。</span><span class="sxs-lookup"><span data-stu-id="dfe85-147">Select an available region.</span></span> |
| <span data-ttu-id="dfe85-148">*版本*</span><span class="sxs-lookup"><span data-stu-id="dfe85-148">*Version*</span></span> | <span data-ttu-id="dfe85-149">5.7</span><span class="sxs-lookup"><span data-stu-id="dfe85-149">5.7</span></span> | <span data-ttu-id="dfe85-150">選擇 hello 最新版本。</span><span class="sxs-lookup"><span data-stu-id="dfe85-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="dfe85-151">*設定效能*</span><span class="sxs-lookup"><span data-stu-id="dfe85-151">*Configure performance*</span></span> | <span data-ttu-id="dfe85-152">基本、50 個計算單位、50 GB</span><span class="sxs-lookup"><span data-stu-id="dfe85-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="dfe85-153">選擇 **[定價層]** 、 **[計算單位]** 、**[儲存體]** \(GB) ，然後按一下 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="dfe85-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="dfe85-154">*Pin tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="dfe85-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="dfe85-155">勾選</span><span class="sxs-lookup"><span data-stu-id="dfe85-155">Check</span></span> | <span data-ttu-id="dfe85-156">建議 toocheck 此方塊，讓您輕鬆地更新版本上可能會發現 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="dfe85-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="dfe85-157">然後按一下 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="dfe85-157">Then, click **Create**.</span></span> <span data-ttu-id="dfe85-158">在一兩分鐘，新的 Azure 資料庫的 MySQL 伺服器 hello 雲端中執行。</span><span class="sxs-lookup"><span data-stu-id="dfe85-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="dfe85-159">您可以按一下**通知**hello 工具列 toomonitor hello 部署程序上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dfe85-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="dfe85-160">設定防火牆</span><span class="sxs-lookup"><span data-stu-id="dfe85-160">Configure firewall</span></span>
<span data-ttu-id="dfe85-161">「適用於 MySQL 的 Azure 資料庫」會受到防火牆保護。</span><span class="sxs-lookup"><span data-stu-id="dfe85-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="dfe85-162">根據預設，將會拒絕所有連線 toohello 伺服器和 hello 資料庫 hello 伺服器內。</span><span class="sxs-lookup"><span data-stu-id="dfe85-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="dfe85-163">連接 tooAzure 資料庫的 MySQL hello 第一次之前，先設定 hello 防火牆 tooadd hello 用戶端機器的公用網路的 IP 位址 （或 IP 位址範圍）。</span><span class="sxs-lookup"><span data-stu-id="dfe85-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="dfe85-164">按一下您新建立的伺服器，然後按一下連線安全性。</span><span class="sxs-lookup"><span data-stu-id="dfe85-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="dfe85-165">![3-1 連線安全性](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="dfe85-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="dfe85-166">您可以在這裡 [新增我的 IP]，或設定防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="dfe85-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="dfe85-167">請記住 tooclick**儲存**建立 hello 規則之後。</span><span class="sxs-lookup"><span data-stu-id="dfe85-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="dfe85-168">您現在可以連接 toohello 伺服器使用 mysql 命令列工具或 MySQL Workbench GUI 工具。</span><span class="sxs-lookup"><span data-stu-id="dfe85-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="dfe85-169">「適用於 MySQL 的 Azure 資料庫」伺服器會透過連接埠 3306 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="dfe85-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="dfe85-170">如果您嘗試 tooconnect 從公司網路內，透過連接埠 3306 輸出流量可能不允許您的網路防火牆。</span><span class="sxs-lookup"><span data-stu-id="dfe85-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="dfe85-171">如果是這樣，您無法連接 tooAzure MySQL 伺服器，除非您的 IT 部門會開啟連接埠 3306。</span><span class="sxs-lookup"><span data-stu-id="dfe85-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="dfe85-172">取得連線資訊</span><span class="sxs-lookup"><span data-stu-id="dfe85-172">Get connection information</span></span>
<span data-ttu-id="dfe85-173">完整的 get hello**伺服器名稱**和**伺服器系統管理員登入名稱**MySQL 伺服器 hello Azure 入口網站從 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfe85-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="dfe85-174">您使用 hello 完整的伺服器名稱 tooconnect tooyour 伺服器使用 mysql 命令列工具。</span><span class="sxs-lookup"><span data-stu-id="dfe85-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="dfe85-175">在[Azure 入口網站](https://portal.azure.com/)，按一下 [**所有資源**從 hello 左側]、 類型 hello 名稱，並搜尋您的 Azure 資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="dfe85-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="dfe85-176">選取 hello 伺服器名稱 tooview hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="dfe85-177">在 hello 設定下標題之下，按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="dfe85-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="dfe85-178">記下 [伺服器名稱] 和 [伺服器管理員登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="dfe85-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="dfe85-179">您可以按一下 hello 複製按鈕下一步 tooeach 欄位 toocopy toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="dfe85-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="dfe85-180">![4-2 伺服器屬性](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="dfe85-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="dfe85-181">在此範例中，hello 伺服器名稱是*myserver4demo.mysql.database.azure.com*，hello server 系統管理員登入，且 *myadmin@myserver4demo* 。</span><span class="sxs-lookup"><span data-stu-id="dfe85-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="dfe85-182">使用 mysql toohello 伺服器連接</span><span class="sxs-lookup"><span data-stu-id="dfe85-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="dfe85-183">使用[mysql 命令列工具](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)tooestablish MySQL 伺服器的連線 tooyour Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfe85-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="dfe85-184">您可以執行 hello mysql 命令列工具，從 hello 瀏覽器中的 hello Azure 雲端殼層或您自己的電腦在本機使用已安裝的 mysql 工具。</span><span class="sxs-lookup"><span data-stu-id="dfe85-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="dfe85-185">toolaunch hello Azure 雲端 Shell 中，按一下 hello`Try It`工具列上的程式碼區塊，在本文中，或請造訪 hello Azure 入口網站，然後按一下 hello `>_` hello 頂端工具列右側的圖示。</span><span class="sxs-lookup"><span data-stu-id="dfe85-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="dfe85-186">輸入 hello 命令 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="dfe85-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="dfe85-187">建立空白資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-187">Create a blank database</span></span>
<span data-ttu-id="dfe85-188">一旦您已連線的 toohello 伺服器，建立具有空白資料庫 toowork。</span><span class="sxs-lookup"><span data-stu-id="dfe85-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="dfe85-189">在 hello 提示字元中執行下列命令 tooswitch 連線 toothis 新建資料庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="dfe85-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="dfe85-190">Hello 資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="dfe85-190">Create tables in hello database</span></span>
<span data-ttu-id="dfe85-191">您現在知道如何 tooconnect toohello Azure 資料庫的 MySQL 資料庫，我們可能會超出如何 toocomplete 某些基本工作。</span><span class="sxs-lookup"><span data-stu-id="dfe85-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="dfe85-192">首先，我們可以建立資料表並在其中載入一些資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="dfe85-193">我們將建立一個儲存清查資訊的資料表。</span><span class="sxs-lookup"><span data-stu-id="dfe85-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="dfe85-194">資料載入至 hello 資料表</span><span class="sxs-lookup"><span data-stu-id="dfe85-194">Load data into hello tables</span></span>
<span data-ttu-id="dfe85-195">既然我們已有資料表，我們可以在其中插入一些資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="dfe85-196">在 hello 開啟命令提示字元視窗中，請執行下列查詢 tooinsert hello 某些資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="dfe85-197">現在您有兩個資料列範例資料插入 hello 您稍早建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="dfe85-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="dfe85-198">查詢和更新 hello 資料表中的 hello 資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="dfe85-199">執行 hello hello 資料庫資料表中的下列查詢 tooretrieve 資訊。</span><span class="sxs-lookup"><span data-stu-id="dfe85-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="dfe85-200">您也可以更新 hello hello 資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="dfe85-201">當您擷取資料時，取得據以更新 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="dfe85-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="dfe85-202">還原資料庫 tooa 前一個點的時間</span><span class="sxs-lookup"><span data-stu-id="dfe85-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="dfe85-203">想像您不小心刪除重要的資料庫資料表，並無法輕易復原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="dfe85-204">Azure 的 MySQL 資料庫可讓您 toorestore hello 伺服器 tooa 點的時間，建立新的伺服器一個 hello 資料庫的副本。</span><span class="sxs-lookup"><span data-stu-id="dfe85-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="dfe85-205">您可以使用這個新的伺服器 toorecover 刪除的資料。</span><span class="sxs-lookup"><span data-stu-id="dfe85-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="dfe85-206">hello 加入 hello 資料表之前，請遵循步驟還原 hello 範例伺服器 tooa 點。</span><span class="sxs-lookup"><span data-stu-id="dfe85-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="dfe85-207">在 hello Azure 入口網站，找出用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="dfe85-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="dfe85-208">在 hello**概觀**頁面上，按一下**還原**hello 工具列上。</span><span class="sxs-lookup"><span data-stu-id="dfe85-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="dfe85-209">hello 還原頁面隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="dfe85-209">hello Restore page opens.</span></span>

   ![10-1 還原資料庫](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="dfe85-211">填寫 hello**還原**hello 所需資訊的表單。</span><span class="sxs-lookup"><span data-stu-id="dfe85-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 還原表單](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="dfe85-213">**還原點**： 選取的時間點想 toorestore，列出的 hello 時間範圍內。</span><span class="sxs-lookup"><span data-stu-id="dfe85-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="dfe85-214">請確定 tooconvert 本地時區 tooUTC。</span><span class="sxs-lookup"><span data-stu-id="dfe85-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="dfe85-215">**還原 toonew 伺服器**： 提供新的伺服器名稱，您想要 toorestore。</span><span class="sxs-lookup"><span data-stu-id="dfe85-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="dfe85-216">**位置**: hello 區域與 hello 來源伺服器相同，且無法變更。</span><span class="sxs-lookup"><span data-stu-id="dfe85-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="dfe85-217">**定價層**: hello 定價層為的 hello hello 與相同來源伺服器，而且無法變更。</span><span class="sxs-lookup"><span data-stu-id="dfe85-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="dfe85-218">按一下**確定**toorestore hello 伺服器太[還原時間點 tooa](./howto-restore-server-portal.md) hello 資料表已刪除之前。</span><span class="sxs-lookup"><span data-stu-id="dfe85-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="dfe85-219">還原伺服器建立一個新的 hello server，位於 hello 您指定的時間點複本。</span><span class="sxs-lookup"><span data-stu-id="dfe85-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="dfe85-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfe85-220">Next steps</span></span>
<span data-ttu-id="dfe85-221">在此教學課程中，您可以使用 hello Azure 入口網站 toolearned 如何以：</span><span class="sxs-lookup"><span data-stu-id="dfe85-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dfe85-222">建立適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="dfe85-223">Hello 伺服器防火牆設定</span><span class="sxs-lookup"><span data-stu-id="dfe85-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="dfe85-224">使用 mysql 命令列工具 toocreate 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="dfe85-225">載入範例資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-225">Load sample data</span></span>
> * <span data-ttu-id="dfe85-226">查詢資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-226">Query data</span></span>
> * <span data-ttu-id="dfe85-227">更新資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-227">Update data</span></span>
> * <span data-ttu-id="dfe85-228">還原資料</span><span class="sxs-lookup"><span data-stu-id="dfe85-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dfe85-229">Tooconnect 應用程式 tooAzure 如何針對 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="dfe85-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
