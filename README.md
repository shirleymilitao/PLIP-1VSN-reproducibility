# Reproducibility of Protein–Ligand Interactions in PDB 1VSN using PLIP
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/shirleymilitao/PLIP-1VSN-reproducibility/blob/main/notebooks/PLIP_1VSN_Reprodutibilidade.ipynb)

Reprodução computacional do perfil de interações proteína–ligante da estrutura cristalográfica **PDB 1VSN**, utilizando o **Protein–Ligand Interaction Profiler (PLIP)**.

## Sobre o projeto

Este projeto foi desenvolvido como um exercício de **bioinformática reprodutível**, com o objetivo de reproduzir uma parte delimitada da análise apresentada por Salentin et al. (2015).

O estudo concentra-se no perfil de interações entre a **catepsina K humana** e o ligante **NFT** na pose cristalográfica da estrutura **PDB 1VSN**, utilizando o **PLIP 3.0.1**.

O objetivo não é reproduzir integralmente o artigo original, mas avaliar se características relevantes do perfil de interações da pose cristalográfica podem ser reproduzidas com uma versão atual do PLIP, documentando também eventuais divergências em relação ao trabalho de referência.

## Pergunta científica

> Quais interações não covalentes entre o ligante NFT e a catepsina K são identificadas pelo PLIP na estrutura experimental PDB 1VSN?

## Estrutura analisada

| Característica | Informação |
|---|---|
| PDB | 1VSN |
| Proteína | Catepsina K humana |
| Ligante | NFT |
| Cadeia | A |
| Resíduo do ligante | 283 |
| Método experimental | Difração de raios X |

## Referência principal

Salentin S, Schreiber S, Haupt VJ, Adasme MF, Schroeder M.  
**PLIP: fully automated protein-ligand interaction profiler.**  
*Nucleic Acids Research*. 2015.  
DOI: 10.1093/nar/gkv315

## Workflow

O experimento foi organizado nas seguintes etapas:

1. preparação do projeto e do ambiente computacional;
2. download reprodutível da estrutura PDB 1VSN e verificação da identidade do arquivo por SHA-256;
3. inspeção da estrutura e identificação do ligante NFT;
4. análise exploratória da proximidade proteína–ligante;
5. execução do PLIP 3.0.1;
6. extração programática das interações;
7. construção e exportação das tabelas de resultados, incluindo uma tabela detalhada com pares atômicos e parâmetros geométricos;
8. inspeção da estrutura protonada gerada pelo PLIP e investigação de casos específicos de protonação e geometria;
9. verificação separada do contato covalente CYS25–NFT;
10. visualização e sumarização das interações não covalentes;
11. investigação das moléculas de água e dos critérios de classificação de `water bridges`;
12. registro das versões do ambiente computacional;
13. testes automáticos de reprodutibilidade e verificação das identidades e geometrias das interações;
14. comparação dos resultados com o trabalho de referência;
15. verificação dos produtos finais e avaliação da reprodutibilidade.

## Resultados

A análise com **PLIP 3.0.1** identificou **13 registros de interação** entre o ligante NFT e a catepsina K.

| Tipo de interação | Número de registros |
|---|---:|
| Ligações de hidrogênio | 7 |
| Contatos hidrofóbicos | 4 |
| Ligações de halogênio | 2 |
| **Total** | **13** |

Foram identificados **8 resíduos distintos** envolvidos nas interações:

- GLN19
- CYS25
- ASP61
- GLY66
- TYR67
- ALA133
- LEU157
- ASN158

Entre esses resíduos, **ASP61** e **TYR67** apresentaram o maior número de registros de interação.

ASP61 apresentou dois registros de ligação de hidrogênio para o mesmo par atômico ASP61 OD2 ↔ NFT N63, com os papéis de doador/aceptor invertidos, além de um contato hidrofóbico. Esses dois registros foram preservados conforme a saída do PLIP, mas não são interpretados automaticamente como duas ligações de hidrogênio físicas independentes.

TYR67 apresentou dois contatos hidrofóbicos e uma ligação de halogênio.

## Investigação das pontes de água

