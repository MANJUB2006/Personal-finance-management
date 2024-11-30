import java.awt.*;
import java.awt.event.*;

public class PersonalFinanceManagement extends Frame implements ActionListener {
    // Labels and TextFields for input
    Label lblIncome, lblExpense, lblInvestment, lblHouseLoan, lblVehicleLoan, lblSavings, lblResult;
    TextField txtIncome, txtExpense, txtInvestment, txtHouseLoan, txtVehicleLoan;
    Button btnCalculate, btnClear, btnExit;

    // Constructor for setting up GUI
    public PersonalFinanceManagement() {
        setTitle("Personal Finance Management System");
        setSize(500, 500);
        setLayout(new BorderLayout(10, 10)); // BorderLayout for better organization

        // Panel for inputs
        Panel inputPanel = new Panel();
        inputPanel.setLayout(new GridLayout(5, 2, 10, 10)); // GridLayout for structured inputs

        // Income Section
        lblIncome = new Label("Total Monthly Income:");
        txtIncome = new TextField();
        inputPanel.add(lblIncome);
        inputPanel.add(txtIncome);

        // Expense Section
        lblExpense = new Label("Total Monthly Expenses:");
        txtExpense = new TextField();
        inputPanel.add(lblExpense);
        inputPanel.add(txtExpense);

        // Investment Section
        lblInvestment = new Label("Total Monthly Investments:");
        txtInvestment = new TextField();
        inputPanel.add(lblInvestment);
        inputPanel.add(txtInvestment);

        // House Loan Section
        lblHouseLoan = new Label("Monthly House Loan Payment:");
        txtHouseLoan = new TextField();
        inputPanel.add(lblHouseLoan);
        inputPanel.add(txtHouseLoan);

        // Vehicle Loan Section
        lblVehicleLoan = new Label("Monthly Vehicle Loan Payment:");
        txtVehicleLoan = new TextField();
        inputPanel.add(lblVehicleLoan);
        inputPanel.add(txtVehicleLoan);

        add(inputPanel, BorderLayout.CENTER);

        // Panel for Buttons
        Panel buttonPanel = new Panel();
        buttonPanel.setLayout(new FlowLayout(FlowLayout.CENTER, 20, 10)); // FlowLayout for centered buttons

        btnCalculate = new Button("Calculate Savings");
        btnClear = new Button("Clear");
        btnExit = new Button("Exit");

        buttonPanel.add(btnCalculate);
        buttonPanel.add(btnClear);
        buttonPanel.add(btnExit);

        add(buttonPanel, BorderLayout.SOUTH);

        // Panel for Output
        Panel outputPanel = new Panel();
        outputPanel.setLayout(new GridLayout(2, 1)); // Vertical layout for labels

        lblSavings = new Label("Remaining Savings:");
        lblResult = new Label("", Label.CENTER); // Center-aligned result
        lblResult.setFont(new Font("Arial", Font.BOLD, 14)); // Bold result text for emphasis

        outputPanel.add(lblSavings);
        outputPanel.add(lblResult);

        add(outputPanel, BorderLayout.NORTH);

        // Adding Action Listeners
        btnCalculate.addActionListener(this);
        btnClear.addActionListener(this);
        btnExit.addActionListener(this);

        // Adding Window Listener for Closing the App
        addWindowListener(new WindowAdapter() {
            public void windowClosing(WindowEvent e) {
                System.exit(0);
            }
        });

        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == btnCalculate) {
            try {
                // Parse inputs
                double income = Double.parseDouble(txtIncome.getText());
                double expense = Double.parseDouble(txtExpense.getText());
                double investment = Double.parseDouble(txtInvestment.getText());
                double houseLoan = Double.parseDouble(txtHouseLoan.getText());
                double vehicleLoan = Double.parseDouble(txtVehicleLoan.getText());

                // Calculate savings
                double totalExpenses = expense + investment + houseLoan + vehicleLoan;
                double savings = income - totalExpenses;

                // Display result
                if (savings < 0) {
                    lblResult.setText("Warning: Deficit! Savings: " + savings);
                    lblResult.setForeground(Color.RED);
                } else {
                    lblResult.setText("Savings: " + savings);
                    lblResult.setForeground(Color.BLUE);
                }
            } catch (NumberFormatException ex) {
                lblResult.setText("Error: Please enter valid numbers.");
                lblResult.setForeground(Color.RED);
            }
        } else if (e.getSource() == btnClear) {
            // Clear all inputs and results
            txtIncome.setText("");
            txtExpense.setText("");
            txtInvestment.setText("");
            txtHouseLoan.setText("");
            txtVehicleLoan.setText("");
            lblResult.setText("");
        } else if (e.getSource() == btnExit) {
            // Exit the application
            System.exit(0);
        }
    }

    public static void main(String[] args) {
        new PersonalFinanceManagement();
    }
}
