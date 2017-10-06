---
title: "Azure AD Connect 同步： 了解 hello 架構 |Microsoft 文件"
description: "本主題描述 Azure AD Connect 同步處理 hello 架構，並說明 hello 詞彙。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Azure AD Connect 同步： 了解 hello 架構
本主題涵蓋 hello Azure AD Connect 同步處理的基本架構。在許多方面，它是類似 tooits 前置 MIIS 2003 ILM 2007 和 FIM 2010。 Azure AD Connect 同步是 hello 演進而來的這些技術。 如果您是熟悉這些舊版的技術，本主題的 hello 內容會熟悉 tooyou 以及。 如果您是新 toosynchronization，本主題是供您。 但它是不成功進行自訂 tooAzure AD Connect 同步 （本主題中的被呼叫的同步處理引擎） 在此主題 toobe 需求 tooknow hello 詳細資料。

## <a name="architecture"></a>架構
hello 同步處理引擎會建立多個連接的資料來源中儲存之物件的整合式的檢視，並管理這些資料來源中的身分識別資訊。 此整合式的檢視由 hello 身分識別資訊從連接的資料來源和一組規則，以決定擷取如何 tooprocess 這項資訊。

### <a name="connected-data-sources-and-connectors"></a>連接的資料來源和連接器
hello 同步處理引擎會處理來自不同的資料儲存機制，例如 Active Directory 或 SQL Server 資料庫的識別資訊。 每個資料儲存機制的組織其資料的資料庫類似格式，而且，提供標準的資料存取的方法是潛在的資料來源候選 hello 同步處理引擎。 hello 資料儲存機制已同步處理的同步處理引擎會呼叫**連接的資料來源**或**連接目錄**(CD)。

hello 同步處理引擎會封裝在模組呼叫連接的資料來源互動**連接器**。 每種類型的連接資料來源都有特定的連接器。 hello 連接器會需要的作業將轉譯成 hello 格式 hello 連接的資料來源能夠了解。

連接器進行 API 呼叫 tooexchange 身分識別資訊 （讀取和寫入） 與連接的資料來源。 它也是可能 tooadd 自訂連接器使用 hello 可延伸的連線能力的架構。 hello 如下圖所示連接器如何連接連接的資料來源 toohello 同步處理引擎。

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

資料可以任一方向流動，但無法同時以兩個方向流動。 換句話說，連接器可以設定的 tooallow 資料 tooflow hello 連接的資料來源 toosync 引擎從或同步處理引擎 toohello 連接的資料來源，但只有其中一個這些作業可能會發生一次一個物件和屬性。 hello 方向可以是不同的物件以及不同的屬性不同。

tooconfigure 連接器，您指定您想 toosynchronize 的 hello 物件類型。 指定 hello 物件型別定義 hello hello 同步處理程序中包含的物件範圍。 hello 下一個步驟是 tooselect hello 屬性 toosynchronize，也就是包含屬性清單。 可以隨時回應 toochanges tooyour 商務規則中變更這些設定。 當您使用 hello Azure AD Connect 的安裝精靈時，則會為您設定這些設定。

tooexport 物件 tooa 連接的資料來源，hello 屬性包含清單至少必須包含最小的 hello 屬性需要的 toocreate 連接的資料來源中的特定物件類型。 例如，hello **sAMAccountName**屬性必須包含在 hello 屬性包含清單 tooexport 使用者物件 tooActive 目錄必須具有在 Active Directory 中的所有使用者物件，因為**sAMAccountName**定義屬性。 同樣地，hello 安裝精靈會設定這個組態。

如果 hello 連接的資料來源使用結構的元件，例如資料分割或容器 tooorganize 物件，您可以限制 hello 連接的資料來源中的 hello 區域用於給定的解決方案。

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Hello 同步處理引擎命名空間的內部結構
hello 整個同步處理引擎命名空間包含兩個命名空間可儲存 hello 身分識別資訊。 hello 兩個命名空間是：

* hello 連接器空間 (CS)
* hello metaverse (MV)

hello**連接器空間**是包含 hello 指定 hello 屬性包含清單中指定的連接的資料來源和 hello 屬性從物件的表示法的臨時區域。 hello 同步處理引擎會使用 hello 連接器空間 toodetermine hello 連接資料來源和 toostage 傳入變更中的變更內容。 hello 同步處理引擎也會使用 hello 連接器空間 toostage 傳出匯出 toohello 連接的資料來源的變更。 hello 同步處理引擎會針對每個連接器維持為暫存區域的相異的連接器空間。

