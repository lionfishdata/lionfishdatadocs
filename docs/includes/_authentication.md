# Authentication

> Example authentication request

```shell
curl https://api.lionfishdata.com/v1/products/B00W9FLKTY/fast?retailer=amazon \
  -u <client_token>:
```

You can authenticate your account by including your client token in your request. Authentication is performed through HTTP Basic Auth, where the client token is the basic auth username value. You do not need to provide a password.

Make sure that you don't share your client token and that you keep it away from publicly accessible areas such as Github, client-side code, etc. Client tokens are tied to your account, so you will be charged for any orders or requests made with your client token. If you believe your client token has been compromised, please contact support@lionfishdata.com immediately.
