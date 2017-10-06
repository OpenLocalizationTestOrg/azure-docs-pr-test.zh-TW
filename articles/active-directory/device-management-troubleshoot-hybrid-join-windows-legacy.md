---
title: "aaaTroubleshooting 混合 Azure Active Directory 加入下層裝置 |Microsoft 文件"
description: "針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解 

本主題是適用的唯一 toohello 下列裝置： 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

對於 Windows 10 或 Windows Server 2016，請參閱[針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解](device-management-troubleshoot-hybrid-join-windows-current.md)。

本主題假設您有[設定混合式 Azure Active Directory 加入裝置](device-management-hybrid-azuread-joined-devices-setup.md)toosupport hello 下列案例：

- 裝置型條件式存取

- [設定的企業漫遊](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello 企業版](active-directory-azureadjoin-passport-deployment.md) 





此主題提供疑難排解指引 tooresolve 可能問題的方式。  

**您應該知道的事情：** 

- hello 的每個使用者的裝置數目上限是裝置為中心。 例如，如果*jdoe*和*jharnett*登入 tooa 裝置建立個別登錄 (DeviceID) 為每個在 hello**使用者**資訊 索引標籤。  

- hello 初始註冊 / 聯結的裝置是已設定的 tooperform 次嘗試登入或鎖定 / 解除鎖定。 工作排程器工作可能會觸發 5 分鐘的延遲。 

- Hello 作業系統或手動重新安裝取消登錄 」 以及 「 重新註冊可能會在 Azure AD 上建立新的註冊和 hello 使用者資訊 索引標籤底下的多個項目會導致 hello Azure 入口網站。 


## <a name="step-1-retrieve-hello-registration-status"></a>步驟 1： 擷取 hello 註冊狀態 

**tooverify hello 註冊狀態：**  

1. 以系統管理員身分開啟 hello 命令提示字元 

2. 輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

此命令會顯示對話方塊，讓您提供更多詳細 hello 聯結狀態。

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>步驟 2： 評估 hello 混合 Azure AD 的聯結狀態 

如果未成功加入 hello 混合 Azure AD，hello 對話方塊會提供您 hello 問題已經發生的相關詳細資料。

**hello 最常見的問題是：**

- AD FS 或 Azure AD 設定不正確

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- 您不是以網域使用者身分登入

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- 已達到配額限制

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- hello 服務沒有回應 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

您也可以在 hello 事件記錄檔中找到 hello 狀態資訊**應用程式和服務 Log\Microsoft 地點**。
  
**失敗的混合式 Azure AD 聯結 hello 最常見原因包括：** 

- 您的電腦不在 hello 組織內部網路或 VPN 連線 tooan 沒有內部部署 AD 網域控制站。

- 您登入 tooyour 電腦與本機電腦帳戶。 

- 服務組態問題： 

  - hello 同盟伺服器已設定的 toosupport **WIAORMULTIAUTHN**。 

  - 沒有在 Azure AD 中指向 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中的服務連接點物件。

  - 使用者已達到 hello 的裝置。 

## <a name="next-steps"></a>後續步驟

如有問題，請參閱 hello[裝置管理常見問題集](device-management-faq.md)  
