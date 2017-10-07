---
title: "aaaIntroduction tooAzure Advisor |Microsoft 文件"
description: "使用 Azure Advisor toooptimize 您的 Azure 部署。"
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>簡介 tooAzure Advisor

了解 Azure Advisor 和其索引鍵的功能，並取得常見問題的解答 toofrequently。

## <a name="what-is-advisor"></a>何謂 Advisor？
Advisor 是個人化的雲端顧問，可協助您遵循最佳作法 toooptimize 您的 Azure 部署。 它會分析您的資源設定和使用遙測，並再建議解決方案，協助您改善 hello 成本效益、 效能、 高可用性和您的 Azure 資源的安全性。

使用 Advisor，您可以：
* 取得主動式、可採取動作且個人化的最佳做法建議。 
* 識別 Azure 整體支出的機會 tooreduce 提升 hello 效能、 安全性及您資源的高可用性。
* 取得內嵌了提議動作的建議。

您可以透過 hello 存取 Advisor [Azure 入口網站](https://aka.ms/azureadvisordashboard)。 登入 toohello[入口網站](https://portal.azure.com)，選取**瀏覽**，然後捲動太**Azure Advisor**。 hello Advisor 儀表板會顯示選取的訂用帳戶的個人化的建議。 

hello 建議分為四種分類： 

* **高可用性**: tooensure 和改善的業務關鍵應用程式的 hello 持續性。 如需詳細資訊，請參閱[建議程式高可用性的建議](advisor-high-availability-recommendations.md)。

* **安全性**: toodetect 威脅與弱點可能會導致 toosecurity 漏洞。 如需詳細資訊，請參閱[建議程式安全性建議](advisor-security-recommendations.md)。

* **效能**: tooimprove hello 速度的應用程式。 如需詳細資訊，請參閱[建議程式效能建議](advisor-performance-recommendations.md)。

* **成本**: toooptimize 並減少整體 Azure 支出。 如需詳細資訊，請參閱[建議程式成本建議](advisor-cost-recommendations.md)。

  ![建議程式建議類型](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。 已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。 此作業「只需要執行一次」。 Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。

您可以按一下建議 toolearn 詳細資訊，請參閱。 您可以執行的機會 tootake 優點，或解決的問題，您也可以了解動作。 

建議程式可透過內嵌動作或文件連結提供建議。 按一下內嵌動作會引導您完成 「 引導式的使用者之旅"tooimplement 它。 按一下文件的連結會指向 toodocumentation 描述 toomanually 實作 hello 動作的方式。 

Advisor 會每小時更新建議。 如果您不想 tootake 立即採取行動的建議，您可以延遲一段指定的時間，或關閉它。 

## <a name="frequently-asked-questions"></a>常見問題集

### <a name="how-do-i-access-advisor"></a>如何存取建議程式？
您可以透過 hello 存取 Advisor [Azure 入口網站](https://aka.ms/azureadvisordashboard)。 登入 toohello[入口網站](https://portal.azure.com)，選取**瀏覽**，然後捲動太**Azure Advisor**。 hello Advisor 儀表板會顯示選取的訂用帳戶的個人化的建議。 

您也可以透過 hello 虛擬機器資源刀鋒視窗中檢視 Advisor 的建議。 選擇虛擬機器，，然後捲動 tooAdvisor hello 功能表中的建議。 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>權限的執行需要 tooaccess Advisor 嗎？

tooaccess Advisor 的建議，您必須先*註冊您的訂閱*與 Advisor。 已經註冊訂閱時*訂用帳戶擁有者*啟動 hello Advisor 儀表板，並按一下 hello**取得建議** 按鈕。 此作業「只需要執行一次」。 Hello 訂用帳戶註冊之後，您可以存取 Advisor 的建議做為*擁有者*，*參與者*，或*讀取器*訂用帳戶，資源群組，或特定的資源。

### <a name="how-often-are-advisor-recommendations-updated"></a>建議程式建議的頻率為何？

Advisor 建議會每小時進行更新。

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>建議程式可提供哪些資源的建議？

Advisor 可提供虛擬機器、可用性設定組、應用程式閘道、應用程式服務、SQL Server、SQL Database 和 Redis 快取的建議。

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>是否可以延遲或解除建議？

toosnooze 或關閉建議，請按一下 hello**延期**按鈕或連結。 您可以指定延遲時間週期或選取**永不**toodismiss hello 建議。

## <a name="next-steps"></a>後續步驟

toolearn 深入了解 Advisor 的建議，請參閱：

* [開始使用建議程式](advisor-get-started.md)
* [建議程式高可用性建議](advisor-high-availability-recommendations.md)
* [建議程式安全性建議](advisor-security-recommendations.md)
* [建議程式效能建議](advisor-performance-recommendations.md)
* [建議程式成本建議](advisor-cost-recommendations.md)
