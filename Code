import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.Dimension;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.Stack;

import javax.swing.*;

class Calculator extends JFrame implements ActionListener {

    JButton button1, button2, button3, button4, button5, button6, button7, button8, button9, button10;
    JButton[] buttons = new JButton[10];
    JTextField field;
    JPanel buttonpanel;
    String exp = "";

    Calculator() {
        this.setLayout(new BorderLayout());

        // create a textfield
        field = new JTextField();
        field.setPreferredSize(new Dimension(200, 50));
        field.setFont(new Font("Aria", Font.BOLD, 20));
        field.setBackground(Color.lightGray);
        field.setEditable(false); // prevent from manual input
        this.add(field, BorderLayout.NORTH); // sets the textfield at the top

        // create buttons
        for (int i = 0; i <= 9; i++) {
            buttons[i] = new JButton(String.valueOf(i));
            buttons[i].setFont(new Font("Asian", Font.BOLD, 30));
            buttons[i].addActionListener(this);
        }
        button1 = new JButton("+");
        button2 = new JButton("-");
        button3 = new JButton("*");
        button4 = new JButton("/");
        button5 = new JButton("=");
        button6 = new JButton("AC");
        button7 = new JButton("^");
        button8 = new JButton(".");
        button9 = new JButton("%");
        button10 = new JButton("⌫");

        button1.setFont(new Font("Asian", Font.BOLD, 30));
        button2.setFont(new Font("Asian", Font.BOLD, 30));
        button3.setFont(new Font("Asian", Font.BOLD, 30));
        button4.setFont(new Font("Asian", Font.BOLD, 30));
        button5.setFont(new Font("Asian", Font.BOLD, 30));
        button6.setFont(new Font("Asian", Font.BOLD, 30));
        button7.setFont(new Font("Asian", Font.BOLD, 30));
        button8.setFont(new Font("Asian", Font.BOLD, 30));
        button9.setFont(new Font("Asian", Font.BOLD, 30));
        button10.setFont(new Font("Asian", Font.BOLD, 30));

        button1.addActionListener(this);
        button2.addActionListener(this);
        button3.addActionListener(this);
        button4.addActionListener(this);
        button5.addActionListener(this);
        button6.addActionListener(this);
        button7.addActionListener(this);
        button8.addActionListener(this);
        button9.addActionListener(this);
        button10.addActionListener(this);

        // create panel
        buttonpanel = new JPanel();
        buttonpanel.setLayout(new GridLayout(5, 4, 5, 5)); // sets the panel in the grid format
        buttonpanel.setBackground(Color.RED);

        // add buttons on panel
        buttonpanel.add(button7);
        buttonpanel.add(button8);
        buttonpanel.add(button9);
        buttonpanel.add(button10);

        buttonpanel.add(buttons[7]);
        buttonpanel.add(buttons[8]);
        buttonpanel.add(buttons[9]);
        buttonpanel.add(button4);

        buttonpanel.add(buttons[4]);
        buttonpanel.add(buttons[5]);
        buttonpanel.add(buttons[6]);
        buttonpanel.add(button3);

        buttonpanel.add(buttons[1]);
        buttonpanel.add(buttons[2]);
        buttonpanel.add(buttons[3]);
        buttonpanel.add(button2);

        buttonpanel.add(button6);
        buttonpanel.add(buttons[0]);
        buttonpanel.add(button5);
        buttonpanel.add(button1);

        // frame setting
        this.add(buttonpanel, BorderLayout.CENTER); // add panel to the center
        this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        this.setSize(500, 500);
        this.setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        Object source = e.getSource();

        // add number in the textfield
        for (int i = 0; i <= 9; i++) {
            if (source == buttons[i]) {
                exp += i;
                field.setText(exp);
                return;
            }
        }
        if (source == button1)
            exp += "+";
        else if (source == button2)
            exp += "-";
        else if (source == button3)
            exp += "*";
        else if (source == button4)
            exp += "/";
        else if (source == button5) { // calculate expression result
            evaluatexp();
            return;
        } else if (source == button6) { // clear all input
            exp = "";
            field.setText("");
            return;
        } else if (source == button7)
            exp += "^";
        else if (source == button8)
            exp += ".";
        else if (source == button9)
            exp += "%";
        else if (source == button10) { // Delete last character
            if (!exp.isEmpty()) {
                exp = exp.substring(0, exp.length() - 1);
                field.setText(exp);
            }
            return;
        }

        field.setText(exp);

    }

    private double evaluatexp() {
        try {
            double result = evaluate(exp);
            exp = Double.toString(result); // Store result for further calculations
            field.setText(exp); // Display result
            return result;
        } catch (Exception e) {
            field.setText("Error");
            exp = "";
            return 0;
        }
    }

    // Manual expression evaluation method (Handles +, -, *, /)
    private double evaluate(String expression) {
        Stack<Double> numbers = new Stack<>();
        Stack<Character> operators = new Stack<>();

        for (int i = 0; i < expression.length(); i++) {
            char c = expression.charAt(i);

            if (Character.isDigit(c)) {
                StringBuilder sb = new StringBuilder();
                while (i < exp.length()
                        && (Character.isDigit(expression.charAt(i)) || expression.charAt(i) == '.')) {
                    sb.append(expression.charAt(i));
                    i++;
                }
                i--;
                numbers.push(Double.parseDouble(sb.toString()));
            } else if (c == '+' || c == '-' || c == '*' || c == '/' || c == '^' || c == '%') {
                while (!operators.isEmpty() && precedence(c, operators.peek())) {
                    numbers.push(applyOp(operators.pop(), numbers.pop(), numbers.pop()));
                }
                operators.push(c);
            }
        }

        while (!operators.isEmpty()) {
            numbers.push(applyOp(operators.pop(), numbers.pop(), numbers.pop()));
        }

        return numbers.pop();
    }

    // Operator precedence
    private boolean precedence(char op1, char op2) {
        if ((op1 == '*' || op1 == '/') && (op2 == '+' || op2 == '-' || op2 == '^' || op2 == '%'))
            return false;
        return true;
    }

    // Apply operator on two numbers
    private double applyOp(char op, double b, double a) {
        switch (op) {
            case '+':
                return a + b;
            case '-':
                return a - b;
            case '*':
                return a * b;
            case '/':
                return a / b;
            case '^':
                return Math.pow(a, b);
            case '%':
                return (a / 100) * b;
        }
        return 0;
    }

}

public class CalculatorApp {
    public static void main(String[] args) {
        new Calculator();
    }

}
