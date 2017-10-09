## <a name="install-wordpress"></a><span data-ttu-id="6b6de-101">安裝 WordPress</span><span class="sxs-lookup"><span data-stu-id="6b6de-101">Install WordPress</span></span>

<span data-ttu-id="6b6de-102">如果您想要 tootry 程式堆疊，安裝範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="6b6de-102">If you want tootry your stack, install a sample app.</span></span> <span data-ttu-id="6b6de-103">例如，下列步驟的 hello 安裝 hello 開放原始碼[WordPress](https://wordpress.org/)平台 toocreate 網站和部落格。</span><span class="sxs-lookup"><span data-stu-id="6b6de-103">As an example, hello following steps install hello open source [WordPress](https://wordpress.org/) platform toocreate websites and blogs.</span></span> <span data-ttu-id="6b6de-104">包含其他工作負載 tootry [Drupal](http://www.drupal.org)和[Moodle](https://moodle.org/)。</span><span class="sxs-lookup"><span data-stu-id="6b6de-104">Other workloads tootry include [Drupal](http://www.drupal.org) and [Moodle](https://moodle.org/).</span></span> 

<span data-ttu-id="6b6de-105">此 WordPress 設定用於概念證明。</span><span class="sxs-lookup"><span data-stu-id="6b6de-105">This WordPress setup is for proof of concept.</span></span> <span data-ttu-id="6b6de-106">如需詳細資訊和實際執行安裝的設定，請參閱 hello [WordPress 文件](https://codex.wordpress.org/Main_Page)。</span><span class="sxs-lookup"><span data-stu-id="6b6de-106">For more information and settings for production installation, see hello [WordPress documentation](https://codex.wordpress.org/Main_Page).</span></span> 



### <a name="install-hello-wordpress-package"></a><span data-ttu-id="6b6de-107">安裝 hello WordPress 套件</span><span class="sxs-lookup"><span data-stu-id="6b6de-107">Install hello WordPress package</span></span>

<span data-ttu-id="6b6de-108">執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6b6de-108">Run hello following command:</span></span>

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a><span data-ttu-id="6b6de-109">設定 WordPress</span><span class="sxs-lookup"><span data-stu-id="6b6de-109">Configure WordPress</span></span>

<span data-ttu-id="6b6de-110">設定 WordPress toouse MySQL 和 PHP。</span><span class="sxs-lookup"><span data-stu-id="6b6de-110">Configure WordPress toouse MySQL and PHP.</span></span> <span data-ttu-id="6b6de-111">執行下列命令 tooopen hello 您選擇的文字編輯器，並建立 hello 檔案`/etc/wordpress/config-localhost.php`:</span><span class="sxs-lookup"><span data-stu-id="6b6de-111">Run hello following command tooopen a text editor of your choice and create hello file `/etc/wordpress/config-localhost.php`:</span></span>

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
<span data-ttu-id="6b6de-112">下列幾行 toohello 檔，以取代為您資料庫的密碼複本 hello *yourPassword* （保持不變的其他值）。</span><span class="sxs-lookup"><span data-stu-id="6b6de-112">Copy hello following lines toohello file, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="6b6de-113">然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b6de-113">Then save hello file.</span></span>

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

<span data-ttu-id="6b6de-114">工作目錄中建立文字檔`wordpress.sql`tooconfigure hello WordPress 資料庫：</span><span class="sxs-lookup"><span data-stu-id="6b6de-114">In a working directory, create a text file `wordpress.sql` tooconfigure hello WordPress database:</span></span> 

```bash
sudo sensible-editor wordpress.sql
```

<span data-ttu-id="6b6de-115">新增下列命令，以取代您的資料庫密碼為 hello *yourPassword* （保持不變的其他值）。</span><span class="sxs-lookup"><span data-stu-id="6b6de-115">Add hello following commands, substituting your database password for *yourPassword* (leave other values unchanged).</span></span> <span data-ttu-id="6b6de-116">然後儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="6b6de-116">Then save hello file.</span></span>

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


<span data-ttu-id="6b6de-117">執行下列命令 toocreate hello 資料庫 hello:</span><span class="sxs-lookup"><span data-stu-id="6b6de-117">Run hello following command toocreate hello database:</span></span>

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

<span data-ttu-id="6b6de-118">Hello 命令完成之後，刪除 hello 檔案`wordpress.sql`。</span><span class="sxs-lookup"><span data-stu-id="6b6de-118">After hello command completes, delete hello file `wordpress.sql`.</span></span>

<span data-ttu-id="6b6de-119">移動 hello WordPress 安裝 toohello web 伺服器文件根目錄：</span><span class="sxs-lookup"><span data-stu-id="6b6de-119">Move hello WordPress installation toohello web server document root:</span></span>

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

<span data-ttu-id="6b6de-120">現在您可以完成 hello WordPress 設定，並發佈 hello 平台上。</span><span class="sxs-lookup"><span data-stu-id="6b6de-120">Now you can complete hello WordPress setup and publish on hello platform.</span></span> <span data-ttu-id="6b6de-121">開啟瀏覽器並移過`http://yourPublicIPAddress/wordpress`。</span><span class="sxs-lookup"><span data-stu-id="6b6de-121">Open a browser and go too`http://yourPublicIPAddress/wordpress`.</span></span> <span data-ttu-id="6b6de-122">取代您的 VM hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6b6de-122">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="6b6de-123">它看起來應該類似 toothis 映像。</span><span class="sxs-lookup"><span data-stu-id="6b6de-123">It should look similar toothis image.</span></span>

![WordPress 安裝頁面](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)