# Reasons for confirming as the correct patches
## 1. Closure6b1
### Dev Patch:
```
Closure6b1/src/com/google/javascript/jscomp/TypeValidator.java

...
405    -      if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
406    -        registerMismatch(rightType, leftType, null);
407    -      } else {
408           mismatch(t, n, msg, rightType, leftType);
409    -      }
...
```
### Explanation:
We just need to ensure that `mismatch(t, n, msg, rightType, leftType);` will always be executed. So the patches in Closure6b1 are considered semantically equivalent to the dev patch.
<br>
<br>

## 2. Time3b1
### Dev Patch:
```
Time3b1/src/main/java/org/joda/time/MutableDateTime.java

635    public void add(DurationFieldType type, int amount) {
           ...
       +        if (amount != 0) {
639             setMillis(type.getField(getChronology()).add(getMillis(), amount));
       +        }
           ...
```
### Explanation:
We check all statements that call the method where the buggy code is located, from which we can know that `amount is always => 0`.  And the comment ```* @param amount  the amount to add of this duration``` (Time3b1/src/main/java/org/joda/time/MutableDateTime.java: 631) shows that the variable `amount` is an increment in design. So we think that `amount != 0` and `amount > 0` are semantically equivalent. 
<br>
<br>
**Here are the statements that call the buggy method:**
| File Path | line | call |
| ------- | ------- | ------- |
|org.joda.time.TestMutableDateTime_Adds.java | 171 | test.add(DurationFieldType.years(), 8)|
|org.joda.time.TestMutableDateTime_Adds.java | 178 | test.add(DurationFieldType.years(), 0)|
|org.joda.time.TestMutableDateTime_Adds.java | 186 | test.add(DurationFieldType.years(), 0)|
|org.joda.time.TestMutableDateTime_Adds.java | 193 | test.add(DurationFieldType.years(), 0)|
|org.joda.time.TestMutableDateTime_Adds.java | 199 | test.add((DurationFieldType)null, 0)|
|org.joda.time.TestMutableDateTime_Adds.java | 208 | test.add((DurationFieldType)null, 6)|
