# A test project

This is a test project to experiment the creation of a RESTful API using Symfony skeleton as a basis to ease everything.

## Why 

The idea is to learn how an RESTful API works behind the scene. As a front-end developer, I sometimes had to build some small micro-services to interact with a database, but often times I ended writing a functionnal but *whacky* solution which works but is neither scalable neither clean.

Also, as a *modern* front-end developer, most of the communications with back-end services are done via REST APIs, and even though using one is pretty straightforward, I sometimes found myself wondering `how does this shit works under the hood, why does it work that way, and am I using it as it was intended to ?` 

This projects was made to fully understand how to secure client-server communications with **JWT authentification** and expose a REST API which interacts with a simple database. I hope to get some experience in that matter and it will for sure help me when I will need to build a backend for my clients.

## Why public

I will try to keep here a list of resources that I found helpful while doing my research, and list the issues I hav encountered and how I tackled them. Maybe you will find here some solutions to problems you encountered yourself in the same process, maybe not. `Who knows`

# Resources

## Tutorials 

* [Youtube tutorial: Symfony REST, **OverSeas Media**](https://www.youtube.com/watch?v=e4-Xgi1vVnU&list=PLqhuffi3fiMN_jVxqlIAILEp4avoBH4wc): a great series of video going through the whole process of setting up a REST API using Symfony

## Tools 

* [FOSRestBundle](https://symfony.com/doc/current/bundles/FOSRestBundle/index.html): A bundle designed to help with the creation of a REST API using Symfony

## Issues encountered

### Couldn't generate a component using the php bin/console

In the tutorial I was following, a Controller was created using the CLI, however when looking on google for the command I found that I has to run the following:

`$ php bin/console generate:controller`

However, this particular command returned the following error:

```
There are no commands defined in the "generate" namespace.
You may be looking for a command provided by the "SensioGeneratorBundle" which is currently not installed. Try running "composer require sensio/generator-bundle".
```

So I ran:

`$ composer require sensio/generator-bundle`

Which ran into another error:

```
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - sensio/generator-bundle v3.1.7 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.6 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.5 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.4 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.3 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.2 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle v3.1.1 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - sensio/generator-bundle 3.1.0 requires symfony/framework-bundle ~2.7|~3.0 -> no matching package found.
    - Installation request for sensio/generator-bundle ^3.1 -> satisfiable by sensio/generator-bundle[3.1.0, v3.1.1, v3.1.2, v3.1.3, v3.1.4, v3.1.5, v3.1.6, v3.1.7].
```

Long story short, the issue comes from the fact that [the link I ended up on the first place](https://symfony.com/doc/current/bundles/SensioGeneratorBundle/commands/generate_controller.html) was refering to an older package used to generate Controllers, which isn't supported anymore and couldn't work with my version of symfony (5.1). The new package is `symfony/maker-bundle`, and we can create a Controller using the following command:

`$ php bin/console make:controller --no-template`