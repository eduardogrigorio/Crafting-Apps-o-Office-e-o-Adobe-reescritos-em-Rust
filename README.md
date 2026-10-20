# 🧰 Crafting Apps: alternativas open source em Rust para fluxos de trabalho de escritório e criação

> *"E se editores de texto, planilhas, imagens e vídeo pudessem ser compilados com `cargo build --release`?"*
> A equipe da [ArtCraft](https://getartcraft.com/) desenvolveu uma família de aplicativos escritos em Rust, de forma independente.

Este guia é um **mapa de referência**: para cada app da família **Craft**, indicamos **qual tipo de fluxo de trabalho ele atende**, quais são os destaques técnicos e **qual é o estágio atual do projeto** (todos estão em *alpha*, conforme os próprios READMEs).

> ⚠️ **Este é um guia independente e não oficial.** Não sou afiliado à Microsoft, à Adobe nem a qualquer outra empresa citada. Veja o [Aviso legal](#️-aviso-legal) e a seção [Motivação e metodologia](#-motivação-e-metodologia).

---

## 🗺️ Resumo rápido

| Repositório | Alternativa para fluxos de trabalho de... | Categoria | Estágio (segundo o README do projeto) |
|---|---|---|---|
| [`wordcraft`](https://github.com/storytold/wordcraft) | Processamento de texto (compatível com `.docx`) | Produtividade | Alpha, ~60% |
| [`gridcraft`](https://github.com/storytold/gridcraft) | Planilhas (compatível com `.xlsx`) | Produtividade | Alpha, ~50% |
| [`deckcraft`](https://github.com/storytold/deckcraft) | Apresentações (compatível com `.pptx`) | Produtividade | Alpha, ~55% |
| [`photocraft`](https://github.com/storytold/photocraft) | Edição de imagens (compatível com `.psd`) | Criação | Alpha inicial |
| [`pdfcraft`](https://github.com/storytold/pdfcraft) | Edição e organização de PDF | Criação | Alpha, ~55% |
| [`effectcraft`](https://github.com/storytold/effectcraft) | Motion graphics e composição | Criação | Alpha, ~45% |
| [`filmcraft`](https://github.com/storytold/filmcraft) | Edição de vídeo não-linear | Criação | Alpha, ~56% |
| [`artcraft-services`](https://github.com/storytold/artcraft-services) | Não é um app: backend do ArtCraft | Infra / serviços | Monorepo de backend + web |

*Os percentuais e estágios são os que cada projeto declara; podem estar desatualizados. Consulte sempre o repositório oficial.*

---

# 🏢 Produtividade

## 📝 WordCraft

**Fluxo de trabalho atendido:** processamento de texto, com suporte ao formato `.docx`.

Editor de textos escrito em Rust. Segundo o README: ribbon, painel de estilos, tabelas, controle de alterações, referências e mala direta.

**Destaques técnicos:**
- 🦀 Roda nativo em Windows, macOS, Linux e BSD, e no navegador via WebAssembly, com GUI nativa em [egui](https://github.com/emilk/egui).
- 📂 Lê e salva `.docx`, `.odt`, `.rtf`, `.html`, `.md`, `.tex` e `.txt`, e exporta PDF.
- ⚡ Re-layout rápido de documentos longos (o projeto cita ~1,4 ms por tecla em 188 páginas).
- 🤖 Centenas de comandos acessíveis por interface, CLI, canal JSON e servidor MCP.
- 🔒 Corretor ortográfico e gramatical offline.

**Estágio:** alpha. Faltam mais testes com documentos reais e fidelidade em gráficos/SmartArt.

---

## 📊 GridCraft

**Fluxo de trabalho atendido:** planilhas, com suporte ao formato `.xlsx`.

**Destaques técnicos:**
- 🧮 500+ funções, incluindo `LET`, `LAMBDA`, `MAP`, `REDUCE` e arrays dinâmicos.
- 🕸️ Motor de cálculo com grafo de dependências e recálculo incremental.
- 📈 17 tipos de gráfico, tabelas dinâmicas, Flash Fill, validação de dados e AutoFiltro.
- 📦 Importa `.csv`, `.tsv`, `.xls`, `.xlsb` e `.ods` (com as limitações descritas no projeto).
- 🕵️ Sem telemetria.

**Estágio:** alpha, ~50%. Próximos passos: fidelidade de XLSX em arquivos reais, planilhas grandes e recálculo multithread.

---

## 📽️ DeckCraft

**Fluxo de trabalho atendido:** apresentações, com suporte ao formato `.pptx`.

**Destaques técnicos:**
- 🔷 150+ formas com handles de ajuste, conectores e operações de mesclar formas.
- 🎞️ Transições, animações, modo apresentador, caneta e ensaio de tempos.
- 📤 Exporta PDF, PNG/JPEG, GIF animado e outlines.
- 🎬 Reprodução de áudio e vídeo em vários codecs.
- 🤖 200+ comandos scriptáveis via CLI, canal JSON e MCP.

**Estágio:** alpha, ~55%.

---

# 🎨 Criação

## 🖼️ PhotoCraft

**Fluxo de trabalho atendido:** edição de imagens em camadas, com suporte a arquivos PSD/PSB.

**Destaques técnicos:**
- 🗂️ Abre, edita e salva PSD/PSB (o projeto reporta preservação de renderização em 307 de 309 arquivos do conjunto de testes `psd-tools`).
- 🧰 67 ferramentas, 16 camadas de ajuste e motor de pincel com sensibilidade a caneta.
- 🎨 RGB, Grayscale, CMYK e Lab em 8, 16 e 32 bits, com gerenciamento de cor ICC.
- ⚡ Compositor em GPU (wgpu) e compositor em CPU usado como referência de testes.
- 🧪 Mais de 1.700 testes.

**Estágio:** early alpha. O próprio README afirma que ainda não substitui ferramentas profissionais no trabalho diário. Faltam recursos de IA generativa, algumas ferramentas e compatibilidade com plug-ins.

---

## 📄 PdfCraft

**Fluxo de trabalho atendido:** leitura, organização, combinação, divisão, comentários, formulários e proteção de PDFs.

**Destaques técnicos:**
- 🔐 Manipulador de segurança do PDF, de RC4 40 bits a AES-256.
- 💾 Salvamento incremental e atômico, verificado com `qpdf` no CI.
- 🛡️ Testado contra 983 arquivos do corpus do pdf.js, sem crashes reportados.
- 🌍 Renderização de diversos sistemas de escrita.
- 🕵️ Sem conta, sem nuvem, sem telemetria.

**Estágio:** alpha. Não converte documentos Office para PDF, a edição de texto existente é limitada e parte da renderização usa a crate `hayro`.

---

## ✨ EffectCraft

**Fluxo de trabalho atendido:** motion graphics e composição.

**Destaques técnicos:**
- 🎛️ 306 efeitos.
- 🧠 Expressões em JavaScript.
- 🎥 Câmeras, luzes e sombras 3D.
- 🧩 Import/export de Lottie e projeto em JSON legível (`.ecproj`), amigável a diffs no Git.
- 🚫 Encoders de VP9, AV1, HEVC e Opus implementados em Rust, sem FFmpeg.

**Estágio:** alpha jovem (primeiro commit em 1º de outubro de 2026). Não abre `.aep` e não executa plug-ins de terceiros. O projeto estima ~45% do caminho para uso profissional.

---

## 🎬 FilmCraft

**Fluxo de trabalho atendido:** edição de vídeo não-linear.

**Destaques técnicos:**
- 🧬 Codecs próprios em Rust, implementados a partir de especificações públicas: H.264, HEVC, ProRes e AAC.
- ⏱️ Base de tempo em inteiros (254.016.000.000 ticks/s), sem deriva em frame rates comuns.
- 🌈 Correção de cor em luz linear 32-bit float, com scopes.
- 🔊 Loudness EBU R128 / ITU-R BS.1770.
- 🔁 Intercâmbio via FCP7 XML, FCPXML, OpenTimelineIO, EDL CMX 3600, AAF e OMF.
- 🤖 650+ comandos controláveis por MCP.

**Estágio:** alpha, ~56%. Não importa `.prproj`, não hospeda plug-ins e a exportação H.264 é o único codec de entrega em software.

---

# ☁️ Repositório de infraestrutura

## `artcraft-services`

Não é um aplicativo de desktop: é o **backend e o front-end web do ArtCraft**, estúdio de IA para imagem e vídeo da mesma equipe (o app desktop está em [`storytold/artcraft`](https://github.com/storytold/artcraft)).

- 🦀 Backend em Rust (Actix Web + Tokio): autenticação, contas, upload de mídia, fila de gerações, créditos e cobrança via Stripe.
- ⚛️ Frontends em React + TypeScript (Nx, Vite, Three.js).
- 🧠 Roteador de geração que conversa com vários provedores de IA.
- 🔑 API programática (`/v1/omni_api`) com chave de API.
- 🗄️ MySQL, Redis, Elasticsearch e armazenamento compatível com S3/R2.

> Este repositório tem **licença própria** (`LICENSE.md`). Leia-a antes de qualquer reutilização.

---

# 🧭 Motivação e metodologia

> **Nota para quem mantém este guia:** esta seção só deve conter fatos verdadeiros e que você possa comprovar. Preencha os campos entre `[colchetes]` com a sua realidade e apague o que não se aplicar. Não afirme "clean room", "sem acesso a código proprietário" ou similares se isso não for rigorosamente verdade.

## Por que estes projetos existem

O custo de licenças de software comercial de produtividade e criação é uma barreira real para estudantes, profissionais autônomos, pequenas equipes e organizações em países com moeda desvalorizada. A motivação por trás dos projetos open source desta lista é oferecer **alternativas acessíveis, auditáveis e sem telemetria**, que permitam trabalhar com formatos de arquivo amplamente usados.

[Descreva aqui, com suas palavras e em primeira pessoa, o seu contexto real: por exemplo, quem você é, qual foi o problema de custo que enfrentou e por que decidiu documentar ou desenvolver estas alternativas.]

## Como o trabalho foi conduzido

[Preencha apenas o que for verdadeiro. Sugestão de pontos a documentar:]

- **Formatos abertos e especificações públicas.** O suporte a formatos como OOXML (ECMA-376 / ISO/IEC 29500), PDF (ISO 32000), ODF (ISO/IEC 26300) e codecs com especificação publicada foi implementado a partir da documentação pública desses padrões. `[confirme]`
- **Sem código ou ativos de terceiros.** Não foram usados código-fonte, binários, ícones, fontes, imagens, textos de interface ou arquivos de recurso de produtos comerciais. `[confirme]`
- **Sem engenharia reversa ou descompilação** de software comercial, e sem contornar licenças, DRM ou termos de uso. `[confirme]`
- **Testes com arquivos próprios ou de corpus públicos** (por exemplo, os conjuntos de teste citados nos READMEs dos projetos), e não com arquivos de terceiros obtidos sem autorização. `[confirme]`
- **Papel neste repositório.** `[Este guia apenas descreve e organiza informações dos projetos listados / eu sou autor de X / colaboro em Y.]`
- **Fonte das informações.** Os dados vêm dos READMEs públicos dos repositórios, consultados em outubro de 2026. Estágio e números são declarados pelos próprios projetos e não foram verificados de forma independente por este guia. `[ajuste se você verificou algo]`

## O que este guia não é

- Não é incentivo a pirataria, a violação de licenças ou a descumprimento de termos de uso de nenhum software.
- Não afirma que qualquer app aqui substitui produtos comerciais; todos estão em alpha e cada pessoa deve avaliar se atende às suas necessidades.
- Não é comparação de desempenho ou qualidade com produtos de terceiros.

---

# 🚀 Quer testar?

Tudo roda com **Rust 1.95+**. Execute os comandos **na sua máquina**, dentro da pasta do repositório clonado. Antes de compilar ou executar qualquer projeto de terceiros, revise o código e confirme que o repositório é o oficial.

```bash
# Exemplo com o WordCraft:
git clone https://github.com/storytold/wordcraft
cd wordcraft
cargo run --release -p wordcraft -- --sample
```

| App | Comando |
|---|---|
| WordCraft | `cargo run --release -p wordcraft -- --sample` |
| GridCraft | `cargo run --release -p gridcraft -- --sample sales` |
| DeckCraft | `cargo run --release -p deckcraft-cli -- render --sample --all --scale 1 out/` |
| PhotoCraft | `cargo run --release -p photocraft -- image.psd` |
| PdfCraft | `cargo run --release -p pdfcraft -- arquivo.pdf` |
| EffectCraft | `cargo run --release -p effectcraft -- --demo` |
| FilmCraft | `cargo run --release -p filmcraft` |

Os repositórios também oferecem instaladores na aba *Releases* e versão web (WebAssembly), segundo seus READMEs. Instale somente a partir dos canais oficiais.

---

## ⚖️ Aviso legal

- Este é um **guia independente e informativo**, **sem vínculo, afiliação, patrocínio ou endosso** da Microsoft, da Adobe ou de qualquer outra empresa citada.
- Microsoft, Word, Excel, PowerPoint, Office, Adobe, Photoshop, Acrobat, After Effects, Premiere Pro e outros nomes são **marcas de seus respectivos titulares**. Aparecem aqui **apenas para identificar formatos de arquivo e fluxos de trabalho com os quais os projetos declaram compatibilidade** (uso descritivo). Nenhum logotipo, ícone, captura de tela ou material de terceiros é usado.
- Os apps Craft são distribuídos sob suas próprias licenças (segundo seus READMEs, MIT ou Apache-2.0, à escolha do usuário). O `artcraft-services` possui licença própria. **Consulte o `LICENSE` de cada repositório**; este guia não substitui esses termos.
- As informações vêm dos READMEs públicos dos projetos (consultados em outubro de 2026) e **podem conter imprecisões ou estar desatualizadas**. Este guia é fornecido "como está", sem garantias. Verifique os dados nos repositórios oficiais antes de tomar decisões.
- Este conteúdo é opinião e informação geral, **não constitui aconselhamento jurídico**.

## 📬 Correções e remoções

Se você é titular de direitos, mantenedor de um dos projetos ou encontrou um erro, abra uma *issue* neste repositório ou escreva para `[seu e-mail de contato]`. Corrigiremos ou removeremos o conteúdo apontado de forma célere e de boa-fé.

---

<p align="center">
 
</p>