藉由使用臨時區域，hello 同步處理引擎會維持獨立的 hello 連接資料來源，並不會受到其可用性和存取範圍。 如此一來，您可以在任何時間的身分識別資訊使用處理 hello 資料 hello 臨時區域中。 hello 同步處理引擎可以要求後 hello 上次通訊工作階段終止或發送出 hello 變更 tooidentity 資訊只有 hello 連接的資料來源，尚未收到，進而降低內 hello 連接的資料來源所做的只有 hello 變更hello hello 同步處理引擎與 hello 連接的資料來源之間的網路流量。

此外，同步處理引擎會儲存它設置 hello 連接器空間中的所有物件的相關狀態資訊。 當收到新的資料時，同步處理引擎一律會評估是否已同步處理 hello 資料。

hello **metaverse**儲存區，其中包含彙總的 hello 身分識別資訊從多個連接的資料來源，提供單一的全域、 整合式檢視的所有合併物件。 擷取從 hello 連接資料來源和一組規則，可讓您 toocustomize hello 同步處理程序的 hello 身分識別資訊會根據建立 Metaverse 物件。

hello 如下圖所示 hello 連接器空間命名空間和 hello 同步處理引擎內 hello metaverse 命名空間。

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>同步處理引擎身分識別物件
hello 同步處理引擎中的 hello 物件是 hello 連接的資料來源中的任一個物件的表示法或 hello 同步處理引擎的整合的檢視這些物件。 每一個同步處理引擎物件都必須有全域唯一識別碼 (GUID)。 Guid 可提供資料完整性以及物件之間的快速關聯性。

### <a name="connector-space-objects"></a>連接器空間物件
當同步處理引擎會與連接的資料來源進行通訊時，它會讀取 hello 連接的資料來源中的 hello 身分識別資訊，和在 hello 連接器空間中使用該資訊 toocreate hello 身分識別物件的表示法。 您無法個別建立或刪除這些物件。 不過，您可以手動刪除連接器空間中的所有物件。

Hello 連接器空間中的所有物件都具有兩個屬性：

* 全域唯一識別碼 (GUID)
* 辨別名稱 (也稱為 DN)

如果 hello 連接資料來源指派唯一屬性 toohello 物件，然後 hello 連接器空間中的物件也可以有的錨點屬性。 hello 錨點屬性可唯一識別 hello 連接的資料來源中的物件。 hello 同步處理引擎會使用 hello 連接的資料來源中的 hello 錨點 toolocate hello 對應這個物件表示。 同步處理引擎會假設該 hello 的錨點物件永遠不會變更透過 hello hello 物件存留期。

許多 hello 連接器使用已知的唯一識別碼 toogenerate 錨點會自動為每個物件時匯入。 例如，hello Active Directory 連接器會使用 hello **objectGUID**屬性的錨點。 對於不提供清楚定義的唯一識別碼的連接的資料來源，您可以指定錨點產生 hello 連接器組態的一部分。

情況下，建置 hello 錨點從一個或多個唯一物件屬性類型，都不變更，並且可唯一識別 （例如，員工編號或使用者識別碼） hello 連接器空間中的 hello 物件。

連接器空間物件可以是 hello 下列其中一種：

* 預備物件
* 預留位置

### <a name="staging-objects"></a>預備物件
暫存物件代表 hello 指定 hello 連接的資料來源的物件類型的執行個體。 此外 toohello GUID 和 hello 辨別的名稱，暫存物件一律會有值，指出 hello 物件類型。

已一律匯入的暫存物件具有 hello 錨點屬性的值。 暫存物件的新佈建同步處理引擎中的 hello 連接的資料來源中建立的 hello 程序沒有 hello 錨點屬性的值。

暫存物件也含有商務屬性和同步處理引擎 tooperform hello 同步處理程序所需的操作資訊的目前值。 操作資訊包含旗標，表示 hello hello 暫存物件上的更新類型。 如果暫存物件已收到新識別資訊從尚未處理的 hello 連接的資料來源，hello 物件標示為**擱置匯入**。 如果暫存物件具有尚未匯出的 toohello 連接的資料來源的新識別資訊，就會標示為**暫止的匯出**。

預備物件可以是匯入物件或匯出物件。 hello 同步處理引擎會使用接收自 hello 連接的資料來源的物件資訊，以建立匯入物件。 當同步處理引擎收到 hello 存在的比對一個 hello hello 連接器中選取的物件類型的新物件的資訊時，它會建立匯入物件 hello 連接器空間中做 hello 連接的資料來源中的 hello 物件的表示法。

