 # rush-02

## Visão geral

Este projeto é um conversor simples de números inteiros para sua forma por extenso usando um dicionário em texto (`dict.txt`). Ele lê um número fornecido como argumento de linha de comando, carrega o dicionário, descreve o número por extenso e imprime o resultado no terminal.

## Arquivos do projeto

### `Makefile`
- Define as regras de compilação do projeto.
- Compila os fontes em `rush-02` usando `gcc` com `-Wall -Wextra -Werror`.
- Regras principais:
  - `make` ou `make all` compila toda a aplicação.
  - `make clean` remove os arquivos objeto (`.o`).
  - `make fclean` remove os arquivos objeto e o executável.
  - `make re` recompila tudo do zero.

### `dict.txt`
- Contém as associações de números para nomes em inglês.
- Exemplo de entrada:
  - `1 : one`
  - `1000 : thousand`
- É usado em tempo de execução para montar a lista de conversão.

### `includes/ft.h`
- Cabeçalho comum do projeto.
- Declara:
  - `t_list` (estrutura com `nbr` e `number_name`).
  - Funções utilitárias, leitura do dicionário e criação da lista.

### `src/main.c`
- Ponto de entrada da aplicação.
- Valida a presença de exatamente um argumento.
- Se o número for negativo, imprime `Error`.
- Chama `create_list("dict.txt")` para carregar as regras de conversão.
- Chama `ft_print()` para imprimir o número por extenso.

### `src/ft_rush02.c`
- Contém a lógica de impressão do número por extenso.
- Funções principais:
  - `get_tens(int nbr)` determina qual valor de dezenas usar para valores até 99.
  - `get_decimal_classes(int nbr)` retorna a classe decimal apropriada: centenas, milhares, milhões ou bilhões.
  - `ft_print(int n, t_list *list, int *first)` imprime recursivamente as partes do número usando a lista do dicionário.
- A função `ft_print()` usa recursão para decompor o número em unidades, dezenas, centenas e classes maiores.

### `src/ft_util.c`
- Contém funções utilitárias e a leitura do dicionário.
- Funções principais:
  - `ft_putchar(char c)` escreve um caractere no `stdout`.
  - `ft_putstr(char *str)` escreve uma string no `stdout`.
  - `ft_strdup(char *src)` duplica uma string com alocação de memória.
  - `ft_atoi(char *str)` converte string para inteiro.
  - `get_nbr(int fd)` lê o número inicial de uma linha do arquivo.
  - `get_number_name(int fd, char *buffer)` lê o nome do número a partir do arquivo.
  - `create_list(char *file_name)` abre `dict.txt`, lê até 32 entradas e constrói o array `t_list`.

## Como compilar e executar

1. Garanta que você tenha o compilador `gcc` instalado.
2. Na raiz do projeto, execute:
   ```sh
   make
   ```
3. Execute o programa com um número como argumento:
   ```sh
   ./rush-02 123
   ```
4. O programa imprime o valor por extenso usando os valores definidos em `dict.txt`.

## Observações importantes

- No ambiente atual, não foi possível executar ou compilar o código porque não existe `gcc` nem `make` disponíveis no shell.
- O código depende de `dict.txt` estar presente na raiz do projeto.
- Há uma possível falha de implementação nas funções `get_nbr()` e `get_number_name()`: elas devolvem strings sem terminar explicitamente com `\0`. Isso pode causar comportamento indefinido.
- Se você quiser testar localmente, instale uma ferramenta compatível como MinGW ou WSL e execute `make`.

## Exemplo de uso

```sh
make
./rush-02 42
```

Saída esperada:

```txt
forty two
```
