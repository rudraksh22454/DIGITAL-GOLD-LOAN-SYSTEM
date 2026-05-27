import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.*;

public class GoldLoanSystem extends JFrame implements ActionListener {

    // ==========================================
    // USER STORAGE
    // ==========================================

    static HashMap<String,String> users =
            new HashMap<>();

    static HashMap<String,String> names =
            new HashMap<>();

    static String currentUser = "";

    static ArrayList<String> loanApplications =
            new ArrayList<>();

    // ==========================================
    // LOGIN COMPONENTS
    // ==========================================

    JTextField usernameField;

    JPasswordField passwordField;

    JButton loginButton;

    JButton registerButton;

    // ==========================================
    // MAIN CONSTRUCTOR
    // ==========================================

    public GoldLoanSystem() {

        loadUsers();

        setTitle("Gold Loan Management System");

        setSize(500,400);

        setLayout(null);

        setLocationRelativeTo(null);

        setDefaultCloseOperation(EXIT_ON_CLOSE);

        JLabel title =
                new JLabel("GOLD LOAN SYSTEM");

        title.setFont(
                new Font(
                        "Arial",
                        Font.BOLD,
                        28
                )
        );

        title.setBounds(
                70,
                30,
                350,
                40
        );

        JLabel userLabel =
                new JLabel("Username");

        userLabel.setBounds(
                70,
                120,
                100,
                30
        );

        JLabel passLabel =
                new JLabel("Password");

        passLabel.setBounds(
                70,
                180,
                100,
                30
        );

        usernameField =
                new JTextField();

        usernameField.setBounds(
                180,
                120,
                180,
                30
        );

        passwordField =
                new JPasswordField();

        passwordField.setBounds(
                180,
                180,
                180,
                30
        );

        loginButton =
                new JButton("LOGIN");

        loginButton.setBounds(
                80,
                280,
                130,
                40
        );

        registerButton =
                new JButton("REGISTER");

        registerButton.setBounds(
                240,
                280,
                130,
                40
        );

        loginButton.addActionListener(this);

        registerButton.addActionListener(this);

        add(title);

        add(userLabel);

        add(passLabel);

        add(usernameField);

        add(passwordField);

        add(loginButton);

        add(registerButton);

        setVisible(true);
    }

    // ==========================================
    // LOAD USERS
    // ==========================================

    static void loadUsers() {

        try {

            File file =
                    new File("users.txt");

            if(!file.exists()) {

                file.createNewFile();
            }

            BufferedReader br =
                    new BufferedReader(
                            new FileReader(file)
                    );

            String line;

            while((line = br.readLine()) != null) {

                String[] data =
                        line.split(",");

                if(data.length == 3) {

                    names.put(
                            data[1],
                            data[0]
                    );

                    users.put(
                            data[1],
                            data[2]
                    );
                }
            }

            br.close();

        } catch(Exception e) {

            e.printStackTrace();
        }
    }

    // ==========================================
    // SAVE USERS
    // ==========================================

    static void saveUser(
            String name,
            String username,
            String password
    ) {

        try {

            FileWriter fw =
                    new FileWriter(
                            "users.txt",
                            true
                    );

            fw.write(
                    name
                            + ","
                            + username
                            + ","
                            + password
                            + "\n"
            );

            fw.close();

        } catch(Exception e) {

            e.printStackTrace();
        }
    }

    // ==========================================
    // SAVE LOAN
    // ==========================================

    static void saveLoan(String data) {

        try {

            FileWriter fw =
                    new FileWriter(
                            "loans.txt",
                            true
                    );

            fw.write(data + "\n");

            fw.close();

        } catch(Exception e) {

            e.printStackTrace();
        }
    }

    // ==========================================
    // BUTTON EVENTS
    // ==========================================

    public void actionPerformed(
            ActionEvent e
    ) {

        if(e.getSource()
                == registerButton) {

            new RegisterFrame();
        }

        if(e.getSource()
                == loginButton) {

            String username =
                    usernameField.getText();

            String password =
                    passwordField.getText();

            // ==================================
            // ADMIN LOGIN
            // ==================================

            if(username.equals("admin")
                    &&
                    password.equals("admin123")) {

                JOptionPane.showMessageDialog(
                        this,
                        "Admin Login Successful"
                );

                new AdminDashboard();

                dispose();

                return;
            }

            // ==================================
            // CUSTOMER LOGIN
            // ==================================

            if(users.containsKey(username)) {

                if(users.get(username)
                        .equals(password)) {

                    currentUser =
                            username;

                    JOptionPane.showMessageDialog(
                            this,
                            "Welcome "
                                    + names.get(username)
                    );

                    new Dashboard();

                    dispose();

                } else {

                    JOptionPane.showMessageDialog(
                            this,
                            "Wrong Password"
                    );
                }

            } else {

                JOptionPane.showMessageDialog(
                        this,
                        "User Not Found"
                );
            }
        }
    }

