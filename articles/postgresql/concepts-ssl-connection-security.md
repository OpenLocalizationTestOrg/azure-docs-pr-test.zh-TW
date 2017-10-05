---
title: "在適用於 PostgreSQL 的 Azure 資料庫中設定 SSL 連線能力 | Microsoft Docs"
description: "用以設定適用於 PostgreSQL 之 Azure 資料庫及相關聯應用程式以適當使用 SSL 連接的指示與資訊。"
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="9ac96-103">在適用於 PostgreSQL 的 Azure 資料庫中設定 SSL 連線能力</span><span class="sxs-lookup"><span data-stu-id="9ac96-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="9ac96-104">適用於 PostgreSQL 的 Azure 資料庫偏好使用安全通訊端層 (SSL)，來將用戶端應用程式連接到 PostgreSQL 服務。</span><span class="sxs-lookup"><span data-stu-id="9ac96-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="9ac96-105">在您的資料庫伺服器和用戶端應用程式之間強制執行 SSL 連接，有助於藉由將伺服器與您應用程式之間的資料流加密，來提供保護以抵禦「中間人」攻擊。</span><span class="sxs-lookup"><span data-stu-id="9ac96-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="9ac96-106">預設會將 PostgreSQL 資料庫服務設定為需要 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="9ac96-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="9ac96-107">(選擇性) 如果您的用戶端應用程式不支援 SSL 連線能力，您可以停用需要 SSL 才能連接到您資料庫服務的功能。</span><span class="sxs-lookup"><span data-stu-id="9ac96-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="9ac96-108">強制執行 SSL 連接</span><span class="sxs-lookup"><span data-stu-id="9ac96-108">Enforcing SSL connections</span></span>
<span data-ttu-id="9ac96-109">針對透過 Azure 入口網站和 CLI 佈建之所有適用於 PostgreSQL 的 Azure 資料庫伺服器，預設會啟用強制執行 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="9ac96-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="9ac96-110">同樣地，您在 Azure 入口網站的伺服器下方 [連接字串] 設定中預先定義的連接字串，會包含通用語言使用 SSL 連接到您資料庫伺服器所需的必要參數。</span><span class="sxs-lookup"><span data-stu-id="9ac96-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="9ac96-111">SSL 參數會根據連接器而有所不同，例如，"ssl=true" 或 "sslmode=require" 或 "sslmode=required" 及其他變化。</span><span class="sxs-lookup"><span data-stu-id="9ac96-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="9ac96-112">設定強制執行 SSL</span><span class="sxs-lookup"><span data-stu-id="9ac96-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="9ac96-113">您可以選擇性地停用強制執行 SSL 連線能力。</span><span class="sxs-lookup"><span data-stu-id="9ac96-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="9ac96-114">Microsoft Azure 建議您一律啟用 [強制執行 SSL 連接] 設定，以取得增強的安全性。</span><span class="sxs-lookup"><span data-stu-id="9ac96-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="9ac96-115">使用 Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9ac96-115">Using the Azure portal</span></span>
<span data-ttu-id="9ac96-116">瀏覽您適用於 PostgreSQL 的 Azure 資料庫伺服器，然後按一下 [連接安全性]。</span><span class="sxs-lookup"><span data-stu-id="9ac96-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="9ac96-117">使用切換按鈕來啟用或停用 [強制執行 SSL 連接] 設定。</span><span class="sxs-lookup"><span data-stu-id="9ac96-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="9ac96-118">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9ac96-118">Then click **Save**.</span></span> 

