1. 在 hello 登入[Azure 入口網站]。
2. 按一下 [+ 新增]  >  [Web + 行動]  >  [行動應用程式]，然後為您的行動應用程式後端提供名稱。
3. Hello**資源群組**，選取現有的資源群組，或建立新的 (使用 hello 與您的應用程式同名)。 
   
    您可以選取另一個 App Service 方案或建立新方案。 如需詳細資訊，應用程式服務計劃和如何 toocreate 新計劃中不同的定價層，然後在您想要的位置，請參閱[Azure App Service 方案深入概觀](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。
4. Hello **App Service 方案**，hello 預設計劃 (在 hello[標準層](https://azure.microsoft.com/pricing/details/app-service/)) 已選取。 您也可以選取不同的方案，或[建立新的方案](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan)。 hello 應用程式服務方案設定會決定 hello[位置、 功能、 成本及計算資源](https://azure.microsoft.com/pricing/details/app-service/)與您的應用程式相關聯。 
   
    當您決定 hello 計劃之後，請按一下**建立**。 這會建立 hello 行動裝置應用程式後端。 
5. 在 hello**設定**按一下刀鋒視窗中的 hello 新的行動裝置應用程式後端**快速入門**> 您的用戶端應用程式平台 >**連接資料庫**。 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. 在 hello**加入資料連接**刀鋒視窗中，按一下**SQL Database** > **建立新的資料庫**，類型 hello 資料庫**名稱**，選擇定價層，然後按一下 **伺服器**。  您可以重複使用這個新資料庫。 如果您已經有 hello 資料庫相同的位置，您可以改為選擇**使用現有的資料庫**。 hello 使用不同的位置中的資料庫時，不建議到期 toobandwidth 成本以及較高的延遲。
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. 在 hello**新伺服器**刀鋒視窗中，在 hello 中輸入唯一的伺服器名稱**伺服器名稱**欄位中提供的登入和密碼，請檢查**允許 azure 服務 tooaccess 伺服器**，然後按一下**確定**。 這會建立 hello 新資料庫。
8. 在 hello**加入資料連接**刀鋒視窗中，按一下**連接字串**，輸入 hello 登入和密碼值，為您的資料庫，然後按一下**確定**。 請稍候幾分鐘後再繼續成功部署的 hello 資料庫 toobe。

<!-- URLs. -->
[Azure 入口網站]: https://portal.azure.com/
