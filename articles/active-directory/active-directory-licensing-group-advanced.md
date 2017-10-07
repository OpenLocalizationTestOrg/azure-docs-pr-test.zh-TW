---
title: "以群組為基礎來授權其他案例的 Active Directory aaaAzure |Microsoft 文件"
description: "Azure Active Directory 群組型授權的更多案例"
services: active-directory
keywords: "Azure AD 授權"
documentationcenter: 
author: curtand
manager: femila
editor: piotrci
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/02/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 782b7c9aa1c062a55c1241d69af673466f7a849c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-limitations-and-known-issues-using-groups-toomanage-licensing-in-azure-active-directory"></a>案例、 限制和使用 Azure Active Directory 中的群組 toomanage 授權的已知的問題

使用下列資訊和範例 toogain 進一步了解 Azure Active Directory (Azure AD) 以群組為基礎授權的 hello。

## <a name="usage-location"></a>使用位置

並非所有位置都可使用某些 Microsoft 服務。 Hello 管理員 tooa 使用者可以指派授權之前，已 toospecify hello**使用位置**hello 使用者屬性。 在[hello Azure 入口網站](https://portal.azure.com)，您可以指定在**使用者** &gt; **設定檔** &gt; **設定**。

取得群組的授權指派，指定使用位置沒有任何使用者將會繼承 hello hello 目錄位置。 如果您有多個位置中的使用者，請確定 tooreflect 正確使用者物件中新增並授權使用者 toogroups 之前。

> [!NOTE]
> 群組授權指派永遠不會修改使用者現有的使用位置值。 我們建議您一律將使用位置做為您的使用者建立流程的一部分 （例如透過 AAD Connect 組態）-可確保的授權指派的 hello 結果一定是正確的且使用者不會收到服務不的位置中的 Azure AD 中允許的。

## <a name="use-group-based-licensing-with-dynamic-groups"></a>對動態群組使用群組型授權

您可以對任何安全性群組使用群組型授權，這表示可與 Azure AD 動態群組結合。 加入對使用者物件屬性 tooautomatically 執行規則的動態群組，並從群組移除使用者。

例如，您可以建立動態群組想 tooassign toousers 某些產品集。 每個群組會擴展其屬性，新增使用者的規則，且每個群組是您想讓 tooreceive hello 分派的授權。 可以指派 hello 屬性在內部部署以及與 Azure AD 同步處理，或者您可以管理直接在 hello 雲端中的 hello 屬性。

授權就會加入 toohello 群組後不久指派 toohello 使用者。 Hello 屬性變更時，hello 使用者離開 hello 群組，並移除 hello 授權。

### <a name="example"></a>範例

請考慮在內部部署身分識別管理解決方案，決定哪些使用者應該可以存取 tooMicrosoft web 服務的 hello 範例。 它會使用**extensionAttribute1** toostore 的字串值 hello 使用者應該具有代表 hello 授權。 Azure AD Connect 會將它與 Azure AD 同步。

使用者可能需要其中一個授權，也可能需要兩個授權。 以下是的範例，在其中您所發佈 Office 365 企業版 E5 和企業行動力 + 安全性 (EMS) 授權 toousers 群組中：

#### <a name="office-365-enterprise-e5-base-services"></a>Office 365 企業版 E5︰基本服務

![Office 365 企業版 E5 基本服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/o365-e5-base-services.png)

#### <a name="enterprise-mobility--security-licensed-users"></a>Enterprise Mobility + Security︰授權的使用者

![Enterprise Mobility + Security 授權的使用者螢幕擷取畫面](media/active-directory-licensing-group-advanced/o365-e5-licensed-users.png)

此範例中，修改一位使用者以及設定其 extensionAttribute1 toohello 值`EMS;E5_baseservices;`如果您想 hello 使用者 toohave 兩個授權。 您可以在內部部署做此修改。 Hello 之後變更與 hello 雲端同步、 hello 使用者會自動加入 tooboth 群組及指派授權。

![顯示如何 tooset hello extensionAttribute1 使用者的螢幕擷取畫面](media/active-directory-licensing-group-advanced/user-set-extensionAttribute1.png)

> [!WARNING]
> 修改現有群組的成員資格規則時請小心。 當變更規則、 hello hello 群組成員資格將會重新評估和不再符合使用者 hello 新規則將會移除 （仍需符合 hello 新規則的使用者將不會影響在此程序）。 那些使用者就能在 hello 程序中無法使用服務，或在某些情況下，可能會導致資料遺失期間移除其授權。

> 如果您有大型的動態群組，視授權指派，請考慮驗證較小的測試群組上進行重大變更，再將它們套用 toohello 主要群組。

## <a name="multiple-groups-and-multiple-licenses"></a>多個群組和多個授權

使用者可以是多個具有授權之群組的成員。 以下是一些事情 tooconsider:

- 多個授權 hello 相同的產品可以重疊，而且它們會讓所有啟用服務正在套用的 toohello 使用者。 hello 下列範例顯示兩個授權群組： *E3 基本服務*包含 hello foundation 服務 toodeploy 第一次，tooall 使用者。 和*E3 擴充服務*包含其他服務 （Sway 和規劃） toodeploy 只有 toosome 的使用者。 在此範例中，hello 使用者加入 tooboth 群組：

  ![已啟用服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/view-enabled-services.png)

  如此一來，hello 使用者有 7 個 hello 12 服務在 hello 產品啟用，同時使用這項產品只能有一個授權。

- 選取 hello *E3*授權顯示更多詳細資料，包括哪些群組會造成 hello 使用者啟用何種服務 toobe 的資訊。

  ![依群組啟用服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/view-enabled-service-by-group.png)

## <a name="direct-licenses-coexist-with-group-licenses"></a>直接授權與群組授權共存

當使用者從群組繼承授權時，無法直接移除，或修改該 hello 使用者內容中的授權指派。 變更 hello 群組中必須進行，然後再傳播 tooall 使用者。

它，直接在加法 toohello toohello 使用者繼承授權 tooassign 但是 hello 相同的產品授權。 您可以啟用其他服務從 hello 產品，只針對一個使用者，而不會影響其他使用者。

可以移除直接指派的授權，而不會影響繼承的授權。 請考慮 hello，使用者會繼承有 Office 365 Enterprise E3 的授權群組。

1. Hello 使用者一開始，只會從 hello 繼承 hello 授權*E3 基本服務*群組，讓您的四個的服務方案，如所示：

  ![E3 群組啟用的服務的螢幕擷取畫面](media/active-directory-licensing-group-advanced/e3-group-enabled-services.png)

2. 您可以選取**指派**toodirectly E3 授權 toohello 將使用者指派。 在此情況下，您將的 toodisable Yammer 企業以外的所有服務計都劃：

  ![如何的螢幕擷取畫面 tooassign 授權直接 tooa 使用者](media/active-directory-licensing-group-advanced/assign-license-to-user.png)

3. 如此一來，hello 使用者仍會使用一個 hello E3 產品的授權。 但 hello 直接指派可讓 hello Yammer 企業服務只會為該使用者。 您可以看到哪些服務為啟用 hello 與 hello 直接指派的群組成員資格：

  ![繼承和直接指派的螢幕擷取畫面](media/active-directory-licensing-group-advanced/direct-vs-inherited-assignment.png)

4. 當您使用直接指派時，允許下列作業的 hello:

  - Yammer 企業可以關閉 hello 使用者物件上直接。 hello**開/關**切換 hello 圖中的已啟用這項服務，但不要 toohello 其他服務切換。 因為在 hello 使用者上直接啟用 hello 服務時，您可以進行修改。
  - 其他服務可以直接將授權指派給 hello 的一部分，啟用。
  - hello**移除**按鈕可以使用的 tooremove hello 直接授權的 hello 使用者。 您可以看到 hello 使用者現在僅有 hello 繼承的群組授權，而且 hello 原始服務保持啟用：

    ![顯示如何 tooremove 直接指派螢幕擷取畫面](media/active-directory-licensing-group-advanced/remove-direct-license.png)

## <a name="managing-new-services-added-tooproducts"></a>管理新的服務加入 tooproducts
當 Microsoft 將新的服務 tooa 產品時，將會啟用預設會在您已指派的所有群組 toowhich hello 產品授權。 在您的租用戶會訂閱的 toonotifications 產品變更的相關的使用者都會收到電子郵件，事先 hello 服務即將新增功能的相關通知。

身為管理員，您可以檢閱 hello 變更影響的所有群組，並採取動作，例如停用每個群組中的 hello 新服務。 例如，如果您建立的群組只要以用於部署的特定服務為目標，您可以返回這些群組，並確定已停用所有新增的服務。

此程序可能如下所示：

1. 您一開始指派 hello *Office 365 企業版 E5*產品 tooseveral 群組。 其中一個群組，稱為*O365 E5-僅適用於 Exchange*已設計的 tooenable 只有 hello *Exchange Online (計劃 2)*服務為其成員。

2. 通知收到 hello 的 E5 將以新的服務-擴充產品的 Microsoft *Microsoft 資料流*。 在您的租用戶可以使用 hello 服務時，您可以執行下列 hello:

3. 移 toohello [ **Azure Active Directory > 授權 > 所有產品**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products)刀鋒視窗，然後選取*Office 365 企業版 E5*，然後選取**授權群組** tooview 該產品的所有群組的清單。

4. 按一下您想 tooreview hello 群組 (在此情況下， *O365 E5-僅適用於 Exchange*)。 這會開啟 hello**授權** 索引標籤。按一下 hello E5 授權會開啟刀鋒視窗中列出所有已啟用的服務。
> [!NOTE]
> hello *Microsoft 資料流*服務已自動新增並啟用在此群組中，在加法 toohello *Exchange Online*服務：

  ![新服務的螢幕擷取畫面加入 tooa 群組授權](media/active-directory-licensing-group-advanced/manage-new-services.png)

5. 如果您想要 toodisable hello 新服務在此群組中的，按一下 hello**開/關**切換 下一步 toohello 服務，然後按一下 hello**儲存**按鈕 tooconfirm hello 變更。 Azure AD 將會立即處理 hello 群組 tooapply hello 變更; 中的所有使用者新增任何使用者 toohello 群組將沒有 hello *Microsoft 資料流*啟用服務。

  > [!NOTE]
  > 使用者可能仍有某些其他授權指派 （另一個群組的成員，或直接授權指派） 透過啟用 hello 服務。

6. 如有需要請執行的 hello 指派相同的步驟，使用這項產品的其他群組。

## <a name="use-powershell-toosee-who-has-inherited-and-direct-licenses"></a>使用 PowerShell toosee 繼承權限，並直接授權
如果使用者有直接指派或繼承自群組的授權，您可以使用 PowerShell 指令碼 toocheck。

1. 執行 hello `connect-msolservice` cmdlet tooauthenticate 並連接 tooyour 租用戶。

2. `Get-MsolAccountSku`可以是使用的 toodiscover hello 租用戶中的所有已佈建的產品授權。

  ![Hello Get-msolaccountsku cmdlet 的螢幕擷取畫面](media/active-directory-licensing-group-advanced/get-msolaccountsku-cmdlet.png)

3. 使用 hello *AccountSkuId* hello 的授權，您有興趣使用中的值[這個 PowerShell 指令碼](./active-directory-licensing-ps-examples.md#check-if-user-license-is-assigned-directly-or-inherited-from-a-group)。 這會產生具有 hello 資訊 hello 授權如何指派此授權的使用者清單。

## <a name="use-audit-logs-toomonitor-group-based-licensing-activity"></a>使用稽核記錄 toomonitor 群組為基礎的授權活動

您可以使用[Azure AD 稽核記錄檔](./active-directory-reporting-activity-audit-logs.md#audit-logs)toosee toogroup 授權，包括相關的所有活動：
- 哪些人變更了群組的授權
- 當 hello 系統已開始處理群組授權變更，以及當它完成
- 哪些授權變更 tooa 使用者群組的授權指派的結果。

>[!NOTE]
> 在 hello Azure Active Directory 區段的 hello 入口網站中的大部分刀鋒視窗上使用稽核記錄檔。 根據您在其中存取它們，篩選可能會預先套用的 tooonly hello 刀鋒視窗的顯示活動相關 toohello 內容。 如果您沒有看到預期的 hello 結果，請檢查[篩選選項的 hello](./active-directory-reporting-activity-audit-logs.md#filtering-audit-logs)或存取進行篩選的 hello 稽核記錄檔下[ **Azure Active Directory > 活動 > 稽核記錄檔**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit).

### <a name="find-out-who-modified-a-group-license"></a>了解哪些人修改了群組授權

1. 設定 hello**活動**太篩選*組群組授權*按一下**套用**。
2. hello 結果包含授權要設定或修改群組的所有的案例。
>[!TIP]
> 您也可以輸入 hello hello 群組名稱在 hello*目標*篩選 tooscope hello 結果。

3. 按一下 hello 清單檢視 toosee hello 詳細資料中的項目，變更的內容。 在下*Modified 屬性*列出 hello 授權指派的舊的和新值。

下列範例顯示最近的群組授權變更，並提供詳細資料：

![群組授權變更的螢幕擷取畫面](media/active-directory-licensing-group-advanced/audit-group-license-change.png)

### <a name="find-out-when-group-changes-started-and-finished-processing"></a>了解群組變更何時開始和完成處理

當授權變更群組時，Azure AD 將會開始套用 hello 變更 tooall 使用者。

1. 群組可讓您開始處理，當 toosee 設定 hello**活動**太篩選*開始套用群組的基礎授權 toousers*。 請注意該 hello 執行者 hello 作業*Microsoft Azure AD 以群組為基礎的授權*-系統帳戶，是使用的 tooexecute 所有群組授權變更。
>[!TIP]
> 按一下項目在 hello 清單 toosee hello *Modified 屬性*欄位-它會顯示已挑選要處理的 hello 授權變更。 如果您進行多個變更 tooa 群組，而且您不確定哪一個已處理，這非常有用。

2. 同樣地，toosee 群組完成處理時，使用 hello 篩選值*結束套用群組的基礎授權 toousers*。
>[!TIP]
> 在此情況下，hello *Modified 屬性*欄位包含 hello 結果的摘要-這是有用的 tooquickly 檢查，如果發生任何錯誤處理。 範例輸出：
> ```
Modified Properties
...
Name : Result
Old Value : []
New Value : [Users successfully assigned licenses: 6, Users for whom license assignment failed: 0.];
> ```

3. toosee hello 完成記錄檔以取得如何群組處理的時間、 所有使用者變更，包括設定 hello 下列篩選：
  - **啟動者 (執行者)**：「Microsoft Azure AD 群組型授權」
  - **日期範圍** (選用)：特定群組開始和完成處理時間的自訂範圍

此範例輸出顯示 hello 開始處理，所有產生的使用者變更與 hello 完成的處理。

![群組授權變更的螢幕擷取畫面](media/active-directory-licensing-group-advanced/audit-group-processing-log.png)

>[!TIP]
> 按一下項目相關太*變更使用者的授權*會顯示授權套用變更 tooeach 個別使用者的詳細資料。

## <a name="limitations-and-known-issues"></a>限制與已知問題

如果您使用以群組為基礎的授權，它是個不錯的主意 toofamiliarize 自己具有 hello 遵循的限制與已知的問題清單。

- 群組型授權目前不支援包含其他群組的群組 (巢狀群組)。 如果您套用授權 tooa 巢狀的群組時，只有 hello 使用者立即回應的第一層級群組的成員 hello 擁有 hello 授權套用。

- hello 功能僅使用安全性群組。 目前不支援 office 群組，而且您不會無法 toouse hello 授權指派程序中。

- hello [Office 365 系統管理入口網站](https://portal.office.com )目前不支援以群組為基礎的授權。 如果使用者會繼承自群組的授權，本授權條款會顯示在 hello Office 管理入口網站中為一般使用者授權。 如果您嘗試的授權，或嘗試 tooremove hello 授權 toomodify，hello 入口網站會傳回錯誤訊息。 無法直接修改使用者繼承的群組授權。

- 當使用者從群組中移除，並失去 hello 授權時，hello 從該授權 (例如 SharePoint Online) 的服務方案設定 tooa **Suspended**狀態。 hello 服務方案未設定 tooa 最終，停用狀態。 此預防措施可避免系統管理員在群組成員資格管理時犯錯，而意外移除使用者資料。

- 當指派或修改大型群組 (例如 100,000 個使用者) 的授權時，可能會影響效能。 具體來說，hello 磁碟區的 Azure AD 自動化所產生的變更可能效能產生負面影響 hello 的 Azure AD 之間的目錄同步作業和在內部部署系統。

- 授權管理自動化不自動反應 tooall hello 環境中的變更類型。 例如，您可能已用盡授權，導致某些使用者 toobe 處於錯誤狀態。 總 hello 可用基座計數 toofree，您可以從其他使用者移除部分直接指派的授權。 不過，hello 系統不會自動回應 toothis 變更，以及修正該錯誤狀態中的使用者。

  做為因應措施 toothese 類型的限制，您可以移 toohello**群組**刀鋒視窗，在 Azure AD 中，按一下 **重新處理**。 此命令會處理該群組中的所有使用者，並解析 hello 錯誤狀態，如果可能的話。

- 群組為基礎的授權不會記錄錯誤時無法指派授權 tooa 使用者因為 tooa 重複 proxy 位址設定 Exchange Online。在授權指派期間略過這類使用者。 如需有關如何 tooidentify 和解決這個問題，請參閱[本節](./active-directory-licensing-group-problem-resolution-azure-portal.md#license-assignment-fails-silently-for-a-user-due-to-duplicate-proxy-addresses-in-exchange-online)。

## <a name="next-steps"></a>後續步驟

toolearn 有關透過群組為基礎授權的授權管理的其他案例的詳細資訊，請參閱：

* [什麼是 Azure Active Directory 中以群組為基礎的授權？](active-directory-licensing-whatis-azure-portal.md)
* [Azure Active Directory 中指派的授權 tooa 群組](active-directory-licensing-group-assignment-azure-portal.md)
* [識別及解決 Azure Active Directory 中群組的授權問題](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [如何 toomigrate 個別授權 toogroup 型授權 Azure Active Directory 中的使用者](active-directory-licensing-group-migration-azure-portal.md)
