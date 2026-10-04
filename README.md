# Gradient Mesh Blobs

Código do vídeo **"Gradient Mesh Blobs"** do canal da [Digital Lift](https://digitallift.com.br).

Fundos orgânicos no estilo Stripe, Linear e Vercel: blobs animados com `border-radius`, o Goo Effect com filtro SVG e a aplicação em uma hero section. **CSS + SVG, zero JavaScript, zero imagens.**

## Como rodar

Abra o `index.html` no navegador.

## Técnica 1: blob com border-radius

```css
.blob {
  /* 4 valores horizontais / 4 verticais = forma orgânica */
  border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
  filter: blur(40px);
  animation: blob1 10s ease-in-out infinite alternate;
}
```

O `@keyframes` interpola entre duas formas de `border-radius`, e o `alternate` faz a animação voltar pelo caminho inverso.

## Técnica 2: Goo Effect

```html
<filter id="goo">
  <feGaussianBlur in="SourceGraphic" stdDeviation="10" result="blur" />
  <feColorMatrix in="blur" type="matrix"
    values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 22 -9" />
</filter>
```

```css
.goo-wrapper { filter: url(#goo); }
```

O blur mistura as bordas dos blobs e o `feColorMatrix` aumenta o contraste do canal alpha: onde os blobs se tocam, eles se fundem.

## Na hero section

- `pointer-events: none` nos blobs, para não bloquear cliques
- um overlay semi-transparente entre os blobs e o texto, para garantir a leitura
- `overflow: hidden` no container e `position: absolute; inset: 0` na camada dos blobs
- bônus: `mix-blend-mode: screen` (linha comentada no fim do CSS) para um visual mais neon

## Arquivos

- `index.html`: hero section, demo do Goo Effect e o filtro SVG
- `style.css`: todo o CSS comentado
