# Atividade sobre Agentes Inteligentes

**Aula:** 20/10/2026  
**Professora:** Kadidja Valéria  
**Disciplina:** Linguagens Formais e Autômatos — Ciência da Computação  
**Estudante:** Guilherme R. de Almeida  
**Turma:** Ciência da Computação — N1

Atividade individual baseada no Capítulo 2 de *Inteligência Artificial*, de Russell e Norvig, com análise de racionalidade, caracterização PEAS e modelos de agentes.

## Preparação

A racionalidade consiste em selecionar uma ação que maximize o **desempenho esperado**, dados o histórico de percepções, o conhecimento prévio e as ações disponíveis. O ambiente de tarefa pode ser descrito por **PEAS**: desempenho, ambiente, atuadores e sensores. As classificações abaixo são condicionadas às hipóteses declaradas em cada cenário.

## Exercício 2.3 — Verdadeiro ou falso

Para cada item, apresenta-se julgamento, justificativa e exemplo ou contraexemplo.

### a. Um agente que detecta apenas informações parciais sobre o estado não pode ser perfeitamente racional.

- **Julgamento:** F
- **Justificativa:** A racionalidade não exige acesso completo ao estado do mundo. Ela exige a melhor ação em termos de desempenho esperado, tendo como base a informação que o agente conseguiu obter e o conhecimento que já possuía. Confundir racionalidade com observação perfeita equivaleria a exigir onisciência.
- **Exemplo ou contraexemplo:** Um aspirador com sensores apenas para a área atual pode limpar quando identifica sujeira e explorar os outros locais. Dependendo da medida de desempenho e das condições do ambiente, essa política é racional mesmo sem um mapa completo.

### b. Existem ambientes de tarefa nos quais nenhum agente reativo puro pode comportar-se racionalmente.

- **Julgamento:** V
- **Justificativa:** O agente reativo puro escolhe uma ação considerando somente a percepção corrente. Se duas situações diferentes apresentam a mesma percepção, mas demandam ações diferentes para atingir o melhor desempenho, o agente precisará de alguma memória ou estado interno.
- **Exemplo ou contraexemplo:** Em um labirinto com corredores indistinguíveis, um robô que não registra os caminhos visitados pode retornar repetidamente ao mesmo lugar. Um agente que mantém a posição e o histórico de exploração consegue decidir melhor.

### c. Existe um ambiente de tarefa em que todo agente é racional.

- **Julgamento:** V
- **Justificativa:** Sim. Se a medida de desempenho atribuir exatamente o mesmo resultado a todas as sequências possíveis de ações, não existe decisão superior a outra. Assim, qualquer comportamento maximiza o desempenho esperado.
- **Exemplo ou contraexemplo:** Em uma tarefa artificial em que o resultado é sempre 10 pontos, independentemente de o agente pressionar A, pressionar B ou permanecer parado, todos os agentes têm desempenho ótimo.

### d. A entrada para o programa de agente é a mesma que a entrada para a função de agente.

- **Julgamento:** F
- **Justificativa:** A função de agente é uma descrição abstrata que associa uma sequência inteira de percepções a uma ação. O programa que implementa essa função normalmente processa a percepção atual e pode manter memória interna para representar as anteriores.
- **Exemplo ou contraexemplo:** A função do aspirador é expressa sobre um histórico como [(A, sujo), (A, limpo), (B, limpo)]. O código em execução recebe, naquele instante, a percepção (B, limpo), podendo consultar o estado que armazenou.

### e. Toda função de agente é implementável por uma combinação de programa/máquina.

- **Julgamento:** F
- **Justificativa:** Uma função matemática pode especificar decisões para infinitos históricos possíveis, mas isso não garante a existência de um algoritmo capaz de calculá-la. Existem funções não computáveis, além de limitações físicas de memória e tempo.
- **Exemplo ou contraexemplo:** Uma função que, para qualquer programa recebido, determina corretamente se sua execução terminará exigiria resolver o problema geral da parada; não há programa universal que a implemente.

