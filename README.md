# FarmTech Solutions — Visão Computacional

## 📌 Sobre o projeto

Este projeto foi desenvolvido durante a **Fase 6 do curso de Inteligência Artificial da FIAP**, com o objetivo de explorar diferentes abordagens de Visão Computacional.

Foram utilizadas imagens de duas classes distintas:

- 🚗 **Carro**
- 👟 **Tênis**

O projeto busca avaliar o comportamento de diferentes modelos na identificação e classificação desses objetos, analisando não apenas a precisão obtida, mas também as diferenças de treinamento, capacidade de generalização e limitações encontradas durante os testes.

---

## 🎯 Objetivos

O projeto foi dividido em experimentos utilizando diferentes abordagens de Visão Computacional:

1. Treinamento de um modelo YOLO utilizando **80 épocas**;
2. Segundo treinamento utilizando **40 épocas**, permitindo comparar o impacto da quantidade de épocas;
3. Treinamento de uma **CNN (Convolutional Neural Network) do zero** para classificação das imagens;
4. Comparação dos resultados obtidos pelas diferentes abordagens.

---

## 📂 Dataset

O conjunto de dados foi construído utilizando imagens das classes **carro** e **tênis**.

As imagens foram separadas entre conjuntos destinados ao treinamento, validação e teste dos modelos.

Durante a construção do dataset, foi observada uma diferença importante entre as classes. Nas imagens de carros, normalmente havia apenas um objeto principal por imagem. Já algumas imagens de tênis apresentavam vários tênis simultaneamente.

Essa diferença pode ter influenciado os resultados, pois imagens contendo múltiplos objetos tornam a tarefa de localização mais complexa.

---

# 🚀 Treinamento YOLO — 80 épocas

O primeiro treinamento foi realizado utilizando **80 épocas**.

### Resultados gerais

| Métrica | Resultado |
|---|---:|
| Precision | **95,4%** |
| Recall | **96,9%** |
| mAP50 | **95,2%** |
| mAP50-95 | **82,6%** |

### Resultados por classe

| Classe | Precision | Recall | mAP50 | mAP50-95 |
|---|---:|---:|---:|---:|
| Carro | 97,6% | 100% | 99,5% | 91,5% |
| Tênis | 93,2% | 93,8% | 91,0% | 73,6% |

O modelo apresentou resultados elevados, principalmente para a classe **carro**.

O Recall de **100% para carros** demonstra que todos os carros presentes no conjunto avaliado foram detectados pelo modelo.

A classe tênis também apresentou bons resultados, porém inferiores aos obtidos para carros. Uma possível explicação observada durante o desenvolvimento foi a maior complexidade das imagens dessa classe, já que diversas imagens possuíam múltiplos tênis.

Nos testes visuais realizados com esse modelo, os objetos presentes nas imagens avaliadas foram identificados corretamente.

O treinamento levou aproximadamente **4 horas**, considerando o ambiente utilizado durante a execução. Esse tempo é aproximado e não foi obtido por uma medição formal de benchmark.

---

# ⚙️ Treinamento YOLO — 40 épocas

Para analisar o impacto da quantidade de épocas, foi realizado um segundo treinamento utilizando **40 épocas**.

### Resultados gerais

| Métrica | Resultado |
|---|---:|
| Precision | **91,0%** |
| Recall | **93,2%** |
| mAP50 | **94,0%** |
| mAP50-95 | **79,8%** |

### Resultados por classe

| Classe | Precision | Recall | mAP50 | mAP50-95 |
|---|---:|---:|---:|---:|
| Carro | 94,6% | 100% | 99,5% | 91,0% |
| Tênis | 87,4% | 86,5% | 88,5% | 68,6% |

O treinamento com 40 épocas apresentou uma redução de desempenho em comparação com o treinamento de 80 épocas.

A diferença ficou particularmente evidente na classe **tênis**, cujo Recall caiu de **93,8% para 86,5%** e o mAP50-95 caiu de **73,6% para 68,6%**.

Nos testes visuais, o modelo conseguiu reconhecer carros e tênis, porém em algumas imagens contendo vários tênis ele deixou de detectar alguns dos objetos presentes.

O treinamento levou aproximadamente **1 hora e 30 minutos a 2 horas**, sendo novamente um valor aproximado observado durante a execução.

---

# 📊 Comparação — 40 vs. 80 épocas

| Métrica | 40 épocas | 80 épocas |
|---|---:|---:|
| Precision | 91,0% | **95,4%** |
| Recall | 93,2% | **96,9%** |
| mAP50 | 94,0% | **95,2%** |
| mAP50-95 | 79,8% | **82,6%** |
| Tempo aproximado | 1h30–2h | ~4h |

Os resultados demonstram que, neste experimento, aumentar o treinamento de **40 para 80 épocas trouxe melhoria nas principais métricas avaliadas**.

O modelo de 80 épocas apresentou maior Precision, Recall e mAP, além de melhor desempenho nos testes visuais.

Durante a análise das curvas de treinamento, foi observado que o modelo de 80 épocas já se aproximava de uma estabilização da curva de aprendizado. Isso sugere que o treinamento adicional permitiu maior convergência do modelo dentro da configuração utilizada.

