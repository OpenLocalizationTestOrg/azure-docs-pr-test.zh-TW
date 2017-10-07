---
title: "Azure Data Lake Tools：使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯 | Microsoft Docs"
description: "了解如何進行 toouse Azure 資料湖 Tools for Visual Studio Code toolocal 執行和本機偵錯。"
Keywords: "VScode，Azure 資料湖工具，本機執行，本機偵錯，本機偵錯預覽的儲存體檔案上, 傳 toostorage 路徑"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a>使用 Visual Studio Code 來進行 U-SQL 本機執行和本機偵錯

## <a name="prerequisites"></a>必要條件
請確定您有下列先決條件備妥，然後再開始這些程序的 hello:
- Azure Data Lake Tools for Visual Studio Code。 如需相關指示，請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。
- C# Visual Studio 程式碼 （如果您想 tooperform U-SQL 本機偵錯）。

   ![安裝 Data Lake Tools for Visual Studio Code 中的 C#](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > hello U-SQL 本機執行和偵錯功能目前僅支援 Windows 使用者。 


## <a name="set-up-hello-u-sql-local-run-environment"></a>設定 hello U-SQL 本機執行環境

1. 選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 下載 LocalRun 相依性**toodownload hello 封裝。  

   ![下載 hello ADL LocalRun 相依性套件](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. 找出 hello hello hello 所示的路徑中的相依性套件**輸出** 窗格中，然後安裝 BuildTools 及 Win10SDK 10240。 路徑範例如下：  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  ![找出 hello 相依性套件](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)

   a. tooinstall BuildTools，依照 hello 精靈的指示。   

  ![安裝 BuildTools](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   b. tooinstall Win10SDK 10240 依照 hello 精靈的指示。  

  ![安裝 Win10SDK 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. 設定 hello 環境變數。 設定 hello **SCOPE_CPP_SDK**環境變數：  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. 重新啟動 hello OS toomake 確定 hello 環境變數設定才會生效。  

   ![請確定已安裝 hello SCOPE_CPP_SDK 環境變數](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a>啟動 hello 本機執行的服務，然後送出 hello U-SQL 作業 tooa 本機帳戶 
Hello 第一次使用者，您會提示的 toodownload hello ADL： 如果尚未安裝的封裝下載 LocalRun 相依性。
1. 選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 啟動本機執行服務**。
2. 選取**接受**tooaccept hello hello 第一次的 Microsoft 軟體授權條款。 

   ![接受 hello Microsoft 軟體授權條款](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. hello cmd 主控台隨即開啟。 對於第一次的使用者，您需要 tooenter **3**，然後找出您的資料輸入和輸出的 hello 本機資料夾路徑。 如需其他選項，您可以使用 hello 預設值。 

   ![Data Lake Tools for Visual Studio Code 本機執行 CMD](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. 選擇 Ctrl + Shift + P tooopen hello 命令選擇區中，輸入**ADL： 送出工作**，然後選取**本機**toosubmit hello 作業 tooyour 本機帳戶。

   ![Data Lake Tools for Visual Studio Code 選取本機](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. 您送出 hello 作業之後，您可以檢視 hello 提交詳細資料。 tooview hello 提交詳細資料選取**jobUrl**在 hello**輸出**視窗。 您也可以檢視從 hello cmd 主控台 hello 作業提交狀態。 輸入**7** hello cmd 主控台中如果您想 tooknow 更多的作業詳細資料。

   ![Data Lake Tools for Visual Studio Code 本機執行輸出](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake Tools for Visual Studio Code 本機執行 CMD 狀態](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png) 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a>啟動本機偵錯 hello U-SQL 工作  
Hello 第一次使用者，您會提示的 toodownload hello ADL： 如果尚未安裝的封裝下載 LocalRun 相依性。
  
1. 選取 Ctrl + Shift + P tooopen hello 命令調色盤，然後輸入**ADL： 啟動本機執行服務**。 hello cmd 主控台隨即開啟。 請確定該 hello **DataRoot**設定。
3. 在您的 C# 程式碼後置中設定中斷點。
4. 在 [hello 指令碼編輯器] 中，選取 Ctrl + Shift + P tooopen hello 命令主控台，然後輸入**本機偵錯**toostart 本機偵錯服務。

![Data Lake Tools for Visual Studio Code 本機偵錯結果](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a>後續步驟
- 若要了解如何使用 Azure Data Lake Tools for Visual Studio Code，請參閱[使用 Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)。
- 如需 Data Lake Analytics 的入門資訊，請參閱[教學課程︰開始使用 Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md)。
- 如需 Data Lake Tools for Visual Studio 的相關資訊，請參閱[教學課程：使用 Data Lake Tools for Visual Studio 開發 U-SQL 指令碼](data-lake-analytics-data-lake-tools-get-started.md)。
- Hello 上開發的組件的資訊，請參閱[開發 U-SQL Azure Data Lake Analytics 工作的組件](data-lake-analytics-u-sql-develop-assemblies.md)。
