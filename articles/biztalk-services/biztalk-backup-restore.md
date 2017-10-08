---
title: "aaaCreate 和還原 BizTalk 服務中的備份 |Microsoft 文件"
description: "BizTalk 服務包含備份與還原功能。 深入了解如何 toocreate 和還原備份，並決定備份的項目。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk 服務：備份與還原

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk 服務包含備份與還原功能。 本主題描述如何使用 toobackup 和還原 BizTalk 服務 hello Azure 傳統入口網站。

您也可以備份 BizTalk 服務使用 hello [BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584)。 

> [!NOTE]
> 混合式連線無法備份，不論 hello 版本。 您必須重新建立混合式連接。


## <a name="before-you-begin"></a>開始之前
* 備份與還原可能不適用於部分版本。 請參閱「 [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)」(英文)。
* 使用 hello Azure 傳統入口網站，您可以建立隨選備份，或建立排定的備份。 
* 備份內容可以是相同的 BizTalk 服務或 tooa 還原的 toohello 新的 BizTalk 服務。 toorestore hello BizTalk 服務使用相同的名稱，現有的 BizTalk 服務的 hello，必須先刪除的 hello 和 hello 名稱必須可供使用。 刪除 BizTalk 服務之後，可能需要較長的時間比希望 hello 相同名稱 toobe 可用。 如果您無法等候 hello 相同命名 toobe 可用，然後還原 tooa 新的 BizTalk 服務。
* BizTalk 服務可以還原的 toohello 相同版本或更高版本。 不支援還原 BizTalk 服務 tooa、 當 hello 備份，從較低版本。
  
    例如，使用的 hello Basic Edition 可還原備份 toohello Premium Edition。 使用 Premium 版本不能的 hello 的備份還原 toohello Standard Edition。
* hello EDI 控制編號會備份 toomaintain 連續性的 hello 控制編號。 如果訊息處理 hello 上次備份後，還原此備份的內容可能會導致重複的控制編號。
* 如果批次具有作用中的訊息，處理 hello 批次**之前**執行備份。 無論是建立隨選備份或排定備份，都不會儲存批次中的訊息。 
  
    **建立備份時，如果批次中有作用中的訊息，則不會備份這些訊息，且這些訊息將會遺失。**
* 選擇性： Hello BizTalk 服務入口網站，在停止的任何管理作業。

## <a name="create-a-backup"></a>建立備份
您隨時都可以建立備份，完全決由掌控。 此區段會列出 hello 步驟 toocreate 備份使用 hello Azure 傳統入口網站，包括：

