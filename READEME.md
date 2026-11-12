Brasileirão — Painel de Probabilidades
Dashboard interativo desenvolvido com HTML, CSS e JavaScript para visualizar a classificação do campeonato e estimar cenários possíveis para o restante da competição. A interface foi organizada em páginas, inspirada em ferramentas de Business Intelligence como o Power BI, para concentrar as informações em telas próprias e facilitar a apresentação dos indicadores.
Atenção: este projeto é um painel demonstrativo e independente. Não é um produto oficial da CBF, não consulta uma API em tempo real e não substitui dados ou projeções oficiais. Os resultados dependem da base estática incluída no código e das premissas do modelo de simulação.

Funcionalidades
- Visão geral: indicadores (KPIs) e gráficos de chance de título, risco de rebaixamento, distribuição por zona e pontos atuais, esperados e máximos possíveis.
- Desempenho: gráfico de força de ataque × defesa e visualização dos resultados das últimas cinco partidas (vitórias, empates e derrotas).
- Classificação: tabela com posição, pontos, partidas, vitórias, empates, derrotas, gols, saldo, aproveitamento, forma recente e situação matemática.
- Probabilidades: estimativas de título, classificação para a Libertadores (G4), Pré-Libertadores (5º), Sul-Americana (6º–11º) e rebaixamento (17º–20º).
- Ranking por objetivo: rankings dos clubes para cada um dos objetivos apresentados no painel.
- Mapa de posições: matriz com a probabilidade estimada de cada clube terminar em cada posição.
- Filtros interativos: filtragem por zona atual, situação, clube e risco de queda.
- Detalhes por clube: clique em um clube nas tabelas ou rankings para abrir uma janela com seus indicadores e distribuição de posições projetada.
- Interação com gráficos: alguns gráficos permitem selecionar clubes ou zonas diretamente.
- Exportação CSV: exporta os dados exibidos conforme os filtros ativos.
- Tema claro e escuro: alternância pelo botão de tema.
- Escudos dos clubes: carregamento automático das imagens dos escudos.
- Layout responsivo: em telas grandes, as páginas ocupam a área disponível; em telas menores, o conteúdo se adapta e pode exigir rolagem.
Abas do dashboard
Aba	Conteúdo
Visão geral	KPIs e quatro gráficos de acompanhamento
Desempenho	Força de ataque × defesa e últimas cinco partidas
Classificação	Tabela geral do campeonato
Probabilidades	Probabilidades estimadas para os objetivos do campeonato
Ranking por objetivo	Cinco rankings comparativos
Mapa de posições	Distribuição probabilística das posições finais


Tecnologias utilizadas
- HTML5: estrutura do dashboard.
- CSS3: identidade visual, componentes, temas e adaptação de layout.
- JavaScript: filtros, tabelas, cálculos, simulações e interações.
- Chart.js 4.4.1: construção dos gráficos.
- Google Fonts (Inter e Space Grotesk): tipografia da interface.
Não há backend ou banco de dados. A base utilizada pelo painel está incorporada no próprio arquivo HTML.
Como executar
1. Baixe ou clone este repositório.
2. Mantenha o arquivo dashboard-brasileirao-relatorio-cbf.html e o README.md na mesma pasta.
3. Abra dashboard-brasileirao-relatorio-cbf.html em um navegador atualizado, como Google Chrome, Microsoft Edge ou Firefox.
4. Aguarde a simulação inicial terminar.
Conexão com a internet
O dashboard é executado localmente no navegador, mas alguns recursos são carregados externamente:
- Chart.js, pela CDN do Cloudflare;
- fontes Inter e Space Grotesk, pelo Google Fonts;
- escudos dos clubes, pelo repositório público Escudos dos Clubes do Brasileirão 2026.
Por isso, é recomendável abrir o painel com conexão à internet. Sem acesso à CDN do Chart.js, os gráficos podem não carregar; as tabelas e demais elementos construídos em HTML continuam disponíveis. Caso um escudo remoto não carregue, o painel utiliza as iniciais do clube como alternativa visual.
Como funciona a simulação
O painel executa 40.000 simulações do restante do campeonato para estimar a distribuição de posições e as probabilidades de cada objetivo.

Em linhas gerais, o modelo:
1. Usa os gols marcados, gols sofridos, partidas disputadas e pontos da base estática para representar a situação atual de cada clube.
2. Calcula índices de força ofensiva e defensiva com ajuste em direção à média da liga (regressão à média).
3. Estima os gols das partidas simuladas usando uma distribuição de Poisson e aplica um fator de mando de campo.
4. Gera cenários para os jogos restantes, respeitando a quantidade de partidas pendentes de cada clube.
5. Ordena a classificação simulada por pontos, vitórias, saldo de gols e gols marcados.
6. Consolida os resultados das simulações para estimar pontos esperados, posição média, faixa provável de posições e probabilidades por objetivo.
Como interpretar os resultados
- Probabilidades são estimativas produzidas pelo modelo, não garantias de resultados futuros.
- As indicações de 100%, 0%, campeão matemático e rebaixado matematicamente são tratadas pelo código como certezas matemáticas com base nos pontos atuais e no máximo de pontos que os clubes podem alcançar. O critério de certeza não considera possíveis desempates.
- A faixa de posição apresentada no detalhe do clube corresponde ao intervalo entre os percentis de 5% e 95% da distribuição simulada.
- Os resultados podem mudar quando a base de classificação for atualizada ou quando as premissas do modelo forem modificadas.
Atualização dos dados
Os dados dos clubes ficam no bloco const RAW dentro do arquivo HTML. Cada registro segue esta ordem:
// nome, pontos, partidas, vitórias, empates, derrotas,
// gols marcados, gols sofridos, últimas 5 partidas, cor, sigla
const RAW = [
  ["Flamengo", 76, 34, 23, 7, 4, 71, 29, "VVVVV", "#c8102e", "FLA"],
  // Demais clubes...
];
Ao atualizar a base:
1. Atualize os números de todos os clubes de acordo com a mesma data de referência.
2. Atualize a sequência das últimas cinco partidas usando V para vitória, E para empate e D para derrota.
3. Confira os jogos disputados e os pontos de cada clube.
4. Atualize a data de referência exibida no painel, no trecho que preenche o elemento #sub.
5. Teste os filtros, tabelas, gráficos e exportação CSV depois da alteração.
A quantidade total de rodadas está definida em TOTAL_ROUNDS (38 no arquivo atual). Caso o regulamento ou a competição seja diferente, revise esse valor e as regras de classificação usadas pelo modelo.
Estrutura do projeto
projeto-brasileirao/
├── dashboard-brasileirao-relatorio-cbf.html
└── README.md
Opcionalmente, é possível criar uma pasta logos/ com imagens locais dos escudos. O painel tenta usar arquivos com o identificador do clube no nome, por exemplo logos/flamengo.png, logos/palmeiras.svg ou logos/sao-paulo.webp, caso a imagem remota não esteja disponível.
Observações
- Os dados são estáticos e refletem a data de referência indicada dentro do painel; não são atualizados automaticamente.
- A simulação é executada no navegador do usuário e pode levar alguns instantes dependendo do dispositivo.
- A exportação CSV considera os clubes que estão visíveis com os filtros atuais.
- Para uma apresentação institucional, recomenda-se validar previamente a base de classificação e as premissas estatísticas com a fonte responsável pelos dados.
Projeto: Painel de Probabilidades do Brasileirão
Stack: HTML, CSS e JavaScript
Visualização de dados: Chart.js