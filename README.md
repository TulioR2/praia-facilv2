# praia-facilv2
Aplicativo de turismo e serviços de praia

## Documentação do projeto

# Praia FÃ¡cil

AplicaÃ§Ã£o web responsiva para frequentadores e turistas de praias. ReÃºne cadastro e autenticaÃ§Ã£o, descoberta de comÃ©rcio e serviÃ§os prÃ³ximos, lista de locais de interesse, perfil do usuÃ¡rio e consulta ao clima.

## Funcionalidades

- Tela de abertura e boas-vindas.
- Cadastro com nome, e-mail, telefone, senha e aceite dos termos.
- Login por e-mail/senha, visualizaÃ§Ã£o de senha e opÃ§Ã£o de salvar sessÃ£o.
- Fluxo de recuperaÃ§Ã£o e redefiniÃ§Ã£o de senha.
- Modo demonstraÃ§Ã£o local: botÃµes Google/Facebook abrem uma tela simulada e autenticam a conta de teste, sem acessar provedores reais.
- Login social real Google/Facebook via OAuth 2.0, quando `DEMO_MODE=false` e as credenciais dos provedores estiverem configuradas.
- Home com saudaÃ§Ã£o, clima, categorias, produtos/serviÃ§os e Ã¡rea de divulgaÃ§Ã£o.
- Busca por nome e categoria.
- Lista pessoal de locais salvos (â€œPedidosâ€).
- Perfil com atualizaÃ§Ã£o de nome, e-mail e telefone e alteraÃ§Ã£o de senha.
- Assistente virtual integrado Ã  OpenAI Responses API para perguntas gerais, com contexto de clima e locais de Boa Viagem (requer chave de API).
- Dados meteorolÃ³gicos via Open-Meteo e locais via OpenStreetMap/Overpass; Google Places opcional.

## Tecnologias

- Front-end: React 18 via CDN e Babel Standalone.
- Back-end: Node.js, Express.
- Banco de dados: SQLite nativo do Node.js (`node:sqlite`), sem mÃ³dulo nativo externo.
- AutenticaÃ§Ã£o: JWT e bcrypt.
- IntegraÃ§Ãµes: Open-Meteo, OpenStreetMap/Overpass, OpenAI Responses API e OAuth Google/Facebook opcional.

## Requisitos

- Node.js 24 LTS ou superior.
- npm.
- ConexÃ£o com a internet para consultar clima, locais e bibliotecas carregadas via CDN.

## Reinstalar apÃ³s atualizar para esta versÃ£o

Se vocÃª jÃ¡ tentou instalar a versÃ£o anterior, apague a pasta `node_modules` e o arquivo `package-lock.json` antigos antes de instalar. No terminal CMD, dentro da pasta `praia-facil`, execute:

```cmd
rmdir /s /q node_modules
del package-lock.json
npm install
```

Se algum desses itens nÃ£o existir, o Windows pode avisar; basta continuar. Esta versÃ£o remove `better-sqlite3`, que exigia compilaÃ§Ã£o nativa no Windows, e usa o SQLite incluÃ­do no prÃ³prio Node.js 24.

## Executar localmente (Windows)

1. Extraia o ZIP e abra a pasta `praia-facil` no terminal.
2. Instale as dependÃªncias:

   ```bash
   npm install
   ```

3. Copie `.env.example` para `.env`.
4. No `.env`, defina `JWT_SECRET` com uma frase aleatÃ³ria longa (mÃ­nimo de 16 caracteres; recomendado 32 ou mais).
5. Inicie:

   ```bash
   npm start
   ```

6. Acesse `http://localhost:3000`.

O banco SQLite `praia.db` serÃ¡ criado automaticamente na primeira execuÃ§Ã£o. O projeto usa o mÃ³dulo `node:sqlite` incluÃ­do no Node.js 24, evitando compilaÃ§Ã£o de bibliotecas C++ e instalaÃ§Ã£o do Visual Studio Build Tools.

