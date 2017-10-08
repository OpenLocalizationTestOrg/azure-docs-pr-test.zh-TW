---
title: "aaaAzure 角色屬性"
description: "了解 toouse hello Azure Toolkit for Eclipse tooconfigure Azure 角色設定的方式。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5c0ec412-5702-465a-8f47-87a8ce99a267
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: d111b4b9e4f12e49f38755bf6c9acc1a1de17a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-role-properties"></a>Azure 角色屬性
您的 Azure 角色的各種組態設定可以設定 hello Azure Toolkit for Eclipse 內。

## <a name="configuring-azure-role-properties"></a>設定 Azure 角色屬性
透過背景工作角色的 hello 屬性對話方塊，來完成設定您的 Azure 角色屬性。 開啟 hello 內容功能表上的 Eclipse 的專案總管 窗格中選取 hello hello 角色**Azure**子功能表。 （如果您沒有看到 hello 角色 hello Eclipse [專案總管] 中的，展開 [專案總管] 中的 Azure 專案）。

![][ic789599]

hello hello 可設定的各種屬性**屬性**對話方塊以本主題所述。 要注意的是，在您建立新的 Azure 部署專案時，系統會自動填入其中的許多屬性。

下列屬性頁的 hello 可供 Azure 角色。

* [虛擬機器屬性](#virtual_machine_properties)
* [快取屬性](#caching_properties)
* [憑證屬性](#certificates_properties)
* [元件屬性](#components_properties)
<!-- * [Debugging properties](#debugging_properties) -->
* [端點屬性](#endpoints_properties)
* [環境變數屬性](#environment_variables_properties)
* [負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性](#session_affinity_properties)
* [本機儲存體屬性](#local_storage_properties)
* [伺服器組態屬性](#server_configuration_properties)
* [SSL 卸載屬性](#ssl_offloading_properties)

<a name="virtual_machine_properties"></a>

### <a name="virtual-machine-properties"></a>虛擬機器屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**屬性**，，而且您將擁有 hello 能力 toochange hello 虛擬機器大小，也會變更hello 執行個體數目、 hello 下列影像所示。

![][ic719499]

> [!NOTE]
> 僅限 Windows： 當您將執行個體數目 hello tooa 值大於 1，您也可以設定應用程式伺服器 hello toolkit 將允許只有 1 的角色執行個體 toorun 在 hello 模擬器中，不論此設定為何。 這是 tooavoid 連接埠繫結衝突 hello 不同的伺服器執行個體 (例如，所有嘗試 toobind tooport 8080) 之間執行上 hello 時相同的電腦。 設定您想要的執行個體計數會保留，但只有在您部署 toohello 雲端時，才會生效。
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>快取屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**快取**。 在這個對話方塊中，您可以啟用具名共置的 memcache 相容快取，可讓您 web 應用程式設定的 toohelp 速度。

![][ic719483]

在 hello**快取**屬性頁面中，您可以指定下列的 hello 的全域設定：

* 是否啟用共置快取。
* hello 快取大小之記憶體的百分比。
* 如果您不想要讓 toosave hello 快取狀態為雲端服務，或無執行應用程式時儲存 hello 快取狀態的 hello 儲存體帳戶名稱。 （hello 儲存體帳戶名稱不是使用 hello 計算模擬器中執行您的應用程式時）。如果您將設定 hello 儲存體帳戶名稱太**（自動）** （此為 hello 預設值），快取組態會自動使用 hello 相同儲存體帳戶，因為您在 hello 中選取一個 hello**發行 tooAzure**對話方塊。

> [!NOTE]
> hello **（自動）**設定會影響 hello 預期只有當您發行您的部署使用 hello Eclipse 工具組的發行精靈。 如果您改為發行 hello.cspkg 檔案，以手動方式使用外部機制，例如 hello [Azure 管理入口網站][Azure Management Portal]，hello 部署將無法正確運作。
> 
> 

hello 下列對話方塊顯示一個快取的 hello 屬性。

![][ic719501]

* **名稱：** hello hello 名稱共置快取。
* **連接埠號碼：** hello hello 快取的連接埠號碼 toouse。
* **到期原則：** hello 下列值，指定何時到期 hello 快取中的索引鍵的其中一個。
  * **絕對值：** hello 金鑰到期時所指定的 hello 時間**分鐘 toolive**為止。
  * **NeverExpires:** hello 金鑰沒有到期時間。
  * **SlidingWindow:** hello 金鑰到期，如果未存取所指定的時間量 hello**分鐘 toolive**; 每次存取時，hello 到期時鐘會重設。
* **分鐘 toolive:**最大分鐘數的金鑰存活 toolive，主旨 toohello 到期原則。
* **在不同角色執行個體上複寫備份以提供高可用性：** 啟用時，有助於利用在不同角色執行個體上複寫備份以提供高可用性。 請注意這項功能 toowork 您部署至少兩個角色執行個體必須作用中。

tooadd 新的快取中，按一下 hello**新增**按鈕在 hello**快取**屬性頁和**設定具名快取**隨即會開啟對話方塊。 提供為上述 hello 屬性的值。

toomodify 具名快取中，選取 hello 快取，然後按一下 hello**編輯**按鈕在 hello**快取**屬性頁。 隨即會開啟對話方塊允許您 toomodify hello 快取屬性。 按**確定**toosave hello 快取值。

toodelete 快取中，選取 hello 快取，然後按一下 hello**移除**按鈕在 hello**快取**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。

如需有關如何 toouse 快取，請參閱[tooUse 共置於快取][How tooUse Co-located Caching]。

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>憑證屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**憑證**。

![][ic710964]

在這個對話方塊中，您可以新增或移除 Eclipse 專案所參考的憑證。 請注意，此處所列的 hello 憑證並不會自動儲存於任何 Java 金鑰存放區，因此不會自動使用於任何從 Java 應用程式中。 它們只會向 Azure，以便它們可以由其他 Windows 軟體預先載入至 hello Windows 憑證存放區上執行您的部署的 hello 虛擬機器和後續使用。 目前，hello 功能 hello 工具組使用 hello 憑證參考 hello 這種方式只**憑證**對話是[SSL 卸載][SSL Offloading]，由於 tooits網際網路資訊服務 (IIS) 和應用程式要求路由 (ARR)，需要依賴 hello 以這種方式提供適當的憑證 toobe。

當您部署您的專案 tooAzure 使用 hello 發行精靈時，您將無法在 hello 個人資訊交換 (PFX) 檔案對應 toothese 憑證，以及他們的密碼，順序 tooautomatically 上載 toohello 提示的 toopointAzure 服務，但前提是它們不已上傳那里先前。

<a name="components_properties"></a> 

### <a name="components-properties"></a>元件屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**元件**。 在這個對話方塊中，您擁有 hello 能力 tooadd、 修改或移除 hello 元件的角色，以及變更 hello 順序處理的。

![][ic719502]

hello 元件功能可讓您 tooadd 相依性 tooyour Azure 部署專案中，例如 Java 應用程式專案、 特殊的檔案和可執行的命令列陳述式所需的部署。

針對每個元件，您可以指定：

* hello 時將您的 Azure 部署專案匯入 hello 元件，會在建立時所採取的步驟 toobe。
* hello 部署 hello Azure 雲端中的元件時所採取的步驟 toobe。

> [!NOTE]
> 當指定元件的檔案或命令列，請記住您的部署將會發行的 tooa Windows 虛擬機器，因此您自訂的步驟必須適用於 windows 的作業系統。 
> 
> 

元件有下列屬性的 hello:

* **匯入：**指出 hello 元件如何將匯入 hello 專案 hello 專案建立時的方法。 這可以是 hello 的下列值的其中一個：
  * **複製：** hello 元件會從指定 hello hello 本機路徑複製**從**成 hello 角色屬性**approot**目錄。
  * **EAR:** hello 元件是 Java 企業封存檔 (EAR) 從在 hello hello 所指定的本機路徑企業應用程式專案匯入**從**屬性。 （這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。
  * **JAR:** hello 元件是 Java 封存檔 (JAR)，從指定 hello hello 本機路徑上的 Java 專案匯入**從**屬性。 （這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。
  * **none:** tooimport hello 元件會採取任何動作。 這是適用於當 hello 元件被假設 tooalready 會出現在 hello 角色**approot**目錄中，或 hello 元件時只可執行的命令列陳述式，如中所指定的 hello **為**屬性時 hello**部署**方法**exec**。
  * **WAR:** hello 元件是 Java web 應用程式封存檔 (WAR)，並且在 hello hello 所指定的本機路徑動態 Web 專案從匯入**從**屬性。 （這是自動偵測 hello hello hello 專案，在該位置的性質為基礎的工具組）。
  * **zip:** hello 元件是 zip 檔案，匯入壓縮 hello 目錄或檔案由 hello**從**屬性。
* **從：**上您的本機電腦 toohello 資料夾或代表 hello 的項目 tooimport tooyour 部署檔案的來源路徑。 此屬性可以使用 Windows 環境變數。 所有匯入元件都會匯入 hello 角色**approot** hello 專案建立時的目錄。
  
    請注意，您有 hello 能力 toodeploy 元件從下載部署 toohello 雲端 （而非 hello 計算模擬器） 時。 請參閱以下有關新增元件的相關資訊。    
* **做為：**檔案名稱下的 hello 元件將會匯入 hello 角色**approot**目錄，以及最後部署 hello Azure 雲端中。 保留此屬性空白 tookeep hello hello 本機電腦也是一樣，因為它的名稱 hello。 (可執行檔元件，也就是指**部署**方法設定得**exec**，這可以是任意的 Windows 命令列陳述式。)
  
  > [!IMPORTANT]
  > 如果您使用此值的空格字元，它們將會以不同方式處理 hello 根據部署方法。 如果 hello 部署方法**exec**，空格會被解譯為命令列引數分隔符號而非 hello 檔案名稱的一部分。 如需所有其他部署方法，空格會被解譯為 hello 檔案名稱的一部分。
  > 
  > 
* **部署：** hello 部署啟動時，指出 hello 動作方法會套用 toohello 元件。 這可以是 hello 的下列值的其中一個：
  
  * **複製：** hello 元件會複製的 toohello hello 所指定的目的地路徑**至**屬性。
  * **exec:** hello 元件是 hello hello hello 所指定的路徑內容中執行的可執行檔 Windows 命令列陳述式**至**屬性，在 hello hello 部署開始的時間。
  * **none:**採取任何動作時，才能套用的 toohello 元件 hello 部署開始。
  * **zip:** hello 元件會解壓縮的 toohello hello 所指定的目的地路徑**至**屬性。 這個方法是之後才可使用 hello**匯入**屬性是**zip**。
* **成為：** hello hello 元件將會部署的虛擬機器上的目的地路徑。 Windows 環境變數可以用於這個屬性，且檔案路徑的相對太**approot**。

tooadd 新元件，請按一下 hello**新增**按鈕在 hello**元件**屬性頁和**Azure 角色元件**隨即會開啟對話方塊。 提供為上述 hello 屬性的值。 

hello 以下顯示新增 WAR 元件的範例。

![][ic719503]

當部署 toohello 雲端 （而非 hello 計算模擬器），如果您希望 toodeploy hello 元件從下載，請確認**從部署在雲端，而不是在 hello 封裝內包含**已核取。 如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，然後填入 hello 剩餘 hello URL 的部分。 如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour 元件**URL**欄位。 指定其中一個 hello 下列方法：

* **複製：** hello 下載元件會複製的 toohello hello 所指定的目的地路徑**tooDirectory**路徑。
* **相同：** hello 使用相同的方法**從下載部署**與**從封裝部署**。
* **zip:** hello 下載元件會解壓縮的 toohello hello 所指定的目的地路徑**tooDirectory**路徑。

toomodify hello 元件，請選取元件，再按一下 hello**編輯**按鈕在 hello**元件**屬性頁。 隨即會開啟對話方塊允許您 toomodify hello 元件屬性。 按**確定**toosave hello 元件值。

toodelete hello 元件，請選取元件，再按一下 hello**移除**按鈕在 hello**元件**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。

元件會處理 hello 按所列的順序。 使用 hello**移**和**下移**按鈕 tooarrange hello 順序。

> [!NOTE]
> hello 伺服器組態功能必須依賴元件。 這些元件無法移除或編輯但不會移除 hello 對應伺服器組態。 嘗試 toomake 變更 toosuch 元件時，將會提示您了解。
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open hello context menu for hello role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have hello ability tooenable or disable remote debugging, as well as create debug configurations, as shown in hello following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>端點屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**端點**。 在這個對話方塊中，您已擁有 hello 能力 toocreate 端點，以及編輯或移除端點，，hello 下列影像所示。

![][ic719505]

tooadd 的端點，請按一下 hello**新增**hello 按鈕**端點**屬性頁和**加入端點**隨即會開啟對話方塊。

![][ic710897]

輸入 hello 端點的名稱，選取 hello 類型 (任一**輸入**，**內部**，或**InstanceInput**)，並指定 hello 公用和私用連接埠。 按**確定**toosave hello 新端點值。

根據端點 hello 類型，您可以使用連接埠範圍，如下所示：

* 輸入執行個體端點，hello 公用連接埠可以是連接埠範圍 (例如**2000年-2010年**) hello 私用連接埠是固定的值。
* 內部端點，未使用 hello 公用連接埠，而且 hello 私用連接埠可以是範圍，或保持空白或設定 tooan 星號 tooindicate 由 Azure 自動設定。
* 輸入端點，hello 公用連接埠只能是固定的值，而且 hello 私用連接埠可以是固定的值，或保持空白或設定 tooan 星號 tooindicate 由 Azure 自動設定。

如果您想 toouse 而非某個範圍的單一通訊埠編號，請將 hello hello 範圍結尾的 hello 文字方塊保留空白。

會組 tooautomatic，如果您需要 toodetermine 在執行階段實際使用的通訊埠的通訊埠，您的應用程式可以使用 hello Azure 服務執行階段 API，而其記錄在 hello[封裝 com.microsoft.windowsazure.serviceruntime （英文）摘要][com.microsoft.windowsazure.serviceruntime package summary]。

<!-- toosee how instance input endpoints can be used toohelp with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

將端點，toomodify 選取 hello 端點，然後按一下 hello**編輯**按鈕在 hello**端點**屬性頁。 Toomodify hello 端點名稱、 類型和公用及私用連接埠，可讓您開啟的對話方塊。 按**確定**toosave hello 修改端點值。

將端點，toodelete 選取 hello 端點，然後按一下hello**移除**hello 按鈕**端點**屬性頁，然後按一下**是**tooconfirm hello 刪除。

在訂單 tooproperly 設定部分 hello 功能 （例如快取、 工作階段相似性或 SSL 卸載） hello 使用者角色上啟用，hello 工具組可能會自動設定特殊的端點，將會與使用者定義的端點一起列出。 hello toolkit 可防止 hello 使用者編輯或刪除這類自動產生的端點，只要 hello 相關聯的功能啟用。

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>環境變數屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**環境變數**。 在這個對話方塊中，您已擁有 hello 能力 toocreate 環境變數，以及修改或移除環境變數，，hello 下列影像所示。

![][ic719506]

Hello 角色啟動時，環境變數會是可用 tooyour 啟動指令碼。

> [!NOTE]
> 在指定環境變數時，請記住您的部署將會發行的 tooa Windows 虛擬機器，因此您的環境變數必須是有效的 windows 作業系統。
> 
> 

例如 hello 角色啟動時所使用的環境變數中，建立新環境變數，即可 hello**新增** 按鈕。 hello 下列範例示範名為的環境變數**MyRoleVersion**正在建立並指派 hello 值**1.0**。

![][ic659268]

在您的 jsp 程式碼，您可以顯示 hello 值使用 hello`System.getenv`方法：

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

當應用程式執行時會產生以下輸出：

![][ic552233]

toomodify 環境變數，選取 hello 環境變數，然後按一下 hello**編輯**按鈕在 hello**環境變數**屬性頁。 隨即會開啟對話方塊允許您 toomodify hello 環境變數屬性。 按**確定**toosave hello 環境變數的值。

toodelete 環境變數，選取 hello 環境變數，然後按一下 hello**移除**按鈕在 hello**環境變數**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。

順序 tooproperly 中設定的一些 hello 功能 （例如伺服器組態、 遠端偵錯或本機儲存體） hello 使用者角色上啟用，hello 工具組可能會自動設定特殊的環境變數會連同列使用者定義的環境變數。 hello toolkit 可防止 hello 使用者編輯或刪除這類自動產生的環境變數，只要 hello 相關聯的功能啟用。

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**負載平衡**。 在這個對話方塊中，您 hello 能力 tooenable 或停用工作階段親和性，hello 下列影像所示。

![][ic719492]

如需相關資訊，請參閱[工作階段親和性][Session Affinity]。 另外請注意這項功能的行為在 hello 內容中的 SSL 卸載，依照[SSL 卸載][SSL Offloading]。

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>本機儲存體屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**本機儲存體**。 在這個對話方塊中，您已擁有 hello 能力 toocreate、 修改或移除 hello 執行應用程式的虛擬機器的暫存本機儲存體。 特定的值可以設定 hello hello 本機儲存體大小，以及是否 hello 內容會保留 hello 角色回收時，hello 下列影像所示。

![][ic719508]

您也可以指定環境變數對應 toohello 本機儲存體。

根據預設，您部署至 Azure 的所有項目是用來放置 （和解壓縮） hello **approot** hello 角色執行個體的資料夾。 雖然大多數的簡單部署可容納即使解壓縮，配置給 hello hello 空間**approot**目錄可是有限且未妥善定義 （小於 1 GB 是合理的經驗法則）。 因此，tooensure Azure 配置足夠的磁碟空間較大的部署，可能不適合在 hello **approot**資料夾中，您應該設定本機儲存體資源使用 hello**本機儲存體**對話方塊。 針對輕鬆 toodo 這個，請參閱[部署大型部署][Deploying Large Deployments]。

您可以從啟動指令碼容易參考 hello 儲存體資源 (例如，您**startup.cmd**) hello中所示，使用自動與hello資源相關聯的helloEclipse工具組的hello環境變數**本機儲存體**對話方塊。 這個環境變數將包含 hello hello hello 次執行啟動指令碼時已設定您的本機資源的完整路徑。 

toomodify 本機儲存體資源，選取 hello 本機儲存體資源，然後按一下 hello**編輯**按鈕在 hello**本機儲存體**屬性頁。 隨即會開啟對話方塊允許您 toomodify hello 本機儲存體資源屬性。 按**確定**toosave hello 本機儲存體資源值。

toodelete 本機儲存體資源，選取 hello 本機儲存體資源，然後按一下 hello**移除**按鈕在 hello**本機儲存體**屬性頁上，然後再按一下**是**tooconfirm hello 刪除。

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>伺服器組態屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下**伺服器組態**。 在這個對話方塊中，您必須 hello 能力 tooadd，移除，並修改 hello JDK 和 Java 應用程式伺服器，供您的部署，以及新增或移除 hello 應用程式 （例如 WAR、 JAR 或 EAR 檔案） 使用您的部署。

### <a name="jdk-configuration"></a>JDK 組態
這個對話方塊可讓您 toospecify hello JDK 封裝 toouse 為您的部署。 如果您在 Windows 上使用 Eclipse，您可以指定 hello JDK 封裝 toouse 在本機執行時在 hello Azure 模擬器，而且您擁有 hello 選項 toodeploy 該本機安裝 tooAzure。 在非 Windows 作業系統上 hello 模擬器 JDK 設定不適用，而且您無法部署 hello 在本機安裝的 JDK，因為它不是與 Windows 相容。 不過，hello 不論作業系統為何，您使用，您可以隨時在 hello 第 3 個合作對象 JDK 封裝 toodeploy tooAzure，或從其他下載位置指向您自己的 Windows 相容 JDK 封裝。

hello 以下是如何在 Windows 上指定 JDK 的範例：

![][ic780647]

如果您在 Windows 上使用 Eclipse，您可以指定以 hello JDK toouse 計算模擬器;因此，請確定 toodo**使用 hello JDK 進行本機測試此檔案路徑**簽入 hello**模擬器部署**> 一節。 然後，指定 hello 本機路徑 tooyour JDK;如果 hello 您想 toouse 不會自動選取，您可以瀏覽 toodifferent JDK。 您也可以 hello 選項 toodeploy 您 JDK tooyour Azure 雲端服務。toodo 因此，選取 hello**部署我的本機 JDK （自動上傳 toocloud 儲存體）**選項在 hello**雲端部署**> 一節。

注意： 在非 Windows 作業系統上 hello**模擬器部署**設定和 hello**部署我的本機 JDK**選項則無法使用。 hello 下列範例說明如何指定 JDK 的 Mac 上或其他支援的非 Windows 作業系統：

![][ic789643]

不論您是在 hello 作業系統，您有下列兩個 hello**雲端部署**hello 來源和類型的 JDK 封裝的選項：

* **部署 Azure 提供的第三方 JDK 封裝** 
* **從自訂下載部署** 

如果您使用 hello**部署第 3 個合作對象 JDK 封裝可從 Azure**選項：

1. 選取名為 hello 核取方塊**部署第 3 個合作對象 JDK 封裝可從 Azure**。
2. 從 [hello] 下拉式清單中，選取位於 Azure 的 hello 第 3 個合作對象 JDK 封裝。
3. 您**JDK**  索引標籤看起來類似 toohello 下列視窗：![][ic780648]和它看起來類似 toohello 下列 Mac OS 或其他支援的非 Windows 作業系統：![][ic789643]
4. 按一下**確定**toosave 您的變更。
5. 當提示的 tooaccept hello hello 第 3 個協力廠商 JDK 封裝提供者授權合約時，請檢閱 hello 授權條款。 假設您接受 hello 條款，請按一下**是**tooclose hello**接受授權合約**對話方塊。
    請注意該 hello 基礎的邏輯 hello 的 hello 下拉式清單中出現的項目**部署第 3 個合作對象 JDK 封裝可從 Azure**可以自訂選項。 toocustomize hello 中的項目，hello **JDK**  對話方塊中，按一下 hello**自訂**連結。 這樣會關閉 hello **JDK**屬性頁，並開啟 hello **componentsets.xml**在 Eclipse，您可以再視需要修改的檔案。 文件**componentsets.xml**隨附於 hello **componentsets.xml**檔案本身。

如果您使用 hello**部署從自訂下載 JDK**選項：

1. 建立 JDK 安裝目錄的 ZIP，請確保該 hello 目錄節點本身是 hello 的子系 hello ZIP 結構和非其內容。 請注意 hello hello 目錄名稱，當您將需要更新版本中，並記住此 JDK 安裝將會部署的 tooa Windows 虛擬機器。
2. 上傳到 Azure 儲存體帳戶的 hello ZIP，以 blob 的形式。 您可以上傳 blob tooAzure 儲存體使用外部的可用工具。 它會建議 toouse 私用 blob。 記下 hello ZIP 內容的 hello blob URL。
3. 選取名為 hello 核取方塊**部署從自訂下載 JDK**。
    如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，然後填入 hello 剩餘 hello URL 的部分。 如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour JDK 下載**URL**欄位。 如果使用 Azure 儲存體，hello URL 中的 blob 名稱必須是小寫。
4. 請確定該 hello **JAVA_HOME**文字方塊參考 toohello 正確的目錄名稱。 根據預設，它會參考 hello 做為您選擇在本機使用的 hello 值相同的 JDK 目錄名稱。 但是，如果包含在 hello ZIP hello 目錄有不同的名稱 (例如，到期 toousing 不同的版本)，更新 hello 目錄名稱中 hello **JAVA_HOME**文字方塊中，因為這項設定將用於 hello 雲端 （不在 hello 計算模擬器）。
5. 按一下**確定**toosave 您的變更。

就這麼簡單。 現在，當您建置 hello 雲端，您會發現 hello 封裝大小會小很多、 hello 建置程序應該會耗費較少的時間和 hello 部署本身發行 toohello 雲端時也應耗費較少的時間。 請注意該 hello**部署我的本機 JDK （自動上傳 toocloud 儲存體）**或**部署從自訂下載 JDK**選項為作用中只有您的應用程式部署時 hello 雲端中。 不會影響您的計算模擬器體驗;當您部署 toohello 計算模擬器時，仍然會使用 hello 的 hello 元件的本機版本。 

### <a name="server-configuration"></a>伺服器組態
hello 的範例如下的方式，您可以指定應用程式伺服器。

![][ic796926]

請確認該 hello**部署這種伺服器**核取方塊已選取，然後選擇 hello 類型要 toouse 的應用程式伺服器。

指定伺服器 toouse 雲端部署，您可以利用 hello 下列選項：

1. **部署在 Azure 上可用的第 3 個合作對象伺服器**-這是特別適用於開發/測試案例，其中部署效率和簡化是優先和 hello 伺服器不需要自訂組態。 或者，要作為起始點的 hello toouse 其中一部伺服器，但您包含適當的伺服器自訂步驟中部署的啟動邏輯。
2. **從自訂下載部署**-這是特別適用於生產案例中，當您想 toouse hello 雲端應用特別準備及設定伺服器。
3. **部署本機伺服器安裝** - 這個選項特別適用於如果本機伺服器安裝已針對您的用途進行自訂設定。 如果您選擇此選項時，您也必須指定本機伺服器的路徑中 hello**本機伺服器路徑**下面文字方塊。

如果您使用 hello**部署在 Azure 上可用的第 3 個合作對象伺服器**選項：

1. 選取名為 hello 核取方塊**部署在 Azure 上可用的第 3 個合作對象伺服器**。
2. 從 hello 下拉式功能表中，選取與您的部署所需的 hello 伺服器軟體 toouse hello 雲端中。 請注意，是否您已經指定一種伺服器 toouse 之前，您將無法限制的 toochoosing 僅雲端中的伺服器 hello 與此伺服器類型相同的系列。 但如果您沒有選擇伺服器類型，您可以選擇任何 Azure 目前可用的 hello 伺服器 hello 伺服器類型將會自動為您選取。
3. 按一下**確定**toosave 您的變更。

如果使用 hello**從自訂下載部署**選項：

1. 請確定您已經選取伺服器類型，根據 toohello 先前步驟。 這會告訴 hello 外掛程式如何從自訂下載，因為它的 toodeploy hello 伺服器必須從 hello 與所選取的伺服器類型相同的家族。
2. 選取名為 hello 核取方塊**從自訂下載部署**。
    如果您想 toodownload 從您的 Azure 儲存體帳戶時，選取 hello 儲存體帳戶從 hello**儲存體帳戶**下拉式清單 (您可以按一下 hello**帳戶**連結 toomodify 功能的 hello 清單)，這會填入在 hello **URL**欄位，以及在 hello 剩餘部分 hello URL tooyour 伺服器然後填滿時，下載 ZIP （使用 Azure 儲存體，hello URL 中的 blob 名稱必須是小寫）。 如果您不想 toouse Azure 儲存體，請選取**（無）**從 hello**儲存體帳戶**下拉式清單，然後輸入 hello hello URL tooyour 伺服器下載 ZIP **URL**欄位。 hello ZIP 會包含代表您應用程式伺服器的安裝目錄的子資料夾。 例如，如果您使用 Apache Tomcat 7.0.35 的 zip，hello 內 zip 會 hello 子資料夾代表 hello 安裝目錄，例如**apache tomcat apache-tomcat-7.0.35**。 
3. 指定 hello hello 主目錄環境變數的值。 它會預設 toohello 值用於您的本機應用程式伺服器，如果有的話，但是如果您的雲端應用程式伺服器是本機應用程式伺服器，您可以指定不同的值。 不過，您需要確定您的雲端應用程式伺服器的 hello toomake 相同家族 hello 稍早選取的伺服器類型。
    如果您更新在 hello 未來您雲端應用程式伺服器 zip，您可以手動變更 hello 主目錄設定，或 toohave 它再次符合您的本機設定 （如果您變更本機應用程式伺服器）。
4. 按一下**確定**toosave 您的變更。

hello 基礎的邏輯，其項目出現在 hello**伺服器** 索引標籤的 hello**伺服器組態**可自訂屬性頁。 這是一項進階的功能，您可能需要如果您的需求超出 hello 預設值，或如果您想 tooadd 其他伺服器。 hello 中的 toocustomize hello 邏輯**伺服器** 對話方塊中，按一下 hello**自訂**連結。 這樣會關閉 hello**伺服器組態**屬性頁，並開啟 hello **componentsets.xml** Eclipse，您可以修改為需要的 tooextend hello 伺服器組態範本中的檔案。 文件**componentsets.xml**隨附於 hello **componentsets.xml**檔案本身。

如果您使用 hello**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**選項：

1. 選取名為 hello 核取方塊**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**。
2. 使用 hello**儲存體帳戶**下拉式清單中，選取**（自動）**。 如果您指定**（自動）** ，hello Eclipse 工具組會使用 hello 相同儲存體帳戶為您的伺服器 hello 其中一個您選取為您的部署中 hello**發行 tooAzure**對話方塊。
3. 按一下**確定**toosave 您的變更。

選取您的電腦上的伺服器安裝路徑中 hello**本機伺服器路徑**文字方塊中，如果任何一個 hello 下列條件成立：

* 您想 tootest hello 模擬器 （適用於僅 tooWindows） 中的部署。
* 您想 toodeploy 您已安裝在本機伺服器的 toohello 雲端。
* 您想 toouse 中擁有 hello 雲端，在此情況下的自訂伺服器下載，也請確認 hello**部署我的本機伺服器 （自動上傳 toocloud 儲存體）**先前已選取的選項。

如果沒有任何上述選項套用 tooyour 情況下，hello 本機伺服器設定是 hello 的選擇性的。

### <a name="applications-configuration"></a>應用程式組態
hello 以下是如何指定應用程式的範例。

![][ic719512]

按一下**新增**tooadd 另一個應用程式，或**移除**tooremove 應用程式。 基於效率考量，如果您想要下載 toouse hello 來源應用程式的部署 toohello 雲端時，使用 hello[元件屬性](#components_properties)toospecify url，儲存體帳戶，依此類推。 

從 hello 2014 年 4 月版開始，您的應用程式會自動上傳到 hello 相同儲存體帳戶 (在 hello **eclipsedeploy**容器) 為 hello 選取為您的部署。 部署的 hello 啟動邏輯包含第一次下載這些應用程式從該儲存體帳戶的步驟。 這表示您可以升級您的應用程式部署中，而不需要 toorebuild 以及手動上傳較新版 hello 應用程式直接 （例如使用 hello Azure 入口網站） 該儲存體帳戶來重新部署整個封裝 hello，取代 hello WAR 檔案原本那裡上傳 hello 工具組。 然後，只要起始 hello 回收所有角色執行個體一次，或透過命令列公用程式使用 Azure 的管理入口網站。 （觸發角色回收直接從內 hello Eclipse 工具組目前不支援。）

### <a name="notes-about-server-configuration"></a>伺服器組態的相關注意事項
透過 hello 所做的變更**伺服器組態**屬性頁會反映在 hello `<component>` hello package.xml 檔的項目。

當您使用 hello**自動上傳...**或**從下載部署...**選項 hello JDK 或應用程式伺服器與您要建立 hello 雲端 （而非 hello 計算模擬器），而且您 toohello 連接的網路，您可能會發現建置訊息，例如 hello 下列在 hello 主控台輸出中，以 hello Ant產生器會驗證 hello 下載的可用性：

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

如果您選取 hello**從下載部署...**選項，可能會顯示下列警告 hello，但仍會繼續建置 hello:

`[windowsazurepackage] warning: Failed tooconfirm blob availability! Make sure hello URL and/or hello access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

這項警告是 hello 唯一表示 hello 下載的可用性尚未經過驗證。 因此如果 hello 雲端中的部署是基於某些原因失敗，請查看 toosee 如果您收到這個警告。

如果您想 toodisable hello 下載驗證 （例如，如果您認為不必要地放慢 hello 建置），將的 hello`verifydownloads`屬性太`false`在 hello `<windowsazurepackage>` package.xml 的項目： 

`<windowsazurepackage verifydownloads="false" ...>` 

如果您選取 hello**自動上傳...**選項，則 hello 主控台視窗中您會看到建置訊息的 hello 上傳每 5 秒，只要上傳時必要的報告 hello 進度。

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL 卸載屬性
在 Eclipse 的專案總管 窗格中開啟 hello hello 角色的內容功能表中，按一下**Azure**，然後按一下 **SSL 卸載**。 

![][ic719481]

在這個對話方塊中，您可以啟用 SSL 卸載，可讓您 tooeasily 啟用超文字傳輸通訊協定安全性 (HTTPS) 支援在 Azure 上的 Java 部署中，而不需要在您的 Java 應用程式伺服器 tooconfigure SSL。 如需詳細資訊，請參閱[SSL 卸載][ SSL Offloading]和[如何 tooUse SSL 卸載][How tooUse SSL Offloading]。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[Azure 專案屬性][Azure Project Properties]

[Azure 儲存體帳戶清單][Azure Storage Account List]

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Project Properties]: http://go.microsoft.com/fwlink/?LinkID=699524
[Azure Storage Account List]: http://go.microsoft.com/fwlink/?LinkID=699528
[com.microsoft.windowsazure.serviceruntime package summary]: http://azure.github.io/azure-sdk-for-java/com/microsoft/windowsazure/serviceruntime/package-summary.html
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Debugging a specific role instance in a multi-instance deployment]: http://go.microsoft.com/fwlink/?LinkID=699535#debugging_specific_role_instance
[Debugging Azure Applications in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Deploying Large Deployments]: http://go.microsoft.com/fwlink/?LinkID=699536
[How tooUse Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How tooUse SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699548
[SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699549

<!-- IMG List -->

[ic789599]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789599.png
[ic719499]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719499.png
[ic719483]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719483.png
[ic719501]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719501.png
[ic710964]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710964.png
[ic719502]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719502.png
[ic719503]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719503.png
[ic719504]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719504.png
[ic719505]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719505.png
[ic710897]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic710897.png
[ic719506]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719506.png
[ic659268]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic659268.png
[ic552233]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic552233.png
[ic719492]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719492.png
[ic719508]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719508.png
[ic780647]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780647.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic780648]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic780648.png
[ic789643]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic789643.png
[ic796926]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic796926.png
[ic719512]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719512.png
[ic719481]: ./media/azure-toolkit-for-eclipse-azure-role-properties/ic719481.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690945.aspx -->
