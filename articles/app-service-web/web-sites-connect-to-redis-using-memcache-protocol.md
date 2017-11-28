---
title: "aaaConnect 透過 hello Memcache 通訊協定-Azure App Service web 應用程式 tooRedis |Microsoft 文件"
description: "在 Azure 應用程式服務 tooRedis 快取中的 web 應用程式連接使用 hello Memcache 通訊協定"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 連接 web 應用程式透過 Memcache 通訊協定 hello Azure App Service tooRedis 快取中
在本文中，您將學習如何 tooconnect WordPress web 應用程式中的[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)太[Azure Redis 快取][ 12]使用 hello [Memcache] [ 13]通訊協定。 如果您有現有的 web 應用程式使用記憶體中快取的 Memcached 伺服器時，您可以移轉它，tooAzure 應用程式服務和使用 hello 第一方快取方案在 Microsoft Azure 中的有少量或沒有 tooyour 應用程式程式碼變更。 此外，您可以使用 Azure App Service 與 Azure Redis 快取中的現有 Memcache 專業 toocreate 可高度擴充、 分散式應用程式，進行記憶體中快取，同時使用常用應用程式架構，例如.NET、 PHP、 Node.js、 Java 和 Python。  

App Service Web 應用程式可讓這項搭配 hello Web 應用程式 Memcache 填充碼，當做呼叫 tooAzure Redis 快取的快取 Memcache proxy 是本機 Memcached 伺服器應用程式案例。 這可讓任何通訊使用 Redis 快取中的 hello Memcache 通訊協定 toocache 資料的應用程式。 此 Memcache 填充碼的運作在 hello 通訊協定層級，所以可以使用任何應用程式或應用程式架構，只要它使用 hello Memcache 通訊協定進行通訊。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## 必要條件
hello Web 應用程式 Memcache 填充碼都可以搭配任何應用程式提供通訊使用 hello Memcache 通訊協定。 針對此特定範例，hello 參考應用程式是可以從 hello Azure Marketplace 中佈建的可擴充 WordPress 站台。

請遵循下列文章中所述的 hello 步驟：

* [佈建 hello Azure Redis 快取服務執行的個體][0]
* [在 Azure 中部署可調整的 WordPress 網站][1]

一旦您擁有 hello 可擴充的 WordPress 網站部署和佈建的 Redis 快取執行個體將會準備 tooproceed 與啟用 Azure App Service Web 應用程式中的 hello Memcache 填充碼。

## 啟用 hello Web 應用程式 Memcache 填充碼
在訂單 tooconfigure Memcache 填充碼，您必須建立三個應用程式設定。 這可以使用各種不同的方法包括 hello [Azure 入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)，hello[傳統入口網站][3]，hello [Azure PowerShell Cmdlet] [ 5]或 hello [Azure 命令列介面][5]。 基於 hello 這篇文章，我們即將 toouse hello [Azure 入口網站][ 4] tooset hello 應用程式設定。 hello 下列值可從擷取**設定**Redis 快取執行個體的刀鋒視窗。