hello 下列圖例顯示匯入物件，代表 hello 連接的資料來源中的物件。

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

hello 同步處理引擎會建立匯出物件，使用 hello metaverse 中的物件資訊。 匯出物件 hello 下一步通訊工作階段期間進行匯出的 toohello 連接的資料來源。 Hello 同步處理引擎的 hello 觀點來看，從匯出的物件不存在於 hello 連接的資料來源尚未。 因此，匯出物件的 hello 錨點屬性無法使用。 從同步處理引擎收到 hello 物件之後，hello 連接的資料來源建立 hello 物件 hello 錨點屬性的唯一值。

hello 下圖顯示匯出的物件建立 hello metaverse 中使用身分識別資訊的方式。

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

hello 同步處理引擎會確認 hello 匯出的 hello 物件由 hello 物件從 hello 連接的資料來源重新匯入。 當同步處理引擎收到 hello 該連接的資料來源的下一步 匯入期間，匯出的物件就會變成匯入物件。

### <a name="placeholders"></a>預留位置
hello 同步處理引擎會使用一般命名空間 toostore 物件。 不過，有些連接的資料來源 (例如 Active Directory) 會使用階層式命名空間。 階層式命名空間從 tootransform 資訊到一般命名空間，同步處理引擎會使用預留位置 toopreserve hello 階層。

每個預留位置代表物件的階層名稱已經不匯入同步處理引擎，但不是必要的 tooconstruct hello 階層名稱的元件 （例如，組織單位）。 填滿間距的不暫存物件在 hello 連接器空間中的 hello 連接資料來源 tooobjects 中的參考所建立。

hello 同步處理引擎也會使用未匯入已的預留位置 toostore 參考物件。 例如，如果同步處理設定的 tooinclude hello 經理屬性 hello *Abbie Spencer*物件，並 hello 接收到的值是一個物件，但尚未已匯入，例如*CN = Lee Sperry，CN = Users，DC = fabrikam，DC = com*，hello 管理員資訊會儲存為 hello 連接器空間中的預留位置。 如果稍後匯入 hello 管理員物件時，會覆寫 hello 暫存物件，代表 hello 管理員 hello 預留位置物件。

### <a name="metaverse-objects"></a>Metaverse 物件
Metaverse 物件包含 hello 彙總檢視的 hello 暫存 hello 連接器空間中的物件具有該同步處理引擎。 同步處理引擎會使用匯入物件中的 hello 資訊建立 metaverse 物件。 有幾個連接器空間物件可以是連結的 tooa 單一 metaverse 物件，但連接器空間物件不能超過一個 metaverse 物件連結的 toomore。

無法以手動方式建立或刪除 Metaverse 物件。 hello 同步處理引擎會自動刪除 hello 連接器空間中沒有連結 tooany 連接器空間物件的 metaverse 物件。

toomap 內連接的資料來源 tooa 對應的物件類型 hello metaverse 中的物件，同步處理引擎會提供一組預先定義的物件類型和相關聯的屬性包含的可延伸結構描述。 您可以為 metaverse 物件建立新的物件類型和屬性。 屬性可以是單一數值或多重值，而且 hello 屬性型別可以是字串、 參考、 數字和布林值。

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>預備物件和 Metaverse 物件之間的關聯性
Hello 同步處理引擎命名空間內 hello 資料流程會啟用 hello 暫存物件和 metaverse 物件之間的連結關聯性。 暫存物件，這個物件稱為連結的 tooa metaverse 物件**聯結的物件**(或**連接器物件**)。 暫存的物件不是連結的 tooa metaverse 物件稱為**脫離物件**(或**斷路器物件**)。 hello 詞彙加入和退出是慣用的 toonot 混淆以 hello 連接器負責匯入和匯出資料從連接的目錄。

預留位置絕不會連結的 tooa metaverse 物件

聯結的物件包含暫存的物件和其連結關聯性 tooa 單一 metaverse 物件。 已加入的物件會使用的 toosynchronize 連接器空間物件和 metaverse 物件之間的屬性值。

當暫存物件會變成聯結的物件同步處理期間時，屬性可以在 hello 暫存物件和 hello metaverse 物件之間流動。 屬性流程是雙向的，並可使用匯入屬性規則和匯出屬性規則加以設定。

