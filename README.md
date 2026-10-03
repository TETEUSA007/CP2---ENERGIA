# CP2---ENERGIA

### Tarefa 1 — interpretação e conclusão

Foram usadas três entradas em `X`: `potencia_kw`, `latitude` e `longitude`. O alvo `y` é `fonte`, com as classes **Solar**, **Eólica** e **Hidráulica**. Não foram usados `SigTipoGeracao`, nomes de empreendimentos, CEG ou descrições de combustível, pois esses campos poderiam revelar diretamente a classe.

A divisão foi feita com **80% para treino e 20% para teste**, de forma **estratificada** e com `random_state=42`. KNN e Regressão Logística foram colocados em `Pipeline` com `StandardScaler`, o que garante que a escala seja aprendida apenas com os dados de treino. O Random Forest não precisa de padronização.

As métricas de Precision, Recall e F1 foram calculadas com média **macro**, para que cada uma das três classes tenha o mesmo peso na comparação, mesmo havendo um pouco mais de exemplos hidráulicos.

Com este conjunto de dados e esta divisão, o **Random Forest** apresentou o melhor desempenho global entre os três modelos, com Accuracy e F1 macro próximos de **0,98**. O KNN também teve desempenho alto, enquanto a Regressão Logística ficou abaixo dos dois modelos não lineares. Isso sugere que a separação entre as fontes não é puramente linear em potência, latitude e longitude.

Na matriz de confusão do Random Forest, a maior parte dos erros envolve **Solar**, principalmente casos solares classificados como Hidráulica ou Eólica. A classe Hidráulica foi reconhecida quase integralmente no conjunto de teste.

Mesmo com bom desempenho, potência e localização **não são suficientes para uma aplicação real sem cautela**. Empreendimentos de fontes diferentes podem ter potências semelhantes e podem existir na mesma região. Além disso, as coordenadas são aproximadas e o conjunto contém possíveis problemas de qualidade cadastral, como coordenadas iguais a zero. Para um sistema real, seriam necessários mais atributos independentes da própria classe, validação em dados novos e análise de possíveis vieses geográficos ou temporais.

**Conclusão:** para este experimento, eu escolheria o **Random Forest**, pois obteve o maior F1 macro e manteve desempenho equilibrado entre as três classes sem exigir uma fronteira linear entre elas.
