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
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a>在適用於 PostgreSQL 的 Azure 資料庫中設定 SSL 連線能力
Azure PostgreSQL 資料庫偏好連接您的用戶端應用程式 toohello PostgreSQL 服務使用安全通訊端層 (SSL)。 強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。

根據預設，hello PostgreSQL 資料庫服務是設定的 toorequire SSL 連線。 （選擇性） 您可以停用來連接 tooyour 資料庫服務，如果用戶端應用程式不支援的 SSL 連線需要 SSL。 

## <a name="enforcing-ssl-connections"></a>強制使用 SSL 連線
PostgreSQL 伺服器 hello Azure 入口網站和 CLI 透過佈建的所有 Azure 資料庫，預設會都啟用強制的 SSL 連線。 

同樣地，hello hello Azure 入口網站中的伺服器 下的 「 連接字串 」 設定中預先定義的連接字串包含通用語言 tooconnect tooyour 的資料庫伺服器使用 SSL 的 hello 必要參數。 hello SSL 參數而異 hello 連接器，例如"ssl = true"或"sslmode = 需要"或"sslmode = 必要 」 和其他變化。

## <a name="configure-enforcement-of-ssl"></a>設定強制使用 SSL
您可以選擇性地停用強制執行 SSL 連線能力。 Microsoft Azure 會建議 tooalways 啟用**強制的 SSL 連線**增強式安全性設定。

### <a name="using-hello-azure-portal"></a>使用 hello Azure 入口網站
瀏覽您適用於 PostgreSQL 的 Azure 資料庫伺服器，然後按一下 [連接安全性]。 使用 hello 切換按鈕 tooenable 或停用 hello**強制的 SSL 連線**設定。 然後按一下 [儲存] 。 

