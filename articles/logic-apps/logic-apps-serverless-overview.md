---
title: "Azure 無伺服器的 aaaOverview |Microsoft 文件"
description: "在 hello 雲端中建立功能強大的解決方案，而不需要 toothink 相關基礎結構。"
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7c9c09d96e472edd1631892982ac60aae97342a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-serverless-with-functions-and-logic-apps"></a>Azure 無伺服器搭配 Functions 和 Logic Apps 的概觀

無伺服器應用程式提供的好處包括加速開發、減少必要的程式碼，以及簡單調整。  這篇文章會進入 hello 的無伺服器方案，部署和 Azure 的無伺服器提供不同的屬性。

## <a name="what-is-serverless"></a>什麼是無伺服器？

非伺服器並不表示沒有伺服器-它只是表示 hello 開發人員沒有 tooworry 有關伺服器的資訊。  大部分的傳統應用程式開發會回答周圍調整、 裝載及監視解決方案 toomeet hello 要求 hello 應用程式的問題。  使用非伺服器，這些問題會處理 hello 方案的一部分。  此外，無伺服器應用程式是以耗用量為基礎的方案計費。  如果從未使用過 hello 應用程式，將永遠不會造成需要付費。  這些功能可讓開發人員 toofocus 只可以在 hello 的商務邏輯的 hello 方案上。

在非伺服器周圍的 Azure 中的 hello 核心服務是[Azure 函式](https://azure.microsoft.com/services/functions/)和[Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/)。  這些解決方案遵循上述的 hello 原則和 toobuild 強大的雲端應用程式，以最少的程式碼可讓開發人員。

## <a name="what-are-azure-functions"></a>什麼是 Azure Functions？

Azure 的函式會很輕鬆地執行少量的程式碼或 「 函數 」 方案 hello 雲端中。 您可以撰寫只 hello 程式碼，不必耽心整個應用程式或 hello 基礎結構 toorun 它需要手邊，hello 問題。 Functions 可讓開發更有生產力，而且您可以使用您選擇的開發語言，例如 C#、F#、Node.js、Python 或 PHP。 只需支付 hello 次您的程式碼執行時，Azure 就會隨著所需。

如果您希望 toojump right，並開始使用 Azure 函式，以啟動[建立您的第一個 Azure 函式](../azure-functions/functions-create-first-azure-function.md)。 如果您要尋找有關函數的更多技術資訊，請參閱 hello[開發人員參考](../azure-functions/functions-reference.md)。

## <a name="what-are-azure-logic-apps"></a>什麼是 Azure Logic Apps？

Azure 邏輯應用程式提供方式 toosimplify，並實作 hello 雲端中的可擴充的整合和工作流程。 它提供視覺化設計工具 toomodel，並且為一系列的呼叫工作流程的步驟自動化程序。  有[多連接器](../connectors/apis-list.md)跨雲端和內部部署服務 tooquickly 連接無伺服器的應用程式 tooother 應用程式開發介面。  邏輯應用程式開頭的觸發程序 （類似 '時將帳戶加入 tooDynamics CRM'） 和許多組合動作、 轉換、 轉換和條件的邏輯，可以開始引發之後。  邏輯應用程式時協調不同的 Azure 功能中處理程序-hello 程序需要與外部系統或應用程式開發介面互動時，特別是很好的選擇。

tooget 開始使用邏輯應用程式，請從開始[建立應用程式的第一個邏輯](logic-apps-create-a-logic-app.md)。  如果您要尋找邏輯應用程式的其他技術資訊，請參閱 hello[開發人員參考](logic-apps-workflow-actions-triggers.md)。

## <a name="how-can-i-build-and-deploy-serverless-applications-in-azure"></a>如何在 Azure 中建置和部署無伺服器應用程式？

Azure 提供一組豐富的工具，涵蓋開發、部署和管理無伺服器應用程式。  應用程式可以直接在 hello Azure 入口網站，或藉由建置[從 Visual Studio 工具](logic-apps-serverless-get-started-vs.md)。  開發應用程式之後，就可以[立即部署](logic-apps-create-deploy-template.md)。  Azure 也支援監視無伺服器應用程式。  此監視可從 hello Azure 入口網站，透過 hello API 或 Sdk，或使用整合式的工具 tooOMS 和 Application Insights 存取。

## <a name="next-steps"></a>後續步驟

* [開始在 Visual Studio 中建置無伺服器應用程式](logic-apps-serverless-get-started-vs.md)
* [使用無伺服器建立 Customer Insights 儀表板](logic-apps-scenario-social-serverless.md)
* [建置邏輯應用程式的部署範本](logic-apps-create-deploy-template.md)