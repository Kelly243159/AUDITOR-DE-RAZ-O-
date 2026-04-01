Auditoria de Padrões Contábeis
Ferramenta web para auditoria de lançamentos contábeis. Compara um arquivo atual com um histórico de padrões, detecta divergências de contas e inversões Débito/Crédito, e gera relatórios visuais com estatísticas e padrões detectados por inteligência artificial.

✨ Funcionalidades
Upload duplo: Carregue um arquivo de histórico padrão e o arquivo a ser auditado.

Processamento automático: Ignora cabeçalhos (primeiras 9 linhas), identifica cada lançamento como Débito (coluna I) ou Crédito (coluna J) e extrai conta (coluna H) e descrição (coluna C).

Comparação inteligente: Encontra a melhor correspondência no histórico por similaridade de descrição (mínimo 60%).

Classificação de divergências:

✅ OK – conta e tipo corretos

✕ CONTA_ERRADA – tipo correto, conta diferente

↔ TIPO_ALTERADO – conta correta, tipo trocado

✕✕ AMBOS – conta e tipo divergentes

? NOVO – sem correspondência no histórico

Painel de estatísticas: Total analisado, itens corretos, contas erradas, tipos trocados, score de conformidade.

Padrões detectados pela IA: Identifica automaticamente problemas recorrentes (descrições com muitas falhas, inversão predominante, novos lançamentos).

Tabela de auditoria: Exibe todos os lançamentos com filtros por status, descrição e conta.

Terminal de log: Acompanhe cada etapa do processamento.

Totalmente client-side: Não requer servidor, funciona diretamente no navegador.

🚀 Como Usar
Abra o arquivo index.html (ou hospede em um servidor web) com um navegador moderno.

Carregue o arquivo de histórico padrão (base de referência).

Carregue o arquivo atual (aquele que será auditado).

Clique em Iniciar Análise de Padrões.

Aguarde o processamento – uma animação indicará que a IA está analisando.

Visualize os resultados no painel de estatísticas, nos cards de padrões e na tabela detalhada.

Use os filtros para refinar a visualização.

📁 Formato dos Arquivos
Ambos os arquivos devem ser planilhas Excel (.xlsx, .xls ou .csv), com a primeira aba contendo os dados.

Mapeamento de colunas (fixo, conforme painel de configuração)
Campo	Coluna (índice)	Descrição
Nº Lançamento	B (2)	Identificador do lançamento
Descrição	C (3)	Texto que descreve o lançamento
Conta	H (8)	Número da conta contábil
Débito (Entrada)	I (9)	Valor se for débito (entrada)
Crédito (Saída)	J (10)	Valor se for crédito (saída)
Regras de processamento:

As primeiras 9 linhas são ignoradas (cabeçalhos).

Uma linha é considerada válida se:

A descrição (coluna C) não estiver vazia.

O valor em I ou J for maior que zero (determina o tipo).

O tipo é definido como Débito se I > 0, Crédito se J > 0.

Se ambos forem zero ou vazios, a linha é ignorada.

🧠 Lógica de Comparação
Para cada lançamento do arquivo atual, a ferramenta:

Calcula a similaridade textual com cada lançamento do histórico (ignorando caracteres especiais e palavras curtas).

Seleciona a melhor correspondência com similaridade ≥ 60%.

Se encontrada, compara conta e tipo; se não, classifica como NOVO.

📊 Painel de Estatísticas
Indicador	Descrição
Total Analisado	Número de lançamentos processados
Padrões Corretos	Lançamentos OK
Conta Incorreta	Apenas conta divergente
Tipo Alterado	Apenas tipo invertido (Débito↔Crédito)
Ambos Errados	Conta e tipo divergentes
Score de Conformidade	Percentual de acertos (100% – % de erros)
🔍 Padrões Detectados pela IA
O sistema identifica automaticamente padrões de comportamento:

Descrições Problemáticas: aquelas que aparecem em muitos erros.

Inversão Débito/Crédito: quando o tipo trocado é o erro predominante.

Contas Incorretas: quando a conta errada é o erro predominante.

Novos Lançamentos: itens sem correspondência no histórico.

Cada padrão exibe um nível de confiança estimado e uma breve descrição.

🛠️ Configuração
O painel de configuração (no topo) exibe os parâmetros fixos:

Ignorar primeiras linhas: 9 (padrão)

Coluna Conta: H

Coluna Débito: I → Entrada

Coluna Crédito: J → Saída

Coluna Descrição: C

Coluna Nº Lançamento: B

Para alterar esses mapeamentos, é necessário editar o código JavaScript (variáveis SKIP_ROWS, COL_NUMERO, etc.) – consulte a seção de personalização abaixo.

💻 Requisitos Técnicos
Navegador web com suporte a JavaScript (Chrome, Firefox, Edge, Safari).

Sem necessidade de instalação de softwares adicionais.

Os arquivos são processados localmente – nenhum dado é enviado para servidores.

🧪 Personalização
Caso seu arquivo tenha estrutura diferente, você pode ajustar as constantes no início da função processData():

javascript
const SKIP_ROWS = 9;          // linhas de cabeçalho a ignorar
const COL_NUMERO = 1;         // coluna B (0-indexed)
const COL_DESCRICAO = 2;      // coluna C
const COL_CONTA = 7;          // coluna H
const COL_DEBITO = 8;         // coluna I
const COL_CREDITO = 9;        // coluna J
Altere também o texto no painel de configuração para refletir as novas colunas.

🐛 Solução de Problemas
Arquivo não carrega: Verifique se é realmente um Excel válido (.xlsx, .xls ou .csv). O navegador deve permitir a leitura local (arquivos carregados via <input> são permitidos).

Nenhum lançamento processado: Confirme que as colunas estão nos índices corretos e que as primeiras 9 linhas realmente contêm cabeçalhos. Se houver linhas vazias, elas serão ignoradas.

Muitos "NOVO": A similaridade mínima é 60%. Se as descrições variam muito, reduza esse limite no código (função performAnalysis, linha if (sim > melhorSimilaridade && sim >= 60)).

Erro ao analisar: Abra o console do navegador (F12) para ver mensagens de erro detalhadas.

📄 Licença
Este projeto é distribuído sob a licença MIT. Sinta-se à vontade para usar, modificar e compartilhar.

Desenvolvido para agilizar auditorias contábeis com tecnologia de inteligência artificial.