A estrutura 1VSN contém **269 moléculas de água cristalográficas**.

Na análise geométrica realizada neste projeto:

- 14 águas apresentaram pelo menos um átomo a até 5 Å de qualquer átomo do ligante NFT;
- 11 apresentaram distância mínima ao NFT dentro do intervalo de 2,5–4,1 Å observado nos parâmetros do PLIP 3.0.1.

Apesar da presença de moléculas de água próximas ao ligante, nenhuma interação foi classificada como `Water Bridge` pelo PLIP 3.0.1 nesta execução.

A referência original descreve interações mediadas por água para a pose cristalográfica analisada.

Portanto, essa característica não foi reproduzida na execução atual.

A causa específica dessa diferença não foi determinada neste experimento. Possíveis efeitos de versão do software, preparação estrutural ou critérios geométricos podem ser investigados futuramente, mas não são considerados explicações comprovadas neste trabalho.

## Avaliação da reprodutibilidade

Os resultados são caracterizados como uma **reprodução parcial do perfil de interações da pose cristalográfica de 1VSN**.

Foi observada concordância qualitativa em características relevantes da análise de referência, especialmente na identificação das ligações de halogênio.

Entretanto, as pontes de água descritas na literatura não foram reproduzidas com PLIP 3.0.1.

Essa divergência foi mantida e documentada como parte do próprio resultado da avaliação de reprodutibilidade.

### Reprodutibilidade computacional

O notebook foi posteriormente executado do início ao fim em ambiente limpo.

Os testes automáticos verificaram:

- 13 registros totais de interação;
- 7 registros de ligações de hidrogênio;
- 4 contatos hidrofóbicos;
- 2 ligações de halogênio;
- 8 resíduos únicos;
- identidade dos pares atômicos dos 4 contatos hidrofóbicos;
- identidade, distâncias e ângulos das 2 ligações de halogênio;
- identidade dos pares atômicos, papéis de doador/aceptor, distâncias D–A e H–A e ângulos D–H···A dos 7 registros de ligações de hidrogênio.

Todas as verificações automatizadas foram concluídas com sucesso. Esses testes avaliam a consistência interna e a reprodutibilidade computacional do workflow, mas não constituem validação experimental das interações moleculares.

#### Verificação independente via GitHub/Google Colab

Após a publicação do projeto no GitHub, o notebook foi aberto diretamente a partir do repositório por meio do botão **Open in Colab** e executado integralmente em uma nova sessão do Google Colab.

O workflow completou todas as etapas previstas e as verificações automatizadas foram concluídas com sucesso, reproduzindo os resultados computacionais esperados. A execução em uma nova sessão fornece evidência de que o workflow disponibilizado no repositório pode ser executado a partir do notebook publicado sem depender do estado da sessão original utilizada durante seu desenvolvimento.

## Visualização dos resultados

A figura abaixo apresenta o perfil de interações identificado pelo PLIP para os resíduos da catepsina K envolvidos na interação com o ligante NFT.

![Perfil de interações PLIP 1VSN](figures/1VSN_interactions.png)

O gráfico mostra que diferentes resíduos podem participar de diferentes categorias de interação. ASP61 e TYR67 apresentam o maior número de registros, enquanto GLY66 participa de duas ligações de hidrogênio.

## Ambiente computacional

A execução utilizada para verificar a reprodutibilidade computacional deste experimento apresentou o seguinte ambiente:

| Ferramenta | Versão |
|---|---:|
| Python | 3.13.16 |
| PLIP | 3.0.1 |
| Open Babel | 3.2.1 |
| pandas | 2.2.3 |
| NumPy | 2.1.3 |
| Matplotlib | 3.10.0 |

As dependências Python utilizadas estão registradas em:

`environment/requirements.txt`

As versões observadas durante a execução também estão documentadas em:

`environment/environment_versions.txt`

O Open Babel constitui uma dependência importante do PLIP e sua instalação pode variar entre sistemas operacionais.

O registro dessas versões aumenta a rastreabilidade e favorece a reprodutibilidade computacional, mas não garante, isoladamente, a reconstrução futura exata do ambiente. Dependências de sistema, bibliotecas transitivas, sistema operacional e alterações na imagem-base do Google Colab também podem influenciar a execução.