![Azure Redis 快取設定刀鋒視窗](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### 新增 REDIS_HOST 應用程式設定
hello 您所需要的第一個應用程式設定 toocreate 為 hello **REDIS\_主機**應用程式設定。 此設定會設定 hello 目的地 toowhich hello 填充碼轉送 hello 快取資訊。 hello 值所需 hello REDIS_HOST 應用程式設定可以擷取從 hello**屬性**Redis 快取執行個體的刀鋒視窗。

![Azure Redis 快取主機名稱](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

集 hello 索引鍵的 hello 應用程式設定過**REDIS\_主機**和 hello 應用程式設定 toohello hello 值**hostname** hello Redis 快取執行個體。

![Web 應用程式 AppSetting REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### 新增 REDIS_KEY 應用程式設定
hello 您所需要的第二個應用程式設定 toocreate 為 hello **REDIS\_金鑰**應用程式設定。 這項設定提供 hello 驗證權杖的必要的 toosecurely 存取 hello Redis 快取執行個體。 您可以擷取從 hello hello REDIS_KEY 應用程式設定所需的 hello 值**存取金鑰**刀鋒視窗中的 hello Redis 快取執行個體。

![Azure Redis 快取主要索引鍵](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

集 hello 索引鍵的 hello 應用程式設定過**REDIS\_金鑰**和 hello 應用程式設定 toohello hello 值**主索引鍵**hello Redis 快取執行個體。

![Azure 網站 AppSetting REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### 新增 MEMCACHESHIM_REDIS_ENABLE 應用程式設定
hello 最後一項應用程式設定為使用的 tooenable hello Memcache 填充碼，在 Web 應用程式，它會使用 hello REDIS_HOST 和 REDIS_KEY tooconnect toohello Azure Redis 快取和轉寄的 hello 快取的呼叫。 集 hello 索引鍵的 hello 應用程式設定過**MEMCACHESHIM\_REDIS\_啟用**和太 hello 值**true**。

![Web 應用程式 AppSetting MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

在您完成新增 hello 三 （3) 應用程式設定，請按一下**儲存**。

## 啟用適用於 PHP 的 Memcache 延伸模組
在 hello 應用程式 toospeak hello Memcache 通訊協定的順序，就需要 tooinstall hello Memcache 延伸 tooPHP-hello 語言架構，您的 WordPress 網站。

### 下載 hello php_memcache 延伸模組
瀏覽過[PECL][6]。 Hello 快取類別目錄，按一下 [ [memcache][7]。 在 [hello 下載欄按一下 hello DLL 連結。

![PHP PECL 網站](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

下載 PHP Web 應用程式中啟用的 hello 版的 hello 非執行緒安全 （來） x86 連結。 (預設為 PHP 5.4)

![PHP PECL 網站 Memcache 封裝](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### 啟用 hello php_memcache 擴充功能
下載 hello 檔案之後，解壓縮並上傳 hello **php\_memcache.dll**到 hello **d:\\家用\\網站\\wwwroot\\bin\\ext\\ **目錄。 Hello php_memcache.dll 會上傳到 hello web 應用程式之後，您會需要 tooenable hello 延伸 toohello PHP 執行階段。 tooenable hello Memcache 副檔名，在 Azure 入口網站中，開啟 hello hello**應用程式設定**刀鋒視窗中的 hello web 應用程式，然後加入新的應用程式設定 hello 索引鍵為**PHP\_延伸**和 hello值**bin\\ext\\php_memcache.dll**。

> [!NOTE]
> 如果 hello web 應用程式需要 tooload 多個 PHP 擴充功能，PHP_EXTENSIONS hello 值應該是以逗號分隔的相對路徑 tooDLL 檔案清單。
> 
> 

![Web 應用程式 AppSetting PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

完成後，按一下 [儲存] 。

## 安裝 Memcache WordPress 外掛程式
> [!NOTE]
> 您也可以下載 hello [Memcached 物件快取外掛程式](https://wordpress.org/plugins/memcached/)從 WordPress.org。
> 
> 

在 [hello WordPress 外掛程式] 頁面上，按一下 [**加入新**。

![WordPress 外掛程式頁面](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

在 [hello] 搜尋方塊中，輸入**memcached**按**Enter**。

![WordPress 新增新的外掛程式](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

尋找**Memcached 物件快取**在 hello] 清單中，然後按一下 [**立即安裝**。

![WordPress 安裝 Memcache 外掛程式](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### 啟用 hello Memcache WordPress 外掛程式
> [!NOTE]
> 依這個部落格中的 hello 指示[如何 tooenable Web 應用程式中的網站擴充功能][ 8] tooinstall Visual Studio Team Services。
> 
> 

在 [hello`wp-config.php`檔案中加入下列程式碼上方 hello 停止編輯註解 hello hello 檔案結尾附近的 hello。

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

此程式碼已貼上，一旦 monaco 會自動儲存 hello 文件。

hello 下一個步驟是 tooenable hello 物件快取外掛程式。 這是藉由拖放**物件 cache.php**從**wp-內容/外掛程式/memcached**資料夾 toohello **wp 內容**資料夾 tooenable hello Memcache 物件快取功能。

![找出 hello memcache 物件 cache.php 外掛程式](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

現在該 hello**物件 cache.php**檔案位於 hello **wp 內容**hello Memcached 物件快取現在已啟用的資料夾。

![啟用 hello memcache 物件 cache.php 外掛程式](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## 確認 hello 外掛程式運作的 Memcache 物件快取
現在，所有的 hello 步驟 tooenable hello Web 應用程式 Memcache 填充碼都完成。 hello 唯一左邊是 tooverify hello 資料會填入您的 Redis 快取執行個體。

### 啟用 Azure Redis 快取中的 hello 非 SSL 連接埠支援
> [!NOTE]
> Hello 撰寫本文時，在 hello Redis CLI 不支援的 SSL 連線，因此 hello 下列的必要步驟。
> 
> 

在 [hello Azure 入口網站，瀏覽您建立此 web 應用程式的 toohello Redis 快取執行個體。 一旦開啟 hello 快取刀鋒視窗中，按一下 hello**設定**圖示。

![Azure Redis 快取設定按鈕](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

選取**存取連接埠**從 hello 清單。

![Azure Redis 快取存取連接埠](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

針對 [只允許透過 SSL 存取]，按一下 [否]。

![Azure Redis 快取存取連接埠僅限 SSL](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

您會看到 hello 非 SSL 連接埠現在已設定。 按一下 [儲存] 。

![Azure Redis 快取 Redis 存取入口網站非 SSL](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### 從 redis cli 連線 tooAzure Redis 快取
> [!NOTE]
> 這個步驟假設 redis 安裝在開發電腦的本機上。 [使用這些指示，在本機上安裝 Redis][9]。
> 
> 

開啟您的選擇，然後輸入下列命令的 hello 的命令列主控台：

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

取代 hello **&lt;主機名稱的-redis-快取&gt;** hello 實際 xxxxx.redis.cache.windows.net 主機名稱與 hello **&lt;主索引鍵-如-redis-快取&gt; ** hello hello 快取的存取金鑰，然後按**Enter**。 一旦 hello CLI 已連接 toohello Redis 快取執行個體，發出任何 redis 命令。 在 [hello 以下螢幕擷取畫面，我選擇 toolist hello 索引鍵。

![從終端機中的 Redis CLI 連線 tooAzure Redis 快取](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

hello 呼叫 toolist hello 索引鍵應該傳回值。 否則，請再試一次瀏覽 toohello web 應用程式，然後再試一次。

## 結論
恭喜！ hello WordPress 應用程式現在會有集中式的記憶體中快取 tooaid 中提高輸送量。 請記住，Web 應用程式 Memcache 填充碼可以搭配任何不論程式設計語言或應用程式架構的 Memcache 用戶端 hello。 tooprovide 意見反應或 tooask 疑問 hello Web 應用程式 Memcache 填充碼，張貼太[MSDN 論壇][ 10]或[Stackoverflow][11]。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## 變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure App Service 與它對現有的 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
