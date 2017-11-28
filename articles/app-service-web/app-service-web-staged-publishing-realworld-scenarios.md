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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="ef302-103">為 Web 應用程式有效地使用 DevOps 環境</span><span class="sxs-lookup"><span data-stu-id="ef302-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="ef302-104">本文章將示範如何 tooset 及多個版本的應用程式中不同的環境，例如開發、 預備、 品質保證 (QA) 及生產環境時，管理 web 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="ef302-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="ef302-105">每個版本的應用程式可視為 hello 的特定目的，是您的部署程序的開發環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="ef302-106">例如，開發人員可以使用 hello QA 環境 tootest hello hello 的應用程式品質，它們推送 hello 變更 tooproduction 之前。</span><span class="sxs-lookup"><span data-stu-id="ef302-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="ef302-107">多個開發環境可以是一項挑戰需要 tootrack 程式碼，因為管理資源 （運算、 web 應用程式、 資料庫、 快取等），並在環境中部署的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef302-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="ef302-108">設定非生產環境 (預備、開發、QA)</span><span class="sxs-lookup"><span data-stu-id="ef302-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="ef302-109">生產環境 web 應用程式已啟動並執行之後，hello 下一個步驟是 toocreate 非生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="ef302-110">toouse 部署位置，請確定您在 hello Standard 或 Premium Azure App Service 方案模式執行。</span><span class="sxs-lookup"><span data-stu-id="ef302-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="ef302-111">部署位置是具有專屬主機名稱的即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="ef302-112">Web 應用程式的內容與組態項目可以交換兩個部署位置，包括 hello 生產位置。</span><span class="sxs-lookup"><span data-stu-id="ef302-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="ef302-113">當您部署您的應用程式 tooa 部署位置時，您會收到 hello 下列優點：</span><span class="sxs-lookup"><span data-stu-id="ef302-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="ef302-114">交換 hello 與 hello 生產位置的應用程式之前，您可以驗證預備部署位置中的變更 tooa web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="ef302-115">當您第一次部署 web 應用程式 tooa 位置交換至生產環境時，hello 位置的所有執行個體已就緒之前正在交換至生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="ef302-116">此程序可排除部署 Web 應用程式時的停機情況。</span><span class="sxs-lookup"><span data-stu-id="ef302-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="ef302-117">hello 流量重新導向，隨選和任何要求遭到捨棄因 tooswap 作業。</span><span class="sxs-lookup"><span data-stu-id="ef302-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="ef302-118">tooautomate 整個工作流程中，設定[自動交換](web-sites-staged-publishing.md#configure-auto-swap)時不需要預先交換驗證。</span><span class="sxs-lookup"><span data-stu-id="ef302-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="ef302-119">交換之後, hello 位置現在具有先前分段 hello web 應用程式有 hello 先前生產環境 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="ef302-120">如果 hello 變更成 hello 生產位置交換未如您所預期，您可以執行 hello 相同交換立即 tooget 您 「 上次已知的良好 」 web 應用程式上一步。</span><span class="sxs-lookup"><span data-stu-id="ef302-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="ef302-121">tooset 預備部署位置，請參閱[設定預備環境中 Azure App Service web 應用程式](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="ef302-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="ef302-122">每個環境都應該包含專屬的一組資源。</span><span class="sxs-lookup"><span data-stu-id="ef302-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="ef302-123">例如，如果 Web 應用程式使用資料庫，則生產和預備 Web 應用程式就應該使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="ef302-124">新增預備環境的開發環境資源，例如資料庫、 儲存或快取 tooset 執行開發環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="ef302-125">使用多個開發環境的範例</span><span class="sxs-lookup"><span data-stu-id="ef302-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="ef302-126">任何專案都應該至少有兩個環境應遵循原始程式碼管理：開發和生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="ef302-127">如果您使用內容管理系統 (CMSs)、 應用程式架構等等，hello 應用程式可能不支援這種情況下，如果沒有自訂程。</span><span class="sxs-lookup"><span data-stu-id="ef302-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="ef302-128">這個可能性適用於某些 hello 受歡迎的架構 hello 下列各節中討論。</span><span class="sxs-lookup"><span data-stu-id="ef302-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="ef302-129">許多問題有 toomind，當您使用 CMS/架構，例如：</span><span class="sxs-lookup"><span data-stu-id="ef302-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="ef302-130">您如何細分 hello 內容到不同的環境？</span><span class="sxs-lookup"><span data-stu-id="ef302-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="ef302-131">可以變更哪些檔案而不影響架構版本更新？</span><span class="sxs-lookup"><span data-stu-id="ef302-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="ef302-132">如何管理各環境的設定？</span><span class="sxs-lookup"><span data-stu-id="ef302-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="ef302-133">您要如何管理模組、 外掛程式，及 hello core framework 的版本更新？</span><span class="sxs-lookup"><span data-stu-id="ef302-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="ef302-134">有許多方式 tooset 總多個專案的環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="ef302-135">hello 下列範例顯示每個個別的應用程式的一種方法。</span><span class="sxs-lookup"><span data-stu-id="ef302-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="ef302-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="ef302-136">WordPress</span></span>
<span data-ttu-id="ef302-137">在本節中，您將學習 tooset 上使用的部署工作流程用於 WordPress 的介面槽。</span><span class="sxs-lookup"><span data-stu-id="ef302-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="ef302-138">WordPress 如同大部分的 CMS 解決方案，在不進行自訂的情況下將不支援多個開發環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="ef302-139">hello Azure App Service Web 應用程式功能有一些功能，可讓您輕鬆 toostore 外部程式碼的組態設定。</span><span class="sxs-lookup"><span data-stu-id="ef302-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="ef302-140">建立預備位置之前，設定您的應用程式程式碼 toosupport 多個環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="ef302-141">toosupport 多個環境中 WordPress，您需要 tooedit`wp-config.php`上您的本機開發 web 應用程式，並加入下列程式碼中的 hello 檔案 hello 開頭的 hello。</span><span class="sxs-lookup"><span data-stu-id="ef302-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="ef302-142">此程序可讓應用程式 toopick hello 正確組態根據 hello 選取的環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="ef302-143">呼叫的 web 應用程式根目錄底下建立資料夾`config`，並加入 hello`wp-config.azure.php`和`wp-config.local.php`分別代表您的 Azure 環境和本機環境中的檔案。</span><span class="sxs-lookup"><span data-stu-id="ef302-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="ef302-144">複製中的 hello 下列`wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="ef302-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="ef302-145">Hello 先前的程式碼所示設定 hello 安全性金鑰可以幫助 tooprevent 您 web 應用程式，從受到駭客攻擊，因此，請使用唯一值。</span><span class="sxs-lookup"><span data-stu-id="ef302-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="ef302-146">如果您需要 toogenerate hello 字串 hello 程式碼中所述的安全性金鑰，您可以[移 toohello 自動產生器](https://api.wordpress.org/secret-key/1.1/salt)toocreate 新索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="ef302-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="ef302-147">複製 hello 下列程式碼中`wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="ef302-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="ef302-148">使用相對路徑</span><span class="sxs-lookup"><span data-stu-id="ef302-148">Use relative paths</span></span>
<span data-ttu-id="ef302-149">一個 hello WordPress 應用程式中的最後一件事 tooconfigure 是相對路徑。</span><span class="sxs-lookup"><span data-stu-id="ef302-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="ef302-150">WordPress hello 資料庫中儲存的 URL 資訊。</span><span class="sxs-lookup"><span data-stu-id="ef302-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="ef302-151">此存放裝置從一個環境 tooanother 移動內容更難。</span><span class="sxs-lookup"><span data-stu-id="ef302-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="ef302-152">每當您從本機 toostage 或階段 tooproduction 環境移動，您會需要 tooupdate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="ef302-153">tooreduce hello 風險的問題會造成與部署資料庫，每次部署從一個環境 tooanother，使用 hello[相對根目錄連結外掛程式](https://wordpress.org/plugins/root-relative-urls/)，您可以使用 hello WordPress 管理員來安裝儀表板。</span><span class="sxs-lookup"><span data-stu-id="ef302-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="ef302-154">新增下列項目 tooyour hello`wp-config.php`檔案再 hello`That's all, stop editing!`註解：</span><span class="sxs-lookup"><span data-stu-id="ef302-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="ef302-155">啟用透過 hello hello 外掛程式`Plugins`WordPress 管理員儀表板中的功能表。</span><span class="sxs-lookup"><span data-stu-id="ef302-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="ef302-156">儲存您的永久連結設定供 WordPress 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="ef302-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="ef302-157">最終的 hello`wp-config.php`檔案</span><span class="sxs-lookup"><span data-stu-id="ef302-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="ef302-158">任何 WordPress 核心更新並不會影響您的 `wp-config.php`、`wp-config.azure.php` 和 `wp-config.local.php` 檔案。</span><span class="sxs-lookup"><span data-stu-id="ef302-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="ef302-159">以下是最後一版的 hello`wp-config.php`檔案：</span><span class="sxs-lookup"><span data-stu-id="ef302-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="ef302-160">設定預備環境</span><span class="sxs-lookup"><span data-stu-id="ef302-160">Set up a staging environment</span></span>
1. <span data-ttu-id="ef302-161">如果您已經有 Azure 訂用帳戶上執行 WordPress web 應用程式，登入 toohello [Azure 入口網站](http://portal.azure.com)，並前往 tooyour WordPress web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="ef302-162">如果您沒有 WordPress web 應用程式，您可以從建立 hello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="ef302-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="ef302-163">詳細資訊，請參閱 toolearn [WordPress web 應用程式建立 Azure App Service 中](web-sites-php-web-site-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="ef302-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="ef302-164">按一下**設定** > **部署位置** > **新增**toocreate 部署位置與 hello 名稱*階段*.</span><span class="sxs-lookup"><span data-stu-id="ef302-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="ef302-165">部署位置是共用 hello hello 主要 web 應用程式與您先前建立的相同資源的其他 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![建立階段部署位置](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="ef302-167">加入另一個的 MySQL 資料庫，例如`wordpress-stage-db`，tooyour 資源群組、 `wordpressapp-group`。</span><span class="sxs-lookup"><span data-stu-id="ef302-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![將 MySQL 資料庫 tooresource 群組加入](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="ef302-169">更新 hello 階段部署位置 toopoint toohello 新的資料庫，連接字串`wordpress-stage-db`。</span><span class="sxs-lookup"><span data-stu-id="ef302-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="ef302-170">您的生產環境 web 應用程式， `wordpressprodapp`，和預備環境 web 應用程式， `wordpressprodapp-stage`，必須點 toodifferent 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="ef302-171">設定環境特定的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="ef302-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="ef302-172">開發人員可以儲存在 Azure 中的字串索引鍵/值組做 hello 組態資訊，呼叫**應用程式設定**，，具有相關聯的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="ef302-173">在執行階段，web 應用程式，自動擷取這些值，並讓它們執行您 web 應用程式中的可用 toocode。</span><span class="sxs-lookup"><span data-stu-id="ef302-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="ef302-174">從安全性觀點來看，這是不錯的附帶效益，因為資料庫連接字串與密碼之類的機密資訊永遠不會在檔案 (例如 `wp-config.php`) 中顯示為純文字。</span><span class="sxs-lookup"><span data-stu-id="ef302-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="ef302-175">此程序會說明下列段落的 hello，很有用，因為它包含檔案的變更和 hello WordPress 應用程式的資料庫變更：</span><span class="sxs-lookup"><span data-stu-id="ef302-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="ef302-176">WordPress 版本升級</span><span class="sxs-lookup"><span data-stu-id="ef302-176">WordPress version upgrade</span></span>
* <span data-ttu-id="ef302-177">加入新的或編輯或升級外掛程式</span><span class="sxs-lookup"><span data-stu-id="ef302-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="ef302-178">加入新的或編輯或升級佈景主題</span><span class="sxs-lookup"><span data-stu-id="ef302-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="ef302-179">設定下列項目的應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="ef302-179">Configure app settings for:</span></span>

* <span data-ttu-id="ef302-180">資料庫資訊</span><span class="sxs-lookup"><span data-stu-id="ef302-180">Database information</span></span>
* <span data-ttu-id="ef302-181">開啟/關閉 WordPress 記錄</span><span class="sxs-lookup"><span data-stu-id="ef302-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="ef302-182">WordPress 安全性設定</span><span class="sxs-lookup"><span data-stu-id="ef302-182">WordPress security settings</span></span>

![Wordpress Web 應用程式的應用程式設定](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="ef302-184">請確認您新增 hello 遵循生產環境 web 應用程式和預備位置的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="ef302-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="ef302-185">請注意 hello 生產環境 web 應用程式和執行 web 應用程式使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="ef302-186">清除 hello**位置設定**WP_ENV 以外的所有 hello 設定參數的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ef302-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="ef302-187">此程序將會針對您的 web 應用程式、 檔案內容和資料庫交換 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="ef302-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="ef302-188">如果**位置設定**是選取此選項，hello web 應用程式的應用程式設定和連接字串組態將*不*進行時，在環境之間移動**交換**作業。</span><span class="sxs-lookup"><span data-stu-id="ef302-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="ef302-189">任何的資料庫變更將不會中斷您的生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="ef302-190">使用 WebMatrix 或您的選擇，例如 FTP、 Git、 或 PhpMyAdmin 的工具，即可部署 hello 本機開發環境 web 應用程式 toohello 階段 web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![WordPress Web 應用程式的 WebMatrix 發佈對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="ef302-192">瀏覽及測試您的預備 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-192">Browse and test your staging web app.</span></span> <span data-ttu-id="ef302-193">Hello 佈景主題的 hello web 應用程式所在 toobe 更新的案例，請考慮以下是 hello 臨時 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![交換位置之前瀏覽預備 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="ef302-195">如果一切看來正常，請按一下 hello**交換**按鈕在您執行的 web 應用程式 toomove 內容 toohello 實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="ef302-196">在此情況下，在環境之間交換 hello web 應用程式與 hello 資料庫每個**交換**作業。</span><span class="sxs-lookup"><span data-stu-id="ef302-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![交換 WordPress 的變更的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="ef302-198">如果您的案例需要 tooonly 推入檔案 （資料庫更新），然後檢查**位置設定**與資料庫相關的所有 hello*應用程式設定*和*連接字串設定*在 hello **Web 應用程式設定**刀鋒視窗內 hello Azure 入口網站，然後再執行 hello**交換**。</span><span class="sxs-lookup"><span data-stu-id="ef302-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="ef302-199">在此情況下，DB_NAME、DB_HOST、DB_PASSWORD、DB_USER 預設連接字串設定在執行**交換**的時候應該不會顯示在預覽變更中。</span><span class="sxs-lookup"><span data-stu-id="ef302-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="ef302-200">在這個階段，當您完成 hello**交換**hello WordPress web 應用程式將會擁有 hello 的作業更新僅適用於檔案。</span><span class="sxs-lookup"><span data-stu-id="ef302-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="ef302-201">這樣做之前**交換**，以下是 hello 生產 WordPress web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="ef302-202">![交換位置之前的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="ef302-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="ef302-203">之後 hello**交換**hello 佈景主題的作業已更新您的生產環境 web 應用程式上。</span><span class="sxs-lookup"><span data-stu-id="ef302-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![交換位置之後的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="ef302-205">當您需要回 tooroll 時，您可以移 toohello 生產環境 web**應用程式設定**，然後按一下 hello**交換**按鈕 tooswap hello web 應用程式和資料庫生產 toostaging 位置。</span><span class="sxs-lookup"><span data-stu-id="ef302-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="ef302-206">請記住，如果資料庫的變更所含**交換**作業，然後 hello 下次部署 tooyour 臨時 web 應用程式，您需要 toodeploy hello 資料庫變更 toohello 目前資料庫執行的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="ef302-207">hello 目前的資料庫可能 hello 先前的實際執行資料庫或 hello 階段資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="ef302-208">摘要</span><span class="sxs-lookup"><span data-stu-id="ef302-208">Summary</span></span>
<span data-ttu-id="ef302-209">以下是適用於任何具有資料庫之應用程式的通用程序：</span><span class="sxs-lookup"><span data-stu-id="ef302-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="ef302-210">安裝在本機環境的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="ef302-211">包含環境特定組態 (本機和 Azure Web Apps)。</span><span class="sxs-lookup"><span data-stu-id="ef302-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="ef302-212">針對 Web Apps 設定預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="ef302-213">如果您已經在 Azure 上執行的實際執行應用程式，同步處理將實際執行內容 （檔案/程式碼和資料庫） toolocal 環境和預備環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="ef302-214">在您的本機環境上開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="ef302-215">將維護中或已鎖定的模式中，您生產環境 web 應用程式，然後同步處理從生產 toostaging 和開發人員環境的資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="ef302-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="ef302-216">部署 toohello 預備環境和測試。</span><span class="sxs-lookup"><span data-stu-id="ef302-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="ef302-217">部署 tooproduction 環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="ef302-218">重複步驟 4 至 6。</span><span class="sxs-lookup"><span data-stu-id="ef302-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="ef302-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="ef302-219">Umbraco</span></span>
<span data-ttu-id="ef302-220">在本節中，您將學習 hello Umbraco CMS 橫跨多個 DevOps 環境所使用的自訂模組 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="ef302-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="ef302-221">此範例提供不同的方法 toomanaging 多個開發環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="ef302-222">[Umbraco CMS (英文)](http://umbraco.com/) 是許多開發人員常用的 .NET CMS 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ef302-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="ef302-223">它提供 hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2)模組 toodeploy 從開發 toostaging tooproduction 環境中。</span><span class="sxs-lookup"><span data-stu-id="ef302-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="ef302-224">您可以使用 Visual Studio 或 WebMatrix，輕鬆地建立 Umbraco CMS Web 應用程式的本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="ef302-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="ef302-225">使用 Visual Studio 建立 Umbraco Web 應用程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="ef302-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="ef302-226">使用 WebMatrix 建立 Umbraco Web 應用程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="ef302-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="ef302-227">一定要記得 tooremove hello`install`資料夾下您的應用程式，並永遠不會將它上傳 toostage 或生產環境 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="ef302-228">本教學課程使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="ef302-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="ef302-229">設定預備環境</span><span class="sxs-lookup"><span data-stu-id="ef302-229">Set up a staging environment</span></span>
1. <span data-ttu-id="ef302-230">建立部署位置，如先前所述的 hello Umbraco CMS web 應用程式中，假設您已經有 Umbraco CMS web 應用程式和執行。</span><span class="sxs-lookup"><span data-stu-id="ef302-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="ef302-231">如果不這麼做，您可以建立一個從 hello Marketplace。</span><span class="sxs-lookup"><span data-stu-id="ef302-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="ef302-232">更新您階段部署位置 toopoint toohello 新的連接字串 hello **umbraco-階段 db**資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="ef302-233">您的生產環境 web 應用程式 (umbraositecms-1) 和執行 web 應用程式 （umbracositecms-1-階段）*必須*點 toodifferent 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![使用新預備資料庫更新預備 Web 應用程式的連接字串](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="ef302-235">按一下**取得發行設定**hello 部署位置**階段**。</span><span class="sxs-lookup"><span data-stu-id="ef302-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="ef302-236">此程序將下載儲存所有 hello 資訊，Visual Studio 或 WebMatrix 需要 toopublish 從 hello 本機開發 web 應用程式 toohello Azure web 應用程式的應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="ef302-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![取得發行 hello 臨時 web 應用程式的設定](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="ef302-238">在 WebMatrix 或 Visual Studio 中開啟您的本機開發 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="ef302-239">本教學課程使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="ef302-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="ef302-240">首先，您需要 tooimport hello 發行臨時的 web 應用程式設定檔。</span><span class="sxs-lookup"><span data-stu-id="ef302-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![使用 WebMatrix 匯入 Umbraco 的發佈設定](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="ef302-242">在 [hello] 對話方塊中檢閱變更並部署本機 web 應用程式 tooyour Azure web 應用程式， *umbracositecms 1 階段*。</span><span class="sxs-lookup"><span data-stu-id="ef302-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="ef302-243">當您在直接 tooyour 臨時 web 應用程式部署的檔案時，您將會省略中 hello 檔案`~/app_data/TEMP/`資料夾，因為第一個 hello 階段 web 應用程式時，將重新產生這些檔案啟動。</span><span class="sxs-lookup"><span data-stu-id="ef302-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="ef302-244">您也應該省略 hello`~/app_data/umbraco.config`也將重新產生的檔案。</span><span class="sxs-lookup"><span data-stu-id="ef302-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![在 WebMatrix 中檢閱發佈變更](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="ef302-246">您已成功發行 hello Umbraco 本機 web 應用程式 toohello 臨時 web 應用程式之後，瀏覽 tooyour 臨時 web 應用程式，並執行一些測試 toorule 發生的問題。</span><span class="sxs-lookup"><span data-stu-id="ef302-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="ef302-247">設定 hello Courier2 部署模組</span><span class="sxs-lookup"><span data-stu-id="ef302-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="ef302-248">以 hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2)模組，您可以直接以滑鼠右鍵按一下 toopush 內容、 樣式表和執行 web 應用程式 tooa 生產環境 web 應用程式從開發模組。</span><span class="sxs-lookup"><span data-stu-id="ef302-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="ef302-249">此程序減少中斷您的生產環境 web 應用程式，當您將更新部署 hello 的風險。</span><span class="sxs-lookup"><span data-stu-id="ef302-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="ef302-250">購買授權 hello Courier2`*.azurewebsites.net`網域與您的自訂網域 (例如 http://abc.com)。</span><span class="sxs-lookup"><span data-stu-id="ef302-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="ef302-251">位置 hello 購買 hello 授權後，下載授權 (。授權檔） 中 hello`bin`資料夾。</span><span class="sxs-lookup"><span data-stu-id="ef302-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![將授權檔案拖放到 bin 資料夾下](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="ef302-253">[下載 hello Courier2 套件](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/)。</span><span class="sxs-lookup"><span data-stu-id="ef302-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="ef302-254">按一下 登入 tooyour 階段 web 應用程式，例如 http://umbracocms-site-stage.azurewebsites.net/umbraco hello**開發人員**功能表，然後再按一下**封裝** > **安裝本機封裝**。</span><span class="sxs-lookup"><span data-stu-id="ef302-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco 套件安裝程式](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="ef302-256">使用上傳 hello Courier2 套件 hello 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![上傳 courier 模組的套件](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="ef302-258">tooconfigure hello 封裝時，您需要下 hello tooupdate hello courier.config 檔案**Config** web 應用程式資料夾。</span><span class="sxs-lookup"><span data-stu-id="ef302-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="ef302-259">在下`<repositories>`，輸入 hello 生產網站的 URL 和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="ef302-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="ef302-260">如果您使用 hello 預設 Umbraco 成員資格提供者，然後加入 hello 識別碼 hello 系統管理使用者在 hello&lt;使用者&gt;> 一節。</span><span class="sxs-lookup"><span data-stu-id="ef302-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="ef302-261">如果您使用自訂的 Umbraco 成員資格提供者，使用`<login>`，`<password>` hello Courier2 模組 tooconnect toohello 生產網站中。</span><span class="sxs-lookup"><span data-stu-id="ef302-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="ef302-262">如需詳細資訊，[檢閱 hello 文件以 hello Courier2 模組](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation)。</span><span class="sxs-lookup"><span data-stu-id="ef302-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="ef302-263">同樣地，hello Courier2 模組安裝在生產網站，並設定它 toopoint toohello 階段 web 應用程式中其各自的 courier.config 檔案，如下所示。</span><span class="sxs-lookup"><span data-stu-id="ef302-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="ef302-264">按一下 hello **Courier2** hello Umbraco CMS web 應用程式儀表板 索引標籤，然後按一下**位置**。</span><span class="sxs-lookup"><span data-stu-id="ef302-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="ef302-265">中所述，您應該看到 hello 儲存機制名稱`courier.config`。</span><span class="sxs-lookup"><span data-stu-id="ef302-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="ef302-266">請在生產和預備 Web 應用程式上執行此程序。</span><span class="sxs-lookup"><span data-stu-id="ef302-266">Do this process on both your production and staging web apps.</span></span>

    ![檢視目的地 Web 應用程式儲存機制](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="ef302-268">從暫存 toohello 的生產環境網站的 hello toodeploy 內容太移**內容**，然後選取現有網頁或建立新的頁面。</span><span class="sxs-lookup"><span data-stu-id="ef302-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="ef302-269">我將我 hello hello 網頁標題所在的 web 應用程式中選取現有的頁面**入門 – 新**，然後按一下**儲存並發行**。</span><span class="sxs-lookup"><span data-stu-id="ef302-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![變更頁面的標題並發佈](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="ef302-271">以滑鼠右鍵按一下 hello 修改頁面 tooview 所有 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="ef302-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="ef302-272">按一下**新細明體**tooopen hello**部署** 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ef302-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="ef302-273">按一下**部署**tooinitiate 部署。</span><span class="sxs-lookup"><span data-stu-id="ef302-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Courier 模組部署對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="ef302-275">檢閱 hello 變更，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="ef302-275">Review hello changes, and then click **Continue**.</span></span>

    ![Courier 模組部署對話方塊檢閱變更](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="ef302-277">hello 部署記錄檔會顯示 hello 部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="ef302-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![檢視 Courier 模組的部署記錄檔](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="ef302-279">如果 hello 的變更會反映，瀏覽您的生產環境 web 應用程式 toosee。</span><span class="sxs-lookup"><span data-stu-id="ef302-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![瀏覽實際執行 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="ef302-281">toolearn 深入了解如何 toouse 新細明體，檢閱 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="ef302-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="ef302-282">如何 tooupgrade hello Umbraco CMS 版本</span><span class="sxs-lookup"><span data-stu-id="ef302-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="ef302-283">新細明體將無法協助您從一個版本的 Umbraco CMS tooanother 升級。</span><span class="sxs-lookup"><span data-stu-id="ef302-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="ef302-284">當您升級 Umbraco CMS 版本，您必須檢查有不相容性與您的自訂模組或模組從夥伴以及 hello Umbraco 核心程式庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="ef302-285">以下是最佳作法：</span><span class="sxs-lookup"><span data-stu-id="ef302-285">Here are best practices:</span></span>

* <span data-ttu-id="ef302-286">務必在升級之前備份您的 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="ef302-287">在 Azure 中的 web 應用程式，您可以設定自動備份您的網站使用 hello 備份功能，並還原您的網站，如果視需要使用 hello 還原功能。</span><span class="sxs-lookup"><span data-stu-id="ef302-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="ef302-288">如需詳細資訊，請參閱[如何設定您的 web 應用程式的 tooback](web-sites-backup.md)和[如何 toorestore 您 web 應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="ef302-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="ef302-289">檢查來自夥伴的封裝是否與您要升級至 hello 版本相容。</span><span class="sxs-lookup"><span data-stu-id="ef302-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="ef302-290">在 hello 套件下載頁面，檢閱與 Umbraco CMS 版的 hello 專案相容。</span><span class="sxs-lookup"><span data-stu-id="ef302-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="ef302-291">如需有關如何 tooupgrade 您 web 應用程式在本機，[看到 hello 一般的升級指導方針](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general)。</span><span class="sxs-lookup"><span data-stu-id="ef302-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="ef302-292">本機開發網站升級之後，將發行 hello 變更 toohello 臨時 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="ef302-293">測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-293">Test your application.</span></span> <span data-ttu-id="ef302-294">如果一切看來正常，使用 hello**交換**按鈕 tooswap 預備網站 toohello 生產 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef302-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="ef302-295">當您使用 hello**交換**作業，您可以檢視將受到影響的 hello 變更 web 應用程式的組態中。</span><span class="sxs-lookup"><span data-stu-id="ef302-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="ef302-296">這**交換**作業交換 hello web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="ef302-297">之後 hello**交換**、 hello 實際執行 web 應用程式將點 toohello umbraco 階段資料庫的資料庫，以及 hello 臨時 web 應用程式將點 tooumbraco-prod db 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![交換部署 Umbraco CMS 的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="ef302-299">以下是交換 hello web 應用程式和 hello 資料庫的優點：</span><span class="sxs-lookup"><span data-stu-id="ef302-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="ef302-300">您可以復原舊版 web 應用程式與另一個 toohello**交換**是否有任何應用程式問題。</span><span class="sxs-lookup"><span data-stu-id="ef302-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="ef302-301">進行升級時，您需要 toodeploy 檔案和資料庫從臨時 web 應用程式 toohello 生產環境 web 應用程式的 hello 和資料庫。</span><span class="sxs-lookup"><span data-stu-id="ef302-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="ef302-302">當您部署檔案和資料庫時，有許多情況可能發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="ef302-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="ef302-303">使用 hello**交換**功能的位置，我們可以在升級期間的停機時間減少，降低 hello 風險的部署變更時所發生的失敗。</span><span class="sxs-lookup"><span data-stu-id="ef302-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="ef302-304">您可以**A / B 測試**使用 hello[在生產環境中測試](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/)功能。</span><span class="sxs-lookup"><span data-stu-id="ef302-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="ef302-305">此範例所示 hello hello 平台，您可以建置自訂模組類似 tooUmbraco 新細明體模組 toomanage 部署環境之間的彈性。</span><span class="sxs-lookup"><span data-stu-id="ef302-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="ef302-306">參考</span><span class="sxs-lookup"><span data-stu-id="ef302-306">References</span></span>
[<span data-ttu-id="ef302-307">敏捷式軟體開發 (Agile Software Development) 與 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ef302-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="ef302-308">針對 Azure App Service 中的 Web 應用程式設定預備環境</span><span class="sxs-lookup"><span data-stu-id="ef302-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="ef302-309">如何 tooblock web 存取 toonon 生產部署位置</span><span class="sxs-lookup"><span data-stu-id="ef302-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