單一的連接器空間物件可以是連結的 tooonly 一個 metaverse 物件。 不過，每個 metaverse 物件可以連結的 toomultiple 連接器空間物件或不同的連接器空間中相同的 hello hello 下列圖例所示。

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

hello 連結 hello 暫存物件之間的關聯性，metaverse 物件都具有持續性，並會移除僅供您指定的規則。

脫離的物件是暫存物件不是連結的 tooany metaverse 物件。 hello 屬性脫離物件的值不會處理任何進一步 hello metaverse 中。 hello hello hello 連接的資料來源中的對應物件的值不會同步處理引擎更新的屬性。

使用分離的物件，可以將身分識別資訊儲存在同步處理引擎，稍後進行處理。 保留暫存物件當做脫離 hello 連接器空間物件有許多優點。 Hello 系統已經有分段 hello 所需資訊，此物件的相關，因為它不是這個物件表示一次在 hello 接著匯入從 hello 連接的資料來源的必要 toocreate。 如此一來，同步處理引擎一律會有完整的快照集的 hello 連接的資料來源，即使沒有目前的連接 toohello 連接的資料來源。 脫離的物件都可以轉換為已加入的物件，反之亦然，根據您指定的 hello 規則。

匯入物件會建立為分離物件。 匯出物件必須是聯結物件。 hello 系統邏輯會強制執行這項規則，並刪除每個匯出的物件不是聯結的物件。

## <a name="sync-engine-identity-management-process"></a>同步處理引擎身分識別管理程序
hello 身分識別管理程序會控制如何更新不同連接的資料來源之間的識別資訊。 身分識別管理可分為三個程序：

* Import
* 同步處理
* 匯出

在 hello 匯入過程中，同步處理引擎會評估 hello 傳入身分識別資訊從連接的資料來源。 偵測到變更時，它會建立新的暫存物件或更新現有同步處理的 hello 連接器空間中的暫存物件。

在 hello 同步處理過程中，同步處理引擎更新發生在 hello 連接器空間中的 hello metaverse tooreflect 變更，並更新 hello 連接器空間 tooreflect 變更 hello metaverse 中所發生的。

在 hello 匯出過程中，同步處理引擎推送變更，接移入暫存物件，且，已標示為暫止的匯出。

hello 下列圖例顯示每個 hello 處理程序發生做為身分識別資訊流程從一個連接的資料來源 tooanother。

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>匯入程序
在 hello 匯入過程中，同步處理引擎會評估更新 tooidentity 資訊。 同步處理引擎會比較從暫存物件的 hello 身分識別資訊與 hello 連接的資料來源收到 hello 身分識別資訊，並判斷是否 hello 暫存物件所需的更新。 如果它是暫存物件的新資料的必要 tooupdate hello，hello 暫存物件標示為暫止的匯入。

準備同步處理之前的 hello 連接器空間中的物件後，同步處理引擎可以處理僅 hello 身分識別已變更的資訊。 這個程序會提供下列優點 hello:

* **有效率的同步處理**。 資料同步處理期間處理的 hello 數量降到最低。
* **有效率的重新同步處理**。 您可以變更同步處理引擎如何處理不重新連線 hello 同步處理引擎 toohello 的資料來源的識別資訊。
* **商機 toopreview 同步**。 您可以預覽同步 tooverify hello 身分識別管理程序的相關假設正確無誤。

Hello 連接器中指定每個物件，如 hello 同步處理引擎會先嘗試 toolocate hello 連接器 hello 連接器空間中的 hello 物件的表示。 同步處理引擎會檢查 hello 連接器空間中的所有暫存物件，並嘗試 toofind 對應的暫存物件具有相符的錨點屬性。 如果沒有現有的暫存物件具有相符屬性的錨點、 同步處理引擎會嘗試 toofind 對應的暫存物件以 hello 相同辨別名稱。

當同步處理引擎會找到符合的辨別名稱，但不是錨點的暫存物件時，hello 特別會發生下列行為：

* 如果位於 hello 連接器空間中的 hello 物件有任何錨點，則同步處理引擎從 hello 連接器空間中移除此物件，並且標記 hello metaverse 物件是連結的 tooas**重試佈建的下一個同步處理執行**。 然後它會建立 hello 新匯入物件。
* 如果位於 hello 連接器空間中的 hello 物件具有錨點，同步處理引擎會假設，此物件已重新命名或刪除 hello 連接的目錄中。 它會將指派 hello 連接器空間物件的暫時、 以新辨別的名稱，使它可以階段 hello 連入的物件。 hello 舊物件就會變成**暫時性**、 等待 hello 連接器 tooimport hello 重新命名或刪除 tooresolve hello 的狀況。

