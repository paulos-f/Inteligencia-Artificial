# Pergunta

04) Suponha que queremos encontrar a rota mais curta entre as estações de metrô em São Paulo. Podemos representar o mapa de metrô como um grafo, onde cada estação é um vértice e as linhas de metrô que conectam as estações são as arestas. Implemente o algoritmo de busca em largura para encontrar o caminho mais curto entre dois locais.


```
grafo_metro = {
    'Barra Funda': ['Palmeiras-Barra Funda', 'Marechal Deodoro'],
    'Palmeiras-Barra Funda': ['Barra Funda', 'Paulista', 'Luz'],
    'Marechal Deodoro': ['Barra Funda', 'Santa Cecília'],
    'Paulista': ['Consolação', 'Palmeiras-Barra Funda'],
    'Luz': ['Palmeiras-Barra Funda', 'Sé', 'República'],
    'Consolação': ['Paulista', 'Clínicas'],
    'Santa Cecília': ['Marechal Deodoro', 'República'],
    'Sé': ['Luz', 'Anhangabaú'],
    'República': ['Luz', 'Santa Cecília', 'Anhangabaú'],
    'Clínicas': ['Consolação', 'Sumaré'],
    'Anhangabaú': ['Sé', 'República'],
    'Sumaré': ['Clínicas']
}
```
Segue imagem abaixo:

![image](https://github.com/user-attachments/assets/71e3e98c-c90b-4175-9986-2985943fb6a9)


---
# Resposta

    
    def busca_em_largura(grafo, inicio, objetivo):
      fila = [(inicio,[inicio])] # Fila dos nós a serem visitados com os seus caminhos
      visitados = {inicio} # Nós que já foram visitados
    
      while fila:
        (vertice, caminho) = fila.pop(0)
    
        if vertice == objetivo:
          return caminho
    
        for vizinho in grafo[vertice]:
          if vizinho not in visitados:
            visitados.add(vizinho)
            fila.append((vizinho, caminho + [vizinho])) # Add o vizinho na fila junto do caminho
    
      return None # Volta caso não ache um caminho entre o primeiro nó e o nó que tem o objetivo

---
    
    inicio = 'República'
    objetivo = 'Sumaré'
    
    caminho = busca_em_largura(grafo_metro, inicio, objetivo)
    
    if caminho:
      print(f"caminho + curto entre {inicio} e {objetivo}: {caminho}")
    else:
      print(f"n tem caminho entre {inicio} e {objetivo}")
