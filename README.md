# Análise de DNA
Será feito o corte de sequências de DNA de acordo com restrições de enzimas, utilizando as bibliotecas base do Python.

## Tarefa 1
A função `leDNA` lê uma sequência de DNA no formato [FASTA](https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&PAGE_TYPE=BlastDocs&DOC_TYPE=BlastHelp).
Um exemplo de uma sequência de DNA de um fungo de fermento, com o código [U49845.1](https://www.ncbi.nlm.nih.gov/nuccore/U49845.1?report=fasta&log$=seqview), pode ser consultada na base de dados do [National Center for Biotechnology Information](https://www.ncbi.nlm.nih.gov/).

```
>U49845.1 Saccharomyces cerevisiae TCP1-beta gene, partial cds; and Axl2p (AXL2) and Rev7p (REV7) genes, complete cds
GATCCTCCATATACAACGGTATCTCCACCTCAGGTTTAGATCTCAACAACGGAACCATTGCCGACATGAG
```

A primeira linha do ficheiro contém um cabeçalho com uma pequena descrição.

As seguintes linhas formam uma string que codifica a sequência de DNA, contendo quatro bases possíveis codificadas com as seguintes letras:

| letra |   base   | 
|:-----:|:--------:|
| A     | adenine  |
| C     | cytosine |
| G     | guanine  |
| T     | thymine  |

O resultado da função é um par de strings que forma uma [cadeia de DNA](https://www.genome.gov/genetics-glossary/Base-Pair), em que a primeira string é a sequência $5' \rightarrow 3'$ lida do ficheiro, e a segunda string é o complemento $3' \rightarrow 5'$, que pode foi calculada aplicando a função `nucleotidePair` a cada letra da primeira string.