### f. Suponha que um agente selecione sua ação uniformemente ao acaso do conjunto de ações possíveis. Existe um ambiente de tarefa determinista em que esse agente é racional.

- **Julgamento:** V
- **Justificativa:** Em um ambiente determinístico, a escolha aleatória pode ser racional caso todas as ações disponíveis sejam igualmente boas em qualquer situação relevante. Ser determinístico não significa que apenas uma ação possa ser ótima.
- **Exemplo ou contraexemplo:** Uma máquina com três botões entrega invariavelmente 5 pontos ao pressionar qualquer um deles, sem custos. Selecionar os botões com probabilidades iguais não reduz o desempenho.

### g. É possível para um dado agente ser perfeitamente racional em dois ambientes de tarefa distintos.

- **Julgamento:** V
- **Justificativa:** A mesma política pode maximizar o desempenho esperado em mais de um ambiente, desde que as condições das tarefas sejam compatíveis com as ações escolhidas. Ambientes diferentes não exigem obrigatoriamente agentes diferentes.
- **Exemplo ou contraexemplo:** Um aspirador que detecta e aspira sujeira pode agir racionalmente em duas salas com disposições distintas, se a tarefa e os sensores permitirem que sua política limpe ambas com desempenho ótimo.

### h. Todo agente é racional em um ambiente não observável.

- **Julgamento:** F
- **Justificativa:** Mesmo sem sensores, o agente ainda pode dispor de conhecimentos prévios e de uma medida de desempenho. Algumas ações serão melhores do que outras; não observar o mundo não torna todos os comportamentos igualmente adequados.
- **Exemplo ou contraexemplo:** Um agente sem sensores sabe que o botão A rende 10 pontos e o B rende zero. Escolher sempre B é irracional, mesmo sem receber novas percepções.

### i. Um agente jogador de pôquer perfeitamente racional nunca perde.

- **Julgamento:** F
- **Justificativa:** Racionalidade maximiza resultados esperados, não garante vitórias reais. O pôquer inclui cartas ocultas, aleatoriedade e adversários; uma escolha correta com base nas probabilidades ainda pode perder em uma rodada.
- **Exemplo ou contraexemplo:** Um jogador pode apostar racionalmente com uma mão forte, mas as cartas seguintes podem completar uma combinação superior para outro participante.

## Exercício 2.4 — Modelo PEAS e classificação

**PEAS:** P = medida de desempenho; E = ambiente; A = atuadores; S = sensores. O termo *estocástico* nas situações físicas e sociais indica incerteza prática no resultado, e não que as leis físicas sejam aleatórias. O conhecimento das **regras** de uma tarefa não implica observação completa do **estado** do ambiente.

### Caso 1 — Jogar futebol

- **Agente analisado e hipóteses:** Um jogador humano de uma equipe com onze integrantes; partida tradicional, adversários ativos e regras conhecidas. Seu objetivo é contribuir para a vitória.
- **P — Medida de desempenho:** Vitória da equipe, gols, passes eficazes, marcação e respeito às regras.
- **E — Ambiente:** Campo, bola, companheiros, adversários, arbitragem e clima.
- **A — Atuadores:** Pernas, pés, cabeça e movimentos corporais para correr, passar, marcar e chutar.
- **S — Sensores:** Visão, audição, tato, equilíbrio e propriocepção.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | O jogador não percebe todo o campo nem conhece a intenção de cada adversário. |
| Número de agentes | Multiagente: cooperativo e competitivo | Coopera com seu time e compete com a equipe contrária. |
| Previsibilidade | Estocástico | Erros de execução, desvios e reações dos demais jogadores tornam os resultados incertos. |
| Dependência entre decisões | Sequencial | Um passe altera o posicionamento e as escolhas da jogada seguinte. |
| Mudança durante a decisão | Dinâmico | Bola e jogadores se movem enquanto se decide. |
| Natureza dos elementos | Contínuo | Posições, velocidades e forças de chutes variam continuamente. |
| Conhecimento do funcionamento | Conhecido | As regras e a dinâmica básica do jogo são conhecidas, embora o resultado exato não seja. |

