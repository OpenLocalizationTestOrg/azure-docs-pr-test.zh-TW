---
title: "Azure Active Directory Domain Services︰啟用 Azure Active Directory Domain Services | Microsoft Docs"
description: "啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c659da59-f4b5-4edd-b702-1727a8ccb36f
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/28/2017
ms.author: maheshu
ms.openlocfilehash: 6263eb1849808a7c85e572e1046bc9039362dd9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>啟用 Azure Active Directory 網域服務使用 hello Azure 傳統入口網站

## <a name="task-3-enable-azure-active-directory-domain-services"></a>工作 3︰啟用 Azure Active Directory Domain Services
在這個工作中，以啟用 Azure Active Directory 網域服務 (Azure AD DS) 為您的目錄執行下列步驟的 hello:

1. 移 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. Hello 左窗格中，選取 [hello **Active Directory** ] 按鈕。
3. 選取您要為其 Azure AD DS tooenable hello Azure Active Directory (Azure AD) 租用 （目錄）。

    ![選取 Azure AD 目錄](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. 在 [hello**預覽目錄**頁面上，按一下 hello**設定**] 索引標籤。

    ![設定目錄的索引標籤](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. 在下**網域服務**，變更 hello**啟用這個目錄的網域服務**太選項**是**。  
    在 hello 頁面上出現其他的 Azure Active Directory 網域服務組態選項。

    ![啟用網域服務](./media/active-directory-domain-services-getting-started/enable-domain-services.png)

   > [!NOTE]
   > 當您啟用 Azure Active Directory 網域服務租用戶時，Azure AD 會產生並儲存 hello Kerberos and NTLM 認證雜湊所需的驗證使用者。
   >
   >
6. 指定 hello**網域服務的 DNS 網域名稱**。

   * hello 目錄 hello 預設網域名稱 (與**。 onmicrosoft.com**尾碼) 預設會選取。

   * hello 清單包含所有已設定的 Azure AD 目錄的網域，包括驗證和未驗證網域上 hello 設定**網域** 索引標籤。

   * 您也可以輸入自訂網域名稱。 在此範例中，hello 自訂網域名稱是*contoso100.com*。

     > [!WARNING]
     > hello 前置詞指定的網域名稱 (例如， *contoso100*在 hello *contoso100.com*網域名稱) 必須包含 15 個字元。 您無法使用包含超過 15 個字元的前置詞建立 Azure Active Directory Domain Services。
     >
     >
7. 請確定您已選擇 hello 受管理的網域不存在 hello 虛擬網路中的 hello DNS 網域名稱。 具體來說，是否檢查 toosee:

   * 您已經擁有網域以 hello 相同 hello 虛擬網路上的 DNS 網域名稱。

   * hello 您選取的虛擬網路有 VPN 連線與內部部署網路，且您必須以 hello 網域相同的 DNS 網域名稱，在內部部署網路上。

   * Hello 虛擬網路上有該名稱與現有的雲端服務。
8. 選取您想要使用的 Azure Active Directory 網域服務 toobe 的虛擬網路。 選取 hello 虛擬網路和專用子網路，您可以在 hello**連接網域服務 toothis 虛擬網路**下拉式清單。 也請考慮下列 hello:

   * 請確定您已指定該 hello 虛擬網路屬於 tooan 支援的 Azure Active Directory 網域服務的 Azure 區域。 tooascertain hello Azure Active Directory 網域服務可使用的 Azure 區域，請參閱[依地區的 Azure 服務](https://azure.microsoft.com/regions/#services/)。

   * 虛擬網路屬於 tooa 地區不支援 Azure Active Directory 網域服務，不要顯示 hello 下拉式清單中。

   * 用於 Azure Active Directory 網域服務中的 hello 虛擬網路內的專用子網路。 請勿*不*選取 hello 閘道子網路。 請參閱[網路考量](active-directory-ds-networking.md)。

   * 同樣地，使用 Azure 資源管理員所建立的虛擬網路並不會顯示 hello 下拉式清單中。 Resource Manager 型虛擬網路目前不為 Azure Active Directory Domain Services 所支援。
9. tooenable Azure Active Directory 網域服務，在 hello hello 頁面底部的 hello 工作窗格中按一下**儲存**。
    * 正在為您的目錄啟用 Azure Active Directory 網域服務，而 hello 頁面會顯示狀態*暫止*。

        ![啟用 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/enable-domain-services-pendingstate.png)

        > [!NOTE]
        > Azure Active Directory Domain Services 可針對您的受管理網域提供高可用性。 啟用 Azure Active Directory 網域服務後，hello hello 虛擬網路上可用服務都在其所在網域的 IP 位址會是一次顯示的一個。 hello 第二個 IP 位址會顯示 hello 後不久前，很快就 hello 服務可讓您的網域的高可用性。 當設定高可用性時，作用中的網域，您應該會看到兩個 IP 位址在 hello**網域服務**區段 hello**設定** 索引標籤。
        >
        >
    * 在約 20 too30 分鐘 hello 在其所在網域服務是在 hello 虛擬網路中可用的第一個 IP 位址後**IP 位址**欄位 hello**設定**頁面。

        ![顯示第一次佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-firstdc-available.png)
    * 當高可用性是您的網域內運作時，兩個 IP 位址會顯示在 [hello] 頁面上。 在所選虛擬網路上，從這兩個 IP 位址可使用您的受管理網域。

10. 請注意 hello 兩個 IP 位址，以便您可以更新 hello DNS 設定虛擬網路。 如此可讓 hello 進行運算，例如網域加入虛擬網路 tooconnect toohello 網域上的虛擬機器。

    ![顯示兩個已佈建 IP 的 [網域服務] 視窗](./media/active-directory-domain-services-getting-started/domain-services-enabled-bothdcs-available.png)

> [!NOTE]
> 根據您的 Azure AD 租用戶 （例如，hello 數字的使用者或群組） 的 hello 大小，同步處理 tooyour 受管理的網域會需要一些時間。 此同步處理程序會在 hello 背景。 針對大型的租用戶提供數以萬計的物件，可能需要一天，或兩個的所有使用者、 群組成員資格和認證 toobe 同步處理。
>
>

## <a name="next-step"></a>後續步驟
[工作 4： 更新 hello hello Azure 虛擬網路的 DNS 設定](active-directory-ds-getting-started-update-dns.md)
