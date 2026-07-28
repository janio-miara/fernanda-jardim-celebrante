# Fernanda Jardim — Celebrante

Landing page de Fernanda Jardim, celebrante de casamentos, formaturas, congressos e homenagens em Santa Catarina.

## Sobre o projeto

Site estático de página única, sem dependências de build. Tudo (HTML, CSS e JS) vive em `index.html`; as imagens ficam em `assets/img/`.

- **Tipografia:** Cormorant Garamond (títulos) + Jost (texto), via Google Fonts
- **Paleta:** verdes oliva/sage da marca, com neutros quentes (creme, areia, taupe)
- **Formulário de orçamento:** monta um resumo formatado e abre o WhatsApp já preenchido — não exige backend
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
assets/img/           fotos e monograma
```

## Editar

- **Telefone do WhatsApp:** constante `WHATSAPP` no script ao final de `index.html`
- **Valores do investimento:** seção `#investimento`
- **Cores e espaçamentos:** bloco `:root` no topo do `<style>`
