# Inconfidência Mineira (1789-1792)

3.615 trechos dos **Autos de Devassa da Inconfidência Mineira**: os interrogatórios de Tiradentes e dos outros réus, presos no Rio de Janeiro entre 1789 e 1791 (vol. 5), e os ofícios, a defesa, o acórdão da Alçada de 18 de abril de 1792 e a certidão da execução de Tiradentes (vol. 7). Cada trecho aponta a página do PDF e o número impresso na edição.

## De onde vem

- **Documento:** *Autos de Devassa da Inconfidência Mineira*, 2ª edição, Câmara dos Deputados e Imprensa Oficial de Minas Gerais (vol. 5 de 1982, vol. 7 de 1982), em PDF publicado pela Escola Judicial do TJMG: [vol. 5](https://ejef.tjmg.jus.br/wp-content/uploads/2022/06/atos_volume-5.pdf), [vol. 7](https://ejef.tjmg.jus.br/wp-content/uploads/2022/06/atos_volume-7.pdf).
- **PDF:** não fica nesta pasta. O chat baixa do TJMG e confere a impressão digital (SHA-256) antes de usar.
- **Direitos:** os autos são documentos do século XVIII e atos oficiais, em domínio público. A edição moderna tem notas, introduções e índices assinados pelos editores (Herculano Gomes Mathias, Tarquínio J. B. de Oliveira, José Seixas Sobrinho, Alexandre Miranda Delgado), que têm autor e **ficaram de fora**.

## Como foi transcrito

Texto literal da camada de texto dos PDFs, sem modelo de IA, com o [agente-extrator](https://github.com/chat-com-alguem/agente-extrator):

```bash
agente-extrator --lote exemplos/inconfidencia-mineira-1789/lote.yaml
```

- Vol. 5, páginas 14 a 538 do PDF (os autos de perguntas); vol. 7, páginas 25 a 380 (dos ofícios à execução). Introduções, sumários e índices ficaram de fora.
- Notas de rodapé, "Notas explicativas" e "Notas biográficas" dos editores foram retiradas (`sem_rodape`, `cortar_a_partir_de`, `excluir_trechos`). As chamadas de nota no texto, como "(1)", ficaram.
- 17 páginas que só têm imagem (folhas de rosto de documentos) não foram transcritas e estão listadas em `sources.yaml`.

## Ressalvas

- Os autos registram a versão da Coroa e o que os réus disseram presos e interrogados, anotado pelo escrivão. Não são um retrato neutro do que aconteceu.
- O PDF do TJMG foi redigitado a partir da edição impressa: a página do PDF não é a do livro. O chat mostra as duas ("página 16, numerada 18").
- Grafia e estilo do século XVIII, com abreviaturas nas assinaturas ("Joaq.m José da S.a X.er").

## Usar no chat

```bash
# chat-com-alguem/.env  (a base já está na pasta databases, basta marcá-la na conversa)
BASE_PADRAO=inconfidencia-mineira-1789
```

Perguntas para começar: *O que Tiradentes respondeu quando perguntaram por que se escondeu no Rio de Janeiro?* · *Qual foi a pena dada a Tiradentes no acórdão de 1792?*
