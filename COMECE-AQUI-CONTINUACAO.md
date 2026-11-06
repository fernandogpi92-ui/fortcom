# FORTCOM — COMECE AQUI (continuação em outro chat)

**Atualizado em:** 06/11/2026  
**Finalidade:** transferir o contexto do projeto para uma nova conversa sem perder o que já foi analisado e validado.

---

## 1. Mensagem pronta para o novo chat

Copie e envie esta mensagem na nova conversa, com o Google Drive e/ou GitHub conectado, se essas integrações estiverem disponíveis:

> Estou continuando o projeto FORTCOM. Primeiro leia o arquivo `COMECE-AQUI-CONTINUACAO.md` dentro da pasta `FORTCOM — Controle de Obras` no meu Google Drive. Depois examine o código-fonte na mesma pasta ou no repositório que eu informar. Não refaça nem publique nada antes de me apresentar um resumo do estado atual e confirmar comigo a próxima alteração. Quero continuar a partir dessa base.

Se o GitHub estiver conectado no novo chat, informe também **seu usuário do GitHub e o nome do repositório**. Não envie senhas nem tokens.

---

## 2. Objetivo do projeto

Criar e evoluir uma versão própria do sistema **FORTCOM — Controle de Obras**, inicialmente igual ao projeto público de referência.

O sistema é voltado à gestão de obras e reformas, com controle de mão de obra, semanas, finanças, etapas, despesas, diário de obra, fotos, relatórios, backups e funcionamento offline.

### Referências públicas originais

- Aplicativo publicado: https://grantech18-stack.github.io/fortcom/
- Repositório original: https://github.com/grantech18-stack/fortcom
- Branch analisada: `main`
- Commit analisado: `3ca1865d6c4c17bf42b425c1c4982ba61ff14dfa`
- Descrição do commit: merge do PR `#3`, com correções da auditoria e melhorias de PIN, sincronização, fotos, cache e relatórios.

---

## 3. Onde os arquivos estão salvos

### Google Drive

- **Pasta:** `FORTCOM — Controle de Obras`
- **Link:** https://drive.google.com/drive/folders/1jAKtsB7Qo3YHtd7PDMd1KbOfZGotp_OU
- **ID da pasta:** `1jAKtsB7Qo3YHtd7PDMd1KbOfZGotp_OU`
- **ZIP com código e testes:** https://drive.google.com/file/d/1tvIaPIpBjJ_L6XbKpaTR4JtCBl8avu1G/view?usp=drivesdk

O ZIP foi preparado sem `.git`, `node_modules` e arquivos temporários. Este documento de continuidade foi adicionado separadamente à pasta do Drive.

### Estrutura principal

```text
FORTCOM/
├── index.html                 # interface, estilos e lógica principal
├── sw.js                      # service worker e funcionamento offline
├── firebase.json              # configuração de deploy das regras
├── firestore.rules            # regras de segurança do Firestore
├── README.md                  # visão geral e instruções
├── FIREBASE.md                # configuração da autenticação e sincronização
├── AUDITORIA.md               # histórico da auditoria técnica
└── testes/
    ├── package.json
    ├── package-lock.json
    ├── suite.js
    └── .gitignore
```

---

## 4. O que já foi feito

1. O site publicado foi acessado e suas telas/funcionalidades foram examinadas.
2. O repositório público original foi clonado e analisado.
3. Uma prévia local foi executada com servidor HTTP.
4. Foi gerada uma captura real do Dashboard em formato de celular; os valores estavam zerados porque não havia dados cadastrados.
5. A suíte automatizada foi instalada e executada.
6. Resultado da validação: **128 verificações aprovadas e 0 falhas**.
7. Uma cópia limpa do projeto foi enviada ao Google Drive, incluindo código, documentação, configurações, testes e ZIP.
8. **Nenhuma personalização visual ou alteração funcional no código-fonte foi feita até agora.**
9. O GitHub não estava conectado/disponível como integração na conversa anterior. Foram orientadas as opções de Fork ou importação do repositório, mas não se confirmou a criação de uma cópia na conta do usuário.

---

## 5. Tecnologia e funcionamento

- Aplicativo de página única em **HTML, CSS e JavaScript**, sem etapa de build.
- `index.html` concentra a interface e a maior parte da lógica.
- Dados locais no `localStorage`, principalmente sob a chave `obra_control_v4`.
- Aplicativo offline/PWA por meio de `sw.js`.
- Fotos ficam no aparelho e são comprimidas antes do armazenamento.
- Nuvem opcional com **Firebase Authentication + Cloud Firestore**.
- Documento de sincronização usado atualmente: `empresas/fortcom/dados/principal`.
- A sincronização atual possui merge de três vias, revisão (`rev`) e registro de conflitos.
- Há monitoramento do tamanho do payload por causa do limite de 1 MB por documento do Firestore.
- Testes com Node.js e `jsdom`, carregando o `index.html` real.

