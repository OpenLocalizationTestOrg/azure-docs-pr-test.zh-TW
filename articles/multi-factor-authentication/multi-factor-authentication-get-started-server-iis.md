---
title: "驗證和 Azure MFA Server aaaIIS |Microsoft 文件"
description: "這是可協助您部署 IIS 驗證與 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d1bf1c8a-2c10-4ae6-9f4b-75f0c3df43eb
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017,it-pro
ms.openlocfilehash: 74bd39c2644e2bca0880baea3824cad4c9215111
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-iis-web-apps"></a>針對 IIS Web 應用程式設定 Azure Multi-Factor Authentication Server

使用 IIS 驗證區段中的 hello Azure Multi-factor Authentication (MFA) Server tooenable hello 和設定 IIS 驗證整合與 Microsoft IIS web 應用程式。 hello Azure MFA Server 會安裝一個外掛程式，可以篩選 toohello IIS web 伺服器 tooadd Azure Multi-factor Authentication Server 上提出的要求。 hello IIS 外掛程式提供表單架構驗證和整合式 Windows HTTP 驗證的支援。 信任的 Ip 也可以從 雙因素驗證設定的 tooexempt 內部 IP 位址。

![IIS 驗證](./media/multi-factor-authentication-get-started-server-iis/iis.png)

## <a name="using-form-based-iis-authentication-with-azure-multi-factor-authentication-server"></a>搭配 Azure Multi-Factor Authentication Server 使用表單架構 IIS 驗證
toosecure IIS web 應用程式使用表單架構驗證、 hello Azure Multi-factor Authentication Server hello IIS web 伺服器上安裝和設定每個程序的 hello hello 伺服器：

1. 在 hello Azure Multi-factor Authentication Server，hello 左側功能表中的 hello IIS 驗證 圖示。
2. 按一下 hello**表單架構** 索引標籤。
3. 按一下 [新增] 。
4. toodetect 使用者名稱、 密碼和網域變數，自動輸入 hello 自動設定表單架構網站 對話方塊中的 hello 登入 URL （例如 https://localhost/contoso/auth/login.aspx)，並按一下**確定**。
5. 檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。
6. 如果無法自動偵測 hello 頁面變數，按一下**手動指定**hello 自動設定表單架構網站 對話方塊中。
7. 在 hello 新增表單架構網站 對話方塊中，輸入 hello 提交 URL 欄位中的 hello URL toohello 登入頁面，並輸入應用程式名稱 （選擇性）。 hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。
8. 選取 hello 正確的要求格式。 這設定得**POST 或 GET**大部分 web 應用程式。
9. 輸入 hello 使用者名稱變數、 密碼變數和網域變數 （如果出現在 hello 登入頁面上）。 hello toofind hello 名稱輸入方塊、 瀏覽網頁瀏覽器 toohello 登入頁面、 在 hello 頁面上，以滑鼠右鍵按一下並選取**檢視原始檔**。
10. 檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。
11. 按一下**進階**tooreview 進階設定，包括：

  - 選取自訂拒絕頁面檔案
  - 針對一段時間使用 cookie 快取成功驗證 toohello 網站
  - 選擇是否要針對 Windows 網域、 LDAP 目錄的 tooauthenticate hello 主要認證。 還是 RADIUS 伺服器來進行驗證。

12. 按一下**確定**tooreturn toohello 新增表單架構網站 對話方塊。
13. 按一下 [確定] 。
14. 一次 hello URL 且已偵測到或輸入頁面變數時，顯示在 hello 表單架構 面板的 hello 網站資料。

## <a name="using-integrated-windows-authentication-with-azure-multi-factor-authentication-server"></a>搭配 Azure Multi-Factor Authentication Server 使用整合式 Windows 驗證
IIS web 應用程式使用整合式 Windows 驗證，Azure MFA Server hello hello IIS web 伺服器上安裝，然後設定的 toosecure hello 伺服器以 hello 下列步驟：

1. 在 hello Azure Multi-factor Authentication Server，hello 左側功能表中的 hello IIS 驗證 圖示。
2. 按一下 hello **HTTP**  索引標籤。
3. 按一下 [新增] 。
4. 在 hello [新增基底 URL] 對話方塊中，輸入 hello 網站 HTTP 驗證 （例如 http://localhost/owa) 執行 hello URL，並提供應用程式名稱 （選擇性）。 hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。
5. 調整 hello 閒置逾時和最大工作階段時間如果 hello 預設值不足。
6. 檢查 hello**需要進行 Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入 hello 伺服器與主體 toomulti 雙因素驗證。 如果大量使用者尚未匯入伺服器 hello 和/或將會豁免於多因素驗證，請不要 hello 方塊中選取。
7. 檢查 hello **Cookie 快取**視方塊。
8. 按一下 [確定] 。

## <a name="enable-iis-plug-ins-for-azure-multi-factor-authentication-server"></a>啟用 Azure Multi-Factor Authentication Server 的 IIS 外掛程式
設定之後 hello 表單架構或 HTTP 驗證 Url 和值，請選取 hello 應載入和在 IIS 中啟用 hello Azure Multi-factor Authentication IIS 外掛程式的位置。 使用下列程序的 hello:

1. 如果在 IIS 6 上執行，請按一下 hello **ISAPI**  索引標籤。選取 hello hello web 應用程式的網站正在執行 （例如預設網站） tooenable hello Azure Multi-factor Authentication ISAPI 篩選外掛程式該站台。
2. 如果在 IIS 7 或更新版本執行，請按一下 hello**原生模組** 索引標籤。選取 hello 伺服器、 網站或應用程式 tooenable hello IIS 外掛程式所需的 hello 層級。
3. 按一下 hello**啟用 IIS 驗證**在 hello 囉 」 畫面最上方的方塊。 Azure Multi-factor Authentication 現在會保護選取的 hello IIS 應用程式。 請確認使用者具有已匯入 hello 伺服器。

## <a name="trusted-ips"></a>信任的 IP
hello 信任的 Ip 允許來自特定 IP 位址或子網路的網站要求的使用者 toobypass Azure 多重要素驗證。 比方說，您可以從 Azure Multi-factor Authentication tooexempt 使用者從 hello 辦公室登入時。 因此，您可以指定 hello 辦公室子網路作為信任的 Ip 項目。 tooconfigure 信任 Ip 時，使用下列程序的 hello:

1. 在 hello IIS 驗證區段中，按一下 hello**信任的 Ip**  索引標籤。
2. 按一下 [新增] 。
3. Hello 新增信任的 Ip 對話方塊出現時，選取 hello**單一 IP**， **IP 範圍**，或**子網路**選項按鈕。
4. 輸入 hello IP 位址、 IP 位址範圍或子網路應列入白名單。 如果輸入子網路、 選取 hello 適當的網路遮罩，然後按一下**確定**。 現在已加入 hello 白名單。
