---
title: "aaaTroubleshooting hello 自動登錄，Azure AD 網域的電腦加入 Windows 下層用戶端 |Microsoft 文件"
description: "疑難排解 hello 自動註冊的 Azure AD 網域加入 Windows 下層用戶端的電腦。"
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD 

本主題僅適用於下列用戶端的唯一 toohello: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

針對 Windows 10 或 Windows Server 2016，請參閱[疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)。

本主題假設您已設定自動註冊已加入網域的裝置如中所述述[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-device-registration-get-started.md)。
 
此主題提供疑難排解指引 tooresolve 可能問題的方式。  
成功的結果的一些事項 toonote: 

- 在 Azure AD 上註冊這些用戶端時是依據個別使用者/裝置。 例如： 如果 jdoe 和 jharnett 登入 toothis 裝置，這些使用者在 hello 使用者資訊] 索引標籤中的每個建立個別登錄 (DeviceID)。  

- 這些用戶端 hello 現成的註冊作業就會在登入或鎖定/解除鎖定設定的 tootry 和可能有 5 分鐘的延遲，這觸發使用工作排程器工作。 

- 重新安裝，hello 作業系統或手動取消註冊及重新登錄可能會在 Azure AD 上建立新的註冊，並會導致多個項目 hello 使用者資訊] 索引標籤底下 hello Azure 入口網站。 


## <a name="step-1-retrieve-hello-registration-status"></a>步驟 1： 擷取 hello 註冊狀態 

**tooverify hello 註冊狀態：**  

1. 以系統管理員身分開啟 hello 命令提示字元 

2. 輸入 `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`

此命令會顯示對話方塊，讓您提供更多詳細 hello 聯結狀態。

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>步驟 2： 評估 hello 登錄狀態 

如果 hello 聯結不成功，hello 對話方塊會提供您 hello 問題已經發生的相關詳細資料。

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
  
**hello 失敗註冊最常見的原因包括：** 

- 您的電腦不在 hello 組織內部網路或 VPN 連線 tooan 沒有內部部署 AD 網域控制站。

- 您登入 tooyour 電腦與本機電腦帳戶。 

- 服務組態問題： 

  - hello 同盟伺服器已設定的 toosupport **WIAORMULTIAUTHN**。 

  - 沒有在 Azure AD 中指向 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中的服務連接點物件。

  - 使用者已達到 hello 的裝置。 請參閱＜開始使用 Azure Active Directory 裝置註冊＞。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 hello[自動裝置註冊常見問題集](active-directory-device-registration-faq.md) 
