# Format Number

Format numbers with locale support, currency, percentages, and precision control.

## Overview

The `<wa-format-number>` component formats numeric values with full internationalization support. It handles currencies, percentages, decimal precision, and locale-specific number formatting, making it perfect for displaying prices, statistics, and financial data.

## Installation

```bash
# Via CDN (cherry-pick)
import 'https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/components/format-number/format-number.js';
```

Or use the autoloader to load components automatically:

```html
<script type="module" src="https://early.webawesome.com/webawesome@3.0.0-beta.6/dist/webawesome.loader.js"></script>
```

## Basic Usage

```html
<!-- Format basic number -->
<wa-format-number value="1234.5"></wa-format-number>
<!-- Output: 1,234.5 -->

<!-- Format with specific decimal places -->
<wa-format-number
  value="1234.567"
  minimum-fraction-digits="2"
  maximum-fraction-digits="2">
</wa-format-number>
<!-- Output: 1,234.57 -->

<!-- Format percentage -->
<wa-format-number value="0.855" type="percent"></wa-format-number>
<!-- Output: 86% -->

<!-- Format currency -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="USD">
</wa-format-number>
<!-- Output: $1,234.50 -->
```

## Number Types

### Decimal (Default)

```html
<!-- Basic decimal -->
<wa-format-number value="1234"></wa-format-number>
<!-- Output: 1,234 -->

<!-- With decimals -->
<wa-format-number value="1234.567"></wa-format-number>
<!-- Output: 1,234.567 -->

<!-- Fixed decimals -->
<wa-format-number
  value="1234.5"
  minimum-fraction-digits="2"
  maximum-fraction-digits="2">
</wa-format-number>
<!-- Output: 1,234.50 -->
```

### Currency

```html
<!-- US Dollars -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="USD">
</wa-format-number>
<!-- Output: $1,234.50 -->

<!-- Euros -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="EUR">
</wa-format-number>
<!-- Output: €1,234.50 -->

<!-- British Pounds -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="GBP">
</wa-format-number>
<!-- Output: £1,234.50 -->

<!-- Japanese Yen -->
<wa-format-number
  value="1234"
  type="currency"
  currency="JPY">
</wa-format-number>
<!-- Output: ¥1,234 -->

<!-- Bitcoin -->
<wa-format-number
  value="0.5"
  type="currency"
  currency="BTC"
  minimum-fraction-digits="8">
</wa-format-number>
<!-- Output: ₿0.50000000 -->
```

### Percent

```html
<!-- Basic percentage -->
<wa-format-number value="0.75" type="percent"></wa-format-number>
<!-- Output: 75% -->

<!-- With decimals -->
<wa-format-number
  value="0.8567"
  type="percent"
  minimum-fraction-digits="2"
  maximum-fraction-digits="2">
</wa-format-number>
<!-- Output: 85.67% -->

<!-- Whole percentage -->
<wa-format-number
  value="0.8567"
  type="percent"
  maximum-fraction-digits="0">
</wa-format-number>
<!-- Output: 86% -->
```

## Decimal Precision

Control the number of decimal places:

```html
<!-- Minimum 2 decimals -->
<wa-format-number
  value="1234"
  minimum-fraction-digits="2">
</wa-format-number>
<!-- Output: 1,234.00 -->

<!-- Maximum 2 decimals -->
<wa-format-number
  value="1234.567"
  maximum-fraction-digits="2">
</wa-format-number>
<!-- Output: 1,234.57 -->

<!-- Fixed 2 decimals -->
<wa-format-number
  value="1234.5"
  minimum-fraction-digits="2"
  maximum-fraction-digits="2">
</wa-format-number>
<!-- Output: 1,234.50 -->

<!-- No decimals -->
<wa-format-number
  value="1234.567"
  maximum-fraction-digits="0">
</wa-format-number>
<!-- Output: 1,235 -->
```

## Locale Support

Format numbers according to different locales:

```html
<!-- US English -->
<wa-format-number value="1234567.89" locale="en-US"></wa-format-number>
<!-- Output: 1,234,567.89 -->

<!-- German (uses . for thousands, , for decimals) -->
<wa-format-number value="1234567.89" locale="de-DE"></wa-format-number>
<!-- Output: 1.234.567,89 -->

<!-- French (uses space for thousands, , for decimals) -->
<wa-format-number value="1234567.89" locale="fr-FR"></wa-format-number>
<!-- Output: 1 234 567,89 -->

<!-- Indian (uses lakhs/crores grouping) -->
<wa-format-number value="1234567.89" locale="en-IN"></wa-format-number>
<!-- Output: 12,34,567.89 -->
```

