---
title: "設定 SSL 連線能力，以安全地連線到適用於 MySQL 的 Azure 資料庫 | Microsoft Docs"
description: "有關如何適當設定「適用於 MySQL 的 Azure 資料庫」及相關聯應用程式以適當使用 SSL 連線的指示"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 77e1b6266a2cf47949fa06358ec003f6b6b38065
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ssl-connectivity-in-your-application-to-securely-connect-to-azure-database-for-mysql"></a><span data-ttu-id="6044e-103">在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="6044e-103">Configure SSL connectivity in your application to securely connect to Azure Database for MySQL</span></span>
<span data-ttu-id="6044e-104">適用於 MySQL 的 Azure 資料庫支援使用安全通訊端層 (SSL)，將適用於 MySQL 的 Azure 資料庫伺服器連線至用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="6044e-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="6044e-105">在您的資料庫伺服器和用戶端應用程式之間強制使用 SSL 連線，可將伺服器與應用程式之間的資料流加密，有助於抵禦「中間人」攻擊。</span><span class="sxs-lookup"><span data-stu-id="6044e-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="6044e-106">步驟 1：取得 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="6044e-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="6044e-107">從 [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) 下載要透過 SSL 與 Azure Database for MySQL 伺服器通訊所需的憑證，並將該憑證檔儲存到本機磁碟機 (在此教學課程中，我們使用 c:\ssl)。</span><span class="sxs-lookup"><span data-stu-id="6044e-107">Download the certificate needed to communicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save the certificate file to your local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="6044e-108">**針對 Microsoft Internet Explorer 和 Microsoft Edge：**在下載完成後，請將憑證重新命名為 BaltimoreCyberTrustRoot.crt.pem。</span><span class="sxs-lookup"><span data-stu-id="6044e-108">**For Microsoft Internet Explorer and Microsoft Edge:** After the download has completed, rename the certificate to BaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="6044e-109">步驟 2：繫結 SSL</span><span class="sxs-lookup"><span data-stu-id="6044e-109">Step 2: Bind SSL</span></span>
### <a name="connecting-to-server-using-the-mysql-workbench-over-ssl"></a><span data-ttu-id="6044e-110">使用 MySQL Workbench 透過 SSL 連線至伺服器</span><span class="sxs-lookup"><span data-stu-id="6044e-110">Connecting to server using the MySQL Workbench over SSL</span></span>
<span data-ttu-id="6044e-111">設定使 MySQL Workbench 安全地透過 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="6044e-111">Configure MySQL Workbench to connect securely over SSL.</span></span> <span data-ttu-id="6044e-112">瀏覽至 MySQL Workbench [設定新連線] 對話方塊中的 [SSL] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6044e-112">Navigate to the **SSL** tab in the MySQL Workbench on the Setup New Connection dialogue.</span></span> <span data-ttu-id="6044e-113">在 [SSL CA 檔案:] 欄位中輸入 **BaltimoreCyberTrustRoot.crt.pem** 的檔案位置。</span><span class="sxs-lookup"><span data-stu-id="6044e-113">Enter the file location of the **BaltimoreCyberTrustRoot.crt.pem** in the **SSL CA File:** field.</span></span>
<span data-ttu-id="6044e-114">![儲存自訂的圖格](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="6044e-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-to-server-using-the-mysql-cli-over-ssl"></a><span data-ttu-id="6044e-115">使用 MySQL CLI 透過 SSL 連線至伺服器</span><span class="sxs-lookup"><span data-stu-id="6044e-115">Connecting to server using the MySQL CLI over SSL</span></span>
<span data-ttu-id="6044e-116">使用 MySQL 命令列介面，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="6044e-116">Using the MySQL command-line interface, execute the following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="6044e-117">步驟 3：強制在 Azure 中使用 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="6044e-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="6044e-118">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6044e-118">Using Azure portal</span></span>
<span data-ttu-id="6044e-119">使用 Azure 入口網站，瀏覽適用於 MySQL 的 Azure 資料庫伺服器，然後按一下 [連線安全性]。</span><span class="sxs-lookup"><span data-stu-id="6044e-119">Using the Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="6044e-120">使用切換按鈕來啟用或停用 [強制使用 SSL 連線] 設定。</span><span class="sxs-lookup"><span data-stu-id="6044e-120">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="6044e-121">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="6044e-121">Then click **Save**.</span></span> <span data-ttu-id="6044e-122">Microsoft 建議一律啟用 [強制使用 SSL 連線] 設定，以增強安全性。</span><span class="sxs-lookup"><span data-stu-id="6044e-122">Microsoft recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="6044e-123">![啟用 ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="6044e-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="6044e-124">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6044e-124">Using Azure CLI</span></span>
<span data-ttu-id="6044e-125">您可以在 Azure CLI 中分別使用 Enabled 或 Disabled 值，以啟用或停用 **ssl-enforcement** 參數。</span><span class="sxs-lookup"><span data-stu-id="6044e-125">You can enable or disable the **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="6044e-126">步驟 4：確認 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="6044e-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="6044e-127">執行 mysql **status** 命令，確認您已使用 SSL 連線至 MySQL 伺服器︰</span><span class="sxs-lookup"><span data-stu-id="6044e-127">Execute the mysql **status** command to verify that you have connected to your MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="6044e-128">檢閱輸出來確認連線已加密。</span><span class="sxs-lookup"><span data-stu-id="6044e-128">Confirm the connection is encrypted by reviewing the output.</span></span> <span data-ttu-id="6044e-129">輸出應該會顯示：**SSL：使用中的編碼器是 AES256-SHA**</span><span class="sxs-lookup"><span data-stu-id="6044e-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="6044e-130">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="6044e-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="6044e-131">PHP</span><span class="sxs-lookup"><span data-stu-id="6044e-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="6044e-132">Python</span><span class="sxs-lookup"><span data-stu-id="6044e-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="6044e-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6044e-133">Next steps</span></span>
<span data-ttu-id="6044e-134">檢閱[「適用於 MySQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項</span><span class="sxs-lookup"><span data-stu-id="6044e-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
