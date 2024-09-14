# ExercicioMVC

![modeloMVC](https://github.com/user-attachments/assets/62eb51f7-77f5-475c-b600-62d96889adf4)

# tela login
![telaloginusuario](https://github.com/user-attachments/assets/aeb9058a-f7fa-4236-aa70-e44666af1603)


# tela cadastro

![telacadastrousuario](https://github.com/user-attachments/assets/2113537c-9e28-4b4a-9cc5-b04d1b04e050)


# class usuario 

// Usuario.java
public class Usuario {
    private String username;
    private String password;

    public Usuario(String username, String password) {
        this.username = username;
        this.password = password;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }
}


# tela cadastro codigo 

// CadastroView.java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionListener;

public class CadastroView extends JFrame {
    private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton cadastrarButton;

    public CadastroView() {
        setTitle("Cadastro de Usuário");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(3, 2));

        JLabel usernameLabel = new JLabel("Usuário:");
        JLabel passwordLabel = new JLabel("Senha:");

        usernameField = new JTextField();
        passwordField = new JPasswordField();
        cadastrarButton = new JButton("Cadastrar");

        add(usernameLabel);
        add(usernameField);
        add(passwordLabel);
        add(passwordField);
        add(new JLabel()); // Placeholder
        add(cadastrarButton);
    }

    public String getUsername() {
        return usernameField.getText();
    }

    public String getPassword() {
        return new String(passwordField.getPassword());
    }

    public void addCadastroListener(ActionListener listener) {
        cadastrarButton.addActionListener(listener);
    }
}


# tela login codigo 

// LoginView.java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionListener;

public class LoginView extends JFrame {
    private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton loginButton;

    public LoginView() {
        setTitle("Login de Usuário");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(3, 2));

        JLabel usernameLabel = new JLabel("Usuário:");
        JLabel passwordLabel = new JLabel("Senha:");

        usernameField = new JTextField();
        passwordField = new JPasswordField();
        loginButton = new JButton("Login");

        add(usernameLabel);
        add(usernameField);
        add(passwordLabel);
        add(passwordField);
        add(new JLabel()); // Placeholder
        add(loginButton);
    }

    public String getUsername() {
        return usernameField.getText();
    }

    public String getPassword() {
        return new String(passwordField.getPassword());
    }

    public void addLoginListener(ActionListener listener) {
        loginButton.addActionListener(listener);
    }
}


# class controller cadastro 

// CadastroController.java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JOptionPane;

public class CadastroController {
    private CadastroView view;
    private Usuario model;

    public CadastroController(CadastroView view) {
        this.view = view;

        this.view.addCadastroListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                handleCadastro();
            }
        });
    }

    private void handleCadastro() {
        String username = view.getUsername();
        String password = view.getPassword();

        if (username.isEmpty() || password.isEmpty()) {
            JOptionPane.showMessageDialog(view, "Por favor, preencha todos os campos.");
        } else {
            model = new Usuario(username, password);
            JOptionPane.showMessageDialog(view, "Usuário cadastrado com sucesso!");
            view.dispose();
            new LoginView().setVisible(true);
        }
    }
}

# class controlador login 

// LoginController.java
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JOptionPane;

public class LoginController {
    private LoginView view;
    private Usuario model;

    public LoginController(LoginView view, Usuario model) {
        this.view = view;
        this.model = model;

        this.view.addLoginListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                handleLogin();
            }
        });
    }

    private void handleLogin() {
        String username = view.getUsername();
        String password = view.getPassword();

        if (username.equals(model.getUsername()) && password.equals(model.getPassword())) {
            JOptionPane.showMessageDialog(view, "Login bem-sucedido!");
        } else {
            JOptionPane.showMessageDialog(view, "Usuário ou senha inválidos.");
        }
    }
}

# class Main 

// Main.java
public class Main {
    public static void main(String[] args) {
        CadastroView cadastroView = new CadastroView();
        CadastroController cadastroController = new CadastroController(cadastroView);
        cadastroView.setVisible(true);
    }
}





