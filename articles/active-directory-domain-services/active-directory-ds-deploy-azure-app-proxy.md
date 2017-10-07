---
title: "Azure Active Directory 網域服務︰部署 Azure Active Directory 應用程式 Proxy | Microsoft Docs"
description: "在 Active Directory Domain Services 受管理網域上使用 Azure AD 應用程式"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>在 Azure AD 網域服務受管理網域上部署 Azure AD 應用程式
Azure Active Directory (AD) 應用程式 Proxy 可協助您支援遠端工作者所發佈在內部部署應用程式 toobe hello 透過存取網際網路。 使用 Azure AD 網域服務中，您可以執行內部 tooAzure 基礎結構服務現在增益集和-shift 舊版應用程式。 然後，您可以發行這些應用程式使用 Azure AD Application Proxy，您組織中的 tooprovide 安全遠端存取 toousers hello。

如果您是新 toohello Azure AD Application Proxy，深入了解這項功能以 hello 下列文章：[如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](../active-directory/active-directory-application-proxy-get-started.md)。


## <a name="before-you-begin"></a>開始之前
本文所列 tooperform hello 工作，您必須：

1. 有效的 **Azure 訂用帳戶**。
2. **Azure AD 目錄** - 與內部部署目錄或僅限雲端的目錄同步處理。
3. **Azure AD Basic 或 Premium 授權**是必要的 toouse hello Azure AD Application Proxy。
4. **Azure AD 網域服務**必須啟用 hello Azure AD 目錄。 如果您尚未這樣做，請遵循 hello 中所述的所有 hello 工作[入門指南](active-directory-ds-getting-started.md)。

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>工作 1 - 針對您的 Azure AD 目錄啟用 Azure AD 應用程式 Proxy
執行下列步驟 tooenable hello Azure AD Application Proxy 為您的 Azure AD 目錄的 hello。

