# Importando bibliotecas
    import random
    import numpy as np


# Criando as mercadorias de forma randômica

    n = 10  # número de mercadorias
    ids = np.arange(1, n+1)
    pesos = np.round(np.random.uniform(1.0, 10.0, size=n), 1)       # pesos entre 1.0 e 10.0
    valores = np.random.randint(100, 1000, size=n)                  # valores entre 100 e 999
    nomes = [f"Mercadoria {i}" for i in ids]

# capacidade máxima do caminhão
    capacidade_max = 50.0

# Mostrando as mercadorias
    print("ID | Nome           | Peso  | Valor")
    for i in range(n):
        print(f"{ids[i]:>2} | {nomes[i]:<13} | {pesos[i]:>5} | {valores[i]:>5}")
    print(f"\nCapacidade máxima do caminhão: {capacidade_max}\n")

# Configurando a população

    pop_size    = 100   # tamanho da população
    geracoes    = 50    # número de gerações
    taxa_mut    = 0.01  # probabilidade de mutação


# Inicializando a população

    def inicializa_população(tam_pop, num_itens):
        return [ [random.randint(0,1) for _ in range(num_itens)]
                 for _ in range(tam_pop) ]
    

# Criando função para calcular FITNESS

    def fitness(chromossomo):
        peso = sum(p*gene for p,gene in zip(pesos, chromossomo))
        valor = sum(v*gene for v,gene in zip(valores, chromossomo))
        return valor if peso <= capacidade_max else 0


# Criando função para SELEÇÃO (Roleta)

    def selecao_roleta(pop, fits):
        total = sum(fits)
        pick = random.uniform(0, total)
        acumulado = 0
        for ind, fi in zip(pop, fits):
            acumulado += fi
            if acumulado >= pick:
                return ind


# Criando função para CROSSOVER (ponto único)

    def crossover_ponto_unico(p1, p2):
        ponto = random.randint(1, len(p1)-1)
        f1 = p1[:ponto] + p2[ponto:]
        f2 = p2[:ponto] + p1[ponto:]
        return f1, f2


# Criando função para MUTAÇÃO (ponto único)

    def mutacao(chromossomo):
        return [ gene if random.random()>taxa_mut else 1-gene
                 for gene in chromossomo ]
    

# Rodando o AG

    pop = inicializa_população(pop_size, n)
    for ger in range(geracoes):
        fits = [fitness(ind) for ind in pop]
        melhor = max(fits)
        print(f"Geração {ger+1:>2}: Melhor aptidão = {melhor}")
        
        nova_pop = []
        for _ in range(pop_size // 2):
            pai1 = selecao_roleta(pop, fits)
            pai2 = selecao_roleta(pop, fits)
            filho1, filho2 = crossover_ponto_unico(pai1, pai2)
            nova_pop += [mutacao(filho1), mutacao(filho2)]
        pop = nova_pop


# Mostrando os resultados finais

    fits = [fitness(ind) for ind in pop]
    melhor = max(fits)
    idx = fits.index(melhor)
    solucao = pop[idx]
    peso_sol = sum(p*gene for p,gene in zip(pesos, solucao))
    
    print("\n=== SOLUÇÃO FINAL ===")
    print(f"Valor transportado: {melhor}")
    print(f"Peso utilizado   : {peso_sol:.1f} / {capacidade_max}")
    print("Itens carregados  :")
    for i,gene in enumerate(solucao):
        if gene:
            print(f"  - {nomes[i]} (peso {pesos[i]}, valor {valores[i]})")