### Caso 2 — Explorar os oceanos subterrâneos de Titã

- **Agente analisado e hipóteses:** Um submarino robótico autônomo em uma missão **hipotética**; pressupõe-se a existência de uma região líquida acessível sob a crosta. Deve coletar dados com segurança.
- **P — Medida de desempenho:** Dados científicos obtidos, extensão mapeada, economia de energia e preservação da sonda.
- **E — Ambiente:** Meio líquido subterrâneo hipotético, obstáculos, relevo, pressão e correntes.
- **A — Atuadores:** Propulsores, mecanismos de coleta, controle de flutuabilidade e comunicação.
- **S — Sensores:** Sonar, sensores de pressão, temperatura e composição, giroscópios e câmeras adequadas.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | Os instrumentos observam somente parte do espaço ao redor. |
| Número de agentes | Agente único | Assume-se apenas uma sonda, sem outros agentes decisórios. |
| Previsibilidade | Estocástico | Correntes e obstáculos desconhecidos dificultam a previsão das consequências. |
| Dependência entre decisões | Sequencial | Rotas escolhidas e gasto de energia condicionam a exploração futura. |
| Mudança durante a decisão | Dinâmico | Pressupõem-se correntes ou outras condições locais variáveis. |
| Natureza dos elementos | Contínuo | Profundidade, pressão, posição e velocidade são grandezas contínuas. |
| Conhecimento do funcionamento | Desconhecido | O comportamento detalhado e a geografia local precisam ser descobertos. |

### Caso 3 — Comprar livros usados de IA na Internet

- **Agente analisado e hipóteses:** Agente de software autorizado a buscar e comprar livros dentro de um limite de orçamento. Consideram-se plataformas e vendedores independentes.
- **P — Medida de desempenho:** Aderência à edição desejada, conservação, custo total e prazo de entrega.
- **E — Ambiente:** Sites de sebos, catálogos, vendedores, compradores e serviços de entrega.
- **A — Atuadores:** Chamadas HTTP/APIs, consulta a anúncios, preenchimento de formulários e pedido digital.
- **S — Sensores:** Respostas de APIs, HTML, fotos, preços, avaliações e informação de estoque.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | Fotos e descrições não revelam necessariamente a conservação real ou a confiabilidade do vendedor. |
| Número de agentes | Multiagente | Vendedores e compradores podem alterar ofertas e disponibilidade. |
| Previsibilidade | Estocástico | Existem incertezas de estoque, entrega e condição efetiva do produto. |
| Dependência entre decisões | Sequencial | Comparar, reservar e comprar muda orçamento e oportunidades posteriores. |
| Mudança durante a decisão | Dinâmico | Anúncios e preços podem mudar durante a pesquisa. |
| Natureza dos elementos | Discreto | A modelagem considera anúncios, cliques, itens e transações digitais. |
| Conhecimento do funcionamento | Conhecido | O agente conhece as operações da plataforma; não conhece necessariamente os dados privados dos vendedores. |

### Caso 4 — Jogar uma partida de tênis

- **Agente analisado e hipóteses:** Um tenista humano contra outro jogador, seguindo as regras da modalidade. Objetivo: vencer sets e a partida.
- **P — Medida de desempenho:** Pontos, games e sets vencidos, precisão dos golpes e poucos erros.
- **E — Ambiente:** Quadra, rede, bola, raquete, oponente, árbitro e condições externas.
- **A — Atuadores:** Braços, mãos e pernas para golpear, sacar e se deslocar.
- **S — Sensores:** Visão, audição, equilíbrio, tato e percepção do próprio corpo.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | A intenção tática do adversário e alguns parâmetros da bola não são conhecidos exatamente. |
| Número de agentes | Multiagente competitivo | Ambos buscam a vitória, adaptando-se um ao outro. |
| Previsibilidade | Estocástico | Golpes e quiques têm variações práticas e os adversários são imprevisíveis. |
| Dependência entre decisões | Sequencial | Cada golpe define o tipo de retorno e as possibilidades seguintes. |
| Mudança durante a decisão | Dinâmico | Bola e adversário se movimentam durante a decisão. |
| Natureza dos elementos | Contínuo | Tempo, ângulos, força e trajetórias são contínuos. |
| Conhecimento do funcionamento | Conhecido | Regras e princípios básicos do movimento são familiares ao jogador. |

