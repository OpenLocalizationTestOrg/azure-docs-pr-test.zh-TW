---
title: "aaaData Data Factory 的管理閘道器 |Microsoft 文件"
description: "設定內部部署與 hello 之間的資料閘道 toomove 資料雲端。 使用資料管理閘道器在 Azure Data Factory toomove 您的資料。"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>資料管理閘道
hello 資料管理閘道器是用戶端代理程式，您必須安裝在內部部署環境 toocopy 資料之間雲端和內部部署資料存放區中。 hello 內部部署資料存放區支援的 Data Factory 會列在 hello[支援的資料來源](data-factory-data-movement-activities.md#supported-data-stores-and-formats)> 一節。

本文補充 hello 逐步解說中 hello[在內部部署與雲端之間移動資料的資料存放區](data-factory-move-data-between-onprem-and-cloud.md)發行項。 Hello 逐步解說中，您可以建立會使用內部部署 SQL Server 資料庫 tooan Azure blob 的 hello 閘道 toomove 資料管線。 本文章提供有關 hello 資料管理閘道器的詳細深入資訊。 

您可以向外延展資料管理閘道將多部在內部部署電腦與 hello 閘道產生關聯。 您可以增加可在節點上同時執行的資料移動作業數目來進行相應增加。 這項功能也適用於具有單一節點的邏輯閘道。 如需得詳細資料，請參閱[在 Azure Data Factory 中調整資料管理閘道](data-factory-data-management-gateway-high-availability-scalability.md)一文。

> [!NOTE]
> 目前，閘道器僅支援 hello 複製活動和預存程序活動 Data Factory 中。 它不是從自訂活動 tooaccess 在內部部署資料來源的可能 toouse hello 閘道。      

## <a name="overview"></a>概觀
### <a name="capabilities-of-data-management-gateway"></a>資料管理閘道功能
資料管理閘道器提供下列功能的 hello:

* 模型在內部部署資料來源和雲端資料來源內 hello 相同的資料處理站，並將資料移動。
* 具有單一的監視和管理與閘道狀態從 hello Data Factory 頁面的可視性的半透明窗格。
* 安全地管理存取 tooon 內部部署資料來源。
  * 不需要 toocorporate 防火牆進行任何變更。 閘道只會以 HTTP 為基礎的輸出連線 tooopen 網際網路。
  * 利用您的憑證加密內部部署資料存放區的認證。
* 有效率地移動資料 – 平行、 復原 toointermittent 網路問題的自動重試邏輯以傳輸資料。

### <a name="command-flow-and-data-flow"></a>命令流程和資料流程
當您使用內部部署與雲端之間的複製活動 toocopy 資料時，hello 活動會使用閘道 tootransfer 資料從內部部署資料來源 toocloud，反之亦然。

以下是 hello 高層級的資料流程和複本資料閘道的步驟摘要：![使用閘道的資料流程](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. 資料開發人員使用任一 hello Azure Data factory 建立閘道[Azure 入口網站](https://portal.azure.com)或[PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx)。
2. 資料開發人員藉由指定 hello 閘道建立內部部署資料存放區連結的服務。 資料開發人員在 hello 設定已連結的服務，使用 hello 設定認證的應用程式 toospecify 驗證類型和認證。  hello 設定認證與 hello 資料通訊的應用程式 對話方塊將 tootest 連接和 hello 閘道 toosave 認證儲存。
3. 閘道會先將 hello 認證儲存在 hello 雲端進行 hello 認證加密與 hello 與 hello 閘道 （由資料開發人員提供），相關聯的憑證。
4. 資料 Factory 服務會與 hello 閘道排程和管理工作會使用共用的 Azure 服務匯流排佇列的控制通道的通訊。 當複製活動作業需要 toobe 開始時，Data Factory 要求排入佇列 hello 以及認證資訊。 後輪詢 hello 佇列 hello 作業就會啟動閘道。
5. hello 閘道解密 hello 認證以 hello 相同憑證，然後使用適當的驗證類型和認證連接 toohello 在內部部署資料存放區。
6. hello 閘道將資料從內部部署存放區 tooa 雲端儲存體，或反之亦然根據 hello 複製活動 hello 資料管線中的設定方式。 針對此步驟，直接與雲端儲存體服務，例如 Azure Blob 儲存體不要透過安全 (HTTPS) 通道通訊 hello 閘道。

### <a name="considerations-for-using-gateway"></a>使用閘道的考量
* 您可以將單一資料管理閘道執行個體用於多個內部部署資料來源。 不過，**單一閘道執行個體是一個 Azure 資料處理站的繫結的 tooonly**並不能共用與另一個 data factory。
* 單一電腦上**只能安裝一個資料管理閘道的執行個體**。 假設您有兩個 data factory 需要 tooaccess 在內部部署資料來源，您需要在兩個內部部署電腦上的 tooinstall 閘道。 換句話說，閘道已繫結的 tooa 特定的 data factory
* hello**閘道不需要在相同電腦做 hello 資料來源的 hello toobe**。 不過，擁有閘道器更接近 toohello 資料來源可減少 hello hello 閘道 tooconnect toohello 資料來源的時間。 我們建議您在其中一個該主機在內部部署資料來源的 hello 與不同的電腦上安裝 hello 閘道。 不同的電腦上的 hello 閘道和資料來源時，hello 閘道不會爭奪與資料來源的資源。
* 您可以擁有**連接 toohello 不同的電腦上的多個閘道相同的內部部署資料來源**。 例如，您可能提供兩個 data factory，但是相同的內部部署資料來源已向這兩個 hello data factory 的 hello 的這兩個閘道。
* 若您已在電腦上安裝用於 **Power BI** 案例的閘道器，請於另一台電腦上安裝**另一個用於 Azure Data Factory 的閘道器**。
* 即使您使用 **ExpressRoute**，也必須使用閘道。
* 即使您使用 **ExpressRoute**，也應該將資料來源視為內部部署資料來源 (亦即在防火牆後面)。 使用 hello 服務與 hello 資料來源之間的 hello 閘道 tooestablish 連線。
* 您必須**使用 hello 閘道**即使 hello 資料存放區上處於 hello 雲端**Azure IaaS VM**。

## <a name="installation"></a>安裝
### <a name="prerequisites"></a>必要條件
* 支援的 hello**作業系統**版本是 Windows 7、 Windows 8/8.1、 Windows 10、 Windows Server 2008 R2、 Windows Server 2012、 Windows Server 2012 R2。 目前不支援安裝在網域控制站上的 hello 資料管理閘道器。
* 必須有 .NET Framework 4.5.1 或更新版本。 如果您要在 Windows 7 電腦上安裝閘道，請安裝 .NET Framework 4.5 或更新版本。 如需詳細資訊，請參閱 [.NET Framework 系統需求](https://msdn.microsoft.com/library/8z6watww.aspx) 。
* 建議的 hello**組態**hello 閘道機器是至少 2 GHz、 4 個核心，8 GB RAM 和 80 GB 的磁碟。
* 如果 hello 主機電腦休眠，hello 閘道沒有回應 toodata 要求。 因此，設定適當**電源計劃**hello 之前安裝 hello 閘道的電腦上。 如果已設定的 toohibernate hello 機器，hello 閘道安裝會提示訊息。
* 您必須是 hello 機器 tooinstall 的系統管理員，並已成功設定 hello 資料管理閘道器。 您可以加入其他使用者 toohello**資料管理閘道使用者**本機 Windows 群組。 hello 這個群組的成員都能 toouse hello**資料管理閘道組態管理員**工具 tooconfigure hello 閘道。

當發生複製活動執行特定的頻率，hello hello 電腦上 （CPU、 記憶體） 的資源使用量也會遵循的 hello 相同模式尖峰和閒置的時間。 資源使用量也仰賴 hello 移動的資料數量。 如果有多個複製作業正在進行，您會看到資源使用量在尖峰時段增加。

### <a name="installation-options"></a>安裝選項
資料管理閘道可以安裝在 hello 下列方法：

* 藉由從 hello 下載 MSI 安裝程式套件[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717)。  hello MSI 也可以使用的 tooupgrade 現有資料管理閘道 toohello 最新版本，以保留的所有設定。
* 按一下 [手動設定] 底下的 [下載並安裝資料閘道] 連結，或 [快速安裝] 之下的 [直接安裝在此電腦上]。 如需使用快速安裝的逐步指示，請參閱 [在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。 hello 手動步驟會帶您 toohello 下載中心取得。  hello 指示下載並從下載中心安裝 hello 閘道位於 hello 下一節。

### <a name="installation-best-practices"></a>安裝最佳作法：
1. Hello hello 閘道的主機電腦上設定的電源計劃 hello 機器不休眠。 如果 hello 主機電腦休眠，hello 閘道沒有回應 toodata 要求。
2. 備份 hello 與 hello 閘道相關聯的憑證。

### <a name="install-hello-gateway-from-download-center"></a>從下載中心安裝 hello 閘道
1. 瀏覽過[Microsoft 資料管理閘道器下載頁面](https://www.microsoft.com/download/details.aspx?id=39717)。
2. 按一下**下載**，選取 hello 適當版本 (**32 位元**vs。**64 位元**)，然後按 [下一步]。
3. 執行 hello **MSI**直接或將它儲存 tooyour 硬碟，並執行。
4. 在 hello ** 褖畫惎**頁面上，選取**語言**按一下**下一步**。
5. **接受**hello 使用者授權合約，然後按一下**下一步**。
6. 選取**資料夾**tooinstall hello 閘道，然後按一下**下一步**。
7. 在 hello**準備 tooinstall**頁面上，按一下**安裝**。
8. 按一下**完成**toocomplete 安裝。
9. 收到 hello Azure 入口網站中的 hello 索引鍵。 請參閱 hello 下一節，如需逐步指示。
10. 在 hello**註冊閘道**頁面**資料管理閘道組態管理員**您電腦上執行下列步驟執行 hello:
    1. 貼上 hello 索引鍵中的 hello 文字。
    2. （選擇性） 按一下**顯示閘道器金鑰**toosee hello 文字。
    3. 按一下 [註冊] 。

### <a name="register-gateway-using-key"></a>使用金鑰註冊閘道
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>如果您尚未在 hello 入口網站中建立邏輯閘道
toocreate hello 入口網站及 get hello 機碼中的閘道，從 hello**設定**頁面上，遵循的步驟逐步解說中 hello[在內部部署與雲端之間移動資料](data-factory-move-data-between-onprem-and-cloud.md)發行項。    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>如果您已經在 hello 入口網站中建立 hello 邏輯閘道
1. 在 Azure 入口網站，瀏覽 toohello **Data Factory**頁面，然後按一下**連結的服務**磚。

    ![Data Factory 頁面](media/data-factory-data-management-gateway/data-factory-blade.png)
2. 在 hello**連結的服務**頁面上，選取 hello 邏輯**閘道**hello 入口網站中建立。

    ![邏輯閘道](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. 在 hello**資料閘道**頁面上，按一下**下載並安裝資料閘道**。

    ![下載 hello 入口網站中的連結](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. 在 hello**設定**頁面上，按一下**重新建立金鑰**。 按一下 [是] hello 警告訊息請仔細閱讀它之後。

    ![重新建立索引鍵](media/data-factory-data-management-gateway/recreate-key-button.png)
5. 按一下 [複製] 按鈕下一個 toohello 索引鍵。 複製的 toohello 剪貼簿 hello 金鑰。

    ![複製金鑰](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>系統匣圖示/通知
hello 下圖顯示一些 hello 您看到的紙匣圖示。

![系統匣圖示](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

如果您將游標移 hello 系統匣圖示/通知訊息時，您會看到有關 hello 快顯視窗中的 hello 閘道/更新作業狀態詳細資料。

### <a name="ports-and-firewall"></a>連接埠和防火牆
有兩個防火牆，您需要 tooconsider:**公司防火牆**hello 組織的 hello 中央路由器上執行和**Windows 防火牆**設定為 hello 本機電腦上的服務精靈，其中 hello安裝閘道。  

![防火牆](./media/data-factory-data-management-gateway/firewalls2.png)

在公司防火牆層級，您需要設定 hello 下列網域和輸出連接埠：

| 網域名稱 | 連接埠 | 說明 |
| --- | --- | --- |
| *.servicebus.windows.net |443、80 |用於與「資料移動服務」後端進行通訊 |
| *.core.windows.net |443 |用於使用 Azure Blob 的分段複製 (如果已設定)|
| *.frontend.clouddatahub.net |443 |用於與「資料移動服務」後端進行通訊 |


Windows 防火牆層級通常會啟用這些輸出連接埠。 如果沒有，您可以設定 hello 網域和連接埠據此閘道機器上。

> [!NOTE]
> 1. 根據您的來源 / 接收器，您可能必須 toowhitelist 其他網域與輸出連接埠，在您的公司/Windows 防火牆。
> 2. 針對某些雲端資料庫 (例如： [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings)， [Azure 資料湖](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access)等等)，您可能需要閘道機器上的防火牆設定 toowhitelist IP 位址。
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>複製資料來源建立資料存放區 tooa 接收資料存放區
請確認正確 hello 公司防火牆，hello 閘道電腦上的 Windows 防火牆上啟用 hello 防火牆規則，然後 hello 資料存放區本身。 啟用這些規則允許 hello 閘道 tooconnect tooboth 來源和接收器成功。 啟用每個資料存放區 hello 複製作業中所包含的規則。

例如，從 toocopy**在內部部署資料存放區 tooan Azure SQL Database 接收或 Azure SQL 資料倉儲接收**，執行下列步驟 hello:

* 在 Windows 防火牆和公司防火牆的通訊埠 **1433** 上都允許進行輸出 **TCP** 通訊。
* 設定 Azure SQL server tooadd hello IP 位址的 hello 閘道機器 toohello 清單允許的 IP 位址的 hello 防火牆設定。

> [!NOTE]
> 如果您的防火牆不允許使用輸出連接埠 1433，閘道將無法直接存取 Azure SQL。 在此情況下，您可以使用[分段複製](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy)tooSQL Azure 資料庫 / SQL Azure DW。 在此案例中，您只需要 hello 資料移動的 HTTPS （連接埠 443）。
>
>


### <a name="proxy-server-considerations"></a>Proxy 伺服器考量
如果您的公司網路環境使用 proxy 伺服器 tooaccess hello 網際網路、 設定資料管理閘道 toouse 適當的 proxy 設定。 您可以在 hello 初始註冊階段期間設定 hello proxy。

![在註冊期間設定 Proxy](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

閘道會使用 hello proxy 伺服器 tooconnect toohello 雲端服務。 進行初始設定時，按一下 [變更]  連結。 您會看到 hello **proxy 設定**對話方塊。

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxySettings.png)

有三個組態選項：

* **不使用 proxy**： 閘道器不會明確地使用任何 proxy tooconnect toocloud 服務。
* **使用系統 proxy**： 閘道使用的設定也就設定在 diahost.exe.config 和 diawp.exe.config hello proxy。如果沒有任何 proxy 設定 diahost.exe.config，diawp.exe.config，閘道正在連接 toocloud 服務直接而不會經過 proxy。
* **使用自訂 proxy**： 設定閘道，而不是使用組態在 diahost.exe.config 和 diawp.exe.config hello HTTP proxy 設定 toouse。必須指定「IP 位址」和「連接埠」。  「使用者名稱」和「密碼」則為選擇性，需視您的 Proxy 驗證設定而定。  所有設定都會經過加密與 hello 閘道 hello 認證憑證，並儲存在本機 hello 閘道主機電腦上。

hello 資料管理閘道主機服務會自動重新啟動之後儲存 hello 更新 proxy 設定。

閘道已成功註冊之後，如果您想要 tooview 或更新 proxy 設定之後，使用資料管理閘道組態管理員。

1. 啟動 **資料管理閘道器組態管理員**。
2. 切換 toohello**設定** 索引標籤。
3. 按一下**變更**中連結**HTTP Proxy**區段 toolaunch hello**設定 HTTP Proxy**對話方塊。  
4. 按一下 hello 之後**下一步** 按鈕，您會看到警告對話方塊，詢問您的權限 toosave hello proxy 設定並重新啟動 hello 閘道器主機服務的。

您可以使用「組態管理員」工具來更新 HTTP Proxy。

![使用組態管理員來設定 Proxy](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> 如果您設定使用 NTLM 驗證的 proxy 伺服器時，閘道器主機服務是 hello 網域帳戶執行。 如果您變更 hello 稍後 hello 網域帳戶的密碼，請記住 tooupdate hello 服務的組態設定，並據此將它重新啟動。 由於 toothis 需求，我們建議使用專用的網域帳戶 tooaccess hello proxy 伺服器，不需要您 tooupdate hello 密碼經常。
>
>

### <a name="configure-proxy-server-settings"></a>設定 Proxy 伺服器設定
如果您選取**使用系統 proxy** hello HTTP proxy 設定，閘道會使用設定 diahost.exe.config 和 diawp.exe.config 中的 hello proxy。如果 proxy 不指定 diahost.exe.config 和 diawp.exe.config，閘道正在連接 toocloud 服務直接而不會經過 proxy。 hello 下列程序說明如何更新 hello diahost.exe.config 檔案。  

1. 在 [檔案總管] 中，製作的安全 C:\Program Files\Microsoft 資料管理 Gateway\2.0\Shared\diahost.exe.config tooback hello 原始檔。
2. 以系統管理員身分啟動 Notepad.exe，並開啟文字檔 C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config。尋找 hello 預設標記的 system.net hello 下列程式碼所示：

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   然後，您可以加入 proxy 伺服器的詳細資料中 hello 下列範例所示：

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   內部 hello proxy 標記 toospecify hello 需要設定，例如 scriptLocation 允許額外的屬性。 請參閱太[項目 （網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx)語法。

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. 到 hello 原始位置中，儲存 hello 設定檔，然後重新啟動 hello 收取 hello 變更的資料管理閘道主機服務。 toorestart hello 服務： 使用 [服務] 小程式從 hello [控制台] 中，或從 hello**資料管理閘道組態管理員**> 按一下 hello**停止服務**按鈕，然後按一下 hello **啟動服務**。 如果 hello 服務未啟動，它可能是不正確的 XML 標記語法，已加入至已編輯過的 hello 應用程式組態檔。

> [!IMPORTANT]
> 不要忘記 tooupdate**兩者**diahost.exe.config 和 diawp.exe.config。  


此外 toothese 點，您也需要 toomake 確定 Microsoft Azure 是在貴公司的白名單中。 有效的 Microsoft Azure IP 位址中的 hello 清單可以下載從 hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653)。

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>防火牆和 Proxy 伺服器相關問題的可能徵兆
如果您遇到下列的錯誤類似 toohello，很可能是由於 tooimproper hello 防火牆或 proxy 伺服器，它會封鎖連接 tooData Factory tooauthenticate 本身的閘道設定。 請參閱 tooprevious 區段 tooensure 防火牆和 proxy 伺服器已正確設定。

1. 當您嘗試 tooregister hello 閘道時，您會收到 hello 下列錯誤: 「 無法 tooregister hello 閘道金鑰。 後再重試 tooregister hello 閘道器金鑰，確認 「 資料管理閘道處於連線狀態的 hello 與 hello 資料管理閘道主機服務已啟動的。
2. 當您開啟「組態管理員」時，您會看到「已中斷連線」或「正在連接」狀態。 檢視 Windows 事件記錄檔，在 「 事件檢視器 」 時 > 」 應用程式及服務記錄檔"> 「 資料管理閘道 」，您會看到錯誤訊息，例如 hello 下列錯誤：`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>開啟用於認證加密的連接埠 8050
hello**設定認證**應用程式會使用 hello 輸入連接埠**8050** toorelay 認證 toohello 閘道當您設定在內部連結 hello Azure 入口網站中的服務。 閘道在安裝期間，根據預設，hello 閘道安裝開啟它 hello 閘道機器上。

如果您使用協力廠商防火牆，您可以手動開啟 hello 連接埠 8050。 如果在閘道安裝期間遇到防火牆問題，您可以嘗試使用下列命令 tooinstall hello 閘道，但未設定 hello 防火牆 hello。

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

如果您選擇不 tooopen hello 連接埠 8050 hello 閘道機器上的，使用機制使用 hello 以外**設定認證**應用程式 tooconfigure 資料存放區認證。 例如，您可以使用 [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell Cmdlet。 如需了解如何設定資料存放區認證，請參閱 [設定認證和安全性](#set-credentials-and-securityy) 一節。

## <a name="update"></a>更新
根據預設，資料管理閘道器會自動更新 hello 閘道較新版本可用時。 hello 閘道才可以更新所有 hello 排程工作都已都完成。 沒有進一步的工作會處理 hello 閘道，直到 hello 更新作業完成。 如果 hello 更新失敗，閘道會復原 toohello 舊版本。

您會看到 hello 排定更新時間，在下列位置的 hello:

* hello 閘道 hello Azure 入口網站中的屬性頁面。
* Hello 資料管理閘道組態管理員的首頁
* 系統匣通知訊息。

hello hello 資料管理閘道組態管理員的 [常用] 索引標籤會顯示 hello 更新排程與 hello 最後一個時間 hello 閘道已安裝/更新。

![更新排程](media/data-factory-data-management-gateway/UpdateSection.png)

您可以立即安裝 hello 更新，或等候 hello 閘道 toobe 在 hello 排程時間自動更新。 例如，hello 下列影像顯示 hello 示 hello 閘道器組態管理員，您可以按一下 tooinstall hello 更新 按鈕以及它立即通知訊息。

![DMG 組態管理員中的更新](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

hello 系統匣中的 hello 通知訊息看起來 hello 下列影像所示：

![系統匣訊息](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

您看到更新作業 （手動或自動） hello 系統匣中的 hello 的狀態。 當您下次啟動閘道器組態管理員時，您就會看到 hello 通知列該 hello 閘道上的訊息已更新以及連結太[什麼是新主題](data-factory-gateway-release-notes.md)。

### <a name="toodisableenable-auto-update-feature"></a>toodisable/啟用自動更新功能
您可以停用/啟用 hello 自動更新 」 功能執行下列步驟的 hello:

[適用於單一節點閘道]
1. Hello 閘道機器上啟動 Windows PowerShell。
2. 切換 toohello C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript 資料夾。
3. 執行下列命令 tooturn hello 自動更新的 hello 功能關閉 （停用）。   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. 重新 tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[適用於多重節點高度可用且可擴充的閘道 (預覽)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Hello 閘道機器上啟動 Windows PowerShell。
2. 切換 toohello C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript 資料夾。
3. 執行下列命令 tooturn hello 自動更新的 hello 功能關閉 （停用）。   

    對於具備高可用性功能的閘道 (預覽)，需要額外的 AuthKey 參數。
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. 重新 tooturn:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
如果您從不同於 hello 閘道機器的電腦存取 hello 入口網站，您必須確定 hello 認證管理員應用程式可以連接 toohello 閘道機器。 如果 hello 應用程式無法到達 hello 閘道電腦，所以不允許您 tooset hello 資料來源和 tootest 連接 toohello 資料來源的認證。  

當您使用 hello**設定認證**應用程式，hello 入口網站 hello 認證會以加密 hello 中所指定的 hello 憑證**憑證** 索引標籤的 hello**閘道Configuration Manager** hello 閘道機器上。

如果您要尋找應用程式開發介面為基礎的方法來加密 hello 認證，您可以使用 hello[新增 AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt 認證。 hello cmdlet 會使用該閘道是設定的 toouse tooencrypt hello 認證 hello 憑證。 加入加密的認證 toohello **EncryptedCredential** hello 的項目**connectionString** hello JSON 中。 您可以使用 hello JSON 以 hello[新增 AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet 或 hello Data Factory 編輯器中。

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

使用「Data Factory 編輯器」來設定認證還有另一個方法。 如果您建立連結的 SQL Server 服務，方法是使用 hello 編輯器和您輸入認證以純文字、 hello 認證會加密使用 hello Data Factory 服務所擁有的憑證。 它不會使用該閘道是設定的 toouse hello 憑證。 雖然這種方法在某些情況下可能快一點，但也比較不安全。 因此，建議您只在開發/測試用途才採用此方法。

## <a name="powershell-cmdlets"></a>PowerShell Cmdlet
本章節描述如何 toocreate 並登錄閘道使用 Azure PowerShell cmdlet。

1. 在系統管理員模式下啟動 **Azure PowerShell** 。
2. 登入 tooyour Azure 帳戶執行下列命令，並輸入您的 Azure 認證的 hello。

    ```PowerShell
    Login-AzureRmAccount
    ```
3. 使用 hello**新增 AzureRmDataFactoryGateway** cmdlet toocreate 邏輯閘道，如下所示：

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **範例命令和輸出**：

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. 在 Azure PowerShell 中，切換 toohello 資料夾: **C:\Program Files\Microsoft 資料管理 Gateway\2.0\PowerShellScript\**。 執行**RegisterGateway.ps1** hello 本機變數與相關聯**$Key** hello 下列命令所示。 此指令碼會註冊 hello 與 hello 您稍早建立的邏輯閘道電腦上安裝的用戶端代理程式。

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    您可以註冊 hello 閘道在遠端電腦上的使用 hello IsRegisterOnRemoteMachine 參數。 範例：

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. 您可以使用 hello **Get AzureRmDataFactoryGateway** data factory 中的閘道 cmdlet tooget hello 清單。 當 hello**狀態**顯示**線上**，這表示您的閘道已準備好 toouse。

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
您可以移除閘道使用 hello**移除 AzureRmDataFactoryGateway**閘道使用 hello 的 cmdlet，並更新描述**組 AzureRmDataFactoryGateway** cmdlet。 如需這些 Cmdlet 的語法及其他詳細資訊，請參閱 Data Factory Cmdlet 參考文件。  

### <a name="list-gateways-using-powershell"></a>使用 PowerShell 列出閘道器

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>使用 PowerShell 移除閘道器

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>後續步驟
* 請參閱 [在內部部署和雲端資料存放區之間移動資料](data-factory-move-data-between-onprem-and-cloud.md) 一文。 Hello 逐步解說中，您可以建立會使用內部部署 SQL Server 資料庫 tooan Azure blob 的 hello 閘道 toomove 資料管線。  
