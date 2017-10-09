---
title: "aaaExcel 增益集的機器學習 Web 服務 |Microsoft 文件"
description: "Toouse Azure 機器學習 Web services 如何直接在 Excel 中而不需要撰寫任何程式碼。"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a>適用於 Azure Machine Learning Web 服務的 Excel 增益集
Excel 可讓您輕鬆 toocall web 服務直接而 hello 需要 toowrite 任何程式碼。

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a>步驟 tooUse hello 活頁簿中的現有 web 服務

1. 開啟 hello[範例 Excel 檔案](http://aka.ms/amlexcel-sample-2)，其中包含 hello Excel 增益集和乘客上的相關資料 hello Titanic。
2. 按一下以選擇 hello web 服務-"浩大存活者預測工具 （Excel 增益集範例） [分數] 「 在此範例中。
   
    ![選取 Web 服務][01]
3. 這會帶您 toohello**預測**> 一節。  此活頁簿已經包含範例資料，但若為空白的活頁簿，您可在 Excel 中選取一個儲存格並按一下 [使用範例資料] 。
4. 選取 hello 與標頭的資料，然後按一下 hello 輸入的資料範圍圖示。  請確定核取 hello 「 我的資料有標頭 」 的方塊。
5. 在下**輸出**，輸入您想這裡 hello 輸出 toobe，例如"H1"hello 資料格數目。
6. 按一下 [預測] 。
   
    ![預測區段][02]

部署 Web 服務或使用現有的 Web 服務。 如需有關如何部署 web 服務的詳細資訊，請參閱[逐步解說步驟 5： 部署 hello Azure 機器學習 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。

取得您的 web 服務的 hello API 金鑰。 執行此動作的位置，取決於您發佈的是傳統 Machine Learning Web 服務或新的 Machine Learning Web 服務。

**使用傳統 Web 服務** 

1. 在機器學習 Studio 中，按一下 hello **WEB 服務**hello 左窗格中，區段，然後選取 hello web 服務。
   
    ![Studio 選取 Web 服務][04]
2. 複製 hello web 服務的 hello API 金鑰。
   
    ![Studio API 金鑰][05]
3. 在 hello**儀表板**hello web 服務索引標籤上，按一下 hello**要求/回應**連結。
4. 尋找 hello**要求 URI** > 一節。  複製並儲存 hello URL。

> [!NOTE]
> 它現在是到 hello 可能 toosign [Azure 機器學習 Web 服務](https://services.azureml.net)傳統的機器學習 web 服務的入口網站 tooobtain hello API 金鑰。
> 
> 

**使用新的 Web 服務**

1. 在 hello [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站中，按一下**Web 服務**，然後選取您的 web 服務。 
2. 按一下 [取用] 。
3. 尋找 hello**基本耗用量資訊**> 一節。 複製並儲存 hello**主索引鍵**和 hello**要求-回應**URL。

## <a name="steps-tooadd-a-new-web-service"></a>步驟 tooAdd 新的 web 服務

1. 部署 Web 服務或使用現有的 Web 服務。 如需有關如何部署 web 服務的詳細資訊，請參閱[逐步解說步驟 5： 部署 hello Azure 機器學習 Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。
2. 按一下 [取用] 。
3. 尋找 hello**基本耗用量資訊**> 一節。 複製並儲存 hello**主索引鍵**和 hello**要求-回應**URL。
4. 在 Excel 中，移 toohello **Web 服務**區段 (如果您是在 hello**預測**區段中，按一下 [web 服務的 hello 上一頁] 箭頭 toogo toohello 清單)。
   
    ![請選取 tooWeb 服務][03]
5. 按一下 [新增 Web 服務] 。
6. 將 hello URL 貼到 Excel 增益集文字方塊標示為 「 hello **URL**。
7. 標示為 hello 文字方塊中的貼上 hello API/主要金鑰**API 金鑰**。
8. 按一下 [新增] 。
   
    ![傳統 Web 服務的 URL 和 API 金鑰。][06]
9. toouse hello web 服務，請遵循上述指示 hello、"步驟 tooUse 現有 web 服務。 」

## <a name="sharing-your-workbook"></a>共用活頁簿
如果您要儲存您的活頁簿，然後也會儲存您加入的 hello web 服務的 hello API/主要索引鍵。 這表示您只應該與您信任的人共用 hello 活頁簿。

在 hello 下列註解區段，或在任何提問我們[論壇](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409)。

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
