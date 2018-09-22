# Style Guide

 - Heuristic: If we could change it to 'zebra' on a whim, then use a string; otherwise use a symbol.
    - E.g. Use strings as keys to the params hash, since changing flexible route segments, query string parameters, or `name=""` values is easy. Use symbols when referring to actual column names.
 - Use `Hash#fetch` instead of `Hash#[]` (for better error messages when wrong key is supplied).
 - To be consistent with the above, use `Array#at` instead of `Array#[]` (even though they are identical).
