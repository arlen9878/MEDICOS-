package models;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.List;

public class User extends ModelBase {
    private static List<User> all = new ArrayList<User>();
    private final static String databasePath = "src/db/users.csv";

    private boolean persisted = false;
    public String username;
    public String password;

    public User() {}

    public User(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public User(int id, String username, String password) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.persisted = true;
    }

    public static User find(int id) throws Exception {
        for (int i = 0; i < all().size(); i++) {
            User instance = all().get(i);
            if (instance.id == id) {
                return instance;
            }
        }
        return new User();
    }

    public static User findByUsername(String username) throws Exception {
      for (int i = 0; i < all().size(); i++) {
          User instance = all().get(i);
          if (instance.username.equals(username)) {
              return instance;
          }
      }
      return new User();
  }

    private static int nextAvailableId() throws Exception {
        int higher = 0;
        for (int i = 0; i < all().size(); i++) {
            User instance = all().get(i);
            if (higher < instance.id) {
                higher = instance.id;
            }
        }
        return higher + 1;
    }

    private static void reload() throws Exception {
        String line = "";
        String delimiter = ",";
        File file = new File(databasePath);
        BufferedReader br = new BufferedReader(new FileReader(file.getAbsolutePath()));
        all.clear();
        while ((line = br.readLine()) != null) {
            String[] row = line.split(delimiter);
            User d = new User(Integer.parseInt(row[0]), row[1], row[2]);
            all.add(d);
        }
    }

    public static List<User> all() throws Exception {
        reload();
        return all;
    }

    public boolean persisted() {
      return this.persisted;
    }

    public boolean authenticate(String password) {
      return this.password.equals(password);
    }

    public void delete() throws Exception {
        if (!this.persisted)
            return;
        File file = new File(databasePath);
        File tempFile = new File(file.getAbsolutePath() + ".tmp");
        BufferedReader br = new BufferedReader(new FileReader(file.getAbsolutePath()));
        PrintWriter pw = new PrintWriter(new FileWriter(tempFile));
        String line = null;

        while ((line = br.readLine()) != null) {
            if (!line.split(",")[0].equals(Integer.toString(this.id))) {
                pw.println(line);
                pw.flush();
            }
        }

        pw.close();
        br.close();
        file.delete();
        tempFile.renameTo(file);
    }

    public void save() throws Exception {
        this.delete();
        File file = new File(databasePath);
        FileWriter pw = new FileWriter(file.getAbsolutePath(), true);
        if (this.persisted == false) {
            this.id = User.nextAvailableId();
        }
        pw.append(this.id + ",");
        pw.append(this.username + ",");
        pw.append(this.password + ",");
        pw.append("\n");
        pw.flush();
        pw.close();
    }

    public String toString() {
        return this.id + ", " + this.username + ", " + this.password + ", ";
    }
}
