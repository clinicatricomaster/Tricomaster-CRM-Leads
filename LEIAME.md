# TricoMaster CRM — versão Firebase

Arquivos:
- `index.html`: o app inteiro (HTML + CSS + JS, sem build)
- `firestore.rules`: regras de segurança do Firestore

## 1. Projeto no Firebase
1. No Console do Firebase, use um projeto existente ou crie um novo.
2. **Authentication → Método de login →** ative **E-mail/senha**.
3. **Firestore Database →** crie o banco (de preferência na região `southamerica-east1`, em São Paulo).
4. **Firestore → Regras →** cole o conteúdo de `firestore.rules` e publique.

## 2. Configurar o app
No Console, abra **Configurações do projeto → Seus apps → App da Web (</>)** e copie o objeto `firebaseConfig`.
Abra o `index.html`, procure `firebaseConfig` e cole os valores no lugar de `COLE_AQUI`.

## 3. Criar os usuários
Para cada pessoa da equipe:
1. **Authentication → Usuários → Adicionar usuário** (com e-mail e senha).
2. Copie o **UID** do usuário.
3. **Firestore →** crie a coleção `usuarios` com um documento cujo **ID é o UID**, com campos como `nome` e `email`.

Sem esse documento, a pessoa consegue fazer login, mas não vê nenhum lead. O app mostra o UID na tela, para facilitar.
Para tirar o acesso de alguém, apague o documento em `usuarios` ou desative o usuário no Authentication.

## 4. Publicar
O app funciona em qualquer hospedagem de arquivo estático: GitHub Pages, Firebase Hosting, KingHost ou Hostinger.
Depois de publicar, adicione o domínio em **Authentication → Configurações → Domínios autorizados**.

## 5. Levar os leads do CRM do claude.ai
1. No CRM do claude.ai, vá em **Configurações → Backup completo → Exportar backup (.json)**.
2. Na versão Firebase, faça login e vá em **Configurações → Restaurar backup**, escolhendo o arquivo.

Os status, valores, histórico, dados do RD e configurações vêm junto.

## Como os dados ficam no Firestore
- `leads/{id}`: um documento por lead.
- `config/listas`: origens, campanhas, motivos, frases, unidades e responsáveis.
- `usuarios/{uid}`: lista de usuários liberados.

## Custos (plano gratuito Spark)
- O app usa um cache local: ao reabrir, lê do servidor só o que mudou.
- Com cerca de 1.000 leads e poucos usuários, o uso fica bem abaixo do limite gratuito (50 mil leituras e 20 mil gravações por dia).
- A importação grava em lotes de 400.
- O botão **Sair** apaga a cópia local dos dados daquele computador.
