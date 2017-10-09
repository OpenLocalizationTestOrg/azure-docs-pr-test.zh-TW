---
title: "aaaUpgrade PhoneFactor tooAzure MFA Server |Microsoft 文件"
description: "開始使用 Azure MFA Server 從 hello 較舊的 phonefactor 代理程式升級時。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>升級 hello PhoneFactor Agent tooAzure Multi-factor Authentication Server
tooupgrade hello PhoneFactor Agent v5.x 或較舊 tooAzure Multi-factor Authentication Server、 解除安裝 PhoneFactor Agent hello 和附屬元件第一次。 然後 hello Multi-factor Authentication Server，而且可以安裝及其附屬的元件。

## <a name="uninstall-hello-phonefactor-agent"></a>解除安裝 PhoneFactor Agent hello

1. 首先，請備份 hello PhoneFactor 資料檔案。 hello 預設安裝位置是 C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata。

2. 如果已安裝使用者入口網站 hello:
  1. 瀏覽 toohello 安裝資料夾，然後備份 hello web.config 檔案。 hello 預設安裝位置是 C:\inetpub\wwwroot\PhoneFactor。

  2. 如果您已新增自訂佈景主題 toohello 入口網站，備份 hello C:\inetpub\wwwroot\PhoneFactor\App_Themes 目錄下的自訂資料夾。

  3. 解除安裝使用者入口網站 hello 透過 hello PhoneFactor Agent (只有安裝在 hello 與相同的伺服器 hello PhoneFactor 代理程式) 或透過 Windows 程式和功能。

3. 如果已安裝 Mobile App Web Service hello:

  1. 移 toohello 安裝資料夾，然後備份 hello web.config 檔案。 hello 預設安裝位置是 C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService。

  2. 解除安裝 hello Mobile App Web Service 透過 Windows 程式和功能。

4. 如果已安裝 hello Web 服務 SDK，請在透過 hello PhoneFactor 代理程式或透過 Windows 程式和功能解除安裝。

5. 解除安裝 hello PhoneFactor 代理程式，透過 Windows 程式和功能。

## <a name="install-hello-multi-factor-authentication-server"></a>安裝 hello Multi-factor Authentication Server

hello 安裝路徑從挑選 hello 登錄 hello 先前 PhoneFactor 代理程式安裝，因此它應該安裝相同 hello 位置 (例如 C:\Program Files\PhoneFactor)。 新安裝將會有不同的預設安裝路徑 (例如，C:\Program Files\Multi-Factor Authentication Server)。 hello 左的 hello 先前 PhoneFactor 代理程式應該在安裝期間，會升級，因此您的使用者和設定仍應該有在安裝之後 hello 新的 Multi-factor Authentication Server 資料檔案。

1. 如果出現提示，請啟用 hello Multi-factor Authentication Server，並確定它指派 toohello 正確的複寫群組。

2. 如果先前已安裝 Web 服務 SDK，hello 安裝 hello 新的 Web 服務 SDK，透過 hello Multi-factor Authentication Server 使用者介面。

  hello 的預設虛擬目錄名稱現在是**MultiFactorAuthWebServiceSdk**而不是**PhoneFactorWebServiceSdk**。 如果您想 toouse hello 先前的名稱，您必須在安裝期間變更 hello hello 虛擬目錄名稱。 否則，如果您允許 hello 安裝 toouse hello 新的預設名稱，您必須 toochange hello URL 任何應用程式中該參考 hello （例如 hello 使用者入口網站和行動裝置應用程式 Web 服務） 的 Web 服務 SDK toopoint hello 正確位置。

3. 如果 hello hello PhoneFactor 代理程式伺服器，在先前已安裝使用者入口網站安裝 hello 新 Multi-factor Authentication 使用者入口網站透過 hello Multi-factor Authentication Server 使用者介面。

  hello 的預設虛擬目錄名稱現在是**MultiFactorAuth**而不是**PhoneFactor**。 如果您想 toouse hello 先前的名稱，您必須在安裝期間變更 hello hello 虛擬目錄名稱。 否則，如果您允許 hello 安裝 toouse hello 新的預設名稱，您應該按一下 Multi-factor Authentication Server hello hello 使用者入口網站 圖示，並更新 hello 設定 索引標籤上的 hello 使用者入口網站 URL。

