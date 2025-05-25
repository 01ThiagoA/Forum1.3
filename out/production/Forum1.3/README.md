import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;
import java.text.DecimalFormatSymbols;
import java.util.Locale;

public class Main {
public static void main(String[] args) {
JFrame frame = new JFrame("Calculadora de IMC");
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setSize(350, 250);

        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(5, 2, 10, 10));

        JLabel pesoLabel = new JLabel("Peso (kg):");
        JTextField pesoField = new JTextField();

        JLabel alturaLabel = new JLabel("Altura (m):");
        JTextField alturaField = new JTextField();

        JButton calcularButton = new JButton("Calcular IMC");
        JLabel resultadoLabel = new JLabel("");

        panel.add(pesoLabel);
        panel.add(pesoField);
        panel.add(alturaLabel);
        panel.add(alturaField);
        panel.add(new JLabel());
        panel.add(calcularButton);
        panel.add(new JLabel("Resultado:"));
        panel.add(resultadoLabel);

        frame.getContentPane().add(panel);
        frame.setVisible(true);

        calcularButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    String pesoTexto = pesoField.getText().replace(",", ".");
                    String alturaTexto = alturaField.getText().replace(",", ".");

                    double peso = Double.parseDouble(pesoTexto);
                    double altura = Double.parseDouble(alturaTexto);

                    double imc = peso / (altura * altura);
                    String classificacao;

                    if (imc < 18.5) classificacao = "Abaixo do peso";
                    else if (imc < 24.9) classificacao = "Peso normal";
                    else if (imc < 29.9) classificacao = "Sobrepeso";
                    else if (imc < 34.9) classificacao = "Obesidade grau I";
                    else if (imc < 39.9) classificacao = "Obesidade grau II";
                    else classificacao = "Obesidade grau III (mórbida)";

                    DecimalFormat df = new DecimalFormat("#.##", new DecimalFormatSymbols(Locale.US));
                    resultadoLabel.setText("IMC: " + df.format(imc) + " - " + classificacao);
                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(frame, "Por favor, insira valores válidos. Ex: 70,5 e 1,75");
                }
            }
        });
    }
}


