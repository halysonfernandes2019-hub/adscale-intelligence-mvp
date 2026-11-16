# AdScale Intelligence · MVP

Plataforma web em português para registrar ofertas e acompanhar sinais públicos de atividade publicitária. Inclui dashboard, busca e filtros, agrupamento por anunciantes, histórico por oferta, snapshots diários manuais, score heurístico 0–100, insights e alertas entre observações, importação CSV/JSON e exportações.

## Executar

O frontend é HTML/CSS/JavaScript sem dependências. Abra `index.html` no navegador (ou hospede esta pasta em qualquer servidor HTTP). Para testes locais use `python3 -m http.server 8080` e visite `http://localhost:8080`.

## Funcionamento de dados

- **Demonstração:** dados totalmente fictícios para conhecer o painel; nunca são exportados como registros reais.
- **Meu workspace:** dados reais que você adiciona ou importa. Armazenamento local (`localStorage`), isolado por navegador e origem. Não é banco multiusuário ou backup permanente.
- **Snapshots:** somente datas verificadas são computadas. O sistema nunca inventa observações em dias sem consulta.
- **Alertas:** calculados comparando dois registros da mesma oferta; não significam faturamento/vendas/ROAS.
- **Integração Meta:** endpoint opcional `api/meta.js` para Vercel, requer autorização e credenciais. A API oficial permite anúncios gerais de UE/Reino Unido e anúncios políticos elegíveis noutras regiões; não cobre todos os anúncios comerciais brasileiros de forma automatizada.

## Configurar API oficial da Meta no Vercel

No projeto Vercel, defina as variáveis **somente no servidor**:

- `META_AD_LIBRARY_TOKEN`: token de acesso autorizado da Meta Ads Library API.
- `META_QUERY_KEY`: senha aleatória longa para proteger o endpoint de consultas; o usuário digita essa chave na busca de API (não é persistida).
- `META_GRAPH_VERSION`: opcional, atualmente `v27.0`.

A API acessa `GET /api/meta?q=...&country=GB` com o cabeçalho `x-adscale-key`. O health check `GET /api/meta?health=1` informa se as credenciais estão configuradas sem expô-las.

**Importante:** não coloque o token Meta em `app.js`, URL pública, repositório ou armazenamento do navegador. A biblioteca da Meta tem regras de uso e controle de acesso. A API apenas devolve uma página (até 25 anúncios) no MVP.

## CSV

Use as colunas:

`offer_name,advertiser,country,niche,ad_count,creative_count,start_date,date,status,ad_url,site_url,notes`

Datas são `YYYY-MM-DD`; status `active`, `inactive`, `unknown`. Uma linha representa uma observação por oferta e data. Ao importar duas linhas com mesmo anunciante e nome, elas compõem o histórico da mesma oferta.

## Atualização diária automática — fase seguinte

Este MVP **não coleta todos os dias sozinho**. Para isso é preciso: (1) fonte autorizada ou parceiro com cobertura de mercado suficiente, (2) base persistente no servidor, (3) jobs agendados (por exemplo Vercel Cron), (4) logs de coleta e controles contra falsos negativos, (5) autenticação e controle de acesso. Isso não pode ser simulado com `localStorage` ou informações criadas artificialmente.

## Metodologia do score

- Longevidade 30 pontos, volume de anúncios 30, crescimento positivo 22, observações recentes 12, volume de criativos 6.
- Score heurístico: sinais de atividade, não escala financeira comprovada.
- Sem duas observações, não há pontuação de crescimento e o score é preliminar.

## Arquivos

- `index.html`: layout e navegação.
- `styles.css`: interface responsiva dark SaaS.
- `app.js`: estado, cálculos, telas, formulários, importação/exportação e interações.
- `api/meta.js`: conector seguro opcional à API oficial, usado somente com credenciais configuradas no servidor.
- `vercel.json`: configuração de função serverless.