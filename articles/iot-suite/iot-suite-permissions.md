---
title: "aaaAzure IoT 套件與 Azure Active Directory |Microsoft 文件"
description: "描述 Azure IoT 套件如何使用 Azure Active Directory toomanage 權限。"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Hello azureiotsuite.com 網站的權限

## <a name="what-happens-when-you-sign-in"></a>當您登入時會發生什麼事？

hello 第一次登入在[azureiotsuite.com][lnk-azureiotsuite]，hello 站台會決定 hello 權限等級，您根據擁有 hello 目前選取的 Azure Active Directory (AAD) 租用戶與 Azure訂用帳戶。

1. 首先，toopopulate hello 清單中看到的租用戶下一步 tooyour 使用者名稱，hello 站台會找出從 Azure 隸屬於哪一個 AAD 租用戶。 目前，hello 站台只能取得一個租用戶的使用者權杖一次。 因此，當您切換使用 hello 右上角中的 hello 下拉式清單中的租用戶，hello 站台記錄您 toothat 租用戶 tooobtain hello 語彙基元中針對該租用戶。

2. 接下來，hello 站台會找出從 Azure 選取租用戶的您擁有 hello 與相關聯的訂用帳戶。 當您建立新的預先設定的方案，您會看到 hello 可用的訂用帳戶。

3. 最後，hello 網站擷取 hello 訂用帳戶中的所有 hello 資源，資源群組會標記為預先設定的解決方案，並於其中填入 hello hello 首頁上的磚。

hello 下列各節說明 hello 角色控制存取 toohello 預先設定的解決方案。

## <a name="aad-roles"></a>AAD 角色

hello AAD 角色控制 hello 能力預先設定的佈建解決方案，並在預先設定的解決方案中管理使用者。

您可以在[在 Azure AD 中指派系統管理員角色][lnk-aad-admin]中的 AAD 找到有關使用者和系統管理員角色的詳細資訊。 hello 目前文件著重於 hello**全域管理員**和 hello**使用者**目錄角色所使用的 hello 預先設定的解決方案。

### <a name="global-administrator"></a>全域管理員

每個 AAD 租用戶可以有很多全域系統管理員：

* 當您建立 AAD 租用戶時，您會由該租用戶的預設 hello 全域管理員。
* hello 全域管理員可以佈建的預先設定的解決方案，而且會指派**Admin** hello 其 AAD 租用戶內的應用程式角色。
* 如果另一位使用者在 hello 相同 AAD 租用戶建立的應用程式、 hello 預設角色授與 toohello 全域系統管理員是**ReadOnly**。
* 全域管理員可以指派使用 hello 應用程式的使用者 tooroles [Azure 入口網站][lnk-portal]。

### <a name="domain-user"></a>網域使用者

每一個 AAD 租用戶可以有很多網域使用者：

* 網域使用者可以佈建的預先設定的解決方案，透過 hello [azureiotsuite.com] [ lnk-azureiotsuite]站台。 根據預設，hello 網域使用者被授與 hello **Admin** hello 中的角色佈建應用程式。
* 網域使用者可以建立應用程式使用 hello build.cmd 指令碼在 hello [azure iot-遠端-監視][lnk-rm-github-repo]， [azure iot-預測-維護][ lnk-pm-github-repo]，或[azure-iot-連線-原廠][ lnk-cf-github-repo]儲存機制。 不過，hello 預設角色授與 toohello 網域使用者是**ReadOnly**，因為網域使用者沒有權限 tooassign 角色。
* 如果 hello AAD 租用戶中的另一位使用者建立的應用程式，hello 網域使用者指派 hello **ReadOnly**依預設，該應用程式角色。
* 網域使用者無法指派給角色給應用程式。因此，即使應用程式使用者佈建應用程式，網域使用者也無法針對應用程式的使用者新增使用者或角色。

### <a name="guest-user"></a>來賓使用者

每一個 AAD 租用戶可以有很多來賓使用者。 Guest 使用者 hello AAD 租用戶中有一組有限的權限。 如此一來，guest 使用者，無法佈建 hello AAD 租用戶中的預先設定的解決方案。

如需有關使用者和角色在 AAD 中的詳細資訊，請參閱 hello 下列資源：

