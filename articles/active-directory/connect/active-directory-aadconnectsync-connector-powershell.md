---
title: "aaaPowerShell 連接器 |Microsoft 文件"
description: "本文說明如何 tooconfigure Microsoft Windows PowerShell 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Windows PowerShell 連接器技術參考
本文描述 Windows PowerShell 連接器 hello。 hello 文章適用 toohello 下列產品：

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。

MIM2016 和 FIM2010R2，hello 連接器可做為從 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495)。

## <a name="overview-of-hello-powershell-connector"></a>Hello PowerShell 連接器的概觀
hello PowerShell 連接器可讓您與外部系統提供 Windows PowerShell 型的應用程式開發介面 toointegrate hello 同步處理服務。 2 (ECMA2) framework 與 Windows PowerShell，hello 連接器提供的 hello 呼叫基礎可延伸的連線的管理代理程式的 hello 功能之間的橋樑。 如需 hello ECMA 架構的詳細資訊，請參閱 hello[可延伸的連線能力 2.2 管理代理程式參考](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx)。

### <a name="prerequisites"></a>必要條件
使用 hello 連接器之前，請確定您擁有 hello 同步處理伺服器 hello 下列項目：

* Microsoft .NET 4.5.2 Framework 或更新版本
* Windows PowerShell 2.0、3.0 或 4.0

hello hello 同步處理服務的伺服器上的執行原則必須設定的 tooallow hello 連接器 toorun Windows PowerShell 指令碼。 除非 hello 指令碼 hello 連接器執行經過數位簽署，以執行此命令設定 hello 執行原則：  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>建立新的連接器
toocreate hello 同步處理服務中的 Windows PowerShell 連接器，您必須提供一系列的 Windows PowerShell 指令碼執行 hello hello 同步處理服務所要求的步驟。 根據 hello 資料來源連接所需的 tooand hello 功能，您必須實作的 hello 指令碼而異。 本節將概述 hello 指令碼，可以實作和它們所需的每個。

hello 連接器的 Windows PowerShell 設計 toostore 每個 hello hello 同步處理服務資料庫內的指令碼。 雖然可能 toorun 指令碼儲存在 hello 檔案系統上，它是直接在 toohello 連接器組態中的每個指令碼更容易 tooinsert hello 主體。

tooCreate PowerShell 連接器，請在**同步處理服務**選取**管理代理程式**和**建立**。 選取 hello **PowerShell (Microsoft)**連接器。

