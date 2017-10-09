---
title: "aaaLDAP 驗證和 Azure MFA Server |Microsoft 文件"
description: "這是可協助您部署 LDAP 驗證和 Azure Multi-factor Authentication Server 的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>LDAP 驗證和 Azure Multi-Factor Authentication Server
根據預設，hello Azure Multi-factor Authentication Server 設定的 tooimport 或從 Active Directory 同步處理使用者。 不過，它可以設定的 toobind toodifferent LDAP 目錄，例如 ADAM 目錄或特定 Active Directory 網域控制站。 當透過 LDAP 連線的 tooa 目錄，hello Azure Multi-factor Authentication Server 可做為 LDAP proxy tooperform 驗證。 它也允許 hello 使用 LDAP 繫結作為 RADIUS 目標，預先驗證與 IIS 驗證的使用者或 hello Azure MFA 使用者入口網站中的主要驗證。

Azure Multi-factor Authentication 作為 LDAP proxy、 toouse 插入 hello LDAP 用戶端 （例如 VPN 應用裝置、 應用程式） 與 hello LDAP 目錄伺服器之間的 hello Azure Multi-factor Authentication Server。 hello Azure Multi-factor Authentication Server 必須已設定的 toocommunicate hello 用戶端伺服器和 hello LDAP 目錄。 此設定會 hello Azure Multi-factor Authentication Server 會接受來自用戶端伺服器及應用程式的 LDAP 要求，並轉送 toohello 目標 LDAP 目錄伺服器 toovalidate hello 主要認證。 如果 hello LDAP 目錄驗證主要認證的 hello，Azure Multi-factor Authentication Server 會執行第二個的身分識別驗證，並傳送回應後 toohello LDAP 用戶端。 只有當 hello LDAP 伺服器驗證和 hello 第二個步驟驗證成功，hello，整個驗證會成功。

## <a name="configure-ldap-authentication"></a>設定 LDAP 驗證
Windows server 上安裝 hello Azure Multi-factor Authentication Server tooconfigure LDAP 驗證。 使用下列程序的 hello:

### <a name="add-an-ldap-client"></a>新增 LDAP 用戶端

