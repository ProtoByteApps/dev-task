# ProtoByte Developer Practical Task

## Overview
This task simulates a small, real-world feature we build at ProtoByte.
It is intentionally time-boxed to **~2 hours**.

We do **not** expect full production readiness.
We care more about **correctness, validation, edge-case awareness, and how you think** than UI polish.

---

## Task
Build a checkout total calculator with optional promo code support.

### Endpoint
Create a single endpoint:

- `POST /calculate-total`

---

## Input

```json
{
  "customer_email": "test@example.com",
  "items": [
    { "sku": "ABC123", "qty": 2, "unit_price": 19.99 },
    { "sku": "SHIP-ELIG-001", "qty": 1, "unit_price": 5.00 }
  ],
  "promo_code": "WELCOME10"
}
```

## Output

```json
{
  "subtotal": 44.98,
  "discount": 4.49,
  "total": 40.49,
  "applied_code": "WELCOME10",
  "messages": []
}
```

---

## Promo Codes

### 1) `WELCOME10`
- 10% off subtotal
- Maximum discount: £25
- Only for first-time customers (email has not used any promo before)

### 2) `FIVEOFF`
- £5 off
- Only if subtotal ≥ £50
- Total must not go below £0

### 3) `FLASH20`
- 20% off
- Only valid between 18:00–20:00 UK time
- Limited to first 100 uses total (global limit)

### 4) `FREESHIP`
- Does not change total
- Should return message: `"Free shipping applied"`
- Only if at least one item SKU starts with `SHIP-ELIG-`

---

## Persistence
Use either:
- Database, or
- File storage

To track:
- Promo usage by email (for first-time checks)
- Global usage count for `FLASH20` (must be safe under concurrent requests)

---

## Constraints
- Time-boxed to ~2 hours
- No authentication required
- No UI required
- Clean, readable code preferred over completeness

---

## Notes
- Validation matters.
- Handle edge cases gracefully.
- Assume money values should be handled safely.
- A short `README` should explain assumptions, trade-offs, and what you’d improve with more time.

---

## Delivery
Push changes to this repository (or provide a link to your fork).
Include a short `README` with:
- How to run it
- What you prioritised
- What you would improve with more time