![建立連接器](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>連線能力
提供用於連接 tooa 遠端系統的組態參數。 這些值會安全地儲存由 hello 同步處理服務，並執行 hello 連接器時進行可用 tooyour Windows PowerShell 指令碼。

![連線能力](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

您可以設定下列連線參數的 hello:

**連線能力**

| 參數 | 預設值 | 目的 |
| --- | --- | --- |
| 伺服器 |<Blank> |Hello 連接器的伺服器名稱應該連接到。 |
| 網域 |<Blank> |Hello 認證 toostore hello 連接器執行時使用的網域。 |
| User |<Blank> |Hello 認證 toostore hello 連接器執行時使用的使用者名稱。 |
| 密碼 |<Blank> |Hello 認證 toostore hello 連接器執行時使用的密碼。 |
| 模擬連接器帳戶 |False |若為 true，hello 同步處理服務會提供 hello 認證 hello 內容中執行 hello Windows PowerShell 指令碼。 如果可能的話，我們建議的 hello **$Credentials**參數會傳遞 tooeach 而不是模擬使用指令碼。 如需其他權限的詳細資訊所需 toouse 此選項，請參閱 <<c0> [ 額外的設定為模擬](#additional-configuration-for-impersonation)。 |
| 模擬時載入使用者設定檔 |False |模擬期間，會指示 Windows tooload hello 使用者設定檔的 hello 連接器的認證。 如果 hello 模擬的使用者有漫遊設定檔，hello 連接器不載入 hello 漫遊設定檔。 如需其他權限的詳細資訊所需 toouse 這個參數，請參閱 <<c0> [ 額外的設定為模擬](#additional-configuration-for-impersonation)。 |
| 模擬時的登入類型 |None |模擬期間的登入類型。 如需詳細資訊，請參閱 hello [dwLogonType] [ dw]文件。 |
| 僅限已簽署的指令碼 |False |如果為 true，hello Windows PowerShell 連接器會驗證每個指令碼具有有效的數位簽章。 如果為 false，請確定 hello 同步處理服務伺服器的 Windows PowerShell 執行原則 RemoteSigned 或不受限制。 |

**通用模組**  
hello 連接器可讓您共用的 Windows PowerShell 模組 toostore hello 組態中。 Hello 連接器執行的指令碼，hello 模組是 Windows PowerShell 擷取 toohello 檔案系統，可以根據每個指令碼匯入。

匯入、 匯出和密碼同步處理的指令碼，hello 通用模組是會擷取的 toohello 連接器 MAData 資料夾。 結構描述、 驗證、 階層和資料分割探索指令碼，hello 通用模組是擷取的 toohello %TEMP%資料夾。 在這兩種情況下，hello 擷取通用模組，根據 toohello 一般模組的指令碼名稱設定名為指令碼。

tooload 模組呼叫 FIMPowerShellConnectorModule.psm1 hello MAData 資料夾，請使用下列陳述式的 hello:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload 模組呼叫 FIMPowerShellConnectorModule.psm1 從 hello %TEMP%資料夾，請使用下列陳述式的 hello:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**參數驗證**  
hello 驗證指令碼是選擇性的 Windows PowerShell 指令碼可以使用的 tooensure hello 系統管理員所提供的連接器組態參數都有效。 驗證伺服器、 連接認證及連線參數 hello 驗證指令碼的常見使用方式。 hello 驗證指令碼會呼叫 hello 下列索引標籤和對話方塊修改之後：

* 連線能力
* 全域參數
* 資料分割組態

hello 驗證指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |hello 設定 索引標籤或對話方塊觸發 hello 驗證要求。 |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |

hello 驗證指令碼應該會傳回單一 ParameterValidationResult 物件 toohello 管線。

**結構描述探索**  
hello 結構描述探索指令碼是必要的。 此指令碼傳回 hello 物件型別、 屬性和屬性條件約束設定屬性流程規則時，同步處理服務會使用該 hello。 hello 結構描述探索指令碼執行連接器的建立期間，並於其中填入 hello 連接器的結構描述。 它也會使用 hello hello 同步處理服務管理員中的重新整理結構描述動作。

hello 結構描述探索指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |

hello 指令碼必須傳回單一[結構描述][ schema]物件 toohello 管線。 hello 結構描述物件組成[SchemaType] [ schemaT]代表物件類型的物件 (例如： 使用者和群組)。 hello SchemaType 物件保存的集合[SchemaAttribute] [ schemaA]代表 hello 屬性的物件 (例如： 名字、 姓氏和郵寄地址) 的 hello 型別。

**其他參數**  
此外 toohello 標準組態設定，您可以定義額外的自訂組態設定的特定 toohello hello 連接器執行個體。 您可以在 hello 連接器，分割區，指定這些參數或層級執行的步驟，並從 hello 相關的 Windows PowerShell 指令碼存取。 自訂組態設定可以在 hello 同步處理服務資料庫中的純文字格式儲存，或可能會進行加密。 hello 同步處理服務會自動加密，並解密所需安全的組態設定。

每個參數以逗號 （，） 的個別 hello 名稱 toospecify 自訂組態設定。

從指令碼 tooaccess 自訂組態設定，您必須尾碼 hello 名稱以底線 ( \_ ) 和 hello hello 參數 （Global、 資料分割或 RunStep） 範圍。 例如，tooaccess hello 全域的 FileName 參數，請使用此程式碼片段：`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>功能
hello hello 管理代理程式的設計工具的 [功能] 索引標籤定義 hello 行為和 hello 連接器功能。 建立 hello 連接器後，無法修改此索引標籤上所做的 hello 選擇。 下表列出 hello 功能設定。

![功能](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| 功能 | 說明 |
| --- | --- |
| [辨別名稱樣式][dnstyle] |指出如果 hello 連接器支援的辨別的名稱，並因此，項目設定樣式。 |
| [匯出類型][exportT] |判斷 hello 會呈現 toohello 匯出指令碼的物件類型。 <li>AttributeReplace – 包含 hello 多重值屬性的值一組完整 hello 屬性變更時。</li><li>AttributeUpdate – 包括只有 hello 差異 tooa 多重值的屬性 hello 屬性變更時。</li><li>MultivaluedReferenceAttributeUpdate - 包含非參考多重值屬性一組完整的值，以及僅多重值參考屬性的差異。</li><li>ObjectReplace - 包含屬性變更時物件的所有屬性</li> |
| [資料正規化][DataNorm] |提供 tooscripts 之前，請指示 hello 同步處理服務 toonormalize 錨點屬性。 |
| [物件確認][oconf] |設定擱置匯入行為 hello hello 同步處理服務中。 <li>標準 – 需要所有的匯出的變更 toobe 確認透過匯入的預設行為</li><li>NoDeleteConfirmation - 當物件被刪除，就不會產生任何擱置中匯入。</li><li>NoAddAndDeleteConfirmation - 當物件建立或被刪除，就不會產生任何擱置中匯入。</li> |
| 使用 DN 做為錨點 |如果 hello 辨別名稱樣式設定 tooLDAP，hello 連接器空間的 hello 錨點屬性也是 hello 辨別的名稱。 |
| 數個連接器並行作業 |核取時，可以同時執行多個 Windows PowerShell 連接器。 |
| 分割數 |有選取時，hello 連接器便可支援多個資料分割和磁碟分割探索。 |
| 階層 |有選取時，hello 連接器支援 LDAP 樣式的階層式結構。 |
| 啟用匯入 |有選取時，hello 連接器匯入資料透過匯入指令碼。 |
| 啟用差異匯入 |有選取時，可以要求 hello 連接器，從 hello 差異匯入指令碼。 |
| 啟用匯出 |有選取時，hello 連接器匯出資料透過匯出指令碼。 |
| 啟用完整匯出 |有選取時，hello 匯出指令碼支援匯出 hello 整個連接器空間。 此選項，啟用匯出也必須檢查 toouse。 |
| 第一個匯出階段沒有參考值 |核取時，會在第二個匯出階段匯出參考屬性。 |
| 啟用物件重新命名 |核取時，您可以修改辨別名稱。 |
| 以刪除新增做為取代 |核取時，會將刪除新增作業匯出為單一取代。 |
| 啟用密碼作業 |核取時，可支援密碼同步處理指令碼。 |
| 在第一個階段啟用匯出密碼 |有選取時，建立 hello 物件時，會匯出在佈建期間設定的密碼。 |

### <a name="global-parameters"></a>全域參數
hello 管理代理程式的設計工具中的 hello 通用參數 索引標籤可讓您 tooconfigure hello Windows PowerShell 指令碼所執行的 hello 連接器。 您也可以設定在 hello 連線 索引標籤上定義的自訂組態設定的全域值。

**資料分割探索**  
資料分割是一個共用結構描述內的個別命名空間。 例如在 Active Directory 中，每個網域就是一個樹系內的資料分割。 資料分割是 hello 邏輯群組，以便匯入和匯出作業。 匯入和匯出將資料分割做為內容，而且所有作業會在此內容中發生。 資料分割在 LDAP 中應該 toorepresent 階層。 hello 資料分割的辨別的名稱會用於匯入 tooverify 所有傳回的物件是資料分割的 hello 範圍內。 在 hello metaverse toohello 連接器空間 toodetermine hello 磁碟分割物件應與在匯出期間從佈建也會使用 hello 資料分割的辨別的名稱。

hello 磁碟分割探索指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |

hello 指令碼必須傳回單一[分割][ part]物件或資料分割物件 toohello 管線的 [T] 清單。

**階層探索**  
只有在 LDAP hello 辨別名稱的樣式功能時，會使用 hello 階層探索指令碼。 hello 指令碼是使用的 tooallow 您 toobrowse，然後選取一組的容器，在或的範圍會被視為匯入和匯出作業。 hello 指令碼應該只提供一份 hello 根節點提供 toohello 指令碼的直接子系的節點。

hello 階層探索指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| ParentNode |[HierarchyNode][hn] |hello hello 階層下的 hello 指令碼應該會傳回直接子系的根節點。 |

hello 指令碼必須傳回單一子 HierarchyNode 物件或子 HierarchyNode 物件 toohello 管線的 [T] 清單。

#### <a name="import"></a>Import
支援匯入作業的連接器必須實作三個指令碼。

**開始匯入**  
hello 開始匯入 hello 開頭執行匯入步驟執行指令碼。 在此步驟中，您可以設定連線 toohello 來源系統，並先匯入資料，從 hello 連線系統執行準備步驟。

hello 開始匯入指令碼會接收 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |告知 hello 類型匯入執行 （差異或完整），資料分割、 階層、 浮水印，以及預期的頁面大小 hello 指令碼。 |
| 類型 |[結構描述][schema] |匯入的 hello 連接器空間的結構描述。 |

hello 指令碼必須傳回單一[OpenImportConnectionResults] [ oicres] toohello 管線的物件，例如：`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**匯入資料**  
直到 hello 指令碼，表示沒有任何多個資料 tooimport hello 匯入資料的指令碼會呼叫 hello 連接器。 hello Windows PowerShell 連接器具有 9,999 物件的頁面的大小。 如果您的指令碼在匯入時傳回超過 9,999 個物件，您必須支援分頁功能。 自訂資料的屬性，讓每個時間 hello 匯入資料的指令碼，您可以使用 tooa 存放區浮水印稱為 hello 連接器會公開，您的指令碼繼續匯入的物件中斷的位置。

hello 匯入資料的指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| GetImportEntriesRunStep |[ImportRunStep][irs] |保留 hello 分頁匯入期間可以使用的浮水印 (CustomData) 和差異匯入。 |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |告知 hello 類型匯入執行 （差異或完整），資料分割、 階層、 浮水印，以及預期的頁面大小 hello 指令碼。 |
| 類型 |[結構描述][schema] |匯入的 hello 連接器空間的結構描述。 |

hello 匯入資料的指令碼必須撰寫清單 [[CSEntryChange][csec]] 物件 toohello 管線。 這個集合是由代表每個所匯入物件的 CSEntryChange 屬性所組成。 在執行完整匯入時，這個集合應該有一組完整的 CSEntryChange 物件，而這些物件擁有每個物件的所有屬性。 差異匯入期間 hello CSEntryChange 物件應該包含每個物件 tooimport 或變更 （取代模式） 的 hello 物件的完整表示法的 hello 屬性層級差異。

**結束匯入**  
在執行的 hello 匯入的 hello 結束時，會執行 hello 結束匯入指令碼。 此指令碼應該執行任何清理必要工作 (例如，關閉連接 toosystems 和回應 toofailures)。

hello 結束匯入的指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |告知 hello 類型匯入執行 （差異或完整），資料分割、 階層、 浮水印，以及預期的頁面大小 hello 指令碼。 |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |告知 hello 匯入已結束的 hello 原因 hello 指令碼。 |

hello 指令碼必須傳回單一[CloseImportConnectionResults] [ cicres] toohello 管線的物件，例如：`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>匯出
Hello 連接器相同 toohello 匯入架構，支援匯出的連接器必須實作三個指令碼。

**開始匯出**  
hello 開始匯出 hello 開頭匯出執行步驟執行指令碼。 在此步驟中，您可以設定連線 toohello 來源系統，並匯出資料 toohello 連線系統之前，進行任何準備步驟。

hello 開始匯出指令碼會接收 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |告知 hello 的匯出執行 （差異或完整），資料分割、 階層和預期的頁面大小的型別中的 hello 指令碼。 |
| 類型 |[結構描述][schema] |匯出的 hello 連接器空間的結構描述。 |

hello 指令碼不應傳回任何輸出 toohello 管線。

**匯出資料**  
hello 同步處理服務呼叫 hello 匯出資料的指令碼，是必要的 tooprocess 所有擱置中匯出的次數。 如果 hello 連接器空間有多個暫止匯出比 hello 連接器的頁面大小，hello 匯出資料的指令碼呼叫多次，可能是多次的 hello 相同的物件。

hello 匯出資料的指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| CSEntries |IList[CSEntryChange][csec] |所有 hello 連接器空間物件和暫止的匯出 toobe 在此階段期間處理的清單。 |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |告知 hello 的匯出執行 （差異或完整），資料分割、 階層和預期的頁面大小的型別中的 hello 指令碼。 |
| 類型 |[結構描述][schema] |匯出的 hello 連接器空間的結構描述。 |

hello 匯出資料的指令碼必須傳回[PutExportEntriesResults] [ peeres]物件 toohello 管線。 此物件不針對每個匯出連接器需要 tooinclude 結果資訊，除非發生錯誤或變更 toohello 錨點屬性。 例如，tooreturn PutExportEntriesResults 物件 toohello 管線：`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**結束匯出**  
在 hello 匯出的 hello 結束時執行，hello 結束匯出指令碼 toorun。 此指令碼應該執行任何清理必要工作 (例如，關閉連接 toosystems 和回應 toofailures)。

hello 結束匯出指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |告知 hello 的匯出執行 （差異或完整），資料分割、 階層和預期的頁面大小的型別中的 hello 指令碼。 |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |告知已結束，hello 匯出的 hello 原因 hello 指令碼。 |

hello 指令碼不應傳回任何輸出 toohello 管線。

#### <a name="password-synchronization"></a>密碼同步處理
Windows PowerShell 連接器可以做為密碼變更/重設的目標。

hello 密碼指令碼會收到 hello hello 連接器中的下列參數：

| 名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Hello 連接器的組態參數的資料表。 |
| 認證 |[PSCredential][pscred] |包含輸入 hello 管理員 hello 連線 索引標籤上的任何認證。 |
| 資料分割 |[資料分割][part] |Hello CSEntry 的目錄磁碟分割內。 |
| CSEntry |[CSEntry][cse] |連接器空間項目 hello 物件接收密碼變更或重設。 |
| OperationType |String |指出 hello 作業是否將其重設 (**SetPassword**) 或變更 (**ChangePassword**)。 |
| PasswordOptions |[PasswordOptions][pwdopt] |旗標，指定 hello 主要密碼重設行為。 只有在 OperationType 是 **SetPassword**時才可以使用此參數。 |
| OldPassword |String |填入 hello 物件的舊密碼，密碼變更。 只有在 OperationType 是 **ChangePassword**時才可以使用此參數。 |
| NewPassword |String |填入 hello 物件應該設定 hello 指令碼的新密碼。 |

hello 密碼指令碼是不預期的 tooreturn 任何結果 toohello Windows PowerShell 管線。 如果 hello 密碼的指令碼中發生錯誤，hello 指令碼應該擲回下列 hello 問題相關的例外狀況 tooinform hello 同步處理服務的 hello 的其中一個：

* [PasswordPolicyViolationException] [ pwdex1] – 如果 hello 密碼不符合 hello 連線系統中的 hello 密碼原則會擲回。
* [PasswordIllFormedException] [ pwdex2] – 如果 hello 密碼是無法接受連接的 hello 系統會擲回。
* [PasswordExtension] [ pwdex3] – hello 密碼的指令碼中的所有其他錯誤，會擲回。

## <a name="sample-connectors"></a>範例連接器
Hello 可用的範例連接器的完整概觀，請參閱[Windows PowerShell 連接器範例連接器集合][samp]。

## <a name="other-notes"></a>其他注意事項
### <a name="additional-configuration-for-impersonation"></a>模擬的其他組態
授與 hello 是模擬 hello 下列 hello 同步處理服務的伺服器上的權限的使用者：

下列登錄機碼的讀取權限 toohello:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

toodetermine hello 安全性識別碼 (SID) 的 hello 同步處理服務服務帳戶，執行下列 PowerShell 命令的 hello:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

下列檔案系統資料夾的讀取權限 toohello:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

替換 hello {ConnectorName} 預留位置 hello hello Windows PowerShell 連接器名稱。

## <a name="troubleshooting"></a>疑難排解
* 如需如何 tooenable 記錄 tootroubleshoot hello 連接器資訊，請參閱 hello[如何 tooEnable ETW 追蹤連接器](http://go.microsoft.com/fwlink/?LinkId=335731)。

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
