# Useful Vanilla JS Snippets

This is a compilation of vanilla js snippets for web developers. 

  * [Convert IPv4 to Decimal](#convert-ipv4-to-decimal)
  * [Convert Decimal to IPv4](#convert-decimal-to-ipv4)

## Convert IPv4 to Decimal

```js
/**
 * Convert IPv4 to Decimal
 * @param {String} ip - a String represents an IPv4
 * @returns a decimal if the input is valid. Otherwise, it returns -1.
 */
function convertIPv4toDecimal(ip) {
  // Simply validate input as IPv4
  const ipv4RegEx = /^(\d{1,3}\.){3}(\d{1,3})$/;
  const valid = ipv4RegEx.test(ip);
  if (!valid) {
    return -1;
  }

  let ipDecimal = 0;
  const octets = ip.split('.');

  for (let i = 0; i < 4; i++) {
    const octet = Number(octets[i]);

    // make sure each value is between 0 and 255
    if (octet > 255 || octet < 0) {
      return -1;
    }

    ipDecimal = ipDecimal * 256 + octet;
  }

  return ipDecimal;
}
```

[Visit Demo](https://jscenter.github.io/vanilla-js-snippets/demo/ipv4-decimal-conversion/)

## Convert Decimal to IPv4

```js
/**
 * Convert Decimal to IPv4
 * @param {Number} decimal - a Number represents a Decimal
 * @returns an IPv4 as String if the input is valid. 
 * Otherwise, it returns an empty string ("").
 */
function convertDecimalToIPv4(decimal) {
  if (typeof decimal !== "number" || 
      Number.isInteger(decimal) === false ||
      decimal < 0 || 
      decimal > 4294967295
  ) {
    return "";
  }

  const p1 = decimal >>> 24;
  const p2 = (decimal & 0x00ff0000) >>> 16;
  const p3 = (decimal & 0x0000ff00) >>> 8;
  const p4 = (decimal & 0x000000ff);

  if (p1 > 255 || p2 > 255 || p3 > 255 || p4 > 255) {
     return "";
  }

  return `${p1}.${p2}.${p3}.${p4}`;
}
```

[Visit Demo](https://jscenter.github.io/vanilla-js-snippets/demo/ipv4-decimal-conversion/)