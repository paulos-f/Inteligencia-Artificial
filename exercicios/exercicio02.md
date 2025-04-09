
# 🔍 Algoritmo de Busca em Largura (BFS)

Este é um exemplo de aplicação do algoritmo de **Busca em Largura (Breadth-First Search)** em um grafo representando bairros de Florianópolis. O objetivo é encontrar o bairro **Cacupé**, iniciando a busca a partir do bairro **Centro**.


## 🗺️ Grafo Resumido (Conexões)

```
Centro
├── Saco dos Limões
│   ├── Trindade
│   └── Costeira
│       ├── Aeroporto
│       └── Campeche
└── Agronômica
    └── Cacupé
        ├── Sambaqui
        ├── Canasvieiras
        │   └── Ingleses
        └── Jurerê
```

---

## 🔁 Pseudocódigo da Busca em Largura

```plaintext
1: escolha uma raiz s de G: Centro
2: marque Centro
3: insira Centro em F
4: enquanto F não está vazia faça
5:     seja v o primeiro vértice de F
6:     para cada w ∈ listaDeAdjacência de v faça
7:         se w não está marcado então
8:             marque w
9:             se w = Cacupé então
10:                retorna w
11:            fim se
12:            insira w em F
13:        fim se
14:    fim para
15:    retira v de F
16: fim enquanto
17: retorna nulo
```

---

## ✅ Resultado da Execução

Durante a execução, os nós são visitados na seguinte ordem:

```
Centro → Saco dos Limões, Agronômica → Cacupé ✅
```

O algoritmo encontra **Cacupé** ao explorar os vizinhos de **Agronômica**, garantindo o menor caminho possível.

---

📌 *Esse pseudocódigo segue a lógica clássica de BFS, usando uma fila (F) e marcações para evitar visitar o mesmo nó mais de uma vez.*
```
