---
title: "aaaConfigure SSL 連線 toosecurely MySQL 連接 tooAzure 資料庫 |Microsoft 文件"
description: "指示 tooproperly MySQL 和相關聯的應用程式 toocorrectly 所設定的 Azure 資料庫使用 SSL 連線"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>設定 SSL 連接您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫
Azure 的 MySQL 資料庫支援連線您的 Azure 資料庫的 MySQL server tooclient 應用程式使用安全通訊端層 (SSL)。 強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。

## <a name="step-1-obtain-ssl-certificate"></a>步驟 1：取得 SSL 憑證
MySQL 伺服器的 Azure 資料庫搭配 SSL 透過下載 hello 所需的憑證 toocommunicate [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem)並儲存 hello 憑證檔案 tooyour 本機磁碟機 （進行這個教學課程中，我們使用 c:\ssl）。
**Microsoft Internet Explorer 和 Microsoft Edge:** hello 下載完成之後，重新命名 hello 憑證 tooBaltimoreCyberTrustRoot.crt.pem。

## <a name="step-2-bind-ssl"></a>步驟 2：繫結 SSL
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>連接使用透過 SSL 的 hello MySQL Workbench tooserver
設定 MySQL Workbench tooconnect 安全地透過 SSL。 瀏覽 toohello **SSL** hello MySQL Workbench 上 hello 安裝新的連接對話方塊中的索引標籤。 輸入 hello 檔案位置的 hello **BaltimoreCyberTrustRoot.crt.pem**在 hello **SSL CA 檔案：**欄位。
![儲存自訂的圖格](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>連接使用透過 SSL 的 hello MySQL CLI tooserver
使用 hello MySQL 命令列介面時，執行下列命令的 hello:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>步驟 3：強制在 Azure 中使用 SSL 連線 
### <a name="using-azure-portal"></a>使用 Azure 入口網站
使用 hello Azure 入口網站，請瀏覽您的 Azure 資料庫的 MySQL server，然後按一下**連線安全性**。 使用 hello 切換按鈕 tooenable 或停用 hello**強制的 SSL 連線**設定。 然後按一下 [儲存] 。 Microsoft 建議 tooalways 啟用**強制的 SSL 連線**增強式安全性設定。
![啟用 ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>使用 Azure CLI
您可以啟用或停用 hello **ssl 強制**參數分別使用 Azure CLI 中的已啟用或停用的值。
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>步驟 4：確認 SSL 連線
執行 hello mysql**狀態**命令 tooverify 連接 tooyour MySQL 伺服器使用 SSL:
```dos
mysql> status
```
確認 hello 連接已加密藉由檢閱 hello 輸出。 輸出應該會顯示：**SSL：使用中的編碼器是 AES256-SHA** 

## <a name="sample-code"></a>範例程式碼
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>後續步驟
檢閱[「適用於 MySQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項
