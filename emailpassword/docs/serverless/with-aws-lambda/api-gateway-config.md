---
id: api-gateway-config
title: 4. Setting Up API Gateway & CORS
hide_title: true
---

<!-- COPY DOCS -->
<!-- ./thirdpartyemailpassword/docs/serverless/with-aws-lambda/api-gateway-config.md -->

# 4. Setting Up API Gateway & CORS

## 1) Create Proxy path for Auth APIs
- In your API Gateway, create a base path `/auth` and then create a proxy path `/auth/{proxy+}`.
- When creating the proxy path, enable both `Enable API Gateway CORS` and `Configure as proxy resource`.

<img src="/docs/static/assets/aws-api-gateway-proxy-create.png" />

## 2) Configure Auth APIs Lambda with API Gateway
- Create a POST method for the proxy route and associate the Auth APIs lambda function created in this [step](./auth-serverless)
- When associating the lambda function, enable the `Lambda Proxy integration` option if available to chose. This is important because this will tell API Gateway not to modify or transform the incoming request when forwarding it to the lambda function.

<img src="/docs/static/assets/aws-api-gateway-proxy-setup.png" />

## 3) Enable CORS for proxy path
- When enabling CORS for the proxy path, make sure to do the following:
    - Add `rid,fdi-version,anti-csrf` to the existing `Access-Control-Allow-Headers`
    - Set `Access-Control-Allow-Origin` to your website domain
    - Set `Access-Control-Allow-Credentials` to `'true'`. Don't miss out on those quotes else it won't get configured correctly.

<img src="/docs/static/assets/aws-api-gateway-proxy-cors.png" />