如果同步處理引擎會找出對應 toohello 物件 hello 連接器中指定的暫存物件，它會判斷何種變更 tooapply。 例如，同步處理引擎可能會重新命名或刪除 hello 連接的資料來源中的 hello 物件或它可能只會更新 hello 物件的屬性值。

具有更新後資料的預備物件會標示為「擱置匯入」。 有不同的暫止匯入類型可以使用。 依據 hello hello 匯入程序結果 hello 連接器空間中的暫存物件具有 hello 下列擱置匯入類型的其中一個：

* **無**。 可使用的暫存物件的 hello 的 hello 屬性沒有變更 tooany。 同步處理引擎不會將此類型標示為「擱置匯入」。
* **新增**。 hello 暫存物件是 hello 連接器空間中的新匯入物件。 暫止進行其他處理 hello metaverse 中的匯入同步處理引擎旗標，這個型別。
* **更新**。 同步處理引擎 hello 連接器空間中，尋找對應的暫存物件，並標示擱置匯入做為這個型別，使其可以處理更新 toohello 屬性 hello metaverse 中。 更新包含物件重新命名。
* **刪除**。 同步處理引擎 hello 連接器空間中，尋找對應的暫存物件，並標示為擱置匯入這個類型，以便 hello 聯結的物件可以刪除的。
* **刪除/新增**。 同步處理引擎在 hello 連接器空間中，尋找對應的暫存物件，但 hello 物件類型不相符。 在此情況下，會預備刪除-新增的修改。 A 刪除新增修改表示 toohello 同步處理引擎，因為不同組的規則將套用 toothis 物件 hello 物件類型變更時，必須發生這個物件的完整重新同步處理。

藉由設定 hello 擱置匯入狀態的暫存物件很可能 tooreduce 大幅 hello 的同步處理期間處理，因為這樣做讓 hello 系統 tooprocess 只有在已更新資料的物件的資料量。

### <a name="synchronization-process"></a>同步處理程序
同步處理是由兩個相關的程序所組成：

* 輸入同步處理，hello metaverse 的 hello 內容更新利用 hello 連接器空間中的 hello 資料時。
* 輸出同步處理，hello 連接器空間中的 hello 內容更新 hello metaverse 中使用的資料時。

使用暫置在 hello 連接器空間中的 hello 資訊，hello 輸入同步處理程序建立 hello 資料儲存在 hello 連接資料來源中的 hello metaverse hello 整合檢視中。 所有暫存物件或只限於擱置匯入資訊是彙總，視 hello 規則的設定方式而定。

hello 輸出同步處理程序更新匯出物件 metaverse 物件變更時。

輸入同步處理建立 hello 收到 hello 連接資料來源的識別資訊的 hello metaverse 中的 hello 整合檢視。 同步處理引擎可以使用 hello 它已從 hello 連接資料來源最新識別資訊來處理在任何時間的身分識別資訊。

**輸入同步處理**

輸入同步處理包含下列程序的 hello:

* **佈建**(也稱為**投影**如果是從這個程序重要 toodistinguish 輸出同步處理佈建)。 hello 同步處理引擎會建立新的 metaverse 物件，根據暫存物件，並連結它們。 佈建是物件層級作業。
* **聯結**。 hello 同步處理引擎會將暫存物件 tooan 現有 metaverse 物件連結。 聯結是物件層級作業。
* **匯入屬性流程**。 同步處理引擎更新 hello 屬性值，稱為 hello metaverse 中的 hello 物件的屬性流程。 匯入屬性流程是屬性層級作業，其需要預備物件與 Metaverse 物件之間的連結。

佈建是會建立物件 hello metaverse 中的 hello 只有程序。 佈建只會影響屬於分離物件的匯入物件。 在佈建、 同步處理引擎會建立對應 hello 匯入物件 toohello 物件類型，且這兩個物件，以便建立聯結的物件間建立連結的 metaverse 物件。

hello 加入程序也會建立匯入物件和 metaverse 物件之間的連結。 聯結和佈建的 hello 差別在於 hello 加入程序需要該 hello 匯入物件是連結的 tooan 現有 metaverse 物件，其中 hello 佈建程序會建立新的 metaverse 物件。

同步處理引擎會嘗試 toojoin 匯入物件 tooa metaverse 物件，利用 hello 同步處理規則設定中指定的準則。

