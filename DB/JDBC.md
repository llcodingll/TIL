## JDBC


: 표준 규격(인터페이스)
- 인터페이스는 구현체 필요


: java 프로그램에서 DB에 일관된 방식으로 접근할 수 있도록 API를 제공하는 클래스 집합
- 데이터베이스에서 자료를 쿼리(SELECT)하거나 업데이트(테이블 등록, 수정, 삭제)하는 방법 제공
- java에서는 JDBC를 이용해 SQL을 DBMS와 주고 받음
- DBMS의 종류에 관계 없이 사용 가능 (약간의 설정만 조금 수정하면 가능)
---
### JDBC 이용해 DB 연결하는 방법(4단계)
1. JDBC 드라이버 로드
   - 클래스 로더가 메소드 영역에 클래스를 내가 처음으로 이걸 사용하려고 했을 때, 올려줌
   - Class라는 클래스를 이용해서 JDBC를 호출해서 올려둠
2. DB 연결
   통로를 뚫겠다
3. SQL문 실행
   - 필요한 SQL문 사용하겠다(DML)
   - 보낼 때, 받을 때(result set(SELECT문)) 쓰는 게 있음
   - insert, update, delete는 int값을 하나 반환해주는데 이 int값의 의미는 건드려진 행의 수를 반환해줌
     - 얘네는 java를 통해 요청을 날릴 때, 여러 개 넣거나 지우거나 할 일이 거의 없겠죠
     - 이렇게 넘겨받은 int값이 1과 같거나 0 초과이거나 1 이상이거나 해야 DB에 잘 등록됨/안됨 보이겠지
4. DB 연결 끊기
   - 끊어야 하는 이유: 자바는 실행할 코드 없으면 알아서 통로가 닫히는데, 서비스를 한다고 하면 컴퓨터가 꺼지지 않으니까 자동으로 없어지지 않으니 스스로 없애줘야 함
     - 비용/자원 소모가 더 이상 발생하지 않도록
   - 나중에는 커넥션풀 관련해서도 고민해봐야 함
     - 통로 하나 만드는 거도 자원 소모하니까 미리 만들어둔 통로를 할당하는 방식도 있다
---
### JDBC 드라이버 로드


: DB와 연결하기 위해 시작할 JDBC 드라이버를 프로그램 시작할 때 로딩
- 필요한 DBMS의 jar 파일을 프로젝트에 추가
- Class 클래스의 정적 메소드 `.forName()`을 이용해 JVM 안으로 클래스를 메모리에 적재
- DriverManager를 통해 접근 가능
---
### /lib : `.jar` 넣어줘야 함
```java
public class JdbcTest {
	
	public JdbcTest() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("성공");
		} catch (ClassNotFoundException e) {
			System.out.println("실패");
//			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		JdbcTest db = new JdbcTest(); //성공
	}
}
```
---
### DB 연결
- DriverManager 클래스의 static 메소드인 `.getConnection(URL, UserId, UserPassword)`를 통해 연결 요청
- `Connection conn = DriverManager.getConnection("URL", "~~”, "~~");`
- Connection은 인터페이스이므로 new 연산자를 통해 인스턴스를 생성하지 않고 만들어진 인스턴스를 얻어와 저장(default는 AutoCommit)

* DB별 URL있음
---
### SQL 실행(Statement)


: SQL문 수행하기 위해 Statement 객체 필요

- Connection 객체 이용해 `createStatement()` 메소드 실행해 생성
- `executeQuery(String sql)`: SELECT문과 같이 결과값이 여러 개의 record로 구해지는 경우 사용
- `executeUpdate(String sql`: INSERT, UPDATE, DELETE문과 같이 테이블이 변경만 되고 결과가 없는 경우 사용 반환 값은 int형
---
### SQL 실행(ResultSet)


: Query에 대한 결과 값 처리
- 반환 값이 여러 개인 경우 이를 받아서 쉽게 처리할 수 있게 설계됨
- `.next()`를 통해 현재 행에서 다음 행으로 이동
- `getXXX(Column Name/index)`를 통해 값을 가져올 수 있음
---
### 데이터베이스 연결 끊기


: 모든 작업이 끝나면 ResultSet, Statement (or PreparedStatement), Connection의 `close()`를 통해 연결 종료
* **역순**으로 종료

```java
public class JdbcTest {
	
	public JdbcTest() {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			System.out.println("성공");
		} catch (ClassNotFoundException e) {
			System.out.println("실패");
//			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		JdbcTest db = new JdbcTest();
	}
	
	//전체 게시글 조회
	private List<Board> selectAll(){
		List<Board> list = new ArrayList<>();
		//DB와의 연결 통로 뚤어줘야 함
		try {
			Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/board?serverTimezone=UTC", "~~", "~~");
			Statement stmt = conn.createStatement();
			String sql = "SELECT * FROM board"; //게시글 전체 조회 SQL문
			ResultSet rs = stmt.executeQuery(sql);
			
			//데이터 몇 개 있는지 모름
			while(rs.next()) {
				Board board = new Board(); // 보드 바구니 준비
				board.setId(rs.getInt("id"));
				board.setWriter(rs.getString("writer"));
				board.setTitle(rs.getString("title"));
				board.setContent(rs.getString("content"));
				
				list.add(board);
			} //내용 채우기
			//list에 모든 게시글이 들억마
			
			rs.close();
			stmt.close();
			conn.close();
			
		} catch (SQLException e) {
			e.printStackTrace();
		}
		return list;
	}
}
```
---
### PreparedStatement


