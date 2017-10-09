## <a name="push-tooazure-from-git"></a>從 Git 推送 tooAzure

新增 Azure 遠端 tooyour 本機 Git 儲存機制。

```bash
git remote add azure <URI from previous step>
```

將 Azure 遠端 toodeploy toohello 推送您的應用程式。 系統提示您先前建立 hello 部署使用者時所建立的 hello 密碼。 請確認您輸入您在建立 hello 密碼[部署使用者設定](#configure-a-deployment-user)，不會 hello toolog 用於 toohello Azure 入口網站的密碼。

```bash
git push azure master
```

hello 上述命令會顯示資訊的類似 toohello 下列範例：
