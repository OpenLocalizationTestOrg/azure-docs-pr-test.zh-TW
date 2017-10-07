---
title: "aaaAzure Active Directory Reporting 常見問題集 |Microsoft 文件"
description: "Azure Active Directory 報告常見問題集。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>Azure Active Directory 報告常見問題集

這篇文章包含有關在 Azure Active Directory 報告集 (faq) 解答 toofrequently。  
如需更多詳細資料，請參閱 [Azure Active Directory 報告](active-directory-reporting-azure-portal.md)。 

**問： 什麼是 hello 的活動記錄 （稽核和登入） 的資料保留在 hello Azure 入口網站？** 

**答：**我們免費的客戶，並藉由切換 tooan Azure AD Premium 1 或 Premium 2 授權，我們會提供 7 天的資料存取，您可以向上 too30 天的資料。 如需有關保留期的更多詳細資料，請參閱 [Azure Active Directory 報告保留原則](active-directory-reporting-retention.md)

--- 

**問： 如何花費時間直到完成工作之後，我可以看見 hello 活動資料？**

**答：**稽核活動記錄檔具有介於 15 分鐘 tooan 小時的延遲。 登入活動記錄檔有延遲，範圍介於 15 分鐘的大部分記錄和 too2 幾個記錄的時數。

---

**問： 我需要的 toobe 全域管理員 toosee hello 活動記錄在 hello Azure 入口網站或透過 hello API tooget 資料？**

**答：**否。 您可以**安全性讀取器**、**安全性管理員**或**全域管理員**toosee 報告資料在 Azure 入口網站或透過 hello API 存取它。

---

**問： 是否可以取得 hello Azure 入口網站透過 Office 365 活動記錄檔資訊？**

**答：**即使 Office 365 活動和 Azure AD 的活動記錄檔共用大量的 hello 目錄資源，如果您想要的完整檢視 hello Office 365 活動記錄檔，您應該移 toohello Office 365 系統管理中心 tooget Office 365 活動記錄檔資訊。

---


**問： 與應用程式開發介面使用 Office 365 活動記錄檔的 tooget 資訊嗎？**

**答：**使用 hello Office 365 管理 Api tooaccess hello [Office 365 活動記錄應用程式開發介面透過](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview)。

---

**問：我可以從 Azure 入口網站下載多少記錄？**

**答：** too120K 記錄從 hello Azure 入口網站，您可以下載。 hello 記錄會依照*最近*，而根據預設，您會收到 hello 最近 120 K 記錄。 

---

**問： 透過 hello 活動 API 可以查詢如何許多記錄？**

**答：** too1 數百萬筆記錄，您可以查詢 (如果您不使用 hello top 運算子，hello 記錄依最新)。 如果您使用 hello"top"運算子，您可以查詢 too500K 記錄。 您可以找到上如何 toouse hello API 此處的範例查詢[這裡](active-directory-reporting-api-getting-started.md)。

---

**問：我要如何取得進階授權？**

**答：**看到[開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)回應 toothis 問題。

---

**問：在取得進階授權之後，我應該多快能看見活動資料？**

**答：**若您已經有免費的授權，活動資料，則您可以看見 hello 相同的資料。 如果您沒有任何資料，則必須花一或兩天的時間。

---

**問：在取得 Azure AD 進階授權之後，我是否會看見上個月的資料？**

**答：**您最近切換 tooa Premium 版本 （包括試用版），您可以一開始查看資料 too7 天。 當資料會累積時，您會看到向上 too30 天。

---

**問： 有處於風險事件的識別身分保護，但我我看不到對應登入 hello 中所有的登入。這是預期行為嗎？**

**答：**是，Identity Protection 會評估所有驗證流程的風險，無論是互動式或非互動式。 不過，所有登入的唯一報表會都顯示只有 hello 互動式登入。

---

**問： 如何可以下載 Azure 入口網站中的 hello 」 使用者標示為進行風險 」 報表？**

**答：** hello 選項 toodownload*使用者加上旗標的風險*報表很快就會加入。

---

**問： 如何知道為什麼登入或使用者已加上旗標 hello Azure 入口網站中有風險？**

**答：** Premium edition 客戶可以進一步了解 hello 基礎 hello 使用者 」 使用者標示為進行風險 」 中按一下，或按一下 hello"風險登入 」 的風險事件。 Free 和 Basic 版客戶會取得 toosee hello 高風險使用者和登入沒有 hello 基礎風險事件資訊。

---

**問： 如何 IP 位址是以 hello 登入和風險的登入報表計算？**

**答：** IP 位址所發出的方式沒有任何明確的連接，IP 位址和該位址為 hello 電腦所在實體之間。 這是比較複雜的因素，例如行動提供者和 Vpn 通常很遠低於 hello 用戶端裝置使用位置為何實際發行從中央集區的 IP 位址。 由於上述 hello，轉換 IP 位址 tooa 實體位置是根據追蹤、 登錄資料、 反向查詢 ups 和其他資訊的最大努力。 

---
