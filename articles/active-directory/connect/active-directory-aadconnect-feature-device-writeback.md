---
title: "Azure AD Connect：啟用裝置回寫 | Microsoft Docs"
description: "此文件詳細資料時，如何使用 Azure AD Connect tooenable 裝置回寫"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect：啟用裝置回寫
> [!NOTE]
> 用於裝置回寫需要訂用帳戶 tooAzure AD Premium。
> 
> 

下列文件的 hello 提供有關在 Azure AD Connect tooenable hello 裝置回寫功能的方式。 裝置回寫用於下列案例的 hello:

* 啟用條件式存取，根據裝置 tooADFS (2012 R2 或更高版本) 受保護的應用程式 （信賴憑證者信任）。

這會提供額外的安全性，並只 tootrusted 裝置授與存取 tooapplications 的保證。 如需條件式存取的詳細資訊，請參閱[使用條件式存取管理風險](../active-directory-conditional-access.md)和[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](../active-directory-conditional-access-automatic-device-registration-setup.md)。

> [!IMPORTANT]
> <li>裝置必須位於相同樹系為 hello 使用者 hello。 裝置必須重新寫入 tooa 單一樹系，因為這項功能目前不支援使用多個使用者樹系的部署。</li>
> <li>只有一個裝置註冊設定的物件可以加入 toohello 在內部部署 Active Directory 樹系。 這項功能與不相容的拓樸其中 hello 內部部署 Active Directory 是已同步處理的 toomultiple Azure AD 目錄。</li>> 

## <a name="part-1-install-azure-ad-connect"></a>第 1 部分：安裝 Azure AD Connect
1. 使用自訂或快速設定安裝 Azure AD Connect。 Microsoft 建議 toostart 與所有使用者和群組已順利同步處理之前啟用裝置回寫。

## <a name="part-2-prepare-active-directory"></a>第 2 部分：準備 Active Directory
使用下列步驟 tooprepare 使用於裝置回寫的 hello。

