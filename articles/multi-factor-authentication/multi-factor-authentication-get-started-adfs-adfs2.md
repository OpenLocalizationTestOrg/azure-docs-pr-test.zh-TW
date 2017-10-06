---
title: "使用 AD FS 2.0 的 Azure MFA Server aaaUse |Microsoft 文件"
description: "這是描述 tooget 如何開始使用 Azure MFA 和 AD FS 2.0 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 96168849-241a-4499-a224-d829913caa7e
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 15011a94ca69dc6e51aa3edf74f5db6cd44d697a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-20"></a>使用 AD FS 2.0 設定 Azure Multi-factor Authentication Server toowork
這篇文章是針對同盟與 Azure Active Directory，而且想要在內部部署的 toosecure 資源組織或 hello 雲端中。 使用 hello Azure Multi-factor Authentication Server 並將它設定 toowork 與 AD FS，以便觸發高價值端點的雙步驟驗證，以保護您的資源。

本文件涵蓋使用 AD FS 2.0 中的 hello Azure Multi-factor Authentication Server。 如需 AD FS 的相關資訊，請參閱[搭配 Windows Server 2012 R2 AD FS 使用 Azure Multi-Factor Authentication Server 保護雲端和內部部署資源](multi-factor-authentication-get-started-adfs-w2k12.md)。

## <a name="secure-ad-fs-20-with-a-proxy"></a>使用 Proxy 保護 AD FS 2.0
toosecure AD FS 2.0 proxy，搭配 hello AD FS proxy 伺服器上安裝 hello Azure Multi-factor Authentication Server。

### <a name="configure-iis-authentication"></a>設定 IIS 驗證
1. 在 hello Azure Multi-factor Authentication Server 中，按一下 hello **IIS 驗證**hello 左功能表中的圖示。
2. 按一下 hello**表單架構** 索引標籤。
3. 按一下 [新增] 。

   <center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/setup1.png)</center>

4. toodetect 使用者名稱、 密碼和網域變數，自動輸入 （例如 https://sso.contoso.com/adfs/ls) hello 自動設定表單架構網站 對話方塊中的 hello 登入 URL，然後按一下**確定**。
5. 檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入伺服器 hello 和主旨 tootwo 步驟驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於兩步驟驗證，請不要 hello 方塊中選取。
6. 如果無法自動偵測 hello 頁面變數，按一下 hello**手動指定...** hello 自動設定表單架構網站 對話方塊中的按鈕。
7. 在 hello 新增表單架構網站 對話方塊中，輸入 hello URL toohello AD FS 登入頁面中 （例如 https://sso.contoso.com/adfs/ls) hello 提交 URL 欄位並輸入應用程式名稱 （選擇性）。 hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。
8. 設定得 hello 要求格式**POST 或 GET**。
9. 輸入 hello 使用者名稱變數 (ctl00$ ContentPlaceHolder1$ UsernameTextBox) 和密碼變數 (ctl00$ ContentPlaceHolder1$ PasswordTextBox)。 如果您以表單為基礎的登入頁面顯示網域文字方塊，輸入 hello 網域變數。 hello hello 登入頁面上，於 web 瀏覽器，移 toohello 登入頁面上的輸入方塊 toofind hello 名稱上按一下滑鼠右鍵 hello 頁面，然後選取**檢視原始檔**。
10. 檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入伺服器 hello 和主旨 tootwo 步驟驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於兩步驟驗證，請不要 hello 方塊中選取。
    <center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/manual.png)</center>
11. 按一下 [進階...] tooreview 進階設定。 您可以進行的設定包括︰

    - 選取自訂拒絕頁面檔案
    - 使用 cookie 快取成功驗證 toohello 網站
    - 選取如何 tooauthenticate hello 主要認證

12. 由於 hello AD FS proxy 伺服器可能不會 toobe 加入 toohello 網域，您可以使用 LDAP tooconnect tooyour 網域控制站的使用者匯入和預先驗證。 在 hello 進階表單架構網站 對話方塊中，按一下 hello**主要驗證**索引標籤並選取**LDAP 繫結**hello 預先驗證驗證類型。
13. 完成後，按**確定**tooreturn toohello 新增表單架構網站 對話方塊。
14. 按一下**確定**tooclose hello 對話方塊。
15. 一次 hello URL 且已偵測到或輸入頁面變數時，顯示在 hello 表單架構 面板的 hello 網站資料。
16. 按一下 hello**原生模組**索引標籤上，選取的伺服器 hello，hello 網站 hello AD FS proxy 執行下 (例如"Default Web Site")，或 hello AD FS proxy 應用程式 （例如"ls"在"adfs"下) tooenable hello IIS 外掛程式在 hello所需的層級。
17. 按一下 hello**啟用 IIS 驗證**在 hello 囉 」 畫面最上方的方塊。

hello IIS 驗證現在已啟用。

### <a name="configure-directory-integration"></a>設定目錄整合
啟用 IIS 驗證，但 tooperform hello 預先驗證 tooyour 透過 Active Directory (AD) 必須設定的 LDAP hello LDAP 連線 toohello 網域控制站。

