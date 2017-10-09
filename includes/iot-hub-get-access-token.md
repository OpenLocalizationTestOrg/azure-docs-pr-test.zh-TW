## <a name="obtain-an-azure-resource-manager-token"></a>取得 Azure Resource Manager 權杖
Azure Active Directory 必須驗證您在使用 hello Azure 資源管理員的資源執行的所有 hello 工作。 hello 如下所示的範例會使用密碼驗證，如其他方法，請參閱[驗證 Azure 資源管理員要求][lnk-authenticate-arm]。

1. 新增下列程式碼 toohello hello **Main** Program.cs tooretrieve hello 應用程式識別碼和密碼，使用 Azure AD 中的語彙基元中的方法。
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. 建立**ResourceManagementClient**物件使用 hello 語彙基元，加入下列程式碼 toohello 結尾 hello hello **Main**方法：
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. 建立或取得指向 hello 您使用的資源群組的參考：
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx