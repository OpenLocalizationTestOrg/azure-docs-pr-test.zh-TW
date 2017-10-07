---
title: "Azure AD Connect Synchronization Service Manager 作業 | Microsoft Docs"
description: "了解 Azure AD Connect 同步處理服務管理員 hello 的 hello 作業 索引標籤。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>使用 hello 同步處理服務管理員作業 索引標籤

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

hello 作業 索引標籤會顯示 hello hello 最新的作業結果。 此索引標籤是索引鍵 toounderstand 和疑難排解問題。

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>了解 hello hello 作業 索引標籤中顯示的資訊
hello 上半部會顯示所有執行中依時間先後順序。 根據預設，hello 作業記錄會保留資訊 hello 過去七天，但是可以變更此設定，以 hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)。 您想 toolook 任何不會顯示成功狀態的執行。 您可以變更 hello hello 標頭，即可排序。

hello**狀態**資料行是 hello 最重要的資訊並顯示 hello 執行最嚴重的問題。 以下是依照優先順序 tooinvestigate hello 最常見狀態的簡短摘要 (其中 * 表示幾個可能的錯誤字串)。

| 狀態 | 註解 |
| --- | --- |
| stopped-* |執行 hello 無法完成。 例如，如果 hello 遠端系統已關閉，且無法聯繫。 |
| stopped-error-limit |有 5,000 個以上的錯誤。 hello 執行自動已停止，因為 toohello 大量的錯誤。 |
| completed-\*-errors |hello 執行已完成，但有錯誤 (少於 5000)，應予調查。 |
| completed-\*-warnings |hello 執行完成，但某些資料不是處於 hello 預期狀態。 如果您遇到錯誤，則此訊息通常只是一個徵狀。 在您解決錯誤之前，不應該調查警告。 |
| 成功 |沒有問題。 |

當您選取一個資料列時，hello 底部更新 tooshow hello 詳細資料，執行。 toohello 最左側的 hello 底部，您可能必須清單指出**步驟 #**。 如果您的樹系中有多個網域，而每個網域都以一個步驟來代表，則只會顯示此清單。 hello 網域名稱可以找到 hello 標題底下**分割**。 在下**同步處理統計資料**，您可以找到 hello 數的變更，已處理的詳細資訊。 您可以按一下 hello 連結 tooget hello 變更物件的清單。 如果您有物件發生錯誤，這些會顯示於 [同步處理錯誤] 下方。

如需詳細資訊，請參閱[針對未同步的物件進行疑難排解](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>後續步驟
深入了解 hello [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)組態。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
