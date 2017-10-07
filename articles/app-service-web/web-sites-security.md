---
title: "aaaSecure Azure App Service 中的應用程式"
description: "深入了解如何 toosecure web 應用程式、 行動裝置應用程式後端或在 Azure App Service API 應用程式。"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>在 Azure App Service 中保護應用程式
這篇文章可協助您開始在 Azure App Service 保護您的行動應用程式、行動裝置應用程式後端或 API 應用程式。 

Azure App Service 中的安全性有兩個層級： 

* **基礎結構與平台安全性**-您可以信任 Azure toohave hello 服務需要 tooactually 執行安全地在 hello 雲端中的項目。
* **應用程式安全性**-您需要 toodesign hello 應用程式本身的安全。 這包括您如何與 Azure Active Directory 整合，您如何管理憑證，以及您如何確保您可以安全地溝通 toodifferent 服務。 

#### <a name="infrastructure-and-platform-security"></a>基礎結構與平台安全性
應用程式服務會維護 hello Azure Vm、 儲存體、 網路連線、 web 架構、 管理及整合功能和執行更多，因為它正在安全，並強化和經過加強的相容性上連續執行 toomake 檢查，確定:

* 您的 App Service 應用程式就會與這兩個 hello 網際網路隔離，並從 hello 其他客戶的 Azure 資源。
* 您的 App Service 應用程式和資源群組中的其他 Azure 資源 (例如 SQL Database) 之間的密碼通訊 (例如連接字串) 仍在 Azure 內，不會跨任何網路界限。 一律會加密密碼。
* 您的 App Service 應用程式和外部資源之間的所有通訊，例如 PowerShell 管理、命令列介面、Azure SDK、REST API 和混合式連線，都會正確加密。
* 全天候威脅管理會保護 App Service 資源免於惡意程式碼、分散式拒絕服務 (DDoS)、攔截式 (MITM) 和其他威脅。 

如需在 Azure 中的基礎結構與平台安全性的詳細資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/security/)。

#### <a name="application-security"></a>應用程式安全性
Azure 負責保護 hello 基礎結構和您的應用程式執行的平台時，它是您的責任 toosecure 您的應用程式本身。 換句話說，您需要 toodevelop，部署及安全的方式來管理您的應用程式程式碼和內容。 若未這麼做，您的應用程式程式碼或內容可以仍是很容易遭受 toothreats 例如：

* SQL 插入
* 工作階段攔截
* 跨網站指令碼
* 應用程式層級 MITM
* 應用程式層級 DDoS

