---
title: "Azure AD Connect 同步：技術概念 | Microsoft Docs"
description: "說明 Azure AD Connect 同步處理的 hello 技術的概念。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Azure AD Connect 同步處理：技術概念
這篇文章是 hello 主題的摘要[了解架構](active-directory-aadconnectsync-technical-concepts.md)。

Azure AD Connect 同步建置在一個穩固的中繼目錄同步處理平台上。
hello 下列各節介紹中繼目錄同步處理的 hello 概念。
建置 MIIS、 ILM，和 FIM，hello Azure Active Directory 同步處理服務提供 hello 下一個平台連線 toodata 來源，資料來源，以及佈建和解除佈建身分識別的 hello 之間同步處理資料。

![技術概念](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

hello 下列各節會提供更多詳細 hello 遵循 hello FIM 同步處理服務的層面：

* 連接器
* 屬性流程
* 連接器空間
* Metaverse
* 佈建

## <a name="connector"></a>連接器
連接器 （之前稱為管理代理程式 (Ma)） 時，會呼叫 hello 程式碼模組所使用的 toocommunicate 與連接的目錄。

這些是執行 Azure AD Connect 同步處理的 hello 電腦上進行安裝。hello 連接器提供 hello 無代理程式的能力 tooconverse 使用遠端系統通訊協定，而不是依賴 hello 部署專用的代理程式。 這表示降低了風險與部署時間，特別是在處理重要的應用程式與系統時。

在上述的 hello 圖片，hello 連接器 hello 連接器空間同義，但包含所有與 hello 外部系統通訊。

hello 連接器負責所有匯入和匯出功能 toohello 系統，以及開發人員不需要 toounderstand 如何使用宣告式佈建 toocustomize 資料轉換時，原生 tooconnect tooeach 系統。

匯入和匯出只發生排程時，允許進一步隔離 hello 系統內發生，因為變更不會自動傳播 toohello 連接的資料來源的變更。 此外，開發人員也可以建立自己的連接器，以連接 toovirtually 任何資料來源。

## <a name="attribute-flow"></a>屬性流程
hello metaverse 是來自相鄰連接器空間所有聯結的身分識別的 hello 合併檢視。 在 hello 圖中，屬性流程描繪以線條傳入和傳出流量的箭頭。 屬性流程是複製或將資料從一個系統 tooanother 轉換 hello 程序，所有屬性流程 （輸入或輸出）。

屬性流程，就會發生 hello 連接器空間和 hello metaverse 之間雙向同步處理 （完整或差異） 的作業排程的 toorun 時。

屬性流程只會在執行這些同步處理時進行。 屬性流動則是在同步化規則中定義。 這些可以是輸入 (ISR hello 如上圖) 或輸出 (OSR 在 hello 如上圖)。

## <a name="connected-system"></a>連接的系統
連接的系統 （也稱為連接的目錄） 正在參照 toohello 遠端系統 Azure AD Connect 同步處理已連接 tooand 讀取和寫入從身分識別資料 tooand。

## <a name="connector-space"></a>連接器空間
每個連接的資料來源被以 hello 物件和屬性在 hello 連接器空間中的篩選子集。
這允許 hello 同步處理服務 toooperate 而 hello 需要 toocontact hello 遠端系統不在本機，hello 物件同步處理時，限制互動 tooimports 並只會匯出。

當 hello 資料來源和 hello 連接器的 hello 能力 tooprovide 變更 （差異匯入） 的清單時，然後 hello 操作效率增加大幅如只能變更自 hello 上次輪詢循環會交換。 hello 連接器空間，以隔離 hello 連接的資料來源自動傳播的要求該 hello 連接器排程匯入和匯出的變更。 此層保障您安心測試、 預覽或確認 hello 下次更新時。

## <a name="metaverse"></a>Metaverse
hello metaverse 是來自相鄰連接器空間所有聯結的身分識別的 hello 合併檢視。

識別連結在一起，並授權單位指派給各種屬性，透過匯入流程對應，hello 中央 metaverse 物件就會開始從多個系統 tooaggregate 資訊。 從這個物件的屬性流程對應，請執行資訊 toooutbound 系統。

當授權系統投射至 hello metaverse 時，會建立物件。 一旦移除所有連線之後，會刪除 hello metaverse 物件。

Hello metaverse 中的物件不能直接編輯。 透過屬性流程，就必須提供 hello 物件中的所有資料。 hello metaverse 會維護持續的連接器，與每個連接器空間。 這些連接器不需要在每次執行每次同步處理進行重新評估。 這表示，Azure AD Connect 同步處理並沒有 toolocate hello 相符的遠端物件每一次。 這可以避免成本高昂的代理程式，通常就是相互關聯的 hello 物件 tooprevent 變更 tooattributes hello 需要。

當探索可能會有預先存在的物件需要 toobe 管理，Azure AD Connect 同步處理使用的程序的新資料來源稱為聯結規則 tooevaluate 潛在候選項目使用哪些 tooestablish 連結。
當建立 hello 連結時，不會再次執行這項評估，而且可能是正常的屬性流程 hello 遠端連接的資料來源與 hello metaverse 之間。

## <a name="provisioning"></a>佈建
當授權來源專案 hello metaverse 新的連接器空間物件至新的物件可由另一個連接器代表下游連接的資料來源中。

這本身就會建立連結，且屬性流程可以雙向進行。

每當規則決定新的連接器空間物件需要 toobe 建立，就稱為佈建。 不過，這項作業只會發生在 hello 連接器空間內，因為它不會延續至 hello 連接的資料來源之前執行匯出。

## <a name="additional-resources"></a>其他資源
* [Azure AD Connect 同步處理：自訂同步處理選項](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
