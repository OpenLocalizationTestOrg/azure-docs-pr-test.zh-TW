---
title: "Azure 角色屬性"
description: "了解如何使用適用於 Eclipse 的 Azure 工具組以進行 Azure 角色設定。"
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
ms.openlocfilehash: cd734c64ba6d1394cb261bace92dee9dd579dd08
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-role-properties"></a>Azure 角色屬性
您可以在適用於 Eclipse 的 Azure 工具組內設定 Azure 角色的各種組態設定。

## <a name="configuring-azure-role-properties"></a>設定 Azure 角色屬性
透過背景工作角色的各個屬性對話方塊，即可完成 Azure 角色屬性的設定工作。 在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，然後選取 [Azure] 子功能表。 (如果在 Eclipse 的 [專案總管] 中看不到角色，請在 [專案總管] 中展開 Azure 專案)。

![][ic789599]

本主題說明可以從 [屬性]  對話方塊設定的各種屬性。 要注意的是，在您建立新的 Azure 部署專案時，系統會自動填入其中的許多屬性。

以下是可供 Azure 角色使用的屬性頁。

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
在 Eclipse 的 [專案總管] 窗格中開啟角色的操作功能表，按一下 [Azure]，然後按一下 [屬性]，您就能夠變更虛擬機器的大小，而且也可以變更執行個體數目，如下圖所示。

![][ic719499]

> [!NOTE]
> 僅限 Windows：若您將執行個體數目設為大於 1 的值，並同時設定了應用程式伺服器，則不論此設定為何，工具組將只會允許在模擬器中執行 1 個角色執行個體。 這是為了避免不同的伺服器執行個體在同一部電腦上執行時，彼此之間發生連接埠繫結衝突 (例如，全都嘗試繫結至連接埠 8080) 。 您想要的執行個體計數設定會保留下來，但此設定只會在您部署至雲端時生效。
> 
> 

<a name="caching_properties"></a> 

### <a name="caching-properties"></a>快取屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [快取]。 在這個對話方塊中，您可以啟用已具名且共置的 memcache 相容快取，以協助 Web 應用程式加快速度。

![][ic719483]

在 [快取]  屬性頁內，您可以指定下列項目的全域設定：

* 是否啟用共置快取。
* 快取大小佔記憶體的百分比。
* 當應用程式以雲端服務的形式執行時，用來儲存快取狀態的儲存體帳戶名稱，若不想儲存快取狀態，則為無  (在計算模擬器中執行應用程式時，不會使用儲存體帳戶名稱)。如果您將儲存體帳戶名稱設定為 [(自動)] \(此為預設值)，您的快取設定會自動使用您在 [發佈至 Azure] 對話方塊中所選取的同一個儲存體帳戶。

> [!NOTE]
> 只有在使用 Eclipse 工具組的發佈精靈發佈部署時，[(自動)] 設定才會有所要的效果。 如果您改為使用外部機制 (例如 [Azure 管理入口網站][Azure Management Portal]) 手動發佈 .cspkg 檔案，部署作業將無法正確運作。
> 
> 

下列對話方塊顯示快取的各項屬性。

![][ic719501]

* **名稱：** 共置快取的名稱。
* **連接埠號碼：** 用於快取的連接埠號碼。
* **到期原則：** 可為下列其中一個值，用以指定快取中的金鑰何時到期。
  * **絕對：**到達 [存留分鐘數] 所指定的時間時，金鑰就會到期。
  * **永久有效：** 金鑰沒有到期時間。
  * **滑動視窗：**金鑰未遭到存取的時間達到 [存留分鐘數] 所指定的時間長度時，金鑰就會到期。金鑰一經存取，便會重設到期時鐘。
* **存留分鐘數：** 依據到期原則所決定的 Memcached 金鑰存留分鐘數上限。
* **在不同角色執行個體上複寫備份以提供高可用性：** 啟用時，有助於利用在不同角色執行個體上複寫備份以提供高可用性。 但請注意，若要讓此功能運作，您的部署中至少要有兩個作用中的角色執行個體。

