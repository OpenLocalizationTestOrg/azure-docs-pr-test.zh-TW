---
title: "為 Web 應用程式有效地使用 DevOps 環境 | Microsoft Docs"
description: "了解如何使用部署位置來設定和管理應用程式的多個開發環境"
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
ms.openlocfilehash: 25248411659f6c7b2e386e310428c365c44ea2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="4c6d5-103">為 Web 應用程式有效地使用 DevOps 環境</span><span class="sxs-lookup"><span data-stu-id="4c6d5-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="4c6d5-104">本文將說明當應用程式的多個版本在不同環境時 (例如開發、預備、品質保證 (QA) 和生產)，如何設定和管理 Web 應用程式部署。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-104">This article shows you how to set up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="4c6d5-105">您應用程式的每個版本可視為適用於部署程序之特定用途的開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-105">Each version of your application can be considered as a development environment for the specific purpose of your deployment process.</span></span> <span data-ttu-id="4c6d5-106">例如，開發人員可以使用 QA 環境來測試應用程式的品質，之後才將變更推入至生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-106">For example, developers can use the QA environment to test the quality of the application before they push the changes to production.</span></span>
<span data-ttu-id="4c6d5-107">多個開發環境是具挑戰性的工作，因為您需要追蹤程式碼、管理資源 (計算、Web 應用程式、資料庫、快取等) 和跨環境部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-107">Multiple development environments can be a challenge because you need to track code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="4c6d5-108">設定非生產環境 (預備、開發、QA)</span><span class="sxs-lookup"><span data-stu-id="4c6d5-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="4c6d5-109">生產 Web 應用程式啟動並執行之後，下一步是建立非生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-109">After a production web app is up and running, the next step is to create a non-production environment.</span></span> <span data-ttu-id="4c6d5-110">若要使用部署位置，請確定您在標準或進階 Azure App Service 方案模式中執行。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-110">To use deployment slots, make sure that you are running in the Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="4c6d5-111">部署位置是具有專屬主機名稱的即時 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="4c6d5-112">兩個部署位置 (包括生產位置) 之間的 Web 應用程式內容與設定項目可以互相交換。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-112">Web app content and configuration elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="4c6d5-113">當您將應用程式部署到部署位置時，會有下列優點：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-113">When you deploy your application to a deployment slot, you get the following benefits:</span></span>

