# Motor Cubo

![Cube Engine](http://i.imgur.com/m9jjG.png)

O Cube Engine é um mecanismo 3D HTML5 baseado em tela, absolutamente sem OpenGL e, portanto, sem aceleração 3D. Esta é uma prova de conceito e projeto de aprendizado, mas pode ser divertido até certo ponto... contanto que você tenha um computador absurdamente poderoso.

## Demonstração
Confira a [demonstração ao vivo](http://nurgak.github.com/Cube-engine).

## Mundo
O mundo se assemelha ao de [Minecraft](http://www.minecraft.net/), o popular jogo 3D do tipo voxel baseado em caixas. Você pode adicionar e remover tudo e qualquer coisa, diferentes tipos de nós estão disponíveis. As bordas são limitadas apenas pelo tamanho de um inteiro em Javascript, o que significa que o mundo é gerado dinamicamente à medida que o jogador visita novas áreas. Não há limite vertical, mas a distância de renderização é um pouco limitada.

A topografia do mundo é gerada por uma função pseudo-aleatória. O sistema subjacente imita o de Minecraft: o mundo é feito de 16 por 16 por nós infinitos "pedaços". A função pseudo-aleatória gera um único valor de altura para cada pedaço e os valores de altura entre eles são interpolados. Tudo sob o valor de altura é preenchido com nós e tudo acima é deixado vazio. Dependendo da altura, podem ser encontrados diferentes tipos de solo (grama, terra, areia...).

Ao contrário do Minecraft, o renderizador de mundo usa um gerador de ruído perlin 2D em vez de 3D, não há minérios ou túneis subterrâneos, inimigos ou mobs, árvores ou física. Como o renderizador toma todo o poder de processamento, os recursos devem ser limitados.

Um mapa de altura e um gráfico de quadros por segundo podem ser ativados no menu.

## Renderização

![Renderização do Cube Engine com texturas](http://i.imgur.com/Iz9IA.png)

A renderização é um algoritmo simples de pintor, tudo é desenhado de trás para frente, então os nós próximos à câmera são desenhados sobre os nós mais distantes. A tela não possui nenhum recurso de renderização 3D, o mecanismo usa técnicas de renderização 3D muito básicas. Algumas técnicas de otimização como back-face culling, occlusion culling e frustum culling foram implementadas. Octrees não são adaptados a este jogo e escala, pedaços são mais adequados.

Para tornar as coisas mais rápidas, uma distância de renderização menor pode ser selecionada.

O Canvas não suporta texturas, então a implementação de texturas deve ser feita do zero: um sistema de mapeamento de textura afim é usado. Renderizar com texturas torna o jogo visivelmente mais lento, então um renderizador simples, que usa cores simples, também está disponível.

As texturas são armazenadas em um arquivo _png_, o posicionamento da textura é exatamente o mesmo do Minecraft, então pode-se usar qualquer pacote de textura atual do Minecraft com este jogo.

## Salvando
Pode-se salvar localmente um jogo, isso armazena todos os nós em um pedaço de 3 por 3 (com o jogador no pedaço do meio) na memória local do navegador ou em um arquivo. Os dados podem ser carregados localmente, mas não de um arquivo (por motivos de segurança). Para carregar um mundo a partir de um arquivo, o programa deve ser executado a partir de um servidor.

## Problemas
O recorte de canto não é suportado, portanto, estar muito perto de um nó levará à sua remoção e será possível ver o que está do outro lado.

A maneira como o Javascript lida com números de ponto flutuante dificulta a obtenção de números inteiros exatos, algo em que o sistema de colisão depende. Isso foi resolvido "arredondando" os números quando perto de um número inteiro, mas não é uma solução muito elegante.

O Chrome tem alguns problemas para renderizar em cores simples, especificamente é a função `context.fill()` que não funciona quando chamada demais, parece.

O Firefox não permite que o navegador bloqueie o ponteiro a menos que esteja em modo de tela cheia, este programa nunca deve ser executado em tela cheia, a menos que seja em um super computador.

## licença
Lançado sob a [WTFPL](http://sam.zoy.org/wtfpl/COPYING). 
