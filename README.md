# Matrix Multiplication Parallel Benchmark

![Foto de Capa](assets/imgs/foto-de-capa.jpg)

[![licence mit](https://img.shields.io/badge/licence-MIT-blue.svg)](./LICENSE)
[![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-%23FE5196?logo=conventionalcommits&logoColor=white)](https://conventionalcommits.org)

## Sumário
- [Matrix Multiplication Parallel Benchmark](#matrix-multiplication-parallel-benchmark)
  - [Sumário](#sumário)
  - [Introdução](#introdução)
  - [Tecnologias Usadas](#tecnologias-usadas)
  - [Fórmulas](#fórmulas)
    - [Multiplicação de Matrizes](#multiplicação-de-matrizes)
    - [Speedup](#speedup)
    - [Eficiência](#eficiência)
  - [Como Executar o Projeto](#como-executar-o-projeto)
    - [Pré-requisitos](#pré-requisitos)
    - [Passos para compilar o projeto](#passos-para-compilar-o-projeto)
    - [Executando o programa no Windows](#executando-o-programa-no-windows)
    - [Observações](#observações)
  - [Licença](#licença)

## Introdução

Este projeto é uma **POC (Proof of Concept)** que implementa um **benchmark de multiplicação de matrizes** utilizando **paralelismo com OpenMP**.
O objetivo é medir o **tempo de execução**, o **speedup** e a **eficiência** para diferentes quantidades de threads, permitindo analisar o ganho de desempenho que a programação paralela oferece em relação à execução sequencial.

O código utiliza duas matrizes 100x100 (com valores fixos para simplificação) e calcula o produto entre elas.
A medição é feita variando de 1 a 8 threads, apresentando os resultados no terminal.

## Tecnologias Usadas
![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)&nbsp;
![OpenMP](https://img.shields.io/badge/OpenMP-00599C?style=for-the-badge)&nbsp;
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)&nbsp;
![Docker Compose](https://img.shields.io/badge/Docker_Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)&nbsp;
![MinGW-w64](https://img.shields.io/badge/MinGW--w64-004880?style=for-the-badge)&nbsp;

## Fórmulas

### Multiplicação de Matrizes
Para matrizes $A$ de dimensão $m \times n$ e $B$ de dimensão $n \times p$, o produto $C = A \cdot B$ é uma matriz $m \times p$, onde cada elemento $C_{i,k}$ é calculado por:

$$
C_{i,k} = \sum_{j=1}^{n} A_{i,j} \cdot B_{j,k}
$$

- $i = 1, \dots, m$ (linhas de A)
- $k = 1, \dots, p$ (colunas de B)
- $j = 1, \dots, n$ percorre os elementos de A e B correspondentes para multiplicação e soma

### Speedup
O **speedup** indica quanto mais rápido o programa roda utilizando múltiplas threads em comparação com a execução sequencial (uma thread):

$$
\text{Speedup}(N) = \frac{T_1}{T_N}
$$

- $T_1$ = tempo de execução com 1 thread
- $T_N$ = tempo de execução com N threads

### Eficiência
A **eficiência** indica a fração do ganho teórico que é efetivamente obtida ao aumentar o número de threads:

$$
\text{Eficiência}(N) = \frac{\text{Speedup}(N)}{N} = \frac{T_1}{N \cdot T_N}
$$

- Um valor próximo de 1 significa que o paralelismo está sendo bem aproveitado.
- Valores menores que 1 indicam overhead ou limitações de paralelismo.

## Como Executar o Projeto

Este projeto utiliza **Docker** e **Docker Compose** para compilar o código C++ com suporte a **OpenMP** e gerar um executável Windows (`.exe`) que pode ser executado localmente.

### Pré-requisitos

Antes de iniciar, verifique se você possui instalados no seu computador:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Passos para compilar o projeto

1. **Clonar o repositório**
```bash
git clone https://github.com/SEU-USUARIO/matrix-parallel-benchmark.git
cd matrix-parallel-benchmark
````

2. **Construir a imagem Docker e compilar**

```bash
docker compose build
```

3. **Gerar o executável**

```bash
docker compose run --rm builder
```

O executável será gerado na pasta:

```sh
./build/main.exe
```

### Executando o programa no Windows

Após o build, basta abrir um terminal (CMD ou PowerShell) no Windows e executar:

```powershell
.\build\main.exe
```

O programa exibirá algo como:

```
BENCHMARK DE DESEMPENHO PARALELO

Quantidade de Threads: 1 | Tempo de Execução: 0.012000 segundos
Speedup: 1.000000 | Eficiência: 1.000000

Quantidade de Threads: 2 | Tempo de Execução: 0.007000 segundos
Speedup: 1.714286 | Eficiência: 0.857143
...
```

### Observações

* Este projeto foi projetado para fins **educacionais**, com foco em demonstrar conceitos de **speedup** e **eficiência** na programação paralela.
* O código não implementa otimizações avançadas para multiplicação de matrizes, pois o objetivo é a clareza conceitual.
* É necessário rodar o executável no **Windows** ou com um emulador compatível com `.exe`.

## Licença

Este projeto está sob a [Licença MIT](./LICENSE). Consulte o arquivo [LICENSE.md](LICENSE.md) para obter mais detalhes.