---
title: "Azure App Service 中 aaaConvert WordPress tooMultisite"
description: "了解 tootake 現有 WordPress web 應用程式透過 hello 組件庫在 Azure 中建立，並將它轉換 tooWordPress 多站台"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>WordPress tooMultisite Azure App Service 中的轉換
## <a name="overview"></a>概觀
*作者 [Ben Lobaugh][ben-lobaugh]，[Microsoft Open Technologies Inc.][ms-open-tech]*

在本教學課程中，您將學習如何 tootake 現有 WordPress web 應用程式透過建立 hello 組件庫在 Azure 和轉換到 WordPress 多站台安裝。 此外，您將學習如何 tooassign hello 的自訂網域 tooeach 子網站中您的安裝。

本文假設您目前已安裝 WordPress。 如果不這麼做，請遵循中提供的 hello 指引[從 hello 組件庫在 Azure 中建立 WordPress 網站][website-from-gallery]。

轉換現有的 WordPress 單一站台安裝 tooMultisite 通常是相當簡單，而且許多此處 hello 初始步驟會直接從 hello[建立網路][ wordpress-codex-create-a-network] hello頁面[WordPress Codex](http://codex.wordpress.org)。

現在就開始吧。

## <a name="allow-multisite"></a>允許多網站
您必須先透過 hello tooenable 多站台`wp-config.php`檔案以 hello **WP\_允許\_多站台**常數。 有兩個方法 tooedit 您 web 應用程式檔案： hello 第一個是透過 FTP 和第二個透過 Git 的 hello。 如果您不熟悉如何 toosetup 其中一種方法，請參閱下列教學課程的 toohello:

* [PHP 網站與 MySQL 和 FTP][website-w-mysql-and-ftp-ftp-setup]
* [PHP 網站與 MySQL 和 Git][website-w-mysql-and-git-git-setup]

開啟 hello `wp-config.php` hello 編輯器，您所選擇的檔案，然後加入上述 hello hello 下列`/* That's all, stop editing! Happy blogging. */`列。

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

是確定 toosave hello 檔案，並將它上傳後 toohello 伺服器 ！

## <a name="network-setup"></a>網路設定
登入 toohello *wp admin*區域，您的 web 應用程式，並且應該會看到新的項目底下 hello**工具**功能表呼叫**網路安裝**。 按一下**網路安裝**和填入 hello 詳細資料，您的網路。

![Network Setup Screen][wordpress-network-setup]

本教學課程使用 hello*子目錄*網站結構描述，因此它一定都可運作，我們將要設定每一個子網站的自訂網域在 hello 教學課程後面。 不過，它應該是子網域安裝，如果您透過 hello 網域對應可能 toosetup [Azure 入口網站](https://portal.azure.com)並正確設定 DNS 的萬用字元。

如需有關子網域與子目錄龐大看到 hello[多站台的網路類型][ wordpress-codex-types-of-networks] hello WordPress Codex 上的發行項。

## <a name="enable-hello-network"></a>啟用 hello 網路
hello 網路現在已設定在 hello 資料庫中，但沒有一個剩餘步驟 tooenable hello 網路功能。 完成 hello`wp-config.php`設定，並確定`web.config`適當地路由傳送每個站台。

按一下 hello 之後**安裝**按鈕 hello*網路安裝*WordPress 頁面，將會嘗試 tooupdate hello`wp-config.php`和`web.config`檔案。 不過，您應該一律檢查 hello 檔案 tooensure hello 更新已成功。 否則，這個畫面將會顯示 hello 必要的更新。 編輯並儲存 hello 檔案。

之後進行這些更新，您將需要 toolog out 及記錄檔送回 hello wp-系統管理儀表板。

在標示為 hello admin 列上現在應該有更多的功能表**我網站**。 此功能表可讓您 toocontrol hello 透過新的網路**網路系統管理員**儀表板。

## <a name="adding-custom-domains"></a>加入自訂網域
hello [WordPress MU 網域對應][ wordpress-plugin-wordpress-mu-domain-mapping]外掛程式可讓您輕鬆 tooadd 自訂網域 tooany 站台網路中。 為了讓 hello 外掛程式 toooperate 正常運作，您需要 toodo 上 hello 入口網站，並在網域註冊機構，某些額外的設定。

## <a name="enable-domain-mapping-toohello-web-app"></a>啟用網域對應 toohello web 應用程式
hello**免費** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)計劃模式不支援新增自訂網域 tooWeb 應用程式。 您將需要 tooswitch 太**共用**或**標準**模式。 toodo 這樣：

* 登入 toohello Azure 入口網站，並找出您的 web 應用程式。 
* 按一下 hello**向上延展**索引標籤中**設定**。
* 在 [一般] 下，選取 [共用] 或 [標準]
* 按一下 [儲存] 

您可能會收到訊息，詢問您 tooverify hello 變更，並確認您 web 應用程式現在可能需支付費用，其使用方式而定，而 hello 您設定其他設定。

需要幾秒鐘 tooprocess hello 新的設定，因此，現在是 恰好 toostart 會設定您的網域。

## <a name="verify-your-domain"></a>驗證網域
Azure Web 應用程式可讓您 toomap 網域 toohello 網站之前，您必須先 tooverify 您擁有 hello 授權 toomap hello 網域。 toodo 因此，您必須在其中加入新的 CNAME 記錄 tooyour DNS 項目。

* 登入 tooyour 網域的 DNS 管理員
* 建立新的 CNAME *awverify*
* 點*awverify*太*awverify。YOUR_DOMAIN.azurewebsites.net*

它可能需要完整生效的 hello DNS 變更 toogo 一些時間，因此如果 hello 步驟沒有作用，請讓咖啡、 杯回來然後再試一次。

## <a name="add-hello-domain-toohello-web-app"></a>新增 hello 網域 toohello web 應用程式
傳回 tooyour web 應用程式透過 hello Azure 入口網站中，按一下**設定**，然後按一下**自訂網域及 SSL**。

當 hello *SSL 設定*會顯示，則會看見 hello 欄位，您將在其中輸入您想 tooassign tooyour web 應用程式的所有 hello 網域。 如果此處未列出網域，它將無法使用對應內 WordPress，不論 hello 網域 DNS 的安裝程式的方式。

![Manage custom domains dialog][wordpress-manage-domains]

之後 hello 文字方塊中輸入您的網域，Azure 會確認 hello 您先前建立的 CNAME 記錄。 如果未完全傳播到 hello DNS，則會顯示紅色指示器。 如果成功，則會出現綠色勾選記號。 

記下 IP 位址會列示在 hello hello 對話方塊底部的 hello。 您將需要此 toosetup hello 記錄為您的網域。

## <a name="setup-hello-domain-a-record"></a>安裝程式 hello 網域 A 記錄
如果 hello 其他步驟成功，您可能會立即指派 hello 網域 tooyour Azure web 應用程式透過 DNS A 記錄。 

它是重要 toonote 這裡 Azure web 應用程式接受 CNAME 及 A 記錄，不過您*必須*使用 A 記錄 tooenable 適當網域之間的對應。 CNAME 無法轉送 tooanother CNAME，這是什麼 Azure 為您建立並 YOUR_DOMAIN.azurewebsites.net。

使用 hello hello 先前步驟中的 IP 位址，傳回 tooyour DNS 管理員及安裝 hello 記錄 toopoint toothat IP。

## <a name="install-and-setup-hello-plugin"></a>安裝及設定 hello 外掛程式
WordPress 多站台目前並沒有內建方法 toomap 自訂網域。 不過，沒有呼叫外掛程式[WordPress MU 網域對應][ wordpress-plugin-wordpress-mu-domain-mapping] ，為您加入了 hello 功能。 在您的站台 toohello 網路系統管理員部分記錄檔並安裝 hello **WordPress MU 網域對應**外掛程式。

安裝和啟用 hello 外掛程式，請瀏覽之後**設定** > **網域對應**tooconfigure hello 外掛程式。 在 hello 第一個文字方塊中，*伺服器 IP 位址*，輸入的 hello IP 位址使用 toosetup hello hello 網域的記錄。 設定任何*網域選項*您想要 （hello 預設值為經常沒問題），按一下 **儲存**。

## <a name="map-hello-domain"></a>Hello 網域對應
請瀏覽 hello**儀表板**您想要 toomap hello 網域 hello 站台。 按一下**工具** > **網域對應**和型別輸入 hello 文字方塊中，然後按一下 hello 新網域**新增**。

根據預設，hello 新網域會重寫的 toohello 自動產生站台的網域。 如果您想 toohave 所有傳送的流量 toohello 新網域時，請檢查 hello*主要網域，如這篇部落格*方塊，之後再儲存。 您可以加入無限的數量的網域 tooa 站台，但只有一個可以是主要。

## <a name="do-it-again"></a>再做一次
Azure Web 應用程式可讓您 tooadd 網域 tooa web 應用程式數目沒有限制。 tooadd 另一個網域，您將需要 tooexecute hello**驗證您的網域**和**安裝 hello 網域 A 記錄**區段，為每個網域。    

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


