---
title: "aaaAzure 存放裝置總管疑難排解指南 |Microsoft 文件"
description: "Hello 兩個 Azure 偵錯功能的概觀"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Azure 儲存體總管疑難排解指南

## <a name="introduction"></a>簡介

Microsoft Azure 儲存體總管 （預覽） 是一個獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。 hello 應用程式可以連接 toStorage Sovereign 雲端 Azure Azure 堆疊上裝載的帳戶。

本指南摘要說明儲存體總管中常見的問題解決方案。

## <a name="sign-in-issues"></a>登入問題

僅支援 Azure Active Directory (AAD) 帳戶。 如果您使用 ADFS 帳戶時，預期會有該登入 tooStorage 總管將無法運作。 在繼續之前，請嘗試重新啟動您的應用程式，並查看是否可以固定 hello 問題。

### <a name="error-self-signed-certificate-in-certificate-chain"></a>錯誤：憑證鏈結中的自我簽署憑證

有數個原因，您可能會遇到這個錯誤，並且 hello 最常見的兩個原因如下：

1. hello 應用程式是透過"transparent proxy"，這表示攔截 HTTPS 流量，解密，而且再加密使用自我簽署的憑證 （例如您公司的伺服器） 的伺服器連接。

2. 您正在執行的應用程式，例如防毒軟體，注入 hello HTTPS 訊息，您會收到自我簽署的 SSL 憑證。

當儲存體總管遇到的其中一個 hello 問題時，它不再可以知道收到 hello HTTPS 訊息是否遭竄改。 如果您有一份 hello 自我簽署憑證，您可以讓信任它的儲存體總管。 如果您不清楚誰正在插入 hello 憑證，請遵循這些步驟 toofind 它：

1. 安裝 Open SSL

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) （任一 hello 淺色版本應已足夠）

    - Mac 和 Linux：應該包含在作業系統中