## Como reproduzir

O workflow principal está disponível em:

`notebooks/PLIP_1VSN_Reprodutibilidade.ipynb`

### Google Colab

O notebook foi preparado para execução sequencial no Google Colab.

Para reproduzir a análise:

1. abra o notebook no Google Colab;
2. utilize um ambiente de execução Python;
3. execute as células sequencialmente do início ao fim;
4. aguarde a instalação das dependências e a execução do PLIP;
5. verifique os testes automáticos ao final.

O próprio notebook realiza o download da estrutura PDB 1VSN, instala as ferramentas necessárias, executa o PLIP, extrai os resultados, gera os arquivos derivados e realiza os testes de reprodutibilidade.

### Resultado esperado

Ao final da execução deverá aparecer:

`Todas as verificações automatizadas foram concluídas com sucesso.

Os principais valores esperados para a execução verificada são:

- 13 registros de interação;
- 7 registros de ligações de hidrogênio;
- 4 contatos hidrofóbicos;
- 2 ligações de halogênio;
- 8 resíduos únicos.

Uma alteração nesses valores em outro ambiente ou versão de software deve ser investigada em vez de ser automaticamente interpretada como erro.

## Limitações

Este projeto não representa uma reprodução integral do artigo de Salentin et al. (2015).

O escopo foi deliberadamente limitado à análise do perfil de interações da pose cristalográfica do complexo PDB 1VSN.

O experimento também utiliza uma versão atual do PLIP, diferente daquela disponível no período da publicação original.

Além disso, embora tenham sido investigadas as moléculas de água próximas ao ligante, não foi realizada uma reimplementação independente dos critérios geométricos utilizados pelo PLIP para classificação de pontes de água.

Portanto, a divergência observada para `Water Bridges` permanece documentada, mas sua causa específica não foi estabelecida.

## Conclusão

A análise reproduziu parcialmente o perfil de interações proteína–ligante da pose cristalográfica da estrutura PDB 1VSN.

Foram identificadas de maneira reprodutível ligações de hidrogênio, contatos hidrofóbicos e ligações de halogênio entre a catepsina K e o ligante NFT.

A presença das ligações de halogênio representa uma concordância qualitativa relevante com a análise de referência.

Por outro lado, as pontes de água descritas na literatura não foram identificadas pelo PLIP 3.0.1 nesta execução. Essa diferença foi investigada e documentada, sem atribuição de uma causa não demonstrada pelos dados.

O workflow computacional foi executado novamente em ambiente limpo, e as verificações automatizadas reproduziram os resultados computacionais esperados quanto às contagens, identidades dos pares atômicos e parâmetros geométricos avaliados.

Dessa forma, o projeto fornece um exemplo delimitado de avaliação de reprodutibilidade em bioinformática estrutural, incluindo não apenas os resultados concordantes, mas também uma divergência observada durante a reprodução.

## Estrutura do repositório

A organização dos arquivos utilizados e produzidos neste projeto é apresentada abaixo:

```text
PLIP-1VSN-reproducibility/
│
├── README.md
│
├── notebooks/
│   └── PLIP_1VSN_Reprodutibilidade.ipynb
│
├── data/
│   └── 1VSN.pdb
│
├── plip_results/
│   ├── 1VSN_report.txt
│   ├── 1VSN_protonated.pdb
│   ├── interactions_1VSN.csv
│   └── interactions_1VSN_detailed.csv
│
├── figures/
│   └── 1VSN_interactions.png
│
└── environment/
    ├── environment_versions.txt
    └── requirements.txt
```

### Conteúdo dos diretórios

- `notebooks/`: notebook principal contendo o workflow completo;
- `data/`: estrutura PDB utilizada como dado de entrada;
- `plip_results/: relatório produzido pelo PLIP, estrutura protonada, tabela resumida e tabela detalhada das interações;
- `figures/`: visualizações produzidas durante a análise;
- `environment/`: versões das ferramentas e dependências utilizadas no experimento.
