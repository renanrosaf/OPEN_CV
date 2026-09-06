# OPEN_CV
Repositório para exercitar git e pré-processamento de imagens utilizando o Open CV

# EXERCÍCIO 1:

## Contexto: 

Você foi contratado como engenheiro de visão computacional por uma fábrica de montagem eletrônica. A empresa possui uma esteira onde uma câmera fotografa bandejas retangulares contendo diferentes componentes (como porcas, parafusos e arruelas) que precisam ser contados e separados.
O problema é que a câmera foi instalada em um ângulo inclinado devido à falta de espaço no teto, deixando a bandeja distorcida na foto. Além disso, a iluminação da fábrica causa reflexos e sombras, gerando ruídos na imagem.
Objetivo: Criar um script em Python usando OpenCV que corrija a perspectiva da bandeja, limpe os ruídos da imagem, identifique cada peça individualmente e salve uma foto separada de cada uma delas para o banco de dados da fábrica

## Tarefas do Exercício:

1. Leitura e Padronização:

-Leia a imagem original do disco.

-Redimensione a imagem para um tamanho padrão (por exemplo, 800x600) para facilitar o processamento.

2. Correção de Perspectiva (Envelopamento):

-Defina os 4 pontos de origem (os cantos distorcidos da bandeja na foto) e os 4 pontos de destino (os cantos de um retângulo perfeito).

-Utilize as funções matemáticas do OpenCV para realizar o warp perspective (envelopamento), gerando uma nova imagem onde a bandeja aparece perfeitamente vista de cima.

3. Pré-processamento e Mudança de Cor:

-Converta a imagem "envelopada" de BGR para Tons de Cinza.

-Aplique um desfoque (Blur) e um limiar (Threshold) ou Canny para criar uma máscara binária (fundo preto e objetos brancos).

4. Operações Morfológicas:

-A máscara gerada provavelmente terá ruídos (pontos brancos isolados) e falhas dentro das peças (buracos pretos).

-Utilize operações de Abertura (Opening) para remover os ruídos externos.

-Utilize operações de Fechamento (Closing) para preencher os buracos dentro dos componentes.

5. Separação de Objetos e Gravação:

-Encontre os contornos das peças na máscara morfológica.

-Para cada peça encontrada, desenhe um retângulo delimitador (Bounding Box) na imagem cinza original (para visualização).

-Recorte (crop) a região de cada peça usando as coordenadas do retângulo.

-Salve cada recorte como um arquivo de imagem individual (ex: peca_1.jpg, peca_2.jpg) em uma pasta específica.

# EXERCÍCIO 2

## Contexto: 
Você atua na equipe de inovação de um laboratório farmacêutico. O laboratório possui uma etapa onde os comprimidos recém-fabricados são colocados sobre uma bandeja retangular para inspeção visual automatizada.Recentemente, o braço robótico que segura a câmera sofreu um leve desvio, fazendo com que as fotos das bandejas saiam com distorção de perspectiva (tortas). Além disso, o pó dos próprios medicamentos cria ruídos brancos na bandeja, e os reflexos da luz criam falsos buracos nos comprimidos.
Objetivo: Desenvolver um script capaz de alinhar a bandeja virtualmente, isolar os comprimidos do fundo, limpar os ruídos (pó e reflexos) e salvar a imagem individual de cada comprimido para que uma futura IA possa classificar se estão perfeitos ou lascados.

## Tarefas Exigidas

1. Leitura e Redimensionamento: 

- Carregue a imagem e redimensione-a para proporções menores (ex: 800x600) para otimizar o tempo de processamento.

2. Envelopamento (Correção de Perspectiva): 

-Isole a bandeja definindo os 4 cantos da imagem distorcida e aplique a transformação matemática para gerar uma visão perfeitamente vertical (planta baixa).

3- Conversão de Cor e Binarização: 

-Converta a imagem alinhada para tons de cinza e crie uma máscara binária onde os comprimidos fiquem brancos e o fundo da bandeja fique preto.

4- Operações Morfológicas:

-Aplique uma Abertura (Opening) para eliminar os ruídos gerados pelo pó do medicamento espalhado na bandeja.
-Aplique um Fechamento (Closing) para preencher eventuais buracos ou falhas causadas por reflexos de luz sobre as pílulas.

5- Separação e Gravação: 

