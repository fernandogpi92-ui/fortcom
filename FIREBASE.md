# Firebase — projeto `fortcom-obras`

Atualizado em 06/11/2026.

## Estado da configuração

- Projeto Firebase próprio: `fortcom-obras`.
- App Web `Fortcom Web` registrado; a configuração pública do app já está em `index.html`.
- Login proprietário escolhido: `fernandogpi92@gmail.com` (o mesmo e-mail usado na conta Google do Console). A senha do Firebase Auth não fica no repositório.
- **Ainda pendente no Console:** habilitar o provedor E-mail/senha, criar o usuário, criar o Firestore e publicar `firestore.rules`.
- Firebase Hosting ainda não foi implantado. O registro do app Web não publica o site automaticamente.

## O que o app sincroniza hoje

O app é offline-first. Os dados são salvos no `localStorage` do navegador e, após autenticação, sincronizados com o Firestore no caminho:

```text
empresas/fortcom/dados/principal
```

O estado inteiro da obra vai atualmente em um único documento (`payload`). O Firestore limita cada documento a 1 MiB; o app monitora o tamanho e interrompe a sincronização ao atingir o limite. **Fotos continuam no aparelho**: esta versão ainda não usa Firebase Storage. Para sincronizá-las, será necessária uma etapa posterior de implementação e avaliação das cotas/custos do Storage.

## Configuração no Firebase Console

### 1. Habilitar autenticação por e-mail e senha

1. Abra **Authentication → Provedores de login**.
2. Ative **E-mail/senha**; deixe o login por link de e-mail desativado.
3. Em **Usuários**, crie o usuário `fernandogpi92@gmail.com` e defina uma senha própria para o Firebase.

Não use nem compartilhe a senha da conta Google. O login do app é uma conta do Firebase Auth.

### 2. Criar o Firestore e publicar as regras

1. Abra **Bancos de dados e armazenamento → Firestore Database** e crie o banco em **modo de produção** (não use regras abertas de teste).
2. Na aba **Regras**, publique o conteúdo de [`firestore.rules`](firestore.rules).
3. As regras permitem leitura e gravação apenas da conta acima, no documento `empresas/fortcom/dados/principal`; todo o restante é negado.

Publicar `firestore.rules` no repositório **não** publica as regras no Firebase. A publicação precisa ser feita no Console ou pela CLI.

### 3. Publicar o app

O app Web foi registrado com Firebase Hosting, mas ainda não foi implantado. `firebase.json` atualmente aponta apenas para as regras do Firestore. A configuração de Hosting será preparada separadamente, publicando somente os arquivos do app — não os documentos internos do repositório.

Depois da implantação, se o login reclamar de domínio não autorizado, adicione o domínio `*.web.app` do site em **Authentication → Configurações → Domínios autorizados**.

## Publicação opcional das regras pela CLI

Depois de instalar e autenticar a Firebase CLI no computador:

```bash
firebase login
firebase deploy --only firestore:rules --project fortcom-obras
```

## Antes de usar dados reais

- Confirme que o usuário proprietário existe em Authentication e que as regras acima foram publicadas.
- Faça um backup `.json` pelo app antes de migrar dados.
- Dados do `localStorage` de outro domínio/aparelho não migram automaticamente para o novo site; use backup/restauração ou a sincronização autenticada.
- A chave de configuração Web (`apiKey`) é pública por design; a proteção dos dados depende da autenticação e das regras do Firestore.
