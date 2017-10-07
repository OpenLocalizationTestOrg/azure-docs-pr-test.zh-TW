---
title: "aaaMFA 與 Windows Server 中的 AD FS 伺服器 |Microsoft 文件"
description: "本文說明 tooget 2016 和 Windows Server 2012 R2 中的 AD FS 與 Azure Multi-factor Authentication 的啟動方式。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 57208068-1e55-45b6-840f-fdcd13723074
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/29/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 656785abcc63a020add765a86670b488a3b84b51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-toowork-with-ad-fs-in-windows-server"></a>使用 Windows Server 中的 AD FS 設定 Azure Multi-factor Authentication Server toowork
如果您使用 Active Directory Federation Services (AD FS)，而且想 toosecure 雲端或內部部署資源，您可以使用 AD FS 設定 Azure Multi-factor Authentication Server toowork。 此組態會觸發高價值端點的雙步驟驗證。

在本文中，我們將討論如何搭配 Windows Server 2012 R2 或 Windows Server 2016 中的 AD FS 使用 Azure Multi-Factor Authentication Server。 如需詳細資訊，了解太[地使用 AD FS 2.0 中使用 Azure Multi-factor Authentication Server 保護雲端和內部部署資源](multi-factor-authentication-get-started-adfs-adfs2.md)。

## <a name="secure-windows-server-ad-fs-with-azure-multi-factor-authentication-server"></a>使用 Azure Multi-Factor Authentication Server 保護 Windows Server AD FS
當您安裝 Azure Multi-factor Authentication Server 時，您會有下列選項的 hello:

* 本機 hello 上安裝 Azure Multi-factor Authentication Server 與 AD FS 相同的伺服器
* Hello AD FS 伺服器上本機安裝 hello Azure 多重要素驗證配接器，然後再安裝一部電腦上的 Multi-factor Authentication Server

開始之前，請留意的 hello 下列資訊：

* 您不需要的 tooinstall Azure Multi-factor Authentication Server AD FS 伺服器上。 不過，您必須安裝 hello Multi-factor Authentication 配接器的 Windows Server 2012 R2 或 Windows Server 2016 執行 AD FS 上的 AD FS。 如果是支援的版本，而且您 hello AD FS 配接器個別安裝 AD FS 同盟伺服器上，您可以在不同電腦上安裝 hello 伺服器。 請參閱 hello 下列程序 toolearn 如何 tooinstall hello 配接器分開。
* 如果您的組織使用簡訊或行動裝置應用程式驗證方法，定義公司設定中的 hello 字串包含預留位置，<$*application_name*$>。 在 MFA Server v7.1 中，您可以提供要取代此預留位置的應用程式名稱。 在 v7.0 或較舊，這個版面配置不會自動時，取代使用 hello AD FS 配接器。 如需這些較舊版本，保護 AD FS 時，從 hello 適當的字串移除 hello 預留位置。
* 使用 toosign 中的 hello 帳戶必須具有 Active Directory 服務中的使用者權限 toocreate 安全性群組。
* hello Multi-factor Authentication AD FS 配接器安裝精靈會建立名執行個體的 Active Directory 中 PhoneFactor Admins 安全性群組。 接著，它會加入您的同盟服務 toothis 群組 hello AD FS 服務帳戶。 PhoneFactor Admins 群組確實已經建立該 hello 與 hello AD FS 服務帳戶是這個群組的成員，請確認您的網域控制站上。 如果有必要，請手動加入 hello AD FS 服務帳戶 toohello PhoneFactor Admins 群組您的網域控制站上。
* 與 hello 使用者入口網站安裝 hello Web 服務 SDK 的相關資訊，請參閱有關[hello 使用者入口網站部署為 Azure Multi-factor Authentication Server。](multi-factor-authentication-get-started-portal.md)

### <a name="install-azure-multi-factor-authentication-server-locally-on-hello-ad-fs-server"></a>Azure Multi-factor Authentication Server 伺服器本機上安裝 AD FS hello
1. 在 AD FS 伺服器上下載並安裝 Azure Multi-Factor Authentication Server。 如需安裝資訊，請參閱 [開始使用 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server.md)。
2. 在 hello Azure Multi-factor Authentication Server 管理主控台中，按一下 hello **AD FS**圖示。 選取 hello 選項**允許使用者註冊**和**tooselect 方法可讓使用者**。
3. 選取您想要 toospecify 貴組織的任何其他選項。
4. 按一下 [安裝 AD FS 配接器] 。
   
   <center>![雲端](./media/multi-factor-authentication-get-started-adfs-w2k12/server.png)</center>

