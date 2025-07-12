public class Book {
    private Integer id;
    private String title;
    private String author;
    private String isbn;
    private Boolean available;

    // Constructor, getters, and setters
    public Book(Integer id, String title, String author, String isbn, Boolean available) {
        this.id = id;
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.available = available;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getIsbn() {
        return isbn;
    }

    public void setIsbn(String isbn) {
        this.isbn = isbn;
    }

    public Boolean getAvailable() {
        return available;
    }

    public void setAvailable(Boolean available) {
        this.available = available;
    }
}
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class BookService {
    private List<Book> books = new ArrayList<>();

    public Book addBook(Book book) {
        books.add(book);
        return book;
    }

    public List<Book> getAllBooks() {
        return books;
    }

    public Book getBookById(Integer id) {
        return books.stream()
                .filter(book -> book.getId().equals(id))
                .findFirst()
                .orElse(null);
    }

    public void deleteBook(Integer id) {
        books.removeIf(book -> book.getId().equals(id));
    }

    public Book updateBookAvailability(Integer id, Boolean available) {
        Book book = getBookById(id);
        if (book != null) {
            book.setAvailable(available);
        }
        return book;
    }
} 
public class BookController {
    private BookService bookService = new BookService();

    public void addBook(Book book) {
        bookService.addBook(book);
    }

    public void getAllBooks() {
        List<Book> books = bookService.getAllBooks();
        System.out.println("All Books:");
        books.forEach(System.out::println);
    }

    public void getBookById(Integer id) {
        Book book = bookService.getBookById(id);
        System.out.println("Book by ID:");
        System.out.println(book);
    }

    public void deleteBook(Integer id) {
        bookService.deleteBook(id);
    }

    public void updateBookAvailability(Integer id, Boolean available) {
        Book book = bookService.updateBookAvailability(id, available);
        System.out.println("Updated Book:");
        System.out.println(book);
    }
}
public class Main {
    public static void main(String[] args) {
        BookController bookController = new BookController();

        // Add books
        Book book1 = new Book(1, "Book 1", "Author 1", "ISBN-1", true);
        Book book2 = new Book(2, "Book 2", "Author 2", "ISBN-2", false);
        bookController.addBook(book1);
        bookController.addBook(book2);

        // Get all books
        bookController.getAllBooks();

        // Get book by ID
        bookController.getBookById(1);

        // Delete book
        bookController.deleteBook(2);

        // Update book availability
        bookController.updateBookAvailability(1, false);
    }
}
