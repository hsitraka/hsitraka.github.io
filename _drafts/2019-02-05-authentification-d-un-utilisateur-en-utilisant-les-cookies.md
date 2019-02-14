---
layout: post
title:  "HapiJS - Authentification d'un utilisateur en utilisant les cookies"
date:   2019-01-24 07:55:49 +0300
categories: HapiJS
---
Cette article illustre l'utilisation des cookies pour créer une session entre le server et le client sur [HapiJS](https://hapijs.com) en utilisant le plugin [hapi-auth-cookie](https://github.com/hapijs/hapi-auth-cookie).


## Principes de fonctionnement

Un cookie une suite d'informations envoyée par un serveur HTTP à un client HTTP, que ce dernier retourne lors de chaque interrogation du même serveur HTTP sous certaines conditions.

![Fonctionnement des cookies](/assets/image/session-cookie.png)

L'utilisateur envoye une requete au serveur pour lui demander de créer une  session en envoyant un nom d'utilisateur et un mot de passe. Le serveur verifie ensuite l'identité de l'utilisateur: si elle est invalide le serveur empeche la création d'une session par contre si l'identité de l'utilisateur a été verifier, le serveur envoye une reponse qui permettra la creation d'un cookie qui stockera l'identifiant de la session.



## Pre-requis
Avant de commencer, il faut dabord installer les paquets necessaire dont `hapi` et `hapi-auth-cookie`:

{% highlight bash %}
$npm install hapi hapi-auth-cookie
{% endhighlight %}

{% highlight javascript %}
// Fichier server.js
'use strict';
// Importer hapi
const Hapi = require('hapi');
// Crée un server
const server = Hapi.Server({
    localhost: 'localhost',
    port: 3000
});
// Configurer le server
const liftOff = async () => {
    await server.register('hapi-auth-cookie');  // Charger le plugin hapi-auth-cookie
    await server.start();  // Démarrer le server
    console.log('server is running...');
};
{% endhighlight %}
