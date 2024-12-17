# HOUSE-RENTAL-SYSTEM-USING-JAVA
import javax.swing.*;
import java.util.*;

public class HouseRentalSystem {
    static Map<String, String> homeownerDatabase = new HashMap<>();
    static Map<String, String> tenantDatabase = new HashMap<>();
    static List<House> houses = new ArrayList<>();

    public static void main(String[] args) {
        initializeHouses();
        new MainMenu();
    }

    private static void initializeHouses() {
        houses.add(new House("Beach House", "Chennai", 15000));
        houses.add(new House("City Apartment", "Trichy", 12000));
        houses.add(new House("Countryside Villa", "Salem", 18000));
        houses.add(new House("Downtown Flat", "Karur", 16000));
        houses.add(new House("Luxury Bungalow", "Thanjavur", 20000));
    }

    static class MainMenu {
        MainMenu() {
            JFrame frame = new JFrame("House Rental System");
            JLabel welcomeLabel = new JLabel("Welcome to the House Rental System", SwingConstants.CENTER);
            JButton adminButton = new JButton("Admin Login");
            JButton homeownerButton = new JButton("Homeowner ");
            JButton tenantButton = new JButton("Tenant ");

            welcomeLabel.setBounds(50, 50, 300, 30);
            adminButton.setBounds(100, 100, 200, 30);
            homeownerButton.setBounds(100, 150, 200, 30);
            tenantButton.setBounds(100, 200, 200, 30);

            frame.add(welcomeLabel);
            frame.add(adminButton);
            frame.add(homeownerButton);
            frame.add(tenantButton);

            frame.setSize(400, 400);
            frame.setLayout(null);
            frame.setVisible(true);

            adminButton.addActionListener(e -> new AdminLogin());
            homeownerButton.addActionListener(e -> new HomeownerRegisterLogin());
            tenantButton.addActionListener(e -> new TenantRegisterLogin());
        }
    }

