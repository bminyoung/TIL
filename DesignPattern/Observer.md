# Observer Pattern
- 어떤 객체의 상태가 변화하면 이에 의존하는 다른 객체에게 상태변화에 대해 알린다.
- 예시) Android에서 위젯의 OnClickListener(객체: Publisher, 리스너: Observer)

## Example
```
interface Observer{
    void update();
}

class Subscriber implements Observer{
    private int num;
    public Subscriber(int num) {
        this.num = num;
    }

    @Override
    public void update() {
        System.out.println(num + ": read");
    }
}

abstract class Publisher{
    private List<Observer> observers = new ArrayList<>();
    public void add(Observer observer){
        observers.add(observer);
    }
    public void delete(Observer observer){
        observers.remove(observer);
    }
    public void notifyObservers(){
        for(Observer o : observers){
            o.update();
        }
    }
}

class Newspaper extends Publisher{
    public void today(){
        System.out.println("today's news");
        notifyObservers();
    }
}
...
public static void main(String[] args) {
    Newspaper news = new Newspaper();
    Subscriber sub1 = new Subscriber(1);
    Subscriber sub2 = new Subscriber(2);
    news.add(sub1);
    news.add(sub2);

    news.today();
    
    //////////////////
    // today's news //
    // 1: read      //
    // 2: read      //
    //////////////////
}
```
- news.today() -> observer에게 notify -> observer.update()
