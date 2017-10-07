---
title: "在重新執行 hello Azure AD Connect 的安裝精靈 |Microsoft 文件"
description: "說明 hello 安裝精靈的運作方式 hello 第二次執行它。"
keywords: "hello Azure AD Connect 的安裝精靈可讓您設定第二次執行的維護設定 hello"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Azure AD Connect 同步： 第二次執行 hello 安裝精靈
hello 第一次執行 hello Azure AD Connect 的安裝精靈，它將逐步引導您 tooconfigure 您的安裝。 如果您再次執行 hello 安裝精靈，它會提供維護選項。

您可以找到名為 hello 開始 功能表中的 hello 安裝精靈**Azure AD Connect**。

![[開始] 功能表](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

當您啟動 hello 安裝精靈時，您會看到與這些選項的頁面：

![含有其他工作清單的頁面](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

如果您已使用 Azure AD Connect 安裝 ADFS，您會有更多選項。 hello 其他選項，您必須針對 ADFS 記載於[ADFS 管理](active-directory-aadconnect-federation-management.md#manage-ad-fs)。

選取其中一項 hello 工作，然後按一下**下一步**toocontinue。

> [!IMPORTANT]
> 當 hello 安裝精靈開啟時，就會暫停 hello 同步處理引擎中的所有作業。 請確定您已完成設定變更時，關閉 hello 安裝精靈。
>
>

## <a name="view-current-configuration"></a>檢視目前的組態
此選項可讓您快速檢視目前設定的選項。

![含有所有選項和其狀態之清單的頁面](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

按一下**上一步**toogo 上一步。 如果您選取**結束**，關閉 hello 安裝精靈。

## <a name="customize-synchronization-options"></a>自訂同步處理選項
這個選項是使用的 toomake 變更 toohello 同步處理設定。 您看到的子集 hello 自訂設定安裝路徑中的選項。 即使您一開始是使用快速安裝也會看到此選項。

* [新增其他目錄](active-directory-aadconnect-get-started-custom.md#connect-your-directories)。 若要移除目錄，請參閱 [刪除連接器](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete)。
* [變更網域和 OU 篩選](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)。
* 移除群組篩選。
* [變更選用功能](active-directory-aadconnect-get-started-custom.md#optional-features)。

hello hello 初始安裝中的其他選項無法變更或不能使用。 這些選項包括：

* 變更 hello 屬性 toouse userPrincipalName 和 sourceAnchor。
* 變更 hello 聯結來自不同樹系的物件的方法。
* 啟用群組式篩選。

## <a name="refresh-directory-schema"></a>重新整理目錄結構描述
會使用此選項，如果您已經變更 hello 結構描述，其中一種您內部部署 AD DS 樹系。 例如，您可能已安裝 Exchange 或升級 Windows Server 2012 tooa 結構描述與裝置物件。 在此情況下，您需要 tooinstruct Azure AD Connect tooread hello 結構描述一次從 AD DS，並更新其快取。 這個動作也會重新產生 hello 同步處理規則。 如果您加入 hello Exchange 結構描述，例如，適用於 Exchange 的 hello 同步處理規則會加入 toohello 組態。

當您選取此選項時，會列出所有組態中的 hello 目錄。 您可以保留 hello 預設設定和重新整理所有樹系或取消選取部分。

![Hello 環境中的所有目錄的清單頁面](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>設定預備模式
此選項可讓您 tooenable 並停用預備模式 hello 伺服器上。 預備模式和其使用方式的詳細資訊可在 [作業](active-directory-aadconnectsync-operations.md#staging-mode)中找到。

如果目前啟用或停用預備 hello 選項就會顯示：  
![也會顯示 hello 的預備模式的目前狀態的選項](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange hello 狀態，請選取此選項和 hello 選取或取消選取核取方塊。  
![也會顯示 hello 的預備模式的目前狀態的選項](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>變更使用者登入
此選項可讓您從密碼同步 toofederation 或 hello 反過來 toochange。 您也無法變更**不設定**。

如需此選項的詳細資訊，請參閱 [使用者登入](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method)。

## <a name="next-steps"></a>後續步驟
* 深入了解使用 Azure AD Connect 同步處理中的 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。

**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)
