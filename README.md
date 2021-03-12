# JWT no Loopback4
Adicionando o JWT no Loopback4 - Tem um detalhe faltando na documentação e um bug no migrate

### Correção no tutorial
https://loopback.io/doc/en/lb4/Authentication-tutorial.html#3b-add-endpoints-in-usercontroller

Seguindo o Tutorial falta implementar o controller do user

Isso se corrigi pegando o arquivo implementado do exemplo: JWT-ToDO

https://github.com/strongloop/loopback-next/blob/master/examples/todo-jwt/src/controllers/user.controller.ts

### BUG: Tabela não existente

O código a seguir corrigir o mesmo:

```
// TOP
import {UserServiceBindings} from '@loopback/authentication-jwt';

...

await app.boot();  // Já existi

await Promise.all(
  [
    ...app.find(UserServiceBindings.USER_REPOSITORY),
    ...app.find(UserServiceBindings.USER_CREDENTIALS_REPOSITORY)
  ].map(b => app.get(b.key))
);

await app.migrateSchema({existingSchema}); // Já existi
```

Depois disso o JWT está funcionando, qualquer informação adicional, colocarei aqui...

Também já tem ***issues abertas*** sobre o assunto, é questão de tempo ser corrigido também!