    // ==========================================
    // REGISTER FRAME
    // ==========================================

    class RegisterFrame extends JFrame
            implements ActionListener {

        JTextField nameField;

        JTextField userField;

        JPasswordField passField;

        JButton createButton;

        RegisterFrame() {

            setTitle("Register Customer");

            setSize(450,400);

            setLayout(null);

            setLocationRelativeTo(null);

            JLabel title =
                    new JLabel(
                            "REGISTER CUSTOMER"
                    );

            title.setFont(
                    new Font(
                            "Arial",
                            Font.BOLD,
                            24
                    )
            );

            title.setBounds(
                    70,
                    30,
                    300,
                    40
            );

            JLabel name =
                    new JLabel("Name");

            name.setBounds(
                    50,
                    100,
                    100,
                    30
            );

            JLabel user =
                    new JLabel("Username");

            user.setBounds(
                    50,
                    160,
                    100,
                    30
            );

            JLabel pass =
                    new JLabel("Password");

            pass.setBounds(
                    50,
                    220,
                    100,
                    30
            );

            nameField =
                    new JTextField();

            nameField.setBounds(
                    170,
                    100,
                    180,
                    30
            );

            userField =
                    new JTextField();

            userField.setBounds(
                    170,
                    160,
                    180,
                    30
            );

            passField =
                    new JPasswordField();

            passField.setBounds(
                    170,
                    220,
                    180,
                    30
            );

            createButton =
                    new JButton(
                            "CREATE ACCOUNT"
                    );

            createButton.setBounds(
                    120,
                    300,
                    180,
                    40
            );

            createButton
                    .addActionListener(this);

            add(title);

            add(name);

            add(user);

            add(pass);

            add(nameField);

            add(userField);

            add(passField);

            add(createButton);

            setVisible(true);
        }

        public void actionPerformed(
                ActionEvent e
        ) {

            String name =
                    nameField.getText();

            String username =
                    userField.getText();

            String password =
                    passField.getText();

            if(name.isEmpty()
                    ||
                    username.isEmpty()
                    ||
                    password.isEmpty()) {

                JOptionPane.showMessageDialog(
                        this,
                        "Fill All Fields"
                );

                return;
            }

            if(users.containsKey(username)) {

                JOptionPane.showMessageDialog(
                        this,
                        "Username Already Exists"
                );

                return;
            }

            users.put(
                    username,
                    password
            );

            names.put(
                    username,
                    name
            );

            saveUser(
                    name,
                    username,
                    password
            );

            JOptionPane.showMessageDialog(
                    this,
                    "Registration Successful"
            );

            dispose();
        }
    }

    // ==========================================
    // CUSTOMER DASHBOARD
    // ==========================================

