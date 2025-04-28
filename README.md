
#jaaaaaaa
// 1) Simple Login Screen
import javax.swing.*;
import java.awt.*;

public class SimpleLogin {
    public static void main(String[] args) {
        // Create the main window
        JFrame frame = new JFrame("Login");
        frame.setSize(250, 150);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new FlowLayout());
        
        // Create components
        JLabel userLabel = new JLabel("Username:");
        JTextField userField = new JTextField(15);
        
        JLabel passLabel = new JLabel("Password:");
        JPasswordField passField = new JPasswordField(15);
        
        JButton loginButton = new JButton("Login");
        JLabel resultLabel = new JLabel("");
        
        // Add action to button
        loginButton.addActionListener(e -> {
            String username = userField.getText();
            String password = new String(passField.getPassword());
            
            if (username.equals("admin") && password.equals("password")) {
                resultLabel.setText("Login successful");
                resultLabel.setForeground(Color.GREEN);
            } else {
                resultLabel.setText("Incorrect username or password");
                resultLabel.setForeground(Color.RED);
            }
        });
        
        // Add components to frame
        frame.add(userLabel);
        frame.add(userField);
        frame.add(passLabel);
        frame.add(passField);
        frame.add(loginButton);
        frame.add(resultLabel);
        
        // Display the window
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}

// 2) Simple Hospital Management
import javax.swing.*;
import java.awt.*;

public class SimpleHospital {
    public static void main(String[] args) {
        // Create main window
        JFrame frame = new JFrame("Hospital Management");
        frame.setSize(400, 300);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());
        
        // Form panel
        JPanel formPanel = new JPanel(new FlowLayout());
        
        JLabel nameLabel = new JLabel("Name:");
        JTextField nameField = new JTextField(10);
        
        JLabel ageLabel = new JLabel("Age:");
        JTextField ageField = new JTextField(3);
        
        JLabel conditionLabel = new JLabel("Condition:");
        String[] conditions = {"Stable", "Critical", "Recovering"};
        JComboBox<String> conditionBox = new JComboBox<>(conditions);
        
        JButton addButton = new JButton("Add Patient");
        
        formPanel.add(nameLabel);
        formPanel.add(nameField);
        formPanel.add(ageLabel);
        formPanel.add(ageField);
        formPanel.add(conditionLabel);
        formPanel.add(conditionBox);
        formPanel.add(addButton);
        
        // Patient list area
        JTextArea patientList = new JTextArea();
        patientList.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(patientList);
        
        // Add action to button
        addButton.addActionListener(e -> {
            try {
                String name = nameField.getText();
                int age = Integer.parseInt(ageField.getText());
                String condition = (String) conditionBox.getSelectedItem();
                
                patientList.append(name + ", " + age + ", " + condition + "\n");
                
                nameField.setText("");
                ageField.setText("");
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(frame, "Please enter a valid age");
            }
        });
        
        // Add panels to frame
        frame.add(formPanel, BorderLayout.NORTH);
        frame.add(scrollPane, BorderLayout.CENTER);
        
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}

// 3) Simple Chat Application
import javax.swing.*;
import java.awt.*;
import javax.swing.*;

public class SimpleChat {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Chat App");
        JTextArea chatArea = new JTextArea(); 
        chatArea.setEditable(false);
        JTextField messageField = new JTextField();
        JButton sendButton = new JButton("Send");

        sendButton.addActionListener(e -> {
            String msg = messageField.getText().trim();
            if (!msg.isEmpty()) {
                chatArea.append("You: " + msg + "\n");
                messageField.setText("");
                // Predefined bot reply
                chatArea.append("Bot: " + getReply(msg) + "\n");
            }
        });

        messageField.addActionListener(e -> sendButton.doClick());

        JPanel inputPanel = new JPanel(new java.awt.BorderLayout());
        inputPanel.add(messageField, "Center");
        inputPanel.add(sendButton, "East");

        frame.add(new JScrollPane(chatArea), "Center");
        frame.add(inputPanel, "South");
        frame.setSize(300, 400);
        frame.setDefaultCloseOperation(3);
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }

    static String getReply(String userMessage) {
        // Simple predefined responses
        if (userMessage.toLowerCase().contains("hello")) return "Hi there!";
        if (userMessage.toLowerCase().contains("how are you")) return "I'm just a bot, but I'm good!";
        if (userMessage.toLowerCase().contains("bye")) return "Goodbye! See you soon.";
        return "I don't understand.";
    }
}


// 4) Simple Calculator
import javax.swing.*;
import java.awt.*;

public class SimpleCalculator {
    public static void main(String[] args) {
        // Create main window
        JFrame frame = new JFrame("Calculator");
        frame.setSize(250, 300);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());
        
        // Result display
        JTextField display = new JTextField("0");
        display.setHorizontalAlignment(JTextField.RIGHT);
        display.setEditable(false);
        
