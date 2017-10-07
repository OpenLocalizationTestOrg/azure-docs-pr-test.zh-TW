---
title: "使用 aaaGet 資料 hello Azure AD 報告 API 使用的憑證 |Microsoft 文件"
description: "說明如何 toouse hello Azure AD 報告 API 的憑證認證 tooget 資料不需要使用者介入的目錄。"
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>取得憑證搭配使用 hello Azure AD 報告 API 的資料
本文將討論如何 toouse hello Azure AD 報告 API 的憑證認證 tooget 資料不需要使用者介入的目錄。 

## <a name="use-hello-azure-ad-reporting-api"></a>使用 hello Azure AD 報告 API 
Azure AD 報告 API 需要您先完成下列步驟的 hello:
 *  安裝必要條件
 *  設定應用程式中的 hello 憑證
 *  取得存取權杖
 *  使用 hello 存取語彙基元 toocall hello Graph API

如需原始程式碼的相關資訊，請參閱[運用報告 API 模組](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)。 

### <a name="install-prerequisites"></a>安裝必要條件
您將需要 Azure AD PowerShell V2 toohave 和 AzureADUtils 模組安裝。

1. 下載並安裝 Azure AD Powershell V2、 在 hello 指示[Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md)。
2. 下載 Azure AD Utils 模組 hello [azure Ad/azure activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1)。 
  此模組會提供數個公用程式 Cmdlet，包括︰
   * hello 最新版本的 ADAL 使用 Nuget
   * 從使用者、應用程式金鑰和憑證存取權杖 (使用 ADAL)
   * 處理分頁結果的圖形 API

**tooinstall hello Azure AD Utils 模組：**

1. 建立目錄 toosave hello 公用程式模組 (例如，c:\azureAD)，並從 GitHub 下載 hello 模組。
2. 開啟的 PowerShell 工作階段，並移 toohello 您剛建立的目錄。 
3. 匯入 hello 模組，並將它安裝在使用 hello 安裝 AzureADUtilsModule cmdlet hello PowerShell 模組路徑。 

hello 工作階段應該看起來類似 toothis 螢幕：

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>設定應用程式中的 hello 憑證
1. 如果您已經有應用程式，請從 hello Azure 入口網站中取得其物件識別碼。 

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. 開啟 PowerShell 工作階段，並連接 tooAzure AD 使用 hello 連接 azure Ad cmdlet。

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. 使用從 AzureADUtils tooadd 憑證認證 tooit hello 新增 AzureADApplicationCertificateCredential 指令程式。 

>[!Note]
>您需要 tooprovide hello 應用程式更早版本，而擷取的物件識別碼以及 hello 憑證物件 (此使用 hello Cert： 磁碟機)。
>


  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>取得存取權杖

tooget 存取權杖，請使用 AzureADUtils hello Get AzureADGraphAPIAccessTokenFromCert cmdlet。 

>[!NOTE]
>您需要而不是您在 hello 最後一節中使用的物件識別碼 hello toouse hello 應用程式識別碼。
>

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>使用 hello 存取語彙基元 toocall hello Graph API

現在您可以建立 hello 指令碼。 以下是使用從 hello AzureADUtils hello Invoke AzureADGraphAPIQuery cmdlet 的範例。 此 cmdlet 會處理多個分頁的結果，並接著會傳送這些結果 toohello PowerShell 管線。 

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/script-completed.png)

您現在已準備好 tooexport tooa CSV，並儲存 tooa SIEM 系統。 您也可以包裝您的指令碼中的排程的工作 tooget Azure AD 資料從您的租用戶定期而不需要在 hello 原始程式碼 toostore 應用程式金鑰。 

## <a name="next-steps"></a>後續步驟
[hello Azure 身分識別管理的基本概念](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



