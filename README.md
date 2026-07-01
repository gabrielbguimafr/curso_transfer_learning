# curso_transfer_learning
Esse repositório público foi feito para fazer a entrega de um dos desafios do curso da bairesdev de machine learning.
Esta atividade compreende o treinamento de uma rede neural para a identificação de gatos e cachorros utilizando os conceitos apresentados no curso. Eu utilizei um notebook do google colab que foi disponibilizado com um código base e as explicações, a partir desse notebook eu trabalhei para adicionar a base de dados e fazer as modificações necessárias para realizar o treinamento e a extração dos pesos para fazer o transferlearning. A estruturação do repositório é bem simples, havendo somente o notebook e este readme com as explicações do que foi feito.

Nas primeira células há a importação das bibliotecas necessárias para a realização da tarefa, o google colab já possuí elas todas instaladas não havendo a necessidade de instalá-las uma por uma.
Logo abaixo temos o download do banco de dados "cat and dogs" recomendado do site tensorflow.
Indo para a terceira há a separação do dataset para treino e para avaliação e categorização das imagens que vem em duas pastas, uma para os gatos e outra para os cachorros.
Na quarta há uma função que ajuda a carregar a imagem em um vetor de entrada.
A partir disso há o carregamento das imagens para formar o dataset, onde vai ser randomizado, como foi ensinado pelo curso e a criação dos testes, validações e treino. Divididos em 70-15-15, porcentagem. Há a separação dos dados para a etiquetagem.
Abaixo bem o pré-processamento dos dados, a normalização é extremamente importante pois permite a regularização dos dados e a estimativa através do processo estatístico.

Indo para a segunda etapa:
As imagens são carregadas nas três categorias supracitadas, aonde temos treino, valor e teste. O formato dos dados de treino é (n,224,224,3), n é o tamango do conjunto de treino, 224 são os redimensionamentos para 225 pixels de altura e largura com 3 canais que são os de cores R,G,B. Com duas classes, tendo 2800 imagens em 2 classes.
Começando o treinamento do zero, utilizando redes covolucionais e maxpooling que são técnicas para destacar os contornos da imagem, reduzindo o tamanho, ajudando a economizar memória e ignorando ruídos.
Seguindo com o treino usando 100 épocas com um tamanho de batch de 128, após isso plotamos e observamos onde começa a estabilização e um possível overfitting, quando uma rede neural se adapta a um dataset de maneira que tem uma reação parecida com decorar.
Avaliamos a perda e a precisão da rede dentro do nosso dataset de teste.

Seguindo para a terceira etapa, transfer learning:
Usando o VGG16 do Keras que é treinado no ImageNet, observamos o sumário dos pesos do imagenet.
Após isso, criamos um input layer de referência, uma nova camada de classificação, conectamos com a pernúltimo camanada do VGG e criamos uma nova rede definindo entrada e saída, nomeada como new_model.
Fazendo o congelamento dos pesos com excessão da última camada de neurônios reduz a quantidade de parâmetros para treino, tornando menos custoso o treino e mantendo a qualidade. A partir disso, usando agora esses hiperparâmetros realizamos treinos com o mesmo batch_size e epochs que o treino anterior e analisamos os resultados. É notável a melhora significativa para o nosso primeiro modelo, de 0.76% de taxa de acerto para 0.94, há um gráfico com ambos os dados plotados também e ao final adicionei células para conseguir baixar os pesos do modelo treinado. 
