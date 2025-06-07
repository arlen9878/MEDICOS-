package models;

import java.io.*;
import java.util.ArrayList;
import java.util.List;
import models.Doctor;
import models.Patient;

public class Appointment extends ModelBase {
    private static List<Appointment> all = new ArrayList<Appointment>();
    private final static String databasePath = "src/db/appointments.csv";

    private boolean persisted = false;
    public Integer doctorId;
    public Integer patientId;
    public String datetime;

    public Appointment() {}

    public Appointment(Integer doctorId, Integer patientId, String datetime) {
        this.doctorId = doctorId;
        this.patientId = patientId;
        this.datetime = datetime;
    }

    public Appointment(int id, Integer doctorId, Integer patientId, String datetime) {
        this.id = id;
        this.doctorId = doctorId;
        this.patientId = patientId;
        this.datetime = datetime;
        this.persisted = true;
    }

    public static Appointment find(int id) throws Exception {
        for (int i = 0; i < all().size(); i++) {
            Appointment instance = all().get(i);
            if (instance.id == id) {
                return instance;
            }
        }
        return new Appointment();
    }

    private static int nextAvailableId() throws Exception {
        int higher = 0;
        for (int i = 0; i < all().size(); i++) {
            Appointment instance = all().get(i);
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
            Appointment d = new Appointment(Integer.parseInt(row[0]), Integer.parseInt(row[1]), Integer.parseInt(row[2]), row[3]);
            all.add(d);
        }
    }

    public static List<Appointment> all() throws Exception {
        reload();
        return all;
    }

    public boolean persisted() {
        return this.persisted;
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
            this.id = Appointment.nextAvailableId();
        }
        pw.append(this.id + ",");
        pw.append(this.doctorId + ",");
        pw.append(this.patientId + ",");
        pw.append(this.datetime);
        pw.append("\n");
        pw.flush();
        pw.close();
    }

    public String toString() {
        try {
            return this.id + ", " + Doctor.find(this.doctorId).fullName() + ", " + Patient.find(this.patientId).fullName() + ", " + this.datetime;
        } catch (Exception e) {
            return "Error";
        }
    }
}
