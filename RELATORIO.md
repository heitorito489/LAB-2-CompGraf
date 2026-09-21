# Relatório - Coelinhos do Brasil

> [!CAUTION]
> - Lembre-se que você <ins>**não pode utilizar ferramentas de IA para
>   escrever este relatório**</ins>

## Dados do aluno

- **Cartão UFRGS**: <mark>`<00601416>`</mark>
- **Nome**: <mark>`<Heitor Lima Pedroso>`</mark>

## Passos que eu segui para resolver o problema especificado (em formato de *"prompt"*)

> [!IMPORTANT]
> - Coloque aqui todas as informações necessárias para que alguém
>   (pessoa ou ferramenta de IA) possa reproduzir os seus passos para
>   solucionar o problema
> - Escreva em formato imperativo, como se fosse um *prompt* com as
>   instruções a serem seguidas na solução do problema
> - Seja objetivo e conciso: quanto *menos palavras* você utilizar,
>   melhor
> - Seja técnico e use terminologia adequada: assuma que quem irá ler
>   os seus passos possui conhecimento de Ciência da Computação e
>   Computação Gráfica
> - Caso você queira incluir informações "longas" (como algum *prompt*
>   grande usado com alguma ferramenta de IA), crie arquivos à parte e
>   adicione links no texto (por exemplo, crie o arquivo `PROMPTS.md`
>   e adicione um link markdown `[os prompts detalhados estão
>   aqui](PROMPTS.md)`)
> - Novamente, lembre-se que você *não pode utilizar ferramentas
>   de IA para escrever este relatório*

<mark>`< 1. Configure a janela e limpe a cena inicial:
Altere o título da janela no "glfwCreateWindow" para o formato exigido.
Remova a esfera e os três coelhos do template dentro do laço principal de renderização, mantendo apenas o plano do chão ("the_plane").

2. Distribua a geometria dos três conjuntos e ajuste a escala
Dimensione o plano do chão para 15 x 15 e expanda o "farplane" da projeção perspectiva para -50 para evitar cortes de visão com o afastamento da câmera.
Aplique uma matriz de escala uniforme S(0.4, 0.4, 0.4) em todos os coelhos para evitar sobreposições e ajustar o tamanho visual.
Posicione as três geometrias concêntricas: 24 coelhos no retângulo externo verde (8 no topo, 4 na direita, 8 na base e 4 na esquerda), 14 coelhos no losango intermediário amarelo e 8 coelhos no círculo central azul.

3. Calibre as rotações locais em Y para o sentido horário
Identifique o vetor frontal nativo do modelo ("bunny.obj"), que aponta originalmente para -X.
Ajuste as matrizes de rotação no eixo Y (Ry) de cada aresta e segmento para garantir que todos os coelhos fiquem virados no sentido horário da trajetória fechada.

4. Parametrize a translação contínua e sincronize o período de volta
Substitua os laços estáticos por variáveis de perímetro contínuas usando fmod e a função de tempo glfwGetTime().
Fixe uma constante de período global em 12 segundos. Calcule as velocidades específicas de cada conjunto dividindo o comprimento de cada percurso por esse período, garantindo ciclos sincronizados.

5. Implemente a cinemática do salto com repouso e contato com o chão
Crie uma função para a altura Y baseada em meia-onda de seno com altura máxima de 0.35 unidades.
Adicione zonas de arrasto/repouso no solo nos primeiros e últimos 20% do comprimento de cada aresta, deixando o salto ativo apenas no intervalo intermediário.
No anel azul, divida a volta completa em 4 saltos de 90 graus cada.
Fixe a altura base em Y=-0.65 para que as patas toquem o plano do chão em repouso.

6. Interpole a rotação nas quinas
Crie uma função de interpolação "LerpAngle" que calcula o menor caminho no círculo trigonométrico entre a aresta atual e a próxima.
Acione a interpolação exclusivamente durante os 20% finais de cada aresta (enquanto o coelho está no chão após o pouso), suavizando a rotação de 90 graus antes de iniciar a aresta seguinte.

7. Modele a boina no modelo do coelho
Renderize a esfera achatada S(0.4, 0.15, 0.4) com o material vermelho "RED_VELVET_SURFACE" acoplada diretamente à matriz de modelo de cada coelho Mboina = Mbunny . T . S
Calibre o deslocamento local da esfera para (-0.45, 0.58, -0.09), assentando a boina na cabeça entre as orelhas.

8. Ajuste fino de proporções e dimensões
Expanda a meia-largura X do losango amarelo para Wy = 3 para aproximar as pontas laterais do retângulo verde.
Ajuste o raio do círculo azul para Rb = 1.15, equilibrando os espaços vazios e concluindo a semelhança visual com o vídeo de referência. >`</mark>

## Principais dificuldades encontradas durante o desenvolvimento (formato livre)

<mark>`< Minhas principais dificuldades encontradas durante o desenvolvimento do trabalho foram: 
1. A orientação e referencial do modelo 3D: o coelho possui o vetor frontal voltado originalmente para -X, o que gerou uma série de confusões iniciais nas rotações no eixo Y. Precisei mapear manualmente os ângulos das arestas para garantir que todos seguissem o sentido horário sem andar de lado ou de ré.
2. Calibração da altura de contato com o solo: o centro de origem do modelo do coelho fica no meio do seu corpo e não na base das patas. Por isso, fixar a altura em 0 deixava o coelho flutuando, enquanto colocar na altura do chão (-1.0) fazia ele afundar durante a descida do salto. Precisei calibrar a altura base empiricamente em Y = -0.65 para que as patas ficassem na altura do plano na inicialização e nos momentos entre os saltos
3.Rotação suave nas quinas do percurso: a transição entre as arestas provocava uma virada brusca de 90 graus. A solução (sugerida por IA e implementada com boa ajuda) foi criar uma interpolação angular combinada com as fases de arrasto no solo, fazendo o coelho girar o corpo aos poucos durante os últimos 20% da aresta antes de iniciar o próximo salto.
*Observação: também tive desafios com o ajuste da boina, que no processo de ajustar os eixos X, Y e Z locais exigiu várias tentativas para não deixar que ela ficasse voando nas orelhas dos coelhos ou torta. A sincronização dos ciclos, apesar dos tamanhos diferentes dos polígonos, também demorou até que ficasse 100% correta. E por fim, solucionar a câmera para enquadrar toda a cena demorou, apesar de não ter sido difícil realmente. >`</mark>

## Você acha que conseguiu resolver o problema de forma adequada?

<mark>`< Creio que sim. >`</mark>

## Se você quiser compartilhar mais alguma coisa, coloque aqui:

<mark>`< Acho válido mencionar aqui que utilizei o Gemini ostensivamente durante o trabalho para me ajudar com a organização do código e sintaxe. Frequentemente precisei de ajuda na implementação das minhas ideias para código, mas não pedi sugestões de como fazer em nenhuma etapa (salvo na mencionada da transição entre as arestas dos coelhos). >`</mark>

## Se você possui alguma sugestão para o professor sobre esta atividade, coloque aqui:

<mark>`< Acredito que se o vídeo do resultado esperado mostrasse diferentes ângulos o trabalho poderia ter sido mais fácil, principalmente no que toca o ajuste da boina dos coelhos, altura em relação ao plano e outros ajustes semelhantes. >`</mark>
