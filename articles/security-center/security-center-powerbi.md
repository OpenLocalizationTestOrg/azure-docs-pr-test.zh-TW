---
title: "從 Power BI 的 Azure 資訊安全中心資料 aaaGet insights |Microsoft 文件"
description: "hello Azure 安全性中心 Power BI 內容套件可輕鬆 toofind 安全性警示，請建議、 攻擊資源和趨勢、 已為您的報表建立資料集為基礎。"
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 0ded6bc7-52e8-43b4-8940-0bee137526e3
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: af68aef626034fe03d793c36b515a3f26619e5f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-insights-from-azure-security-center-data-with-power-bi"></a>使用 Power BI 從 Azure 資訊安全中心的資料取得見解
hello [Power BI 儀表板](http://aka.ms/azure-security-center-power-bi)Azure 資訊安全中心可讓您 toovisualize，分析及篩選建議和從任何地方，包括您的行動裝置的安全性警示。 使用 hello Power BI 儀表板 tooreveal 趨勢，而攻擊的模式-檢視安全性警示的資源或來源 IP 位址，並依資源或年齡 unaddressed 安全性風險。

您也可以用相關方式結合資訊安全中心建議、安全性警示和其他資料，例如使用 [Azure 稽核記錄檔](https://powerbi.microsoft.com/blog/monitor-azure-audit-logs-with-power-bi/)和 [Azure SQL Database 稽核](https://powerbi.microsoft.com/blog/monitor-your-azure-sql-database-auditing-activity-with-power-bi/)中的資料。 同時提供 Power BI 儀表板，而您也可以匯出此資料 tooExcel，hello 安全性狀態，提供雲端資源的簡單報表。

## <a name="using-azure-security-center-dashboard-tooaccess-power-bi"></a>使用 Azure 資訊安全中心儀表板 tooaccess Power BI
您也可以使用 hello Azure 資訊安全中心儀表板 tooaccess Power BI 報表。 請依照下列 hello 步驟 tooperform 這項工作：

1. 在 hello **Azure 資訊安全中心**儀表板，按一下  **Power BI**  按鈕。

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig1-1-newUI-2017.png)
2. hello **Power BI** hello 右邊會開啟刀鋒視窗，hello 遵循畫面所示：

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig1-new11-2017.png)
3. 如果您要建立 hello hello 的 Power BI 儀表板第一次，您可以選擇在 hello hello 下列其中一種選項**Power BI 中的瀏覽**刀鋒視窗中：

   * **安全性 insights 儀表板**： 如果您想 toocreate 儀表板，其中包含安全性狀態、 執行緒和偵測，請選擇此選項。 對於負責分析各訂用帳戶的防護狀態及偵測到之警示的 DevOps 角色而言，這是較常見的選項。
   * **原則管理儀表板**： 選擇此選項，如果您要 tooexplore 管理和強制執行原則。  對於偏重控管的中心 IT 人員而言，這是較常見的選項。 他們可以使用此儀表板 toogain 可見性和 insights 安全性原則一致性跨組織。
   * 如果您已經有了 Power BI 儀表板，按一下**Go tooyour 目前 Power BI 儀表板**。
4. 在這個範例中，請點選 [安全性深入解析儀表板]  選項。 如果這是 hello 第一次，您要建立 Power BI 儀表板，針對您的資訊安全中心提示 tooinstall hello 內容套件。 按一下**取得**按鈕在 hello **Power bi 內容套件**視窗 hello 遵循畫面所示：

    ![Azure 資訊安全中心安全性深入解析儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new3.png)
5. hello**連接 tooAzure 安全性中心的安全性深入解析**視窗會出現。 請確定 hello**驗證**方法**oAuth2**如下所示，按一下 [**登入**] 按鈕。

    ![驗證](./media/security-center-powerbi/security-center-powerbi-fig1-new4.png)
6. 您可能會要求 tooauthenticate 再次與您的 Azure 認證。 驗證之後，將會建立您的儀表板。 一旦建立 hello 儀表板之後您會看到與 hello 類似結構報告 hello 遵循畫面所示：

    ![Power BI 儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new5.png)