![連接安全性：停用強制執行 SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

您可以藉由檢視 hello 確認 hello 設定**概觀**頁面 toosee hello **SSL 強制執行狀態**指標。

### <a name="using-azure-cli"></a>使用 Azure CLI
您可以啟用或停用 hello **ssl 強制**參數使用`Enabled`或`Disabled`分別中 Azure CLI 的值。

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a>確定您的應用程式或架構支援 SSL 連線
許多針對資料庫服務 (例如 Drupal 和 Django) 使用 PostgreSQL 的常見應用程式架構，預設不會在安裝期間啟用 SSL。 安裝完成後，或透過 CLI 命令特定 toohello 應用程式，必須完成啟用 SSL 連線。 如果 PostgreSQL 伺服器強制的 SSL 連線，而且相關聯的 hello 應用程式未正確設定，hello 應用程式可能無法 tooconnect tooyour 資料庫伺服器。 請參閱您的應用程式文件 toolearn 如何 tooenable SSL 連線。


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a>需要憑證驗證才能啟用 SSL 連線能力的應用程式
在某些情況下，應用程式需要安全地從受信任的憑證授權單位 (CA) 憑證檔案 (.cer) tooconnect 產生的本機憑證檔。 請參閱下列步驟 tooobtain hello.cer 檔 hello、 解碼 hello 憑證和 tooyour 應用程式繫結。

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a>從憑證授權單位 (CA) hello 下載 hello 憑證檔案 
hello 憑證所需 toocommunicate 透過 SSL 與您的 Azure 資料庫 PostgreSQL 伺服器所在[這裡](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt)。 下載 hello 憑證檔案儲存在本機。

### <a name="download-and-install-openssl-on-your-machine"></a>在您的電腦上下載並安裝 OpenSSL 
toodecode hello 憑證檔案安全地所需的應用程式 tooconnect tooyour 資料庫伺服器時，您需要在本機電腦上的 tooinstall OpenSSL。

#### <a name="for-linux-os-x-or-unix"></a>針對 Linux、OS X 或 Unix
hello OpenSSL 程式庫會提供來源的程式碼中直接 hello [OpenSSL Software Foundation](http://www.openssl.org)。 hello 下列指示引導您完成 hello 步驟需要 tooinstall OpenSSL Linux 電腦上。 這篇文章會使用已知 toowork 在 Ubuntu 12.04 和更新版本的命令。

開啟終端機工作階段並安裝 OpenSSL
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
從 hello 下載套件解壓縮 hello 檔案
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
輸入 hello 目錄 hello 檔案解壓縮的位置。 預設應該如下所示。

```bash
cd openssl-1.1.0e
```
藉由執行下列命令的 hello 設定 OpenSSL。 如果您想與 /usr/local/openssl 不同資料夾中的 hello 檔案，請確定 toochange hello 遵循依適當情況。

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
既然 OpenSSL 的設定正確，您需要 toocompile 它 tooconvert 您的憑證。 toocompile，執行下列命令的 hello:

```bash
make
```
編譯完成之後，您可以準備 tooinstall OpenSSL 與可執行檔執行下列命令的 hello:
```bash
make install
```
tooconfirm 已成功安裝 OpenSSL 您系統上，執行的 hello 下列命令，請確定您取得 hello toomake 相同的輸出。

```bash
/usr/local/openssl/bin/openssl version
```
如果成功的話您應該會看到下列訊息的 hello。
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a>若為 Windows
在 Windows 電腦上安裝 OpenSSL 可依下列方式 hello:
1. **（建議選項）**使用中視窗 10 hello 內建撞 for Windows 功能和更新版本，預設會安裝 OpenSSL。 指示 tooenable 撞 for Windows 功能，在 Windows 10 中可以找到如何[這裡](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)。
2. 透過下載 hello 社群所提供的 Win32/64 應用程式。 雖然 hello OpenSSL Software Foundation 不會提供或背書保證任何特定的 Windows 安裝程式，但會提供一份可用的安裝程式[這裡](https://wiki.openssl.org/index.php/Binaries)

### <a name="decode-your-certificate-file"></a>將憑證檔案解碼
hello 下載檔案的加密格式的根 CA。 使用 OpenSSL toodecode hello 憑證檔案。 toodo，執行此 OpenSSL 命令：

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a>使用 SSL 憑證驗證的連接 tooAzure PostgreSQL 資料庫
既然您已成功解碼您的憑證，您可以現在 tooyour 資料庫伺服器安全地透過 SSL 連線。 tooallow 伺服器憑證驗證，hello 憑證必須放在 hello 檔案 ~/.postgresql/root.crt hello 使用者主目錄中。 （Microsoft Windows hello 檔案上名為 %appdata%\postgresql\root.crt。）。 hello 以下提供連接 PostgreSQL tooAzure 資料庫的指示。

> [!NOTE]
> 目前沒有已知的問題。 如果您使用 「 sslmode = 確認完整 「 連線 toohello 服務，在 hello 連接將會失敗與 hello 下列錯誤：_伺服器憑證 」&lt;區域&gt;。control.database.windows.net 」 （和其他 7 的名稱） 不符合主機名稱"&lt;servername&gt;。 postgres.database.azure.com"。_
> 如果 「 sslmode = 確認完整"是必要，請使用 hello 伺服器命名慣例 **&lt;servername&gt;。.database.windows.net**為您的連接字串的主機名稱。 我們計劃 tooremove hello 未來在這項限制。 使用其他連接[SSL 模式](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS)應該繼續 toouse hello 慣用主機命名慣例 **&lt;servername&gt;。 postgres.database.azure.com**。

#### <a name="using-psql-command-line-utility"></a>使用 psql 命令列公用程式
hello 下列範例會示範如何 toosuccessfully 連接 tooyour PostgreSQL 伺服器使用 hello psql 命令列公用程式。 使用 hello`root.crt`建立檔案和 hello`sslmode=verify-ca`或`sslmode=verify-full`選項。

使用 hello PostgreSQL 命令列介面時，執行下列命令的 hello:
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
如果成功的話，您會收到 hello 下列輸出：
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

#### <a name="using-pgadmin-gui-tool"></a>使用 pgAdmin GUI 工具
透過 SSL 安全地設定 pgAdmin 4 tooconnect 需要 tooset hello`SSL mode = Verify-CA`或`SSL mode = Verify-Full`，如下所示：

![pgAdmin - 連接 - 需要 SSL 模式的螢幕擷取畫面](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a>後續步驟
檢閱[適用於 PostgreSQL 之 Azure 資料庫的連線庫](concepts-connection-libraries.md)後面的各種應用程式連線能力選項
