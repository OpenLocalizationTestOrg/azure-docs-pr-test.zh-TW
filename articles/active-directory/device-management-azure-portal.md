---
title: "使用 aaaManaging 裝置 hello Azure 入口網站-預覽 |Microsoft 文件"
description: "了解如何 toouse hello Azure 入口網站 toomanage 裝置。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>管理使用的裝置 hello Azure 入口網站-預覽

>[!NOTE]
>這項功能目前為公開預覽版。 準備 toorevert 或移除任何變更。 公開預覽期間的任何 Azure Active Directory (Azure AD) 訂用帳戶中使用 hello 功能。 不過，hello 功能正式推出時，某些層面 hello 功能可能需要 Azure Active Directory premium 訂用帳戶。


使用 Azure Active Directory (Azure AD) 中的裝置管理，您可以確保使用者會從符合安全性與合規性之標準的裝置來存取您的資源。 

本主題內容：

- 假設您熟悉 hello[簡介 toodevice 管理 Azure Active Directory 中](device-management-introduction.md)

- 提供您管理您的裝置使用的相關資訊與 hello Azure 入口網站


toomanage 裝置 hello Azure 入口網站中的，您需要 tooclick**裝置**在 hello**管理**區段 hello hello **Azure Active Directory**刀鋒視窗。