### Currency with Locale

```html
<!-- USD in US locale -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="USD"
  locale="en-US">
</wa-format-number>
<!-- Output: $1,234.50 -->

<!-- USD in German locale -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="USD"
  locale="de-DE">
</wa-format-number>
<!-- Output: 1.234,50 $ -->

<!-- EUR in French locale -->
<wa-format-number
  value="1234.50"
  type="currency"
  currency="EUR"
  locale="fr-FR">
</wa-format-number>
<!-- Output: 1 234,50 € -->
```

## Configuration

### Props / Attributes

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | number | `0` | No | The number to format |
| `locale` | string | - | No | Locale code for formatting (e.g., `en-US`, `de-DE`) |
| `type` | string | `'decimal'` | No | Number type: `decimal`, `currency`, `percent` |
| `currency` | string | - | No | Currency code (required when type is `currency`, e.g., `USD`, `EUR`, `GBP`) |
| `minimum-fraction-digits` | number | - | No | Minimum number of decimal places |
| `maximum-fraction-digits` | number | - | No | Maximum number of decimal places |
| `minimum-integer-digits` | number | - | No | Minimum number of integer digits |
| `minimum-significant-digits` | number | - | No | Minimum number of significant digits |
| `maximum-significant-digits` | number | - | No | Maximum number of significant digits |

## Examples

### Price Display

```html
<style>
  .product-card {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1.5rem;
    max-width: 300px;
  }
  .product-image {
    width: 100%;
    height: 200px;
    background-color: #f3f4f6;
    border-radius: 0.25rem;
    margin-bottom: 1rem;
  }
  .product-title {
    font-size: 1.125rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
  }
  .product-price {
    font-size: 1.5rem;
    font-weight: 700;
    color: #3b82f6;
    margin-bottom: 0.5rem;
  }
  .product-original-price {
    font-size: 1rem;
    color: #6b7280;
    text-decoration: line-through;
  }
  .product-discount {
    display: inline-block;
    background-color: #ef4444;
    color: white;
    padding: 0.25rem 0.5rem;
    border-radius: 0.25rem;
    font-size: 0.875rem;
    font-weight: 600;
    margin-left: 0.5rem;
  }
</style>

<div class="product-card">
  <div class="product-image"></div>
  <div class="product-title">Premium Wireless Headphones</div>
  <div class="product-price">
    <wa-format-number
      value="79.99"
      type="currency"
      currency="USD">
    </wa-format-number>
  </div>
  <div>
    <span class="product-original-price">
      <wa-format-number
        value="129.99"
        type="currency"
        currency="USD">
      </wa-format-number>
    </span>
    <span class="product-discount">
      Save
      <wa-format-number value="0.385" type="percent" maximum-fraction-digits="0">
      </wa-format-number>
    </span>
  </div>
</div>
```

### Statistics Dashboard

```html
<style>
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
  }
  .stat-card {
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1.5rem;
  }
  .stat-label {
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 0.5rem;
  }
  .stat-value {
    font-size: 2rem;
    font-weight: 700;
    color: #1f2937;
  }
  .stat-change {
    font-size: 0.875rem;
    margin-top: 0.5rem;
  }
  .stat-change.positive {
    color: #10b981;
  }
  .stat-change.negative {
    color: #ef4444;
  }
</style>

<div class="stats-grid">
  <div class="stat-card">
    <div class="stat-label">Total Revenue</div>
    <div class="stat-value">
      <wa-format-number
        value="247890.50"
        type="currency"
        currency="USD"
        maximum-fraction-digits="0">
      </wa-format-number>
    </div>
    <div class="stat-change positive">
      <wa-icon name="arrow-up"></wa-icon>
      <wa-format-number value="0.125" type="percent" maximum-fraction-digits="1">
      </wa-format-number>
      vs last month
    </div>
  </div>

  <div class="stat-card">
    <div class="stat-label">Conversion Rate</div>
    <div class="stat-value">
      <wa-format-number
        value="0.0347"
        type="percent"
        minimum-fraction-digits="2"
        maximum-fraction-digits="2">
      </wa-format-number>
    </div>
    <div class="stat-change positive">
      <wa-icon name="arrow-up"></wa-icon>
      <wa-format-number value="0.089" type="percent" maximum-fraction-digits="1">
      </wa-format-number>
      vs last month
    </div>
  </div>

  <div class="stat-card">
    <div class="stat-label">Active Users</div>
    <div class="stat-value">
      <wa-format-number value="12847"></wa-format-number>
    </div>
    <div class="stat-change negative">
      <wa-icon name="arrow-down"></wa-icon>
      <wa-format-number value="0.034" type="percent" maximum-fraction-digits="1">
      </wa-format-number>
      vs last month
    </div>
  </div>

  <div class="stat-card">
    <div class="stat-label">Average Order Value</div>
    <div class="stat-value">
      <wa-format-number
        value="87.23"
        type="currency"
        currency="USD">
      </wa-format-number>
    </div>
    <div class="stat-change positive">
      <wa-icon name="arrow-up"></wa-icon>
      <wa-format-number value="0.056" type="percent" maximum-fraction-digits="1">
      </wa-format-number>
      vs last month
    </div>
  </div>
</div>
```

