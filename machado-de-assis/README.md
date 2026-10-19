# Machado de Assis

8.820 trechos de Machado de Assis, todos em domínio público, em cinco fontes:

| Fonte | Trechos | O que é |
|---|---|---|
| Cartas de Machado e Nabuco (1865-1908) | 469 | 47 cartas com remetente e destinatário, 44 delas com data; as de Machado aparecem à direita no chat |
| Graça Aranha: comentários (1923) | 318 | O ensaio que abre o livro das cartas: é a opinião de Graça Aranha |
| Crônicas de "A Semana" (1892-1900) | 4.694 | As crônicas semanais na Gazeta de Notícias |
| Dom Casmurro (1899) | 1.715 | Romance narrado por Bento Santiago |
| Memórias Póstumas de Brás Cubas (1881) | 1.624 | Romance narrado por Brás Cubas |

## De onde vem

- **Cartas e comentários:** Graça Aranha, *Machado de Assis e Joaquim Nabuco: commentarios e notas á correspondencia entre estes dous escriptores*, Monteiro Lobato & Cia., 1923, na [Brasiliana Guita e José Mindlin (USP)](https://digital.bbm.usp.br/handle/bbm/3932), que registra o livro como domínio público. O chat baixa o PDF de lá.
- **Crônicas e romances:** portal Machado de Assis do Ministério da Educação ([machado.mec.gov.br](https://machado.mec.gov.br)), com o texto da *Obra Completa* (Nova Aguilar, 1994). O portal bloqueia downloads automáticos, então os três PDFs estão em `arquivos/`, com SHA-256.
- **Direitos:** Machado morreu em 1908, Nabuco em 1910 e Graça Aranha em 1931: tudo em domínio público.

## Como foi transcrito

Texto literal da camada de texto dos PDFs, sem modelo de IA, com o [agente-extrator](https://github.com/chat-com-alguem/agente-extrator):

```bash
agente-extrator --lote exemplos/machado-de-assis/lote.yaml
```

- **Cartas:** a opção `cartas` do agente reconhece o cabeçalho de cada carta ("MACHADO A NABUCO") e dá a cada trecho o remetente, o destinatário e a data escrita no começo da carta. Três cartas ficaram sem data: duas escrevem o ano com dois dígitos ("10-3-99", "28-7-05") e uma não traz o ano ("Sexta-feira, 10 de fevereiro"). O agente não chuta.
- As notas de Graça Aranha depois de cada carta e o cabeçalho corrido das páginas foram retirados.
- O livro de 1923 vem de reconhecimento ótico (OCR) da digitalização: há erros ocasionais de letra ("Am.0" por "Am.º"). Grafia da época ("hontem", "annos").

## Ressalvas

- Nos romances quem fala é o narrador, personagem de ficção, não Machado. A base instrui o chat a dizer "o narrador de Dom Casmurro diz...".
- Crônica tem ironia: nem toda frase é opinião literal de Machado.
- Pergunta sem resposta única (como "Capitu traiu Bentinho?") recebe as leituras possíveis em ordem alfabética, cada uma com o trecho que a sustenta.

## Usar no chat

```bash
# chat-com-alguem/.env  (a base já está na pasta databases, basta marcá-la na conversa)
BASE_PADRAO=machado-de-assis
```

Perguntas para começar: *O que Machado escreveu a Nabuco depois da morte de Carolina?* · *O que o narrador de Dom Casmurro diz sobre os olhos de Capitu?*