![連接安全性：停用強制執行 SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="9ac96-120">您可以檢視 [概觀] 頁面來查看 [SSL 強制執行狀態] 指標，藉以確認設定。</span><span class="sxs-lookup"><span data-stu-id="9ac96-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="9ac96-121">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9ac96-121">Using Azure CLI</span></span>
<span data-ttu-id="9ac96-122">您可以在 Azure CLI 中分別使用 `Enabled` 或 `Disabled` 值，來啟用或停用 **sssl-enforcement** 參數。</span><span class="sxs-lookup"><span data-stu-id="9ac96-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="9ac96-123">確定您的應用程式或架構支援 SSL 連接</span><span class="sxs-lookup"><span data-stu-id="9ac96-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="9ac96-124">許多針對資料庫服務 (例如 Drupal 和 Django) 使用 PostgreSQL 的常見應用程式架構，預設不會在安裝期間啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="9ac96-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="9ac96-125">啟用 SSL 連線能力必須在安裝完成之後完成，或者透過應用程式特定的 CLI 命令來完成。</span><span class="sxs-lookup"><span data-stu-id="9ac96-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="9ac96-126">如果您的 PostgreSQL 伺服器正強制執行 SSL 連接，且未正確設定相關聯的應用程式，則應用程式可能無法連接到您的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ac96-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="9ac96-127">請參閱您的應用程式文件，以了解如何啟用 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="9ac96-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="9ac96-128">需要憑證驗證才能啟用 SSL 連線能力的應用程式</span><span class="sxs-lookup"><span data-stu-id="9ac96-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="9ac96-129">在某些情況下，應用程式需要從受信任憑證授權單位 (CA) 憑證檔案 (.cer) 所產生的本機憑證檔，才能安全地連接。</span><span class="sxs-lookup"><span data-stu-id="9ac96-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="9ac96-130">請參閱下列步驟來取得 .cer 檔案、解碼憑證，並將它繫結至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ac96-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="9ac96-131">從憑證授權單位 (CA) 下載憑證檔</span><span class="sxs-lookup"><span data-stu-id="9ac96-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="9ac96-132">您可以在[這裡](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt)找到要透過 SSL 與您適用於 PostgreSQL 之 Azure 資料庫伺服器通訊所需的憑證。</span><span class="sxs-lookup"><span data-stu-id="9ac96-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="9ac96-133">本機下載憑證檔。</span><span class="sxs-lookup"><span data-stu-id="9ac96-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="9ac96-134">在您的電腦上下載並安裝 OpenSSL</span><span class="sxs-lookup"><span data-stu-id="9ac96-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="9ac96-135">若要將應用程式所需的憑證檔解碼以便安全地連接到您的資料庫伺服器，您需要在本機電腦上安裝 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="9ac96-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="9ac96-136">針對 Linux、OS X 或 Unix</span><span class="sxs-lookup"><span data-stu-id="9ac96-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="9ac96-137">[OpenSSL Software Foundation (英文)](http://www.openssl.org) 中會以原始程式碼形式直接提供 OpenSSL 程式庫。</span><span class="sxs-lookup"><span data-stu-id="9ac96-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="9ac96-138">下列指示會引導您逐步完成在 Linux 電腦上安裝 OpenSSL 的必要步驟。</span><span class="sxs-lookup"><span data-stu-id="9ac96-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="9ac96-139">這篇文章會使用已知可在 Ubuntu 12.04 和更新版本上運作的命令。</span><span class="sxs-lookup"><span data-stu-id="9ac96-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="9ac96-140">開啟終端機工作階段，然後安裝 OpenSSL</span><span class="sxs-lookup"><span data-stu-id="9ac96-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="9ac96-141">從下載套件中將檔案解壓縮</span><span class="sxs-lookup"><span data-stu-id="9ac96-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="9ac96-142">進入已解壓縮檔案的目錄。</span><span class="sxs-lookup"><span data-stu-id="9ac96-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="9ac96-143">它預設應該如下。</span><span class="sxs-lookup"><span data-stu-id="9ac96-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="9ac96-144">執行下列命令來設定 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="9ac96-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="9ac96-145">如果您想要使用與 /usr/local/openssl 不同資料夾中的檔案，請務必適當地變更下列內容。</span><span class="sxs-lookup"><span data-stu-id="9ac96-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="9ac96-146">既然已正確設定 OpenSSL，則您需要編譯它來轉換憑證。</span><span class="sxs-lookup"><span data-stu-id="9ac96-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="9ac96-147">若要進行編譯，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9ac96-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="9ac96-148">編譯完成之後，您就可以執行下列命令，以可執行檔形式安裝 OpenSSL：</span><span class="sxs-lookup"><span data-stu-id="9ac96-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="9ac96-149">若要確認您已在系統上成功安裝 OpenSSL，請執行下列命令，然後檢查以確定您得到相同的輸出。</span><span class="sxs-lookup"><span data-stu-id="9ac96-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="9ac96-150">如果成功，您應該會看到下列訊息。</span><span class="sxs-lookup"><span data-stu-id="9ac96-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="9ac96-151">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="9ac96-151">For Windows</span></span>
<span data-ttu-id="9ac96-152">在 Windows 電腦上安裝 OpenSSL，可使用下列方式來完成：</span><span class="sxs-lookup"><span data-stu-id="9ac96-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="9ac96-153">**(建議)** 在 Window 10 和更新版本中使用內建的 Bash for Windows 功能，預設會安裝 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="9ac96-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="9ac96-154">您可以在[這裡](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)找到如何在 Window 10 啟用 Bash for Windows 功能的指示。</span><span class="sxs-lookup"><span data-stu-id="9ac96-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="9ac96-155">透過下載社群所提供的 Win32/64 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ac96-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="9ac96-156">雖然 OpenSSL Software Foundation 不會提供任何特定的 Windows 安裝程式或為其背書，但會在[這裡 (英文)](https://wiki.openssl.org/index.php/Binaries) 提供一份可用的安裝程式</span><span class="sxs-lookup"><span data-stu-id="9ac96-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="9ac96-157">將憑證檔案解碼</span><span class="sxs-lookup"><span data-stu-id="9ac96-157">Decode your certificate file</span></span>
<span data-ttu-id="9ac96-158">下載的根 CA 檔案是加密格式。</span><span class="sxs-lookup"><span data-stu-id="9ac96-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="9ac96-159">使用 OpenSSL 來將憑證檔案解碼。</span><span class="sxs-lookup"><span data-stu-id="9ac96-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="9ac96-160">若要這樣做，請執行此 OpenSSL 命令：</span><span class="sxs-lookup"><span data-stu-id="9ac96-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="9ac96-161">使用 SSL 憑證驗證連接至適用於 PostgreSQL 的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="9ac96-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="9ac96-162">既然您已成功將憑證解碼，您現在可以透過 SSL 安全地連接到資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ac96-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="9ac96-163">若要允許伺服器憑證驗證，憑證必須放置於使用者主目錄上的 ~/.postgresql/root.crt 檔案中</span><span class="sxs-lookup"><span data-stu-id="9ac96-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="9ac96-164">(在 Microsoft Windows 上，此檔案會命名為 %APPDATA%\postgresql\root.crt)。</span><span class="sxs-lookup"><span data-stu-id="9ac96-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="9ac96-165">以下提供連接到適用於 PostgreSQL 之 Azure 資料庫的指示。</span><span class="sxs-lookup"><span data-stu-id="9ac96-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="9ac96-166">目前有個已知問題，如果您在對服務的連線中使用「sslmode=verify-full」，連線會失敗，並出現下列錯誤：_"&lt;區域&gt;.control.database.windows.net" (和其他 7 個名稱) 的伺服器憑證，不符合主機名稱 "&lt;伺服器名稱&gt;.postgres.database.azure.com"。_</span><span class="sxs-lookup"><span data-stu-id="9ac96-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="9ac96-167">如果一定要使用「sslmode=verify-full」，請使用伺服器名稱慣例 **&lt;伺服器名稱&gt;.database.windows.net** 來作為連接字串的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="9ac96-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="9ac96-168">我們計劃在未來移除這項限制。</span><span class="sxs-lookup"><span data-stu-id="9ac96-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="9ac96-169">使用其他 [SSL 模式](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS)的連線請繼續使用常用的主機命名慣例 **&lt;伺服器名稱&gt;.postgres.database.azure.com**。</span><span class="sxs-lookup"><span data-stu-id="9ac96-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="9ac96-170">使用 psql 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="9ac96-170">Using psql command-line utility</span></span>
<span data-ttu-id="9ac96-171">下列範例會示範如何使用 psql 命令列公用程式，來成功地連線到 PostgreSQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9ac96-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="9ac96-172">使用所建立的 `root.crt` 檔案和 `sslmode=verify-ca` 或 `sslmode=verify-full` 選項。</span><span class="sxs-lookup"><span data-stu-id="9ac96-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="9ac96-173">使用 PostgreSQL 命令列介面，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="9ac96-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="9ac96-174">如果成功，您應該會收到下列輸出：</span><span class="sxs-lookup"><span data-stu-id="9ac96-174">If successful, you receive the following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="9ac96-175">使用 pgAdmin GUI 工具</span><span class="sxs-lookup"><span data-stu-id="9ac96-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="9ac96-176">若要將 pgAdmin 4 設定為透過 SSL 進行安全連線，您必須如下所示地設定 `SSL mode = Verify-CA` 或 `SSL mode = Verify-Full`：</span><span class="sxs-lookup"><span data-stu-id="9ac96-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![pgAdmin - 連接 - 需要 SSL 模式的螢幕擷取畫面](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="9ac96-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ac96-178">Next steps</span></span>
<span data-ttu-id="9ac96-179">檢閱[適用於 PostgreSQL 之 Azure 資料庫的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項</span><span class="sxs-lookup"><span data-stu-id="9ac96-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
