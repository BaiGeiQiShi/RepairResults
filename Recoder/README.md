# Reasons for confirming as the correct patches

**Note:** If you cannot understand the format of patches, please look [here](../rules.md).

## 1. Chart18b2
### Dev Patch:
```
Chart18b2/source/org/jfree/data/DefaultKeyedValues.java

...
318    -        if (index < this.keys.size()) {
319             rebuildIndex();
320    -        }
...
```
### Explanation:
We just need to ensure that `rebuildIndex();` will always be executed. And the patch in Chart18b2 inserts `rebuildIndex();` before this **if block**, which means that `rebuildIndex();` will be executed at least once.
<br>
<br>
Here is the  `rebuildIndex();` (shown below), from which we can see that the results of executing twice and executing once are the same. So we believe that it is semantically equivalent to the dev patch.
```
Chart18b2/source/org/jfree/data/DefaultKeyedValues.java

...
298    private void rebuildIndex () {
299        this.indexMap.clear();
300        for (int i = 0; i < this.keys.size(); i++) {
301            final Object key = this.keys.get(i);
302            this.indexMap.put(key, new Integer(i));
303        }
304    }
...
```
<br>

## 2. Closure6b1
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
We just need to ensure that `mismatch(t, n, msg, rightType, leftType);` will always be executed. So the patch in Closure6b1 is considered semantically equivalent to the dev patch.
<br>
<br>

## 3. Closure106b2
### Dev Patch:
```
Closure106b2/src/com/google/javascript/rhino/JSDocInfoBuilder.java

...
189    -    if (parseDocumentation) {
190         populated = true;
191    -    }
...
```
### Explanation:
We just need to ensure that `populated = true;` will always be executed. So the patches in Closure106b2 are considered semantically equivalent to the dev patch.