    class Dashboard extends JFrame
            implements ActionListener {

        JButton profileButton;

        JButton emiButton;

        JButton goldButton;

        JButton applyLoanButton;

        JButton payLoanButton;

        JButton logoutButton;

        Dashboard() {

            setTitle("Customer Dashboard");

            setSize(850,550);

            setLayout(null);

            setLocationRelativeTo(null);

            JLabel title =
                    new JLabel(
                            "WELCOME "
                                    + names.get(currentUser)
                    );

            title.setFont(
                    new Font(
                            "Arial",
                            Font.BOLD,
                            28
                    )
            );

            title.setBounds(
                    180,
                    40,
                    450,
                    40
            );

            profileButton =
                    new JButton("PROFILE");

            profileButton.setBounds(
                    40,
                    180,
                    140,
                    50
            );

            emiButton =
                    new JButton("CHECK EMI");

            emiButton.setBounds(
                    210,
                    180,
                    140,
                    50
            );

            goldButton =
                    new JButton("GOLD RATE");

            goldButton.setBounds(
                    380,
                    180,
                    140,
                    50
            );

            applyLoanButton =
                    new JButton("APPLY LOAN");

            applyLoanButton.setBounds(
                    550,
                    180,
                    180,
                    50
            );

            payLoanButton =
                    new JButton("PAY EMI");

            payLoanButton.setBounds(
                    220,
                    320,
                    180,
                    50
            );

            logoutButton =
                    new JButton("LOGOUT");

            logoutButton.setBounds(
                    450,
                    320,
                    180,
                    50
            );

            profileButton.addActionListener(this);

            emiButton.addActionListener(this);

            goldButton.addActionListener(this);

            applyLoanButton.addActionListener(this);

            payLoanButton.addActionListener(this);

            logoutButton.addActionListener(this);

            add(title);

            add(profileButton);

            add(emiButton);

            add(goldButton);

            add(applyLoanButton);

            add(payLoanButton);

            add(logoutButton);

            setVisible(true);
        }

        public void actionPerformed(
                ActionEvent e
        ) {

            // ==================================
            // PROFILE
            // ==================================

            if(e.getSource()
                    == profileButton) {

                JOptionPane.showMessageDialog(
                        this,
                        "NAME : "
                                + names.get(currentUser)
                                + "\nUSERNAME : "
                                + currentUser
                );
            }

            // ==================================
            // EMI
            // ==================================

            if(e.getSource()
                    == emiButton) {

                double principal =
                        200000;

                double annualRate =
                        10;

                int months =
                        12;

                double monthlyRate =
                        annualRate
                                / 12
                                / 100;

                double emi =
                        (
                                principal
                                        * monthlyRate
                                        * Math.pow(
                                        1 + monthlyRate,
                                        months
                                )
                        )
                                /
                                (
                                        Math.pow(
                                                1 + monthlyRate,
                                                months
                                        ) - 1
                                );

                JOptionPane.showMessageDialog(
                        this,
                        "Monthly EMI = ₹"
                                + Math.round(emi)
                );
            }

            // ==================================
            // GOLD RATE
            // ==================================

            if(e.getSource()
                    == goldButton) {

                Random random =
                        new Random();

                int rate =
                        7000
                                + random.nextInt(600);

                JOptionPane.showMessageDialog(
                        this,
                        "Today's Gold Rate = ₹"
                                + rate
                                + " / gram"
                );
            }

            // ==================================
            // APPLY LOAN
            // ==================================

            if(e.getSource()
                    == applyLoanButton) {

                String weight =
                        JOptionPane.showInputDialog(
                                this,
                                "Enter Gold Weight (grams)"
                        );

                try {

                    double goldWeight =
                            Double.parseDouble(weight);

                    Random random =
                            new Random();

                    int goldRate =
                            7000
                                    + random.nextInt(500);

                    double eligibleLoan =
                            goldWeight
                                    * goldRate
                                    * 0.75;

                    String application =
                            "CUSTOMER="
                                    + currentUser
                                    + ",NAME="
                                    + names.get(currentUser)
                                    + ",WEIGHT="
                                    + goldWeight
                                    + " grams"
                                    + ",RATE="
                                    + goldRate
                                    + ",LOAN="
                                    + Math.round(eligibleLoan)
                                    + ",STATUS=PENDING";

                    loanApplications.add(application);

                    saveLoan(application);

                    JOptionPane.showMessageDialog(
                            this,
                            "Loan Applied Successfully\n"
                                    + "Eligible Loan = ₹"
                                    + Math.round(eligibleLoan)
                    );

                } catch(Exception ex) {

                    JOptionPane.showMessageDialog(
                            this,
                            "Invalid Weight"
                    );
                }
            }

            // ==================================
            // PAY EMI
            // ==================================

            if(e.getSource()
                    == payLoanButton) {

                String amount =
                        JOptionPane.showInputDialog(
                                this,
                                "Enter EMI Amount"
                        );

                try {

                    double emiAmount =
                            Double.parseDouble(amount);

                    FileWriter fw =
                            new FileWriter(
                                    "payments.txt",
                                    true
                            );

                    fw.write(
                            "CUSTOMER="
                                    + currentUser
                                    + ",NAME="
                                    + names.get(currentUser)
                                    + ",PAID="
                                    + emiAmount
                                    + ",DATE="
                                    + new Date()
                                    + "\n"
                    );

                    fw.close();

                    JOptionPane.showMessageDialog(
                            this,
                            "Payment Successful\n"
                                    + "Paid ₹"
                                    + emiAmount
                    );

                } catch(Exception ex) {

                    JOptionPane.showMessageDialog(
                            this,
                            "Invalid Amount"
                    );
                }
            }

            // ==================================
            // LOGOUT
            // ==================================

            if(e.getSource()
                    == logoutButton) {

                dispose();

                new GoldLoanSystem();
            }
        }
    }

    // ==========================================
    // ADMIN DASHBOARD
    // ==========================================

