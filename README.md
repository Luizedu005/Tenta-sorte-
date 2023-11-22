
import pygame
import sys

pygame.init()

# Configurações do jogo
largura_tela = 800
altura_tela = 600
tela = pygame.display.set_mode((largura_tela, altura_tela))
pygame.display.set_caption("Jogo de Quebra-Cabeças")

# Classe do Núcleo
class Nucleo(pygame.sprite.Sprite):
    def __init__(self, cor, x, y):
        super().__init__()
        self.image = pygame.Surface((50, 50))
        self.image.fill(cor)
        self.rect = self.image.get_rect()
        self.rect.x = x
        self.rect.y = y

# Lista de núcleos
lista_nucleos = pygame.sprite.Group()

# Adicionar núcleos à lista (pode ser em um loop)
nucleo = Nucleo((255, 0, 0), 100, 100)
lista_nucleos.add(nucleo)

# Variáveis do jogo
pontuacao = 0
nivel_atual = 1

# Função para gerar níveis dinamicamente
def gerar_nivel(nivel):
    # Adicionar lógica para gerar níveis dinamicamente
    print(f"Gerando nível {nivel}")

# Função para dar recompensas
def dar_recompensa():
    # Adicionar lógica para dar recompensas ao jogador
    print("Você ganhou uma recompensa!")

# Função para desafiar amigos
def desafiar_amigos():
    # Adicionar lógica para desafiar amigos
    print("Você desafiou seus amigos!")

# Loop principal do jogo
while True:
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif evento.type == pygame.MOUSEBUTTONDOWN:
            if evento.button == 1:  # Clique esquerdo
                for nucleo in lista_nucleos:
                    if nucleo.rect.collidepoint(evento.pos):
                        pontuacao += 10
                        if pontuacao % 50 == 0:
                            dar_recompensa()

    # Lógica para avançar para o próximo nível
    if pontuacao >= nivel_atual * 100:  # Exemplo: avançar a cada 100 pontos
        gerar_nivel(nivel_atual)
        nivel_atual += 1
        desafiar_amigos()

    # Detectar colisão entre os núcleos
    colisoes = pygame.sprite.groupcollide(lista_nucleos, lista_nucleos, False, False)
    for nucleo, outros_nucleos in colisoes.items():
        # Adicionar lógica de colisão entre núcleos aqui
        print(f"Colisão entre {nucleo} e {outros_nucleos}")

    # Desenhar na tela
    tela.fill((255, 255, 255))  # Cor de fundo branca
    pygame.draw.rect(tela, (0, 0, 0), (0, 0, largura_tela, altura_tela), 2)  # Borda da tela
    lista_nucleos.draw(tela)   # Desenhar núcleos na tela

    # Exibir pontuação na tela
    fonte = pygame.font.Font(None, 36)
    texto_pontuacao = fonte.render(f"Pontuação: {pontuacao}", True, (0, 0, 0))
    tela.blit(texto_pontuacao, (10, 10))

    # Atualizar a tela
    pygame.display.flip()# Tenta-sorte-
