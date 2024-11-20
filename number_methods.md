# Complete JavaScript Number Methods Guide

## 1. Number Object Creation Methods

| Method | Description | Example |
|--------|-------------|----------|
| `Number()` | Creates a number | `const num = Number('123')` |
| `Number.parseInt()` | Parses integer | `Number.parseInt('123.45')` // 123 |
| `Number.parseFloat()` | Parses float | `Number.parseFloat('123.45')` // 123.45 |
| `Number.isInteger()` | Checks if integer | `Number.isInteger(5)` // true |
| `Number.isFinite()` | Checks if finite | `Number.isFinite(Infinity)` // false |

### Creation Examples:

```javascript
// Example 1: Different ways to create numbers
const num1 = Number('123');      // From string
const num2 = Number(true);       // From boolean (1)
const num3 = Number(false);      // From boolean (0)
const num4 = Number(null);       // 0
const num5 = Number(undefined);  // NaN
const num6 = Number('abc');      // NaN

console.log("Number creations:");
console.log(num1);  // 123
console.log(num2);  // 1
console.log(num3);  // 0
console.log(num4);  // 0
console.log(num5);  // NaN
console.log(num6);  // NaN

// Example 2: Parsing numbers
const int1 = Number.parseInt('123.45');    // 123
const int2 = Number.parseInt('123abc');    // 123
const int3 = Number.parseInt('abc123');    // NaN
const float1 = Number.parseFloat('123.45'); // 123.45
const float2 = Number.parseFloat('123.45abc'); // 123.45
const float3 = Number.parseFloat('abc123.45'); // NaN

// Example 3: Number validation
console.log(Number.isInteger(5));      // true
console.log(Number.isInteger(5.5));    // false
console.log(Number.isFinite(10/2));    // true
console.log(Number.isFinite(10/0));    // false
console.log(Number.isNaN(NaN));        // true
console.log(Number.isNaN('abc'));      // false (different from global isNaN())
```

## 2. Number Properties Reference

| Property | Description | Value |
|----------|-------------|--------|
| `Number.EPSILON` | Smallest interval between numbers | ≈ 2.22044604925031e-16 |
| `Number.MAX_VALUE` | Largest representable number | ≈ 1.7976931348623157e+308 |
| `Number.MIN_VALUE` | Smallest representable positive number | ≈ 5e-324 |
| `Number.MAX_SAFE_INTEGER` | Maximum safe integer | 9007199254740991 |
| `Number.MIN_SAFE_INTEGER` | Minimum safe integer | -9007199254740991 |
| `Number.POSITIVE_INFINITY` | Represents infinity | Infinity |
| `Number.NEGATIVE_INFINITY` | Represents negative infinity | -Infinity |
| `Number.NaN` | Not a Number | NaN |

```javascript
// Example: Using Number properties
function checkNumberLimits(num) {
    return {
        isSafeInteger: Number.isSafeInteger(num),
        exceedsMaxValue: num > Number.MAX_VALUE,
        exceedsMinValue: num < Number.MIN_VALUE,
        isInfinite: !Number.isFinite(num),
        withinSafeRange: num >= Number.MIN_SAFE_INTEGER && 
                        num <= Number.MAX_SAFE_INTEGER
    };
}

console.log(checkNumberLimits(9007199254740991n));
console.log(checkNumberLimits(Number.MAX_VALUE * 2));
```

## 3. Number Instance Methods

| Method | Description | Example |
|--------|-------------|----------|
| `toFixed()` | Format decimals | `(123.456).toFixed(2)` // "123.46" |
| `toPrecision()` | Format to length | `(123.456).toPrecision(4)` // "123.5" |
| `toString()` | Convert to string | `(123).toString()` // "123" |
| `toExponential()` | Scientific notation | `(123.456).toExponential()` // "1.23456e+2" |
| `toLocaleString()` | Locale format | `(1234.56).toLocaleString()` // "1,234.56" |

### Formatting Examples:

```javascript
// Example 1: Number formatting
function formatNumber(num) {
    return {
        fixed2: num.toFixed(2),
        precision4: num.toPrecision(4),
        exponential: num.toExponential(),
        binary: num.toString(2),
        octal: num.toString(8),
        hex: num.toString(16),
        localeString: num.toLocaleString()
    };
}

console.log(formatNumber(123.456789));

// Example 2: Currency formatting
function formatCurrency(amount, currency = 'USD', locale = 'en-US') {
    return new Intl.NumberFormat(locale, {
        style: 'currency',
        currency: currency
    }).format(amount);
}

console.log(formatCurrency(123456.789));       // "$123,456.79"
console.log(formatCurrency(123456.789, 'EUR', 'de-DE')); // "123.456,79 €"

// Example 3: Percentage formatting
function formatPercentage(number, decimals = 2) {
    return new Intl.NumberFormat(undefined, {
        style: 'percent',
        minimumFractionDigits: decimals,
        maximumFractionDigits: decimals
    }).format(number);
}

console.log(formatPercentage(0.12345));  // "12.35%"
```

## 4. Math Operations and Rounding

