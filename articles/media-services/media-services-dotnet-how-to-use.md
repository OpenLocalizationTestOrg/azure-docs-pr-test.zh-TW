---
title: "aaaHow tooSet 與.NET 的 Media Services 開發的總電腦"
description: "深入了解使用 hello Media Services SDK for.NET 的 Media Services 的 hello 必要條件。 也了解如何 toocreate Visual Studio 應用程式。"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a>使用 .NET 進行媒體服務開發
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

本主題討論 toostart 開發媒體服務如何使用.NET 應用程式。

hello **Azure Media Services.NET SDK**程式庫可讓您針對使用.NET 的 Media Services tooprogram。 它甚至.NET 中，以更容易 toodevelop hello toomake **Azure Media Services.NET SDK Extensions**提供程式庫。 此程式庫包含一組延伸方法和協助程式函數，以簡化 .NET 程式碼。 這兩個程式庫都是透過 **NuGet** 和 **GitHub** 取得。

## <a name="prerequisites"></a>必要條件
* 新的或現有 Azure 訂用帳戶中的媒體服務帳戶。 請參閱 hello 主題[如何 tooCreate Media Services 帳戶](media-services-portal-create-account.md)。
* 作業系統：Windows 10、Windows 7、Windows 2008 R2 或 Windows 8。
* .NET Framework 4.5。
* Visual Studio。

## <a name="create-and-configure-a-visual-studio-project"></a>建立和設定 Visual Studio 專案
這個區段會顯示如何 toocreate Visual Studio 中的專案將它設定 Media Services 開發。  在此情況下，hello 專案是 C# Windows 主控台應用程式，但 hello 相同的設定步驟，如下所示套用 tooother 類型，您可以建立媒體服務應用程式 （例如，在 Windows Forms 應用程式或 ASP.NET Web 應用程式） 的專案。

此區段會顯示如何 toouse **NuGet** tooadd Media Services.NET SDK 延伸模組和其他相依程式庫。

或者，您可以從 GitHub 取得 hello 最新的媒體服務.NET SDK 位元 ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services)或[github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions))，建立 hello 方案，並新增 hello 參考 toohello 用戶端專案。 下載並自動擷取所有與 hello 必要的相依性。

1. 在 Visual Studio 中，建立新的 C# 主控台應用程式。 輸入 hello**名稱**，**位置**，和**方案名稱**，然後按一下確定。
2. 建置 hello 方案。
3. 使用**NuGet** tooinstall 並加入**Azure Media Services.NET SDK Extensions** (**windowsazure.mediaservices.extensions**)。 安裝這個封裝，也會安裝 **Media Services .NET SDK** ，並新增所有其他必要相依性。
   
    確定您擁有 hello NuGet 安裝最新版本。 如需詳細資訊和安裝指示，請參閱 [NuGet](http://nuget.codeplex.com/)。
4. 在 方案總管 hello hello 專案名稱上按一下滑鼠右鍵並選擇 管理 NuGet 封裝。
   
    hello [管理 NuGet 封裝] 對話方塊隨即出現。
5. 在 hello 線上圖庫中，搜尋 Azure MediaServices Extensions，選擇 Azure Media Services.NET SDK Extensions，，然後按一下 hello [安裝] 按鈕。
   
    hello 專案會修改，並參考 toohello Media Services.NET SDK Extensions，Media Services.NET SDK，並加入其他相依的組件。
6. toopromote 清除工具開發環境中，請考慮啟用 NuGet 封裝還原。 如需詳細資訊，請參閱 [NuGet 封裝還原](http://docs.nuget.org/consume/package-restore)。
7. 將參考加入太**System.Configuration**組件。 這個組件包含 hello System.Configuration。**ConfigurationManager**類別也就是使用的 tooaccess 組態檔案 (例如，App.config)。
   
    tooadd 參考使用 hello 管理參考 對話方塊中，以滑鼠右鍵按一下 hello hello 方案總管 中的專案名稱。 然後，依序選取 [加入] 和 [參考]。
   
    hello 管理參考 對話方塊隨即出現。
8. 在.NET framework 組件，尋找並選取 hello System.Configuration 組件，按下 [確定]。
9. 開啟 hello App.config 檔案，然後加入*appSettings*節 toohello 檔案。     
   
    設定所需的 tooconnect toohello Media Services API 的 hello 值。 如需詳細資訊，請參閱[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

    如果您使用[使用者驗證](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication)組態檔可能會有值為您的 Azure AD 租用戶網域和 hello AMS REST API 端點。
    
    >[!Important]
    >Hello Azure Media Services 文件中的大部分程式碼範例會設定，請使用使用者驗證 tooconnect toohello AMS 應用程式開發介面的類型 （互動式）。 這種驗證方法適用於管理或監控原生應用程式：行動應用程式、Windows 應用程式和主控台應用程式。 這種驗證方法不適用於伺服器、Web 服務、API 類型的應用程式。  如需詳細資訊，請參閱[存取 hello AMS API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. 覆寫現有的 hello**使用**hello Program.cs 檔案，以下列程式碼的 hello 的 hello 開頭的陳述式。
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

此時，您就準備好 toostart 開發媒體服務應用程式。    

## <a name="example"></a>範例

以下是小型的範例連接 toohello AMS 應用程式開發介面，並列出所有可用的媒體處理器。
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a>後續步驟

現在[您可以連接 toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md)並啟動[開發](media-services-dotnet-get-started.md)。


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