1. 按一下 hello**目錄整合**圖示。
2. 在 hello 設定 索引標籤上選取 hello**使用特定 LDAP 設定**選項按鈕。

   <center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap1.png)</center>

3. 按一下 [ **編輯**]。
4. 在 hello [編輯 LDAP 組態] 對話方塊中，填入 hello 欄位與 hello 資訊需要的 tooconnect toohello AD 網域控制站。 Hello 欄位的說明包含在 hello Azure Multi-factor Authentication Server 說明檔。
5. 按一下 hello 測試 hello LDAP 連線**測試** 按鈕。

   <center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/ldap2.png)</center>

6. 如果 hello LDAP 連線測試成功，請按一下**確定**。

### <a name="configure-company-settings"></a>進行公司設定
1. 接下來，按一下 [hello**公司設定**圖示，然後選取 hello**使用者名稱解析**] 索引標籤。
2. 選取 hello**使用 LDAP 唯一識別碼屬性比對使用者名稱**選項按鈕。
3. 如果使用者輸入其使用者名稱以"domain\username"格式，hello 伺服器建立 hello LDAP 查詢時，必須關閉 hello username toobe 無法 toostrip hello 網域。 這個動作可透過登錄設定完成。
4. 開啟 hello 登錄編輯程式，並移 tooHKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Positive 網路/PhoneFactor 64 位元伺服器上的。 在 32 位元伺服器上，如果需要 hello"Wow6432Node"hello 路徑之外。 建立 DWORD 登錄機碼稱為"UsernameCxz_stripPrefixDomain"，並設定 hello 值 too1。 Azure Multi-factor Authentication 現在會保護 hello AD FS proxy。

請確認已被使用者從 Active Directory 匯入 hello 伺服器。 請參閱 hello[信任的 Ip 區段](#trusted-ips)如果您想要的 toowhitelist 內部 IP 位址，因此 toohello 網站，從這些位置在登入時，不需要雙步驟驗證。

<center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/reg.png)</center>

## <a name="ad-fs-20-direct-without-a-proxy"></a>沒有 Proxy 的 AD FS 2.0 Direct
您可以在不使用 hello AD FS proxy 時保護 AD FS。 Hello AD FS 伺服器上安裝 Azure Multi-factor Authentication Server hello 和設定的 hello 伺服器 hello 下列每一個步驟：

1. 在 hello Azure Multi-factor Authentication Server 中，按一下 hello **IIS 驗證**hello 左功能表中的圖示。
2. 按一下 hello **HTTP**  索引標籤。
3. 按一下 [新增] 。
4. 在 [hello [新增基底 URL] 對話方塊中，輸入 hello AD FS 網站 HTTP 驗證執行的地方 （例如 https://sso.domain.com/adfs/ls/auth/integrated) hello 基底 URL] 欄位到 hello URL。 然後，輸入應用程式名稱 (選擇性)。 hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。
5. 如有需要，調整 hello 閒置逾時和最大工作階段 時間。
6. 檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入伺服器 hello 和主旨 tootwo 步驟驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於兩步驟驗證，請不要 hello 方塊中選取。
7. 如有需要，請檢查 hello cookie 快取方塊。

   <center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/noproxy.png)</center>

8. 按一下 [確定] 。
9. 按一下 hello**原生模組** 索引標籤並選取 hello 伺服器、 hello 網站 (例如"Default Web Site") 或 hello AD FS 的應用程式 （例如"ls"在"adfs"下) tooenable hello IIS 外掛程式在 hello 所需層級。
10. 按一下 hello**啟用 IIS 驗證**在 hello 囉 」 畫面最上方的方塊。

Azure Multi-Factor Authentication 現已保護 AD FS。

請確認已被使用者從 Active Directory 匯入 hello 伺服器。 請參閱 hello 信任的 Ip 區段，如果您想要 toowhitelist 內部 IP 位址，讓登入 toohello 網站，從這些位置時，不需要雙步驟驗證。

## <a name="trusted-ips"></a>信任的 IP
信任的 Ip 允許來自特定 IP 位址或子網路的網站要求的使用者 toobypass Azure 多重要素驗證。 例如，您可以 tooexempt 雙步驟驗證的使用者登入從 hello office 時。 因此，您可以指定 hello 辦公室子網路作為信任的 Ip 項目。

### <a name="tooconfigure-trusted-ips"></a>tooconfigure 可信任 Ip
1. 在 hello IIS 驗證區段中，按一下 hello**信任的 Ip**  索引標籤。
2. 按一下 hello**新增...** 按鈕。
3. Hello 新增信任的 Ip 對話方塊出現時，請選取其中一個 hello**單一 IP**， **IP 範圍**，或**子網路**選項按鈕。
4. 輸入 hello IP 位址、 IP 位址範圍或應列入白名單的子網路。 如果輸入子網路，請選取 hello 適當的網路遮罩，然後按一下 hello**確定** 按鈕。 hello 信任 IP 現在已加入。

<center>![設定](./media/multi-factor-authentication-get-started-adfs-adfs2/trusted.png)</center>