    class AdminDashboard extends JFrame
            implements ActionListener {

        JTextArea area;

        JButton usersButton;

        JButton loansButton;

        JButton paymentsButton;

        JButton approveButton;

        JButton logoutButton;

        AdminDashboard() {

            setTitle("Admin Dashboard");

            setSize(900,650);

            setLayout(null);

            setLocationRelativeTo(null);

            JLabel title =
                    new JLabel("ADMIN PANEL");

            title.setFont(
                    new Font(
                            "Arial",
                            Font.BOLD,
                            30
                    )
            );

            title.setBounds(
                    300,
                    20,
                    300,
                    40
            );

            area =
                    new JTextArea();

            JScrollPane pane =
                    new JScrollPane(area);

            pane.setBounds(
                    40,
                    90,
                    790,
                    360
            );

            usersButton =
                    new JButton("VIEW USERS");

            usersButton.setBounds(
                    20,
                    520,
                    170,
                    40
            );

            paymentsButton =
                    new JButton("VIEW PAYMENTS");

            paymentsButton.setBounds(
                    220,
                    520,
                    180,
                    40
            );

            loansButton =
                    new JButton("VIEW LOANS");

            loansButton.setBounds(
                    430,
                    520,
                    170,
                    40
            );

            approveButton =
                    new JButton("APPROVE LOAN");

            approveButton.setBounds(
                    630,
                    520,
                    180,
                    40
            );

            logoutButton =
                    new JButton("LOGOUT");

            logoutButton.setBounds(
                    340,
                    570,
                    180,
                    40
            );

            usersButton.addActionListener(this);

            paymentsButton.addActionListener(this);

            loansButton.addActionListener(this);

            approveButton.addActionListener(this);

            logoutButton.addActionListener(this);

            add(title);

            add(pane);

            add(usersButton);

            add(paymentsButton);

            add(loansButton);

            add(approveButton);

            add(logoutButton);

            setVisible(true);
        }

        void loadUsersData() {

            try {

                area.setText("");

                File file =
                        new File("users.txt");

                BufferedReader br =
                        new BufferedReader(
                                new FileReader(file)
                        );

                String line;

                while((line = br.readLine()) != null) {

                    String[] data =
                            line.split(",");

                    area.append(
                            "NAME : "
                                    + data[0]
                                    + "\n"
                    );

                    area.append(
                            "USERNAME : "
                                    + data[1]
                                    + "\n"
                    );

                    area.append(
                            "PASSWORD : "
                                    + data[2]
                                    + "\n"
                    );

                    area.append(
                            "-----------------------------------\n"
                    );
                }

                br.close();

            } catch(Exception e) {

                e.printStackTrace();
            }
        }

        void loadLoans() {

            try {

                area.setText("");

                File file =
                        new File("loans.txt");

                if(!file.exists()) {

                    file.createNewFile();
                }

                BufferedReader br =
                        new BufferedReader(
                                new FileReader(file)
                        );

                String line;

                while((line = br.readLine()) != null) {

                    area.append(
                            line
                                    + "\n\n"
                    );
                }

                br.close();

            } catch(Exception e) {

                e.printStackTrace();
            }
        }

        void loadPayments() {

            try {

                area.setText("");

                File file =
                        new File("payments.txt");

                if(!file.exists()) {

                    file.createNewFile();
                }

                BufferedReader br =
                        new BufferedReader(
                                new FileReader(file)
                        );

                String line;

                while((line = br.readLine()) != null) {

                    area.append(
                            line
                                    + "\n\n"
                    );
                }

                br.close();

            } catch(Exception e) {

                e.printStackTrace();
            }
        }

        void approveLoan(String username) {

            try {

                File inputFile =
                        new File("loans.txt");

                File tempFile =
                        new File("temp.txt");

                BufferedReader reader =
                        new BufferedReader(
                                new FileReader(inputFile)
                        );

                BufferedWriter writer =
                        new BufferedWriter(
                                new FileWriter(tempFile)
                        );

                String line;

                while((line = reader.readLine()) != null) {

                    if(line.contains(
                            "CUSTOMER="
                                    + username
                    )) {

                        line =
                                line.replace(
                                        "STATUS=PENDING",
                                        "STATUS=APPROVED"
                                );
                    }

                    writer.write(line);

                    writer.newLine();
                }

                writer.close();

                reader.close();

                inputFile.delete();

                tempFile.renameTo(inputFile);

                JOptionPane.showMessageDialog(
                        this,
                        "Loan Approved"
                );

                loadLoans();

            } catch(Exception e) {

                e.printStackTrace();
            }
        }

        public void actionPerformed(
                ActionEvent e
        ) {

            if(e.getSource()
                    == usersButton) {

                loadUsersData();
            }

            if(e.getSource()
                    == paymentsButton) {

                loadPayments();
            }

            if(e.getSource()
                    == loansButton) {

                loadLoans();
            }

            if(e.getSource()
                    == approveButton) {

                String username =
                        JOptionPane.showInputDialog(
                                this,
                                "Enter Username"
                        );

                approveLoan(username);
            }

            if(e.getSource()
                    == logoutButton) {

                dispose();

                new GoldLoanSystem();
            }
        }
    }

    // ==========================================
    // MAIN
    // ==========================================

    public static void main(
            String[] args
    ) {

        SwingUtilities.invokeLater(
                () -> {

                    new GoldLoanSystem();
                }
        );
    }
}