5. 如果顯示 hello Active Directory 視窗，就表示兩件事。 您的電腦是聯結的 tooa 網域和 hello hello AD FS 介面卡與 hello Multi-factor Authentication 服務之間安全通訊的 Active Directory 組態不完整。 按一下**下一步**tooautomatically 完成這項設定，或選取 hello**略過自動 Active Directory 設定，然後設定手動**核取方塊。 按一下 [下一步] 。
6. 如果顯示 hello 本機群組的 windows，這表示兩件事。 您的電腦不是聯結的 tooa 網域而 hello AD FS 介面卡與 hello Multi-factor Authentication 服務之間安全通訊的 hello 本機群組設定尚未完成。 按一下**下一步**tooautomatically 完成這項設定，或選取 hello**略過自動本機群組設定，然後設定手動**核取方塊。 按一下 [下一步] 。
7. 在 hello 安裝精靈 中，按一下 **下一步**。 Azure Multi-factor Authentication Server 建立 hello PhoneFactor Admins 群組，並將 hello AD FS 服務帳戶 toohello PhoneFactor Admins 群組。
   <center>![雲端](./media/multi-factor-authentication-get-started-adfs-w2k12/adapter.png)</center>
8. 在 hello**啟動安裝程式**頁面上，按一下**下一步**。
9. 在 hello Multi-factor Authentication AD FS 配接器安裝程式中，按一下 **下一步**。
10. 按一下**關閉**hello 安裝完成時。
11. 如果已安裝 hello 配接器，您必須使用 AD FS 來進行註冊。 開啟 Windows PowerShell 並執行下列命令的 hello:<br>
    `C:\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`
    <center>![雲端](./media/multi-factor-authentication-get-started-adfs-w2k12/pshell.png)</center>
12. toouse 您新註冊的配接器，用來在 AD FS 中編輯 hello 通用驗證原則。 在 hello AD FS 管理主控台中，移 toohello**驗證原則**節點。 在 hello **multi-factor Authentication**區段中，按一下 hello**編輯**連結下一步 toohello**通用設定**> 一節。 在 hello**編輯全域驗證原則**視窗中，選取**Multi-factor Authentication**作為其他驗證方法，然後按一下**確定**。 hello 配接器會登錄為 WindowsAzureMultiFactorAuthentication。 重新啟動 hello 註冊 tootake 效果 hello AD FS 服務。

<center>![雲端](./media/multi-factor-authentication-get-started-adfs-w2k12/global.png)</center>

此時，Multi-factor Authentication Server 設定 toobe 與 AD FS 的其他驗證提供者 toouse。

## <a name="install-a-standalone-instance-of-hello-ad-fs-adapter-by-using-hello-web-service-sdk"></a>使用 hello Web 服務 SDK 安裝 hello AD FS 配接器的獨立執行個體
1. 安裝 Web 服務 SDK hello hello 執行 Multi-factor Authentication Server 的伺服器上。
2. 複製 hello 下列檔案從 hello \Program Files\Multi-Authentication Server 目錄 toohello 伺服器計劃 tooinstall hello AD FS 配接器：
   * MultiFactorAuthenticationAdfsAdapterSetup64.msi
   * Register-MultiFactorAuthenticationAdfsAdapter.ps1
   * Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
   * MultiFactorAuthenticationAdfsAdapter.config
3. 執行 hello MultiFactorAuthenticationAdfsAdapterSetup64.msi 安裝檔案。
4. 在 hello Multi-factor Authentication AD FS 配接器安裝程式中，按一下 **下一步**toostart hello 安裝。
5. 按一下**關閉**hello 安裝完成時。

## <a name="edit-hello-multifactorauthenticationadfsadapterconfig-file"></a>編輯 hello MultiFactorAuthenticationAdfsAdapter.config 檔案
請遵循這些步驟 tooedit hello MultiFactorAuthenticationAdfsAdapter.config 檔案：

1. 設定 hello **UseWebServiceSdk**節點太**true**。  
2. 設定 hello 值**WebServiceSdkUrl** toohello hello Multi-factor Authentication Web 服務 SDK URL。 例如： *https://contoso.com/&lt;certificatename&gt;/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx*，其中*certificatename* hello 您的憑證名稱。  
3. 編輯 hello Register-multifactorauthenticationadfsadapter.ps1 指令碼，藉由新增*-ConfigurationFilePath&lt;路徑&gt;* toohello 結尾 hello`Register-AdfsAuthenticationProvider`命令，其中 *&lt;路徑&gt;* hello 完整路徑 toohello MultiFactorAuthenticationAdfsAdapter.config 檔案。

### <a name="configure-hello-web-service-sdk-with-a-username-and-password"></a>使用使用者名稱和密碼設定 Web 服務 SDK hello
有兩個選項，以設定 Web 服務 SDK hello。 hello 第一個是使用者名稱和密碼，hello 第二個用戶端憑證。 依照下列步驟進行 hello 第一個選項，或跳 hello 第二個。  

1. 設定 hello 值**WebServiceSdkUsername** tooan 帳戶 hello PhoneFactor Admins 安全性群組的成員。 使用 hello&lt;網域&gt;&#92;&lt;使用者名稱&gt;格式。  
2. 設定 hello 值**webservicesdkpassword 設定**toohello 適當的帳戶密碼。

### <a name="configure-hello-web-service-sdk-with-a-client-certificate"></a>設定用戶端憑證的 hello Web 服務 SDK
如果您不想 toouse 使用者名稱和密碼，請依照下列用戶端憑證與這些步驟 tooconfigure hello Web 服務 SDK。