1. Hello 中的系統管理員身分登入[Azure 入口網站](http://portal.azure.com)。

2. 按一下**Azure Active Directory** toobring 向上 hello directory 概觀。 按一下 [企業應用程式]。

    ![選取 Azure AD 目錄](./media/app-proxy/app-proxy-enable-start.png)
3. 按一下 [應用程式 Proxy]。 如果您沒有 Azure AD Basic 或 Azure AD Premium 訂用帳戶，您會看到選項 tooenable 試用版。 切換**啟用應用程式 Proxy？**太**啟用**按一下**儲存**。

    ![啟用應用程式 Proxy](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload hello 連接器，請按一下 hello**連接器** 按鈕。

    ![下載連接器](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Hello 下載頁面上，接受 hello 授權條款及隱私權合約，並按一下 hello**下載** 按鈕。

    ![確認下載](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>工作 2-佈建已加入網域的 Windows 伺服器 toodeploy hello Azure AD 應用程式 Proxy 連接器
您需要已加入網域的 Windows Server 虛擬機器，您可以在其安裝 hello Azure AD 應用程式 Proxy 連接器。 根據發行的 hello 應用程式，您可以選擇 tooprovision hello 連接器安裝所在的多部伺服器。 這個部署選項為您提供更高的可用性，並協助處理更大量的驗證負載。

Hello 連接器的伺服器上佈建 hello 相同虛擬網路 （或連接/所以的虛擬網路），在您已啟用您 Azure AD 網域服務受管理的網域。 同樣地，hello 伺服器裝載 hello 您透過 hello 應用程式 Proxy 發佈的應用程式需要 toobe hello 上安裝相同的 Azure 虛擬網路。

tooprovision 連接器的伺服器，請遵循 hello 文章的標題中的 hello 工作[加入 Windows 虛擬機器 tooa 受管理的網域](active-directory-ds-admin-guide-join-windows-vm.md)。


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>工作 3-安裝和註冊 hello Azure AD 應用程式 Proxy 連接器
先前，您要佈建 Windows Server 虛擬機器，並加入 toohello 受管理的網域。 在這項工作，您將此虛擬機器上安裝 hello Azure AD 應用程式 Proxy 連接器。

1. 將複製 hello 連接器安裝封裝 toohello VM 安裝 hello Azure AD Web 應用程式 Proxy 連接器。

2. 執行**AADApplicationProxyConnectorInstaller.exe** hello 虛擬機器上。 接受 hello 軟體授權條款。

    ![接受安裝的條款](./media/app-proxy/app-proxy-install-connector-terms.png)
3. 在安裝期間，您必須提示的 tooregister hello hello 的 Azure AD 目錄的應用程式 Proxy 連接器。
    * 提供您的 **Azure AD 全域管理員認證**。 您的全域管理員租用戶可能與您的 Microsoft Azure 認證不同。
    * hello 系統管理員使用帳戶 tooregister hello 連接器必須屬於 toohello 相同的目錄啟用 hello 應用程式 Proxy 服務的位置。 例如，如果 hello 租用戶網域為 contoso.com，hello admin 應該是admin@contoso.com或任何其他有效的別名在該網域上。
    * 如果 IE 增強式安全性設定已開啟 hello 伺服器要在其中安裝 hello 連接器，hello 註冊畫面可能會封鎖。 tooallow 存取權，遵循 hello hello 錯誤訊息中的指示。 請確定已停用 [Internet Explorer 增強式安全性]。
    * 如果連接器註冊不成功，請參閱 [針對應用程式 Proxy 進行疑難排解](../active-directory/active-directory-application-proxy-troubleshoot.md)。

    ![安裝的連接器](./media/app-proxy/app-proxy-connector-installed.png)
4. tooensure hello 連接器正常執行，執行的 hello Azure AD 應用程式 Proxy 連接器疑難排解。 執行 hello 疑難排解之後，您應該看到成功的報表。

    ![疑難排解程式成功](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. 您應該會看到 Azure AD 目錄中的 hello 應用程式 proxy 頁面上所列的 hello 新安裝的連接器。

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> 您可以選擇多部伺服器上的 tooinstall 連接器 tooguarantee 驗證透過 hello Azure AD Application Proxy 發行應用程式的高可用性。 執行的 hello 上列 tooinstall hello 連接器，在其他伺服器聯結的 tooyour 受管理的網域上的相同的步驟。
>
>

## <a name="next-steps"></a>後續步驟
您擁有 hello Azure AD Application Proxy 設定，並且整合與您 Azure AD 網域服務受管理的網域。

* **移轉應用程式 tooAzure 虛擬機器：**增益 shift 您可以將應用程式從內部部署伺服器 tooAzure 虛擬機器聯結的 tooyour 受管理的網域。 這樣可協助您移除 hello 的內部部署執行伺服器上的基礎結構成本。

* **使用 Azure AD Application Proxy 發行應用程式：**發行應用程式使用 Azure AD Application Proxy hello Azure 虛擬機器上執行。 如需詳細資訊，請參閱[使用 Azure AD 應用程式 Proxy 發佈應用程式](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>部署附註 - 使用 Azure AD 應用程式 Proxy 發佈 IWA (整合式 Windows 驗證) 應用程式
啟用單一登入 tooyour 應用程式使用整合式 Windows 驗證 (IWA) 應用程式 Proxy 連接器權限授與 tooimpersonate 使用者，以及傳送和接收代表語彙基元。 設定 kerberos 限制委派 (KCD) hello 連接器 toogrant hello 所需的權限 tooaccess 上的資源 hello 受管理的網域。 使用受管理的網域上的 hello 資源型 KCD 機制，以提高安全性。


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>啟用 hello Azure AD 應用程式 Proxy 連接器的資源型 kerberos 限制委派
hello Azure 應用程式 Proxy 連接器應該進行 kerberos 限制委派 (KCD)，讓它可以模擬使用者上設定 hello 受管理的網域。 在 Azure AD Domain Services 受管理的網域上，您沒有網域系統管理員權限。 因此，**無法在受管理的網域上設定傳統帳戶層級 KCD**。

使用本[文章](active-directory-ds-enable-kcd.md)中所述的資源型 KCD。

> [!NOTE]
> 您需要 toobe 成員 hello ' AAD DC Administrators' 群組的 tooadminister hello 管理網域使用 AD PowerShell cmdlet。
>
>

將 hello Get-adcomputer PowerShell cmdlet tooretrieve hello 設定用於 hello 的 hello Azure AD 應用程式 Proxy 連接器安裝的電腦上。
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

之後，使用向上資源型 KCD hello Set-adcomputer cmdlet tooset hello 資源伺服器。
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

如果您已在受管理的網域部署多個應用程式 Proxy 連接器，您需要 tooconfigure 資源型 KCD 每個這類連接器執行個體。


## <a name="related-content"></a>相關內容
* [Azure AD Domain Services - 入門指南](active-directory-ds-getting-started.md)
* [在受管理的網域上設定 Kerberos 限制委派](active-directory-ds-enable-kcd.md)
* [Kerberos 限制委派概觀](https://technet.microsoft.com/library/jj553400.aspx)
