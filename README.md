BoardMain, BoardSVC, BoardVO, DatabaseUtil
1. 문제명 : 게시판(board) HashMap으로 만들었던 것을 SQL로 저장하기

2. 각 클래스 역할
 1) DatabaseUtil 클래스 >> 데이터베이스 기능 클래스(connect, disconnect, insert, search, update, delete 메서드)
 2) BoardMain 클래스 >> 메뉴 보여주기, 메뉴 고르면 메서드 호출하기
 3) BoardVO 클래스 : DB에서 받아온 정보 받아와 객체화하는 멤버(id, writer, passwd, subject, email)를 가진 클래스 
 4) BoardSVC 클래스 : 등록, 수정, 삭제, 목록, 검색 기능이 있는 클래스(메인에서 불러올 기능들)

3. 클래스 세부 설명
 1) BoardSVC 클래스 기능 설명
  1.1) 등록 >> 게시글 정보 받아와 DB로 전송하기
  1.2) 수정 >> 목록을 불러온 후 제목, 작성자, 비밀번호를 입력 받아 일치하면 삭제하기
  1.3) 삭제 >> 목록을 불러온 후 몇번 인덱스 선택할지 물어보기 비밀번호 물어봐서 맞다면 삭제하기
  1.4) 게시글 목록 보여주기 
  1.5) 검색 >> 제목, 작성자, 이메일 검색 기능 만들기
  (로그인 기능은 안해도 됨)

 2) BoardVO 클래스 수정사항
  2.1) 멤버(register, subject, email, passwd)를 사용해 데이터 베이스와 연결하기
  2.2) 기존 BoardVO register를 데이터베이스의 writer로 바꾸기
  2.3) 기존 BoardVO에 id를 추가해 글 작성때마다 인덱스로 사용하기.(pk값)

 3) DatabaseUtil 클래스
  3.1) 데이터베이스 기능을 담은 클래스.
  3.2) disconnect 메서드(추가 됨, connect 끊는 메서드) >> 매개 변수가 stmt, pstmt, con일때 각각 오버로딩하여 connect를 close()할 수 있는 메서드 만들기

4. 연습문제 목적 : 메인 클래스에서 메뉴 보여주고 메뉴를 고르면 메서드를 호출하도록 작성하기
모든 메뉴를 데이터 베이스와 연결하기


2024.03.21 update 내용

DatabaseUtil 클래스 public int sizeOfArticles() >> 작성된 게시글 숫자 반환

BoardSVC 클래스 public void changeArticle()
public void removeArticles()

삭제, 수정 메서드에 게시글이 없다면 "게시글이 없으므로 종료합니다." 문구나오고 메서드 종료.
"작성된 게시글의 수: "+size 출력
게시글이 있는데 해당 id의 게시글이 없으면 null값을 반환하므로 문자열 equals() 메서드에서 예외가 발생하여 해당 id 게시글 존재하지 않는다고 반환 후 메서드 종료.
