---
title: "Azure 雲端服務和虛擬機器診斷 aaaConfiguring |Microsoft 文件"
description: "描述如何偵錯 Azure 雲端服務和 Visual Studio 中的虛擬機器 (Vm) tooconfigure 診斷資訊。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>為 Azure 雲端服務和虛擬機器設定診斷功能
當您需要 tootroubleshoot Azure 雲端服務或 Azure 虛擬機器時，您可以使用 Visual Studio 更輕鬆地設定 Azure 診斷。 Azure 診斷會擷取系統資料和記錄資料 hello 虛擬機器和執行雲端服務的虛擬機器執行個體，並將該資料傳送到您選擇的儲存體帳戶。 如需有關 Azure 中診斷記錄的詳細資訊，請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](app-service-web/web-sites-enable-diagnostic-log.md)。

本主題說明如何 tooenable 和設定 Azure 診斷，在 Visual Studio 中之前和之後部署，以及 Azure 虛擬機器中。 它也將示範如何 tooselect hello 類型的診斷資訊 toocollect 和如何收集 tooview hello 資訊之後。

您可以在 hello 下列方式設定 Azure 診斷：

* 您可以變更診斷組態設定，透過 hello**診斷組態**Visual Studio 中的對話方塊。 hello 設定會儲存在稱為 diagnostics.wadcfgx (diagnostics.wadcfg 在 Azure SDK 2.4 或更早版本) 的檔案。 或者，您可以直接修改 hello 設定檔。 如果您手動更新 hello 檔案，hello 組態變更才會生效 hello 您 hello 雲端服務 tooAzure 或 hello 模擬器中執行的 hello 服務部署的下一次。
* 使用**Cloud Explorer**或**伺服器總管**在 Visual Studio toochange hello 的執行中雲端服務或虛擬機器的診斷設定。

## <a name="azure-26-diagnostics-changes"></a>Azure 2.6 診斷變更
Visual Studio 中的 Azure SDK 2.6 專案，進行下列變更 hello。 （這些變更也適用於 Azure SDK toolater 版本。）

* hello 本機模擬器現在支援診斷。 這表示您可以收集診斷資料，並確認您的應用程式會建立 hello 正確的追蹤時您正在開發和測試 Visual Studio 中。 hello 連接字串`UseDevelopmentStorage=true`時，您在 Visual Studio 中執行雲端服務專案，使用 hello Azure 儲存體模擬器，請啟用收集診斷資料。 所有診斷資料都收集 hello （開發儲存體） 儲存體帳戶中。
* hello 診斷儲存體帳戶連接字串 (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) 再一次儲存 hello 服務組態 (.cscfg) 檔中。 在 Azure SDK 2.5 hello 診斷儲存體帳戶指定 hello diagnostics.wadcfgx 檔案中。

有一些值得注意的差異之間 hello 連接字串已在 Azure SDK 2.4 及更早版本的運作，而且在 Azure SDK 2.6 和更新版本，它的運作方式。

