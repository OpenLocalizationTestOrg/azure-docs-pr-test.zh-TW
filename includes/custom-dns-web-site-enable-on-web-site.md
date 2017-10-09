傳播 hello 記錄您的網域名稱之後，您必須使其與您 Web 應用程式。 使用下列步驟 tooenable hello 網域名稱使用網頁瀏覽器的 hello。

> [!NOTE]
> 它可能需要一些時間透過 DNS 系統 hello hello 上一個步驟 toopropagate 中建立 TXT 記錄。 Hello TXT 記錄已傳播之前，您無法加入 hello tooyour web 應用程式的網域名稱。 如果您使用 A 記錄，您無法加入 hello 記錄的網域名稱 tooyour web 應用程式，直到傳播到 hello 先前步驟中建立的 hello TXT 記錄。
> 
> 您可以使用服務，例如<a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> hello TXT 記錄的 tooverify 為止。
> 
> 

1. 在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello **Web 應用程式**索引標籤上，按一下您的 web 應用程式，hello 名稱，然後選取**自訂網域**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. 在 hello**自訂網域**刀鋒視窗中，按一下 **新增主機名稱**。
4. 使用 hello **Hostname**文字方塊 tooenter hello 網域名稱 tooassociate 與此 web 應用程式。
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. 按一下 [驗證] 。
6. 按一下 [驗證] 後，Azure 便會開始進行網域驗證工作流程。 這會檢查網域擁有權，以及主機名稱可用性和報告成功或規定 guidence 上 toofix hello 錯誤的方式與詳細的錯誤。    

此時，您應該瀏覽器中是無法 tooenter hello 自訂網域名稱，並查看它成功採用您 tooyour web 應用程式。

