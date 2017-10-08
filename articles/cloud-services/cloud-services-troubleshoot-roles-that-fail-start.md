---
title: "無法 toostart 的 aaaTroubleshoot 角色 |Microsoft 文件"
description: "以下是雲端服務角色為什麼無法 toostart 一些常見原因。 也提供解決方案 toothese 問題。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>疑難排解失敗 toostart 的雲端服務角色
以下是一些常見的問題和解決方案無法 toostart 的相關的 tooAzure 雲端服務角色。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>遺失 Dll 或相依性
角色沒有回應，以及角色在 [正在初始化]、[忙碌] 和 [正在停止] 狀態之間循環，有可能是因為遺失 DLL 或組件所致。

遺失 DLL 或組件的徵狀可能是：

* 您的角色執行個體在 [正在初始化]、[忙碌] 及 [正在停止] 狀態之間循環。
* 您的角色執行個體已經移動過**準備**但如果您導覽 tooyour web 應用程式時，不會出現 hello 頁面。

有數個建議的方法可調查這些問題。

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>診斷 Web 角色中遺失 DLL 的問題
當您瀏覽 tooa 網站，部署在 web 角色，並 hello 瀏覽器會顯示伺服器錯誤類似 toohello 後的時，它可能表示 DLL 遺失。

!['/' 應用程式中有伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>關閉自訂錯誤以診斷問題
可以藉由設定 hello web 角色 tooset hello 自訂錯誤模式 tooOff hello web.config 和重新部署 hello 服務檢視更完整資訊時發生錯誤。

tooview 更完成而不需要使用遠端桌面的錯誤：

1. 開啟 Microsoft Visual Studio 中的 hello 方案。
2. 在 [hello**方案總管] 中**，找出 hello web.config 檔案，並將它開啟。
3. 在 hello web.config 檔案中，找出 hello system.web 區段並加入以下的 hello:

    ```xml
    <customErrors mode="Off" />
    ```
4. 儲存 hello 檔案。
5. 重新封裝，然後重新部署 hello 服務。

一旦 hello 服務重新部署之後，您會看到 hello hello 遺漏組件或 DLL 名稱的錯誤訊息。

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>藉由從遠端檢視 hello 錯誤診斷問題
您可以使用遠端桌面 tooaccess hello 角色，並從遠端檢視更完整資訊時發生錯誤。 使用下列步驟 tooview hello 錯誤使用遠端桌面的 hello:

1. 確定已安裝 Azure SDK 1.3 或更新版本。
2. 太 hello 部署期間使用 Visual Studio 的 hello 方案，選擇  設定遠端桌面連線。 如需設定 hello 遠端桌面連線的詳細資訊，請參閱[透過 Azure 角色使用遠端桌面](../vs-azure-tools-remote-desktop-roles.md)。
3. Hello Microsoft Azure 傳統入口網站中，一旦 hello 執行個體顯示狀態**準備**，按一下其中一個 hello 角色執行個體。
4. 按一下 hello**連接**圖示 hello**遠端存取**hello 功能區的區域。
5. 使用 hello hello 遠端桌面組態期間指定的認證登入 toohello 虛擬機器。
6. 開啟命令視窗。
7. 輸入 `IPconfig`。
8. 請注意 hello IPV4 位址的值。
9. 開啟 Internet Explorer。
10. 輸入 hello 位址和 hello hello web 應用程式名稱。 例如： `http://<IPV4 Address>/default.aspx`。

瀏覽 toohello 網站現在會傳回更明確的錯誤訊息：

* '/' 應用程式中有伺服器錯誤。
* 描述： Hello 執行 hello 目前 web 要求期間發生未處理的例外狀況。 請檢閱有關 hello 錯誤更多資訊的 hello 堆疊追蹤以及產生 hello 程式碼中的位置。
* 例外狀況詳細資料：System.IO.FIleNotFoundException：無法載入檔案或組件 ‘Microsoft.WindowsAzure.StorageClient，Version=1.1.0.0，Culture=neutral，PublicKeyToken=31bf856ad364e35’ 或其相依性之一。 hello 系統找不到指定的 hello 檔案。

例如：

!['/' 應用程式中有明確的伺服器錯誤。](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>使用 hello 計算模擬器來診斷問題
您可以使用 hello Microsoft Azure 計算模擬器 toodiagnose 後遺失相依性與 web.config 錯誤的問題進行疑難排解。

若要讓這種診斷方法獲得最佳結果，您應該使用具有 Windows 全新安裝的電腦或虛擬機器。 toobest 模擬 hello Azure 環境，請使用 Windows Server 2008 R2 x64。

1. 安裝 hello 獨立版的 hello [Azure SDK](https://azure.microsoft.com/downloads/)。
2. Hello 開發在電腦上，建置 hello 雲端服務專案。
3. 在 Windows 檔案總管，瀏覽 toohello hello 雲端服務專案的 bin\debug 資料夾。
4. 複製 hello.csx 資料夾及.cscfg 檔案 toohello 電腦使用 toodebug hello 問題。
5. Hello 清除電腦上開啟 Azure SDK 命令提示字元視窗，輸入`csrun.exe /devstore:start`。
6. 在 hello 命令提示字元中輸入`run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`。
7. Hello 角色啟動時，您會看到詳細的錯誤資訊，在 Internet Explorer 中。 您也可以使用標準的 Windows 疑難排解工具 toofurther 診斷 hello 問題。

## <a name="diagnose-issues-by-using-intellitrace"></a>使用 IntelliTrace 診斷問題
對於使用 .NET Framework 4 的背景工作角色和 Web 角色，您可以使用 Microsoft Visual Studio Enterprise 所提供的 [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx)。

啟用了 IntelliTrace，請遵循這些步驟 toodeploy hello 服務：

1. 確定已安裝 Azure SDK 1.3 或更新版本。
2. 使用 Visual Studio 部署 hello 方案。 在部署期間，檢查 hello**為.NET 4 角色啟用 IntelliTrace**核取方塊。
3. 一旦 hello 執行個體啟動時，開啟 hello**伺服器總管**。
4. 展開 hello **Azure\\雲端服務**節點並找出 hello 部署。
5. 展開 hello 部署，直到您看到 hello 角色執行個體。 以滑鼠右鍵按一下其中一個 hello 執行個體。
6. 選擇 [檢視 IntelliTrace 記錄檔] 。 hello **IntelliTrace 摘要**隨即開啟。
7. 找出 hello hello 摘要的例外狀況 > 一節。 如果有例外狀況，將會標示為 hello 區段**例外狀況資料**。
8. 展開 hello**例外狀況資料**並尋找**System.IO.FileNotFoundException**類似 toohello 下列錯誤：

![例外狀況資料、遺失檔案或組件](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>解決遺失 Dll 和組件的問題
tooaddress 遺失 DLL 和組件的錯誤，請遵循下列步驟：

1. 開啟 Visual Studio 中的 hello 方案。
2. 在**方案總管 中**，開啟 hello**參考**資料夾。
3. 按一下 hello hello 錯誤中指出的組件。
4. 在 hello**屬性** 窗格中，找出**複製本機屬性**並將 hello 值設定為太**True**。
5. 重新部署 hello 雲端服務。

一旦您確認已更正所有錯誤時，您可以部署 hello 服務而不檢查 hello**為.NET 4 角色啟用 IntelliTrace**核取方塊。

## <a name="next-steps"></a>後續步驟
檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。

toolearn tootroubleshoot 雲端服務角色如何發出使用 Azure PaaS 電腦診斷資料，請參閱[Kevin Williamson 部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。
