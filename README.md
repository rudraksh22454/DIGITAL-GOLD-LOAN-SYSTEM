class Main {

    // USER MODULE
    static class User {
        int userId;
        String name;
        double goldWeight;

        User(int userId, String name, double goldWeight) {
            this.userId = userId;
            this.name = name;
            this.goldWeight = goldWeight;
        }

        void displayUser() {
            System.out.println("User ID: " + userId);
            System.out.println("Name: " + name);
            System.out.println("Gold Weight: " + goldWeight + " grams");
        }
    }

    // LOAN MODULE
    static class Loan {
        int loanId;
        double loanAmount;
        double interestRate;

        Loan(int loanId, double loanAmount, double interestRate) {
            this.loanId = loanId;
            this.loanAmount = loanAmount;
            this.interestRate = interestRate;
        }

        void displayLoan() {
            System.out.println("Loan ID: " + loanId);
            System.out.println("Loan Amount: " + loanAmount);
            System.out.println("Interest Rate: " + interestRate + "%");
        }
    }

    // INTEREST MODULE
    static class Interest {
        double calculateInterest(double amount, double rate) {
            return (amount * rate * 1) / 100;
        }

        double calculateTotal(double amount, double interest) {
            return amount + interest;
        }
    }

    // MAIN METHOD
    public static void main(String[] args) {

        java.util.Scanner sc = new java.util.Scanner(System.in);

        System.out.println("Digital Gold Loan System");

        System.out.print("Enter User ID: ");
        int id = sc.nextInt();
        sc.nextLine();

        System.out.print("Enter Name: ");
        String name = sc.nextLine();

        System.out.print("Enter Gold Weight: ");
        double goldWeight = sc.nextDouble();

        User user = new User(id, name, goldWeight);

        double ratePerGram = 5000;
        double loanAmount = goldWeight * ratePerGram * 0.70;

        Loan loan = new Loan(101, loanAmount, 10);

        Interest obj = new Interest();
        double interest = obj.calculateInterest(loanAmount, 10);
        double total = obj.calculateTotal(loanAmount, interest);

        System.out.println("\nUser Details:");
        user.displayUser();

        System.out.println("\nLoan Details:");
        loan.displayLoan();

        System.out.println("\nInterest: " + interest);
        System.out.println("Total Amount: " + total);

        sc.close();
    }
}