### Caso 5 — Praticar tênis contra uma parede

- **Agente analisado e hipóteses:** Um tenista humano praticando sozinho diante de uma parede rígida; busca manter as devoluções e aumentar a precisão.
- **P — Medida de desempenho:** Número de devoluções, regularidade e acerto da região-alvo.
- **E — Ambiente:** Parede, piso, bola, raquete e condições físicas do local.
- **A — Atuadores:** Braços, pernas e movimentos necessários para rebater a bola.
- **S — Sensores:** Visão, audição, tato, equilíbrio e propriocepção.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | A percepção não mede exatamente rotação, velocidade e ponto de contato da bola. |
| Número de agentes | Agente único | A parede é passiva e não toma decisões. |
| Previsibilidade | Estocástico | No treino real, pequenas variações no golpe e na superfície produzem resultados incertos. |
| Dependência entre decisões | Sequencial | A batida atual determina o próximo retorno. |
| Mudança durante a decisão | Dinâmico | A bola se desloca enquanto o jogador prepara outro golpe. |
| Natureza dos elementos | Contínuo | Trajetória, velocidade e tempo variam continuamente. |
| Conhecimento do funcionamento | Conhecido | As propriedades mecânicas gerais do choque contra a parede são conhecidas. |

### Caso 6 — Realizar um salto de altura

- **Agente analisado e hipóteses:** Um atleta durante uma única tentativa, sem interferência direta dos concorrentes. Deve ultrapassar o sarrafo em segurança.
- **P — Medida de desempenho:** Altura superada, tentativa válida, técnica e segurança.
- **E — Ambiente:** Pista, sarrafo, suportes, colchão e condições atmosféricas.
- **A — Atuadores:** Pernas, braços e tronco para correr, impulsionar e controlar a postura.
- **S — Sensores:** Visão, equilíbrio, tato e propriocepção.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | O atleta não conhece precisamente todas as forças e condições corporais instantâneas. |
| Número de agentes | Agente único | Na tentativa considerada, não há outro decisor interferindo diretamente. |
| Previsibilidade | Estocástico | Variações de impulso, aderência e equilíbrio afetam a execução. |
| Dependência entre decisões | Sequencial | Passadas iniciais condicionam o ângulo e a velocidade da impulsão. |
| Mudança durante a decisão | Dinâmico | Durante a aproximação, o corpo e sua posição mudam mesmo enquanto decide. |
| Natureza dos elementos | Contínuo | Posição, velocidade, altura e trajetória são contínuas. |
| Conhecimento do funcionamento | Conhecido | A técnica e as leis mecânicas gerais são conhecidas. |

### Caso 7 — Participar de um leilão de um item

- **Agente analisado e hipóteses:** Agente de software em um leilão eletrônico aberto, com lances e prazo visíveis. Não pode ultrapassar a avaliação máxima do usuário.
- **P — Medida de desempenho:** Arrematar quando vantajoso, evitar preços excessivos e respeitar o limite.
- **E — Ambiente:** Plataforma, item, outros licitantes, regras e relógio do leilão.
- **A — Atuadores:** Enviar lances por interface/API, desistir ou confirmar operações.
- **S — Sensores:** Lances exibidos, notificações, prazo restante e respostas da plataforma.

