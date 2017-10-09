## <a name="install-wordpress"></a>安裝 WordPress

如果您想要 tootry 程式堆疊，安裝範例應用程式。 例如，下列步驟的 hello 安裝 hello 開放原始碼[WordPress](https://wordpress.org/)平台 toocreate 網站和部落格。 包含其他工作負載 tootry [Drupal](http://www.drupal.org)和[Moodle](https://moodle.org/)。 

此 WordPress 設定用於概念證明。 如需詳細資訊和實際執行安裝的設定，請參閱 hello [WordPress 文件](https://codex.wordpress.org/Main_Page)。 



### <a name="install-hello-wordpress-package"></a>安裝 hello WordPress 套件

執行下列命令的 hello:

```bash
sudo apt install wordpress
```

### <a name="configure-wordpress"></a>設定 WordPress

設定 WordPress toouse MySQL 和 PHP。 執行下列命令 tooopen hello 您選擇的文字編輯器，並建立 hello 檔案`/etc/wordpress/config-localhost.php`:

```bash
sudo sensible-editor /etc/wordpress/config-localhost.php
```
下列幾行 toohello 檔，以取代為您資料庫的密碼複本 hello *yourPassword* （保持不變的其他值）。 然後儲存 hello 檔案。

```php
<?php
define('DB_NAME', 'wordpress');
define('DB_USER', 'wordpress');
define('DB_PASSWORD', 'yourPassword');
define('DB_HOST', 'localhost');
define('WP_CONTENT_DIR', '/usr/share/wordpress/wp-content');
?>
```

工作目錄中建立文字檔`wordpress.sql`tooconfigure hello WordPress 資料庫： 

```bash
sudo sensible-editor wordpress.sql
```

新增下列命令，以取代您的資料庫密碼為 hello *yourPassword* （保持不變的其他值）。 然後儲存 hello 檔案。

```sql
CREATE DATABASE wordpress;
GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER
ON wordpress.*
toowordpress@localhost
IDENTIFIED BY 'yourPassword';
FLUSH PRIVILEGES;
```


執行下列命令 toocreate hello 資料庫 hello:

```bash
cat wordpress.sql | sudo mysql --defaults-extra-file=/etc/mysql/debian.cnf
```

Hello 命令完成之後，刪除 hello 檔案`wordpress.sql`。

移動 hello WordPress 安裝 toohello web 伺服器文件根目錄：

```bash
sudo ln -s /usr/share/wordpress /var/www/html/wordpress

sudo mv /etc/wordpress/config-localhost.php /etc/wordpress/config-default.php
```

現在您可以完成 hello WordPress 設定，並發佈 hello 平台上。 開啟瀏覽器並移過`http://yourPublicIPAddress/wordpress`。 取代您的 VM hello 公用 IP 位址。 它看起來應該類似 toothis 映像。

![WordPress 安裝頁面](./media/virtual-machines-linux-tutorial-wordpress/wordpressstartpage.png)