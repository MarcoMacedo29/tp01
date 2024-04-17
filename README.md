Trabalho Prático01 - Jogo Pacman em MonoGame com C# - 
Engenharia e Desenvolvimento de Jogos Digitais
Marco Macedo nº27919 / Miguel Freitas nº29562 

Introdução:
Este relatório apresenta a implementação de uma versão simplificada do jogo Pac-Man, desenvolvida utilizando o framework MonoGame em C#. O objetivo é fornecer uma visão geral da estrutura do projeto, decisões de implementação e instruções de jogo. Além disso, será feita uma análise dos códigos disponibilizados, abordando a organização e a lógica implementada.

Implementação:
•	Estrutura de Pastas:
PacMan/
|-- Content/
      |-- Fonts/
      |-- SpriteSheets/
      |-- Sounds/
|-- Code/
      |-- Blinky.cs
      |-- Clyde.cs
      |-- Enemy.cs
      |-- Game1.cs
      |-- GameOver.cs
      |-- Inky.cs
      |-- Menu.cs
      |-- MySounds.cs
      |-- Node.cs
      |-- Pathfinding.cs
      |-- Pinky.cs
      |-- Player.cs
      |-- Program.cs
      |-- Snack.cs
      |-- SpriteAnimation.cs
      |-- SpriteSheet.cs
      |-- Text.cs
      |-- Title.cs

Content/: Contém recursos como imagens, fontes e sons.
Code/: Contém o código-fonte do jogo organizado em entidades, gerenciadores, telas e ajudantes.

Instruções de Jogo:
•	Objetivo:
Mova o Pac-Man pelo labirinto para comer todos os pontos e evitar os fantasmas.
•	Controles
Setas Direcionais: Mova o Pac-Man nas direções desejadas.
•	Fantasmas e Vidas
Fantasmas: Evite ser capturado pelos fantasmas.
Vidas: Você tem um número limitado de vidas.
•	Pontuação
Acumule pontos comendo os pontos pelo labirinto.

Decisões de Implementação:
•	Entidades:
PacMan: Representa o jogador controlável.
Ghost: Representa os inimigos que perseguem o Pac-Man.
•	Gerenciadores:
GameManager: Gerencia o estado geral do jogo, como pontuação e vidas.
•	Telas:
GameScreen: Controla o fluxo do jogo, como iniciar, pausar e encerrar.
•	Ajudantes:
CollisionHelper: Auxilia na detecção de colisões entre entidades.
Análise dos Códigos Disponibilizados:

Conclusão:
Implementamos com sucesso uma versão simplificada do clássico Pac-Man usando MonoGame em C#. Este projeto recria a emoção do jogo original, mantendo a jogabilidade icônica e desafiadora. Com controles simples e objetivos claros, o jogo oferece uma experiência divertida e envolvente para jogadores de todas as idades. A combinação de design retro com tecnologia moderna torna esta versão do Pac-Man uma homenagem ao legado duradouro deste jogo atemporal.
