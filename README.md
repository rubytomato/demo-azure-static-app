# demo-azure-static-app

## azure-static-app

https://learn.microsoft.com/ja-jp/azure/static-web-apps/overview

### configuration

https://learn.microsoft.com/ja-jp/azure/static-web-apps/configuration

ファイル名: `staticwebapp.config.json`

#### アプリケーション全体へのアクセスを制限する

```json
{
  "routes": [
    {
      "route": "/*",
      "allowedRoles": ["authenticated"]
    }
  ],
  "responseOverrides": {
    "401": {
      "statusCode": 302,
      "redirect": "/.auth/login/aad"
    }
  }
}
```

#### Azure Static Web Apps でのカスタム認証

バージョン 1

```json
{
  "auth": {
    "identityProviders": {
      "azureActiveDirectory": {
        "userDetailsClaim": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",
        "registration": {
          "openIdIssuer": "https://login.microsoftonline.com/<TENANT_ID>",
          "clientIdSettingName": "AZURE_CLIENT_ID",
          "clientSecretSettingName": "AZURE_CLIENT_SECRET_APP_SETTING_NAME"
        }
      }
    }
  }
}
```

Microsoft Entra バージョン 2

```json
{
  "auth": {
    "identityProviders": {
      "azureActiveDirectory": {
        "registration": {
          "openIdIssuer": "https://login.microsoftonline.com/<TENANT_ID>/v2.0",
          "clientIdSettingName": "AZURE_CLIENT_ID",
          "clientSecretSettingName": "AZURE_CLIENT_SECRET_APP_SETTING_NAME"
        }
      }
    }
  }
}
```

**認証コールバック**

ログイン

```text
https://<YOUR_SITE>/.auth/login/aad/callback
```

ログアウト

```text
https://<YOUR_SITE>/.auth/logout/aad/callback
```

**ログイン、ログアウト、ユーザーの詳細**

ユーザの詳細

```text
/.auth/me
```


```text
https://<YOUR_SITE>/.auth/complete
```
## azure entra id

https://learn.microsoft.com/ja-jp/azure/static-web-apps/authentication-authorization
