---
title: "aaaEnable Microsoft Windows Hello 企業版中組織 |Microsoft 文件"
description: "部署指示 tooenable Microsoft Passport 您組織中。"
services: active-directory
documentationcenter: 
keywords: "設定 Microsoft Passport、Microsoft Windows Hello 企業版部署"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>在組織中啟用 Microsoft Windows Hello 企業版
之後[連接 Windows 10 已加入網域的裝置與 Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md)，請勿遵循您組織中的 Microsoft Windows Hello 企業 tooenable hello:

1. 部署 System Center Configuration Manager  
2. 設定原則設定
3. 設定 hello 憑證設定檔  

## <a name="deploy-system-center-configuration-manager"></a>部署 System Center Configuration Manager
根據 Windows Hello 的商務索引鍵 toodeploy 使用者憑證，您需要 hello 下列：

* **System Center Configuration Manager 最新分支**-您需要 tooinstall 版本 1606年或更高。 如需詳細資訊，請參閱 hello [for System Center Configuration Manager 文件](https://technet.microsoft.com/library/mt346023.aspx)和[System Center Configuration Manager 小組部落格](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)。
* **公開金鑰基礎結構 (PKI)** -tooenable Microsoft Windows Hello 商務藉由使用使用者憑證，您必須具備 PKI。 如果您沒有其中一個，或您不想 toouse 它的使用者憑證，您可以部署新的網域控制站已建置 10551 （或更新版本） 安裝的 Windows Server 2016。 請依照下列步驟 hello 太[現有網域中安裝複本網域控制站](https://technet.microsoft.com/library/jj574134.aspx)或太[安裝新的 Active Directory 樹系中，如果您要建立新環境](https://technet.microsoft.com/library/jj574166)。 (hello Iso 可供下載[Signiant 媒體交換](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true)。)

## <a name="configure-policy-settings"></a>設定原則設定
tooconfigure hello Microsoft Windows Hello 的商務原則設定，您有兩個選項：

* Active Directory 中的群組原則 
* hello System Center Configuration Manager 

在 Active Directory 中的使用 「 群組原則是 hello 建議方法 tooconfigure Microsoft Windows Hello 的商務原則設定。 

使用 System Center Configuration Manager 是 hello 慣用方法，當您使用它 toodeploy 憑證。 此案例：

* 可確保與 hello 較新的部署案例的相容性
* 需要 Windows 10 版本 1607年或更佳的 hello 用戶端。

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>透過 Active Directory 中的群組原則設定 Microsoft Windows Hello 企業版
**步驟**：

1. 開啟 [伺服器管理員] 並瀏覽過**工具** > **群組原則管理**。
2. 從群組原則管理 瀏覽 toohello 對應您想要設定 Azure AD Join tooenable toohello 網域的網域節點。
3. 以滑鼠右鍵按一下 [群組原則物件]，選取 [新增]。 指定群組原則物件的名稱，例如「啟用 Windows Hello 企業版」。 按一下 [確定] 。
4. 以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯] 。
5. 瀏覽過**電腦設定** > **原則** > **系統管理範本** > **Windows元件** > **Windows Hello 企業**。
6. 以滑鼠右鍵按一下 [啟用 Windows Hello 企業版]，然後選取 [編輯]。
7. 選取 hello**啟用**選項按鈕，然後再按一下**套用**。 按一下 [確定] 。
8. 您現在可以將連結 hello 群組原則物件 tooa 您選擇的位置。 tooenable hello 組織連結 hello 群組原則 toohello 網域中，已加入網域的 Windows 10 裝置的所有此原則。 例如：
   * Active Directory 中將放置已加入網域的 Windows 10 電腦的特定組織單位 (OU)
   * 已加入網域且會向 Azure AD 自動註冊的 Windows 10 電腦所屬的特定安全性群組

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>使用 System Center Configuration Manager設定 Windows Hello 企業版
**步驟**：

1. 開啟 hello **System Center Configuration Manager**，然後瀏覽過**資產與相容性 > 相容性設定 > 公司資源存取 > 商務設定檔的 Windows Hello**。
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. 在 hello hello 上方的工具列中按一下**建立商務設定檔的 Windows Hello**。
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. 在 [hello**一般**] 對話方塊中，執行下列步驟的 hello:
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. 在 hello**名稱**文字方塊中，輸入您設定檔名稱，例如**WHfB 我的設定檔**。
   
    b. 按一下 [下一步] 。
4. 在 hello**支援的平台**對話方塊中，選取 hello 平台，必須具備此 Windows Hello，為商務設定檔，然後按一下**下一步**。
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. 在 [hello**設定**] 對話方塊中，執行下列步驟的 hello:
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. 對於 [設定 Windows Hello 企業版]，選取 [已啟用]。
   
    b. 對於 [使用信賴平台模組 (TPM)]，選取 [必要]。 
   
    c. 對於 [驗證方法]，選取 [憑證型]。
   
    d. 按一下 [下一步] 。
6. 在 hello**摘要** 對話方塊中，按一下 **下一步**。
7. 在 hello**完成** 對話方塊中，按一下 **關閉**。
8. 在 hello hello 上方的工具列中按一下**部署**。
   
    ![設定 Windows Hello 企業版](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>設定 hello 憑證設定檔
如果您在內部部署驗證使用憑證型驗證，您需要 tooconfigure 並部署憑證設定檔。 這項工作需要 tooset 設定 NDES 伺服器，在 hello System Center Configuration Manager 憑證登錄點站台角色。 如需詳細資訊，請參閱 hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx)。

1. 開啟 hello **System Center Configuration Manager**，然後瀏覽過**資產與相容性 > 相容性設定 > 公司資源存取 > 憑證設定檔**。
2. 選取一個含有智慧卡登入擴充金鑰使用方法 (EKU) 的範本。

在 hello**頁面 SCEP 註冊**頁面 hello 憑證設定檔，您需要 toochoose**安裝 tooPassport for Work 否則便失敗**為 hello**金鑰儲存提供者**。

## <a name="next-steps"></a>後續步驟
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [透過 Microsoft Passport 不需要密碼就能驗證身分識別](active-directory-azureadjoin-passport.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