        // Button panel
        JPanel buttonPanel = new JPanel(new GridLayout(4, 4, 5, 5));
        
        // Calculator variables
        double[] number = {0};  // Using array to make it accessible in lambda
        String[] operator = {""};
        boolean[] startNewNumber = {true};
        
        // Create number buttons
        for (int i = 1; i <= 9; i++) {
            final int digit = i;
            JButton button = new JButton(String.valueOf(i));
            button.addActionListener(e -> {
                if (startNewNumber[0]) {
                    display.setText(String.valueOf(digit));
                    startNewNumber[0] = false;
                } else {
                    display.setText(display.getText() + digit);
                }
            });
            buttonPanel.add(button);
        }
        
        // Create operator buttons
        String[] operators = {"+", "-", "*", "/"};
        for (String op : operators) {
            JButton button = new JButton(op);
            button.addActionListener(e -> {
                number[0] = Double.parseDouble(display.getText());
                operator[0] = op;
                startNewNumber[0] = true;
            });
            buttonPanel.add(button);
        }
        
        // Zero button
        JButton zeroButton = new JButton("0");
        zeroButton.addActionListener(e -> {
            if (startNewNumber[0]) {
                display.setText("0");
                startNewNumber[0] = false;
            } else {
                display.setText(display.getText() + "0");
            }
        });
        
        // Clear button
        JButton clearButton = new JButton("C");
        clearButton.addActionListener(e -> {
            display.setText("0");
            number[0] = 0;
            operator[0] = "";
            startNewNumber[0] = true;
        });
        
        // Equal button
        JButton equalButton = new JButton("=");
        equalButton.addActionListener(e -> {
            double secondNumber = Double.parseDouble(display.getText());
            double result = 0;
            
            switch (operator[0]) {
                case "+": result = number[0] + secondNumber; break;
                case "-": result = number[0] - secondNumber; break;
                case "*": result = number[0] * secondNumber; break;
                case "/": result = secondNumber != 0 ? number[0] / secondNumber : 0; break;
            }
            
            display.setText(String.valueOf(result));
            startNewNumber[0] = true;
        });
        
        // Add remaining buttons
        buttonPanel.add(zeroButton);
        buttonPanel.add(clearButton);
        buttonPanel.add(equalButton);
        
        // Add components to frame
        frame.add(display, BorderLayout.NORTH);
        frame.add(buttonPanel, BorderLayout.CENTER);
        
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}

// 5) Simple Voting Application
import javax.swing.*;
import java.awt.*;
import java.util.HashMap;
import java.util.Map;

public class SimpleVoting {
    public static void main(String[] args) {
        // Create main window
        JFrame frame = new JFrame("Voting App");
        frame.setSize(300, 250);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout());
        
        // Create components
        JPanel votingPanel = new JPanel(new GridLayout(0, 1));
        
        JLabel titleLabel = new JLabel("Select a candidate:");
        votingPanel.add(titleLabel);
        
        // Initialize candidates and votes
        Map<String, Integer> votes = new HashMap<>();
        votes.put("Candidate A", 0);
        votes.put("Candidate B", 0);
        votes.put("Candidate C", 0);
        
        // Create radio buttons
        ButtonGroup group = new ButtonGroup();
        Map<String, JRadioButton> radioButtons = new HashMap<>();
        
        for (String candidate : votes.keySet()) {
            JRadioButton button = new JRadioButton(candidate);
            radioButtons.put(candidate, button);
            group.add(button);
            votingPanel.add(button);
        }
        
        // Vote button
        JButton voteButton = new JButton("Vote");
        votingPanel.add(voteButton);
        
        // Results area
        JTextArea resultsArea = new JTextArea();
        resultsArea.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(resultsArea);
        
        // Update results function
        Runnable updateResults = () -> {
            resultsArea.setText("Results:\n");
            for (Map.Entry<String, Integer> entry : votes.entrySet()) {
                resultsArea.append(entry.getKey() + ": " + entry.getValue() + " votes\n");
            }
        };
        
        // Initial results display
        updateResults.run();
        
        // Add action to vote button
        voteButton.addActionListener(e -> {
            boolean voted = false;
            
            for (Map.Entry<String, JRadioButton> entry : radioButtons.entrySet()) {
                if (entry.getValue().isSelected()) {
                    String candidate = entry.getKey();
                    votes.put(candidate, votes.get(candidate) + 1);
                    voted = true;
                    break;
                }
            }
            
            if (voted) {
                group.clearSelection();
                updateResults.run();
                JOptionPane.showMessageDialog(frame, "Vote recorded!");
            } else {
                JOptionPane.showMessageDialog(frame, "Please select a candidate");
            }
        });
        
        // Add panels to frame
        frame.add(votingPanel, BorderLayout.NORTH);
        frame.add(scrollPane, BorderLayout.CENTER);
        
        frame.setLocationRelativeTo(null);
        frame.setVisible(true);
    }
}
