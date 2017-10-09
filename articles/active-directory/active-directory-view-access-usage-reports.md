---
title: "aaaView 存取和使用方式報表 |Microsoft 文件"
description: "說明如何 tooview 存取和使用方式報告 toogain 深入了解 hello 完整性與安全性貴組織的目錄。"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>檢視存取和使用情況報告
*這份文件屬於 hello [Azure Active Directory 報告指南](active-directory-reporting-guide.md)。*

您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。 利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。

Hello Azure 管理入口網站，在報表的分類中 hello 下列方法：

* 異常報表-包含登入事件，我們發現 toobe 異常。 我們的目標是 toomake 您注意這類活動，並讓您 toobe 無法 toomake 判斷事件是否可疑。
* 整合式應用程式報告 – 可供深入了解雲端應用程式在組織中的使用方式。 Azure Active Directory 提供與數千個雲端應用程式的整合。
* 錯誤報表 – 指出佈建帳戶 tooexternal 應用程式時可能發生的錯誤。
* 使用者特定報告 – 顯示特定使用者的裝置/登入活動資料。
* 活動記錄-hello 內所有稽核事件的記錄包含過去 24 小時、 過去 7 天或過去 30 天內，以及群組活動變更、 和密碼重設和註冊活動。

> [!NOTE]
> * 某些進階的異常和資源使用情況報告僅適用於您啟用 [Azure Active Directory Premium](active-directory-get-started-premium.md)時。 進階的報表可協助您改善存取安全性，回應 toopotential 威脅，並取得存取 tooanalytics 裝置存取與應用程式使用量。
> * Azure Active Directory Premium 和 Basic 版本可供位於中國的客戶使用 hello Azure Active Directory 的全球執行個體。 Azure Active Directory Premium 和 Basic 版是目前不支援在中國的 21Vianet 所操作的 hello Microsoft Azure 服務中。 如需詳細資訊，請連絡我們在 hello [Azure Active Directory 論壇](https://feedback.azure.com/forums/169401-azure-active-directory/)。
> 
> 

## <a name="reports"></a>報告
| 報告 | 說明 |
| --- | --- |
| **異常活動報告** | |
| [從不明來源登入](active-directory-reporting-sign-ins-from-unknown-sources.md) |可能表示在嘗試 toosign 不被追蹤。 |
| [在多次失敗後登入](active-directory-reporting-sign-ins-after-multiple-failures.md) |可能表示暴力密碼破解攻擊成功。 |
| [從多個地理區域登入](active-directory-reporting-sign-ins-from-multiple-geographies.md) |可能表示多位使用者所登入 hello 相同帳戶。 |
| [從具有可疑活動的 IP 位址登入](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |可能表示使用者嘗試多次入侵後成功登入。 |
| [從可能受感染的裝置登入](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |可能表示嘗試 toosign 中，從可能受感染的裝置。 |
| [異常的登入活動](active-directory-reporting-irregular-sign-in-activity.md) |可能表示事件異常 toousers' 登入模式。 |
| [具有異常登入活動的使用者](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |指示帳戶可能已受到危害的使用者。 |
| 認證外洩的使用者 |認證外洩的使用者 |
| **活動記錄檔** | |
| 稽核報告 |目錄中的已稽核事件 |
| 密碼重設活動 |提供您組織中所執行之密碼重設的詳細檢視。 |
| 密碼重設註冊活動 |提供您組織中所執行之密碼重設登錄的詳細檢視。 |
| 自助群組活動 |提供活動記錄 tooall 群組自助活動，在您的目錄 |
| **整合式應用程式** | |
| 應用程式使用情況 |針對與您目錄整合的所有 SaaS 應用程式提供使用摘要。 |
| 帳戶佈建活動 |提供嘗試的歷程記錄 tooprovision 帳戶 tooexternal 應用程式。 |
| 密碼變換狀態 |提供 SaaS 應用程式自動密碼變換狀態的詳細概觀。 |
| 帳戶佈建錯誤 |表示影響 toousers' 存取 tooexternal 應用程式。 |
| **版權管理** | |
| RMS 使用量 |提供 Rights Management 使用量的摘要 |
| 最活躍的 RMS 使用者 |列出已存取受 RMS 保護之檔案的前 1000 名有效使用者 |
| RMS 裝置使用量 |列出存取受 RMS 保護的檔案所使用的裝置 |
| 啟用 RMS 的應用程式使用量 |提供啟用 RMS 之應用程式的使用量 |

## <a name="report-editions"></a>報告版本
| 報告 | 免費 | 基本 | 高級 |
| --- | --- | --- | --- |
| **異常活動報告** | | | |
| 從不明來源登入 |✓ |✓  |✓ |
| 在多次失敗後登入 |✓ |✓  |✓ |
| 從多個地理區域登入 |✓ |✓  |✓ |
| 從具有可疑活動的 IP 位址登入 | | |✓ |
| 從可能受感染的裝置登入 | | |✓ |
| 異常的登入活動 | | |✓ |
| 具有異常登入活動的使用者 | | |✓ |
| 認證外洩的使用者 | | |✓ |
| **活動記錄檔** | | | |
| 稽核報告 |✓ |✓  |✓ |
| 密碼重設活動 | | |✓ |
| 密碼重設註冊活動 | | |✓ |
| 自助服務群組活動 | | |✓ |
| **整合式應用程式** | | | |
| 應用程式使用情況 | | |✓ |
| 帳戶佈建活動 |✓ |✓  |✓ |
| 密碼變換狀態 | | |✓ |
| 帳戶佈建錯誤 |✓ |✓  |✓ |
| **版權管理** | | | |
| RMS 使用量 | | |僅 RMS |
| 最活躍的 RMS 使用者 | | |僅 RMS |
| RMS 裝置使用量 | | |僅 RMS |
| 啟用 RMS 的應用程式使用量 | | |僅 RMS |

## <a name="anomalous-activity-reports"></a>異常活動報告
<p>hello 異常登入活動報表可疑活動 tooOffice365、 Azure 管理入口網站、 Azure AD 存取面板、 Sharepoint Online、 Dynamics CRM Online，及其他 Microsoft online services 中的旗標。</p>

<p>所有這些報表，除了 hello 」 多次失敗後的登入 」 的報表，還加上旗標可疑<i>同盟</i>登入 toohello 上述服務，不論 hello 同盟提供者。 </p>

<p>hello 下列報表可用： </p><ul>

<li>[從不明來源登入](active-directory-reporting-sign-ins-from-unknown-sources的一部分。md)的一部分。</li>

<li>[在多次失敗後登入](active-directory-reporting-sign-ins-after-multiple-failures的一部分。md)的一部分。</li>

<li>[從多個地理區域登入](active-directory-reporting-sign-ins-from-multiple-geographies的一部分。md)的一部分。</li>

<li>[從具有可疑活動的 IP 位址登入](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity的一部分。md)的一部分。</li>

<li>[異常的登入活動](active-directory-reporting-irregular-sign-in-activity的一部分。md)的一部分。</li>

<li>[從可能受感染的裝置登入](active-directory-reporting-sign-ins-from-possibly-infected-devices的一部分。md)的一部分。</li>

<li>[具有異常登入活動的使用者](active-directory-reporting-users-with-anomalous-sign-in-activity.md)的一部分。</li>

<li>認證外洩的使用者</li></ul>

## <a name="activity-logs"></a>活動記錄檔
### <a name="audit-report"></a>稽核報告
| 說明 | 報告位置 |
|:--- |:--- |
| 顯示 hello 過去 24 小時、 過去 7 天或過去 30 天內所有稽核事件的記錄。 <br /> 如需詳細資訊，請參閱 [Azure Active Directory 稽核報告事件](active-directory-reporting-audit-events.md) |目錄 > 報告索引標籤 |

![稽核報告](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>密碼重設活動
| 說明 | 報告位置 |
|:--- |:--- |
| 顯示您的組織中發生的所有密碼重設嘗試 |目錄 > 報告索引標籤 |

![密碼重設活動](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>密碼重設註冊活動
| 說明 | 報告位置 |
|:--- |:--- |
| 顯示您的組織中發生的所有密碼重設登錄 |目錄 > 報告索引標籤 |

![密碼重設註冊活動](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>自助服務群組活動
| 說明 | 報告位置 |
|:--- |:--- |
| 在您的目錄中顯示 hello 自助服務受管理群組的所有活動。 |目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤 |

![自助服務群組活動](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>整合式應用程式報告
### <a name="application-usage-summary"></a>應用程式使用情況：摘要
| 說明 | 報告位置 |
|:--- |:--- |
| 當您想 toosee 使用量所有 hello SaaS 應用程式目錄中時，請使用這份報表。 這份報表會根據使用者已按一下 hello hello 存取面板中的應用程式的 hello 次數。 |目錄 > 報告索引標籤 |

這份報表包含登入太*所有*您目錄具有應用程式存取，包括預先整合的 Microsoft 應用程式。

預先整合的 Microsoft 應用程式包括 Office 365、 Sharepoint、 hello Azure 管理入口網站和其他項目。

![應用程式使用情況摘要](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>應用程式使用情況：詳細
| 說明 | 報告位置 |
|:--- |:--- |
| 當您想的 toosee 正在使用多少特定 SaaS 應用程式時，請使用這份報表。 這份報表會根據使用者已按一下 hello hello 存取面板中的應用程式的 hello 次數。 |目錄 > 報告索引標籤 |

### <a name="application-dashboard"></a>應用程式儀表板
| 說明 | 報告位置 |
|:--- |:--- |
| 此報表指出累計登單元 toohello 應用程式中選取的時間間隔內，組織的使用者。 hello 儀表板頁面上的 hello 圖表可協助您識別該應用程式的所有使用量的趨勢。 |目錄 > 應用程式 > 儀表板索引標籤 |

## <a name="error-reports"></a>錯誤報告
### <a name="account-provisioning-errors"></a>帳戶佈建錯誤
| 說明 | 報告位置 |
|:--- |:--- |
| 使用從 SaaS 應用程式 tooAzure Active Directory 的帳戶 hello 同步處理期間發生此 toomonitor 錯誤。 |目錄 > 報告索引標籤 |

![帳戶佈建錯誤](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>特定使用者報告
### <a name="devices"></a>裝置
| 說明 | 報告位置 |
|:--- |:--- |
| 當您想 toosee hello IP 位址和地理位置的特定使用者已使用 tooaccess Azure Active Directory 的裝置時，請使用這份報表。 |目錄 > 使用者 > <i>使用者</i> > 裝置索引標籤 |

### <a name="activity"></a>活動
| 說明 | 報告位置 |
|:--- |:--- |
| 顯示 hello 登入使用者的活動。 hello 報表包含 hello 登入的應用程式、 使用的裝置、 IP 位址和位置等資訊。 我們不會收集使用 Microsoft 帳戶登入的使用者的 hello 歷程記錄。 |目錄 > 使用者 > <i>使用者</i> > 活動索引標籤 |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>登入 hello 使用者活動報表中所含事件
只有某些類型的登入事件會出現在 hello 使用者活動報表。

| 事件類型 | 已包含？ |
| --- | --- |
| 登入 toohello[存取面板](http://myapps.microsoft.com/) |是 |
| 登入 toohello [Azure 管理入口網站](https://manage.windowsazure.com/) |是 |
| 登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com/) |是 |
| 登入 toohello [Office 365 入口網站](http://portal.office.com/) |是 |
| 登入 tooa 原生應用程式，例如 Outlook （請參閱底下的例外狀況） |是 |
| 登入 tooa 同盟/佈建應用程式透過存取面板，例如 Salesforce hello |是 |
| 登入 tooa 密碼為基礎的應用程式透過存取面板，例如 Twitter hello |是 |
| 登入 tooa 自訂商務應用程式已新增 toohello 目錄 |否 (敬請期待) |
| 登入 tooan Azure AD Application Proxy 應用程式已新增 toohello 目錄 |否 (敬請期待) |

> 注意： 這份報表，雜訊 tooreduce hello 數量的登入的 hello [Microsoft Online Services 登入小幫手](http://community.office365.com/en-us/w/sso/534.aspx)不會顯示。
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>如果您懷疑安全性缺口的事情 tooconsider
如果您懷疑可能危害的使用者帳戶，或任何一種可能會導致 tooa 的目錄資料的安全性缺口 hello 雲端中的可疑的使用者活動，您可能會想 tooconsider 一或多個 hello 下列動作：

* 請連絡 hello 使用者 tooverify hello 活動
* 重設 hello 使用者密碼
* [啟用多因素驗證](../multi-factor-authentication/multi-factor-authentication-get-started.md) 以提供額外的安全性

## <a name="view-or-download-a-report"></a>檢視或下載報告
1. 在 hello Azure 傳統入口網站，按一下  **Active Directory**，按一下 hello 貴組織的目錄名稱，然後按一下**報表**。
2. 在 hello 報表頁面上，按一下您想要 tooview hello 報表和 （或) 下載。
   
   > [!NOTE]
   > 如果這是 hello 您已使用 hello 報告功能的 Azure Active Directory 的第一次，您會看到訊息 tooOpt 中。 如果您同意，請按一下 hello 核取記號圖示 toocontinue。
   > 
   > 
3. 按一下 下拉式選單下一步 tooInterval hello，，然後選取其中一個 hello 後應該產生此報表時使用的時間範圍：
   
   * 過去 24 小時
   * 過去 7 天
   * 過去 30 天
4. 按一下 hello 核取記號圖示 toorun hello 報表。
   * 向上 too1000 hello Azure 傳統入口網站中會顯示事件。
5. 如果適用的話，按一下**下載**toodownload hello 報表 tooa 壓縮的檔案以逗號分隔值 (CSV) 格式離線檢視或封存。
   * 向上 too75，000 事件將會包含在 hello 下載檔案。
   * 如需詳細資料，查看 hello [Azure AD 報告 API](active-directory-reporting-api-getting-started.md)。

## <a name="ignore-an-event"></a>忽略事件
如果正在檢視任何異常報告，您可能會注意到您可以忽略顯示在相關報告中的各種事件。 tooignore 事件，只要醒目提示 hello 報表中的 hello 事件，然後按一下**忽略**。 hello**忽略**按鈕將會永久移除 hello 報表中的 hello 反白顯示的事件，只用於授權全域管理員。

## <a name="automatic-email-notifications"></a>自動電子郵件通知
如需有關 Azure AD 的報告通知詳細資訊，請參閱 [Azure Active Directory 報告通知](active-directory-reporting-notifications.md)。

## <a name="whats-next"></a>後續步驟
* [開始使用 Azure Active Directory Premium](active-directory-get-started-premium.md)
* [新增公司品牌 tooyour 登入及存取面板頁面](active-directory-add-company-branding.md)

