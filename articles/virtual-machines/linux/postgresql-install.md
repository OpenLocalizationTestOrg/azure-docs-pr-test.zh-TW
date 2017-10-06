---
title: "Linux VM 上 PostgreSQL 向上 aaaSet |Microsoft 文件"
description: "深入了解如何 tooinstall 和在 Azure 中 Linux 虛擬機器上設定 PostgreSQL"
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
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="4bad6-103">安裝和設定 Azure 上的 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4bad6-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="4bad6-104">PostgreSQL 是進階的開放原始碼資料庫類似 tooOracle 和 DB2。</span><span class="sxs-lookup"><span data-stu-id="4bad6-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="4bad6-105">它包含企業用功能，例如完整的 ACID 的相容性、可靠的交易式程序，以及多版本的並行控制。</span><span class="sxs-lookup"><span data-stu-id="4bad6-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="4bad6-106">它也支援標準，例如 ANSI SQL 和 SQL/MED (包括 Oracle、MySQL、MongoDB 和許多其他項目的外部資料包裝函式)。</span><span class="sxs-lookup"><span data-stu-id="4bad6-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="4bad6-107">其高度可擴充性支援超過 12 種程序性語言、GIN 和 GiST 索引、空間資料支援和多個類似 NoSQL 的功能，適用於 JSON 或以索引鍵-值為基礎的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bad6-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="4bad6-108">在本文中，您將學習如何 tooinstall 上及設定 PostgreSQL 執行 Linux 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4bad6-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="4bad6-109">安裝 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4bad6-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="4bad6-110">您必須已經順序 toocomplete 在本教學課程執行 Linux 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4bad6-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="4bad6-111">toocreate 及設定 Linux VM 之前，請參閱[Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4bad6-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="4bad6-112">在此情況下，使用連接埠 1999年作為 hello PostgreSQL 連接埠。</span><span class="sxs-lookup"><span data-stu-id="4bad6-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="4bad6-113">連接 toohello Linux VM 建立透過 putty 連線。</span><span class="sxs-lookup"><span data-stu-id="4bad6-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="4bad6-114">如果這是 hello 第一次您使用 Azure Linux VM，請參閱[如何 tooUse 與 Azure 上的 Linux SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn toouse 如何 PuTTY tooconnect tooa Linux VM。</span><span class="sxs-lookup"><span data-stu-id="4bad6-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="4bad6-115">執行下列命令 tooswitch toohello 根 （系統管理員） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="4bad6-116">某些散發套件有相依性，您必須先安裝這些相依性再安裝 PostgreSQL。</span><span class="sxs-lookup"><span data-stu-id="4bad6-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="4bad6-117">檢查您 distro 這份清單中，並執行 hello 適當的命令：</span><span class="sxs-lookup"><span data-stu-id="4bad6-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="4bad6-118">Red Hat 基底 Linux：</span><span class="sxs-lookup"><span data-stu-id="4bad6-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="4bad6-119">Debian 基底 Linux：</span><span class="sxs-lookup"><span data-stu-id="4bad6-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="4bad6-120">SUSE Linux：</span><span class="sxs-lookup"><span data-stu-id="4bad6-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="4bad6-121">下載 PostgreSQL 到 hello 根目錄，並再解壓縮 hello 封裝：</span><span class="sxs-lookup"><span data-stu-id="4bad6-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="4bad6-122">hello 上述是範例。</span><span class="sxs-lookup"><span data-stu-id="4bad6-122">hello above is an example.</span></span> <span data-ttu-id="4bad6-123">您可以找到 hello 更多詳細的下載中 hello 位址[索引/pub/來源/](https://ftp.postgresql.org/pub/source/)。</span><span class="sxs-lookup"><span data-stu-id="4bad6-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="4bad6-124">toostart hello 建置，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="4bad6-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="4bad6-125">如果您想 toobuild 所有項目可以建置，包括 hello 文件集 （HTML 和 man 頁面） 和其他模組 (contrib)，執行下列命令，而是 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="4bad6-126">您應該會收到下列確認訊息的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="4bad6-127">設定 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4bad6-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="4bad6-128">（選擇性）建立符號連結 tooshorten hello PostgreSQL 參考 toonot 包含 hello 版本號碼：</span><span class="sxs-lookup"><span data-stu-id="4bad6-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="4bad6-129">建立 hello 資料庫的目錄：</span><span class="sxs-lookup"><span data-stu-id="4bad6-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="4bad6-130">建立非根使用者，並修改該使用者的設定檔。</span><span class="sxs-lookup"><span data-stu-id="4bad6-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="4bad6-131">然後，切換 toothis 新使用者 (稱為*postgres*在我們的範例):</span><span class="sxs-lookup"><span data-stu-id="4bad6-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="4bad6-132">基於安全性理由，請 PostgreSQL 使用非根使用者 tooinitialize、 啟動或關閉 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4bad6-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="4bad6-133">編輯 hello *bash_profile*輸入下列 hello 命令的檔案。</span><span class="sxs-lookup"><span data-stu-id="4bad6-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="4bad6-134">這些線條將會加入 toohello 結尾 hello *bash_profile*檔案：</span><span class="sxs-lookup"><span data-stu-id="4bad6-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="4bad6-135">執行 hello *bash_profile*檔案：</span><span class="sxs-lookup"><span data-stu-id="4bad6-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="4bad6-136">使用下列命令的 hello，以驗證您的安裝：</span><span class="sxs-lookup"><span data-stu-id="4bad6-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="4bad6-137">如果您的安裝成功，您會看到下列回應 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="4bad6-138">您也可以檢查 hello PostgreSQL 版本：</span><span class="sxs-lookup"><span data-stu-id="4bad6-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="4bad6-139">初始化 hello 資料庫：</span><span class="sxs-lookup"><span data-stu-id="4bad6-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="4bad6-140">您應該會收到 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="4bad6-140">You should receive hello following output:</span></span>

![image](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="4bad6-142">設定 PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4bad6-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="4bad6-143">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="4bad6-144">修改 hello /etc/init.d/postgresql 檔案中的兩個變數。</span><span class="sxs-lookup"><span data-stu-id="4bad6-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="4bad6-145">hello 前置詞設定 PostgreSQL toohello 安裝路徑： **/opt/microsoft pgsql**。</span><span class="sxs-lookup"><span data-stu-id="4bad6-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="4bad6-146">PGDATA 設定 PostgreSQL toohello 資料儲存體路徑： **/opt/microsoft pgsql_data**。</span><span class="sxs-lookup"><span data-stu-id="4bad6-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](./media/postgresql-install/no2.png)

<span data-ttu-id="4bad6-148">變更 hello 檔案 toomake 它可執行檔：</span><span class="sxs-lookup"><span data-stu-id="4bad6-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="4bad6-149">啟動 PostgreSQL：</span><span class="sxs-lookup"><span data-stu-id="4bad6-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="4bad6-150">檢查 PostgreSQL hello 端點是否上：</span><span class="sxs-lookup"><span data-stu-id="4bad6-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="4bad6-151">您應該會看到下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-151">You should see hello following output:</span></span>

![image](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="4bad6-153">連接 toohello Postgres 資料庫</span><span class="sxs-lookup"><span data-stu-id="4bad6-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="4bad6-154">同樣地切換 toohello postgres 使用者：</span><span class="sxs-lookup"><span data-stu-id="4bad6-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="4bad6-155">建立 Postgres 資料庫：</span><span class="sxs-lookup"><span data-stu-id="4bad6-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="4bad6-156">連接您剛才建立的 toohello 事件資料庫：</span><span class="sxs-lookup"><span data-stu-id="4bad6-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="4bad6-157">建立和刪除 Postgres 資料表</span><span class="sxs-lookup"><span data-stu-id="4bad6-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="4bad6-158">既然您已經連接 toohello 資料庫，您可以在其中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="4bad6-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="4bad6-159">例如，建立新的範例 Postgres 資料表使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="4bad6-160">您現在已設定四個資料行的資料表，以 hello 下列資料行名稱和限制：</span><span class="sxs-lookup"><span data-stu-id="4bad6-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="4bad6-161">hello"name"的資料行具有已受到 hello VARCHAR 命令 toobe 底下 20 個字元長時間。</span><span class="sxs-lookup"><span data-stu-id="4bad6-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="4bad6-162">hello"food"資料行指出 hello 食物項目，讓每個人。</span><span class="sxs-lookup"><span data-stu-id="4bad6-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="4bad6-163">VARCHAR 限制 30 個字元在這個文字 toobe。</span><span class="sxs-lookup"><span data-stu-id="4bad6-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="4bad6-164">hello 「 確認 」 資料行記錄是否 hello 人員 rsvp toohello 聚會的活動。</span><span class="sxs-lookup"><span data-stu-id="4bad6-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="4bad6-165">hello 可接受值為"Y"和"N"。</span><span class="sxs-lookup"><span data-stu-id="4bad6-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="4bad6-166">hello 「 日期 」 欄會顯示這些註冊 hello 事件時。</span><span class="sxs-lookup"><span data-stu-id="4bad6-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="4bad6-167">Postgres 的必要日期格式為 yyyy-mm-dd。</span><span class="sxs-lookup"><span data-stu-id="4bad6-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="4bad6-168">如果已成功建立您的資料表，您應該看到 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4bad6-168">You should see hello following if your table has been successfully created:</span></span>

![image](./media/postgresql-install/no4.png)

<span data-ttu-id="4bad6-170">您也可以使用下列命令的 hello 檢查 hello 資料表結構：</span><span class="sxs-lookup"><span data-stu-id="4bad6-170">You can also check hello table structure by using hello following command:</span></span>

![image](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="4bad6-172">加入資料 tooa 資料表</span><span class="sxs-lookup"><span data-stu-id="4bad6-172">Add data tooa table</span></span>
<span data-ttu-id="4bad6-173">首先，將資料插入資料列：</span><span class="sxs-lookup"><span data-stu-id="4bad6-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="4bad6-174">您應該會看見此輸出：</span><span class="sxs-lookup"><span data-stu-id="4bad6-174">You should see this output:</span></span>

![image](./media/postgresql-install/no6.png)

<span data-ttu-id="4bad6-176">您可以加入一些更多人 toohello 資料表以及。</span><span class="sxs-lookup"><span data-stu-id="4bad6-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="4bad6-177">以下是一些選項，或者您可以建立自己的選項：</span><span class="sxs-lookup"><span data-stu-id="4bad6-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="4bad6-178">顯示資料表</span><span class="sxs-lookup"><span data-stu-id="4bad6-178">Show tables</span></span>
<span data-ttu-id="4bad6-179">使用下列命令 tooshow 資料表 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="4bad6-180">hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="4bad6-180">hello output is:</span></span>

![image](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="4bad6-182">刪除資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="4bad6-182">Delete data in a table</span></span>
<span data-ttu-id="4bad6-183">使用下列命令 toodelete 資料在資料表中的 hello:</span><span class="sxs-lookup"><span data-stu-id="4bad6-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="4bad6-184">這會刪除 hello"John"的資料列中的所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="4bad6-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="4bad6-185">hello 輸出為：</span><span class="sxs-lookup"><span data-stu-id="4bad6-185">hello output is:</span></span>

![image](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="4bad6-187">更新資料表中的資料</span><span class="sxs-lookup"><span data-stu-id="4bad6-187">Update data in a table</span></span>
<span data-ttu-id="4bad6-188">使用下列命令 tooupdate 資料在資料表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="4bad6-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="4bad6-189">此一，Sandy 已確認，她出席，因此我們將變更從 「 N 」 她 RSVP 太"Y":</span><span class="sxs-lookup"><span data-stu-id="4bad6-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="4bad6-190">取得 PostgreSQL 的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4bad6-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="4bad6-191">既然您已完成的 PostgreSQL Azure Linux VM 中的 hello 安裝，您可以享用在 Azure 中使用它。</span><span class="sxs-lookup"><span data-stu-id="4bad6-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="4bad6-192">深入了解 PostgreSQL，toolearn 造訪 hello [PostgreSQL 網站](http://www.postgresql.org/)。</span><span class="sxs-lookup"><span data-stu-id="4bad6-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

