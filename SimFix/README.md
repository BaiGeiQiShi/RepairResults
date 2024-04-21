Note: You can look for comments that contain "start/end of generated patch" and "start/end of original code" in the Java files to see what's changed by the patch.

# Reasons for confirming as the correct patches

## 1. Chart18b2
### Dev Patch:
```
Chart18b2/source/org/jfree/data/DefaultKeyedValues.java
...
315	public void removeValue(int index) {
316	  this.keys.remove(index);
317	  this.values.remove(index);
318    -        if (index < this.keys.size()) {
319             rebuildIndex();
320    -        }
321	}
...
```
### Explanation:
The reason for this bug is, when `index = this.keys.size()`, the  value of `this.keys.size()` will decrease by one, resulting in the value of `index` to be the same as the value of `size`, causing the program does not execute `rebuildIndex();`. And when `index` bigger than `this.keys.size()` or smaller than 0, it will throw exception in line 316. So we just need to address this bug by replacing `if (index < this.keys.size()) {`  with `if (index <= this.keys.size()) {`. So the patch in Chart18b2 is considered semantically equivalent to the dev patch.

<br>

## 2. Closure6b1
### Dev Patch:
```
Closure6b1/src/com/google/javascript/jscomp/TypeValidator.java

...
404	if (!rightType.canAssignTo(leftType)) {
405    -      if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
406    -        registerMismatch(rightType, leftType, null);
407    -      } else {
408           mismatch(t, n, msg, rightType, leftType);
409    -      }
410	return false
411	}
...
```
### Explanation:
We just need to ensure that `mismatch(t, n, msg, rightType, leftType);` will always be executed. So the patches in Closure6b1 add `leftType==null` or `leftType.toObjectType()==null` to line 405. If `leftType` is null, line 404 will throw exception. If `leftType` is not null, the condition of line 405 is always false, so that it will execute `mismatch(t, n, msg, rightType, leftType)`. So we believe that it is semantically equivalent to the dev patch.
