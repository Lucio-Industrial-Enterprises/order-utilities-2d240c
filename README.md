# Warehouse tools

Small Python utilities for warehouse order and shipping workflows.

Run the tests with `python3 -m unittest discover -s tests -v`.

## Shipping

`shipping_quote(weight_kg, zone, service="standard")` returns a delivery quote
in dollars.

| Parameter | Values | Notes |
|-----------|--------|-------|
| `weight_kg` | positive float | Parcel weight |
| `zone` | `"local"`, `"regional"` | Delivery zone |
| `service` | `"standard"` *(default)*, `"express"` | Express adds $7.00 |

**Examples (Python)**

```python
from warehouse.rates import shipping_quote

shipping_quote(2, "local")                    # → 8.0  (standard)
shipping_quote(2, "local", service="express") # → 15.0 (express)
```

**CLI**

```
python -m warehouse.cli <weight_kg> <zone> [--service {standard,express}]
```

```
$ python -m warehouse.cli 2 local
$8.00
$ python -m warehouse.cli 2 local --service express
$15.00
```

Zones are `local` and `regional`; weights must be positive; unknown services
are rejected with a `ValueError`.
