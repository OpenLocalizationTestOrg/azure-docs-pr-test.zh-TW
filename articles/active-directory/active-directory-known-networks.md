---
title: "hello Azure 傳統入口網站中的 aaaKnown 網路 |Microsoft 文件"
description: "藉由設定已知的網路，您可以避免必須包含在 hello 從多個地理位置登入 」 和 「 從具有可疑活動報告的 IP 位址登入您組織所擁有的 IP 位址。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>已知的網路

> [!div class="op_single_selector"]
> * [Azure 傳統入口網站](active-directory-known-networks.md)
> * [Azure 入口網站](active-directory-known-networks-azure-portal.md)
> 
> 


您可以使用 Azure Active Directory 的存取和使用方式報表 toogain 掌握 hello 完整性與安全性貴組織的目錄。 利用此資訊，目錄管理員更能夠判斷可能發生安全性風險的地方，讓他們做充裕的計畫 toomitigate 這些風險。

它有可能在 hello"*從多個地理位置登入*"和"*來自 IP 位址的登入具有可疑活動*」 報告不正確的旗標實際擁有的 IP 位址您組織。 

比方說，這可以發生在下列情形： 

* 波士頓辦公室中的使用者登入遠端 tooyour 資料中心 San Francisco 觸發程序 hello 「 從多個地理位置登入 」 報告中 
* 您組織的使用者嘗試 toosign 入數次以不正確的密碼觸發程序 hello 「 從具有可疑活動的 IP 位址的登入 」 報告 

tooprevent 這種情況下，從產生誤導安全性報告，您應該加入已知的 IP 位址範圍 toohello 清單貴組織的公用 IP 位址。    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>tooadd 貴組織的公用 IP 位址範圍，請執行下列步驟的 hello:

1. 登入 toohello [Azure 管理入口網站](https://manage.windowsazure.com)。

2. 在 hello 左窗格中，按一下  **Active Directory**。 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-01.png)

3. 在 hello**目錄**索引標籤上，選取您的目錄。

4. 在 hello 最上層顯示 hello 功能表上，按一下**設定**。 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-02.png)

5. Hello 設定索引標籤上，前往 太**您組織公用 IP 位址範圍** 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-03.png)

6. 按一下 新增已知的 IP 位址範圍 。

7. 在 hello 對話方塊出現，新增您的位址範圍，然後按一下 hello 核取記號按鈕完成時。 

    ![已知的網路](./media/active-directory-known-networks/known-netwoks-04.png)

**其他資源：**

* [檢視存取和使用情況報告](active-directory-view-access-usage-reports.md)
* [從具有可疑活動的 IP 位址登入](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [從多個地理區域登入](active-directory-reporting-sign-ins-from-multiple-geographies.md)