## ConfiguraÃ§Ã£o da praia

As variÃ¡veis `BEACH_NAME`, `BEACH_LAT`, `BEACH_LON` e `BEACH_RADIUS` definem a praia de referÃªncia e o raio de busca. Os valores de exemplo apontam para Boa Viagem, Recife. A consulta meteorolÃ³gica usa essas coordenadas; nÃ£o representa automaticamente a localizaÃ§Ã£o GPS de cada usuÃ¡rio.

## Login Google e Facebook

O fluxo estÃ¡ implementado, mas exige credenciais prÃ³prias. Configure `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`, `FB_APP_ID` e `FB_APP_SECRET` no `.env` e cadastre exatamente as URLs de callback correspondentes ao domÃ­nio usado. Sem essas credenciais, os botÃµes sociais informam que o recurso nÃ£o estÃ¡ configurado.

## LimitaÃ§Ãµes conhecidas â€” leia antes de apresentar como produto final

- A recuperaÃ§Ã£o de senha gera token e registra o link no console do servidor; no modo de desenvolvimento ele tambÃ©m Ã© mostrado na interface. Para produÃ§Ã£o, integrar envio real de e-mail (SMTP/provedor transacional).
- O texto de Termos de Uso Ã© provisÃ³rio. Criar Termos e PolÃ­tica de Privacidade aprovados antes de publicar.
- O carrossel da home apresenta locais encontrados na regiÃ£o; ainda nÃ£o existe painel nem campanha de publicidade paga.
- â€œPedidosâ€ Ã© uma lista de locais salvos/roteiro de interesse, nÃ£o um sistema de compra, reserva ou pagamento.
- O assistente responde sobre dados meteorolÃ³gicos disponÃ­veis. MarÃ©s e condiÃ§Ãµes do mar nÃ£o estÃ£o integradas.
- A disponibilidade e precisÃ£o dos locais dependem da base externa e da praia configurada.

## DocumentaÃ§Ã£o acadÃªmica

O levantamento dos requisitos funcionais e nÃ£o funcionais, fluxos, regras de negÃ³cio, critÃ©rios de aceite e roteiro de testes estÃ¡ em [`docs/levantamento-requisitos.md`](docs/levantamento-requisitos.md). O documento foi organizado a partir dos requisitos informados e deve ser validado com o professor/equipe.

## SeguranÃ§a antes de publicar

- Nunca envie `.env`, tokens ou segredos para o GitHub.
- Use HTTPS e `NODE_ENV=production`.
- Defina um `JWT_SECRET` forte e exclusivo.
- Configure envio de e-mail e URLs de callback do domÃ­nio de produÃ§Ã£o.
- Revise Termos de Uso, PolÃ­tica de Privacidade e tratamento de dados conforme a LGPD.
- Revise atribuiÃ§Ã£o e condiÃ§Ãµes de uso das fontes externas.


## Assistente virtual com IA

Para habilitar respostas a perguntas gerais, crie uma chave no painel da OpenAI e adicione ao `.env`:

```env
OPENAI_API_KEY=sua_chave_secreta
OPENAI_MODEL=gpt-6.2-astra
```

Reinicie o servidor com `npm start`. A chave fica somente no servidor e nunca deve ser colocada no React/navegador. O assistente usa a Responses API e pesquisa na web quando necessÃ¡rio. O uso da API pode gerar cobranÃ§a separada da assinatura do ChatGPT; consulte sua conta e limites antes de usar.

Sem a chave, o app continua com clima e catÃ¡logo de locais, mas o chat de perguntas gerais informa que precisa ser configurado.

## CatÃ¡logo de Boa Viagem

