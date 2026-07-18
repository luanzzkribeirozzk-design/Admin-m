# Admin Panel — App Android

Projeto Capacitor pronto para build automatico de APK via GitHub Actions.

## Como usar

1. Crie um repositorio novo no GitHub (pode ser privado).
2. Suba TODOS os arquivos desta pasta para o repositorio, mantendo a estrutura:
   ```
   .github/workflows/build-apk.yml
   www/index.html
   www/manifest.json
   www/icon-192.png
   www/icon-512.png
   package.json
   capacitor.config.json
   ```
3. Va na aba **Actions** do repositorio no GitHub.
4. O workflow "Build APK" roda automaticamente a cada push na branch main/master.
   Se nao rodar sozinho, clique em "Build APK" -> "Run workflow" (botao manual).
5. Quando terminar (leva uns 3-5 minutos), abra a execucao concluida e baixe
   o artefato **admin-panel-apk** — dentro dele esta o `app-debug.apk`.
6. Transfira o `.apk` para o celular Android e instale
   (pode precisar habilitar "Instalar apps de fontes desconhecidas").

## Estrutura

- `www/index.html` — o app inteiro (mesmo codigo/funcoes de antes: login,
  geracao de keys, paginas Gerar/Keys/Conta, Firebase Firestore em tempo real).
- `capacitor.config.json` — configuracao do app nativo (nome, appId, pasta web).
- `.github/workflows/build-apk.yml` — pipeline que instala o Capacitor,
  gera o projeto Android e compila o APK, tudo no servidor do GitHub.

## Importante sobre o APK gerado

- Este workflow gera um **APK de debug** (nao assinado para loja),
  ideal para instalar direto no celular e testar.
- Se no futuro voce quiser publicar na Google Play, e preciso gerar uma
  keystore de assinatura e trocar `assembleDebug` por `assembleRelease`
  no workflow — posso te ajudar com isso quando chegar a hora.
- O `appId` (`com.adminpanel.app`) e o identificador unico do app.
  Pode trocar no `capacitor.config.json` antes do primeiro build se quiser
  outro nome de pacote.

## Nenhuma funcao foi alterada

Login, geracao de keys, calculo de creditos, pausar/ativar, resetar
dispositivo, apagar key, busca, acoes em massa — tudo identico ao
HTML original. So a "casca" mudou: agora roda como app Android nativo
(WebView) em vez de pagina no navegador.