Encontre os contornos na máscara morfológica, desenhe um retângulo de destaque ao redor de cada comprimido, recorte-os da imagem colorida corrigida e grave (salve) cada um em uma pasta local.

# EXERCÍCIO 3: Processamento em lote (btach processing)

## Contexto
Você foi contratado como Engenheiro(a) de Visão Computacional na
FinTrack, uma empresa focada em automação financeira. O sistema principal da empresa lê notas fiscais
escaneadas (dataset SROIE v2) para realizar reembolsos automáticos utilizando OCR (Reconhecimento
Óptico de Caracteres).
No entanto, o motor de OCR está falhando porque as imagens chegam com iluminação irregular, sombras e
ruídos.
Sua Missão: Construir um pipeline de pré-processamento de imagens focado em limpar e corrigir uma nota
fiscal, utilizando Python e a biblioteca OpenCV, garantindo que o texto fique perfeitamente legível para o motor
de extração de dados.

## Roteiro de Desenvolvimento (Passo a Passo)

Para resolver este problema e entregar uma imagem otimizada para o OCR, siga as etapas abaixo em seu script. Procure escrever um código
limpo e estruturado (utilizando funções ou classes).

● Passo 1: Preparação e Leitura Importe a biblioteca OpenCV (cv2) e utilize a função cv2.imread() para carregar uma imagem de
teste do dataset de notas fiscais para a memória.

● Passo 2: Validação de Segurança Sistemas de produção lidam frequentemente com arquivos corrompidos ou caminhos inválidos.
Implemente uma validação simples (verificando se a variável da imagem lida é None) para que o seu código exiba uma mensagem de
erro clara e amigável em vez de quebrar inesperadamente.

● Passo 3: Simplificação dos Dados (Escala de Cinza) Motores de OCR operam identificando contrastes geométricos, não cores.
Pesquise e aplique a função do OpenCV capaz de converter a matriz da imagem do padrão BGR para Escala de Cinza. Isso reduzirá
drasticamente o peso do processamento.

● Passo 4: Tratamento de Ruídos (Suavização) Scanners e câmeras de celular costumam adicionar granulações à imagem que o OCR
pode confundir com vírgulas ou pontos. Aplique um filtro de suavização gaussiana (cv2.GaussianBlur()). Dica: Teste um tamanho de
kernel ímpar pequeno, como (5, 5), para limpar as impurezas do papel sem embaçar as letras.

● Passo 5: O Coração do Problema (Correção de Iluminação) Notas fiscais quase sempre possuem gradientes de luz (o clarão do flash
de um lado e a sombra da mão do outro). Se você utilizar um limiar de corte global simples, a área com sombra se tornará uma mancha
preta ilegível. Sua tarefa é pesquisar e aplicar a Limiarização Adaptativa (cv2.adaptiveThreshold()). Ajuste os parâmetros para
que o algoritmo calcule o contraste baseado na vizinhança local dos pixels, garantindo um texto nítido tanto na luz quanto na escuridão.

● Passo 6: Exportação do Resultado Utilize a função cv2.imwrite() para salvar a imagem final processada no seu diretório de saída.
Atenção: Salve obrigatoriamente no formato .png. Como este formato possui compressão sem perdas, ele preservará as bordas das
letras intactas para a leitura do OCR.

### Automatização do script

A FinTrack recebe milhares de notas digitalizadas por dia. Alterar o código manualmente para cada imagem é inviável. Você deve
automatizar o script para processar uma pasta inteira imagem por imagem (de forma sequencial e não concorrente).

● Passo 7: Reestruturação (Refatoração) Encapsule a lógica de tratamento visual construída na Fase 1 dentro de uma
função isolada ou estruture-a dentro de uma Classe.

● Passo 8: Mapeamento e Filtragem do Diretório Utilize bibliotecas nativas como os ou pathlib para ler a pasta de
imagens brutas. Implemente uma validação que garanta que a sua lista de trabalho contenha apenas arquivos que terminem
com extensões de imagem válidas (como .jpg ou .png), ignorando arquivos de sistema.

● Passo 9: O Loop de Automação Crie um laço de repetição (for) que itere sobre a sua lista de imagens. Para cada
imagem, o código deve:
1. Construir dinamicamente o caminho de leitura.
2. Construir dinamicamente o caminho de salvamento, forçando a conversão da extensão para .png.
3. Acionar a sua função de processamento.