* [在 Azure AD 中建立使用者][lnk-create-edit-users]
* [指派使用者 tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Azure 訂用帳戶管理員角色

hello Azure 系統管理員角色來控制 hello 能力 toomap 的 Azure 訂用帳戶 tooan AD 租用戶。

進一步了解 hello 文件中的 hello Azure 系統管理員角色[如何 tooadd 或變更 Azure 共同管理員、 服務管理員及帳戶管理員][lnk-admin-roles]。

## <a name="application-roles"></a>應用程式角色

hello 應用程式角色控制存取 toodevices 預先設定方案中。

在已佈建的應用程式中有兩個定義的角色和一個隱含角色：

* **系統管理員：**具有完整控制權 tooadd，管理、 移除裝置，以及修改設定。
* **唯讀：**可以檢視裝置、規則、動作、作業和遙測。

您可以找到 hello 權限指派中 hello tooeach 角色[RolePermissions.cs] [ lnk-resource-cs]原始程式檔。

### <a name="changing-application-roles-for-a-user"></a>變更使用者的應用程式角色

您可以使用下列程序 toomake 使用者部署 Active Directory 系統管理員的您預先設定的方案中的 hello。

您必須是使用者 AAD 全域管理員 toochange 角色：

1. 移 toohello [Azure 入口網站][lnk-portal]。
2. 選取 **Azure Active Directory**。
3. 請確定您使用您選擇的 hello 目錄上 azureiotsuite.com 您佈建您的方案時。 如果您有多個訂用帳戶相關聯的目錄，您可以切換如果您按一下您在 hello 的右上方 hello 入口網站的帳戶名稱。
4. 依序按一下 [企業應用程式] 和 [所有應用程式]。
4. 顯示具有**任何**狀態的**所有應用程式**。 然後搜尋具有預先設定解決方案名稱的應用程式。
5. 按一下 hello 符合預先設定的方案名稱 hello 應用程式名稱。
6. 按一下 [使用者和群組]。
7. 選取您想要 tooswitch 角色 hello 使用者。
8. 按一下**指派**和選取 hello 角色 (例如**Admin**) 您想要 tooassign toohello 使用者，按一下 hello 核取記號。

## <a name="faq"></a>常見問題集

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>我的服務系統管理員，我希望我的訂閱與特定的 AAD 租用戶之間 toochange hello 目錄對應。 如何完成這項工作？

1. 移 toohello [Azure 傳統入口網站][lnk-classic-portal]，按一下 **設定**hello 上 hello 左手邊服務清單中。
2. 選取您想要到 toochange hello 目錄對應的 hello 訂用帳戶。
3. 按一下 [編輯目錄] 。
4. 選取 hello**目錄**希望 toouse hello 下拉式清單中的。 按一下 hello 正向箭號。
5. 確認 hello 目錄對應，以及受影響的共同管理員。 如果您要從另一個目錄中移動，則會移除 hello 原始目錄中的 hello 共同管理員。

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>我是網域使用者/成員在 hello AAD 租用戶上，而且我已建立預先設定的解決方案。 如何獲得我的應用程式的角色？

您在 hello AAD 的全域管理員租用戶，然後將指派角色 toousers 自行要求全域管理員 toomake。 或者，請詢問全域管理員 tooassign 您直接的角色。 如果您想要 toochange hello AAD 租用戶已部署至您預先設定的方案，請參閱 hello 下一個問題。

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>我要如何切換 hello 指派給我的遠端監視的預先設定的解決方案和應用程式的 AAD 租用戶？

您可以從 <https://github.com/Azure/azure-iot-remote-monitoring> 執行雲端部署，並利用新建立的 AAD 租用戶重新部署。 因為您是根據預設，當您建立 AAD 租用戶的全域系統管理員權限 tooadd 使用者也可以 toothose 使用者指派角色。

1. 建立 AAD 目錄中 hello [Azure 入口網站][lnk-portal]。
2. 跳過<https://github.com/Azure/azure-iot-remote-monitoring>。
3. 執行 `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (例如，`build.cmd cloud debug myRMSolution`)
4. 出現提示時，設定 hello **tenantid** toobe 您新建立的租用戶，而不是您先前的租用戶。

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>我想 toochange 服務管理員或共同管理員，當使用 organisational 的帳戶登入

請參閱 hello 技術支援文件[變更服務管理員和共同管理員時的 organisational 帳戶登入時][lnk-service-admins]。

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>為什麼出現以下錯誤？ 「 您的帳戶沒有 hello 適當的權限 toocreate 方案。 請洽詢您的帳戶管理員或嘗試使用不同的帳戶。」

查看下列指導方針的圖表 hello:

![][img-flowchart]

> [!NOTE]
> 如果您繼續 toosee hello 錯誤驗證之後您 hello AAD 租用戶的全域系統管理員和共同管理員 hello 訂用帳戶，具有您的帳戶管理員移除 hello 使用者，並重新指派這個順序的必要權限。 首先，新增 hello 使用者的全域管理員身分，然後將使用者新增為 hello Azure 訂用帳戶的共同管理員。 如果問題持續發生，請連絡[說明與支援][lnk-help-support]。

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>當我有 Azure 訂用帳戶時為何會出現此錯誤？ 「 Azure 訂用帳戶是必要的 toocreate 預先設定的解決方案。 只需要幾分鐘的時間，您就可以建立免費試用帳戶。」

如果您不確定您擁有 Azure 訂用帳戶，驗證 hello 租用戶訂用帳戶的對應，並確認 [hello] 下拉式清單中選取 hello 正確租用戶。 如果已驗證 hello 所需的租用戶是正確，請遵循上述圖表中的 hello，而且驗證 hello 對應您的訂閱，且此 AAD 租用戶。

## <a name="next-steps"></a>後續步驟
toocontinue 深入了解 IoT 套件，請參閱 < 如何[來自訂預先設定的解決方案][lnk-customize]。

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
