## Kotlin의 컬렉션

![image-20230216174627135](C:\Users\jm342\AppData\Roaming\Typora\typora-user-images\image-20230216174627135.png)

- mutable~ 이면 변경가능 아니라면 변경 불가능.

```kotlin
    // Immutable
    val currencyList = listOf("달러", "유로", "원")

    // mutable
    val mutableCurrencyList = mutableListOf<String>().apply {
        add("달러")
        add("유로")
        add("원")
    }
```

- LinkedLIst나 arrayList같은 구현체도 사용가능

  ```kotlin
      // linkedList
      val linkedList = LinkedList<Int>().apply {
          addFirst(1)
          addLast(2)
      }
  
      // arrayList
      val arrayList = ArrayList<Int>().apply {
          add(1)
          add(2)
          add(3)
      }
  
  ```

  

- Iterator도 사용 가능하다. (상속 받음)

  ```kotlin
      val iterator = currencyList.iterator()
      while (iterator.hasNext()) {
          println(iterator.next())
      }
  
      println("---------------")
      for (currency in currencyList) {
          println(currency)
      }
  ```

  

- forEach 같은 stream 함수도 사용가능

  ```kotlin
      // foreach 라는 표준함수도 사용가능
      currencyList.forEach {
          println(it)
      }
      // for loop -> map
      val lowerList = listOf("a", "b", "c")
  //    val upperList = mutableListOf<String>()
  
      // for 문보다 훨씬 간단.
      val newUpperList = lowerList.map { it.uppercase() };
      println(newUpperList)
  
      val filteredList = newUpperList.filter { it == "B" }
      println(filteredList)
  ```

- java8의 stream과 다른것은 터미널 오퍼레이터가 호출이 되지 않아도 동작을 한다.

- asSequence를 호출하면 stream과 동일하게 동작한다.
  ilter 체인이 많아지면 collection 을 매일 항상 새로 만들기때문에 out of memory가 날수가 있다.

- 따라서 대량의 데이터를 핸들링 할때는 asSequence를 고려해봐도 좋다.

- 벤치마크상 데이터가 적으면 asSequence가 퍼포먼스 측면에서 낫다고도 한다

  ```kotlin
      val filteredList2 = newUpperList
          .asSequence()
          .filter { it == "B" }
          .toList()
  ```

  
