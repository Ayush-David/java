# java
// 1) Login Screen Creation
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class LoginScreen extends JFrame {
    private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton loginButton;
    private JLabel messageLabel;

    public LoginScreen() {
        setTitle("Login Screen");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(4, 1, 10, 10));
        panel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        
        // Username field
        JPanel usernamePanel = new JPanel(new BorderLayout());
        usernamePanel.add(new JLabel("Username: "), BorderLayout.WEST);
        usernameField = new JTextField(15);
        usernamePanel.add(usernameField, BorderLayout.CENTER);
        
        // Password field
        JPanel passwordPanel = new JPanel(new BorderLayout());
        passwordPanel.add(new JLabel("Password: "), BorderLayout.WEST);
        passwordField = new JPasswordField(15);
        passwordPanel.add(passwordField, BorderLayout.CENTER);
        
        // Login button
        loginButton = new JButton("Login");
        loginButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                
                if (username.equals("admin") && password.equals("password")) {
                    messageLabel.setText("Login successful!");
                    messageLabel.setForeground(Color.GREEN);
                } else {
                    messageLabel.setText("Invalid username or password!");
                    messageLabel.setForeground(Color.RED);
                }
            }
        });
        
        // Message label
        messageLabel = new JLabel("");
        messageLabel.setHorizontalAlignment(JLabel.CENTER);
        
        panel.add(usernamePanel);
        panel.add(passwordPanel);
        panel.add(loginButton);
        panel.add(messageLabel);
        
        add(panel);
        setVisible(true);
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new LoginScreen();
            }
        });
    }
}

// 2) Hospital Management Application
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

class Patient {
    String name;
    int age;
    String condition;
    
    public Patient(String name, int age, String condition) {
        this.name = name;
        this.age = age;
        this.condition = condition;
    }
}

public class HospitalManagement extends JFrame {
    private ArrayList<Patient> patients = new ArrayList<>();
    private JTextField nameField, ageField;
    private JComboBox<String> conditionCombo;
    private JButton addButton;
    private JTextArea patientList;
    
    public HospitalManagement() {
        setTitle("Hospital Management System");
        setSize(500, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        JPanel mainPanel = new JPanel(new BorderLayout(10, 10));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        
        // Input panel
        JPanel inputPanel = new JPanel(new GridLayout(4, 2, 5, 5));
        inputPanel.setBorder(BorderFactory.createTitledBorder("Add Patient"));
        
        inputPanel.add(new JLabel("Name:"));
        nameField = new JTextField();
        inputPanel.add(nameField);
        
        inputPanel.add(new JLabel("Age:"));
        ageField = new JTextField();
        inputPanel.add(ageField);
        
        inputPanel.add(new JLabel("Condition:"));
        String[] conditions = {"Critical", "Stable", "Recovering"};
        conditionCombo = new JComboBox<>(conditions);
        inputPanel.add(conditionCombo);
        
        addButton = new JButton("Add Patient");
        addButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                try {
                    String name = nameField.getText();
                    int age = Integer.parseInt(ageField.getText());
                    String condition = (String) conditionCombo.getSelectedItem();
                    
                    if (!name.isEmpty()) {
                        patients.add(new Patient(name, age, condition));
                        updatePatientList();
                        
                        // Clear inputs
                        nameField.setText("");
                        ageField.setText("");
                    }
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(null, "Please enter a valid age!");
                }
            }
        });
        inputPanel.add(new JLabel(""));
        inputPanel.add(addButton);
        
        // Patient list panel
        JPanel listPanel = new JPanel(new BorderLayout());
        listPanel.setBorder(BorderFactory.createTitledBorder("Patients List"));
        
        patientList = new JTextArea();
        patientList.setEditable(false);
        JScrollPane scrollPane = new JScrollPane(patientList);
        listPanel.add(scrollPane, BorderLayout.CENTER);
        
        mainPanel.add(inputPanel, BorderLayout.NORTH);
        mainPanel.add(listPanel, BorderLayout.CENTER);
        
        add(mainPanel);
        setVisible(true);
    }
    
    private void updatePatientList() {
        StringBuilder sb = new StringBuilder();
        sb.append(String.format("%-20s %-10s %-15s\n", "Name", "Age", "Condition"));
        sb.append("------------------------------------------\n");
        
        for (Patient p : patients) {
            sb.append(String.format("%-20s %-10d %-15s\n", p.name, p.age, p.condition));
        }
        
        patientList.setText(sb.toString());
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new HospitalManagement();
            }
        });
    }
}

