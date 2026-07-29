# Fernanda Jardim — Celebrante

Landing page de Fernanda Jardim, celebrante de casamentos, formaturas, congressos e homenagens em Santa Catarina.

**Domínio:** https://fernandacelebrante.com.br

## Sobre o projeto

Site estático de página única, sem dependências de build. Tudo (HTML, CSS e JS) vive em `index.html`; as imagens ficam em `assets/img/`.

- **Tipografia:** Cormorant Garamond (títulos) + Jost (texto), via Google Fonts
- **Paleta:** verdes oliva/sage da marca, com neutros quentes (creme, areia, taupe)
- **Acessibilidade:** foco visível, link de pular conteúdo, `prefers-reduced-motion`, contraste revisado
- **Responsivo:** testado de 360px a 1440px

## Rodar localmente

```bash
python3 -m http.server 8000
# abra http://localhost:8000
```

## Estrutura

```
index.html            página completa (markup + estilos + scripts)
index.original.html   versão anterior, mantida como referência
robots.txt            libera a indexação e aponta o sitemap
sitemap.xml           mapa do site para o Google
vercel.json           cache das imagens e cabeçalhos de segurança
assets/img/           fotos, monograma e avatares dos depoimentos
assets/_originais/    cards de depoimento originais (fora do deploy)
```

## Formulário de orçamento

Não exige backend. O visitante preenche os campos e escolhe o canal:

- **Enviar pelo WhatsApp** — abre o WhatsApp com o resumo já formatado
- **Enviar por e-mail** — abre o app de e-mail com assunto e corpo preenchidos

Os dois usam a mesma validação e o mesmo resumo. Endereços ficam nas constantes `WHATSAPP` e `EMAIL`, no início do script ao final do `index.html`.

> **Limitação do e-mail:** o botão depende de o visitante ter um app de e-mail configurado. Em celular quase sempre funciona; em desktop com webmail, às vezes não abre nada. Para a mensagem cair direto na caixa de entrada sem depender do visitante, é preciso um serviço de formulário — veja abaixo.

### Opcional: receber os pedidos direto na caixa de entrada

Serviços como Web3Forms ou Formspree entregam o formulário por e-mail sem backend. O ajuste é pequeno: dar um `action` ao `<form>` e trocar o `preventDefault()` por um `fetch`. Precisa de uma chave gratuita gerada no site do serviço.

## SEO

O que já está configurado:

- `<title>` e meta description com as buscas-alvo (celebrante de casamento + cidade)
- Canonical, Open Graph, Twitter Card e meta tags de geolocalização
- **Dados estruturados JSON-LD:** `ProfessionalService` (com 22 cidades atendidas, catálogo de serviços e depoimentos), `Person`, `WebSite`, `WebPage` e `FAQPage`
- Seção de perguntas frequentes visível, com o mesmo conteúdo do `FAQPage`
- `robots.txt` e `sitemap.xml` com as imagens principais
- Textos alternativos descritivos, `loading="lazy"` e dimensões declaradas nas imagens
- Rodapé com as cidades atendidas, para busca local

### O que ainda depende de você

1. **Google Business Profile** — cadastre em business.google.com. É o que faz aparecer no Maps e no bloco local. Provavelmente vale mais que tudo que está no site.
2. **Google Search Console** — em search.google.com/search-console, adicione o domínio e envie o `sitemap.xml`.
3. **Avaliações no Google** — peça aos casais. Só use `aggregateRating` no JSON-LD quando houver notas reais; inventar nota viola as diretrizes do Google e pode gerar penalidade.
4. **Se o domínio mudar** — atualize em `index.html` (bloco comentado no topo do `<head>`), `robots.txt` e `sitemap.xml`.

### Melhoria de desempenho pendente

As imagens somam ~1,6 MB em JPEG. Converter para WebP reduz a uns 400 KB e melhora o Core Web Vitals. Não havia encoder WebP nesta máquina; para fazer depois:

```bash
brew install webp
cd assets/img
for f in *.jpg; do cwebp -q 80 "$f" -o "${f%.jpg}.webp"; done
```

Depois troque cada `<img src="...jpg">` por `<picture>` com `<source srcset="...webp" type="image/webp">`.

## Editar

- **Telefone e e-mail:** constantes `WHATSAPP` e `EMAIL` no script ao final de `index.html`
- **Valores do investimento:** seção `#investimento` (e a resposta correspondente em `#perguntas` e no JSON-LD)
- **Depoimentos:** seção `#depoimentos` — cada slide é uma `<figure class="testimonial-card">`
- **Cores e espaçamentos:** bloco `:root` no topo do `<style>`
