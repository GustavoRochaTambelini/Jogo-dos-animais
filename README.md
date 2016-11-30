package ArvoreAlti;

import java.awt.Font;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;

public class Jogo {
	static JButton botao;
	static JFrame tela;
	static JLabel text;

	public static void janela() {
		tela = new JFrame("Jogo Dos Animais");
		tela.setSize(300, 150);
		tela.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		tela.setLayout(null);
		tela.setLocationRelativeTo(null);
		tela.setResizable(false);
		tela.setVisible(true);

		text = new JLabel("Pense Em Um Animal !!!!!");
		tela.add(text);
		text.setBounds(80, 30, 150, 15);
		text.setFont(new Font("Arial", 0, 13));

		botao = new JButton("Pensei");
		tela.add(botao);
		botao.setBounds(75, 60, 150, 30);

	}

	public static void main(String[] args) {

		No viveNaAgua = new No("vive na agua");
		
		No tubarao = new No("Tubarão");
		No macaco = new No("Macaco");

		viveNaAgua.simEsquerdo = tubarao;
		viveNaAgua.naoDireito = macaco;

		janela();
		
		botao.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent e) {
				busca(viveNaAgua);
			}
			
		});

	}

	public static void busca(No animal) {
		int opcao = JOptionPane.showConfirmDialog(null, "O animal que você pensou " + animal.valor + "?");
		if (opcao == 0) {
			if (animal.simEsquerdo == null) {
				JOptionPane.showMessageDialog(null, "Acertei !!!!!!!");
			} else {
				busca(animal.simEsquerdo);
			}
		} else if (opcao == 1) {
			if (animal.naoDireito == null) {
				String newAnimal = JOptionPane.showInputDialog("Qual animal voce pensou ?");
				String acao = JOptionPane
						.showInputDialog("Um(a) " + newAnimal + "________________ e um Macaco nao!!");
				No novo = new No(newAnimal);
				No acaoDoAnimal = new No(acao);

				animal.naoDireito = acaoDoAnimal;
				acaoDoAnimal.simEsquerdo = novo;

			}else{
				busca(animal.naoDireito);
			}
		}else{
			System.exit(0);
		}
	}

}