- <span data-ttu-id="4c6d5-114">您可以在預備部署位置中驗證 Web 應用程式的變更，之後再將應用程式與生產位置交換。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-114">You can validate changes to a web app in a staging deployment slot before you swap the app with the production slot.</span></span>
- <span data-ttu-id="4c6d5-115">當您將 Web 應用程式先部署至某個位置，然後再將它交換到生產位置時，該位置的所有執行個體在交換到生產位置之前都已準備就緒。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-115">When you deploy a web app to a slot first and swap it into production, all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="4c6d5-116">此程序可排除部署 Web 應用程式時的停機情況。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="4c6d5-117">流量能夠順暢地重新導向，且不會因為交換作業而捨棄任何要求。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-117">The traffic redirection is seamless, and no requests are dropped due to swap operations.</span></span> <span data-ttu-id="4c6d5-118">若要自動化這整個工作流程，請在不需要預先交換驗證時設定[自動交換](web-sites-staged-publishing.md#configure-auto-swap)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-118">To automate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="4c6d5-119">交換之後，含有之前預備 Web 應用程式的位置，現已擁有之前的生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-119">After a swap, the slot that has the previously staged web app now has the previous production web app.</span></span> <span data-ttu-id="4c6d5-120">若交換到生產位置的變更不是您需要的變更，您可以立即執行相同的交換，以取回「上一個已知良好的」Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-120">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good" web app back.</span></span>

<span data-ttu-id="4c6d5-121">若要設定預備部署位置，請參閱[針對 Azure App Service 中的 Web 應用程式設定預備環境](web-sites-staged-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-121">To set up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="4c6d5-122">每個環境都應該包含專屬的一組資源。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="4c6d5-123">例如，如果 Web 應用程式使用資料庫，則生產和預備 Web 應用程式就應該使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="4c6d5-124">新增預備開發環境資源 (例如資料庫、儲存體或快取) 以設定您的預備開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-124">Add staging development environment resources such as database, storage, or cache to set your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="4c6d5-125">使用多個開發環境的範例</span><span class="sxs-lookup"><span data-stu-id="4c6d5-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="4c6d5-126">任何專案都應該至少有兩個環境應遵循原始程式碼管理：開發和生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="4c6d5-127">如果您使用內容管理系統 (CMS)、應用程式架構等等，在不進行自訂的情況下，應用程式可能無法支援此案例。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-127">If you use content management systems (CMSs), application frameworks, etc., the application might not support this scenario without customization.</span></span> <span data-ttu-id="4c6d5-128">此問題常見於一些熱門的架構，我們將在下列數節中討論。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-128">This eventuality is true for some of the popular frameworks that are discussed in the following sections.</span></span> <span data-ttu-id="4c6d5-129">使用 CMS/架構時會浮現很多問題，例如：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-129">Lots of questions come to mind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="4c6d5-130">如何將內容分散到不同環境中？</span><span class="sxs-lookup"><span data-stu-id="4c6d5-130">How do you break the content out into different environments?</span></span>
- <span data-ttu-id="4c6d5-131">可以變更哪些檔案而不影響架構版本更新？</span><span class="sxs-lookup"><span data-stu-id="4c6d5-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="4c6d5-132">如何管理各環境的設定？</span><span class="sxs-lookup"><span data-stu-id="4c6d5-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="4c6d5-133">如何為模組、外掛程式及核心架構管理版本更新？</span><span class="sxs-lookup"><span data-stu-id="4c6d5-133">How do you manage version updates for modules, plugins, and the core framework?</span></span>

<span data-ttu-id="4c6d5-134">有許多方法可以為專案設定多個環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-134">There are many ways to set up multiple environments for your project.</span></span> <span data-ttu-id="4c6d5-135">下列範例會針對個別應用程式逐一說明方法。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-135">The following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="4c6d5-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="4c6d5-136">WordPress</span></span>
<span data-ttu-id="4c6d5-137">在本節中，您將學習如何使用 WordPress 位置來設定部署工作流程。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-137">In this section, you will learn how to set up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="4c6d5-138">WordPress 如同大部分的 CMS 解決方案，在不進行自訂的情況下將不支援多個開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="4c6d5-139">Azure App Service 的 Web Apps 功能，有一些功能可讓您更輕鬆地將組態設定儲存在您的程式碼之外。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-139">The Web Apps feature of Azure App Service has a few features that make it easy to store configuration settings outside your code.</span></span>

1. <span data-ttu-id="4c6d5-140">在您建立預備位置之前，請先設定應用程式程式碼來支援多個環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-140">Before you create a staging slot, set up your application code to support multiple environments.</span></span> <span data-ttu-id="4c6d5-141">若要在 WordPress 中支援多個環境，您需要在您的本機開發 Web 應用程式上編輯 `wp-config.php`，並在檔案的開頭加入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-141">To support multiple environments in WordPress, you need to edit `wp-config.php` on your local development web app and add the following code at the beginning of the file.</span></span> <span data-ttu-id="4c6d5-142">此程序這會讓您的應用程式根據所選環境挑選正確的組態。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-142">This process will enable your application to pick the correct configuration based on the selected environment.</span></span>

    ```
    // Support multiple environments
    // set the config file based on current environment
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
    // include the config file if it exists, otherwise WP is going to fail
    require_once $path. $config_file;
    ```

2. <span data-ttu-id="4c6d5-143">在 Web 應用程式根目錄下建立名為 `config` 的資料夾，並新增 `wp-config.azure.php` 和 `wp-config.local.php` 檔案，它們分別代表 Azure 環境和本機環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-143">Create a folder under web app root called `config`, and add the `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="4c6d5-144">複製 `wp-config.local.php` 中的下列項目：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-144">Copy the following in `wp-config.local.php`:</span></span>

    ```
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this to true to enable the display of notices during development.
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

    <span data-ttu-id="4c6d5-145">設定上述程式碼中的安全性金鑰可以協助防止 Web 應用程式受到駭客攻擊，因此請使用唯一值。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-145">Setting the security keys as illustrated in the previous code can help to prevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="4c6d5-146">如果您需要為程式碼中所述的安全性金鑰產生字串，您可[透過自動產生器 (英文)](https://api.wordpress.org/secret-key/1.1/salt) 來產生新的金鑰/值組。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-146">If you need to generate the string for security keys mentioned in the code, you can [go to the automatic generator](https://api.wordpress.org/secret-key/1.1/salt) to create new key/value pairs.</span></span>

4. <span data-ttu-id="4c6d5-147">複製 `wp-config.azure.php`中的下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-147">Copy the following code in `wp-config.azure.php`:</span></span>

    ```    
    <?php
    // MySQL settings
    /** The name of the database for WordPress */

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
    * Change this to true to enable the display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging to investigate issues without displaying to end user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on the page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need to generate the string for security keys mentioned above, you can go the automatic generator to create new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
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

#### <a name="use-relative-paths"></a><span data-ttu-id="4c6d5-148">使用相對路徑</span><span class="sxs-lookup"><span data-stu-id="4c6d5-148">Use relative paths</span></span>
<span data-ttu-id="4c6d5-149">最後一件事是將 WordPress 應用程式設定為使用相對路徑。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-149">One last thing to configure in the WordPress app is relative paths.</span></span> <span data-ttu-id="4c6d5-150">WordPress 會在資料庫中儲存 URL 資訊。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-150">WordPress stores URL information in the database.</span></span> <span data-ttu-id="4c6d5-151">這種儲存方式會使將內容從一個環境移至另一個環境變得更加困難。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-151">This storage makes moving content from one environment to another more difficult.</span></span> <span data-ttu-id="4c6d5-152">每當您從本機移至預備環境，或是從預備環境移至生產環境時，都必須更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-152">You need to update the database every time you move from local to stage or stage to production environments.</span></span> <span data-ttu-id="4c6d5-153">若要減少每次在不同環境間部署資料庫時可能造成問題的風險，請使用[相對根連結外掛程式 (英文)](https://wordpress.org/plugins/root-relative-urls/)，您可以使用 WordPress 管理員儀表板來安裝它。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-153">To reduce the risk of issues that can be caused with deploying a database every time you deploy from one environment to another, use the [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using the WordPress administrator dashboard.</span></span>

<span data-ttu-id="4c6d5-154">將下列項目加入至您的 `wp-config.php` 檔案中 `That's all, stop editing!` 註解之前：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-154">Add the following entries to your `wp-config.php` file before the `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="4c6d5-155">透過 WordPress 管理員儀表板中的 `Plugins` 功能表啟用外掛程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-155">Activate the plugin through the `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="4c6d5-156">儲存您的永久連結設定供 WordPress 應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="the-final-wp-configphp-file"></a><span data-ttu-id="4c6d5-157">最終 `wp-config.php` 檔案</span><span class="sxs-lookup"><span data-stu-id="4c6d5-157">The final `wp-config.php` file</span></span>
<span data-ttu-id="4c6d5-158">任何 WordPress 核心更新並不會影響您的 `wp-config.php`、`wp-config.azure.php` 和 `wp-config.local.php` 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="4c6d5-159">以下是 `wp-config.php` 檔案的最終版本：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-159">Here's a final version of the `wp-config.php` file:</span></span>

```
<?php
/**
 * The base configurations of the WordPress.
 *
 * This file has the following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get the MySQL settings from your web host.
 *
 * This file is used by the wp-config.php creation script during the
 * installation. You don't have to use the web web app, you can just copy this file
 * to "wp-config.php" and fill in the values.
 *
 * @package WordPress
 */

// Support multiple environments
// set the config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include the config file if it exists, otherwise WP is going to fail
  require_once $path. $config_file;
}

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="4c6d5-160">設定預備環境</span><span class="sxs-lookup"><span data-stu-id="4c6d5-160">Set up a staging environment</span></span>
1. <span data-ttu-id="4c6d5-161">如果您已經在 Azure 訂用帳戶中執行 WordPress Web 應用程式，請登入 [Azure 入口網站](http://portal.azure.com)，然後移至 WordPress Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-161">If you already have a WordPress web app running on your Azure subscription, sign in to the [Azure portal](http://portal.azure.com), and then go to your WordPress web app.</span></span> <span data-ttu-id="4c6d5-162">如果您沒有 WordPress Web 應用程式，您可以從 Azure Marketplace 建立一個。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-162">If you don't have a WordPress web app, you can create one from the Azure Marketplace.</span></span> <span data-ttu-id="4c6d5-163">若要深入了解，請參閱[在 Azure App Service 中建立 WordPress Web 應用程式](web-sites-php-web-site-gallery.md)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-163">To learn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="4c6d5-164">按一下 [設定]  >  [部署位置]  >  [新增] 來建立名稱為 *stage* 的部署位置。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-164">Click **Settings** > **Deployment slots** > **Add** to create a deployment slot with the name *stage*.</span></span> <span data-ttu-id="4c6d5-165">部署位置是與您之前建立的主要 Web 應用程式共用相同資源的另一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-165">A deployment slot is another web application that shares the same resources as the primary web app that you created previously.</span></span>

    ![建立階段部署位置](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="4c6d5-167">將另一個 MySQL 資料庫 (假設為 `wordpress-stage-db`) 加入至您的資源群組 `wordpressapp-group`。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-167">Add another MySQL database, say `wordpress-stage-db`, to your resource group, `wordpressapp-group`.</span></span>

    ![將 MySQL 資料庫新增至資源群組](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="4c6d5-169">將預備部署位置的連接字串更新，以指向新的資料庫 `wordpress-stage-db`。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-169">Update the connection strings for your stage deployment slot to point to the new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="4c6d5-170">您的生產 Web 應用程式 `wordpressprodapp` 和預備 Web 應用程式 `wordpressprodapp-stage` 必須指向不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point to different databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="4c6d5-171">設定環境特定的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="4c6d5-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="4c6d5-172">開發人員可以隨著與 Web 應用程式相關聯的組態資訊 (稱為「應用程式設定」) 在 Azure 中儲存索引鍵/值字串組。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-172">Developers can store key/value string pairs in Azure as part of the configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="4c6d5-173">在執行階段，Web 應用程式會為您自動擷取這些值，並使該值可供您 Web 應用程式中執行的程式碼使用。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-173">At runtime, web apps automatically retrieve these values and make them available to code that's running in your web app.</span></span> <span data-ttu-id="4c6d5-174">從安全性觀點來看，這是不錯的附帶效益，因為資料庫連接字串與密碼之類的機密資訊永遠不會在檔案 (例如 `wp-config.php`) 中顯示為純文字。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="4c6d5-175">在下列段落中說明的這個程序非常實用，因為它同時包含 WordPress 應用程式的檔案變更和資料庫變更：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-175">This process, which is explained in the following paragraphs, is useful because it includes both file changes and database changes for the WordPress app:</span></span>

* <span data-ttu-id="4c6d5-176">WordPress 版本升級</span><span class="sxs-lookup"><span data-stu-id="4c6d5-176">WordPress version upgrade</span></span>
* <span data-ttu-id="4c6d5-177">加入新的或編輯或升級外掛程式</span><span class="sxs-lookup"><span data-stu-id="4c6d5-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="4c6d5-178">加入新的或編輯或升級佈景主題</span><span class="sxs-lookup"><span data-stu-id="4c6d5-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="4c6d5-179">設定下列項目的應用程式設定：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-179">Configure app settings for:</span></span>

* <span data-ttu-id="4c6d5-180">資料庫資訊</span><span class="sxs-lookup"><span data-stu-id="4c6d5-180">Database information</span></span>
* <span data-ttu-id="4c6d5-181">開啟/關閉 WordPress 記錄</span><span class="sxs-lookup"><span data-stu-id="4c6d5-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="4c6d5-182">WordPress 安全性設定</span><span class="sxs-lookup"><span data-stu-id="4c6d5-182">WordPress security settings</span></span>

![Wordpress Web 應用程式的應用程式設定](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="4c6d5-184">請確定您為您的生產 Web 應用程式和預備位置加入下列應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-184">Make sure that you add the following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="4c6d5-185">請注意，生產 Web 應用程式和預備 Web 應用程式使用不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-185">Note that the production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="4c6d5-186">清除 WP_ENV 以外所有設定參數的 [位置設定] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-186">Clear the **Slot Setting** checkbox for all the settings parameters except WP_ENV.</span></span> <span data-ttu-id="4c6d5-187">這個程序將會交換 Web 應用程式的組態、檔案內容和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-187">This process will swap the configuration for your web app, file content, and database.</span></span> <span data-ttu-id="4c6d5-188">如果已選取 [位置設定]，執行「交換」作業時，Web 應用程式的應用程式設定、連接字串組態將「不會」跨環境移動。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-188">If **Slot Setting** is checked, the web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="4c6d5-189">任何的資料庫變更將不會中斷您的生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="4c6d5-190">使用 WebMatrix 或您選擇的工具 (例如 FTP、Git 或 PhpMyAdmin)，將本機開發環境 Web 應用程式部署到預備 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-190">Deploy the local development environment web app to the stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![WordPress Web 應用程式的 WebMatrix 發佈對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="4c6d5-192">瀏覽及測試您的預備 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-192">Browse and test your staging web app.</span></span> <span data-ttu-id="4c6d5-193">假設我們要更新 Web 應用程式的佈景主題，以下是預備的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-193">Considering a scenario where the theme of the web app is to be updated, here is the staging web app.</span></span>

    ![交換位置之前瀏覽預備 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="4c6d5-195">如果一切已就緒，請在預備 Web 應用程式上按一下 [交換] 按鈕，將您的內容移到生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-195">If all looks good, click the **Swap** button on your staging web app to move your content to the production environment.</span></span> <span data-ttu-id="4c6d5-196">在此情況下，您會在每個「交換」作業期間交換環境之間的 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-196">In this case, you swap the web app and the database across environments during every **Swap** operation.</span></span>

    ![交換 WordPress 的變更的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="4c6d5-198">如果您的案例只需要推送檔案 (沒有資料庫更新)，那麼請在執行「交換」之前，於 Azure 入口網站 [Web 應用程式設定] 刀鋒視窗中選取與所有資料庫相關的 [應用程式設定] 和 [連接字串設定] 的 [位置設定]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-198">If your scenario needs to only push files (no database updates), then check **Slot Setting** for all the database-related *app settings* and *connection strings settings* in the **Web App Settings** blade within the Azure portal before doing the **Swap**.</span></span> <span data-ttu-id="4c6d5-199">在此情況下，DB_NAME、DB_HOST、DB_PASSWORD、DB_USER 預設連接字串設定在執行**交換**的時候應該不會顯示在預覽變更中。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="4c6d5-200">在此時，當您完成「交換」作業，WordPress Web 應用程式將只會更新檔案。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-200">At this time, when you complete the **Swap** operation, the WordPress web app will have the updates files only.</span></span>
    >
    >

    <span data-ttu-id="4c6d5-201">執行「交換」之前，這裡是生產 WordPress Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-201">Before doing a **Swap**, here is the production WordPress web app.</span></span>
    <span data-ttu-id="4c6d5-202">![交換位置之前的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="4c6d5-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="4c6d5-203">在「交換」作業之後，佈景主題已在您的生產 Web 應用程式上更新。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-203">After the **Swap** operation, the theme has been updated on your production web app.</span></span>

    ![交換位置之後的生產 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="4c6d5-205">當您需要回復時，您可以移至生產 Web [應用程式設定]，並按一下 [交換] 按鈕，將 Web 應用程式與資料庫從生產交換至預備位置。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-205">When you need to roll back, you can go to the production web **App Settings**, and click the **Swap** button to swap the web app and database from production to staging slot.</span></span> <span data-ttu-id="4c6d5-206">請記住，只要「交換」作業伴隨有資料庫變更，則在下次重新部署至預備 Web 應用程式時，您就必須將資料庫變更部署到預備 Web 應用程式目前的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-206">Remember that if database changes are included with a **Swap** operation, then the next time you deploy to your staging web app, you need to deploy the database changes to the current database for your staging web app.</span></span> <span data-ttu-id="4c6d5-207">目前的資料庫可能是先前的生產資料庫或預備資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-207">The current database might be the previous production database or the stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="4c6d5-208">摘要</span><span class="sxs-lookup"><span data-stu-id="4c6d5-208">Summary</span></span>
<span data-ttu-id="4c6d5-209">以下是適用於任何具有資料庫之應用程式的通用程序：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="4c6d5-210">在本機環境上安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-210">Install the application on your local environment.</span></span>
2. <span data-ttu-id="4c6d5-211">包含環境特定組態 (本機和 Azure Web Apps)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="4c6d5-212">針對 Web Apps 設定預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="4c6d5-213">如果您已經在 Azure 上執行生產應用程式，請將您的生產內容 (檔案/程式碼和資料庫) 同步到本機和預備環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-213">If you have a production application already running on Azure, sync your production content (files/code and database) to local and staging environments.</span></span>
5. <span data-ttu-id="4c6d5-214">在您的本機環境上開發應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="4c6d5-215">將您的生產 Web 應用程式置於維護或鎖定模式，並將資料庫內容從生產環境同步到預備環境和開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-215">Place your production web app under maintenance or locked mode, and sync database content from production to staging and dev environments.</span></span>
7. <span data-ttu-id="4c6d5-216">部署至預備環境並測試。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-216">Deploy to the staging environment and test.</span></span>
8. <span data-ttu-id="4c6d5-217">部署至生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-217">Deploy to production environment.</span></span>
9. <span data-ttu-id="4c6d5-218">重複步驟 4 至 6。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="4c6d5-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="4c6d5-219">Umbraco</span></span>
<span data-ttu-id="4c6d5-220">在本節中，您將了解 Umbraco CMS 如何使用自訂模組在多個 DevOps 環境間進行部署。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-220">In this section, you will learn how the Umbraco CMS uses a custom module to deploy across multiple DevOps environments.</span></span> <span data-ttu-id="4c6d5-221">此範例將提供不同的方法來管理多個開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-221">This example provides a different approach to managing multiple development environments.</span></span>

<span data-ttu-id="4c6d5-222">[Umbraco CMS (英文)](http://umbraco.com/) 是許多開發人員常用的 .NET CMS 解決方案。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="4c6d5-223">它提供 [Courier2 (英文)](http://umbraco.com/products/more-add-ons/courier-2) 模組，可從開發環境部署到預備環境或生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-223">It provides the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module to deploy from development to staging to production environments.</span></span> <span data-ttu-id="4c6d5-224">您可以使用 Visual Studio 或 WebMatrix，輕鬆地建立 Umbraco CMS Web 應用程式的本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="4c6d5-225">使用 Visual Studio 建立 Umbraco Web 應用程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="4c6d5-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="4c6d5-226">使用 WebMatrix 建立 Umbraco Web 應用程式 (英文)</span><span class="sxs-lookup"><span data-stu-id="4c6d5-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="4c6d5-227">務必記得移除應用程式下的 `install` 資料夾，而且永遠不要將它上傳至預備或生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-227">Always remember to remove the `install` folder under your application, and never upload it to stage or production web apps.</span></span> <span data-ttu-id="4c6d5-228">本教學課程使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="4c6d5-229">設定預備環境</span><span class="sxs-lookup"><span data-stu-id="4c6d5-229">Set up a staging environment</span></span>
1. <span data-ttu-id="4c6d5-230">如上所述為 Umbraco CMS Web 應用程式建立部署位置 (假設您已有 Umbraco CMS Web 應用程式運作且執行中)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-230">Create a deployment slot as mentioned previously for the Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="4c6d5-231">如果沒有，您可以從 Marketplace 建立一個。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-231">If you do not, you can create one from the Marketplace.</span></span>
2. <span data-ttu-id="4c6d5-232">將預備部署位置的連接字串更新，以指向新的 **umbraco-stage-db** 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-232">Update the connection string for your stage deployment slot to point to the new **umbraco-stage-db** database.</span></span> <span data-ttu-id="4c6d5-233">您的生產 Web 應用程式 (umbraositecms-1) 和預備 Web 應用程式 (umbracositecms-1-stage)「必須」指向不同的資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point to different databases.</span></span>

    ![使用新預備資料庫更新預備 Web 應用程式的連接字串](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="4c6d5-235">按一下部署位置 **stage** 的 [取得發佈設定]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-235">Click **Get Publish settings** for the deployment slot **stage**.</span></span> <span data-ttu-id="4c6d5-236">此程序會下載發佈設定檔，它可儲存 Visual Studio 或 WebMatrix 將您的應用程式從本機開發 Web 應用程式發佈到 Azure Web 應用程式所需的一切資訊。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-236">This process will download a publish settings file that stores all the information that Visual Studio or WebMatrix requires to publish your application from the local development web app to the Azure web app.</span></span>

    ![取得預備 Web 應用程式的發佈設定](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="4c6d5-238">在 WebMatrix 或 Visual Studio 中開啟您的本機開發 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="4c6d5-239">本教學課程使用 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="4c6d5-240">首先，您必須為您的預備 Web 應用程式匯入發佈設定檔。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-240">First, you need to import the publish settings file for your staging web app.</span></span>

    ![使用 WebMatrix 匯入 Umbraco 的發佈設定](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="4c6d5-242">在對話方塊中檢閱變更，並將本機 Web 應用程式部署至您的 Azure Web 應用程式 *umbracositecms-1-stage*。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-242">Review changes in the dialog box, and deploy your local web app to your Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="4c6d5-243">當您將檔案直接部署到預備 Web 應用程式時，會略過 `~/app_data/TEMP/` 資料夾中的任何檔案，因為這些檔案將在預備 Web 應用程式首次啟動時重新產生。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-243">When you deploy files directly to your staging web app, you will omit files in the `~/app_data/TEMP/` folder because these files will be regenerated when the stage web app is first started.</span></span> <span data-ttu-id="4c6d5-244">您也應該省略 `~/app_data/umbraco.config` 檔案，該檔案也將重新產生。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-244">You should also omit the `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![在 WebMatrix 中檢閱發佈變更](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="4c6d5-246">在您成功發佈 Umbraco 本機 Web 應用程式至預備 Web 應用程式之後，請瀏覽至預備 Web 應用程式，並執行一些測試來排除任何問題。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-246">After you successfully publish the Umbraco local web app to the staging web app, browse to your staging web app, and run a few tests to rule out any issues.</span></span>

#### <a name="set-up-the-courier2-deployment-module"></a><span data-ttu-id="4c6d5-247">設定 Courier2 部署模組</span><span class="sxs-lookup"><span data-stu-id="4c6d5-247">Set up the Courier2 deployment module</span></span>
<span data-ttu-id="4c6d5-248">透過 [Courier2 (英文)](http://umbraco.com/products/more-add-ons/courier-2) 模組，您只要以右鍵按一下即可從預備 Web 應用程式將內容、樣式表及部署模組推送到生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-248">With the [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click to push content, style sheets, and development modules from a staging web app to a production web app.</span></span> <span data-ttu-id="4c6d5-249">此程序可以降低在部署更新時中斷生產 Web 應用程式的風險。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-249">This process reduces the risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="4c6d5-250">針對 `*.azurewebsites.net` 網域和您的自訂網域 (假設為 http://abc.com) 購買 Courier2 授權。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-250">Purchase a license for Courier2 for the `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="4c6d5-251">購買授權後，將下載的授權 (.LIC 檔案) 放置到 `bin` 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-251">After you purchase the license, place the downloaded license (.LIC file) in the `bin` folder.</span></span>

![將授權檔案拖放到 bin 資料夾下](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="4c6d5-253">[下載 Courier2 套件 (英文)](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-253">[Download the Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="4c6d5-254">登入您的預備 Web 應用程式 (假設是 http://umbracocms-site-stage.azurewebsites.net/umbraco)，按一下 [開發人員] 功能表然後按一下 [套件]  >  [安裝本機套件]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-254">Sign in to your stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click the **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Umbraco 套件安裝程式](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="4c6d5-256">使用安裝程式將 Courier2 套件上傳。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-256">Upload the Courier2 package by using the installer.</span></span>

    ![上傳 courier 模組的套件](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="4c6d5-258">若要設定套件，您必須更新 Web 應用程式 [Config] 資料夾下的 courier.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-258">To configure the package, you need to update the courier.config file under the **Config** folder of your web app.</span></span>

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. <span data-ttu-id="4c6d5-259">在 `<repositories>`底下，輸入生產網站 URL 和使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-259">Under `<repositories>`, enter the production site URL and user information.</span></span>
    <span data-ttu-id="4c6d5-260">如果您使用預設 Umbraco 成員資格提供者，則請在 &lt;user&gt; 區段中新增管理員使用者的識別碼。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-260">If you are using the default Umbraco membership provider, then add the ID for the Administration user in the &lt;user&gt; section.</span></span>
    <span data-ttu-id="4c6d5-261">如果您使用自訂 Umbraco 成員資格提供者，請使用 Courier2 模組中的 `<login>`、`<password>` 來連接到生產網站。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in the Courier2 module to connect to the production site.</span></span>
    <span data-ttu-id="4c6d5-262">如需詳細資訊，[請檢閱 Courier2 模組的文件 (英文)](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-262">For more details, [review the documentation for the Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="4c6d5-263">同樣地，請在您的生產網站上安裝 Courier2 模組，並如此處所示，將其設定為在各自的 courier.config 檔案中指向預備 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-263">Similarly, install the Courier2 module on your production site, and configure it to point to the stage web app in its respective courier.config file as shown here.</span></span>

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how to connect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set the passwordEncoding to clear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. <span data-ttu-id="4c6d5-264">在 Umbraco CMS Web 應用程式儀表板中的 [Courier2] 索引標籤上按一下，並選取 [位置]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-264">Click the **Courier2** tab in the Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="4c6d5-265">您應該會看到 `courier.config`中所提及的儲存機制名稱。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-265">You should see the repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="4c6d5-266">請在生產和預備 Web 應用程式上執行此程序。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-266">Do this process on both your production and staging web apps.</span></span>

    ![檢視目的地 Web 應用程式儲存機制](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="4c6d5-268">若要將內容從預備網站部署至生產網站，請移至 [內容]，然後選取現有的頁面或建立新頁面。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-268">To deploy content from the staging site to the production site, go to **Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="4c6d5-269">我將從我的 Web 應用程式選取現有的網頁 (其中頁面的標題會是「開始使用 - 新增」)，接著按一下 [儲存並發佈]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-269">I will select an existing page from my web app where the title of the page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![變更頁面的標題並發佈](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="4c6d5-271">以滑鼠右鍵按一下已修改的頁面來檢視所有選項。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-271">Right-click the modified page to view all the options.</span></span> <span data-ttu-id="4c6d5-272">按一下 [Courier] 開啟 [部署] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-272">Click **Courier** to open the **Deployment** dialog box.</span></span> <span data-ttu-id="4c6d5-273">按一下 [部署] 來起始部署。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-273">Click **Deploy** to initiate deployment.</span></span>

    ![Courier 模組部署對話方塊](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="4c6d5-275">檢閱變更，然後按一下 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-275">Review the changes, and then click **Continue**.</span></span>

    ![Courier 模組部署對話方塊檢閱變更](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="4c6d5-277">部署記錄檔會顯示部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-277">The deployment log shows if the deployment was successful.</span></span>

     ![檢視 Courier 模組的部署記錄檔](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="4c6d5-279">瀏覽您的生產 Web 應用程式以查看是否反映了變更。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-279">Browse your production web app to see if the changes are reflected.</span></span>

     ![瀏覽實際執行 Web 應用程式](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="4c6d5-281">若要深入了解如何使用 Courier，請檢閱文件集。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-281">To learn more about how to use Courier, review the documentation.</span></span>

#### <a name="how-to-upgrade-the-umbraco-cms-version"></a><span data-ttu-id="4c6d5-282">如何升級 Umbraco CMS 版本</span><span class="sxs-lookup"><span data-stu-id="4c6d5-282">How to upgrade the Umbraco CMS version</span></span>
<span data-ttu-id="4c6d5-283">從某個版本的 Umbraco CMS 升級至另一個版本時，Courier 並沒有幫助。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-283">Courier will not help you upgrade from one version of Umbraco CMS to another.</span></span> <span data-ttu-id="4c6d5-284">升級 Umbraco CMS 版本時，您必須檢查與您的自訂模組或合作夥伴模組和 Umbraco 核心程式庫的不相容項目。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and the Umbraco Core libraries.</span></span> <span data-ttu-id="4c6d5-285">以下是最佳作法：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-285">Here are best practices:</span></span>

* <span data-ttu-id="4c6d5-286">務必在升級之前備份您的 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="4c6d5-287">在 Azure 中的 Web 應用程式上，您可以使用備份功能設定網站的自動備份，並在需要時使用還原功能還原您的網站。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-287">On web apps in Azure, you can set up automatic backups for your websites by using the backup feature and restore your site if needed by using the restore feature.</span></span> <span data-ttu-id="4c6d5-288">如需詳細資訊，請參閱[如何備份您的 Web 應用程式](web-sites-backup.md)和[如何還原您的 Web 應用程式](web-sites-restore.md)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-288">For more details, see [How to back up your web app](web-sites-backup.md) and [How to restore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="4c6d5-289">檢查您要升級的版本是否與合作夥伴的套件相容。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-289">Check if packages from partners are compatible with the version you're upgrading to.</span></span> <span data-ttu-id="4c6d5-290">在套件的下載頁面，檢閱與 Umbraco CMS 版本的專案相容性。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-290">On the package's download page, review the project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="4c6d5-291">如需如何在本機升級 Web 應用程式的詳細資料，[請參閱一般升級指導方針 (英文)](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-291">For more details about how to upgrade your web app locally, [see the general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="4c6d5-292">在本機開發網站升級之後，將變更發佈至預備 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-292">After your local development site is upgraded, publish the changes to the staging web app.</span></span> <span data-ttu-id="4c6d5-293">測試您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-293">Test your application.</span></span> <span data-ttu-id="4c6d5-294">如果一切看起來正常，請使用 [交換] 按鈕，將預備網站交換為生產 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-294">If all looks good, use the **Swap** button to swap your staging site to the production web app.</span></span> <span data-ttu-id="4c6d5-295">使用「交換」作業時，您可以檢視將在您的 Web 應用程式組態中受到影響的變更。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-295">When you use the **Swap** operation, you can view the changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="4c6d5-296">此「交換」作業會交換 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-296">This **Swap** operation swaps the web apps and databases.</span></span> <span data-ttu-id="4c6d5-297">在「交換」之後，生產 Web 應用程式會指向 umbraco-stage-db 資料庫，而預備 Web 應用程式會指向 umbraco-prod-db 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-297">After the **Swap**, the production web app will point to the umbraco-stage-db database, and the staging web app will point to umbraco-prod-db database.</span></span>

![交換部署 Umbraco CMS 的預覽](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="4c6d5-299">以下為交換 Web 應用程式和資料庫的優點：</span><span class="sxs-lookup"><span data-stu-id="4c6d5-299">Here are advantages of swapping both the web app and the database:</span></span>

* <span data-ttu-id="4c6d5-300">如果發生任何應用程式問題，您可以利用另一個「交換」回復至舊版的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-300">You can roll back to the previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="4c6d5-301">針對升級，您需要將來自預備 Web 應用程式的檔案和資料庫部署到生產 Web 應用程式和資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-301">For an upgrade, you need to deploy files and databases from the staging web app to the production web app and database.</span></span> <span data-ttu-id="4c6d5-302">當您部署檔案和資料庫時，有許多情況可能發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="4c6d5-303">若使用位置的「交換」功能，我們就可以在升級期間減少停機時間，並降低部署變更時可能發生的失敗風險。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-303">By using the **Swap** feature of slots, we can reduce downtime during an upgrade and reduce the risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="4c6d5-304">您可以使用「在生產環境中測試」功能執行 [A/B 測試 (英文)](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/)。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-304">You can do **A/B testing** by using the [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="4c6d5-305">此範例將示範平台的彈性，讓您得以建置類似於 Umbraco Courier 模組的自訂模組，以便管理整個環境的部署。</span><span class="sxs-lookup"><span data-stu-id="4c6d5-305">This example shows you the flexibility of the platform where you can build custom modules similar to Umbraco Courier module to manage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="4c6d5-306">參考</span><span class="sxs-lookup"><span data-stu-id="4c6d5-306">References</span></span>
[<span data-ttu-id="4c6d5-307">敏捷式軟體開發 (Agile Software Development) 與 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4c6d5-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="4c6d5-308">針對 Azure App Service 中的 Web 應用程式設定預備環境</span><span class="sxs-lookup"><span data-stu-id="4c6d5-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="4c6d5-309">封鎖對非生產部署位置的 Web 存取</span><span class="sxs-lookup"><span data-stu-id="4c6d5-309">How to block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
