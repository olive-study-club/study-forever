## Indexer 사용
- 클래스 내부에 있는 배열에 한번에 접근하고 싶을 때 인덱서를 사용
- 클래스 내부에 있는 배열을 객체 배열처럼 손쉽게 접근할 수 있게 하는 문법에 사용하는 키워드 this 활용
     - public 반환형 this[int idx]만들고 내부에 get, set으로 값 할당


     ``` C#
     public 반환형 this[int idx] //인덱스는 파라미터를 받을 수 있음. 프로퍼티는 불가
    {
        get { return 배열[idx]; }
        set { 배열[idx] = value; }
    }
    ```
    
    ```C#
    var instance = new class();
    instance[0] = value;
    var a instance[0];
    ```
    </br>

> 출처: https://blockdmask.tistory.com/598 [개발자 지망생:티스토리]</br>

</br>
</br>

## 추가 정의
- get 접근자는 데이터를 반환 / set 접근자는 데이터를 할당 
- 인텍싱 값은 형식이나 인스턴스 멤버를 명시적으로 지정하지 않고 설정하고 검색할 수 있음
- 인덱서는 내부 컬렉션 또는 배열을 캡슐화하는데 주로 사용되는 형식에서 자주 구현됨
- 인덱스 매개 변수 형식을 정수로 제한되지 않음. 문자열 사용 

## e.g.
``` C#

namespace IndexerTest
{
    class Mycache
    {
        private Dictionary<string, string> cache;
        //Dictionary : Key 를 가지고 Value 를 찾는 자료 구조 class
        //<string, string> Generic == <Key, Value>

        public MyCache() //생성자
        {
            cache = new Dictionary<string, string>();
            cache.Add("Debug","false");
            cache.Add("Logging", "true");

        }

        public void Add(string key, string value)
        {
            if(!cache.ContainKey(key))
            {
                cache[key] = value;
            }
            else
            {
                throw new ApplicationException("Key already exists");
            }
        }

        public string Get(string key)
        {
            if(cache.ContainKey(key))
            {
                return cache[key];
            }
            return null;
        }

        public void Set(string key, string value)
        {
            if(cache.ContainKey(key))
            {
                cache[key] = value;
            }
            else
            {
                throw new ApplicationException("key not found);
            }
        } 
    }
}
```

``` C#
namespace IndexerTest
{
    class Program
    {
        static void Main(string[] args)
        {
            Mycache mycache = new Mycache();
            mycache.Add("ItemId", "1100");
            string dbg = mycahce.Get("Debug"); //프로퍼티는 get,set 을 통해 특정 요소를 반환, 할당하는 것이 아니라 전체를 반환, 할당한다
            myCache.Set("Debug","false");
        }
    }
}

```