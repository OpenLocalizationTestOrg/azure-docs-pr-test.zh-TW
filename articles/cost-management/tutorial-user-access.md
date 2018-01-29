---
title: "在 Azure 成本管理中指派存取權 | Microsoft Docs"
description: "透過定義實體存取層級的使用者帳戶，指派成本管理資料的存取權。"
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 10/11/2017
ms.topic: tutorial
ms.service: cost-management
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: a42f3b51bf6d888d0d5602887ed317c6164391ef
ms.sourcegitcommit: d03907a25fb7f22bec6a33c9c91b877897e96197
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2017
---
# <a name="assign-access-to-cost-management-data"></a>指派成本管理資料的存取權

成本管理資料的存取權是由使用者或實體管理所提供。 Cloudyn 使用者帳戶可決定「實體」和系統管理功能的存取權。 存取權的類型有兩種：系統管理員和使用者。 除非依照使用者進行修改，否則系統管理員存取權允許使用者無限制使用 Cloudyn 入口網站中的所有功能，包括：使用者管理、收件者清單管理，以及所有實體資料的根實體存取權。 使用者存取權主要可供使用者檢視報告，以及使用其擁有的實體資料存取權來建立報告。

實體用來反映您企業組織的階層式結構。 其可在 Cloudyn 中識別貴組織的部門、事業部和小組。 實體階層可協助您精確地追蹤各實體的支出。

在您註冊 Azure 合約或帳戶後，就會在 Cloudyn 中建立具有系統管理員權限的帳戶，以便您執行本教學課程中的所有步驟。 本教學課程涵蓋成本管理資料 (包括使用者管理與實體管理) 的存取權。 您會了解如何：

> [!div class="checklist"]
> * 建立具有系統管理員存取權的使用者
> * 建立具有使用者存取權的使用者
> * 管理實體



## <a name="create-a-user-with-admin-access"></a>建立具有系統管理員存取權的使用者

雖然您已經有系統管理員存取權，但您組織中的同事也可能需要有系統管理員存取權。 在 Cloudyn 入口網站中，按一下右上角的齒輪符號並選取 [使用者管理]。 按一下 [新增使用者] 以新增使用者。

輸入使用者的相關資訊。 您可以將密碼欄位留空，以便使用者在第一次登入時設定新密碼。 當您選取 [透過電子郵件通知使用者] 時，系統就會透過電子郵件從 Cloudyn 將含有登入資訊的連結傳送給使用者。 選擇允許「使用者管理」的權限，以便使用者建立和修改其他使用者。 「收件者清單管理」可允許使用者編輯收件者清單。

在 [使用者具有系統管理員存取權] 之下，已選取您組織的根實體。 讓根實體保留已選取狀態，然後儲存使用者資訊。 選取根實體，可讓使用者不只擁有樹狀目錄中根實體的系統管理員權限，也擁有其下所有實體的系統管理員權限。  
  ![新增具有系統管理員存取權的使用者](.\media\tutorial-user-access\new-admin-access.png)

## <a name="create-a-user-with-user-access"></a>建立具有使用者存取權的使用者
需要成本管理資料 (如儀表板和報告) 存取權的一般使用者，應該具有使用者存取權才能檢視這些資料。 建立具有使用者存取權的新使用者，類似於您建立具有系統管理員存取權的使用者，但有下列差異：

- 清除 [允許使用者管理]、[允許收件者清單管理]，並清除 [使用者具有系統管理員存取權] 清單中的所有項目。
- 在 [使用者具有使用者存取權] 清單中選取使用者需要存取的實體。
- 您也可以視需要允許系統管理員存取特定實體。

![新增具有使用者存取權的使用者](.\media\tutorial-user-access\new-user-access.png)

若要觀看有關新增使用者的教學課程影片，請看[將使用者新增至 Cloudyn 的 Azure 成本管理](https://youtu.be/Nzn7GLahx30)。

## <a name="create-entities"></a>管理實體

當您定義成本實體階層時，最佳做法是識別您組織的結構。

當您建立樹狀目錄時，請考慮您在想要或需要查看其成本的方式：依照業務單位、成本中心、環境和銷售部門區隔。 Cloudyn 中的實體樹狀目錄因實體繼承而具有彈性。 雲端帳戶的個別訂用帳戶會連結到特定實體。 因此，實體為多租用戶。 您可以使用實體，將特定使用者存取權僅指派給您企業中其所屬的部門。 這麼做可隔離資料，即使橫跨企業的大型部分 (像是分公司)。 此外，資料隔離有助於控管。  

在您向 Cloudyn 註冊 Azure 合約或帳戶後，您的 Azure 資源資料 (包括您訂用帳戶中的使用量、效能、帳單和標籤資料) 便已複製到您的 Cloudyn 帳戶。 不過，您必須手動建立您的實體樹狀目錄。 如果您略過 Azure Resource Manager 註冊，則只能在 Cloudyn 入口網站中取得計費資料和一些資產報告。

在 Cloudyn 入口網站中，按一下右上角的 [設定] 並選取 [雲端帳戶]。 您可從單一實體 (根目錄) 開始，並在根目錄下建置您的實體樹狀目錄。 以下是樹狀目錄完成後的實體階層範例，這可能類似於許多 IT 組織：

![實體樹狀目錄](.\media\tutorial-user-access\entity-tree.png)

按一下 [實體] 旁邊的 [新增實體]。 輸入您想新增之人員或部門的相關資訊。 [全名] 和 [電子郵件] 欄位不必與現有的使用者相符。 如果您想要檢視存取層級清單，請在說明中搜尋「新增實體」。

![新增實體](.\media\tutorial-user-access\add-entity.png)

在完成時 [儲存] 實體。


若要觀看建立成本實體階層的教學課程影片，請參閱[在 Cloudyn 提供的 Azure 成本管理中建立成本實體階層](https://youtu.be/dAd9G7u0FmU)。

如果您是 Azure Enterprise 合約使用者，請看[使用 Cloudyn 的 Azure 成本管理連線至 Azure Resource Manager](https://youtu.be/oCIwvfBB6kk) 中有關將帳戶和訂用帳戶與實體建立關聯的教學課程影片。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立具有系統管理員存取權的使用者
> * 建立具有使用者存取權的使用者
> * 管理實體

前進到下一個教學課程，以了解如何使用歷程記錄資料預測花費。

> [!div class="nextstepaction"]
> [測未來花費](tutorial-forecast-spending.md)
