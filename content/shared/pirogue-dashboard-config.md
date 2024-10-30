---
title: "Get or change the password of the dashboard"
---

The default username of the dashboard is `admin`.

As the password of the dashboard is randomly generated during the installation, the following command allows you to retrieve it.
```shell {title="Get the password of the dashboard"}
pirogue-admin-client dashboard get-configuration
```

The password of the dashboard can be changed with:
```shell {title="Change the password of the dashboard"}
pirogue-admin-client dashboard set-configuration --password 'mySuperSecretPassword!'
```

