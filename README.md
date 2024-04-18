# Trabalho Prático01 - Jogo Pacman em MonoGame com C# - Engenharia e Desenvolvimento de Jogos Digitais - Marco Macedo nº27919 / Miguel Freitas nº29562 

# __Indíce__
1. [__Introdução__](#Introdução)
2. [__Implementação__](#Implementação)
3. [__Instruções de Jogo__](#instru)
4. [__Decisões de Implementação__](#decisoes)
5. [__Análise dos Códigos Disponibilizados__](#analise)
6. [__Conclusão__](#Conclusão)

# __Introdução__
Este relatório apresenta a implementação de uma versão simplificada do jogo Pac-Man, desenvolvida utilizando o framework MonoGame em C#. O objetivo é fornecer uma visão geral da estrutura do projeto, decisões de implementação e instruções de jogo. Além disso, será feita uma análise dos códigos disponibilizados, abordando a organização e a lógica implementada.
<p align="center">
  <img src="https://s2-techtudo.glbimg.com/Zgdo7fpjWUEzhDFBuMthj2OXnRw=/0x0:695x390/984x0/smart/filters:strip_icc()/i.s3.glbimg.com/v1/AUTH_08fbf48bc0524877943fe86e43087e7a/internal_photos/bs/2021/o/S/uINhTlQ8KW9l4wvqsu4g/2014-10-01-pac-man-curiosidades-classico.jpg"  alt="Pacman" width=700>
</p>

# __Implementação__


## __Estrutura de Pastas:__

* __PacMan/__
    - |-- Content/
    - |-- Fonts/
    - |-- SpriteSheets/
    - |-- Sounds/

* __Code/__
    - [|-- Inky.cs](#4codigos)
    - |-- Blinky.cs
    - |-- Pinky.cs  
    - |-- Clyde.cs
    - |-- Controller.cs
    - |-- MySounds.cs 
    - |-- Game1.cs
    - |-- GameOver.cs
    - |-- Menu.cs
    - |-- Node.cs
    - |-- Pathfinding.cs
    - |-- Player.cs
    - |-- Program.cs
    - |-- Snack.cs
    - |-- SpriteAnimation.cs
    - |-- Text.cs
    - |-- Tile.cs 
    - |-- Enemy.cs
    - |-- SpriteSheet.cs
    
    

- __Pacman/:__ Contém recursos como imagens, fontes e sons.
- __Code/:__ Contém o código-fonte do jogo organizado em entidades, gerenciadores, telas e ajudantes.

<a name="instru"></a>
# __Instruções de Jogo__
* __Objetivo:__ 
    - Mova o Pac-Man pelo labirinto para comer todos os pontos e evitar os fantasmas.
* __Controles:__
    - __Setas Direcionais:__ Mova o Pac-Man nas direções desejadas.
* __Fantasmas e Vidas:__
    - __Fantasmas:__ Evite ser capturado pelos fantasmas.
    - __Vidas:__ Você tem um número limitado de vidas.
* __Pontuação:__
    - Acumule pontos comendo os pontos pelo labirinto.

<a name="decisoes"></a>
# __Decisões de Implementação__
*  __Entidades:__
     - __PacMan:__ Representa o jogador controlável.
     - __Ghost:__ Representa os inimigos que perseguem o Pac-Man.
*  __Gerenciadores:__
     - __GameManager:__ Gerencia o estado geral do jogo, como pontuação e vidas.
*	 __Telas:__
     - __GameScreen:__ Controla o fluxo do jogo, como iniciar, pausar e encerrar.
*	 __Ajudantes:__
     - __CollisionHelper:__ Auxilia na detecção de colisões entre entidades.

<a name="analise"></a>
# __Análise dos Códigos Disponibilizados__

<a name="4codigos"></a>
## 	__Inky.cs, Blinky.cs, Pinky.cs, Clyde.cs:__
Cada ficheiro de cada um representa o inimigo no jogo Pac-Man. Ela herda da classe base Enemy e é responsável por inicializar as características específicas do inimigo, como seu alvo de dispersão, retângulos de animação e comportamento de perseguição. 

O código implementa métodos para determinar a posição do alvo de perseguição do inimigo com base na distância em relação ao jogador. Em resumo, esta classe organiza o comportamento e as propriedades do inimigo no contexto do jogo Pac-Man. Como os códigos .cs são semelhantes , concluimos só mostrar um (Blinky.cs):

```
using System.Collections.Generic;
using System.Linq;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;

namespace Pacman
{
    public class Blinky : Enemy
    {
        public Blinky(int tileX, int tileY, Tile[,] tileArray) : base(tileX, tileY, tileArray)
        {
            ScatterTargetTile = new Vector2(26, 2);
            type = GhostType.Blinky;

            rectsDown[0] = new Rectangle(1659, 195, 42, 42);
            rectsDown[1] = new Rectangle(1707, 195, 42, 42);

            rectsUp[0] = new Rectangle(1563, 195, 42, 42);
            rectsUp[1] = new Rectangle(1611, 195, 42, 42);

            rectsLeft[0] = new Rectangle(1467, 195, 42, 42);
            rectsLeft[1] = new Rectangle(1515, 195, 42, 42);

            rectsRight[0] = new Rectangle(1371, 195, 42, 42);
            rectsRight[1] = new Rectangle(1419, 195, 42, 42);

            enemyAnim = new SpriteAnimation(0.08f, rectsLeft);
        }
    }
}
```

## 	 	__Controller.cs:__
A classe Controller é responsável pelo controle do jogo, incluindo a criação do mapa, a lógica dos fantasmas, a verificação do tipo de bloco e muito mais. Ela mantém o estado do jogo, como o estado dos fantasmas, a pontuação, as vidas extras do jogador e assim por diante. 

Além disso, gerencia a criação e o controle dos objetos no jogo, como snacks e fantasmas, e possui métodos para atualizar e desenhar elementos do jogo, como fantasmas, snacks e a grade de debug.


## 		__MySounds.cs:__
Este código define uma classe estática chamada MySounds que armazena referências para efeitos sonoros do jogo Pac-Man. 

Ele fornece campos estáticos para cada efeito sonoro, permitindo acesso global e controle centralizado dos sons do jogo. 
Cada campo representa um efeito sonoro específico.
```
using System;
using System.Collections.Generic;
using System.Text;

using Microsoft.Xna.Framework.Audio;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

namespace Pacman
{
    public static class MySounds
    {
        public static SoundEffect game_start;
        public static SoundEffect munch;
        public static SoundEffectInstance munchInstance;
        public static SoundEffect credit;
        public static SoundEffect death_1;
        public static SoundEffect death_2;
        public static SoundEffect eat_fruit;
        public static SoundEffect eat_ghost;
        public static SoundEffect power_pellet;
        public static SoundEffectInstance power_pellet_instance;
        public static SoundEffect extend;
        public static SoundEffect intermission;
        public static SoundEffect retreating;
        public static SoundEffectInstance retreatingInstance;
        public static SoundEffect siren_1;
        public static SoundEffectInstance siren_1_instance;
        public static SoundEffect siren_2;
        public static SoundEffect siren_3;
        public static SoundEffect siren_4;
        public static SoundEffect siren_5;
    }
}
```
## 		__Game1.cs:__
O Game1.cs é o principal do jogo Pac-Man, onde a maioria das operações essenciais acontecem. Ela gerencia o ciclo de vida do jogo, desde sua inicialização até a renderização na tela. Responsável por carregar recursos, como imagens e sons, também coordena a interação entre os elementos do jogo, como os fantasmas, o jogador e os itens. Além disso, controla o estado do jogo, como pausas, game over e retorno ao menu principal. 

Em resumo, é responsável por garantir uma experiência de jogo fluida e envolvente para o jogador.

## 	 	__GameOver.cs:__
A classe GameOver controla a tela de fim de jogo. Quando a tecla de espaço é pressionada, ela volta ao menu principal. 

A mensagem "game over!" é exibida em vermelho, e há uma instrução para pressionar a tecla espaço para voltar ao menu. 

```
using System;
using System.Linq;
using System.Collections.Generic;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
using Microsoft.Xna.Framework.Audio;

namespace Pacman
{
    public static class GameOver
    {
        private static SpriteFont basicFont;
        private static Vector2 basicFontPos = new Vector2(93, 400);
        public static SpriteFont setBasicFont
        {
            set { basicFont = value; }
        }

        public static void Update()
        {
            KeyboardState kState = Keyboard.GetState();
            if (kState.IsKeyDown(Keys.Space))
            {
                Game1.gameController.gameState = Controller.GameState.Menu;
            }
        }

        public static void Draw(SpriteBatch spriteBatch, Text text)
        {
            text.draw(spriteBatch, "game over!", new Vector2(100, 321), 48, Text.Color.Red, 2f);
            spriteBatch.DrawString(basicFont, "PRESS SPACE TO GO TO MENU", basicFontPos, Color.Red);
        }
    }
}
```

## 	 	__Menu.cs:__
O Menu.cs, responsável por exibir e gerenciar o menu inicial do jogo. Ela contém métodos para atualizar e desenhar o menu na tela, incluindo o logotipo do Pac-Man e a mensagem "PRESS ENTER TO PLAY". 

Quando o jogador pressiona a tecla Enter, o estado do jogo muda para o modo normal e o som de início do jogo é reproduzido.

```
using System;
using System.Linq;
using System.Collections.Generic;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
using Microsoft.Xna.Framework.Audio;

namespace Pacman
{
    public static class Menu
    {
        private static Texture2D pacmanLogo;
        private static Rectangle pacmanLogoPos = new Rectangle(13, 40, 4530/7, 1184/7);
        private static SpriteFont basicFont;
        private static Vector2 basicFontPos = new Vector2(150, 400);

        public static SpriteFont setBasicFont
        {
            set { basicFont = value; }
        }

        public static Texture2D setPacmanLogo
        {
            set { pacmanLogo = value; }
        }

        public static void Update(GameTime gameTime)
        {
            KeyboardState kState = Keyboard.GetState();
            if (kState.IsKeyDown(Keys.Enter))
            {
                Game1.gameController.gameState = Controller.GameState.Normal;
                MySounds.game_start.Play();
            }
        }

        public static void Draw(SpriteBatch spriteBatch)
        {
            spriteBatch.DrawString(basicFont, "PRESS ENTER TO PLAY", basicFontPos, Color.Red);
            spriteBatch.Draw(pacmanLogo, pacmanLogoPos, Color.White);
        }
    }
}
```

## 	 	__Node.cs:__
A classe Node neste código serve como uma representação abstrata de um ponto específico no mapa do jogo Pac-Man. Ela é essencial para o algoritmo de busca utilizado para calcular os caminhos que os fantasmas devem seguir para alcançar o jogador. Cada nó armazena informações importantes, como sua posição, se é ou não um local onde os fantasmas podem se mover, os custos associados ao movimento até esse ponto e uma referência ao nó pai. 

Isso permite que o jogo determine os caminhos mais eficientes para os fantasmas percorrerem o labirinto, evitando paredes e obstáculos. Em resumo, a classe Node desempenha um papel crucial na inteligência artificial dos fantasmas, garantindo que eles persigam o jogador de forma inteligente e desafiadora.

```
using System;
using System.Collections.Generic;
using System.Text;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

namespace Pacman
{
    public class Node
    {
        public int gCost;
        public int hCost;

        public Node parent;
        public Dir ignoreDirection = Dir.None;

        public void setIgnoreDirection(Dir currentDir)
        {
            switch (currentDir)
            {
                case Dir.Right:
                    ignoreDirection = Dir.Left;
                    break;
                case Dir.Left:
                    ignoreDirection = Dir.Right;
                    break;
                case Dir.Down:
                    ignoreDirection = Dir.Up;
                    break;
                case Dir.Up:
                    ignoreDirection = Dir.Down;
                    break;
            }
        }

        public void setParent(Node parent)
        {
            this.parent = parent;
        }
        
        public int fCost {
            get {
                return gCost + hCost;
            }
        }

        public bool isWalkable;

        public Vector2 pos;
        Tile tile;

        public Node(Vector2 pos, Tile[,] tileArray)
        {
            if (pos.X < 0 || pos.Y < 0 || pos.X >= Controller.numberOfTilesX || pos.Y >= Controller.numberOfTilesY)
            {
                this.pos = new Vector2(-100, -100);
            }
            else
            {
                this.pos = pos;
                tile = tileArray[(int)pos.X, (int)pos.Y];
                if (tile.tileType == Tile.TileType.Wall)
                {
                    isWalkable = false;
                }
                else
                {
                    isWalkable = true;
                }
            }

        }

        public Node Copy(Tile[,] tileArray)
        {
            Node node = new Node(pos, tileArray);

            node.hCost = hCost;
            node.gCost = gCost;
            node.ignoreDirection = ignoreDirection;
            if (parent != null)
            {
                node.setParent(parent.Copy(tileArray));
            }

            return node;
        }

        public List<Node> getNeighbours(Tile[,] tileArray)
        {
            List<Node> neighbours = new List<Node>();

            if (ignoreDirection != Dir.Left)
            { 
                Node left = new Node(new Vector2(pos.X - 1, pos.Y), tileArray);
                if (left.pos != new Vector2(-100, -100)) neighbours.Add(left);
            }

            if (ignoreDirection != Dir.Right)
            {
                Node right = new Node(new Vector2(pos.X + 1, pos.Y), tileArray);
                if (right.pos != new Vector2(-100, -100)) neighbours.Add(right);
            }

            if (ignoreDirection != Dir.Up)
            {
                Node up = new Node(new Vector2(pos.X, pos.Y - 1), tileArray);
                if (up.pos != new Vector2(-100, -100)) neighbours.Add(up);
            }

            if (ignoreDirection != Dir.Down)
            {
                Node down = new Node(new Vector2(pos.X, pos.Y + 1), tileArray);
                if (down.pos != new Vector2(-100, -100)) neighbours.Add(down);
            }

            return neighbours;
        }
    }
}
```
##  __Pathfinfings.cs:__
Este código implementa um algoritmo de busca chamado A* (A estrela) para encontrar o caminho mais curto entre dois pontos em um labirinto, usado no jogo Pac-Man para os fantasmas perseguirem o jogador. O
algoritmo:
Inicializa duas listas: uma para nós a serem examinados e outra para nós já examinados.
Itera até encontrar o destino ou esgotar os nós a serem examinados.
Seleciona o próximo nó com o menor custo total para exploração.
Expande os nós vizinhos, calculando custos e atualizando caminhos se necessário.
Reconstrói o caminho mais curto se encontrado.
Essa implementação é crucial para o comportamento inteligente dos fantasmas, permitindo que eles naveguem pelo labirinto e persigam o jogador de forma eficiente.

## 	 	__Player.cs:__
Este código implementa a classe Player para controlar o personagem do jogador no jogo Pac-Man. Aqui estão suas principais características:
Atributos: Define a posição, direção, velocidade e animações do jogador, bem como variáveis para controle de movimento, temporizadores e vidas extras.
Inicialização: Configura a posição inicial do jogador no labirinto e define os retângulos para animações de movimento e de morte.
Atualização: Processa entrada do teclado para definir a próxima direção de movimento do jogador e atualiza sua posição de acordo. Também gerencia animações de movimento.
Interseção com Tiles: Verifica se o jogador está sobre um determinado tile no labirinto e executa ações correspondentes, como comer snacks ou teletransportar.
Desenho: Desenha o jogador na tela usando animações de sprite.
Essa classe é fundamental para controlar a mecânica do jogo e interagir com o ambiente do labirinto e os elementos do jogo, como os snacks e os teletransportadores. 
mas em atualizaçao meter update e o mesmo no desenho e atributos e assim.

## 		__Program.cs:__
Este código serve como o ponto de entrada para o jogo Pac-Man.
```
using System;

namespace Pacman
{
    public static class Program
    {
        [STAThread]
        static void Main()
        {
            using (var game = new Game1())
                game.Run();
        }
    }
}
```
## 	 	__Snack.cs:__
Este código implementa a classe Snack para representar os snacks (ou pontos) que o jogador pode coletar no jogo Pac-Man. Aqui está uma breve explicação das principais características desta classe:
Enumerador SnackType: Define os tipos de snacks disponíveis, como "Small" (pequeno) e "Big" (grande).
Atributos: Inclui a posição do snack no grid do labirinto, o tipo de snack, a pontuação ganha ao coletar o snack e o retângulo de desenho para snacks pequenos e grandes.
Método Construtor: Inicializa um novo snack com base no tipo fornecido, definindo sua posição no grid e atribuindo uma pontuação e um deslocamento de raio adequados.
Método Draw: Desenha o snack na tela com base no seu tipo e posição. Para snacks grandes, um temporizador é usado para alternar entre a visualização do snack e uma visualização intermitente.
Essa classe é responsável por representar os snacks no jogo Pac-Man e desenhá-los na tela para que o jogador possa coletá-los durante o jogo.

```
using System;
using System.Collections.Generic;
using System.Text;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

namespace Pacman
{
    public class Snack
    {
        public enum SnackType { Small, Big };
        public SnackType snackType;
        private Vector2 gridPosition;
        private int[] gridTile;
        public int scoreGain;
        private Rectangle smallSnackRect = new Rectangle(33, 33, 6, 6);
        private Rectangle bigSnackRect = new Rectangle(24, 72, 24, 24);
        private int radiusOffSet;
        private int timerBigSnack = 20;

        public Vector2 Position
        {
            get { return gridPosition; }
        }

        public Snack(SnackType newSnackType, Vector2 newPosition, int[] newGridTile)
        {
            snackType = newSnackType;
            if (newSnackType == SnackType.Big)
            {
                scoreGain = 50;
                radiusOffSet = 12;
            }
            else
            {
                scoreGain = 10;
                radiusOffSet = 3;
            }
                
            gridPosition = newPosition;
            gridTile = newGridTile;
        }

        public void Draw(SpriteBatch spriteBatch)
        {
            if (snackType == SnackType.Small)
                Game1.spriteSheet1.drawSprite(spriteBatch, smallSnackRect, new Vector2(gridPosition.X + Controller.tileWidth / 2 - radiusOffSet, gridPosition.Y + Controller.tileHeight / 2 - radiusOffSet));
            else
            { 
                if (timerBigSnack >= 10 || Game1.gamePauseTimer > 0)
                    Game1.spriteSheet1.drawSprite(spriteBatch, bigSnackRect, new Vector2(gridPosition.X + Controller.tileWidth / 2 - radiusOffSet, gridPosition.Y + Controller.tileHeight / 2 - radiusOffSet));
                timerBigSnack -= 1;
                if (timerBigSnack < 0)
                {
                    timerBigSnack = 20;
                }
            }
        }
    }
}
```

## 	 	__SpriteAnimation.cs:__
Esta classe, SpriteAnimation, é responsável por gerenciar a animação de sprites em um jogo. Aqui está uma explicação das suas principais características:
Atributos: Inclui um temporizador para controlar a taxa de atualização da animação, um conjunto de retângulos de origem que representam os frames da animação, um índice de animação para acompanhar o frame atual, e variáveis para controlar se a animação está em loop e se está sendo reproduzida.
Métodos Construtores: Fornece várias opções para inicializar a animação com diferentes configurações, como especificar o limiar de tempo, os retângulos de origem e o índice de animação inicial.
Métodos de Atualização e Desenho: Atualiza o frame da animação com base no tempo decorrido e desenha o frame atual na tela. Dependendo das configurações, a animação pode ser em loop ou reproduzida uma vez e, em seguida, parar.
Essa classe é fundamental para criar e exibir animações de sprites em um jogo, permitindo que elementos do jogo, como personagens e objetos, tenham movimentos suaves e realistas.

## 	 	__Text.cs:__
Essa classe, Text, é responsável por desenhar texto na tela do jogo usando uma folha de sprite. Aqui estão suas principais características:
Enumeração de Cores: Define uma enumeração para as cores do texto, como branco e vermelho.
Atributos: Inclui uma folha de sprite que contém os caracteres de texto e retângulos para cada caractere.
Métodos Construtores: Define um método construtor para inicializar a folha de sprite com uma textura fornecida.
Métodos de Desenho: Fornece métodos para desenhar texto na tela com diferentes cores e escalas. Os caracteres são desenhados com base na string fornecida e na posição especificada, com um espaçamento entre letras opcional.
Essa classe é útil para exibir informações na tela do jogo, como pontuações, mensagens de texto e outros elementos de interface do usuário. Ela permite personalizar a aparência do texto e integrá-lo perfeitamente ao estilo visual do jogo.

## 	 	__Tile.cs:__
Essa classe, Tile, representa um único tile no mapa do jogo Pac-Man. Aqui estão seus principais pontos:
Enumeração de Tipos de Tiles: Define uma enumeração para os tipos de tiles, incluindo Nenhum, Parede, Fantasma, Casa dos Fantasmas, Jogador e Snack.
Atributos: Inclui um tipo de tile, que indica o tipo de conteúdo do tile, e um indicador de vazio para determinar se o tile está ocupado ou não.
Propriedade de Posição: Fornece uma propriedade para acessar a posição do tile no mapa.
Método para Obter Distância entre Tiles: Implementa um método estático para calcular a distância euclidiana entre duas posições de tiles.
Métodos Construtores: Define construtores para criar um tile com uma posição e um tipo de tile especificados.
Essa classe é fundamental para representar e interagir com os diferentes elementos no mapa do jogo Pac-Man, como paredes, fantasmas, snacks e o jogador. Ela facilita o gerenciamento e a manipulação dos tiles durante a jogabilidade.

```
using System;
using System.Collections.Generic;
using System.Text;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

namespace Pacman
{
    public class Tile
    {
        public enum TileType { None, Wall, Ghost, GhostHouse, Player, Snack };

        public TileType tileType = TileType.None;
        public bool isEmpty = true;

        Vector2 position;

        public Vector2 Position
        {
            get
            {
                return position;
            }
        }

        public static int getDistanceBetweenTiles(Vector2 pos1, Vector2 pos2)
        {
            return (int)Math.Sqrt(Math.Pow(pos1.X - pos2.X, 2) + Math.Pow(pos1.Y - pos2.Y, 2));
        }

        public Tile(Vector2 newPosition)
        {
            position = newPosition;
        }

        public Tile(Vector2 newPosition, TileType newTileType)
        {
            position = newPosition;
            tileType = newTileType;
        }
    }
}
```

## 	 	__Enemy.cs:__
O código define uma série de enums para os tipos de fantasmas (GhostType) e estados do inimigo (EnemyState).Há a definição de diversas propriedades e variáveis para controlar a posição, direção, velocidade e estado dos fantasmas, bem como para armazenar informações sobre as animações dos mesmos.O construtor da classe inicializa várias dessas propriedades com valores padrão e configura as animações dos fantasmas.Há métodos para desenhar (Draw) e atualizar (Update) os fantasmas no jogo. Isso inclui lógica para decidir a direção dos fantasmas, movê-los pelo tabuleiro e lidar com a colisão deles com o jogador ou com outros elementos do jogo.Existem métodos para calcular a posição alvo dos fantasmas em diferentes estados do jogo, como perseguição, fuga e quando são comidos pelo jogador.
Além disso, há métodos para lidar com eventos específicos, como quando um fantasma é comido pelo jogador. Basicamente esta parte define como os fantasmas se movem, reagem aos eventos do jogo e interagem com o jogador.

## __SpriteSheet.cs:__
O SpriteSheet.cs facilita o desenho de sprites em um jogo, permitindo a renderização eficiente de elementos visuais, como personagens e itens. 

Ela gerencia uma imagem que contém vários sprites e fornece métodos para desenhar esses sprites na tela em diferentes posições e escalas.

```
using System;
using System.Collections.Generic;
using System.Text;

using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

namespace Pacman
{
    public class SpriteSheet
    {
        private Texture2D spriteSheet;

        public SpriteSheet(Texture2D newSpriteSheet)
        {
            spriteSheet = newSpriteSheet;
        }

        public void drawSprite(SpriteBatch spriteBatch, Rectangle sourceRectangle, Vector2 position)
        {
            spriteBatch.Draw(spriteSheet, position, sourceRectangle, Color.White);
        }

        public void drawSprite(SpriteBatch spriteBatch, Rectangle sourceRectangle, Vector2 position, float scale)
        {
            spriteBatch.Draw(spriteSheet, position, sourceRectangle, Color.White, 0f, new Vector2(0,0), scale, SpriteEffects.None, 0f);
        }
    }
}
```
# __Conclusão__
Implementamos com sucesso uma versão simplificada do clássico Pac-Man usando MonoGame em C#. Este projeto recria a emoção do jogo original, mantendo a jogabilidade icônica e desafiadora. Com controles simples e objetivos claros, o jogo oferece uma experiência divertida e envolvente para jogadores de todas as idades. A combinação de design retro com tecnologia moderna torna esta versão do Pac-Man uma homenagem ao legado duradouro deste jogo atemporal.

<p align="center">
  <img src="https://lh4.googleusercontent.com/proxy/Pk0kAWyTCeDVYcgMK34QZbTBDLMRxyOAU_fmoxJUxoJs2Mjge3j6gBT3HY6bIGodMr233c4D1hk-_jPB-P38AJPIYu0QAtIZFPayv_1TlP1cYAYCa2Sr4h8J_yVe" width="300" alt="Pacman">
</p>

