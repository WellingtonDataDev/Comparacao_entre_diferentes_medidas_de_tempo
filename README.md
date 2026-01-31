## =========================
##        INSTRUÇÕES
## =========================

As instruções são destinada para pessoas que já possuem experiência prévia na ferramenta Power BI, por isso o passo a passo é voltado diretamente para a solução.

```

Passos:

1. Na tabela {dcalendario}, crie as colunas de [Ano], [Nº Trimestre], [Nº Mês] e [Nº Semana].

2. Ainda na tabela {dCalendario}, crie as colunas de [Ano e Trimestre], [Ano e Mês], e por fim [Ano e Semana]. Deixe em um formato que fique fácil de entender, pois serão as opções a selecionar.

3. Agora crie as colunas que unem de forma numérica as colunas de [Ano e Trimestre], [Ano e Mês], e [Ano e Semana]. Optei em nomear as medidas começando com "Ordem", da seguinte maneira:
    - [Ordem Ano e Trimestre] = Ano * 10 + Trimestre (Dessa forma resultará em algo como 202401, que seria o 1º Trimestre de 2024, por exemplo);
    - [Ordem Ano e Mês] = Ano * 100 + [Nº Mês] (Dessa forma resultará em algo como 2024010, que seria o mês de Outubro de 2024, por exemplo);
    - [Ordem Ano e Semana] = Ano * 100 + [Nº Semana] (Dessa forma resultará em algo como 2024032, que seria a semana 32 de 2024, por exemplo).

4. Crie um novo parâmetro de campo chamado [Tipo Período] e adicione a ele o [Ano], [Ano e Trimestre], [Ano e Mês] e [Ano e Semana]. 

5. Altere a nova segmentação que apareceu para segmentação de botão, caso já esteja siga para o próximo passo.

6. Duplique a segmentação de botão [Tipo Período] e configure uma delas para  "mostrar valores do campo selecionado", clicando com o botão direito do mouse no valor.

7. Se estiver tudo certo: 
    - Em uma segmentação aparecerá os períodos de Ano, Trimestre, Mês e Semana;
    - E na outra segmentação aparecerá os períodos de acordo com a seleção. Por exemplo: com [Ano] selecionado, aparecerá na outra segmentação 2026, 2027 e 2028.

8. Agora com essas medidas criadas, utilize as medidas prontas no arquivo [Medidas.md].

9. Crie uma matriz.

10. Adicone na matriz da seguinte forma:
    - Em linhas, adicione a descrição que está sendo analisada, como por exemplo, as contas de uma DRE;
    - Em colunas, adicione o [Tipo de Período];
    - Em valores, adicione o [Valor a ser comparado], [03 - Diferença (R$)] e [04 - Diferença (%)].

11. Chegando até aqui, você deve conseguir:
    - Selecionar em qual medida de tempo deseja comparar os valores;
    - Selecionar os períodos específicos de cada medida de tempo, como por exemplo: 2024, 2024-1T, Janeiro/2024, Semana 32/2024;
    - Ter a matriz que demonstra toda a comparação.

Espero ter ajudado com um pouco de conhecimento, até a próxima!