* 在 Azure SDK 2.4 及更早版本，hello 已使用的連接字串做為執行階段 hello 診斷外掛程式 tooget hello 儲存體帳戶資訊的傳輸診斷記錄檔。
* 在 Azure SDK 2.6 和更新版本，hello 診斷連接字串使用 Visual Studio tooconfigure hello 診斷延伸模組以在發行期間的 hello 適當的儲存體帳戶資訊。 hello 連接字串可讓您定義不同的服務組態，Visual Studio 在發行時使用不同的儲存體帳戶。 不過，因為 （在 Azure SDK 2.5) 已無法再使用 hello 診斷外掛程式，hello.cscfg 檔案本身無法啟用 hello 診斷延伸模組。 您有透過 Visual Studio 或 PowerShell 之類的工具來分別 tooenable hello 延伸模組。
* toosimplify hello 程序使用 PowerShell 設定 hello 診斷延伸模組，從 Visual Studio 的 hello 封裝輸出也包含 hello 公用組態 XML，每個角色的 hello 診斷延伸模組。 Visual Studio 使用 hello 診斷連接字串 toopopulate hello 儲存體帳戶資訊出現在 hello 公用組態。 hello 公用組態檔 hello 擴充功能 資料夾中建立，並遵循 Paasdiagnostics.<rolename>.pubconfig.xml 的 hello 模式。&lt;RoleName >。模式。 任何 PowerShell 部署可以使用此模式 toomap 每個組態 tooa 角色。
* hello hello.cscfg 檔案中的連接字串也會使用 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)tooaccess hello 診斷資料，所以可以顯示在 hello**監視**需要索引 hello 連接字串tooconfigure hello 服務 tooshow 詳細資訊監視 hello 入口網站中的資料。

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>移轉專案 tooAzure SDK 2.6 和更新版本
當移轉從 Azure SDK 2.5 tooAzure SDK 2.6 或更新版本，如果您在診斷儲存體帳戶，指定在 hello.wadcfgx 檔案中，然後它會留在那裡。 tootake 優點 hello 彈性使用不同的儲存體帳戶的不同存放裝置組態，您必須加入 hello 連接字串 tooyour 專案 toomanually。 如果您從 Azure SDK 2.4 或較早 tooAzure SDK 2.6 移轉專案，然後 hello 的診斷連接字串會保留。 不過，請注意 hello 變更連接字串中的處理方式在 Azure SDK 2.6 中所述的 hello 上一節。

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Visual Studio 如何決定 hello 診斷儲存體帳戶
* 如果 hello.cscfg 檔案中指定診斷連接字串，Visual Studio 會使用 tooconfigure hello 診斷擴充功能發行時，並在封裝期間產生 hello 公用組態 xml 檔案時。
* 如果 hello.cscfg 檔案中不指定任何診斷連接字串，然後 Visual Studio 會回復指定 hello.wadcfgx 檔案 tooconfigure hello 診斷擴充功能發行時及產生 hello 公用 toousing hello 儲存體帳戶設定 xml 檔案封裝時。
* hello.cscfg 檔案中的 hello 診斷連接字串的優先順序高於 hello hello.wadcfgx 檔案中的儲存體帳戶。 如果診斷連接字串 hello.cscfg 檔案中指定然後 Visual Studio 會使用，並忽略.wadcfgx 中的 hello 儲存體帳戶。

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>功能沒有 hello 「 更新開發儲存體連接字串...」 作用為何？
hello 核取方塊**更新開發儲存體連接字串以供診斷和快取，使用 Microsoft Azure 儲存體帳戶認證發行 tooMicrosoft Azure 時**可讓您方便 tooupdate 任何開發儲存體帳戶連接字串與 hello 發行期間指定的 Azure 儲存體帳戶。

例如，假設您選取此核取方塊並 hello 診斷連接字串指定`UseDevelopmentStorage=true`。 當您發行 hello 專案 tooAzure 時，Visual Studio 會自動更新 hello 診斷連接字串與 hello hello 發行精靈中指定的儲存體帳戶。 不過，如果實際的儲存體帳戶指定為 hello 診斷連接字串，然後該帳戶改用。

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Azure SDK 2.4 及更舊版本和 Azure SDK 2.5 及更新版本之間的診斷功能差異
如果您要升級您的專案，從 Azure SDK 2.4 tooAzure SDK 2.5 或更新版本，您應該謹記在心 hello 下列診斷功能差異。

