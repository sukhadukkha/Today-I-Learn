# ☕ Java 공부 기록

## 📘 학습 날짜
- 2025-06-20

## 📅 오늘 배운 내용

### ✨ 1. 자바 중급 1편 섹션 8 중첩클래스, 내부클래스2

#### 🔍 1-1. 지역 클래스, 익명클래스에 대하여

### 📍 지역 클래스 (Local class)
메서드 내부에 정의되는 클래스.

바깥 클래스와 지역 변수에 접근 가능.

단, 접근하는 지역 변수는 final 또는 사실상 final이어야 함.

```java
public void process(int paramVar) {
int localVar = 1;

    class LocalPrinter {
        public void print() {
            System.out.println(localVar); // 캡처됨
        }
    }

    LocalPrinter printer = new LocalPrinter();
    printer.print();
}
```


### 지역 변수 캡처란? 
인스턴스 생성 시 지역 변수의 값을 복사해 인스턴스 내부에 저장하는 것.

### 🤖 익명 클래스 (Anonymous class)
이름 없이 일회성으로 사용되는 지역 클래스.

클래스 선언과 객체 생성을 동시에 수행.

```java

Printer printer = new Printer() {
public void print() {
System.out.println("Hello from anonymous!");
}
};
```
### 특징
인터페이스 또는 추상 클래스 구현 필수.

생성자 없음 (이름이 없기 때문).

바깥 클래스, 지역 변수, 매개변수 모두 접근 가능 (지역 변수는 캡처됨).

💡 사용 목적
특정 클래스 내부에서만 사용되는 클래스를 감추고 싶을 때.

바깥 클래스와 긴밀하게 연결된 로직을 그룹화할 때.

코드 간결성과 캡슐화를 위해.

람다를 통해 메서드만 넘겨줄 수 있음. 

### 문제와 풀이 : 도서관리 시스템 

```java
package nested.test.ex1;

public class Library {

    private Book[] books;
    private int bookCount;


    public Library(int size) {
        books = new Book[size];
        bookCount = 0;
    }

    public void addBook(String title, String author) {
        if (bookCount < books.length) {
            books[bookCount++] = new Book(title, author);

        } else {
            System.out.println("도서관 저장 곤간이 부족합니다");
        }
    }
    public void showBooks() {
        for (int i = 0; i < books.length; i++) {
            System.out.println("도서 제목: " + books[i].title + ", 저자: " + books[i].author);
        }
    }

    static class Book {
        private String title;
        private String author;

        public Book(String title, String author) {
            this.title = title;
            this.author = author;
        }

    }
}

```
```java
package nested.test.ex1;

public class LibraryMain {
    public static void main(String[] args) {
        Library library = new Library(4);   //최대 4권의 도서를 저장할 수 있는 도서관 생성
        library.addBook("책1", "저자1");
        library.addBook("책2", "저자2");
        library.addBook("책3", "저자3");
        library.addBook("자바 ORM 표준 JPA 프로그래밍", "김영한");
        library.addBook("OneMoreThing", "잡스");
        library.showBooks(); // 도서관의 모든 도서 정보 출력
    }
}

```

