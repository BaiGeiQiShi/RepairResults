# Reasons for confirming as the correct patches
## 1. Closure_6_2
### Dev Patch:
```
Closure_6_2/src/com/google/javascript/jscomp/TypeValidator.java

...
365         if (!leftType.isNoType() && !rightType.canAssignTo(leftType)) {
366    -      if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
367    -        registerMismatch(rightType, leftType, null);
368    -      } else {
369           // Do not type-check interface methods, because we expect that
370           // they will have dummy implementations that do not match the type
371           // annotations.
...
382               "assignment to property " + propName + " of " +
383               getReadableJSTypeName(owner, true),
384               rightType, leftType);
385    -      }
...
```
### Explanation:
We just need to ensure that `registerMismatch(rightType, leftType, null);` will never be executed. The patches of Closure_6_2 in ./correct_patches all ensure that the if condition in line 366 is always false. For example, the if condition (line 366) in Closure_6_2/Patch_624_130.txt contains `&& !(!leftType.isNoType() && !rightType.canAssignTo(leftType))`, which is opposite to the if condition in line 365 and uses `&&` to connect to its previous condition. Therefore, As long as the line 365 is true, the line 366 must be false. So we believe that they are semantically equivalent to the dev patch.
<br>

## 2. Chart_18_2
### Dev Patch:
```
Chart_18_2/source/org/jfree/data/DefaultKeyedValues.java

...
316	        this.keys.remove(index);
317             this.values.remove(index);
318    -        if (index < this.keys.size()) {
319             rebuildIndex();
320    -        }
...
```
### Explanation:
①We just need to ensure that `rebuildIndex();` will always be executed. And the patches of Chart_18_2/Patch_91_66.txt, Chart_18_2/Patch_112_85.txt and Chart_18_2/Patch_147_117.txt insert `rebuildIndex();` before or after this **if block**, which means that `rebuildIndex();` will be executed at least once.
<br>
Here is the  `rebuildIndex();` (shown below), from which we can see that the results of executing twice and executing once are the same. So we believe that it is semantically equivalent to the dev patch.

```
Chart_18_2/source/org/jfree/data/DefaultKeyedValues.java

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
②By the way, the patch in Chart_18_2/Patch_125_98.txt just replaces `if (index < this.keys.size()) {` with `if ((index < this.keys.size()) || !(index < 0)) {`, which is also considered semantically equivalent. Because when `index<0`, an exception will be thrown when executing line 316. So we believe that it is semantically equivalent to the dev patch.

<br>

## 3. Closure_106_2

### Dev Patch:

```
Closure_106_2/src/com/google/javascript/rhino/JSDocInfoBuilder.java

...
188		public boolean recordBlockDescription(String description) {
189		-    if (parseDocumentation) {
190					populated = true;
191		-    }
192			return currentInfo.documentBlock(description);
193		}
...
```

The patch in Closure_106_2/Patch_594_235.txt is the same as develop patch. 

<br>

## 4. Closure_138_1

### Dev Patch

```
Closure_138_1/src/com/google/javascript/jscomp/ClosureReverseAbstractInterpreter.java

...
206	if (callee.getType() == GETPROP && param.isQualifiedName()) {
207		JSType paramType =  getTypeIfRefinable(param, blindScope);
208	-		if (paramType != null) {
209				Node left = callee.getFirstChild();
210				Node right = callee.getLastChild();
...
...			
215				if (restricter != null) {
216					return restrictParameter(param, paramType, blindScope, restricter,
217						outcome);
218	-           }
219	       }
220	    }
221	}

```

The patch in Closure_138_1/Patch_89_24.txt is the same as develop patch. 