---

## 6. Funcionalidades existentes

- Dashboard com indicadores e gráficos.
- Cadastro e seleção de múltiplas obras.
- Semanas de obra, presenças, diárias, horas extras e adiantamentos.
- Custos extras da semana.
- Cadastro consolidado de funcionários.
- Controle de valor da obra, recebimentos, gastos, saldo e lucro.
- Orçamento por etapas, realizado e avanço físico.
- Curva S, Curva ABC e comparativos.
- Diário de obra.
- Materiais, despesas, fornecedores, vencimentos e pagamentos.
- Galeria de fotos por obra e semana.
- Relatórios e exportações.
- Backup e restauração em JSON; exportação CSV.
- PIN com hash, troca, código de resgate e limite de tentativas.
- Sincronização opcional entre aparelhos.
- Instalação no celular e uso offline.

---

## 7. Como executar e testar

Depois de baixar e extrair o ZIP:

```bash
cd FORTCOM
python3 -m http.server 8000 --bind 0.0.0.0
```

Abra `http://localhost:8000` no computador que estiver executando o servidor.

Para os testes:

```bash
cd FORTCOM/testes
npm install
npm test
```

Resultado esperado na base atual: **128 verificações, 128 aprovadas**.

---

## 8. Cuidados importantes antes de continuar

1. **O código ainda aponta para o Firebase do projeto original.** Para uma versão independente, criar/configurar um Firebase próprio e substituir as credenciais públicas de configuração, o caminho dos dados, o login autorizado e as regras, conforme necessário.
2. Não usar a nuvem original para uma operação independente nem inserir dados reais antes de decidir a configuração definitiva.
3. Publicar regras restritas do Firestore e testar acesso negado para usuários não autenticados.
4. Não colocar senhas, tokens ou outros segredos no código, no GitHub ou neste documento.
5. As credenciais compartilhadas na conversa anterior não foram gravadas aqui. Recomenda-se trocar senhas que tenham sido expostas em chats.
6. Trocar o PIN de fábrica antes do uso real e guardar o código de resgate em local seguro.
7. Fazer backup antes de migrações, alterações de sincronização ou mudanças nas regras do Firebase.
8. A seção final de `FIREBASE.md` contém observações históricas sobre A3/M5 que parecem desatualizadas: os testes atuais verificam merge de três vias, tratamento de conflitos e monitoramento do limite de 1 MB. Conferir o código e os testes antes de tratar esses itens como pendentes.
9. Não enviar `node_modules`, caches ou arquivos temporários ao repositório.

---

## 9. Próximas decisões com o usuário

Antes de modificar o sistema, confirmar:

1. O projeto continuará com a marca **FORTCOM** ou terá outro nome?
2. Haverá novo logotipo, cores, dados da empresa e identidade visual?
3. A primeira etapa será apenas publicar a cópia ou já personalizar o sistema?
4. O repositório no GitHub será público ou privado?
5. O usuário já concluiu o Fork/importação? Qual é a URL do novo repositório?
6. A nuvem será mantida, substituída por um Firebase próprio ou desativada inicialmente?
7. O sistema continuará exatamente com o visual atual ou haverá redesign?
8. Quais dados de demonstração podem ser usados nas capturas e nos testes?

---

## 10. Sequência recomendada

1. Confirmar a URL do repositório do usuário ou criar a cópia no GitHub.
2. Fazer um novo backup da base antes das alterações.
3. Criar uma branch de trabalho, se o Git estiver disponível.
4. Aplicar primeiro a identidade visual e os dados da empresa, se essa for a prioridade.
5. Configurar o Firebase próprio somente depois de definir como a nuvem será usada.
6. Executar `npm test` antes e depois das alterações.
7. Testar manualmente no celular: PIN, cadastro de obra, semana, funcionário, presença, despesa, backup e restauração.
8. Publicar no GitHub Pages usando branch `main`, pasta `/(root)`.
9. Conferir o endereço `https://USUARIO.github.io/REPOSITORIO/` e o funcionamento offline.
10. Atualizar este documento com o novo repositório, as alterações realizadas e o resultado dos testes.

---

## 11. Regra de trabalho para o próximo chat

- Não presumir que o GitHub está conectado: verificar a integração disponível.
- Não presumir que o Fork foi criado: pedir ou localizar a URL fornecida pelo usuário.
- Ler primeiro os arquivos e apresentar um diagnóstico curto.
- Fazer alterações pequenas e verificáveis.
- Preservar o funcionamento offline e os 128 testes aprovados.
- Não apagar nem sobrescrever dados ou arquivos sem confirmação.
- Não solicitar senha do GitHub, Gmail ou Firebase.
- Ao terminar cada etapa, informar o que mudou, os testes executados e o próximo passo.
