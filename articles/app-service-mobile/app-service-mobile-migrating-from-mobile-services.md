---
title: "aaaMigrate 從行動服務 tooan App Service 行動應用程式"
description: "了解 tooeasily 要如何移轉您的行動服務應用程式 tooan App Service 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>移轉您現有的 Azure 行動服務 tooAzure 應用程式服務
以 hello [Azure 應用程式服務的公開上市]，Azure Mobile Services 站台可以輕鬆地移轉就地 tootake hello Azure App Service 的所有功能的優點。  本文件說明哪些 tooexpect 時從應用程式服務的 Azure Mobile Services tooAzure 移轉您的網站。

## <a name="what-does-migration-do"></a>移轉的作用為何 tooyour 網站
移轉您的 Azure 行動服務會將行動服務[Azure App Service]應用程式，而不會影響 hello 程式碼。  您通知中樞、SQL 資料連接、驗證設定、排定的作業和網域名稱都會保持不變。  使用您的 Azure 行動服務的行動用戶端繼續 toooperate 正常運作。  一旦傳送的 tooAzure 應用程式服務，則移轉會重新啟動您的服務。

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>為何您應移轉網站
Microsoft 會建議您移轉 hello 功能的 Azure 應用程式服務，包括您 Azure 行動服務 tootake 優點：

* 新的主機功能，包括 [WebJobs] 和[自訂網域名稱]。
* 連線 tooyour 在內部使用的資源[VNet]此外太[混合式連線]。
* 使用 New Relic 或 [Application Insights]進行監視和疑難排解作業。
* 內建的 DevOps 工具，包括[預備位置]、回復和生產環境測試。
* [自動調整]、負載平衡，以及[效能監視]。

如需 hello 優點 Azure 應用程式服務的詳細資訊，請參閱 hello [vs 行動服務。App Service] 主題。

## <a name="before-you-begin"></a>開始之前
網站開始任何主要工作之前，您應該先備份您的行動服務指令碼和 SQL Database。

## <a name="migrating-site"></a>移轉您的網站
hello 移轉程序移轉單一 Azure 區域內的所有站台。

toomigrate 網站：

1. 登入 toohello [Azure 傳統入口網站]。
2. 選取行動服務在 hello 區域中，您希望 toomigrate。
3. 按一下 hello**移轉 tooApp 服務** 按鈕。

   ![hello 移轉按鈕][0]
4. 讀取 hello 移轉 tooApp 服務 對話方塊。
5. 提供的 hello 方塊中輸入您的行動服務的 hello 名稱。  如果您的網域名稱是 contoso.azure mobile.net，比方說，然後輸入*contoso* hello 提供的方塊中。
6. 按一下 hello 刻度 按鈕。

監視 hello hello 活動監視器 」 中的 hello 移轉狀態。 您的網站會列為*移轉*hello Azure 傳統入口網站中。

  ![移轉活動監視器][1]

每個移轉可以需要 3 too15 分鐘每個要移轉的行動服務。  Hello 移轉期間，仍可使用您的網站。
您的網站會重新啟動在 hello hello 移轉程序的結尾。  hello 重新啟動程序期間，可能會持續幾秒鐘，則無法使用 hello 站台。

## <a name="finalizing-migration"></a>正在完成 hello 移轉
規劃 tootest 行動用戶端 hello 結論 hello 移轉程序在您的網站。  請確定您可以執行所有一般不變更 toohello 行動用戶端的用戶端動作。  

### <a name="update-app-service-tier"></a>選取適當的 App Service 定價層
您可以更靈活地定價之後移轉 tooAzure 應用程式服務。

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**App Service 方案**hello 設定 功能表中。
5. 按一下 hello**定價層**磚。
6. 按一下適當的 tooyour hello 磚的需求，然後按一下 **選取**。  您可能需要 tooClick**檢視所有**toosee hello 可用的定價層。

做為起點，我們建議您遵循層 hello:

| 行動服務定價層 | App Service 定價層 |
|:--- |:--- |
| 免費 |F1 免費 |
| 基本 |B1 基本 |
| 標準 |S1 標準 |

選擇 hello 右定價層應用程式中沒有相當大的彈性。  請參閱太[應用程式服務定價]如需新的應用程式服務的定價 hello 的完整詳細資料。

> [!TIP]
> hello 應用程式服務標準層包含存取 toomany 功能，您可能想 toouse，包括[預備位置]，自動備份，並自動調整。  當您有查看 hello 新功能 ！
>
>