* **組態 API 已被取代** – 診斷的程式設計組態可在 Azure SDK 2.4 或更舊版本中使用，但在 Azure SDK 2.5 及更新版本中已被取代。 如果您的診斷組態目前定義在程式碼中，您將需要 tooreconfigure 從頭診斷 tookeep 工作順序中的 hello 移轉專案中的這些設定。 hello Azure SDK 2.4 的診斷組態檔是 diagnostics.wadcfg，是 diagnostics.wadcfgx Azure SDK 2.5 和更新版本。
* **雲端服務應用程式的診斷功能只能在 hello 角色層級，不是在 hello 執行個體層級設定。**
* **每次您部署應用程式時，會更新 hello 診斷組態**– 如果您從 [伺服器總管] 中變更診斷組態，然後重新部署您的應用程式，這可能會造成同位檢查問題。
* **在 Azure SDK 2.5 和更新版本，hello 診斷組態檔中，未在程式碼中設定損毀傾印**– 如果您有程式碼中設定損毀傾印，您就必須 toomanually 傳送嗨組態從程式碼 toohello 組態檔由於 hello 損毀傾印不傳送 hello 移轉 tooAzure SDK 2.6 期間。

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>部署雲端服務專案中的診斷之前先將其啟用
在 Visual Studio 中，您可以選擇 toocollect hello 模擬器中執行 hello 服務後再進行部署時，在 Azure 中執行的角色的診斷資料。 Visual Studio 中的所有變更 toodiagnostics 設定會都儲存在 hello diagnostics.wadcfgx 組態檔。 這些組態設定會指定診斷資料儲存當您部署雲端服務的 hello 儲存體帳戶。

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>在 Visual Studio 中部署之前的 tooenable 診斷
1. Hello 您感興趣的 hello 角色的捷徑功能表，選擇 **屬性**，然後選擇 hello**組態**hello 角色中的索引標籤**屬性**視窗。
2. 在 hello**診斷**區段中，請確定該 hello**啟用診斷**選取核取方塊。
   
    ![存取 hello 啟用診斷 選項](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Hello 省略符號 （...） 按鈕 toospecify hello 儲存體帳戶選擇您想要儲存 hello 診斷資料 toobe。 您選擇的 hello 儲存體帳戶會儲存診斷資料的 hello 位置。
   
    ![指定 hello 儲存體帳戶 toouse](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. 在 hello**建立儲存體連接字串**對話方塊方塊中，指定是否要 tooconnect 使用 hello Azure 儲存體模擬器，Azure 訂用帳戶，或手動輸入的認證。
   
    ![儲存體帳戶對話方塊](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * 如果您選擇 hello Microsoft Azure 儲存體模擬器，hello 連接字串設定 tooUseDevelopmentStorage = true。
   * 如果您選擇 hello 訂用帳戶選項，您可以選擇 hello 想 toouse 和 hello 帳戶名稱的 Azure 訂用帳戶。 您可以選擇 hello 管理帳戶按鈕 toomanage 您 Azure 訂用帳戶。
   * 如果您選擇 hello 手動輸入認證 選項，您提示的 tooenter hello 名稱和金鑰 hello 想 toouse 的 Azure 帳戶。
5. 選擇 hello**設定**按鈕 tooview hello**診斷組態** 對話方塊。 每個索引標籤 (除了 [一般] 和 [記錄檔目錄] 之外) 都代表您可以收集的診斷資料來源。 hello 預設索引標籤上，**一般**，提供您下列診斷資料收集選項 hello:**只限錯誤**，**所有資訊**，和**自訂計劃**. hello 預設選項，**只限錯誤**，採用 hello 最少的儲存體，因為它不會傳輸警告或追蹤訊息。 hello，所有的資訊 選項傳輸 hello 最多資訊與，因此，hello 儲存體成本最高的選項。
   
    ![啟用 Azure 診斷和組態](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. 此範例中，選取 hello**自訂計劃**選項，因此您可以自訂 hello 資料收集。
7. hello**磁碟配額 （mb）**方塊可讓您指定想 tooallocate 中多少的空間儲存體帳戶的診斷資料。 如果您想要您可以變更 hello 預設值。
8. 診斷資料的每個索引標籤中，您想 toocollect，選取其**啟用傳輸<log type>**核取方塊。 例如，如果您想 toocollect 應用程式記錄檔，選取 hello**啟用傳輸應用程式記錄檔**hello 核取方塊**應用程式記錄檔** 索引標籤。此外，請指定每個診斷資料類型所需的其他資訊。 請參閱 hello 節**設定診斷資料來源**本主題稍後的每個索引標籤上的組態資訊。
9. 在您啟用收集所有您想要的 hello 診斷資料之後，請選擇 hello**確定** 按鈕。
10. 如往常一般在 Visual Studio 中建立 Azure 雲端服務專案。 當您使用您的應用程式，您已啟用的 hello 記錄資訊會儲存 toohello 您所指定的 Azure 儲存體帳戶。

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>在 Azure 虛擬機器中啟用診斷
在 Visual Studio 中，您可以選擇為 Azure 虛擬機器 toocollect 診斷資料。

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>Azure 虛擬機器中的 tooenable 診斷
1. 在**伺服器總管**選擇 hello Azure 節點，然後連接 tooyour Azure 訂用帳戶，如果您還未連線。
2. 展開 hello**虛擬機器**節點。 您可以建立新的虛擬機器，或選取一個已經存在的虛擬機器。
3. 在 hello hello 您感興趣的虛擬機器的捷徑功能表，選擇 **設定**。 這會顯示 hello 虛擬機器組態 對話方塊。
   
    ![設定 Azure 虛擬機器](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. 如果尚未安裝，請加入 hello Microsoft Monitoring Agent 診斷延伸模組。 這項擴充功能可讓您收集 hello Azure 虛擬機器的診斷資料。 在 hello 安裝擴充功能清單中，選擇 hello 可用的擴充功能] 下拉式清單選取功能表，然後選擇 [Microsoft Monitoring Agent 診斷。
   
    ![安裝 Azure 虛擬機器延伸模組](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > 其他可供您的虛擬機器使用的診斷延伸模組。 如需詳細資訊，請參閱 Azure VM 延伸模組和功能。
   > 
   > 
5. 選擇 hello**新增**按鈕 tooadd hello 延伸模組並檢視其**診斷組態** 對話方塊。
6. 選擇 hello**設定**按鈕 toospecify 儲存體帳戶，然後選擇 [hello**確定**] 按鈕。
   
    每個索引標籤 (除了 [一般] 和 [記錄檔目錄] 之外) 都代表您可以收集的診斷資料來源。
   
    ![啟用 Azure 診斷和組態](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    hello 預設索引標籤上，**一般**，提供您下列診斷資料收集選項 hello:**只限錯誤**，**所有資訊**，和**自訂計劃**. hello 預設選項，**只限錯誤**，採用 hello 最少的儲存體，因為它不會傳輸警告或追蹤訊息。 hello**所有資訊**選項傳輸 hello 最多資訊與進行，因此，儲存體的 hello 成本最高選項。
7. 此範例中，選取 hello**自訂計劃**選項，因此您可以自訂 hello 資料收集。
8. hello**磁碟配額 （mb）**方塊可讓您指定想 tooallocate 中多少的空間儲存體帳戶的診斷資料。 如果您想要您可以變更 hello 預設值。
9. 診斷資料的每個索引標籤中，您想 toocollect，選取其**啟用傳輸<log type>**核取方塊。
   
    例如，如果您想 toocollect 應用程式記錄檔，選取 hello**啟用傳輸應用程式記錄檔**hello 核取方塊**應用程式記錄檔** 索引標籤。此外，請指定每個診斷資料類型所需的其他資訊。 請參閱 hello 節**設定診斷資料來源**本主題稍後的每個索引標籤上的組態資訊。
10. 在您啟用收集所有您想要的 hello 診斷資料之後，請選擇 hello**確定** 按鈕。
11. 儲存更新的 hello 的專案。
    
     您會看到訊息，以在 hello **Microsoft Azure 活動記錄檔**hello 虛擬機器的視窗是否有變更。

## <a name="configure-diagnostics-data-sources"></a>設定診斷資料來源
啟用收集診斷資料之後，您可以選擇完全何種資料來源，您想要 toocollect 和所收集的資訊。 hello 下列是一份索引標籤中 hello**診斷組態**對話方塊和每個組態選項的意義。

### <a name="application-logs"></a>應用程式記錄檔
**應用程式記錄檔**包含 Web 應用程式所產生的診斷資訊。 如果您想 toocapture 應用程式記錄檔，請選取 hello**啟用傳輸應用程式記錄檔**核取方塊。 您可以增加或減少的分鐘傳送嗨應用程式記錄檔時的 hello 數 tooyour 儲存體帳戶，藉由變更 hello**傳輸期間 （分鐘）**值。 您也可以變更 hello hello 記錄層級的值設定 hello 記錄中擷取的資訊數量。 例如，您可以選擇**Verbose** tooget 的詳細資訊，或選擇**重大**toocapture 僅重大錯誤。 如果您有特定的診斷提供者發出應用程式記錄檔，您可以擷取這些新增 hello 提供者的 GUID toohello**提供者 GUID**方塊。

  ![應用程式記錄檔](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  如需有關應用程式記錄檔的詳細資訊，請參閱 [在 Azure App Service 中針對 Web 應用程式啟用診斷記錄功能](app-service-web/web-sites-enable-diagnostic-log.md)。

### <a name="windows-event-logs"></a>Windows 事件記錄檔
如果您想 toocapture Windows 事件記錄檔，請選取 hello**啟用傳輸 Windows 事件記錄檔**核取方塊。 您可以增加或減少的分鐘傳送嗨事件記錄檔時的 hello 數 tooyour 儲存體帳戶，藉由變更 hello**傳輸期間 （分鐘）**值。 選取您想 tootrack 事件 hello 類型 hello 核取方塊。

  ![事件記錄檔](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

如果您使用 Azure SDK 2.6 或更新版本，而且想 toospecify 自訂資料來源，請輸入在 hello  **<Data source name>** 文字] 方塊，然後選擇 [hello**新增**按鈕的下一個 tooit。 hello 資料來源會加入 toohello diagnostics.cfcfg 檔案。

如果您使用 Azure SDK 2.5，而且想 toospecify 自訂資料來源，您可以將它加入 toohello`WindowsEventLog`區段 hello diagnostics.wadcfgx 檔案，如 hello 下列範例所示。

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>效能計數器
效能計數器資訊可協助您找出系統瓶頸並微調系統和應用程式效能。 如需詳細資訊，請參閱[在 Azure 應用程式中建立及使用效能計數器](https://msdn.microsoft.com/library/azure/hh411542.aspx)。 如果您想 toocapture 效能計數器，請選取 hello**啟用傳輸效能計數器**核取方塊。 您可以增加或減少的分鐘傳送嗨事件記錄檔時的 hello 數 tooyour 儲存體帳戶，藉由變更 hello**傳輸期間 （分鐘）**值。 Hello 效能計數器的 tootrack 選取 hello 核取方塊。

  ![效能計數器](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack 未列出的效能計數器使用的輸入 hello 建議的語法，然後選擇 [hello**新增**] 按鈕。 hello 虛擬機器上的 hello 作業系統決定您可以追蹤的效能計數器。如需有關語法的詳細資訊，請參閱 [指定計數器路徑](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx)。

### <a name="infrastructure-logs"></a>基礎結構記錄檔
如果您想 toocapture 基礎結構記錄檔，其中包含 hello Azure 診斷基礎結構、 hello RemoteAccess 模組和 hello RemoteForwarder 模組的相關資訊，請選取 hello**啟用傳輸基礎結構記錄檔**核取方塊。 您可以增加或減少的分鐘傳送嗨記錄檔時的 hello 數 tooyour 藉由變更 hello 傳輸期間 （分鐘） 值的儲存體帳戶。

  ![診斷基礎結構記錄檔](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  如需詳細資訊，請參閱 [使用 Azure 診斷收集記錄資料](https://msdn.microsoft.com/library/azure/gg433048.aspx) 。

### <a name="log-directories"></a>記錄檔目錄
如果您想 toocapture 記錄檔目錄，其中包含從記錄檔目錄的網際網路資訊服務 (IIS) 要求收集的資料，失敗的要求或資料夾，選取 hello**啟用傳輸記錄檔目錄**核取方塊。 您可以增加或減少的分鐘傳送嗨記錄檔時的 hello 數 tooyour 儲存體帳戶，藉由變更 hello**傳輸期間 （分鐘）**值。

您可以選取您想 toocollect，例如 hello 記錄檔的 hello 方塊**IIS 記錄檔**和**失敗要求**記錄檔。 提供預設儲存體容器名稱，但如果您想要您可以變更 hello 名稱。

此外，您可以從任何資料夾擷取記錄檔。 只需要指定 hello 路徑在 hello**從絕對目錄記錄**區段，然後選擇 [hello**新增目錄**] 按鈕。 hello 記錄檔將會擷取 toohello 指定容器。

  ![記錄檔目錄](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW 記錄檔
如果您使用[Windows 事件追蹤](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx)(ETW)，而且想 toocapture ETW 記錄檔、 選取 hello**啟用傳輸 ETW 記錄檔**核取方塊。 您可以增加或減少的分鐘傳送嗨記錄檔時的 hello 數 tooyour 儲存體帳戶，藉由變更 hello**傳輸期間 （分鐘）**值。

從事件來源和您指定的事件資訊清單會擷取 hello 事件。 toospecify 事件來源、 輸入的名稱，在 hello**事件來源**區段，然後選擇 [hello**新增事件來源**] 按鈕。 同樣地，您可以指定事件資訊清單中 hello**事件資訊清單**區段，然後選擇 [hello**加入事件資訊清單**] 按鈕。

  ![ETW 記錄檔](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  hello ETW 架構支援在 ASP.NET 中透過類別在 hello [System.Diagnostics.aspx] （https://msdn.microsoft.com/library/system.diagnostics (v = vs.110) 命名空間。 hello Microsoft.WindowsAzure.Diagnostics 命名空間，其繼承並擴充標準 [System.Diagnostics.aspx] （https://msdn.microsoft.com/library/system.diagnostics (v = vs.110) 類別，可讓 hello [System.Diagnostics.aspx] （使用為 hello Azure 環境中的記錄架構 https://msdn.microsoft.com/library/system.diagnostics (v = vs.110)。 如需詳細資訊，請參閱[在 Microsoft Azure 中控制記錄和追蹤](https://msdn.microsoft.com/magazine/ff714589.aspx)和[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services/cloud-services-dotnet-diagnostics.md)。

### <a name="crash-dumps"></a>損毀傾印
如果您想 toocapture 資訊的角色執行個體發生當機，請選取 hello**啟用傳輸損毀傾印**核取方塊。 (由於 ASP.NET 處理大多數例外狀況，這通常只對背景工作角色才有用。)您可以增加或減少 hello 百分比的儲存空間藉由變更 hello 專 toohello 損毀傾印**目錄配額 （%）**值。 您可以變更 hello 儲存體容器 hello 損毀傾印會儲存位置，而您可以選取是否要將 toocapture**完整**或**迷你**傾印。

列出目前正在追蹤的 hello 程序。 選取您想 toocapture 的 hello 程序的 hello 核取方塊。 tooadd 另一個處理序 toohello 清單中，輸入 hello 處理序名稱，然後選擇 [hello**加入處理序**] 按鈕。

  ![損毀傾印](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  如需詳細資訊，請參閱[在 Microsoft Azure 中控制記錄和追蹤](https://msdn.microsoft.com/magazine/ff714589.aspx)和 [Microsoft Azure 診斷第 4 部分：自訂記錄元件和 Azure 診斷 1.3 變更](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/)。

## <a name="view-hello-diagnostics-data"></a>檢視 hello 診斷資料
已收集到的雲端服務或虛擬機器的 hello 診斷資料之後，您可以檢視它。

### <a name="tooview-cloud-service-diagnostics-data"></a>tooview 雲端服務的診斷資料
1. 如往常般部署雲端服務並加以執行。
2. 您可以檢視 Visual Studio 會產生一份或資料表中的 hello 診斷資料儲存體帳戶中。 tooview hello 資料在報表中，開啟**Cloud Explorer**或**伺服器總管**，開啟 hello 的 hello 角色感興趣，hello 節點的捷徑功能表，然後選擇**檢視診斷資料**.
   
    ![檢視診斷資料](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    顯示 hello 可用資料的報表隨即出現。
   
    ![Visual Studio 中的 Microsoft Azure 診斷報告](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    如果未出現 hello 最新的資料，您可能必須針對 hello 傳輸週期 tooelapse toowait。
   
    選擇 hello**重新整理**連結 tooimmediately 更新 hello 資料，或選擇間隔中 hello**自動重新整理**下拉式清單方塊 toohave hello 資料自動更新。 tooexport hello 錯誤資料，選擇 hello**匯出 tooCSV**按鈕 toocreate 逗號分隔值檔案，您可以在試算表中開啟。
   
    在**Cloud Explorer**或**伺服器總管**，開啟 hello 與 hello 部署相關聯的儲存體帳戶。
3. 在 hello 資料表檢視器 中開啟 hello 診斷資料表，然後檢閱您所收集的 hello 資料。 在 IIS 記錄檔和自訂記錄檔中，您可以開啟 blob 容器。 透過檢閱下表中的 hello，您可以找到包含您感興趣的 hello 資料 hello 表格或 blob 容器。 此外，toohello 資料記錄檔、 hello 資料表項目包含 EventTickCount、 DeploymentId、 角色和您識別哪些虛擬機器和角色的 RoleInstance toohelp 產生 hello 資料和時間。 
   
   | 診斷資料 | 說明 | 位置 |
   | --- | --- | --- |
   | 應用程式記錄檔 |您的程式碼來呼叫 hello System.Diagnostics.Trace 類別的方法所產生的記錄檔。 |WADLogsTable |
   | 事件記錄檔 |此資料是從 hello hello 虛擬機器上 Windows 事件記錄檔。 Windows 會將資訊儲存在這些記錄檔，但應用程式和服務也使用這些 tooreport 錯誤或記錄資訊。 |WADWindowsEventLogsTable |
   | 效能計數器 |您可以在 hello 虛擬機器有任何效能計數器收集資料。 hello 作業系統提供效能計數器，其包括記憶體使用量和處理器時間等多種統計資料。 |WADPerformanceCountersTable |
   | 基礎結構記錄檔 |從 hello 診斷基礎結構本身的記錄檔。 |WADDiagnosticInfrastructureLogsTable |
   | IIS 記錄檔 |這些記錄檔會記錄 web 要求。 如果您的雲端服務取得大量的流量，這些記錄檔可能會相當冗長，因此您應該只在需要時收集並儲存此資料。 |您可以找到 hello wad-iis-failedreqlogs 下該部署、 角色和執行個體的路徑下的 blob 容器中的失敗要求記錄檔。 您可以在 wad-iis-logfiles 下找到完整的記錄檔。 Hello WADDirectories 表格中建立的每個檔案的項目。 |
   | 損毀傾印 |這項資訊提供雲端服務處理序的二進位映像 (通常是背景工作角色)。 |wad-crush-dumps blob 容器 |
   | 自訂記錄檔 |您預先定義的資料記錄檔。 |儲存體帳戶中，您可以指定自訂的記錄檔的程式碼 hello 位置。 例如，您可以指定自訂 blob 容器。 |
4. 如果任何類型的資料遭到截斷，您可以嘗試增加 hello 緩衝區，該資料類型或縮短 hello 傳輸間隔的資料從 hello 虛擬機器 tooyour 儲存體帳戶。
5. （選擇性）清除資料，從 hello 儲存體帳戶有時候 tooreduce 整體儲存體成本。
6. 當您進行完整部署時，在 Azure 中，更新 hello diagnostics.cscfg 檔案 (Azure SDK 2.5.wadcfgx)，而您的雲端服務會收取任何變更 tooyour 診斷組態。 相反地，您會更新現有的部署，如果不會在 Azure 中更新 hello.cscfg 檔案。 您仍然可以依照 hello hello 下一節中的步驟，變更診斷設定。 如需有關執行完整部署和更新現有部署的詳細資訊，請參閱 [發佈 Azure 應用程式精靈](vs-azure-tools-publish-azure-application-wizard.md)。

### <a name="tooview-virtual-machine-diagnostics-data"></a>tooview 虛擬機器的診斷資料
1. 在 hello hello 虛擬機器的捷徑功能表，選擇 **檢視診斷資料**。
   
    ![在 Azure 虛擬機器中檢視診斷資料](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    這會開啟 hello**診斷摘要**視窗。
   
    ![Azure 虛擬機器診斷摘要](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    如果未出現 hello 最新的資料，您可能必須針對 hello 傳輸週期 tooelapse toowait。
   
    選擇 hello**重新整理**連結 tooimmediately 更新 hello 資料，或選擇間隔中 hello**自動重新整理**下拉式清單方塊 toohave hello 資料自動更新。 tooexport hello 錯誤資料，選擇 hello**匯出 tooCSV**按鈕 toocreate 逗號分隔值檔案，您可以在試算表中開啟。

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>在部署後設定雲端服務診斷
如果您想調查雲端服務的問題，已在執行中，您可能想 toocollect 原先已部署的 hello 角色之前，您沒有指定的資料。 在此情況下，您可以啟動 toocollect 該資料在伺服器總管 中使用 hello 設定。 您可以在角色中，根據您是否從 hello hello 執行個體或 hello 角色的捷徑功能表開啟 hello 診斷組態對話方塊中設定的單一執行個體或所有 hello 執行個體的診斷功能。 如果您設定 hello 角色節點，任何變更將套用 tooall 執行個體。 如果您設定 hello 執行個體的節點時，任何變更將套用只有 toothat 執行個體。

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>執行中雲端服務的 tooconfigure 診斷
1. 在 伺服器總管 中，展開 hello**雲端服務** 節點，然後展開 節點 toolocate hello 角色或您想 tooinvestigate 或兩個執行個體。
   
    ![設定診斷](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. 在 hello 的執行個體節點或角色節點的捷徑功能表，選擇 **更新診斷設定**，然後選擇您想 toocollect 的診斷設定 hello。
   
    Hello 組態設定的相關資訊，請參閱**設定診斷資料來源**本主題中。 如需如何 tooview hello 診斷資料，請參閱**檢視 hello 的診斷資料**本主題中。
   
    如果您變更 [伺服器總管] 中的資料收集，這些變更會持續生效，直到您完全重新部署您的雲端服務為止。 如果您使用 hello 預設發行設定，hello 變更不會覆寫，因為發行 hello 預設設定是 tooupdate hello 現有部署，而不是執行完整部署。 在部署階段，請移 toohello 清除 toomake 確定 hello 設定**進階設定** 索引標籤在 hello 發行精靈 和 清除 hello**部署更新**核取方塊。 當您重新部署清除該核取方塊時，hello 設定便會還原為透過 hello 角色 hello 屬性編輯器組 toothose hello.wadcfgx （或.wadcfgx） 檔案中。 如果您更新您的部署，Azure 會保留 hello 舊的設定。

## <a name="troubleshoot-azure-cloud-service-issues"></a>疑難排解 Azure 雲端服務問題
如果您遇到問題的雲端服務專案，例如角色一直顯示 「 忙碌 」 狀態，重複回收，或擲回內部伺服器錯誤，有工具和技術，您可以使用 toodiagnose 並修正這些問題。 特定的範例，常見的問題和解決方案，以及 hello 概念與工具概觀用 toodiagnose 和修正這類錯誤，請參閱[Azure PaaS 計算診斷資料](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。

## <a name="q--a"></a>問答集
**什麼是 hello 緩衝區大小，而它應該多大？**

在每個虛擬機器執行個體，配額會限制多少診斷資料可以儲存在 hello 本機檔案系統上。 此外，您可以為每種診斷資料類型指定可用的緩衝區大小。 這個緩衝區大小就像是該資料類型的個別配額。 您可以藉由檢查 hello 對話方塊底部的 hello，判斷 hello 整體配額和 hello 的記憶體數量所保留下來。 如果您指定較大的緩衝區或更多類型的資料，就會愈趨 hello 整體配額。 您可以變更 hello 修改 hello diagnostics.wadcfg/.wadcfgx 組態檔的整體配額。 hello 診斷資料儲存在 hello 相同的檔案系統為您的應用程式資料，因此如果您的應用程式使用大量的磁碟空間，您不應該增加 hello 整體診斷配額。

**什麼是 hello 傳輸週期過後，以及多久應該？**

hello 傳輸週期是時間的 hello 擷取的資料之間經過量。 每個傳輸週期過後之後, 會從 hello 本機檔案系統上儲存體帳戶中的虛擬機器 tootables 移動資料。 如果 hello 收集的資料量超過 hello 配額 hello 傳輸期間結束之前，會捨棄較舊的資料。 如果您正在遺失資料，因為您的資料超過 hello 緩衝區大小或 hello 整體配額，您可能想 toodecrease hello 傳輸週期。

**哪個時區是 hello 中的時間戳記？**

hello 時間戳記是以 hello 當地時區 hello 資料中心裝載您的雲端服務。 hello hello 記錄資料表中的下列三個時間戳記資料行使用。

* **PreciseTimeStamp**是 hello ETW 事件時間戳記的 hello。 也就是 hello 時間 hello 事件會記錄從 hello 用戶端。
* **時間戳記**PreciseTimeStamp 無條件捨去 toohello 上傳頻率界限。 因此，如果您上傳頻率是 5 分鐘且 hello 事件時間 00:17:12，TIMESTAMP 將會是 00:15:00。
* **時間戳記**是在哪一個 hello hello Azure 資料表中建立實體的 hello 時間戳記。

**收集診斷資訊時如何管理成本？**

hello 預設設定 (**記錄層級**設定得**錯誤**和**傳輸週期**設定得**1 分鐘**) 所設計的 toominimize 成本。 如果您收集更多診斷資料，或減少 hello 傳輸期間，將會增加您的運算成本。 不收集超過，也不要忘記 toodisable 資料集合，當您不再需要的資料。 您可以一律再次啟用它，即使在執行階段，hello 上一節中所示。

**如何從 IIS 收集失敗要求記錄檔？**

根據預設，IIS 不會收集失敗要求記錄檔。 您可以設定 IIS toocollect 它們如果您編輯 hello web 角色的 web.config 檔案。

**我無法從 OnStart 之類的 RoleEntryPoint 方法取得追蹤資訊。問題在哪裡？**

hello WAIISHost.exe，非 IIS 內容中呼叫的 hello RoleEntryPoint 方法。 因此，hello 啟用追蹤不會套用一般由 web.config 中的組態資訊。 tooresolve 這個問題，請加入.config 檔案 tooyour web 角色專案，並將命名 hello 檔案 toomatch hello 輸出組件包含 hello RoleEntryPoint 程式碼。 Hello 預設 web 角色專案中的 hello.config 檔案的 hello 名稱將會是 WAIISHost.exe.config。然後加入下列行 toothis 檔 hello:

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

現在，在 hello**屬性**視窗中，設定 hello**複製 tooOutput 目錄**屬性太**永遠複製**。

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解診斷記錄在 Azure 中，請參閱[在 Azure 雲端服務和虛擬機器中啟用診斷](cloud-services/cloud-services-dotnet-diagnostics.md)和[啟用 Azure App Service 中的 web 應用程式的診斷記錄](app-service-web/web-sites-enable-diagnostic-log.md)。

