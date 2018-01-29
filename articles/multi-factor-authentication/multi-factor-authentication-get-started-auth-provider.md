---
title: "開始使用 Azure Multi-Factor Auth Provider | Microsoft Docs"
description: "了解如何建立 Azure Multi-Factor Auth Provider。"
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/08/2017
ms.author: joflore
ms.reviewer: richagi
ms.custom: it-pro
ms.openlocfilehash: b04fd6f969461cf39016df951007c59047c8857a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="getting-started-with-an-azure-multi-factor-authentication-provider"></a>開始使用 Azure Multi-Factor Authentication Provider
依預設，擁有 Azure Active Directory 和 Office 365 使用者的全域管理員可以使用雙步驟驗證。 不過，如果您想要充分利用[進階功能](multi-factor-authentication-whats-next.md)，則應該購買完整版的 Azure Multi-Factor Authentication (MFA)。

Azure Multi-Factor Auth Provider 可用來充分利用完整版 Azure MFA 所提供的功能。 它的適用對象是**未透過 Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 取得授權**的使用者。  Azure MFA、Azure AD Premium 和 EMS 預設會包含完整版 Azure MFA。 如果您有授權，則不需要 Azure Multi-Factor Auth Provider。

下載 SDK 需要 Azure Multi-Factor Auth Provider。

> [!IMPORTANT]
> 已宣告 Azure Multi-Factor Authentication 軟體開發套件 (SDK) 即將過時。 新客戶不再支援此功能。 目前的客戶可以繼續使用 SDK 直到 2018 年 11 月 14 日。 在這個時間之後，對 SDK 的呼叫將會失敗。

> [!IMPORTANT]
>若要下載 SDK，即使您有 Azure MFA、AAD Premium 或 EMS 授權，還是需要建立 Azure 多因素驗證提供者。  如果您針對此用途建立 Azure Multi-Factor Auth Provider，且已有授權，請務必使用**每個啟用的使用者**模型建立提供者。 然後，將提供者連結至包含 Azure MFA、Azure AD Premium 或 EMS 授權的目錄。 這個組態可確保您只會在執行雙步驟驗證的唯一使用者超過您所擁有的授權數目時收到帳單。 

## <a name="what-is-an-mfa-provider"></a>什麼是 MFA Provider？

如果您沒有 Azure Multi-factor Authentication 的授權，可以建立驗證提供者，為您的使用者要求雙步驟驗證。

驗證提供者的類型有兩種，差異在於您 Azure 訂用帳戶的收費方式。 每次驗證選項會計算一個月中對您的租用戶執行之驗證數目。 如果您有許多使用者偶爾才會進行驗證，最好使用此選項。 每位使用者選項會計算您的租用戶中一個月執行雙步驟驗證之個人數目。 如果您的某些使用者已擁有授權，但是需要將 MFA 擴充至您授權限制之外的更多使用者，最好使用此選項。

## <a name="create-an-mfa-provider"></a>建立 MFA Provider

使用下列步驟，在 Azure 入口網站中建立 Azure Multi-Factor Authentication Provider：

1. 以系統管理員身分登入 [Azure 入口網站](https://portal.azure.com)。 
2. 選取 [Azure Active Directory] > [MFA Server] > [提供者]。

   ![提供者][Providers]

3. 選取 [新增] 。
4. 填寫下列欄位，然後選取 [新增]：
   - **名稱** – 提供者的名稱。
   - **使用量模型** – 選擇兩個選項其中之一：
      * 每次驗證 – 購買依每次驗證付費的模式。 通常用於在取用者導向應用程式中使用 Azure Multi-factor Authentication 的案例。
      * 每個啟用的使用者 – 購買依每個啟用使用者付費的模式。 通常用於員工存取 Office 365 之類的應用程式。 如果某些使用者已擁有 Azure MFA 的授權，請選擇這個選項。
   - **訂用帳戶** – 透過 Provider 針對雙步驟驗證活動計費的 Azure 訂用帳戶。 
   - **目錄** – 與 Provider 相關聯的 Azure Active Directory 租用戶。
      * 您不需要 Azure AD 目錄即可建立 Provider。 如果您只打算下載 Azure Multi-Factor Authentication Server，請將方塊保留空白。
      * Provider 必須與 Azure AD 目錄產生關聯，才能利用進階功能。
      * 只有一個 Provider 可以與任何一個 Azure AD 目錄相關聯。

## <a name="manage-your-mfa-provider"></a>管理 MFA Provider

建立 MFA 提供者之後，您就無法變更使用量模型 (依據已啟用的使用者或依據驗證)。 不過，您可以刪除 MFA 提供者，然後建立一個使用不同使用量模型的 MFA 提供者。

如果目前的 Multi-Factor Auth Provider 與 Azure AD 目錄 (也稱為 Azure AD 租用戶) 相關聯，您就可以安全地將 MFA 提供者刪除，並建立連結至相同 Azure AD 租用戶的 MFA 提供者。 或者，如果您購買的 MFA、Azure AD Premium 或 Enterprise Mobility + Security (EMS) 授權已足夠讓啟用 MFA 的所有使用者使用，您可以一併刪除 MFA 提供者。

如果您的 MFA 提供者未連結至 Azure AD 租用戶，或是您將新的 MFA 提供者連結至不同 Azure AD 租用戶，則使用者設定和組態選項並不會進行轉移。 此外，現有 Azure MFA 伺服器也需要使用新 MFA 提供者產生的啟用認證重新啟動。 重新啟用 MFA 伺服器以將其連結至新的 MFA 提供者，並不會影響電話和簡訊驗證，但所有使用者的行動裝置應用程式通知將會停止運作，直到他們重新啟動行動裝置應用程式。

## <a name="next-steps"></a>後續步驟

[進行 Multi-Factor Authentication 設定](multi-factor-authentication-whats-next.md)

[Providers]: ./media/multi-factor-authentication-get-started-auth-provider/add-providers.png "新增 MFA 提供者"
