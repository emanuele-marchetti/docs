# You moved a number into the destination, but the destination does not hold a number

**Applies to:** COBOL packed-decimal fields (COMP-3) | **Level:** Intermediate | **Time to resolve:** 2 minutes

You moved a number from one field to another. It should remain the same, but after the move, you see something different. There are no other operations to check. Just the MOVE.

The data is still the same. It looks different now, because of the format.

## Why this happens

COMP-3 stores a number in packed form: two digits share each byte, and the last half-byte holds the sign. The number 12345 occupies three bytes rather than five.

This works as long as the field is treated as what it is, a number. If you move it into an alphanumeric field, COBOL does not convert it. The bytes are copied as they are, and read as characters they mean nothing.

## Why odd and even behave differently

A byte holds two digits, and the sign always takes half a byte at the end.

Declare five digits and the field fits exactly: five digits plus the sign make three full bytes. Declare six, and there is half a byte left over at the front. COBOL ignores it in calculations, but copies it along with everything else.

## Fix it

### If you need to read the value

Move the field into a numeric DISPLAY field, not an alphanumeric one. COBOL unpacks the digits and writes one per byte, and the value appears as a number.

### If you need to move the bytes

Copying a COMP-3 field into an alphanumeric field preserves the bytes, not the value. The field cannot be read, compared, or used in arithmetic. This is acceptable when the bytes are being written to a file or passed to another program that knows how to interpret them. It is not a way to inspect the data.

### Declare an odd number of digits

A COMP-3 field declared with an odd number of digits fills its bytes exactly. Declared with an even number, it carries half a byte that nothing initialises and nothing clears. Choosing an odd number removes the problem entirely.

*Written by Emanuele Marchetti*
