## **Análise de Redes Complexas da Wikipedia**

---

## 👥 Integrantes 
- Juan Pablo
- Jucinara Melo
- Lucas Ferreira
- Pablo Arthur

---

## 🎥 Vídeo de Apresentação

---

## 🎯 Objetivo
Construir e analisar uma **rede de links da Wikipedia** a partir de **5 páginas-semente de áreas distintas**, explorando os links até **nível 2 (altura < 3)**, aplicando métricas de centralidade, análise de k-core/k-shell, detecção de comunidades e heurísticas de otimização.

O objetivo é compreender como diferentes áreas da ciência, tecnologia e sociedade se conectam dentro da estrutura de links da Wikipedia.

---

## 🗂️ Base de Dados
- Fonte: **Wikipedia**
- Páginas-semente utilizadas:
  - Python (programming language) — Tecnologia
  - COVID-19 — Saúde
  - Photosynthesis — Biologia
  - Energy crisis — Energia e Sociedade
  - Eclipse — Astronomia
- Estratégia:
  - Busca em largura (BFS)
  - Profundidade máxima: nível 2
  - Fusão das redes geradas a partir de cada seed em um único grafo

---

## ⚙️ Metodologia

### Construção do Grafo
- O grafo foi construído utilizando a biblioteca **NetworkX**
- Cada nó representa uma página da Wikipedia
- Cada aresta representa um link entre páginas
- O grafo final é a união das redes coletadas a partir das cinco páginas-semente

---

## Requisito 1 – Métricas de Centralidade (Gephi)
Foram geradas visualizações no **Gephi** a partir do grafo final, obedecendo aos seguintes critérios:

- Tamanho do vértice proporcional ao **degree (número de vizinhos)**
- Cores dos vértices baseadas em uma métrica de centralidade:
  - Closeness Centrality **OU**
  - Betweenness Centrality **OU**
  - Eigenvector Centrality
- Uso de layout apropriado (Force Atlas 2)

### Betweenness Centrality

<img width="764" height="790" alt="image" src="https://github.com/user-attachments/assets/9b9682b8-08af-456b-bb97-fe67674ff0cc" />

**Análise:**  
. A visualização baseada em *betweenness centrality* destaca os nós que atuam como **pontes entre diferentes regiões da rede**. Observa-se que poucos vértices concentram valores elevados dessa métrica, indicando páginas que conectam áreas distintas do conhecimento, como ciência, tecnologia e fenômenos naturais. Esses nós são fundamentais para a coesão global da rede, pois facilitam o fluxo de informação entre comunidades que, de outra forma, estariam fracamente conectadas.

---

### Closeness Centrality

<img width="756" height="796" alt="image" src="https://github.com/user-attachments/assets/515a8fc6-f737-402c-8e42-2a05d1b74c80" />

**Análise:**
A *closeness centrality* evidencia os nós que possuem **menor distância média em relação aos demais vértices da rede**. Na visualização, esses nós aparecem mais centrais espacialmente, indicando páginas que conseguem alcançar rapidamente grande parte da rede. Isso sugere que tais páginas representam conceitos amplos ou altamente referenciados dentro da Wikipedia.

---

### Degree Centrality

<img width="763" height="828" alt="image" src="https://github.com/user-attachments/assets/6efa7df1-b7fd-4907-a6ee-832ea19a58ae" />

**Análise:**  
A centralidade de grau (*degree centrality*) destaca os nós com **maior número de conexões diretas**. A figura evidencia a presença de hubs bem definidos, caracterizados por vértices maiores e altamente conectados. Esses nós correspondem a páginas muito referenciadas, exercendo forte influência na estrutura local da rede.

---

### Eigenvector Centrality

<img width="781" height="791" alt="image" src="https://github.com/user-attachments/assets/563554c2-ee9f-484b-ac46-b5cdc1921409" />

**Análise:**
A *eigenvector centrality* identifica nós que estão conectados a outros nós também altamente importantes. A visualização mostra um subconjunto de vértices com valores elevados dessa métrica, indicando páginas que ocupam posições estratégicas no núcleo da rede. Esses nós refletem a estrutura hierárquica da rede e representam centros de influência global.

---

## Requisito 2 – K-core e K-shell (Gephi)
Foi realizada a decomposição do grafo em **k-core** e **k-shell**, destacando a estrutura interna da rede.

- Tamanho dos vértices proporcional ao degree
- Destaque visual para o núcleo mais interno da rede
- Layout de livre escolha

