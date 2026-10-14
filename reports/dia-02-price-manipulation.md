<img width="1910" height="1066" alt="image" src="https://github.com/user-attachments/assets/1f6b3190-b570-4c0a-a7d1-58fad95eab39" /># Security Finding — Client-Side Price Manipulation

**Lab:** PortSwigger Web Security Academy — Excessive trust in client-side controls
**Category:** Business Logic Vulnerability
**Tool:** Burp Suite Community Edition
**Status:** Price manipulation confirmed in cart; checkout impact pending verification.

## 1. Description

The application trusts a user-controlled `price` parameter in the `POST /cart` request.

An attacker can modify this parameter to change the price displayed in the shopping cart without the server enforcing the product's original price.

## 2. Steps to Reproduce

1. Open the authorized PortSwigger laboratory.
2. Add product ID `4` to the shopping cart.
3. Capture the `POST /cart` request using Burp Suite.
4. Send the request to Burp Repeater.
5. With a clean cart, change the `price` parameter from `4469` to `100`.
6. Send the modified request.
7. Open the cart and observe the updated price.

**Original request body:**

```http
productId=4&redir=PRODUCT&quantity=1&price=4469
```

**Modified request body:**

```http
productId=4&redir=PRODUCT&quantity=1&price=100
```

## 3. Expected Result

The server should obtain the official product price from a trusted server-side source instead of accepting an arbitrary client-supplied price.

## 4. Actual Result

- HTTP response: `302 Found`.
- The product appeared in the shopping cart for `$1.00`.
- The original price was `$44.69`.

## 5. Security Impact

An attacker may manipulate product prices. If the manipulated price is also accepted during checkout, the vulnerability could enable purchases at unauthorized prices and cause financial losses.

## 6. Recommended Remediation

- Retrieve authoritative product prices on the server.
- Never trust client-supplied prices for financial transactions.
- Validate quantities, discounts and totals server-side.
- Recalculate and validate the total during checkout.
- Implement automated security tests for price manipulation.

## 7. Evidence

- [X] Screenshot of the original request.
<img width="1910" height="1066" alt="image" src="https://github.com/user-attachments/assets/17892f17-af40-458f-aef5-85cc55267705" />
- [X] Screenshot of the modified request in Burp Repeater.
<img width="1917" height="1046" alt="image" src="https://github.com/user-attachments/assets/f23073c8-77bd-42de-aa1a-bb92b45a9c87" />
- [X] Screenshot showing the manipulated cart price.
<img width="1881" height="1048" alt="image" src="https://github.com/user-attachments/assets/72816c50-f3df-4f7e-b96d-83e789c5ec60" />
- [X] Checkout result, if verified.
<img width="1868" height="971" alt="image" src="https://github.com/user-attachments/assets/ad47876c-b607-4a94-a5ef-e6615831e151" />


**Testing scope:** Authorized PortSwigger training laboratory only.
