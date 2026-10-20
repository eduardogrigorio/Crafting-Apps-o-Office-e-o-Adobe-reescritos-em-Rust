# Crafting-Apps-o-Office-e-o-Adobe-reescritos-em-Rust
Este guia é um mapa de tradução: pra cada app da família Craft, mostramos qual programa comercial ele "imita", o que ele tem de nerd por baixo do capô e qual é o estágio real do projeto (spoiler: todo mundo está em alpha, e eles mesmos admitem isso).

# 🧰 Crafting Apps: o Office e o Adobe, reescritos em Rust

> *"E se o Word, o Photoshop e o Premiere fossem compilados com `cargo build --release`?"*
> A galera da [ArtCraft](https://getartcraft.com/) respondeu: **reescreveu tudo do zero em Rust**, sem Electron, sem FFmpeg e sem pedir licença pra ninguém.

Este guia é um **mapa de tradução**: pra cada app da família **Craft**, mostramos **qual programa comercial ele "imita"**, o que ele tem de nerd por baixo do capô e **qual é o estágio real do projeto** (spoiler: todo mundo está em *alpha*, e eles mesmos admitem isso).

---

## 🗺️ Resumo rápido

| Repositório | Equivale a... | Categoria | Estágio (segundo o próprio README) |
|---|---|---|---|
| [`wordcraft`](https://github.com/storytold/wordcraft) | 📝 **Microsoft Word** | Pacote Office | Alpha, ~60% pronto pra uso real |
| [`gridcraft`](https://github.com/storytold/gridcraft) | 📊 **Microsoft Excel** | Pacote Office | Alpha, ~50% |
| [`deckcraft`](https://github.com/storytold/deckcraft) | 📽️ **Microsoft PowerPoint** | Pacote Office | Alpha, ~55% |
| [`photocraft`](https://github.com/storytold/photocraft) | 🖼️ **Adobe Photoshop** | Pacote Adobe | Alpha inicial |
| [`pdfcraft`](https://github.com/storytold/pdfcraft) | 📄 **Adobe Acrobat** | Pacote Adobe | Alpha, ~55% no uso cotidiano |
| [`effectcraft`](https://github.com/storytold/effectcraft) | ✨ **Adobe After Effects** | Pacote Adobe | Alpha, ~45% |
| [`filmcraft`](https://github.com/storytold/filmcraft) | 🎬 **Adobe Premiere Pro** | Pacote Adobe | Alpha, ~56% |
| [`artcraft-services`](https://github.com/storytold/artcraft-services) | ☁️ **Não é um app: é o backend do ArtCraft** | Infra / serviços | Monorepo de backend + web |

---

# 🏢 Time "Office"

## 📝 WordCraft → o "Word" que não pede assinatura

**Equivalente a:** Microsoft Word

O processador de textos que fala `.docx` fluentemente, mas é escrito em Rust puro. Tem a **ribbon** no lugar de sempre, painel de estilos com preview ao vivo, tabelas, controle de alterações, referências, mala direta... a ficha completa do Word, só que open source.

**Nerdices:**
- 🦀 Roda **nativo** em Windows, macOS, Linux e BSD, e **dentro do navegador** via WebAssembly. Sem Electron, sem Tauri: GUI nativa com [egui](https://github.com/emilk/egui) na GPU.
- 📂 Além de `.docx`, lê e salva `.odt`, `.rtf`, `.html`, `.md`, `.tex` e `.txt`, e exporta PDF com texto selecionável.
- ⚡ Re-layout de um documento de 188 páginas em ~1,4 ms por tecla digitada.
- 🤖 **422 comandos** acessíveis por ribbon, atalhos, CLI, canal JSON e **servidor MCP**. Ou seja: uma IA consegue editar seu documento do mesmo jeito que você.
- 🔒 Corretor ortográfico e gramatical funcionando **offline**.

**Realidade:** alpha. Falta testar com mais `.docx` do mundo real e manter gráficos/SmartArt num ida-e-volta.

---

## 📊 GridCraft → o "Excel" sem a assinatura mensal

**Equivalente a:** Microsoft Excel

Planilha de alta performance, com **fórmulas, tabelas dinâmicas, gráficos, formatação condicional e sparklines**, tudo escrito em Rust. O formato nativo é **XLSX**.

**Nerdices:**
- 🧮 **500+ funções**, incluindo as hypadas: `LET`, `LAMBDA`, `MAP`, `REDUCE`, `SCAN`, `BYROW`, `BYCOL`, `MAKEARRAY`, mais arrays dinâmicos com *spilling*.
- 🕸️ Motor de cálculo com **grafo de dependências** e recálculo incremental. Só recalcula o que mudou.
- 📈 17 tipos de gráfico, tabelas dinâmicas (pivot), Flash Fill, validação de dados e AutoFiltro.
- 📦 Importa `.csv`, `.tsv`, `.xls` (valores/fórmulas), `.xlsb` e `.ods` (valores).
- ⌨️ Até as *keytips* de Alt/F10 da ribbon estão lá.
- 🕵️ Zero telemetria, zero servidor de licença.

**Realidade:** alpha, ~50% pronto. Próximos passos: fidelidade de XLSX em arquivos reais, planilhas gigantes e recálculo multithread.

---

## 📽️ DeckCraft → o "PowerPoint" feito em Rust

**Equivalente a:** Microsoft PowerPoint

Monta apresentações com temas, layouts, formas, tabelas, gráficos, transições e animações. Abre e salva `.pptx` e apresenta em tela cheia.

**Nerdices:**
- 🔷 **150+ formas** prontas com *handles* de ajuste e conectores que "grudam" nas formas, além de operações de mesclar formas (união, interseção, subtração...).
- 🎞️ Transições (até **Morph**), animações de entrada/saída/trajetória, modo apresentador, caneta e ensaio de tempos.
- 📤 Exporta PDF, PNG/JPEG, **GIF animado** do deck inteiro e outlines.
- 🎬 Toca áudio e vídeo (H.264, HEVC, VP9, AV1...).
- 🤖 200+ comandos scriptáveis via CLI, canal JSON e MCP.

**Realidade:** alpha, ~55% pronto.

---

# 🎨 Time "Adobe"

## 🖼️ PhotoCraft → o "Photoshop" open source

**Equivalente a:** Adobe Photoshop

O carro-chefe da família (e de longe o mais famoso: ~69 mil estrelas no GitHub). Camadas, máscaras, camadas de ajuste, estilos de camada, texto, vetores, pincéis e, o ponto mais ambicioso, **arquivos PSD de verdade**.

**Nerdices:**
- 🗂️ Abre, edita e salva **PSD/PSB**; na bateria de testes, o re-save preserva a renderização de 307 de 309 arquivos do conjunto psd-tools.
- 🧰 **67 ferramentas**, **16 camadas de ajuste** (Curves, Levels, Selective Color, Gradient Map...) e motor de pincel com pressão/inclinação de caneta.
- 🎨 RGB, Grayscale, **CMYK e Lab** em 8, 16 e 32 bits, com gerenciamento de cor ICC em Rust puro.
- ⚡ Compositor na GPU (wgpu: Metal, Vulkan, DX12, WebGPU) e um compositor na CPU como "gabarito" pra testar o da GPU.
- 🧪 Mais de 1.700 testes.

**Realidade:** *early alpha*. O próprio README diz que **ainda não substitui o Photoshop no trabalho profissional diário**. Faltam recursos de IA generativa, algumas ferramentas e compatibilidade com plug-ins.

---

## 📄 PdfCraft → o "Acrobat" sem dor de cabeça

**Equivalente a:** Adobe Acrobat

A "bancada de trabalho" de PDF: ler, organizar, combinar, dividir, comentar, preencher formulários e proteger documentos.

**Nerdices:**
- 🔐 Implementa o manipulador de segurança do PDF **completo**: de RC4 40 bits até **AES-256**.
- 💾 Cada salvamento é **incremental** (os bytes originais ficam intactos) e atômico, verificado com `qpdf` no CI.
- 🛡️ Testado contra 983 arquivos do corpus do pdf.js: **0 crashes**.
- 🗃️ Organiza páginas como cartas numa mesa, combina arquivos mantendo links, formulários e camadas.
- 🌍 Renderiza scripts do mundo todo (árabe, devanágari, japonês vertical, emoji colorido).
- 🕵️ Sem conta, sem nuvem, sem telemetria.

**Realidade:** alpha. Ainda **não converte documentos Office para PDF**, a edição de texto existente é limitada e parte da renderização ainda usa a crate `hayro` emprestada.

---

## ✨ EffectCraft → o "After Effects" que roda no navegador

**Equivalente a:** Adobe After Effects

Motion graphics e composição: composições, camadas, keyframes, efeitos, expressões, câmeras 3D e fila de render. Os painéis (Project, Timeline, Effect Controls...) e até os atalhos (`P`, `S`, `R`, `T`...) seguem o After Effects.

**Nerdices:**
- 🎛️ **306 efeitos** (simulação de partículas, Glow, Fractal Noise, Timewarp, Layer Styles...).
- 🧠 **Expressões em JavaScript** com o modelo de objetos do AE (`wiggle`, `loopOut`, `thisComp.layer("…")`).
- 🎥 Câmeras, luzes e sombras 3D com *ray tracing* suave.
- 🧩 **Import/export de Lottie** nativo e projeto em **JSON legível** (`.ecproj`) que dá diff limpinho no Git.
- 🚫 **Sem FFmpeg**: os encoders de VP9, AV1, HEVC e Opus são código Rust próprio.

**Realidade:** alpha jovem (primeiro commit em 1º de outubro de 2026). **Não abre `.aep`** e plug-ins do After Effects não rodam. Estima-se ~45% do caminho para substituir o AE em trabalho profissional.

---

## 🎬 FilmCraft → o "Premiere Pro" feito do zero

**Equivalente a:** Adobe Premiere Pro

Editor de vídeo não-linear profissional, com monitores Source/Program, bins, timeline multitrack, colorização, mixagem de áudio, títulos, legendas e exportação.

**Nerdices:**
- 🧬 Os **codecs são próprios**, escritos em Rust a partir das especificações: H.264, HEVC, ProRes e AAC. Nada de FFmpeg dentro (ele só serve de "oráculo" nos testes).
- ⏱️ Tempo **exato em inteiros**: 254.016.000.000 ticks por segundo, divisível por todo frame rate comum. 23,976 e 29,97 drop-frame sem aproximação, então as edições nunca "derivam".
- 🌈 Corretor de cor com curvas, rodas, HSL secundário e scopes (waveform e vectorscope), tudo em **luz linear 32-bit float**.
- 🔊 Loudness EBU R128 / ITU-R BS.1770, mixer com automação estilo console.
- 🔁 Intercâmbio com outros editores: FCP7 XML, FCPXML, OpenTimelineIO, EDL CMX 3600, AAF e OMF.
- 🤖 650+ comandos controláveis por MCP: um agente de IA consegue cortar, colorir e exportar.

**Realidade:** alpha, ~56% pronto. **Não importa `.prproj`** (use XML/AAF/OTIO), não hospeda plug-ins e a exportação H.264 é o único codec de entrega em software.

---

# ☁️ O "intruso" da lista

## `artcraft-services` → não é um app, é a casa de máquinas

**Equivalente a:** *nenhum aplicativo da Adobe*, porque este repositório é **infraestrutura**.

Se os apps acima são os "programas de desktop", este é o **backend e o front-end web do ArtCraft**, o estúdio de IA para imagem e vídeo da mesma equipe (o app desktop vive em [`storytold/artcraft`](https://github.com/storytold/artcraft)).

**O que tem lá dentro:**
- 🦀 **Backend em Rust** (Actix Web + Tokio): autenticação, contas, upload de mídia, fila de gerações, créditos e cobrança via Stripe.
- ⚛️ **Frontends em React + TypeScript** (workspace Nx, Vite, Three.js) para o app web e o site do produto.
- 🧠 Um **roteador de geração** que fala com vários provedores de IA para gerar **imagem, vídeo, áudio, malha 3D e *splats***.
- 🔑 Uma **API programática** (`/v1/omni_api`) com chave de API para gerar mídia e consultar o status dos jobs.
- 🗄️ Stack de apoio: MySQL, Redis, Elasticsearch e armazenamento compatível com S3/R2.

> 💡 **Analogia (e só analogia):** é o tipo de "cozinha" que existe por trás de ferramentas de IA generativa na nuvem. Não há um equivalente 1:1 na lista de apps da Adobe.

---

# 🎁 Bônus: os irmãos que ficaram de fora

A família **Crafting Apps** tem mais gente. Pelas descrições do próprio README, o paralelo com a Adobe seria este:

| App | O que faz | Parece com |
|---|---|---|
| `vectorcraft` | Ilustração vetorial | Illustrator |
| `lightcraft` | Biblioteca de fotos e revelação RAW | Lightroom |
| `designcraft` | Diagramação e publicação | InDesign |

*(Os nomes dos programas equivalentes aqui são uma associação pelo tipo de ferramenta; confira cada repositório para detalhes.)*

---

# 🚀 Quer testar? (nível "nerd de terminal")

Tudo roda com **Rust 1.95+**. Os comandos abaixo são para executar **na sua estação de trabalho**, dentro da pasta do repositório clonado, não em servidor.

```bash
# Exemplo com o WordCraft (na sua estação, em qualquer terminal com Rust instalado):
git clone https://github.com/storytold/wordcraft
cd wordcraft
cargo run --release -p wordcraft -- --sample
```

| App | Comando (dentro da pasta do repo, na sua estação) |
|---|---|
| WordCraft | `cargo run --release -p wordcraft -- --sample` |
| GridCraft | `cargo run --release -p gridcraft -- --sample sales` |
| DeckCraft | `cargo run --release -p deckcraft-cli -- render --sample --all --scale 1 out/` |
| PhotoCraft | `cargo run --release -p photocraft -- image.psd` |
| PdfCraft | `cargo run --release -p pdfcraft -- arquivo.pdf` |
| EffectCraft | `cargo run --release -p effectcraft -- --demo` |
| FilmCraft | `cargo run --release -p filmcraft` |

Prefere não compilar? Cada repositório tem **instaladores prontos** (MSI, DMG, AppImage, Flatpak, .deb, .rpm) na aba *Releases*, e também uma versão **web (WebAssembly)**.

---

## ⚖️ Aviso nerd-jurídico

Esses são projetos **independentes e open source** (licença MIT ou Apache-2.0, à sua escolha, nos apps Craft). **Não são afiliados, patrocinados ou endossados** pela Microsoft nem pela Adobe. Os nomes Word, Excel, PowerPoint, Photoshop, Acrobat, After Effects, Premiere Pro e afins são marcas dos respectivos donos e aparecem aqui apenas para descrever os fluxos de trabalho com os quais cada app é compatível. O repositório `artcraft-services` tem licença própria (`LICENSE.md`), então confira antes de reutilizar.

*Dados de estrelas e estágio de maturidade vêm dos READMEs dos repositórios, consultados em outubro de 2026, e mudam rápido (todos estão em desenvolvimento ativo).*

---

<p align="center">
  Feito com ☕, <code>cargo</code> e muita curiosidade 🦀
</p>
