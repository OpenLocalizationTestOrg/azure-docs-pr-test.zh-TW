---
title: "使用 Azure Active Directory 裝置註冊的內部部署條件式存取 aaaSetting |Microsoft 文件"
description: "逐步指南 tooenabling 條件式存取 tooon 內部部署應用程式使用 Windows Server 2012 R2 中 Active Directory Federation Services (AD FS)。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>使用 Azure Active Directory 裝置註冊來設定內部部署條件式存取
當您需要使用者 tooworkplace 聯結其個人裝置 toohello Azure Active Directory (Azure AD) 裝置註冊服務時，他們的裝置可以標示為已知的 tooyour 組織。 以下是用於 Windows Server 2012 R2 中使用 Active Directory Federation Services (AD FS) 來啟用條件式存取 tooon 內部部署應用程式的逐步指南。

> [!NOTE]
> 使用在 Azure Active Directory 裝置註冊服務條件式存取原則中註冊的裝置時，需要有 Office 365 授權或 Azure AD Premium 授權。 這些包括內部部署資源中的 AD FS 所強制執行的原則。
> 
> 如需在內部部署資源的 hello 條件式存取案例的詳細資訊，請參閱[tooworkplace 從任何裝置加入 SSO 和無縫式次要因素驗證，跨公司應用程式](https://technet.microsoft.com/library/dn280945.aspx)。

這些功能是可用 toocustomers 購買 Azure Active Directory Premium 授權。

## <a name="supported-devices"></a>支援的裝置
* 已加入網域的 Windows 7 裝置
* 個人和已加入網域的 Windows 8.1 裝置
* iOS 6 和更新版本的 hello Safari 瀏覽器
* Android 4.0 或更新版本、Samsung GS3 或更新的手機、Samsung Note 2 或更新的平板電腦

## <a name="scenario-prerequisites"></a>案例必要條件
* 訂用帳戶 tooOffice 365 或 Azure Active Directory Premium
* Azure Active Directory 租用戶
* Windows Server Active Directory (Windows Server 2008 或更新版本)
* Windows Server 2012 R2 中更新的結構描述
* Azure Active Directory Premium 的授權
* Windows Server 2012 R2 Federation Services，設定 SSO tooAzure AD
* Windows Server 2012 R2 Web 應用程式 Proxy 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(下載 Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* 已驗證的網域

## <a name="known-issues-in-this-release"></a>此版本已知的問題
* 裝置型條件式存取原則需要裝置物件回寫 tooActive 從 Azure Active Directory 的目錄。 就可以在裝置物件 toobe 寫回目錄 tooActive toothree 小時。
* iOS 7 裝置一律會在用戶端憑證驗證期間提示 hello 使用者 tooselect 憑證。
* iOS 8.3 之前的某些 iOS 8 版本無法運作。

## <a name="scenario-assumptions"></a>案例假設
此案例假設您有一個由 Azure AD 租用戶與內部部署 Active Directory 所組成的混合式環境。 這些租用戶應該以 Azure AD Connect 連接、具有已驗證的網域，以及具有用來進行 SSO 的 AD FS。 使用下列檢查清單 toohelp 您設定根據 toohello 需求環境的 hello。

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>檢查清單︰條件式存取案例的必要條件
將 Azure AD 租用戶與內部部署 Active Directory 執行個體連接。

## <a name="configure-azure-active-directory-device-registration-service"></a>設定 Azure Active Directory 裝置註冊服務
使用此指南 toodeploy 並設定為您的組織 hello Azure Active Directory 裝置註冊服務。

本指南假設您已設定 Windows Server Active Directory，而訂閱 tooMicrosoft Azure Active Directory。 請參閱稍早所述的 hello 必要條件。

租用戶 toodeploy hello Azure Active Directory 與 Azure Active Directory 裝置註冊服務，因此這個 hello 下列檢查清單順序中的 hello 完成工作。 當參考連結將您導向 tooa 觀念性主題時，傳回 toothis 檢查清單之後，因此，您可以繼續執行 hello 剩餘的工作。 部分工作包括案例驗證步驟，可協助您確認是否已成功完成 hello 步驟。

## <a name="part-1-enable-azure-active-directory-device-registration"></a>第 1 部分：啟用 Azure Active Directory 裝置註冊
Hello 檢查清單 tooenable 中的 hello 步驟，並設定 hello Azure Active Directory 裝置註冊服務。

| Task | 參考 | 
| --- | --- |
| 可讓您 Azure Active Directory 租用戶 tooallow 裝置 toojoin hello 工作地點中的裝置註冊。 根據預設，Azure Multi-factor Authentication 不會對 hello 服務啟用。 不過，建議您在註冊裝置時使用 Multi-Factor Authentication。 在 Active Directory 註冊服務中啟用 Multi-Factor Authentication 之前，請確定已為 Multi-Factor Authentication 提供者設定 AD FS。 |[啟用 Azure Active Directory 裝置註冊](active-directory-device-registration-get-started.md)| 
|裝置透過尋找已知的 DNS 記錄來探索您的 Azure Active Directory 裝置註冊服務。 請設定您的公司 DNS，以便讓裝置探索您的 Azure Active Directory 裝置註冊服務。 |[設定 Azure Active Directory 裝置註冊探索](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>第 2 部分：部署和設定 Windows Server 2012 R2 Active Directory Federation Services，以及設定與 Azure AD 的同盟關係

| 工作 | 參考 |
| --- | --- |
| 將 Active Directory 網域服務部署的 hello Windows Server 2012 R2 結構描述延伸模組。 您不需要 tooupgrade 任何您的網域控制站 tooWindows Server 2012 R2。 hello 架構升級為 hello 唯一的需求。 |[升級您的 Active Directory Domain Services 結構描述](#upgrade-your-active-directory-domain-services-schema) |
| 裝置透過尋找已知的 DNS 記錄來探索您的 Azure Active Directory 裝置註冊服務。 請設定您的公司 DNS，以便讓裝置探索您的 Azure Active Directory 裝置註冊服務。 |[準備您的 Active Directory 支援裝置](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>第 3 部分：在 Azure AD 中啟用裝置回寫
| 工作 | 參考 |
| --- | --- |
| 完成「在 Azure AD Connect 中啟用裝置回寫」的第 2 部分。 之後您會完成它傳回 toothis 指南。 |[在 Azure AD Connect 中啟用裝置回寫](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[選擇性] 第 4 部分：啟用 Multi-Factor Authentication
我們強烈建議您設定一個 hello 幾個選項用於多重要素驗證。 如果您想 toorequire Multi-factor Authentication，請參閱[為您選擇 hello Multi-factor Authentication 的安全性解決方案](../multi-factor-authentication/multi-factor-authentication-get-started.md)。 它包含一個描述每個解決方案，並連結 toohelp hello 解決方案，您所選擇的設定。

## <a name="part-5-verification"></a>第 5 部分：驗證
hello 部署現在已完成，以及您可以嘗試部分案例。 使用下列連結 tooexperiment 與 hello 服務並熟悉其功能的 hello。

| Task | 參考 |
| --- | --- |
| 使用 Azure Active Directory 裝置註冊服務，將某些裝置 tooyour 工作地點。 您可以將 iOS、Windows 及 Android 裝置加入。 |[將使用 Azure Active Directory 裝置註冊服務的裝置 tooyour 工作場所聯結](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| 檢視和啟用或停用已註冊的裝置使用 hello 管理員入口網站。 在這項工作，您可以使用 hello 管理員入口網站來檢視已註冊的裝置。 |[Azure Active Directory 裝置註冊服務概觀](active-directory-device-registration-get-started.md) |
| 請確認該裝置物件寫回從 Azure Active Directory tooWindows Server Active Directory。 |[請確認已註冊的裝置寫回 tooActive 目錄](#verify-registered-devices-are-written-back-to-active-directory) |
| 現在使用者可以註冊其裝置，您可以在 AD FS 中建立僅允許已註冊裝置的應用程式存取原則。 在這項工作中，您需建立應用程式存取規則和自訂拒絕存取訊息。 |[建立應用程式存取原則和自訂的拒絕存取訊息](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>整合 Azure Active Directory 與內部部署 Active Directory
此步驟可協助您使用 Azure AD Connect 將 Azure AD 租用戶與內部部署 Active Directory 整合。 雖然 hello 步驟可在 hello Azure 傳統入口網站中，記下的這一節中所列的任何特殊指示。

1. Toohello Azure 傳統入口網站使用的登入 Azure AD 中為全域管理員帳戶。
2. 在 [hello] 左窗格中，選取 [ **Active Directory**。
3. 在 [hello**目錄**索引標籤上，選取您的目錄。
4. 選取 hello**目錄整合**] 索引標籤。
5. 在 [hello**部署和管理**區段中，請依照下列步驟 1 到 3 toointegrate Azure Active Directory 與內部部署目錄。
   
   1. 新增網域。
   2. 安裝及執行 Azure AD Connect 使用 hello 指示[的 Azure AD Connect 自訂安裝](connect/active-directory-aadconnect-get-started-custom.md)。
   3. 驗證及管理目錄同步作業。此步驟中可取得單一登入的指示。
   
   此外，依照[自訂 Azure AD Connect 安裝](connect/active-directory-aadconnect-get-started-custom.md)所述，設定與 AD FS 的同盟。

## <a name="upgrade-your-active-directory-domain-services-schema"></a>升級您的 Active Directory 網域服務結構描述
> [!NOTE]
> 升級您的 Active Directory 結構描述之後，就無法回復 hello 程序。 我們建議您先在測試環境中執行 hello 升級。
> 

1. 登入具有企業系統管理員和架構系統管理員權限的帳戶與 tooyour 網域控制站。
2. 複製 hello **[media] \support\adprep** Active Directory 網域控制站的目錄和子目錄 tooone (其中**[media]** hello 路徑 toohello Windows Server 2012 R2 安裝媒體).
4. 從命令提示字元中，移 toohello **adprep**目錄中，而且執行**adprep.exe /forestprep**。 請遵循 hello 畫面上的指示 toocomplete hello 結構描述升級。

## <a name="prepare-your-active-directory-toosupport-devices"></a>準備您的 Active Directory toosupport 裝置
> [!NOTE]
> 這是一次性的操作，您必須執行 tooprepare Active Directory 樹系 toosupport 裝置。 toocomplete 此程序，您必須登入企業系統管理員權限，而且您的 Active Directory 樹系必須具有 hello Windows Server 2012 R2 結構描述。
> 


### <a name="prepare-your-active-directory-forest"></a>準備您的 Active Directory 樹系
1. 在您的同盟伺服器上，開啟 Windows PowerShell 命令視窗，然後輸入 **Initialize-ADDeviceRegistration**。 
2. 當系統提示您輸入**ServiceAccountName**，輸入 hello hello hello 服務帳戶當做 AD fs 的服務帳戶名稱。 如果 gMSA 帳戶，輸入 hello 帳戶在 hello **domain\accountname$**格式。 網域帳戶，使用 [hello 格式**domain\accountname**。

### <a name="enable-device-authentication-in-ad-fs"></a>在 AD FS 中啟用裝置驗證
1. 在您的同盟伺服器上開啟 [hello AD FS 管理主控台，並移過**AD FS** > **驗證原則**。
2. 在 [hello**動作**窗格中，選取**編輯全域主要驗證**。
3. 勾選 [啟用裝置驗證]，然後選取 [確定]。
4. AD FS 預設會定期從 Active Directory 移除未使用的裝置。 使用 Azure Active Directory 裝置註冊服務時，請停用此工作，以便在 Azure 中管理裝置。

### <a name="disable-unused-device-cleanup"></a>停用未使用的裝置清除
在您的同盟伺服器上，開啟 Windows PowerShell 命令視窗，然後輸入 **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**。

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>準備 Azure AD Connect 以便裝置回寫
完成第 1 部分：準備 Azure AD Connect。

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>將裝置 tooyour 工作地方聯結使用 Azure Active Directory 裝置註冊服務

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>使用 Azure Active Directory 裝置註冊來加入 iOS 裝置
Azure Active Directory 裝置註冊使用 hello Over-the-Air Profile 註冊程序適用於 iOS 裝置。 Hello 使用者連接與 Safari toohello 設定檔註冊 URL 時，就會開始此程序。 hello URL 格式如下所示：

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

在此情況下，`yourdomainname`是 hello 您設定與 Azure Active Directory 的網域名稱。 例如，如果您的網域名稱為 contoso.com，hello URL 如下所示：

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

有許多不同的方式 toocommunicate 此 URL tooyour 使用者。 例如，其中一個建議方式是在 AD FS 的自訂應用程式拒絕存取訊息中發佈此 URL。 這項資訊會在 hello 後續章節中說明[建立應用程式存取原則和自訂存取拒絕訊息](#create-an-application-access-policy-and-custom-access-denied-message)。

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>使用 Azure Active Directory 裝置註冊來加入 Windows 8.1 裝置
1. 在 Windows 8.1 裝置上，選取 [電腦設定] > [網路] > [工作場所]。
2. 以 UPN 格式輸入您的使用者名稱；例如 **dan@contoso.com**。
3. 選取 [加入] 。
4. 出現提示時，使用您的認證登入。 hello 裝置隨即加入。

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>使用 Azure Active Directory 裝置註冊來加入 Windows 7 裝置
tooregister Windows 7 加入網域的裝置，您需要 toodeploy hello 裝置註冊軟體套件。 hello 軟體封裝稱為工作地方聯結的 Windows 7，而且可用下載 hello [Microsoft Connect 網站](https://connect.microsoft.com/site1164)。 

中的指引來說明如何 toouse hello 封裝可用[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>確認的已註冊的裝置寫回 tooActive 目錄
您可以檢視並確認該裝置物件已寫回 tooyour Active Directory 使用 LDP.exe 或 ADSI 編輯。 兩者都提供 hello Active Directory 系統管理員工具。

依照預設，從 Azure Active Directory 寫回裝置物件放在 hello 相同 AD FS 陣列的網域。

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>建立應用程式存取原則和自訂的拒絕存取訊息
請考慮下列案例中的 hello： 您建立的應用程式中 AD FS 信賴憑證者信任，並設定發行授權規則，可讓已註冊的裝置。 已註冊的裝置現在允許 tooaccess hello 應用程式。 

toomake 輕鬆使用者 toogain 存取 toohello 應用程式，您設定自訂的拒絕存取訊息，其中包含有關如何 toojoin 他們的裝置。 現在您的使用者有流暢的方式 tooregister 他們的裝置讓他們可以存取應用程式。

hello 下列步驟說明如何 tooimplement 這種情況。

> [!NOTE]
> 本節假設您已在 AD FS 中為您的應用程式設定信賴憑證者信任。
> 

1. 開啟 hello AD FS MMC 工具，然後選取**AD FS** > **信任關係** > **信賴憑證者信任**。
2. 找出 hello 應用程式 toowhich 套用此新存取規則。 Hello 應用程式，以滑鼠右鍵按一下，然後選取**編輯宣告規則**。
3. 選取 hello**發佈授權規則**索引標籤，然後選取**加入規則**。
4. 從 hello**宣告規則**範本下拉式清單中，選取**拒絕使用者根據傳入宣告允許或**。 然後，選取 [下一步]。
5. 在 [hello**宣告規則名稱**欄位中，輸入**允許已註冊的裝置存取**。
6. 從 hello**傳入宣告類型**下拉式清單中，選取**是已註冊的使用者**。
7. 在 [hello**連入宣告值**欄位中，輸入**true**。
8. 選取 hello**具有這個傳入宣告允許存取 toousers**選項按鈕。
9. 選取 [完成]，然後選取 [套用]。
10. 移除任何比您所建立的 hello 規則更寬鬆的規則。 例如，移除 hello 預設規則**允許存取 tooall 使用者**。

現在已設定的 tooallow 存取 hello 使用者來自其已註冊，並加入 toohello 工作地點的裝置時，才，就會是您的應用程式。 如需更進階的存取原則，請參閱[針對敏感性應用程式使用額外的 Multi-Factor Authentication 來管理風險](https://technet.microsoft.com/library/dn280949.aspx)。

接下來，您將為應用程式設定自訂的錯誤訊息。 hello 錯誤訊息可讓使用者知道，他們必須先將其裝置 toohello 工作場所，才能存取 hello 應用程式。 您可以使用自訂 HTML 和 PowerShell 來建立自訂的應用程式拒絕存取訊息。

在您的同盟伺服器上開啟 PowerShell 命令視窗中，，然後輸入下列命令的 hello。 取代項目，則特定 tooyour 系統部份 hello 命令：

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
在您可以存取此應用程式之前，您必須註冊您的裝置。

**如果您使用 iOS 裝置，選取此連結 toojoin 裝置**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

將此 iOS 裝置 tooyour 工作地點。

如果您使用 Windows 8.1 裝置，則可以選取 [電腦設定]> [網路] > [工作場所] 來加入您的裝置。

在上述命令，hello**信賴憑證者信任名稱**是 hello AD FS 中的應用程式的信賴憑證者信任物件名稱。
和**yourdomain.com**是 hello 與 Azure Active Directory (例如，contoso.com)，您已設定的網域名稱。
是任何分行符號 （如果有的話） 從 hello HTML 內容，您將傳遞 toohello 確定 tooremove **Set-adfsrelyingpartywebcontent** cmdlet。

現在當使用者從 hello Azure Active Directory 裝置註冊服務未註冊的裝置存取您的應用程式，他們會看到一個看起來類似 toohello 下列螢幕擷取畫面的頁面。

![使用者尚未向 Azure AD 註冊其裝置時的錯誤螢幕擷取畫面](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


