---
name: busca-de-vagas
description: Busca vagas de emprego na internet a partir de um currículo (PDF, DOCX ou texto) e das preferências da pessoa (cargo, município/estado e modalidade presencial, híbrida e/ou remota). Pesquisa em Gupy, Glassdoor, Indeed, GeekHunter e outras plataformas que encontrar, e entrega as vagas com % de aderência ao currículo e os requisitos que faltam, ordenadas por aderência, no chat e em uma planilha Excel. Use sempre que o usuário pedir para procurar vagas, oportunidades, emprego, estágio ou recolocação, enviar currículo para ver onde se encaixa, ou mencionar Gupy, Indeed, Glassdoor, GeekHunter ou LinkedIn Vagas, mesmo que não cite a palavra "skill".
---

# Busca de vagas

Encontra vagas reais e atuais que combinam com o currículo e as preferências da pessoa. A qualidade depende de três coisas: entender bem o perfil, respeitar a combinação cargo × modalidade × localidade e só entregar vagas que você confirmou que existem. Responda no idioma do usuário (normalmente português do Brasil).

## Passo 1: ler o currículo

1. Procure o arquivo em `/mnt/user-data/uploads`. Se não houver nenhum, peça que a pessoa envie o currículo e aguarde.
2. Leia o arquivo conforme o tipo (consulte a skill `file-reading` se o conteúdo não estiver no contexto).
3. Extraia: cargos atuais e anteriores, senioridade e anos de experiência, habilidades técnicas, ferramentas e tecnologias, idiomas, formação, certificações e setores de atuação.
4. Mostre um resumo curto (3 a 5 linhas) do perfil encontrado, para a pessoa corrigir algo se precisar.

Dados pessoais do currículo (nome, telefone, e-mail, endereço) nunca entram em consultas de busca. Use só cargo, habilidades e localidade desejada.

## Passo 2: perguntar as preferências

Pergunte apenas o que ainda não foi informado. Se a pessoa já disse algo na mensagem, use e não repita a pergunta.

- **Cargo(s)**: um ou mais cargos, **separados por vírgula** (ex.: "Product Owner, Product Manager, Gerente de Produto"). Oriente a pessoa a usar vírgula entre os cargos. Sugira 2 ou 3 opções coerentes com o currículo, mas aceite o que ela escrever. Divida a resposta nas vírgulas, ignore espaços extras e remova repetidos.
- **Localidade**: sempre **município e estado** (ex.: Itajaí, SC). Peça os dois. Pergunte mesmo quando a modalidade for só remota; nesse caso o local não restringe a busca (veja o Passo 3).
- **Raio de busca (km)**: a distância máxima, em quilômetros, a partir do município informado, dentro da qual vagas presenciais e híbridas serão consideradas (ex.: 30, 50, 100). **Não existe valor padrão**: a pessoa precisa informar. Se ela não disser, pergunte; se responder algo que não seja um número positivo de km (ex.: "perto"), peça um número. Só é dispensável se a modalidade escolhida for apenas remota, pois o raio não se aplica a vagas remotas.
- **Modalidade**: presencial, híbrida e/ou remota. **A pessoa pode escolher mais de uma opção.** Se houver a ferramenta de opções clicáveis (`ask_user_input_v0`), use seleção múltipla para este item.

Faça as perguntas em uma única rodada, não uma por mensagem.

## Passo 3: pesquisar

Plataformas mínimas: **Gupy, Glassdoor, Indeed, GeekHunter**. Além delas, procure em todas as outras que fizerem sentido para o cargo, por exemplo LinkedIn Vagas, Catho, InfoJobs, Vagas.com, Programathor, Trampos.co, páginas de carreira de empresas e agregadores. Se o cargo for de uma área específica, busque também plataformas especializadas dela.

Faça buscas separadas por cargo, por plataforma e por modalidade, porque uma busca única que mistura tudo devolve resultados rasos. Consulte a data de hoje no contexto e use-a para priorizar vagas recentes.

**Regra de localidade por modalidade:**

| Modalidade | Como tratar a localidade |
|---|---|
| Presencial | Considere três grupos: (1) vagas no **município exato** informado; (2) vagas em **municípios vizinhos** (que fazem divisa com ele); (3) vagas em **municípios a até o raio informado pela pessoa (R km)** do município informado. Estime a distância rodoviária aproximada e só inclua o município se ficar dentro do raio informado. Confirme o município real na página da vaga. |
| Híbrida | Mesma regra do presencial, pois exige ir ao local. |
| Remota | **Qualquer vaga remota dentro do Brasil**, sem filtrar por município ou estado. A localidade informada não restringe. Sinalize nas observações as que exigem residir em estado específico, ter presença eventual ou trabalhar em horário de outro fuso. Descarte as que exigem morar fora do Brasil. |