![管理 Intune 裝置](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>設定裝置設定

您的裝置使用 hello Azure 入口網站，他們需要 toobe toomanage 註冊或聯結 tooAzure AD。 身為管理員，您可以微調 hello 註冊，並將裝置設定 hello 裝置設定程序。

![管理 Intune 裝置](./media/device-management-azure-portal/22.png)


hello 裝置設定 刀鋒視窗，可讓您 tooconfigure:

- **使用者可以將裝置 tooAzure AD** -這個設定可讓您可以加入裝置 tooAzure AD tooselect hello 使用者。 hello 預設值是**所有**。

- **Azure AD 的其他本機系統管理員已加入裝置**-您可以選取在裝置上的本機系統管理員權限授與 hello 使用者。 如果在此處加入使用者加入 toohello*裝置系統管理員*在 Azure AD 中的角色。 Azure AD 中的全域管理員和裝置擁有者預設會授與本機系統管理員權限。 此選項是 premium edition 的功能可透過 Azure AD Premium 或 Enterprise Mobility Suite (EMS) hello 等產品。 

- **使用者可以向 Azure AD 註冊其裝置**-您需要向 Azure AD 中註冊此設定 tooallow 裝置 toobe tooconfigure。 如果您選取**無**，不允許 tooregister 未加入的 Azure AD 或 Azure AD 加入的混合式裝置。 需要先註冊 (registration)，才可註冊 (enrollment) Microsoft Intune 或適用於 Office 365 的行動裝置管理 (MDM)。 如果您已設定任一服務，則會選取 [全部] 且無法使用 [無]。

- **需要 Multi-factor Auth toojoin 裝置**-您可以選擇使用者是否需要的 tooprovide 第二個驗證因素 toojoin 其裝置 tooAzure AD。 hello 預設值是**否**。 建議在註冊裝置時要求 Multi-Factor Authentication。 啟用此服務的多重要素驗證之前，您必須確定 hello 使用者註冊其裝置的設定多重要素驗證。 如需不同 Azure Multi-Factor Authentication 服務的詳細資訊，請參閱[開始使用 Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md)。 

- **裝置數目上限**-此設定可讓您的使用者可以在 Azure AD 中擁有的裝置 tooselect hello 最大數目。 如果使用者達到此配額時，直到其中一個會無法可以 tooadd 其他裝置或多 hello 現有裝置的移除。 針對所有的裝置加入 Azure AD 或 Azure AD 註冊今天計算 hello 裝置引號。 hello 預設值是**20**。

- **使用者可以跨裝置同步設定及應用程式資料**-根據預設，此設定為太**NONE**。 選取特定的使用者或群組，或全部允許 hello 使用者的設定和應用程式資料 toosync 跨他們的 Windows 10 裝置。 深入了解同步在 Windows 10 中的運作方式。
這個選項是可透過 Azure AD Premium 或 Enterprise Mobility Suite (EMS) hello 等產品的高階功能。
 
    ![管理 Intune 裝置](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>尋找裝置

身為管理員，在 hello Azure 入口網站，您有兩個選項 toolocate 已註冊，並加入裝置：

- **所有裝置**在 hello**管理**區段 hello**裝置**刀鋒視窗  

    ![所有裝置](./media/device-management-azure-portal/41.png)


- **裝置**在 hello**管理**區段**使用者**刀鋒視窗
 
    ![所有裝置](./media/device-management-azure-portal/43.png)



兩個選項，您可以使用取得 tooa 檢視的：


- 可讓您 toosearch 裝置做為篩選條件使用 hello 顯示名稱。

- 為您提供已註冊和已加入裝置的詳細概觀

- 可讓您 tooperform 一般裝置管理工作
   

![所有裝置](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>裝置管理工作

身為管理員，您可以管理 hello 註冊或已加入的裝置。 本節為您提供一般裝置管理工作的相關資訊。


**管理 Intune 裝置** - 如果您是 Intune 系統管理員，您可以管理標示為 **Microsoft Intune** 的裝置。 系統管理員可能會看到其他裝置 

![管理 Intune 裝置](./media/device-management-azure-portal/31.png)


**啟用/停用 Azure AD 裝置**

tooenable 或停用裝置，您會需要在 Azure AD 中 toobe 全域管理員。 停用裝置可防止裝置存取您的 Azure AD 資源。  toodisable hello 裝置，您可以按一下*...* 按一下 hello 裝置以取得其他詳細資料。

 
![管理 Intune 裝置](./media/device-management-azure-portal/33.png)

停用裝置 hello 會將狀態變更在 hello**啟用**資料行太**否**。

![停用裝置](./media/device-management-azure-portal/32.png)


**刪除 Azure AD 裝置**-toodelete 裝置，您需要在 Azure AD 中的 toobe 全域管理員。  
刪除裝置：
 
- 防止裝置存取您的 Azure AD 資源 

- 移除所有詳細資料會附加的 toohello 裝置，例如，適用於 Windows 裝置的 BitLocker 金鑰  

- 代表無法復原的活動，除非必要，否則不建議使用

如果裝置已由另一個管理授權單位 (例如 Microsoft Intune) 管理，請確定已抹除 / 淘汰之前刪除 Azure AD 中的 hello 裝置 hello 裝置。

您可選取 […] toodelete hello 裝置，或按一下 其他詳細資料的 hello 裝置上
 
![刪除裝置](./media/device-management-azure-portal/34.png)


**檢視或複製裝置識別碼**-您可以在 hello 裝置或使用 PowerShell 在疑難排解期間使用裝置識別碼 tooverify hello 裝置識別碼詳細資料。 tooaccess hello 複製選項，請按一下 hello 裝置。

![檢視裝置識別碼](./media/device-management-azure-portal/35.png)
  

**檢視或複製 BitLocker 金鑰**-如果您是系統管理員，您可以檢視和複製 hello BitLocker 金鑰 toohelp 使用者 toorecover 加密的磁碟機。 這些金鑰只適用於已加密並將其金鑰儲存在 Azure AD 中的 Windows 裝置。 存取 hello 裝置的詳細資料時，您可以複製這些機碼。
 
![檢視 BitLocker 金鑰](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>稽核記錄檔


hello 裝置活動皆可透過 hello 活動記錄檔。 這包括觸發 hello 裝置註冊服務或由 hello 使用者的活動：

- 建立裝置和 hello 裝置上加入擁有者/使用者

- 變更 toodevice 設定

- 刪除或更新裝置等裝置作業
 
是您稽核資料的項目點 toohello**稽核記錄檔**在 hello**活動**hello 區段 **裝置*刀鋒視窗。

![稽核記錄檔](./media/device-management-azure-portal/61.png)


稽核記錄的預設清單檢視顯示︰

- hello 日期和時間 hello 出現項目

- hello 目標

- hello 啟動器 / 動作項目 （使用者） 的活動

- hello 活動 （目標）

![稽核記錄檔](./media/device-management-azure-portal/63.png)

您可以自訂 hello 清單檢視中，依序按一下**資料行**hello 工具列中。
 
![稽核記錄檔](./media/device-management-azure-portal/64.png)


向下 hello toonarrow 報告資料 tooa 層級，適用於您，您可以篩選 hello 稽核資料，使用下列欄位的 hello:

- 分類
- 活動資源類型
- 活動
- 日期範圍
- 目標
- 啟動者 (執行者)

此外 toohello 篩選，您可以搜尋特定的項目。

![稽核記錄檔](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>後續步驟

* [Azure Active Directory 中的簡介 toodevice 管理](device-management-introduction.md)



