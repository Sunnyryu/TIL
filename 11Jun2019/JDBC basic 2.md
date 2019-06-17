## JDBC



#### Basic

JDBC 복습



- 프로그래밍 단계

  - 연결할 데이터베이스의 driver class 클래스 (~.jar)를 운영체제의 환경변수 classpath에 추가
  - JDK 또는 JRE의 라이브러리 검색 위치에 넣어줌 (외부 확장 라이브러리 (JRE나 JDK에 있는 ext에 보통에 넣어줌..)
  - 이클립스에서 build path>configure build path>library>library>library add external jar......추가

  ```java
  1.import java.sql.*: - JDBC API import 함
  2. DriverClass 로딩
  try{
  Class.forName(" ");//oracle.jdbc.OracleDriver
  }catch(ClassNotFoundException e){
  
  }
  3. Connection
      로딩된 드라이버 클래스의 static 맴버 객체
  	DriverManager.getConnection(url, user ,pwd) 이용해서 DB에 connect합니다.
      DB에 connect합니다.
      DB에 세션 생성되고, 세션이 리턴됩니다. => java.sql.Connection객체로 받습니다.
      Connection 인터페이스에 주요 메소드 :close(), createStatement(), propareStatedment(), callableStatement(). setAutoCommit(),setAutoCommit(false), commit(), rollback(), setSavepoint(),.. 
  4. SQL 실행 대행 객체 Statement 객체 생성 
  Statement : 완전한 sql 문장을 문자열로 DB에 전송하므로 매번 hard parsing을 수행될 확률이 높음
  PreparedStatement : sql 문장 중에서 변경되는 부분들을 ? (index 파라미터)로 설정하여 미리 sql을 전송하고 실행할 때마다 값만 전송해서 실행(soft parsing으로 수행될 확률이 높음!)
  CallableStatement : DB에 저장되어 잇는 Pprocedure, function을 호출해서 결과를 받을 때
  5. SQL 문 실행
  executeQuery() - select문장, ResultSet 객체 리턴
  executeUpdate() - DML문은 int 리턴 타입(int가 의미하는 것은 변경된 행수), DDL, DCL문
  execute() - select문, DML문, boolean 리턴(true면 select로 수행, false면 select가 아닌 것을 사용)
  6. select 수행 결과 처리
  while(re.next()){
  	rs.getint(컬럼명이나 셀렉트에 정의된 숫자 번호를 사용함(컬럼 position)), rs.getdouble()...
  	rs.getString(컬럼 position) (날짜나 문자열)
  	rs.getDate()
  	
  }
  7. SQLException 예외 처리
  8. 사용했던 자원 (Connection, Statement, ResultSet) 반납
  	close()   --- > exception 처리 해줘야함
  	
  ```

  - 소스코드에 db연결정보를 hard coding 하는 것은 보안상 문제가 되므로 보안 폴더에 properties를 만들어줌
    - 보안폴더는 내부에서만 접근 가능한 거임..
    - properties파일에 key=value형태로 저장함

```java 
Properties prop = new Properties();
prop.load(new FileInputStream("경료/이름.."));
String value = prop.getProperty("key");
```

##### JDBC

- Transction
  - 트랜잭션이란 여러 개의 오퍼레이션을 하나의 작업 단위로 묶어 주는 것을 말함
  - 트랜잭션은 하나의 작업 단위의 일들은 전체 작업이 모두 올바르게 수행되거나 또는 전체 작업 이 모두 수행되지 않아야함
  - 원자성, 일관성, 독립성(분리), 지속성을 가짐

```
setAutoCommit(boolean autoCommit) – autoCommit이 true이면 트랜잭션을 시작하지 않겠다는 의미, false 이면 트랜잭션을 시작하겠다는 의미임
commit() – setAutoCommit(false)와 commit() 사이에 있는 모든 operation를 수행하겠다는 의미임
rollback() - setAutoCommit(false)와 rollback() 사이에 있는 모든 operation를 수행하지 않겠다는 의미임.

```

- properties
  - properties파일의 집합을 추상화 클래스
  - Stream를 로드하여 저장 가능, Map 형태로 관리하여 Key를 알면 Key에 대한 Value을 얻어올 수 있는 클래스

```java
//ex 1)
package lab.java.core;

import java.io.FileInputStream;
import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Savepoint;
import java.sql.Statement;
import java.util.Properties;

public class TransactionTest {

	public static void main(String[] args) {
		Connection con = null; //DB 연결상태 세션 정보 저장
		PreparedStatement selectPs = null; 
		PreparedStatement updatePs = null; 
		ResultSet rs = null; 
		String query = "SELECT id, price FROM product WHERE price > ?"; 
		String update = "UPDATE product SET price = ? WHERE id = ?"; 
		
		try {
			Properties prop = new Properties();
			prop.load(new FileInputStream("C:/workspace/JDBC/src/lab/java/core/dbinfo.properties"));
			
			Class.forName(prop.getProperty("driver"));
			System.out.println("driver loading 성공");
			con = DriverManager.getConnection(prop.getProperty("url"),
					prop.getProperty("user"),
					prop.getProperty("pwd"));
			System.out.println("db connect 성공");
			
			con.setAutoCommit(false);  //명시적 트랜잭션 제어를 위해  
			
			selectPs = con.prepareStatement(query); 
			updatePs = con.prepareStatement(update); 

			selectPs.setInt(1, 100); 
			rs = selectPs.executeQuery(); 

			Savepoint save1 = con.setSavepoint(); 
			while (rs.next()) { 
				String id = rs.getString("id"); 
				int oldPrice = rs.getInt("price"); 
				int newPrice = (oldPrice * 2); 
				updatePs.setInt(1, newPrice); 
				updatePs.setString(2, id); 
				updatePs.executeUpdate(); 
				System.out.println("New Price of " + oldPrice+ 
						" is " + newPrice); 
				if (newPrice >= 5000) {
					con.rollback(save1); 
				} 
			} //while end
			
			System.out.println(); 			
			selectPs.setInt(1, 100); 
			rs = selectPs.executeQuery(); 

			Savepoint save2 = con.setSavepoint(); 

			while (rs.next()) { 
				String id = rs.getString("id"); 
				int oldPrice = rs.getInt("price"); 
				int newPrice = (oldPrice * 2); 
				updatePs.setInt(1, newPrice); 
				updatePs.setString(2, id); 
				updatePs.executeUpdate(); 
				System.out.println("New price of  is " +newPrice); 
				if (newPrice >= 5000) { 
					con.rollback(save2); 
				} 
			} 
			System.out.println(); 
			con.commit(); 			
			
			Statement stmt = con.createStatement(); 
			rs = stmt.executeQuery("SELECT id, price FROM product"); 

			System.out.println(); 
			while (rs.next()) { 
				String id = rs.getString("id");
				int price = rs.getInt("price"); 
				System.out.println("id : "+ id 
						+" , price : " + price); 
			} 
			
		}catch(ClassNotFoundException e) {
			System.out.println("driver없음");
		}catch(SQLException e) {
			System.out.println(e.getMessage());
			//db 연결 실패
		}catch(IOException e) {
			System.out.println(e.getMessage()); //properties파일의 경로, 존재 오류
		}finally {
			try {			 
				if(rs != null)rs.close(); 
				if(selectPs != null)selectPs.close(); 
				if(updatePs != null)updatePs.close(); 
				if(con != null)con.close();
			}catch(Exception e) {
				e.printStackTrace();
			}
		}//finally end	

	}//main end

}//class end


```

```java
package lab.jdbc.biz;

import java.io.FileInputStream;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.ArrayList;
import java.util.Properties;

import lab.jdbc.entity.Book;
import lab.jdbc.util.BookUtil;

public class BookBiz {
	private ArrayList<Book> books;
	
	public BookBiz(){
		super();
	}
	public Connection dbCon() {
		Connection con = null;
		try {
			Properties prop = new Properties();
			prop.load(new FileInputStream("C:/workspace/JDBC/src/lab/java/core/dbinfo.properties"));
			
			Class.forName(prop.getProperty("driver"));
			con = DriverManager.getConnection(prop.getProperty("url"),
					prop.getProperty("user"),
					prop.getProperty("pwd"));
		}catch(Exception e) {
			e.printStackTrace();
		}
		return con;
	}
	public void dbClose(Connection con, Statement stat, ResultSet rs) {
		try {			 
			if(rs!= null)rs.close(); 
			if(stat!= null)stat.close(); 
			if(con != null)con.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
		
	}
	public void printAllBooks() {//모든책 
		Connection con = null;
		Statement stat = null;
		String sql = "select * from book";
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.createStatement();
			rs = stat.executeQuery(sql);
			BookUtil.printHeader();
			while(rs.next()) {
				Book book = new Book();
				book.setIsbn(rs.getString("isbn"));
				book.setTitle(rs.getString("title"));
				book.setAuthor(rs.getString("author"));
				book.setPrice(rs.getInt("price"));
				book.setDescript(rs.getString("descript"));
				System.out.println(book);
			}
			BookUtil.printTail();
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		
	}
	public void printAllNovels() {//모든 소설만 출력하기 위해
		Connection con = null;
		Statement stat = null;
		String sql = "select * from book where isbn like 'N%'";//Novel이 n으로 시작하기때문에
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.createStatement();
			rs = stat.executeQuery(sql);
			BookUtil.printHeader();
		while(rs.next()) {
			Book book = new Book();
			book.setIsbn(rs.getString("isbn"));
			book.setTitle(rs.getString("title"));
			book.setAuthor(rs.getString("author"));
			book.setPrice(rs.getInt("price"));
			System.out.println(book);
			
			}
			BookUtil.printTail();
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		
	}
	public void printAllmagazine() {//모든 잡지만 출력하기 위해
		Connection con = null;
		Statement stat = null;
		String sql = "select * from book where isbn like 'M%'";//Magazine이 m으로 시작하기 떄문에
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.createStatement();
			rs = stat.executeQuery(sql);
			BookUtil.printHeader();
		while(rs.next()) {
			Book book = new Book();
			book.setIsbn(rs.getString("isbn"));
			book.setTitle(rs.getString("title"));
			book.setAuthor(rs.getString("author"));
			book.setPrice(rs.getInt("price"));
			System.out.println(book);
			
			}
			BookUtil.printTail();
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		
	}
	public void printMagazineOneYearSubscription() {// 잡지 1년 수익
		Connection con = null;
		Statement stat = null;
		String sql = "select * from book where isbn like 'M%'";
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.createStatement();
			rs = stat.executeQuery(sql);
			int num = 1;
		while(rs.next()) {
			System.out.println(num++ +". "+rs.getString("title")+":"+rs.getInt("price")*12+"원");
			
			}
			System.out.println("----------------------");
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		
	}
		
	
	public ArrayList<Book> searchNovelByAuthor(String author) {//소설가 이름으로 출력
		ArrayList<Book> searchBooks = new ArrayList();
		Connection con = null;
		PreparedStatement stat = null;
		String sql = "select * from book where isbn like 'N%' and author like ?";
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.prepareStatement(sql);
			stat.setString(1, "%"+author+"%");
			rs = stat.executeQuery();
		while(rs.next()) {
			Book book = new Book();
			book.setIsbn(rs.getString("isbn"));
			book.setTitle(rs.getString("title"));
			book.setAuthor(rs.getString("author"));
			book.setPrice(rs.getInt("price"));
			searchBooks.add(book);
		}
		
			
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		return searchBooks;
	}
		
	public ArrayList<Book> searchNovelByPrice(int minPrice, int maxPrice){// 최대 최소값 범위 이용
		
		
		ArrayList<Book> searchBooks = new ArrayList();
		Connection con = null;
		PreparedStatement stat = null;
		String sql = "select * from book where isbn like 'N%' and price between ? and ?";
		ResultSet rs = null;
		try {
			con = dbCon();
			stat = con.prepareStatement(sql);
			stat.setInt(1, minPrice);
			stat.setInt(2, maxPrice);
			rs = stat.executeQuery();
		while(rs.next()) {
			Book book = new Book();
			book.setIsbn(rs.getString("isbn"));
			book.setTitle(rs.getString("title"));
			book.setAuthor(rs.getString("author"));
			book.setPrice(rs.getInt("price"));
			searchBooks.add(book);
		}
		
			
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, rs);
		}
		return searchBooks;
	}
	public int insertBook(Book newBook) {// 삽입하기.
		int rows = 0;
		Connection con = null;
		PreparedStatement stat = null;
		String novel = "insert into book (ibsn, title, author, price) values (?,?,?,?)";
		String magazine = "insert into book (ibsn, title, price, category, descript) values (?,?,?,?,?)";
		try {
			con = dbCon();
			if(newBook.getIsbn().startsWith("N")) {
				stat = con.prepareStatement(novel);
				stat.setString(1, newBook.getIsbn());
				stat.setString(2, newBook.getTitle());
				stat.setString(3, newBook.getAuthor());
				stat.setInt(4, newBook.getPrice());
			}else {
				stat = con.prepareStatement(magazine);
				stat.setString(1, newBook.getIsbn());
				stat.setString(2, newBook.getTitle());
				stat.setInt(3, newBook.getPrice());
				stat.setString(4, newBook.getCategory());
				stat.setString(5, newBook.getDescript());
			}
			rows = stat.executeUpdate();
		}catch (Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, null);
		}
		return rows;
	}
	public int updateBook(Book modifyBook) {// 수정하기
		int rows = 0;
		Connection con = null;
		PreparedStatement stat = null;
		String novel = "update book set price =? where isbn = ?";
		String magazine = "update book set price = ?, descript = ? where isbn = ?";
		try {
			con = dbCon();
			if(modifyBook.getIsbn().startsWith("N")) {
				stat = con.prepareStatement(novel);
				stat.setString(2, modifyBook.getIsbn());
				stat.setInt(1, modifyBook.getPrice());
			}else {
				stat = con.prepareStatement(magazine);
				stat.setString(3, modifyBook.getIsbn());
				stat.setInt(1, modifyBook.getPrice());
				stat.setString(2, modifyBook.getDescript());
			}
			rows = stat.executeUpdate();
		}catch (Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, null);
		}
		return rows;
		
	}
	public int deleteBook(String isbn) {// 삭제하기
		int rows = 0;
		Connection con = null;
		PreparedStatement stat = null;
		String sql = "delete from book where isbn = ?";
		try {
			con = dbCon();
			stat = con.prepareStatement(sql);
			stat.setString(1,  isbn);
			rows = stat.executeUpdate();
		
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			dbClose(con, stat, null);
		}
		return rows;
		
	}
	
		
		
	}
	
```

