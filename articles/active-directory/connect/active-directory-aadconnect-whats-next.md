---
title: "Azure AD Connect： 後續步驟及如何 toomanage Azure AD Connect |Microsoft 文件"
description: "了解如何 tooextend hello 預設設定和操作工作 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>後續步驟及如何 toomanage Azure AD Connect
貴組織的需求與需求，請使用此發行項 toocustomize Azure Active Directory (Azure AD) 連線 toomeet hello 操作程序。  

## <a name="add-additional-sync-admins"></a>新增額外的同步處理管理員
根據預設，安裝和本機系統管理員未 hello 唯一 hello 使用者會無法 toomanage hello 安裝同步處理引擎。 針對其他人 toobe 無法 tooaccess 和管理 hello 同步處理引擎，找出 hello 本機伺服器上名為 ADSyncAdmins hello 群組並將它們加入 toothis 群組。

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>指派授權 tooAzure AD Premium 和 Enterprise Mobility Suite 的使用者
現在，您的使用者已同步處理 toohello 雲端需要 tooassign 它們以便它們可以開始使用雲端應用程式，例如 Office 365 的授權。

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>Azure AD Premium 或 Enterprise Mobility Suite 授權 tooassign

1. 登入 toohello Azure 入口網站為系統管理員。
2. Hello 左側選取**Active Directory**。
3. 在 [hello **Active Directory**頁面中，按兩下要 tooset hello 使用者 hello 目錄。
4. 在 hello 頂端 hello 目錄] 頁面上，選取**授權**。
5. 在 [hello**授權**頁面上，選取**Active Directory Premium**或**Enterprise Mobility Suite**，然後按一下 [**指派**。
6. 在 hello] 對話方塊中，選取您想 tooassign 授權，然後按一下 [hello 核取記號圖示 toosave hello 變更 hello 使用者。

## <a name="verify-hello-scheduled-synchronization-task"></a>驗證 hello 排程的同步處理工作
使用同步處理的 hello Azure 入口網站 toocheck hello 狀態。

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tooverify hello 排程的同步處理工作
1. 登入 toohello Azure 入口網站為系統管理員。
2. Hello 左側選取**Active Directory**。
3. 在 [hello **Active Directory**頁面中，按兩下要 tooset hello 使用者 hello 目錄。
4. 在 hello 頂端 hello 目錄] 頁面上，選取**目錄整合**。
5. 在下**與本機 active directory 整合**，注意 hello 上次同步處理時間。

<center>![目錄同步處理時間](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>啟動已排定的同步處理工作
如果您需要 toorun 同步處理工作，您可以透過 hello Azure AD Connect 精靈重新執行。  您需要 tooprovide Azure AD 認證。  在 hello 精靈中，選取 [hello**自訂同步處理選項**工作，並按一下**下一步**toomove 透過 hello 精靈。 在 hello 結束時，請確定該 hello **hello 初始設定完成之後儘速開始 hello 同步處理程序**方塊為已選取。

<center>![開始同步處理](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

如需有關 hello Azure AD Connect 同步處理排程器的詳細資訊，請參閱[Azure AD 連接排程器](active-directory-aadconnectsync-feature-scheduler.md)。

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Azure AD Connect 中可用的其他工作
之後您的 Azure AD Connect 的初始安裝，您可以一律 hello 重新啟動精靈從 hello Azure AD Connect 開始頁面或桌面捷徑。  您會發現，再次進行 hello 精靈提供的其他工作的 hello 表單中的部分新選項。  

hello 下表提供這些工作的摘要和每項工作的簡短描述。

![其他工作清單](./media/active-directory-aadconnect-whats-next/addtasks.png)

| 其他工作 | 說明 |
| --- | --- |
| **檢視 hello 選取的案例** |檢視目前的 Azure AD Connect 解決方案。  這包括一般設定、同步處理的目錄，以及同步處理設定。 |
| **自訂同步處理選項** |變更 hello 如加入額外的 Active Directory 樹系 toohello 設定，或啟用同步處理選項，例如使用者、 群組、 裝置或密碼回寫目前的設定。 |
| **啟用預備模式** |階段資訊不會立即同步處理，也不會匯出 tooAzure AD 或內部部署 Active Directory。  利用此功能，您可以在發生前加以預覽 hello 同步處理。 |

## <a name="next-steps"></a>後續步驟
深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。
