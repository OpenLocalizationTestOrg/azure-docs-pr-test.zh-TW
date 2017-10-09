## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="7d6f0-101">取得 Azure Resource Manager 權杖</span><span class="sxs-lookup"><span data-stu-id="7d6f0-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="7d6f0-102">Azure Active Directory 必須驗證您在使用 hello Azure 資源管理員的資源執行的所有 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="7d6f0-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="7d6f0-103">hello 如下所示的範例會使用密碼驗證，如其他方法，請參閱[驗證 Azure 資源管理員要求][lnk-authenticate-arm]。</span><span class="sxs-lookup"><span data-stu-id="7d6f0-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="7d6f0-104">新增下列程式碼 toohello hello **Main** Program.cs tooretrieve hello 應用程式識別碼和密碼，使用 Azure AD 中的語彙基元中的方法。</span><span class="sxs-lookup"><span data-stu-id="7d6f0-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
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
2. <span data-ttu-id="7d6f0-105">建立**ResourceManagementClient**物件使用 hello 語彙基元，加入下列程式碼 toohello 結尾 hello hello **Main**方法：</span><span class="sxs-lookup"><span data-stu-id="7d6f0-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="7d6f0-106">建立或取得指向 hello 您使用的資源群組的參考：</span><span class="sxs-lookup"><span data-stu-id="7d6f0-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
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