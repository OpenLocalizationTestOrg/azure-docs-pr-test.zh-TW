---
title: "設定 Linux VM 上的 PostgreSQL | Microsoft Docs"
description: "了解如何在 Azure 中的 Linux 虛擬機器上安裝和設定 PostgreSQL"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 0bccdc1cfdbda06b57da8cd662373ef137768672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="eab01-103">安裝和設定 Azure 上的 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eab01-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="eab01-104">PostgreSQL 是與 Oracle 和 DB2 類似的進階開放原始碼資料庫。</span><span class="sxs-lookup"><span data-stu-id="eab01-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span></span> <span data-ttu-id="eab01-105">它包含企業用功能，例如完整的 ACID 的相容性、可靠的交易式程序，以及多版本的並行控制。</span><span class="sxs-lookup"><span data-stu-id="eab01-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="eab01-106">它也支援標準，例如 ANSI SQL 和 SQL/MED (包括 Oracle、MySQL、MongoDB 和許多其他項目的外部資料包裝函式)。</span><span class="sxs-lookup"><span data-stu-id="eab01-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="eab01-107">其高度可擴充性支援超過 12 種程序性語言、GIN 和 GiST 索引、空間資料支援和多個類似 NoSQL 的功能，適用於 JSON 或以索引鍵-值為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eab01-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="eab01-108">在本文中，您將學習如何在執行 Linux 的 Azure 虛擬機器上安裝和設定 PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="eab01-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="eab01-109">安裝 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eab01-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="eab01-110">您必須已經具有執行 Linux 的 Azure 虛擬機器，才能完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="eab01-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="eab01-111">若要建立並設定 Linux VM 再繼續進行，請參閱 [Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="eab01-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="eab01-112">在此情況下，使用連接埠 1999 做為 PostgreSQL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="eab01-112">In this case, use port 1999 as the PostgreSQL port.</span></span>  

