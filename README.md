# Entre Nos

Site estatico com um unico feed privado para duas pessoas publicarem textos, links e comentarios.

## Estado atual

O `index.html` ja funciona sem configuracao, usando `localStorage`. Nesse modo, os dados ficam apenas no navegador atual.

## O que preciso do Firebase

No console do Firebase, crie um projeto e um app Web. Depois me envie o objeto `firebaseConfig`, parecido com este:

```js
const firebaseConfig = {
  apiKey: "...",
  authDomain: "...",
  projectId: "...",
  storageBucket: "...",
  messagingSenderId: "...",
  appId: "..."
};
```

Tambem me envie uma chave privada para o link do site, por exemplo:

```text
minha-chave-longa-e-dificil-de-adivinhar
```

Com isso eu deixo o `index.html` pronto para sincronizar em tempo real e bloquear acesso sem `?key=sua-chave`.

## Firestore

Ative o Firestore Database no Firebase. Para um primeiro teste simples, estas regras funcionam:

```text
rules_version = '2';

service cloud.firestore {
  match /databases/{database}/documents {
    match /spaces/entre-nos/{collection}/{document} {
      allow read, write: if true;
    }
  }
}
```

Esse modelo e simples, mas nao e seguranca forte: quem tiver o link e a configuracao publica do Firebase pode ler/escrever. Para privacidade real, o proximo passo seria login ou backend.
