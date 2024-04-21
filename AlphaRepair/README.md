# Reasons for confirming as the correct patches
## 1. Closure-138-1

### Dev Patch

```
Closure-138-1/src/com/google/javascript/jscomp/ClosureReverseAbstractInterpreter.java

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

### Explanation:
We just need to ensure the `if condition` in line 208 will always be true. The patches of Closure-138-1 in ./correct_patches all ensure that. Because if `callee` or `param` is null, an exception will be thrown when executing line 206. So we believe that these patches are semantically equivalent to the dev patch.
<br>
## 2. Time-3-1
### Dev Patch:
```
Time-3-1/src/main/java/org/joda/time/MutableDateTime.java
		...
635    public void add(DurationFieldType type, int amount) {
636	        if (type == null) {
637		    throw new IllegalArgumentException("Field must not be null");
638		}
       +        if (amount != 0) {
639             setMillis(type.getField(getChronology()).add(getMillis(), amount));
       +        }
640    }
           ...
```
### Explanation:
The patches of Time-3-1 in ./correct_patches are all semantically equivalent to the dev patch.
<br>
## 3. Time-3-2
### Dev Patch:
```
Time-3-2/src/main/java/org/joda/time/MutableDateTime.java
		...
659    public void addYears(final int years) {
       +        if (years != 0) {
660             setMillis(getChronology().years().add(getMillis(), years));
       +        }
661    }
           ...
```
### Explanation:
The patch of Time-3-2 in ./correct_patches is semantically equivalent to the dev patch.
<br>
## 4. Time-3-4
### Dev Patch:
```
Time-3-4/src/main/java/org/joda/time/MutableDateTime.java
		...
722    public void addWeeks(final int weeks) {
       +        if (weeks != 0) {
723             setMillis(getChronology().weeks().add(getMillis(), weeks));
       +        }
724	}
           ...
```
### Explanation:
The patch of Time-3-4 in ./correct_patches is semantically equivalent to the dev patch.
<br>
## 5. Closure-6-1
### Dev Patch:
```
Closure-6-1/src/com/google/javascript/jscomp/TypeValidator.java

...
405    -      if ((leftType.isConstructor() || leftType.isEnumType()) && (rightType.isConstructor() || rightType.isEnumType())) {
406    -        registerMismatch(rightType, leftType, null);
407    -      } else {
408           mismatch(t, n, msg, rightType, leftType);
409    -      }
...
```
### Explanation:
We just need to ensure that `mismatch(t, n, msg, rightType, leftType);` will always be executed. So the patch of Closure-6-1 in ./correct_patches is considered semantically equivalent to the dev patch.
<br>
## 6. Lang-53-3
### Dev Patch:
```
Lang-53-3/src/java/org/apache/commons/lang/time/DateUtils.java

...
640		int millisecs = val.get(Calendar.MILLISECOND);
641		if (!round || millisecs < 500) {
642	             time = time - millisecs;
	  +	}
643		if (field == Calendar.SECOND) {
644	             done = true;
645	  -	}
646	}
...
```
### Explanation:
We just need to ensure that `if (field == Calendar.SECOND) { done = true; }` will always be executed. So the patch of Lang-53-3 in ./correct_patches is considered semantically equivalent to the dev patch.
<br>
## 7. Chart-18-2
### Dev Patch:
```
Chart-18-2/source/org/jfree/data/DefaultKeyedValues.java
...
315	public void removeValue(int index) {
316		this.keys.remove(index);
317		this.values.remove(index);
318   -   	if (index < this.keys.size()) {
319           		rebuildIndex();
320   -   	}
321	}
...
```
### Explanation:
①We just need to ensure that `rebuildIndex();` will always be executed. And the patches of Patch Number 3400, 3845 insert `rebuildIndex();` before this **if block**, which means that `rebuildIndex();` will be executed at least once.
<br>
Here is the  `rebuildIndex();` (shown below), from which we can see that the results of executing twice and executing once are the same. So we believe that it is semantically equivalent to the dev patch.

```
Chart-18-2/source/org/jfree/data/DefaultKeyedValues.java

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

②The rest patches are all guaranteed that the **if condition** in line 318 is always true or add a ` rebuildIndex();` after the **if block**, which ensure that `rebuildIndex();` will always be executed. So we believe that it is semantically equivalent to the dev patch.