若要新增快取，請按一下 [快取] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [設定具名快取] 對話方塊。 提供上述屬性的值。

若要修改具名快取，請選取快取，然後按一下 [快取] 屬性頁中的 [編輯] 按鈕。 隨即會開啟對話方塊供您修改快取屬性。 按 [確定]  以儲存快取值。

若要刪除快取，請選取快取，按一下 [快取] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。

如需有關如何使用快取的詳細資訊，請參閱[如何使用共置快取][How to Use Co-located Caching]。

<a name="certificates_properties"></a> 

### <a name="certificates-properties"></a>憑證屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [憑證]。

![][ic710964]

在這個對話方塊中，您可以新增或移除 Eclipse 專案所參考的憑證。 請注意，此處所列的憑證不會自動儲存在任何 Java 金鑰存放區內，因此無法自動在 Java 應用程式內提供使用。 這些憑證只會向 Azure 進行註冊，以便可以預先載入到執行部署之虛擬機器上的 Windows 憑證存放區，並於隨後供其他 Windows 軟體使用。 目前來說，工具組中只有一個功能會使用 [憑證] 對話方塊中以此方式所參考的憑證，那就是 [SSL 卸載][SSL Offloading]，因為此功能需依賴 Internet Information Services (IIS) 和應用程式要求路由 (ARR)，而這兩者要求適當的憑證必須以這種方式提供。

當您使用發佈精靈將專案部署至 Azure 時，系統會提示您指向這些憑證所對應的個人資訊交換 (PFX) 檔案以及憑證的密碼，以便自動將憑證上傳至 Azure 服務，但前提是這些憑證先前並未上傳至該處。

<a name="components_properties"></a> 

### <a name="components-properties"></a>元件屬性
在 Eclipse 的 [專案總管] 窗格中開啟角色的操作功能表，按一下 [Azure]，然後按一下 [元件]。 在這個對話方塊中，您可以新增、修改或移除角色的元件，以及變更它們的處理順序。

![][ic719502]

元件功能可讓您對 Azure 部署專案新增相依項目，例如 Java 應用程式專案、特殊檔案，以及部署所需的可執行命令列陳述式。

針對每個元件，您可以指定：

* 在建置 Azure 部署專案時，將元件匯入到其中時所要採取的步驟。
* 在 Azure 雲端部署該元件時所要採取的步驟。

> [!NOTE]
> 在指定元件檔案或命令列時請記住，您的部署將會發佈至 Windows 虛擬機器，因此您自訂的步驟必須適用於 Windows 架構的作業系統。 
> 
> 

元件具有下列屬性：

* **匯入：** 指出在建置專案時用來將元件匯入到其中的方法。 此屬性可為下列其中一個值：
  * **複製：**將元件從 [來源] 屬性所指定的本機路徑複製到角色的 **approot** 目錄。
  * **EAR：**元件是 Java 企業封存檔 (EAR)，從 [來源] 屬性所指定之本機路徑上的企業應用程式專案所匯入。 (工具組會根據該位置之專案的性質自動偵測此元件)。
  * **JAR：**元件是 Java 封存檔 (JAR)，從 [來源] 屬性所指定之本機路徑上的 Java 專案所匯入。 (工具組會根據該位置之專案的性質自動偵測此元件)。
  * **無：** 不採取任何動作來匯入元件。 此值適用於假設元件已出現在角色的 **approot** 目錄中時，或當元件只是如 [為] 屬性所指定的可執行命令列陳述式時 (當 [部署] 方法是 [可執行檔] 時)。
  * **WAR：**元件是 Java Web 應用程式封存檔 (WAR)，從 [來源] 屬性所指定之本機路徑上的動態 Web 專案所匯入。 (工具組會根據該位置之專案的性質自動偵測此元件)。
  * **Zip 檔：**元件是 Zip 檔案，透過壓縮 [來源] 屬性所指定的目錄或檔案所匯入。
* **來源：** 代表要匯入部署中之項目的資料夾或檔案在本機電腦上的來源路徑。 此屬性可以使用 Windows 環境變數。 在建置專案時，所有可匯入的元件都會匯入到角色的 **approot** 目錄。
  
    請注意，在部署到雲端 (而非計算模擬器) 時，可以透過下載來部署元件。 請參閱以下有關新增元件的相關資訊。    