<img width="960" height="696" alt="image" src="https://github.com/user-attachments/assets/ffaf1025-1391-40f7-aa6d-00cb67c819ff" />

**Análise:**
A visualização evidencia a decomposição da rede em **k-core** e **k-shell**, permitindo identificar sua estrutura interna. O núcleo mais interno (k-core), destacado na figura, concentra os nós mais densamente conectados, que desempenham papel central na sustentação da rede. Esses vértices apresentam alta conectividade mútua e são fundamentais para a robustez estrutural do grafo.

Os nós pertencentes aos k-shells externos aparecem mais dispersos e com menor número de conexões, representando áreas mais periféricas da rede. Essa diferenciação mostra claramente a hierarquia estrutural da rede, onde poucos nós formam um núcleo altamente conectado, enquanto a maioria ocupa posições mais periféricas.

---

## Requisito 3 – Comunidades (Rede em Produção)
A rede foi analisada em modo de produção, destacando suas comunidades:

- Comunidades detectadas pelo algoritmo **Louvain**
- Vértices coloridos de acordo com a comunidade
- Tamanho dos vértices proporcional ao degree

<img width="951" height="673" alt="image" src="https://github.com/user-attachments/assets/3ff6e3dc-6da7-42ff-ac06-b07708263d58" />

**Análise:**

A figura apresenta a rede em modo de produção, com os vértices coloridos de acordo com as **comunidades identificadas pelo algoritmo de Louvain**. Observa-se a formação de grupos bem definidos, cada um representando conjuntos de páginas mais densamente conectadas entre si, refletindo diferentes domínios do conhecimento presentes na rede.

As conexões entre comunidades indicam a existência de nós intermediários que atuam como pontos de ligação entre áreas distintas, evidenciando a natureza multidisciplinar da rede. Essa estrutura mostra como temas de ciência, tecnologia e fenômenos naturais se organizam em módulos, ao mesmo tempo em que permanecem interconectados dentro da Wikipedia.

---

## Requisito 4 – Heurística e Estrutura de Dados
A exploração da Wikipedia até o nível 2 gera alto custo computacional devido ao crescimento exponencial do número de páginas. Para tornar a coleta viável, foram adotadas as seguintes estratégias:

- Busca em largura (BFS) com controle de profundidade
- Uso de estruturas do tipo `set` para evitar revisitar páginas já processadas
- Limitação do número máximo de links explorados por página
- Filtro de páginas irrelevantes da Wikipedia (listas, identificadores e namespaces)
- Mesclagem incremental dos grafos gerados a partir de cada seed

Essas heurísticas reduzem significativamente a explosão do grafo, tornando a análise computacionalmente viável mesmo com seeds de áreas distintas.

---

## 📈 Análises Complementares

Além dos requisitos obrigatórios, foram realizadas análises complementares com o objetivo de aprofundar a compreensão da estrutura da rede:

- **Distribuição de grau da rede**, evidenciando a presença de poucos nós altamente conectados (hubs) e uma grande quantidade de nós com baixo grau, característica comum em redes complexas reais.
- **Comparação entre diferentes métricas de centralidade** (degree, closeness, betweenness e eigenvector), permitindo observar como cada métrica destaca papéis distintos dos vértices na rede, conforme apresentado nas visualizações do Requisito 1.
- **Identificação de nós intermediários**, que conectam diferentes comunidades e áreas temáticas, especialmente evidenciados pelas métricas de betweenness centrality e pela análise de comunidades.

Essas análises complementares reforçam a interpretação da rede como uma estrutura multidisciplinar, composta por módulos bem definidos e conectados por um conjunto reduzido de nós centrais, contribuindo para a compreensão da organização global da rede.

---

## 📌 Observações Finais

Os resultados apresentados dependem diretamente das páginas-semente escolhidas e das heurísticas adotadas durante o processo de coleta. Alterações nos parâmetros de profundidade, no limite de links explorados por página ou na escolha das seeds podem resultar em redes com estruturas significativamente diferentes.

Além disso, a Wikipedia é uma base de dados dinâmica, estando sujeita a atualizações constantes, o que pode ocasionar pequenas variações nos grafos obtidos ao longo do tempo. Apesar dessas limitações, a metodologia empregada mostrou-se adequada para a análise estrutural de redes reais, permitindo a extração de padrões relevantes por meio de métricas de centralidade, decomposição em k-core e detecção de comunidades.

Por fim, o trabalho evidencia a importância do uso de grafos e técnicas de redes complexas como ferramentas eficazes para a análise e interpretação de sistemas complexos e interconectados.










