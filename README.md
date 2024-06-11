# Bioinformatic Genomic Analysis Project 
Analysis of Purinergic Pathway Overload Due to the Use of Cannabidiol in the Treatment of SARS-CoV-2\
O artigo escolhido está dísponível nesse repositório com o nome ***Cannabidiol inhibits SARS-CoV-2 replication through***\
Os softwares utilizados foram:
- [Galaxy](https://usegalaxy.org)
- [DAVID](https://ngdc.cncb.ac.cn/databasecommons/database/id/3061)
- [KEGG](https://www.genome.jp/kegg/)

  
## Overview
A SARS-CoV-2 é responsável pela COVID-19, com uma gama de sintomas que vão desde leves até graves, destacando a necessidade de estudos sobre tratamentos alternativos devido à alta taxa de disseminação do vírus. Um estudo recente indica que o canabidiol (CBD) pode reduzir a ativação de citocinas, porém, o sistema purinérgico também desempenha um papel crucial na inflamação. Além disso, enzimas como a purina nucleosídeo fosforilase (PNP) e a AMP desaminase estão implicadas no metabolismo das purinas e podem ter influência significativa na resposta do organismo. A hipótese é que o tratamento com CBD pode sobrecarregar o sistema purinérgico, potencialmente mascarando os sintomas da SARS-CoV-2.


## Arquivos
Para esse projeto, foram utilizados os arquivos: 
- ***[Human.GRCh38.p13.annot.tsv.gz].gtf***, como o genoma humano para a base do trabalho
- ***[GSE168797_Raw_gene_counts_matrix.txt.gz].tabular***, como a tabela de genes utilizados no artigo
- ***[GSE168797_cortados].tabular***, como a tabela de genes selecionados e pronta para a análise.

  
## Metodologia
O sequenciamento de RNA de alto rendimento foi conduzido na plataforma Illumina NovaSeq 6000, com leitura emparelhadas de 100 bases (paired end), utilizando uma biblioteca de cDNA e fonte de biblioteca transcriptômica. As leituras passaram por processamento para garantir qualidade e remoção de adaptadores. Posteriormente, foram mapeadas para os genomas humano (versão hg19) e SARS-CoV-2.\
Para análise da expressão gênica diferencial de **RNA-Seq**, foram adicionadas tags aos dados para identificar tratamentos e sequenciamentos, essenciais para análises com **DESeq2**, que retorna estatísticas relevantes, como a tabela de DEGs contendo as informações como log2-fold change (medida da diferença na expressão gênica entre duas condições em uma escala logarítmica) e p-ajustado (correção do valor-p para controlar os falsos positivos na análise de expressão gênica) para cada Ensembl ID. Posteriormente, os dados de anotação gênica do genoma humano foram adicionados à tabela. Os genes mais expressos diferencialmente entre os tratamentos foram selecionados com **p-valor < 0,05 e abs(log2FC)>1**. Com base nos **Z-scores**, que expressam o desvio dos dados em relação à média da amostra em termos do desvio padrão, **Volcano Plot e Heatmaps** foram gerados para melhor visualização.
Na etapa de enriquecimento funcional, utilizou-se como input na plataforma **DAVID** apenas os genes diferencialmente expressos positivamente. Isso permitiu uma compreensão mais detalhada das funções biológicas e processos, utilizando a ontologia de genes para categorizá-los e o banco de dados **KEGG** para explorar as vias metabólicas associadas.


## Resultados
- O PCA plot revela a variabilidade entre os grupos de tratamento (canabidiol ou veículo), mostrando que eles se agrupam de acordo com o tipo de tratamento. A distância entre os grupos indica que o tratamento tem um impacto significativo nas amostras.\
 ![PCA PLOT_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/c9291b5e-22ff-4229-9291-d5b5a0bd729b)
- O gráfico de dispersão calcula um valor final que representa a variabilidade dos genes estudados com base nos dados brutos, mostrado em azul. A maioria dos genes, representados pelos pontos pretos, está próxima ao valor final, indicando uma variação consistente e previsível, o que sugere qualidade nos dados.\
  ![DISPERSÃO_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/e19fd9bb-6b94-4e49-8bb8-00ec6102acaa)
- No histograma de frequência, a concentração maior de valores de p-value igual a zero indica que há diferenças significativas nas expressões gênicas avaliadas entre as amostras tratadas com canabidiol e as tratadas com veículo.\
  ![FREQUENCIA_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/f092a8df-1bb2-4557-84fe-9894f91271d2)
- O gráfico de MA-plot indica diferenças na expressão gênica entre os grupos de amostras, destacando genes com expressão aumentada (pontos acima do eixo x) ou reduzida (pontos abaixo do eixo x). Isso levanta questões sobre quais genes poderiam estar mais expressos, considerando a redução significativa de citocinas indicada no artigo durante a resposta imune inflamatória.\
  ![MA_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/9418c34d-a1f1-4ecc-b945-fb4ca3adfff7)
- No Volcano plot, são destacados os genes que ultrapassaram os limites de FDR e log FoldChange, mostrando aqueles regulados positivamente (em vermelho) e negativamente (em azul). Genes "Up" estão significativamente aumentados em expressão na condição de infecção com canabidiol em comparação com a infecção com veículo, enquanto "Down" estão diminuídos.\
  ![VOLCANO_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/afc873c4-7d0c-42fc-a8bc-4d83e061a369)
- Na análise do heatmap, as amostras são exibidas no eixo X, com um dendrograma destacando a similaridade entre seus perfis de expressão gênica. O eixo Y apresenta 1591 genes expressos positivamente, também acompanhados por um dendrograma que mostra a similaridade entre seus níveis de expressão. As amostras são organizadas no heatmap de acordo com o tipo de tratamento, sendo divididas em seis colunas que representam condições experimentais distintas, incluindo tratamentos com canabidiol e com veículo. Isso indica que há três replicatas por tratamento, organizadas em dois grupos principais no heatmap, cada um correspondente a uma condição experimental.\
  ![mais positivo png_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/ec4991ff-9303-4265-a169-1c1b13fd91ed)
  ![mais expresso_page-0001](https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/b543847f-01f9-418d-80fe-5cc3ed489b29)


## Conclusões
A partir dessas informações, acredita-se que ao analisar apenas a expressão de citocinas como fonte de inflamação, o artigo acaba não considerando outras vias que também podem estar relacionadas. Nesse caso, a via purinérgica que está associada como fonte de resposta à eventos inflamatórios, apresenta superexpressão, o que pode indicar uma sobrecarga dessa via devido ao uso do canabidiol, que ao invés de servir como um componente anti-inflamatório, como proposto, pode estar apenas mascarando os efeito de uma via específica, relacionada às citocinas do sistema imune, desta forma, para manter a homeostase do organismo, há uma sobrecarga de outra via.