```javascript
// Example 1: Basic rounding methods
function roundingExamples(num) {
    return {
        ceil: Math.ceil(num),      // Round up
        floor: Math.floor(num),    // Round down
        round: Math.round(num),    // Round to nearest
        trunc: Math.trunc(num)     // Remove decimals
    };
}

console.log(roundingExamples(3.7));  // {ceil: 4, floor: 3, round: 4, trunc: 3}
console.log(roundingExamples(-3.7)); // {ceil: -3, floor: -4, round: -4, trunc: -3}

// Example 2: Precise calculations
function preciseCalculations(a, b) {
    // Handle floating point precision issues
    const multiply = (x, y) => {
        const factor = Math.pow(10, 10);
        return Math.round(x * factor) * Math.round(y * factor) / (factor * factor);
    };
    
    const divide = (x, y) => {
        const factor = Math.pow(10, 10);
        return Math.round(x * factor) / Math.round(y * factor);
    };
    
    return {
        standard: {
            multiply: a * b,
            divide: a / b
        },
        precise: {
            multiply: multiply(a, b),
            divide: divide(a, b)
        }
    };
}

console.log(preciseCalculations(0.1, 0.2));

// Example 3: Random number generation
function randomNumberGenerator(min, max, options = {}) {
    const {
        isInteger = false,
        decimals = 2,
        exclude = []
    } = options;
    
    let result;
    do {
        if (isInteger) {
            result = Math.floor(Math.random() * (max - min + 1)) + min;
        } else {
            result = Math.random() * (max - min) + min;
            result = Number(result.toFixed(decimals));
        }
    } while (exclude.includes(result));
    
    return result;
}

console.log(randomNumberGenerator(1, 10, { isInteger: true }));
console.log(randomNumberGenerator(0, 1, { decimals: 3 }));
```

## 5. Number Validation and Type Checking

```javascript
// Example 1: Comprehensive number validation
function validateNumber(value) {
    return {
        isNumber: typeof value === 'number',
        isFinite: Number.isFinite(value),
        isInteger: Number.isInteger(value),
        isSafeInteger: Number.isSafeInteger(value),
        isNaN: Number.isNaN(value),
        isFloat: Number(value) === value && value % 1 !== 0,
        isPositive: value > 0,
        isNegative: value < 0,
        isZero: value === 0,
        type: typeof value
    };
}

// Example 2: Range validation
function validateRange(num, min, max) {
    if (!Number.isFinite(num)) return false;
    return num >= min && num <= max;
}

// Example 3: Custom number type checker
function getNumberType(num) {
    if (!Number.isFinite(num)) return 'not a finite number';
    if (Number.isInteger(num)) {
        if (num > 0) return 'positive integer';
        if (num < 0) return 'negative integer';
        return 'zero';
    }
    if (num > 0) return 'positive float';
    if (num < 0) return 'negative float';
    return 'zero';
}
```

## 6. Practical Number Utilities

```javascript
// Example 1: Number formatting utility
const NumberFormatter = {
    addCommas(num) {
        return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    },
    
    removeCommas(str) {
        return str.replace(/,/g, '');
    },
    
    toOrdinal(num) {
        const suffix = ['th', 'st', 'nd', 'rd'];
        const v = num % 100;
        return num + (suffix[(v - 20) % 10] || suffix[v] || suffix[0]);
    },
    
    toWords(num) {
        const ones = ['', 'one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'];
        const tens = ['', '', 'twenty', 'thirty', 'forty', 'fifty', 'sixty', 'seventy', 'eighty', 'ninety'];
        const teens = ['ten', 'eleven', 'twelve', 'thirteen', 'fourteen', 'fifteen', 'sixteen', 'seventeen', 'eighteen', 'nineteen'];
        
        if (num < 10) return ones[num];
        if (num < 20) return teens[num - 10];
        if (num < 100) return tens[Math.floor(num / 10)] + (num % 10 ? '-' + ones[num % 10] : '');
        return num.toString();
    },
    
    toFileSize(bytes) {
        const sizes = ['Bytes', 'KB', 'MB', 'GB', 'TB'];
        if (bytes === 0) return '0 Byte';
        const i = parseInt(Math.floor(Math.log(bytes) / Math.log(1024)));
        return Math.round(bytes / Math.pow(1024, i), 2) + ' ' + sizes[i];
    }
};

// Example 2: Mathematical utilities
const MathUtils = {
    gcd(a, b) {
        return b === 0 ? a : this.gcd(b, a % b);
    },
    
    lcm(a, b) {
        return (a * b) / this.gcd(a, b);
    },
    
    isPrime(num) {
        if (num <= 1) return false;
        if (num <= 3) return true;
        if (num % 2 === 0 || num % 3 === 0) return false;
        for (let i = 5; i * i <= num; i += 6) {
            if (num % i === 0 || num % (i + 2) === 0) return false;
        }
        return true;
    },
    
    factorial(num) {
        if (num < 0) return undefined;
        if (num <= 1) return 1;
        return num * this.factorial(num - 1);
    },
    
    fibonacci(n) {
        if (n <= 1) return n;
        let [a, b] = [0, 1];
        for (let i = 2; i <= n; i++) {
            [a, b] = [b, a + b];
        }
        return b;
    }
};

// Example usage
console.log(NumberFormatter.toOrdinal(123));     // "123rd"
console.log(NumberFormatter.toWords(45));        // "forty-five"
console.log(NumberFormatter.toFileSize(1234567)); // "1.18 MB"

console.log(MathUtils.gcd(48, 18));             // 6
console.log(MathUtils.lcm(48, 18));             // 144
console.log(MathUtils.isPrime(17));             // true
console.log(MathUtils.factorial(5));            // 120
console.log(MathUtils.fibonacci(8));            // 21
```

These examples demonstrate:
1. Number creation and parsing
2. Formatting and localization
3. Mathematical operations
4. Validation and type checking
5. Practical utilities for common number operations

Would you like me to explain any particular aspect in more detail?