| Propriedade | Classificação | Justificativa |
|---|---|---|
| Observabilidade | Parcialmente observável | Os limites de orçamento e estratégias de outros participantes são ocultos. |
| Número de agentes | Multiagente competitivo | Outros licitantes disputam o mesmo item. |
| Previsibilidade | Estocástico | Não se conhecem antecipadamente os lances dos concorrentes. |
| Dependência entre decisões | Sequencial | Ofertas alteram o preço corrente e as decisões posteriores. |
| Mudança durante a decisão | Dinâmico | O prazo avança e novos lances podem aparecer durante a decisão. |
| Natureza dos elementos | Discreto | Na modelagem, lances e incrementos monetários são quantizados. |
| Conhecimento do funcionamento | Conhecido | As regras da disputa são conhecidas, mas as decisões privadas dos demais não. |

### Comparação final

1. **Tênis contra uma pessoa versus contra a parede:** Na partida, há um adversário com estratégia e objetivos próprios, tornando o sistema multiagente e competitivo. A parede não decide como devolver a bola; o retorno depende das condições físicas do impacto. Nos dois casos a bola continua em movimento e as decisões são sequenciais.
2. **Informação incompleta ao comprar livros usados:** As ofertas mostram somente dados selecionados pelos vendedores. Fotografias podem ocultar páginas rasgadas, anotações ou defeitos; avaliações não garantem a entrega. O agente deve usar os indícios disponíveis sem confundir o anúncio com o estado real do produto.
3. **Influência de outros agentes no futebol e no leilão:** No futebol, companheiros colaboram e adversários dificultam jogadas; o agente precisa considerar ambos. No leilão, ofertas concorrentes modificam preço e oportunidades, exigindo avaliação estratégica do limite de gasto.

## Exercício 2.5 — Conceitos e exemplos

### Agente
- **Definição:** Entidade que recebe percepções de um ambiente por sensores e realiza ações nele por atuadores. Pode ser uma pessoa, um robô ou um sistema de software.
- **Exemplo:** Um aspirador robótico detecta sujeira e obstáculos e controla seus motores e o mecanismo de sucção.

### Função de agente
- **Definição:** Relação matemática abstrata que associa a cada sequência possível de percepções uma ação. Define o comportamento esperado sem determinar seu código.
- **Exemplo:** Uma função que associa o histórico de localização e sujeira de um aspirador à próxima ação de limpar ou deslocar-se.

### Programa de agente
- **Definição:** Implementação concreta da função de agente em uma arquitetura computacional. Processa percepções recebidas e pode atualizar uma memória interna antes de emitir ações.
- **Exemplo:** Código em Java que lê sensores e decide quando acionar os motores de um robô.

### Racionalidade
- **Definição:** Selecionar a ação que maximiza a medida de desempenho esperada com base nas percepções acumuladas, no conhecimento disponível e nas ações possíveis. Não é garantia de acerto em todos os resultados.
- **Exemplo:** Um aplicativo de rotas escolhe o caminho com menor duração prevista, mesmo que um incidente inesperado ocorra depois.

### Autonomia
- **Definição:** Capacidade de orientar o comportamento a partir da própria experiência e das percepções, reduzindo a dependência exclusiva das regras ou conhecimentos fornecidos pelo projetista.
- **Exemplo:** Um robô identifica em quais regiões aparece mais sujeira e passa a priorizá-las.

### Agente reativo
- **Definição:** Um agente reativo simples aplica regras condição–ação sobre a percepção presente sem utilizar o histórico das percepções como estado interno.
- **Exemplo:** Um termostato liga o aquecedor ao detectar temperatura abaixo do limite ajustado.

### Agente baseado em modelo
- **Definição:** Mantém uma representação interna de aspectos do ambiente, atualizada a partir das percepções e do conhecimento sobre como o mundo evolui. Isso permite atuar quando nem tudo é observável.
- **Exemplo:** Um robô de limpeza memoriza quais cômodos já foram visitados mesmo quando deixam de aparecer em seus sensores.

### Agente baseado em objetivos
- **Definição:** Usa a representação do estado e um objetivo explícito para escolher ações capazes de conduzir a uma situação desejada. Pode precisar planejar vários passos.
- **Exemplo:** Um sistema de navegação monta uma rota para chegar ao endereço escolhido.

