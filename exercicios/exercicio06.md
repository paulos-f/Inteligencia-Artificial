### Código arrumado:
---
    
    def busca_gulosa(nos, heuristicas, arestas, inicio, objetivo):
        visitados = [False] * len(nos)
        caminho = []
    
        atual = inicio
        caminho.append(atual)
        visitados[atual] = True
    
        while atual != objetivo:
            vizinhos = []
            
            # Encontra os vizinhos do nó atual que ainda não foram visitados
            for (origem, destino, custo) in arestas:
                if origem == atual and not visitados[destino]:
                    vizinhos.append(destino)
    
            if not vizinhos:
                print("Caminho não encontrado!")
                return
            
            # Escolhe o vizinho com a menor heurística
            proximo = min(vizinhos, key=lambda x: heuristicas[x])
    
            atual = proximo
            caminho.append(atual)
            visitados[atual] = True
    
        print("Caminho encontrado:", " -> ".join(map(str, caminho)))
    
    # Definição dos nós e heurísticas
    nos = [0, 1, 2, 3, 4, 5]
    heuristicas = [7, 6, 2, 1, 0, 3]
    
    # Definição das arestas com custos
    arestas = [(0, 1, 1), (0, 2, 4), (1, 3, 2), (2, 4, 5), (3, 4, 1),
               (3, 5, 3), (4, 5, 2), (5, 4, 3)]
    
    inicio = 0
    objetivo = 4
    busca_gulosa(nos, heuristicas, arestas, inicio, objetivo)

----

### Saída:

    Caminho encontrado: 0 -> 2 -> 4
---

### 🧠 Explicação:

- O algoritmo sempre escolhe o **vizinho com menor valor de heurística** (h(n)).
- Ele para ao encontrar o **nó objetivo**.
- Nós visitados são marcados para evitar ciclos.

---
