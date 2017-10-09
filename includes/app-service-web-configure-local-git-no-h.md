設定本機 Git 部署 toohello web 應用程式以 hello [az webapp 部署來源設定為本機的 git](/cli/azure/webapp/deployment/source#config-local-git)命令。

應用程式服務支援數種方式 toodeploy 內容 tooa web 應用程式，例如 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 Bitbucket。 針對這個快速入門，您要使用本機 Git 來進行部署。 這表示您使用 Git 命令 toopush 從本機儲存機制 tooa 儲存機制，在 Azure 中部署。 

下列命令，取代在 hello  *\<app_name >* web 應用程式的名稱。

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

hello 輸出具有下列格式的 hello:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

hello`<username>`為 hello[部署使用者](#configure-a-deployment-user)您在上一個步驟中建立。

複製 hello URI 所示。您將 hello 下一個步驟中使用它。