### Agente baseado em utilidade
- **Definição:** Compara resultados possíveis por uma medida de preferência ou utilidade, permitindo avaliar alternativas mesmo quando há mais de um objetivo ou existe incerteza.
- **Exemplo:** Um planejador de viagens equilibra preço, duração e conforto para selecionar a opção mais vantajosa.

### Agente com aprendizagem
- **Definição:** Ajusta seu comportamento com base nos resultados e nas experiências acumuladas. Pode usar componentes de desempenho, avaliação crítica, aprendizagem e exploração de novas possibilidades.
- **Exemplo:** Um classificador de e-mails melhora a identificação de spam após receber correções do usuário.

## Síntese com autômatos

**Caso escolhido:** Caso 3 — Comprar livros usados de inteligência artificial pela Internet. O agente é um programa que consulta anúncios, avalia ofertas e realiza a compra com autorização e orçamento definidos.

### Três estados internos (Q)

1. **q₀ — Pesquisando:** ainda busca anúncios compatíveis.
2. **q₁ — Avaliando:** já encontrou uma oferta e está conferindo seus critérios.
3. **q₂ — Finalizado:** encerrou a tarefa após confirmar a compra.

### Três percepções (Σ)

1. **p₁ — Livro encontrado:** foi identificado um anúncio pertinente.
2. **p₂ — Oferta aprovada:** o preço e as condições atendem aos critérios.
3. **p₃ — Oferta inadequada:** preço acima do limite ou estado insatisfatório.

### Três ações (A)

1. **a₁ — Pesquisar:** consultar novos anúncios.
2. **a₂ — Comparar:** conferir preço, descrição, frete e avaliação do vendedor.
3. **a₃ — Comprar:** enviar a confirmação da compra à plataforma.

### Duas regras de transição

1. **δ(q₀, p₁) → (q₁, a₂):** quando encontra um livro pertinente, o agente passa de pesquisa para avaliação e compara a oferta.
2. **δ(q₁, p₂) → (q₂, a₃):** quando a oferta atende aos critérios, o agente confirma a compra e encerra a tarefa.

**Representação da informação passada:** O estado `q₁` indica que já houve uma busca bem-sucedida; o agente está analisando algo encontrado anteriormente. Em uma aplicação completa, poderia armazenar o livro selecionado, o histórico de preços e o orçamento disponível. Assim, decisões futuras não dependeriam somente da entrada atual.

**Limitação:** O modelo de três estados não representa todas as situações reais, como estoque esgotado, falha no pagamento, alterações de preço ou avaliação simultânea de vários anúncios. Também resume preços e características contínuas/variadas em poucas categorias discretas. Seriam necessárias mais informações internas e transições para um sistema real.

> **Observação:** As duas regras ilustram parte do comportamento de um autômato com saída do tipo Mealy. Não se pretende especificar toda a função de transição, já que o enunciado solicita apenas duas regras.

---

## Conclusão

A racionalidade de um agente deve ser avaliada em relação à sua medida de desempenho e às informações realmente disponíveis, e não por uma exigência de sucesso infalível. A descrição PEAS ajuda a estabelecer o que constitui a tarefa, como o agente percebe o ambiente e como pode agir. A classificação dos cenários mostra que diferentes níveis de observabilidade, interações entre agentes e incertezas exigem estratégias de decisão distintas. A síntese com autômatos representa parte dessas decisões como estados e transições, embora agentes reais possam demandar modelos mais ricos, memória e aprendizagem.

## Referências

RUSSELL, Stuart; NORVIG, Peter. **Agentes inteligentes**. In: RUSSELL, Stuart; NORVIG, Peter. *Inteligência artificial*. 3. ed. Rio de Janeiro: Elsevier, 2013. cap. 2.

Material disponibilizado pela professora para a atividade de 20/10/2026, disciplina Linguagens Formais e Autômatos — UDF.

