---
title: "在 Azure Active Directory aaaNamed 位置 |Microsoft 文件"
description: "藉由設定名為位置，您可以避免 IP 位址，您的組織所擁有的產生誤判 hello 不可能的旅遊 tooatypical 位置風險事件類型。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Azure Active Directory 中的具名位置

以 hello 名為位置的 Azure Active Directory 的功能，您可以在您的組織中標籤受信任的 IP 位址範圍。 在您的環境，您可以使用具名的位置 hello 內容中的 hello 偵測[風險事件](active-directory-reporting-risk-events.md)。 hello 功能有助於減少 hello hello 報告誤判數目*不可能的旅遊 tooatypical 位置*風險事件類型。 

## <a name="configuration"></a>組態

tooconfigure 具名的位置：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)全域系統管理員身分。

2. 在 [hello] 左窗格中，按一下 [ **Azure Active Directory**。

    ![hello 左窗格中的 hello Azure Active Directory 連結](./media/active-directory-named-locations/01.png)

3. 在 [hello **Azure Active Directory**刀鋒視窗中的，在 hello**安全性**區段中，按一下**條件式存取**。

    ![hello 條件式存取命令](./media/active-directory-named-locations/05.png)


4. 在 [hello**條件式存取**刀鋒視窗中的，在 hello**管理**區段中，按一下**名為位置**。

    ![hello 具名位置命令](./media/active-directory-named-locations/06.png)


5. 在 [hello**名為位置**刀鋒視窗中，按一下 [**新位置**。

    ![hello 新位置的命令](./media/active-directory-named-locations/07.png)


6. 在 hello**新增**刀鋒視窗中，執行下列 hello:

    ![hello 新刀鋒視窗](./media/active-directory-named-locations/08.png)

    a. 在 [hello**名稱**方塊中，輸入您的具名位置的名稱。

    b. 在 [hello **IP 範圍**方塊中，輸入 IP 範圍。 hello IP 範圍必須在 hello toobe*無類別網域間路由*(選擇 CIDR) 格式。  

    c. 按一下 [建立] 。



## <a name="what-you-should-know"></a>您應該知道的事情

**大量更新**： 當您建立或更新具名的位置，大量更新，您可以上傳或下載 CSV 檔案與 hello IP 範圍。 上傳 hello 檔案 toohello 清單，而非覆寫 hello 清單中加入 hello IP 範圍。

![hello 上傳和下載連結](./media/active-directory-named-locations/09.png)


**限制**： 您可以定義最多 60 具名的位置，請使用其中一個 IP 範圍指派 tooeach。 如果您有一個具名的位置設定時，您可以為它定義總 too500 IP 範圍。


## <a name="next-steps"></a>後續步驟

toolearn 詳細資料的風險事件，請參閱[Azure Active Directory 風險事件](active-directory-reporting-risk-events.md)。