* **為：**元件要匯入到角色的 **approot** 目錄下的檔案名稱，而且此元件最終會部署在 Azure 雲端。 將此屬性空白，可讓名稱保持與位於本機電腦上時相同  (若為可執行檔元件，亦即 [部署] 方法設為 [可執行檔] 的元件，此屬性可以是任意的 Windows 命令列陳述式。)
  
  > [!IMPORTANT]
  > 如果您對這個值使用空格字元，則會根據部署方法進行不同的處理。 如果部署方法是 [可執行檔] ，系統會將空格解譯為命令列引數分隔符號，而非檔案名稱的一部分。 若為其他所有部署方法，系統會將空格解譯為檔案名稱的一部分。
  > 
  > 
* **部署：** 指出開始部署時套用至元件之動作的方法。 此屬性可為下列其中一個值：
  
  * **複製：**元件會複製到 [目的地] 屬性所指定的目的地路徑。
  * **可執行檔：**元件是可執行的 Windows 命令列陳述式，會在開始部署於 [目的地] 屬性所指定之路徑的內容中執行。
  * **無：** 開始部署時，不會對元件套用任何動作。
  * **Zip 檔：**元件會解壓縮到 [目的地] 屬性所指定的目的地路徑。 這個方法只適用於 [匯入] 屬性是 [Zip 檔] 時。
* **目的地：** 元件將要部署在虛擬機器上的目的地路徑。 此屬性可以使用 Windows 環境變數，而且檔案路徑是相對於 **approot**。

若要新增元件，請按一下 [元件] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [Azure 角色元件] 對話方塊。 提供上述屬性的值。 

下圖顯示新增 WAR 元件的範例。

![][ic719503]

在部署到雲端 (而非計算模擬器) 時，如果您想要透過下載來部署元件，請確定您已核取 [在雲端中而非納入封裝時，透過下列方式部署]  。 如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入 URL 的其餘部分。 如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入元件的 URL。 指定下列其中一個方法：

* **複製：**下載元件會複製到 [目的地目錄] 路徑所指定的目的地路徑。
* **相同：**用於 [從下載部署] 和用於 [從封裝部署] 的方法相同。
* **Zip 檔：**下載元件會解壓縮到 [目的地目錄] 路徑所指定的目的地路徑。

若要修改元件，請選取元件，然後按一下 [元件] 屬性頁中的 [編輯] 按鈕。 隨即會開啟對話方塊供您修改元件屬性。 按 [確定]  以儲存元件值。

若要刪除元件，請選取元件，按一下 [元件] 屬性頁中的 [移除] 按鈕，然後按一下 [是]以確認刪除。

元件會依照所列順序進行處理。 使用 [上移] 和 [下移] 按鈕來排列順序。

> [!NOTE]
> 伺服器組態功能也需依賴元件。 不移除對應的伺服器組態，就無法移除或編輯這些元件。 當您嘗試對這類元件進行變更時，將會提示您相關資訊。
> 
> 

<!-- <a name="debugging_properties"></a> -->

<!-- ### Debugging properties -->
<!-- Open the context menu for the role in Eclipse's Project Explorer pane, click **Azure**, and then click **Debugging**. Within this dialog, you have the ability to enable or disable remote debugging, as well as create debug configurations, as shown in the following image. -->

<!-- ![][ic719504] -->

<!-- For related information about debugging, see [Debugging Azure Applications in Eclipse][Debugging Azure Applications in Eclipse]. -->

<a name="endpoints_properties"></a> 

### <a name="endpoints-properties"></a>端點屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [端點]。 在這個對話方塊中，您可以建立端點以及編輯或移除端點，如下圖所示。

![][ic719505]

若要新增端點，請按一下 [端點] 屬性頁中的 [新增] 按鈕，隨即就會開啟 [新增端點] 對話方塊。

![][ic710897]