### Invoice Table

```html
<style>
  .invoice-table {
    width: 100%;
    border-collapse: collapse;
    margin-bottom: 1rem;
  }
  .invoice-table th {
    text-align: left;
    padding: 0.75rem;
    background-color: #f3f4f6;
    font-weight: 600;
    border-bottom: 2px solid #e5e7eb;
  }
  .invoice-table td {
    padding: 0.75rem;
    border-bottom: 1px solid #e5e7eb;
  }
  .invoice-table tfoot td {
    font-weight: 600;
    background-color: #f9fafb;
  }
  .text-right {
    text-align: right;
  }
  .text-center {
    text-align: center;
  }
</style>

<table class="invoice-table">
  <thead>
    <tr>
      <th>Item</th>
      <th class="text-center">Quantity</th>
      <th class="text-right">Unit Price</th>
      <th class="text-right">Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Premium Support Package</td>
      <td class="text-center">
        <wa-format-number value="1"></wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="299.00" type="currency" currency="USD">
        </wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="299.00" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
    <tr>
      <td>API Credits (10,000)</td>
      <td class="text-center">
        <wa-format-number value="3"></wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="49.99" type="currency" currency="USD">
        </wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="149.97" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
    <tr>
      <td>Cloud Storage (1TB)</td>
      <td class="text-center">
        <wa-format-number value="2"></wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="19.99" type="currency" currency="USD">
        </wa-format-number>
      </td>
      <td class="text-right">
        <wa-format-number value="39.98" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td colspan="3" class="text-right">Subtotal:</td>
      <td class="text-right">
        <wa-format-number value="488.95" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
    <tr>
      <td colspan="3" class="text-right">
        Tax (<wa-format-number value="0.08" type="percent" maximum-fraction-digits="0"></wa-format-number>):
      </td>
      <td class="text-right">
        <wa-format-number value="39.12" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
    <tr>
      <td colspan="3" class="text-right">Total:</td>
      <td class="text-right">
        <wa-format-number value="528.07" type="currency" currency="USD">
        </wa-format-number>
      </td>
    </tr>
  </tfoot>
</table>
```

### Interactive Calculator

