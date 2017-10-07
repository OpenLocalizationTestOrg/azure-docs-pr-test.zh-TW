---
title: "Linux 虛擬機器上的設定 Apache Tomcat aaaSet |Microsoft 文件"
description: "深入了解如何使用 Azure 虛擬機器執行 Linux 向上 Apache Tomcat7 tooset。"
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a>使用 Azure 在 Linux 虛擬機器上設定 Tomcat7
Apache Tomcat （或只是 Tomcat 中，也原名雅加達 Tomcat） 是開放原始碼 web 伺服器及 servlet hello Apache 軟體基礎 (ASF) 所開發的容器。 Tomcat 實作 hello Java Servlet 和 Sun Microsystems 從 hello JavaServer 頁面 (JSP) 規格。 Tomcat 提供純 Java HTTP web 伺服器環境中哪些 toorun Java 程式碼。 Tomcat hello 簡單的組態，是單一的作業系統處理序中執行。 此程序會執行 Java 虛擬機器 (JVM)。 從瀏覽器 tooTomcat 每個 HTTP 要求會處理做為個別的執行緒在 hello Tomcat 程序中。  

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。 本文件涵蓋如何 toouse hello 傳統部署模型。 建議最新的部署使用 hello 資源管理員的模型。 toouse 資源管理員範本 toodeploy Ubuntu 具有 VM Open JDK 和 Tomcat，請參閱[本文](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/)。

在本文中，您將在 Linux 映像上安裝 Tomcat7 並且部署於 Azure 中。  

您將了解：  

* 如何 toocreate Azure 中的虛擬機器。
* 如何 tooprepare hello Tomcat7 虛擬機器。
* 如何 tooinstall Tomcat7。

