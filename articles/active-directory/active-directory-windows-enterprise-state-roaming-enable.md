---
title: "Azure Active Directory 中的企業狀態漫遊 aaaEnable |Microsoft 文件"
description: "Windows 裝置中企業狀態漫遊設定的常見問題集。 企業狀態漫遊使用者提供一致的方式透過他們的 Windows 裝置，並減少 hello 設定新裝置所需的時間。"
services: active-directory
keywords: "企業狀態漫遊，windows 雲端如何 tooenable 企業狀態漫遊"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>在 Azure Active Directory 中啟用企業狀態漫遊
企業狀態漫遊是可用 tooany 組織與 Premium Azure Active Directory (Azure AD) 的訂用帳戶。 如需有關如何 tooget Azure AD 訂用帳戶，請參閱 hello [Azure AD 產品頁面](https://azure.microsoft.com/services/active-directory)。

當您啟用企業狀態漫遊時，您的組織將會自動獲得可用、 使用限制的訂用帳戶 tooAzure Rights Management 的授權。 此免費訂閱，而且有限的 tooencrypting 解密企業設定及同步處理方式是 hello 企業狀態漫遊服務; 的應用程式資料您必須擁有 Azure Rights Management 付費訂用帳戶 toouse hello 完整功能。

取得 Azure AD Premium 訂用帳戶之後, 請依照企業狀態漫遊這些步驟 tooenable:

1. 登入 toohello Azure 傳統入口網站。
2. Hello 左側選取**ACTIVE DIRECTORY**，然後選取您想要的企業狀態漫遊 tooenable hello 目錄。
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. 移 toohello**設定**hello 最上層顯示 索引標籤。
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. 捲動 hello 頁面，然後選取**使用者可以同步設定及企業應用程式資料**，然後按一下**儲存**。
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Windows 10 裝置 tooroam 設定的 hello 企業狀態漫遊的服務，必須使用 Azure AD 身分識別驗證 hello 裝置。 對於會聯結的 tooAzure AD 的裝置，hello 使用者的主要登入是 hello Azure AD 身分識別，因此不不需要任何額外的組態。 針對使用傳統的內部部署 Active Directory 中，裝置 hello IT 系統管理員必須[連接 hello 已加入網域裝置 tooAzure AD 以進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)。

## <a name="sync-data-storage"></a>同步處理資料儲存體
企業狀態漫遊資料裝載於一或多個[Azure 區域](https://azure.microsoft.com/regions/)最符合設定 hello Azure Active Directory 執行個體中的 hello 國家 （地區） 值。 企業狀態漫遊的資料是根據三個主要地理區域來分割︰北美洲、EMEA 和 APAC。 企業狀態漫遊 hello 租用戶的資料在本機位於與 hello 地理區域，並不會跨區域複寫。  例如，客戶 EMEA 國家/地區的國家/地區值組 tooone 像 「 法國 」 或 「 幾內亞 」 將具有其資料裝載於其中一個或的 hello 內歐洲 Azure 區域。  他們國家/地區中設定值 North America 國家/地區的 Azure AD tooone 像 「 美國 」 或 「 加拿大 」 將具有其資料的客戶裝載於一或多個 hello hello 美國內的 Azure 區域。  亞太地區 （apac） 國家/地區的 Azure AD tooone 中設定它們國家/地區的值，像是 「 澳洲"或"紐西蘭 」 將會有其資料的客戶裝載於一或多個 hello 亞洲內的 Azure 區域。  南美洲的國家/地區和南極洲資料將裝載於美國 hello 內的一或多個 Azure 區域。  hello 國家/地區值設定為 hello Azure AD 目錄的建立程序的一部分，而且不能做修改。 

如果您需要資料儲存體位置的詳細資料，請向 [Azure 支援](https://azure.microsoft.com/support/options/)提出票證。

## <a name="manage-enterprise-state-roaming"></a>管理企業狀態漫遊
Azure AD 全域管理員可以啟用和停用 hello Azure 傳統入口網站中的 企業狀態漫遊。
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

全域系統管理員可以限制設定同步處理 toospecific 安全性群組。

全域管理員的 hello Active Directory 執行個體中選取特定的使用者也可以檢視每個使用者裝置同步處理狀態報表**使用者**清單，並按一下**裝置** 索引標籤，然後選取檢視**裝置同步設定與企業應用程式資料**。
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>資料保留
透過企業狀態漫遊的資料同步處理 tooAzure 會無限期保留，除非手動刪除作業會執行，或有問題的 hello 資料決定的 toobe 過時。 

**明確刪除：**為 Azure 系統管理員刪除使用者或目錄或系統管理員明確要求的資料是 toobe 刪除時，會刪除 hello 資料。

* **使用者刪除**: hello 漫遊資料的使用者帳戶在 Azure AD 中刪除使用者時，將會標示為刪除，並會刪除 too180 後 90 天之間。 
* **目錄刪除**：在 Azure AD 中刪除整個目錄是即時作業。 所有 hello 設定相關都聯的資料具有該目錄將會標示為刪除，並刪除 too180 後 90 天之間。 
* **在要求刪除**: hello 系統管理員如果 hello Azure AD 系統管理員想 toomanually 刪除特定使用者的資料或設定資料，可以提出票證[Azure 支援](https://azure.microsoft.com/support/)。 

**過時的資料刪除**： 尚未一年 （"hello 保留週期 」） 會被視為過時，而且可從 Azure 刪除被存取的資料。 hello 保留期限是主體 toochange，但不是會超過 90 天。 hello 過時資料可能是一組特定的 Windows/應用程式的設定或使用者的所有設定。 例如：

* 如果沒有任何裝置存取特定的設定集合 （例如，應用程式從 hello 裝置移除，或設定群組，例如 「 主題 」 已停用的所有使用者的裝置），則該集合會過時 hello 的保留週期後，可能是刪除。 
* 如果使用者已關閉其所有裝置上的設定同步處理，然後無 hello 設定資料將可存取，而且所有 hello 設定資料，該使用者將會變成過時，而且可能 hello 保留期限後刪除。 
* 如果 hello Azure AD 目錄系統管理員會關閉企業狀態漫遊 hello 整個目錄，然後所有使用者的目錄將會停止同步處理設定，並針對所有使用者的所有設定資料將會變成過時，而且可能 hello 保留期限後刪除。 

**刪除資料復原**: hello 資料保留原則是不可設定。 一旦 hello 資料都已永久刪除，將無法復原它。 不過，請務必 toonote hello 設定資料，將只會從 Azure hello 使用者裝置刪除。 如果任何裝置稍後重新連線 toohello 企業狀態漫遊服務，hello 設定會一次同步處理並儲存在 Azure 中。

## <a name="related-topics"></a>相關主題
* [企業狀態漫遊概觀](active-directory-windows-enterprise-state-roaming-overview.md)
* [設定和資料漫遊常見問題集](active-directory-windows-enterprise-state-roaming-faqs.md)
* [設定同步處理的群組原則和 MDM 設定](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 漫遊設定參考](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [疑難排解](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
