# Exibir infos dos Alunos

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.ArrayList;
import java.util.Scanner;

public class ArquivoLeEscreve {

    public static void main(String[] args) {
        ArrayList<Estudante> estudantes = new ArrayList<>();
        String nome, sexo, CPF;
        Scanner entrada = new Scanner(System.in);

        File arquivo = new File("alunos.txt");
        try {
            if (!arquivo.exists()) {
//cria um arquivo (vazio)
                arquivo.createNewFile();
            }
            for (int i = 1; i <= 5; i++) {
                System.out.println("Digite o nome do Aluno");
                nome = entrada.nextLine();
                System.out.println("Digite o sexo do aluno");
                sexo = entrada.nextLine();
                System.out.println("Digite o CPF do Aluno");
                CPF = entrada.nextLine();
                Estudante est = new Estudante(nome, sexo, CPF);
                estudantes.add(est);
            }
//escreve no arquivo
            FileWriter fw = new FileWriter(arquivo, true);
            BufferedWriter bw = new BufferedWriter(fw);
            for (Estudante est : estudantes)
            {
            bw.write(est.getNome()+","+est.getSexo()+","+est.getCPF());
            bw.newLine();}
            
            bw.close();
            fw.close();
//faz a leitura do arquivo 

            FileReader fr = new FileReader(arquivo);
            BufferedReader br = new BufferedReader(fr);
//enquanto houver mais linhas
            while (br.ready()) {
//lê a proxima linha
                String linha = br.readLine();
//faz algo com a linha
                System.out.println(linha);
            }
            br.close();
            fr.close();
        } catch (IOException ex) {
            ex.printStackTrace();
        }
    }
}