[隨選備份](#backupnow)

[排定備份](#backupschedule)

#### <a name="backupnow"></a>隨選備份
1. 在 hello Azure 傳統入口網站，選取  **BizTalk 服務**，，然後選取 hello 想 toobackup BizTalk 服務。
2. 在 hello**儀表板**索引標籤上，選取**Back up** hello hello 頁底端。
3. 輸入備份名稱。 例如，輸入 *myBizTalkService*BU*Date*。
4. 選擇 blob 儲存體帳戶和選取 hello 核取記號 toostart hello 備份。

Hello 備份完成之後，您輸入的 hello 備份名稱的容器會建立 hello 儲存體帳戶中。 此容器包含 BizTalk 服務備份組態。

#### <a name="backupschedule"></a>排定備份
1. 在 hello Azure 傳統入口網站，選取  **BizTalk 服務**，選取 hello BizTalk 服務名稱，tooschedule hello 備份，然後再選取 hello**設定** 索引標籤。
2. 設定 hello**備份狀態**太**自動**。 
3. 選取 hello**儲存體帳戶**toostore hello 備份中，輸入 hello**頻率**toocreate hello 備份和多久 tookeep hello 備份 (**保留天數**):
   
    ![][AutomaticBU]
   
    **注意事項**     
   
   * 在**保留天數**，hello 保留期限必須大於 hello 備份頻率。
   * 選取**永遠保留至少一個備份**，即使它已超出 hello 保留期限。
4. 選取 [ **儲存**]。

已排定的備份工作執行時，它會建立 hello 您輸入的儲存體帳戶中的容器 （toostore 備份資料）。 hello hello 容器名*BizTalk 服務名稱日期時間*。 

如果顯示 hello BizTalk 服務儀表板**失敗**狀態：

![上次排定的備份狀態][BackupStatus] 

hello 連結會開啟 hello toohelp 疑難排解管理服務的作業記錄。 請參閱 [BizTalk 服務：使用作業記錄進行疑難排解](http://go.microsoft.com/fwlink/p/?LinkId=391211)。

## <a name="restore"></a>還原
您可以還原備份，從 Azure 傳統入口網站 hello 或 hello[還原 BizTalk 服務 REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582)。 此區段會列出 hello 步驟 toorestore 使用 hello 傳統入口網站。

#### <a name="before-restoring-a-backup"></a>還原備份之前
* 還原 BizTalk 服務時可以輸入新的追蹤、封存和監視儲存區。
* hello 還原相同 EDI 執行階段資料。 hello EDI 執行階段備份會儲存 hello 控制編號。 還原的 hello 控制編號是從 hello hello 備份時的順序。 如果訊息處理 hello 上次備份後，還原此備份的內容可能會導致重複的控制編號。

#### <a name="restore-a-backup"></a>還原備份
1. 在 hello Azure 傳統入口網站，選取 **新增** > **應用程式服務** > **BizTalk 服務** > **還原**:
   
    ![還原備份][Restore]
2. 在**備份 URL**選取 hello 資料夾圖示，依序展開 存放區 hello BizTalk 服務設定備份的 hello Azure 儲存體帳戶。 展開 hello 容器，然後在 hello 右窗格中，選取 hello 對應備份.txt 檔案。 
   <br/><br/>
   選取 [開啟] 。
3. 在 hello**還原 BizTalk 服務**頁面上，輸入**BizTalk 服務名稱**並確認 hello**網域 URL**， **Edition**，和**區域**的 hello 還原 BizTalk 服務。 **建立新的 SQL 資料庫執行個體**追蹤資料庫的 hello:
   
    ![][RestoreBizTalkService]
   
    選取 hello 下一步 箭號。
4. 確認 hello hello SQL 資料庫名稱，輸入該伺服器 hello 實體伺服器 hello SQL 資料庫建立的位置和使用者名稱/密碼。

    如果您想 tooconfigure hello SQL 資料庫版本、 大小和其他屬性，選取**設定進階資料庫設定**。 

    選取 hello 下一步 箭號。

1. 建立新的儲存體帳戶，或輸入 hello BizTalk 服務現有的儲存體帳戶。
2. 選取 hello 核取記號 toostart hello 還原。

Hello 還原已成功完成之後，新的 BizTalk 服務會列在 hello Azure 傳統入口網站中的 hello BizTalk 服務頁面上的暫止狀態。

### <a name="postrestore"></a>還原備份之後
hello BizTalk 服務系統一定會還原在**Suspended**狀態。 處於此狀態，您可以進行任何組態變更之前 hello 新環境正常運作，包括：

* 如果您建立 BizTalk 服務使用 hello Azure BizTalk 服務 SDK 的應用程式，您可能需要還原的 hello 環境與這些應用程式 toowork tootooupdate hello 存取控制 (ACS) 認證。
* 您還原 BizTalk 服務 tooreplicate 現有的 BizTalk 服務環境。 在此情況下，如果沒有合約 hello 原始 BizTalk 服務入口網站中設定使用 FTP 來源 資料夾中，您可能需要 tooupdate hello 最近還原環境 toouse 不同的來源 FTP 資料夾中的 hello 協議。 否則，可能有兩個不同的協議嘗試 toopull hello 相同的訊息。
* 如果您還原 toohave 多個 BizTalk 服務環境，請確定目標 hello Visual Studio 應用程式、 PowerShell 指令程式、 REST Api 或交易夥伴管理 OM Api 中的 hello 正確環境。
* 它是很好的作法 tooconfigure 自動化上的備份 hello 最近還原 BizTalk 服務的環境。

toostart hello BizTalk 服務在 hello Azure 傳統入口網站，選取 hello 還原 BizTalk 服務，然後選取**繼續**hello 工作列中。 

## <a name="what-gets-backed-up"></a>備份什麼項目
建立備份時，hello 下列項目會備份：

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>備份的項目</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Azure BizTalk 服務入口網站</strong></td>
</tr> 
<tr>
<td>組態和執行階段</td> 
<td>
<ul>
<li>夥伴和設定檔詳細資料</li>
<li>夥伴協議</li>
<li>已部署的自訂組件</li>
<li>已部署的橋接器</li>
<li>憑證</li>
<li>已部署的轉換</li>
<li>管線</li>
<li>建立及儲存於 hello BizTalk 服務入口網站的範本</li>
<li>X12 ST01 和 GS01 對應</li>
<li>控制編號 (EDI)</li>
<li>AS2 訊息 MIC 值</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Azure BizTalk 服務</strong></td>
</tr> 
<tr>
<td>SSL 憑證</td> 
<td>
<ul>
<li>SSL 憑證資料</li>
<li>SSL 憑證密碼</li>
</ul>
</td>
</tr> 
<tr>
<td>BizTalk 服務設定</td> 
<td>
<ul>
<li>調整單位計數</li>
<li>版本</li>
<li>產品版本</li>
<li>區域/資料中心</li>
<li>存取控制服務 (ACS) 命名空間和金鑰</li>
<li>追蹤資料庫連接字串</li>
<li>封存儲存體帳戶連接字串</li>
<li>監視儲存體帳戶連接字串</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>其他項目</strong></td>
</tr> 
<tr>
<td>追蹤資料庫</td> 
<td>建立 hello BizTalk 服務時，會輸入 hello 追蹤資料庫的詳細資訊，包括 hello Azure SQL Database 伺服器和 hello 追蹤資料庫名稱。 hello 追蹤資料庫不會自動備份。
<br/><br/>
<strong>重要</strong><br/>
如果 hello 追蹤資料庫刪除與 hello 復原的資料庫需求，必須存在先前的備份。 如果備份不存在，便無法復原 hello 追蹤資料庫和其資料。 在此情況下，建立新的追蹤資料庫以 hello 相同的資料庫名稱。 建議採用地理複寫。</td>
</tr> 
</table>

## <a name="next"></a>下一步
toocreate Azure BizTalk 服務中太 hello Azure 傳統入口網站中，移至[BizTalk 服務： 佈建使用 Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=302280)。 建立應用程式，請跳過 toostart[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)。

## <a name="see-also"></a>另請參閱
* [備份 BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [從備份還原 BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk 服務：開發人員、基本、標準和高級版本圖表](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk 服務：使用 Azure 傳統入口網站進行佈建](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk 服務：佈建狀態圖](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk 服務：儀表板、監視和調整索引標籤](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk 服務：節流](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk 服務：簽發者名稱和簽發者金鑰](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

