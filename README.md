# GIL — Galeria Interativa de Lâminas
Criado por estudantes da Unifesp.

Aplicação React/Next.js para estudo e memorização de conteúdos de histologia, com estudos organizados por sistema e suporte a lâminas técnicas.

## Stack

- **Next.js**, **React** e **TypeScript** no site público e no editor local.
- **Tailwind CSS** no editor e **CSS global** no site público.
- **NextAuth.js** para autenticação institucional.
- **Google Gemini** para a Liah, tutora de histologia executada no servidor.
- **React Markdown** para respostas formatadas da Liah.
- **Upstash Redis** para quotas distribuídas em produção.

## Estrutura

```text
gil/
├── web/                         # site público (Next.js)
│   ├── app/                     # páginas, rotas e APIs
│   ├── components/              # componentes React
│   ├── lib/                     # tipos, catálogo e serviços
│   ├── data/                    # catálogo e datasets de histologia
│   └── package.json
└── editor/                      # editor local independente
```

## Estudos atuais

O catálogo inicial contém três estudos, todos sem imagens para preenchimento futuro:

- Sistema urinário: Rim, Ureter, Bexiga urinária e Uretra.
- Sistema reprodutor feminino: Ovário, Tuba uterina, Útero, Colo uterino e Vagina.
- Sistema genital masculino: Testículo, Epidídimo, Ducto deferente, Vesícula seminal, Próstata e Pênis.

Os datasets são compartilhados entre `web/` e `editor/` em `web/data/`.

## Metadados de lâminas

Cada imagem pode conter um objeto `Histologia` com informações técnicas opcionais:

```json
{
  "url": "assets/histologia/sistema-urinario/imagens/rim.png",
  "indicação": "Corpúsculo renal em corte transversal",
  "Histologia": {
    "orgaoTecido": "Rim",
    "estrutura": "Corpúsculo renal",
    "aumento": "100×",
    "objetiva": "10×",
    "coloracao": "Hematoxilina e eosina (HE)",
    "microscopio": "Óptico de campo claro",
    "fonteLamina": "Coleção institucional",
    "observacoes": "Descrição complementar da lâmina."
  }
}
```

A interface pública mostra somente os campos preenchidos em **Informações da lâmina**. O editor permite cadastrar, alterar e remover esses dados sem criar objetos vazios.

## Executando localmente

```bash
cd web
npm install
npm run dev -- -p 8000
```

Acesse `http://localhost:8000`. Para produção, use `npm run build` e `npm run start -- -p 8000`.

O editor é executado separadamente:

```bash
cd editor
npm install
npm run dev
```

Acesse `http://localhost:3000`. O editor grava os mesmos arquivos em `web/data/`.

## Liah e variáveis de ambiente

A Liah é uma tutora de histologia disponível para usuários autenticados com conta Google verificada no domínio `@unifesp.br`. A chamada ao Gemini ocorre exclusivamente no servidor. Nunca use `NEXT_PUBLIC_GEMINI_API_KEY`.

Copie `web/.env.example` para `web/.env.local` e configure as variáveis necessárias. Em produção, configure também `UPSTASH_REDIS_REST_URL` e `UPSTASH_REDIS_REST_TOKEN`. As quotas podem ser ajustadas por `GIL_DAILY_LIMIT` e `GIL_MINUTE_LIMIT`; as variáveis antigas `ANIAH_*` são aceitas temporariamente como fallback.

## Licença e créditos

Consulte o campo `Copyright` de cada imagem para os requisitos de atribuição.

Este projeto é um fork do projeto AnaMed acessível em `https://anamed.vercel.app/`.