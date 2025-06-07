package lib;
import java.util.Scanner;

import models.User;

public class Login {
  public static void authenticate() throws Exception {
    Scanner inputReader = new Scanner(System.in);
    String username, password;
    System.out.print("Usuario: ");
    username = inputReader.nextLine();
    System.out.print("Contraseña: ");
    password = inputReader.nextLine();
    User user = User.findByUsername(username);
    if (user.persisted() && user.authenticate(password)) {
        System.out.println("\n------------------");
        System.out.println("Bienvenido " + user.username);
        System.out.println("------------------\n");
    } else {
        System.out.println("\nUsuario y/o contraseña inválida, intente nuevamente.\n");
        authenticate();
    }
  }
}