<span data-ttu-id="eab01-113">連接到您透過 PuTTY 建立的 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="eab01-113">Connect to the Linux VM you created via PuTTY.</span></span> <span data-ttu-id="eab01-114">如果這是您第一次使用 Azure Linux VM，請參閱[如何搭配 Azure 上的 Linux 使用 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 以了解如何使用 PuTTY 來連接到 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="eab01-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span></span>

1. <span data-ttu-id="eab01-115">執行下列命令來切換至 root (admin)：</span><span class="sxs-lookup"><span data-stu-id="eab01-115">Run the following command to switch to the root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="eab01-116">某些散發套件有相依性，您必須先安裝這些相依性再安裝 PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="eab01-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="eab01-117">檢查此清單中的 distro 並執行適當的命令：</span><span class="sxs-lookup"><span data-stu-id="eab01-117">Check for your distro in this list and run the appropriate command:</span></span>
   
   * <span data-ttu-id="eab01-118">Red Hat 基底 Linux：</span><span class="sxs-lookup"><span data-stu-id="eab01-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="eab01-119">Debian 基底 Linux：</span><span class="sxs-lookup"><span data-stu-id="eab01-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="eab01-120">SUSE Linux：</span><span class="sxs-lookup"><span data-stu-id="eab01-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="eab01-121">下載 PostgreSQL 到根目錄，接著將封裝解壓縮：</span><span class="sxs-lookup"><span data-stu-id="eab01-121">Download PostgreSQL into the root directory, and then unzip the package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="eab01-122">以上是範例。</span><span class="sxs-lookup"><span data-stu-id="eab01-122">The above is an example.</span></span> <span data-ttu-id="eab01-123">您可以在 [Index of /pub/source/](https://ftp.postgresql.org/pub/source/)中找到更詳細的下載位址。</span><span class="sxs-lookup"><span data-stu-id="eab01-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="eab01-124">若要啟動組建，請執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="eab01-124">To start the build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="eab01-125">如果您想要建置所有可以建置的項目 (包括文件 (HTML 和 man 頁面) 和其他模組 (contrib))，請改為執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="eab01-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="eab01-126">您會收到下列確認訊息：</span><span class="sxs-lookup"><span data-stu-id="eab01-126">You should receive the following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready to install.

## <a name="configure-postgresql"></a><span data-ttu-id="eab01-127">設定 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eab01-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="eab01-128">(選擇性) 建立符號連結來縮短 PostgreSQL 參考，使其不包含版本號碼：</span><span class="sxs-lookup"><span data-stu-id="eab01-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="eab01-129">建立資料庫的目錄：</span><span class="sxs-lookup"><span data-stu-id="eab01-129">Create a directory for the database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="eab01-130">建立非根使用者，並修改該使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="eab01-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="eab01-131">然後切換到這個新的使用者 (在我們的範例中稱為 *postgres* )：</span><span class="sxs-lookup"><span data-stu-id="eab01-131">Then, switch to this new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="eab01-132">基於安全性理由，PostgreSQL 會使用非根使用者初始化、啟動或關閉資料庫。</span><span class="sxs-lookup"><span data-stu-id="eab01-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span></span>
   > 
   > 
4. <span data-ttu-id="eab01-133">輸入下列命令以編輯 bash_profile 檔。</span><span class="sxs-lookup"><span data-stu-id="eab01-133">Edit the *bash_profile* file by entering the commands below.</span></span> <span data-ttu-id="eab01-134">這幾行將會加入至 bash_profile 檔案的結尾：</span><span class="sxs-lookup"><span data-stu-id="eab01-134">These lines will be added to the end of the *bash_profile* file:</span></span>
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. <span data-ttu-id="eab01-135">執行 bash_profile 檔案：</span><span class="sxs-lookup"><span data-stu-id="eab01-135">Execute the *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="eab01-136">利用下列命令驗證安裝：</span><span class="sxs-lookup"><span data-stu-id="eab01-136">Validate your installation by using the following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="eab01-137">如果您成功安裝，您將會看見下列回應：</span><span class="sxs-lookup"><span data-stu-id="eab01-137">If your installation is successful, you will see the following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="eab01-138">您也可以檢查 PostgreSQL 版本：</span><span class="sxs-lookup"><span data-stu-id="eab01-138">You can also check the PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="eab01-139">初始化資料庫：</span><span class="sxs-lookup"><span data-stu-id="eab01-139">Initialize the database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="eab01-140">您應該會收到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="eab01-140">You should receive the following output:</span></span>

![image](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="eab01-142">設定 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="eab01-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="eab01-143">執行以下命令：</span><span class="sxs-lookup"><span data-stu-id="eab01-143">Run the following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="eab01-144">修改 /etc/init.d/postgresql 檔案中的兩個變數。</span><span class="sxs-lookup"><span data-stu-id="eab01-144">Modify two variables in the /etc/init.d/postgresql file.</span></span> <span data-ttu-id="eab01-145">前置詞設為 PostgreSQL 的安裝路徑： **/opt/pgsql**。</span><span class="sxs-lookup"><span data-stu-id="eab01-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="eab01-146">PGDATA 設為 PostgreSQL 的資料儲存路徑：**/opt/pgsql_data**。</span><span class="sxs-lookup"><span data-stu-id="eab01-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](./media/postgresql-install/no2.png)

<span data-ttu-id="eab01-148">變更檔案，使其可執行：</span><span class="sxs-lookup"><span data-stu-id="eab01-148">Change the file to make it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="eab01-149">啟動 PostgreSQL：</span><span class="sxs-lookup"><span data-stu-id="eab01-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="eab01-150">查看 PostgreSQL 端點是否位於：</span><span class="sxs-lookup"><span data-stu-id="eab01-150">Check if the endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="eab01-151">您應該會看見下列輸出：</span><span class="sxs-lookup"><span data-stu-id="eab01-151">You should see the following output:</span></span>

![image](./media/postgresql-install/no3.png)

## <a name="connect-to-the-postgres-database"></a><span data-ttu-id="eab01-153">連接到 Postgres 資料庫</span><span class="sxs-lookup"><span data-stu-id="eab01-153">Connect to the Postgres database</span></span>
<span data-ttu-id="eab01-154">再一次切換到 postgres 使用者：</span><span class="sxs-lookup"><span data-stu-id="eab01-154">Switch to the postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="eab01-155">建立 Postgres 資料庫：</span><span class="sxs-lookup"><span data-stu-id="eab01-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="eab01-156">連接到您剛建立的事件資料庫：</span><span class="sxs-lookup"><span data-stu-id="eab01-156">Connect to the events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="eab01-157">建立和刪除 Postgres 資料表</span><span class="sxs-lookup"><span data-stu-id="eab01-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="eab01-158">既然您已經連接到資料庫，可以在其中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="eab01-158">Now that you have connected to the database, you can create tables in it.</span></span>

<span data-ttu-id="eab01-159">例如，利用下列命令建立新的範例 Postgres 資料表：</span><span class="sxs-lookup"><span data-stu-id="eab01-159">For example, create a new example Postgres table by using the following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="eab01-160">您現在已經利用下列資料行名稱和限制設定了 4 個資料行的資料表：</span><span class="sxs-lookup"><span data-stu-id="eab01-160">You have now set up a four-column table with the following column names and restrictions:</span></span>

1. <span data-ttu-id="eab01-161">“name” 資料行已經由 VARCHAR 命令限制在 20 個字元以下。</span><span class="sxs-lookup"><span data-stu-id="eab01-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span></span>
2. <span data-ttu-id="eab01-162">"Food" 資料行指出每個人將會攜帶的食物項目。</span><span class="sxs-lookup"><span data-stu-id="eab01-162">The “food” column indicates the food item that each person will bring.</span></span> <span data-ttu-id="eab01-163">VARCHAR 將此文字限制在 30 個字元以下。</span><span class="sxs-lookup"><span data-stu-id="eab01-163">VARCHAR limits this text to be under 30 characters.</span></span>
3. <span data-ttu-id="eab01-164">“confirmed” 資料行記錄該人員是否具有聚會的 RSVP'd。</span><span class="sxs-lookup"><span data-stu-id="eab01-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span></span> <span data-ttu-id="eab01-165">可接受的值為 "Y" 和 "N"。</span><span class="sxs-lookup"><span data-stu-id="eab01-165">The acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="eab01-166">“date” 資料行顯示他們註冊此事件的時間。</span><span class="sxs-lookup"><span data-stu-id="eab01-166">The “date” column shows when they signed up for the event.</span></span> <span data-ttu-id="eab01-167">Postgres 的必要日期格式為 yyyy-mm-dd。</span><span class="sxs-lookup"><span data-stu-id="eab01-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="eab01-168">如果您成功建立資料表，您會看到下列內容：</span><span class="sxs-lookup"><span data-stu-id="eab01-168">You should see the following if your table has been successfully created:</span></span>

![image](./media/postgresql-install/no4.png)

<span data-ttu-id="eab01-170">您也可以利用下列命令檢查資料表結構：</span><span class="sxs-lookup"><span data-stu-id="eab01-170">You can also check the table structure by using the following command:</span></span>

![image](./media/postgresql-install/no5.png)

### <a name="add-data-to-a-table"></a><span data-ttu-id="eab01-172">將資料新增至資料表</span><span class="sxs-lookup"><span data-stu-id="eab01-172">Add data to a table</span></span>
<span data-ttu-id="eab01-173">首先，將資料插入資料列：</span><span class="sxs-lookup"><span data-stu-id="eab01-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="eab01-174">您應該會看見此輸出：</span><span class="sxs-lookup"><span data-stu-id="eab01-174">You should see this output:</span></span>

![image](./media/postgresql-install/no6.png)

<span data-ttu-id="eab01-176">您也可以將更多人員新增至資料表。</span><span class="sxs-lookup"><span data-stu-id="eab01-176">You can add a couple more people to the table as well.</span></span> <span data-ttu-id="eab01-177">以下是一些選項，或者您可以建立自己的選項：</span><span class="sxs-lookup"><span data-stu-id="eab01-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="eab01-178">顯示資料表</span><span class="sxs-lookup"><span data-stu-id="eab01-178">Show tables</span></span>
<span data-ttu-id="eab01-179">使用下列命令來顯示資料表：</span><span class="sxs-lookup"><span data-stu-id="eab01-179">Use the following command to show a table:</span></span>

    select * from potluck;

<span data-ttu-id="eab01-180">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="eab01-180">The output is:</span></span>

![image](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="eab01-182">刪除資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="eab01-182">Delete data in a table</span></span>
<span data-ttu-id="eab01-183">使用下列命令刪除資料表中的資料：</span><span class="sxs-lookup"><span data-stu-id="eab01-183">Use the following command to delete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="eab01-184">這會刪除 "John" 資料列中的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="eab01-184">This deletes all the information in the "John" row.</span></span> <span data-ttu-id="eab01-185">輸出如下：</span><span class="sxs-lookup"><span data-stu-id="eab01-185">The output is:</span></span>

![image](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="eab01-187">更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="eab01-187">Update data in a table</span></span>
<span data-ttu-id="eab01-188">使用下列命令更新資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="eab01-188">Use the following command to update data in a table.</span></span> <span data-ttu-id="eab01-189">對於此項目，Sandy 已確認她會參加，所以我們要將她的 RSVP 從 "N" 變更為 "Y"：</span><span class="sxs-lookup"><span data-stu-id="eab01-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="eab01-190">取得 PostgreSQL 的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="eab01-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="eab01-191">既然您已完成在 Azure Linux VM 中的 PostgreSQL 安裝，您可以在 Azure 中享用它。</span><span class="sxs-lookup"><span data-stu-id="eab01-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="eab01-192">若要深入了解 PostgreSQL，請造訪 [PostgreSQL 網站](http://www.postgresql.org/)。</span><span class="sxs-lookup"><span data-stu-id="eab01-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span></span>

