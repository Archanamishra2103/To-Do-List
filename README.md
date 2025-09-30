# To-Do-List
A simple Java Swing-based To-Do List Application that allows users to manage tasks with a graphical interface. This project demonstrates Java Swing components (JFrame, JButton, JTextField, JList) and event handling.   Currently adding more features to it ..like tick mark, Date adder etc

    import javax.swing.*;
    import java.awt.*;
    import java.awt.event.*;

    public class ToDoApp extends JFrame {
    private DefaultListModel<String> taskListModel;
    private JList<String> taskList;
    private JTextField taskInput;
    private JButton addButton, deleteButton;

    public ToDoApp() {
        setTitle("✅ To-Do List App");
        setSize(400, 450);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null); // Center window
        setLayout(new BorderLayout());

        // Set custom icon (optional: place an icon file in project folder)
        ImageIcon icon = new ImageIcon("todo_icon.png");
        setIconImage(icon.getImage());

        // Set background color
        getContentPane().setBackground(new Color(240, 248, 255)); // light blueish

        // Input panel
        JPanel inputPanel = new JPanel(new BorderLayout());
        inputPanel.setBackground(new Color(230, 240, 255));

        taskInput = new JTextField();
        taskInput.setFont(new Font("Arial", Font.PLAIN, 16));
        taskInput.setBorder(BorderFactory.createEmptyBorder(5, 5, 5, 5));

        addButton = new JButton("➕ Add Task");
        addButton.setBackground(new Color(100, 149, 237));
        addButton.setForeground(Color.WHITE);
        addButton.setFocusPainted(false);

        inputPanel.add(taskInput, BorderLayout.CENTER);
        inputPanel.add(addButton, BorderLayout.EAST);

        // Task list
        taskListModel = new DefaultListModel<>();
        taskList = new JList<>(taskListModel);
        taskList.setFont(new Font("Segoe UI", Font.PLAIN, 14));
        taskList.setSelectionBackground(new Color(135, 206, 250));
        JScrollPane scrollPane = new JScrollPane(taskList);

        // Delete button
        deleteButton = new JButton("🗑️ Delete Task");
        deleteButton.setBackground(new Color(220, 20, 60));
        deleteButton.setForeground(Color.WHITE);
        deleteButton.setFocusPainted(false);

        // Add components
        add(inputPanel, BorderLayout.NORTH);
        add(scrollPane, BorderLayout.CENTER);
        add(deleteButton, BorderLayout.SOUTH);

        // Add Task Action
        addButton.addActionListener(e -> {
            String task = taskInput.getText().trim();
            if (!task.isEmpty()) {
                taskListModel.addElement(task);
                taskInput.setText("");
            } else {
                JOptionPane.showMessageDialog(this, "Task cannot be empty!");
            }
        });

        // Delete Task Action
        deleteButton.addActionListener(e -> {
            int selectedIndex = taskList.getSelectedIndex();
            if (selectedIndex != -1) {
                taskListModel.remove(selectedIndex);
            } else {
                JOptionPane.showMessageDialog(this, "Select a task to delete!");
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new ToDoApp().setVisible(true);
        });
    }
    }

       

   
