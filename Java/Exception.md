# Exception

- 예상치 못한 오류 상황
- 예외 처리를 통해 예외상황을 제어하고 적절히 대처할 수 있다
- 개발자가 대처할 수 있다
- cf) Error : 시스템 레벨에서 발생하기 때문에 개발자가 대처할 수 없다

### 예외 처리 : try-catch-finally
- try 블록 : 수행할 코드
- catch 블록 : try 블록에서 예외 발생시 수행할 코드
- finally : 예외 유무에 상관없이 무조건 수행할 코드    

- 예외 발생 x : try -> finally
- 예외 발생 : try -> catch -> finally

### 예외 처리 : throws
- 예외가 발생하면 해당 함수를 호출한 쪽(caller)으로 책임을 넘긴다
- caller는 예외를 처리하거나 자신을 호출한 쪽으로 또 넘겨야한다

### Checked / Unchecked
- Checked exception
	- 컴파일할 때 체크해서 해당 예외가 있으면 컴파일이 안된다
	- 예외처리를 해주어야 한다(try-catch 또는 throws)

```
//컴파일 안 됨
BufferedReader br = new BuferedReader(new InputStreamReader(System.in));
String str = br.readLine();
```

```
// try-catch
try{
	BufferedReader br = new BuferedReader(new InputStreamReader(System.in));
	String str = br.readLine();
}
catch(IOException e){
	e.printStackTrace();
}
```

```
// throws
String func() throws IOException{
	BufferedReader br = new BuferedReader(new InputStreamReader(System.in));
	String str = br.readLine();
	return str;
}
```




- Unchecked
	- 예외처리를 해주지 않아도 컴파일이 가능하다

```
// NullPointerException이 발생하는 코드지만 컴파일이 됨

List<Integer> list;
//Exception 발생
list.add(1);
```