# Confissões de Santo Agostinho

2.982 trechos dos treze livros das *Confissões* (c. 397-400), em duas traduções em domínio público:

| Fonte | Trechos | O que é |
|---|---|---|
| Tradução portuguesa anônima (Garnier, 1905) | 1.979 | Grafia antiga, de OCR com erros; cada trecho aponta a página do PDF |
| Tradução inglesa de E. B. Pusey (1838) | 1.003 | Texto limpo; cada trecho diz de que livro é ("Livro VIII") |

## De onde vem

- **Português:** *Confissões do grande Doutor da Igreja Santo Agostinho*, "traduzidas na lingua portugueza por hum devoto", H. Garnier, Rio de Janeiro, 1905, [digitalizada no Internet Archive](https://archive.org/details/confissoes-do-grande-doutor-da-igreja-santo-agostinho-1905). O chat baixa o PDF de lá. Seria reedição de uma tradução de Lisboa de 1783-1784, segundo quem publicou a digitalização; isso não foi confirmado em catálogo.
- **Inglês:** Project Gutenberg, [eBook #3296](https://www.gutenberg.org/ebooks/3296), em texto puro. A cópia usada está em `arquivos/`, com SHA-256.
- **Direitos:** o texto latino é domínio público. A tradução de 1905 é anônima (no Brasil, obra anônima fica livre 70 anos depois de publicada), e a de Edward Bouverie Pusey (morto em 1882) também é livre.
- **Por que não a tradução mais conhecida:** a de J. Oliveira Santos e A. Ambrósio de Pina (Apostolado da Imprensa, Porto) tem direito autoral até 2066 (Pina morreu em 1995).

## Como foi transcrito

Texto literal, sem modelo de IA, com o [agente-extrator](https://github.com/chat-com-alguem/agente-extrator):

```bash
agente-extrator --lote exemplos/confissoes-santo-agostinho/lote.yaml
```

- **1905:** páginas 9 a 462 do PDF (o índice ficou de fora). Saíram o cabeçalho corrido, as manchas lidas como letras e os trechos que são só ruído de OCR (`qualidade_minima`, cerca de 10%). O livro de cada trecho não foi marcado, porque o OCR erra os números romanos do cabeçalho. Títulos de capítulo ("CAPITULO XVII") ficaram no meio do texto.
- **Pusey:** a licença do Project Gutenberg, no começo e no fim do arquivo, foi retirada (`remover_texto`). Os títulos "BOOK I" a "BOOK XIII" não viraram trechos: deram o nome do livro aos trechos seguintes (opção `secao`). Texto sem páginas: a citação mostra o livro e o link da fonte.

## Ressalvas

- A tradução de 1905 tem erros de OCR e trechos perdidos: confira a página original, que o chat mostra ao lado da citação. A de Pusey serve para confirmar a leitura.
- Pusey é inglês do século XIX ("Thou", "hast"). Tradução feita na resposta é do chat, não do livro.
- O livro é uma oração dirigida a Deus ("vós" na de 1905, "Thou" na de Pusey).

## Usar no chat

```bash
# chat-com-alguem/.env  (a base já está na pasta databases, basta marcá-la na conversa)
BASE_PADRAO=confissoes-santo-agostinho
```

Perguntas para começar: *O que aconteceu no jardim de Milão, no Livro VIII?* · *O que Agostinho diz sobre o tempo no Livro XI?*