輸入端點名稱，選取類型 ([輸入]、[內部] 或 [執行個體輸入])，並指定公用和私人連接埠。 按 [確定]  以儲存新的端點值。

根據端點的類型，您可以使用的連接埠範圍如下：

* 若為輸入執行個體端點，公用連接埠可以是連接埠範圍 (例如 **2000-2010**)，但私人連接埠是固定值。
* 若為內部端點，則不會使用公用連接埠，而且私用連接埠可以是範圍、保留空白，或設為星號以表示它會由 Azure 自動設定。
* 若為輸入端點，則公用連接埠只能是固定值，但私用連接埠可以是固定值、保留空白，或設為星號以表示它會由 Azure 自動設定。

如果您想要使用單一連接埠號碼而非某個範圍，請將代表範圍結尾的文字方塊保留空白。

針對設為自動設定的連接埠，如果您需要確定在執行階段實際使用的連接埠，則應用程式可以使用 [com.microsoft.windowsazure.serviceruntime 封裝摘要][com.microsoft.windowsazure.serviceruntime package summary]中所記載的「Azure 服務執行階段 API」。

<!-- To see how instance input endpoints can be used to help with debugging a multi-instance deployment, see [Debugging a specific role instance in a multi-instance deployment][Debugging a specific role instance in a multi-instance deployment]. -->

若要修改端點，請選取端點，然後按一下 [端點] 屬性頁中的 [編輯] 按鈕。 隨即會開啟對話方塊供您修改端點名稱、類型和公用與私人連接埠。 按 [確定]  以儲存修改過的端點值。

若要刪除端點，請選取端點，按一下 [端點] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。

為了正確設定使用者對某個角色所啟用的某些功能 (例如快取、工作階段親和性或 SSL 卸載)，工具組可能會自動設定隨使用者定義的端點一起列出的特殊端點。 只要啟用關聯的功能，工具組就會防止使用者編輯或刪除這類自動產生的端點。

<a name="environment_variables_properties"></a> 

### <a name="environment-variables-properties"></a>環境變數屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [環境變數]。 在這個對話方塊中，您可以建立環境變數以及修改或移除環境變數，如下圖所示。

![][ic719506]

當角色啟動時，啟動指令碼就能夠使用環境變數。

> [!NOTE]
> 在指定環境變數時請記住，您的部署將會發佈至 Windows 虛擬機器，因此您的環境變數必須適用於 Windows 架構的作業系統。
> 
> 

為了舉例說明角色啟動時可供使用的環境變數，請按一下 [新增] 按鈕以建立新的環境變數。 下圖顯示我們將會建立名為 **MyRoleVersion** 的環境變數，並對其指派 **1.0** 的值。

![][ic659268]

在 jsp 程式碼中，您可以使用 `System.getenv` 方法來顯示值：

    <body>
      <b> Hello World!</b>
      <p>Running role version: <%= System.getenv("MyRoleVersion") %></p>
    </body>

當應用程式執行時會產生以下輸出：

![][ic552233]

若要修改環境變數，請選取環境變數，然後按一下 [環境變數] 屬性頁中的 [編輯] 按鈕。 隨即會開啟對話方塊供您修改環境變數屬性。 按 [確定]  以儲存環境變數值。

若要刪除環境變數，請選取環境變數，按一下 [環境變數] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。

為了正確設定使用者對某個角色所啟用的某些功能 (例如伺服器組態、遠端偵錯或本機儲存體)，工具組可能會自動設定隨使用者定義的環境變數一起列出的特殊環境變數。 只要啟用關聯的功能，工具組就會防止使用者編輯或刪除這類自動產生的環境變數。

<a name="session_affinity_properties"></a> 

### <a name="load-balancing--session-affinity-aka-sticky-sessions-properties"></a>負載平衡/工作階段親和性 (也稱為「黏性工作階段」) 屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [負載平衡]。 在這個對話方塊中，您可以啟用或停用工作階段親和性，如下圖所示。

![][ic719492]

如需相關資訊，請參閱[工作階段親和性][Session Affinity]。 另外，請注意這項功能在 SSL 卸載情況下的行為，如 [SSL 卸載][SSL Offloading]所述。