假設您已經有 Azure 訂用帳戶。  如果沒有，您可以註冊免費試用版在[hello Azure 網站](https://azure.microsoft.com/)。 如果您擁有 MSDN 訂用帳戶，請參閱 [Microsoft Azure 特價：MSDN、MPN 及 BizSpark 優惠](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39)。 toolearn 深入了解 Azure 中，請參閱[何謂 Azure？](https://azure.microsoft.com/overview/what-is-azure/)。

本文假設您有 Tomcat 和 Linux 的基本操作知識。  

## <a name="phase-1-create-an-image"></a>第 1 階段：建立映像。
在這個階段，您將在 Azure 中使用 Linux 映像建立虛擬機器。  

### <a name="step-1-generate-an-ssh-authentication-key"></a>步驟 1：產生 SSH 驗證金鑰
SSH 對系統管理員而言是很重要的工具。 不過，不建議根據人為決定的密碼來設定存取安全性。 惡意使用者可以依據使用者名稱和弱式密碼侵入系統。

hello 好消息是 tooleave 遠端存取開啟的而不必擔心密碼。 此方法是由使用非對稱密碼編譯的驗證所組成。 hello 使用者的私密金鑰為 hello 授與 hello 驗證的其中一個。 您甚至可以鎖定 hello 使用者帳戶 toonot 允許密碼驗證。

這個方法的另一個好處是，您不需要不同的密碼 toosign toodifferent 伺服器中。 您可以藉由 hello 個人私密金鑰所有在伺服器上，這可讓您不必 tooremember 數個密碼進行驗證。



請遵循這些步驟 toogenerate hello SSH 驗證金鑰。

1. 下載並安裝從下列位置的 hello Ssh-keygen: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. 執行 Puttygen.exe。
3. 按一下**產生**toogenerate hello 索引鍵。 在 hello 過程中，您可以增加隨機性移動 hello 滑鼠 hello hello 視窗中的空白區域上。  
   ![PuTTY 金鑰產生器螢幕擷取畫面顯示 hello 產生新的索引鍵 按鈕][1]
4. Hello 產生程序之後，Puttygen.exe 會顯示新的公開金鑰。  
   ![PuTTY 金鑰產生器螢幕擷取畫面顯示 hello 新的公開金鑰與 hello 儲存私用金鑰按鈕][2]
5. 選取並複製 hello 公開金鑰，並將它儲存在名為 publicKey.pem 的檔案。 不要按**儲存公開金鑰**，因為 hello 儲存公開金鑰的檔案格式是我們想要的 hello 公用金鑰不同。
6. 按一下 [儲存私密金鑰]，並將它儲存在名為 privateKey.ppk 的檔案中。

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a>步驟 2: Hello Azure 入口網站中建立 hello 映像
1. 在 hello[入口網站](https://portal.azure.com/)，按一下**新增**在 hello 工作列 toocreate 映像。 然後選擇 hello Linux 映像，取決於您的需求。 hello 下列範例使用 hello Ubuntu 14.04 映像。
![顯示 hello 新按鈕的 hello 入口網站的螢幕擷取畫面][3]

2. 如**主機名稱**，指定 hello hello URL，您和網際網路用戶端會使用 tooaccess 此虛擬機器的名稱。 定義 hello DNS 名稱，例如 tomcatdemo hello 最後一個部分。 Azure 會隨後產生 hello URL 為 tomcatdemo.cloudapp.net。  

3. 如**SSH 驗證金鑰**，從 hello publicKey.pem 檔案，其中包含 hello Ssh-keygen 所產生的公開金鑰複製 hello 索引鍵值。  
![方塊 hello 入口網站中的 SSH 驗證金鑰][4]

4. 視需要設定其他設定，然後按一下建立。  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a>第 2 階段：準備用於 Tomcat7 的虛擬機器
在這個階段中，您將設定 Tomcat 流量的端點，並再連接 tooyour 新的虛擬機器。

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a>步驟 1： 開啟 hello HTTP 連接埠 tooallow web 存取
Azure 中的端點包含 TCP 或 UDP 通訊協定，以及公用和私人連接埠。 hello 私用連接埠是 hello hello 服務會接聽 tooon hello 虛擬機器的通訊埠。 hello 公用連接埠是 hello Azure 雲端服務的 hello 連接埠會接聽 tooexternally 針對以網際網路為基礎的連入流量。  

TCP 連接埠 8080 是 Tomcat 使用 toolisten hello 預設連接埠號碼。 如果使用 Azure 端點開啟這個連接埠，您和其他網際網路用戶端即可存取 Tomcat 頁面。  

1. 在 hello 入口網站中，按一下 **瀏覽** > **虛擬機器**，然後按一下hello 您所建立的虛擬機器。  
   ![Hello Virtual machines 目錄的螢幕擷取畫面][5]
2. tooadd 端點 tooyour 虛擬機器，按一下 hello**端點**方塊。
   ![顯示 hello 端點方塊的螢幕擷取畫面][6]
3. 按一下 [新增] 。  

   1. Hello 端點，請輸入的名稱中的 hello 端點**端點**，然後輸入 80**公用連接埠**。  

      如果您將它設定 too80，您不需要使用的 tooaccess Tomcat hello URL tooinclude hello 連接埠號碼。 例如，http://tomcatdemo.cloudapp.net。    

      如果您設定它 tooanother 值，例如 81，您需要 tooadd hello 連接埠號碼 toohello URL tooaccess Tomcat。 例如，http://tomcatdemo.cloudapp.net:81/。
   2. 在 [私人連接埠] 中輸入 8080。 Tomcat 預設會接聽 TCP 連接埠 8080。 如果您變更 hello 預設接聽 Tomcat 連接埠，您應該更新**私用連接埠**toobe hello 與 hello Tomcat 接聽連接埠相同。  
      ![UI 的螢幕擷取畫面，其中顯示 [新增] 命令、[公用連接埠] 和 [私人連接埠]][7]
4. 按一下**確定**tooadd hello 端點 tooyour 虛擬機器。

### <a name="step-2-connect-toohello-image-you-created"></a>步驟 2： 連接 toohello 您所建立的映像
您可以選擇任何 SSH 工具 tooconnect tooyour 虛擬機器。 在此範例中，我們使用 PuTTY。  

1. 收到 hello 入口網站中的 hello 的虛擬機器的 DNS 名稱。
    1. 按一下 [瀏覽] > [虛擬機器]。
    2. 選取您的虛擬機器的 hello 名稱，然後按一下**屬性**。
    3. 在 hello**屬性**磚中，查看 hello**網域名稱**方塊 tooget hello DNS 名稱。  

2. 取得從 hello SSH 連線的 hello 連接埠號碼**SSH**方塊。  
![顯示 hello SSH 連接埠號碼的螢幕擷取畫面][8]

3. 下載 [PuTTY](http://www.putty.org/)。  

4. 下載之後，按一下 Putty.exe hello 可執行檔。 在 PuTTY 組態中，設定 hello 基本選項與 hello 主機名稱和連接埠號碼是從虛擬機器的 hello 屬性取得。   
![螢幕擷取畫面會顯示 hello PuTTY 設定主機名稱和連接埠的選項][9]

5. Hello 左窗格中，按一下 **連接** > **SSH** > **Auth**，然後按一下**瀏覽**toospecifyhello hello privateKey.ppk 檔案位置。 hello privateKey.ppk 檔案含有 hello 私密金鑰所產生的 Ssh-keygen 稍 hello 」 階段 1： 建立映像 」 一節。  
![顯示 hello 連接目錄階層和瀏覽 按鈕的螢幕擷取畫面][10]

6. 按一下 [開啟] 。 您可能會收到警告訊息方塊。 如果您已設定 hello DNS 名稱，並正確連接埠號碼，請按一下**是**。
![會顯示 hello 通知的螢幕擷取畫面][11]

7. 您會提示的 tooenter 您的使用者名稱。  
![螢幕擷取畫面顯示在哪裡 tooenter 使用者名稱][12]

8. 輸入 hello hello 用於 toocreate hello 虛擬機器的使用者名稱 」 階段 1： 建立映像 」 稍早在本文中的 > 一節。 您會看到類似下列 hello:  
![顯示 hello authentication 確認的螢幕擷取畫面][13]

## <a name="phase-3-install-software"></a>第 3 階段：安裝軟體
在這個階段中，您可以安裝 hello Java runtime environment、 Tomcat7 和其他 Tomcat7 元件。  

### <a name="java-runtime-environment"></a>Java 執行階段環境
Tomcat 是以 Java 撰寫的。 Java 開發套件 (JDK) 有兩種類型 (OpenJDK 和 Oracle JDK)。 您可以選擇您想要的 hello。  

> [!NOTE]
> 同時 Jdk 有幾乎相同的 hello Java API 中的 hello 類別的程式碼的 hello 但 hello hello 虛擬機器的程式碼都不同。 OpenJDK 傾向 toouse 開啟文件庫，而 Oracle JDK 傾向 toouse 關閉的。 Oracle JDK 有較多的類別和一些已修復的錯誤，而 Oracle JDK 則比 OpenJDK 穩定。

#### <a name="install-openjdk"></a>安裝 OpenJDK  

使用下列命令 toodownload OpenJDK hello。   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* toocreate 目錄 toocontain hello JDK 檔案：  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK 檔案到 hello/usr/lib/jvm/目錄：  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a>安裝 Oracle JDK


使用 hello hello Oracle 網站中的下列命令 toodownload Oracle JDK。  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* toocreate 目錄 toocontain hello JDK 檔案：  

        sudo mkdir /usr/lib/jvm  
* tooextract hello JDK 檔案到 hello/usr/lib/jvm/目錄：  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* tooset hello 預設 Java 虛擬機器的 Oracle JDK:  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a>確認 Java 安裝成功
您可以使用類似下列 tootest，如果已正確安裝 hello Java 執行階段環境的 hello 的命令：  

    java -version  

如果您安裝 OpenJDK，您應該會看到類似 hello 下列訊息：![成功 OpenJDK 安裝訊息][14]

如果您已安裝 Oracle JDK，您應該會看到類似 hello 下列訊息：![成功 Oracle JDK 安裝的訊息][15]

### <a name="install-tomcat7"></a>安裝 Tomcat7
使用下列命令 tooinstall Tomcat7 hello。  

    sudo apt-get install tomcat7  

如果您未使用 Tomcat7，使用這個命令的 hello 適當的變體。  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a>確認 Tomcat7 安裝成功
toocheck 如果成功安裝 Tomcat7，瀏覽 tooyour Tomcat 伺服器的 DNS 名稱。 在本文中，hello 範例 URL 會是 http://tomcatexample.cloudapp.net/。 如果您看到類似下列 hello 訊息，Tomcat7 已正確安裝。
![Tomcat7 安裝成功訊息][16]

### <a name="install-other-tomcat7-components"></a>安裝其他 Tomcat7 元件
您也可以安裝其他選用 Tomcat 元件。  

使用 hello **sudo apt 快取搜尋 tomcat7**命令 toosee 所有 hello 可用的元件。 使用下列命令 tooinstall hello 一些有用的元件。  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a>第 4 階段：設定 Tomcat7
在這個階段，您可以管理 Tomcat。

### <a name="start-and-stop-tomcat7"></a>啟動和停止 Tomcat7
當您安裝它，hello Tomcat7 伺服器會自動啟動。 您也可以啟動它以 hello 下列命令：   

    sudo /etc/init.d/tomcat7 start

toostop Tomcat7:

    sudo /etc/init.d/tomcat7 stop

Tomcat7 tooview hello 狀態：

    sudo /etc/init.d/tomcat7 status

toorestart Tomcat 服務： 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a>Tomcat7 系統管理
您可以編輯 hello Tomcat 使用者組態檔案 tooset 系統管理員認證。 使用下列命令的 hello:  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

下列是一個範例：  
![顯示 hello sudo vi 命令輸出的螢幕擷取畫面][17]  

> [!NOTE]
> 建立 hello 管理員使用者名稱的強式密碼。  

編輯這個檔案之後, 應該重新啟動 Tomcat7 服務，以下列命令 tooensure hello 變更生效的 hello:  

    sudo /etc/init.d/tomcat7 restart  

開啟瀏覽器，並輸入**http://<your tomcat server DNS name>/管理員/html**為 hello URL。 如本文中的 hello 範例，hello URL 是 http://tomcatexample.cloudapp.net/manager/html。  

連接之後，您應該會看到類似 toohello 下列：  
![Hello Tomcat Web 應用程式管理員的螢幕擷取畫面][18]

## <a name="common-issues"></a>常見問題
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a>無法從 hello 網際網路存取與 Tomcat Moodle hello 虛擬機器
#### <a name="symptom"></a>徵狀  
  Tomcat 正在執行，但是您無法看到 hello Tomcat 預設頁面與您的瀏覽器。
#### <a name="possible-root-cause"></a>可能的根本原因   

  * hello Tomcat 接聽連接埠不是 hello 與 hello Tomcat 流量的虛擬機器的端點的私人連接埠相同。  

     檢查您的公用連接埠和私用連接埠端點設定，並確定 hello 私用連接埠是 hello 相同 hello Tomcat 接聽連接埠。 請參閱本文＜第 1 階段：建立映像＞一節，以取得為虛擬機器設定端點的指示。  

     toodetermine hello Tomcat 接聽連接埠，請開啟 /etc/httpd/conf/httpd.conf (Red Hat release) 或 /etc/tomcat7/server.xml （Debian 發行）。 根據預設，hello Tomcat 接聽連接埠為 8080。 下列是一個範例：  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     如果您使用虛擬機器，Debian 或 Ubuntu 和您想要 toochange hello 預設連接埠的 Tomcat 接聽 (例如 8081) 一樣，您也應該開啟 hello hello 作業系統的連接埠。 首先，開啟 hello 設定檔：  

        sudo vi /etc/default/tomcat7  

     然後取消註解 hello 最後一行，並變更 「 否 」 太"yes"。  

        AUTHBIND=yes
  2. hello 防火牆已停用 hello 接聽連接埠的 Tomcat。

     您只能看到 hello 本機主機 hello Tomcat 預設頁面。 hello 問題是最有可能是冀望的 tooby Tomcat，hello 連接埠已被 hello 防火牆封鎖。 您可以使用 hello w3m 工具 toobrowse hello 網頁。 hello 下列命令安裝 w3m 並瀏覽 toohello Tomcat 預設頁面：  


        sudo yum  install w3m w3m-img


        w3m http://localhost:8080  
#### <a name="solution"></a>方案

  * Hello Tomcat 接聽連接埠不是 hello 相同 hello hello 端點的流量 toohello 虛擬機器的私用連接埠為，如果您需要變更 hello 私用連接埠 toobe hello 與 hello Tomcat 接聽連接埠相同。   
  2. 如果 hello 問題因防火牆/iptables，加入下列行太/等/sysconfig/iptables hello。 https 流量，才需要 hello 第二行：  

      -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT

      -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  

     > [!IMPORTANT]
     > 請確定 hello 先前行的位置會全域限制存取，例如 hello 下列任何程式碼行上方:-A 輸入-j 拒絕-拒絕與 icmp 主機禁止



tooreload hello iptables，執行下列命令的 hello:

    service iptables restart

這在 CentOS 6.3 上已經過測試。

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a>權限被拒絕，當您上傳專案檔太/var/lib/tomcat7/webapps /
#### <a name="symptom"></a>徵狀
  當您使用 SFTP 用戶端 （例如 FileZilla) tooconnect tooyour 虛擬機器，並瀏覽太/var/lib/tomcat7/webapps/toopublish 您的網站，取得錯誤訊息類似 toohello 下列：  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a>可能的根本原因
  您有任何權限 tooaccess hello /var/lib/tomcat7/webapps 資料夾。  
#### <a name="solution"></a>方案  
  您需要 tooget hello 根帳戶的權限。 您可以變更該資料夾的 hello 擁有權與您佈建 hello 機器時所使用的根 toohello 使用者名稱。 以下是範例與 hello azureuser 帳戶名稱：  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  使用 hello-R 選項 tooapply hello 權限的目錄內的所有檔案。  

  此命令也適用於目錄。 hello-R 選項變更 hello 所有檔案和目錄 hello 目錄內的權限。 下列是一個範例：  

     sudo chown -R username:group directory  

  此命令會變更擁有權 （使用者和群組） 的所有檔案和 hello 目錄內的目錄。  

  hello 下列命令只會變更 hello 資料夾目錄中的 hello 權的限。 hello 檔案與 hello 目錄內的資料夾不會變更。  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
