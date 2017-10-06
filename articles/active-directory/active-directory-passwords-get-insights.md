---
title: "深入了解：Azure AD 密碼管理報告 | Microsoft Docs"
description: "本文說明 toouse 報告 tooget 深入了解您組織中的密碼管理作業的方式。"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 1472b51d-53f4-4b0f-b1be-57f6fa88fa65
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 90e0b8e621cdfe3e3a2f15df7b98115008855500
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-operational-insights-with-password-management-reports"></a>Tooget operational insights 使用密碼管理報告的方式
> [!IMPORTANT]
> **您來到此處是因為有登入問題嗎？** 若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account)。
>
>

本章節描述如何使用 Azure Active Directory 的密碼管理報告的 tooview 使用者如何使用密碼重設和變更您的組織中。

* [**密碼管理報告概觀**](#overview-of-password-management-reports)
* [**Tooview 密碼管理報告的方式，在 hello 新版 Azure 入口網站**](#how-to-view-password-management-reports)
 * [目錄角色允許 tooread 報表](#directory-roles-allowed-to-read-reports)
* [**自助密碼管理活動中的型別 hello 新版 Azure 入口網站**](#self-service-password-management-activity-types)
 * [封鎖自助式密碼重設](#activity-type-blocked-from-self-service-password-reset)
 * [變更密碼 (自助式)](#activity-type-change-password-self-service)
 * [重設密碼 (由系統管理員)](#activity-type-reset-password-by-admin)
 * [重設密碼 (自助式)](#activity-type-reset-password-self-service)
 * [自助式密碼重設流程活動進度](#activity-type-self-serve-password-reset-flow-activity-progress)
 * [解除鎖定使用者帳戶 (自助式)](#activity-type-unlock-user-account-self-service)
 * [使用者已註冊自助式密碼重設](#activity-type-user-registered-for-self-service-password-reset)
* [**如何從 tooretrieve 密碼管理事件 hello Azure AD 報告和事件 API**](#how-to-retrieve-password-management-events-from-the-azure-ad-reports-and-events-api)
 * [報告 API 資料擷取限制](#reporting-api-data-retrieval-limitations)
* [**如何 toodownload 密碼重設註冊事件使用 PowerShell**](#how-to-download-password-reset-registration-events-quickly-with-powershell)
* [**Tooview 密碼管理報告的方式，在 hello 傳統入口網站**](#how-to-view-password-management-reports-in-the-classic-portal)
* [**檢視密碼重設註冊活動與 hello 傳統的入口網站中您組織中**](#view-password-reset-registration-activity-in-the-classic-portal)
* [**檢視密碼重設 hello 傳統入口網站中您組織中的活動**](#view-password-reset-activity-in-the-classic-portal)


## <a name="overview-of-password-management-reports"></a>密碼管理報告概觀
一旦您部署了密碼重設，其中一個 hello 最常見的下一個步驟是的 toosee 如何正在使用您組織中。  例如，您可能想 tooget 深入解析成使用者如何註冊密碼重設，或多少密碼重設已在 hello 過去幾天中完成。  以下是一些 hello 常見問題的解答，您應該可以存在於 hello 的 hello 密碼管理報表與 tooanswer [Azure 管理入口網站](https://manage.windowsazure.com)今天：

* 有多少人已註冊密碼重設？
* 有誰已註冊密碼重設？
* 什麼資料是人員註冊？
* 很多人重設其密碼，在 hello 過去 7 天？
* 什麼是 hello 最常見方法的使用者或系統管理員使用 tooreset 他們的密碼？
* 什麼是常見發出使用者或系統管理員面對嘗試 toouse 密碼重設嗎？
* 哪些系統管理員經常重設自己的密碼？
* 密碼重設時是否有任何可疑的活動？

## <a name="how-tooview-password-management-reports"></a>如何 tooview 密碼管理報告
在新的 hello [Azure 入口網站](https://portal.azure.com)體驗，我們已改進的方式 tooview 密碼重設和密碼重設註冊活動。  遵循下一個 toofind hello 密碼重設密碼的 hello 步驟重設註冊事件，在新的 hello [Azure 入口網站](https://portal.azure.com):

1. 瀏覽過[**portal.azure.com**](https://portal.azure.com)
2. 按一下 hello**更多服務**hello 主要 Azure 入口網站左導覽功能表
3. 搜尋**Azure Active Directory**在 hello 服務清單，並加以選取
4. 按一下**使用者和群組**hello Azure Active Directory 瀏覽功能表中
5. 按一下 hello**稽核記錄檔**hello 使用者和群組瀏覽功能表中的 [瀏覽項目。 這會顯示您針對所有 hello 使用者 hello 稽核事件所發生的所有目錄中。 您可以篩選此檢視 toosee 所有 hello 密碼相關的事件，以及。
6. 此檢視 tooonly hello 密碼管理相關的 toofilter 事件，按一下 hello**篩選**在 hello hello 刀鋒視窗頂端的按鈕。
7. 從 hello**篩選**功能表中，選取 hello**類別**下拉式清單中，並將它變更 toohello**自助密碼管理**類別目錄類型。
8. （選擇性） 進一步篩選 hello 清單中的選擇 hello 特定**活動**您感興趣
### <a name="direct-link-toouser-audit-blade"></a>直接連結 tooUser 稽核刀鋒視窗
如果您已登入 tooyour 入口網站，以下是直接連結 toohello 使用者稽核刀鋒視窗，您可以看到這些事件：

* [移 toouser 管理直接稽核檢視](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Audit)

### <a name="directory-roles-allowed-tooread-reports"></a>目錄角色允許 tooread 報表
目前，hello 下列目錄角色可能會讀取 hello 傳統 Azure 入口網站中的 Azure AD 密碼管理報告：

* 全域管理員

之前所能 tooread 這些報表，hello 公司的全域管理員必須有選擇用於瀏覽 hello 至少一次報告] 索引標籤或稽核記錄檔擷取代表 hello 組織這個資料 toobe。 在此之前，不會為您的組織收集資料。

目錄角色與他們的可以詳細資訊，請參閱的 tooread[指派 Azure Active Directory 中的系統管理員角色](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-assign-admin-roles)。

## <a name="self-service-password-management-activity-types"></a>自助式密碼管理活動類型
下列活動類型的 hello 會出現在 hello**自助密碼管理**稽核事件類別目錄。  以下是每一項的描述。

* [**自助式密碼重設封鎖**](#activity-type-blocked-from-self-service-password-reset) -表示使用者嘗試 tooreset 密碼，來使用特定的閘道，或驗證的電話號碼 5 個以上的 24 小時內的總時間。
* [**變更密碼 （自助）** ](#activity-type-change-password-self-service) -指出使用者執行自願性質，或強制 (到期 tooexpiry) 密碼變更。
* [**重設密碼 （由系統管理員）** ](#activity-type-reset-password-by-admin) -表示系統管理員執行密碼重設代表 hello Azure 入口網站的使用者。
* [**重設密碼 （自助）** ](#activity-type-reset-password-self-service) -表示使用者已成功重設其密碼從 hello [Azure AD 密碼重設入口網站](https://passwordreset.microsoftonline.com)。
* [**自助密碼重設流程活動進度**](#activity-type-self-serve-password-reset-flow-activity-progress) -表示每個使用者就會繼續進行，（例如，傳遞特定的密碼重設驗證閘道） 的特定步驟一部分 hello 密碼重設程序。
* [**解除鎖定使用者帳戶 （自助）** ](#activity-type-unlock-user-account-self-service) -表示使用者已成功解除其 Active Directory 帳戶鎖定而不重設其密碼從 hello [Azure AD 密碼重設入口網站](https://passwordreset.microsoftonline.com)使用 hello [AD 帳戶解除鎖定，而不重設](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password)功能。
* [**使用者註冊自助密碼重設**](#activity-type-user-registered-for-self-service-password-reset) -表示使用者已註冊所有必要的 hello 資訊 toobe 無法 tooreset hello 目前指定的租用戶密碼重設原則根據他們的密碼。

### <a name="activity-type-blocked-from-self-service-password-reset"></a>活動類型︰封鎖自助式密碼重設
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 表示使用者嘗試 tooreset 密碼，請使用特定的閘道，或驗證電話號碼 5 個以上的 24 小時內的總時間。
* **活動執行者**-已執行其他節流的 hello 使用者重設作業。 可能是使用者或系統管理員。
* **活動的目標**-已執行其他節流的 hello 使用者重設作業。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_-表示使用者已節流處理來自執行任何額外的重設，嘗試任何其他驗證方法，或驗證未來 24 小時內的任何其他的電話號碼 hello。
* **活動狀態失敗原因** - 不適用

### <a name="activity-type-change-password-self-service"></a>活動類型：變更密碼 (自助式)
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 指出使用者執行自願性質，或強制 (到期 tooexpiry) 密碼變更。
* **活動執行者**-hello 使用者變更其密碼。 可能是使用者或系統管理員。
* **活動的目標**-hello 使用者變更其密碼。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_ - 指出使用者已成功變更密碼
 * _失敗_-表示使用者無法 toochange 他或她的密碼。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。
* **活動狀態失敗原因** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello 使用者選取已自動禁用到期 tooMicrosoft 的禁用密碼偵測功能尋找 toobe 太常見或特別是弱式密碼。

### <a name="activity-type-reset-password-by-admin"></a>活動類型：重設密碼 (由系統管理員)
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 表示系統管理員執行密碼重設代表 hello Azure 入口網站的使用者。
* **活動執行者**-hello 系統管理員執行 hello 密碼重設代表另一個使用者或系統管理員。 必須是全域管理員、密碼管理員、使用者管理員或技術服務管理員。
* **活動的目標**-hello 使用者重設其密碼。 可能是使用者或不同的系統管理員。
* **允許的活動狀態**
 * _成功_ - 指出系統管理員已成功重設使用者的密碼
 * _失敗_-表示系統管理員無法 toochange 使用者的密碼。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。

### <a name="activity-type-reset-password-self-service"></a>活動類型：重設密碼 (自助式)
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 表示使用者已成功重設其密碼從 hello [Azure AD 密碼重設入口網站](https://passwordreset.microsoftonline.com)。
* **活動執行者**-hello 使用者重設其密碼。 可能是使用者或系統管理員。
* **活動的目標**-hello 使用者重設其密碼。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_ - 指出使用者已成功重設密碼
 * _失敗_-表示使用者無法 tooreset 他或她自己的密碼。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。
* **活動狀態失敗原因** -
 * _FuzzyPolicyViolationInvalidPassword_ -hello 系統管理員選取已自動禁用到期 tooMicrosoft 的禁用密碼偵測功能尋找 toobe 太常見或特別是弱式密碼。

### <a name="activity-type-self-serve-password-reset-flow-activity-progress"></a>活動類型：自助式密碼重設流程活動進度
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 指出每個特定步驟，使用者就會繼續進行 （例如，傳遞特定的密碼重設驗證閘道） 一部分 hello 密碼重設程序。
* **活動執行者**-執行 hello 密碼一部分的 hello 使用者重設流程。 可能是使用者或系統管理員。
* **活動的目標**-執行 hello 密碼一部分的 hello 使用者重設流程。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_-表示使用者已成功完成特定步驟的 hello 密碼重設流程。
 * _失敗_-表示特定步驟的 hello 密碼重設失敗的流程。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。
* **允許的活動狀態原因**
 * 請參閱下表中的[所有允許的重設活動狀態原因](#allowed-values-for-details-column)

### <a name="activity-type-unlock-user-account-self-service"></a>活動類型：解除鎖定使用者帳戶 (自助式)
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 表示使用者已成功解除其 Active Directory 帳戶鎖定而不重設其密碼從 hello [Azure AD 密碼重設入口網站](https://passwordreset.microsoftonline.com)使用 hello [AD不重設的帳戶解除鎖定](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-passwords-customize#allow-users-to-unlock-accounts-without-resetting-their-password)功能。
* **活動執行者**-hello 使用者解除鎖定其帳戶，而不重設其密碼。 可能是使用者或系統管理員。
* **活動的目標**-hello 使用者解除鎖定其帳戶，而不重設其密碼。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_ - 指出使用者已成功解除鎖定帳戶
 * _失敗_-表示使用者無法 toounlock 他或她的帳戶。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。

### <a name="activity-type-user-registered-for-self-service-password-reset"></a>活動類型︰使用者已註冊自助式密碼重設
hello 下列清單說明此活動，在詳細資料：

* **活動描述**– 表示使用者已註冊所有必要的 hello 資訊 toobe 無法 tooreset hello 目前指定的租用戶密碼重設原則根據他們的密碼。
* **活動執行者**-hello 使用者註冊密碼重設。 可能是使用者或系統管理員。
* **活動的目標**-hello 使用者註冊密碼重設。 可能是使用者或系統管理員。
* **允許的活動狀態**
 * _成功_-指出已成功註冊密碼重設根據 hello 目前原則的使用者。
 * _失敗_-指出使用者無法 tooregister 密碼重設。 按一下 hello 資料列可讓您 toosee hello**活動狀態原因**類別 toolearn 更多關於 hello 失敗發生的原因。 請注意-這不表示使用者已無法 tooreset 他或她自己的密碼，只是他或她未完成 hello 註冊程序。 如果正確 （例如電話號碼，不會驗證），其帳戶中沒有未驗證的資料即使它們未驗證這個電話號碼，他們仍然可以使用它 tooreset 他們的密碼。 如需詳細資訊，請參閱[當使用者註冊時會發生什麼事？](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-learn-more#what-happens-when-a-user-registers)

## <a name="how-tooretrieve-password-management-events-from-hello-azure-ad-reports-and-events-api"></a>如何從 tooretrieve 密碼管理事件 hello Azure AD 報告和事件 API
從 2015 年 8 月開始 hello Azure AD 報告和事件 API 現在支援擷取所有 hello hello 密碼重設和密碼重設註冊報表中包含的資訊。 藉由使用此應用程式開發介面，您可以下載個別的密碼重設和密碼重設註冊事件整合以 hello 報表您 choce 的技術。

### <a name="how-tooget-started-with-hello-reporting-api"></a>如何 tooget 入門 hello 報告 API
tooaccess 這項資料，您將需要 toowrite 小型應用程式或指令碼 tooretrieve 從我們的伺服器。 [了解如何 tooget 入門 hello Azure AD 報告 API](active-directory-reporting-api-getting-started.md)。

工作的指令碼之後，您會接下來想 tooexamine hello 密碼重設和註冊事件，您可以擷取 toomeet 您的案例。

* [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)： 密碼重設事件會列出可用的 hello 資料行
* [SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent)： 密碼重設註冊事件會列出可用的 hello 資料行

### <a name="reporting-api-data-retrieval-limitations"></a>報告 API 資料擷取限制
目前，hello Azure AD 報告和事件 API 會擷取向上太**75000 個別事件**的 hello [SsprActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent)和[SsprRegistrationActivityEvent](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprRegistrationActivityEvent)類型跨越 hello**過去 30 天內**。

如果您需要 tooretrieve，或儲存超過此視窗的資料，則建議您保存在外部資料庫，並使用 hello API tooquery hello 差異所導致。 最佳作法是 toobegin 擷取這項資料，當您啟動您的密碼重設您的組織在註冊程序、 將它保存在外部，然後再從這個點 tootrack hello 差異的向前復原。

## <a name="how-toodownload-password-reset-registration-events-quickly-with-powershell"></a>如何 toodownload 密碼重設註冊事件使用 PowerShell
此外 toousing hello Azure AD 報告和事件 API 直接，您也可以使用下列 PowerShell 指令碼 toorecent 註冊事件 hello 目錄中。 這會很有用，如果您想 toosee 最近，已註冊，或想要如預期般發生 tooensure 密碼重設首度發行。

* [Azure AD SSPR 註冊活動 PowerShell 指令碼](https://gallery.technet.microsoft.com/scriptcenter/azure-ad-self-service-e31b8aee)

## <a name="how-tooview-password-management-reports-in-hello-classic-portal"></a>Tooview 密碼管理報告的方式，在 hello 傳統入口網站
toofind hello 密碼管理報表，請遵循下列 hello 步驟：

1. 按一下 hello **Active Directory** hello 中的擴充功能[Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 從出現在 hello 入口網站中的 hello 清單中選取您的目錄。
3. 按一下 hello**報表**] 索引標籤。
4. 查看 [hello**活動記錄**> 一節。
5. 選取任一 hello**密碼重設活動**報表或 hello**密碼重設註冊活動**報表。

## <a name="view-password-reset-registration-activity-in-hello-classic-portal"></a>檢視密碼重設註冊活動與 hello 傳統的入口網站中
hello 密碼重設註冊活動報告會顯示所有密碼重都設您的組織中發生的註冊。  任何使用者都已順利登錄驗證資訊在 hello 密碼重設註冊入口網站，將會顯示這份報表中的密碼重設註冊 ([http://aka.ms/ssprsetup](http://aka.ms/ssprsetup))。

* **時間範圍上限**：30 天
* **資料列數目上限**：75,000
* **可下載**：是，透過 CSV 檔案

### <a name="description-of-report-columns"></a>報告資料行說明
hello 下列清單說明每個 hello 報表中的資料行詳細資料：

* **使用者**– hello 使用者嘗試進行密碼重設註冊作業。
* **角色**– hello hello 目錄中的 hello 使用者角色。
* **日期和時間**– hello 的日期和時間 hello 嘗試。
* **註冊資料**– 密碼過程中提供的驗證資料 hello 使用者重設註冊。

### <a name="description-of-report-values"></a>報告值說明
hello 下表描述 hello 允許每個資料行不同的值：

| 資料欄 | 允許的值及其意義 |
| --- | --- |
| 已註冊資料 |**替代電子郵件**– 使用者使用替代電子郵件或驗證電子郵件 tooauthenticate<p><p>**辦公室電話**– 使用辦公室電話 tooauthenticate 使用者。<p>**行動電話**-使用者使用行動電話或驗證電話 tooauthenticate<p>**安全性問題**– 使用者使用安全性問題 tooauthenticate<p>**Hello 上方 （例如替代電子郵件 + 行動電話） 的任何組合**– 2 閘道原則指定顯示哪兩種方式 hello tooauthentication 用使用者時，就會發生密碼重設要求。 |

## <a name="view-password-reset-activity-in-hello-classic-portal"></a>檢視密碼重設 hello 傳統入口網站中的活動
此報告會顯示您的組織中發生的所有密碼重設嘗試。

* **時間範圍上限**：30 天
* **資料列數目上限**：75,000
* **可下載**：是，透過 CSV 檔案

### <a name="description-of-report-columns"></a>報告資料行說明
hello 下列清單說明每個 hello 報表中的資料行詳細資料：

1. **使用者**– hello 使用者嘗試進行密碼重設作業 （根據 hello hello 使用者到達 tooreset 密碼時提供的使用者識別碼欄位）。
2. **角色**– hello hello 目錄中的 hello 使用者角色。
3. **日期和時間**– hello 的日期和時間 hello 嘗試。
4. **方法使用**– 哪種驗證方法 hello 使用者使用此重設作業。
5. **結果**– hello 最終結果 hello 密碼重設作業。
6. **詳細資料**– hello 的為什麼 hello 密碼重設的詳細資料，產生 hello 值一樣。  也包含您可能需要 tooresolve 未預期的錯誤的任何安全防護步驟。

### <a name="description-of-report-values"></a>報告值說明
hello 下表描述 hello 允許每個資料行不同的值：

| 資料欄 | 允許的值及其意義 |
| --- | --- |
| 使用方法 |**替代電子郵件**– 使用者使用替代電子郵件或驗證電子郵件 tooauthenticate<p>**辦公室電話**– 使用辦公室電話 tooauthenticate 使用者。<p>**行動電話**– 使用者使用行動電話或驗證電話 tooauthenticate<p>**安全性問題**– 使用者使用安全性問題 tooauthenticate<p>**Hello 上方 （例如替代電子郵件 + 行動電話） 的任何組合**– 2 閘道原則指定顯示哪兩種方式 hello tooauthentication 用使用者時，就會發生密碼重設要求。 |
| 結果 |**已放棄** – 使用者開始重設密碼，但是又中途停止而未完成<p>**封鎖**– 使用者的帳戶已予以防止的 toouse 密碼重設到期 tooattempting toouse hello 密碼重設頁面或單一密碼重設閘道太多次 24 小時<p>**取消**– 使用者已開始密碼重設，但按 hello 取消] 5d; 按鈕 toocancel hello 工作階段中途透過 <p>**連絡系統管理員**– 使用者在他無法解決的工作階段期間發生了問題，因此 hello 使用者已按下 hello 「 連絡您的系統管理員 」 連結而未完成 hello 密碼重設流程<p>**無法**– 使用者不能 tooreset 密碼，可能因為 hello 使用者無法設定的 toouse hello 功能 （例如沒有授權、 缺少驗證資訊、 受管理的密碼由內部部署但回寫為關閉）。<p>**成功** – 密碼重設成功。 |
| 詳細資料 |請參閱下表 |

### <a name="allowed-values-for-details-column"></a>允許的詳細資料資料行的值
以下是使用 hello 密碼重設活動報表時，您可能預期的結果型別 hello 清單：

| 詳細資料 | 結果類型 |
| --- | --- |
| 使用者在完成 hello 電子郵件驗證選項之後放棄 |Abandoned |
| 使用者在完成 hello 行動電話 SMS 驗證選項之後放棄 |Abandoned |
| 使用者在完成 hello 行動電話語音通話驗證選項之後放棄 |Abandoned |
| 使用者在完成 hello 辦公室語音通話驗證選項之後放棄 |Abandoned |
| 使用者在完成 hello 安全性問題選項後放棄。 |Abandoned |
| 在輸入其使用者識別碼之後使用者已放棄 |Abandoned |
| 使用者在開始 hello 電子郵件驗證選項之後放棄 |Abandoned |
| 使用者在開始 hello 行動電話 SMS 驗證選項之後放棄 |Abandoned |
| 使用者在開始 hello 行動電話語音通話驗證選項之後放棄 |Abandoned |
| 使用者在開始 hello 辦公室語音通話驗證選項之後放棄 |Abandoned |
| 使用者在開始 hello 安全性問題選項後放棄。 |Abandoned |
| 選取新密碼之前使用者已放棄 |Abandoned |
| 選取新密碼之際使用者已放棄 |Abandoned |
| 使用者輸入太多無效的 SMS 驗證碼，因此封鎖 24 小時 |Blocked |
| 使用者嘗試行動電話語音驗證太多次，因此封鎖 24 小時 |Blocked |
| 使用者嘗試辦公室電話語音驗證太多次，因此封鎖 24 小時 |Blocked |
| 使用者因嘗試太多次 tooanswer 安全性問題而被封鎖 24 小時 |Blocked |
| 使用者因嘗試太多次 tooverify 電話號碼而被封鎖 24 小時 |Blocked |
| 使用者在傳遞所需的 hello 的驗證方法前取消 |Cancelled |
| 在提交新密碼之前使用者已取消 |Cancelled |
| 使用者在嘗試 hello 電子郵件驗證選項之後連絡管理員 |Contacted admin |
| 使用者在嘗試 hello 行動電話 SMS 驗證選項之後連絡管理員 |Contacted admin |
| 使用者在嘗試 hello 行動電話語音通話驗證選項之後連絡管理員 |Contacted admin |
| 使用者在嘗試 hello 辦公室語音通話驗證選項之後連絡管理員 |Contacted admin |
| 使用者在嘗試 hello 安全性問題驗證選項之後連絡管理員 |Contacted admin |
| 這位使用者未啟用密碼重設。 啟用密碼重設下 hello] 索引標籤 tooresolve 進行此設定 |Failed |
| 使用者沒有授權。 您可以加入授權 toohello 使用者 tooresolve |Failed |
| 使用者嘗試從裝置 tooreset 未啟用 cookie |Failed |
| 使用者的帳戶已定義驗證方法不足。 新增驗證資訊 tooresolve |Failed |
| 使用者的密碼是在內部部署進行管理。 這啟用密碼回寫 tooresolve |Failed |
| 我們無法取得您的內部部署密碼重設服務。 請檢查您的同步處理電腦的事件記錄檔 |Failed |
| 我們發現重設 hello 使用者在內部部署密碼時發生的問題。 請檢查您的同步處理電腦的事件記錄檔 |Failed |
| 此使用者不是 hello 密碼重設使用者群組的成員。 加入此使用者 toothat 群組 tooresolve。 |Failed |
| 已針對此租用戶完全停用密碼重設。 請參閱[這裡](http://aka.ms/ssprtroubleshoot)tooresolve 這。 |Failed |
| 使用者成功重設密碼 |Succeeded |

## <a name="next-steps"></a>後續步驟
以下是 hello 的 Azure AD 密碼重設的文件頁面連結 tooall:

* **您來到此處是因為有登入問題嗎？** 若是如此， [以下是如何變更和重設密碼的說明](active-directory-passwords-update-your-own-password.md#reset-or-unlock-my-password-for-a-work-or-school-account)。
* [**它的運作方式**](active-directory-passwords-how-it-works.md) -了解 hello 六個不同的元件 hello 服務，以及每個未
* [**使用者入門**](active-directory-passwords-getting-started.md) -了解如何 tooallow 使用者 tooreset 及變更其雲端或內部部署密碼
* [**自訂**](active-directory-passwords-customize.md) -了解 toocustomize hello 外觀和風格和行為的 hello 服務 tooyour 組織的需求
* [**最佳做法**](active-directory-passwords-best-practices.md) -了解 tooquickly 部署，並有效地管理您組織中的密碼
* [**常見問題集**](active-directory-passwords-faq.md) -取得解答 toofrequently 常見問題
* [**疑難排解**](active-directory-passwords-troubleshoot.md) -了解 tooquickly hello 服務問題的疑難排解
* [**進一步了解**](active-directory-passwords-learn-more.md) -請深度進入 hello hello 服務的運作方式的技術詳細資料