4. 如果 hello 使用者入口網站及/或 Mobile App Web Service 先前已安裝在不同的伺服器上 hello PhoneFactor 代理程式：

  1. 請 toohello 安裝位置 (例如 C:\Program Files\PhoneFactor)，並複製一或多個安裝程式 toohello 另一部伺服器。 有 32 位元和 64 位元的 hello 使用者入口網站和行動裝置應用程式 Web 服務的安裝程式。 它們稱為 MultiFactorAuthenticationUserPortalSetupXX.msi 和 MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi。

  2. tooinstall hello 使用者入口網站 hello 網頁伺服器上，開啟命令提示字元，以系統管理員，然後執行 MultiFactorAuthenticationUserPortalSetupXX.msi。

    hello 的預設虛擬目錄名稱現在是**MultiFactorAuth**而不是**PhoneFactor**。 如果您想 toouse hello 先前的名稱，您必須在安裝期間變更 hello hello 虛擬目錄名稱。 否則，如果您允許 hello 安裝 toouse hello 新的預設名稱，您應該按一下 Multi-factor Authentication Server hello hello 使用者入口網站 圖示，並更新 hello 設定 索引標籤上的 hello 使用者入口網站 URL。現有的使用者需要 toobe hello 新 URL 的通知。

  3. 移 toohello 使用者入口網站安裝位置 (例如 C:\inetpub\wwwroot\MultiFactorAuth) 並編輯 hello web.config 檔案。 複製您 hello 升級前備份到 hello 新的 web.config 檔案的原始 web.config 檔案中的 hello appSettings 及 applicationSettings 區段中的 hello 值。 如果安裝 hello Web 服務 SDK 時保留 hello 新的預設虛擬目錄名稱，，變更 hello applicationSettings 區段 toopoint toohello 正確的位置中的 hello URL。 如果在 hello 先前的 web.config 檔案中變更了任何其他預設值，適用於那些相同變更 toohello 新的 web.config 檔案。

  4. tooinstall hello Mobile App Web Service hello 網頁伺服器上，開啟命令提示字元，以系統管理員，然後執行 hello MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi。

    hello 的預設虛擬目錄名稱現在是**MultiFactorAuthMobileAppWebService**而不是**PhoneFactorPhoneAppWebService**。 如果您想 toouse hello 先前的名稱，您必須在安裝期間變更 hello hello 虛擬目錄名稱。 您可能會想 toochoose 較短的名稱 toomake 輕鬆使用者 tootype 中行動裝置上。 否則，如果您允許 hello 安裝 toouse hello 新的預設名稱，您應該按一下 hello hello Multi-factor Authentication Server 中的行動裝置應用程式圖示，並更新 hello Mobile App Web Service URL。

  5. 移 toohello Mobile App Web Service 安裝位置 (例如 C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) 並編輯 hello web.config 檔案。 複製您 hello 升級前備份到 hello 新的 web.config 檔案的原始 web.config 檔案中的 hello appSettings 及 applicationSettings 區段中的 hello 值。 如果安裝 hello Web 服務 SDK 時保留 hello 新的預設虛擬目錄名稱，，變更 hello applicationSettings 區段 toopoint toohello 正確的位置中的 hello URL。 如果在 hello 先前的 web.config 檔案中變更了任何其他預設值，適用於那些相同變更 toohello 新的 web.config 檔案。

## <a name="next-steps"></a>後續步驟

- [安裝 hello 使用者入口網站](multi-factor-authentication-get-started-portal.md)hello Azure Multi-factor Authentication Server。

- 為您的應用程式[設定 Windows 驗證](multi-factor-authentication-get-started-server-windows.md)。 
