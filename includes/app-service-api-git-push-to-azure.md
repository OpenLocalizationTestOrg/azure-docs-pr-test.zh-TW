您 API 應用程式使用 hello Azure CLI tooget hello 遠端部署 URL。 下列命令，取代在 hello  *\<app_name >* web 應用程式的名稱。

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

設定您本機 Git 部署 toobe 無法 toopush toohello 遠端。

```bash
git remote add azure <URI from previous step>
```

將 Azure 遠端 toodeploy toohello 推送您的應用程式。 系統提示您先前建立 hello 部署使用者時所建立的 hello 密碼。 請確定您輸入 hello 快速入門中，在中建立的 hello 密碼而不會 hello toolog 用於 toohello Azure 入口網站的密碼。

```bash
git push azure master
```
