傳播 hello 記錄您的網域名稱之後，您應該要能夠 toouse 您可以將自訂網域名稱的瀏覽器 tooverify 是使用的 tooaccess 在 Azure App Service web 應用程式。

> [!NOTE]
> 可能需要一些時間，您的 CNAME toopropagate 透過 hello DNS 系統。 您可以使用服務，例如<a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> hello CNAME 的 tooverify 為止。
> 
> 

如果您在 Traffic Manager 端點並不加入您的 web 應用程式，您必須進行才能執行名稱解析，為 hello 自訂網域名稱的路由 tooTraffic 管理員。 然後，traffic Manager 路由傳送 tooyour web 應用程式。 使用中的 hello 資訊[新增或刪除端點](../articles/traffic-manager/traffic-manager-endpoints.md)tooadd web 應用程式為您的 Traffic Manager 設定檔中的端點。

> [!NOTE]
> 如果在新增端點時未列出您的 Web 應用程式，請確認模式是設為 [ **標準** ] App Service 計劃模式。 您必須使用**標準**順序 toowork 使用 Traffic Manager 中的 web 應用程式的模式。
> 
> 

1. 在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello **Web 應用程式**索引標籤上，按一下您 web 應用程式，選取 hello 名稱**設定**，然後選取**自訂網域**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. 在 hello**自訂網域**刀鋒視窗中，按一下 **新增主機名稱**。
4. 使用 hello **Hostname**文字方塊 tooenter hello Traffic Manager 網域名稱 tooassociate 與此 web 應用程式。
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. 按一下**驗證**toosave hello 網域名稱設定。
6. 按一下 [驗證] 後，Azure 便會開始進行網域驗證工作流程。 這會檢查網域擁有權，以及主機名稱可用性和報告成功或規定 guidence 上 toofix hello 錯誤的方式與詳細的錯誤。    
7. 成功驗證後**新增 hostname**按鈕會變成作用中，您也可以 toohello 指派主機名稱。 現在您可以瀏覽 tooyour 瀏覽器中的自訂網域名稱。 您現在應會看到您應用程式正在使用您的自訂網域名稱執行。 
   
   一旦組態完成之後，hello 自訂網域名稱將會列在 hello**網域名稱**web 應用程式 > 一節。

此時，您也應該能夠 tooenter hello Traffic Manager 網域名稱在瀏覽器並查看它成功採用您 tooyour web 應用程式。

