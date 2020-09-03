# Singleton Pattern
- 객체의 개수를 제한하는 패턴이다.
	- 객체를 무제한으로 생성하면 자원을 불필요하게 많이 사용하게 된다.
- 예시) LogWriter, DB Connection Pool

## Example
```
1  class SingletonEx{
2 	 private static SingletonEx singletonEx;
3	 private SingletonEx(){
4		 super();
5	 }
6
7	 public static SingleTonEx getInstance(){
8		 if(singletonEx == null){
9			 singletonEx = new SingletonEx();
10		 }
11		 return singletonEx;
12	 }
13 }
```
2 : private static으로 객체를 선언해서 외부에서 접근하지 못하도록 하고 하나의 객체를 공유하도록 한다.    
3 : private으로 생성자를 선언해서 외부에서 객체를 생성하지 못하도록 한다.    
7 : 객체가 생성되어 있지 않으면 새로 생성하고, 생성되어 있으면 객체를 반환한다.

## Thread Problem
```
private SingletonEx(){
	Thread.sleep(100); // db 연결과 같은 상황 가정
	super();
}

...

public static void main(String[] args){
	Runnable r = () -> {
		try{
			SingletonEx st = SingletonEx.getInstance();
		}catch(Exception e){}
	};
	for(int i = 0; i < 10; i++){
		Thread t = new Thread(r);
		t.start();
	}
}
```
- getInstance()에서 null체크 후 객체를 생성하는 속도보다 < for문의 속도    
	=> for문을 도는 만큼 객체를 생성하게 된다. (객체==null로 처리됨)

### Then
#### 1. Synchronized
```
public synchronized static SingleTonEx getInstance(){
	if(singletonEx == null){
		singletonEx = new SingletonEx();
	}
	return singletonEx;
}
```

#### 2. 미리 생성
```
class SingletonEx{
	//객체를 미리 생성한다.
	private static SingletonEx singletonEx = new SingletonEx();
	private SingletonEx(){
		super();
	}

	public static SingleTonEx getInstance(){
		//null체크 삭제
		//if(singletonEx == null){
		//	singletonEx = new SingletonEx();
		//}
		return singletonEx;
	}
}
```