### <a name="review-migration-scheduler-jobs"></a>檢閱 hello 移轉排程器作業
排程器作業在移轉後約 30 分鐘內將不會顯示。  排程的工作會繼續 toorun hello 背景。
tooview 後才看得見一次排程的工作：

1. 登入 toohello [Azure 入口網站]。
2. 選取**瀏覽 >**，輸入**排程**在 hello*篩選*方塊，然後選取 **排程器集合**。

移轉後可用的排程器作業數量將有所限制。  檢閱您的使用量和 hello [Azure 排程器方案]。

### <a name="configure-cors"></a>視需要設定 CORS
跨原始資源共用是技術 tooallow 網站 tooaccess Web API 在不同的網域。  如果您使用 Azure 行動服務與相關聯的網站，您需要 tooconfigure CORS hello 移轉的一部分。  如果您要以獨佔方式從行動裝置存取 Azure 行動服務，CORS 不需要 toobe 設定以外，在少數情況下。

已移轉的 CORS 設定都像 hello **MS_CrossDomainWhitelist**應用程式設定。  toomigrate 您站台 toohello 應用程式服務的 CORS 功能：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**CORS** hello API 功能表中。
5. 任何允許出處 hello 提供方塊中輸入，每個之後按下 Enter。
6. 一旦您允許出處的清單正確，請按一下 hello [儲存] 按鈕。

