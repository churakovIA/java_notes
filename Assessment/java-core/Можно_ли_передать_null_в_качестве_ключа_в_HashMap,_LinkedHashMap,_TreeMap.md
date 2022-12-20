# Можно ли передать null в качестве ключа в HashMap, LinkedHashMap, TreeMap?
---

- HashMap, LinkedHashMap - допускают null в качестве ключа
- TreeMap - зависит от компаратора переданного в конструктор. При натуральном упорядочивании - NPE при попытке вставки null-ключа

```java
     * @throws NullPointerException if the specified key is null
     *         and this map uses natural ordering, or its comparator
     *         does not permit null keys
     */
    public V put(K key, V value) {

```

Этот код выполнится без ошибок:

```java
    TreeMap<Integer, String> treeMap = new TreeMap<>((a,b)->0);
    treeMap.put(1, "TreeMap1");
    treeMap.put(null, "TreeMap2");
    System.out.println(treeMap.get(1));
    System.out.println(treeMap.get(null));
    
    /* output:
        TreeMap2
        TreeMap2
     */
```

