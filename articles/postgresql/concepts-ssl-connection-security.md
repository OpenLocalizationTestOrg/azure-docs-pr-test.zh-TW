---
title: "aaaConfigure Azure PostgreSQL 資料庫中的 SSL 連線 |Microsoft 文件"
description: "指示和資訊 tooconfigure PostgreSQL 和相關聯的應用程式 tooproperly Azure 資料庫使用 SSL 連線。"
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="fc908-103">在適用於 PostgreSQL 的 Azure 資料庫中設定 SSL 連線能力</span><span class="sxs-lookup"><span data-stu-id="fc908-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="fc908-104">Azure PostgreSQL 資料庫偏好連接您的用戶端應用程式 toohello PostgreSQL 服務使用安全通訊端層 (SSL)。</span><span class="sxs-lookup"><span data-stu-id="fc908-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="fc908-105">強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。</span><span class="sxs-lookup"><span data-stu-id="fc908-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="fc908-106">根據預設，hello PostgreSQL 資料庫服務是設定的 toorequire SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fc908-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="fc908-107">（選擇性） 您可以停用來連接 tooyour 資料庫服務，如果用戶端應用程式不支援的 SSL 連線需要 SSL。</span><span class="sxs-lookup"><span data-stu-id="fc908-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="fc908-108">強制使用 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="fc908-108">Enforcing SSL connections</span></span>
<span data-ttu-id="fc908-109">PostgreSQL 伺服器 hello Azure 入口網站和 CLI 透過佈建的所有 Azure 資料庫，預設會都啟用強制的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fc908-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="fc908-110">同樣地，hello hello Azure 入口網站中的伺服器 下的 「 連接字串 」 設定中預先定義的連接字串包含通用語言 tooconnect tooyour 的資料庫伺服器使用 SSL 的 hello 必要參數。</span><span class="sxs-lookup"><span data-stu-id="fc908-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="fc908-111">hello SSL 參數而異 hello 連接器，例如"ssl = true"或"sslmode = 需要"或"sslmode = 必要 」 和其他變化。</span><span class="sxs-lookup"><span data-stu-id="fc908-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="fc908-112">設定強制使用 SSL</span><span class="sxs-lookup"><span data-stu-id="fc908-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="fc908-113">您可以選擇性地停用強制執行 SSL 連線能力。</span><span class="sxs-lookup"><span data-stu-id="fc908-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="fc908-114">Microsoft Azure 會建議 tooalways 啟用**強制的 SSL 連線**增強式安全性設定。</span><span class="sxs-lookup"><span data-stu-id="fc908-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="fc908-115">使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fc908-115">Using hello Azure portal</span></span>
<span data-ttu-id="fc908-116">瀏覽您適用於 PostgreSQL 的 Azure 資料庫伺服器，然後按一下 [連接安全性]。</span><span class="sxs-lookup"><span data-stu-id="fc908-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="fc908-117">使用 hello 切換按鈕 tooenable 或停用 hello**強制的 SSL 連線**設定。</span><span class="sxs-lookup"><span data-stu-id="fc908-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="fc908-118">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="fc908-118">Then click **Save**.</span></span> 