```html
<style>
  .calculator {
    max-width: 400px;
    border: 1px solid #e5e7eb;
    border-radius: 0.5rem;
    padding: 1.5rem;
  }
  .calculator-title {
    font-size: 1.25rem;
    font-weight: 600;
    margin-bottom: 1rem;
  }
  .calculator-field {
    margin-bottom: 1rem;
  }
  .calculator-result {
    margin-top: 1.5rem;
    padding: 1rem;
    background-color: #f3f4f6;
    border-radius: 0.25rem;
  }
  .result-label {
    font-size: 0.875rem;
    color: #6b7280;
    margin-bottom: 0.25rem;
  }
  .result-value {
    font-size: 1.5rem;
    font-weight: 700;
    color: #1f2937;
  }
</style>

<div class="calculator">
  <div class="calculator-title">Loan Calculator</div>

  <div class="calculator-field">
    <wa-input
      id="loanAmount"
      type="number"
      label="Loan Amount"
      value="50000">
    </wa-input>
  </div>

  <div class="calculator-field">
    <wa-input
      id="interestRate"
      type="number"
      label="Interest Rate (%)"
      value="5.5"
      step="0.1">
    </wa-input>
  </div>

  <div class="calculator-field">
    <wa-input
      id="loanTerm"
      type="number"
      label="Loan Term (years)"
      value="15">
    </wa-input>
  </div>

  <div class="calculator-result">
    <div class="result-label">Monthly Payment</div>
    <div class="result-value">
      <wa-format-number
        id="monthlyPayment"
        value="408.54"
        type="currency"
        currency="USD">
      </wa-format-number>
    </div>
  </div>

  <div class="calculator-result">
    <div class="result-label">Total Interest</div>
    <div class="result-value">
      <wa-format-number
        id="totalInterest"
        value="23537.20"
        type="currency"
        currency="USD">
      </wa-format-number>
    </div>
  </div>
</div>

<script>
  const loanAmount = document.getElementById('loanAmount');
  const interestRate = document.getElementById('interestRate');
  const loanTerm = document.getElementById('loanTerm');
  const monthlyPayment = document.getElementById('monthlyPayment');
  const totalInterest = document.getElementById('totalInterest');

  function calculateLoan() {
    const principal = parseFloat(loanAmount.value) || 0;
    const rate = (parseFloat(interestRate.value) || 0) / 100 / 12;
    const payments = (parseFloat(loanTerm.value) || 0) * 12;

    if (principal > 0 && rate > 0 && payments > 0) {
      const x = Math.pow(1 + rate, payments);
      const monthly = (principal * rate * x) / (x - 1);
      const total = monthly * payments;
      const interest = total - principal;

      monthlyPayment.value = monthly;
      totalInterest.value = interest;
    }
  }

  loanAmount.addEventListener('wa-input', calculateLoan);
  interestRate.addEventListener('wa-input', calculateLoan);
  loanTerm.addEventListener('wa-input', calculateLoan);
</script>
```

## Methods

The component updates automatically when properties change:

```javascript
const formatter = document.querySelector('wa-format-number');

// Update value
formatter.value = 1234.56;

// Change type
formatter.type = 'currency';
formatter.currency = 'EUR';

// Update precision
formatter.minimumFractionDigits = 2;
formatter.maximumFractionDigits = 2;

// Change locale
formatter.locale = 'de-DE';
```

## Best Practices

- ✅ Use appropriate decimal precision for the context (2 for currency, 0-2 for percentages)
- ✅ Always specify currency code when using type="currency"
- ✅ Respect user locale preferences when available
- ✅ Use consistent number formatting throughout your application
- ✅ Round appropriately for display (don't show false precision)
- ❌ Don't mix different currency symbols in the same view without clear context
- ❌ Avoid showing excessive decimal places for large numbers
- ❌ Don't perform calculations with formatted values (use raw numbers)
- ❌ Don't forget to handle zero, negative, and null values

## Accessibility

- The component outputs plain text that is naturally accessible to screen readers
- Consider adding context for screen reader users:

```html
<span aria-label="Price: 1,234 dollars and 50 cents">
  <wa-format-number value="1234.50" type="currency" currency="USD">
  </wa-format-number>
</span>
```

- For percentages, consider adding context:

```html
<span aria-label="Completion rate: 85 percent">
  <wa-format-number value="0.85" type="percent">
  </wa-format-number>
</span>
```

## Troubleshooting

### Currency Symbol Not Showing

**Problem:** Currency displays as number without symbol

**Solution:** Ensure you've set both type="currency" and the currency attribute

```html
<!-- ❌ Wrong: missing type -->
<wa-format-number value="1234.50" currency="USD"></wa-format-number>

<!-- ❌ Wrong: missing currency -->
<wa-format-number value="1234.50" type="currency"></wa-format-number>

<!-- ✅ Correct: both attributes -->
<wa-format-number value="1234.50" type="currency" currency="USD">
</wa-format-number>
```

### Incorrect Decimal Places

**Problem:** Number shows wrong number of decimal places

**Solution:** Set both minimum and maximum fraction digits for fixed precision

```html
<!-- ❌ May show variable decimals -->
<wa-format-number value="1234.5"></wa-format-number>

<!-- ✅ Fixed 2 decimals -->
<wa-format-number
  value="1234.5"
  minimum-fraction-digits="2"
  maximum-fraction-digits="2">
</wa-format-number>
```

### Value Not Updating

**Problem:** Displayed value doesn't change when updating

**Solution:** Ensure you're setting a numeric value, not a string

```javascript
// ❌ Wrong: string value
formatter.value = '1234.56';

// ✅ Correct: numeric value
formatter.value = 1234.56;
formatter.value = parseFloat(inputValue);
```

## Related

- [Format Bytes](./format-bytes.md)
- [Format Date](./format-date.md)
- [Input](./input.md)
- [Range](./range.md)
