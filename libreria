package lib;

import java.util.Scanner;

import models.Doctor;
import models.Patient;
import models.Appointment;

public class Menu {
  private static String ask(String text) {
    Scanner inputReader = new Scanner(System.in);
    System.out.print(text);
    return inputReader.nextLine();
  }

  private static String askln(String text) {
    Scanner inputReader = new Scanner(System.in);
    System.out.println(text);
    return inputReader.nextLine();
  }

  public static void printWelcome() {
    System.out.println("\n------------------");
    System.out.println("MediClinic v1.0");
    System.out.println("------------------\n");
  }

  public static void main() throws Exception {
    System.out.println("1. Doctores");
    System.out.println("2. Pacientes");
    System.out.println("3. Citas");
    String select = ask("\nSeleccione una opción: ");
    if (select.equals("1")) {
      printCrud("doctor");
    } else if (select.equals("2")) {
      printCrud("patient");
    } else if (select.equals("3")) {
      printCrud("appointment");
    }
    main();
  }
  
  private static void printCrud(String model) throws Exception {
    System.out.println("\n1. Listado");
    System.out.println("2. Buscar");
    System.out.println("3. Agregar");
    System.out.println("4. Editar");
    System.out.println("5. Eliminar");
    String select = ask("\nSeleccione una opción: ");
    if (select.equals("1")) {
      list(model);
    } else if (select.equals("2")) {
      find(model);
    } else if (select.equals("3")) {
      create(model);
    } else if (select.equals("5")) {
      delete(model);
    }
  }

  private static void list(String model) throws Exception {
    if (model.equals("doctor")) {
      System.out.println("\n----------------------");
      Doctor.all().forEach((doctor) -> {
        System.out.println(doctor.toString());
        System.out.println("----------------------");
      });
    } else if (model.equals("patient")) {
      System.out.println("\n----------------------");
      Patient.all().forEach((patient) -> {
        System.out.println(patient.toString());
        System.out.println("----------------------");
      });
    } else if (model.equals("appointment")) {
      System.out.println("\n----------------------");
      Appointment.all().forEach((appointment) -> {
        System.out.println(appointment.toString());
        System.out.println("----------------------");
      });
    }
    System.out.println("");
  }

  private static void create(String model) throws Exception {
    String firstName, surname, speciality, year, month, day, hour, minute;
    Integer doctorId, patientId;
    if (model.equals("doctor")) {
      firstName = ask("Nombre: ");
      surname = ask("Apellido: ");
      speciality = ask("Especialidad: ");
      Doctor doctor = new Doctor(firstName, surname, speciality);
      doctor.save();
      System.out.println("\nSe creo satisfactoriamente el doctor:");
      System.out.println(doctor.toString() + "\n");
    } else if (model.equals("patient")) {
      firstName = ask("Nombre: ");
      surname = ask("Apellido: ");
      Patient patient = new Patient(firstName, surname);
      patient.save();
      System.out.println("\nSe creo satisfactoriamente el paciente:");
      System.out.println(patient.toString() + "\n");
    } else if (model.equals("appointment")) {
      doctorId = Integer.parseInt(ask("Id de doctor: "));
      patientId = Integer.parseInt(ask("Id de paciente: "));
      year = ask("Año: ");
      month = ask("Mes: ");
      day = ask("Día: ");
      hour = ask("Hora (formato 24 horas): ");
      minute = ask("Minutos: ");
      String datetime = day + "/" + month + "/" + year + "-" + hour + ":" + minute;
      Appointment appointment = new Appointment(doctorId, patientId, datetime);
      appointment.save();
      System.out.println("\nSe creo satisfactoriamente la cita:");
      System.out.println(appointment.toString() + "\n");
    }
  }

  private static void delete(String model) throws Exception {
    if (model.equals("doctor")) {
      String id = ask("id: ");
      Doctor doctor = Doctor.find(Integer.parseInt(id));
      doctor.delete();
      System.out.println("\nSe eliminó satisfactoriamente el doctor:");
      System.out.println(doctor.toString() + "\n");
    } else if (model.equals("patient")) {
      String id = ask("id: ");
      Patient patient = Patient.find(Integer.parseInt(id));
      patient.delete();
      System.out.println("\nSe eliminó satisfactoriamente el paciente:");
      System.out.println(patient.toString() + "\n");
    } else if (model.equals("appointment")) {
      String id = ask("id: ");
      Appointment appointment = Appointment.find(Integer.parseInt(id));
      appointment.delete();
      System.out.println("\nSe eliminó satisfactoriamente la cita:");
      System.out.println(appointment.toString() + "\n");
    }
  }

  private static void find(String model) throws Exception {
    Integer id = Integer.parseInt(ask("id: "));
    if (model.equals("doctor")) {
      Doctor doctor = Doctor.find(id);
      System.out.println(doctor.toString() + "\n");
    } else if (model.equals("patient")) {
      Patient patient = Patient.find(id);
      System.out.println(patient.toString() + "\n");
    } else if (model.equals("appointment")) {
      Appointment appointment = Appointment.find(id);
      System.out.println(appointment.toString() + "\n");
    }
  }
}
