# Analise de Feedback de Clientes Bancarios - Engenharia de Prompt e CX Analytics

Estudo de caso e arquitetura de prompt aplicada para processamento de linguagem natural, analise de sentimentos e geracao de relatorios estrategicos de Customer Experience (CX) no setor bancario.

## Visao geral

Este projeto documenta o desenvolvimento de uma solucao baseada em Modelos de Linguagem de Grande Escala (LLMs) para transformar feedbacks textuais nao estruturados de clientes bancarios em inteligencia de negocios acionavel. 

Atraves de tecnicas avancadas de Engenharia de Prompts (como roleplay contextual, delimitadores semanticos, injecao de taxonomia restrita e padronizacao rigorosa de saida), o sistema classifica avaliacoes de clientes, quantifica o sentimento medio e sintetiza um plano de acao priorizado para a diretoria de operacoes.

## Tecnologias e Metodologias

| Camada / Dominio | Tecnologia / Tecnica | Finalidade |
|---|---|---|
| Motor de Processamento | Large Language Models (LLMs) | Processamento de linguagem natural e compreensao de texto nao estruturado |
| Engenharia de Prompts | Roleplay, Delimitadores e Saida Tabular | Ancoragem de comportamento, controle de alucinacoes e determinismo |
| Analise de Sentimento | Taxonomia Granular de CX | Rotulacao sistematica de avaliacoes e priorizacao de urgencia |
| Saida e Integracao | Formato Tabular e Sintese Executiva | Extracao de dados pronta para pipelines SQL e dashboards |

## Arquitetura do Prompt e Metodologia

O prompt foi desenhado seguindo as melhores praticas de alinhamento e ancoragem de LLMs:

1. **Definicao de Papel (Roleplay Contextual):** Atuacao como Analista de Dados Senior especialista em CX bancario, elevando a profundidade analitica e o vocabulário tecnico do modelo.
2. **Taxonomia Rigida de Categorizacao:** Classificacao das mensagens em dimensoes predefinidas:
   - Aplicativo Movel (estabilidade, UI/UX, bugs).
   - Atendimento em Agencias (tempo de espera, atendimento humano).
   - Tarifas e Taxas (transparencia, taxas ocultas, anuidade).
   - Suporte via Chat (resolutividade do chatbot vs atendente humano).
3. **Escala de Sentimentos Padronizada:** Rotulacao binaria ou granular (Positivo, Neutro, Negativo) acompanhada de indicador de urgencia operacional (Baixa, Media, Alta).
4. **Formato de Saida Estruturado:** Exigencia de sintese executiva, tabelas comparativas de metricas e plano de acao em formato SMART.

## Especificacao do Prompt Arquitetado

```text
Atue como um Analista de Dados Senior especializado em Experiencia do Cliente (CX) no setor bancario.

Sua tarefa e analisar uma base de feedbacks de clientes sobre os nossos servicos (aplicativo movel, atendimento nas agencias, taxas e suporte via chat) e gerar um relatorio estrategico para a diretoria.

Diretrizes de Execucao:
1. Categorizacao: Classifique cada feedback em um dos quatro pilares: App, Agencia, Taxas ou Suporte.
2. Sentimento e Urgencia: Atribua o sentimento (Positivo, Neutro ou Negativo) e a urgencia de intervencao (Baixa, Media, Critica).
3. Destaques Qualitativos: Identifique os 3 maiores pontos de atrito (pain points) e as 2 principais fontes de elogio.
4. Tabela Sintetica: Monte uma tabela comparativa com Categoria, Volume Relativo, Sentimento Predominante e Acao Recomendada.
5. Plano de Acao Executivo: Apresente recomendacoes acionaveis divididas em Curto Prazo (quick wins) e Medio/Longo Prazo (melhorias estruturais de produto e TI).

Adote um tom analitico, profissional, baseado em evidencias e orientado a dados.
```

## Estrutura do Relatorio de Saida Gerado

Ao ser submetido com bases de feedbacks reais ou sinteticos, o modelo produz:

1. **Resumo Executivo (Executive Summary):** Visao holistica da saude dos canais bancarios com metricas simuladas de CSAT/NPS.
2. **Matriz de Atrito e Oportunidades:** Mapeamento de problemas criticos (ex: lentidao em transferencias Pix ou filas excessivas de atendimento).
3. **Tabela de Diagnostico Operacional:**
   - Categoria analisada.
   - Diagnostico de causa raiz.
   - Impacto na retencao de clientes (Churn risk).
   - Responsavel pela resolucao (Squad de Produto, Engenharia de Software ou Operacoes de Suporte).
4. **Plano de Remediacao:** Matriz de esforco versus impacto para priorizacao pelo time de gestao.

## Decisoes tecnicas e Mitigacao de Alucinacoes

- **Delimitadores explicitos:** O isolamento dos dados de entrada dentro de marcadores impede a injecao de instrucoes acidentais pelo texto do cliente.
- **Restricao de escopo:** O modelo e instruido a inferir dados estritamente a partir das evidencias do texto fornecido, sem especular sobre servicos nao mencionados.
- **Saida deterministica:** A solicitacao de matrizes tabulares obriga o LLM a seguir um esquema previsivel de colunas, facilitando a extracao e ingestao posterior em pipelines de dados relacionais (PostgreSQL/SQLite) ou dashboards (Power BI/Next.js).
