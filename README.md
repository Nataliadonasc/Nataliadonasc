
import random
tabuleiro = [[0, 0, 0], [0, 0, 0], [0, 0, 0]]
def imprimir_tabuleiro():
    for linha in tabuleiro:
        print(" ".join(str(celula) for celula in linha))
    print()
def verificar_vitoria(jogador):
    for i in range(3):
        if all(tabuleiro[i][j] == jogador for j in range(3)) or all(tabuleiro[j][i] == jogador for j in range(3)):
            return True
    if tabuleiro[0][0] == jogador and tabuleiro[1][1] == jogador and tabuleiro[2][2] == jogador:
        return True
    if tabuleiro[0][2] == jogador and tabuleiro[1][1] == jogador and tabuleiro[2][0] == jogador:
        return True
    return False
def jogada_maquina():
    while True:
        a = random.randint(0, 2)
        b = random.randint(0, 2)
        if tabuleiro[a][b] == 0:
            tabuleiro[a][b] = 1
            break
def jogada_humano():
    while True:
        try:
            linha = int(input('Digite a linha (0-2): '))
            coluna = int(input('Digite a coluna (0-2): '))
            if tabuleiro[linha][coluna] == 0:
                tabuleiro[linha][coluna] = 2
                break
            else:
                print("Posição ocupada! Tente novamente.")
        except (ValueError, IndexError):
            print("Entrada inválida! Insira números entre 0 e 2.")
while True:
    jogada_maquina()
    imprimir_tabuleiro()
    
    if verificar_vitoria(1):
        print("Vitória da máquina!")
        break
    jogada_humano()
    imprimir_tabuleiro()
    
    if verificar_vitoria(2):
        print("Vitória do humano!")
        break