<a name="local_storage_properties"></a> 

### <a name="local-storage-properties"></a>本機儲存體屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [本機儲存體]。 在這個對話方塊中，您可以建立、修改或移除正在執行應用程式之虛擬機器的暫存本機儲存體。 您可以針對本機儲存體大小，以及回收角色時是否保留其內容設定特定值，如下圖所示。

![][ic719508]

您也可以選擇性地指定對應至本機儲存體的環境變數。

根據預設，所有部署至 Azure 的項目皆會放置 (和解壓縮) 在角色執行個體的 **approot** 資料夾。 雖然該資料夾可容納大多數的簡單部署 (即使在解壓縮之後)，但配置給 **approot** 目錄的空間實際上有限且未明確定義 (根據經驗合理推估是小於 1 GB)。 因此，為確保 Azure 配置足夠的磁碟空間來容納 **approot** 資料夾可能放不下的較大部署，您應該使用 [本機儲存體] 對話方塊設定本機儲存資源。 若要了解這項設定的簡單做法，請參閱[部署大型部署][Deploying Large Deployments]。

您可以使用由 Eclipse 工具組自動關聯至資源的環境變數，從啟動指令碼 (例如 **startup.cmd**) 輕鬆參考儲存體資源，如 [本機儲存體] 對話方塊所示。 該環境變數會包含您已在執行啟動指令碼時設定之本機資源的完整路徑。 

若要修改本機儲存資源，請選取本機儲存資源，然後按一下 [本機儲存體] 屬性頁中的 [編輯] 按鈕。 隨即會開啟對話方塊供您修改本機儲存資源屬性。 按 [確定]  以儲存本機儲存資源的值。

若要刪除本機儲存資源，請選取本機儲存資源，按一下 [本機儲存] 屬性頁中的 [移除] 按鈕，然後按一下 [是] 以確認刪除。

<a name="server_configuration_properties"></a> 

### <a name="server-configuration-properties"></a>伺服器組態屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [伺服器組態]。 在這個對話方塊中，您可以新增、移除和修改部署所使用的 JDK 和 Java 應用程式伺服器，以及新增或移除部署所使用的應用程式 (例如 WAR、JAR 或 EAR 檔案)。

### <a name="jdk-configuration"></a>JDK 組態
這個對話方塊可讓您指定要用於部署的 JDK 封裝。 如果您在 Windows 上使用 Eclipse，您可以指定當 JDK 封裝是在 Azure 模擬器中執行時，讓此封裝在本機上使用，而且您可以選擇將該本機安裝部署至 Azure。 在非 Windows 作業系統上則不適用模擬器 JDK 設定，而且您無法部署本機安裝的 JDK，因為它與 Windows 不相容。 不過，無論您使用什麼作業系統，一律都可以選擇使用第三方 JDK 封裝來部署至 Azure，或從其他下載位置指向您自己的 Windows 相容 JDK 封裝。

以下範例說明如何在 Windows 上指定 JDK：

![][ic780647]

如果您在 Windows 上使用 Eclipse，您可以指定用於計算模擬器的 JDK，若要進行指定，請確定已勾選 [模擬器部署] 區段中的 [使用此檔案路徑中的 JDK 以進行本機測試]。 然後，指定 JDK 的本機路徑，如果系統未自動選取您想使用的 JDK，您可以瀏覽至不同的 JDK。 您也可以選擇將 JDK 部署至 Azure 雲端服務，若要這樣做，請選取 [雲端部署] 區段中的 [部署本機 JDK (自動上傳至雲端儲存體)] 選項。

附註：在非 Windows 作業系統中，無法使用 [模擬器部署] 設定和 [部署本機 JDK] 選項。 下列範例說明如何在 Mac 或其他支援的非 Windows 作業系統上指定 JDK：

![][ic789643]

不論您所在的作業系統為何，JDK 封裝的來源和類型都有下列兩個 [雲端部署]  選項：

* **部署 Azure 提供的第三方 JDK 封裝** 
* **從自訂下載部署** 

