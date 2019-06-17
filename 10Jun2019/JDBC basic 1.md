## JDBC



#### Basic

JDBC

- 자바를 이용하여 데이터베이스에 접근하여 각종 SQL문을수행할 수 있도록 제공하는 API를 말함.

![](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1560151081749.png)

- JDBC의 구조의 역할

  - 인터페이스와 드라이버로 나눔
  - 응용프로그램에서는 SQL문을 만들어 JDBC Interface를 통해 전송하면 실제 구현 클래스인 JDBC 드라이버에서
    DBMS에 접속을 시도하여 SQL문을 전송함.
  - JDBC의 역할은 Application과 DBMS의 Bridge 역할을 함.

- JDBC 드라이브의 종류

  - JDBC-ODBC, 데이터베이스 API 드라이버, 네트워크 프로토콜 드라이버, 데이터 베이스 프로토콜 드라이버

    

  ![](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1560151367645.png)

- Tier (JDBC에서는 Tier 사용,  물리적 시스템 분할)

  - 2Tier
    - 양방향 커뮤니케이션 허용, 런타임의 효율성에 의한 모듈 분할
    - 자바 애플리케이션이 JDBC 드라이버를 통해서 직접 데이터베이스를 접근하는 형식임. JDBC 드라이버가 직접 DBMS에 전달해줌
  - 3Tier
    - 3tier
      모델은 2tier 모델에 미들웨어 계층이 추가된 형태이며, 미들웨어에서 DBMS에 직접 전달함.
      - 2tier에 비해 속도가 느리며, 유지보수의 비용을 절약 가능 ( 2tier에 비해 느슨하여 수정하기가 더 쉬움).

- Layer(논리적 시스템 분할)

  - 층상으로 중첩된 상태 혹은 개별 기초의 하나하나를 나타냄
  - 양방향 커뮤니케이션 불가능, 변경 및 관리 용이성에 의한 모듈 분할
  - JDBC를 이용한 데이터베이스 연결 방법

  

  ```
  1 단계 : import java.sql.*;
  2 단계 : 드라이버를 로드 한다.
  3 단계 : Connection 객체를 생성한다.
  4 단계 : Statement 객체를 생성한다.
  5 단계 : SQL문에 결과물이 있다면 ResultSet 객체를 생성한다.
  6 단계 : 모든 객체를 닫는다.
  ```

  ​	(Connection 주요 메서드)

![](C:\Users\student\Desktop\1.jpg)

- Statement

  - SQL문을 전송할 수 있음. 

  - 객체는 Connection 인터페이스의 createStatement() 메서드를 사용하여 얻을 수 있음.

    - select - executeQuery(String sql)
    - insert, update, delete - executeUpdate(String sql)
    - SQL을 모를 때 - execute(String sql)   

    (Statement 주요 메소드)

    ![](C:\Users\student\Desktop\2.jpg)

    - result set 객체 생성
      - SQL 결과 처리 객체
      - Statement 인터페이스의 executeQuery() 메서드를 실행한 결과로 ResultSet 객체를 리턴 받음

  ```java
  // ex) select
      package lab.java.core;
  
  import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.ResultSet;
  import java.sql.SQLException;
  import java.sql.Statement;
  
  public class DBTest {
  
  	public static void main(String[] args) {
  		Connection con = null; // DB 연결된 세션 정보가 저장되어 있음
  		Statement stat = null;
  		String url = "jdbc:oracle:thin:@localhost:1521:orcl";
  		String sql = "Select * from dept";
  		ResultSet rs = null;
  		try {
  			Class.forName("oracle.jdbc.OracleDriver");
  //			System.out.println("driver loading 성공");
  			con = DriverManager.getConnection(url, "scott", "oracle");
  //			System.out.println("db connect 성공");
  			stat = con.createStatement();
  			rs =stat.executeQuery(sql);
  			while(rs.next()) {
  				System.out.print(rs.getInt("deptno"));
  //				System.out.print(rs.getInt("1"));
  //				System.out.print(rs.getString(2));
  				System.out.print(rs.getString("dname"));
  //				System.out.println(rs.getString(3));
  				System.out.println(rs.getString("loc"));
  				
  			}
  		}
  			catch(ClassNotFoundException e) {
  				System.out.println("driver 없음");
  		}
  			catch(SQLException e) {
  				System.out.println(e.getMessage());
  				
  			}finally {
  				try {
  				if(rs!=null) rs.close();
  				if(stat!=null) stat.close();
  				if(con!=null) con.close();
  			}catch(Exception e) {
  				e.printStackTrace();
  			}
  			}//finally end
  
  	}// main end
  
  }// class end
  // ex2 ) insert
  package lab.java.core;
  
  import java.io.FileInputStream;
  import java.io.IOException;
  import java.sql.Connection;
  import java.sql.DriverManager;
  import java.sql.PreparedStatement;
  import java.sql.SQLException;
  
  import java.util.Properties;
  
  public class InsertTest {
  
  	public static void main(String[] args) {
  		Connection con = null; // DB 연결된 세션 정보가 저장되어 있음
  		PreparedStatement stat = null;
  		String sql = "insert into dept values (?,?,?) ";
  		
  		try {
  			Properties prop = new Properties();
  			prop.load(new FileInputStream("C:/workspace/JDBC/src/lab/java/core/dbinfo.properties"));
  			Class.forName(prop.getProperty("driver"));
  			System.out.println("driver loading 성공");
  			con = DriverManager.getConnection(prop.getProperty("url"),
  					prop.getProperty("user"),
  					prop.getProperty("pwd"));
  			System.out.println("db connect 성공");
  					
  			stat = con.prepareStatement(sql);
  			stat.setInt(1, 70);
  			stat.setString(2, "Bigdata");
  			stat.setString(3, "서울");
  			int rows =stat.executeUpdate(); // 변경된 행수 리턴
  			if(rows>0) {
  				System.out.println("insert 성공");
  			}
  		}
  			catch(ClassNotFoundException e) {
  				System.out.println("driver 없음");
  		}
  			catch(SQLException e) {
  				System.out.println(e.getMessage());
  				
  			}catch(IOException e) {
  				System.out.println(e.getMessage());// properties 파일의 경로 오류 및 존재 오류
  			}finally {
  				try {
  				if(stat!=null) stat.close();
  				if(con!=null) con.close();
  			}catch(Exception e) {
  				e.printStackTrace();
  			}
  			}//finally end
  
  	}// main end
  
  }// class end
  ```

  

  

  