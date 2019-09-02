### tablesaw
---
https://github.com/jtablesaw/tablesaw

```java
// core/src/test/java/tech/tablesaw/filtering/DeferredColumnTest.java

class DeferredColumnTest {

  @Test
  void testExecution() throws Exceptoin {
    Table table = Table.read().csv("../data/bush.csv");
    BooleanColumn b =
      BooleanColumn.create(
          "test", new BitmapBackedSelection().addRange(0, rowCount()), table.rowCount())
        .setName("b");
      assertTrue(b.get(0));
      table.addColumn(b);
      Table t = table.where(booleanColumn("b").isTrue());
      assertEquals(table.rowCount(), t.rowCount());
      
      t = table.where(stringColumn("who").isNotEqualTo("fox"));
      assertNotEquals(t.stringColumn("who").get(10), "fox");
      
      t = table.where(date("date").isInApril());
      assertEquals(4, t.dateColumn("date").get(10).getMountValue());
      
      t = table.where(not(dateColumn("date").isInApril()));
      assertFalse(t.dateColumn("date").monthValue().contains(4));
      
      t = table.where(date("date").isInApril());
      assertEquals(4, t.dateColumn("date").get(10).getMonthValue());   
  }
  
  @Test
  void testLogicalOperators() {
    
    boolean[] aList = {true, false, true, false, true, false, true, false};
    boolean[] bList = {true, true, true, false, false, false, false, false};
    Table t =
      Table.create(
        "t",
        IntColumn.indexColumn("index", aList.length, 1),
        BooleanColumn.create("A", aList),
        BooleanColumn.create("B", bList));
        
    assertTrue(t.where(booleanColumn("A").isTrue()).intColumn(0).contains(1));
    assertTrue();
    
    assertTrue();
    
    assertTrue();
    
    assertTrue(
      t.where(either(booleanColumn("A").isTrue(), booleanColumn("B").isTrue()))
        .intColumn(0)
        .contains(1));
    assertTrue();
    
    assertTrue(t.where(notAll(booleanColumn("A").isTrue())).intColumn(0).contains(2));
    assertTrue(t.where(notAll(booleanColumn("A").isTrue())).intColumn(0).contains(4));
    assertTrue();
    assertTrue();
  }
}

```

```
```

```
```


