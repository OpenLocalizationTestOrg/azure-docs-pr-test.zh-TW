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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="57054-103">設定 SSL 連接您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫</span><span class="sxs-lookup"><span data-stu-id="57054-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="57054-104">Azure 的 MySQL 資料庫支援連線您的 Azure 資料庫的 MySQL server tooclient 應用程式使用安全通訊端層 (SSL)。</span><span class="sxs-lookup"><span data-stu-id="57054-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="57054-105">強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。</span><span class="sxs-lookup"><span data-stu-id="57054-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="57054-106">步驟 1：取得 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="57054-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="57054-107">MySQL 伺服器的 Azure 資料庫搭配 SSL 透過下載 hello 所需的憑證 toocommunicate [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem)並儲存 hello 憑證檔案 tooyour 本機磁碟機 （進行這個教學課程中，我們使用 c:\ssl）。</span><span class="sxs-lookup"><span data-stu-id="57054-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="57054-108">**Microsoft Internet Explorer 和 Microsoft Edge:** hello 下載完成之後，重新命名 hello 憑證 tooBaltimoreCyberTrustRoot.crt.pem。</span><span class="sxs-lookup"><span data-stu-id="57054-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="57054-109">步驟 2：繫結 SSL</span><span class="sxs-lookup"><span data-stu-id="57054-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="57054-110">連接使用透過 SSL 的 hello MySQL Workbench tooserver</span><span class="sxs-lookup"><span data-stu-id="57054-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="57054-111">設定 MySQL Workbench tooconnect 安全地透過 SSL。</span><span class="sxs-lookup"><span data-stu-id="57054-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="57054-112">瀏覽 toohello **SSL** hello MySQL Workbench 上 hello 安裝新的連接對話方塊中的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="57054-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="57054-113">輸入 hello 檔案位置的 hello **BaltimoreCyberTrustRoot.crt.pem**在 hello **SSL CA 檔案：**欄位。</span><span class="sxs-lookup"><span data-stu-id="57054-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="57054-114">![儲存自訂的圖格](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="57054-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="57054-115">連接使用透過 SSL 的 hello MySQL CLI tooserver</span><span class="sxs-lookup"><span data-stu-id="57054-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="57054-116">使用 hello MySQL 命令列介面時，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="57054-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="57054-117">步驟 3：強制在 Azure 中使用 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="57054-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="57054-118">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="57054-118">Using Azure portal</span></span>
<span data-ttu-id="57054-119">使用 hello Azure 入口網站，請瀏覽您的 Azure 資料庫的 MySQL server，然後按一下**連線安全性**。</span><span class="sxs-lookup"><span data-stu-id="57054-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="57054-120">使用 hello 切換按鈕 tooenable 或停用 hello**強制的 SSL 連線**設定。</span><span class="sxs-lookup"><span data-stu-id="57054-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="57054-121">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="57054-121">Then click **Save**.</span></span> <span data-ttu-id="57054-122">Microsoft 建議 tooalways 啟用**強制的 SSL 連線**增強式安全性設定。</span><span class="sxs-lookup"><span data-stu-id="57054-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="57054-123">![啟用 ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="57054-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="57054-124">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="57054-124">Using Azure CLI</span></span>
<span data-ttu-id="57054-125">您可以啟用或停用 hello **ssl 強制**參數分別使用 Azure CLI 中的已啟用或停用的值。</span><span class="sxs-lookup"><span data-stu-id="57054-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="57054-126">步驟 4：確認 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="57054-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="57054-127">執行 hello mysql**狀態**命令 tooverify 連接 tooyour MySQL 伺服器使用 SSL:</span><span class="sxs-lookup"><span data-stu-id="57054-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="57054-128">確認 hello 連接已加密藉由檢閱 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="57054-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="57054-129">輸出應該會顯示：**SSL：使用中的編碼器是 AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="57054-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="57054-130">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="57054-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="57054-131">PHP</span><span class="sxs-lookup"><span data-stu-id="57054-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="57054-132">Python</span><span class="sxs-lookup"><span data-stu-id="57054-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="57054-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57054-133">Next steps</span></span>
<span data-ttu-id="57054-134">檢閱[「適用於 MySQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項</span><span class="sxs-lookup"><span data-stu-id="57054-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