: Statement의 단점을 극복한 인터페이스

- 간단하게 쿼리문 작성할 수 있도록 도움
- Connection 인터페이스의 `.prepareStatement(String sql)`메서드를 통해 가져옴
- `.executeQuery()`, `.executeUpdate()` 사용
- SQL문은 `?`기호를 사용해서 표현 가능
  `INSERT INTO (table명) VALUES(?, ?, ?, ?);`
- `?`기호에 값을 setter(int 순서/ 실제 데이터나 변수)를 통해 할당

---
#### Connection


: 데이터베이스와의 연결을 나타내는 객체
- 데이터베이스 서버와 물리적인 설정이나 관리들을 진행할 수 있게 해줌
- 메타데이터에 접근 가능(MySQL 서버에 설정되어 있는 정보 가져올 때)
- 자동 커밋 설정 - 트랜잭션 관리(commit, rollback)
- Statement, PreparedStatement 객체 생성을 도와줌
---
`.createStatement()`: SQL문을 보낼 수 있는 쪽지가 될 종이 한 장 생김

---
`.close()`

JDBC 객체들은 메모리 공간 안에서 GC에 의해 자동 삭제되는 곳이 아님

그래서 이 친구들은 안쪽에서 시스템에 의해 네트워크로 연결되어 있는(MySQL과 연결) 거라서 자동으로 메모리가 해제되지 X

그래서 명시적으로 해당 JDBC 객체 리소스를 해제하라고 명령문을 날려야 함

* 순서가 정해져있음
  - connection먼저 생성해서 conn의 종이 한 장 만드는 거를 stmt에 넣어줬으니까 역순으로 닫아주어야 함
    - 우편함에 종이 쪽지 넣었으면 종이 쪽지 먼저 빼고 우편함 닫아야지

* 요즘은 아래와 같이 사용
```java
try (Connection conn = DriverManager.getConnection(url, id, pw);
	Statement stmt = conn.createStatement()){
} catch (Exception e) {
}	
```
---
### Statement vs PreparedStatement

**java.sql.Statement**


: SQL문을 보낸다. 단순하게 정적인 SQL문(문자열)을 실행하는 객체
- `executeQuery(String sql)` : 주어진 SQL 명령이 SELECT 문인 경우, SQL 문을 실행하고 ResultSet 객체를 반환합니다.
- `executeUpdate(String sql)` : 주어진 SQL 명령이 INSERT, UPDATE 또는 DELETE 문이거나 DDL(Data Definition Language) 명령인 경우, SQL 문을 실행합니다.
- `close()` : Statement 객체를 닫습니다.

**java.sql.PreparedStatement**


: SQL문을 보낸다. 플레이스홀더(: ?)라는 값을 통해서 미리 컴파일된 SQL문을 완성해둘 수 있음
- `executeUpdate()`: INSERT, UPDATE 또는 DELETE 문 또는 SQL DDL(Data Definition Language) 문을 실행합니다.
  - 반환값, insert/update/delete는 mysql에서 치면 몇 개(int)의 row가 나오는지 반환함(몇 개의 record가 변경되었는지 반환해준다는 말)
    - `.execute()` : 실행 유무 확인을 boolean으로 반환함 (true → 성공)
- `setString(int parameterIndex, String x)`: 지정된 인덱스의 위치홀더에 String 값을 설정합니다.
- `setInt(int parameterIndex, int x)`: 지정된 인덱스의 위치홀더에 int 값을 설정합니다.
- `executeQuery()`: SQL 문을 실행하고, 그 결과를 ResultSet 객체에 저장합니다. 
  - 얘는 DB로부터 가져온 데이터를 반환함
    - ResultSet이라는 객체를 가져옴

```java
				// 단일 학생 조회
				// SQL 쿼리를 미리 준비합니다. '?'는 위치홀더로, 나중에 실제 값으로 대체됩니다.
				String text = "1";
				String sql = "select * from student where id = ?";
				String sql2 = "SELECT * FROM student WHERE id = "+ text;
				// Q. 미리 준비된 SQL 쿼리를 실행할 PreparedStatement 객체를 생성하는 메서드를 호출해 봅시다.
				pstmt = conn.prepareStatement(sql);
				Statement stmt2 = conn.createStatement();
				stmt2.executeQuery(sql2); //보안상 문제가 있는 코드
```
**어떤 보안 상의 문제?**
`SQL Injection`

문자열 1이면 괜찮은데, 사용자가 악의적으로 “*”이나 “1 or 1 = 1”;이런 식으로 입력했다면?
→ 모든 유저 데이터가 다 나와버림
---
### 트랜잭션의 일관성(Consistency)
- 일관성이란 트랜잭션 전후의 데이터 상태가 항상 유효한 상태를 유지해야 한다는 것이다.
- **논리적 작업 단위**로 전부 성공하거나 전부 실패해야 하며 ACID 중 C에 해당한다.
- 예를 들어, 계좌이체 시 A 계좌에서 출금됐지만 B 계좌에 입금이 안 되면 데이터가 불일치하게 되어 일관성이 깨진다.