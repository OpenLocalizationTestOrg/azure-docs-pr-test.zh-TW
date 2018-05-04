---
title: "適用於資料科學家的 Team Data Science Process | Microsoft Docs"
description: "提供使用 Team Data Science Process 和 Azure Machine Learning 來了解分析工作負載的指引。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/21/2017
ms.author: bradsev;BuckWoody
ms.openlocfilehash: 52d6fe0757043a0a298c3fdee0478fb364074537
ms.sourcegitcommit: cfd1ea99922329b3d5fab26b71ca2882df33f6c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2017
---
# <a name="team-data-science-process-for-data-scientists"></a>適用於資料科學家的 Team Data Science Process

本文提供一組目標的指引，這些目標通常與 Azure 技術搭配使用來實作全方位的資料科學解決方案。 將會引導您完成下列各項：

- 了解分析工作負載 
- 使用 Team Data Science Process
- 使用 Azure Machine Learning
- 資料傳輸與儲存的基礎
- 提供資料來源文件
- 使用工具來進行分析處理

這些訓練教材是關於 Team Data Science Process (TDSP) 和 Microsoft 與開放原始碼軟體和工具套件，對於構思、執行和傳遞資料科學解決方案很有幫助。

## <a name="lesson-path"></a>課程路徑
您可以利用下表中的項目來引導自己的自我學習。 請參閱「說明」欄來依循路徑操作、按一下「主題」連結來取得研究參考資料，以及使用「知識檢驗」欄來檢驗您的技能。

