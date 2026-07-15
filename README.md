# Blind Spot — Entrelinhas

Plataforma de inteligência estratégica. Um arquivo único, autônomo, com três lentes a partir de uma home:

- **Análise de empresa** — o Blind Spot completo (motor embutido) para uma empresa.
- **Varredura** — radar dos sinais das últimas horas (cobertura obrigatória de China).
- **Cruzar** — árvore de pontos cegos a partir de um fato × setor.

Tudo roda no navegador e chama a API da Anthropic direto. A chave fica salva **só no navegador do usuário** (localStorage). Para um produto de verdade, o passo seguinte é mover a chamada para um backend.

## Arquivos

```
index.html     → o app inteiro (SPA, sem build, sem dependências locais)
vercel.json    → config estática (todas as rotas servem o index.html)
README.md      → este arquivo
```

Não há `package.json` nem etapa de build: é um site estático.

## Subir no GitHub

No terminal, dentro desta pasta:

```bash
git init
git add .
git commit -m "Blind Spot — versão unificada"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/blind-spot.git
git push -u origin main
```

(Crie antes o repositório vazio em github.com/new.)

## Publicar no Vercel

1. Em [vercel.com](https://vercel.com) → **Add New… → Project**.
2. **Import** o repositório do GitHub.
3. **Framework Preset: Other** (não há build). Root Directory: `/`. Build Command e Output: deixe em branco.
4. **Deploy**.

Pronto. A URL pública serve o `index.html`.

## Marcas (white-label por URL)

O mesmo app se co-marca sozinho conforme o caminho da URL — não há arquivos separados por marca:

- `/` (raiz) → **só Blind Spot** (powered by Entrelinhas).
- `/bradesco` → co-marca **Bradesco** (logo na home e na análise).
- `/oracle` → co-marca **Oracle** (logo).
- `/safra` → co-marca **Safra** (logo; por ser azul-marinho, aparece sobre um chip branco na barra escura).

Como funciona: o `vercel.json` reescreve qualquer rota para o `index.html`, e o app lê o caminho (`/bradesco`, `/oracle`, `/safra`) para escolher a marca. Para demonstrar a cada player, basta enviar a URL com o caminho dele.

**Arquivos de logo** ficam na raiz do deploy (`brand-bradesco.png`, `brand-oracle.png`, `brand-safra.svg`) e são servidos como estáticos — o Vercel entrega o arquivo antes de aplicar a reescrita. Para adicionar uma nova marca, coloque o logo na raiz e me peça para ligá-lo.

## Primeiro uso

Na primeira análise/varredura, o app pede a chave da Anthropic (`sk-ant-...`) e a guarda no navegador. A mesma chave vale para as três lentes.

## Observações

- **Precisa de HTTPS** (o Vercel já entrega isso). A chamada direta à API da Anthropic não funciona ao abrir o arquivo localmente via `file://` por causa de CORS — use a URL do Vercel para testar de verdade.
- **A chave nunca sai do navegador do usuário.** Quando o produto amadurecer, mova a chamada (e a chave) para um backend.