// 3) Chat Application
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class ChatApplication extends JFrame {
    private JTextArea chatArea;
    private JTextField messageField;
    private JButton sendButton;
    private String currentUser = "User";
    
    public ChatApplication() {
        setTitle("Simple Chat Application");
        setSize(400, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        JPanel mainPanel = new JPanel(new BorderLayout(5, 5));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
        
        // Chat display area
        chatArea = new JTextArea();
        chatArea.setEditable(false);
        chatArea.setLineWrap(true);
        chatArea.setWrapStyleWord(true);
        JScrollPane scrollPane = new JScrollPane(chatArea);
        
        // Input panel
        JPanel inputPanel = new JPanel(new BorderLayout(5, 0));
        messageField = new JTextField();
        messageField.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                sendMessage();
            }
        });
        
        sendButton = new JButton("Send");
        sendButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                sendMessage();
            }
        });
        
        inputPanel.add(messageField, BorderLayout.CENTER);
        inputPanel.add(sendButton, BorderLayout.EAST);
        
        mainPanel.add(scrollPane, BorderLayout.CENTER);
        mainPanel.add(inputPanel, BorderLayout.SOUTH);
        
        // User selection
        JPanel userPanel = new JPanel(new FlowLayout(FlowLayout.LEFT));
        userPanel.add(new JLabel("Current user:"));
        
        JRadioButton user1 = new JRadioButton("User");
        user1.setSelected(true);
        JRadioButton user2 = new JRadioButton("Friend");
        
        ButtonGroup userGroup = new ButtonGroup();
        userGroup.add(user1);
        userGroup.add(user2);
        
        user1.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentUser = "User";
            }
        });
        
        user2.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                currentUser = "Friend";
            }
        });
        
        userPanel.add(user1);
        userPanel.add(user2);
        
        mainPanel.add(userPanel, BorderLayout.NORTH);
        
        add(mainPanel);
        setVisible(true);
        
        messageField.requestFocus();
    }
    
    private void sendMessage() {
        String message = messageField.getText().trim();
        if (!message.isEmpty()) {
            chatArea.append(currentUser + ": " + message + "\n");
            messageField.setText("");
        }
        messageField.requestFocus();
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new ChatApplication();
            }
        });
    }
}

// 4) Simple Calculator
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class SimpleCalculator extends JFrame {
    private JTextField displayField;
    private double firstNumber = 0;
    private String operation = "";
    private boolean start = true;
    
    public SimpleCalculator() {
        setTitle("Simple Calculator");
        setSize(300, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        // Display field
        displayField = new JTextField("0");
        displayField.setHorizontalAlignment(JTextField.RIGHT);
        displayField.setEditable(false);
        displayField.setFont(new Font("Arial", Font.PLAIN, 24));
        
        // Button panel
        JPanel buttonPanel = new JPanel(new GridLayout(5, 4, 5, 5));
        
        // Add buttons
        String[] buttonLabels = {
            "7", "8", "9", "/",
            "4", "5", "6", "*",
            "1", "2", "3", "-",
            "0", ".", "=", "+",
            "C", "←", "", ""
        };
        
        for (String label : buttonLabels) {
            if (label.isEmpty()) {
                buttonPanel.add(new JLabel());
                continue;
            }
            
            JButton button = new JButton(label);
            button.setFont(new Font("Arial", Font.PLAIN, 18));
            
            if (label.matches("[0-9.]")) {
                button.addActionListener(new NumberListener());
            } else if (label.matches("[+\\-*/=]")) {
                button.addActionListener(new OperationListener());
            } else if (label.equals("C")) {
                button.addActionListener(new ActionListener() {
                    public void actionPerformed(ActionEvent e) {
                        displayField.setText("0");
                        start = true;
                        firstNumber = 0;
                        operation = "";
                    }
                });
            } else if (label.equals("←")) {
                button.addActionListener(new ActionListener() {
                    public void actionPerformed(ActionEvent e) {
                        String text = displayField.getText();
                        if (text.length() > 1) {
                            displayField.setText(text.substring(0, text.length() - 1));
                        } else {
                            displayField.setText("0");
                            start = true;
                        }
                    }
                });
            }
            
            buttonPanel.add(button);
        }
        
        setLayout(new BorderLayout(5, 5));
        add(displayField, BorderLayout.NORTH);
        add(buttonPanel, BorderLayout.CENTER);
        
        setVisible(true);
    }
    
    private class NumberListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            String digit = ((JButton) e.getSource()).getText();
            if (start) {
                if (digit.equals(".")) {
                    displayField.setText("0.");
                } else {
                    displayField.setText(digit);
                }
                start = false;
            } else {
                String currentText = displayField.getText();
                if (digit.equals(".") && currentText.contains(".")) {
                    return;
                }
                displayField.setText(currentText + digit);
            }
        }
    }
    
    private class OperationListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            String command = ((JButton) e.getSource()).getText();
            
            if (start) {
                if (command.equals("-")) {
                    displayField.setText(command);
                    start = false;
                } else {
                    operation = command;
                }
            } else {
                if (operation.isEmpty()) {
                    operation = command;
                    firstNumber = Double.parseDouble(displayField.getText());
                    start = true;
                } else if (command.equals("=")) {
                    double secondNumber = Double.parseDouble(displayField.getText());
                    double result = calculate(firstNumber, secondNumber, operation);
                    displayField.setText(String.valueOf(result));
                    firstNumber = result;
                    operation = "";
                    start = true;
                } else {
                    double secondNumber = Double.parseDouble(displayField.getText());
                    double result = calculate(firstNumber, secondNumber, operation);
                    displayField.setText(String.valueOf(result));
                    firstNumber = result;
                    operation = command;
                    start = true;
                }
            }
        }
        
        private double calculate(double n1, double n2, String op) {
            switch (op) {
                case "+": return n1 + n2;
                case "-": return n1 - n2;
                case "*": return n1 * n2;
                case "/": return n2 == 0 ? 0 : n1 / n2;
                default: return n2;
            }
        }
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new SimpleCalculator();
            }
        });
    }
}

