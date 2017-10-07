---
title: "安裝 aaaProblem hello 應用程式 Proxy 代理程式連接器 |Microsoft 文件"
description: "如何 tootroubleshoot 問題可能會安裝時的字體 hello 應用程式 Proxy 代理程式連接器"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>安裝應用程式 Proxy 代理程式連接器 hello 的問題

Microsoft AAD 應用程式 Proxy 連接器是使用輸出連線 tooestablish hello 連線從 hello 雲端可用端點 toohello 內部網域的內部網域元件。

## <a name="general-problem-areas-with-connector-installation"></a>連接器安裝的一般問題區域

Hello 連接器安裝失敗時，hello 根本原因通常是一個 hello 下列區域：

1.  **連線**– hello 新連接器需求 tooregister toocomplete 安裝成功，並建立未來的信任屬性。 這是藉由連接 toohello AAD 應用程式 Proxy 的雲端服務。

2.  **建立信任**– hello 新連接器建立自我簽署的憑證，並登錄 toohello 雲端服務。

3.  **驗證的 hello admin** – 在安裝期間，hello 使用者必須提供系統管理員認證 toocomplete hello 連接器安裝。

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>請確認連接 toohello 雲端應用程式 Proxy 服務，且 Microsoft 登入頁面

**目標：**確認該 hello 連接器電腦可以連線 toohello AAD 應用程式 Proxy 註冊端點，以及 Microsoft 登入頁面。

1.  開啟下列網頁瀏覽器並前往 toohello: <https://aadap-portcheck.connectorporttest.msappproxy.net> ，確認該 hello 連線 tooCentral 美國和美國東部資料中心與連接埠 9090 和 9091 運作正常。

2.  如果任何這些連接埠不成功 （沒有綠色的核取記號），請確認該 hello 防火牆或 proxy 後端有\*。 msappproxy.net 9090 和 9091 定義正確的連接埠。

3.  開啟瀏覽器 （個別索引標籤），並移 toohello 下列網頁： <https://login.microsoftonline.com>，請確定您可以登入 toothat 頁面。

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>確認電腦和後端元件支援應用程式 Prxoy 信任憑證

**目標：**確認 hello 連接器的電腦、 後端 proxy 和防火牆，可以支援 hello 建立 hello 連接器未來的信任的憑證。

>[!NOTE]
>hello 連接器會嘗試 toocreate 受到 TLS1.2 SHA512 憑證。 如果機器 hello 或 hello 後端防火牆和 proxy 不支援 TLS1.2，hello 安裝失敗。
>
>

**tooresolve hello 問題：**

1.  請確認 hello 電腦支援 TLS1.2 – 2012 R2 之後的所有 Windows 版本應該支援 TLS 1.2。 如果您連接器的電腦，從的 2012 R2 版本或之前，請確定該 hello hello 機器已安裝下列 Kb: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  連絡您的網路系統管理員並要求 tooverify 確定 hello 後端 proxy 和防火牆不會封鎖 SHA512 傳出流量。

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>確認系統管理員是使用的 tooinstall hello 連接器

**目標：**確認嘗試 tooinstall hello 連接器該 hello 使用者是系統管理員的正確認證。 目前，hello 使用者必須是 hello 安裝 toosucceed 的全域系統管理員。

**tooverify hello 認證正確：**

連接太<https://login.microsoftonline.com>並用 hello 相同的認證。 請確定 hello 登入成功。 您可以檢查 hello 使用者角色移過**Azure Active Directory**  - &gt; **使用者和群組** - &gt; **所有使用者**. 

選取您的使用者帳戶，然後 「 目錄角色 」 hello 產生功能表中。 請確認該 hello 選取的角色是 「 全域系統管理員 」。 如果您無法 tooaccess hello 的任何頁面沿著這些步驟，您不是全域系統管理員。

## <a name="next-steps"></a>後續步驟
[了解 Azure AD 應用程式 Proxy 連接器](application-proxy-understand-connectors.md)