1. 在 hello Azure Multi-factor Authentication Server，選取左窗格中 hello hello [LDAP 驗證] 圖示。
2. 檢查 hello**啟用 LDAP 驗證**核取方塊。

   ![LDAP 驗證](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Hello 用戶端 索引標籤上變更 hello TCP 連接埠和 SSL 連接埠如果 hello Azure Multi-factor Authentication LDAP 服務應繫結 toonon 標準連接埠 toolisten LDAP 要求。
4. 如果您計畫從 hello Azure Multi-factor Authentication Server 的用戶端 toohello toouse LDAPS，SSL 憑證必須安裝在 hello 與 MFA Server 相同的伺服器。 按一下**瀏覽**下一步 toohello SSL 憑證 方塊中，然後選取憑證 toouse hello 安全的連接。
5. 按一下 [新增] 。
6. 在 hello [新增 LDAP 用戶端] 對話方塊中，輸入 hello 的 hello 應用裝置、 伺服器或驗證 toohello 伺服器和應用程式名稱 （選用） 的應用程式的 IP 位址。 hello 應用程式名稱會出現在 Azure Multi-factor Authentication 報告，並可能會顯示在簡訊或行動裝置應用程式驗證訊息內。
7. 檢查 hello**需要 Azure Multi-factor Authentication 使用者比對**方塊如果所有使用者，或者將匯入伺服器 hello 和主旨 tootwo 步驟驗證。 如果大量使用者尚未匯入伺服器 hello 和/或豁免雙步驟驗證，請不要 hello 方塊中選取。 這項功能，請參閱 hello MFA Server 說明檔以取得其他資訊。

重複這些步驟 tooadd 其他 LDAP 用戶端。

### <a name="configure-hello-ldap-directory-connection"></a>設定 hello LDAP 目錄連線

Hello Azure 多重要素驗證時設定的 tooreceive LDAP 驗證，則必須將這些驗證 toohello LDAP 目錄。 因此，hello 目標 索引標籤只會顯示單一灰色選項 toouse LDAP 目標。

1. tooconfigure hello LDAP 目錄連線，按一下 hello**目錄整合**圖示。
2. 在 hello 設定 索引標籤上選取 hello**使用特定 LDAP 設定**選項按鈕。
3. 選取 [編輯...]
4. 在 hello [編輯 LDAP 組態] 對話方塊中，填入 hello 欄位 hello 所需的資訊 tooconnect toohello LDAP 目錄。 Hello 欄位的說明包含在 hello Azure Multi-factor Authentication Server 說明檔。

    ![目錄整合](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. 按一下 hello 測試 hello LDAP 連線**測試** 按鈕。
6. 如果 hello LDAP 連線測試成功，請按一下 hello**確定** 按鈕。
7. 按一下 hello**篩選** 索引標籤 hello 伺服器已預先設定的 tooload 容器、 安全性群組和使用者從 Active Directory。 如果繫結 tooa 不同的 LDAP 目錄，您可能需要顯示 tooedit hello 篩選器。 按一下 hello**協助**如需篩選的詳細資訊的連結。
8. 按一下 hello**屬性** 索引標籤 hello 伺服器是 Active Directory 中的預先設定的 toomap 屬性。
9. 如果您要繫結 tooa 不同 LDAP 目錄或 toochange hello 預先設定的屬性對應，按一下**編輯...**
10. 在 hello [編輯屬性] 對話方塊中，修改您的目錄 hello LDAP 屬性對應。 屬性名稱可以輸入或選取按一下 hello **...** 下一個 tooeach 欄位按鈕。 按一下 hello**協助**屬性的詳細資訊的連結。
11. 按一下 hello**確定** 按鈕。
12. 按一下 hello**公司設定**圖示，然後選取 hello**使用者名稱解析** 索引標籤。
13. 如果您正在從已加入網域的伺服器連接 tooActive 目錄，將保留 hello**使用 Windows 安全性識別碼 (Sid) 比對使用者名稱**選取選項按鈕。 否則，請選取 hello**使用 LDAP 唯一識別碼屬性比對使用者名稱**選項按鈕。 

當 hello**使用 LDAP 唯一識別碼屬性比對使用者名稱**選取選項按鈕，hello Azure Multi-factor Authentication Server 會嘗試 tooresolve 每個使用者名稱 tooa 唯一識別碼 hello LDAP 目錄中的。 在執行 LDAP 搜尋上 hello Username 屬性定義在 hello 目錄整合-> 屬性 索引標籤。使用者驗證時，hello 使用者名稱時解析的 toohello hello LDAP 目錄中的唯一識別碼。 hello 唯一識別項用於比對 hello Azure Multi-factor Authentication 資料檔中的 hello 使用者。 這可進行不區分大小寫的比較，且允許完整或簡短的使用者名稱格式。

完成這些步驟之後，hello MFA Server 會接聽 hello 的 LDAP 存取要求的 hello 設定連接埠上設定用戶端，以及做為 proxy 的那些要求 toohello LDAP 目錄進行驗證。

## <a name="configure-ldap-client"></a>設定 LDAP 用戶端
tooconfigure hello LDAP 用戶端，使用 hello 指導方針：

* 設定您的應用裝置、 伺服器或應用程式 tooauthenticate 透過 LDAP toohello Azure Multi-factor Authentication Server，就好像是 LDAP 目錄。 使用 hello 相同設定，您通常會使用 tooconnect 直接 tooyour LDAP 目錄中的，除了 hello 伺服器名稱或 IP 位址，應採用 hello Azure Multi-factor Authentication Server。
* 設定 hello LDAP 逾時 too30 60 秒，以便有時間 toovalidate hello 使用者的認證與 hello LDAP 目錄、 執行 hello 第二個步驟的驗證、 接收其回應，以及回應 toohello LDAP 存取要求。
* 如果使用 LDAPS，hello 應用裝置或 hello，LDAP 查詢的伺服器必須信任 hello hello Azure Multi-factor Authentication Server 上安裝的 SSL 憑證。