// 5) Voting Application
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.HashMap;
import java.util.Map;

public class VotingApplication extends JFrame {
    private Map<String, Integer> candidateVotes = new HashMap<>();
    private JPanel votingPanel;
    private JPanel resultsPanel;
    private ButtonGroup candidateGroup;
    
    public VotingApplication() {
        setTitle("Voting Application");
        setSize(400, 500);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        // Initialize candidates
        candidateVotes.put("Candidate A", 0);
        candidateVotes.put("Candidate B", 0);
        candidateVotes.put("Candidate C", 0);
        candidateVotes.put("Candidate D", 0);
        
        JTabbedPane tabbedPane = new JTabbedPane();
        
        // Voting panel
        votingPanel = new JPanel(new BorderLayout(10, 10));
        votingPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        
        JLabel titleLabel = new JLabel("Cast Your Vote");
        titleLabel.setFont(new Font("Arial", Font.BOLD, 18));
        titleLabel.setHorizontalAlignment(JLabel.CENTER);
        
        JPanel candidatePanel = new JPanel(new GridLayout(0, 1, 5, 5));
        candidatePanel.setBorder(BorderFactory.createTitledBorder("Select a Candidate"));
        
        candidateGroup = new ButtonGroup();
        
        for (String candidate : candidateVotes.keySet()) {
            JRadioButton radioButton = new JRadioButton(candidate);
            candidateGroup.add(radioButton);
            candidatePanel.add(radioButton);
        }
        
        JButton voteButton = new JButton("Vote");
        voteButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                boolean voted = false;
                
                for (Component comp : candidatePanel.getComponents()) {
                    if (comp instanceof JRadioButton) {
                        JRadioButton radioButton = (JRadioButton) comp;
                        if (radioButton.isSelected()) {
                            String candidate = radioButton.getText();
                            candidateVotes.put(candidate, candidateVotes.get(candidate) + 1);
                            voted = true;
                            break;
                        }
                    }
                }
                
                if (voted) {
                    candidateGroup.clearSelection();
                    updateResults();
                    JOptionPane.showMessageDialog(null, "Vote cast successfully!");
                    tabbedPane.setSelectedIndex(1); // Switch to results tab
                } else {
                    JOptionPane.showMessageDialog(null, "Please select a candidate!");
                }
            }
        });
        
        votingPanel.add(titleLabel, BorderLayout.NORTH);
        votingPanel.add(candidatePanel, BorderLayout.CENTER);
        votingPanel.add(voteButton, BorderLayout.SOUTH);
        
        // Results panel
        resultsPanel = new JPanel(new BorderLayout(10, 10));
        resultsPanel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        
        JLabel resultsTitle = new JLabel("Election Results");
        resultsTitle.setFont(new Font("Arial", Font.BOLD, 18));
        resultsTitle.setHorizontalAlignment(JLabel.CENTER);
        
        JPanel resultsDisplay = new JPanel(new GridLayout(0, 2, 10, 10));
        resultsDisplay.setBorder(BorderFactory.createTitledBorder("Current Vote Count"));
        
        // Initial results display will be updated
        updateResultsPanel(resultsDisplay);
        
        JButton refreshButton = new JButton("Refresh Results");
        refreshButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                updateResults();
            }
        });
        
        resultsPanel.add(resultsTitle, BorderLayout.NORTH);
        resultsPanel.add(resultsDisplay, BorderLayout.CENTER);
        resultsPanel.add(refreshButton, BorderLayout.SOUTH);
        
        // Add panels to tabbed pane
        tabbedPane.addTab("Vote", votingPanel);
        tabbedPane.addTab("Results", resultsPanel);
        
        add(tabbedPane);
        setVisible(true);
    }
    
    private void updateResults() {
        Component[] components = resultsPanel.getComponents();
        for (Component comp : components) {
            if (comp instanceof JPanel && ((JPanel)comp).getBorder() != null) {
                JPanel resultsDisplay = (JPanel) comp;
                updateResultsPanel(resultsDisplay);
                break;
            }
        }
    }
    
    private void updateResultsPanel(JPanel panel) {
        panel.removeAll();
        
        for (Map.Entry<String, Integer> entry : candidateVotes.entrySet()) {
            panel.add(new JLabel(entry.getKey() + ":"));
            panel.add(new JLabel(entry.getValue() + " votes"));
        }
        
        panel.revalidate();
        panel.repaint();
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new VotingApplication();
            }
        });
    }
}
