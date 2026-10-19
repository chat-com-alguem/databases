# Bases do Chat com alguém

Bases de mensagens prontas para o [chat-com-alguem](https://github.com/chat-com-alguem/chat): cada pasta é uma base, com as mensagens (ou trechos), as fontes de onde saíram e o que é preciso para conferir cada uma.

| Base | O que tem | Trechos | Fontes |
|---|---|---|---|
| [`2026-brasil-eleicoes-segundo-turno`](2026-brasil-eleicoes-segundo-turno/) **(padrão do chat)** | Propostas de governo das 14 candidaturas do 2º turno de 2026 (Presidente e Governador), registradas no TSE, e a ficha oficial de cada uma | 17.673 | 25 documentos oficiais do TSE |
| [`vorcaro-pf-2026`](vorcaro-pf-2026/) | Mensagens do celular de Daniel Vorcaro reproduzidas em relatório da Polícia Federal | 668 | 1 relatório público (218 páginas) |
| [`inconfidencia-mineira-1789`](inconfidencia-mineira-1789/) | Interrogatórios de Tiradentes e dos outros réus, a sentença de 1792 e a execução, nos Autos de Devassa | 3.615 | 2 volumes dos Autos de Devassa (TJMG), domínio público |
| [`machado-de-assis`](machado-de-assis/) | Cartas de Machado de Assis e Joaquim Nabuco, crônicas de "A Semana", Dom Casmurro e Memórias Póstumas | 8.820 | 4 PDFs em domínio público (Brasiliana USP e MEC) |
| [`confissoes-santo-agostinho`](confissoes-santo-agostinho/) | Os treze livros das Confissões de Santo Agostinho, numa tradução portuguesa de 1905 e na inglesa de Pusey (1838) | 2.982 | 2 traduções em domínio público (Internet Archive e Project Gutenberg) |

Cada pasta tem um `README.md` que explica a base: de onde vem, como foi transcrita, o que ficou de fora e as ressalvas.

## Usar as bases no chat

Clone este repositório **ao lado** do chat (o instalador do chat já faz isso):

```bash
git clone https://github.com/chat-com-alguem/chat.git chat-com-alguem
git clone https://github.com/chat-com-alguem/databases.git
```

O chat carrega **todas** as bases desta pasta. Na tela, o botão **Base: ...** (no topo) abre a lista: marque uma ou várias e pergunte. Com várias, cada resposta mostra de qual base veio cada mensagem. Numa conversa nova vem marcada a `2026-brasil-eleicoes-segundo-turno`; para mudar isso, na pasta `chat-com-alguem`, edite o `.env`:

```bash
# chat-com-alguem/.env
BASE_PADRAO=vorcaro-pf-2026                                       # uma
BASE_PADRAO=machado-de-assis,inconfidencia-mineira-1789           # várias
```

**Base nova:** coloque a pasta aqui dentro, ao lado das outras, e religue o chat (`./scripts/chat.sh parar` e `./scripts/chat.sh iniciar`; no Windows, `scripts\chat.cmd`). Na primeira vez com cada base, o chat monta o índice de busca dela (a tela mostra o progresso); depois, sobe em segundos.

Passo a passo completo, inclusive sem Docker e no Windows: **[Escolher e adicionar bases](https://github.com/chat-com-alguem/chat/blob/main/docs/trocar-de-base.md)**.

## Gerar uma base nova

Use o [agente-extrator](https://github.com/chat-com-alguem/agente-extrator). Ele lê posts do X, páginas web, PDFs (longos e escaneados), prints e conversas exportadas do WhatsApp e grava uma pasta neste formato, já validada pelas regras do chat:

```bash
cd agente-extrator
agente-extrator https://x.com/jkrums/status/1121915133 relatorio.pdf --dados ../databases/minha-base
```

Várias fontes viram uma base só, e o chat responde sobre todas, citando de onde veio cada mensagem. Exemplos para cada tipo de fonte estão no [README do agente](https://github.com/chat-com-alguem/agente-extrator#exemplos-um-para-cada-tipo-de-entrada). O formato de uma base está em [formato-dos-dados.md](https://github.com/chat-com-alguem/chat/blob/main/docs/formato-dos-dados.md).

## Conferir uma fonte

Cada fonte em `sources.yaml` traz os links e a **impressão digital (SHA-256)** do arquivo original. Se um único caractere do arquivo mudar, o número muda. Para conferir, baixe o original pelo link e rode:

| Sistema | Comando |
|---|---|
| Linux | `sha256sum arquivo.pdf` |
| macOS | `shasum -a 256 arquivo.pdf` |
| Windows (PowerShell) | `Get-FileHash arquivo.pdf -Algorithm SHA256` |

O resultado tem de ser igual ao `sha256` da fonte. O chat faz a mesma conferência antes de mostrar uma página ou uma cópia arquivada.

## Contribuir com uma base

Bases novas e correções entram por *pull request*. Antes de aprovar, cada fonte é conferida:

1. **Fonte pública e verificável.** Todo documento precisa de link para o original ou do arquivo com SHA-256. Nada de vazamento, fonte anônima ou material sob sigilo.
2. **Posts de rede social e páginas de notícia** precisam da cópia arquivada (o agente-extrator guarda em `arquivos/`, com SHA-256) e, se possível, de um link do Wayback Machine ou do archive.today.
3. **Dados pessoais mascarados** em conversas privadas (telefones, documentos, endereços). O validador do chat recusa a base se encontrar um telefone sem máscara.
4. **Base válida.** O chat precisa subir com ela. O agente-extrator já grava só bases válidas. Antes do *pull request*, rode no chat o teste que confere todas as bases desta pasta: `cd ../chat-com-alguem && python -m pytest tests/test_bases_reais.py -v`.
5. **Um `README.md` na pasta da base**, explicando de onde vem, como foi transcrita e o que ficou de fora.
6. **Uma linha no [CHANGELOG](CHANGELOG.md)**: quem enviou, o que mudou e quando. O commit fica registrado no histórico do Git.

## Licença

As bases são publicadas sob **[Creative Commons Atribuição 4.0 (CC BY 4.0)](LICENSE)**: qualquer pessoa pode copiar, adaptar e usar, inclusive comercialmente, desde que cite este projeto como origem.

A licença cobre o trabalho deste projeto: a transcrição, a organização e os metadados. Os documentos originais continuam com os direitos de quem os produziu; documentos oficiais (como os do TSE e da Polícia Federal) são públicos, e posts de redes sociais são citados como fonte, com link para o original.

## Quem fez

Projeto de Bittencourt, da série **Bittencourt Talks**. Acompanhe no TikTok: [@mrbittencourttalks](https://www.tiktok.com/@mrbittencourttalks).
