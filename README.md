# Análise de DNA
Este é um projeto da cadeira de Programação 2 da proposto pela Faculdade Ciências da Universidade do Porto, cujo objetivo é o corte de sequências de DNA de acordo com restrições de enzimas, utilizando as bibliotecas base do Python.

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

## Tarefa 2

A função `leEnzima` lê uma lista de restrições de enzimas no formato [staden](https://extras.csc.fi/staden/doc/manual/formats_unix_23.html).
Pode encontrar uma listagem de enzimas neste formato na base de dados [REBASE](http://rebase.neb.com/rebase/link_staden). 

```
AanI/TTA'TAA//
AarI/CACCTGCNNNN'NNNN/'NNNNNNNNGCAGGTG//
```

Depois de um cabeçalho de algumas linhas, cada linha define uma enzima no formato `nome/cut53/cut35//`, em que `cut53` e `cut35` são padrões de excertos de DNA nos sentidos $5' \rightarrow 3'$ e $3' \rightarrow 5'$ que compõe a enzima. Estes padrões podem ser as bases `ACGT`, ou as seguintes letras que determinam várias opções de bases:

| letra |   base           | 
|:-----:|:----------------:|
| Y     | C ou T           |
| R     | A ou G           |
| W     | A ou T           |
| S     | G ou C           |
| K     | T ou G           |
| M     | C ou A           |
| D     | A ou G ou T      |
| V     | A ou C ou G      |
| V     | A ou C ou G      |
| H     | A ou C ou T      |
| B     | C ou G ou T      |
| X     | A ou T ou G ou C |
| N     | A ou T ou G ou C |

A variável `nucleotideBases` representa esta tabela como um dicionário.

Cada excerto pode conter um caracter especial `'` que determina a posição particular em que a enzima corta uma sequência de DNA; quando uma posição de corte não é definida concretamente, a posição de corte assumida é no fim do excerto no sentido $5' \rightarrow 3'$ e no início no sentido $3' \rightarrow 5'$. Quando o excerto `cut35` não é dado explicitamente, este é calculado a partir da função `nucleotidePair`, e a sua posição de corte é o inverso da posição de corte do excerto `cut53`.

O resultado da função `leEnzima` é uma base de dados de enzimas, representada como um dicionário de nomes de enzimas para representações de enzimas no formato `(excerto53,pos53,excerto35,pos35)`, em que `excerto53` e `excerto35` são excertos de DNA e `pos53` e `pos35` são respetivamente as posições de corte em cada excerto.
