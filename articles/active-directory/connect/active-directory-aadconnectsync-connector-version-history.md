---
title: "aaaConnector 版本發行記錄 |Microsoft 文件"
description: "本主題列出 hello 連接器的所有版本 Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>連接器版本發行歷程記錄
Forefront Identity Manager (FIM) 和 Microsoft Identity Manager (MIM) hello 連接器會經常更新。

> [!NOTE]
> 本主題僅討論 FIM 與 MIM。 不支援在 Azure AD Connect 上安裝這些連接器。 發行的連接器在升級 toospecified 組建時，會預先安裝在 AADConnect。

本主題列出 hello 連接器已發行的所有的版本。

相關連結：

* [下載最新的連接器](http://go.microsoft.com/fwlink/?LinkId=717495)
* [一般 LDAP 連接器](active-directory-aadconnectsync-connector-genericldap.md) 參考文件
* [一般 SQL 連接器](active-directory-aadconnectsync-connector-genericsql.md) 參考文件
* [Web 服務連接器](http://go.microsoft.com/fwlink/?LinkID=226245) 參考文件
* [PowerShell 連接器](active-directory-aadconnectsync-connector-powershell.md) 參考文件
* [Lotus Domino 連接器](active-directory-aadconnectsync-connector-domino.md) 參考文件


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect 擱置版本)


### <a name="fixed-issues"></a>已修正的問題：

* 一般 Web 服務︰
  * 已修正在有兩個或多個端點時無法建立 SOAP 專案的問題。
* 一般 SQL：
  * Hello 匯入作業中 hello GSQL 已不會將轉換時間是否正確，當儲存 tooconnector 空間。 hello 預設日期和時間格式的 hello GSQL 連接器空間已經從 'yyyy MM dd: ssz' too'yyyy-MM-dd: ssz '。

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>已修正的問題：

* 一般 Web 服務︰
  * hello Wsconfig 工具未轉換正確 hello Json 陣列，從 「 範例要求 」 hello REST 服務方法。 這會造成問題的序列化 hello REST 要求此 Json 陣列。
  * Web 服務連接器組態工具不支援在 JSON 屬性名稱中使用空間符號 
    * 取代模式可以手動新增 toohello WSConfigTool.exe.config 檔案，例如：```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes：
  * 當 hello 選項**公司/組織單位可讓自訂 certifiers**已停用將 hello 連接器無法在匯出後 hello 匯出傳送所有屬性 （更新） 期間會匯出的 tooDomino，但在 hello 時間匯出 KeyNotFoundException 會傳回 tooSync。 
    * 藉由變更下列 hello 屬性的其中一個主要原因是嘗試 toochange DN （使用者名稱屬性） 時，hello 重新命名作業將會失敗：  
      - 姓氏
      - FirstName
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - ou
      - altcommonname

  * 當 [允許組織/組織單位使用自訂認證者] 選項啟用，但必要的認證者仍然空白時，就會出現 KeyNotFoundException。

### <a name="enhancements"></a>增強功能：

* 一般 SQL：
  * **情節：重新設計的實作：** "*" 功能
  * **解決方案說明：**已變更[多重值參照屬性處理方法](active-directory-aadconnectsync-connector-genericsql.md)。


### <a name="fixed-issues"></a>已修正的問題：

* 一般 Web 服務︰
  * 如果 WebService 連接器存在，則無法匯入伺服器組態
  * WebService 連接器不使用多個 Web 服務

* 一般 SQL：
  * 不列出單一值所參照屬性的物件類型
  * 移除多重值資料表中的值時，變更追蹤策略上的差異匯入會刪除物件
  * GSQL 連線器中的 OverflowException 與 AS/400 上的 DB2

Lotus：
  * 加入的選項 tooenable\disable 開啟 GlobalParameters 頁面之前搜尋的 Ou

## <a name="114430"></a>1.1.443.0

發行日期：2017 年 3 月

### <a name="enhancements"></a>增強功能

* 一般 SQL：</br>
  **案例徵兆：**它是以 hello SQL Connector 我們只允許參考 tooone 物件類型而且需要與成員的交叉參考已知的限制。 </br>
  **方案的描述：** hello 處理步驟的參考是"*"選擇選項，回復 toohello 同步處理引擎會傳回所有物件類型的組合。

>[!Important]
- 這會造成許多預留位置
- 它是必要的 toomake 確定 hello 命名為唯一跨物件類型。


* 一般 LDAP：</br>
 **案例：**只有幾個容器會選取特定的資料分割中，然後 hello 搜尋仍會執行整個分割區中。 詳細資料會依同步處理服務來進行篩選，而不是依可能會造成效能降低的 MA。 </br>

 **方案的描述：**變更 GLDAP 連接器的程式碼 toomake 它可能瀏覽所有容器，並在每個項目，而不是在 hello 整個分割區中搜尋中搜尋物件。


* Lotus Domino：

  **案例︰**在匯出期間移除人員時支援刪除 Domino 郵件。 </br>
  **解決方案︰**可設定在匯出期間移除人員時刪除 Domino 郵件的支援。

### <a name="fixed-issues"></a>已修正的問題：
* 一般 Web 服務︰
 * 則會發生下列錯誤 hello 預設變更 hello 服務 URL 時 SAP wsconfig 規劃透過 web 服務組態工具： 找不到 hello 路徑的一部分

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* 一般 LDAP：
 * GLDAP 連接器無法看到 AD LDS 中的所有屬性
 * 精靈偵測不到任何 UPN 屬性從 hello LDAP 目錄結構描述時的符號
 * 如果未選取 "objectclass" 屬性，完整匯入期間不會顯示差異匯入的探索失敗錯誤
 * 「 設定資料分割和階層 」 設定 頁面中，不會顯示哪種類型是等於 toohello Novel 伺服器 hello 泛型中的資料分割的任何物件  
LDAP MA。 頁面上只會顯示來自 RootDSE 資料分割的物件。


* 一般 SQL：
 * 修正未匯入一般 SQL 浮水印差異匯入多重值屬性的錯誤
 * 匯出作業刪除\新增多重值屬性的值時，不會在資料來源中刪除\新增這些值。  


* Lotus Notes：
 * 「 完整名稱 」 顯示 hello metaverse 中正確但是時匯出 tooNotes hello 值 hello 屬性是 Null 或空的特定欄位。
 * 修正重複認證者錯誤
 * 與其他物件的 hello Lotus Domino 連接器上選取 hello 物件沒有任何資料時然後我們收到 hello 探索錯誤時執行完整匯入。
 * 差異匯入時正在執行上 hello Lotus Domino 連接器，在該回合，hello 的 hello 結尾 Microsoft.IdentityManagement.MA.LotusDomino.Service.exe 服務有時會傳回應用程式錯誤。
 * 群組成員資格的整體運作正常，仍會保留，但執行 hello 匯出 tootry tooremove 使用者時從成員資格顯示為成功安裝更新後，但不會實際取得 Lotus Notes 的成員資格中移除 hello 使用者。
 * 匯出為 「 在下方的附加項目 」 的機會 toochoose 模式已在組態中加入 GUI Lotus MA tooappend 新項目底部多重值屬性的 hello 匯出期間。
 * 連接器會將 hello 需要邏輯 toodelete hello 檔案從 hello 郵件資料夾和識別碼保存庫。
 * 刪除成員資格時不會跨 NAB 成員進行。
 * 值應該會成功從多重值屬性中刪除

## <a name="111170"></a>1.1.117.0
發行日期：2016 年 3 月

**一般 SQL 連接器**  
初始版本的 hello[泛型 SQL Connector](active-directory-aadconnectsync-connector-genericsql.md)。

**新功能︰**

* 一般 LDAP 連接器：
  * 新增使用 Isode 進行差異匯入的支援。
* Web 服務連接器：
  * 更新的 hello csEntryChangeResult 活動和 setImportErrorCode 活動 tooallow 物件層級錯誤 toobe 傳回後 toohello 同步處理引擎。
  * 更新的 hello SAP6 和 SAP6User 範本 toouse hello 新物件層級錯誤功能。
* Lotus Domino 連接器：
  * 進行匯出時，您需要針對每個通訊錄使用一個認證者。 您可以現在使用 hello 相同密碼的所有 certifiers toomake hello 管理更容易。

**已修正的問題：**

* 一般 LDAP 連接器：
  * 針對 IBM Tivoli DS，並未正確偵測到某些參考屬性。
  * 若為差異匯入期間開啟 LDAP，已截斷空白字元 hello 開頭和結尾的字串。
  * Novell 與 NetIQ，Ou/容器之間，而在 hello 移動物件的匯出相同的時間已重新命名的 hello 物件失敗。
* Web 服務連接器：
  * 如果 hello web 服務在相同的繫結的多個端點，然後 hello 連接器未正確地探索這些端點。
* Lotus Domino 連接器：
  * 匯出的 hello fullName 屬性 tooa mail 在資料庫無法運作。
  * 匯出會同時加入和從群組移除成員，只匯出的 hello 加入成員。
  * 如果是無效的資訊文件 （hello 屬性 isValid 設定 toofalse），然後 hello 連接器會失敗。

## <a name="older-releases"></a>較舊的版本
2016 年 3 月前 hello 連接器已經發行支援 主題。

**一般 LDAP**

* [KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597，2015 年 9 月
* [KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549，2015 年 3 月
* [KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534，2015 年 1 月
* [KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419，2014 年 9 月
* [KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082，2014 年 3 月

**WebServices**

* [KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419，2014 年 9 月

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419，2014 年 9 月

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597，2015 年 9 月
* [KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549，2015 年 3 月
* [KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712，2014 年 8 月
* [KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003，2014 年 2 月  
* [KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721，2013 年 10 月
* [KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534，2013 年 8 月

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
