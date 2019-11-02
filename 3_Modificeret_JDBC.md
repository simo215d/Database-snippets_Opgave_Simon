Jeg har gjort så den looper #2, #3 og #4 så man kan blive ved med at indtaste SQL kommandoer, med mindre man indtaster "exit", så går den til #5. Jeg gjorde også så man kan indtaste hvor mange columns man vil vise. variablen hedder "collNum" og den bliver brugt i #4.
```
import java.sql.*;
import java.util.Scanner;

public class SimpleJdbc {
    public static void main(String[] args) throws SQLException {

        System.out.print("----- \nProgram til hentning af landedata fra world.sql databasen. \n ");

        // #1. Connect to the database
        Connection connection = null;
        connection = DriverManager.getConnection(
                "jdbc:mysql://localhost/Legoklodser?serverTimezone=UTC",
                "root",
                "qtj38gve");
        System.out.println("\nDatabase connected.");

        while(true) {
            System.out.println("enter sql:");
            Scanner scanner = new Scanner(System.in);

            // #2. Create a statement
            String mitQuery = scanner.nextLine();
            if (mitQuery.equals("exit")) break;
            System.out.println("Enter number of columns");
            int collNum = scanner.nextInt();
            Statement statement = connection.createStatement();

            // #3. Execute the statement and send the SQL-query to the SQL-server
            ResultSet resultSet = statement.executeQuery(mitQuery);
            System.out.println("Følgende query er sendt til MySQL-serveren: " + mitQuery);
            System.out.println("Svar fra databasen: " + "\n");


            // #4. Iterate through the result and print the results
            // (vi har måske flere resultater end 1, derfor vil en løkke læse alle rækker ud fra resultSettet)
            while (resultSet.next()) {
                for (int x = 1; x <= collNum; x++) {
                    System.out.print(resultSet.getString(x) + ", ");
                }
                System.out.println();
            }
        }
        // #5. Close the connection (always!)
        connection.close();
        System.out.println("BYE");
    }
}
```
