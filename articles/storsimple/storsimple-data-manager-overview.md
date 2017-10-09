---
title: "aaaMicrosoft Azure StorSimple Data Manager 概觀 |Microsoft 文件"
description: "提供 hello StorSimple Data Manager 服務 （私人預覽中） 的概觀"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>StorSimple Data Manager 概觀 (私人預覽)

## <a name="overview"></a>概觀

Microsoft Azure StorSimple 是混合式雲端儲存體解決方案位址 hello 通常與檔案共用相關聯的非結構化資料的複雜性。 StorSimple 會使用雲端儲存體，當做 hello 的延伸模組在內部部署解決方案和自動層 hello 在內部部署儲存體和雲端存放裝置之間的資料。 整合資料保護與本機和雲端快照集，可以降低對 hello 正在擴張的儲存體基礎結構需求。 封存和災害復原也是無縫式與 hello 做為異地位置的雲端中。

我們在本文中導入的 hello 資料轉換服務可讓您 tooseamlessly 存取 hello StorSimple hello 雲端中的資料。 此服務從 StorSimple 提供 Api tooextract 資料，並加以呈現 tooother Azure 服務，可以輕易地取用的格式。 支援在這個預覽中的 hello 格式是 Azure blob 和 Azure Media Services 資產。 此轉換可讓您 tooeasily 網路服務，例如 Azure Media Services、 Azure HDInsight、 Azure Machine Learning 中，與 Azure 搜尋 toooperate 資料 StorSimple 8000 系列的內部部署裝置上。

相關的高階區塊圖如下所示。

![高階圖表](./media//storsimple-data-manager-overview/high-level-diagram.png)

本文說明如何註冊此服務的私人預覽。 它也會說明如何使用這個 hello 雲端中使用 StorSimple 資料和其他 Azure 服務的服務 toowrite 應用程式。

## <a name="sign-up-for-data-manager-preview"></a>註冊資料管理員預覽
註冊 hello 資料管理員服務之前，請檢閱下列先決條件的 hello。

### <a name="prerequisites"></a>必要條件

本練習假設您有
* 有效的 Azure 訂用帳戶。
* 存取 tooa 註冊 StorSimple 8000 系列裝置
* 所有 hello 與 hello StorSimple 8000 系列裝置相關聯的索引鍵。

### <a name="sign-up"></a>註冊

hello StorSimple Data Manager 是在私人預覽。 執行下列步驟 toosign 註冊此服務的私人預覽中的 hello:

1.  以登入 hello Azure 入口網站在 hello StorSimple Data Manager 擴充功能： [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)。 使用您的 Azure 認證 toolog 中。

2.  按一下 hello  **+** 圖示 toocreate 服務。 按一下**儲存體**，然後按一下**看到所有**在 hello 刀鋒視窗中開啟。

    ![搜尋 StorSimple Data Manager 圖示](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. 您會看到 hello StorSimple 資料管理員圖示。

    ![選取 StorSimple Data Manager 圖示](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. 按一下 StorSimple Data Manager 圖示，然後按一下建立。 選取您想 tooenable hello private preview 中，然後按一下 hello 訂閱**我要註冊 ！**

    ![我要註冊](./media/storsimple-data-manager-overview/sign-me-up.png)

5. 這會將要求 tooonboard 您。 我們會儘速讓您加入。 在您的訂用帳戶啟用後，您就可以建立 StorSimple Data Manager 服務。

6. tooeasily 存取 hello StorSimple Data Manager 服務，請按一下 hello 星狀圖示 toopin 它 tooyour 我的最愛。

    ![存取 StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>後續步驟

[您的資料使用 StorSimple 資料管理員 UI tootransform](storsimple-data-manager-ui.md)。