Para vagas presenciais e híbridas, monte a lista de municípios antes de pesquisar: o município exato, os vizinhos (mesmo que ultrapassem o raio, se fizerem divisa) e os demais dentro do raio informado (use o conhecimento geográfico e, em caso de dúvida, confirme a distância com uma busca). Pesquise cada município relevante por plataforma, começando pelo exato. Ao entregar, informe para cada vaga presencial ou híbrida o município real e a relação com o município pedido: "município exato", "município vizinho" ou "a cerca de X km". Na ordenação, a proximidade só desempata vagas com a mesma aderência.

**Dicas por plataforma:**
- Gupy: cada empresa tem seu portal (`empresa.gupy.io`). Use buscas com `site:gupy.io` mais cargo e cidade.
- Se uma plataforma exigir login ou bloquear a leitura, não invente resultados. Registre que não foi possível ler e, ao final, entregue um link de busca pré-montado para a pessoa abrir.

**Confirme cada vaga** abrindo a página (`web_fetch`) sempre que possível. Trechos de resultados de busca ficam velhos. Verifique se a vaga está aberta, qual é a modalidade e qual é o local. Descarte vagas encerradas, duplicadas (a mesma vaga em duas plataformas vira uma linha com os dois links) e as que não batem com a modalidade ou localidade pedidas. Só inclua vagas com URL real que você viu.

## Passo 4: calcular a aderência e ordenar

Para cada vaga confirmada, calcule a **% de aderência** ao currículo:

1. Liste os requisitos que a vaga pede (formação, experiência, anos de senioridade, tecnologias, ferramentas, idiomas, certificações, conhecimentos). Considere só o que está escrito na vaga.
2. Para cada requisito, verifique se o currículo comprova. Marque como atendido apenas o que **consta** no currículo; não presuma habilidades que a pessoa provavelmente tem.
3. Dê peso 2 aos requisitos obrigatórios e peso 1 aos desejáveis ou diferenciais. Se a vaga não separa os dois, use peso 1 para todos.
4. Aderência = soma dos pesos atendidos ÷ soma dos pesos totais, arredondada para número inteiro.
5. Se a vaga não traz requisitos suficientes para calcular (descrição vaga ou ausente), escreva "não calculável" em vez de inventar um número.

Vagas cujo título não corresponde a nenhum dos cargos pedidos ficam de fora. Entre as restantes, ordene da maior para a menor aderência e, em caso de empate, pela vaga mais recente.

## Passo 5: entregar

**No chat**, uma tabela ou lista ordenada com: cargo, empresa, plataforma, modalidade, local (com a relação com o município pedido, quando presencial ou híbrida), link, **% de aderência** e **o que a vaga pede que não consta no currículo**. Antes dela, diga em uma frase quantas vagas encontrou, em quais plataformas buscou e, se houve vagas presenciais ou híbridas, o raio em km usado na busca. Depois, liste as plataformas que não puderam ser lidas, com os links de busca.

Regra do campo "o que falta": sempre que a aderência for menor que 100%, liste de forma objetiva cada requisito da vaga que não aparece no currículo (ex.: "Docker", "inglês avançado", "5+ anos com Java"). Com 100%, escreva "nada, o currículo cobre todos os requisitos". Use a redação "não consta no currículo" e não "a pessoa não tem", pois a habilidade pode existir e só não estar escrita; quando for o caso, sugira ao final que a pessoa inclua no currículo o que realmente domina.

**Em planilha Excel (.xlsx)**: leia `/mnt/skills/public/xlsx/SKILL.md` e gere o arquivo em `/mnt/user-data/outputs/vagas.xlsx`, depois apresente com `present_files`. Colunas: Posição, Cargo pesquisado, Cargo da vaga, Empresa, Plataforma, Modalidade, Município/UF, Distância do município informado (exato, vizinho ou km aproximados; "n/a" para remotas), Link, Data de publicação (se informada), % de aderência, Requisitos atendidos, Requisitos que não constam no currículo, Observações. Links clicáveis, cabeçalho congelado, filtros ativados e a coluna de aderência formatada como porcentagem.

Não copie descrições de vagas na íntegra; resuma com suas palavras.

## Casos especiais

- **Poucas ou nenhuma vaga**: diga isso com clareza e sugira ampliar (cargos parecidos, um raio maior em km, outra modalidade). Não complete a lista com vagas não confirmadas.
- **Currículo ilegível ou muito curto**: peça ao usuário as informações que faltam em vez de adivinhar o perfil.
- **Vários cargos (separados por vírgula)**: faça a busca completa para cada cargo. No chat, agrupe o resultado por cargo, com um título por cargo e a ordenação por aderência dentro de cada grupo. Na planilha, use uma única aba com a coluna "Cargo pesquisado" (o cargo informado pela pessoa, além do título da vaga) e ordene por cargo pesquisado e depois por aderência. Se uma vaga servir a mais de um cargo, liste uma vez só, no cargo de melhor correspondência, e cite o outro nas observações. Se algum cargo não render vagas, diga isso claramente em vez de omiti-lo.