Entretanto, o ganho de desempenho teve como custo um aumento considerável no tempo de treinamento.

---

# 🧠 CNN treinada do zero

Além dos experimentos utilizando YOLO, foi desenvolvida uma **Rede Neural Convolucional (CNN)** treinada do zero para realizar a classificação das imagens.

### Resultado

| Métrica | Resultado |
|---|---:|
| Accuracy | **80,95%** |
| Loss | **0,4781** |

A CNN atingiu aproximadamente **81% de acurácia** no conjunto avaliado.

Durante os testes com novas imagens, foram observadas algumas classificações incorretas, apresentando desempenho inferior ao obtido com o YOLO nos experimentos realizados.

É importante destacar que algumas imagens utilizadas para avaliar a CNN foram diferentes das utilizadas nos testes do YOLO. Portanto, a comparação visual entre os modelos deve ser interpretada considerando essa diferença.

Em um dos testes, por exemplo, foi utilizada uma imagem de uma pessoa utilizando tênis, permitindo verificar se a CNN conseguiria identificar a classe mesmo em um cenário diferente das imagens mais simples utilizadas durante o desenvolvimento.

Uma possível limitação da CNN foi a quantidade relativamente pequena de imagens disponível para que uma rede treinada do zero aprendesse características suficientemente generalizáveis das duas classes.

Uma abordagem futura possível seria utilizar **Transfer Learning**, aproveitando características visuais previamente aprendidas por uma rede treinada em um dataset maior. Entretanto, seria necessário realizar novos experimentos para determinar se essa abordagem apresentaria desempenho superior ao YOLO neste problema.

---

# 🔎 Comparação das abordagens

Os experimentos mostraram diferenças importantes entre as abordagens utilizadas.

| Característica | YOLO 40 épocas | YOLO 80 épocas | CNN do zero |
|---|---|---|---|
| Desempenho observado | Alto | **Melhor resultado** | Inferior ao YOLO |
| Precision geral | 91,0% | **95,4%** | — |
| Recall geral | 93,2% | **96,9%** | — |
| mAP50 | 94,0% | **95,2%** | — |
| Accuracy | — | — | **80,95%** |
| Tempo de treinamento | ~1h30–2h | ~4h | Menor que o YOLO nos experimentos |
| Múltiplos objetos | Sim | Sim | Classificação da imagem |
| Resultado nos testes | Bom | **Melhor** | Alguns erros de classificação |

As métricas de YOLO e CNN possuem objetivos diferentes e, portanto, não devem ser interpretadas como equivalentes diretamente. Enquanto o YOLO realiza **detecção de objetos**, identificando também a localização dos objetos na imagem, a CNN desenvolvida realiza **classificação da imagem**.

Mesmo considerando essa diferença, os testes realizados mostraram que o YOLO apresentou resultados mais consistentes para o conjunto de dados utilizado.

---

# 💡 Principais conclusões

A quantidade de épocas teve impacto direto no desempenho do YOLO neste experimento.

O treinamento com **80 épocas apresentou o melhor resultado**, alcançando Precision de **95,4%**, Recall de **96,9%** e mAP50 de **95,2%**.

A classe **carro** apresentou desempenho superior à classe tênis. Uma possível influência foi a composição das imagens utilizadas no dataset: as imagens de carro geralmente possuíam apenas um objeto principal, enquanto diversas imagens de tênis apresentavam múltiplos objetos.

O treinamento com **40 épocas** apresentou resultados bons, porém inferiores ao modelo de 80 épocas, principalmente na detecção de tênis.

A **CNN treinada do zero** atingiu aproximadamente **81% de acurácia**, porém apresentou mais erros durante os testes realizados. A quantidade limitada de dados pode ter dificultado o aprendizado de características mais generalizáveis.

Dessa forma, entre as abordagens avaliadas, o **YOLO treinado por 80 épocas apresentou o melhor desempenho geral**, embora também tenha exigido maior tempo de treinamento.

---

# ⚠️ Limitações

Durante o desenvolvimento foram identificadas algumas limitações:

- Quantidade relativamente pequena de imagens disponíveis para treinamento;
- Diferenças na quantidade de objetos presentes nas imagens de cada classe;
- Algumas imagens de teste da CNN foram diferentes das utilizadas na avaliação do YOLO;
- Os tempos de treinamento apresentados são aproximados e não foram obtidos através de benchmark controlado;
- Um dataset maior e mais diversificado poderia fornecer uma avaliação mais robusta da capacidade de generalização dos modelos.

---

# 📓 Notebook / Google Colab

Todo o processo de preparação dos dados, treinamento, validação, testes e análise dos resultados está documentado no notebook do projeto.

**Acessar o notebook:**  
`[INSERIR LINK DO COLAB AQUI]`

---

# 🎥 Vídeo demonstrativo

Foi produzido um vídeo demonstrando o funcionamento da solução e os principais resultados encontrados durante o desenvolvimento.

**YouTube — vídeo não listado:**  
`[INSERIR LINK DO VÍDEO AQUI]`

---

## 👨‍💻 Autor

**Gustavo [SOBRENOME]**  
**RM:** [SEU RM]

Projeto desenvolvido para a **FIAP — Inteligência Artificial — Fase 6**.
