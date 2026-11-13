# Code-golf: evalExpr — entry by zkhiel

**Entry file:** `evalExpr.js` — **65 bytes**:

```js
module.exports={evalExpr:s=>eval(s.replace(/\d+\.?\d*/g,m=>+m))}
```

How it works: every numeric literal is first normalised through `+m`, which
strips leading zeros (`010` → `10`, killing the legacy-octal trap) and
canonicalises decimals (`0.50` → `0.5`); the host evaluator then applies
correct precedence, parentheses, decimals and unary minus natively. Passes
all 9 published cases plus spot checks (`010+1`=11, `.5*2`=1, `2*-3`=-6).

**Fallback:** `evalExpr-readable.js` (392 bytes) is a dependency-free
recursive-descent parser (tokeniser-free, explicit precedence levels,
unary minus) that passes the same cases — kept here in case the grading
sandbox ever disallows dynamic evaluation.
