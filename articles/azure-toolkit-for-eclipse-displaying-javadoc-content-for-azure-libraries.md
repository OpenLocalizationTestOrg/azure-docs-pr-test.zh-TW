---
title: "hello for Java 的 Azure 程式庫封裝 aaaDisplaying 在 Eclipse 中的 Javadoc 內容"
description: "如何 toodisplay hello Javadoc 內容在 Eclipse 中的 hello Azure 程式庫。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 8070023a24dc07eca8df906db5b8b662ceed6ccc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-hello-azure-libraries-package-for-java"></a>在 Eclipse 中顯示 Javadoc 內容 hello for Java 的 Azure 程式庫封裝
hello hello Azure Libraries for Java 的 Javadoc 內容可以透過建立 hello Javadoc 內容 toohello Azure Libraries for Java 的關聯檢視 Eclipse 環境中。 hello 下列步驟說明如何 toouse 這項功能在 Eclipse 內。

此程序假設您已經加入 hello Azure Library for Java tooyour 組建路徑。

## <a name="toodisplay-javadoc-content-in-eclipse-for-hello-azure-libraries-for-java"></a>toodisplay 在 Eclipse 中的 hello Azure Libraries for Java 的 Javadoc 內容
* 在 Eclipse 的專案總管中，在 hello**參考程式庫**專案的區段中，開啟 hello hello Azure Library for Java JAR 的內容功能表。 例如， **microsoft windowsazure api-0.1.0.jar** （hello 版本號碼可能會不同，取決於您已安裝哪些版本）。

* 按一下 [內容] 。

* 在 hello**屬性**對話方塊中的，hello 左窗格中，按一下**Javadoc 位置**。 hello **Javadoc 位置** 對話方塊隨即出現。

* 您可以指定 [Javadoc URL]或 [封存檔案中的 Javadoc]。

   * 如果您選擇 toospecify **Javadoc URL**，例如使用 hello Url **http://dl.windowsazure.com/javadoc**或**http://dl.windowsazure.com/storage/javadoc**。

   * 如果您選擇 toouse**封存中的 Javadoc**，您可以指定外部檔案或工作區檔案。

   選擇後視需要進行瀏覽/驗證。 hello 下列範例將 hello Azure Libraries for Java 與 hello 對應 Javadoc JAR 已下載至本機資料夾 tooa **c:\MyAzureJARs**。

   ![][ic553487]

* 選擇性步驟：按一下 [驗證]。 無法在此顯示以 hello Javadoc JAR 的潛在問題。

* 按一下 [確定] 。

一旦與 hello 程式庫相關聯，hello Javadoc 內容應該會顯示在您的 Eclipse IDE。 例如，如果`blob`定義的型別`CloudBlockBlob`您的程式碼內 hello 以下是您輸入時，會出現的 Javadoc 內容範例`blob.acquireLease`程式碼中：

![][ic553488]

## <a name="see-also"></a>另請參閱
[適用於 Eclipse 的 Azure 工具組][Azure Toolkit for Eclipse]

[在 Eclipse 中為 Azure 建立 Hello World 應用程式][Creating a Hello World Application for Azure in Eclipse]

[安裝 Azure Toolkit for Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

如需有關使用 Azure 與 Java 的詳細資訊，請參閱 hello [Azure Java 開發人員中心][Azure Java Developer Center]。

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
