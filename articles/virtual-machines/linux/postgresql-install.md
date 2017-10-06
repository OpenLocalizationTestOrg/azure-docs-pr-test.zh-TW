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
# <a name="install-and-configure-postgresql-on-azure"></a>安裝和設定 Azure 上的 PostgreSQL
PostgreSQL 是進階的開放原始碼資料庫類似 tooOracle 和 DB2。 它包含企業用功能，例如完整的 ACID 的相容性、可靠的交易式程序，以及多版本的並行控制。 它也支援標準，例如 ANSI SQL 和 SQL/MED (包括 Oracle、MySQL、MongoDB 和許多其他項目的外部資料包裝函式)。 其高度可擴充性支援超過 12 種程序性語言、GIN 和 GiST 索引、空間資料支援和多個類似 NoSQL 的功能，適用於 JSON 或以索引鍵-值為基礎的應用程式。

在本文中，您將學習如何 tooinstall 上及設定 PostgreSQL 執行 Linux 的 Azure 虛擬機器。

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>安裝 PostgreSQL
> [!NOTE]
> 您必須已經順序 toocomplete 在本教學課程執行 Linux 的 Azure 虛擬機器。 toocreate 及設定 Linux VM 之前，請參閱[Azure Linux VM 教學課程](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。
> 
> 

在此情況下，使用連接埠 1999年作為 hello PostgreSQL 連接埠。  

連接 toohello Linux VM 建立透過 putty 連線。 如果這是 hello 第一次您使用 Azure Linux VM，請參閱[如何 tooUse 與 Azure 上的 Linux SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn toouse 如何 PuTTY tooconnect tooa Linux VM。

1. 執行下列命令 tooswitch toohello 根 （系統管理員） 的 hello:
   
        # sudo su -
2. 某些散發套件有相依性，您必須先安裝這些相依性再安裝 PostgreSQL。 檢查您 distro 這份清單中，並執行 hello 適當的命令：
   
   * Red Hat 基底 Linux：
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Debian 基底 Linux：
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux：
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. 下載 PostgreSQL 到 hello 根目錄，並再解壓縮 hello 封裝：
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    hello 上述是範例。 您可以找到 hello 更多詳細的下載中 hello 位址[索引/pub/來源/](https://ftp.postgresql.org/pub/source/)。
4. toostart hello 建置，執行下列命令：
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. 如果您想 toobuild 所有項目可以建置，包括 hello 文件集 （HTML 和 man 頁面） 和其他模組 (contrib)，執行下列命令，而是 hello:
   
        # gmake install-world
   
    您應該會收到下列確認訊息的 hello:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>設定 PostgreSQL
1. （選擇性）建立符號連結 tooshorten hello PostgreSQL 參考 toonot 包含 hello 版本號碼：
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. 建立 hello 資料庫的目錄：
   
        # mkdir -p /opt/pgsql_data
3. 建立非根使用者，並修改該使用者的設定檔。 然後，切換 toothis 新使用者 (稱為*postgres*在我們的範例):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > 基於安全性理由，請 PostgreSQL 使用非根使用者 tooinitialize、 啟動或關閉 hello 資料庫。
   > 
   > 
4. 編輯 hello *bash_profile*輸入下列 hello 命令的檔案。 這些線條將會加入 toohello 結尾 hello *bash_profile*檔案：
   
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
5. 執行 hello *bash_profile*檔案：
   
        $ source .bash_profile
6. 使用下列命令的 hello，以驗證您的安裝：
   
        $ which psql
   
    如果您的安裝成功，您會看到下列回應 hello:
   
        /opt/pgsql/bin/psql
7. 您也可以檢查 hello PostgreSQL 版本：
   
        $ psql -V
8. 初始化 hello 資料庫：
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    您應該會收到 hello 下列輸出：

![image](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>設定 PostgreSQL
<!--    [postgres@ test ~]$ exit -->

執行下列命令的 hello:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

修改 hello /etc/init.d/postgresql 檔案中的兩個變數。 hello 前置詞設定 PostgreSQL toohello 安裝路徑： **/opt/microsoft pgsql**。 PGDATA 設定 PostgreSQL toohello 資料儲存體路徑： **/opt/microsoft pgsql_data**。

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![image](./media/postgresql-install/no2.png)

變更 hello 檔案 toomake 它可執行檔：

    # chmod +x /etc/init.d/postgresql

啟動 PostgreSQL：

    # /etc/init.d/postgresql start

檢查 PostgreSQL hello 端點是否上：

    # netstat -tunlp|grep 1999

您應該會看到下列輸出的 hello:

![image](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>連接 toohello Postgres 資料庫
同樣地切換 toohello postgres 使用者：

    # su - postgres

建立 Postgres 資料庫：

    $ createdb events

連接您剛才建立的 toohello 事件資料庫：

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>建立和刪除 Postgres 資料表
既然您已經連接 toohello 資料庫，您可以在其中建立資料表。

例如，建立新的範例 Postgres 資料表使用下列命令的 hello:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

您現在已設定四個資料行的資料表，以 hello 下列資料行名稱和限制：

1. hello"name"的資料行具有已受到 hello VARCHAR 命令 toobe 底下 20 個字元長時間。
2. hello"food"資料行指出 hello 食物項目，讓每個人。 VARCHAR 限制 30 個字元在這個文字 toobe。
3. hello 「 確認 」 資料行記錄是否 hello 人員 rsvp toohello 聚會的活動。 hello 可接受值為"Y"和"N"。
4. hello 「 日期 」 欄會顯示這些註冊 hello 事件時。 Postgres 的必要日期格式為 yyyy-mm-dd。

如果已成功建立您的資料表，您應該看到 hello 下列：

![image](./media/postgresql-install/no4.png)

您也可以使用下列命令的 hello 檢查 hello 資料表結構：

![image](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>加入資料 tooa 資料表
首先，將資料插入資料列：

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

您應該會看見此輸出：

![image](./media/postgresql-install/no6.png)

您可以加入一些更多人 toohello 資料表以及。 以下是一些選項，或者您可以建立自己的選項：

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>顯示資料表
使用下列命令 tooshow 資料表 hello:

    select * from potluck;

hello 輸出為：

![image](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>刪除資料表中的資料
使用下列命令 toodelete 資料在資料表中的 hello:

    delete from potluck where name=’John’;

這會刪除 hello"John"的資料列中的所有 hello 資訊。 hello 輸出為：

![image](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>更新資料表中的資料
使用下列命令 tooupdate 資料在資料表中的 hello。 此一，Sandy 已確認，她出席，因此我們將變更從 「 N 」 她 RSVP 太"Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>取得 PostgreSQL 的詳細資訊
既然您已完成的 PostgreSQL Azure Linux VM 中的 hello 安裝，您可以享用在 Azure 中使用它。 深入了解 PostgreSQL，toolearn 造訪 hello [PostgreSQL 網站](http://www.postgresql.org/)。