Web 應用程式的安全性考量的完整討論已超出本文件 hello 範圍。 做為指引進一步保護您的應用程式的起始點，請參閱 hello[開啟 Web 應用程式安全性專案 (OWASP)](https://www.owasp.org/index.php/Main_Page)，特別是 hello[前 10 個專案。](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)，此清單 hello 目前的前 10 個重要的 web 應用程式安全性缺陷，由 OWASP 成員所決定。

## <a name="perform-penetration-testing-on-your-app"></a>在您的應用程式上執行滲透測試
其中一個最簡單方式 tooget hello 入門測試，您的 App Service 應用程式的弱點可能會是 toouse hello[與 Tinfoil Security 整合](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)tooperform 單鍵的弱點可能會掃描您的應用程式上。 您可以在容易瞭解報表中，檢視 hello 測試結果，並了解如何 toofix 每項弱點的逐步指示。

如果您偏好 tooperform 自己滲透測試，或想 toouse，另一個掃描器套件或提供者，您必須依照 hello [Azure 滲透測試核准程序](https://security-forms.azure.com/penetration-testing/terms)並取得預先核准 tooperform hello 預期入侵測試。

## <a name="https"></a> 與客戶的安全通訊
如果您使用 hello  **\*。 名稱是.azurewebsites.net**網域名稱建立 App Service 應用程式中，所有提供的 SSL 憑證，您可以立即使用 HTTPS，  **\*。 名稱是.azurewebsites.net**網域名稱。 如果您的網站使用[自訂網域名稱](app-service-web-tutorial-custom-domain.md)，您可以將上傳 SSL 憑證太[啟用 HTTPS](app-service-web-tutorial-custom-ssl.md) hello 自訂網域。

啟用[HTTPS](https://en.wikipedia.org/wiki/HTTPS)有助於防範 MITM 攻擊 hello 應用程式與使用者之間的通訊。

## <a name="secure-data-tier"></a>保護資料層
與 SQL 資料庫高整合應用程式服務，該 hello 應用程式，使跨 hello 面板會加密所有 hello 連接字串，並且只會解密 hello VM 上執行*和*只當 hello 應用程式執行。 此外，Azure SQL Database 包含安全 e-security 潛在威脅，包括從應用程式資料的許多安全性功能 toohelp[在 rest 加密](https://msdn.microsoft.com/library/dn948096.aspx)，[永遠加密](https://msdn.microsoft.com/library/mt163865.aspx)， [動態資料遮罩](../sql-database/sql-database-dynamic-data-masking-get-started.md)，和[威脅偵測](../sql-database/sql-database-threat-detection.md)。 如果您的機密資料或規範需求，請參閱[保護您的 SQL Database](../sql-database/sql-database-security-overview.md)如需有關如何 toosecure 您的資料。

如果您使用協力廠商資料庫提供者，例如 ClearDB，應該洽詢 hello 提供者的文件，直接在安全性最佳作法。  

## <a name="develop"></a> 保護開發和部署
### <a name="publishing-profiles-and-publish-settings"></a>發行設定檔和發行設定
在開發應用程式時，執行管理工作或自動化工作，例如使用公用程式**Visual Studio**， **Web Matrix**， **Azure PowerShell**或 hello**Azure 命令列介面 (Azure CLI)**，您可以使用*發行設定*檔案或*發行設定檔*。 這兩種檔案類型驗證您有了 Azure，而且應該受到 tooprevent 未經授權的存取。

* **發行設定** 檔案包含
  
  * 您的 Azure 訂用帳戶 ID
  * 可讓您 tooperform 訂用帳戶的管理工作的管理憑證*不用 tooprovide 帳戶名稱或密碼*。
* **發行設定檔** 檔案包含
  
  * 發行 tooyour 應用程式的資訊

如果您使用的公用程式會使用發行設定檔或發行設定檔，匯入包含 hello 發行設定 hello 檔案或至 hello 公用程式設定檔，然後**刪除**hello 檔案。 如果您必須保留 hello 檔案，與其他人，例如處理 hello 專案 tooshare 將它儲存在安全的位置例如*加密*目錄以有限權限。

此外，您應該確定保護 hello 匯入的認證。 例如， **Azure PowerShell**和 hello **Azure 命令列介面 (Azure CLI)**同時匯入的資訊儲存在您**主目錄**(*~*  Linux 或 OS X 系統上和*/使用者/您的使用者名稱*在 Windows 系統上。)為了加強安全性，您可能希望太**加密**使用適用於您作業系統的加密工具可以使用這些位置。

### <a name="configuration-settings-and-connection-strings"></a>組態設定和連接字串
它是常見的作法 toostore 連接字串、 驗證認證和其他組態檔中的機密資訊。 然而，這些檔案可能會暴露在您的網站上，或簽入公開的儲存機制，因而公開此資訊。 簡單的搜尋[GitHub](https://github.com)，比方說，可以找出與 hello 公用儲存機制中的公開密碼無數的組態檔。

hello 最佳作法是 tookeep 超出您的應用程式組態檔的這項資訊。 應用程式服務可讓您將組態資訊儲存為 hello 執行階段環境的一部分**應用程式設定**和**連接字串**。 hello 的值為公開的 tooyour 應用程式，透過在執行階段*環境變數*大部分的程式設計語言。 若是 .NET 應用程式，則這些值會在執行階段加入您的 .NET 組態。 除了這些情況下，這些組態設定會維持加密狀態，除非您檢視或設定它們使用 hello [Azure 入口網站](https://portal.azure.com)或公用程式，例如 PowerShell 或 hello Azure CLI。 

將組態資訊儲存在應用程式服務，可讓 hello 應用程式系統管理員 toolock 下 hello 實際執行應用程式的敏感性資訊。 開發人員可以開發應用程式使用一組個別的組態設定，並由 App Service 中設定的 hello 設定可以自動取代 hello 設定。 甚至 hello 開發人員需要 tooknow hello 密碼設定為 hello 生產環境應用程式。 如需在 App Service 中設定應用程式設定和連接字串的詳細資訊，請參閱 [設定 Web 應用程式](web-sites-configure.md)。

### <a name="ftps"></a>FTPS
Azure App Service 透過應用程式提供安全的 FTP 存取 toohello 檔案系統**FTPS**。 這可讓您 toosecurely 存取 hello 應用程式程式碼 hello web 應用程式，以及診斷記錄檔。 建議您一律使用 FTPS 而不是 FTP。 

hello FTPS 連結您的應用程式可以找到以 hello 下列步驟：

1. 開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 選取 [全部瀏覽] 。
3. 從 hello**瀏覽**刀鋒視窗中，選取**應用程式服務**。
4. 從 hello**應用程式服務**刀鋒視窗中，選取 hello 所需的應用程式。
5. 從應用程式 hello 刀鋒視窗中，選取**所有設定**。
6. 從 hello**設定**刀鋒視窗中，選取**屬性**。
7. hello FTP 和 FTPS 連結上提供 hello**設定**刀鋒視窗。 

如需 FTPS 的詳細資訊，請參閱 [檔案傳輸通訊協定](http://en.wikipedia.org/wiki/File_Transfer_Protocol)。

## <a name="next-steps"></a>後續步驟
如需 hello Azure 平台上報告資訊的 hello 安全性**濫用或安全性事件**，或 tooinform 所執行的 Microsoft**滲透測試**的您站台，請參閱 hello 安全性 > 一節的 hello [Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/security/)。

如需 App Service 應用程式的 **web.config** 或 **applicationhost.config** 檔案詳細資訊，請參閱[已在 Azure App Service Web Apps 中解除鎖定的設定選項](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/)。

如需記錄 App Service 應用程式資訊的詳細資訊 (此資訊可能對偵測攻擊很有幫助)，請參閱 [啟用診斷記錄](web-sites-enable-diagnostic-log.md)。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的起始應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

