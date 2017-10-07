---
title: "aaaAzure MFA Server 升級 |Microsoft 文件"
description: "步驟和指引 tooupgrade hello Azure Multi-factor Authentication Server tooa 較新版本。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>升級 toohello 最新的 Azure Multi-factor Authentication Server

本文將引導您完成 hello 處理升級 Azure Multi-factor Authentication (MFA) Server v6.0 或更高版本。 如果您需要 tooupgrade hello PhoneFactor 代理程式的舊版本，請參閱太[升級 hello PhoneFactor Agent tooAzure Multi-factor Authentication Server](multi-factor-authentication-get-started-server-upgrade.md)。

如果您是從 v6.x 或較舊的 toov7.x 升級或更新版本時，所有元件會從.NET 2.0 too.NET 4.5 都變更。 所有元件也都需要 Microsoft Visual C++ 2015 可轉散發套件更新 1 或更新版本。 如果未安裝，hello MFA Server 安裝程式會安裝這些元件的兩個 hello x86 和 x64 版本。 如果不同伺服器上執行 hello 使用者入口網站和行動裝置應用程式 Web 服務，您需要 tooinstall 這些封裝之前升級這些元件。 您可以搜尋 hello 最新版 Microsoft Visual c + + 2015年可轉散發的 update 上 hello [Microsoft Download Center](https://www.microsoft.com/en-us/download/)。 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>安裝 Azure MFA Server hello 最新版本

1. 使用中的 hello 指示[下載 hello Azure Multi-factor Authentication Server](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello 最新版本的 Azure MFA Server hello。
2. 製作 hello MFA Server 資料檔案位於 C:\Program files\multi-factor Authentication 驗證 Server\Data\PhoneFactor.pfdata 主要的 MFA 伺服器上 （假設 hello 預設安裝位置） 的備份。
3. 如果您執行的高可用性的多部伺服器，變更 hello 驗證 toohello MFA Server，好讓它們停止將流量傳送 toohello 伺服器要升級的用戶端系統。 如果您使用的負載平衡器，MFA Server 移除 hello 負載平衡器、 執行 hello 升級，然後再加入 hello 伺服器回 hello 伺服陣列。
4. MFA 的每部伺服器上執行 hello 新的安裝程式。 第一次升級次級伺服器，因為他們可以讀取 hello 所複寫的 hello master 舊資料檔案。 

  您不需要 toouninstall 目前的 MFA 伺服器之前執行 hello 安裝程式。 hello 安裝程式會執行就地升級。 hello 安裝路徑從挑選 hello 登錄從 hello 先前的安裝，因此它會安裝在 hello 相同位置 (例如 C:\Program files\multi-factor Authentication Server)。 
  
5. 如果您是提示的 tooinstall Microsoft Visual c + + 2015年可轉散發套件的更新套件，接受 hello 提示。 這兩個 hello x86 和 x64 版本的 hello 封裝會安裝。
5. 如果您使用 hello Web 服務 SDK，系統會提示您 tooinstall hello 新的 Web 服務 SDK。 當您安裝 hello 新的 Web 服務 SDK，請確定該 hello 虛擬目錄名稱符合 hello 先前安裝的虛擬目錄 (例如，MultiFactorAuthWebServiceSdk)。
6. Hello 上重複步驟的所有次級伺服器。 升級 hello 部屬 toobe hello 新主機，然後升級 hello 舊的主要伺服器的其中一個。 

## <a name="upgrade-hello-user-portal"></a>升級 hello 使用者入口網站

1. 請 hello 的 hello 使用者入口網站安裝位置 (例如 C:\inetpub\wwwroot\MultiFactorAuth) 的虛擬目錄中的 hello web.config 檔案的備份。 如果任何變更時 toohello 預設佈景主題，請製作 hello App_Themes\Default 資料夾的備份。 它是較佳的 toocreate hello 預設資料夾的複本，並建立新的佈景主題，比 toochange hello 預設佈景主題。
2. 如果在同一部伺服器 hello 其他 MFA Server 元件，因為 hello 的 hello 執行 hello 使用者入口網站 MFA Server 安裝會提示您 tooupdate hello 使用者入口網站。 接受 hello 提示，並安裝 hello 使用者入口網站更新。 檢查該 hello 虛擬目錄名稱符合先前安裝的 hello 虛擬目錄 (例如，MultiFactorAuth)。
3. 如果 hello 使用者入口網站是在自己的伺服器上，複製 hello MultiFactorAuthenticationUserPortalSetup64.msi 檔案從 hello 安裝其中一個 hello MFA 伺服器的位置，並將它放置到 hello 使用者入口網站 web 伺服器。 執行 hello 安裝程式。 

  如果發生錯誤指出，"Microsoft Visual c + + 2015年可轉散發套件 Update 1 或更新版本為必要項，「 從下載並安裝 hello 最新的更新套件 hello [Microsoft Download Center](https://www.microsoft.com/download/)。 安裝這兩個 hello x86 和 x64 版本。

4. Hello 更新已安裝軟體的使用者入口網站之後，比較您在步驟 1 與 hello 新的 web.config 檔案中所做的 hello web.config 備份。 如果新的屬性不存在 hello 新 web.config 中，複製 hello 虛擬目錄 toooverwrite hello 新備份 web.config。 另一個選項是 toocopy/貼上 hello appSettings 值和 hello hello 備份 hello 新的 web.config 檔中的 Web 服務 SDK URL。

如果您有多部伺服器上的 hello 使用者入口網站時，重複在 hello 安裝。 


## <a name="upgrade-hello-mobile-app-web-service"></a>升級 hello Mobile App Web Service

1. 請 hello Mobile App Web Service 安裝位置 （例如，C:\inetpub\wwwroot\app 或 C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService） 處於 hello hello 虛擬目錄的 web.config 檔案的備份。
2. 從 hello 複製 hello MultiFactorAuthenticationMobileAppWebServiceSetup64.msi 檔案安裝的 hello MFA 伺服器的位置，並將它放置到 hello 行動裝置應用程式註冊的 web 伺服器。
3. 執行 hello 安裝程式。 

  如果發生錯誤，指出需要 Microsoft Visual c + + 2015年可轉散發套件 Update 1 或更新版本的下載並安裝 hello 最新的更新封裝從 hello [Microsoft Download Center](https://www.microsoft.com/download/)。 安裝這兩個 hello x86 和 x64 版本。

4. Hello 更新 Mobile App Web Service 軟體安裝之後，比較備份在步驟 1 與 hello 新的 web.config 檔案中的 hello web.config 檔案。 如果新的屬性不存在 hello 新 web.config 中，您可以將已儲存的 web.config 複製回 hello 虛擬目錄，並覆寫 hello 新。 另一個選項是 toocopy/貼上 hello appSettings 值和 hello hello 備份 hello 新的 web.config 檔中的 Web 服務 SDK URL。

如果您有多部伺服器上的 hello Mobile App Web Service 時，重複在 hello 安裝。 

## <a name="upgrade-hello-ad-fs-adapters"></a>升級 hello AD FS 配接器


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>如果 MFA 與 AD FS 不是在同一部伺服器上執行

只有當您將 Multi-Factor Authentication Server 與您的 AD FS 伺服器分開執行時，才適用這些指示。 如果這兩項服務上執行 hello 相同的伺服器，請略過本節並移 toohello 安裝步驟。 

1. 儲存已註冊於 AD FS 中的 hello MultiFactorAuthenticationAdfsAdapter.config 檔案的複本或匯出 hello 設定使用下列 PowerShell 命令的 hello: `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`。 hello 配接器名稱會是"WindowsAzureMultiFactorAuthentication"或"AzureMfaServerAuthentication"視 hello 先前安裝的版本而定。
2. 複製下列檔案從 hello MFA Server 安裝位置 toohello AD FS 伺服器 hello:

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. 編輯 hello Register-multifactorauthenticationadfsadapter.ps1 指令碼，藉由新增`-ConfigurationFilePath [path]`toohello 結尾 hello`Register-AdfsAuthenticationProvider`命令。 取代*[path]* hello 完整路徑 toohello MultiFactorAuthenticationAdfsAdapter.config 檔案或 hello 設定檔匯出 hello 上一個步驟中。 

  如果兩者相符 hello 舊組態檔，請檢查新 MultiFactorAuthenticationAdfsAdapter.config toosee hello 中的 hello 屬性。 如果任何屬性已加入或移除 hello 新版本中，將從舊組態檔案 toohello hello 新複製 hello 屬性值或修改 hello 舊組態檔案 toomatch。

### <a name="install-new-ad-fs-adapters"></a>安裝新的 AD FS 配接器

> [!IMPORTANT] 
> 您的使用者將無法在步驟 3-8 的這個區段的必要的 tooperform 雙步驟驗證。 如果您有 AD FS 中設定多個叢集，您可以移除，升級和還原 hello 中的每個叢集伺服器陣列之外，獨立 hello 其他叢集 tooavoid 停機時間。

1. 移除 hello 伺服陣列中的某些 AD FS 伺服器。 更新這些伺服器 hello 其他人仍在執行時。
2. 從 hello AD FS 伺服器陣列移除每個伺服器上安裝 hello 新 AD FS 配接器。 如果每個 AD FS 伺服器上安裝 MFA Server hello，您可以更新透過 hello MFA Server 管理經驗 否則，可透過執行 MultiFactorAuthenticationAdfsAdapterSetup64.msi 來更新。 

  如果發生錯誤指出，"Microsoft Visual c + + 2015年可轉散發套件 Update 1 或更新版本為必要項，「 從下載並安裝 hello 最新的更新套件 hello [Microsoft Download Center](https://www.microsoft.com/download/)。 安裝這兩個 hello x86 和 x64 版本。

3. 跳過**AD FS** > **驗證原則** > **編輯全域的多重要素驗證原則**。 取消核取**WindowsAzureMultiFactorAuthentication**或**AzureMFAServerAuthentication** （取決於 hello 安裝目前的版本）。 

  完成此步驟之後，您必須先完成步驟 8，才能在此 AD FS 叢集中透過 MFA Server 進行雙步驟驗證。

4. 取消註冊 hello 舊版的 hello AD FS 配接器執行 hello Unregister-multifactorauthenticationadfsadapter.ps1 PowerShell 指令碼。 請確定該 hello *-名稱*（「 WindowsAzureMultiFactorAuthentication"或"AzureMFAServerAuthentication"） 的參數符合在步驟 3 中所顯示的 hello 名稱。 這適用於 tooall hello 相同 AD FS 叢集中的伺服器，因為沒有集中式組態。
5. 執行 hello Register-multifactorauthenticationadfsadapter.ps1 PowerShell 指令碼，以註冊 hello 新 AD FS 配接器。 這適用於 tooall hello 相同 AD FS 叢集中的伺服器，因為沒有集中式組態。
6. 重新啟動 hello 從 hello AD FS 伺服器陣列移除每個伺服器上的 AD FS 服務。
7. 新增更新的 hello 伺服器備份 toohello AD FS 伺服器陣列，並移除 hello hello 伺服陣列中的其他伺服器。
8. 跳過**AD FS** > **驗證原則** > **編輯全域的多重要素驗證原則**。 勾選 [AzureMfaServerAuthentication]。
9. 重複步驟 2 tooupdate hello 伺服器，而現在從 hello AD FS 伺服器陣列中移除，並重新啟動這些伺服器上的 hello AD FS 服務。
10. 這些伺服器將重新加入至 hello AD FS 伺服器陣列。

## <a name="next-steps"></a>後續步驟

- 取得[使用 Azure Multi-Factor Authentication 與協力廠商 VPN 的進階案例](multi-factor-authentication-advanced-vpn-configurations.md)的範例

- [將 MFA Server 與 Windows Server Active Directory 同步處理](multi-factor-authentication-get-started-server-dirint.md)

- 為您的應用程式[設定 Windows 驗證](multi-factor-authentication-get-started-server-windows.md)
