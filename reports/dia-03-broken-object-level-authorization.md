# Security Finding — Broken Object Level Authorization (IDOR)

**Lab:** PortSwigger Web Security Academy — User ID controlled by request parameter  
**Category:** Access Control Vulnerability  
**Tool:** Chrome DevTools — Network  
**Status:** Vulnerability confirmed; lab solved.

## 1. Description

The application uses the user-controlled `id` query parameter in `GET /my-account` to select which account details to return.

While authenticated as the test user `wiener`, changing the parameter to `carlos` returned Carlos's account data. The server did not enforce object-level authorization for the requested account.

## 2. Steps to Reproduce

1. Open the authorized PortSwigger Web Security Academy lab.
2. Log in with the provided test account `wiener`.
3. In Chrome DevTools Network, inspect the account request:

   ```http
   GET /my-account?id=wiener
   ```

4. Confirm the response is `200 OK` and the page shows Wiener's account.
5. Keep the same authenticated session and change the requested account identifier:

   ```http
   GET /my-account?id=carlos
   ```

6. Send the request and inspect the status and page content.

**Baseline request:**

```http
GET /my-account?id=wiener
```

**Modified request:**

```http
GET /my-account?id=carlos
```

## 3. Expected Result

The server should verify that the authenticated user is authorized to access the requested account. A request by `wiener` for `carlos`'s account should be denied, with no protected account data in the response.

## 4. Actual Result

- Baseline request: `200 OK`, showing Wiener's account data.
- Modified request, in the same session: `200 OK`, showing Carlos's account data.
- The PortSwigger lab displayed **Solved** after the issue was exploited.

No API key, cookie, token, or unique lab-instance URL is included in this report.

## 5. Security Impact

An authenticated user could access another user's account data by changing an identifier in the request. In a real application, the impact would depend on the data and actions exposed through the affected endpoint.

## 6. Recommended Remediation

- Derive the authenticated user's identity from a server-validated session or token.
- Enforce authorization on the server for every requested object and action.
- Where appropriate, scope database queries to the authenticated user's authorized records instead of querying solely by a client-supplied ID.
- Return a controlled denial response without protected data when access is not allowed.
- Add regression tests for both authorized and unauthorized object access.

## 7. Evidence

- [X] Baseline request observed in Chrome DevTools Network: `GET /my-account?id=wiener`, `200 OK`.
- [X] Modified request observed in the same session: `GET /my-account?id=carlos`, `200 OK`, with Carlos's account data.
- [X] PortSwigger lab completion confirmed by the **Solved** message.

**Testing scope:** Authorized PortSwigger training laboratory only.

## References

- [PortSwigger Web Security Academy — User ID controlled by request parameter](https://portswigger.net/web-security/access-control/lab-user-id-controlled-by-request-parameter)
- [OWASP API Security Top 10 — API1:2023 Broken Object Level Authorization](https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/)
