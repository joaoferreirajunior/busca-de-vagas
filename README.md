# Busca de vagas (skill para o Claude)

Skill que lê o seu currículo e procura vagas de emprego reais e atuais na internet (Gupy, Glassdoor, Indeed, GeekHunter e outras plataformas), entregando o resultado no chat e em uma planilha Excel.

## O que ela faz

- Lê o currículo (PDF, DOCX ou texto) e resume o seu perfil.
- Pergunta: cargo(s) separados por vírgula, município/estado, raio de busca em km e modalidade (presencial, híbrida e/ou remota).
- Presencial e híbrida: considera o município exato, os vizinhos e os que ficam dentro do raio informado.
- Remota: considera qualquer vaga remota no Brasil.
- Confirma cada vaga abrindo a página e descarta as encerradas.
- Calcula a **% de aderência** ao currículo e lista o que a vaga pede e **não consta** no currículo.
- Entrega uma tabela no chat e o arquivo `vagas.xlsx`.

## Como instalar

1. Baixe `busca-de-vagas.skill` na aba Releases (ou compacte a pasta `busca-de-vagas/` em um `.zip` e renomeie para `.skill`).
2. No Claude, abra Configurações > Capacidades (ou Skills) e envie o arquivo.
3. Envie seu currículo e peça: "procure vagas para mim".

## Como a aderência é calculada

Pontos atendidos ÷ pontos totais. Requisito obrigatório vale 2 pontos e desejável vale 1; quando a vaga não separa os dois, todos valem 1. Só conta como atendido o que está escrito no currículo.

## Privacidade

Dados pessoais do currículo (nome, telefone, e-mail, endereço) não entram nas consultas de busca.