1. 從執行 hello Web 服務 SDK 的 hello 伺服器憑證授權單位取得用戶端憑證。 了解如何太[取得用戶端憑證](https://technet.microsoft.com/library/cc770328.aspx)。  
2. 匯入 hello 用戶端憑證 toohello 本機電腦個人憑證存放區執行 hello Web 服務 SDK 的 hello 伺服器上。 請確定該 hello 憑證授權單位的公開憑證位於受信任的根憑證的憑證存放區。  
3. 匯出 hello 用戶端憑證 tooa.pfx 檔案的 hello 公用和私用的金鑰。  
4. Hello 公開金鑰 Base64 格式 tooa.cer 檔案中的匯出。  
5. 在 [伺服器管理員] 中，確認已安裝該 hello 網頁伺服器 (IIS) \Web Server\Security\IIS 用戶端憑證對應驗證功能。 如果未安裝，請選取**新增角色及功能**tooadd 這項功能。  
6. 在 [IIS 管理員] 中，按兩下**組態編輯器**hello 網站中的包含 hello Web 服務 SDK 虛擬目錄。 它是重要的 tooselect hello 網站，而非 hello 虛擬目錄。  
7. 移 toohello **system.webServer/security/authentication/iisClientCertificateMappingAuthentication** > 一節。  
8. 集合也啟用**true**。  
9. 將 onetoonecertificatemappingsenabled 設定太**true**。  
10. 按一下 hello **...**按鈕下一步 toooneToOneMappings，，然後按一下hello**新增**連結。  
11. 開啟您稍早匯出的 hello Base64.cer 檔案。 移除 *-----BEGIN CERTIFICATE-----*、*-----END CERTIFICATE-----*，以及任何分行符號。 將複製 hello 產生的字串。  
12. 設定憑證 toohello 字串 hello 前面步驟中複製。  
13. 集合也啟用**true**。  
14. 設定使用者名稱 tooan 帳戶 hello PhoneFactor Admins 安全性群組的成員。 使用 hello&lt;網域&gt;&#92;&lt;使用者名稱&gt;格式。  
15. 設定 hello 密碼 toohello 適當的帳戶密碼，然後關閉 設定編輯器。  
16. 按一下 hello**套用**連結。  
17. 在 hello Web 服務 SDK 虛擬目錄中，按兩下**驗證**。  
18. 請確認 ASP.NET 模擬與基本驗證已設定太**啟用**，而且其他所有項目也設定太**已停用**。  
19. 在 hello Web 服務 SDK 虛擬目錄中，按兩下**SSL 設定**。  
20. 設定用戶端憑證太**接受**，然後按一下**套用**。  
21. 將匯出執行 hello AD FS 配接器的較早 toohello 伺服器 hello.pfx 檔案複製。  
22. 匯入 hello.pfx 檔案 toohello 本機電腦個人憑證存放區。  
23. 以滑鼠右鍵按一下並選取**管理私密金鑰**，，然後授與讀取權限 toohello 帳戶 toosign 用於 toohello AD FS 服務。  
24. 從 hello 開啟 hello 用戶端憑證並複製 hello 指紋**詳細資料** 索引標籤。  
25. 在 hello MultiFactorAuthenticationAdfsAdapter.config 檔案中，設定**WebServiceSdkCertificateThumbprint** toohello 字串 hello 上一個步驟中複製。  

最後，tooregister hello 配接器執行 hello \Program Files\Multi-因素 Authentication Server\register-multifactorauthenticationadfsadapter.ps1 指令碼在 PowerShell 中的。 hello 配接器會登錄為 WindowsAzureMultiFactorAuthentication。 重新啟動 hello 註冊 tootake 效果 hello AD FS 服務。

## <a name="secure-azure-ad-resources-using-ad-fs"></a>使用 AD FS 保護 Azure AD 資源
toosecure 您雲端的資源，設定宣告規則，讓使用者執行雙步驟驗證成功時，Active Directory Federation Services 會發出 hello multipleauthn 宣告。 這個宣告會傳遞 tooAzure AD 上。 請遵循此程序 toowalk，透過 hello 步驟：

1. 開啟 [AD FS 管理]。
2. Hello 左側選取**信賴憑證者信任**。
3. 以滑鼠右鍵按一下 [Microsoft Office 365 身分識別平台]，然後選取 [編輯宣告規則...]

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. 在 [發佈轉換規則] 上，按一下 [新增規則]

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. 在 hello 新增轉換宣告規則精靈中，選取**傳遞或篩選傳入宣告**從 hello 下拉式清單，然後按一下 **下一步**。

   ![雲端](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. 指定規則的名稱。
7. 選取**驗證方法參考**為 hello 傳入宣告類型。
8. 選取 [傳遞所有宣告值]。
    ![新增轉換宣告規則精靈](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. 按一下 [完成] 。 關閉 hello AD FS 管理主控台。

## <a name="related-topics"></a>相關主題
如需疑難排解說明，請參閱 hello [Azure Multi-factor Authentication 常見問題集](multi-factor-authentication-faq.md)
