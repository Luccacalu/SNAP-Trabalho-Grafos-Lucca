# Análise da rede P2P Gnutella (p2p-Gnutella06)

Trabalho prático da disciplina de **Teoria dos Grafos** (UFBA).
Estudamos o grafo `p2p-Gnutella06` do repositório [SNAP](https://snap.stanford.edu/data/p2p-Gnutella06.html): uma captura da rede de compartilhamento de arquivos Gnutella feita em 6 de agosto de 2002, com **8.717 vértices** (computadores) e **31.525 arestas** (conexões).

O trabalho tem três partes:

| Parte | O que faz | Notebook |
|---|---|---|
| Tratamento + **Parte I** | Limpa o grafo e calcula as medidas estruturais (graus, densidade, componentes, diâmetro, clusterização, triângulos etc.) | `01_tratamento_e_parte1.ipynb` |
| **Parte II** | Implementa BFS, DFS, eulerianidade, Dijkstra, Bellman-Ford, Floyd-Warshall, Tarjan e árvore geradora mínima (Kruskal e Prim) e compara o tempo medido com a complexidade teórica | `02_parte2_algoritmos.ipynb` |
| **Parte III** | Small-world, lei de potência, robustez a falhas e ataques, descoberta mais interessante e comparação com modelos clássicos (ER, BA, WS) | `03_parte3_analise.ipynb` |

O relatório em formato de artigo (template WebMedia) foi escrito no Overleaf e entregue em PDF.

---

## Estrutura das pastas

```
.
├── data/
│   ├── raw/            # p2p-Gnutella06.txt.gz
│   └── processed/      # grafos tratados
├── notebooks/          # os 3 notebooks
├── figures/            # figuras geradas (.png)
├── results/            # tabelas geradas (.csv)
├── requirements.txt
└── README.md
```

As pastas `data/processed`, `figures` e `results` são criadas automaticamente pelos notebooks se não existirem.

---

## Como executar

### 1. Pré-requisitos

- **Python 3.13** (testado com 3.13.1; versões próximas devem funcionar)
- Jupyter (Notebook, Lab ou o suporte a notebooks do VS Code)

### 2. Baixar o código

```bash
git clone https://github.com/Luccacalu/SNAP-Trabalho-Grafos-Lucca.git
cd SNAP-Trabalho-Grafos-Lucca
```

### 3. Instalar as bibliotecas

Para usar um ambiente virtual:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# Linux/macOS:
source .venv/bin/activate

pip install -r requirements.txt
```

As bibliotecas usadas são: `networkx`, `numpy`, `scipy`, `pandas`, `matplotlib`, `seaborn`, `python-igraph` e `jupyter`.

> O `igraph` é usado só para calcular a intermediação (*betweenness*) no ataque da Parte III. Se ele não estiver instalado, o notebook 03 usa uma versão aproximada própria e avisa na saída (`Betweenness: ...`). Para reproduzir os números do relatório, instale o `igraph`.

### 4. Colocar os dados originais

O arquivo bruto não precisa ser descompactado. É possível baixar em
<https://snap.stanford.edu/data/p2p-Gnutella06.txt.gz>

(Mesmo com a pasta `data/processed` já no repositório, o notebook 01 ainda assim deve ser executado primeiro, pois ele a regenera.)

### 5. Rodar os notebooks **nesta ordem**

1. `01_tratamento_e_parte1.ipynb`
2. `02_parte2_algoritmos.ipynb`
3. `03_parte3_analise.ipynb`

O notebook 01 gera os grafos tratados em `data/processed/`, que os outros dois leem. Em cada notebook, use **Kernel → Restart & Run All** (ou "Executar tudo").

Abra o Jupyter a partir da raiz do projeto ou da pasta `notebooks/`. Os caminhos funcionam nos dois casos:

```bash
jupyter lab
```

---

## O que esperar

**Tempo de execução** (varia conforme o computador): o 01 e o 02 levam alguns minutos; o **03 é o mais demorado**, principalmente o teste da lei de potência (100 amostras sintéticas) e as repetições de robustez. Os tempos da Parte II dependem da máquina e mudam um pouco a cada execução; o relatório usa as medições feitas em um Intel Core i5-9300H com 16 GB de RAM.

**Resultados repetíveis:** todos os sorteios usam sementes fixas, então os números não mudam entre execuções (exceto os tempos medidos da Parte II).

### Arquivos gerados

| Pasta | Conteúdo |
|---|---|
| `data/processed/` | `gnutella06_directed_clean.edgelist` e `gnutella06_undirected_clean.edgelist` |
| `results/` | tabelas em `.csv` (controle da Parte I, validação SNAP, tempos, inclinações, robustez, modelos etc.) |
| `figures/` | figuras em `.png` usadas no relatório (distribuição de graus, visualização dos 120 maiores hubs, escalonamento da complexidade, lei de potência, boxplots de robustez e CCDF dos modelos) |

---

## Problemas comuns

- **`FileNotFoundError` no notebook 01:** o arquivo `p2p-Gnutella06.txt.gz` não está em `data/raw/`.
- **`FileNotFoundError` nos notebooks 02 ou 03:** o notebook 01 ainda não foi executado (ele cria `data/processed/`).
- **`ModuleNotFoundError: igraph`:** rode `pip install python-igraph` (o nome para importar é `igraph`).
- **Tempos da Parte II diferentes dos do relatório:** é normal, pois dependem do computador e do que mais está rodando.

---

## Autor

Lucca Giovanni Lobo Gonçalves — Universidade Federal da Bahia (UFBA), Teoria dos Grafos.