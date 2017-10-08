---
title: "web 應用程式的有效 aaaUse DevOps 環境 |Microsoft 文件"
description: "了解如何 toouse 部署位置設定的 tooset 和管理多個應用程式的開發環境"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>為 Web 應用程式有效地使用 DevOps 環境
本文章將示範如何 tooset 及多個版本的應用程式中不同的環境，例如開發、 預備、 品質保證 (QA) 及生產環境時，管理 web 應用程式部署。 每個版本的應用程式可視為 hello 的特定目的，是您的部署程序的開發環境。 例如，開發人員可以使用 hello QA 環境 tootest hello hello 的應用程式品質，它們推送 hello 變更 tooproduction 之前。
多個開發環境可以是一項挑戰需要 tootrack 程式碼，因為管理資源 （運算、 web 應用程式、 資料庫、 快取等），並在環境中部署的程式碼。

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>設定非生產環境 (預備、開發、QA)
生產環境 web 應用程式已啟動並執行之後，hello 下一個步驟是 toocreate 非生產環境。 toouse 部署位置，請確定您在 hello Standard 或 Premium Azure App Service 方案模式執行。 部署位置是具有專屬主機名稱的即時 Web 應用程式。 Web 應用程式的內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。 當您部署您的應用程式 tooa 部署位置時，您會收到 hello 下列優點：