A busca combina resultados do OpenStreetMap com uma lista inicial de referÃªncia de restaurantes e quiosques conhecidos no bairro, como Entre Amigos Praia, Bode do NÃ´, Bar do Cuscuz, ParraxaxÃ¡, Chica Pitanga, Ilha dos Navegantes, Cia do Chopp, Quiosque 44, Quiosque 13 e Tapiocas da SÃ©. O catÃ¡logo nÃ£o Ã© exaustivo; confirme endereÃ§o, horÃ¡rio e funcionamento antes de visitar. Os dados de locais externos podem variar.


## Modo de demonstraÃ§Ã£o local â€” Google e Facebook

Por padrÃ£o, em execuÃ§Ã£o local fora de produÃ§Ã£o, o modo de demonstraÃ§Ã£o Ã© ativado automaticamente. Os botÃµes Google e Facebook redirecionam para uma tela com campos editÃ¡veis de e-mail e senha, claramente identificada como simulaÃ§Ã£o (nÃ£o Ã© uma pÃ¡gina oficial desses provedores). O formulÃ¡rio verifica os dados no banco local do Praia FÃ¡cil e permite entrar com a conta de teste ou com outra conta jÃ¡ cadastrada no prÃ³prio aplicativo.

**Conta de demonstraÃ§Ã£o prÃ©-criada:**
- E-mail: `teste01@gmail.com`
- Senha: `teste01`
- A conta Ã© inserida/atualizada no banco local na inicializaÃ§Ã£o quando o modo de demonstraÃ§Ã£o estÃ¡ ativo.

**Teste do cadastro:**
- Crie normalmente uma conta pelo formulÃ¡rio com `teste02@gmail.com`.
- Use a senha `teste02` (7 caracteres, aceita somente no modo de demonstraÃ§Ã£o).
- Informe nome e telefone e marque o aceite dos termos.
- O cadastro `teste02` Ã© persistido como uma conta local comum; nÃ£o Ã© uma conta Google/Gmail real.

Importante: os campos dessas telas sÃ£o apenas uma simulaÃ§Ã£o local. A senha digitada Ã© enviada ao servidor local do Praia FÃ¡cil para validar uma conta cadastrada no aplicativo; ela nÃ£o Ã© enviada ao Google ou ao Facebook e nÃ£o autentica uma conta real desses provedores. NÃ£o digite sua senha real do Google/Facebook nessa demonstraÃ§Ã£o. Para desativar a simulaÃ§Ã£o e ativar OAuth real, configure `DEMO_MODE=false`, configure os Client IDs/Secrets vÃ¡lidos e os callbacks descritos nas seÃ§Ãµes seguintes.

## Configurar login Google

1. Acesse Google Cloud Console e crie/seleciona um projeto.
2. Configure a tela de consentimento OAuth e crie um ID de cliente do tipo Aplicativo da Web.
3. Em "Origens JavaScript autorizadas", adicione `http://localhost:3000`.
4. Em "URIs de redirecionamento autorizados", adicione `http://localhost:3000/auth/google/callback`.
5. Copie o ID e o segredo para `GOOGLE_CLIENT_ID` e `GOOGLE_CLIENT_SECRET` no `.env`.

## Configurar login Facebook

1. Registre-se no Meta for Developers e crie um aplicativo com o produto Facebook Login para Web.
2. Configure o domÃ­nio do app e a URL de redirecionamento OAuth vÃ¡lida: `http://localhost:3000/auth/facebook/callback`.
3. Copie o ID e o segredo do aplicativo para `FB_APP_ID` e `FB_APP_SECRET` no `.env`.
4. Para testes, adicione os usuÃ¡rios/contas como testadores ou administradores do aplicativo. Para disponibilizar publicamente, conclua as etapas de publicaÃ§Ã£o e anÃ¡lise exigidas pela Meta.

Os botÃµes sociais jÃ¡ iniciam os fluxos OAuth do servidor, mas nÃ£o conseguem autenticar atÃ© que as credenciais reais sejam cadastradas nos respectivos painÃ©is. Nunca compartilhe os segredos nem publique o `.env`.
