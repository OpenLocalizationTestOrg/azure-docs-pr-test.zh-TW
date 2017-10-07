---
title: "不同的狀態或狀態，在 BizTalk 服務中允許的 aaaTasks |Microsoft 文件"
description: "hello 動作/允許在 MABS 的不同狀態的作業： 停止、 啟動、 重新啟動、 暫停、 繼續、 刪除、 調整、 設定更新組態和備份"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>哪些可以和無法使用 hello BizTalk 服務狀態

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

根據 hello 的 hello BizTalk 服務的目前狀態，有可以或無法在 hello BizTalk 服務上執行的作業。

例如，您佈建 hello Azure 傳統入口網站中新的 BizTalk 服務。 Hello BizTalk 服務時成功完成，已處於`active`狀態。 Hello 作用中狀態，您可以停止、 暫停，然後刪除 hello BizTalk 服務。 如果停止 hello BizTalk 服務，而且會停止失敗，則 hello BizTalk 服務會 tooa`StopFailed`狀態。 在 hello`StopFailed`狀態時，您可以重新啟動 hello BizTalk 服務。 如果您嘗試的作業，則不允許繼續執行，例如，就會發生下列錯誤 hello:

`Operation not allowed`

## <a name="view-hello-possible-states"></a>檢視 hello 可能的狀態

hello 以下表格列出 hello 作業或可以在 hello BizTalk 服務處於特定狀態時完成的動作。 ✔ 表示允許 hello 作業處於該狀態中。 空白項目表示 hello 操作無法在該狀態中。

| 服務狀態 | Start | 停止 | 重新啟動 | 暫止 | 繼續 | 刪除 | 調整 | 更新 <br/> 組態 | 備份 |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Active |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| 已停用 |  |  |  |  |  | ✔ | |  |  | 
| 暫止 |  |  |  |  | ✔ | ✔ | |  | ✔ |
| 已停止 | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| 服務更新失敗 |  |  |  |  |  | ✔ | |  |  | 
| 停用失敗 |  |  |  |  |  | ✔ | |  |  | 
| 啟用失敗 |  |  |  |  |  | ✔ | |  |  | 
| 啟動失敗 <br/> 停止失敗 <br/> 重新啟動失敗 | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| 暫止失敗 <br/> 繼續失敗|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| 建立失敗 <br/> 還原失敗 |  |  |  |  |  | ✔ | |  |  | 
| 設定更新失敗  |  |  | ✔ |  |  | ✔ | |✔ | |
| 調整失敗 |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>另請參閱
* [建立 BizTalk 服務使用 hello Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [您可以在 BizTalk 服務的 hello 儀表板、 監視器和調整規模索引標籤中執行](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [您會取得在 BizTalk 服務中的 hello Developer、 Basic、 Standard 和 Premium 版本](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [如何 tooback 及還原 BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk 服務中說明的節流](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [擷取 BizTalk 服務的 hello 服務匯流排和存取控制簽發者名稱和簽發者金鑰值](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)

