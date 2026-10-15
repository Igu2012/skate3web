# Skate3Web

Build web local do projeto `skate-3-rust-engine`, com uma interface enxuta e publicação estática em GitHub Pages.

**Site:** https://igu2012.github.io/skate3web/

## Conteúdo

- `engine/`: código-fonte do engine, baseado na branch [`cleanroom-web`](https://github.com/andrewnakas/skate-3-rust-engine/tree/cleanroom-web). A página web foi simplificada para iniciar diretamente no jogo, sem botão de tela cheia.
- `docs/`: build WebAssembly já compilado e arquivos estáticos servidos pelo GitHub Pages. Contém o seletor simples de mapa e os nove parques incluídos na release clean pack.
- `CREDITOS-E-ORIGEM.md`: proveniência dos projetos e dos assets.

Não são incluídos ISOs nem arquivos retail do Skate 3, e os ZIPs opcionais de mods não fazem parte deste pacote.

## Arquivos grandes

O pack principal é dividido em `docs/core.pack.part0` (95.000.000 bytes) e `docs/core.pack.part1`. O `loader.js` carrega as partes e concatena os bytes automaticamente antes de iniciar o engine. Os arquivos do WASM e dos mapas também permanecem abaixo do limite individual de 100 MB do GitHub; não é necessário juntar arquivos manualmente.

## Rodar a página compilada

Use um servidor HTTP estático (não abra `docs/index.html` diretamente como `file://`):

```bash
python3 -m http.server 8000 --directory docs
```

Acesse `http://localhost:8000/` em um navegador Chromium/Edge com suporte a WebGPU e um adaptador gráfico disponível.

## Recompilar a partir do source

A build atual em `docs/` já está pronta. Para recompilar, instale Rust, adicione o alvo `wasm32-unknown-unknown`, instale `wasm-bindgen-cli` na versão `0.2.127` e obtenha a release [Clean pack 2026-10-11](https://github.com/andrewnakas/skate3-cleanroom/releases/tag/clean-pack-2026-10-11). Extraia os dados clean localmente e, a partir de `engine/`, rode no PowerShell:

```powershell
powershell -File tools/build_web.ps1 -Pack <pasta-do-pack-extraído> -Out ../docs -DefaultMap StartPark
```

A documentação técnica completa está em `engine/docs/web.md`.

## Créditos e licença

Veja [`CREDITOS-E-ORIGEM.md`](CREDITOS-E-ORIGEM.md). Este projeto é não oficial e não afiliado à EA; as marcas Skate e Skate 3 pertencem aos respectivos titulares. A atribuição não cria uma licença adicional.
