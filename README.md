# Gestão Time Trairagem 2026

App de gestão do time de futebol Trairagem: jogadores, resultados, próximos jogos, estatísticas e financeiro (mensalidades, caixa mensal, despesas).

Arquivo único (`index.html`), sem build — HTML + CSS + JS puro, com sincronização em tempo real via Firebase.

## Links

- App publicado (GitHub Pages): https://joaosilva09.github.io/gestao-time-trairagem-2026/
- Domínio próprio (Hostinger): em configuração — `trairagemfc.app.br`
- Console do Firebase: https://console.firebase.google.com/project/trairagem-2026

## Como funciona o acesso

- **Visualizador**: qualquer pessoa do time entra com um clique ("Entrar como visualizador"), sem senha. Só pode ver os dados, nenhum campo é editável.
- **Administrador**: login com e-mail/senha (conta criada no Firebase Authentication). Só o admin pode editar jogadores, resultados, financeiro etc.
- A permissão de escrita é validada nas regras do Firestore (não só na interface) — visualizadores não conseguem alterar dados mesmo tentando pelo console do navegador.

Credenciais de admin: gerenciadas no Firebase Console → Authentication → Usuários (não estão neste repositório por segurança).

## Arquitetura

- **Frontend**: `index.html` único, sem dependências de build.
- **Banco de dados**: Cloud Firestore (`teams/trairagem-2026`), região `southamerica-east1`. O documento inteiro guarda o estado do app em JSON.
- **Autenticação**: Firebase Auth — Anônimo (visualizador) e E-mail/Senha (admin).
- **Sincronização**: mudanças salvam no Firestore com debounce (~700ms) e chegam em tempo real para todos os outros clientes conectados (`onSnapshot`).
- Também mantém uma cópia em `localStorage` do navegador como cache local.

## Publicar mudanças

1. Editar `index.html`.
2. `git add index.html && git commit -m "..."` e `git push`.
3. O GitHub Pages atualiza sozinho em ~1 minuto.
4. Para a Hostinger: subir o `index.html` atualizado manualmente pelo Gerenciador de Arquivos (hPanel), substituindo o antigo.

## Backup dos dados

Botão "Exportar backup" no topo do app baixa um `.json` com todos os dados atuais — use de vez em quando para guardar uma cópia local.
