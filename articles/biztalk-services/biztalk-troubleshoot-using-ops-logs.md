---
title: "aaaTroubleshoot BizTalk 服務使用作業記錄 |Microsoft 文件"
description: "使用作業記錄疑難排解 BizTalk 服務。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>BizTalk 服務：使用作業記錄檔進行疑難排解

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Hello 作業記錄檔有哪些？
作業記錄檔也提供 hello tooview 您的 Azure 服務，包括 BizTalk 服務上執行的作業歷程記錄檔可讓您的 Azure 傳統入口網站的管理服務功能。 這可讓您 tooview 歷程記錄資料相關的 BizTalk 服務訂用帳戶早在 180 天的 toomanagement 作業。

> [!NOTE]
> 在 BizTalk 服務的管理作業，例如 hello 服務啟動時，記錄備份最多，依此類推，只會擷取這項功能。 這類作業會受到追蹤，不論它們是否會執行從 hello Azure 傳統入口網站或使用 hello [BizTalk 服務 REST Api](http://msdn.microsoft.com/library/azure/dn232347.aspx)。 如需使用管理服務進行追蹤的作業完整清單，請參閱[使用 Azure 管理服務進行追蹤的作業](#bizops)。<br/><br/>
> 這不會擷取 hello 記錄檔中的活動相關 tooBizTalk 服務執行階段 （例如訊息處理橋接器等。）。 tooview 這些記錄檔時，使用 hello 從 hello BizTalk 服務入口網站的追蹤檢視。 如需詳細資訊，請參閱[追蹤訊息](http://msdn.microsoft.com/library/azure/hh949805.aspx)。
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>檢視 BizTalk 服務作業記錄檔
1. 在 hello Azure 傳統入口網站，選取**管理服務**，然後選取 hello**作業記錄檔** 索引標籤。
2. 您可以篩選不同的參數，例如訂閱、 日期範圍、 服務類型 (例如 BizTalk Services)、 服務名稱或 hello 作業 （成功、 失敗） 的狀態為基礎的 hello 記錄檔。
3. 選取 hello 核取記號 tooview hello 篩選清單。 hello 下列影像顯示活動相關的 tootestbiztalkservice:![檢視作業記錄檔][ViewLogs] 
4. 進一步了解特定作業，tooview 選取 hello 資料列，然後按一下**詳細資料**hello 底部 hello 工作列中。

## <a name="bizops"></a>使用 Azure 管理服務進行追蹤的作業
hello 下表列出會追蹤使用 hello Azure 管理服務的 hello 作業：

| 作業名稱 | 工作 |
| --- | --- |
| CreateBizTalkService |作業 toocreate 新的 BizTalk 服務 |
| DeleteBizTalkService |作業 toodelete BizTalk 服務 |
| RestartBizTalkService |作業 toorestart BizTalk 服務 |
| StartBizTalkService |作業 toostart BizTalk 服務 |
| StopBizTalkService |作業 toostop BizTalk 服務 |
| DisableBizTalkService |作業 toodisable BizTalk 服務 |
| EnableBizTalkService |作業 tooenable BizTalk 服務 |
| BackupBizTalkService |作業 tooback BizTalk 服務 |
| RestoreBizTalkService |作業 toorestore 從指定的備份 BizTalk 服務 |
| SuspendBizTalkService |作業 toosuspend BizTalk 服務 |
| ResumeBizTalkService |作業 tooresume BizTalk 服務 |
| ScaleBizTalkService |作業 tooscale BizTalk 服務向上或向下 |
| ConfigUpdateBizTalkService |BizTalk 服務作業 tooupdate hello 組態 |
| ServiceUpdateBizTalkService |作業 tooupgrade 或降級 tooa 不同 BizTalk 服務的版本 |
| PurgeBackupBizTalkService |作業 toopurge 備份的 hello 保留期間外 hello BizTalk 服務 |

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

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