    static class AdminLogin {
        AdminLogin() {
            JFrame frame = new JFrame("Admin Login");
            JButton loginButton = new JButton("Login");
            JTextField usernameField = new JTextField();
            JPasswordField passwordField = new JPasswordField();

            JLabel usernameLabel = new JLabel("Username:");
            JLabel passwordLabel = new JLabel("Password:");

            usernameLabel.setBounds(100, 70, 200, 30);
            usernameField.setBounds(100, 100, 200, 30);
            passwordLabel.setBounds(100, 130, 200, 30);
            passwordField.setBounds(100, 160, 200, 30);
            loginButton.setBounds(100, 200, 200, 30);

            frame.add(usernameLabel);
            frame.add(usernameField);
            frame.add(passwordLabel);
            frame.add(passwordField);
            frame.add(loginButton);
frame.setSize(400, 300);
            frame.setLayout(null);
            frame.setVisible(true);

            loginButton.addActionListener(e -> {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());

                if (username.equals("admin") && password.equals("admin@123")) {
                    JOptionPane.showMessageDialog(frame, "Login Successful!");
                    frame.setVisible(false);
                    new AdminDashboard();
                } else {
                    JOptionPane.showMessageDialog(frame, "Invalid Credentials!");
                }
            });
        }
    }

    static class AdminDashboard {
        AdminDashboard() {
            JFrame frame = new JFrame("Admin Dashboard");
            JButton manageUsersButton = new JButton("Manage Users");
            JButton manageHousesButton = new JButton("Manage Houses");
            JButton logoutButton = new JButton("Logout");

            manageUsersButton.setBounds(100, 100, 200, 30);
            manageHousesButton.setBounds(100, 150, 200, 30);
            logoutButton.setBounds(100, 200, 200, 30);

            frame.add(manageUsersButton);
            frame.add(manageHousesButton);
            frame.add(logoutButton);

            frame.setSize(400, 400);
            frame.setLayout(null);
            frame.setVisible(true);

            manageUsersButton.addActionListener(e -> {
                String[] users = homeownerDatabase.keySet().toArray(new String[0]);
                String selectedUser = (String) JOptionPane.showInputDialog(
                        frame, "Select a user to delete:", "Manage Users",
                        JOptionPane.QUESTION_MESSAGE, null, users, users[0]);
                if (selectedUser != null) {
                    homeownerDatabase.remove(selectedUser);
                    JOptionPane.showMessageDialog(frame, "User deleted successfully!");
                }
            });

            manageHousesButton.addActionListener(e -> {
                String[] houseNames = houses.stream().map(h -> h.name).toArray(String[]::new);
                String selectedHouse = (String) JOptionPane.showInputDialog(
                        frame, "Select a house to delete:", "Manage Houses",
                        JOptionPane.QUESTION_MESSAGE, null, houseNames, houseNames[0]);
                if (selectedHouse != null) {
                    houses.removeIf(h -> h.name.equals(selectedHouse));
                    JOptionPane.showMessageDialog(frame, "House deleted successfully!");
                }
            });

            logoutButton.addActionListener(e -> {
                frame.setVisible(false);
                new MainMenu();
            });
        }
    }
    static class HomeownerRegisterLogin {
        HomeownerRegisterLogin() {
            JFrame frame = new JFrame("Homeowner Register/Login");
            JButton registerButton = new JButton("Register");
            JButton loginButton = new JButton("Login");
            JTextField nameField = new JTextField();
            JTextField ageField = new JTextField();
            JTextField usernameField = new JTextField();
            JPasswordField passwordField = new JPasswordField();
            JTextField emailField = new JTextField();

            JLabel nameLabel = new JLabel("Name:");
            JLabel ageLabel = new JLabel("Age:");
            JLabel usernameLabel = new JLabel("Username:");
            JLabel passwordLabel = new JLabel("Password:");
            JLabel emailLabel = new JLabel("Email:");

            nameLabel.setBounds(50, 30, 200, 30);
            nameField.setBounds(150, 30, 200, 30);
            ageLabel.setBounds(50, 70, 200, 30);
            ageField.setBounds(150, 70, 200, 30);
            usernameLabel.setBounds(50, 110, 200, 30);
            usernameField.setBounds(150, 110, 200, 30);
            passwordLabel.setBounds(50, 150, 200, 30);
            passwordField.setBounds(150, 150, 200, 30);
            emailLabel.setBounds(50, 190, 200, 30);
            emailField.setBounds(150, 190, 200, 30);
            registerButton.setBounds(50, 230, 150, 30);
            loginButton.setBounds(220, 230, 150, 30);

            frame.add(nameLabel);
            frame.add(nameField);
            frame.add(ageLabel);
            frame.add(ageField);
            frame.add(usernameLabel);
            frame.add(usernameField);
            frame.add(passwordLabel);
            frame.add(passwordField);
            frame.add(emailLabel);
            frame.add(emailField);
            frame.add(registerButton);
            frame.add(loginButton);

            frame.setSize(400, 350);
            frame.setLayout(null);
            frame.setVisible(true);

            registerButton.addActionListener(e -> {
                String name = nameField.getText();
                int age = Integer.parseInt(ageField.getText());
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                String email = emailField.getText();

                if (age < 18) {
                    JOptionPane.showMessageDialog(frame, "Age must be above 18!", "Error", JOptionPane.ERROR_MESSAGE);
                } else if (homeownerDatabase.containsKey(username)) {
                    JOptionPane.showMessageDialog(frame, "Username already exists!", "Error", JOptionPane.ERROR_MESSAGE);
                } else {
                    homeownerDatabase.put(username, password);
                    JOptionPane.showMessageDialog(frame, "Registration Successful!");
                    frame.setVisible(false);
                    new HomeownerRegisterLogin(); // Redirect back to login
                }
            });

            loginButton.addActionListener(e -> {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());

                if (homeownerDatabase.containsKey(username) && homeownerDatabase.get(username).equals(password)) {
                    JOptionPane.showMessageDialog(frame, "Login Successful!");
                    frame.setVisible(false);
                    new HomeownerDashboard(username);
                } else {
                    JOptionPane.showMessageDialog(frame, "Invalid Credentials!");
                }
            });
        }
    }
    static class HomeownerDashboard {
        HomeownerDashboard(String username) {
            JFrame frame = new JFrame("Homeowner Dashboard");
            JButton addHouseButton = new JButton("Add New House");
            JButton viewHousesButton = new JButton("View Your Houses");
            JButton logoutButton = new JButton("Logout");

            addHouseButton.setBounds(100, 100, 200, 30);
            viewHousesButton.setBounds(100, 150, 200, 30);
            logoutButton.setBounds(100, 200, 200, 30);

            frame.add(addHouseButton);
            frame.add(viewHousesButton);
            frame.add(logoutButton);

            frame.setSize(400, 400);
            frame.setLayout(null);
            frame.setVisible(true);

            addHouseButton.addActionListener(e -> {
                String name = JOptionPane.showInputDialog(frame, "Enter House Name:");
                String location = JOptionPane.showInputDialog(frame, "Enter Location:");
                String rentStr = JOptionPane.showInputDialog(frame, "Enter Rent (per month):");
                try {
                    int rent = Integer.parseInt(rentStr);
                    houses.add(new House(name, location, rent));
                    JOptionPane.showMessageDialog(frame, "House added successfully!");
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(frame, "Invalid rent entered!");
                }
            });

            viewHousesButton.addActionListener(e -> {
                StringBuilder ownerHouses = new StringBuilder("Your Houses:\n");
                for (House house : houses) {
                    ownerHouses.append("Name: ").append(house.name)
                            .append(", Location: ").append(house.location)
                            .append(", Rent: $").append(house.rent).append("\n");
                }
                JOptionPane.showMessageDialog(frame, ownerHouses.toString());
            });

            logoutButton.addActionListener(e -> {
                frame.setVisible(false);
                new MainMenu();
            });
        }
    }
    static class TenantRegisterLogin {
        TenantRegisterLogin() {
            JFrame frame = new JFrame("Tenant Register/Login");
            JButton registerButton = new JButton("Register");
            JButton loginButton = new JButton("Login");
            JTextField nameField = new JTextField();
            JTextField ageField = new JTextField();
            JTextField usernameField = new JTextField();
            JPasswordField passwordField = new JPasswordField();
            JTextField emailField = new JTextField();

            JLabel nameLabel = new JLabel("Name:");
            JLabel ageLabel = new JLabel("Age:");
            JLabel usernameLabel = new JLabel("Username:");
            JLabel passwordLabel = new JLabel("Password:");
            JLabel emailLabel = new JLabel("Email:");

            nameLabel.setBounds(50, 30, 200, 30);
            nameField.setBounds(150, 30, 200, 30);
            ageLabel.setBounds(50, 70, 200, 30);
            ageField.setBounds(150, 70, 200, 30);
            usernameLabel.setBounds(50, 110, 200, 30);
            usernameField.setBounds(150, 110, 200, 30);
            passwordLabel.setBounds(50, 150, 200, 30);
            passwordField.setBounds(150, 150, 200, 30);
            emailLabel.setBounds(50, 190, 200, 30);
            emailField.setBounds(150, 190, 200, 30);
            registerButton.setBounds(50, 230, 150, 30);
            loginButton.setBounds(220, 230, 150, 30);

            frame.add(nameLabel);
            frame.add(nameField);
            frame.add(ageLabel);
            frame.add(ageField);
            frame.add(usernameLabel);
            frame.add(usernameField);
            frame.add(passwordLabel);
            frame.add(passwordField);
            frame.add(emailLabel);
            frame.add(emailField);
            frame.add(registerButton);
            frame.add(loginButton);

            frame.setSize(400, 350);
            frame.setLayout(null);
            frame.setVisible(true);

            registerButton.addActionListener(e -> {
                String name = nameField.getText();
                int age = Integer.parseInt(ageField.getText());
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());
                String email = emailField.getText();

                if (age < 18) {
                    JOptionPane.showMessageDialog(frame, "Age must be above 18!", "Error", JOptionPane.ERROR_MESSAGE);
                } else if (tenantDatabase.containsKey(username)) {
                    JOptionPane.showMessageDialog(frame, "Username already exists!", "Error", JOptionPane.ERROR_MESSAGE);
                } else {
                    tenantDatabase.put(username, password);
                    JOptionPane.showMessageDialog(frame, "Registration Successful!");
                    frame.setVisible(false);
                    new TenantRegisterLogin(); // Redirect back to login
                }
            });

            loginButton.addActionListener(e -> {
                String username = usernameField.getText();
                String password = new String(passwordField.getPassword());

                if (tenantDatabase.containsKey(username) && tenantDatabase.get(username).equals(password)) {
                    JOptionPane.showMessageDialog(frame, "Login Successful!");
                    frame.setVisible(false);
                    new TenantDashboard();
                } else {
                    JOptionPane.showMessageDialog(frame, "Invalid Credentials!");
                }
            });
        }
    }
    static class TenantDashboard {
        TenantDashboard() {
            JFrame frame = new JFrame("Tenant Dashboard");
            JButton viewHousesButton = new JButton("View Available Houses");
            JButton bookHouseButton = new JButton("Book a House");
            JButton logoutButton = new JButton("Logout");

            viewHousesButton.setBounds(100, 100, 200, 30);
            bookHouseButton.setBounds(100, 150, 200, 30);
            logoutButton.setBounds(100, 200, 200, 30);

            frame.add(viewHousesButton);
            frame.add(bookHouseButton);
            frame.add(logoutButton);

            frame.setSize(400, 400);
            frame.setLayout(null);
            frame.setVisible(true);

            viewHousesButton.addActionListener(e -> {
                if (houses.isEmpty()) {
                    JOptionPane.showMessageDialog(frame, "No houses available!");
                    return;
                }

                StringBuilder houseList = new StringBuilder("Available Houses:\n");
                for (House house : houses) {
                    houseList.append("House Name: ").append(house.name).append("\n")
                            .append("Location: ").append(house.location).append("\n")
                            .append("Rent: $").append(house.rent).append("\n\n");
                }
                JOptionPane.showMessageDialog(frame, houseList.toString());
            });

            bookHouseButton.addActionListener(e -> {
                if (houses.isEmpty()) {
                    JOptionPane.showMessageDialog(frame, "No houses available for booking!");
                    return;
                }

                String[] houseNames = houses.stream().map(h -> h.name).toArray(String[]::new);
                String selectedHouse = (String) JOptionPane.showInputDialog(
                        frame, "Select a house to book:", "Book a House",
                        JOptionPane.QUESTION_MESSAGE, null, houseNames, houseNames[0]);

                if (selectedHouse != null) {
                    houses.removeIf(h -> h.name.equals(selectedHouse)); // Remove booked house
                    JOptionPane.showMessageDialog(frame, "You have successfully booked the house: " + selectedHouse);
                }
            });

            logoutButton.addActionListener(e -> {
                frame.setVisible(false);
                new MainMenu();
            });
        }
    }

    static class House {
        String name;
        String location;
        int rent;

        House(String name, String location, int rent) {
            this.name = name;
            this.location = location;
            this.rent = rent;
        }
    }
}
