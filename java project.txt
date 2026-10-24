
import java.util.Scanner;
import java.time.LocalDate;
import java.time.temporal.ChronoUnit;

class InsurancePolicy {
    int policyNo;
    String customerName;
    String policyName;
    double premium;
    LocalDate dueDate;

    InsurancePolicy(int no, String customer, String policy,
                    double amount, LocalDate date) {
        policyNo = no;
        customerName = customer;
        policyName = policy;
        premium = amount;
        dueDate = date;
    }

    void display() {
        System.out.println("\nPolicy Number: " + policyNo);
        System.out.println("Customer Name: " + customerName);
        System.out.println("Policy Name: " + policyName);
        System.out.println("Premium Amount: Rs." + premium);
        System.out.println("Due Date: " + dueDate);
    }

    void checkReminder() {
        LocalDate today = LocalDate.now();
        long days = ChronoUnit.DAYS.between(today, dueDate);

        if (days < 0) {
            System.out.println("Reminder: Premium is overdue!");
        } else if (days == 0) {
            System.out.println("Reminder: Premium is due today!");
        } else if (days <= 7) {
            System.out.println("Reminder: Premium due in "
                               + days + " days.");
        } else {
            System.out.println("No immediate reminder needed.");
        }
    }
}

public class InsuranceManagement {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        InsurancePolicy[] policies = new InsurancePolicy[100];
        int count = 0;
        int choice;

        do {
            System.out.println("\n--- Insurance Policy Management ---");
            System.out.println("1. Add Policy");
            System.out.println("2. Display All Policies");
            System.out.println("3. Check Premium Reminder");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            choice = sc.nextInt();
            sc.nextLine();

            switch (choice) {
                case 1:
                    if (count == policies.length) {
                        System.out.println("Policy storage is full.");
                        break;
                    }

                    System.out.print("Enter Policy Number: ");
                    int no = sc.nextInt();
                    sc.nextLine();

                    System.out.print("Enter Customer Name: ");
                    String name = sc.nextLine();

                    System.out.print("Enter Policy Name: ");
                    String policy = sc.nextLine();

                    System.out.print("Enter Premium Amount: ");
                    double amount = sc.nextDouble();
                    sc.nextLine();

                    System.out.print("Enter Due Date (YYYY-MM-DD): ");
                    LocalDate date = LocalDate.parse(sc.nextLine());

                    policies[count++] = new InsurancePolicy(
                        no, name, policy, amount, date
                    );

                    System.out.println("Policy added successfully!");
                    break;

                case 2:
                    if (count == 0) {
                        System.out.println("No policies available.");
                    } else {
                        for (int i = 0; i < count; i++) {
                            policies[i].display();
                        }
                    }
                    break;

                case 3:
                    if (count == 0) {
                        System.out.println("No policies available.");
                    } else {
                        for (int i = 0; i < count; i++) {
                            System.out.println("\nPolicy: "
                                               + policies[i].policyNo);
                            policies[i].checkReminder();
                        }
                    }
                    break;

                case 4:
                    System.out.println("Thank you for using the system!");
                    break;

                default:
                    System.out.println("Invalid choice. Try again.");
            }
        } while (choice != 4);

        sc.close();
    }
}
