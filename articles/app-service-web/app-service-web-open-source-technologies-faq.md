---
title: "aaaOpen 原始碼技術常見問題集 azure web 應用程式 |Microsoft 文件"
description: "收到 hello Web 應用程式功能的 Azure App Service 中的開放原始碼技術的相關常見問題的解答 toofrequently。"
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Azure 中的 Web Apps 相關開放原始碼技術常見問題集

這篇文章有集 (Faq) 解答 toofrequently 相關問題的開放原始碼技術，用於 hello [Azure App Service Web 應用程式功能](https://azure.microsoft.com/services/app-service/web/)。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>我的 ClearDB 資料庫已關閉。 如何解決這個問題？

如有資料庫相關的問題，請連絡 [ClearDB 支援](https://www.cleardb.com/developers/help/support) (英文)。 

如需 ClearDB 答案 toocommon 問題，請參閱[ClearDB 常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>為什麼我的 ClearDB 資料庫中沒有顯示 hello 入口網站？

如果您建立的 ClearDB 資料庫在 hello [Azure 入口網站](http://portal.azure.com/)，hello 資料庫不會出現在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)。 toowork 解決這個問題，您可以手動連結 toohello web 應用程式資料庫。

同樣地，如果您建立的 ClearDB 資料庫在 hello [Azure 傳統入口網站](http://manage.windowsazure.com/)，不會看到您的資料庫中 hello [Azure 入口網站](http://portal.azure.com/)。 對於這種情況，目前沒有可行的因應措施。 

如需詳細資訊，請參閱 [ClearDB MySQL 資料庫搭配 Azure App Service 的常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>為什麼我的 ClearDB 資料庫在我的訂用帳戶移轉期間未移轉？

當跨訂用帳戶執行資源移轉時，適用某些限制。 ClearDB MySQL 資料庫是第三方服務，因此在 Azure 訂用帳戶移轉期間是不會移轉的。

如果您未管理 hello 移轉您的 MySQL 資料庫，則在移轉您的 Azure 資源之前，可能無法使用您的 ClearDB MySQL 資料庫。 tooavoid 這，首先，手動將移轉您的 ClearDB 資料庫，然後再移轉 hello web 應用程式的 Azure 訂用帳戶。

如需詳細資訊，請參閱 [ClearDB MySQL 資料庫搭配 Azure App Service 的常見問題集](https://docs.microsoft.com/azure/store-cleardb-faq/)。

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>如何開啟 PHP 記錄 tootroubleshoot PHP 問題？

tooturn PHP 記錄：

1. 登入 tooyour [Kudu 網站](https://*yourwebsitename*.scm.azurewebsites.net)。
2. 在 hello 上方功能表中，選取 **偵錯主控台** > **CMD**。
3. 選取 hello**網站**資料夾。
4. 選取 hello **wwwroot**資料夾。
5. 選取 hello  **+** 圖示，然後選取**新檔案**。
6. 設定 hello 檔案名稱得**。 user.ini**。
7. 選取 hello 鉛筆圖示旁太**。 user.ini**。
8. 在 hello 檔案中，加入下列程式碼：`log_errors=on`
9. 選取 [ **儲存**]。
10. 選取 hello 鉛筆圖示旁太**wp config.php**。
11. 變更下列程式碼的 hello 文字 toohello:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. 在 hello Azure 入口網站，在 hello web 應用程式功能表中，重新啟動您的 web 應用程式。

如需詳細資訊，請參閱[啟用 WordPress 錯誤記錄檔](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) (英文)。

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>如何在 App Service 內裝載的應用程式中記錄 Python 應用程式錯誤？

toocapture Python 應用程式錯誤：

1. 在 hello Azure 入口網站，在您 web 應用程式中，選取 **設定**。
2. 在 hello**設定**索引標籤上，選取**應用程式設定**。
3. 在下**應用程式設定**，輸入下列索引鍵/值組的 hello:
    * 索引鍵：WSGI_LOG
    * 值：D:\home\site\wwwroot\logs.txt (輸入您選擇的檔案名稱)

您現在應該會看到 hello wwwroot 資料夾中的 hello logs.txt 檔案中的錯誤。

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>如何變更 hello 版的 hello App Service 中裝載 Node.js 應用程式？

toochange hello 版的 hello Node.js 應用程式，您可以使用其中一個 hello 下列選項：

*   在 hello Azure 入口網站，使用**應用程式設定**。
    1. 在 hello Azure 入口網站，移 tooyour web 應用程式。
    2. 在 hello**設定**刀鋒視窗中，選取**應用程式設定**。
    3. 在**應用程式設定**、 您可以包含 WEBSITE_NODE_DEFAULT_VERSION hello 索引鍵，以及 hello 版本的 Node.js 要做為 hello 值。
    4. 移 tooyour [Kudu 主控台](https://*yourwebsitename*.scm.azurewebsites.net)。
    5. toocheck hello Node.js 版本中，輸入下列命令的 hello:  
   ```
   node -v
   ```
*   修改 hello iisnode.yml 檔案。 變更 hello iisnode.yml 檔案中的 hello Node.js 版本只會設定 hello 執行階段環境的 iisnode 使用。 Kudu cmd 和其他人仍使用設定中的 hello Node.js 版本**應用程式設定**hello Azure 入口網站中。

    tooset hello iisnode.yml 手動建立 iisnode.yml 檔案，您的應用程式根資料夾中。 在 hello 檔案中，包括以下各 hello:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   設定原始檔控制部署期間使用 package.json 的 hello iisnode.yml 檔案。
    hello Azure 的原始檔控制部署程序牽涉到 hello 下列步驟：
    1. 移動內容 toohello Azure web 應用程式。
    2. 如果沒有則 （deploy.cmd、.deployment 檔案），hello web 應用程式根資料夾中，會建立預設部署指令碼。
    3. 執行部署指令碼，並建立這 iisnode.yml 檔案若提到 hello package.json 檔案中的 hello Node.js 版本 > 引擎`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. hello iisnode.yml 檔案具有下列的程式碼行 hello:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>我在我的 WordPress 應用程式裝載在 App Service 中看到 hello 訊息 「 建立資料庫連線錯誤 」。 我該如何進行疑難排解？

如果您看到此錯誤在您的 Azure WordPress 應用程式、 tooenable php_errors.log 和 debug.log，完成 hello 步驟詳細說明[啟用 WordPress 錯誤記錄檔](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/)。

Hello 記錄啟用時，重現 hello 錯誤，然後檢查 hello 記錄 toosee 如果即將用盡連線：
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

如果您看到此錯誤在 debug.log 或 php_errors.log 檔案時，您的應用程式超出 hello 連接數目。 如果您正在裝載 ClearDB 上，確認 hello 中可用的連線數目您[服務計劃](https://www.cleardb.com/pricing.view)。

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>如何對於 App Service 中裝載的 Node.js 應用程式進行偵錯？

1.  移 tooyour [Kudu 主控台](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole)。
2.  移 tooyour 應用程式記錄檔資料夾 (D:\home\LogFiles\Application)。
3.  Hello logging_errors.txt 檔案中，檢查的內容。

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>如何在 App Service Web 應用程式或 API 應用程式中安裝原生 Python 模組？

某些封裝可能不會使用 Azure 中的 pip 進行安裝。 hello 封裝可能無法在 hello Python 封裝索引，或可能必須使用編譯器 （編譯器不 hello hello web 應用程式執行中應用程式服務的電腦上）。 如需在 App Service Web 應用程式及 API 應用程式中安裝原生模組的相關資訊，請參閱[在 App Service 中安裝 Python 模組](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/) (英文)。

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>如何使用 Git 和 hello 的新版本，Python 的部署如 Django 應用程式 tooApp 服務？

如需安裝如 Django 資訊，請參閱[部署如 Django 應用程式 tooApp 服務](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/)。

## <a name="where-are-hello-tomcat-log-files-located"></a>Hello Tomcat 記錄檔是否位於哪裡？

對於 Azure Marketplace 和自訂部署：

* 資料夾位置：D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* 感興趣區域：
    * catalina.*yyyy-mm-dd*.log
    * host-manager.*yyyy-mm-dd*.log
    * localhost.*yyyy-mm-dd*.log
    * manager.*yyyy-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log


對於入口網站**應用程式設定**部署：

* 資料夾位置：D:\home\LogFiles
* 感興趣區域：
    * catalina.*yyyy-mm-dd*.log
    * host-manager.*yyyy-mm-dd*.log
    * localhost.*yyyy-mm-dd*.log
    * manager.*yyyy-mm-dd*.log
    * site_access_log.*yyyy-mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>如何進行 JDBC 驅動程式連線錯誤的疑難排解？

您可能會看見 hello 下 Tomcat 記錄檔中的訊息：

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

tooresolve hello 錯誤：

1. 從您的應用程式/lib 資料夾移除 hello sqljdbc*.jar 檔案。
2. 如果您使用 hello 自訂 Tomcat 或 Azure Marketplace Tomcat web 伺服器，將複製此 d 檔案 toohello Tomcat lib 資料夾。
3. 如果您要啟用從 Java hello Azure 入口網站 (選取**Java 1.8** > **Tomcat 伺服器**)，是平行 tooyour 應用程式的 hello 資料夾中複製 hello sqljdbc.* jar 檔案。 接著，新增下列 classpath 設定 toohello web.config 檔的 hello:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>為什麼當我嘗試 toocopy 即時記錄檔時看到錯誤？

如果您嘗試 toocopy Java 應用程式 (例如，Tomcat) 的即時記錄檔，您可能會看到這個 FTP 錯誤：

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

hello 錯誤訊息可能有所不同，hello FTP 用戶端。

所有的 Java 應用程式都有這個鎖定問題。 只有 Kudu 支援 hello 應用程式執行時，請下載此檔案。

正在停止 hello 應用程式可讓 FTP 存取 toothese 檔案。

另一個解決方法是 toowrite WebJob 排程執行，而且複製這些檔案 tooa 不同的目錄。 範例專案，請參閱 hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob)專案。

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>其中找到 Jetty hello 記錄檔？

服務商場和自訂部署，hello 記錄檔是 hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs 資料夾中。 請注意 hello 資料夾位置，取決於您使用的 Jetty hello 版本。 例如，hello 提供路徑的 Jetty 9.1.2 如下。 尋找 jetty_*YYYY_MM_DD*.stderrout.log。

入口網站的應用程式設定部署的 hello 記錄檔位於 D:\home\LogFiles。 尋找 jetty_*YYYY_MM_DD*.stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>我能否從 Azure Web 應用程式傳送電子郵件？

App Service 沒有內建的電子郵件功能。 如需從應用程式傳送電子郵件的一些可行替代方案，請參閱本篇 [Stack Overflow 討論](http://stackoverflow.com/questions/17666161/sending-email-from-azure) (英文)。

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>為什麼我的 WordPress 網站重新導向 tooanother URL？

如果您最近有移轉 tooAzure，WordPress 可能會重新導向 toohello 舊網域 URL。 這被因為 hello MySQL 資料庫中的設定。

WordPress 協同 + 是 Azure 站台擴充功能，您可以直接在 hello 資料庫中使用 tooupdate hello 重新導向 URL。 如需使用 WordPress Buddy+ 的詳細資訊，請參閱 [WordPress 工具以及使用 WordPress Buddy+ 進行 MySQL 移轉](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (英文)。

或者，如果您使用 SQL 查詢或 PHPMyAdmin 偏好 toomanually 更新 hello 重新導向 URL，請參閱[WordPress： 重新導向 URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/)。

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>如何變更我的 WordPress 登入密碼？

如果您忘記您的 WordPress 登入密碼，您可以使用 WordPress 協同 + tooupdate 它。 密碼、 安裝 hello WordPress 協同 + Azure 網站擴充功能，並再完成 hello 步驟中所述的 tooreset [WordPress 工具和 MySQL 移轉與 WordPress 協同 +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)。

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>我無法登入 tooWordPress。 如何解決這個問題？

最近安裝外掛程式之後，如果您發現遭鎖定而無法進入 WordPress，則表示外掛程式可能有問題。 WordPress Buddy+ 是 Azure 網站擴充功能，可協助您停用 WordPress 中的外掛程式。 如需詳細資訊，請參閱 [WordPress 工具以及使用 WordPress Buddy+ 進行 MySQL 移轉](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/) (英文)。

## <a name="how-do-i-migrate-my-wordpress-database"></a>我要如何移轉我的 WordPress 資料庫？

您已針對移轉的 hello MySQL 資料庫，連接的 tooyour WordPress 網站的多個選項：

* 開發人員： 使用 hello[命令提示字元或 PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* 非開發人員：使用 [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>如何使 WordPress 更安全？

請參閱 toolearn WordPress 的安全性最佳作法的相關[的 WordPress 在 Azure 中的安全性最佳做法](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/)。

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>我試著 toouse PHPMyAdmin，而且我看到 hello 訊息 「 拒絕存取 」。 如何解決這個問題？

如果 hello MySQL 中應用程式功能並非在此應用程式服務執行個體中尚未執行，您可能會遇到此問題。 tooresolve hello 問題，請再試一次 tooaccess 您的網站。 這樣會啟動所需的 hello 程序，包括 hello MySQL 應用程式內的程序。 MySQL 正在執行的應用程式內，處理序總管中，確定該 mysqld.exe tooverify 會列在 hello 處理程序。

確定 MySQL 在應用程式正在執行之後，請再試一次 toouse PHPMyAdmin。

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>當我 tooimport 再試一次，或使用 PHPMyadmin 匯出我 MySQL 應用程式內的資料庫時，我會收到 HTTP 403 錯誤。 如何解決這個問題？

如果您使用舊版 Chrome，您可能會遇到已知的錯誤。 升級 tooa 較新版本的 Chrome tooresolve hello 問題。 也請嘗試使用不同的瀏覽器，如 Internet Explorer 或邊緣，其中 hello 不會發生問題。
