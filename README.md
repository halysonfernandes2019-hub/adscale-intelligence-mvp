# AdScale Intelligence — MVP atualizado

Radar de ofertas com filtros e ranking heurístico de sinais públicos de atividade publicitária.

## Busca local (workspace)
- Termos em qualquer ordem, sem diferença entre maiúsculas/minúsculas e acentos.
- Pesquise por oferta, anunciante, nicho, país, notas e links.
- Filtros de país, nicho, status, mínimo de anúncios, score e recência da observação.
- Ordenação por score, relevância, volume, crescimento recente, atualização e cobertura histórica.
- Cadastro de ofertas e observações por data, prevenção de duplicatas, importação CSV/JSON e exportação.
- O histórico fica armazenado **somente no navegador** em que foi registrado, usando localStorage.

## Pesquisa pública na Meta
Na página Radar de ofertas, use **Pesquisar anúncios na Biblioteca da Meta**, informe a palavra-chave e o país e abra a busca oficial. A busca avançada aceita frases exatas e status ativo/inativo. As sugestões são **termos de descoberta**, não anúncios comprovadamente escalados.

Esta versão GitHub Pages é **estática** e não incorpora automaticamente resultados da biblioteca ao radar. Para descobrir e acompanhar ofertas brasileiras automaticamente todos os dias, precisamos contratar/configurar uma fonte autorizada que forneça dados comerciais com cobertura do Brasil, além de um servidor e banco persistente.

## Score
Heurístico de 0 a 100, com ponderação por longevidade informada, anúncios observados, evolução recente, persistência das observações e criativos. Aplica descontos quando o histórico é insuficiente/desatualizado ou o anúncio está marcado como inativo.
A **cobertura histórica** separada representa distribuição/quantidade de observações, **não** verificação independente dos dados.

Nenhuma classificação comprova faturamento, ROAS, investimento ou lucratividade; a Meta não publica esses números para anúncios comerciais comuns.

## Publicação
GitHub Pages, com `index.html` na raiz e branch `main`.
Desenvolvimento local: abra `index.html` no navegador. Nenhuma dependência de build é necessária.

## Próximos módulos
1. Conector autorizado de dados Meta/comerciais reais e configuração de credenciais no servidor.
2. Banco centralizado (ofertas, anúncios individuais, snapshots, fontes e logs de coleta).
3. Agendador diário, controle de falhas, alertas e painel de auditoria.
4. Consolidação de anúncios duplicados por anunciante, página de vendas e fingerprint criativo.

Data da revisão: 16/11/2026.