| **目標**                                                                             | **主題**                                                                                                                                            | **說明**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | **知識檢驗**                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 了解開發分析專案的程序                                 | [Team Data Science Process 簡介](overview.md)       | 我們會從探討 Team Data Science Process (TDSP) 的概觀開始著手。 此程序將引導您完成分析專案的每個步驟。 請完整閱讀這其中的每一節來深入了解此程序，以及如何實作此程序。                                                                                                                                                                                                                                                                                                                                                                                        | 針對您的專案，檢閱並[將 TDSP 專案結構成品下載到您的本機電腦](https://github.com/Azure/Azure-TDSP-ProjectTemplate) \(英文\)。                                                                                                                                                                                                                                                                                                         |
|                                                                                           | [敏捷式開發](https://www.visualstudio.com/agile/)                                                                                             | Team Data Science Process 與許多不同的程式設計方法都能良好搭配運作。 在此學習路徑中，我們將使用敏捷式軟體開發 (Agile Software Development)。 請完整閱讀「什麼是敏捷式開發？」 和「建立敏捷文化」文章，這些文章涵蓋以敏捷方式進行工作的基本概念。 此網站也有其他參考資料可供您進行深入了解。                                                                                                                                                                                                                                                                               | 向同事說明「持續整合」和「持續傳遞」。                                                                                                                                                                                                                                                                                                                                                                                          |
|                                                                                           | [適用於資料科學的 DevOps](https://mva.microsoft.com/training-courses/devops-an-it-pro-guide-8286?l=GVFXzCXy_8104984382)                        | 開發人員作業 (DevOps) 涉及您可用來逐步完成專案並將解決方案整合到組織標準 IT 的人員、程序及平台。 此整合對採用、安全及安全性來說是不可或缺的。 在此線上課程中，除了了解您擁有的一些工具鏈選項之外，您還會了解到 DevOps 做法。                                                                                                                                                                                                                                                                               | 準備一個 30 分鐘的簡報，向技術對象說明為何 DevOps 對分析專案來說是不可或缺的。                                                                                                                                                                                                                                                                                                                                                     |
| 了解資料儲存與處理的技術                               | [Microsoft 商務分析與 AI](https://www.microsoft.com/cloud-platform/what-is-cortana-intelligence)                                   | 在此學習路徑中，我們將焦點放在一些您可用來建立分析解決方案的技術上，但 Microsoft 還有更多的技術。 若要瞭解您所擁有的選項，請務必檢閱 Microsoft Azure、Azure Stack 及內部部署選項中提供的平台和功能。 請檢閱此資源，以了解可供您用來回答分析問題的各種工具。                                                                                                                                                                                                                                   | [下載並檢閱來自此研討會的簡報資料](https://info.microsoft.com/CO-Azure-CNTNT-FY16-Oct2015-Cortana-Registration.html) \(英文\)。                                                                                                                                                                                                                                                                                                          |
| 安裝並設定您的訓練、開發及生產環境               | [Microsoft Azure](https://azure.microsoft.com/training/learning-paths/azure-solution-architect/)                                               | 現在，我們將在 Microsoft Azure 中建立一個用於訓練的帳戶，並了解如何建立開發和測試環境。 這些免費的訓練資源將協助您開始進行操作。 請完成「初學者」和「中級者」路徑。                                                                                                                                                                                                                                                                                                                                                                                                                 | [如果您沒有 Azure 帳戶，請建立一個帳戶](https://azure.microsoft.com/free/?v=17.39&WT.srch=1&WT.mc_id=AID559320_SEM_2kAfgmyQ&lnkd=Bing_Azure_Brand)。 請登入 Microsoft Azure 入口網站，然後[建立一個資源群組](../../azure-resource-manager/resource-group-portal.md)以供訓練使用。                                                                                                                     |
|                                                                                           | [Microsoft Azure 命令列介面 (CLI)](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli?view=azure-cli-latest)      | 與 Microsoft Azure 搭配運作的方式有多種 – 從圖形化工具 (例如 VSCode 與 Visual Studio) 到 Web 介面 (例如 Azure 入口網站)，以及從命令列 (例如 Azure PowerShell 命令與函式)，都可以與 Azure 搭配運作。 在本文中，我們會涵蓋「命令列介面」(CLI)，除了在 Azure 入口網站中使用此工具之外，您也可以在工作站本機、在 Windows 及其他作業系統中使用此工具。                                                                                                                                                                                                                   | [使用 Azure CLI 來設定您的預設訂用帳戶](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli?view=azure-cli-latest)。                                                                                                                                                                                                                                                                                                      |
|                                                                                           | [Microsoft Azure 儲存體](../../storage/common/storage-introduction.md)                                                | 您需要一個可儲存資料的地方。 在本文中，您將了解 Microsoft Azure 的儲存體選項、如何建立儲存體帳戶，以及如何將資料複製或移動到雲端。 請完整閱讀這份簡介來深入了解。                                                                                                                                                                                                                                                                                                                                                                                                        | [在您的訓練資源群組中建立儲存體帳戶、為 Blob 物件建立一個容器，然後上傳及下載資料。](../../storage/blobs/storage-quickstart-blobs-cli.md)                                                                                                                                                                                                                                              |
|                                                                                           | [Microsoft Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)                                  | Microsoft Azure Active Directory (AAD) 可形成您應用程式的安全防護基礎。 在本文中，您將了解帳戶、權利及權限。 Active Directory 與安全性是複雜的主題，因此請直接完整閱讀此資源來了解基本概念。                                                                                                                                                                                                                                                                                                                                                  | [將一個使用者新增到 Azure Active Directory](../../active-directory/add-users-azure-active-directory.md)。 注意：如果您不是訂用帳戶的系統管理員，可能不具備此動作的權限。 如果是這種情況，[請直接檢閱此教學課程來深入了解](../../active-directory/add-users-azure-active-directory.md)。                                                        |
|                                                                                           | [Microsoft Azure 資料科學虛擬機器](../data-science-virtual-machine/overview.md)    | 您可以在多個作業系統本機安裝工具來與「資料科學」搭配運作。 但 Microsoft Azure 資料科學虛擬機器 (DSVM) 則是已包含您所需的一切工具，以及可供搭配運作的眾多專案範例。 在本文中，您將深入了解 DVSM 及如何逐步完成其範例。 此資源將說明「資料科學虛擬機器」、如何建立一個這類虛擬機器，以及一些使用它來開發程式碼的選項。 其中也包含完成此學習路徑所需的所有軟體 – 因此，請務必完成本主題的「知識路徑」。 | [建立資料科學虛擬機器並至少逐步完成一個實驗室作業](../data-science-virtual-machine/provision-vm.md)。                                                                                                                                                                                                                                                                                   |
| 安裝並了解可與資料科學解決方案搭配運作的工具和技術 
| [使用 Git](https://mva.microsoft.com/training-courses/github-for-windows-users-16749?l=KTNeW39wC_6006218965)                           | 為了依循我們搭配 TDSP 的 DevOps 程序，我們必須有一個版本控制系統。 「Microsoft Azure Machine Learning 服務」會使用 Git，這是一個熱門的開放原始碼分散式儲存機制系統。 在本文中，您將了解如何安裝、設定及使用 Git 和中央儲存機制 – Github。                                                                                                                                                                                                                                                                                                                      | [複製這個 Github 專案以供您的學習路徑專案結構使用](https://github.com/Azure/Azure-TDSP-ProjectTemplate) \(英文\)。                                                                                                                                                                                                                                                                                                                                      |
|                                                                                           | [VSCode](https://code.visualstudio.com/docs/getstarted/introvideos) \(英文\)                                                                                  | VSCode 是一個可以與多語言和 Azure 工具搭配使用的跨平台「整合式開發環境」(IDE)。 您可以使用此單一環境來建立整個解決方案。 請觀看這些簡介影片來開始進行操作。                                                                                                                                                                                                                                                                                                                                                                                             | 安裝 VSCode，然後[在互動式編輯器練習環境中逐步完成 VS Code 功能](https://code.visualstudio.com/docs/introvideos/basics) \(英文\)。                                                                                                                                                                                                                                                                                                            |
|                                                                                           | [使用 Python 進行程式設計](https://docs.python.org/3/tutorial/index.html) \(英文\)                                                                             | 在這個解決方案中，我們會使用 Python，這是「資料科學」中最受歡迎的語言之一。 本文涵蓋以 Python 撰寫分析程式碼的基本概念，以及可供進行深入了解的資源。 請逐步完成此參考資料的第 1-9 節，然後檢驗您的知識。                                                                                                                                                                                                                                                                                                                                                                            | [使用 Python 將一個實體新增到 Azure 資料表](../../cosmos-db/table-storage-how-to-use-python.md)。                                                                                                                                                                                                                                                                                                                               |
|                                                                                           | [使用 Notebook](https://jupyter-notebook.readthedocs.io/en/latest/notebook.html#introduction) \(英文\)                                               | Notebook 是一種在同一份文件中導入文字和程式碼的方式。 「Azure Machine Learning 服務」可以與 Notebook 搭配運作，因此了解如何使用 Notebook 會相當有幫助。 請完整閱讀此教學課程，然後在＜知識驗證＞一節中加以嘗試。                                                                                                                                                                                                                                                                                                                                                                | [開啟此頁面](https://try.jupyter.org/)，然後按一下 [Welcome to Python.ipynb] \(歡迎使用 Python.ipynb\) 連結。 逐步完成該頁面上的範例。                                                                                                                                                                                                                                                                                                                            |
|                                                                                           | [Machine Learning](https://mva.microsoft.com/training-courses/data-science-and-machine-learning-essentials-14100?l=UyhoTxWdB_3505050723)       
| 建立進階「分析」解決方案涉及處理資料、使用「機器學習服務」，這同時也構成與「人工智慧」及「深入學習」搭配運作的基礎。 本課程將讓您深入了解「機器學習服務」。 [如需有關資料科學的完整課程，請參考此認證](https://academy.microsoft.com/professional-program/tracks/data-science/) \(英文\)。                                                                                                                                                                                                                                                | 尋找有關「機器學習服務演算法」的資源。 (提示：依據「Azure Machine Learning 演算法小密技」進行搜尋)                                                                                                                                                                                                                                                                                                                                              |
|                                                                                           | [scikit-learn](http://scikit-learn.org/stable/tutorial/basic/tutorial.html)                                                                          | scikit-learn 工具組可讓您執行以 Python 撰寫的資料科學工作。 我們在解決方案中使用此架構。 本文涵蓋基本概念，並說明您可以從哪裡取得深入了解資訊。                                                                                                                                                                                                                                                                                                                                                                                                                                              | 藉由使用 Iris 資料集，利用 Pickle 保存 SVM 模型。                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                           | [使用 Docker](https://docs.microsoft.com/dotnet/standard/microservices-architecture/container-docker-introduction/docker-defined) \(英文\)      | Docker 是一個分散式平台，用來建置、提供及執行應用程式，並且是 Azure Machine Learning 服務中經常使用的平台。 本文涵蓋這項技術的基本概念，並說明您可以從哪裡取得深入了解資訊。                                                                                                                                                                                                                                                                                                                                                                                                           | 開啟 Visual Studio Code，然後[安裝 Docker 擴充功能](https://code.visualstudio.com/Docs/languages/dockerfile) \(英文\)。 [建立一個簡單的 Node Docker 容器](https://blogs.msdn.microsoft.com/vscode/2015/08/11/getting-started-with-docker/) \(英文\)。                                                                                                                                                                                                                 |
|                                                                                           | [HDInsight](../../hdinsight/hdinsight-hadoop-introduction.md)                                                          | HDInsight 是 Hadoop 的開放原始碼基礎結構，在 Microsoft Azure 中是作為一項服務。 您的「機器學習服務」演算法可能涉及大型的資料集，而 HDInsight 具備儲存、傳輸及處理大規模資料的能力。 本文涵蓋使用 HDInsight。                                                                                                                                                                                                                                                                                                                                                   | [建立小型 HDInsight 叢集](../../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md)。 使用 HiveQL 陳述式[將資料行投射到 /example/data/sample.log 檔案](../../hdinsight/hdinsight-use-hive.md)。 或者，[您也可以在本機系統上完成此知識檢驗](../../hdinsight/hdinsight-hadoop-emulator-get-started.md)。 |
| 從業務需求建立資料處理流程                                  | [判斷問題、依循 TDSP 進行操作](https://buckwoody.wordpress.com/2017/08/31/the-keys-to-effective-data-science-projects-the-question/) | 在已安裝和設定開發環境並已了解技術和程序的情況下，即可使用 TDSP 將一切整合在一起來執行分析。 我們必須從定義問題、選取資料來源及 Team Data Science Process 中的其餘步驟開始著手。 在我們逐步完成此程序時，請將 DevOps 程序牢記在心。 在本文中，您將了解如何將組織的需求納入考量，然後使用 Team Data Science Process 透過應用程式建立一個資料流程對應，以定義您的解決方案。                                       
| 尋找有關 [5 個資料科學問題](../studio/data-science-for-beginners-the-5-questions-data-science-answers.md)的資源，然後描述一個您組織在這些領域中可能發生的問題。 針對該問題，您應該將焦點放在哪些演算法上？                                                                                                                                            |
| 使用 Azure Machine Learning 服務來建立預測性解決方案                       | [Azure Machine Learning 服務](../preview/overview-what-is-azure-ml.md)                         | Microsoft Azure Machine Learning 包括處理資料來源、使用 AI 來進行資料整理和功能工程、建立實驗，以及追蹤模型執行。 這全部都在單一環境中運作，且大多數功能都可在本機或 Azure 中執行。 您可以使用 Cognitive Network Toolkit (CNTK)、TensorFlow 及其他架構來建立實驗。 在本文中，我們會將焦點放在使用您到目前為止所學到的一切知識，來進行此程序的完整範例。                                                                                                                                                   | [完成這個有關 Azure Machine Learning 服務與 TDSP 的教學課程。](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/machine-learning/preview/scenario-tdsp-classifying-us-incomes.md)                                                                                                                                                                                                                                                    |
| 使用 Power BI 以視覺方式呈現結果                                                         | [Power BI](https://powerbi.microsoft.com/guided-learning/)                                                                                     | Power BI 是 Microsoft 的資料視覺化工具。 從 Web 到行動裝置及桌上型電腦等多種平台上都有提供此工具。 在本文中，您將了解如何藉由從 Azure 儲存體存取結果及使用 Power BI 來建立視覺效果，處理您所建立之解決方案的輸出。                                                                                                                                                                                                                                                                                                                             | [完成這個有關 Power BI 的教學課程。](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) 然後將 Power BI 連接到在實驗執行中建立的 Blob CSV。                                                                                                                                                                                                                                                                       |
| 監視您的解決方案                                                                     | [Application Insights](../../application-insights/app-insights-overview.md)                                            | 有多種工具可供您用來監視您的端點解決方案。 Azure Application Insights 可讓您輕鬆將內建的監視功能整合到解決方案中。                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | [設定 Application Insights 來監視應用程式](https://cmatskas.com/visual-studio-code-integration-with-azure-application-insights/) \(英文\)。                                                                                                                                                                                                                                                                                                                  |
|                                                                                           | [Azure Log Analytics](../../log-analytics/log-analytics-overview.md)                                                   | 另一個監視您應用程式的方法是將其整合到 DevOps 程序中。 Azure Log Analytics 系統提供一組豐富的功能，可協助您在部署分析解決方案之後，監控這些解決方案。                                                                                                                                                                                                                                                                                                                                                                                                                       | [完成這個有關使用 Azure Log Analytics 的教學課程](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal) \(英文\)。                                                                                                                                                                                                                                                                                                       |
| 完成此學習路徑                                                               | 其他可嘗試的專案                                                                                                                           | 恭喜！ 您已完成此學習路徑。 還有許多需要學習的內容。 其中一個較進階的範例是在「Azure Machine Learning 服務」中建置客戶變換模型。 [立即在這裡試用](../preview/scenario-churn-prediction.md)。                                                                                                                                                                                                                                                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                 

## <a name="next-steps"></a>後續步驟
[適用於開發人員作業的 Team Data Science Process](team-data-science-process-for-devops.md)。本文將探索對「進階分析」和「辨識服務」解決方案實作而言特定的「開發人員作業」(DevOps) 功能。 