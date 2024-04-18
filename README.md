# Trabalho Prático01 - Jogo Pacman em MonoGame com C# - Engenharia e Desenvolvimento de Jogos Digitais - Marco Macedo nº27919 / Miguel Freitas nº29562 

# Indíce
1. [__Implementação__](#Implementação)

2. [__Instruções de Jogo__](#Instruções de Jogo)
# Introdução
Este relatório apresenta a implementação de uma versão simplificada do jogo Pac-Man, desenvolvida utilizando o framework MonoGame em C#. O objetivo é fornecer uma visão geral da estrutura do projeto, decisões de implementação e instruções de jogo. Além disso, será feita uma análise dos códigos disponibilizados, abordando a organização e a lógica implementada.
<p align="center">
  <img src="https://s2-techtudo.glbimg.com/Zgdo7fpjWUEzhDFBuMthj2OXnRw=/0x0:695x390/984x0/smart/filters:strip_icc()/i.s3.glbimg.com/v1/AUTH_08fbf48bc0524877943fe86e43087e7a/internal_photos/bs/2021/o/S/uINhTlQ8KW9l4wvqsu4g/2014-10-01-pac-man-curiosidades-classico.jpg"  alt="Pacman" width=700>
</p>

# Implementação

## Estrutura de Pastas:

* PacMan/
  - |-- Content/
  - |-- Fonts/
  - |-- SpriteSheets/
  - |-- Sounds/

* Code/
  - |-- Blinky.cs
  - |-- Clyde.cs
  - |-- Enemy.cs
  - |-- Game1.cs
  - |-- GameOver.cs
  - |-- Inky.cs
  - |-- Menu.cs
  - |-- MySounds.cs
  - |-- Node.cs
  - |-- Pathfinding.cs
  - |-- Pinky.cs
  - |-- Player.cs
  - |-- Program.cs
  - |-- Snack.cs
  - |-- SpriteAnimation.cs
  - |-- SpriteSheet.cs
  - |-- Text.cs
  - |-- Title.cs

- __Pacman/:__ Contém recursos como imagens, fontes e sons.
- __Code/:__ Contém o código-fonte do jogo organizado em entidades, gerenciadores, telas e ajudantes.

# Instruções de Jogo
* __Objetivo:__ 
    - Mova o Pac-Man pelo labirinto para comer todos os pontos e evitar os fantasmas.
* __Controles:__
    - __Setas Direcionais:__ Mova o Pac-Man nas direções desejadas.
* __Fantasmas e Vidas:__
    - __Fantasmas:__ Evite ser capturado pelos fantasmas.
    - __Vidas:__ Você tem um número limitado de vidas.
* __Pontuação:__
    - Acumule pontos comendo os pontos pelo labirinto.

# Decisões de Implementação
*  Entidades:
   - __PacMan:__ Representa o jogador controlável.
   - __Ghost:__ Representa os inimigos que perseguem o Pac-Man.
*  Gerenciadores:
   - __GameManager:__ Gerencia o estado geral do jogo, como pontuação e vidas.
*	 Telas:
   - GameScreen: Controla o fluxo do jogo, como iniciar, pausar e encerrar.
*	 Ajudantes:
   - CollisionHelper: Auxilia na detecção de colisões entre entidades.

# Análise dos Códigos Disponibilizados

## 	Inky.cs, Blinky.cs, Pinky.cs, Lyde.cs:
Cada ficheiro de cada um representa o inimigo no jogo Pac-Man. Ela herda da classe base Enemy e é responsável por inicializar as características específicas do inimigo, como seu alvo de dispersão, retângulos de animação e comportamento de perseguição. O código implementa métodos para determinar a posição do alvo de perseguição do inimigo com base na distância em relação ao jogador. Em resumo, esta classe organiza o comportamento e as propriedades do inimigo no contexto do jogo Pac-Man.

## 	 	Controller.cs:
A classe Controller gerencia a lógica do jogo Pac-Man. Ela mantém informações sobre o estado do jogo, como a grade do mapa, a posição dos lanches, o estado dos fantasmas e do Pac-Man, entre outros. Além disso, controla a transição entre os estados dos fantasmas (perseguir ou dispersar), cria e reinicia os fantasmas quando necessário, e verifica se os caminhos estão disponíveis para movimento.
O código utiliza estruturas de repetição para inicializar a grade do mapa com base em um array bidimensional, onde cada número representa um tipo de elemento no jogo, como paredes, lanches, casa dos fantasmas, entre outros. Ele também implementa métodos para desenhar a grade de depuração do mapa, bem como para desenhar e atualizar os fantasmas e os caminhos de busca.
Além disso, a classe gerencia eventos como a vitória do jogador, o fim do jogo, a morte do Pac-Man e o reinício do jogo. O código é organizado e modular, permitindo um controle eficiente do estado e do comportamento do jogo.

## 		MySounds.cs:
Este código define uma classe estática chamada MySounds que armazena referências para efeitos sonoros do jogo Pac-Man. Ele fornece campos estáticos para cada efeito sonoro, permitindo acesso global e controle centralizado dos sons do jogo. Cada campo representa um efeito sonoro específico.

## 		Game1.cs:
Este código é a classe principal do jogo Pac-Man, chamada Game1. Ela contém a lógica principal do jogo, incluindo a inicialização, carregamento de conteúdo, atualização e renderização dos elementos do jogo.
Variáveis e campos: Define diversos campos estáticos e instâncias necessárias para controlar o jogo, como o controlador do jogo, texturas, animações e sons.
Métodos de inicialização: Initialize e LoadContent são chamados durante a inicialização do jogo para configurar o ambiente e carregar recursos, como sprites e sons.
Métodos de atualização e desenho: Update e Draw são responsáveis por atualizar e renderizar os elementos do jogo, como o jogador (Pac-Man), fantasmas, pontos de comida e outros elementos visuais.
Lógica do jogo: Controla o fluxo do jogo, incluindo a detecção de colisões, movimentação dos personagens, gerenciamento de vidas, pontuação e transições de estado do jogo (como menu, jogo em andamento e game over).
Interação com o usuário: Permite que o jogador controle o Pac-Man usando o teclado e define as condições de vitória e derrota.
Renderização de elementos de interface: Desenha elementos como a pontuação, vidas restantes e outros textos na tela.

## 	 	GameOver.cs:
Este trecho de código implementa a classe GameOver, responsável por gerenciar e exibir a tela de fim de jogo no Pac-Man. Aqui está uma análise:
Campos e Propriedades:
basicFont: Armazena a fonte usada para renderizar o texto.
basicFontPos: Armazena a posição onde o texto será desenhado.
Método Update:
Verifica se a tecla de espaço foi pressionada. Se sim, muda o estado do jogo para o menu.
Método Draw:
Renderiza o texto "game over!" na tela com tamanho 48 e cor vermelha, com um fator de escala de 2.
Desenha o texto "PRESS SPACE TO GO TO MENU" usando a fonte básica definida anteriormente.
Essencialmente, essa classe fornece a funcionalidade para exibir a tela de fim de jogo e permite ao jogador voltar ao menu principal pressionando a tecla de espaço.

## 	 	Menu.cs:
Esse código implementa a classe Menu, responsável por gerenciar e exibir o menu principal do jogo Pac-Man. Aqui está uma análise:
Campos e Propriedades:
pacmanLogo: Armazena a textura do logotipo do Pac-Man.
pacmanLogoPos: Armazena a posição e o tamanho onde o logotipo do Pac-Man será desenhado.
basicFont: Armazena a fonte usada para renderizar o texto.
basicFontPos: Armazena a posição onde o texto será desenhado.
Método Update:
Verifica se a tecla Enter foi pressionada.
Se sim, muda o estado do jogo para o modo normal e inicia a reprodução do som de início de jogo.
Método Draw:
Renderiza o texto "PRESS ENTER TO PLAY" na tela com a fonte básica definida anteriormente e na cor vermelha.
Desenha o logotipo do Pac-Man na tela na posição e tamanho definidos.

## 	 	Node.cs:
Esse código define a classe node, que representa um nó em um grafo utilizado para o algoritmo de busca A* no jogo Pac-Man. Aqui está uma análise do código:
Campos:
gCost: Custo acumulado do nó até o nó inicial.
hCost: Custo heurístico estimado do nó até o nó de destino.
parent: Nó pai no caminho até o nó atual.
ignoreDirection: Direção a ser ignorada ao determinar os vizinhos do nó.
isWalkable: Indica se o nó é navegável (não é uma parede).
pos: Posição do nó no mapa.
tile: Referência ao tile associado ao nó.
Método setIgnoreDirection:
•	Define a direção a ser ignorada com base na direção atual.
Método setParent:
•	Define o nó pai.
Propriedade fCost:
•	Retorna a soma dos custos gCost e hCost.
Construtor:
•	Inicializa o nó com base na posição fornecida.
Verifica se a posição está dentro dos limites do mapa e se o tile associado é uma parede ou não.
Método Copy:
•	Cria uma cópia do nó.
•	A cópia inclui a cópia do nó pai, se existir.
Método getNeighbours:
Obtém os vizinhos navegáveis do nó, excluindo a direção especificada para ignorar.
Verifica se os vizinhos estão dentro dos limites do mapa e se são navegáveis.
Essa classe é fundamental para o algoritmo de busca A* usado para calcular caminhos para os fantasmas no jogo Pac-Man, garantindo que eles se movam de forma inteligente pelo labirinto, evitando paredes e alcançando o jogador de forma eficiente.

##  Pathfinfings.cs:
Este código implementa um algoritmo de busca chamado A* (A estrela) para encontrar o caminho mais curto entre dois pontos em um labirinto, usado no jogo Pac-Man para os fantasmas perseguirem o jogador. O algoritmo:
Inicializa duas listas: uma para nós a serem examinados e outra para nós já examinados.
Itera até encontrar o destino ou esgotar os nós a serem examinados.
Seleciona o próximo nó com o menor custo total para exploração.
Expande os nós vizinhos, calculando custos e atualizando caminhos se necessário.
Reconstrói o caminho mais curto se encontrado.
Essa implementação é crucial para o comportamento inteligente dos fantasmas, permitindo que eles naveguem pelo labirinto e persigam o jogador de forma eficiente.

## 	 	Player.cs:
Este código implementa a classe Player para controlar o personagem do jogador no jogo Pac-Man. Aqui estão suas principais características:
Atributos: Define a posição, direção, velocidade e animações do jogador, bem como variáveis para controle de movimento, temporizadores e vidas extras.
Inicialização: Configura a posição inicial do jogador no labirinto e define os retângulos para animações de movimento e de morte.
Atualização: Processa entrada do teclado para definir a próxima direção de movimento do jogador e atualiza sua posição de acordo. Também gerencia animações de movimento.
Interseção com Tiles: Verifica se o jogador está sobre um determinado tile no labirinto e executa ações correspondentes, como comer snacks ou teletransportar.
Desenho: Desenha o jogador na tela usando animações de sprite.
Essa classe é fundamental para controlar a mecânica do jogo e interagir com o ambiente do labirinto e os elementos do jogo, como os snacks e os teletransportadores. 
mas em atualizaçao meter update e o mesmo no desenho e atributos e assim.

## 		Program.cs:
Este código serve como o ponto de entrada para o jogo Pac-Man.

## 	 	Snack.cs:
Este código implementa a classe Snack para representar os snacks (ou pontos) que o jogador pode coletar no jogo Pac-Man. Aqui está uma breve explicação das principais características desta classe:
Enumerador SnackType: Define os tipos de snacks disponíveis, como "Small" (pequeno) e "Big" (grande).
Atributos: Inclui a posição do snack no grid do labirinto, o tipo de snack, a pontuação ganha ao coletar o snack e o retângulo de desenho para snacks pequenos e grandes.
Método Construtor: Inicializa um novo snack com base no tipo fornecido, definindo sua posição no grid e atribuindo uma pontuação e um deslocamento de raio adequados.
Método Draw: Desenha o snack na tela com base no seu tipo e posição. Para snacks grandes, um temporizador é usado para alternar entre a visualização do snack e uma visualização intermitente.
Essa classe é responsável por representar os snacks no jogo Pac-Man e desenhá-los na tela para que o jogador possa coletá-los durante o jogo.

## 	 	SpriteAnimation.cs:
Esta classe, SpriteAnimation, é responsável por gerenciar a animação de sprites em um jogo. Aqui está uma explicação das suas principais características:
Atributos: Inclui um temporizador para controlar a taxa de atualização da animação, um conjunto de retângulos de origem que representam os frames da animação, um índice de animação para acompanhar o frame atual, e variáveis para controlar se a animação está em loop e se está sendo reproduzida.
Métodos Construtores: Fornece várias opções para inicializar a animação com diferentes configurações, como especificar o limiar de tempo, os retângulos de origem e o índice de animação inicial.
Métodos de Atualização e Desenho: Atualiza o frame da animação com base no tempo decorrido e desenha o frame atual na tela. Dependendo das configurações, a animação pode ser em loop ou reproduzida uma vez e, em seguida, parar.
Essa classe é fundamental para criar e exibir animações de sprites em um jogo, permitindo que elementos do jogo, como personagens e objetos, tenham movimentos suaves e realistas.

## 	 	Text.cs:
Essa classe, Text, é responsável por desenhar texto na tela do jogo usando uma folha de sprite. Aqui estão suas principais características:
Enumeração de Cores: Define uma enumeração para as cores do texto, como branco e vermelho.
Atributos: Inclui uma folha de sprite que contém os caracteres de texto e retângulos para cada caractere.
Métodos Construtores: Define um método construtor para inicializar a folha de sprite com uma textura fornecida.
Métodos de Desenho: Fornece métodos para desenhar texto na tela com diferentes cores e escalas. Os caracteres são desenhados com base na string fornecida e na posição especificada, com um espaçamento entre letras opcional.
Essa classe é útil para exibir informações na tela do jogo, como pontuações, mensagens de texto e outros elementos de interface do usuário. Ela permite personalizar a aparência do texto e integrá-lo perfeitamente ao estilo visual do jogo.

## 	 	Tile.cs
Essa classe, Tile, representa um único tile no mapa do jogo Pac-Man. Aqui estão seus principais pontos:
Enumeração de Tipos de Tiles: Define uma enumeração para os tipos de tiles, incluindo Nenhum, Parede, Fantasma, Casa dos Fantasmas, Jogador e Snack.
Atributos: Inclui um tipo de tile, que indica o tipo de conteúdo do tile, e um indicador de vazio para determinar se o tile está ocupado ou não.
Propriedade de Posição: Fornece uma propriedade para acessar a posição do tile no mapa.
Método para Obter Distância entre Tiles: Implementa um método estático para calcular a distância euclidiana entre duas posições de tiles.
Métodos Construtores: Define construtores para criar um tile com uma posição e um tipo de tile especificados.
Essa classe é fundamental para representar e interagir com os diferentes elementos no mapa do jogo Pac-Man, como paredes, fantasmas, snacks e o jogador. Ela facilita o gerenciamento e a manipulação dos tiles durante a jogabilidade.

## 	 	Enemy.cs
O código define uma série de enums para os tipos de fantasmas (GhostType) e estados do inimigo (EnemyState).Há a definição de diversas propriedades e variáveis para controlar a posição, direção, velocidade e estado dos fantasmas, bem como para armazenar informações sobre as animações dos mesmos.O construtor da classe inicializa várias dessas propriedades com valores padrão e configura as animações dos fantasmas.Há métodos para desenhar (Draw) e atualizar (Update) os fantasmas no jogo. Isso inclui lógica para decidir a direção dos fantasmas, movê-los pelo tabuleiro e lidar com a colisão deles com o jogador ou com outros elementos do jogo.Existem métodos para calcular a posição alvo dos fantasmas em diferentes estados do jogo, como perseguição, fuga e quando são comidos pelo jogador.
Além disso, há métodos para lidar com eventos específicos, como quando um fantasma é comido pelo jogador. Basicamente esta parte define como os fantasmas se movem, reagem aos eventos do jogo e interagem com o jogador. 

# Conclusão
Implementamos com sucesso uma versão simplificada do clássico Pac-Man usando MonoGame em C#. Este projeto recria a emoção do jogo original, mantendo a jogabilidade icônica e desafiadora. Com controles simples e objetivos claros, o jogo oferece uma experiência divertida e envolvente para jogadores de todas as idades. A combinação de design retro com tecnologia moderna torna esta versão do Pac-Man uma homenagem ao legado duradouro deste jogo atemporal.

<p align="center">
  <img src="https://lh4.googleusercontent.com/proxy/Pk0kAWyTCeDVYcgMK34QZbTBDLMRxyOAU_fmoxJUxoJs2Mjge3j6gBT3HY6bIGodMr233c4D1hk-_jPB-P38AJPIYu0QAtIZFPayv_1TlP1cYAYCa2Sr4h8J_yVe" width="300" alt="Pacman">
</p>

