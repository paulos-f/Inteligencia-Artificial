# 🌲 Algoritmo de Busca em Profundidade (DFS)

Executamos aqui o algoritmo de **Busca em Profundidade (Depth-First Search)** no grafo de bairros de Florianópolis, partindo do nó **Centro**, com o objetivo de encontrar o bairro **Campeche**.

---

## 🗺️ Estrutura do Grafo

```
Centro
├── Saco dos Limões
│   ├── Trindade
│   └── Costeira
│       ├── Aeroporto
│       └── Campeche ✅
└── Agronômica
    └── Cacupé
        ├── Sambaqui
        ├── Canasvieiras
        │   └── Ingleses
        └── Jurerê
```

---

## 🧠 Lógica da DFS

A DFS visita o primeiro filho de cada nó até alcançar o nó mais profundo possível antes de voltar e continuar a busca em outros ramos. Ela **desce primeiro**, explora, e **só depois volta**.

---

## 📋 Pseudocódigo Formatado

```plaintext
1: escolha uma raiz s de G: Centro
2: marque Centro
3: se Centro = Campeche então
4:     retorna Centro
5: para cada v ∈ listaDeAdjacência de Centro faça
6:     se v não está marcado então
7:         chame DFS(v)
8: fim para
```

---

## 🧭 Caminho Percorrido

A busca em profundidade segue o seguinte trajeto até encontrar o **Campeche**:

```
Centro
→ Saco dos Limões
→ Trindade
← volta
→ Costeira
→ Aeroporto
← volta
→ Campeche ✅ (encontrado)
```
---
### Representação do grafo como dicionário de adjacência
    grafo = {
        "CENTRO": ["SACO DOS LIMÕES", "AGRONÔMICA"],
        "SACO DOS LIMÕES": ["TRINDADE", "COSTEIRA"],
        "AGRONÔMICA": ["JOÃO PAULO", "SANTA MÔNICA"],
        "TRINDADE": ["CÓRREGO GRANDE"],
        "COSTEIRA": ["CAMPECHE"],
        "JOÃO PAULO": ["ITACORUBI"],
        "SANTA MÔNICA": [],
        "CÓRREGO GRANDE": ["PANTANAL"],
        "PANTANAL": [],
        "ITACORUBI": [],
        "CAMPECHE": []
    }
    
    def dfs(inicio, objetivo, visitados=None, caminho=None):
        if visitados is None:
            visitados = set()
        if caminho is None:
            caminho = []
    
        visitados.add(inicio)
        caminho.append(inicio)
    
        if inicio == objetivo:
            print("Caminho encontrado:", " -> ".join(caminho))
            return caminho
    
        for vizinho in grafo.get(inicio, []):
            if vizinho not in visitados:
                resultado = dfs(vizinho, objetivo, visitados, caminho)
                if resultado:
                    return resultado
    
        caminho.pop()
        return None

# Executando a busca
dfs("CENTRO", "CAMPECHE")

---

## 🖼️ Representação Visual

Aqui está a imagem representando a estrutura e o caminho da DFS até o nó "Campeche":

![DFS até Campeche](https://storage.satc.edu.br/arquivos/docentes/4479/20251/files/IA/Campeche.png)  

---

✅ *A busca foi concluída com sucesso no nó "Campeche", respeitando a ordem de profundidade.*