2. 執行 Open SSL

    - Windows： 開啟 hello 安裝目錄中，按一下**/bin/**，然後按兩下**openssl.exe**。
    - Mac 和 Linux：從終端機執行 **openssl**。

3. 執行 s_client -showcerts -connect microsoft.com:443

4. 尋找自我簽署憑證。 如果您不確定哪些是自我簽署，請尋找任何位置 hello 主旨 ("s") 及簽發者 （「 i:"） 是 hello 相同。

5. 當您找到任何自我簽署的憑證時，每個複製和貼上的所有項目從和包括**---BEGIN CERTIFICATE---**太**---憑證結尾---** tooa 新.cer 檔案。

6. 開啟 [儲存體總管] 中，按一下**編輯** > **SSL 憑證** > **匯入憑證**，，然後使用 hello 檔案選擇器 toofind，選取，然後開啟您建立的 hello.cer 檔案。

如果找不到任何使用上述步驟 hello 的自我簽署的憑證，請與我們連絡透過 hello 意見工具，如需詳細說明。

### <a name="unable-tooretrieve-subscriptions"></a>無法 tooretrieve 訂用帳戶

如果您無法 tooretrieve 之後您訂用帳戶已成功登入，請遵循這些步驟 tootroubleshoot 此問題：

- 請確認您的帳戶具有存取 toohello 訂用帳戶，登入 hello Azure 入口網站。

- 請確定您已登入使用 hello 正確環境 （Azure、 Azure China、 Azure 德國、 Azure 美國政府或自訂 Azure 環境/堆疊）。

- 如果您在 proxy 背景，請確定您已正確設定 hello 存放裝置總管 proxy。

- 請嘗試移除並 hello 帳戶正在重新加入。

- 試著刪除下列檔案從根目錄 (亦即 C:\Users\ContosoUser)，然後再重新新增 hello 帳戶 hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- 監看式 hello 開發人員工具主控台 （藉由按 F12） 當您要登入的任何錯誤訊息：

![開發人員工具](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>無法 toosee hello 驗證頁面

如果您無法 toosee hello 驗證 頁面上，請遵循這些步驟 tootroubleshoot 此問題：

- 根據您的連線 hello 速度，它可能需要一些時間，hello 登入頁面 tooload、 等待至少一分鐘，再關閉 hello [驗證] 對話方塊。

- 如果您在 proxy 背景，請確定您已正確設定 hello 存放裝置總管 proxy。

- 按 hello F12 鍵 hello 開發人員主控台檢視。 觀看 hello 回應 hello 開發人員主控台，並查看是否都可以找到任何線索為何無法運作的驗證。

### <a name="cannot-remove-account"></a>無法移除帳戶

如果您無法 tooremove 帳戶，或是 hello 重新驗證連結不會執行任何動作，請遵循這些步驟 tootroubleshoot 此問題：

- 試著刪除下列檔案從您的根目錄，並再正在重新加入 hello 帳戶 hello:

    - .adalcache

    - .devaccounts

    - .extaccounts

- 如果您想 tooremove SAS 附加儲存體資源，請刪除下列檔案的 hello:

    - Windows 是 %AppData%/StorageExplorer 資料夾

    - Mac 是 /Users/<您的名稱>/Library/Applicaiton SUpport/StorageExplorer

    - Linux 是 ~/.config/StorageExplorer

> [!NOTE]
>  如果您刪除這些檔案您將有指定 tooreenter 您的認證。

## <a name="proxy-issues"></a>Proxy 問題

首先，請確定該 hello 遵循您所輸入的資訊都正確：

- hello proxy URL 和連接埠號碼

- 使用者名稱和密碼，如果所需的 hello proxy

### <a name="common-solutions"></a>常見的解決方案

如果您仍然遇到問題，請遵循這些步驟 tootroubleshoot 它們：

- 如果您可以連接 toohello 網際網路，而不使用 proxy，請確認儲存體總管就不會啟用 proxy 設定。 在 hello 情況下，可能是您的 proxy 設定發生問題。 使用 proxy 系統管理員 tooidentify hello 問題。

- 請確認其他應用程式使用 hello proxy 伺服器會在如預期般運作。

- 確認您能夠連線使用網頁瀏覽器 toohello Microsoft Azure 入口網站

- 確認您可以收到服務端點的回應。 在瀏覽器中輸入其中一個端點 URL。 如果可以連線，您應該會收到 InvalidQueryParameterValue 或類似的 XML 回應。

- 如果有其他人也用您的 proxy 伺服器使用儲存體總管，請確認他們可以連線。 如果它們可以連接，您可能必須 toocontact proxy 的伺服器管理員。

### <a name="tools-for-diagnosing-issues"></a>診斷問題的工具

如果您有網路的工具，例如 Fiddler 適用於 Windows，您可能無法 toodiagnose hello 問題，如下所示：

- 如果您有 toowork 透過您的 proxy 時，您可能必須 tooconfigure 您網路的工具 tooconnect 透過 hello proxy。

- 請檢查您的網路工具所使用的 hello 連接埠號碼。

- 輸入 hello 本機主機 URL 和 hello 網路工具的連接埠號碼為儲存體總管 中的 proxy 設定。 如果進行此設定正確，您的網路工具會啟動記錄提出儲存體總管 toomanagement 與服務端點的網路要求。 例如，輸入您在瀏覽器中的 blob 端點 https://cawablobgrs.blob.core.windows.net/，而且您會收到回應類似於 hello 下列，建議 hello 資源存在，雖然您無法存取它。

![程式碼範例](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>連絡 proxy 伺服器管理員

如果您的 proxy 設定正確無誤，您可能必須 toocontact 您的 proxy 伺服器系統管理員，並

- 請確定您的 proxy 不會封鎖流量 tooAzure 管理或資源的端點。

- 請確認您的 proxy 伺服器所使用的 hello 驗證通訊協定。 儲存體總管目前不支援 NTLM proxy。

## <a name="unable-tooretrieve-children-error-message"></a>「 無法 tooRetrieve 子系 」 錯誤訊息

如果您是透過 proxy 連線的 tooAzure，請確認您的 proxy 設定正確。 如果您已從 hello hello 訂用帳戶或帳戶的擁有者授與存取 tooa 資源，請確認您具有讀取或列出該資源的權限。

### <a name="issues-with-sas-url"></a>SAS URL 問題
如果您要連接 tooa 服務使用 SAS URL，以及發生此錯誤：

- 確認 hello URL 提供 hello 必要的權限 tooread 或清單的資源。

- 請確認該 hello URL 尚未過期。

- 如果 hello SAS URL 根據存取原則，請確認尚未撤銷 hello 存取原則。

## <a name="next-steps"></a>後續步驟

如果無 hello 方案為您的工作，送出 hello 與您的電子郵件的意見反應工具透過您的問題，而且可以包含做為您的 hello 問題的相關詳細資料，以便我們可以與您連絡以修正問題，hello。

toodo 此，依序按一下**協助**功能表，然後再按一下**傳送意見反應**。

![意見反應](./media/storage-explorer-troubleshooting/4022503_en_1.png)
