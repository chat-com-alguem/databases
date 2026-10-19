# Eleições 2026, 2º turno: propostas de governo registradas no TSE

As propostas de governo das **14 candidaturas do 2º turno de 2026**, como cada uma registrou no Tribunal Superior Eleitoral, mais a ficha oficial de cada candidatura (número, partido, coligação, vice). É a base padrão do [chat-com-alguem](https://github.com/chat-com-alguem/chat).

- **Presidente:** Lula (PT) e Flávio Bolsonaro (PL).
- **Governador:** Acre, Amazonas, Distrito Federal, Espírito Santo, Rio Grande do Norte e Tocantins, os seis lugares com 2º turno para governador. Nos outros 21, o governador foi eleito no 1º turno.

## De onde vem

Tudo vem do **DivulgaCandContas**, o sistema oficial do TSE. A lei obriga cada candidatura a Presidente e a Governador a registrar suas propostas junto com o pedido de candidatura ([Lei 9.504/1997](https://www.planalto.gov.br/ccivil_03/leis/l9504.htm), art. 11, § 1º, IX). Cada fonte aponta para o endereço oficial do arquivo no TSE e guarda a impressão digital (SHA-256) do PDF.

- **Quem está no 2º turno:** a situação "2º turno" que o próprio TSE atribui a cada candidatura.
- **Quais arquivos:** todos os documentos do tipo "proposta de governo" registrados pela candidatura, sem escolha nossa. Por isso o Omar Aziz aparece com 9 arquivos (ele dividiu o plano em 9 volumes) e o Alan Rick e o Ricardo Ferraço com 2 (versões diferentes, as duas registradas).
- **Ordem:** pelo número de urna.

Os PDFs estão em `arquivos/`, porque o site do TSE bloqueia downloads automáticos e o chat não conseguiria baixá-los para mostrar a página original. Para conferir que é o mesmo arquivo do TSE, baixe pelo navegador no endereço que está em `sources.yaml` e compare o SHA-256 (veja o README do repositório).

## Como foi transcrito

**Nenhum modelo de IA leu ou resumiu os documentos.** Cada trecho é o texto literal tirado da camada de texto do PDF, dividido em parágrafos pelo [agente-extrator](https://github.com/chat-com-alguem/agente-extrator) no modo `trechos`, com as mesmas opções para todas as candidaturas. Cada trecho guarda a página e de qual candidatura ele é.

Páginas que só têm imagem (capas, infográficos, páginas escaneadas) não têm texto para tirar e **ficaram de fora**. A lista exata de cada documento está em `sources.yaml`, nas ressalvas da fonte. Os valores, telefones e e-mails das campanhas ficaram como estão no documento oficial, sem máscara.

| Candidatura | Arquivos | Páginas | Só imagem (fora) | Trechos |
|---|---|---|---|---|
| LULA (PT), Presidente | 1 | 84 | 5 (6%) | 304 |
| FLAVIO BOLSONARO (PL), Presidente | 1 | 76 | 4 (5%) | 340 |
| ALAN RICK (REPUBLICANOS), Governador do Acre | 2 | 50 | 4 (8%) | 396 |
| MAILZA ASSIS (PP), Governador do Acre | 1 | 68 | 1 (1%) | 599 |
| PROFESSORA MARIA DO CARMO (PL), Governador do Amazonas | 1 | 9 | 1 (11%) | 38 |
| OMAR AZIZ (PSD), Governador do Amazonas | 9 | 1.742 | 99 (6%) | 11.896 |
| CELINA LEÃO (PP), Governador do Distrito Federal | 1 | 42 | 2 (5%) | 288 |
| LEANDRO GRASS (PT), Governador do Distrito Federal | 1 | 124 | 5 (4%) | 706 |
| LORENZO PAZOLINI (REPUBLICANOS), Governador do Espírito Santo | 1 | 54 | 5 (9%) | 228 |
| RICARDO FERRAÇO (MDB), Governador do Espírito Santo | 2 | 162 | 5 (3%) | 826 |
| CADU DE LULA (PT), Governador do Rio Grande do Norte | 1 | 74 | 1 (1%) | 523 |
| ALLYSON (UNIÃO), Governador do Rio Grande do Norte | 1 | 44 | 14 (32%) | 202 |
| PROFESSORA DORINHA (UNIÃO), Governador do Tocantins | 1 | 84 | 5 (6%) | 889 |
| VICENTINHO JÚNIOR (PSDB), Governador do Tocantins | 1 | 36 | 2 (6%) | 424 |
| **Total** | **24** | **2.649** | **153** | **17.659** |

Mais 14 trechos com as fichas oficiais (fonte `tse-candidaturas-2-turno-2026`).

**Atenção à cobertura:** o documento do Allyson (RN) tem 14 de 44 páginas só com imagem, então um terço dele ainda não está na base. Ler essas páginas exige um modelo de IA com visão; quando isso for feito, será feito para as 153 páginas de todas as candidaturas, com o mesmo modelo, e registrado no [CHANGELOG](../CHANGELOG.md).

## Imparcialidade

- O chat recebe a regra de não opinar, não avaliar qual proposta é melhor, não recomendar voto e não usar adjetivos sobre candidatos ou propostas (`projeto.yaml`, campo `subject`).
- As perguntas sugeridas sempre tratam juntas as duas candidaturas de um mesmo cargo.
- **Busca equilibrada** (`balanced_search: true`): a busca alterna os resultados entre as candidaturas. Sem isso, quem registrou mais páginas (o Amazonas tem 11.896 trechos de um lado e 38 do outro) ocuparia todas as vagas de uma resposta só pelo volume de texto.
- Propostas são compromissos declarados pelas candidaturas, não fatos. O chat diz isso na tela.

## Como gerar de novo

Do zero, com os dados oficiais do momento (precisa do Chrome instalado, porque o TSE bloqueia acesso automatizado):

```bash
cd agente-extrator
pip install -e ".[tse]"
python exemplos/2026-brasil-eleicoes-segundo-turno/coletar_tse.py
agente-extrator --lote exemplos/2026-brasil-eleicoes-segundo-turno/tse-2026/lote.yaml --sim --substituir
```

O script `coletar_tse.py` lista no TSE quem está no 2º turno, baixa as fichas e as propostas e gera o lote. Depois, o `projeto.yaml` desta pasta precisa ser revisto à mão (ele não é sobrescrito se já existir).