如果您使用 [部署可從 Azure 取得的第三方 JDK 封裝]  選項：

1. 核取名為 [部署可從 Azure 取得的第三方 JDK 封裝] 的核取方塊。
2. 從下拉式清單中，選取 Azure 提供的第三方 JDK 封裝。
3. 您**JDK**  索引標籤看起來類似下列的 Windows:![][ic780648]和看起來會類似下列的 Mac OS 或其他支援的非 Windows 作業系統：![][ic789643]
4. 按一下 [確定]  儲存變更。
5. 當系統提示您接受第三方 JDK 封裝提供者所提出的授權合約時，請檢閱授權條款。 假設您接受這些條款，請按一下 [是] 以關閉 [接受授權合約] 對話方塊。
    請注意，您可以自訂 [部署可從 Azure 取得的第三方 JDK 封裝] 選項的下拉式清單中要出現哪些項目的基礎邏輯。 若要自訂出現的項目，請在 [JDK] 對話方塊中按一下 [自訂] 連結。 此動作將會關閉 [JDK] 屬性頁，並在 Eclipse 中開啟 **componentsets.xml** 檔案，然後您就可以視需要進行修改。 **componentsets.xml** 的說明文件隨附於 **componentsets.xml** 檔案本身。

如果您使用 [從自訂下載部署 JDK]  選項：

1. 建立 JDK 安裝目錄的 ZIP 檔，確保目錄節點本身是 ZIP 結構的子系，而非其內容的子系。 記下目錄名稱，因為您稍後會需要它，並請記住此 JDK 安裝將會部署到 Windows 虛擬機器。
2. 以 blob 的形式將 ZIP 檔上傳到 Azure 儲存體帳戶。 若要這麼做，您可以使用外部取得的工具來將 blob 上傳至 Azure 儲存體。 建議您使用私人 blob。 記下 ZIP 內容的 blob URL。
3. 核取名為 [從自訂下載部署 JDK] 的核取方塊。
    如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入 URL 的其餘部分。 如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入 JDK 下載的 URL。 如果使用 Azure 儲存體，則 URL 中的 blob 名稱必須是小寫。
4. 確定 [JAVA_HOME] 文字方塊有參考正確的目錄名稱。 根據預設，它會參考與您為本機使用所選擇之值相同的 JDK 目錄名稱。 但如果 ZIP 檔中包含的目錄有不同名稱 (例如由於使用不同版本)，請相應地更新 [JAVA_HOME] 文字方塊中的目錄名稱，因為此設定會用於雲端 (而非計算模擬器)。
5. 按一下 [確定]  儲存變更。

就這麼簡單。 現在，當您針對雲端進行建置時，您會發現封裝大小變小很多，建置程序所需的時間通常較少，而且部署本身在發佈至雲端時所需的時間也應該會變少。 請注意，只有當應用程式部署在雲端時，[部署本機 JDK (自動上傳至雲端儲存體)] 或 [從自訂下載部署 JDK] 選項才有作用。 在使用計算模擬器時，這兩個選項不會有任何作用，當您部署至計算模擬器時，仍然會使用本機版本的元件。 

### <a name="server-configuration"></a>伺服器組態
以下範例說明如何指定應用程式伺服器。

![][ic796926]

確認已選取 [部署此類型的伺服器]  核取方塊，然後選擇您想要使用的應用程式伺服器類型。

若要指定要用於雲端部署的伺服器，您可以利用下列選項：

1. **部署 Azure 提供的第三方伺服器** - 這個選項特別適用於開發/測試案例，因為這種案例的優先考量是部署效率和簡易性，因此伺服器不需要自訂組態。 或者，當您想要使用其中一部伺服器做為起點，但您在部署的啟動邏輯中加入了適當的伺服器自訂步驟。
2. **從自訂下載部署** - 這個選項特別適用於生產案例，前提示您有為了在雲端中使用而特別準備及設定的伺服器。
3. **部署本機伺服器安裝** - 這個選項特別適用於如果本機伺服器安裝已針對您的用途進行自訂設定。 如果您選擇此選項，則必須同時在下方的 [本機伺服器路徑]  文字方塊中指定本機伺服器的路徑。