- 交換 hello 與 hello 生產位置的應用程式之前，您可以驗證預備部署位置中的變更 tooa web 應用程式。
- 當您第一次部署 web 應用程式 tooa 位置交換至生產環境時，hello 位置的所有執行個體已就緒之前正在交換至生產環境。 此程序可排除部署 Web 應用程式時的停機情況。 hello 流量重新導向，隨選和任何要求遭到捨棄因 tooswap 作業。 tooautomate 整個工作流程中，設定[自動交換](web-sites-staged-publishing.md#configure-auto-swap)時不需要預先交換驗證。
- 交換之後, hello 位置現在具有先前分段 hello web 應用程式有 hello 先前生產環境 web 應用程式。 如果 hello 變更成 hello 生產位置交換未如您所預期，您可以執行 hello 相同交換立即 tooget 您 「 上次已知的良好 」 web 應用程式上一步。

tooset 預備部署位置，請參閱[設定預備環境中 Azure App Service web 應用程式](web-sites-staged-publishing.md)。 每個環境都應該包含專屬的一組資源。 例如，如果 Web 應用程式使用資料庫，則生產和預備 Web 應用程式就應該使用不同的資料庫。 新增預備環境的開發環境資源，例如資料庫、 儲存或快取 tooset 執行開發環境。

## <a name="examples-of-using-multiple-development-environments"></a>使用多個開發環境的範例
任何專案都應該至少有兩個環境應遵循原始程式碼管理：開發和生產環境。 如果您使用內容管理系統 (CMSs)、 應用程式架構等等，hello 應用程式可能不支援這種情況下，如果沒有自訂程。 這個可能性適用於某些 hello 受歡迎的架構 hello 下列各節中討論。 許多問題有 toomind，當您使用 CMS/架構，例如：

- 您如何細分 hello 內容到不同的環境？
- 可以變更哪些檔案而不影響架構版本更新？
- 如何管理各環境的設定？
- 您要如何管理模組、 外掛程式，及 hello core framework 的版本更新？

有許多方式 tooset 總多個專案的環境。 hello 下列範例顯示每個個別的應用程式的一種方法。

### <a name="wordpress"></a>WordPress
在本節中，您將學習 tooset 上使用的部署工作流程用於 WordPress 的介面槽。 WordPress 如同大部分的 CMS 解決方案，在不進行自訂的情況下將不支援多個開發環境。 hello Azure App Service Web 應用程式功能有一些功能，可讓您輕鬆 toostore 外部程式碼的組態設定。

1. 建立預備位置之前，設定您的應用程式程式碼 toosupport 多個環境。 toosupport 多個環境中 WordPress，您需要 tooedit`wp-config.php`上您的本機開發 web 應用程式，並加入下列程式碼中的 hello 檔案 hello 開頭的 hello。 此程序可讓應用程式 toopick hello 正確組態根據 hello 選取的環境。

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. 呼叫的 web 應用程式根目錄底下建立資料夾`config`，並加入 hello`wp-config.azure.php`和`wp-config.local.php`分別代表您的 Azure 環境和本機環境中的檔案。

3. 複製中的 hello 下列`wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Hello 先前的程式碼所示設定 hello 安全性金鑰可以幫助 tooprevent 您 web 應用程式，從受到駭客攻擊，因此，請使用唯一值。 如果您需要 toogenerate hello 字串 hello 程式碼中所述的安全性金鑰，您可以[移 toohello 自動產生器](https://api.wordpress.org/secret-key/1.1/salt)toocreate 新索引鍵/值組。

4. 複製 hello 下列程式碼中`wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>使用相對路徑
一個 hello WordPress 應用程式中的最後一件事 tooconfigure 是相對路徑。 WordPress hello 資料庫中儲存的 URL 資訊。 此存放裝置從一個環境 tooanother 移動內容更難。 每當您從本機 toostage 或階段 tooproduction 環境移動，您會需要 tooupdate hello 資料庫。 tooreduce hello 風險的問題會造成與部署資料庫，每次部署從一個環境 tooanother，使用 hello[相對根目錄連結外掛程式](https://wordpress.org/plugins/root-relative-urls/)，您可以使用 hello WordPress 管理員來安裝儀表板。

新增下列項目 tooyour hello`wp-config.php`檔案再 hello`That's all, stop editing!`註解：

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

啟用透過 hello hello 外掛程式`Plugins`WordPress 管理員儀表板中的功能表。 儲存您的永久連結設定供 WordPress 應用程式使用。

#### <a name="hello-final-wp-configphp-file"></a>最終的 hello`wp-config.php`檔案
任何 WordPress 核心更新並不會影響您的 `wp-config.php`、`wp-config.azure.php` 和 `wp-config.local.php` 檔案。 以下是最後一版的 hello`wp-config.php`檔案：

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>設定預備環境
1. 如果您已經有 Azure 訂用帳戶上執行 WordPress web 應用程式，登入 toohello [Azure 入口網站](http://portal.azure.com)，並前往 tooyour WordPress web 應用程式。 如果您沒有 WordPress web 應用程式，您可以從建立 hello Azure Marketplace。 詳細資訊，請參閱 toolearn [WordPress web 應用程式建立 Azure App Service 中](web-sites-php-web-site-gallery.md)。
按一下**設定** > **部署位置** > **新增**toocreate 部署位置與 hello 名稱*階段*. 部署位置是共用 hello hello 主要 web 應用程式與您先前建立的相同資源的其他 web 應用程式。

    ![建立階段部署位置](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. 加入另一個的 MySQL 資料庫，例如`wordpress-stage-db`，tooyour 資源群組、 `wordpressapp-group`。

    ![將 MySQL 資料庫 tooresource 群組加入](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. 更新 hello 階段部署位置 toopoint toohello 新的資料庫，連接字串`wordpress-stage-db`。 您的生產環境 web 應用程式， `wordpressprodapp`，和預備環境 web 應用程式， `wordpressprodapp-stage`，必須點 toodifferent 資料庫。

#### <a name="configure-environment-specific-app-settings"></a>設定環境特定的應用程式設定
開發人員可以儲存在 Azure 中的字串索引鍵/值組做 hello 組態資訊，呼叫**應用程式設定**，，具有相關聯的 web 應用程式。 在執行階段，web 應用程式，自動擷取這些值，並讓它們執行您 web 應用程式中的可用 toocode。 從安全性觀點來看，這是不錯的附帶效益，因為資料庫連接字串與密碼之類的機密資訊永遠不會在檔案 (例如 `wp-config.php`) 中顯示為純文字。

此程序會說明下列段落的 hello，很有用，因為它包含檔案的變更和 hello WordPress 應用程式的資料庫變更：

* WordPress 版本升級
* 加入新的或編輯或升級外掛程式
* 加入新的或編輯或升級佈景主題

設定下列項目的應用程式設定：

* 資料庫資訊
* 開啟/關閉 WordPress 記錄
* WordPress 安全性設定

![Wordpress Web 應用程式的應用程式設定](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

請確認您新增 hello 遵循生產環境 web 應用程式和預備位置的應用程式設定。 請注意 hello 生產環境 web 應用程式和執行 web 應用程式使用不同的資料庫。

1. 清除 hello**位置設定**WP_ENV 以外的所有 hello 設定參數的核取方塊。 此程序將會針對您的 web 應用程式、 檔案內容和資料庫交換 hello 組態。 如果**位置設定**是選取此選項，hello web 應用程式的應用程式設定和連接字串組態將*不*進行時，在環境之間移動**交換**作業。 任何的資料庫變更將不會中斷您的生產 Web 應用程式。

2. 使用 WebMatrix 或您的選擇，例如 FTP、 Git、 或 PhpMyAdmin 的工具，即可部署 hello 本機開發環境 web 應用程式 toohello 階段 web 應用程式和資料庫。

    ![WordPress Web 應用程式的 WebMatrix 發佈對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. 瀏覽及測試您的預備 Web 應用程式。 Hello 佈景主題的 hello web 應用程式所在 toobe 更新的案例，請考慮以下是 hello 臨時 web 應用程式。

    ![交換位置之前瀏覽預備 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. 如果一切看來正常，請按一下 hello**交換**按鈕在您執行的 web 應用程式 toomove 內容 toohello 實際執行環境。 在此情況下，在環境之間交換 hello web 應用程式與 hello 資料庫每個**交換**作業。

    ![交換 WordPress 的變更的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > 如果您的案例需要 tooonly 推入檔案 （資料庫更新），然後檢查**位置設定**與資料庫相關的所有 hello*應用程式設定*和*連接字串設定*在 hello **Web 應用程式設定**刀鋒視窗內 hello Azure 入口網站，然後再執行 hello**交換**。 在此情況下，DB_NAME、DB_HOST、DB_PASSWORD、DB_USER 預設連接字串設定在執行**交換**的時候應該不會顯示在預覽變更中。 在這個階段，當您完成 hello**交換**hello WordPress web 應用程式將會擁有 hello 的作業更新僅適用於檔案。
    >
    >

    這樣做之前**交換**，以下是 hello 生產 WordPress web 應用程式。
    ![交換位置之前的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    之後 hello**交換**hello 佈景主題的作業已更新您的生產環境 web 應用程式上。

    ![交換位置之後的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. 當您需要回 tooroll 時，您可以移 toohello 生產環境 web**應用程式設定**，然後按一下 hello**交換**按鈕 tooswap hello web 應用程式和資料庫生產 toostaging 位置。 請記住，如果資料庫的變更所含**交換**作業，然後 hello 下次部署 tooyour 臨時 web 應用程式，您需要 toodeploy hello 資料庫變更 toohello 目前資料庫執行的 web 應用程式。 hello 目前的資料庫可能 hello 先前的實際執行資料庫或 hello 階段資料庫。

#### <a name="summary"></a>摘要
以下是適用於任何具有資料庫之應用程式的通用程序：

1. 安裝在本機環境的 hello 應用程式。
2. 包含環境特定組態 (本機和 Azure Web Apps)。
3. 針對 Web Apps 設定預備和生產環境。
4. 如果您已經在 Azure 上執行的實際執行應用程式，同步處理將實際執行內容 （檔案/程式碼和資料庫） toolocal 環境和預備環境。
5. 在您的本機環境上開發應用程式。
6. 將維護中或已鎖定的模式中，您生產環境 web 應用程式，然後同步處理從生產 toostaging 和開發人員環境的資料庫內容。
7. 部署 toohello 預備環境和測試。
8. 部署 tooproduction 環境。
9. 重複步驟 4 至 6。

### <a name="umbraco"></a>Umbraco
在本節中，您將學習 hello Umbraco CMS 橫跨多個 DevOps 環境所使用的自訂模組 toodeploy。 此範例提供不同的方法 toomanaging 多個開發環境。

[Umbraco CMS (英文)](http://umbraco.com/) 是許多開發人員常用的 .NET CMS 解決方案。 它提供 hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2)模組 toodeploy 從開發 toostaging tooproduction 環境中。 您可以使用 Visual Studio 或 WebMatrix，輕鬆地建立 Umbraco CMS Web 應用程式的本機開發環境。

- [使用 Visual Studio 建立 Umbraco Web 應用程式 (英文)](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [使用 WebMatrix 建立 Umbraco Web 應用程式 (英文)](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

一定要記得 tooremove hello`install`資料夾下您的應用程式，並永遠不會將它上傳 toostage 或生產環境 web 應用程式。 本教學課程使用 WebMatrix。

#### <a name="set-up-a-staging-environment"></a>設定預備環境
1. 建立部署位置，如先前所述的 hello Umbraco CMS web 應用程式中，假設您已經有 Umbraco CMS web 應用程式和執行。 如果不這麼做，您可以建立一個從 hello Marketplace。
2. 更新您階段部署位置 toopoint toohello 新的連接字串 hello **umbraco-階段 db**資料庫。 您的生產環境 web 應用程式 (umbraositecms-1) 和執行 web 應用程式 （umbracositecms-1-階段）*必須*點 toodifferent 資料庫。

    ![使用新預備資料庫更新預備 Web 應用程式的連接字串](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. 按一下**取得發行設定**hello 部署位置**階段**。 此程序將下載儲存所有 hello 資訊，Visual Studio 或 WebMatrix 需要 toopublish 從 hello 本機開發 web 應用程式 toohello Azure web 應用程式的應用程式的發行設定檔。

    ![取得發行 hello 臨時 web 應用程式的設定](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. 在 WebMatrix 或 Visual Studio 中開啟您的本機開發 Web 應用程式。 本教學課程使用 WebMatrix。 首先，您需要 tooimport hello 發行臨時的 web 應用程式設定檔。

    ![使用 WebMatrix 匯入 Umbraco 的發佈設定](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. 在 [hello] 對話方塊中檢閱變更並部署本機 web 應用程式 tooyour Azure web 應用程式， *umbracositecms 1 階段*。 當您在直接 tooyour 臨時 web 應用程式部署的檔案時，您將會省略中 hello 檔案`~/app_data/TEMP/`資料夾，因為第一個 hello 階段 web 應用程式時，將重新產生這些檔案啟動。 您也應該省略 hello`~/app_data/umbraco.config`也將重新產生的檔案。

    ![在 WebMatrix 中檢閱發佈變更](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. 您已成功發行 hello Umbraco 本機 web 應用程式 toohello 臨時 web 應用程式之後，瀏覽 tooyour 臨時 web 應用程式，並執行一些測試 toorule 發生的問題。

#### <a name="set-up-hello-courier2-deployment-module"></a>設定 hello Courier2 部署模組
以 hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2)模組，您可以直接以滑鼠右鍵按一下 toopush 內容、 樣式表和執行 web 應用程式 tooa 生產環境 web 應用程式從開發模組。 此程序減少中斷您的生產環境 web 應用程式，當您將更新部署 hello 的風險。
購買授權 hello Courier2`*.azurewebsites.net`網域與您的自訂網域 (例如 http://abc.com)。 位置 hello 購買 hello 授權後，下載授權 (。授權檔） 中 hello`bin`資料夾。

![將授權檔案拖放到 bin 資料夾下](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [下載 hello Courier2 套件](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/)。 按一下 登入 tooyour 階段 web 應用程式，例如 http://umbracocms-site-stage.azurewebsites.net/umbraco hello**開發人員**功能表，然後再按一下**封裝** > **安裝本機封裝**。

    ![Umbraco 套件安裝程式](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. 使用上傳 hello Courier2 套件 hello 安裝程式。

    ![上傳 courier 模組的套件](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. tooconfigure hello 封裝時，您需要下 hello tooupdate hello courier.config 檔案**Config** web 應用程式資料夾。

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. 在下`<repositories>`，輸入 hello 生產網站的 URL 和使用者資訊。
    如果您使用 hello 預設 Umbraco 成員資格提供者，然後加入 hello 識別碼 hello 系統管理使用者在 hello&lt;使用者&gt;> 一節。
    如果您使用自訂的 Umbraco 成員資格提供者，使用`<login>`，`<password>` hello Courier2 模組 tooconnect toohello 生產網站中。
    如需詳細資訊，[檢閱 hello 文件以 hello Courier2 模組](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation)。

5. 同樣地，hello Courier2 模組安裝在生產網站，並設定它 toopoint toohello 階段 web 應用程式中其各自的 courier.config 檔案，如下所示。

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. 按一下 hello **Courier2** hello Umbraco CMS web 應用程式儀表板 索引標籤，然後按一下**位置**。 中所述，您應該看到 hello 儲存機制名稱`courier.config`。 請在生產和預備 Web 應用程式上執行此程序。

    ![檢視目的地 Web 應用程式儲存機制](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. 從暫存 toohello 的生產環境網站的 hello toodeploy 內容太移**內容**，然後選取現有網頁或建立新的頁面。 我將我 hello hello 網頁標題所在的 web 應用程式中選取現有的頁面**入門 – 新**，然後按一下**儲存並發行**。

    ![變更頁面的標題並發佈](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. 以滑鼠右鍵按一下 hello 修改頁面 tooview 所有 hello 選項。 按一下**新細明體**tooopen hello**部署** 對話方塊。 按一下**部署**tooinitiate 部署。

    ![Courier 模組部署對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. 檢閱 hello 變更，然後按一下**繼續**。

    ![Courier 模組部署對話方塊檢閱變更](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    hello 部署記錄檔會顯示 hello 部署是否成功。

     ![檢視 Courier 模組的部署記錄檔](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. 如果 hello 的變更會反映，瀏覽您的生產環境 web 應用程式 toosee。

     ![瀏覽實際執行 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn 深入了解如何 toouse 新細明體，檢閱 hello 文件。

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>如何 tooupgrade hello Umbraco CMS 版本
新細明體將無法協助您從一個版本的 Umbraco CMS tooanother 升級。 當您升級 Umbraco CMS 版本，您必須檢查有不相容性與您的自訂模組或模組從夥伴以及 hello Umbraco 核心程式庫。 以下是最佳作法：

* 務必在升級之前備份您的 Web 應用程式和資料庫。 在 Azure 中的 web 應用程式，您可以設定自動備份您的網站使用 hello 備份功能，並還原您的網站，如果視需要使用 hello 還原功能。 如需詳細資訊，請參閱[如何設定您的 web 應用程式的 tooback](web-sites-backup.md)和[如何 toorestore 您 web 應用程式](web-sites-restore.md)。
* 檢查來自夥伴的封裝是否與您要升級至 hello 版本相容。 在 hello 套件下載頁面，檢閱與 Umbraco CMS 版的 hello 專案相容。

如需有關如何 tooupgrade 您 web 應用程式在本機，[看到 hello 一般的升級指導方針](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general)。

本機開發網站升級之後，將發行 hello 變更 toohello 臨時 web 應用程式。 測試您的應用程式。 如果一切看來正常，使用 hello**交換**按鈕 tooswap 預備網站 toohello 生產 web 應用程式。 當您使用 hello**交換**作業，您可以檢視將受到影響的 hello 變更 web 應用程式的組態中。 這**交換**作業交換 hello web 應用程式和資料庫。 之後 hello**交換**、 hello 實際執行 web 應用程式將點 toohello umbraco 階段資料庫的資料庫，以及 hello 臨時 web 應用程式將點 tooumbraco-prod db 資料庫。

![交換部署 Umbraco CMS 的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

以下是交換 hello web 應用程式和 hello 資料庫的優點：

* 您可以復原舊版 web 應用程式與另一個 toohello**交換**是否有任何應用程式問題。
* 進行升級時，您需要 toodeploy 檔案和資料庫從臨時 web 應用程式 toohello 生產環境 web 應用程式的 hello 和資料庫。 當您部署檔案和資料庫時，有許多情況可能發生錯誤。 使用 hello**交換**功能的位置，我們可以在升級期間的停機時間減少，降低 hello 風險的部署變更時所發生的失敗。
* 您可以**A / B 測試**使用 hello[在生產環境中測試](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/)功能。

此範例所示 hello hello 平台，您可以建置自訂模組類似 tooUmbraco 新細明體模組 toomanage 部署環境之間的彈性。

## <a name="references"></a>參考
[敏捷式軟體開發 (Agile Software Development) 與 Azure App Service](app-service-agile-software-development.md)

[針對 Azure App Service 中的 Web 應用程式設定預備環境](web-sites-staged-publishing.md)

[如何 tooblock web 存取 toonon 生產部署位置](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
