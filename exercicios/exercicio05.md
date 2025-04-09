----

- **Busca Gulosa** → leva em conta apenas a **distância em linha reta** (heurística h(n)).
- **Busca A\*** → leva em conta a **distância acumulada até o nó atual** (g(n)) + **a heurística** (h(n)).

---

## 🔍 Informações úteis da imagem:

### 🧭 Heurística (h(n)) – Distância em linha reta até Bucharest:

| Cidade         | h(n) (para Bucharest) |
|----------------|------------------------|
| Arad           | 366                    |
| Bucharest      | 0                      |
| Craiova        | 160                    |
| Dobreta        | 242                    |
| Eforie         | 161                    |
| Fagaras        | 178                    |
| Giurgiu        | 77                     |
| Hirsova        | 151                    |
| Iasi           | 226                    |
| Lugoj          | 244                    |
| Mehadia        | 241                    |
| Neamt          | 234                    |
| Oradea         | 380                    |
| Pitesti        | 98                     |
| Rimnicu Vilcea | 193                    |
| Sibiu          | 253                    |
| Timisoara      | 329                    |
| Urziceni       | 80                     |
| Vaslui         | 199                    |
| Zerind         | 374                    |


---

## 🚀 Busca Gulosa (Greedy Best-First Search)

- Estratégia: Escolher sempre o nó com **menor h(n)**.
- Ignora o custo real até o nó (g(n)).

### 🔄 Etapas da execução (Arad → Bucharest):

1. **Arad (366)**  
   → Vizinhos: **Zerind (374)**, **Sibiu (253)**, **Timisoara (329)**  
   → Escolhe **Sibiu**

2. **Sibiu (253)**  
   → Vizinhos: **Fagaras (178)**, **Rimnicu Vilcea (193)**  
   → Escolhe **Fagaras**

3. **Fagaras (178)**  
   → Vizinho: **Bucharest (0)**  
   → Escolhe **Bucharest ✅**

### ✅ Caminho final (Gulosa):
```
Arad → Sibiu → Fagaras → Bucharest
```
---
### 📘 Pseudocódigo - Busca Gulosa

1. Crie uma fila de prioridade `F`
2. Insira o nó inicial (Arad) em `F`, com prioridade h(Arad)
3. Enquanto `F` não estiver vazia:
    4. Remova o nó `n` com menor h(n) de `F`
    5. Se `n` for o objetivo (Bucharest), retorne o caminho
    6. Para cada vizinho `v` de `n`:
        7. Se `v` ainda não foi visitado:
            8. Marque `v` como visitado
            9. Insira `v` em `F` com prioridade h(v)
10. Se a fila esvaziar sem encontrar o objetivo, retorne "falha"

---
### 📘 Código - Busca Gulosa
         
         import heapq
         
         def busca_gulosa(grafo, heuristica, inicio, objetivo):
             visitados = set()
             fila = []
             heapq.heappush(fila, (heuristica[inicio], [inicio]))
         
             while fila:
                 _, caminho = heapq.heappop(fila)
                 no_atual = caminho[-1]
         
                 if no_atual in visitados:
                     continue
         
                 visitados.add(no_atual)
         
                 if no_atual == objetivo:
                     print("Caminho encontrado (Gulosa):", " -> ".join(caminho))
                     return caminho
         
                 for vizinho, custo in grafo.get(no_atual, []):
                     if vizinho not in visitados:
                         novo_caminho = list(caminho)
                         novo_caminho.append(vizinho)
                         heapq.heappush(fila, (heuristica[vizinho], novo_caminho))
         
             print("Caminho não encontrado (Gulosa)")
             return None



---

## 🌟 Busca A* (A estrela)

- Estratégia: Escolhe o nó com menor **f(n) = g(n) + h(n)**  
- Onde:
  - **g(n)** = custo do caminho desde o início até o nó atual
  - **h(n)** = heurística (estimativa da distância até o objetivo)

### 🔄 Etapas da execução (com g(n) + h(n)):

1. **Arad**
   - h(n) = 366  
   - g(n) = 0  
   - f(n) = 366  
   → Vizinhos:
     - **Zerind**: g = 75, h = 374 → f = 449
     - **Sibiu**: g = 140, h = 253 → f = 393 ✅
     - **Timisoara**: g = 118, h = 329 → f = 447  
     → Escolhe **Sibiu**

2. **Sibiu**
   - g = 140  
   - h = 253  
   - f = 393  
   → Vizinhos:
     - **Fagaras**: g = 140 + 99 = 239, h = 178 → f = 417  
     - **Rimnicu Vilcea**: g = 140 + 80 = 220, h = 193 → f = 413 ✅  
     → Escolhe **Rimnicu Vilcea**

3. **Rimnicu Vilcea**
   - g = 220  
   - h = 193  
   - f = 413  
   → Vizinhos:
     - **Pitesti**: g = 220 + 97 = 317, h = 98 → f = 415 ✅
     - **Craiova**: g = 220 + 146 = 366, h = 160 → f = 526  
     → Escolhe **Pitesti**

4. **Pitesti**
   - g = 317  
   - h = 98  
   - f = 415  
   → Vizinho: **Bucharest**: g = 317 + 101 = 418, h = 0 → f = 418 ✅

### ✅ Caminho final (A*):

```
Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest
```
---
### 📘 Pseudocódigo - Busca A*

1. Crie uma fila de prioridade `F`
2. Insira o nó inicial (Arad) em `F`, com prioridade f(n) = g(n) + h(n), onde g(Arad) = 0
3. Crie um mapa `custo` para registrar o custo g(n) do caminho até cada nó
4. custo[Arad] = 0
5. Enquanto `F` não estiver vazia:
    6. Remova o nó `n` com menor f(n) da fila `F`
    7. Se `n` for o objetivo (Bucharest), retorne o caminho
    8. Para cada vizinho `v` de `n`:
        9. Calcule g(v) = g(n) + custo entre n e v
        10. Se `v` não estiver em `custo` ou g(v) for menor que custo[v]:
            11. Atualize custo[v]
            12. Calcule f(v) = g(v) + h(v)
            13. Insira ou atualize `v` em `F` com prioridade f(v)
14. Se a fila esvaziar sem encontrar o objetivo, retorne "falha"
---

### 📘 Código - Busca A*
      
      def busca_a_star(grafo, heuristica, inicio, objetivo):
          visitados = set()
          fila = []
          heapq.heappush(fila, (heuristica[inicio], 0, [inicio]))  # f(n), g(n), caminho
      
          while fila:
              f, custo_atual, caminho = heapq.heappop(fila)
              no_atual = caminho[-1]
      
              if no_atual in visitados:
                  continue
      
              visitados.add(no_atual)
      
              if no_atual == objetivo:
                  print("Caminho encontrado (A*):", " -> ".join(caminho))
                  print("Custo total:", custo_atual)
                  return caminho
      
              for vizinho, custo in grafo.get(no_atual, []):
                  if vizinho not in visitados:
                      g = custo_atual + custo
                      f = g + heuristica[vizinho]
                      heapq.heappush(fila, (f, g, caminho + [vizinho]))
      
          print("Caminho não encontrado (A*)")
          return None


---

## 📊 Comparação

| Algoritmo     | Caminho                                      | Custo real (g(n)) |
|---------------|----------------------------------------------|-------------------|
| Busca Gulosa  | Arad → Sibiu → Fagaras → Bucharest           | 140 + 99 + 211 = **450** |
| Busca A\*     | Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest | 140 + 80 + 97 + 101 = **418** |

---