如果您使用 [部署 Azure 提供的第三方伺服器]  選項：

1. 核取名為 [部署 Azure 提供的第三方伺服器] 的核取方塊。
2. 從下拉式功能表中，選取想要在雲端中搭配部署使用的伺服器軟體。 請注意，如果您先前已指定要使用的伺服器類型，您會遭到限制而只能選擇與該伺服器類型位於相同系列中的雲端伺服器。 但如果您沒有選擇伺服器類型，則可以選擇 Azure 上目前提供的任何伺服器，而且系統會自動為您選取伺服器類型。
3. 按一下 [確定]  以儲存變更。

如果使用 [從自訂下載部署]  選項：

1. 確定您已根據上述步驟選取伺服器類型。 這會告訴外掛程式如何從自訂下載部署伺服器，因為伺服器必須來自與所選伺服器類型相同的系列。
2. 核取名為 [部署可從 Azure 取得的第三方 JDK 封裝] **從自訂下載部署**。
    如果您想要從 Azure 儲存體帳戶進行下載，請從 [儲存體帳戶] 下拉式清單選取儲存體帳戶 (您可以按一下 [帳戶] 連結以修改清單內容)，所選結果會部分填入 [URL] 欄位，請您自行填入伺服器下載 ZIP 檔之 URL 的其餘部分 (在使用 Azure 儲存體時，URL 中的 blob 名稱必須是小寫)。 如果您不想使用 Azure 儲存體，請從 [儲存體帳戶] 下拉式清單選取 [(無)]，然後在 [URL] 欄位中輸入伺服器下載 ZIP 檔的 URL。 ZIP 檔會包含代表應用程式伺服器安裝目錄的子資料夾。 例如，如果您使用 Apache Tomcat 7.0.35 的 ZIP 檔，ZIP 檔內會有代表安裝目錄的子資料夾，例如 **apache-tomcat-7.0.35**。 
3. 指定主目錄環境變數的值。 它會預設為用於本機應用程式伺服器的值 (如果有的話)，但如果您的雲端應用程式伺服器與本機應用程式伺服器不同，則可以指定不同的值。 不過，您必須確定雲端應用程式伺服器屬於與先前所選伺服器類型相同的系列。
    如果您日後更新雲端應用程式伺服器 ZIP 檔，您可以手動變更主目錄設定，或讓它再次符合本機設定 (如果您也變更了本機應用程式伺服器)。
4. 按一下 [確定]  儲存變更。

您可以自訂 [伺服器組態] 屬性頁的 [伺服器] 索引標籤中要出現哪些項目的基礎邏輯。 如果您需要的不是預設值，或如果您想要新增其他伺服器，就可能需要這項進階功能。 若要自訂此邏輯，請在 [伺服器] 對話方塊中按一下 [自訂] 連結。 此動作將會關閉 [伺服器組態] 屬性頁，並在 Eclipse 中開啟 **componentsets.xml** 檔案，然後您就可以視需要進行修改，以擴充伺服器組態範本。 **componentsets.xml** 的說明文件隨附於 **componentsets.xml** 檔案本身。

如果您使用 [部署本機伺服器 (自動上傳至雲端儲存體)]  選項：

1. 核取名為 [部署本機伺服器 (自動上傳至雲端儲存體)] 的核取方塊。
2. 使用 [儲存體帳戶] 下拉式清單，選取 [(自動)]。 如果您在此指定 [(自動)]，Eclipse 工具組會為您的伺服器使用與您在 [發佈至 Azure] 對話方塊中為部署所選帳戶相同的儲存體帳戶。
3. 按一下 [確定]  儲存變更。

如果下列任一條件成立，請在 [本機伺服器路徑]  文字方塊中選取電腦上的伺服器安裝路徑：

* 您想要在模擬器中測試部署 (僅適用於 Windows)。
* 您想要將本機安裝的伺服器部署到雲端。
* 您想要使用雲端中的自有自訂伺服器下載，若是這種情況，也請確定您已選取上面的 [部署本機伺服器 (自動上傳至雲端儲存體)]  選項。

