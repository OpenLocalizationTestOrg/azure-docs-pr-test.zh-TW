---
title: "Azure Active Directory 網域服務： 更新 hello Azure 虛擬網路的 DNS 設定 |Microsoft 文件"
description: "開始使用 Azure Active Directory 網域服務"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>更新 hello Azure 虛擬網路的 DNS 設定
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>工作 4： 更新 hello Azure 虛擬網路的 DNS 設定
在 hello 之前設定工作，您已成功啟用 Azure Active Directory 網域服務目錄。 hello 下一個工作是 tooensure hello 虛擬網路內的電腦可以連線，並使用這些服務。 在本文中，您可以更新 hello DNS 伺服器設定您虛擬網路 toopoint toohello 兩個 IP 位址的 Azure Active Directory 網域服務位於 hello 虛擬網路。

> [!NOTE]
> 啟用 Azure Active Directory 網域服務的 hello 目錄之後，請注意 hello IP 位址的 Azure Active Directory 網域服務，會顯示在 hello**設定**您目錄的索引標籤。
>
>

tooupdate hello DNS 伺服器設定為已啟用 Azure Active Directory 網域服務，完成下列步驟的 hello hello 虛擬網路的：

1. 移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左窗格中，選取**網路**。  
    hello**網路**視窗隨即開啟。

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. 在 hello**虛擬網路**索引標籤，選取 hello 虛擬網路中您已啟用 Azure Active Directory 網域服務 tooview 其屬性。
4. 按一下 hello**設定** 索引標籤。

    ![虛擬網路視窗](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. 在 [hello **DNS 伺服器**區段中，輸入這兩個 hello hello 中所顯示的 IP 位址**網域服務**hello] 區段**設定**您目錄的索引標籤。
6. toosave hello DNS 伺服器設定為此虛擬網路，在 hello hello 視窗底部的 hello 工作窗格中按一下**儲存**。

   ![更新 hello hello 虛擬網路的 DNS 伺服器設定](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Hello 網路中的虛擬機器重新啟動之後，只能取得 hello 新的 DNS 設定。 如果您需要它們 tooget hello 更新 DNS 設定以立即開始，會觸發重新啟動依 hello 入口網站、 PowerShell 或 hello CLI。
>
>

## <a name="next-steps"></a>後續步驟
工作 5:[啟用密碼同步處理 tooAzure Active Directory 網域服務](active-directory-ds-getting-started-password-sync.md)