![連接安全性：停用強制執行 SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="fc908-120">您可以藉由檢視 hello 確認 hello 設定**概觀**頁面 toosee hello **SSL 強制執行狀態**指標。</span><span class="sxs-lookup"><span data-stu-id="fc908-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="fc908-121">使用 Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc908-121">Using Azure CLI</span></span>
<span data-ttu-id="fc908-122">您可以啟用或停用 hello **ssl 強制**參數使用`Enabled`或`Disabled`分別中 Azure CLI 的值。</span><span class="sxs-lookup"><span data-stu-id="fc908-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="fc908-123">確定您的應用程式或架構支援 SSL 連線</span><span class="sxs-lookup"><span data-stu-id="fc908-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="fc908-124">許多針對資料庫服務 (例如 Drupal 和 Django) 使用 PostgreSQL 的常見應用程式架構，預設不會在安裝期間啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="fc908-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="fc908-125">安裝完成後，或透過 CLI 命令特定 toohello 應用程式，必須完成啟用 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fc908-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="fc908-126">如果 PostgreSQL 伺服器強制的 SSL 連線，而且相關聯的 hello 應用程式未正確設定，hello 應用程式可能無法 tooconnect tooyour 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="fc908-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="fc908-127">請參閱您的應用程式文件 toolearn 如何 tooenable SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fc908-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="fc908-128">需要憑證驗證才能啟用 SSL 連線能力的應用程式</span><span class="sxs-lookup"><span data-stu-id="fc908-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="fc908-129">在某些情況下，應用程式需要安全地從受信任的憑證授權單位 (CA) 憑證檔案 (.cer) tooconnect 產生的本機憑證檔。</span><span class="sxs-lookup"><span data-stu-id="fc908-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="fc908-130">請參閱下列步驟 tooobtain hello.cer 檔 hello、 解碼 hello 憑證和 tooyour 應用程式繫結。</span><span class="sxs-lookup"><span data-stu-id="fc908-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="fc908-131">從憑證授權單位 (CA) hello 下載 hello 憑證檔案</span><span class="sxs-lookup"><span data-stu-id="fc908-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="fc908-132">hello 憑證所需 toocommunicate 透過 SSL 與您的 Azure 資料庫 PostgreSQL 伺服器所在[這裡](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt)。</span><span class="sxs-lookup"><span data-stu-id="fc908-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="fc908-133">下載 hello 憑證檔案儲存在本機。</span><span class="sxs-lookup"><span data-stu-id="fc908-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="fc908-134">在您的電腦上下載並安裝 OpenSSL</span><span class="sxs-lookup"><span data-stu-id="fc908-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="fc908-135">toodecode hello 憑證檔案安全地所需的應用程式 tooconnect tooyour 資料庫伺服器時，您需要在本機電腦上的 tooinstall OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="fc908-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="fc908-136">針對 Linux、OS X 或 Unix</span><span class="sxs-lookup"><span data-stu-id="fc908-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="fc908-137">hello OpenSSL 程式庫會提供來源的程式碼中直接 hello [OpenSSL Software Foundation](http://www.openssl.org)。</span><span class="sxs-lookup"><span data-stu-id="fc908-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="fc908-138">hello 下列指示引導您完成 hello 步驟需要 tooinstall OpenSSL Linux 電腦上。</span><span class="sxs-lookup"><span data-stu-id="fc908-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="fc908-139">這篇文章會使用已知 toowork 在 Ubuntu 12.04 和更新版本的命令。</span><span class="sxs-lookup"><span data-stu-id="fc908-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="fc908-140">開啟終端機工作階段並安裝 OpenSSL</span><span class="sxs-lookup"><span data-stu-id="fc908-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="fc908-141">從 hello 下載套件解壓縮 hello 檔案</span><span class="sxs-lookup"><span data-stu-id="fc908-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="fc908-142">輸入 hello 目錄 hello 檔案解壓縮的位置。</span><span class="sxs-lookup"><span data-stu-id="fc908-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="fc908-143">預設應該如下所示。</span><span class="sxs-lookup"><span data-stu-id="fc908-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="fc908-144">藉由執行下列命令的 hello 設定 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="fc908-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="fc908-145">如果您想與 /usr/local/openssl 不同資料夾中的 hello 檔案，請確定 toochange hello 遵循依適當情況。</span><span class="sxs-lookup"><span data-stu-id="fc908-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="fc908-146">既然 OpenSSL 的設定正確，您需要 toocompile 它 tooconvert 您的憑證。</span><span class="sxs-lookup"><span data-stu-id="fc908-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="fc908-147">toocompile，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc908-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="fc908-148">編譯完成之後，您可以準備 tooinstall OpenSSL 與可執行檔執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc908-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="fc908-149">tooconfirm 已成功安裝 OpenSSL 您系統上，執行的 hello 下列命令，請確定您取得 hello toomake 相同的輸出。</span><span class="sxs-lookup"><span data-stu-id="fc908-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="fc908-150">如果成功的話您應該會看到下列訊息的 hello。</span><span class="sxs-lookup"><span data-stu-id="fc908-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="fc908-151">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="fc908-151">For Windows</span></span>
<span data-ttu-id="fc908-152">在 Windows 電腦上安裝 OpenSSL 可依下列方式 hello:</span><span class="sxs-lookup"><span data-stu-id="fc908-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="fc908-153">**（建議選項）**使用中視窗 10 hello 內建撞 for Windows 功能和更新版本，預設會安裝 OpenSSL。</span><span class="sxs-lookup"><span data-stu-id="fc908-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="fc908-154">指示 tooenable 撞 for Windows 功能，在 Windows 10 中可以找到如何[這裡](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)。</span><span class="sxs-lookup"><span data-stu-id="fc908-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="fc908-155">透過下載 hello 社群所提供的 Win32/64 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc908-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="fc908-156">雖然 hello OpenSSL Software Foundation 不會提供或背書保證任何特定的 Windows 安裝程式，但會提供一份可用的安裝程式[這裡](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="fc908-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="fc908-157">將憑證檔案解碼</span><span class="sxs-lookup"><span data-stu-id="fc908-157">Decode your certificate file</span></span>
<span data-ttu-id="fc908-158">hello 下載檔案的加密格式的根 CA。</span><span class="sxs-lookup"><span data-stu-id="fc908-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="fc908-159">使用 OpenSSL toodecode hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="fc908-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="fc908-160">toodo，執行此 OpenSSL 命令：</span><span class="sxs-lookup"><span data-stu-id="fc908-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="fc908-161">使用 SSL 憑證驗證的連接 tooAzure PostgreSQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="fc908-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="fc908-162">既然您已成功解碼您的憑證，您可以現在 tooyour 資料庫伺服器安全地透過 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="fc908-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="fc908-163">tooallow 伺服器憑證驗證，hello 憑證必須放在 hello 檔案 ~/.postgresql/root.crt hello 使用者主目錄中。</span><span class="sxs-lookup"><span data-stu-id="fc908-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="fc908-164">（Microsoft Windows hello 檔案上名為 %appdata%\postgresql\root.crt。）。</span><span class="sxs-lookup"><span data-stu-id="fc908-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="fc908-165">hello 以下提供連接 PostgreSQL tooAzure 資料庫的指示。</span><span class="sxs-lookup"><span data-stu-id="fc908-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="fc908-166">目前沒有已知的問題。 如果您使用 「 sslmode = 確認完整 「 連線 toohello 服務，在 hello 連接將會失敗與 hello 下列錯誤：_伺服器憑證 」&lt;區域&gt;。control.database.windows.net 」 （和其他 7 的名稱） 不符合主機名稱"&lt;servername&gt;。 postgres.database.azure.com"。_</span><span class="sxs-lookup"><span data-stu-id="fc908-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="fc908-167">如果 「 sslmode = 確認完整"是必要，請使用 hello 伺服器命名慣例 **&lt;servername&gt;。.database.windows.net**為您的連接字串的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="fc908-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="fc908-168">我們計劃 tooremove hello 未來在這項限制。</span><span class="sxs-lookup"><span data-stu-id="fc908-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="fc908-169">使用其他連接[SSL 模式](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS)應該繼續 toouse hello 慣用主機命名慣例 **&lt;servername&gt;。 postgres.database.azure.com**。</span><span class="sxs-lookup"><span data-stu-id="fc908-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="fc908-170">使用 psql 命令列公用程式</span><span class="sxs-lookup"><span data-stu-id="fc908-170">Using psql command-line utility</span></span>
<span data-ttu-id="fc908-171">hello 下列範例會示範如何 toosuccessfully 連接 tooyour PostgreSQL 伺服器使用 hello psql 命令列公用程式。</span><span class="sxs-lookup"><span data-stu-id="fc908-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="fc908-172">使用 hello`root.crt`建立檔案和 hello`sslmode=verify-ca`或`sslmode=verify-full`選項。</span><span class="sxs-lookup"><span data-stu-id="fc908-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="fc908-173">使用 hello PostgreSQL 命令列介面時，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc908-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="fc908-174">如果成功的話，您會收到 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="fc908-174">If successful, you receive hello following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="fc908-175">使用 pgAdmin GUI 工具</span><span class="sxs-lookup"><span data-stu-id="fc908-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="fc908-176">透過 SSL 安全地設定 pgAdmin 4 tooconnect 需要 tooset hello`SSL mode = Verify-CA`或`SSL mode = Verify-Full`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="fc908-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![pgAdmin - 連接 - 需要 SSL 模式的螢幕擷取畫面](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="fc908-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc908-178">Next steps</span></span>
<span data-ttu-id="fc908-179">檢閱[適用於 PostgreSQL 之 Azure 資料庫的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項</span><span class="sxs-lookup"><span data-stu-id="fc908-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