如果您的情況不適用上述任何選項，則可以選擇使用本機伺服器設定。

### <a name="applications-configuration"></a>應用程式組態
以下範例說明如何指定應用程式。

![][ic719512]

按一下 [新增] 以新增其他應用程式，或按一下 [移除] 以移除應用程式。 為求效率，如果您想要在部署到雲端時使用下載做為應用程式的來源，請使用 [元件屬性](#components_properties) 以指定 URL、儲存體帳戶等項目。 

從 2014 年 4 月版本開始，您的應用程式會自動上傳至與您為部署所選帳戶相同的儲存體帳戶 (在 **eclipsedeploy** 容器之下)。 部署的啟動邏輯包含先從該儲存體帳戶下載這些應用程式的步驟。 這表示您不需要重新建置並重新部署整個封裝就可以升級部署中的應用程式，方法是直接將較新版的應用程式手動上傳至該儲存體帳戶 (例如使用 Azure 入口網站)，來取代工具組原本上傳至該處的 WAR 檔案。 然後，就只要再次使用 Azure 的管理入口網站或透過命令列公用程式開始回收所有角色執行個體  (目前不支援直接從 Eclipse 工具組內觸發角色回收程序)。

### <a name="notes-about-server-configuration"></a>伺服器組態的相關注意事項
透過 [伺服器組態] 屬性頁所做的變更會反映在 package.xml 檔的 `<component>` 元素中。

當您針對 JDK 或應用程式伺服器使用 [自動上傳...] 或 [從下載部署...] 選項，而且您正在針對雲端 (而非計算模擬器) 進行建置，並且已連線到網路時，您可能會發現建置訊息 (例如主控台輸出中的下列內容)，因為 Ant 產生器會驗證下載的可用性：

`[windowsazurepackage] Verifying blob availability (https://example.blob.core.windows.net/temp/tomcat6.zip)...` 

如果您選取 [從下載部署...]  選項，可能會顯示下列警告，但建置作業會繼續：

`[windowsazurepackage] warning: Failed to confirm blob availability! Make sure the URL and/or the access key is correct (https://example.blob.core.windows.net/temp/tomcat6.zip).` 

只有這個警告會指出尚未驗證下載的可用性。 因此如果雲端中的部署因為某些原因失敗，請檢查是否有收到這個警告。

如果您想要停用下載驗證 (例如，如果您認為進行驗證只會拖慢建置速度)，請在 package.xml 的 `<windowsazurepackage>` 項目中，將 `verifydownloads` 屬性設定為 `false`。 

`<windowsazurepackage verifydownloads="false" ...>` 

如果您已選取 [自動上傳...]  選項，則每當需要上傳時，您就會在主控台視窗中看到每隔 5 秒報告一次上傳進度的建置訊息。

<a name="ssl_offloading_properties"></a> 

### <a name="ssl-offloading-properties"></a>SSL 卸載屬性
在 Eclipse 的 [專案總管] 窗格中，開啟角色的操作功能表，按一下 [Azure]，然後按一下 [SSL 卸載]。 

![][ic719481]

在這個對話方塊中，您可以啟用 SSL 卸載，以便在 Azure 上的 Java 部署中輕鬆啟用超文字安全傳輸通訊協定 (HTTPS) 支援，而不必在 Java 應用程式伺服器中設定 SSL。 如需詳細資訊，請參閱 [SSL 卸載][SSL Offloading]和[如何使用 SSL 卸載][How to Use SSL Offloading]。

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[安裝適用於 Eclipse 的 Azure 工具組][Installing the Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[Azure 專案屬性][Azure Project Properties]

[Azure 儲存體帳戶清單][Azure Storage Account List]

如需有關如何搭配使用 Azure 與 Java 的詳細資訊，請參閱 [Azure Java 開發人員中心][Azure Java Developer Center]。

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
[How to Use Co-located Caching]: http://go.microsoft.com/fwlink/?LinkID=699542
[How to Use SSL Offloading]: http://go.microsoft.com/fwlink/?LinkID=699545
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
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
