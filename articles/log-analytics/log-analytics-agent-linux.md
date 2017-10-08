---
title: "aaaConnect 您的 Linux 電腦 tooOperations Management Suite (OMS) |Microsoft 文件"
description: "本文說明如何 tooconnect Linux 電腦裝載於 Azure、 其他雲端或內部部署 tooOMS 使用 hello OMS Agent for Linux。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>連接您的 Linux 電腦 tooOperations Management Suite (OMS) 

透過 Microsoft Operations Management Suite (OMS)，您可以收集從下列位置產生的資料，並對資料採取動作：從 Linux 電腦；存放在內部部署資料中心做為實體伺服器或虛擬機器的容器解決方案，如 Docker；如 Amazon Web Services (AWS) 或 Microsoft Azure 等雲端託管服務中的虛擬機器。 您也可以使用變更追蹤，tooidentify 組態變更，例如在 OMS 中可用的管理解決方案，並更新管理 toomanage 軟體更新 tooproactively 管理的 Linux Vm 的 hello 生命週期。 

hello OMS Agent for Linux 通訊會透過 TCP 連接埠 443，輸出以 hello OMS 服務，而且如果 hello 電腦透過 hello 網際網路，連線 tooa 防火牆或 proxy 伺服器 toocommunicate 檢閱[設定用於 HTTP proxy 的 hello 代理程式伺服器或閘道 OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand 何種設定變更必須套用 toobe。  如果您要監視 hello 與 System Center 2016-Operations Manager 或 Operations Manager 2012 R2 的電腦可以是多重主目錄 hello OMS 服務 toocollect 資料與正向 toohello 服務並仍由 Operations Manager 監視。  由整合與 OMS 的 Operations Manager 管理群組監視的 Linux 電腦不會收到資料來源的組態，並收集轉寄透過 hello 管理群組的資料。  hello OMS 代理程式不能設定的 tooreport toomore 比一個工作區。  

如果您的 IT 安全性原則不允許您的網路 tooconnect toohello 網際網路上的電腦，hello 代理程式可以設定的 tooconnect toohello OMS 閘道 tooreceive 組態資訊和傳送收集的資料，取決於您擁有 hello 解決方案啟用。 如需詳細資訊以及有關如何 tooconfigure 您的 OMS Linux 代理程式 toocommunicate 透過 OMS 閘道 toohello OMS 服務，請參閱步驟[連接使用 hello OMS 閘道電腦 tooOMS](log-analytics-oms-gateway.md)。  

hello 下列圖表描述 hello hello 代理程式管理的 Linux 電腦和 OMS，包括 hello 方向和連接埠之間的連線。

![代理程式直接與 OMS 通訊的圖表](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>系統需求
開始之前，請檢閱下列符合 hello 必要條件的詳細資料 tooverify hello。

### <a name="supported-linux-operating-systems"></a>支援的 Linux 作業系統
hello 下列 Linux 發佈都正式支援。  不過，其他未列出的發佈也可能執行 OMS Agent for Linux hello。

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5、6 和 7 (x86/x64)
* Oracle Linux 5、6 和 7 (x86/x64)
* Red Hat Enterprise Linux Server 5、6 和 7 (x86/x64)
* Debian GNU/Linux 6、7 和 8 (x86/x64)
* Ubuntu 12.04 LTS、14.04 LTS、15.04、15.10、16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 和 12 (x86/x64)

### <a name="network"></a>網路
hello 資訊底下清單 hello proxy 和防火牆設定資訊所需的 hello Linux 代理程式 toocommunicate 與 OMS。 已從您的網路 toohello OMS 服務的輸出流量。 

|代理程式資源| 連接埠 |  
|------|---------|  
|*.ods.opinsights.azure.com | 連接埠 443|   
|*.oms.opinsights.azure.com | 連接埠 443|   
|*.blob.core.windows.net/ | 連接埠 443|   
|*.azure-automation.net | 連接埠 443|  

### <a name="package-requirements"></a>封裝需求

 **必要封裝**   | **說明**   | **最低版本**
--------------------- | --------------------- | -------------------
Glibc | GNU C 程式庫   | 2.5-12 
Openssl | OpenSSL 程式庫 | 0.9.8e 或 1.0
Curl | cURL Web 用戶端 | 7.15.5
Python-ctypes | | 
PAM | 插入式驗證模組 | 

> [!NOTE]
>  需要 rsyslog 或 syslog-ng 是必要的 toocollect syslog 訊息。 在第 5 版 Red Hat Enterprise Linux、 CentOS 和 Oracle Linux 版本 (sysklog) 上的 hello 預設 syslog 服務精靈不支援 syslog 事件收集。 toocollect syslog 資料，從這一版的這些發佈，hello rsyslog 精靈應該安裝和設定 tooreplace sysklog 

hello 代理程式包含多個封裝。 hello 發行檔案包含下列套件，以執行 hello 殼層配套 hello `--extract`:

**Package** | **版本** | **說明**
----------- | ----------- | --------------
omsagent | 1.4.0 | hello Operations Management Suite Agent for Linux
omsconfig | 1.1.1 | Hello OMS 代理程式的設定代理程式
omi | 1.2.0 | 開放式管理基礎結構 (OMI) - 輕量型 CIM 伺服器
scx | 1.6.3 | 作業系統效能計量的 OMI CIM 提供者
apache-cimprov | 1.0.1 | OMI 的 Apache HTTP 伺服器效能監視提供者。 在偵測到 Apache HTTP 伺服器時安裝。
mysql-cimprov | 1.0.1 | OMI 的 MySQL 伺服器效能監視提供者。 在偵測到 MySQL/MariaDB 伺服器時安裝。
docker-cimprov | 1.0.0 | OMI 的 Docker 提供者。 在偵測到 Docker 時安裝。

### <a name="compatibility-with-system-center-operations-manager"></a>與 System Center Operations Manager 的相容性
hello OMS Agent for Linux 與 hello System Center Operations Manager 代理程式共用代理程式二進位檔。 如果您安裝 hello OMS Agent for Linux 目前由 Operations Manager 管理的系統上，它會 hello hello 電腦 tooa 較新版本的 OMI 和 SCX 封裝。 這個版本、 hello OMS 與 System Center 2016-適用於 Linux 的 Operations Manager/Operations Manager 2012 R2 代理程式都相容。 

> [!NOTE]
> System Center 2012 SP1 和較早版本。 目前不相容或支援以 hello OMS Agent for Linux<br>
> 如果 hello OMS Agent for Linux 安裝的 tooa 目前不是由 Operations Manager 監視的電腦，然後想 toomonitor hello 電腦與 Operations Manager，您就必須修改 hello [OMI 設定](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager)先前toodiscovering hello 電腦。 **這是步驟*不*如果 hello Operations Manager 代理程式安裝之前 hello OMS Agent for Linux 需要。**

### <a name="system-configuration-changes"></a>系統組態變更
在安裝之後 hello OMS Agent for Linux 套件，hello 下列全系統設定變更會套用。 解除安裝 hello omsagent 套件時，會移除這些成品。

* 會建立名為 `omsagent` 的非特殊權限使用者。 這是 hello hello omsagent 精靈執行的帳戶做為。
* sudoers “include” 檔案建立在 /etc/sudoers.d/omsagent。 這會授權 omsagent toorestart hello syslog 和 omsagent 精靈。 如果 sudo 安裝 hello 版本不支援 sudo"include"指示詞，這些項目會寫入太/等/sudoers。
* hello syslog 組態是修改的 tooforward 事件 toohello 代理程式的子集。 如需詳細資訊，請參閱 hello**設定資料收集**下一節

### <a name="upgrade-from-a-previous-release"></a>從舊版升級
此版本支援從 1.0.0-47 之前的版本升級。 執行以 hello hello 安裝`--upgrade`命令升級 hello 代理程式 toohello 最新版本的所有元件。

## <a name="installing-hello-agent"></a>Hello 代理程式安裝

本章節描述如何 tooinstall hello OMS Agent for Linux 使用 bunndle，其中包含 Debian 和 RPM 封裝每一個 hello 代理程式元件。  它可以直接安裝，或擷取 tooretrieve hello 個別封裝。  

您首先需要您的 OMS 工作區識別碼和金鑰，您可以藉由切換 toohello 找到[OMS 傳統入口網站](https://mms.microsoft.com)。  在 [hello**概觀**從 hello 上方功能表中選取] 頁面上，**設定**，然後瀏覽過**連接 Sources\Linux 伺服器**。  您會看到 hello 值 toohello 右邊的**工作區識別碼**和**主索引鍵**。  將兩者複製並貼到您最愛的編輯器。    

1. 最新版本下載 hello [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh)或[OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh)從 GitHub。  
2. 傳送嗨適當的配套 （x86 或 x64） tooyour Linux 電腦使用 scp/sftp 來進行。
3. 安裝 hello 組合使用 hello`--install`或`--upgrade`引數。 

    > [!NOTE]
    > 例如，當已安裝適用於 Linux 的 hello System Center Operations Manager 代理程式安裝任何現有的封裝，如果使用 hello`--upgrade`引數。 在安裝期間，tooconnect tooOperations Management Suite 提供 hello`-w <WorkspaceID>`和`-s <Shared Key>`參數。


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall 並將產品上架直接
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>tooupgrade hello 代理程式套件
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall 和美國政府雲端中的上架 tooa 工作區
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>設定 HTTP proxy 伺服器或 OMS 閘道使用的 hello 代理程式
hello OMS Agent for Linux 支援透過 HTTP 或 HTTPS 的 proxy 伺服器或閘道 OMS toohello OMS 服務進行通訊。  不支援匿名和基本驗證 (使用者名稱/密碼)。  

### <a name="proxy-configuration"></a>Proxy 組態
hello proxy 組態值具有 hello，請使用下列語法：

`[protocol://][user:password@]proxyhost[:port]`

屬性|說明
-|-
通訊協定|http 或 https
user|用於驗證 Proxy 的選擇性使用者名稱
password|用於驗證 Proxy 的選擇性密碼
proxyhost|Hello proxy 伺服器/OMS 閘道的位址或者 FQDN
連接埠|選擇性的連接埠號碼為 hello proxy 伺服器/OMS 閘道

例如：`http://user01:password@proxy01.contoso.com:8080`

在安裝期間或安裝後修改 hello proxy.conf 組態檔，可以指定 hello proxy 伺服器。   

### <a name="specify-proxy-configuration-during-installation"></a>安裝期間指定 Proxy 組態
hello`-p`或`--proxy`hello omsagent 安裝配套的引數指定 hello proxy 組態 toouse。 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>在檔案中定義 hello proxy 設定
hello proxy 組態可以設定在 hello 檔案`/etc/opt/microsoft/omsagent/proxy.conf`和`/etc/opt/microsoft/omsagent/conf/proxy.conf `。 hello 檔案可以直接建立或編輯，但其權限必須是更新的 toogrant hello omiuser 使用者 hello 檔案讀取權限。 例如：
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>正在移除 hello proxy 設定
tooremove 先前定義的 proxy 設定並還原 toodirect 連線之後，移除 hello proxy.conf 檔案：
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>透過 Operations Management Suite 上架
如果 hello 配套安裝期間未提供工作區識別碼和金鑰，hello 代理程式必須接著向 Operations Management Suite。

### <a name="onboarding-using-hello-command-line"></a>使用 hello 命令列的上架
執行提供 hello 工作區識別碼 hello omsadmin.sh 命令，並為您工作區金鑰。 此命令必須以根身分 (具有 sudo 提升權限) 執行：
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>使用檔案上架
1.  建立 hello 檔案`/etc/omsagent-onboard.conf`。 hello 檔案必須是可讀取和寫入的根。
`sudo vi /etc/omsagent-onboard.conf`
2.  插入下列行 hello 與工作區識別碼和共用金鑰的檔案中的 hello:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  執行下列命令 tooOnboard tooOMS hello:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  在順利上架上刪除 hello 檔案。

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>啟用 hello OMS Agent for Linux tooreport tooSystem Center Operations Manager
執行下列步驟 tooconfigure hello OMS Agent for Linux tooreport tooa System Center Operations Manager 管理群組的 hello。  

1. 編輯 hello 檔案`/etc/opt/omi/conf/omiserver.conf`
2. 請確定該 hello 行首**httpsport =**定義 hello 連接埠 1270年。 例如：`httpsport=1270`
3. 重新啟動 hello OMI 伺服器：`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>代理程式記錄檔
hello 記錄檔的 hello OMS Agent for Linux，請參閱： `/var/opt/microsoft/omsagent/<workspace id>/log/` hello omsconfig （代理程式組態） 程式可以找到在 hello 記錄檔： `/var/opt/microsoft/omsconfig/log/` hello OMI 和 SCX 元件 （提供效能標準資料） 的記錄檔，請參閱：`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>記錄輪替組態##
omsagent 的 hello 記錄旋轉組態，請參閱：`/etc/logrotate.d/omsagent-<workspace id>`

hello 預設設定是： 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>解除安裝 hello OMS Agent for Linux
hello 代理程式套件可以解除安裝執行 hello 配套.sh 檔案與 hello`--purge`引數，這完全從 hello 電腦中移除 hello 代理程式和其組態。   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>疑難排解

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>問題： 無法 tooconnect 透過 proxy tooOMS

#### <a name="probable-causes"></a>可能的原因
* hello proxy 登入期間指定不正確
* hello OMS 服務端點不是在您的資料中心 whitelistested 

#### <a name="resolutions"></a>解決方式
1. Reonboard toohello OMS 服務以使用下列命令以 hello 選項 hello hello OMS Agent for Linux`-v`啟用。 這可讓透過 hello proxy toohello OMS 服務的 hello 代理程式的詳細資訊輸出。 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. 檢閱 hello 區段 [設定用於 HTTP proxy 的 hello 代理程式 server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify 您正確設定 hello 代理程式 toocommunicate 透過 proxy 伺服器。    
* 再次確認 hello 下列 OMS 服務端點會在允許清單中：

    |代理程式資源| 連接埠 |  
    |------|---------|  
    |*.ods.opinsights.azure.com | 連接埠 443|   
    |*.oms.opinsights.azure.com | 連接埠 443|   
    |ods.systemcenteradvisor.com | 連接埠 443|   
    |*.blob.core.windows.net/ | 連接埠 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>問題： 您收到 403 錯誤時嘗試 tooonboard

#### <a name="probable-causes"></a>可能的原因
* Linux 伺服器上的日期與時間不正確 
* 使用的工作區識別碼和工作區金鑰不正確

#### <a name="resolution"></a>解決方案

1. 請檢查 hello Linux 伺服器 hello 命令日期與時間。 如果 hello 時間 + /-15 分鐘，從目前的時間，就會失敗登入。 toocorrect 此更新 hello 日期及/或 Linux 伺服器的時區。 
2. 請確認您已經安裝 hello 最新版 hello OMS Agent for Linux。  hello 最新版本現在會通知您如果時間誤差導致 hello 登入失敗。
3. Reonboard 使用正確的工作區識別碼和工作區金鑰 hello 稍早在本主題中的安裝指示。

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>問題： 您看到 500 和 404 錯誤 hello 記錄檔中的登入之後，權限
這是已知第一次將 Linux 資料上傳至 OMS 工作區時會發生的問題。 這不會影響正在傳送的資料或服務體驗。

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>問題： 您未看見 hello OMS 入口網站中的任何資料

#### <a name="probable-causes"></a>可能的原因

- 上架 toohello OMS 服務失敗
- OMS 服務會封鎖連接 toohello
- OMS Agent for Linux 資料已備份

#### <a name="resolutions"></a>解決方式
1. 檢查上架 hello OMS 服務是否成功藉由檢查有 hello 下列檔案：`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. 使用 hello Reonboard`omsadmin.sh`命令列指示
3. 如果使用 proxy，請參閱稍早提供的 toohello proxy 解決步驟。
4. 在某些情況下，hello 適用於 Linux 的 OMS 代理程式無法與 hello OMS 服務通訊時 hello 代理程式上的資料會是 toohello 佇列已滿的緩衝區大小為 50 MB。 藉由執行下列命令的 hello hello OMS Agent for Linux 應該重新啟動： `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`。 

    >[!NOTE]
    >此問題已在代理程式 1.1.0-28 版和更新版本中修正。
> 