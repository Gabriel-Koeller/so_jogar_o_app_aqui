# React + TypeScript + Vite + Tailwind CSS

Este projeto foi configurado com React, TypeScript, Vite e Tailwind CSS.

## ⚠️ PROBLEMA CRÍTICO: Tailwind CSS v4 vs v3

### O Problema

Durante um teste presencial, foi instalado o **Tailwind CSS v4** (versão mais recente), mas essa versão tem uma configuração completamente diferente da v3, causando erros e impedindo que os estilos CSS funcionassem na aplicação.

### Erro Encontrado

Ao tentar executar `npm run dev`, o seguinte erro aparecia:

```
[postcss] It looks like you're trying to use `tailwindcss` directly as a PostCSS plugin. 
The PostCSS plugin has moved to a separate package, so to continue using Tailwind CSS with 
PostCSS you'll need to install `@tailwindcss/postcss` and update your PostCSS configuration.
```

### Por Que Isso Aconteceu?

O **Tailwind CSS v4** (lançado em 2024) introduziu mudanças significativas:

1. **Plugin PostCSS separado**: A v4 requer o pacote `@tailwindcss/postcss` separado
2. **Sintaxe CSS diferente**: A v4 usa `@import "tailwindcss"` ao invés de `@tailwind base/components/utilities`
3. **Configuração diferente**: Não usa mais o `tailwind.config.js` da mesma forma
4. **Ainda em desenvolvimento**: A v4 ainda está em fase beta/alpha e pode ter problemas de compatibilidade

### Como Identificar o Problema

**Sintomas:**
- ✅ Instalação do Tailwind pareceu bem-sucedida
- ❌ Classes do Tailwind não funcionam (ex: `bg-gray-100`, `text-red-500`)
- ❌ Erro no console sobre PostCSS plugin
- ❌ Estilos não são aplicados na aplicação

**Verificar a versão instalada:**
```bash
npm list tailwindcss
```

Se mostrar versão `4.x.x`, você está com o problema!

### Solução: Usar Tailwind CSS v3 (Recomendado)

A **v3** é estável, bem documentada e amplamente suportada. Use ela para projetos de produção e testes.

#### Passos para Corrigir:

1. **Desinstalar a v4:**
```bash
npm uninstall tailwindcss @tailwindcss/postcss
```

2. **Instalar a v3:**
```bash
npm install -D tailwindcss@^3 postcss autoprefixer
```

3. **Configurar o PostCSS** (`postcss.config.js`):
```js
export default {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

4. **Configurar o Tailwind** (`tailwind.config.js`):
```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

5. **Configurar o CSS** (`src/index.css`):
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

6. **Reiniciar o servidor:**
```bash
npm run dev
```

### Como Evitar no Futuro

1. **Sempre especifique a versão ao instalar:**
```bash
npm install -D tailwindcss@^3 postcss autoprefixer
```

2. **Verifique a versão antes de começar:**
```bash
npm list tailwindcss
```

3. **Use a documentação oficial da v3:**
   - Site: https://tailwindcss.com/docs
   - A v4 ainda não tem documentação completa

4. **Em testes/entrevistas:**
   - Se possível, use a v3 (mais estável)
   - Se precisar usar v4, estude a nova configuração antes
   - Tenha um projeto de referência configurado com v3

### Diferenças Principais: v3 vs v4

| Aspecto | Tailwind v3 | Tailwind v4 |
|---------|-------------|-------------|
| **Instalação** | `npm install -D tailwindcss` | `npm install -D tailwindcss @tailwindcss/postcss` |
| **PostCSS Config** | `tailwindcss: {}` | `'@tailwindcss/postcss': {}` |
| **CSS Syntax** | `@tailwind base;` | `@import "tailwindcss";` |
| **Config File** | `tailwind.config.js` | Configuração diferente |
| **Estabilidade** | ✅ Estável | ⚠️ Beta/Alpha |
| **Documentação** | ✅ Completa | ⚠️ Limitada |

### Comandos Úteis

```bash
# Verificar versão instalada
npm list tailwindcss

# Instalar v3 (recomendado)
npm install -D tailwindcss@^3 postcss autoprefixer

# Instalar v4 (não recomendado para produção)
npm install -D tailwindcss@next @tailwindcss/postcss

# Limpar cache e reinstalar
rm -rf node_modules package-lock.json
npm install
```

### Recursos

- [Documentação Tailwind CSS v3](https://tailwindcss.com/docs)
- [Guia de Instalação com Vite](https://tailwindcss.com/docs/guides/vite)
- [Tailwind CSS v4 (Beta)](https://tailwindcss.com/blog/tailwindcss-v4-beta)

---

## 🚀 Como Executar o Projeto

```bash
# Instalar dependências
npm install

# Executar em desenvolvimento
npm run dev

# Build para produção
npm run build

# Preview da build
npm run preview
```