在 hello 佈建和聯結處理程序，請同步處理引擎會連結脫離的 tooa metaverse 物件，使其加入。 這些物件層級的作業都完成後，同步處理引擎可以更新 hello hello 相關聯的 metaverse 物件屬性值。 此程序稱為匯入屬性流程。

匯入屬性流程就會執行新的資料，而且連結的 tooa metaverse 物件的所有匯入物件上發生。

**輸出同步處理**

輸出同步處理會在 Metaverse 物件變更但未刪除時更新匯出物件。 hello 目標的輸出同步處理是 tooevaluate 是否變更 toometaverse 物件需要更新 toostaging 物件 hello 連接器空間中。 在某些情況下，更新的 hello 變更可能需要暫存物件中所有的連接器空間。 變更的預備物件會標示為「擱置匯出」，並使其成為匯出物件。 這些物件稍後推入 toohello 連接的資料來源 hello 匯出程序期間的匯出。

輸出同步處理有三個程序：

* **佈建**
* **解除佈建**
* **匯出屬性流程**

佈建和解除佈建都是物件層級的作業。 解除佈建相依於佈建，因為只有佈建可以啟始它。 佈建移除 hello 間的 metaverse 物件和匯出物件時，會觸發取消佈建。

佈建永遠觸發不套用的 tooobjects hello metaverse 中的變更。 當 toometaverse 物件進行變更時，同步處理引擎可以執行任何 hello hello 佈建程序的一部分，下列工作：

* 建立聯結的物件，其中的 metaverse 物件是新建立的連結的 tooa 匯出的物件。
* 重新命名聯結的物件。
* 斷開 Metaverse 物件與預備物件之間的連結，進而建立分離的物件。

佈建需要同步處理引擎 toocreate 新的連接器物件，如果是 hello 暫存物件 toowhich hello metaverse 物件連結永遠是匯出的物件，因為 hello 物件尚未存在 hello 連接的資料來源中。

如果佈建需要同步處理引擎 toodisjoin 聯結的物件，並建立脫離的物件，就會觸發取消佈建。 hello 解除佈建程序刪除 hello 物件。

在解除佈建，刪除匯出物件不會實際刪除 hello 物件。 hello 物件標示為**刪除**，這表示該 hello 刪除作業預備 hello 物件上。

匯入屬性流程的類似 toohello 方式匯出屬性流程也會發生在 hello 輸出同步處理過程中，輸入同步處理期間發生。 匯出屬性流程只會發生於聯結的 Metaverse 與匯出物件之間。

### <a name="export-process"></a>匯出程序
在 hello 匯出過程中，同步處理引擎會檢查所有暫止的匯出 hello 連接器空間，加上旗標的匯出物件，然後傳送更新 toohello 已連接資料來源。

hello 同步處理引擎可以判斷匯出的 hello 成功，但它完全無法判斷 hello 身分識別管理程序已完成。 Hello 連接的資料來源中的物件一律可以變更其他處理程序。 同步處理引擎不需要持續連線 toohello 連接的資料來源，因為它不足夠 toomake 假設 hello 屬性只根據成功匯出通知 hello 連接的資料來源中的物件。

例如，hello 中的處理序已連接資料來源無法變更 hello 物件的屬性回 tootheir 原始值 （也就是 hello 連接的資料來源可能會覆寫 hello 值 hello 資料推入縮小由同步處理引擎及成功之後，立即hello 連接的資料來源中套用）。

hello 同步處理引擎存放區匯出和匯入每個暫存物件的狀態資訊。 如果指定 hello 屬性包含清單中的 hello 屬性的值已變更過 hello 最後一個匯出，hello 匯入的儲存體，並適當地匯出狀態啟用同步處理引擎 tooreact。 同步處理引擎會使用 hello 匯入程序 tooconfirm 屬性值已匯出的 toohello 連接的資料來源。 匯入 hello 之間的比較，並匯出的詳細資訊，hello 下列圖例所示讓同步處理引擎 toodetermine hello 匯出是否成功，或是否需要 toobe 重複。

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

例如，如果同步處理引擎會匯出屬性 C 的值為 5，tooa 已連接資料來源，它會儲存在匯出狀態記憶體中的 C = 5。 在此物件上每個其他的匯出結果，嘗試 tooexport C = 5 toohello 連接的資料來源中一次因為同步處理引擎會假設，此值尚未持續套用的 toohello 物件 （亦即，除非已最近匯入不同的值從 hello 連接資料來源）。 C = 5 收到 hello 物件上的匯入作業期間時，會清除 hello 匯出記憶體。

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

