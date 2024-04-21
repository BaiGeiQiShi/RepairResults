# The reason why ARJA-e cannot generate correct patches
Actually, ARJA-e can generate correct edits in **Chart18b2** and **Lang50b2**. However, at the same time, ARJA-e also generates edits in additional positions, resulting in unnecessary semantic modifications, so we do not identify them as correct patches.


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
For example, [**Patch_3666.txt**](plausible_patches/Chart18b2/Patch_3666.txt) contains the correct fix in its **fourth** edit. But the first three edits have changed its semantics.

<br>

## 2. Lang50b2
### Dev Patch:
```
Lang50b2/src/java/org/apache/commons/lang/time/FastDateFormat.java
...

       +        if (locale == null) {
       +            locale = Locale.getDefault();
285    -        if (locale != null) {
286    -            key = new Pair(key, locale);
287             }
288 
       +        key = new Pair(key, locale);
...
```
### Explanation:
For example, [**Patch_9317.txt**](plausible_patches/Lang50b2/Patch_9317.txt) contains the correct fix in its **first** and **second** edits. But the remaining edits have changed its semantics.
