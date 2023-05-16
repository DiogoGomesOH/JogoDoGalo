# JogoDoGalo
Codigo do jogo do galo em java.

import java.util.Scanner;

public class JogoDaVelha
{
    private static char[][] tabuleiro = new char[3][3];
    private static char jogador = 'X';

    public static void main (String[]args)
    {
        Tabuleiroinicio ();
        mostrarTabuleiro ();

        while (true)
        {
            System.out.print ("Jogador " + jogador +  ", digite a linha (1 a 3): ");
            int linha = lerNumero ();
            System.out.print ("Jogador " + jogador +  ", digite a coluna (1 a 3): ");
            int coluna = lerNumero ();

            if (jogadaValida (linha, coluna))
            {
                tabuleiro[linha - 1][coluna - 1] = jogador;
                mostrarTabuleiro ();

                if (jogadorGanhou ())
                {
                    System.out.println ("Jogador " + jogador + " venceu!");
                    break;
                }

                if (tabuleiroCompleto ())
                {
                    System.out.println ("Empate!");
                    break;
                }

                jogador = (jogador == 'X') ? 'O' : 'X';
            }
            else
            {
                System.out.println ("Jogada invC!lida, tente novamente.");
            }
        }
    }

    private static void  Tabuleiroinicio ()
    {
        for (int i = 0; i < tabuleiro.length; i++)
        {
            for (int j = 0; j < tabuleiro[i].length; j++)
            {
                tabuleiro[i][j] = ' ';
            }
        }
    }

    private static void mostrarTabuleiro ()
    {
        System.out.println (" " + tabuleiro[0][0] + " | " + tabuleiro[0][1] +
                " | " + tabuleiro[0][2] + " ");
        System.out.println ("---+---+---");
        System.out.println (" " + tabuleiro[1][0] + " | " + tabuleiro[1][1] +
                " | " + tabuleiro[1][2] + " ");
        System.out.println ("---+---+---");
        System.out.println (" " + tabuleiro[2][0] + " | " + tabuleiro[2][1] +
                " | " + tabuleiro[2][2] + " ");
    }

    private static int lerNumero ()
    {
        Scanner scanner = new Scanner (System.in);
        return scanner.nextInt ();
    }
    private static boolean jogadaValida (int linha, int coluna)
    {
        if (linha < 1 || linha > 3 || coluna < 1 || coluna > 3)
        {
            return false;
        }
        return tabuleiro[linha - 1][coluna - 1] == ' ';
    }


    private static boolean jogadorGanhou ()
    {
        // Verifica linhas
        for (int i = 0; i < 3; i++)
        {
            if (tabuleiro[i][0] == jogador && tabuleiro[i][1] == jogador
                    && tabuleiro[i][2] == jogador)
            {
                return true;
            }
        }

        // Verifica colunas
        for (int i = 0; i < 3; i++)
        {
            if (tabuleiro[0][i] == jogador && tabuleiro[1][i] == jogador
                    && tabuleiro[2][i] == jogador)
            {
                return true;
            }
        }

        // Verifica diagonais
        if (tabuleiro[0][0] == jogador&& tabuleiro[1][1] == jogador
                && tabuleiro[2][2] == jogador)
        {
            return true;
        }
        if (tabuleiro[0][2] == jogador && tabuleiro[1][1] == jogador
                && tabuleiro[2][0] == jogador)
        {
            return true;
        }

        return false;
    }

    private static boolean tabuleiroCompleto ()
    {
        for (int i = 0; i < tabuleiro.length; i++)
        {
            for (int j = 0; j < tabuleiro[i].length; j++)
            {
                if (tabuleiro[i][j] == ' ')
                {
                    return false;
                }
            }
        }
        return true;
    }
}
