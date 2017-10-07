---
title: "在 Azure 上的 aaaEnterprise 類別 WordPress |Microsoft 文件"
description: "了解 toohost 企業級 WordPress Azure App Service 上的站台"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>Azure 上的企業級 WordPress
Azure App Service 針對關鍵的大規模 [WordPress][wordpress] 網站，提供可調整、安全又容易使用的環境。 Microsoft 本身執行企業級站台，例如 hello [Office] [ officeblog]和[Bing] [ bingblog]部落格。 本文章將示範如何 toouse hello tooestablish Microsoft Azure App Service Web 應用程式功能及維護企業級、 以雲端為基礎的 WordPress 網站，可處理大量的訪客。

## <a name="architecture-and-planning"></a>架構與規劃
基本 WordPress 安裝僅有兩項需求：

* **MySQL 資料庫**： 這項需求是透過[hello Azure Marketplace 中的 ClearDB][cdbnstore]。 或者，您可以使用 [Windows][mysqlwindows] 或 [Linux][mysqllinux]，自行管理 Azure 虛擬機器上的 MySQL 安裝。

  > [!NOTE]
  > ClearDB 提供數種 MySQL 組態。 每個組態具有不同的效能特性。 請參閱 hello [Azure 市集][ cdbnstore]供應項目透過 hello Azure 市集或直接 hello 所見，會提供有關[ClearDB 網站](http://www.cleardb.com/pricing.view)。
  >
  >
* **PHP 5.2.4 或更高版本**：Azure App Service 目前提供 [PHP 5.4、5.5 和 5.6 版][phpwebsite]。

  > [!NOTE]
  > 我們建議，您永遠執行的 hello 最新版的 PHP，讓您擁有 hello 最新的安全性修正程式。
  >
  >

### <a name="basic-deployment"></a>基本部署
如果您使用只 hello 基本需求，您可以建立 Azure 的區域內的基本方案。

![Azure Web 應用程式與 MySQL 資料庫裝載於單一 Azure 區域中][basic-diagram]

雖然這樣會讓您建立多個 hello 網站 tooscale 出您的應用程式的 Web 應用程式執行個體，所有項目被裝載在 hello 資料中心必須位於特定地理區域中。 在此區域之外訪客可能會看到回應時間緩慢 hello 站台使用時。 如果在此區域中的 hello 資料中心同時停機時，也會應用程式。

### <a name="multi-region-deployment"></a>多重區域部署
使用 Azure [Traffic Manager][trafficmanager]，您可以調整您的 WordPress 網站到多個地理區域，並提供所有造訪者 hello 相同的 URL。 所有造訪者有透過 Traffic Manager，並為基礎的路由的 tooa 區域 hello 負載平衡設定。

![裝載在多個區域，使用 CDBR 高可用性路由器 tooroute tooMySQL 各地區的 Azure web 應用程式][multi-region-diagram]

在每個區域中，hello WordPress 網站仍會跨越多個 Web 應用程式執行個體，但此項縮放是特定 tooa 區域。 高流量區域和低流量區域的調整可能會有所不同。

您可以使用 tooreplicate 和路由流量 toomultiple MySQL 資料庫，請[ClearDB 高可用性路由器 (CDBRs)] [ cleardbscale] （顯示左） 或[MySQL 叢集載波等級版本 (CGE)][cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>包含媒體儲存體和快取的多重區域部署
如果 hello 網站接受上傳或主機媒體檔案，使用 Azure Blob 儲存體。 如果您需要快取，請考慮[Redis 快取][rediscache]， [Memcache 雲端](http://azure.microsoft.com/gallery/store/garantiadata/memcached/)， [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/)，或其中一個 hello hello 中的其他快取提供項目[Azure 市集](http://azure.microsoft.com/gallery/store/)。

![裝載於多個區域中的 Azure Web 應用程式，搭配受管理的快取、Blob 儲存體和內容傳遞網路，為 MySQL 使用 CDBR 高可用性路由器][performance-diagram]

Blob 儲存體是地理分散到區域，依預設，所以您不需 tooworry 相關的所有站台複寫檔案。 您也可以啟用 hello Azure[內容傳遞網路][ cdn]針對 Blob 儲存體，這會發佈檔案 tooend 之節點的更接近 tooyour 訪客。

### <a name="planning"></a>規劃
#### <a name="additional-requirements"></a>其他需求
| toodo 這... | 目的... |
| --- | --- |
| **上傳或儲存大型檔案** |[使用 Blob 儲存體的 WordPress 外掛程式][storageplugin] |
| **傳送電子郵件** |[SendGrid] [ storesendgrid]和 hello[使用 SendGrid WordPress 外掛程式][sendgridplugin] |
| **自訂網域名稱** |[在 Azure App Service 中設定自訂網域名稱][customdomain] |
| **HTTPS** |[針對 Azure App Service 中的 Web 應用程式啟用 HTTPS][httpscustomdomain] |
| **生產前驗證** |[針對 Azure App Service 中的 Web 應用程式設定預備環境][staging] <p>當您從暫存 tooproduction 移動 web 應用程式時，您也可以移動 hello WordPress 組態。 請確定所有設定都都更新的 toohello 生產應用程式的需求，然後才能移接移的 hello 應用程式 tooproduction。</p> |
| **監視與疑難排解** |[針對 Azure App Service 中的 Web 應用程式啟用診斷記錄功能][log]及[監視 Azure App Service 中的 Web Apps][monitor] |
| **部署您的網站** |[在 Azure App Service 中部署 Web 應用程式][deploy] |

#### <a name="availability-and-disaster-recovery"></a>可用性和災難復原
| toodo 這... | 目的... |
| --- | --- |
| **負載平衡網站**或**異地發佈網站** |[使用 Azure 流量管理員路由傳送流量][trafficmanager] |
| **備份與還原** |[備份 Azure App Service 中的 Web 應用程式][backup]及[還原 Azure App Service 中的 Web 應用程式][restore] |

#### <a name="performance"></a>效能
Hello 雲端中的效能是主要是透過快取和向外延展來達成。不過，應該考慮 hello 記憶體、 頻寬和其他屬性的 Web 應用程式裝載。

| toodo 這... | 目的... |
| --- | --- |
| **了解 App Service 執行個體功能** |[定價詳細資料，包括 App Service 層的功能][websitepricing] |
| **快取資源** |[Redis 快取][rediscache]， [Memcache 雲端](/gallery/store/garantiadata/memcached/)， [MemCachier](/gallery/store/memcachier/memcachier/)，或其中一個 hello hello 中的其他快取提供項目[Azure 市集](/gallery/store/) |
| **調整您的應用程式** |[調整 Azure App Service 中的 Web 應用程式][websitescale]及 [ClearDB 高可用性路由][cleardbscale]。 如果您選擇 toohost 並管理您自己的 MySQL 安裝時，您應該考慮[MySQL 叢集 CGE] [ cge]的向外延展。 |

#### <a name="migration"></a>移轉
有兩個方法 toomigrate 現有的 WordPress 網站 tooAzure 應用程式服務：

* **[WordPress 匯出][export]**： 這個方法會將匯出 hello 部落格的內容。 您可以接著使用匯入 hello 內容 tooa 新 WordPress 網站上 Azure App Service hello [WordPress 匯入工具外掛程式][import]。

  > [!NOTE]
  > 此程序可讓您移轉內容，但它無法移轉任何外掛程式、主題或其他自訂。 您必須手動重新安裝這些元件。
  >
  >
* **手動移轉**:[備份您的站台][ wordpressbackup]和[資料庫][wordpressdbbackup]，然後手動將它還原 tooa 在 Azure 中的 web 應用程式應用程式服務和相關聯的 MySQL 資料庫。 這個方法是有用的 toomigrate 高度自訂的網站，因為它可避免 hello tedium 手動安裝的外掛程式、 主題和其他自訂。

## <a name="step-by-step-instructions"></a>逐步指示
### <a name="create-a-wordpress-site"></a>建立 WordPress 網站
1. 使用 hello [Azure Marketplace] [ cdbnstore] toocreate hello 大小所識別的 hello 的 MySQL 資料庫[架構和規劃](#planning)hello 區域或區域中的區段您將會在其中裝載您的網站。
2. 中的 hello 步驟[WordPress web 應用程式建立 Azure App Service 中][ createwordpress] toocreate WordPress web 應用程式。 當您建立 hello web 應用程式時，選取**使用現有的 MySQL 資料庫**，然後選取您在步驟 1 中建立的 hello 資料庫。

如果您要移轉現有的 WordPress 網站，請參閱[移轉現有的 WordPress 網站 tooAzure](#Migrate-an-existing-WordPress-site-to-Azure)之後建立新的 web 應用程式。

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>移轉現有的 WordPress 網站 tooAzure
Hello 中所述[架構和規劃](#planning)區段中，有兩種方式 toomigrate WordPress 網站：

* **使用匯出和匯入**，不需要太多自訂，或只想 toomove hello 內容的站台。
* **使用備份和還原**的站台有很多自訂您想 toomove 的所有項目。

使用下列各節 toomigrate hello 的其中一個站台。

#### <a name="hello-export-and-import-method"></a>hello 匯出和匯入方法
1. 使用[WordPress 匯出][ export] tooexport 現有站台。
2. 建立 web 應用程式使用中 hello hello 步驟[建立 WordPress 網站](#Create-a-new-WordPress-site)> 一節。
3. 登入 tooyour WordPress 網站上 hello [Azure 入口網站][mgmtportal]，然後按一下**外掛程式** > **加入新**。 搜尋及安裝 hello **WordPress 匯入工具**外掛程式。
4. 安裝 hello WordPress 匯入工具外掛程式之後，請按一下**工具** > **匯入**，然後按一下 **WordPress** toouse hello WordPress 匯入工具的外掛程式。
5. 在 hello**匯入 WordPress**頁面上，按一下**選擇檔案**。 尋找現有的 WordPress 網站，從匯出的 hello WXR 檔案並按一下**上傳的檔案和匯入**。
6. 按一下 [提交] 。 系統會提示您 hello 匯入成功。
7. 完成所有步驟之後，重新啟動您的網站，從其**應用程式服務**刀鋒視窗中 hello [Azure 入口網站][mgmtportal]。

您匯入 hello 站台後，您可能需要 tooperform hello 遵循步驟 tooenable 設定不在 hello 匯入檔案中。

| 如果使用... | 執行此動作... |
| --- | --- |
| **固定連結** |從 hello WordPress 儀表板的 hello 新網站，按一下 **設定** > **永久連結**，然後更新 hello 永久連結結構。 |
| **影像/媒體連結** |tooupdate 連結 toohello 新位置，請使用 hello [Velvet 則藍色更新 Url 外掛程式][velvet]，搜尋和取代工具，或手動更新資料庫中的 hello 連結。 |
| **佈景主題** |跳過**外觀** > **佈景主題**，然後視需要更新 hello 網站佈景主題。 |
| **功能表** |如果您的佈景主題支援功能表，tooyour 首頁連結可能仍有 hello 內嵌在這些舊的子目錄。 跳過**外觀** > **功能表**，並予以更新。 |

#### <a name="hello-backup-and-restore-method"></a>hello 備份和還原方法
1. 備份您現有的 WordPress 網站使用在 hello 資訊[WordPress 備份][wordpressbackup]。
2. 備份您現有的資料庫，藉由在 hello 資訊[備份資料庫][wordpressdbbackup]。
3. 建立資料庫，然後還原 hello 備份。

   1. 購買新的資料庫從 hello [Azure Marketplace][cdbnstore]，或設定上的 MySQL 資料庫[Windows] [ mysqlwindows]或[Linux] [ mysqllinux]虛擬機器。
   2. 使用 MySQL 用戶端，像是[MySQL Workbench] [ workbench] tooconnect toohello 新資料庫，然後匯入您的 WordPress 資料庫。
   3. 更新 hello 資料庫 toochange hello 網域項目 tooyour 新 Azure 應用程式服務的網域，例如 mywordpress.azurewebsites.net。 使用 hello[搜尋和取代 WordPress 資料庫指令碼][ searchandreplace] toosafely 變更所有執行個體。
4. 在 hello Azure 入口網站中建立 web 應用程式，並將發行 hello WordPress 備份。

   1. toocreate 之 web 應用程式資料庫，在 hello [Azure 入口網站][mgmtportal]，按一下 **新增** > **Web + 行動** > **Azure Marketplace** > **Web 應用程式** > **Web 應用程式 + SQL** (或**Web 應用程式 + MySQL**) >**建立**。 設定所有必要的 hello 設定 toocreate 空 web 應用程式。
   2. 在您的 WordPress 備份，找出 hello **wp config.php**檔案，並在編輯器中開啟它。 取代下列項目與新的 MySQL 資料庫的 hello 資訊 hello:

      * **DB_NAME**: hello hello 資料庫使用者名稱。
      * **DB_USER**: hello 使用者名稱使用 tooaccess hello 資料庫。
      * **DB_PASSWORD**: hello 使用者密碼。

        變更這些項目之後，請儲存並關閉 hello **wp config.php**檔案。
   3. 使用 hello[部署在 Azure App Service web 應用程式][ deploy]資訊 tooenable hello 部署方法，toouse，並接著部署 WordPress 備份 tooyour web 應用程式在 Azure App Service 中的。
5. 部署 hello WordPress 網站之後，您應該能夠 tooaccess hello 新站台 （做為 App Service web 應用程式） 使用 hello *。 azurewebsite.net hello 網站 URL。

### <a name="configure-your-site"></a>設定網站
已建立或移轉 hello WordPress 網站之後，請使用下列資訊 tooimprove 效能 hello 或啟用其他功能。

| toodo 這... | 目的... |
| --- | --- |
| **設定 App Service 計劃模式、大小，以及啟用調整規模** |[在 Azure App Service 中調整 Web 應用程式規模][websitescale]。 |
| **啟用持續資料庫連線** |根據預設，WordPress 不使用持續性資料庫連接，可能會造成您之後的多個連線進行節流的連接 toohello 資料庫 toobecome。 tooenable 持續連線，安裝 hello[持續連線的介面卡外掛程式](https://wordpress.org/plugins/persistent-database-connection-updater/installation/)。 |
| **提升效能** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">停用 hello ARR cookie</a>，如此可改善效能，多個 Web 應用程式執行個體上執行 WordPress 時。</p></li><li><p>啟用快取。 您可以使用<a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">Redis 快取</a>（預覽） 以 hello <a href="https://wordpress.org/plugins/redis-object-cache/">Redis 物件快取 WordPress 外掛程式</a>，或者您可以使用其中一個 hello hello 從其他快取提供項目<a href="/gallery/store/">Azure 市集</a>。</p></li><li><p>[利用 Wincache 讓 WordPress 變得更快](https://wordpress.org/plugins/w3-total-cache/)。 Web 應用程式預設已啟用 Wincache。 當同時使用 WinCache 與動態快取，WinCache 的檔案快取，來關閉，但保留 hello 使用者和工作階段快取已啟用。 tooturn 關閉檔案快取，在系統層級.ini 檔案中，設定下列值的 hello:<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[在 Azure App Service 中調整 Web 應用程式規模][websitescale]並使用 <a href="http://www.cleardb.com/developers/cdbr/introduction">ClearDB 高可用性路由</a>或 <a href="http://www.mysql.com/products/cluster/">MySQL Cluster CGE</a>。</p></li></ul> |
| **使用 Blob 進行儲存** |<ol><li><p>[建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。</p></li><li><p>了解如何太[使用 hello 內容散發網路](../cdn/cdn-create-new-endpoint.md)toogeo-發佈在 blob 中儲存的資料。</p></li><li><p>安裝和設定 hello <a href="https://wordpress.org/plugins/windows-azure-storage/">WordPress 外掛程式的 Azure 儲存體</a>。</p><p>如需詳細的設定和 hello 外掛程式的組態資訊，請參閱 hello<a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">使用者指南</a>。</p> </li></ol> |
| **啟用電子郵件** |啟用<a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a>使用 hello Azure 存放區。 安裝 hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">SendGrid 外掛程式</a>用於 WordPress。 |
| **設定自訂網域名稱** |[在 Azure App Service 中設定自訂網域名稱][customdomain]。 |
| **啟用自訂網域名稱的 HTTPS** |[針對 Azure App Service 中的 Web 應用程式啟用 HTTPS][httpscustomdomain]。 |
| **負載平衡或異地發佈您的網站** |[使用 Azure 流量管理員路由傳送流量][trafficmanager]。 如果您使用自訂網域，請參閱[Azure App Service 中設定自訂網域名稱][ customdomain]如需有關資訊 toouse Traffic Manager 使用自訂網域名稱。 |
| **啟用自動備份** |[在 Azure App Service 中備份 Web 應用程式][backup]。 |
| **啟用診斷記錄** |[在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能][log]。 |

## <a name="next-steps"></a>後續步驟
* [WordPress 最佳化 (英文)](http://codex.wordpress.org/WordPress_Optimization)
* [WordPress toomultisite Azure App Service 中的轉換](web-sites-php-convert-wordpress-multisite.md)
* [適用於 Azure 的 ClearDB 升級精靈 (英文)](http://www.cleardb.com/store/azure/upgrade)
* [將 WordPress 裝載到 Azure App Service 中 Web 應用程式的子資料夾中 (英文)](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [逐步解說：使用 Azure 建立 WordPress 網站](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [在 Azure 上裝載現有的 WordPress 部落格 (英文)](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [在 WordPress 中啟用美化的固定連結 (英文)](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [如何 toomigrate 及 Azure App Service 上執行您的 WordPress 部落格](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Toorun WordPress 的 Azure App Service 上可用的方式](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [在兩分鐘內完成在 Azure 上的 WordPress (英文)](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [移動 WordPress 部落格 tooAzure-第 1 部分： 在 Azure 上建立 WordPress 部落格](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [移動 WordPress 部落格 tooAzure-第 2 部分： 傳送您的內容](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [移動 WordPress 部落格 tooAzure-3 部分： 設定您的自訂網域](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [移動 WordPress 部落格 tooAzure-第 4 部分： 永久連結和 URL 重寫規則看起來很](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [移動 WordPress 部落格 tooAzure-第 5 部分： 從子資料夾 toohello 根移動](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [如何註冊 WordPress tooset web 應用程式，您的 Azure 帳戶](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [在 Azure 上維持 WordPress (英文)](http://www.johnpapa.net/wordpress-on-azure/)
* [在 Azure 上的 WordPress 秘訣 (英文)](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務已啟動，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡，無需承諾。
>
>

## <a name="whats-changed"></a>變更的項目
從網站 tooApp 服務指南 toohello 變更，請參閱[Azure App Service 以及它對現有的 Azure 服務影響](http://go.microsoft.com/fwlink/?LinkId=529714)。

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
