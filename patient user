package models;
import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.PrintWriter;
import java.util.ArrayList;
import java.util.List;

public class Patient extends ModelBase {
    private static List<Patient> all = new ArrayList<Patient>();
    private final static String databasePath = "src/db/patients.csv";

    private boolean persisted = false;
    public String firstName;
    public String surname;

    public Patient() {}

    public Patient(String firstName, String surname) {
        this.firstName = firstName;
        this.surname = surname;
    }

    public Patient(int id, String firstName, String surname) {
        this.id = id;
        this.firstName = firstName;
        this.surname = surname;
        this.persisted = true;
    }

    public String fullName() {
        return firstName + " " + surname;
    }

    public static Patient find(int id) throws Exception {
        for (int i = 0; i < all().size(); i++) {
            Patient instance = all().get(i);
            if (instance.id == id) {
                return instance;
            }
        }
        return new Patient();
    }

    private static int nextAvailableId() throws Exception {
        int higher = 0;
        for (int i = 0; i < all().size(); i++) {
            Patient instance = all().get(i);
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
            Patient d = new Patient(Integer.parseInt(row[0]), row[1], row[2]);
            all.add(d);
        }
    }

    public static List<Patient> all() throws Exception {
        reload();
        return all;
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
            this.id = Patient.nextAvailableId();
        }
        pw.append(this.id + ",");
        pw.append(this.firstName + ",");
        pw.append(this.surname + ",");
        pw.append("\n");
        pw.flush();
        pw.close();
    }

    public String toString() {
        return this.id + ", " + this.firstName + ", " + this.surname + ", ";
    }
}
