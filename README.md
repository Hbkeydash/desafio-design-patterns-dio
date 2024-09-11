# desafio-design-patterns-dio

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Implementação da Interface, EvaluationStrategy e seu método abstrato:
interface EvaluationStrategy {
    String evaluate(double average);
}

// Classe Concreta, ExcellentStrategy e sua lógica de resolução aplicada:
class ExcellentStrategy implements EvaluationStrategy {
    public String evaluate(double average) {
        return average >= 9 ? "Excelente" : "";
    }
}

// TODO: Crie a classe Concreta, GoodStrategy e sua lógica de avaliação aplicada:
class GoodStrategy implements EvaluationStrategy {
    public String evaluate(double average) {
        return average >= 7 && average < 9 ? "Bom" : "";
    }
}

// TODO: Crie a classe Concreta, RegularStrategy e sua lógica de avaliação aplicada:
class RegularStrategy implements EvaluationStrategy {
    public String evaluate(double average) {
        return average >= 5 && average < 7 ? "Regular" : "";
    }
}

// TODO: Crie a classe Concreta, UnsatisfactoryStrategy e sua lógica de avaliação aplicada:
class UnsatisfactoryStrategy implements EvaluationStrategy {
    public String evaluate(double average) {
        return average < 5 ? "Insatisfatório" : "";
    }
}

public class ProjectEvaluation {

    private static final List<Double> evaluations = new ArrayList<>();

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);


        double evaluation1 = scanner.nextDouble();
        evaluations.add(evaluation1);

  
        double evaluation2 = scanner.nextDouble();
        evaluations.add(evaluation2);

        double average = calculateAverage(evaluations);

        EvaluationStrategy[] strategies = {
            new ExcellentStrategy(),
            new GoodStrategy(),
            new RegularStrategy(),
            new UnsatisfactoryStrategy()
        };

        String status = "";
        for (EvaluationStrategy strategy : strategies) {
            status = strategy.evaluate(average);
            if (!status.isEmpty()) {
                break;
            }
        }

        System.out.printf("Media: %.1f. Status: %s.%n", average, status);
    }

    private static double calculateAverage(List<Double> evaluations) {
        double sum = 0;
        for (double eval : evaluations) {
            sum += eval;
        }
        return sum / evaluations.size();
    }
}


-----------------------------------------------------------------------------------------------------------------------------


import java.time.LocalTime;
import java.util.Scanner;

// Classe TimeFactory:
class TimeFactory {
    // TODO: Crie o método estático para criar um objeto LocalTime a partir de uma string:
    public static LocalTime createTime(String timeString) {
        //TODO: Implemente o LocalTime.parse() para converter a string em LocalTime:
    return LocalTime.parse(timeString);
    }
}

public class MeetingScheduler {

    private static final LocalTime MIN_TIME = LocalTime.of(9, 0); 
    private static final LocalTime MAX_TIME = LocalTime.of(18, 0); 
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

      
        String desiredTimeInput = scanner.nextLine();
        //TODO: Implemente o TimeFactory.createTime() para converter desiredTimeInput em LocalTime:
        LocalTime desiredTime = TimeFactory.createTime(desiredTimeInput);


        String currentTimeInput = scanner.nextLine();
        //TODO: Implemente o TimeFactory.createTime() para converter currentTimeInput em LocalTime:
        LocalTime currentTime = TimeFactory.createTime(currentTimeInput);

        if (isMeetingSchedulable(desiredTime)) {
            System.out.println("Reuniao pode ser agendada.");
        } else {
            System.out.println("Reuniao nao pode ser agendada. Horario fora do intervalo permitido.");
        }
    }

    private static boolean isMeetingSchedulable(LocalTime desiredTime) {
        return !desiredTime.isBefore(MIN_TIME) && !desiredTime.isAfter(MAX_TIME);
    }
}


-----------------------------------------------------------------------------------------------------------------------------------


import java.util.Scanner;

// Classe Employee para representar os detalhes do funcionário:
class Employee {
    private int hoursWorked;
    private double hourlyRate;

    public Employee(int hoursWorked, double hourlyRate) {
        this.hoursWorked = hoursWorked;
        this.hourlyRate = hourlyRate;
    }

    public double calculateSalary() {
        return hoursWorked * hourlyRate;
    }
}

// TODO: Implemente a classe Factory para criar objetos Employee:
class EmployeeFactory {
    // TODO: Implemente o método createEmployee:
    // Método estático para criar e retornar um objeto Employee:
    public static Employee createEmployee(int hoursWorked, double hourlyRate) {
        return new Employee(hoursWorked, hourlyRate);
    }
}


public class SalaryCalculator {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

      
        int hoursWorked = scanner.nextInt();
        double hourlyRate = scanner.nextDouble();
        
        // TODO: Utilize o Factory Method para criar um objeto Employee:
        Employee employee = EmployeeFactory.createEmployee(hoursWorked, hourlyRate);
        
        
        double salary = employee.calculateSalary();

        System.out.printf("Salario total: %.1f%n", salary);
    }
}
