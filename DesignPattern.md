
# Design Pattern

## Singleton Design Pattern

### What is Singleton Pattern
생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이도록 제한하여, 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴하도록 하는 디자인 패턴이다.
여러개의 objects들이 하나의 DB를 공유하고 싶은 상황(DB Connection Pool)에 자주 사용된다.

### Singleton Pattern을 쓰는 이유
- 고정된 메모리 영역을 얻으면서 메모리 낭비를 방지
- singleton으로 만들어진 클레스의 인스턴스는 전역 인스턴스이기 때문에 다른 클레스의 인스턴스들이 데이터를 공유하기 쉽다.
- 두번째 이용시부터는 객체 로딩 시간이 현저하게 줄어 성능이 좋아진다.
- 인스턴스가 절대적으로 한개만 존재함을 보증하고 싶은 경우에 사용!

### Implementation
#### Classic Implementation
``` Java
class Singleton
{
    private static Singleton obj;
    private Singleton() {}
    public static Singleton getInstance()
    {
        if (obj == null)
            obj = new Singleton();
        return obj;
    }

}
```
getInstance()를 static으로 정의한 이유는 Singleton을 인스턴스화 하지 않은 상태에서 call할 수 있도록 하기 위해서 입니다. 처음에 getInstance()를 call하면 새로운 singleton object가 생성되고 그 이후부터는 생성했던 그 object를 return 하는 방식으로 구현되어 있습니다.  Singleton object는 우리가 getInstance()를 call하기 전까지 생성되지 않습니다. 그것은 lazy instantiation이라고 합니다.
하지만 이 방식은 mult-thread 환경에서 여러개의 object가 생성될 수 있다는 문제가 있습니다.

#### make getInstance() synchronized
``` Java
class Singleton
{
    private static Singleton obj;
    private Singleton() {}
    public static synchronized Singleton getInstance()
    {
        if (obj == null)
            obj = new Singleton();
        return obj;
    }

}
```
이 코드는 getInstance에 synchronized를 사용하여 한번에 하나의 thread에서만 실행될 수 있도록 보장한 코드입니다. 하지만 이 코드의 문제는 singleton object를 생성할 때 마다 synchronized를 사용하기 때문에 program 성능이 낮아집니다. (하지만 getInstance()가 본인의 프로그램내에서 중요하고 자주 사용되는 것이 아니라면, 위의 코드는 깔끔하고 간단한 해결법이 될 것입니다.)


### Eager Instantiation
``` Java
class Singleton
{
    private static Singleton obj = new Singleton();
    private Singleton() {}
    public static Singleton getInstance()
    {
        return obj;
    }

}
```
static initializer를 이용하여 singleton 인스턴트를 만드는 방식이다. JVM은 class가 load될때 static initializer를 실행하기 때문에 mult-thread 상황에서도 안전하다. 하지만 이 방식은 singleton 클레스가 가볍고 처음부터 끝까지 사용되는 경우에 사용하는 것을 권장한다.

### use "Double Checked Locking"
``` Java
class Singleton
{
    private volatile static Singleton obj ;
    private Singleton() {}
    public static Singleton getInstance(){
        if (obj == null){
            synchronized (Singleton.class){
                if(obj == null){
                    obj = new Singleton();
                }
            }
        }
        return obj;
    }
}
```
사실 singleton object를 생성하고 나면 동기화는 필요하지 않습니다. 더이상 obj는 null이 아니기 때문에 어느 순간에 getInstance를 해도 일관성있는 return을 받을 수 있기 때문입니다. 그래서 우리는 object가 null인 경우에만 lock을 걸어도 충분합니다. 또한 obj변수에 volatile 키워드를 걸어서 mult-thread 들이 정확한 obj 변수 값을 가져올 수 있도록 했습니다. 이 방식은 synchronized 방식에서 생기는 오버해드를 현저히 줄일 수 있는 방법입니다.