1. 從已安裝 Azure AD Connect 的 hello 機器，請在提升權限模式下啟動 PowerShell。
2. 如果未安裝 hello Active Directory PowerShell 模組，使用安裝 hello 下列命令：
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. 如果未安裝 hello Azure Active Directory PowerShell 模組，請下載並安裝從[Azure Active Directory 的 Windows PowerShell 模組 （64 位元版本）](http://go.microsoft.com/fwlink/p/?linkid=236297)。 此元件具有相依性 hello 登入小幫手，它會隨 Azure AD Connect。
4. 使用企業系統管理員認證，執行下列命令的 hello，然後結束 [PowerShell。
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

企業系統管理員認證是必要的因為所需的變更 toohello 組態命名空間。 網域系統管理員沒有足夠的權限。

![啟用裝置回寫的 Powershell](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Description:

* 如果尚未存在，請在 CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn] 下方建立並設定新的容器和物件。
* 如果尚未存在，請在 CN=RegisteredDevices,[domain-dn] 下方建立並設定新的容器和物件。 將會在此容器中建立裝置物件。
* 設定 hello Azure AD 連接器帳戶，請在您的 Active Directory toomanage 裝置必要的權限。
* 如果即使在多個樹系上安裝 Azure AD Connect，只需要 toorun 上有一個樹系。

參數：

* DomainName：將建立裝置物件的 Active Directory 網域。 附註：指定的 Active Directory 樹系的所有裝置都會在單一網域中建立。
* AdConnectorAccount: Hello 目錄中的 Azure AD Connect toomanage 物件將會使用 Active Directory 帳戶。 這是使用 Azure AD Connect 同步處理 tooconnect tooAD hello 帳戶。 如果您使用快速設定安裝，它就會是加上 MSOL_ hello 帳戶。

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>第 3 部分：在 Azure AD Connect 中啟用裝置回寫功能
使用下列程序 tooenable 裝置回寫，在 Azure AD Connect 的 hello。

1. 再次執行 hello 安裝精靈。 選取**自訂同步處理選項**hello 其他工作的頁面上，按一下 [**下一步**。
   ![自訂安裝自訂同步處理選項](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. 在 hello 選擇性功能] 頁面上，裝置回寫將不再會變成灰色。請注意，是否 hello Azure AD Connect 的準備步驟尚未完成裝置回寫將會以灰色顯示出 hello 選擇性功能] 頁面中。 核取 hello 用於裝置回寫] 方塊，按一下**下一步**。 如果仍然已停用 hello 核取方塊，請參閱 hello[疑難排解 > 一節](#the-writeback-checkbox-is-still-disabled)。
   ![自訂安裝裝置回寫可選功能](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. 在 hello 回寫頁面上，您會看到 hello 提供網域以 hello 預設裝置回寫的樹系。
   ![自訂安全裝置回寫樹系](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. 完成安裝 hello hello 精靈而不變更其他設定。 如有需要請參閱太[的 Azure AD Connect 自訂安裝。](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>啟用條件式存取
此案例中所提供的詳細的指示 tooenable[設定使用 Azure Active Directory 裝置註冊的內部部署條件式存取](../active-directory-conditional-access-automatic-device-registration-setup.md)。

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>確認裝置已同步處理的 tooActive 目錄
裝置回寫現在應該正常運作。 請注意，就可以在裝置物件 toobe 寫回 tooAD too3 小時。  您的裝置會正常運作，同步 tooverify hello 後完成 hello 同步處理規則：

1. 啟動 Active Directory 管理中心。
2. 展開 RegisteredDevices，hello 正在同盟的網域內。
   ![Active Directory 管理中心已註冊的裝置](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. 此處會列出目前已註冊的裝置。
   ![Active Directory 管理中心已註冊的裝置清單](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>疑難排解
### <a name="hello-writeback-checkbox-is-still-disabled"></a>仍然停用 hello 回寫] 核取方塊
如果 hello 核取方塊，即使您已依照 hello 上述步驟，未啟用裝置回寫 hello 下列步驟將引導您完成哪些 hello 安裝精靈正在驗證啟用 hello 方塊之前。

首先：

* 確定至少有一個樹系具備 Windows Server 2012R2。 hello 裝置物件型別必須要有。
* Hello 安裝精靈已在執行中，如果任何變更將無法偵測。 在此情況下，完成 hello 安裝精靈，然後再次執行。
* 請確定您提供 hello 初始化指令碼中的 hello 帳戶是實際 hello 正確的使用者使用 hello Active Directory 連接器。 tooverify，請遵循下列步驟：
  * 從 hello 開始] 功能表開啟**同步處理服務**。
  * 開啟 hello**連接器**] 索引標籤。
  * 類型為 Active Directory 網域服務尋找 hello 連接器並選取它。
  * 選取 [動作] 下方的 [屬性]。
  * 跳過**連接 tooActive Directory 樹系**。 請確認此畫面相符 hello 提供帳戶 toohello 指令碼中指定該 hello 網域和使用者名稱。
    ![Sync Service Manager 中的連接器帳戶](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

確認 Active Directory 中的組態：

* 請確認該裝置註冊服務位於以下 hello 位置中的 hello (CN = DeviceRegistrationService，CN = 裝置註冊服務，CN = Device Registration Configuration，CN = Services，CN = Configuration) 下設定命名內容。

![疑難排解，組態命名空間中的 DeviceRegistrationService](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* 確認有只有一個組態物件藉由搜尋 hello 組態命名空間。 如果有一個以上，刪除 hello 重複項目。

![疑難排解，請搜尋 hello 重複物件](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* 在 [hello 裝置註冊服務物件，請確定 hello 屬性 Msds-primary-computer DeviceLocation 存在且具有值。 查閱此位置，請確定它存在於與 hello objectType Msds-primary-computer DeviceContainer。

![疑難排解，msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![疑難排解，RegisteredDevices 物件類別](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* 請確認 hello 所使用帳戶 hello Active Directory 連接器 hello 上一個步驟所找到的 hello 註冊的裝置容器上具有必要權限。 這是預期的 hello 這個容器上的權限：

![疑難排解，驗證容器上的權限](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* 確認 hello Active Directory 帳戶擁有權限 hello CN = Device Registration Configuration，CN = Services，CN = 組態物件。

![疑難排解，，驗證裝置註冊組態的權限](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>其他資訊
* [使用條件式存取管理風險](../active-directory-conditional-access.md)
* [使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。