> [!NOTE]
> Hello 報表重新整理是每日的排程的 tootake 位置。 如果您遇到此重新整理失敗時，讀取[可能會發生重新整理問題 hello Azure 安全性中心 Power BI](https://blogs.msdn.microsoft.com/azuresecurity/2016/04/07/azure-security-center-power-bi-refresh-fails/)，如需有關如何 tootroubleshoot。
>
>

您可以查看 hello 編號安全性警示和建議，以及 hello Vm、 Azure SQL database 和 Azure 資訊安全中心受監視的網路資源數目。

連結 tooAzure 資訊安全中心重新導向 toohello Azure 入口網站。 hello 圖表讓安全性建議和警示，包括簡單 toovisualize 資訊：

* 資源安全性狀態
* 擱置建議
* VM 建議
* 不同時間的警示
* 受到攻擊的資源
* 受到攻擊的 IP

每個圖表背後都有額外的見解。 選取磚 toosee 的詳細資訊。 例如，hello**資源安全性狀態**磚會顯示您的其他詳細資料的相關暫止的建議資源 hello 遵循畫面所示：

![建議](./media/security-center-powerbi/security-center-powerbi-fig1-new6.png)

如果您按一下此圖表的任何一行，hello 其他人將 toogray 出與您的重點只在您選取的 hello。 tooreturn toohello 儀表板中，按一下  **Azure 資訊安全中心**下 hello**儀表板**hello 左窗格上的此頁面的選項。

> [!NOTE]
> 如果您想要 toocustomize 報表藉由新增其他欄位，或變更現有的視覺效果，您可以編輯 hello 報表。 如需詳細資訊，請閱讀 [在 Power BI 中與編輯檢視的報告互動](https://powerbi.microsoft.com/documentation/powerbi-service-interact-with-a-report-in-editing-view/) 。
>
>

hello**經過一段時間，攻擊資源警示**和**攻擊者的 Ip**當您按一下每個磚會有 hello 相似的輸出。 這是因為 hello 報表彙總所有的三個變數的相關資訊，並呼叫它**遭受攻擊的資源**hello 遵循畫面所示：

![遭受攻擊的資源](./media/security-center-powerbi/security-center-powerbi-fig1-new7.png)

此時您也可以儲存此報表的複本、 列印或 hello 網站上發佈使用 hello 中可用的 hello 選項**檔案**功能表。

![[檔案] 功能表](./media/security-center-powerbi/security-center-powerbi-fig8.png)

## <a name="exploring-your-azure-security-center-data-with-power-bi-services"></a>使用 Power BI 服務探索 Azure 資訊安全中心的資料
連接 toohello [Power BI 內容套件服務](https://msit.powerbi.com/groups/me/getdata/services)Power BI 中，然後執行下列步驟的 hello:

1. 在 hello**適用於 Power BI 內容套件**視窗將會看到兩個選項，如下所示。

    ![Power BI 內容套件](./media/security-center-powerbi/security-center-powerbi-fig1-new.png)

   > [!NOTE]
   > 如果已經執行本文章的 hello 第一個部分，您會看到一個選項，這是 Azure 安全性中心的 原則管理。
   >
   >
2. 為了 hello 此範例中，按一下 **取得**在 hello **Azure 安全性中心的 原則管理**磚。
3. 在 hello**連接 tooAzure 安全性 Center 原則管理**視窗中，請確定 tooselect **oAuth2**下**驗證方法**卸除下如下所示，然後按一下**登入** 按鈕。

    ![原則管理視窗](./media/security-center-powerbi/security-center-powerbi-fig1-new8.png)
4. 您將會重新導向的 tooan 驗證頁面上，您應該在其中輸入 hello 認證使用 tooconnect tooAzure 資訊安全中心。 Hello 驗證程序完成之後，Power BI 會開始匯入資料 toobuild 您的報表。 在這段期間可能會看到下列訊息上的瀏覽器的 hello 右上角的 hello:

    ![連接使用 Power BI tooAzure 資訊安全中心](./media/security-center-powerbi/security-center-powerbi-fig4.png)

   > [!NOTE]
   > hello 儀表板建立時的 hello 第一次它可以比平常長，主要用於情況下，您需要多個訂用帳戶。
   >
   >
5. Azure 安全性中心 Power BI 儀表板在 hello 程序完成時，便會載入 hello**原則管理**報告類似 toohello 一個如下所示：

    ![原則管理儀表板](./media/security-center-powerbi/security-center-powerbi-fig1-new9.png)

## <a name="see-also"></a>另請參閱
在本文件中，您學到如何 toouse Azure 資訊安全中心中的 Power BI。 toolearn 進一步了解 Azure 資訊安全中心，請參閱 hello 下列資訊：

* [Azure 資訊安全中心計劃與作業指南](security-center-planning-and-operations-guide.md)— 了解如何 tooplan Azure 資訊安全中心採用。
* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure Azure 資訊安全中心中的安全性設定
* [Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) — 了解如何 toomanage 和回應 toosecurity 警示
* [Azure 資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。
