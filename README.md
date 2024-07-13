# Snake---Python
Jogo da Cobrinha - Snake - Python
 jogo básico da cobrinha (Snake) em Python usando a biblioteca Pygame. Vou fornecer o código completo para um jogo simples. Você pode executar este código no seu ambiente local.

Passos para instalar o Pygame:
Certifique-se de ter o Python instalado em seu sistema.
Instale a biblioteca Pygame usando pip:
sh
Copiar código
pip install pygame
Código do Jogo da Cobrinha
python
Copiar código
import pygame
import time
import random

pygame.init()

# Definindo cores
white = (255, 255, 255)
yellow = (255, 255, 102)
black = (0, 0, 0)
red = (213, 50, 80)
green = (0, 255, 0)
blue = (50, 153, 213)

# Definindo a dimensão da janela
dis_width = 800
dis_height = 600

dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('Jogo da Cobrinha')

clock = pygame.time.Clock()
snake_block = 10
snake_speed = 15

font_style = pygame.font.SysFont("bahnschrift", 25)
score_font = pygame.font.SysFont("comicsansms", 35)

def your_score(score):
    value = score_font.render("Sua Pontuação: " + str(score), True, black)
    dis.blit(value, [0, 0])

def our_snake(snake_block, snake_List):
    for x in snake_List:
        pygame.draw.rect(dis, black, [x[0], x[1], snake_block, snake_block])

def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 6, dis_height / 3])

def gameLoop():
    game_over = False
    game_close = False

    x1 = dis_width / 2
    y1 = dis_height / 2

    x1_change = 0
    y1_change = 0

    snake_List = []
    Length_of_snake = 1

    foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
    foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0

    while not game_over:

        while game_close == True:
            dis.fill(blue)
            message("Você perdeu! Pressione Q-Quit ou C-Play Again", red)
            your_score(Length_of_snake - 1)
            pygame.display.update()

            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        gameLoop()

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0

        if x1 >= dis_width or x1 < 0 or y1 >= dis_height or y1 < 0:
            game_close = True
        x1 += x1_change
        y1 += y1_change
        dis.fill(blue)
        pygame.draw.rect(dis, green, [foodx, foody, snake_block, snake_block])
        snake_Head = []
        snake_Head.append(x1)
        snake_Head.append(y1)
        snake_List.append(snake_Head)
        if len(snake_List) > Length_of_snake:
            del snake_List[0]

        for x in snake_List[:-1]:
            if x == snake_Head:
                game_close = True

        our_snake(snake_block, snake_List)
        your_score(Length_of_snake - 1)

        pygame.display.update()

        if x1 == foodx and y1 == foody:
            foodx = round(random.randrange(0, dis_width - snake_block) / 10.0) * 10.0
            foody = round(random.randrange(0, dis_height - snake_block) / 10.0) * 10.0
            Length_of_snake += 1

        clock.tick(snake_speed)

    pygame.quit()
    quit()

gameLoop()
Explicação do Código:
Importações e Inicialização: Importamos Pygame, tempo e random, e inicializamos Pygame.
Cores e Dimensões: Definimos algumas cores e as dimensões da janela do jogo.
Configuração do Jogo: Criamos a janela do jogo e definimos a velocidade e o tamanho do bloco da cobra.
Funções:
your_score(): Exibe a pontuação atual na tela.
our_snake(): Desenha a cobra na tela.
message(): Exibe mensagens na tela.
gameLoop(): Função principal que contém a lógica do jogo. Gerencia os eventos, movimentos da cobra, colisões, alimentação e atualização da tela.
Como Executar:
Salve o código em um arquivo Python, por exemplo, snake_game.py.
Execute o script usando o Python:
sh
Copiar código
python snake_game.py
Este é um jogo básico da cobrinha em Python usando Pygame. Você pode personalizar e expandir o jogo com novos recursos, como níveis, sons, gráficos aprimorados, etc.
