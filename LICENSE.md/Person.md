import java.io.IOException;
import java.sql.*;

public class Person {

    private String firstName;
    private String lastName;
    private int ballance;
    private String login;
    private String password;



    public String getLogin() {
        return login;
    }

    public void setLogin(String login) {
        this.login = login;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }


    public String getFirstName() {
        return firstName;
    }


    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }


    public String getLastName() {
        return lastName;
    }


    public void setLastName(String lastName) {
        this.lastName = lastName;
    }

    public int getBallance() {
        return ballance;
    }

    public void setBallance(int ballance) {
        this.ballance = ballance;
    }


    //Операция транзакции
    public void transaktion(Person person, int i) {
        if (i < 0) System.out.println("Ошибка");
        else {
            if (ballance < i) System.out.println("Отказано в переведе. Недостаточно средств");
            else {
                person.setBallance(person.getBallance() + i);
                setBallance(getBallance() - i);
            }
        }
    }

    public void createAccount(Person person) throws ClassNotFoundException, SQLException, IOException {
        String userName = "root";
        String password = "komajavadev";
        String URL = "jdbc:mysql://localhost:3306/PERSON_BANKS";
        Class.forName("com.mysql.jdbc.Driver");
        try (Connection connection = DriverManager.getConnection(URL, userName, password);
             Statement statement = connection.createStatement()) {
            statement.executeUpdate("INSERT INTO person (firstName, lastName, login, password) VALUES ('" + person.getFirstName() + "','" + person.getLastName() + "','" + person.getLogin() + "','" + person.getPassword() + "')");

        }

    }
}