> [!TIP]
> 使用 Azure 應用程式服務的 hello 優點的其中一個是，您可以在 hello 上執行您的網站和行動服務相同的站台。  如需詳細資訊，請參閱 hello[接下來的步驟](#next-steps)> 一節。
>
>

### <a name="download-publish-profile"></a>下載新的發行設定檔
移轉 tooAzure 應用程式服務時，會變更 hello 網站的發行設定檔。  如果您想 toopublish 您從 Visual Studio 中的網站，您會需要新的發行設定檔。  toodownload hello 新發行設定檔：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 按一下 [取得發行設定檔]。

下載的 tooyour 電腦 hello PublishSettings 檔案。  此檔案通常名為 *sitename*.PublishSettings。  匯入 hello 發行到現有的專案設定：

1. 開啟 Visual Studio 和您的 Azure 行動服務專案。
2. 以滑鼠右鍵按一下您的專案中 hello**方案總管 中**選取**發行...**
3. 按一下 [匯入]。
4. 按一下 [瀏覽]，然後選取已下載的發佈設定檔案。  按一下 [檔案] &gt; [新增] &gt; [專案] 
5. 按一下**驗證連線**tooensure hello 發行設定的工作。
6. 按一下**發行**toopublish 您的網站。

## <a name="working-with-your-site"></a>在移轉後使用您的網站
開始使用新的應用程式服務在 hello [Azure 入口網站]移轉後。  hello 以下是一些附註的特定作業 tooperform 用於 hello [Azure 傳統入口網站]搭配其應用程式服務的對等項目。

### <a name="publishing-your-site"></a>下載和發佈您已移轉的網站
您的網站可透過 git 或 ftp 來使用，而且可透過各種不同的機制重新發佈，包括 WebDeploy、TFS、Mercurial、GitHub 及 FTP。  hello 的部署認證會以您的站台 hello 其餘部分移轉。  如果您未設定部署認證，或您不記得，您可以將其重設：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**部署認證**hello 發行功能表中。
5. Hello 方塊中，請輸入 hello 新的部署認證，然後按一下 [儲存] 按鈕，hello。

您可以使用這些認證 tooclone hello 站台與 git 或自動部署設定從 GitHub、 TFS 或 Mercurial。  如需詳細資訊，請參閱 hello [Azure App Service 部署文件]。

### <a name="appsettings"></a>應用程式設定
已移轉的行動服務大部分的設定都可透過 [應用程式設定] 來使用。  您可以從 hello 取得一份 hello 應用程式設定[Azure 入口網站]。
tooview 或變更您的應用程式設定：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**應用程式設定**hello 一般功能表中。
5. 捲動 toohello 應用程式設定 區段中，找出您的應用程式設定。
6. 按一下 hello 應用程式設定 tooedit hello 值 hello 值。  按一下**儲存**toosave hello 值。

您可以更新多個應用程式設定在 hello 相同的時間。

> [!TIP]
> 有兩個應用程式設定以 hello 相同的值。  例如，您可能會看到 ApplicationKey 和 MS\_ApplicationKey。  更新在 hello 這兩個應用程式設定相同的時間。
>
>

### <a name="authentication"></a>驗證
所有的驗證設定都可做為已移轉之網站中的 [應用程式設定]。  tooupdate 您的驗證設定，您必須變更適當的應用程式設定。  hello 下表顯示 hello 適當的應用程式設定為驗證提供者：

| 提供者 | 用戶端識別碼 | 用戶端密碼 | 其他設定 |
|:--- |:--- |:--- |:--- |
| Microsoft 帳戶 |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

注意： **MS\_AadTenants**儲存為租用戶網域 （hello hello Mobile Services 入口網站中的 「 允許租用戶 」 欄位） 的逗號分隔清單。

> [!WARNING]
> **請勿在 [hello 設定] 功能表中使用 hello 驗證機制**
>
> Azure App Service 提供個別 「 沒有程式碼 」 驗證和授權的系統在 hello*驗證 / 授權*設定 功能表和 hello （已過時）*行動驗證*hello 設定 功能表下的選項。  這些選項與已移轉的 Azure 行動服務不相容。  您可以[升級您的站台](app-service-mobile-net-upgrading-from-mobile-services.md)tootake hello Azure 應用程式服務驗證的優點。
>
>

### <a name="easytables"></a>資料
hello*資料*行動服務中的索引標籤已被取代*簡單資料表*hello Azure 入口網站中。  tooaccess 簡單的資料表：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**簡單資料表**hello 行動功能表中。

您可以加入資料表，依序按一下 hello**新增**按鈕，或按一下資料表名稱，藉以存取現有的資料表。  在此刀鋒視窗中可以執行各種作業，包括：

* 變更資料表權限
* 編輯 hello 作業指令碼
* 管理 hello 資料表結構描述
* 刪除 hello 資料表
* 清除 hello 資料表內容
* 刪除 hello 資料表的特定資料列

### <a name="easyapis"></a>API
hello *API*行動服務中的索引標籤已被取代*簡單 Api* hello Azure 入口網站中。  tooaccess 簡單的 Api:

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 按一下**簡單 Api** hello 行動功能表中。

您移轉應用程式開發介面已列在 [hello] 刀鋒視窗。  您也可以在此刀鋒視窗中新增 API。  toomanage 特定 API 中，按一下 hello API。
從 hello 新刀鋒視窗中，您可以調整 hello 權限，並編輯 hello hello API 的指令碼。

### <a name="on-demand-jobs"></a>排程器作業
所有排程器工作皆可透過 hello 排程器工作集合 > 一節。  tooaccess 排程器作業：

1. 登入 toohello [Azure 入口網站]。
2. 選取**瀏覽 >**，輸入**排程**在 hello*篩選*方塊，然後選取 **排程器集合**。
3. 選取您的網站 hello 工作集合。  它的名稱為 *sitename*-Jobs。
4. 按一下 [設定] 。
5. 按一下 [管理] 下的 [排程器作業]。

排程的作業會列出與您指定在移轉前的 hello 頻率。  隨選作業便已停用。  toorun 視作業：

1. 選取您想 toorun hello 作業。
2. 如果有必要，請按一下**啟用**tooenable hello 作業。
3. 按一下 [設定]，然後按一下 [排程]。
4. 選取 [一次] 的週期性，然後按一下 [儲存]

您的隨需作業會位於 `App_Data/config/scripts/scheduler post-migration`。  我們建議您轉換所有隨工作太[WebJobs]或[Functions]。  撰寫新的排程器作業，做為 [WebJobs] 或 [Functions]。

### <a name="notification-hubs"></a>通知中樞
行動服務會使用通知中樞進行推播通知作業。  下列應用程式設定的 hello 在移轉之後仍使用的 toolink hello 通知中樞 tooyour 行動服務：

| 應用程式設定 | 說明 |
|:--- |:--- |
| **MS\_PushEntityNamespace** |hello 通知中樞命名空間 |
| **MS\_NotificationHubName** |hello 通知中樞名稱 |
| **MS\_NotificationHubConnectionString** |hello 通知中樞連接字串 |
| **MS\_NamespaceName** |MS_PushEntityNamespace 的別名 |

透過 hello 管理您的通知中樞[Azure 入口網站]。  請注意 hello 通知中樞名稱 （您可以找到此使用 hello 應用程式設定）：

1. 登入 toohello [Azure 入口網站]。
2. 選取 [瀏覽>]，然後選取 **通知中樞**
3. 按一下 hello 與 hello 行動服務相關聯的通知中樞名稱。

> [!NOTE]
> 如果您的通知中樞是「混合」類型，則不會顯示。  「混合」類型的通知中樞會同時使用「通知中樞」和舊版的「服務匯流排」功能。  [轉換混合式命名空間]，再繼續作業。  您的通知中樞 hello 轉換完成之後，會出現在 hello [Azure 入口網站]。
>
>

如需詳細資訊，請檢閱 hello[通知中樞]文件。

> [!TIP]
> 通知中心管理功能，在 hello [Azure 入口網站]是仍在預覽中的。  hello [Azure 傳統入口網站]仍然可供管理所有通知中樞。
>
>

### <a name="legacy-push"></a>舊版推播設定
如果您配置您之前在通知中樞上的 hello 簡介的行動服務推入，您使用*舊版推播*。  如果您使用推播，組態中卻沒有列出通知中樞，您很可能使用的是「舊版推播」。  這項功能會和所有其他功能一起移轉。  不過，建議您升級 tooNotification 集線器後 hello 移轉已完成。

在 hello 暫時 （與 hello 顯著的例外狀況的 hello APNS 憑證） 的所有 hello 舊版推播設定都可用於應用程式設定。  透過取代 hello hello 檔案系統上適當的檔案來更新 hello APNS 憑證。

### <a name="app-settings"></a>其他應用程式設定
hello 下列其他應用程式設定會從您的行動服務移轉，可在*設定* > *應用程式設定*:

| 應用程式設定 | 說明 |
|:--- |:--- |
| **MS\_MobileServiceName** |hello 應用程式名稱 |
| **MS\_MobileServiceDomainSuffix** |hello 網域前置詞。 亦即 azure-mobile.net |
| **MS\_ApplicationKey** |您的應用程式金鑰 |
| **MS\_MasterKey** |您的應用程式主要金鑰 |

hello 應用程式金鑰和主要金鑰都是從原始的行動服務的相同 toohello 應用程式金鑰。  特別是，hello 應用程式金鑰會傳送行動用戶端 toovalidate hello 行動應用程式開發介面使用。

### <a name="cliequivalents"></a>命令列對等項目
您可以再使用 hello *azure 行動*命令 toomanage Azure Mobile Services 網站。  相反地，許多函式已取代為 hello *azure 站台*命令。  使用下列資料表 toofind 對等項目的常用命令的 hello:

| *Azure Mobile* 命令 | 對等的 *Azure site* 命令 |
|:--- |:--- |
| mobile locations |site location list |
| mobile list |site list |
| mobile show *name* |site show *name* |
| mobile restart *name* |site restart *name* |
| mobile redeploy *name* |site deployment redeploy *commitId* *name* |
| mobile key set *name* *type* *value* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile config list *name* |site appsetting list *name* |
| mobile config get *name* *key* |site appsetting show *key* *name* |
| mobile config set *name* *key* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile domain list *name* |site domain list *name* |
| mobile domain add *name* *domain* |site domain add *domain* *name* |
| mobile domain delete *name* |site domain delete *domain* *name* |
| mobile scale show *name* |site show *name* |
| mobile scale change *name* |site scale mode *mode* *name* <br /> site scale instances *instances* *name* |
| mobile appsetting list *name* |site appsetting list *name* |
| mobile appsetting add *name* *key* *value* |site appsetting add *key*=*value* *name* |
| mobile appsetting delete *name* *key* |site appsetting delete *key* *name* |
| mobile appsetting show *name* *key* |site appsetting delete *key* *name* |

更新設定，藉由更新 hello 適當的應用程式設定的驗證或推播通知。
請編輯檔案，並透過 ftp 或 git 發佈您的網站。

### <a name="diagnostics"></a>診斷和記錄
Azure App Service 通常會停用 [診斷記錄]。  tooenable 診斷記錄：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 預設會開啟 hello 設定 刀鋒視窗。
4. 選取**診斷記錄檔**hello 功能 功能表底下。
5. 按一下**ON** hello 下列記錄檔：**的應用程式記錄 （檔案系統）**，**詳細錯誤訊息**，和**追蹤失敗的要求**
6. 針對 Web 伺服器記錄，按一下 [檔案系統] 
7. 按一下 [儲存] 

tooview hello 記錄檔：

1. 登入 toohello [Azure 入口網站]。
2. 選取**所有資源**或**應用程式服務**然後按一下 已移轉的行動服務的 hello 名稱。
3. 按一下 hello**工具**按鈕
4. 選取**記錄檔資料流**hello 觀察功能表底下。

會產生這些記錄檔會顯示在 [hello] 視窗。  您也可以下載 hello 記錄供稍後分析，使用您的部署認證。 如需詳細資訊，請參閱 hello[記錄]文件。

## <a name="known-issues"></a>已知問題
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>刪除移轉的行動應用程式複製會導致網站服務中斷
如果您複製您移轉的行動服務，使用 Azure PowerShell，然後刪除 hello 複製時，會移除 hello 實際執行服務的 DNS 項目。  您的站台不再是可從 hello 網際網路存取。  

解決方式： 如果您想 tooclone 您的網站，這樣透過 hello 入口網站。

### <a name="changing-webconfig-does-not-work"></a>變更 Web.config 並未發生作用
如果您的 ASP.NET 網站，變更 toohello`Web.config`檔案並不會套用。  hello Azure 應用程式服務建立適合`Web.config`啟動 toosupport hello 行動服務執行階段期間的檔案。  您可以使用 XML 轉換檔案來覆寫特定設定 (例如自訂標頭)。  建立檔案在呼叫`applicationHost.xdt`-此檔案必須結束 hello`D:\home\site`目錄 hello Azure 服務。  透過自訂部署指令碼或直接使用 Kudu 上傳 `applicationHost.xdt` 檔案。  hello 下列範例示範的範例文件：

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

如需詳細資訊，請參閱 hello [XDT 轉換範例]GitHub 上的文件。

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>移轉的行動服務無法加入 tooTraffic 管理員
當您建立 Traffic Manager 設定檔時，您無法直接選擇遷移行動服務 toohello 設定檔。  使用「外部端點」。  外部端點只能透過 PowerShell 來新增。  如需詳細資訊，請參閱[流量管理員教學課程](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/)。

## <a name="next-steps"></a>後續步驟
您的應用程式成為移轉的 tooApp 服務之後，有更多的功能，您可以使用：

* 部署[預備位置]toostage 變更 tooyour 站台可讓您和執行 A / B 測試。
* [WebJobs] 可取代隨選排定作業。
* 您可以[持續部署]網站的連結您的站台 tooGitHub、 TFS 或 Mercurial。
* 您可以使用[Application Insights] toomonitor 您的網站。
* 服務的網站和行動裝置應用程式開發介面從 hello 相同的程式碼。

### <a name="upgrading-your-site"></a>升級您的行動服務網站 tooAzure 行動應用程式 SDK
* Node.js 伺服器專案 hello 新[行動應用程式 Node.js SDK]提供數種新功能。 例如，您現在可以執行本機開發和偵錯、使用 0.10 以上的任何 Node.js 版本，以及使用任何 Express.js 中介軟體自訂。
* 。以網路為基礎的伺服器專案中，新 hello[行動應用程式 SDK 的 NuGet 封裝](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/)NuGet 相依性上有更大的彈性。  這些封裝支援 hello 新的應用程式服務驗證，並與任何 ASP.NET 專案撰寫。 若要深入了解如何升級，請參閱[升級您現有的.NET 行動服務 tooApp 服務](app-service-mobile-net-upgrading-from-mobile-services.md)。

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[App Service 價格]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[自動調整]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Azure App Service 部署文件]: ../app-service-web/web-sites-deploy.md
[Azure 傳統入口網站]: https://manage.windowsazure.com
[Azure 入口網站]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Azure 排程器方案]: ../scheduler/scheduler-plans-billing.md
[持續部署]: ../app-service-web/app-service-continuous-deployment.md
[轉換混合式命名空間]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[自訂網域名稱]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[Azure 應用程式服務的公開上市]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[混合式連線]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[記錄]: ../app-service-web/web-sites-enable-diagnostic-log.md
[行動應用程式 Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[vs 行動服務。App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[通知中樞]: ../notification-hubs/notification-hubs-push-notification-overview.md
[效能監視]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[預備位置]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT 轉換範例]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[Functions]: ../azure-functions/functions-overview.md
